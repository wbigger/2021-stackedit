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
- metto tutti gli elementi dinamici in un file `.json`, all'interno del mio server
- da front-end, leggo il file JSON attraverso una chiamata HTTP, ad esempio `
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE5ODc3MDIxM119
-->