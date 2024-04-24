# Introduzione a JavaScript


Benvenuti in un'introduzione completa a JavaScript, uno strumento imprescindibile nel mondo dello sviluppo web. Cominciamo con un viaggio nella **storia di JavaScript**, esplorando le sue origini e le sue versioni. Creato da Brendan Eich nel 1995, JavaScript è stato inizialmente concepito per rendere le pagine web più interattive. Da allora, è cresciuto enormemente, diventando uno dei linguaggi di scripting più diffusi al mondo. Con l'introduzione di ECMAScript, una specifica standard, JavaScript si è evoluto in termini di funzionalità e performance. Ogni versione di ECMAScript, come ES5 o ES6, ha portato nuove e potenti caratteristiche, come le arrow functions, le classi, le promesse e i moduli, rendendolo un linguaggio sempre più potente e versatile.

Passando al **setup dell'ambiente di sviluppo**, la configurazione iniziale per lavorare con JavaScript è sorprendentemente semplice. In quanto linguaggio interpretato eseguito dai browser, tutto ciò di cui avete bisogno è un editor di testo e un browser moderno. Tuttavia, per un'esperienza di sviluppo più robusta, strumenti come Node.js, che permette di eseguire JavaScript lato server, e NPM, il gestore di pacchetti di Node.js, sono essenziali. Questi strumenti non solo espandono le capacità di JavaScript ma forniscono anche l'accesso a un vasto ecosistema di librerie e framework.

Ora, immergiamoci nella **sintassi di base di JavaScript**. In JavaScript, le variabili sono contenitori per memorizzare dati, che possono essere dichiarate utilizzando `var`, `let`, o `const`, ognuna con le proprie peculiarità in termini di scope (ambito di visibilità) e ri-assegnabilità. JavaScript è un linguaggio dinamicamente tipizzato, il che significa che le variabili possono contenere diversi tipi di dati come numeri, stringhe e booleani. Gli operatori in JavaScript sono utilizzati per eseguire operazioni su questi valori, inclusi operatori aritmetici, logici e di confronto.

Infine, esaminiamo le **strutture di controllo**. JavaScript, come altri linguaggi di programmazione, utilizza istruzioni condizionali e cicli per controllare il flusso del programma. Le istruzioni condizionali come `if` e `else` consentono di eseguire differenti blocchi di codice a seconda delle condizioni. I cicli, inclusi `for` e `while`, sono utili per eseguire un blocco di codice ripetutamente fino a quando una condizione specifica è soddisfatta, rendendoli strumenti potenti per iterare su array e oggetti.

Questa panoramica di JavaScript vi fornisce una solida base per iniziare a esplorare le sue capacità. Con la sua ricca storia, un ambiente di sviluppo accessibile, una sintassi flessibile e potenti strutture di controllo, JavaScript si afferma come una pietra miliare nel panorama dello sviluppo web moderno.


JavaScript è un linguaggio di programmazione versatile e potente, fondamentale nello sviluppo di pagine web dinamiche. Iniziamo con le **funzioni**, un concetto centrale in JavaScript. Una funzione è un blocco di codice riutilizzabile progettato per eseguire una specifica attività. La creazione di una funzione inizia con la parola chiave `function`, seguita dal nome della funzione, parametri tra parentesi e, infine, il corpo della funzione tra parentesi graffe. Questi parametri agiscono come variabili all'interno della funzione. Quando la funzione viene invocata o chiamata, restituisce un risultato che può essere utilizzato in altre parti del programma.

Passiamo ora agli **array**. In JavaScript, un array è un oggetto che può memorizzare più valori in una singola variabile. Questi valori possono essere numeri, stringhe o anche altri array e oggetti. La manipolazione degli array è facilitata da una serie di metodi incorporati. Ad esempio, `map()` crea un nuovo array applicando una funzione a ogni elemento dell'array originale, `filter()` crea un nuovo array contenente solo elementi che soddisfano una condizione specifica, e `reduce()` combina tutti gli elementi di un array in un singolo valore.

