# CVE VULNERABILITY ASSESSMENT E MITRE

## CVE 
il CVE è il codice fiscale della vulnerabilità contiene un codice univoco una breve descrizione con riferimento tecnico e un punteggio CVSS( da 0.0 a 10.0) non vi è riportato come risolvere il problema ma lo identifica in maniera standard.

## VULNERABILITY ASSESSMENT
è il processo con il quale un azienda scansiona i sistemi identifica vulnerabilità note (CVE) valuta la gravità prioritizza gli interventi svolgendo scansioni automatiche in modo programmato e periodico cosi da analizzare le possibil CVE rilevate valutare il rischio e stipulare un report di priorità basate sul livello del CVSS che gli viene assegnato questo per trovare vulnerabilità prima che lo faccia un attaccante

## MITRE
La MITRE è un organizzazione no-profit statunitense che gesticse CVE ATT&CK Framework CWE (Common Weakness Enumeration) CAPEC (Catalogo delle tecniche di attacco) è il “custode” degli standard globali sulla classificazione delle vulnerabilità ed è questa organizzazione che si occupa di assegnare i CVE mantenere il database pubblico definire categorie di debolezza (CWE) e studiare le tecniche degli attaccanti (ATT&CK)

# Vulnerability Assessment in Azienda Privata
Il Vulnerability Assessment è il processo con cui un’azienda identifica, analizza e classifica le vulnerabilità presenti nei propri sistemi, per ridurre il rischio prima che venga sfruttato da un attaccante.

1) Definizione del Perimetro e Pianificazione
   
il perimetro:
- server, VM, endpoint
- dispositivi di rete
- applicazioni interne ed esterne
- servizi cloud
- database
- dispositivi mobili
- reti interne e DMZ

Attività principali
- definire gli asset da scansionare
- stabilire finestre temporali (per evitare impatti)
- ottenere autorizzazioni formali
- definire strumenti e metodologie

2) Scansione delle Vulnerabilità
In questa fase si utilizzano strumenti automatici per identificare vulnerabilità note (CVE)

Attività principali:
- scansioni di rete
- scansioni degli host
- scansioni delle applicazioni
- scansioni delle configurazioni
- scansioni delle dipendenze software

**Gli strumenti confrontano i sistemi con database come CVE e CWE fornendo una lista di vulnerabilità potenziali**

3) Analisi e Classificazione dei Risultati
Questa è la fase più importante: non tutte le vulnerabilità rilevate sono reali o critiche

Validazione serve a eliminare falsi positivi vulnerabilità non sfruttabili errori di configurazione dello scanner

**ROOR CAUSE ANALYSIS** si analizza il perche esiste la vulnerabilità se ci sono patch mancanti configurazioni errate versione obsolete errori in sviluppo permessi eccessivi l'obiettivo è capire la causa per risolvere dalla radice

4) Valutazione del Rischio e Prioritizzazione
Una vulnerabilità non è automaticamente un rischio: dipende dal contesto

Criteri di valutazione:
- CVSS (gravità tecnica)
- esposizione (è raggiungibile da Internet?)
- valore dell’asset
- probabilità di sfruttamento
- impatto sul business
- presenza di exploit pubblici
- mitigazioni già presenti

Prioritizzazione tipica:
- (0.0 - 3.9) Low → pianificabile
- (4.0 - 6.9) Medium → entro settimane
- (7.0 - 8.9) High → entro pochi giorni
- (9.0 - 10.0) Critical → da correggere subito

5) Reporting e Documentazione
Il report finale deve essere chiaro, leggibile e utile al management contenendo una sintesi esecutive elenco delle vulnerabilità con rischio associato e priorità le raccomandazioni tecniche il root cause analysis lo stato delle mitigazioni e il trend rispetto ai mesi precedenti è importante perche dimostra conformità iso 27001 GDPR e NIS2 permette di pianificare busget e interventi e crea uno storico per gli audit e incident response sostanzialemnte il report è cio che trasforma l'analisini in decisione aziendale

6) Mitigazione e Remediation
La mitigazione non elimina la vulnerabilità, ma riduce il rischio che venga sfruttata limitando funzionalità aumentando il monitoraggio isolando il servizio vulnerabile ecc praticamente argina il problema senza risolverlo e si attua quando la patch di sicurezza non è ancora pronta o non è conforme al funzionamento dei servizi o semplicemente se la remediation è troppo costosa rispetto al rischio.
La Remediation al contrario è l'azione che che risolve completamente la vulnerabilità installando una patch funzionante aggiornando software obsoleti correggere configurazioni errate o riscrivendo il codice vulnerabile

