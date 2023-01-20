**Studente**: Pierotti Michele \
**Matricola**: 309256

# Servizio Localizzazione Negozi
## Descrizione del servizio implementato e del suo scopo

Oggigiorno la tecnologia ha raggiunto passi da gigante, ed è in continuo sviluppo. La sua grande evoluzione ha portato con sé purtroppo, oltre agli innumerevoli pregi, parecchi problemi di diverso tipo. Uno di questi è la sedentarietà.\
Questa piattaforma è stata pensata per poter reperire la posizione di alcuni negozi di diverso genere (abbigliamento, arredamento, spaccio, etc.) tramite i dati forniti dal sito (https://dati.gov.it/).

La piattaforma dispone di molteplici funzionalità:
1. È possibile avere una visuale generale di tutti i punti di interesse tramite una mappa, con il rispettivo elenco.
2. È possibile ricercare un punto di interesse per tipo, nome, codice univoco o indice.
3. È possibile aggiungere o rimuovere un punto di interesse.


## Descrizione di architettura e scelte implementative 
La piattaforma è basata su NodeJS. I dati utilizzati sono forniti tramite un file CSV. \
I dati presenti nel file CSV non sono stati in alcun modo ritoccati o modificati.
Notare che alcuni punti di interesse mancano di alcuni attributi, e.g. il nome, per questo non viene reso obbligatorio l'inserimento del nome di un nuovo punto di interesse.

Il front-end è stato sviluppato grazie all'uso di HTML5, CSS3 e JS. Inoltre, per la creazione della mappa, sono stati utilizzati Leaflet (una libreria JavaScript open source per mappe interattive ottimizzate per dispositivi mobili, https://leafletjs.com/), e OpenStreetMap. \
Il back-end è composto da JS e alcuni moduli:
- `express`: per usare NodeJS
- `fs`: per manipolare i file
- `ejs`: per effettuare il render di pagine HTML con JS.

È stato utilizzato JS per la manipolazione e la validazione dei dati inseriti da tastiera tramite form. \
È presente una piccola funzione di refresh dei campi del form, scritta in JQuery. \
Gli endpoint possono essere contattati sia tramite form che tramite URL.

In un'epoca dove il mobile sta prendendo sempre più piede, è stato scelto di ottimizzare la piattaforma per renderla esteticamente più piacevole anche su schermi di dimensione inferiore rispetto a quella di un PC.

## Documentazione dell’API implementata
 - **progetto_negozi.glitch.me/** \
Endpoint GET che restituisce la pagina principale (index.html) \
**INPUT**: niente \
**OUTPUT**: views/index.html

 - **progetto_negozi.glitch.me/negozicsv** \
Endpoint GET che restituisce il file CSV contenente tutti i dati \
**INPUT**: niente \
**OUTPUT**: views/negozi.csv

- **progetto_negozi.glitch.me/overview** \
Endpoint GET che restituisce la pagina web che mostra la mappa di tutti i punti di interesse con il rispettivo elenco \
**INPUT**: niente \
**OUTPUT**: views/overview.html

- **progetto_negozi.glitch.me/ricerca** \
Endpoint GET che restituisce la pagina web per la ricerca di uno specifico punto di interesse \
**INPUT**: niente \
**OUTPUT**: views/ricerca.html

- **progetto_negozi.glitch.me/inserisci** \
Endpoint GET che restituisce la pagina web per l'inserimento di un nuovo punto di interesse tramite form \
**INPUT**: niente \
**OUTPUT**: views/inserisci.html

- **progetto_negozi.glitch.me/rimuovi** \
Endpoint GET che restituisce la pagina web per la rimozione di un punto di interesse \
**INPUT**: niente \
**OUTPUT**: views/rimuovi.html

- **progetto_negozi.glitch.me/dati/:par** \
Endpoint GET che restituisce le informazioni appartenenti ad un punto di interesse, ricercato tramite tipo, nome, codice o indice (posizione nell'elenco) nella pagina ricerca.html \
**INPUT**: il parametro :par può assumere diversi tipi e configurazioni, in base a quale criterio si vuole ricercare il punto di interesse \
**OUTPUT**: 
   - Se il parametro :par è un numero, ovvero l'indice, viene restituito il punto di interesse in quella posizione nell'elenco.
   - Se il parametro :par è una stringa, si sta cercando un punto di interesse per tipo, per nome o per codice

&emsp;&emsp;Se la ricerca non va a buon fine, viene restituito un messaggio di errore opportuno con HTTP response 404 (400 nel caso di un indice &emsp;&emsp;non ammesso). \
&emsp;&emsp;L'API è dotata di opportuni controlli per restituire all'utente il risultato che si aspetta in base al parametro fornito.

- **progetto_negozi.glitch.me/inserimento** \
Endpoint GET che permette l'inserimento di un nuovo punto di interesse tramite form HTML. \
**INPUT**: la form HTML dispone di diversi campi da compilare: tipo, nome, codice, indirizzo, longitudine e latitudine. \
&emsp;&emsp;&emsp;I nomi dei campi sono i seguenti: *tipo, nome, codice, indirizzo, long, lat*. \
*N.B.*: dato che alcuni punti di interesse presenti nel file CSV mancano del nome, non è obbligatorio compilare il campo "nome" della form. \
**OUTPUT**: views/success.html

- **progetto-negozi.glitch.me/inserimento** \
Endpoint POST che permette l'inserimento di un nuovo punto di interesse da client esterni. \
**INPUT**: è necessario specificare i nomi degli attributi esattamente come li richiede l'endpoint GET. \
**OUTPUT**: HTTP response 200 se l'inserimento va a buon fine, HTTP response 400 se mancano dei parametri o se l'inserimento non va a buon fine in generale.

**N.B.**: Per le API di inserimento (GET e POST), è stato necessario recuperare due volte i parametri di longitudine e latitudine, per restituirli entrambi sia all'inizio che alla fine della stringa di output. Questo per mantenere la sintassi del file CSV originale.

- **progetto-negozi.glitch.me/rimuovi/:par** \
Endpoint DELETE che permette la rimozione di un punto di interesse. \
**INPUT**: l'indice del punto di interesse da rimuovere. \
**OUTPUT**: HTTP response 200 se la rimozione va a buon fine, altrimenti HTTP response 400.

Per alcuni endpoint è stato scelto di utilizzare una funzione di conversione da CSV ad array, presa dal seguente link: (https://www.bennadel.com/blog/1504-ask-ben-parsing-csv-strings-with-javascript-exec-regular-expression-command.htm). Ciò è stato fatto per poter lavorare meglio con i dati.

## Descrizione delle modalità della messa online del servizio
La piattaforma è fruibile attraverso il seguente link: (https://progetto-negozi.glitch.me). \
Il link Glitch rimanda alla pagina principale *index.html*.

## Esempio descrittivo di utilizzo del servizio Web + Screenshot
Questa è la homepage:

![index](https://user-images.githubusercontent.com/88444678/213774888-9609391d-aab3-4122-9dab-872edaac4425.png)

La mappa viene presentata nel seguente modo:

![localizzazione](https://user-images.githubusercontent.com/88444678/213775008-b87c9915-4b25-4f5f-833b-06470393448f.png)

Questa è la pagina di ricerca tramite form:

![tabella](https://user-images.githubusercontent.com/88444678/213775103-46a2d971-8ed0-4ce6-8a8d-5eed0a67f98a.png)

Scegliendo un tipo oppure scrivendo un nome, un codice o un indice, e cliccando sul corrispondente bottone di ricerca, si ottiene il risultato che ci si aspetta.

Nel caso di una ricerca a vuoto:

![vuoto](https://user-images.githubusercontent.com/88444678/213775151-a7ad96d6-069b-49f4-89e3-702808c9feee.png)

Se non si sceglie alcun tipo, o non si scrive alcun nome, codice o indice, viene restituito un messaggio di errore.
Se la ricerca non produce risultati, viene restituito un messaggio di errore.

Questa è la pagina di inserimento di un nuovo punto di interesse:

![errore](https://user-images.githubusercontent.com/88444678/213775281-1b139575-903c-4ad6-81f8-b67fd0eb3a79.png)

Come si può notare, il nome del punto di interesse non è obbligatorio. Al contrario, lo sono tutti gli altri campi.

Questa è la pagina di rimozione di un punto di interesse:

![rimuovi](https://user-images.githubusercontent.com/88444678/213775352-a83694f0-167c-42b5-b02d-a3e4a7c8b823.png)

Come si può notare, se l'indice esiste il punto viene rimosso.

![nrimuovi](https://user-images.githubusercontent.com/88444678/213775415-448bcfd1-5783-4de4-8ab7-2dc959a075be.png)

Se l'indice non esiste, viene restituito un messaggio di errore.

### Postman
Inserendo correttamente tutti i valori, si ottiene il seguente risultato:

![post1](https://user-images.githubusercontent.com/88444678/213775491-3220f019-56fe-4643-9cf3-74cc9e6aa044.png)

Se mancano alcuni valori, si ottiene il seguente risultato:

![post2](https://user-images.githubusercontent.com/88444678/213775536-5bd6e774-25ed-48ba-a928-080838669dda.png)

![post3](https://user-images.githubusercontent.com/88444678/213775552-c9899271-a1e6-4ea1-9d44-b7b6e427b23d.png)
