# DPIA(Data Protection Impact Assessment) valutazione dell'impatto sulla rpotezione dei dati
È un processo strutturato che permette di:
- descrivere il trattamento e le sue finalità
- valutarne necessità e proporzionalità
- identificare rischi per gli interessati
- definire misure tecniche e organizzative per ridurli
- documentare la conformità al GDPR

Il GDPR richiede che la DPIA sia svolta prima dell’inizio del trattamento e che sia considerata un processo continuo, non un documento statico
Una DPIA completa include:

- Descrizione del trattamento dei dati trattati, finalità, modalità, sistemi utilizzati
- Valutazione di necessità e proporzionalità in base giuridica, minimizzazione, tempi di conservazione
- Analisi dei rischi tramite probabilità, impatto, scenari di minaccia
- Misure di mitigazione tramite cifratura, pseudonimizzazione, controlli accessi, policy interne
- Valutazione del rischio residuo se rimane elevato → consultazione dell’autorità garante
- Coinvolgimento del DPO con parere documentato

in alcune situazioni specifiche è obbligatoria
La DPIA è necessaria quando il trattamento comporta rischio elevato, in particolare nei casi indicati dall’art. 35 GDPR e dalle linee guida europee

- profilazione o valutazione sistematica di aspetti personali
- trattamento su larga scala di dati sensibili (salute, biometria, genetica, giudiziari)
- monitoraggio sistematico e su larga scala di aree pubbliche (es. videosorveglianza)
- uso di tecnologie innovative
- trattamenti che coinvolgono minori o soggetti vulnerabili

# infrastrutture IAAS(Infrastructure as a Service)
sono un modello di cloud computing in cui un provider mette a disposizione server, storage, rete e risorse di calcolo completamente virtualizzate e accessibili via Internet. L’azienda non deve più acquistare o gestire hardware fisico: paga solo le risorse utilizzate e può scalarle rapidamente secondo necessità
Il provider cloud ospita l’infrastruttura nei propri data center el'utente crea e configura VM, reti e storage gestisce sistemi operativi, middleware e applicazioni paga solo ciò che consuma
Il provider invece gestisce hardware, alimentazione, sicurezza fisica, rete e virtualizzazione

**Cosa offre un’infrastruttura IaaS**

- Server virtuali on‑demand: macchine virtuali configurabili in pochi minuti.
- Storage scalabile: volumi, oggetti, dischi virtuali.
- Networking cloud: reti virtuali, firewall, bilanciatori di carico.
- Sicurezza e data center gestiti dal provider: l’hardware è mantenuto dal fornitore.
- Accesso tramite API o console web: totale automazione e provisioning rapido.

**SLA Service Level Agreement**

Uno SLA è un documento contrattuale che definisce in modo misurabile:

- quali servizi vengono forniti
- con quale qualità
- con quali tempi di risposta
- con quali responsabilità
- con quali penali in caso di mancato rispetto
È uno strumento fondamentale per garantire trasparenza, affidabilità e responsabilità tra fornitore e cliente.
Uno SLA ben fatto include:

1. Livelli di disponibilità (uptime)
- 99,9% uptime mensile
- indica quanto il servizio deve essere operativo
2. Tempi di risposta
- tempo massimo per rispondere a un ticket
- tempo massimo per iniziare la risoluzione
3. Tempi di ripristino (RTO)
- quanto tempo può durare un’interruzione
4. Obiettivi di perdita dati (RPO)
- quanto è accettabile perdere in termini di dati (es. backup ogni 24h)
5. Metriche di performance
- latenza
- throughput
- capacità minima garantita
6. Sicurezza
- misure minime richieste
- gestione incidenti
- logging e monitoraggio
7. Penali e compensazioni
- crediti di servizio se il provider non rispetta gli impegni
8. Esclusioni
- casi in cui lo SLA non si applica (manutenzioni programmate, cause di forza maggiore)

# SaaS  (Software as a Service)
è un modello di cloud computing in cui il software non viene installato sul computer dell’utente, ma è ospitato nel cloud e accessibile tramite Internet, di solito da un browser. È il modello più “pronto all’uso” tra i servizi cloud: l’utente si limita a usare l’applicazione, mentre il provider gestisce tutto il resto, Il SaaS è un software distribuito via Internet, fornito in abbonamento o pay‑per‑use

**Il provider:**
- ospita l’applicazione nei propri server
- gestisce infrastruttura, sicurezza, aggiornamenti e manutenzione
- garantisce accesso da qualsiasi dispositivo connesso

**L’utente:**
- crea un account
- accede al servizio via browser o app
- non installa nulla in locale

**il SaaS:**
- Il software gira nei server del provider.
- L’utente accede tramite browser web o app mobile.
- I dati vengono elaborati e archiviati nel cloud.
- Gli aggiornamenti sono automatici e centralizzati.

# IDS IPS E SOC

**IDS – Intrusion Detection System**
- Un IDS monitora il traffico di rete alla ricerca di attività sospette o non autorizzate.
- Confronta il traffico con firme di attacchi noti o cerca anomalie.
- Quando rileva qualcosa di sospetto, genera un allarme per gli amministratori.
- Non blocca il traffico, è un sistema passivo.