Le **stringhe** sono un altro tipo di dati essenziale in JavaScript. Sono utilizzate per rappresentare e manipolare testo. JavaScript fornisce molti metodi per lavorare con stringhe, come `split()`, che divide una stringa in un array di sottostringhe in base a un separatore specificato, e `join()`, che fa esattamente il contrario, unendo elementi di un array per formare una stringa. Altri metodi comuni includono `replace()`, per sostituire parti di una stringa, e `slice()`, per estrarre una parte di una stringa.

Ora, esploriamo gli **oggetti** in JavaScript. Un oggetto è una collezione di proprietà, dove ogni proprietà è una coppia chiave-valore. Gli oggetti sono estremamente flessibili e possono contenere una varietà di tipi di dati, comprese altre funzioni, note come metodi. Gli oggetti sono fondamentali in JavaScript perché permettono di organizzare i dati in modo strutturato e intuitivo.

Una parte cruciale di JavaScript è la manipolazione del **Document Object Model (DOM)**. Il DOM è una rappresentazione strutturata della pagina HTML e JavaScript può essere usato per manipolare questa struttura, permettendo di aggiungere, modificare o rimuovere elementi HTML e CSS. Questo è particolarmente potente perché significa che il contenuto di una pagina web può cambiare dinamicamente in risposta alle azioni dell'utente.

La **gestione degli eventi** è un altro aspetto chiave di JavaScript. Gli eventi sono azioni che accadono all'interno del browser, come clic del mouse o pressioni di tasti. JavaScript può "ascoltare" questi eventi e eseguire codice in risposta a essi. Ad esempio, possiamo usare `addEventListener()` per eseguire una funzione quando un utente clicca su un bottone.

Infine, parliamo della **gestione dei form**. I form sono un modo essenziale per raccogliere input dall'utente in una pagina web. JavaScript può essere utilizzato per validare questi input, assicurandosi che siano completi e nel formato corretto prima di essere inviati a un server. Questo è fondamentale per la sicurezza e l'usabilità di una pagina web.

In sintesi, JavaScript arricchisce l'esperienza web offrendo la possibilità di creare pagine dinamiche e interattive. Da semplici operazioni su stringhe e array, alla manipolazione complessa del DOM e alla gestione degli eventi, JavaScript è uno strumento indispensabile per qualsiasi sviluppatore web.

La programmazione orientata agli oggetti (OOP) è un paradigma di programmazione basato sul concetto di "oggetti", che possono contenere dati sotto forma di campi (spesso noti come attributi o proprietà) e codice sotto forma di procedure (spesso note come metodi). In JavaScript, la OOP viene implementata attraverso prototipi e, a partire da ES6, tramite la sintassi delle classi che offre un modo più chiaro e familiare di creare oggetti e gestire l'ereditarietà.

# La OOP in Javascript

La programmazione orientata agli oggetti (OOP, Object-Oriented Programming) è un paradigma di programmazione basato sull'idea di "oggetti", che possono contenere dati sotto forma di campi (spesso chiamati attributi o proprietà) e codice sotto forma di procedure (conosciute come metodi). La OOP si concentra sulla creazione di oggetti che raggruppano sia dati che funzionalità correlate, che possono essere utilizzati per modellare oggetti del mondo reale o astrazioni concettuali.

### Incapsulamento

L'incapsulamento è il concetto di nascondere i dettagli interni di un oggetto e mostrare solo le funzionalità necessarie all'esterno. In JavaScript, l'incapsulamento può essere ottenuto tramite l'uso di funzioni e chiusure.

**Esempio:**

```javascript
function Automobile(marca, modello) {
  let velocita = 0; // Proprietà privata

  // Metodo pubblico
  this.accelera = function() {
    velocita += 10;
    console.log(`${marca} ${modello} sta accelerando, velocità attuale: ${velocita}`);
  };

  // Metodo pubblico
  this.frena = function() {
    velocita -= 10;
    console.log(`${marca} ${modello} sta frenando, velocità attuale: ${velocita}`);
  };
}

const miaAuto = new Automobile('Toyota', 'Corolla');
miaAuto.accelera();
miaAuto.frena();
```

### Ereditarietà

L'ereditarietà è un principio in cui una classe (chiamata sottoclasse) può ereditare proprietà e metodi da un'altra classe (chiamata superclasse). In JavaScript, l'ereditarietà può essere realizzata tramite la catena dei prototipi o usando la sintassi `class` di ES6.

