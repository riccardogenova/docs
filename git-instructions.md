# Cos'è Git e a cosa serve

Git è un sistema gratuito ed open source che rientra nella categoria dei **VCS (Version Control System)**. Permette di tenere traccia delle modifiche apportate ai files di un progetto nel corso del tempo. L'architettura distribuita di Git consente di mantenere un repository locale dei files su cui si potrà lavorare indipendentemente dagli altri utenti, e un repository remoto a cui tutti gli utenti fanno riferimento.

# Terminologia

- **Repository**: la copia sincronizzabile della directory principale del progetto. Servizi come Github mettono a disposizione un hosting per i repository, permettendo di controllare gli accessi e agevolando il lavoro in team.

- **Commit**: letteralmente **consegnare**, è l'elenco delle modifiche effettuate a un progetto e validate. Git assegna una stringa di numeri e lettere a ogni commit in modo che sia tracciabile.

- **Push e Pull**: comandi che servono per inviare e ricevere gli aggiornamenti. Il push invierà i tuoi commit al repository principale, il pull chiederà a
  quest'ultimo di poter scaricare le modifiche sul tuo repository locale e unirle ai tuoi file.

- **Fetch**: è il comando che dice a Git di recuperare il
  contenuto di un repository.

- **Merge**: è l’unione tra commit di branch differenti.

- **Branch**: indica una versione del tuo repository contenente uno o
  più commit non presenti nella versione “originale”.
  In Git, infatti, abbiamo un “ramo” principale chiamato **master** che raccoglie tutti commit dei file del tuo
  progetto. Può succedere tuttavia che sia necessario creare un ramo nuovo per testare delle versioni diverse di
  uno o più file del progetto. In questo caso creeremo un branch, (assegnandogli anche un nome identificativo)
  che conterrà tutti i commit delle modifiche ai file.

- **HEAD**: il branch di lavoro attuale. Più precisamente, HEAD è la referenza all’ultimo commit di un
  ramo di lavoro di un branch al quale si sta lavorando.

- **_Git Bush_**
- _Comandi di utilizzo:_
- **Git checkout**: scartiamo modifiche che abbiamo in locale che ancora non abbiamo etichettato.
- **Git diff + name**: modifiche fatte in un file/ hash.
- **Git reset + commit hash**: resettare ad un commit specifico.
- **Git status**: lo stato del git locale.
- **Git add**: si utilizza per tracciare uno o piu' file.
- **Git commit -m**: "...." comando unico per scrivere sulla stessa riga la descrizione dell'etichetta.
- **Git config user.email "lorenzo.santangelo@" --global**: ci permette di mette l'email, e di modificare il file a livello globale.
- **Git log**: da la lista dei commit locali.
- **Git push**: carica in remoto le modifiche effettuate.
- **Git push (origin) nome del branch (main/master)**:
