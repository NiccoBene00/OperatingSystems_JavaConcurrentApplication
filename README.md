# SISTEMI OPERATIVI - Oral exam 
## Studente: Niccolò Benedetto MAT. 7024656
## Docente: Pierfrancesco Bellini

> [!IMPORTANT]
> La repository contine un unico file .md in cui si risponde alle domande più comuni fatte durante gli esami orali.

**1) Che cosa significa che un sistema operativo è interrupt driven?**

I sitemi operativi "Interrupt Driven" hanno la particolarità di gestire le interruzioni del sistema (dovute a richieste dell'utente, richieste da parte di periferiche, timer, eccezioni)
in maniera sistematica. Differentemente infatti da quei OS che utilizzano il polling, un sistema operativo "interrupt driven" (basato su interrupt) è progettato per rispondere rapidamente a eventi esterni e interni tramite un meccanismo chiamato "interrupt" (interruzione). Gli interrupt sono segnali inviati al processore che indicano che un evento che richiede attenzione immediata è avvenuto. Questo approccio consente al sistema operativo di gestire le risorse in modo efficiente e di rispondere prontamente a situazioni urgenti. Esite una tabella degli interruput che contiene gli indirizzi delle routine di servizio associate ad ogni interrupt.

**2) Cosa sono e come sono gestite le interruzioni sincrone?**

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

**3) Introdurre le chiamate di sistema**

Le chiamate di sistema sono delle richieste che i processi eseguono per avere l'autorizzazione per poter soddisfare operazini tipiche della kernel mode (ad esempio l'allocazione di memoria).
Se ottenuta questa autorizzazione allora i processi possono eseguire le istruzioni associate alla chiamata di sistema eseguita. Ogni tipo di chiamata di sistema e istruzioni associate sono contenute
in una tabella.
Un processo che effettua una chiamata di sistema potrebbe avere la necessità di passare alcuni parametri. Questo passaggio avvine secondo tre diverse modalità:
  - attraverso i regsitri di CPU;
  - attraverso l'indirizzo di memoria in cui viene salvato il parametro;
  - attraverso lo STACK.

**4) Introdurre il concetto di macchina virtuale con particolare riferimento alla JVM**

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

**5) Elencare quali sono i possibili stati in cui può trovarsi un processo dal momento della sua creazione sino alla sua terminazione**

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

**6) Introdurre il Process Control Block**

Il PCB è una struttura dati che contiene le principali informazioni relative ad un processo in esecuzione. Si annoverano il PID (process identificator), lo stato corrente in cui si trova,
il valore del Program Counter (registro che contiene l'indirizzo dell'istruzione corrente), lo stato dei registri della CPU, il numero di cicli di clock eseguiti sono a quel momento per quel processo,
i file utilizzati e letti durante l'esecuzione.

**7) Fornire una panoramiche delle code necessarie per lo scheduling dei processi**

I moderni sistemi operativi dispongono di tre diverse code per la gestione dello scheduling dei processi:
  - Job queue: coda che contiene tutti i processi del sistema, ossia quelli negli stati ready, running o waiting;
  - Ready queue: coda che contiene i soli processi che si trovano nello stato di ready, ossia quei processi che sono in attesa di essere assgnati alla CPU per l'effettiva esecuzione;
  - Device queue: coda che contiene i processi che sono in attesa di un evento di I/O o di altri eventi esterni.

La schedulazione (scheduling) dei processi può essere di due tipologie:
  - schedulazione a lungo termine (job scheduling): os si occupa di assegnare i processi che si trovano nella coda di attesa nella coda di ready, ossia schedula i processi che sono in memoria secondaria
    e hanno necessità di andare in memoria primaria;
  - schedulazione a breve termine (CPU scheduling): os si occupa di assegnare i processi che si trovano nella ready queue alla CPU seguendo una qualche politica di scheduling.

**8) Che cos'è il context switch?**

