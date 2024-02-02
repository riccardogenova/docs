#### Introduzione alle Classi

In JavaScript, una classe è un tipo di funzione utilizzata per creare oggetti e implementare il concetto di ereditarietà. Le classi forniscono un modo più chiaro e sintetico per creare oggetti e gestire l'ereditarietà rispetto alle funzioni costruttrici e al pattern di ereditarietà basato su prototipi esistenti in JavaScript prima dell'introduzione delle classi in ES6 (ECMAScript 2015).

#### Struttura di una Classe

Una classe in JavaScript può essere definita utilizzando la parola chiave `class`, seguita dal nome della classe e da un blocco di codice che racchiude i suoi metodi. Esempio:

```javascript
class MyClass {
  // Metodi della classe
}
```

#### Il Costruttore

Il metodo `constructor` è un metodo speciale di una classe. Viene utilizzato per creare e inizializzare un oggetto creato con una classe. C'è solo un metodo `constructor` in una classe, e se si tenta di definirne più di uno, si verificherà un errore di sintassi.

Il `constructor` viene chiamato automaticamente quando si crea un'istanza della classe con `new`.

Esempio:

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const person1 = new Person('Alice', 30);
console.log(person1.name); // Alice
console.log(person1.age);  // 30
```

#### Estendere una Classe con `extends`

La parola chiave `extends` in JavaScript viene utilizzata per creare una classe figlia di un'altra classe. Questo è il modo per implementare l'ereditarietà tra classi in JavaScript.

Esempio:

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Chiama il costruttore della classe padre
    this.breed = breed;
  }

  speak() {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog('Rex', 'Golden Retriever');
dog.speak(); // Rex barks.
```

#### Uso di `super`

La parola chiave `super` viene utilizzata in due modi: come funzione e come oggetto.

- Come **funzione**, `super` chiama il costruttore della classe padre. È obbligatorio chiamare il costruttore del genitore prima di accedere a `this` in una classe figlia.
  
- Come **oggetto**, `super` è usato per chiamare metodi del genitore da metodi della classe figlia.

Esempio di `super` come oggetto:

```javascript
class Cat extends Animal {
  speak() {
    super.speak(); // Chiama il metodo speak del genitore
    console.log(`${this.name} meows.`);
  }
}

const cat = new Cat('Mia');
cat.speak(); // Mia makes a noise. Mia meows.
```

#### Conclusione

Le classi in JavaScript offrono un modo chiaro e conciso per lavorare con l'ereditarietà e per organizzare e strutturare il codice in modo orientato agli oggetti. Attraverso l'uso del costruttore, `extends`, e `super`, JavaScript fornisce un modello robusto e flessibile per la definizione e l'estensione di classi.


### I metodi `static`

Un metodo statico in una classe è un metodo che appartiene alla classe stessa piuttosto che a qualsiasi istanza specifica della classe. Questo significa che un metodo statico può essere chiamato sulla classe direttamente, senza dover creare un'istanza della classe. I metodi statici sono utili per implementare funzionalità che sono relative alla classe nel suo complesso piuttosto che a un oggetto specifico creato dalla classe.

