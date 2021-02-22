
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
Immaginiamo di avere una immagine e volerla muovere con dei tasti.

Questo è il wireframe della pagina:

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAjEAAAGHCAYAAABBFAMBAAAgAElEQVR4Xu3dCbQUxd3+8R+ogAgqyKagoAZFgqLAq+KWuIAm0Shq3P4GiUbivu9b4q5xXwhCxO01rnkjRqNG3KOgBlCUIGKM4IIKKFEQBUX+5+mhYRjuvVNzp7unuvvb53iEe3uqqz7V3H5uVXV3E2NDAAEEEEAAAQRSKNAkhXWmyggggAACCCCAgBFiOAkQQAABBBBAIJUChJhUdhuVRgABBBBAAAFCDOcAAggggAACCKRSoM4QM3To0CWpbA2VRgABBBBAAIFMCowcOXKlzFJviBkxYkQmEWgUAggggAACCKRL4De/+Y0RYtLVZ9QWAQQQQAABBMyMEMNpgAACCCCAAAKpFCDEpLLbqDQCCCCAAAIIEGI4BxBAAAEEEEiBwLvvvmsTJkywd955x2bNmmXffPONtWjRwjp06GDdu3e3vn372sYbb1xVS5I4xkszzf48zewfH5pNm2s2b5FZ62Zm3duY7dTFbP9NzLZfz60ZhBg3J/ZCAAEEEECgJgIffvihjR49Oggu2267rW222Wa27rrrBgFGQWbmzJk2depUe/nll4NAs88++1iXLl0qqmsSx5g02+zcF83+Pdfs0J5mu3U167mO2ZrNzL5cZDblM7OnZpjdPcXsB23MLt3BrHf7hptBiKmom9kZAQQQQACB5ATGjRtnd9xxhx144IG2yy67lD3wM888Y/fff78NGTLE+vfvX3Z/7ZDEMe6aYnbY42bX72x2Yp/y1bphotlJz5rd+ROzwT3r358QU96SPRBAAAEEEEhcQOHioYcesqOPPto23HBD5+O/9957Nnz4cBs0aFDZIJPEMRRgzn7B7P/2Ntt2Xedm2Msfm+33sNnlO9UfZAgx7p7siQACCCCAQCICmt65+OKL7ayzzqoowISVU5C54oor7Pzzz693aimJY2gKacu7zMYdUlmACduhINP/HrPXB9c9tZSqEPPVV18Fc39z5861Tp062QcffJDIycRB0iew2mqrWZs2bWy99dazNdZYI30NoMYIIJBrgZtvvtl69uzpNIVUH5SmlqZMmWLHHXdcnbskcYw9HzIb0NVtCqm+dmhqacwMs0cHrbxHakLM7Nmzbdq0adatWzdr3769NWvWLNcnOI1vWGDRokWmc2b69Om2ySabBOcMGwIIIJAGAd0hdOedd9pFF11UdXUvuOACO+yww1a6aymJY+gupCOeMJt6eNXNsB63mY3aY+W7llIRYjQC8/rrr9vmm29ua665ZvUalJAbgS+//NLefPNN23LLLRmRyU2v01AE0i3wwAMPWKtWreynP/1p1Q157LHHbP78+XbAAQesUFYSxzj5ObN1Wpidt23VzbBLXjb77Buz6368YlmpCDG6J75ly5bWuXPn6iUoIXcCH330kS1YsCB4jgIbAggg4LvApZdeagcffLBttNFGVVdVa2PuueceO/fcc1coK4lj9L3bbNiujVsLU9pwrY057mmz8YemMMS8+uqrwW/STCFVfT7nsoCFCxfapEmTbOutt85l+2k0AgikS+DEE0+0K6+8MngOTLWbniNz5pln2g033LBCUUkcY82bzD78TeE5MNVueo5MlxFmXx6fshCzZMkSGzt2rG2//fbVGvD5HAu89NJLnEM57n+ajkCaBDRFMmLEiMiqXFd5SRyjyTVmS06NrBlWV3mpmE7iAhTdSZDXkjiH8trztBuB9AkkMUqSxDEYiVl67jV0AdKiTS3edNmaN28erNDWrbds+RIgxOSrv2ktAmkW0HqVQw45pFHPhylt93/+8x+7995761wTE/cx+t1tdnOEa2KOfdpsQhrXxDR0Aark4qR9tenee4JMmv+JV173Ss6TykvnEwgggEB0AkncOZTEMbg7yWEkppKLk/ZVgNHDfxoTZLQ+p3Rr0qRJdGcuJcUmUMl5ElslKBgBBBBwEEjiGS5JHIPnxMQQYrRAWE/8rTTIDBs2zN54442VTr+mTZta165dg6G/DTbYwOH0rM0ud999d/Do6R//uOQm+9pUJ/GjEmISJ+eACCBQhUAST9NN4hg8sdfMoppO0voZbWuttZZpBOWLL76wXr16OZ1mYYjR01/1eW26dVevPlAoUpi55JJLbJ111nEqL8md3n77bbv22mutX79+duSRRyZ5aG+ORYjxpiuoCAIIOAgk8V6jJI7Bu5MiDDHff/99sAhY/ynA6P+ut26HIebss88OXn1QvN122232yiuv2O6772777ruvw+mZzC6PPvqoaVHXv/71r+CAhBhu00/mzOMoCCAQhUASb5hO4hi5f4t1VCMxpSdVJb+dNxRi/vnPf9qtt95qW221lR111FHBYcaPH296SN/UqVODBxZp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" style="max-width:100%;" />

