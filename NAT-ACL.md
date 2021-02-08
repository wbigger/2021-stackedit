
  
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

## Creazione delle macchine
Andiamo sul nostro account AWS e nella 
## Accesso alle macchine EC2

Prima dAbbiamo un
Creazione di due istanze EC2.

Una delle due sarà bastian host con indirizzo IP pubblico.

Collegarsi via SSH al bastian host

Dal bastian host, collegarsi via SSH al secondo host

Provare a fare il PING dal bastian host a google.

Vedere il traffico che passa attraverso il NAT Gateway.


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg2NTkzODUzMV19
-->
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzM4NDcwNjcsNzY1MzE4OTQyXX0=
-->