7) Verifica e monitoraggio
Successivamente all'attuazione di una mitigazione o remediation si attuano politiche di rescanning per verificare cheil problema sia stato risolto e di monitoraggio ricorrente e programmato con cadenza regolare

**SFOTWARE "OPENVAS, NMAP(NSE), OWASP**

## categorizzazione CVSS
1) Base Score
   - exploit
     - attack vector dove avviene
     - attack complexity quanta difficolta per essere eseguito
     - privileges required se serve un autenticazione specifica o meno
    - impact
      - riservatezza
      - integrità
      - disponibilità
2) Temporal score (cambia nel tempo) 
    -  quanto è grave in questo momento
3) Environmental score
   - Misurano quanto è importante per la tua azienda
   - Misurano se l'attacco complisce dati sensibili o meno
   - misurano la gravità generale a livell fisico e legale

## Processo di remediation
La remediation è il processo strutturato con cui un’azienda elimina una vulnerabilità riducendo il rischio senza interrompere le attività operative.
È un processo rigoroso, composto da fasi precise, ognuna con responsabilità e controlli chiari.

**Prioritizzazione**
Prima di intervenire, si decide l’ordine delle attività.

Come si stabilisce la priorità:
- CVSS Score (Base + Temporal + Environmental)
- Importanza dell’asset (criticità per il business)
- Esposizione (internet-facing, DMZ, rete interna)
- Presenza di exploit pubblici
- Impatto operativo della correzione

**Filtro dei falsi positivi**

Prima di procedere, si eliminano:
- vulnerabilità non reali
- errori dello scanner
- condizioni non sfruttabili
  
Questa fase spesso genera un trouble ticket per ogni vulnerabilità valida.
Un trouble ticket è un record ufficiale che descrive un problema tecnico, una vulnerabilità o un malfunzionamento rilevato in azienda Senza ticket, non esiste tracciabilità, non esiste accountability, e non si può fare audit

**Pianificazione e Definizione delle Responsabilità**
Si stabilisce chi fa cosa e quando.

Attività principali:
- assegnazione delle task ai team competenti (IT, Dev, SecOps, Cloud)
- definizione delle scadenze
- approvazione del change management
- valutazione dell’impatto sui servizi

Tutto deve essere tracciato tramite ticketing

**Maintenance Window**
La remediation non si fa mai durante l’orario di lavoro.

Obiettivi:
- evitare downtime imprevisti
- ridurre l’impatto sugli utenti
- garantire la presenza dei team tecnici

Le maintenance window vengono programmate:
- di notte
- nel weekend
- in periodi di basso traffico

**NO FRIDAY DEPLOY**: mai fare deploy di venerdì

**Sviluppo della Strategia di Remediation**
Si decide come correggere la vulnerabilità la scelta dipende dal rischio, compatibilit, impatto operativo e costi.

Possibili soluzioni:
- applicare una patch
- modificare una configurazione
- aggiornare o sostituire un software
- disabilitare un servizio vulnerabile
- applicare un compensating control (se la patch non è disponibile)

**Testing in Ambiente di Staging**
Mai applicare una patch direttamente in produzione utilizzare un ambiente di staging il piu possibili simile alla produzione

Fasi del testing:
- utilizzo di una sandbox o ambiente di staging
- verifica della compatibilità
- controllo che la patch non rompa applicazioni o servizi
- test funzionali e di integrazione
- simulazione del carico

## Deployment Roll-out
Implementazione (Deployment / Roll-out)
Una volta validata la patch, si procede al rilascio.

Regole operative:
- roll-out graduale (canary release, blue-green deployment)
- monitoraggio in tempo reale
- applicazione prima su un piccolo gruppo di server
- estensione progressiva al resto dell’infrastruttura

Piano di Roll-back
Deve essere sempre pronto e testato prima del rilascio.

Include:
- backup aggiornato
- snapshot delle VM
- script di ripristino database
- trigger di interruzione automatica in caso di errori

## Monitoraggio Post-Rilascio
Dopo il deploy, si controlla che tutto funzioni correttamente soprattuto nelle prime ore dove il rilascio poiche sono le piu critiche.

Cosa monitorare:
- performance dei sistemi
- error log
- alert di sicurezza
- feedback degli utenti
- stabilità dei servizi

## Documentazione e Change Management
Ogni remediation deve essere documentata.

Documentazione necessaria:
- ticket di change management
- descrizione della vulnerabilità
- soluzione applicata
- impatto sul sistema
- evidenze dei test
- esito del roll-out
- eventuale post-mortem che Serve a capire perché è successo qualcosa e come evitare che succeda di nuovo

Comunicazione
- avvisi agli utenti
- comunicazioni interne ai team
- aggiornamento della knowledge base archivio strutturato di informazioni tecniche e operative guide ai processi procedure ecc.

