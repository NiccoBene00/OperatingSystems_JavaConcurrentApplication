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