Il cambio di contesto (o context switch) rappresenta l'operazione di cui si fa carico il processore quando si schedula un processo con un altro. In questo momento infatti la CPU continua a lavorare, ma esegue 
piuttosto operazioni di salvataggio dei registri (si deve salvare infatti lo stato del processi che viene prelazionato e caricare lo stato del nuovo processo) invece che di compiti effettivamente utili. 

**9) Che cos'è un processo zombie?**

Un processo si trova in uno stato di zombie quando questo è un processo figlio che è terminato senza che il processo padre ne abbia richiesto ad esempio il suo valore di ritorno.
Si parla di processo zombie in quanto, nonostante abbia comunque finito di eseguire tutte le istruzioni associate, ha ancora allocato il PCB associato, dunque consumando inutilmente risorse del sistema.


**10) Come avviene la comunicazione tra processi in un sistema operativo?**

L'inter process comunication (IPC) all'interno di un sistema operativo può avvenire secondo due diverse modalità:
  - memoria condivisa: viene creata un zona comune a più processi che necessita di accedere alle stesse informazioni. Questa modalità è indicata quando si vuole scambiare scambiare grandi quantità di dati
    anche tra più di due processi;
  - scambio si messaggi: i processi si scambiano veri e propri messaggi attraverso il kernel. Si utilizza quando si vuole scambiare poche quantità di dati prediligendo l'efficacia oppure quando è necessario
    sincronizzare processi diversi.

**11) Approfondire la comunicazione tra processi mediante scambio di messaggi**

Lo scambio di messaggi prevede l'introduzione di due operazioni quali *send(message)* e *receive(message)* che possono essere eseguite attraverso una duplice modalità:
  - comunicazione diretta: si deve conoscere il PID del mittente e del ricevete, dunque le operazioni vengono così modificate *send(P, message)* e *receive(P, message)*. Questa modalità consente
    dunque la comunicazione tra soli due processi alla volta e può essere implementata in maniera unidirezionale o bidirezionale;
  - comunicazione indiretta: in questo caso il sistema operativo apre una porta di comunicazione identificata da un ID. Tutti i processi che conoscono l'ID della porta possono sfruttarla attraverso le
    operazioni *send(IDPort, message)* e *receive(IDPort, message)*. Si osservi che quando la porta è condivisa tra più processi si deve determinare anche come gestire la ricezione dei messaggi.

**12) Esplicitare la potenzialità di un sistema multithread**

In un sistema monothread il sistema operativo è in grado di eseguire le istruzioni dei processi come se fosse una sola unica sequenza di istruzioni, non andando così a sfruttare le reale potenza dei processori
di oggi. Con l'introduzione invece del multithreading, la stessa sequenza di istruzioni può essere eseguita parallelamente (si parla di parallelismo finto nei sistemi monoprocessore e parallelismo reale in 
quelli multiprocessore).
I thrad possono essere distinti in user thread e kernel thread: i primi svolgono operazioni di base, gli altri operazioni a livello kernel.
La relazione che sussiste tra le due tipologie di thread può essere implementata secondo tre diverse configurazioni:
  - molti a uno: più user thread sono gestiti da un unico kernel thrad. Si tratta della modalità che deve essere presa in considerazione quando si dispone di sistemi monoprocessore. Tuttavia
    quando uno user thread effettua una chiamata bloccante, il kernel thread deve necessariamente bloccare l'esecuzione degli altri user thread;
  - uno a uno: un unico user thread è gestito da un unico kenel thread. Un'ipotetica chiamata bloccante non interferisce con gli altri user thread, tuttavia questa modalità offre un limitato grado di
    multiprogrammazione legato al numero di processori nel sistema;
  - molti a molti: si hanno N user thread gestiti da M kernel thread. Questa è la configurazione che, se possibile applicare, permette di ottimizzare l'utilizzo delle risorse dell'elaboratore. 


**13) Dettagliare lo scheduling LINUX**