# Database durante roll-out e roll-back
 database sono sistemi stato‑dipendenti: contengono dati che cambiano continuamente Per questo, durante un roll‑out o un roll‑back, vanno trattati in modo diverso rispetto a un’applicazione o a un servizio stateless

 **Prima regola: MAI fare roll‑out senza un backup consistente**
 Il database deve avere un backup completo, consistente e verificato immediatamente prima del roll‑out
 Questo backup serve come:
- piano di roll‑back
- snapshot dello stato dei dati
- punto di ripristino garantito

Durante un roll‑out, l’applicazione può:
- cambiare schema del database
- aggiungere colonne
- modificare tabelle
- cambiare indici
- trasformare dati

Se fai un roll‑back dell’applicazione ma non del database, rischi:
- incompatibilità
- errori di lettura
- corruzione dati
- perdita di integrità referenziale

## Strategie corrette per gestire i database
1) Backup + Script di Migrazione Versionati
Ogni release deve avere:
- uno script di migrazione (upgrade)
- uno script di rollback (downgrade)

Esempi:
- Flyway
- Liquibase
- Script SQL versionati

2) Test delle migrazioni in staging
Prima del roll‑out:
- si applicano le migrazioni in un ambiente di staging
- si verifica che l’applicazione funzioni
- si testa anche il rollback

Se il rollback non funziona in staging, NON si procede in produzione

3) Blue‑Green Deployment per i database?
Per i database è difficile, ma possibile se:
- il database è replicato
- si usa un sistema di shadow tables
- si applicano migrazioni backward‑compatible

# Principio di Integrità Referenziale
L’integrità referenziale è una regola dei database relazionali che garantisce che le relazioni tra tabelle rimangano sempre coerenti Non possono esistere riferimenti a dati che non esistono

In un database relazionale hai:
- una Primary Key (PK) → identifica un record
- una Foreign Key (FK) → punta alla PK di un’altra tabella

L’integrità referenziale garantisce che:
- ogni FK deve puntare a una PK esistente
- non puoi cancellare una PK se esistono FK che la usano
- non puoi modificare una PK senza aggiornare le FK collegate

**a seconda della relazione delle tabelle tra i dati "one to many...one to one...many to many**

# Point‑In‑Time Recovery (PITR)
Il Point‑In‑Time Recovery (PITR) è la capacità di ripristinare un database esattamente a un momento specifico nel passato, non solo all’ultimo backup completo.

Il PITR è fondamentale quando:
- un’applicazione ha scritto dati sbagliati
- una patch ha corrotto il database
- un utente ha cancellato dati per errore
- un ransomware ha cifrato solo parte del DB
- una migrazione ha fallito
- un roll‑out ha generato inconsistenze

Il PITR si basa su due elementi:
- Backup completo (full backup)
- Log delle transazioni (transaction log / WAL / redo log)

Il database registra ogni modifica nei log.
Durante il ripristino:
- si ripristina il backup completo
- si “riapplicano” i log fino al minuto/secondo desiderato

# Branch Cut
Il branch cut è il momento in cui si “taglia” un ramo (branch) del repository per bloccare una versione del codice e prepararla alla release si congela il codice, si crea un branch dedicato alla release e da quel momento in poi solo fix critici possono essere aggiunti. È un concetto chiave in GitFlow, trunk‑based development e in qualsiasi pipeline CI/CD professionale.

Il branch cut serve a:
- stabilizzare una release
- evitare che nuove funzionalità entrino per errore
- permettere ai team di continuare a sviluppare sul branch principale
- isolare bugfix e patch della release
- preparare il codice al roll‑out in produzione

**Come funziona**
Il team decide che la release è pronta.

Si crea un branch dedicato:
- release/v1.4
- hotfix/2026-05-08

Quel branch viene congelato:
- niente nuove feature
- solo bugfix
- solo patch critiche
- Il branch viene testato, validato e preparato al deploy.

Una volta rilasciato, il branch viene:
- taggato (v1.4.0)
- eventualmente chiuso
- mergiato in main e develop

**Il branch cut è il checkpoint della release.**

# Roll‑Forward dei Log
Il roll‑forward è il processo con cui un database, dopo essere stato ripristinato da un backup, riapplica tutte le transazioni registrate nei log per riportarlo a uno stato più recente.

Un backup completo fotografa il database in un momento preciso.

Ma tra quel momento e l’incidente possono essere passate:
- ore
- giorni
- settimane

Durante questo tempo il database ha registrato:
- inserimenti
- aggiornamenti
- cancellazioni
- transazioni complesse

**Il roll‑forward permette di non perdere questi dati.**