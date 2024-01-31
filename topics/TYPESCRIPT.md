# Introduzione a TypeScript

## Cosa è TypeScript?

TypeScript è un superset di JavaScript open-source sviluppato da Microsoft, il che significa che qualsiasi codice JavaScript è anche un codice TypeScript valido. TypeScript estende JavaScript aggiungendo tipi statici alle variabili. Quando si compila il codice TypeScript, questo viene trasformato in codice JavaScript puro, che può essere eseguito in qualsiasi browser o ambiente JavaScript, come Node.js.

## Vantaggi di TypeScript

### Tipizzazione Stretta

La caratteristica principale di TypeScript è la sua tipizzazione statica. A differenza di JavaScript, che è dinamicamente tipizzato, TypeScript consente di specificare i tipi di variabili, funzioni, oggetti, ecc. Questo aiuta a catturare errori, come l'uso improprio di tipi, in fase di sviluppo prima ancora di eseguire il codice.

### Migliore Supporto agli IDE

Grazie alla sua tipizzazione, TypeScript offre un migliore supporto negli ambienti di sviluppo integrati (IDE). Funzionalità come il completamento automatico del codice, il refactoring e le indicazioni sugli errori in tempo reale sono più accurate e utili, migliorando la produttività dello sviluppatore.

### Migliore Leggibilità e Manutenibilità

Definire esplicitamente i tipi nel tuo codice può rendere più chiaro il contratto delle funzioni o delle componenti. Questo aiuta non solo te come sviluppatore nell'evitare errori, ma rende anche il tuo codice più leggibile per altri sviluppatori, facilitando la manutenzione e l'estensione del codice nel tempo.

### Compatibilità con JavaScript

TypeScript è compatibile con tutti i framework e le librerie JavaScript esistenti. Puoi convertire gradualmente un progetto JavaScript esistente in TypeScript, sfruttando i vantaggi della tipizzazione statica dove necessario, senza dover riscrivere l'intera base di codice.

### Potenti Funzionalità di OOP

TypeScript supporta le funzionalità di programmazione orientata agli oggetti (OOP) come classi, interfacce e moduli, rendendolo una scelta eccellente per costruire applicazioni complesse e di grandi dimensioni.

### Facilità di Refactoring

La tipizzazione statica rende il refactoring del codice più sicuro e prevedibile. È possibile apportare modifiche significative alla base di codice con una maggiore fiducia che non si introdurranno nuovi bug, poiché molti errori potenziali possono essere rilevati in fase di compilazione.

### Migliore Integrazione con gli Strumenti di Sviluppo

TypeScript è ben supportato da molti strumenti di sviluppo, build system e linters, rendendo facile integrarlo in pipeline di CI/CD (Continuous Integration/Continuous Deployment) e pratiche di sviluppo agile.

## Tipi Primitivi

TypeScript estende i tipi primitivi di JavaScript con tipizzazione statica:

- **`string`**: Sequenze di caratteri.
  ```typescript
  let nome: string = "Alice";
  ```
- **`number`**: Numeri interi e a virgola mobile.
  ```typescript
  let eta: number = 30;
  ```
- **`boolean`**: Valori logici `true` o `false`.
  ```typescript
  let isStudent: boolean = true;
  ```
- **`null` e `undefined`**: Indicano l'assenza di un valore o un valore non assegnato.
  ```typescript
  let nullo: null = null;
  let indefinito: undefined = undefined;
  ```
- **`void`**: Usato per funzioni che non restituiscono un valore.
  ```typescript
  function saluta(): void {
      console.log("Ciao a tutti!");
  }
  ```
- **`any`**: Permette qualsiasi tipo di valore, da evitare quando possibile.
  ```typescript
  let sconosciuto: any = "Potrebbe cambiare tipo";
  ```
- **`unknown`**: Simile a `any`, ma richiede un controllo del tipo prima dell'uso.
  ```typescript
  let valore: unknown = 30;
  if (typeof valore === "number") {
      let somma = valore + 10;
  }
  ```

## Tipi per Oggetti

Definisci tipi complessi specificando i tipi delle proprietà:

```typescript
let persona: { nome: string; eta: number; } = { nome: "Alice", eta: 30 };
```

### Interfacce

Le interfacce permettono di nominare e riutilizzare i tipi degli oggetti:

```typescript
interface Persona {
    nome: string;
    eta: number;
}

let studente: Persona = { nome: "Bob", eta: 20 };
```

### Estensione delle Interfacce

Crea sottotipi estendendo una o più interfacce:

```typescript
interface Lavoratore {
    professione: string;
}

interface LavoratoreSpecializzato extends Persona, Lavoratore {
    competenze: string[];
}
```

## Tipi Generici

I tipi generici aumentano la flessibilità permettendo di lavorare con qualsiasi tipo di dato:

### Funzioni Generiche

```typescript
function primoElemento<T>(arr: T[]): T | undefined {
    return arr[0];
}
```

### Interfacce Generiche

```typescript
interface Coppia<T, U> {
    primo: T;
    secondo: U;
}

let coppia: Coppia<string, number> = { primo: "età", secondo: 30 };
```

