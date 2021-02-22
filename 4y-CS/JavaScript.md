
# JavaScript

La pagina fin qui creata è _statica_, ovvero i dati degli eventi sono scritti in maniera fissa, non modificabile, all'interno del file HTML. Chiaramente non è quello che vogliamo, perché il nostro obiettivo è che ogni volta che l'utente apre la pagina, gli mostri gli eventi aggiornati in quel momento: vogliamo una pagina _dinamica_. Per fare questo ci serve l'ultimo componente di HTML5: JavaScript.

## Un po' di storia

<p class="img-container">
<img class="right_side" title="Bernard Eich." alt="Bernard Eich" src="https://wbigger.github.io/book-html5/html5/assets/js-eich.jpg">
</p>

JavaScript è nato all'interno della <a href="https://it.wikipedia.org/wiki/Netscape_Navigator">Netscape</a>, la società americana che sviluppò nel 1993 il primo web browser grafico di larga diffusione (ricordiamo che il web è nato nel 1989 in Europa). Nel 1995 cercavano una tecnologia per rendere dinamiche le pagine web e diedero l'incarico al neo-assunto <a href="https://en.wikipedia.org/wiki/Brendan_Eich">Bernard Eich</a> di creare un linguaggio di programmazione per competere con i rivali (Java e Microsoft). Gli diedero 10 giorni di tempo, nel maggio 1995.

Eich riuscì nell'impresa e creò il linguaggio JavaScript, definito nel suo [annuncio ufficiale](https://web.archive.org/web/20070916144913/http://wp.netscape.com/newsref/pr/newsrelease67.html) come "open, cross-platform object scripting language" che avrebbe dovuto "complementare il linguaggio Java".

