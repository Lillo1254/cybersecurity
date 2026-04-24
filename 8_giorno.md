# Disaster Recovery
Il Disaster Recovery è l’insieme di politiche, tecnologie e procedure che permettono a un’organizzazione di ripristinare rapidamente sistemi e dati dopo un evento critico causate da errori umani, guasti hardware, cyberattacchi, blackout o disastri naturali, riducendo al minimo downtime e perdita di informazioni.

Definisce:
- quali applicazioni sono mission‑critical
- quanto downtime è accettabile
- quanta perdita di dati è tollerabile
- quali risorse (server, storage, rete, cloud) devono essere disponibili per il ripristino

Ed è composto da:
- Piano di Disaster Recovery un documento che descrive ruoli, responsabilità, priorità e procedure di ripristino.
- Backup e replica dei dati di copie locali, remote o in cloud, con strategie di failover/failback
- Infrastruttura alternativa decentralizzata come data center secondario, cloud di emergenza, sistemi ridondati
- Test periodici con simulazioni per verificare tempi reali e correggere eventuali criticità
  
Due metriche chiave guidano ogni strategia di Disaster Recovery:
- RTO (Recovery Time Objective): tempo massimo accettabile per ripristinare un servizio.
- RPO (Recovery Point Objective): quantità massima di dati che si può perdere (es. ultimi 15 minuti).

**Un’interruzione non pianificata può costare centinaia di migliaia di dollari all’ora, oltre a danni reputazionali e sanzioni normative. In settori critici (sanità, finanza, energia) tempi di ripristino troppo lunghi possono avere impatti gravissimi. Il Disaster Recovery nasce dall'esigenza di proteggere dati e infrastrutture in conformita con la DPIA riducende i tempi di fermo, garantendo la continuità operativa, conforme al GDPR ISO 27001 ed aumenta la resilienza complessiva dell'organizzazione. Il Disaster Recovery è legato anche al Business Continuity che pero riguarda internamente l'azienda per la continuità dei processi, adempimento dei dovere verso le persone, comunicazioni e sedi questa pianificazione è legata anche al service level agreement SLA**

# Cold Site
È il livello più economico e il più lento da attivare ha una Struttura fisica disponibile (edificio, rete elettrica, connettività) , Nessun hardware installato o solo minimo, Nessun dato replicato in tempo reale, Richiede tempo per installare server, configurare sistemi, ripristinare backup ha costi di mantenimento molto bassi utilizzato da aziende che non richiedono un RTO basso proprio per questi motivi di funzionamento ha un RTO molto lungo richiede un intervento manuale massiccio ed il rischio operativo è elevato

# Warm Site
È un compromesso tra costi e velocità di ripristino composto da Hardware presente e configurato, ma non sempre attivo, Dati replicati periodicamente, non in tempo reale, Alcuni servizi pronti, altri da avviare manualmente ed ha un RTO medio (ore), è un buon equilibrio tra costi e resilienza ovviamente non garantisce zero perdita di dati e richiede comunque intervento umano

# Hot Site
È la soluzione più costosa ma anche la più veloce e resiliente composto da un Infrastruttura completamente attiva e sincronizzata, Replica in tempo reale dei dati (RPO ≈ 0), Sistemi pronti al failover immediato , Continuità quasi totale Ideale per servizi mission‑critical ovviamente ha un Costo elevato (hardware, licenze, replica continua) e richiede gestione costante

# Cluster di Failover
Un Cluster di Failover è un insieme di server che lavorano insieme per garantire che un servizio rimanga sempre disponibile, anche se uno dei nodi si guasta È una delle tecnologie più importanti nella Business Continuity e nel Disaster Recovery perché elimina il Single Point of Failure

Un cluster di failover è composto da:

- 2 o più nodi (server fisici o virtuali)
- Storage condiviso o replica dei dati
- Un sistema di monitoraggio che verifica lo stato dei nodi
- Un meccanismo di failover automatico

**Se un nodo primario smette di funzionare, un nodo secondario subentra automaticamente, mantenendo attivi servizi e applicazioni**

**Failover nel cluster**