Nel mondo UNIX ad ogni processo vengono assegante due tipi di priorità: una statica e una dinamica. La prima è rappresentata dal *nice value*, un valore fisso che decreta la priorità generale del processo, mentre
la seconda può appunto variare nel tempo ed è o assegnata manualmente dall'utente oppure direttamente dal kernel.
La schedulazione della CPU è basata sul concetto di epoca: ogni volta prima di ogni epoca si seleziona il set dei processi che deve essere eseguito e si determinano, per ogni processo, i quanti di tempi da assegnare. Una volta che un processo ha terminato i propri quanti di tempo, viene messo in attesa sino alla prossima epoca. La scelta dei quanti si basa sulla "goodness", una particolare funzione che restituisce 
per il processo in questione un quantificatore in relazione al rapporto tra l'utilizzo della CPU del processo stesso e il suo *nice value*.

Con il Linux Scheduler O(1) si fa in modo che la schedulazone dei processi avvenga sempre secondo una tempistica costante, e quindi non relazionata al numero dei processi ready in quell'istante. Ad ogni processo può essere assegnato un livello di priorità che varia tra 0 (priorità max) e 139 (priorità min). Sono presenti due code FIFO (First-In-First-Out) per ogni livello di priorità: una, detta "active queue", che accoda i processi che non hanno ancora terminato i loro rispettivi quanti, e l'altra, detta "expired queue", che contiene i processi che invece hanno terminato il quanto. Lo scheduler semplicemente sceglie tra i processi presenti nella "active queue" quello a priorità più alta, quindi gli assegna la CPU. Quando tutte le "active queue" sono vuote allora viene effettuato uno scambio: le "expired queue" diventano "active queue" e viceversa. Per favorire quei processi che, per motivi di priorità, hanno programmato un alto tasso di utilizzo della CPU, ma per la maggior parte dell'epoca si trovano in I/0 perchè, ad esempio prelazionati da altri processi a priorità maggiore, è stato pensato implementare una funzionalità di bonus, ossia un incremento del valore di priorità. In genere questo incremento varia nel range [-5;+5].

Con le ultime versione di Linux, è stato introdotto il "Linux Completely Fair Scheduler", un nuovo schedulatore che assegna dinamicamente la CPU ai processi, utilizzando un'organizzazione di questi medianta una struttura ad albero red-black per garantire un aggiornamento efficiente e una ricerca computazionale O(log2 n). Il livello di priorità viene aggiornato in relazione al valore del *nice value* e il tempo di utilizzo della CPU.  

**14) Esplicitare il problema dell'inversione di priorità**

Si tratta di uno scenario che si verifica quando un processo a bassa priorità (L = low) possiede una risorsa R, risorsa che è richiesta da un altro processo a più alta priorità (H = high). Si ha inversione di priorità quando un terzo processo a più bassa priorità di H, ma comunque più alta di L (M = medium) prelaziona L, senza l'urgente necessità di richiedere R. In questo caso l'ordine di esecuzione dei processi sarebbe infatti M-L-H.
Una soluzione a questo scenario è da trovarsi nell'innalzamento temporaneo della priorità: i.e. si alza il livello della priorità di L almemo quanto la priorità di H.

**15) Che cosa si intende per stallo (o deadlocks) di un insieme di processi? Come lo gestisce un sistema operativo?**

