
  
# NAT & ACL with AWS - Tutorial

# Accesso ad AWS
Per questo tutorial, non è possibile usare l'account di classe perché alcune funzioni sono limitate, bisognerà usare il proprio free starter account.

Accedere alla console di AWS *del proprio starter account* (non quello della classe), potete farlo accedendo ad AWS educate con le solite credenziali e quindi selezionando in alto a destra su AWS Account e quindi su Starter Account.  

# Creazione NAT Gateway  
Nella console, selezionate il Servizio VPC.  
  
Nel menu a destra, selezionate NAT gateway e createne uno.  
 
Associate un indirizzo IP elastico. Se non ne avete nessuno disponibile, fatevene creare uno sul momento.

Fine! Il NAT Gateway è pronto.

# Impostazione ACL
Immaginiamo che la nostra subnet ospiti un sito web, che vogliamo far visitare anche dall'esterno. Modifichiamo le ACL di conseguenza.  
Nel menu a destra, selezionate Netwoark ACLs e modificate le regole come specificato di seguito.

## Regole inbound
Filtra i pacchetti in ingresso alla nostra rete. Impostiamole in modo che: 
- sia permesso il traffico HTTP e HTTPS da chiunque  
- sia permesso il traffico SSH da chiunque; nota: quando andremo in produzione dovremo ricordarci di limitare l'accesso solo ad un numero limitato di indirizzi IP affidabili 
- sia permesso il traffico di ritorno delle richieste della nostra subnet verso il mondo esterno; dobbiamo accettare il protocollo TCP da qualsiasi sorgente con il range di porte 32768-65535  
- sia permesso il ping
- tutte le altre richieste devono essere negate (ricordatevi quindi di cancellare la regola che accetta tutto).