Esistono due tipi principali:
- NIDS (Network IDS): monitora la rete.
- HIDS (Host IDS): monitora un singolo host (log, file, processi).

**IPS – Intrusion Prevention System**

Un IPS è simile a un IDS, ma con una differenza cruciale: 
- interviene attivamente.
- Analizza il traffico in tempo reale.
- Se rileva una minaccia, blocca il pacchetto, chiude la connessione o riconfigura il firewall.
- È un sistema proattivo.

**SOC – Security Operations Center**

Il SOC è un team organizzativo, non un dispositivo.
- Riceve gli alert da IDS, IPS, firewall, SIEM, ecc.
- Analizza gli incidenti, correla gli eventi, risponde agli attacchi.
- Lavora 24/7 per monitorare e proteggere l’infrastruttura.

Il SOC è quindi il “cervello” che coordina la difesa, mentre IDS e IPS sono “sensori” e “scudi” è composto da persone professionisti della sicurezza IT , processi
e tecnologie che lavorano insieme per monitorare, rilevare, analizzare e rispondere agli incidenti di sicurezza.

# Costi di ripresa post - attacco

**Costi tecnici (IT e operativi)**

- Ripristino dei sistemi: reinstallazione server, workstation, applicazioni.
- Recupero dei dati: restore da backup, ricostruzione database, analisi integrità.
- Incident response: intervento di team interni o esterni specializzati.
- Analisi forense: identificazione del punto di compromissione, raccolta prove.
- Sostituzione hardware compromesso: server, firewall, endpoint danneggiati.
- Aggiornamenti e patching straordinario: hardening post‑attacco.
- Interruzione operativa: perdita di produttività, fermo dei servizi.
- Acquisto di nuovi strumenti di sicurezza: EDR, SIEM, firewall, MFA, ecc.

**Costi legali e normativi**

- Consulenza legale: interpretazione obblighi GDPR, contratti, responsabilità.
- Notifica al Garante Privacy (entro 72 ore) e gestione documentale.
- Notifica agli interessati se c’è rischio elevato per i diritti e le libertà.
- Sanzioni amministrative (GDPR, NIS2, contratti con clienti).
- Contenziosi: richieste di risarcimento da clienti o partner.
- Costi assicurativi: franchigie o esclusioni della polizza cyber.
- Conservazione delle prove per eventuali procedimenti giudiziari.

**Costi di comunicazione**

- Comunicazione interna: informare dipendenti, reparti, direzione.
- Comunicazione esterna: clienti, partner, fornitori, media.
- Gestione della crisi reputazionale: comunicati stampa, PR, social media.
- Call center e supporto clienti: aumento richieste post‑attacco.
- Campagne di trasparenza e rassicurazione: ricostruire fiducia.
- Perdita di clienti: churn, rescissioni contrattuali, calo vendite.
- Danni all’immagine del brand: impatto a lungo termine.

# NIS2
La Direttiva NIS2 è il nuovo quadro normativo europeo che rafforza in modo significativo la cybersecurity di reti e sistemi informativi in tutta l’Unione Europea. È stata introdotta con la Direttiva (UE) 2022/2555 e sostituisce la precedente NIS1 del 2016, ampliando settori coinvolti, obblighi, controlli e sanzioni

La NIS2 stabilisce regole comuni e più rigorose per aumentare la resilienza informatica di aziende e pubbliche amministrazioni in 18 settori critici, imponendo:

- misure di gestione del rischio più stringenti
- obblighi di notifica degli incidenti più rapidi
- controlli e vigilanza più severi
- cooperazione tra Stati membri
- requisiti uniformi per sicurezza, supply chain e gestione vulnerabilità

**Entità essenziali**

Settori come:

- energia
- trasporti
- sanità
- infrastrutture digitali
- finanza
- acqua potabile e reflue
- PA centrale e regionale
- spazio

**Entità importanti**
- servizi digitali (cloud, DNS, data center, marketplace, social)
- gestione rifiuti
- manifattura di prodotti critici
- servizi postali e di corriere
- altri settori industriali strategici

**Obblighi principali della NIS2**
. Le aziende devono adottare misure di sicurezza che includono:

 **Gestione del rischio**

- politiche di sicurezza
- controllo accessi
- cifratura
- gestione vulnerabilità
- sicurezza della supply chain

**Notifica degli incidenti**

Obbligo di segnalare incidenti significativi al CSIRT Italia entro tempi precisi (finestra di 24 ore per early warning, 72 ore per notifica completa).

**Misure tecniche e organizzative**

- business continuity
- disaster recovery
- formazione del personale
- audit periodici
- monitoraggio continuo

**Registrazione annuale**

Le organizzazioni classificate devono registrarsi sul Portale NIS tra il 1° gennaio e il 28 febbraio di ogni anno.

**Scadenze operative (Italia)**
Secondo le determinazioni ACN del 2025:

