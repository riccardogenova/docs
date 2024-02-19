# Introduzione a Redux Toolkit

## Concetti Teorici

Redux Toolkit (RTK) rappresenta l'approccio ufficiale consigliato per scrivere logica Redux. È progettato per semplificare la scrittura del codice Redux, riducendo il boilerplate e rendendo più facile la gestione dello stato.

### Perché Redux Toolkit?

Tradizionalmente, Redux richiede molto codice boilerplate e configurazioni complesse. Redux Toolkit risolve questi problemi fornendo un set di API per configurare lo store, creare reducer e azioni, gestire le operazioni asincrone e molto altro, in modo più efficiente.

## Redux Toolkit vs Context API

Mentre il Context API di React è un sistema di gestione dello stato incorporato in React per "trasmettere" i dati attraverso l'albero dei componenti, Redux Toolkit offre una soluzione più robusta e scalabile per la gestione dello stato globale in applicazioni più grandi e complesse.

- **Context API** è più adatto per "trasportare" lo stato e logiche semplici attraverso l'albero dei componenti senza l'uso di prop drilling.
- **Redux Toolkit**, invece, offre una soluzione più completa per la gestione dello stato globale, ottimizzando le prestazioni e fornendo potenti strumenti di debugging.


## Esempio Pratico: Counter App

Per illustrare l'uso di Redux Toolkit, creeremo una semplice applicazione counter che incrementa, decrementa e resetta un valore.

### Setup

Per iniziare, installa Redux Toolkit e React Redux nel tuo progetto:

```bash
npm install @reduxjs/toolkit react-redux
```

### Configurazione dello Store

Crea uno store Redux utilizzando `configureStore` fornito da RTK:

```javascript
// src/app/store.js
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from '../features/counter/counterSlice';

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

## Il `preloadedState`

`preloadedState` permette di inizializzare lo store con uno stato definito, utile per ripristinare sessioni utente. 

Esempio:
```javascript
import { configureStore } from '@reduxjs/toolkit';
import rootReducer from './reducers';

const store = configureStore({
  reducer: rootReducer,
  preloadedState: {
    users: [{ id: 1, name: 'John Doe' }],
  },
});
```

In questo esempio, `configureStore` crea uno store con stato iniziale pre-caricato.

### I `middlewares`

Un middleware in Redux è una funzione che intercetta le azioni inviate allo store prima che raggiungano i reducer. Può essere utilizzato per logica asincrona, logging, gestione degli errori e molto altro.

Ecco un esempio semplice di middleware che registra in console l'azione e lo stato corrente:

```javascript
const loggerMiddleware = store => next => action => {
  console.log('Dispatching:', action);
  console.log('Current state:', store.getState());
  const result = next(action);
  console.log('Next state:', store.getState());
  return result;
};
```

Questo middleware utilizza una serie di funzioni annidate per accedere allo store, all'azione successiva da eseguire e all'azione attuale. Logga l'azione corrente e lo stato prima e dopo che l'azione è stata gestita dal reducer.

Per aggiungere un middleware allo store in Redux Toolkit, lo inserisci nell'opzione `middleware` di `configureStore`. Puoi usare `getDefaultMiddleware` per ottenere i middleware predefiniti e poi aggiungere i tuoi personalizzati usando `.concat()`.

Ecco un esempio di configurazione dello store con il middleware personalizzato `loggerMiddleware`:

```javascript
import { configureStore } from '@reduxjs/toolkit';
import loggerMiddleware from './loggerMiddleware';

