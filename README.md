# SISTEMI OPERATIVI - Oral exam 
## Studente: Niccolò Benedetto MAT. 7024656
## Docente: Pierfrancesco Bellini

> [!IMPORTANT]
> La repository contine un unico file .md in cui si risponde alle domande più comuni fatte durante gli esami orali.

*1) Introdurre il concetto di Interrupt Driven di un Sistema Operativo*

I sitemi operativi "Interrupt Driven" hanno la particolarità di gestire le interruzioni del sistema (dovute a richieste dell'utente, richieste da parte di periferiche, timer, eccezioni)
in maniera sistematica. Differentemente infatti da quei OS che utilizzano il polling, questi appena rilevata un'interruzione la confrontano con un interrupt vector che appunto contiene
gli indirizzi delle routine di servizio associate. Non si ricorre dunque a nessun tipo di ciclo per il controllo periodico dell'evento interruzione, risparmiando così perdita di tempo 
inutile.

*2) Cosa sono e come sono gestite le interruzioni sincrone*

Le interruzioni sincrone sono eventi che si verificano in modo correlato e sincronizzato con l'esecuzione del programma. Questo significa che avvengono in momenti specifici del flusso e
direttamente collegate alle operazioni in corso. Le tre più comuni forme di interruzioni sincrone sono:
  - loop infiniti;
  - accessi a zone di memoria errate;
  - accessi concorrenti alla stessa zone di memoria (si pensi al caso in cui alcuni processi vogliano scrivere in un particalore indirizzo di memoria che allo stesso tempo è letto da altri
    processi);

Gli ultimi due casi sono gestiti attraverso l'introduzione di una duplicità modalità di utilizzo del sistema opertivo: la user e la kernel mode. Se la user mode è accessibile dall'utente che può
eseguire funzionalità di base, la kernel mode è direttamente accessibile dall'OS e permette il dialogo con tutte le risorse hw del sistema.
Il primo caso invece viene risolto attraverso l'introduzione di un particolare timer, che ad intervalli regolari "risveglia" il sistema per un check: se viene riconosciuto un ciclo infinito allora
si tenta di uscirne (break), altrimenti si il timer viene resettato e il sistema continua con l'esecuzione delle istruzioni.

*3) Introdurre le chiamate di sistema*

Le chiamate di sistema sono delle richieste che i processi eseguono per avere l'autorizzazione per poter soddisfare operazini tipiche della kernel mode (ad esempio l'allocazione di memoria).
Se ottenuta questa autorizzazione allora i processi possono eseguire le istruzioni associate alla chiamata di sistema eseguita. Ogni tipo di chiamata di sistema e istruzioni associate sono contenute
in una tabella.
Un processo che effettua una chiamata di sistema potrebbe avere la necessità di passare alcuni parametri. Questo passaggio avvine secondo tre diverse modalità:
  - attraverso i regsitri di CPU;
  - attraverso l'indirizzo di memoria in cui viene salvato il parametro;
  - attraverso lo STACK.

*4) Introdurre il concetto di macchina virtuale con particolare riferimento alla JVM*

Una macchina virtuale è un'astrazione che permette di ottenere una sorta di "computer virtuale" dentro un elaboratore fisico. Questa tecnica offre quindi la possibilità di disporre di più sistemi 
operativi sullo stesso hardware. Ovviamene più macchine virtuali si installano su uno stesso sistema maggiore alternanza nell'utilizzo di CPU si avrà, visto che se ne dispone di un numero limitato 
su ogni elaboratore.
La particolarità però è che ogni macchina virtuale percepisce di possedere il proprio kernel e di essere completamente separata dalle altre, fornendo quindi un ambiente isolato e autonomo per l'esecuzione dei processi e delle applicazioni al suo interno.
La Java Virtual Machine (JVM) ha la particolare caratteristica di permette l'esecuzione di programmi JAVA su qualsiasi macchina fisica. Infatti la JVM è responsabile dell'esecuzione del bytecode, ovvero quel 
formato di linguaggio intermedio tra il codice sorgente scritto dal programmatore e il linguaggio macchina, che viene generato a seguito della compilazione del file sorgente. Si riportino le principali
caratteristiche della JVM:
  - Indipendenza dalla piattaforma: una volta compilato, il bytecode può essere eseguito su qualsiasi piattaforma disponga di una JVM senza la necessità di ricompilazione;
  - Garbage Collector: è direttemente implementato un meccanismo che gestisce l'allocazione e la deallocazione della memoria (prevenzione dai memory leaks)
  - Sicurezza: sono già presenti meccanismo di sicurezza che effettua il controllo delle istruzioni bytecode;
  - Gestione delle eccezioni;
  - Compilazione JIT: la compilazione Just-In-Time permette di compilare il bytecode in codice macchina nativo direttmante durante l'esecuzione del programma;
  - Supporto per multithreading: modulo che consente la creazione e la gestione di thread all'interno dello stesso programma JAVA, consentendo così il supporto di applicazioni concorrenti e parallele.

*5) Elencare quali sono i possibili stati in cui può trovarsi un processo dal momento della sua creazione sino alla sua terminazione*

Durante il proprio ciclo di vita un processo può trovarsi in diversi cinque stati:
  - "new": il processo è stato creato, ma ancora non ha eseguito la sua prima istruzione. Deve infatti ancora ottenere le risorse necessarie.
  - "ready": il processo ha acquisito tutte le risorse necessarie eccetto la CPU;
  - "running": il processo è attualmente in esecuzione sulla CPU;
  - "waiting": il processo è in atteso di un qualche tipo di evente per continuare la sua esecuzione (I/0 ad esempio);
  - "terminated": il processo ha terminato l'esecuzione di tutte le istruzioni, quindi si rilasciano le risorse acquisite.

I possibili passaggi consentiti tra questi cinque stati sono:
  - da "new" a "ready";
  - da "ready" a "running";
  - da "running" a "terminated";
  - da "running" a "waiting";
  - da "waiting" a "ready"; 
  - da "running" a "ready";

*6) Introdurre il Process Control Block*

Il PCB è una struttura dati che contiene le principali informazioni relative ad un processo in esecuzione. Si annoverano il PID (process identificator), lo stato corrente in cui si trova,
il valore del Program Counter (registro che contiene l'indirizzo dell'istruzione corrente), lo stato dei registri della CPU, il numero di cicli di clock eseguiti sono a quel momento per quel processo,
i file utilizzati e letti durante l'esecuzione.

*7) Fornire una panoramiche delle code necessarie per lo scheduling dei processi*

I moderni sistemi operativi dispongono di tre diverse code per la gestione dello scheduling dei processi:
  - Job queue: coda che contiene tutti i processi del sistema, ossia quelli negli stati ready, running o waiting;
  - Ready queue: coda che contiene i soli processi che si trovano nello stato di ready, ossia quei processi che sono in attesa di essere assgnati alla CPU per l'effettiva esecuzione;
  - Device queue: coda che contiene i processi che sono in attesa di un evento di I/O o di altri eventi esterni.

La schedulazione (scheduling) dei processi può essere di due tipologie:
  - schedulazione a lungo termine (job scheduling): os si occupa di assegnare i processi che si trovano nella coda di attesa nella coda di ready, ossia schedula i processi che sono in memoria secondaria
    e hanno necessità di andare in memoria primaria;
  - schedulazione a breve termine (CPU scheduling): os si occupa di assegnare i processi che si trovano nella ready queue alla CPU seguendo una qualche politica di scheduling.

*8) Che cos'è il context switch?*

Il cambio di contesto (o context switch) rappresenta l'operazione di cui si fa carico il processore quando si schedula un processo con un altro. In questo momento infatti la CPU continua a lavorare, ma esegue 
piuttosto operazioni di salvataggio dei registri (si deve salvare infatti lo stato del processi che viene prelazionato e caricare lo stato del nuovo processo) invece che di compiti effettivamente utili. 

*9) Che cos'è un processo zombie?*

Un processo si trova in uno stato di zombie quando questo è un processo figlio che è terminato senza che il processo padre ne abbia richiesto ad esempio il suo valore di ritorno.
