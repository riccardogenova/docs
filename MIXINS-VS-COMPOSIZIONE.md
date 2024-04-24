# Mixin VS Composizione

In JavaScript, l'ereditarietà tra classi tramite il prototipo ti permette di ereditare metodi e proprietà da una singola classe genitore. JavaScript non supporta nativamente l'ereditarietà multipla diretta (la capacità di una classe di ereditare da più di una classe genitore). Tuttavia, ci sono alcune tecniche che puoi usare per ottenere un comportamento simile all'ereditarietà multipla, come il mixin e la composizione.

# Mixins

I mixin sono un pattern che permette di "mescolare" metodi e proprietà da più sorgenti in un'unica classe. Questo approccio non è ereditarietà nel senso tradizionale, ma piuttosto un modo per aggiungere ("mixin") funzionalità a una classe.

Ecco come puoi usare un mixin per aggiungere metodi e proprietà da più "classi" (o meglio, oggetti, poiché in JavaScript le classi sono in realtà funzioni speciali):

```javascript

// Definisci un mixin
let mixinSalutatore = {
    saluta() {
        console.log(`Ciao, il mio nome è ${this.nome}!`);
    }
};

let mixinLavoratore = {
    lavora() {
        console.log(`Sto lavorando come ${this.ruolo}.`);
    }
};

// Funzione che applica i mixin a una classe
function applicaMixin(classe, mixin) {
    Object.assign(classe.prototype, mixin);
}

// Classe principale
class Persona {
    constructor(nome) {
        this.nome = nome;
    }
}

// Applica i mixin alla classe Persona
applicaMixin(Persona, mixinSalutatore);
applicaMixin(Persona, mixinLavoratore);

// Creazione di un'istanza che usa i mixin
let persona = new Persona("Mario");
persona.saluta(); // "Ciao, il mio nome è Mario!"
persona.lavora(); // Errore, perché `ruolo` non è definito in `Persona`
```

# Composizione 

Un altro approccio è la composizione, che consiste nell'includere istanze di altre classi come proprietà di una classe, anziché ereditarne direttamente i metodi e le proprietà. Questo approccio favorisce la composizione al posto dell'ereditarietà.


```javascript
class Salutatore {
    saluta(nome) {
        console.log(`Ciao, il mio nome è ${nome}!`);    
    }
}

class Lavoratore {
    lavora(ruolo) {
        console.log(`Sto lavorando come ${ruolo}.`);
    }
}

class Persona {
    constructor(nome, ruolo) {
        this.nome = nome;
        this.ruolo = ruolo;
        this.salutatore = new Salutatore();
        this.lavoratore = new Lavoratore();
    }

    saluta() {
        this.salutatore.saluta(this.nome);
    }

    lavora() {
        this.lavoratore.lavora(this.ruolo);
    }
}

let persona = new Persona("Mario", "Ingegnere");
persona.saluta(); // "Ciao, il mio nome è Mario!"
persona.lavora(); // "Sto lavorando come Ingegnere."
``````

In questo esempio, Persona non eredita direttamente da Salutatore o Lavoratore, ma invece compone la sua funzionalità includendo istanze di queste classi e delegando a esse le chiamate ai metodi appropriati.

Entrambi gli approcci hanno i loro pro e contro, e la scelta tra mixin, composizione o un'altra forma di ereditarietà dipende dallo specifico problema che stai cercando di risolvere e dalle preferenze di design.