Ecco le principali differenze tra metodi statici e non statici (o metodi d'istanza):

1. **Chiamata del metodo**: 
   - Un metodo statico viene chiamato sulla classe stessa. Ad esempio, se hai una classe `MathUtils` con un metodo statico `add`, lo chiameresti come `MathUtils.add()`.
   - Un metodo d'istanza viene chiamato su un'istanza della classe. Ad esempio, se hai una classe `Calculator` con un metodo d'istanza `subtract`, devi prima creare un'istanza (`let calc = new Calculator()`) e poi chiamare il metodo su quell'istanza (`calc.subtract()`).

2. **Uso della parola chiave `this`**:
   - In un metodo statico, `this` fa riferimento alla classe stessa. Ciò significa che non puoi accedere direttamente alle proprietà d'istanza della classe all'interno di un metodo statico, poiché non c'è un oggetto d'istanza.
   - In un metodo d'istanza, `this` fa riferimento all'oggetto specifico (istanza) su cui il metodo viene chiamato, consentendo l'accesso alle sue proprietà e metodi.

3. **Scopo e utilizzo**:
   - I metodi statici sono spesso utilizzati per operazioni utility o funzioni che non richiedono dati da un'istanza specifica della classe. Ad esempio, una funzione di aiuto per validare un indirizzo email potrebbe essere un metodo statico in una classe di utilità.
   - I metodi d'istanza sono utilizzati per operazioni che richiedono o modificano lo stato di un'istanza specifica della classe.

4. **Ereditarietà**:
   - I metodi statici possono essere ereditati in una sottoclasse, ma il loro `this` si riferirà sempre alla classe su cui sono stati definiti, non alla classe derivata, a meno che non vengano esplicitamente richiamati sulla sottoclasse.
   - I metodi d'istanza possono essere sovrascritti nelle sottoclassi, fornendo implementazioni specifiche che possono fare uso delle proprietà di quella sottoclasse.

Ecco un semplice esempio per illustrare un metodo statico rispetto a un metodo d'istanza:

```javascript
class MathUtils {
  static add(a, b) {
    return a + b; // Metodo statico
  }

  subtract(a, b) {
    return a - b; // Metodo d'istanza
  }
}

// Chiamata del metodo statico direttamente sulla classe
console.log(MathUtils.add(5, 3)); // 8

// Chiamata del metodo d'istanza su un'istanza della classe
const util = new MathUtils();
console.log(util.subtract(10, 4)); // 6
```

In questo esempio, `add` è un metodo statico che può essere chiamato direttamente su `MathUtils`, mentre `subtract` è un metodo d'istanza che richiede un oggetto `MathUtils` per essere chiamato.

### Metodi Statici nelle Classi

Oltre ai metodi d'istanza che operano su dati specifici dell'oggetto, le classi in JavaScript possono anche avere metodi statici. I metodi statici sono chiamati sulla classe stessa, non su istanze della classe. Sono spesso utilizzati per operazioni che non richiedono dati da un'istanza della classe.

#### Definizione di un Metodo Statico

Per definire un metodo statico, usi la parola chiave `static` prima del nome del metodo all'interno della classe. Ecco un esempio:

```javascript
class MathUtils {
  static sum(a, b) {
    return a + b;
  }
}

console.log(MathUtils.sum(5, 10)); // 15
```

In questo esempio, `sum` è un metodo statico della classe `MathUtils` e può essere chiamato direttamente sulla classe.

#### Getter e Setter

JavaScript supporta anche i getter e i setter nelle classi, permettendoti di avere un controllo più fine sull'accesso e la modifica delle proprietà di un oggetto.

Esempio:

```javascript
class Person {
  constructor(name) {
    this._name = name; // L'uso di un underscore è una convenzione per indicare una proprietà "privata"
  }

  get name() {
    return this._name;
  }

  set name(value) {
    if (value.length < 4) {
      console.log("Il nome deve avere almeno 4 caratteri.");
      return;
    }
    this._name = value;
  }
}

let person = new Person("Alice");
console.log(person.name); // Alice

person.name = "Al"; // Il nome deve avere almeno 4 caratteri.
console.log(person.name); // Alice (non cambiato)
```

I getter e i setter ti permettono di eseguire logica aggiuntiva ogni volta che accedi o modifichi una proprietà, come la validazione dei dati in questo esempio.


#### Metodi Privati nelle Classi JavaScript e TypeScript*

Nell'ambito della programmazione orientata agli oggetti, i metodi privati di una classe sono metodi che non possono essere chiamati o accessibili dall'esterno della classe. Questo concetto supporta l'incapsulamento e l'astrazione, consentendo agli sviluppatori di nascondere i dettagli di implementazione e di esporre solo le parti necessarie di un oggetto.

#### Metodi Privati in JavaScript

Con l'introduzione di ECMAScript 2015 (ES6), JavaScript ha introdotto il concetto di classi, ma senza un supporto nativo per i metodi privati. Tuttavia, con ECMAScript 2020 (ES2020), JavaScript ha introdotto una sintassi per i campi privati e i metodi privati nelle classi, utilizzando il prefisso `#`.

##### Sintassi dei Metodi Privati

```javascript
class MyClass {
  #myPrivateMethod() {
    console.log('Questo è un metodo privato.');
  }

  publicMethod() {
    this.#myPrivateMethod(); // Chiamata interna al metodo privato
  }
}

const myInstance = new MyClass();
myInstance.publicMethod(); // Funziona
myInstance.#myPrivateMethod(); // Errore! Il metodo è privato e non accessibile dall'esterno.
```

In questo esempio, `#myPrivateMethod` è un metodo privato accessibile solo all'interno della definizione della classe `MyClass`.

#### Metodi Privati in TypeScript

TypeScript estende JavaScript aggiungendo tipi e altre funzionalità, tra cui un miglior supporto per l'incapsulamento tramite la parola chiave `private`.

##### Utilizzo della Parola Chiave `private`

In TypeScript, puoi segnare un metodo come privato usando la parola chiave `private`. Questo impedisce che il metodo venga chiamato al di fuori della classe.

```typescript
class MyClass {
  private myPrivateMethod() {
    console.log('Questo è un metodo privato.');
  }

  publicMethod() {
    this.myPrivateMethod(); // Chiamata interna al metodo privato
  }
}

const myInstance = new MyClass();
myInstance.publicMethod(); // Funziona
myInstance.myPrivateMethod(); // Errore TypeScript, ma attenzione...
```

##### Limitazioni

Anche se TypeScript segnala un errore quando si tenta di accedere a un metodo privato dall'esterno della classe, **è importante notare che questa è una restrizione a livello di linguaggio impostata da TypeScript. Quando il codice TypeScript viene compilato in JavaScript, la distinzione tra metodi privati e pubblici non persiste nello stesso modo, perché JavaScript fino a ES2019 non supportava nativamente i metodi privati.**

Con l'introduzione dei metodi privati in ES2020, TypeScript può ora sfruttare questa caratteristica di JavaScript per i progetti che vengono compilati con un target di ES2020 o successivo.

#### Conclusioni

I metodi privati sono uno strumento essenziale nell'incapsulamento e nell'astrazione della programmazione orientata agli oggetti, consentendo di nascondere i dettagli di implementazione di una classe. In JavaScript, l'uso di metodi privati è diventato possibile con ES2020, mentre TypeScript ha fornito un supporto sintattico per l'incapsulamento fin dalla sua introduzione, con alcune limitazioni nella compilazione verso versioni precedenti di JavaScript. È cruciale comprendere queste differenze e limitazioni quando si lavora con classi e incapsulamento in TypeScript e JavaScript.