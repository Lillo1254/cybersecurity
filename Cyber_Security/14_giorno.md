# Difesa in Profondità (Defence in Depth)
La difesa in profondità è una strategia di sicurezza che prevede l’uso di più livelli di protezione, in modo che se un livello fallisce, ce ne sia un altro pronto a bloccare o rilevare l’attacco.

## I livelli della Difesa in Profondità
La difesa in profondità si basa su tre categorie principali:

- Controlli Preventivi
- Controlli Detective
- Controlli Correttivi

## Controlli di Detection
I controlli detective servono a rilevare attività sospette, anomalie, attacchi in corso o compromissioni già avvenute.

Esempi:
- log di sistema
- IDS/IPS
- SIEM
- XDR
- UEBA
- monitoraggio del traffico
- alert comportamentali

## DR – Extended Detection and Response
XDR è un sistema avanzato che unifica:
- endpoint
- server
- rete
- cloud
- identità
- applicazioni
- per rilevare e rispondere agli attacchi in modo coordinato e automatizzato.

Caratteristiche principali
- correlazione automatica degli eventi
- analisi comportamentale
- risposta automatica (isolamento host, kill process, blocco IP)
- visibilità end‑to‑end
- riduzione dei falsi positivi

## SIEM – Security Information and Event Management
Il SIEM è il sistema che raccoglie, normalizza e correla tutti i log dell’azienda.

Cosa fa un SIEM
- centralizza i log
- applica regole di correlazione
- genera alert
- supporta incident response
- conserva log per audit e compliance
- permette analisi forense

Esempi di log raccolti
- firewall
- server
- applicazioni
- autenticazioni
- database
- cloud
- endpoint

**il SIEM raccoglie e correla log da tutta l'azienda l' XDR rileva e risponde agli attacchi in modo automatizzato**

### Difesa in Profondità: come si compone davvero
Ecco una visione completa dei livelli:

**Controlli Preventivi**

- firewall
- MFA
- hardening
- patching
- segmentazione
- access control
- VPN
- WAF

**Controlli Detective**

- SIEM
    - centralizza i log da server, firewall, cloud, applicazioni, endpoint
    - applica regole di correlazione per individuare attacchi
    - genera alert per il SOC
    - conserva log per audit, compliance e forensics
    - permette analisi storiche e investigazioni
    - È il cervello analitico della sicurezza: vede tutto e collega gli eventi
- XDR
    - rileva comportamenti anomali
    - isola automaticamente host compromessi
    - blocca processi malevoli
    - analizza telemetria da più fonti
    - riduce i falsi positivi
    - automatizza la risposta agli incidenti
- IDS/IPS
    - IDS – Intrusion Detection System
        - monitora il traffico
        - rileva anomalie o firme di attacco
        - genera alert
        - non blocca il traffico

    - IPS – Intrusion Prevention System
        - analizza il traffico in tempo reale
        - blocca pacchetti malevoli
        - chiude connessioni sospette
        - applica regole di prevenzione
- monitoraggio log
    - controlla errori, warning, accessi, anomalie
    - individua comportamenti sospetti
    - permette audit e tracciabilità
    - supporta incident response
- UEBA User and Entity Behavior Analytics
    - analizza il comportamento di utenti e dispositivi per individuare anomalie
    - crea un profilo comportamentale “normale”
    - rileva deviazioni (es. login insoliti, download anomali)
    - identifica insider threat
    - segnala compromissioni di account
    - usa machine learning per ridurre falsi positivi
- honeypot
    - è un sistema volutamente vulnerabile o interessante per attirare gli attaccanti
    - attira attacchi lontano dai sistemi reali
    - registra tecniche, strumenti e comportamenti degli attaccanti
    - permette analisi forense
    - segnala compromissioni precoci
    - aiuta a creare regole IDS/IPS e SIEM

**A CATENA IN AZIENDA**
**il SIEM fa detection su correlazione e analisi log l'XDR fa una detection con automatismo di risposta su possibili violazioni IDS rileva anomalie e genera alert IPS controlla il traffico in tempo reale e attua regole preventive bloccando o chiudendo il traffico il monitoraggio dei log è solo un osservazione continua lo UEBA fa un analisi comportamentale e veriica deviazione dal normale svolgimento dell'attività segnalando comportamenti anomali e l'honeypot è un sistema trappola per ingannare gli attaccanti registrare tecniche utilizzate per l'attacco e i loro comportamenti per aiutare a creare regole di detenction e response** 

**Controlli Correttivi**

# SOC E SOC2
**SOC – Security Operations Center**

Il SOC è un centro operativo di sicurezza, composto da persone, processi e tecnologie che monitorano e difendono l’azienda 24/7

Cosa fa un SOC
- monitora log, eventi e traffico
- rileva attacchi (SIEM, XDR, IDS/IPS)
- gestisce incidenti di sicurezza
- fa threat hunting
- coordina la risposta agli incidenti
- produce report e miglioramenti continui

Chi lavora nel SOC
- analisti Tier 1, 2, 3
- incident responder
- threat hunter
- ingegneri di sicurezza
- SOC manager

**SOC 2 – Service Organization Control 2**
Il SOC 2 NON è un team.
È un framework di audit e certificazione sviluppato dall’AICPA per valutare la sicurezza dei fornitori di servizi (cloud, SaaS, MSP, ecc.).

