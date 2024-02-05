# ReactJS: Superare il Props Drilling con il Context

Benvenuti in questa lezione dedicata al Context di React, una funzionalità potente per gestire lo stato e condividere i dati in modo efficiente tra i componenti dell'applicazione, senza dover ricorrere al cosiddetto "props drilling".

## Cosa è il Props Drilling?

Il "props drilling" si verifica quando si passano dati da un componente all'altro attraverso una catena di componenti figli, anche se non tutti questi componenti necessitano effettivamente di tali dati. Questa pratica può rendere il codice complesso, difficile da mantenere e propenso a errori, specialmente in applicazioni di grandi dimensioni.

## Soluzione con Context

Il Context di React fornisce un modo per condividere valori simili a props globali per un albero di componenti. Invece di passare le props attraverso ogni livello dell'albero, i componenti possono accedere ai dati del Context direttamente, indipendentemente da quanto profondamente si trovino nell'albero dei componenti.

## Esempio Pratico: Contatore con Context

Immaginiamo di avere un'applicazione con un contatore che può essere incrementato o decrementato. Senza il Context, dovremmo passare la funzione di aggiornamento e il valore del contatore attraverso ogni livello di componenti. Vediamo come possiamo semplificare questo con il Context.

### Passo 1: Creazione del Context

Prima di tutto, creiamo un nuovo Context. In un nuovo file, ad esempio `CounterContext.js`, definiamo il nostro Context e una funzione che ci permetterà di utilizzarlo più facilmente nei nostri componenti.

```jsx
import React, { createContext, useContext, useState } from 'react';

const CounterContext = createContext();

export const useCounter = () => useContext(CounterContext);

export const CounterProvider = ({ children }) => {
  const [count, setCount] = useState(0);

  const increment = () => setCount((prevCount) => prevCount + 1);
  const decrement = () => setCount((prevCount) => prevCount - 1);

  return (
    <CounterContext.Provider value={{ count, increment, decrement }}>
      {children}
    </CounterContext.Provider>
  );
};
```

### Passo 2: Utilizzo del Provider

Per utilizzare il Context nel nostro componente principale o nell'applicazione, dobbiamo avvolgere la parte dell'albero dei componenti che necessita di accedere ai dati del Context nel Provider che abbiamo definito.

Nel file principale dell'app, ad esempio `App.js`, utilizziamo il `CounterProvider`.

```jsx
import React from 'react';
import { CounterProvider } from './CounterContext';
import CounterDisplay from './CounterDisplay';
import CounterControls from './CounterControls';

function App() {
  return (
    <CounterProvider>
      <div>
        <h1>Contatore con Context</h1>
        <CounterDisplay />
        <CounterControls />
      </div>
    </CounterProvider>
  );
}

export default App;
```

### Passo 3: Accesso ai Dati del Context

Ora che abbiamo un Provider che passa i dati del contatore, possiamo accedere a questi dati nei nostri componenti senza doverli passare esplicitamente come props.

Per esempio, nel componente `CounterDisplay`, che mostra il valore del contatore:

```jsx
import React from 'react';
import { useCounter } from './CounterContext';

function CounterDisplay() {
  const { count } = useCounter();

  return <h2>Valore Contatore: {count}</h2>;
}

export default CounterDisplay;
```

E nel componente `CounterControls`, che contiene i pulsanti per incrementare e decrementare il contatore:

```jsx
import React from 'react';
import { useCounter } from './CounterContext';

function CounterControls() {
  const { increment, decrement } = useCounter();

  return (
    <div>
      <button onClick={decrement}>Decrementa</button>
      <button onClick={increment}>Incrementa</button>
    </div>
  );
}

export default CounterControls;
```

## Conclusione

Con questo approccio, abbiamo superato il problema del props drilling, mantenendo il nostro codice pulito, mantenibile e facile da comprendere. Il Context ci ha permesso di condividere lo stato del contatore in modo efficiente tra i componenti, senza passare manualmente le props attraverso ogni livello dell'albero dei componenti.

Spero che questa lezione vi
