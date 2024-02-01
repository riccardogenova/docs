# La Classe `Object` in JavaScript

La classe `Object` in JavaScript è una delle classi fondamentali del linguaggio, al punto che quasi tutti gli oggetti in JavaScript sono istanze di `Object`. Questa classe fornisce un insieme di metodi statici che sono utili per operazioni come la manipolazione, l'ispezione e la creazione di oggetti. 

## `Object.assign(target, ...sources)`

Questo metodo viene utilizzato per copiare tutte le proprietà enumerabili da uno o più oggetti sorgente a un oggetto target. Restituisce l'oggetto target.

**Esempio:**

```javascript
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);       // Output: { a: 1, b: 4, c: 5 }
console.log(returnedTarget); // Output: { a: 1, b: 4, c: 5 }
```

## `Object.create(proto, [propertiesObject])`

Crea un nuovo oggetto con l'oggetto prototipo specificato e, opzionalmente, le proprietà specificate.

**Esempio:**

```javascript
const person = {
  isHuman: false,
  printIntroduction: function() {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};

const me = Object.create(person);

me.name = 'Alice'; // "nome" è una proprietà "propria" di "me"
me.isHuman = true; // ereditata proprietà può essere sovrascritta

me.printIntroduction(); // Output: My name is Alice. Am I human? true
```

## `Object.defineProperty(obj, prop, descriptor)`

Definisce una nuova proprietà direttamente su un oggetto, o modifica una proprietà esistente su un oggetto, e restituisce l'oggetto.

**Esempio:**

```javascript
const object1 = {};

Object.defineProperty(object1, 'property1', {
  value: 42,
  writable: false
});

object1.property1 = 77;
// la proprietà "property1" non è scrivibile, quindi rimane 42

console.log(object1.property1); // Output: 42
```

## `Object.entries(obj)`

Restituisce un array di coppie [chiave, valore] delle proprietà enumerabili di un dato oggetto.

**Esempio:**

```javascript
const obj = { foo: 'bar', baz: 42 };
console.log(Object.entries(obj)); // Output: [ ['foo', 'bar'], ['baz', 42] ]
```

## `Object.freeze(obj)`

Congela un oggetto: impedisce l'aggiunta di nuove proprietà, rende tutte le proprietà esistenti non configurabili, e impedisce che i valori delle proprietà esistenti possano essere modificati.

**Esempio:**

```javascript
const obj = {
  prop: 42
};

Object.freeze(obj);

obj.prop = 33;
// Le modifiche non avranno effetto poiché l'oggetto è congelato

console.log(obj.prop); // Output: 42
```

## `Object.keys(obj)`

Restituisce un array contenente i nomi delle proprietà enumerabili di un dato oggetto.

**Esempio:**

```javascript
const obj = { foo: 'bar', baz: 42 };
console.log(Object.keys(obj)); // Output: ['foo', 'baz']
```

## `Object.values(obj)`

Restituisce un array contenente i valori delle proprietà enumerabili di un dato oggetto.

**Esempio:**

```javascript
const obj = { foo: 'bar', baz: 42 };
console.log(Object.values(obj)); // Output: ['bar', 42]
```

## `Object.hasOwnProperty(prop)`

Restituisce un booleano che indica se l'oggetto ha la proprietà specificata come sua proprietà diretta.

**Esempio:**

```javascript
const obj = { foo: 'bar' };

console.log(obj.hasOwnProperty('foo')); // Output: true
console.log(obj.hasOwnProperty('baz')); // Output: false
```
