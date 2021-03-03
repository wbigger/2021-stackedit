# Separazione di front-end e back-end


È importante per far crescere in maniera organica il proprio progetto avere una buona separazione tra front-end e back-end.

In pratica significa che:
- sviluppatore front-end e back-end possano lavorare in parallelo
- posso cambiare il dispositivo di visualizzazione (tablet, smartphone, etc) senza toccare il backend
- posso cambiare la logica del backend (es. database, linguaggio di programmazione, etc) senza toccare il frontend

Per fare questo, dobbiamo fare in modo che front-end e back-end abbiamo un punto di contatto chiaro e ben definito. Di solito si usa il linguaggio [JSON](https://www.json.org/json-en.html), che è un formato di testo che è facilmente comprensibile alle macchine ma può essere letto e scritto anche da un essere umano.

> Un alternativa a JSON è l'XML

## Fasi di implementazione

Dopo aver creato la pagina web statica, si possono seguire i seguenti passi:
- metto tutti gli elementi dinamici in un file di test `.json`, all'interno del mio server, ad esempio `data.json`
- da front-end, leggo il file JSON attraverso una chiamata HTTP, ad esempio `$.getJSON('data.json')`
- da back-end, genero il file `data.json` con i dati presi dal database o come ritengo opportuno attraverso il mio linguaggio di programmazione preferito, ad esempio PHP
- quando tutto è pronto, sostituisco la chiamata al file locale `.json` con il la chiamata allo script del backend

## Esempio
Per un esempio di implementazione, potete guardare [qui](https://github.com/giadaventurini-pixel/2021-marconi-turismo-cremona/tree/f34f032cc1294937ea4c6a21a9274ea1d105c7d0/WebPage), con particoare riferimento ai file:
- index.html
- script.js
- poi_list.json
- index.php


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4NjMxNTM0MCwxODU5MzA1OTAwXX0=
-->