## Regole outbound
Filtra i pacchetti in uscita alla nostra rete. Impostiamole in modo che: 
- sia permesso il traffico HTTP e HTTPS verso chiunque (utile se dobbiamo fare richieste ad altri server
- sia permesso il traffico delle richieste originate dall'esterno verso il nostro server; dobbiamo accettare il protocollo TCP verso qualsiasi destinazione con il range di porte 32768-65535  
- sia permesso il ping
- tutte le altre richieste devono essere negate (ricordatevi quindi di cancellare la regola che accetta tutto).

# Verifica della configurazione

Per verificare la configurazione, dobbiamo creare delle macchine virtuali su EC2.

L'obiettivo è dimostrare che è possibile accedere ad internet dall'interno della nostra rete anche se una macchina _non_ ha un indirizzo IP pubblico, ma solo quello privato.

## Nota sull'accesso alle macchine dall'esterno
Per poter testare la configurazione, dobbiamo entrare in SSH all'interno delle nostre macchine dal nostro computer di casa o di scuola. Questo non è banale con il NAT perché le macchine interne hanno solo indirizzi IP privati e non sono quindi raggiungibili dall'esterno. Ricordiamo infatti che il NAT risolve il problema per una LAN di accedere all'esterno, ma _non_ il problema di accedere dall'esterno ai computer della nostra LAN.

Per risolvere questa situazione ci sono diverse strategie:
- **port forwarding**: diciamo al firewall che se proviamo ad accedere sulla porta 22, la richiesta deve essere reindirizzata ad una specifica macchina interna alla LAN; questa strategia non è semplice da implementare su AWS nella nostra configurazione
- **bastion host** (computer bastione): una macchina con indirizzo IP pubblico all'interno di una nostra subnet pubblica che  accessibile dall'esterno e che ci fa da tramite per il resto della nostra rete interna.

Useremo questa seconda strategia, quindi andremo a creare due macchine: una la chiamiamo PC0-bastion e l'altra PC1.

## Creazione delle macchine
Andiamo sul nostro account AWS e tra i servizi scegliamo EC2.

Useremo la _subnet 0_ come sottorete pubblica, e la _subnet 1_ come sottorete privata.

### PC0-bastion

Andiamo a sinistra su _Istanze_, quindi in alto a destra _Lancia instanze_. Lasciamo _Amazon Linux 2 AMI_ e premiamo su _Seleziona_. Lasciamo t2.micro e ancora _Next: Configura dettagli istanza_. 

Nella schermata di configurazione, selezioniamo la VPC di default (o quella che volete) e la _Subnet 0_. Nella voce _Auto-assign Public IP_ mettiamo _Enable_, perché questa macchina deve essere accessibile anche dall'esterno. Premiamo ora su _Next_ diverse volte finché non arriviamo a _Security groups_.

Qui mettiamo le seguenti regole:
- accesso via SSH
- ping (All ICMP - IPv4).


### PC1
Lanciamo una nuova istanza sempre Amazon Linux 2 AMI di tipo t2.micro.

Nella schermata di configurazione, selezioniamo la stessa VPC ma stavolta selezionamo la subnet 0. Nella voce _Auto-assign Public IP_ stavolta mettiamo _Disable_, perché questa macchina non deve essere accessibile anche dall'esterno. Nel Security Group, mettiamo le stesse regole del PC0-bastion (SSH e pint), andiamo su Review and Launch e lanciamo la macchina.

### Configurazione del routing
Il diagramma di rete che andremo ad usare è qualcosa di simile al seguente, preso dalla [documentazione ufficiale](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html).
![Diagramma di rete NAT](https://github.com/wbigger/2021-stackedit/blob/main/nat-gateway-diagram.png?raw=true)

Dobbiamo fare in modo che:
- la tabella di routing della nostra sottorete pubblica, nel nostro caso _subnet 0_, come rotta di default abbia l'internet gateway
- la tabella di routing della nostra sottorete privata, nel nostro caso _subnet 1_, abbiamo come rotta di default il nat gateway.

Andiamo quindi su AWS, nei servizi selezioniamo *VPC*-> *Route Tables* -> *Route 0* (se non esiste, createla), nei dettagli in basso controllate che sia associata alla _subnet 0_, quindi andate sulla tab _Routes_ e quindi _Edit routes_. Nella tabella ci devono essere due rotte: la local (lasciatela così) e _0.0.0.0/0_ che deve puntare all'internet gateway (qualcosa che comincia con _igw_, se non avete un internet gateway, createlo nella voce dedicata del menù a sinistra).

Ripetiamo la stessa operazione con la rotta _Route 1_, anche qui se non esiste createla. Lasciate la rotta local così com'é e aggiungete la rotta _0.0.0.0/0_ con destinazione il NAT Gateway (qualcosa che comincia con _nat_).

## Esecuzione del test

Per comodità, nella lista delle istanze rinominiamo le macchine come PC0-bastion e PC1.

Seleziamo PC1 e dai dettagli in basso ci segniamo il suo indirizzo IPv4 privato, nel mio caso è `172.30.0.213`.

Ora dobbiamo accedere a PC0-bastion che ci fa da ponte per il PC1. Ma per collegarci via ssh da PC0-bastion a PC1 dovremmo avere la nostra chiave su PC0-bastion, che per definizione è poco sicuro. Come facciamo a fare da ponte senza copiare la chiave?

Ci viene in aiuto una funzionalità di SSH che si chiama _agent forwarding_. Con questo metodo, possiamo collegarci ad una macchina e poi a seguire ad un altra, usando 

Nota: la prima volta scriviamo la chiave per connetterci in scp con l'opzione `-i`, la seconda volta è per specificare il file che stiamo copiando.

Ora connettiamoci via SSH a PC0-bastion, con qualcosa del tipo:
```shell
ssh -i "miachiave.pem" ec2-user@18.212.212.224
```

Dall'interno di questa macchina, connettiamoci a PC1:
```shell
# sono dentro PC0-bastion
ssh -i "miachiave.pem" ec2-user@172.30.0.213
```

Infine, da dentro PC1 pingo il server google:
```shell
ping www.google.com
```

Ci siamo, funziona!

### Verifica del traffico sul NAT Gateway
Se tornate su VPC->NAT Gateway, potete vedere il traffico che passa attraverso il gateway.


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg2NTkzODUzMV19
-->
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MjUzMjM5NTAsLTIwMDM1Njg4MzgsLT
E0MDMyMDkxNDcsLTc2Njc1NzY5NiwtMTM1MDQ0MzQxNiwxOTcw
OTk3OTcwLC0xOTExNDk4ODczLDUzMzU2MTA1NCw3NjUzMTg5ND
JdfQ==
-->