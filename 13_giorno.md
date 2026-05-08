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