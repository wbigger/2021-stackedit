
# Attacchi SSH

Gli attacchi SSH sono tra i più comuni e pericolosi per i nostri server. In genere, si tratta di attacchi a forza bruta o basati su dizionari di password comuni. Ad esempio [qui](https://github.com/forScie/SSHAttacker) trovate un semplice software che si può usare per attacchi di questo genere.

Per mitigare questi attacchi, potete usare i seguenti accorgimenti:
1. **Disabilitare l'accesso root**: è buona pratica fare accesso sempre come utente non root ed eseguire i comandi da amministratore solo quando necessario
2. **Disabilitare servizi non usati**: se non usi SSH su una macchina, disabilitalo
3. **Filtrare il traffico SSH al tuo server**: imposta le regole del firewall in modo che solo alcuni IP possano accedere
4. **Cambiare la porta standard di SSH**: un po' scomodo, ma diminuisce considerevolmente gli attacchi automatici sulla porta di default (la 22)
5. **Forzare password sicure**: come sappiamo, password lunghe, con caratteri speciali e casuali diminuiscono drasticamente le possibilità di attacchi a forza bruta o basate su dizionari
6. **Usare software anti-brute-force**: un'ulteriore cosa da mantenere, ma efficace: controlla i log di sistema per vedere se ci sono stati un alto numero di tentativi errati (es. [DenyHost](https://it.wikipedia.org/wiki/DenyHosts)).
7. **Limitare il rate dei tentativi di connessione**: evita gli attacchi rapidi in successione.

Fonti: 
- [Protect Against Brute-force/Dictionary SSH Attacks](https://www.cmu.edu/iso/aware/be-aware/brute-force_ssh_attack.html), Carnegie Mellon University
- [SSHAttacker](https://github.com/forScie/SSHAttacker)

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjA5ODUzMTgyXX0=
-->