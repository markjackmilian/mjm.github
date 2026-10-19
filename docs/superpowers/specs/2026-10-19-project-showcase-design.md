# Vetrina progetti — design

## Obiettivo

Creare una breve vetrina in italiano per i progetti e le applicazioni di MJM. Chi visita il sito deve capire rapidamente quali progetti esistono e raggiungere la relativa pagina dedicata o il sito esterno. Il sito deve restare facile da aggiornare quando arriveranno altri progetti.

## Contenuto

La pagina iniziale mostra cinque schede:

1. **Toolotoolo** — nome e invito neutro a visitare `https://toolotoolo.com/`. Non attribuire caratteristiche al progetto senza una descrizione fornita dal proprietario o verificata.
2. **Project Orbit** — workspace personale che funziona offline; link a `https://project-orb.it/`. Questa descrizione è supportata dal README del progetto locale.
3. **mjm.cleaner** — applicazione macOS per individuare e rimuovere file temporanei rigenerabili dopo anteprima e conferma esplicita. La scheda porta a una pagina dedicata interna.
4. e 5. **In arrivo** — segnaposto visibili, senza collegamenti inattivi o finte descrizioni.

La pagina dedicata a mjm.cleaner contiene una sintesi concisa del flusso di analisi, anteprima e conferma, un link al repository `https://github.com/markjackmilian/mjm.cleaner` e un ritorno alla vetrina. Non promette download o disponibilità commerciale.

Una sezione breve dopo la griglia invita chi apprezza il lavoro a sostenere i progetti tramite Buy Me a Coffee. La pagina di mjm.cleaner ripete il collegamento in modo discreto. Usare un normale link esterno, senza widget, script di terze parti o richieste di pagamento dentro il sito. La destinazione deve essere il profilo Buy Me a Coffee comunicato dal proprietario; finché non è disponibile, il collegamento non viene pubblicato.

## Struttura e aspetto

- Una testata essenziale con marchio testuale “MJM” e collegamento alla sezione progetti.
- Un'introduzione breve: titolo chiaro, una frase descrittiva e un collegamento alla griglia dei progetti.
- Griglia responsive: tre colonne su schermi ampi, due su tablet, una su telefono. Le due schede “In arrivo” mantengono la stessa misura visiva ma uno stato distinto.
- Fondo chiaro, testo scuro, un solo colore d'accento freddo, linee sottili, spazi generosi, tipografia di sistema e movimento discreto. Nessuna immagine o logo inventato.
- Piè di pagina minimale con nome del sito e anno.
- Il supporto resta secondario rispetto all'esplorazione dei progetti: un invito testuale e un pulsante riconoscibile, senza banner invadenti.

## Comportamento e accessibilità

- I link esterni sono espliciti e raggiungibili da tastiera; i segnaposto non sono interattivi.
- Contrasto leggibile, struttura semantica, focus visibile e rispetto della preferenza per movimento ridotto.
- Le pagine funzionano senza JavaScript e si adattano a schermi mobili.

## Implementazione e pubblicazione

Usare HTML e CSS statici, senza framework, dipendenze o build. File principali: `index.html`, `projects/mjm-cleaner.html` e un foglio di stile condiviso. Usare percorsi relativi, così il sito funziona sia alla radice sia sotto un prefisso di GitHub Pages. Il repository locale è inizialmente vuoto: inizializzare Git e aggiungere i file. La pubblicazione richiede un repository remoto GitHub e accesso autenticato; verificare queste condizioni al momento del rilascio.

## Verifica

Controllare che le due pagine si aprano localmente, che i link interni ed esterni puntino alle destinazioni concordate, che non esistano link fittizi e che il layout resti leggibile su desktop e telefono. Verificare che GitHub Pages possa servire direttamente i file statici.
