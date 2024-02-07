# Metodi in una Classe VS `prototype`

Quando definisci un metodo all'interno di una classe o di una funzione costruttore, ogni volta che crei un'istanza di quella classe o costruttore, una nuova copia del metodo viene creata e assegnata a ciascuna istanza. Questo approccio aumenta l'utilizzo della memoria perché ogni istanza mantiene la sua copia unica del metodo, anche se la logica del metodo è esattamente la stessa per ogni istanza.

Esempio con metodo definito all'interno del costruttore:

```javascript
function Persona(nome) {
  this.nome = nome;
  this.saluta = function() {
    console.log(`Ciao, il mio nome è ${this.nome}!`);
  };
}
```

In questo caso, ogni volta che crei un nuovo oggetto `Persona`, viene creata una nuova funzione `saluta` per quell'oggetto.

D'altro canto, quando aggiungi un metodo al prototipo di una classe o di una funzione costruttore, tutte le istanze create da quella classe o costruttore condividono lo stesso metodo. Questo metodo è definito una sola volta nella memoria e ogni istanza accede a questo metodo tramite la catena dei prototipi. Ciò è più efficiente in termini di memoria, specialmente quando hai molte istanze della stessa classe.

Esempio con metodo aggiunto al prototipo:

```javascript
function Persona(nome) {
  this.nome = nome;
}

Persona.prototype.saluta = function() {
  console.log(`Ciao, il mio nome è ${this.nome}!`);
};
```

In questo secondo caso, il metodo `saluta` è definito una sola volta, indipendentemente da quante istanze di `Persona` vengano create. Ogni istanza di `Persona` può usare `saluta`, ma non c'è una copia separata del metodo `saluta` per ogni istanza.

Questo approccio è più efficiente in termini di memoria e segue il principio DRY ("Don't Repeat Yourself"), poiché il codice del metodo è definito una sola volta ma può essere utilizzato da molteplici istanze.