1) Il nodo attivo eroga il servizio (database, VM, applicazione, file server).
2) Il cluster monitora costantemente lo stato dei nodi.
3) Se rileva un guasto (hardware, software, rete):
4) esegue il failover
5) sposta il servizio su un nodo sano
- L’utente finale spesso non si accorge del passaggio.

## Tipologie di Cluster di Failover

1) Active–Passive
   
- Un nodo lavora, l’altro è in standby.
- Il failover avviene solo in caso di guasto.
- Più semplice e meno costoso.

2) Active–Active
   
- Tutti i nodi lavorano contemporaneamente.
- Carico distribuito e failover immediato.
- Richiede configurazioni più complesse.

3) N+1 / N+M
   
- N nodi attivi + 1 o più nodi di riserva.
- Usato in ambienti enterprise ad alta scalabilità.

# I Dati
I dati sono informazioni grezze, non ancora interpretate, che possono essere raccolte, archiviate, elaborate o trasmesse da un sistema informatico sono la base di ogni processo digitale: senza dati, nessun software, algoritmo o servizio può funzionare

## Tipologia di Dati
1) Dati Strutturati
   
- Organizzati in tabelle, righe e colonne
- Facili da cercare, ordinare, analizzare
- Esempi: database SQL, fogli Excel, anagrafiche

2) Dati Non Strutturati
   
- Non seguono uno schema rigido
- Richiedono analisi più complesse (AI, NLP)
- Esempi: email, PDF, immagini, video, log

3) Dati Semi‑strutturati
   
- Hanno una struttura flessibile
- JSON, XML, YAML

**Dati e Sicurezza**
Nel contesto della sicurezza informatica, i dati devono essere protetti secondo i tre principi fondamentali:

- Confidenzialità → accesso solo a chi è autorizzato
- Integrità → i dati non devono essere alterati
- Disponibilità → i dati devono essere accessibili quando servono

**Questi tre principi formano la triade CIA (Confidentiality, Integrity, Availability).**

## Dati e GDPR
Il GDPR distingue tra Dati personali informazioni che identificano una persona fisica (nome, email, IP, foto, ecc.), Categorie particolari di dati quali dati sensibili come salute biometria opinioni politiche religione ed orientamento sessuale che richiedono misure di protezione piu forti tramite DPIA

Il piano di Disaster Recovery definisce
- RPO → quanti dati posso perdere
- RTO → quanto tempo posso restare offline
- Strategie di backup
- Replica dei dati
- Hot/Warm/Cold Site
- Cluster di failover
  
**Senza una corretta gestione dei dati, il Disaster Recovery non può funzionare per il recupero dei dati stessi**

# Database e DBA
Database e DBA sono due concetti inseparabili: il primo è il cuore dei dati, il secondo è il professionista che ne garantisce vita, sicurezza e prestazioni.
Un database è un sistema organizzato per archiviare, gestire e recuperare dati in modo efficiente e sicuro

**Caratteristiche principali**
- Organizzazione dei dati (tabelle, indici, viste, relazioni)
- Integrità (vincoli, chiavi primarie/esterne)
- Sicurezza (permessi, ruoli, crittografia)
- Performance (query ottimizzate, indici, caching)
- Affidabilità (backup, replica, clustering)

**Tipologie di database**

- Relazionali (SQL) → MySQL, PostgreSQL, SQL Server, Oracle
- Non relazionali (NoSQL) → MongoDB, Redis, Cassandra
- In‑memory → Redis, Memcached
- Distribuiti → CockroachDB, Yugabyte
- Cloud‑managed → AWS RDS, Azure SQL, Google Cloud SQL

## DBA Database Administrator
Il DBA è il professionista responsabile della gestione, sicurezza, disponibilità e performance dei database.
È una figura critica in qualunque azienda che gestisce dati sensibili, applicazioni mission‑critical o infrastrutture complesse

1) Installazione e configurazione
- Installazione del motore database
- Configurazione iniziale (storage, parametri, utenti, ruoli)
- Setup di cluster, replica, HA

2) Sicurezza
- Gestione utenti e permessi
- Crittografia (TDE, SSL/TLS)
- Audit e logging
- Conformità GDPR (minimizzazione, accessi, DPIA)