### Classi Generiche

```typescript
class Coda<T> {
    private dati: T[] = [];
    aggiungi(elemento: T) {
        this.dati.push(elemento);
    }
    rimuovi(): T | undefined {
        return this.dati.shift();
    }
}
```

### Operatore `keyof`

L'operatore `keyof` prende un tipo di oggetto e produce un tipo unione delle sue chiavi. È estremamente utile quando hai bisogno di riferirti alle chiavi di un oggetto come tipi letterali.

**Esempio d'uso di `keyof`:**

```typescript
interface Utente {
  nome: string;
  eta: number;
}

type ChiaviUtente = keyof Utente; // 'nome' | 'eta'

function mostraProprieta(utente: Utente, chiave: ChiaviUtente) {
  console.log(utente[chiave]);
}

const utente: Utente = {
  nome: "Alice",
  eta: 30
};

mostraProprieta(utente, "nome"); // Output: Alice
// mostraProprieta(utente, "nonEsiste"); // Errore: "nonEsiste" non è una chiave di Utente
```

In questo esempio, `ChiaviUtente` è un tipo unione che corrisponde a `"nome" | "eta"`, le chiavi dell'interfaccia `Utente`. La funzione `mostraProprieta` accetta solo valori che sono chiavi valide dell'oggetto `Utente`.

### Operatore `typeof`

L'operatore `typeof` in TypeScript, simile a quello di JavaScript, può essere utilizzato in contesti di tipizzazione per catturare il tipo di una variabile esistente. Questo è particolarmente utile per creare tipi basati sui valori di variabili JavaScript/TypeScript esistenti.

**Esempio d'uso di `typeof`:**

```typescript
const configurazione = {
  darkMode: true,
  versione: "1.0.0"
};

type Configurazione = typeof configurazione;

function impostaConfigurazione(config: Configurazione) {
  console.log(`Modalità scura: ${config.darkMode ? "Attiva" : "Disattiva"}`);
}

impostaConfigurazione(configurazione); // Output: Modalità scura: Attiva
```

In questo esempio, il tipo `Configurazione` è derivato direttamente dalla struttura dell'oggetto `configurazione`, catturando i tipi delle sue proprietà (`{ darkMode: boolean; versione: string }`). La funzione `impostaConfigurazione` accetta quindi un oggetto che ha la stessa forma dell'oggetto `configurazione`.


### `Partial<Type>`

Questo tipo utility rende tutti i campi di un tipo `Type` opzionali. È utile quando si desidera creare un oggetto che non necessita di tutte le proprietà del tipo originale.

```typescript
interface Utente {
  nome: string;
  eta: number;
}

const utenteParziale: Partial<Utente> = { nome: "Alice" };
```

### `Readonly<Type>`

Questo tipo trasforma tutti i campi di un tipo `Type` in sola lettura, il che significa che non possono essere riassegnati dopo la loro inizializzazione.

```typescript
interface Utente {
  nome: string;
}

const utente: Readonly<Utente> = { nome: "Bob" };
// utente.nome = "Alice"; // Errore: Cannot assign to 'nome' because it is a read-only property.
```

### `Record<Keys, Type>`

Questo tipo utility crea un tipo che utilizza un set di chiavi `Keys` e assegna a queste chiavi un tipo `Type`. È utile per creare oggetti quando sappiamo quali saranno le chiavi ma tutti i valori avranno lo stesso tipo.

```typescript
const numeriPagina: Record<string, number> = {
  home: 1,
  about: 2,
  contact: 3,
};
```

### `Pick<Type, Keys>`

Permette di creare un tipo selezionando un set di proprietà `Keys` da un altro tipo `Type`. È utile per creare un tipo che contenga solo un sottoinsieme delle proprietà di un altro tipo.

```typescript
interface Utente {
  nome: string;
  eta: number;
  email: string;
}

type UtenteNomeEmail = Pick<Utente, 'nome' | 'email'>;
```

### `Omit<Type, Keys>`

Questo tipo utility fa l'opposto di `Pick`; crea un tipo rimuovendo il set di proprietà `Keys` da un altro tipo `Type`.

```typescript
interface Utente {
  nome: string;
  eta: number;
  email: string;
}

type UtenteSenzaEmail = Omit<Utente, 'email'>;
```

### `Exclude<Type, ExcludedUnion>`

Questo tipo utility costruisce un tipo escludendo da `Type` tutti i tipi union presenti in `ExcludedUnion`.

```typescript
type Disponibile = string | number | boolean;
type NonNumerico = Exclude<Disponibile, number>; // string | boolean
```

### `NonNullable<Type>`

Crea un tipo rimuovendo `null` e `undefined` da un tipo `Type`.

```typescript
type ForseNumero = number | null | undefined;
type SoloNumero = NonNullable<ForseNumero>; // number
```

### `ReturnType<Type>`

Questo tipo utility estrae il tipo di ritorno di una funzione.

```typescript
function ottieniNumero() {
  return 123;
}

type Numero = ReturnType<typeof ottieniNumero>; // number
```
