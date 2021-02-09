
  
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

### PC0-bastion

Andiamo a sinistra su _Istanze_, quindi in alto a destra _Lancia instanze_. Lasciamo _Amazon Linux 2 AMI_ e premiamo su _Seleziona_. Lasciamo t2.micro e ancora _Next: Configura dettagli istanza_. 

Nella schermata di configurazione, selezioniamo la VPC di default (o quella che volete) e la _Subnet 0_. Nella voce _Auto-assign Public IP_ mettiamo _Enable_, perché questa macchina deve essere accessibile anche dall'esterno. Premiamo ora su _Next_ diverse volte finché non arriviamo a _Security groups_.

Qui mettiamo delle regole che permettono l'accesso via SSH e abilitiamo il ping (All ICMP - IPv4).


### PC1
Lanciamo una nuova istanza sempre Amazon Linux 2 AMI di tipo t2.micro.

Nella schermata di configurazione, selezioniamo la stessa VPC e la stessa subnet 0. Nella voce _Auto-assign Public IP_ stavolta mettiamo _Disable_, perché questa macchina non deve essere accessibile anche dall'esterno. Assicuriamoci che il Secuirty Group sia lo stesso di PC0-bastion (con le stesse regole), andiamo su Review and Launch e lanciamo la macchina.

## Esecuzione del test

Per comodità, nella lista delle istanze rinominiamo le macchine come PC0-bastion e PC1.

Seleziamo PC1 e dai dettagli in basso ci segniamo il suo indirizzo IPv4 privato, nel mio caso è `172.30.0.213`.

Ora dobbiamo copiare la nostra chiave privata nel PC0-bastion per permettergli di connettersi alle altre macchine. Selezioniamo PC0-bastion e annotiamo il suo indirizzo IP pubblico, nel mio caso `18.212.212.224`. Dal nostro computer di casa possiamo copiare la chiave con qualcosa del tipo:

```shell
scp -i miachiave.pem ./miachiave.pem ec2-user@18.212.212.224:
```

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
eyJoaXN0b3J5IjpbLTQyMzM0NzY2OCwtNzY2NzU3Njk2LC0xMz
UwNDQzNDE2LDE5NzA5OTc5NzAsLTE5MTE0OTg4NzMsNTMzNTYx
MDU0LDc2NTMxODk0Ml19
-->