3) Backup e Disaster Recovery
- Pianificazione backup (full, diff, incremental)
- Test periodici di ripristino
- Definizione di RTO e RPO
- Replica geografica
- Gestione di Hot/Warm/Cold Site

4) Performance Tuning
- Ottimizzazione query
- Creazione e manutenzione indici
- Monitoraggio CPU, RAM, I/O
- Analisi dei piani di esecuzione

5) Alta Disponibilità (HA)
- Cluster di failover
- Replica sincrona/asincrona
- Load balancing
- Failover automatico

6) Manutenzione
- Patch e aggiornamenti
- Pulizia log e archivi
- Gestione spazio disco
- Monitoraggio continuo

Il DBA è una figura chiave nella sicurezza infromatica perché protegge i dati da accessi non autorizzati, garantisce intyegrità e disponibilità, collabora con il DPO per DPIA e GDPR, previene data breach tramite controlli audit e assicura che i backup siano sicuri e ripristinabili. SI occupa direttamente di strategie di backup, testare il ripristino verificare che il database rispetti RTO e RPO documentare procedure chiare e ripetibili e garantire continuitò in caso di disastro. sostanzialmente il Disaster Recovery non può funzionare senza un DBA

# ETL (Extract–Transform–Load)
è il processo che permette di raccogliere dati da più fonti, pulirli, trasformarli e caricarli in un data warehouse, rendendoli coerenti, affidabili e pronti per l’analisi, estrae dati da sistemi eterogenei (CRM, ERP, database SQL/NoSQL, API, IoT), trasforma i dati applicando regole di business, pulizia, deduplicazione, aggregazioni, carica i dati nel data warehouse, che diventa la single source of truth aziendale, Il data warehouse è un archivio centralizzato progettato per analisi, reportistica e BI. Senza ETL, i dati arriverebbero disordinati, incoerenti e difficili da analizzare.

1) Extract – Estrazione
Raccoglie dati da fonti strutturate, semi‑strutturate e non strutturate:
- SQL, NoSQL, JSON, XML, file flat, email, sistemi legacy.
  
L’obiettivo è acquisire i dati senza modificarli. 

2) Transform – Trasformazione
È la fase più complessa:

- pulizia (rimozione errori, valori nulli)
- normalizzazione
- deduplicazione
- join tra tabelle
- aggregazioni
- applicazione di regole di business
  
Serve a garantire qualità, coerenza e integrità dei dati. 

3) Load – Caricamento
Due modalità:

- Full Load → carica tutto (tipico dell’inizializzazione)
- I-ncremental Load → carica solo dati nuovi o modificati
  
È la fase che popola il data warehouse

**Strumenti ETL più comuni Azure Data Factory SQL Server Integration Services (SSIS) AWS Glue Informatica PowerCenter Talend Pentaho**

# Data Lake
Un Data Lake è un grande repository centralizzato che conserva dati di qualsiasi tipo — strutturati, semi‑strutturati e non strutturati — nel loro formato originale, senza trasformazioni obbligatorie al momento dell’ingestione. Un data lake è progettato per raccogliere enormi volumi di dati eterogenei, mantenendoli grezzi e integri ideale per Big Data, Machine Learning, Analisi predittiva, Data exploration, Conservazione economica di grandi dataset Grazie alla sua architettura aperta e scalabile, può contenere dati provenienti da database, file, log, sensori IoT, immagini, audio, video e molto altro.

- Schema‑on‑read → lo schema viene applicato solo quando i dati vengono analizzati, non quando vengono caricati
- Dati grezzi → nessuna trasformazione obbligatoria
- Alta scalabilità → spesso basato su storage cloud economico
- Flessibilità totale → adatto a data scientist e analisi avanzate
- Zone di dati → raw, cleaned, curated (a seconda della maturità del dato)

**Dal Data Lake un’evoluzione recente è il data lakehouse, che combina flessibilità del data lake performance e governance del data warehouse Supporta sia schema‑on‑read sia schema‑on‑write, con transazioni ACID e query SQL veloci**

