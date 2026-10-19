# MJM — progetti e applicazioni

Vetrina statica in inglese per [Toolotoolo](https://toolotoolo.com/), [Project Orbit](https://www.project-orb.it/) e mjm.cleaner. Due schede “Coming soon” sono pronte per i prossimi progetti. Il sito è composto da HTML e CSS, senza build o dipendenze.

## Modificare il sito

- `index.html` contiene introduzione, profilo GitHub, schede dei progetti e invito al supporto. Per aggiungere un progetto, sostituire una scheda `project-card--soon` con una scheda attiva e un link reale.
- `projects/mjm-cleaner.html` è la pagina dedicata a mjm.cleaner. Le altre pagine dedicate possono seguire lo stesso schema nella cartella `projects/`.
- `assets/site.css` contiene lo stile condiviso e i layout per schermi piccoli.
- `assets/site-swiss.css` applica la direzione visiva Swiss scelta per la homepage e la pagina mjm.cleaner.
- `.nojekyll` permette a GitHub Pages di servire i file statici senza elaborazione Jekyll.

Usare percorsi relativi per i link interni: dalla homepage `projects/nome.html`, da una pagina nella cartella `projects/` `../index.html#projects` e `../assets/site.css`. I link esterni devono puntare a destinazioni HTTPS reali; le schede “Coming soon” non devono contenere link.

La sezione profilo usa l'avatar pubblico di GitHub. I numeri e i riconoscimenti sono una fotografia dei dati pubblici al 19 ottobre 2026, indicata anche nella pagina: aggiornare i valori e la data in `index.html` quando si desidera mostrare statistiche più recenti. “Commit contributions” è il conteggio dei contributi di tipo commit negli ultimi 12 mesi secondo GitHub, non il totale dei commit di sempre.

## Anteprima locale

```bash
python3 -m http.server 8765
```

Aprire `http://localhost:8765/` e verificare anche `http://localhost:8765/projects/mjm-cleaner.html`. Controllare navigazione, link, leggibilità, focus da tastiera e impaginazione su desktop e telefono. Il sito non ha una suite di test automatizzati: per le pagine statiche queste verifiche osservano il comportamento reale senza duplicare il contenuto HTML in test di sola corrispondenza.

## Pubblicazione su GitHub Pages con `gh`

Il repository previsto è `markjackmilian/mjm.github`; come project site, l'indirizzo atteso è `https://markjackmilian.github.io/mjm.github/`. Fare riferimento all'URL effettivo restituito dall'API Pages dopo l'attivazione. Se si sceglie un altro repository, sostituire proprietario e nome in tutti i comandi e usare il nuovo URL effettivo.

1. Controllare l'accesso GitHub:

   ```bash
   gh auth status
   ```

   Se la CLI segnala un token non valido, eseguire `gh auth login -h github.com` e completare l'accesso nel browser prima di continuare. Non salvare token in file del sito.

2. Se `markjackmilian/mjm.github` non esiste, creare il repository pubblico dal checkout e caricare `main`:

   ```bash
   gh repo create markjackmilian/mjm.github --public --source=. --remote=origin --push
   ```

   Se il repository esiste già, controllare l'URL con `gh repo view markjackmilian/mjm.github --json url --jq .url`, collegarlo al checkout se manca `origin`, poi caricare `main`:

   ```bash
   git remote add origin https://github.com/markjackmilian/mjm.github.git
   git push -u origin main
   ```

   Se `origin` è già configurato, verificare che punti al repository desiderato e usare soltanto `git push -u origin main`.

3. Verificare se Pages è già attivo:

   ```bash
   gh api repos/markjackmilian/mjm.github/pages --jq .html_url
   ```

   Se il comando risponde `404`, attivare la pubblicazione dal branch `main` e dalla radice:

   ```bash
   gh api -X POST repos/markjackmilian/mjm.github/pages \
     -f 'source[branch]=main' \
     -f 'source[path]=/'
   ```

4. Leggere l'URL effettivo e verificare entrambe le pagine pubblicate:

   ```bash
   gh api repos/markjackmilian/mjm.github/pages --jq .html_url
   ```

   Aprire l'URL restituito e il percorso `projects/mjm-cleaner.html`. La prima pubblicazione può richiedere qualche minuto; se l'URL non risponde ancora, controllare lo stato Pages nel repository GitHub e riprovare dopo il completamento della build.

I successivi aggiornamenti si pubblicano con commit e `git push` su `main`.