- entro 9 mesi → obbligo di notifica incidenti significativi
- entro 18 mesi → adozione delle misure di sicurezza di base (Allegato 1 o 2)

**Sanzioni**
La NIS2 introduce sanzioni molto più elevate rispetto alla NIS1:

- fino a 10 milioni di euro o 2% del fatturato globale per entità essenziali
- fino a 7 milioni di euro o 1,4% del fatturato per entità importanti

**Un azienda conforme**
- conosce tutte le leggi applciabili
- ha processi e sistemi adeguati
- fa audit regolari tramite auditor
    - l'audit è il processo di controllo sistematico indipendente documentato basato su evidenze ggettive e finalizzato alla valutazione della conformità
    - l'auditor è colui che esegui l'audit 
- documenta tutto
- ha responsabili designati

**Un azienda non conforme**
- ignora le nromative
- non ha processi adeguati
- non fa controlli
- non documenta
- nessun responsabile

# In cyber security
**Diligenza dovuta (due diligence)**
principio legalper l'azienda che ha il dovere di fare tutto ciò che una persona ragionevole farebbe per proteggere dati e sistemi

- installa antivirus e firewall
- aggiorna regolarmente sistemi
- usa password forti
- cripta dati sensibili
- fa backuo regolari
- forma i dipendenti

Ogni intervento deve essere documentato
- policy scritte
  - ogni parte della privacy e policy deve essere scritta e documentata
- registri di investimento
  - documentazione di investimenti in sicurezza quali antivirus firewall ecc..
- formazione del personale
  - documentazione che riporta sia quali dipendenti sono stati formati sia su quali argomenti
- audit eseguiti
  - la documentazione degli audit eseguiti e delle valutazioni

# ISO 27001: standard mondiale
 è una norma certificabile, riconosciuta globalmente, che definisce come un’organizzazione deve proteggere dati, sistemi e processi attraverso un SGSI (Sistema di Gestione della Sicurezza delle Informazioni).
**ISO 27001 è uno standard mondiale che stabilisce:**

- come identificare e valutare i rischi informatici
- come implementare controlli di sicurezza efficaci
- come garantire la protezione continua di dati e infrastrutture
- come dimostrare conformità tramite audit e certificazione

È utilizzato da aziende, enti pubblici, provider cloud, banche, ospedali, MSP, SOC e qualsiasi organizzazione che gestisce informazioni critiche

**Lo standard si basa su tre pilastri fondamentali:**

- Confidenzialità → i dati devono essere accessibili solo a chi è autorizzato
- Integrità → i dati devono essere corretti e non alterati
- Disponibilità → i dati devono essere accessibili quando servono

**Per raggiungere questi obiettivi, ISO 27001 richiede:**

- analisi e trattamento del rischio
- politiche di sicurezza
- gestione degli accessi
- continuità operativa
- sicurezza fisica e logica
- formazione del personale
- monitoraggio e miglioramento continuo

**La ISO 27001 ha validità 3 anni**

# Formazione del personale
- Formazione iniziale di 1/2 ore per nuovi dipendenti  su cyber security, policy aziendali, riconoscimento phishing
- Formazione continua annuale o semestrale per aggiornare sui possibili nuovi tipi di attacchi studiare dei casi conosciuti ed eseguire un quiz di verifica
- Simulazione di phishing controllate da parte dell'azienda per testare se i dipendenti sanno identificare una minaccia o hanno bisogno di formazione aggiuntiva
- Formazione specializzata per componenti dell'azienda che hanno ruoli con accesso a dati sensibili su tecniche avanzate e conformitò legale
- Campagne di sensibilizzazione tramite poster, email, video a step fissi o a caso durante l'anno per mantenere sempre accesa l'attenzione sulle possibili minacce

# ROI – Return on Investment
Misura quanto rende un investimento rispetto al suo costo
Investi 10.000 € in sicurezza e risparmi 15.000 € di potenziali danni → ROI = 50%.

# RTO – Recovery Time Objective
Il tempo massimo accettabile di fermo di un servizio dopo un incidente
“Per quanto tempo possiamo restare offline prima che il danno diventi critico?”
È un parametro chiave del Disaster Recovery

# RPO – Recovery Point Objective
La quantità massima di dati che possiamo perdere, misurata in tempo L’RPO indica il punto nel tempo a cui devi poter tornare dopo un disastro, cioè la quantità massima di dati che puoi perdere, misurata in minuti, ore o giorni
“Quanti dati possiamo permetterci di perdere?”
RPO determina ogni quanto fare backup

**RPO = 24 ore**
- Backup giornaliero
- Puoi perdere i dati dell’ultimo giorno
- Tipico per uffici, posta, file server non critici
  
**RPO = 1 ora**
- Backup orario
- Perdita massima: 60 minuti
- Tipico per ERP, CRM, database importanti
  
**RPO = 5 minuti**
- Replica continua o snapshot molto frequenti
- Perdita massima: 5 minuti
- Tipico per e‑commerce, sistemi finanziari
  
**RPO = 0**
- Nessuna perdita dati accettabile
- Serve replica sincrona  
- Tipico per sistemi bancari, trading, sanità