const store = configureStore({
  reducer: rootReducer,
  middleware: (getDefaultMiddleware) => getDefaultMiddleware().concat(loggerMiddleware),
});
```

In questo esempio, `loggerMiddleware` viene aggiunto ai middleware predefiniti di Redux Toolkit, consentendo di loggare le azioni e lo stato durante il dispatch delle azioni.

### Gli `enhancers`

Gli `enhancers` in Redux sono funzioni che estendono lo store con funzionalità aggiuntive, come il middleware o l'integrazione con strumenti di sviluppo come Redux DevTools. Consentono di avvolgere il metodo createStore per aggiungere nuove capacità. Per esempio, Redux DevTools Extension si utilizza spesso come enhancer per abilitare funzionalità avanzate di debugging direttamente nel browser.  

Un enhancer custom in Redux può essere utilizzato per aggiungere funzionalità extra allo store. Ad esempio, potresti voler tracciare il tempo impiegato da ogni azione per essere completata. Ecco come potresti implementare un enhancer del genere:

```javascript
const timingEnhancer = createStore => (reducer, initialState, enhancer) => {
  const store = createStore(reducer, initialState, enhancer);
  const originalDispatch = store.dispatch;
  
  store.dispatch = (action) => {
    const start = performance.now();
    const result = originalDispatch(action);
    const end = performance.now();
    console.log(`${action.type} executed in ${end - start}ms`);
    return result;
  };

  return store;
};

// Uso con configureStore di Redux Toolkit
const store = configureStore({
  reducer: rootReducer,
  enhancers: [timingEnhancer]
});
```

Questo enhancer misura il tempo di esecuzione di ogni azione e lo stampa in console, fornendo un feedback utile per l'ottimizzazione delle prestazioni. Puoi personalizzare ulteriormente l'enhancer in base alle tue specifiche esigenze.


### Creazione dello Slice

Uno slice rappresenta una porzione dello stato globale e la logica per gestirlo:

```javascript
// src/features/counter/counterSlice.js
import { createSlice } from '@reduxjs/toolkit';

export const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0,
  },
  reducers: {
    increment: state => {
      state.value += 1;
    },
    decrement: state => {
      state.value -= 1;
    },
    reset: state => {
      state.value = 0;
    },
  },
});

export const { increment, decrement, reset } = counterSlice.actions;

export default counterSlice.reducer;
```

### Utilizzo nel Componente

Integra Redux nel tuo componente React utilizzando `useSelector` per leggere lo stato e `useDispatch` per inviare azioni:

```jsx
// src/features/counter/Counter.js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement, reset } from './counterSlice';

export function Counter() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <div>Count: {count}</div>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
      <button onClick={() => dispatch(reset())}>Reset</button>
    </div>
  );
}
```

### Fetching Dati da un'API

`createAsyncThunk` in Redux Toolkit è una funzione progettata per gestire operazioni asincrone all'interno dello store di Redux, come le richieste API. 
Semplifica il processo generando automaticamente tipi di azione e stati del ciclo di vita (in sospeso, completato, rifiutato) per le tue operazioni asincrone, aiutandoti a gestire più efficacemente gli stati di caricamento e gli errori.

Quando utilizzi `createAsyncThunk`, definisci una stringa della tua azione e una funzione creatrice di payload, che è dove risiede la tua logica asincrona. 
Questa funzione può accedere al `dispatch` e `getState` di Redux attraverso il parametro `thunkAPI`, permettendoti di interagire con lo store o di inviare ulteriori azioni se necessario.


```javascript
const fetchPosts = createAsyncThunk(
  'posts/fetchPosts',
  async (thunkAPI) => {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    if (!response.ok) {
      return thunkAPI.rejectWithValue('Errore di rete!');
    }
    return await response.json();
  }
);
```

Il parametro `thunkAPI`, passato alla funzione detta `payloadCreator`, offre accesso a funzioni come dispatch e getState, consentendoti di interagire ulteriormente con lo store Redux all'interno del thunk. Puoi anche utilizzare _thunkAPI.rejectWithValue_ per restituire un payload personalizzato in caso di errore, il che è utile per gestire gli errori in modo più granulare.

Il ciclo di vita di un thunk creato con `createAsyncThunk` coinvolge tre stati:
- **/pending**: Viene inviato quando l'operazione asincrona inizia.
- **/fulfilled**: Viene inviato se l'operazione si completa con successo, con il risultato passato come payload.
- **/rejected**: Viene inviato se l'operazione fallisce, con l'errore passato come payload. Puoi anche usare `thunkAPI.rejectWithValue` per restituire un payload di errore personalizzato.

I reducer possono rispondere a queste azioni utilizzando `extraReducers` in `createSlice`, consentendoti di aggiornare il tuo stato in base al risultato dell'operazione asincrona. Questo approccio consente una gestione pulita e organizzata della logica asincrona in Redux.

Inoltre, `createAsyncThunk` fornisce funzionalità come l'invio condizionale, dove puoi annullare l'operazione prima che inizi in base allo stato corrente o ad altre condizioni, e la gestione degli errori, dove puoi personalizzare il payload dell'errore o gestire gli errori localmente all'interno del componente che ha inviato il thunk.

Per i componenti, puoi inviare un thunk utilizzando `useDispatch` e gestire il suo risultato o gli errori utilizzando il metodo `.unwrap()` sulla promessa restituita. Questo metodo ti consente di lavorare con il risultato o l'errore come se stessi utilizzando una funzione asincrona standard, rendendo più facile integrare operazioni asincrone nei tuoi componenti.


```javascript
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';

