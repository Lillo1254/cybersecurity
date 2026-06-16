# Project management
Il project management è l'applicazione delle conoscenze e si sviluppa su 3 punto fondamentali **l'ambito che definisce il lavoro necesario per raggiungere gli obiettivi, il tempo tramite pianificazioni di scadenze e delle attività, e il costo per la gestione del budget e delle risorse necessarie sia finanziarie che umane**.

## le 5 fasi del ciclo di vita
Un progetto si sviluppa tramite 5 fasi standar definite dal project management instistute (PMI) 

**avvio** => Definizione dell'idea e nomina del project manager e autorizzazione formale Stakeholder Analysis identificano non solo i beneficiari, ma anche chi potrebbe essere un "attaccante" o chi è responsabile della conformità (DPO, CISO) High-Level Risk Assessment valuta se il progetto espone l'azienda a rischi critici

**Pianificazione** => creazione del piano d'azione definizione dei tempi e allocazione delle risorse Si pianifica già cosa fare se qualcosa va storto durante lo sviluppo o dopo il rilascio

**esecuzione** Sviluppo Sicuro: Se il progetto è software, gli sviluppatori scrivono codice seguendo standard come OWASP Gestione degli accessi: Si applica il principio del "minimo privilegio" (nessuno ha più permessi di quelli strettamente necessari per lavorare)

**monitoraggio e controllo** Questa fase corre in parallelo all'esecuzione. Non si controllano solo tempi e costi, ma anche la postura di sicurezza Vulnerability Scanning: Test continui per trovare falle appena create Audit di conformità: Verificare che ciò che si sta costruendo rispetti ancora le normative (GDPR, NIST, ecc.) Change Management: Ogni modifica al progetto deve essere analizzata per capire se introduce nuove vulnerabilità

**chiusura** Il progetto finisce, ma la sicurezza continua Handover alla Security Operations: Si passano le "chiavi" del progetto al team che si occuperà della manutenzione e del monitoraggio post-rilascio (SOC) Dismissione sicura: Se il progetto sostituisce un vecchio sistema, i dati precedenti devono essere cancellati in modo sicuro (Data Wiping)

## I pilastri e le aree di gestione
Per gestire un progetto in modo efficace un project manager deve presidiare diverse aree

**risorse** => gestione delle persone (team) dei materiali e delle tecnologie

**comunicazione** => allineamento costante tra il team e gli stakeholder

**rischi** => identificazione e gestione dei potenziali problemi che potrebbero ostacolare il progetto

**qualità** => controllo che il risultato soddisfi gli standard richiesti

## metodologie principale

**waterfall (cascata)** => approccio tradizionale e lineare dove ogni fase inizia solo al termine della precedente

**Agile** metodo iterativo e flessibile ideale per progetto in cui i requisiti possono cambiare rapidamente

**Il Business Case è il documento fondamentale della fase di Avvio. In ambito Cyber Security, però, non serve solo a giustificare una spesa, ma a dimostrare che l'investimento protegge il valore dell'azienda Se il Business Case è il "perché" facciamo il progetto, il Project Charter è l'atto di nascita ufficiale. È il documento, emesso nella fase di Avvio, che conferisce al Project Manager l'autorità di utilizzare le risorse aziendali**

# Il diagramma di Gantt
Il diagramma di Gantt è uno degli strumenti più importanti nel project management, e in cyber security diventa fondamentale per pianificare attività tecniche, dipendenze, controlli di sicurezza e milestone critiche.

Sintesi operativa
Un Gantt rappresenta visivamente:
- attività del progetto
- durata
- dipendenze
- responsabilità
- stato di avanzamento

Nel contesto cyber security serve per coordinare attività come risk assessment, vulnerability management, test di sicurezza, audit, deployment sicuro, incident response readiness. a sicurezza non è un’attività isolata: va distribuita lungo tutto il progetto inizialmente inserire attività di risk assessment e security requirements Definire dipendenze Pianificare threat modeling prima dello sviluppo Collegare dipendenze tra architettura e controlli di sicurezza in fase di sviluppo Inserire cicli di code review e analisi statica Collegare attività di sviluppo a test di sicurezza incrementali durante il Testing Pianificare VA/PT con buffer per remediation Prevedere milestone di approvazione sicurezza dal deployment e l'operatività Attività di hardening, configurazioni sicure, monitoraggio Pianificare esercitazioni di incident response

## Stakeholder nel progetto
In un progetto gli stakeholder sono tutte le persone o entità che hanno un interesse, un impatto o una responsabilità rispetto al progetto Nel contesto cyber security, gli stakeholder non sono solo tecnici: includono management, utenti, fornitori, compliance, legali e team operativi

Gli stakeholder sono:
- Soggetti che influenzano il progetto
- Soggetti che subiscono l’impatto del progetto
- Soggetti che devono approvare o controllare il progetto

Sono fondamentali perché definiscono requisiti, vincoli, priorità, budget e rischi e si dividono in stakeholder interni ed esterni

## Stakeholder interni
**Executive Sponsor**  
- Responsabile del budget e dell’approvazione strategica

**Project Manager**
- Coordina attività, risorse, tempi, rischi

**Team IT**  
- Amministratori di rete, sistemisti, sviluppatori.

**Security Team / SOC ** 
- Definisce controlli, monitora, valida sicurezza.

**Compliance / Legal**  
- Garantisce rispetto di normative (GDPR, ISO 27001).

**Data Owner e Data Custodian**  
- Proprietari e gestori dei dati coinvolti.

## Stakeholder esterni
**Fornitori**  
- Vendor di software, cloud provider, MSSP.

**Clienti o utenti finali**  
- Utilizzano il sistema e subiscono l’impatto delle misure di sicurezza.

**Autorità o enti regolatori**  
- Impongono standard e verificano la conformità.

# WBS (Work Breakdown Structure)
La WBS (Work Breakdown Structure) è uno degli strumenti fondamentali del project management, soprattutto nei progetti di cyber security, perché permette di scomporre il lavoro in parti chiare, gestibili e assegnabili Serve a definire tutto ciò che deve essere fatto evitare attività mancanti o duplicate assegnare responsabilità stimare tempi e costi costruire Gantt, RACI, budget e risk assessment

La WBS è organizzata in livelli:
- Livello 1 – Progetto
- Livello 2 – Fasi principali
- Livello 3 – Deliverable
- Livello 4 – Attività
- Livello 5 – Task operativi

## Matrice RACI
La matrice RACI è uno degli strumenti più importanti del project management, soprattutto nei progetti di cyber security, perché chiarisce chi fa cosa, chi decide, chi supporta e chi deve essere informato

RACI è un acronimo che indica quattro ruoli:
- R – Responsible  
    - Chi esegue operativamente il task.
- A – Accountable  
    - Chi è responsabile finale del risultato e approva.
- C – Consulted  
    - Chi deve essere consultato prima dell’esecuzione.
- I – Informed  
    - Chi deve essere informato dell’avanzamento o dell’esito.

**La sicurezza coinvolge molti attori diversi: IT, SOC, compliance, legal, management, utenti** Senza una matrice RACI le attività critiche non hanno un responsabile chiaro i controlli di sicurezza vengono ignorati si creano conflitti tra team si rallenta il progetto si rischiano non conformità (GDPR, ISO 27001) La RACI elimina queste ambiguità