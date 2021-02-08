---


---

<h1 id="nat--acl-with-aws---tutorial">
# NAT &amp; ACL with AWS - Tutorial</h1>
<h1 id="accesso-ad-aws">

# Accesso ad AWS</h1>
<p>
Per questo tutorial, non è possibile usare l’'account di classe perché alcune funzioni sono limitate, bisognerà usare il proprio free starter account.</p>
<p>

Accedere alla console di AWS <em>*del proprio starter account</em>* (non quello della classe), potete farlo accedendo ad AWS educate con le solite credenziali e quindi selezionando in alto a destra su AWS Account e quindi su Starter Account.</p>
<h1 id="creazione-nat-gateway">  

# Creazione NAT Gateway</h1>
<p>  
Nella console, selezionate il Servizio VPC.</p>
<p>  
  
Nel menu a destra, selezionate NAT gateway e createne uno.</p>
<p>  
 
Associate un indirizzo IP elastico. Se non ne avete nessuno disponibile, fatevene creare uno sul momento.</p>
<p>

Fine! Il NAT Gateway è pronto.</p>
<h1 id="impostazione-acl">

# Impostazione ACL</h1>
<p>
Immaginiamo che la nostra subnet ospiti un sito web, che vogliamo far visitare anche dall’'esterno. Modifichiamo le ACL di conseguenza.<br>  
Nel menu a destra, selezionate Netwoark ACLs e modificate le regole come specificato di seguito.</p>
<h2 id="regole-inbound">

## Regole inbound</h2>
<p>
Filtra i pacchetti in ingresso alla nostra rete. Impostiamole in modo che:</p>
<ul>
<li> 
- sia permesso il traffico HTTP e HTTPS da chiunque</li>
<li>  
- sia permesso il traffico SSH da chiunque; nota: quando andremo in produzione dovremo ricordarci di limitare l’'accesso solo ad un numero limitato di indirizzi IP affidabili</li>
<li> 
- sia permesso il traffico di ritorno delle richieste della nostra subnet verso il mondo esterno; dobbiamo accettare il protocollo TCP da qualsiasi sorgente con il range di porte 32768-65535</li>
<li>  
- sia permesso il ping</li>
<li>
- tutte le altre richieste devono essere negate (ricordatevi quindi di cancellare la regola che accetta tutto).</li>
</ul>
<h2 id="regole-outbound">

## Regole outbound</h2>
<p>
Filtra i pacchetti in uscita alla nostra rete. Impostiamole in modo che:</p>
<ul>
<li> 
- sia permesso il traffico HTTP e HTTPS verso chiunque (utile se dobbiamo fare richieste ad altri server</li>
<li>
- sia permesso il traffico delle richieste originate dall’'esterno verso il nostro server; dobbiamo accettare il protocollo TCP verso qualsiasi destinazione con il range di porte 32768-65535</li>
<li>  
- sia permesso il ping</li>
<li>
- tutte le altre richieste devono essere negate (ricordatevi quindi di cancellare la regola che accetta tutto).</li>
</ul>
<h1 id="verifica-della-configurazione">

# Verifica della configurazione</h1>
<p>

Creazione di due istanze EC2.</p>
<p>

Una delle due sarà bastian host con indirizzo IP pubblico.</p>
<p>

Collegarsi via SSH al bastian host</p>
<p>

Dal bastian host, collegarsi via SSH al secondo host</p>
<p>

Provare a fare il PING dal bastian host a google.</p>
<p>

Vedere il traffico che passa attraverso il NAT Gateway.</p>
<blockquote>
<p>


> Written with <a href="[StackEdit](https://stackedit.io/">StackEdit</a>.</p>
</blockquote>
).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzY1MzE4OTQyXX0=
-->