[Sembra](https://www.crockford.com/javascript/javascript.html) che il prefisso Java sia stato scelto intenzionalmente per creare confusione e per scherzo. In ogni caso la Sun Microsystem, che deteneva i diritti di Java a quel tempo, non protestò, e cosi è rimasto questo nome.

<p class="img-container">
<img class="left_side" title="JavaScript logo" alt="JavaScript logo" src="https://wbigger.github.io/book-html5/html5/assets/js-logo.png">

</p>

Da allora il linguaggio è cresciuto in funzionalità e diffusione, fino ad arrivare nel 2019 ad essere tra i 10 linguaggi più usati al mondo, in continua crescita. La sua vitalità è testimoniata dagli standard in continuo aggiornamento. Le funzionalità di JavaScript sono infatti definite e standardizzate dalla [ECMA](https://www.ecma-international.org/) (European Computer Manufacturers Association), con sede a Ginevra. L'ultima versione dello standard JavaScript si chiama ES2017 (anche detto ES8, giusto per creare un po' più di confusione).


La nascita un po' casuale di questo linguaggio è uno dei motivi per cui molte cose in JavaScript non hanno una ragione particolare, almeno nella versione classica (fino allo standard ES5 del 2009).

Inoltre, JavaScript lascia molta libertà agli sviluppatori di decidere il loro stile di programmazione. Questo fa sì che, senza delle linee guida condivise tra sviluppatori, il codice scritto da persone diverse finisce per essere incompatibile o incomprensibile. Per evitare il problema, è necessario scegliere una linea guida comune. Ne esistono molte, per semplicità possiamo usare quella ufficiale di [w3school](https://www.w3schools.com/html/html5_syntax.asp).

> Per una guida più completa potete consultare [questa](https://crockford.com/javascript/code.html) pagina con le linee guida di Douglas Crockford.



## Agganciare HTML e JS
Nel nostro editor preferito, creiamo un file `index.html`. Se usate VSCode, potete generare lo scheletro della pagina premendo `!` quandoil file è ancora vuoto.

Creando un file nella stessa cartella dell'`index.html` e lo chiamiamo `script.js`. Per fare una prova, per ora mettiamo solo la visualizzazione di un pop-up, che in JavaScript si ottiene con la funzione `alert()`.

```js
alert("JS test");
```

Se proviamo ora ad aggiornare la nostra pagina, non succede niente. Perché?

Come abbiamo detto, **tutto parte sempre dall'HTML**. Il nostro browser comincia a leggere il file HTML che abbiamo indicato con l'URL nella barra di navigazione e riga dopo riga interpreta quello che c'è scritto. Dobbiamo quindi mettere nel nostro `index.html` l'istruzione per dirgli di andare a leggere il file.

Il tag necessario per questa operazione è **`<script>`**, a cui bisogna specificare come attributo il nome del file che vogliamo caricare. Ecco il codice che ci serve:

```html
<script src="script.js"></script>
```

Dove mettiamo questa riga di codice? Nei testi a volte viene suggerito di mettere il tag `<script>` all'interno del tag `<head>`, ma noi non seguiremo questo suggerimento. Il motivo è di efficienza: di default il browser eseguirà tutto il codice dentro il nostro script e **solo dopo** continuerà ad interpretare la pagina, con la conseguenza l'utente potrebbe avvertire una fastidiosa sensazione di lentezza.

> Come sempre in VSCode, digitando script:src si avvia l'auto-completamento.


Avviando la pagina otteniamo la seguente cosa.
<p align="center">
<img class="w80p" title="js-alert" src="https://wbigger.github.io/book-html5/html5/assets/js-alert.png">
</p>

Bene, il file JavaScript è collegato correttamente! 🥳

Prima di andare avanti, vogliamo semplificarci un po' le cose usando una libreria molto diffusa che permette di ridurre drasticamente il codice da scrivere per eseguire operazioni comuni: jQuery.

> Un'altra libreria molto usata è [Lodash](https://lodash.com/), che semplifica la manipolazione di array, stringhe e oggetti.

## Importare jQuery
[jQuery](https://jquery.com/) (pronuncia _jeiquiri_) è una delle librerie più diffuse per JavaScript, perché permette di semplificare e velocizzare operazioni che altrimenti richiederebbero un bel po' di linee di codice. Per scaricare l'ultima versione, andate sul sito ufficiale, sezione Download, e selezionate la versione "Download the compressed, production jQuery". Se volete scaricare il file, vi conviene premere con il tasto destro sul link e selezionare "Salva destinazione con nome..." o l'equivalente nel vostro browser. 

Come al solito, salvate il file nella stessa cartella dove si trova il file html.

> Se usate repl.it, potete anche cliccare sulla sinistra nella gestione dei packages, cercare JQuery e premere sul + per aggiungerlo al progetto.

<p align="center">
<img class="w80p" title="js-jquery" src="https://wbigger.github.io/book-html5/html5/assets/js-jquery.png">
</p>

> Attenzione: la semplificazione offerta da jQuery non è gratis. Questa libreria è piuttosto pesante ed il browser ci metterà un po' di tempo a caricarla, con il rischio di inficiare l'esperienza utente. Quando diventerete sviluppatori front-end professionisti, dovrete fare attenzione anche a queste cose. Il codice JavaScript "puro", senza l'uso di nessuna libreria, è anche detto _VanillaJS_; [qui](http://vanilla-js.com/) trovate un sito scherzoso sull'argomento.

Colleghiamo il file nel nostro progetto, mettendo il tag script _prima_ dell'inclusione del nostro file JavaScript. Questo è fondamentale perché, come abbiamo detto, il browser interpreta le linee in ordine, quindi è necessario prima importare jQuery e dopo il nostro codice che dipende da questa libreria.

```html
<script src="jquery-3.5.1.min.js"></script>
<script src="script.js"></script>
```

È interessante notare come non sia possibile importare una dipendenza direttamente all'interno del file JavaScript, ma bisogna passare per il file HTML.

> Per risolvere questo problema, sono nati vari framework più o meno complessi che permettono di gestire le dipendenze in maniera efficente ed efficace. Chi è interessato, può ad esempio studiarsi [Webpack](https://webpack.js.org/).

## Primi passi con jQuery
Per cominciare ad usare jQuery, dobbiamo inizializzare la libreria. Andiamo sul nostro file JavaScript e aggiungiamo il seguente snippet di codice.

```js
var init = function() {
  alert("JS test with Jquery");
}

$(document).ready(init);
```

Vediamo in dettaglio cosa abbiamo fatto. Partiamo dall'ultima riga.
```js
$(document).ready(init);
```

Il simbolo `$` è il nome della variabile oggetto messa a disposizione dalla libreria jQuery. In JavaScript infatti, il dollaro è un carattere valido per l'inizio di una nome di una variabile o funzione.

> jQuery mette a disposizione solo la variabile `$`. Pubblicare una sola variabile è una cosa molto comune in JavaScript, come vedremo.

La variabile **`document`** è invece messa a disposizione dal browser e contiene tutte le informazioni che riguarda la pagina html e i relativi fogli di stile CSS. È il nostro punto di contatto tra l'html e gli script JavaScript.

L'espressione `$(document)` serve a _inizializzare_ la libreria jQuery con il documento corrente. In questo modo inoltre jQuery prende il controllo del documento e noi non andremo _mai più_ ad usare la variabile `document` direttamente, ma passeremo sempre attraverso l'oggetto `$()`.

Immediatamente dopo l'inizializzazione viene chiamato il metodo `.ready()`, che richiede come parametro _una funzione_. Passare come parametri funzioni è una cosa estremamente comune in JavaScript e anche noi la useremo estensivamente. Il metodo `ready` invocherà la funzione passatagli come parametro, nel nostro caso `init`, quando il caricamento della pagina sarà completo e quindi saremo pronti per il processamento del documento.

Vediamo ora come abbiamo dichiarato la funzione `init`.

```js
var init = function() {
  alert("JS test with Jquery");
}
```

Facciamo particolare attenzione a questa sintassi. Abbiamo dichiarato la variabile `init` ed abbiamo usato l'operatore di assegnazione (il simbolo `=`) per assegnarli come valore una funzione. In questo modo abbiamo di fatto creato una variabile che può essere invocata come una funzione (ovvero con le parentesi tonde, `init()`).

> La funzione dichiarata in questo modo _non_ ha un nome suo, infatti non c'è nessun identificativo fra la keyword `function` e le parentesi tonde che seguono. Questo tipo di funzioni si chiamano _anonime_, in inglese _anonymous-functions_. Chi vuole approfondire può leggere [questo articolo](http://helephant.com/2008/08/23/javascript-anonymous-functions/).

Se ora ricarichiamo la pagina, otteniamo un comportamento molto simile al procedente.

<p align="center">
<img class="w80p" title="js-alert" src="https://wbigger.github.io/book-html5/html5/assets/js-alert.png">
</p>

## Scope di funzione
Prima di andare avanti, è bene impostare correttamente il file JavaScript. Questo linguaggio infatti lascia moltissima libertà ai programmatori nell'organizzazione del codice, e questa è una buona cosa perché è possibile creare librerie e framework molto potenti, ma senza un po' di disciplina si finisce con lo scrivere del codice che è completamente non mantenibile e soggetto ad infiniti tipi di bug. Rimandiamo al link all'inizio di questa pagina per una style-guide.

> Fate particolare attenzione quando copiate-incollate codice da Internet. Assicuratevi che sia scritto bene e che segua le vostre convenzioni. Alcune stime non ufficiali dicono che l'80% del codice JavaScript reperibile su Internet è monnezza, quindi state in guardia.

Per cominciare, bisogna sapere che le variabili in JavaScript dichiarate con `var` hanno uno **scope di funzione**, ovvero sono visibili in tutta la funzione in cui sono state dichiarate, _indipendentemente dal blocco in cui si trovano_.

Cosa significa in pratica? Significa che i seguenti due snippet di codice sono equivalenti, provate ad implementarli:

```javascript
var init = function() {
	var myName = "Harry";
	if (myName == "Harry") {
		var myFriend = "Ron";
	}
	alert("myFriend name is "+ myFriend);
}
```

```javascript
var init = function() {
	var myName = "Harry";
	var myFriend;
	if (myName == "Harry") {
		myFriend = "Ron";
	}
	alert("myFriend name is "+ myFriend);
}
```
Come vedete, la dichiarazione della variabile `myFriend` è salita fino in cima alla funzione, uscendo dallo scope dell'`if`. Questo è un comportamento inusuale, rispetto ad altri linguaggi, e potenzialmente rischioso! Infatti si rischia un conflitto di nomi tra variabili dichiarate anche lontano fra loro.

> Questo comportamento si chiama _hoisting_. Vedi la [JavaScript Hoisting](https://www.w3schools.com/js/js_hoisting.asp) su w3schools per dettagli.

La cosa è particolarmente pericolosa se si dichiarano variabili al di fuori di tutte le funzioni. Cosa succede in questo caso? Le variabili vanno a finire nella funzione _globale_ del browser, che si chiama `window()`. Come sappiamo, le variabili globali sono estremamente pericolose perché potrebbero andare in conflitto in qualsiasi momento e in modo imprevedibile con altre variabili dichiarate chissà dove, da noi o da altre librerie.

### Uso di let e const
Per mitigare il problema, possiamo dichiarare le variabili con le keyword `let` o `const`:

```javascript
var init = function() {
	var myName = "Harry";
	if (myName == "Harry") {
		let myFriend = "Ron";
	}
	alert("myFriend name is "+ myFriend); // errore
}
```

Con `let` o `const`, le variabili hanno una visibilità di ambito (scope), ovvero sono visibili solo all'interno del blocco racchiuso in parentesi graffe in cui si trovano e non sono utilizzabili all'esterno.

In particolare:
- `let` dichiara una variabile _mutabile_, che può quindi essere riassegnata
- `const` dichiara una variabile _immutabile_, che non può essere riassegnata.

Questo è un comportamento più simile a quello che ci si aspetta e più sicuro.

> Originariamente esisteva solo la parola chiave `var`. Le parole chiave `let` e `const` sono state standardizzate ufficialmente solo nel 2015, è per questo che la maggior parte di codice scritto prima di quella data non li usa e che alcuni sviluppatori veterani usino `var` semplicemente per abitudine.

#### Precisazione sul significato delle keyword
Per memorizzare, può essere utile precisare cosa significano le keyword che usiamo:
- `var` è l'abbreviazione di variabile
- `let` lo possiamo tradurre in questo caso con "permetti" (sottinteso: l'uso della variabile nel mio codice), è una delle prime keyword della storia, risalente a Lisp (1958)
- `const` è l'abbreviazione di "constant" che significa costante!


### Cosa devo usare quindi?
Per farla breve:
- se la variabile è costante, usate `const`
- in tutti gli altri casi, usate `let`

Usate `var` se e solo se sapete esattamente cosa state facendo

## Gestione del click del mouse

Per gestire il click del mouse, ci sono varie strategie, noi useremo quella idiomatica di JQuery, attraverso la funzione `on()`.

Per cominciare, nella nostra pagina HTML aggiungiamo un bottone.
```html
<button  id="moveUp">move UP</button>
```

Per associare il click del mouse, nella nostra funzione di init mettiamo la seguente riga di codice:
```javascript
$("#moveUp").on("click",moveUp);
```

Vediamo cosa abbiamo fatto:
- con `$("#moveUp")` ho selezionato l'elemento con id `#moveUp#`
- con `on("click",moveUp)` sto dicendo che quando si clicca con il mouse, dovrò richiamare la funzione `moveUp` (che ancora non abbiamo dichiarato, lo faremo dopo).

### Altri eventi che possono essere gestiti
Esistono tanti tipi di eventi, come ad esempio:
- `mouseenter`: l'utente passa il mouse sopra l'elemento (senza cliccarlo)
- `mouseleave`: l'utente toglie il mouse da sopra l'elemento
- `dblclick`: doppio click sull'elemento
- `keypress`: è stato premuto un tasto
- `scroll`: l'utente sta scorrendo la pagina

La lista è lunghissima, l'elenco completo lo trovate [qui](https://www.w3schools.com/jsref/dom_obj_event.asp).

## Modifica dello stile da JavaScript
È possibile cambiare lo stile in modo programmatico da JavaScript.

Per leggere il valore di una proprietà, ad esempio il valore di `top` dell'elemento con id "moveUp":
```javascript
$("#moveUp").css("top");
```

Se vogliamo invece scrivere una proprietà, dobbiamo chiamare la stessa funzione con due argomenti:
```javascript
$("#moveUp").css("top","50%");
```

In questo modo abbiamo impostato il valore `top` dell'elemento con id `#moveUp` al 50%.

## Modifica dello stile con JavaScript+CSS
Come abbiamo visto, modificare lo stile da JavaScript è possibile, ma in linea generale è meglio evitarlo: dobbiamo ricordarci che tutto quello che riguarda l'aspetto visivo è competenza del foglio di stile `.css`, quindi 
Un modo migliore per poter gestire



<style>
.centered {
	text-align: center;
}

table {
  font-family: monospace;
}

.xxl-font {
	font-size: xx-large;
}

.large-font {
	font-size: large;
}

img {
  width: 20%;
}

img.right_side {
  float: right;
  margin:5px 5px 0px 20px;
}
img.left_side {
  float:left;
  margin:5px 20px 0px 5px;
}

img.w100p {
  width: 100%;
}

img.w80p {
  width: 80%;
}

img.w50p {
  width: 50%;
}

img.w35p {
  width: 35%;
}

p.clear {
  clear: both;
}
p.img-container {
  margin-bottom: 15px;
}

p.img-container::after {
  margin-bottom: 15px;
  overflow: hidden;
  clear: both;
}

figcaption {
  font-size: medium;
  font-style: italic; 
}
</style>

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NDkxMTgxMTddfQ==
-->