export const fetchPosts = createAsyncThunk('posts/fetchPosts', async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  return response.json();
});

const postsSlice = createSlice({
  name: 'posts',
  initialState: {
    posts: [],
    status: 'idle', // 'idle' | 'loading' | 'succeeded' | 'failed'
    error: null,
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchPosts.pending, (state) => {
        state.status = 'loading';
      })
      .addCase(fetchPosts.fulfilled, (state, action) => {
        state.status = 'succeeded';
        state.posts = action.payload;
      })
      .addCase(fetchPosts.rejected, (state, action) => {
       state.status = 'failed';
        state.error = action.error.message;
      });
  },
});

export default postsSlice.reducer;
```

In questo esempio, `createAsyncThunk` viene utilizzato per definire una funzione asincrona `fetchPosts` che esegue il fetch dei dati dall'API. La funzione `createSlice` crea uno slice dello stato che include i reducer e gestisce automaticamente le azioni generate da `createAsyncThunk`, come `pending`, `fulfilled`, e `rejected`, per aggiornare lo stato in base allo stato della richiesta.

L'invio condizionale in `createAsyncThunk` di Redux Toolkit ti permette di eseguire logiche specifiche prima che l'azione asincrona venga effettivamente inviata. Questo è utile per evitare chiamate non necessarie o per controllare se determinate condizioni sono soddisfatte prima di procedere con l'operazione asincrona.

Per esempio, puoi utilizzare la funzione `condition` nell'oggetto `options` di `createAsyncThunk` per determinare se l'azione asincrona deve essere inviata o meno. Questa funzione riceve come argomenti lo stato attuale dello store e tutti gli argomenti passati al thunk, e deve restituire un valore booleano che indica se l'azione deve essere eseguita.

Se la funzione `condition` restituisce `false`, l'invio del thunk viene annullato e nessuna delle azioni del ciclo di vita (pending, fulfilled, rejected) viene inviata. Questo ti permette di saltare l'esecuzione di thunks basati su condizioni specifiche dello stato o su altri criteri.

### In caso di invio condizionale:

```javascript
const fetchPosts = createAsyncThunk('posts/fetchPosts', async (args, thunkAPI) => {
  const { posts } = thunkAPI.getState();
  // Logica per controllare se i post sono già stati caricati
  if (posts.loaded) return;
  // Altrimenti, procedi con il fetch dei post
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  return await response.json();
}, {
  condition: (args, thunkAPI) => {
    const { posts } = thunkAPI.getState();
    // Non inviare se i post sono già stati caricati
    return !posts.loaded;
  }
});
```

### L'utilizzo di `createAction` 

Supponiamo di voler creare un'azione `aggiornaUtente` che accetta un oggetto utente come parametro. Ecco come potresti farlo con `createAction`:

```javascript
import { createAction } from '@reduxjs/toolkit';