**Cosa certifica SOC 2**

Valuta se un’azienda rispetta i Trust Service Criteria:
- Security
- Availability
- Processing Integrity
- Confidentiality
- Privacy

Tipi di report SOC 2
Type I → verifica il design dei controlli in un momento specifico
Type II → verifica l’efficacia dei controlli nel tempo (3–12 mesi)

**IL SOC FA LA SICUREZZA DELL'AZIENDA MENTRE IL SOC2 NE ATTESTA L'AFFIDABILITA'**

# HIDS – Host‑Based Intrusion Detection System
L’HIDS (Host‑Based Intrusion Detection System) è un sistema di rilevazione delle intrusioni installato direttamente su un host, cioè su:
- server
- workstation
- VM (VirtualMachine)
- container
- dispositivi critici

In pratica controlla tutto ciò che accade dentro la macchina, non sulla rete.

## Monitoraggio dei file di sistema (File Integrity Monitoring – FIM)
Controlla se file critici vengono modificati:
- /etc/passwd
- /etc/shadow
- file di configurazione
- binari di sistema
- directory sensibili

## Monitoraggio dei log locali
Analizza:
- log di sistema
- log di autenticazione
- log applicativi
- log di sicurezza

## Rilevazione di rootkit e malware
Controlla:
- processi nascosti
- moduli kernel sospetti
- librerie alterate
- comportamenti anomali

## Controllo dell’integrità del sistema
Confronta lo stato attuale dell’host con uno stato “pulito” registrato in precedenza

## Monitoraggio delle configurazioni
Rileva modifiche a:
- firewall locali
- policy di sicurezza
- servizi attivi
- porte aperte

## Alert in tempo reale
Quando rileva un’anomalia, invia un alert a:
- SIEM
- XDR
- sistemi di ticketing
- SOC

**software**
- OSSEC / Wazuh
- Tripwire
- Samhain
- AIDE
- CrowdStrike Falcon (parte EDR/XDR)
- Elastic Agent (FIM + log + detection)

**HIDS (CHE AGISCE SULLE MACCHINE) E NIDS(CHE AGISCE SULLA RETE) FORMANO UNA COPERTURA COMPLETA PER LA SICUREZZA**

# Differenza tra HIDS e EDR
L’HIDS è un sistema che rileva anomalie e compromissioni sull’host, ma non interviene L’EDR è molto più avanzato: rileva, analizza e risponde agli attacchi sugli endpoint L’EDR è un sistema di detection + response

# CONTROLLO TRANSAZIONI BANCARIE    

## Come vengono controllate le transazioni con carta e pagamenti online
Quando fai un pagamento con carta (POS, e‑commerce, app), entrano in gioco diversi sistemi di sicurezza e controllo.
Li elenco in ordine cronologico, come un flusso reale

1) Autenticazione del titolare (3‑D Secure / SCA)
Prima che la transazione venga autorizzata, il sistema verifica che sei davvero tu.

Esempi:
- OTP via SMS
- App della banca (push)
- Biometria (impronta, volto)
- Token hardware

2) Autorizzazione della banca emittente
La banca che ha emesso la carta controlla:

- saldo disponibile
- plafond
- limiti giornalieri
- comportamento abituale del cliente
- geolocalizzazione
- rischio della transazione

3) Controlli antifrode in tempo reale
Ogni transazione passa attraverso motori antifrode basati su:

- machine learning
- regole statiche (es. importi anomali)
- reputazione del merchant
- velocità delle transazioni
- paese di origine
- tipo di dispositivo
- fingerprint del browser

4) Tokenizzazione dei dati della carta
Nei pagamenti online moderni (Apple Pay, Google Pay, PayPal, e‑commerce sicuri):
- il numero reale della carta non viene mai inviato
- viene usato un token univoco e inutilizzabile altrove

5) Cifratura end‑to‑end
I dati della carta vengono cifrati:
- sul dispositivo
- durante il transito
- nei sistemi del payment gateway

6) Controlli del circuito (Visa, Mastercard, Amex)
I circuiti applicano controlli aggiuntivi:

- verifica del merchant
- scoring del rischio
- blacklist globali
- monitoraggio transazioni sospette

7) Monitoraggio continuo post‑transazione
Le banche monitorano:

- pattern anomali
- tentativi ripetuti
- transazioni da paesi ad alto rischio
- comportamenti fuori dal profilo del cliente

## PCI‑DSS (Payment Card Industry – Data Security Standard)
È lo standard internazionale che tutti i soggetti che trattano dati di carte devono rispettare:
- e‑commerce
- POS
- banche
- payment gateway
- software che gestiscono carte
- provider cloud che ospitano sistemi di pagamento

Proteggere i dati della carta cifrando mascherando applicando il divieto di memorizzazione CVV e tokenizza i dati per proteggere i dati della carta stessa.

Bisogna proteggere rete e sistemi con firewall segmentazione hardening e patching utilizzando un controllo rigoroso degli accessi MFA least privilege e logging completo con monitoraggio e test continui di vulnerability scanning penetration testing log retention SIEM e IDS/IPS è necessario anche la formazione del personale le corrette procedure per la gestione degli incidenti completamente documentata e gli audit annuali