Quando in un insieme di processi si crea il particolare scenario in cui un processo richiede una risorsa già allocata per un altro processo che a sua volta richiede una risorsa allocata per il primo processo si incorre nella sitazione di deadlock, ossia entrambi i processi si mettono in attesa indefinita in quanto il sistema non è in grado di soddisfare le loro richieste.
I sistemi operativi gestiscono la situazione di stallo usufruendo di 3 diverse tecniche:
  - prevenzione: mira a garantire che la situazione sopra descritta non si verifichi mai. Questo risultato può essere raggiungo imponendo che quando un processo richiede una risorsa non ne abbia una già allocata, oppure che rilasci tutte quelle che già possiede nel momento in cui effettua una nuova richiesta;
  - rilevamento e recupero: il sistema operativo verifica periodicamente se l'insieme dei processi non avanza nel soddisfacimento delle richieste, dunque applica un meccanismo di recupero dello stato totale dei      processi (rollback dello stato) prima del verificarsi di questo scenario. Il tutto richiede una gestione sofisticata degli stati e può comportare un ritardo nell'esecuzione delle operazioni;
  - ignorare il problema: gran parte dei sistemi operativi moderni passano sopra la problematica di stallo delegando il tutto alle applicazioni interessate.

**16) Come si implementa la tecnica di allocazione contigua della memoria?**

Partendo dal presupposto che ad ogni processo il sistema operativo assegna una porzione di memoria abbastanza ampia da poterlo contenere, un processo dunque è definito attraverso un intervallo di memoria (base + limite). Quando effettivamente il processo richiede l'accesso in memoria il MMU (Memory Management Unit) somma l'offset richiesto alla base del processo in questione e se non viene superato il limite allora la richiesta di accesso può essere soddisfatta altrimenti gli viene negato l'accesso.
Quando poi il processo termina allora viene liberata la memoria da esso occupata: si viene quindi a creare un "buco di memoria". Questo buco non è altro che memoria libera allocabile per nuovi processi. L'allocazione contigua prevede tre diversi criteri di rimepimento: 
  - first fit: si alloca il primo buco capace di contenere il processo;
  - best fit: si alloca il buco più piccolo capace di contenere il processo;
  - worst fit: si alloca il buco più grande per il nuovo processo.
Indubbiamente l'approccio più efficiente è il best fit, ma richiede tempo e risorse computazionali. Inoltre genera il problema della frammentazione. Si parla di frammentazione esterna quando si vengono a creare tanti porzioni di memoria libera (tanti buchi) dove nessuno è in grado di contenere il nuovo processo (non è detto che la somma di tutti questi piccoli buchi sia ancora non sufficiente per contenerlo). Una possibile soluzione è l'operazione di compattazione: il sistema operativo riordina le aree di memoria libera in modo da crearne un unico blocco. Si tratta di un'operazione onerosa e costosa.
Si parla invece di frammentazione interna quando un processo occupa solo una minima parte dell'area di memoria assegnata.

**17) Parlare della paginazione**

Nei sistemi operativi con gestione della memoria basata sulla paginazione gli indirizzi logici (indirizzi generati dalla CPU che permettono ai processi di utilizzare uno spazio di indirizzamento continuo e isolati indipendentemente dalla reale disposizione fisica delle memoria) sono suddivisi in pagine, mentre gli indirizzi fisici (è il risultato della mappatura del MMU che riceve in input un indirizzo logico) sono suddivisi in frame. Pagine e frame hanno la stesso lunghezza (in genere una potenza del due), ma non è detto che alla prima pagina corrisponda il primo frame, bensì possono essere assegnati in manier flessibile in relazione alla necessità della memoria. Per gestire l'associazione tra pagine e frame ad ogni processo è assegnata una tabella delle pagine che appunto mappa le pagine nei frame relativi. Inoltre ad ogni pagina è affiancato un bit di validità, che indica se quella pagina è già stata utilizzata o meno.
Per gestire in maniera efficiente l'utilizzazione della memoria la paginazione sfrutta tre diversi approcci:
  - paginazione gerarchica: suddivide la struttura della tabella delle pagine in più livelli gerarchici, garantendo efficienza anche nella gestione di grandi spazi di indirizzamento;
  - paginazione con tabelle hash: la mappatura che la tabella delle pagine esegue tra pagine e frame è implementata mediante utilizzo di una tabella hash. In genere questo approccio viene considerato quando
    si hanno indirizzi maggiori di 32 bit, ossia quando la tabella delle pagine raggiunge dimensioni proibitive;
  - paginazione invertita: si utilizza una singola tabella delle pagine, anzichè una tabella per ogni processo. In questo caso l'indirizzo logico è composto da un identificare del processo, il numero di pagina e     l'offset. E' un metodo efficiente per quanto riguarda l'utilizzo della memoria, tuttavia rende difficile la condivisione di pagine tra processi.