// Definizione dell'azione con un parametro
const aggiornaUtente = createAction('utente/aggiorna');

// Creazione di un'azione con un oggetto utente come payload
const azioneAggiornaUtente = aggiornaUtente({ nome: 'Mario', eta: 30 });
console.log(azioneAggiornaUtente);
// Output: { type: 'utente/aggiorna', payload: { nome: 'Mario', eta: 30 } }
```

In questo esempio, l'azione `aggiornaUtente` viene creata con `createAction` e può essere invocata con un oggetto utente come parametro. L'oggetto utente diventa il `payload` dell'azione.

### Configurazione dello Slice

Per gestire l'azione `aggiornaUtente` nello slice, puoi utilizzare `extraReducers` per definire come lo stato dovrebbe cambiare in risposta all'azione. Ecco un esempio di come potrebbe essere configurato uno slice che gestisce l'aggiornamento dell'utente:

```javascript
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  utente: {}
};

const utenteSlice = createSlice({
  name: 'utente',
  initialState,
  reducers: {
    // Reducers per altre azioni possono essere definiti qui
  },
  extraReducers: (builder) => {
    builder.addCase(aggiornaUtente, (state, action) => {
      // Aggiorna lo stato dell'utente con il payload dell'azione
      state.utente = action.payload;
    });
  }
});

export default utenteSlice.reducer;
```

In questo esempio di slice, l'`extraReducer` viene utilizzato per ascoltare l'azione `aggiornaUtente`. Quando l'azione viene inviata, il reducer aggiorna lo stato dell'utente con i dati forniti nel `payload` dell'azione.

Nel caso di `createSlice`, le cose sono ancora più semplificate perché non devi nemmeno usare `createAction` esplicitamente. Quando definisci uno slice, Redux Toolkit crea automaticamente le azioni basate sui reducer che hai definito all'interno dello slice.

Ecco come si presenta:

```javascript
import { createSlice } from '@reduxjs/toolkit';

const contatoreSlice = createSlice({
  name: 'contatore',
  initialState: 0,
  reducers: {
    // Il reducer incrementa direttamente crea l'azione 'contatore/incrementa'
    incrementa: state => state + 1,
  },
});

// Azioni generate automaticamente dallo slice
export const { incrementa } = contatoreSlice.actions;

// Reducer
export default contatoreSlice.reducer;
```

In questo esempio, `createSlice` ha creato un'azione chiamata `incrementa` basata sul reducer `incrementa`. Non è necessario definire esplicitamente l'azione; viene generata automaticamente e può essere esportata e utilizzata nel tuo componente o nel tuo store.


## Redux DevTools

La Redux DevTools è uno strumento di sviluppo indispensabile per le applicazioni Redux, che fornisce potenti funzionalità di debugging. Consente di visualizzare, tracciare e manipolare lo stato e le azioni dell'applicazione in tempo reale. Con RTK, l'uso di Redux DevTools è semplificato e abilitato di default tramite configureStore(), migliorando l'esperienza di sviluppo e aiutando a individuare e risolvere i problemi più rapidamente.

## Conclusione

Redux Toolkit semplifica notevolmente la scrittura e la manutenzione del codice Redux, rendendo più accessibile la gestione dello stato globale nelle applicazioni React. Offre strumenti potenti come `configureStore`, `createSlice`, e `createAsyncThunk` per ridurre il boilerplate, migliorare la leggibilità del codice e facilitare le operazioni asincrone.

Per approfondire i concetti di Redux Toolkit e esplorare altre funzionalità, visita la [documentazione ufficiale di Redux Toolkit](https://redux-toolkit.js.org/).