Il nostro codice sarà, prendendo ad esempio l'immagine di un lama:
```html
<button  id="moveUp">Move UP</button>
<img  id="lamaImage"  src="./lama.jpeg"  alt="Immagine del lama">
```
```css
#lamaImage {
	position:absolute;
	left:50%;
	top:50%;
	width:  12%;
}
```

Per leggere il valore di una proprietà, ad esempio il valore di `top` dell'elemento con id "moveUp", possiamo scrivere:
```javascript
let topValue = $("#lamaImage").css("top");
```
Da notare che il valore delle posizioni vengono sempre ritornate in pixels, con la desinenza `px`. Per poter leggere il valore intero, possiamo fare il parsing:
```javascript
let topValue = parseInt($("#lamaImage").css("top"));
```


Se vogliamo invece scrivere una proprietà, dobbiamo chiamare la stessa funzione con due argomenti:
```javascript
$("#lamaImage").css("top", topValue + "%");
```
Attenzione al percento alla fine: gli sto dicendo 


```js
let topValue = 50;
let moveUp = function () {
	console.log("Sposto il lama in alto");
	topValue -= 5;
	$("#lamaImage").css("top", topValue + "%");
};
let init = function () {
	$("#moveUp").on("click", moveUp);
};
$(document).ready(init);
```





In questo modo abbiamo impostato il valore `top` dell'elemento con id `#moveUp` al 50%.

## Modifica dello stile con JavaScript+CSS
Come abbiamo visto, modificare lo stile da JavaScript è possibile, ed in alcuni casi non è possibile evitarlo: ad esempio se dobbiamo cambiare ad ogni pressione del tasto il valore di `top`.

In linea generale è meglio evitare di modificare lo stile da JavaScript, perché dobbiamo ricordarci che tutto quello che riguarda l'aspetto visivo è competenza del foglio di stile `.css`. Come faccio quindi a rendere dinamico l'aspetto della pagina, ma mantenendo tutte le regole nel foglio di stile?

La soluzione è quella di creare delle classi dedicate allo stile, scrivere le regole relative nel foglio di stile, ed aggiungere e togliere le classi in modo dinamico in JavaScript.

Facciamo un esempio: aggiungiamo un bottone che mi ingrandisce l'immagine.
```html
<button  id="enlargeButton">enlarge</button>
```
Quando si preme questo pulsante, un certo elemento dovrà
```css
```




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
eyJoaXN0b3J5IjpbLTE0Mzk0MDMyOTQsLTE0MzAwNTA0MTMsOT
I1MTAzODg3LDE4OTUxNjY5NzgsMjMwNjA5MDY1XX0=
-->