#### Esempio con la sintassi `class`:

```javascript
class Veicolo {
  constructor(marca) {
    this.marca = marca;
  }

  mostraMarca() {
    console.log(`La marca del veicolo è ${this.marca}`);
  }
}

class Automobile extends Veicolo {
  constructor(marca, modello) {
    super(marca); // Chiama il costruttore della classe genitore
    this.modello = modello;
  }

  mostraModello() {
    console.log(`Il modello dell'automobile è ${this.modello}`);
  }
}

const miaAuto = new Automobile('Toyota', 'Corolla');
miaAuto.mostraMarca();
miaAuto.mostraModello();
```

#### Esempio con l'approccio funzionale:

In JavaScript, prima dell'introduzione delle classi in ES6, l'ereditarietà veniva spesso realizzata attraverso funzioni costruttrici e la catena dei prototipi.

```javascript
function Veicolo(marca) {
  this.marca = marca;
}

Veicolo.prototype.mostraMarca = function() {
  console.log(`La marca del veicolo è ${this.marca}`);
};

function Automobile(marca, modello) {
  Veicolo.call(this, marca); // Chiama il costruttore del genitore con il contesto dell'Automobile
  this.modello = modello;
}

// Eredita da Veicolo
Automobile.prototype = Object.create(Veicolo.prototype);
Automobile.prototype.constructor = Automobile;

Automobile.prototype.mostraModello = function() {
  console.log(`Il modello dell'automobile è ${this.modello}`);
};

const miaAuto = new Automobile('Toyota', 'Corolla');
miaAuto.mostraMarca();
miaAuto.mostraModello();
```

In questo esempio, `Automobile` eredita da `Veicolo` utilizzando funzioni costruttrici. `Veicolo.call(this, marca);` chiama il costruttore di `Veicolo` nel contesto di un'istanza di `Automobile`, permettendo così di inizializzare la proprietà `marca`. Con `Automobile.prototype = Object.create(Veicolo.prototype);`, impostiamo il prototipo di `Automobile` per ereditare da `Veicolo`, e con `Automobile.prototype.constructor = Automobile;`, assicuriamo che il costruttore punti correttamente ad `Automobile`.

Questi due esempi mostrano come l'ereditarietà può essere implementata in JavaScript sia con la sintassi delle classi introdotta in ES6 sia con l'approccio funzionale più tradizionale.

### Polimorfismo

Il polimorfismo è la capacità di una variabile, funzione o oggetto di assumere più forme. In JavaScript, il polimorfismo si verifica principalmente tramite l'overriding dei metodi, dove una sottoclasse può sovrascrivere un metodo della superclasse.

**Esempio:**

```javascript
class Veicolo {
  avvia() {
    console.log("Il veicolo è stato avviato");
  }
}

class Automobile extends Veicolo {
  // Overriding del metodo avvia
  avvia() {
    console.log("L'automobile è stata avviata con un rumore specifico del motore");
  }
}

const mioVeicolo = new Veicolo();
mioVeicolo.avvia(); // Output: Il veicolo è stato avviato

const miaAuto = new Automobile();
miaAuto.avvia(); // Output: L'automobile è stata avviata con un rumore specifico del motore
```

### Astrazione

L'astrazione è il concetto di nascondere la complessità dettagliata e mostrare solo l'informazione essenziale all'utente. Può essere ottenuta usando classi astratte o interfacce (TypeScript offre supporto per le interfacce).

**Esempio in TypeScript:**

```typescript
abstract class Dispositivo {
  abstract accendi(): void;
  spegni() {
    console.log("Il dispositivo è stato spento");
  }
}

class Smartphone extends Dispositivo {
  accendi()

 {
    console.log("Lo smartphone è stato acceso");
  }
}

const mioSmartphone = new Smartphone();
mioSmartphone.accendi();
mioSmartphone.spegni();
```

In questo esempio, `Dispositivo` è una classe astratta che definisce un'astrazione per i dispositivi, specificando che devono avere un metodo `accendi`, ma non fornisce un'implementazione. `Smartphone` implementa questa astrazione fornendo un'implementazione per `accendi`.

Questi esempi dimostrano come i principi chiave della programmazione orientata agli oggetti possano essere applicati in JavaScript e TypeScript.