**18) Dare un panoramica completa del concetto di memoria virtuale **

Quando si parla di memoria virtuale si fa riferimento alla tecnica utilizzata dal sistema operativo che simula un aumento di memoria primaria nei confronti della macchina fisica. Se infatti all'accensione la memoria RAM è libera, via via con l'accumolarsi dei processi in esecuzione questa non impiega troppo tempo a pienarsi (specialmente nelle macchine con RAM ridotte) generando errori di memoria. I moderni sistemi operativi implementano la memoria virtuale attraverso la paginazione su richiesta. Questa politica definisce quando e come si debba portare una pagina che è memorizzata su disco (memoria secondaria) nella RAM (memoria primaria). E' necessario ogniqualvotla si esegua questa operazione verificare il bit di validità della pagina in entrata: se infatti questo è settato ad 1 allora tale pagina è già presente. Invece la pagina che deve essere sostituita viene scelta attraverso tre diversi criteri:
  - FIFO: la pagina più vecchia caricata in RAM è anche la prima che viene prelazionata per far spazio alla nuova pagina. Questa politica non è ottimale in quanto introduce la problematica di Belady, per alcune      sequenze di processi l'aumento dei frame aumenta il numero di accessi in RAM, generando di conseguenza un maggior tasso di page fault;
  - sostituzione ottimale: viene rimossa la pagina che sarà utilizzata nel futuro più lontanto. Questa politica tuttavia richiede un livello di conoscenza da parte del sistema operativo circa il comportamento
    futuro di ogni processi e dunque, anche se ottimale, non sempre è raggiungibile;
  - LRU (Least Recently Used): viene rimossa la pagina che non è stata utilizzata per più tempo. In genere questa tecnica prevede di associare ad ogni processo uno stack o un contatore.
    Si tratta ancora una volta però di un'implementazione rigorosa e onerosa in termini computazionali, quindi i moderni sistemi operativi si affidano a una sua versione semplificiata conosciuta come pseudo LRU:     ogni volta che una pagina è utilizzata viene settato un bit di validità, quindi si vanno a sostiuire quelle pagine che hanno tale bit a zero.

**19) Che cos'è il trashing?**

Il trashing è un problema che affligge la tecnica di paginazione su richiesta. Potrebbe infatti verificarsi il tipico scenario in cui la risorsa CPU sia prettamente occupata nel continuo trasferimento di pagina dalla memoria secondaria alla primaria e viceversa, invece che nell'effettiva esecuzione dei processi. Un tale scenario porta a un calo dell'utilizzo della CPU, calo che potrebbe essere inteso dallo stesso processore come indice di terminazione di alcuni processi, e ciò avrebbe come ripercussione l'accodarsi di ulteriori processi pronti. Una soluzione sarebbe quella di importare in memoria l'intero working set di ogni processo. Con working set si intende l'insieme di tutte le pagine che vengono utilizzate attivamente da un processo nel corso di tutto il suo ciclo di vita. Sebbene si riveli un'ottima soluzione, non sempre è attuabile in quanto bisogna tener presente che vi sono processi con working set veramente grandi.

**20) Che cos'è il componente hw DMAC?**

Con la sigla DMAC (Direct Memory Access Controller) si fa riferimento ad un componente hardware che permette l'accesso delle periferiche del sistema elaboratore senza il coinvolgimento diretto della risorsa processora, risorse che dunque sarà impiegata su altre attività prioritarie consentendo il trasferimento di dati in background. 
