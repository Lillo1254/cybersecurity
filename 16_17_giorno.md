# Penetration Testing
Il penetration testing è la simulazione di un attacco informatico contro un sistema per valutare la sicurezza identifiando le vulnerabilitò prima dei criminali informatici

**obiettivi**
- identificare la vulnerabilità di sicurezza
- valutare l'efficacia delle difese attuali
- garantire la conformità alle normative PCI-DSS GDPR
- prevenire violazioni dei dati finanziari e reputazionali
- testare la capacità di risposta del team di sicurezza (blue team)

**tipologie**
black Box (scatola nera)
- il tester non ha informazioni sul sistema simula un attacco esterno realistico richiede molto tempo per il riconoscimento

white box (scatola bianca)
- il tester ha pieno accesso a codice e arichitettura cosi da permettere un analisi profonda e mirata ottimizzando i tempi di scoperta delle falle

grey Box (scatola grigia)
- il tester ha informazioni parziali come le credenziali di un utente simula un attacco da parte di insider bilanciando realismo ed efficenza dei tempi

## le fasi del penetration testing
1) ricognizioni
raccolta di informazioni sul bersaglio utilizzo di fonti pubbliche (OSINT) identificazione dei domini email e indirizzi IP

2) scansione
individuazione dei servizi attivi sulle porte utilizzando strumenti automatici come **Nmap**(network mapping) identificando sistemi operativi e versioni

3) Accesso (Exploitation)
**sfruttamento delle vulnerabilità scoperte utilizzando framework come **metasploit** violando i sistemi per dimostrarne il rischio**

sfruttamente delle vulnerabilità per un accesso abusivo reale superando controlli di sicurezza

4) mantenimentometodologia di exploitation mirata

creazione di backdoor nel sistema violato simulando una minaccia persistente avanzata APT e mo- sfruttamento di falle note CVE 
- attacchi alla web application sfruttare vulnerabilità logiche per costringere il server web a restituire i dati del database o a eseguire comandi di sistema

utilizzo di framework come metasploit
ingegnerizzare l'attacco gestire i payload e stabilire sessioni di controllo stabili

metodologia di pen test assisti da framework
- selezione e configurazione ricerda del modulo di exploit corretto all'interno della console metaploit impostazione parametri dell'host remoto e della porta
- generazione del payload configurazione di un payload avanzata come una sessione meterpreter in modalità reverse TCP per far in modo che sia la macchina attaccata a collegarsi con il proprio pc del tester aggirando i blocchi del firewall aziendalevimento laterale verso altri sistemi della rete

5) analisi e reportistica
documentazione dettagliata di ogni falla scoperta e annessa valutazione dell'impatto sul business aziendale e fornitura delle linee guida per la risoluzione (remediation)

## principali ambiti di applicazione
- network pen test verifica dei firewall router switch
- web application pen test per analisi di siti e API
- wireless pen test verifica delle reti wifi e protocolli radio
- social engineering per effettuare test del personale traminite phishing o vishing

## strumenti essenziali
- Kali linux sistema operativo deidicato alla sicurezza
- Nmap 
- burp suite
- metasploit
- wireshark

## identificazione delle vulnerabilità
l'obiettivo è mappare l'intera superfice d'attacco alla ricerca di difetti logici bug software o configurazioni errate

**vulnerability scanning**
    - esecuzione di scansioni con strumenti come **Nessus OpenVas Qualys**
    - configurazione di scansioni autenticate con credenziali per analizzare l'interno del sistema
    - configurazione di scansioni non autenticate per verificare l'esposizione perimetrale

**analisi statica e dinamica del codice (SAST/DAST)**
    - SAST analisi del codice sorgente senza eseguirlo alla ricerca di patter insicuri
    - DAST test dell'applicazione in esecuzione per osservare la risposta a input malevoli

**verifica manuale**
    - intercettazione del traffico HTTP/S tramite proxy di livello applicativo come Burp Suite
    - manipolazone manueale dei parametri dei token dei cookie e dei campi di input
    - eliminazione dei falsi positivi generati dagli scanner automatici attraverso tentativi mirati di esploitation

## valutare l'efficacia delle difese attuali
l'obiettivo è testare la reale capacitò di tenuta dei sistemi di protezione attivi (firewall EDR IPS WAF) di fronte a tecniche di attacco reali

**WAF FIREWALL BYPASSING**
- utilizzo di tecniche di offuscamento dei payload tramite codifica url multipla base64 esadecimale
- frammentazione dei pacchetti ip per aggirare i controlli dei firewall perimetrali
- iniezione di payload polimorfici per evitare i motori di rilevamente basati su firma

**EDR e antivirus evasion**
- cifratura del codice malevolo tramite crypting custom per bypassare l'analisi statica
- esecuzione del codice direttamente in memoria tramite process injection per eludere il controllo sul disco fisso
- utilizzo di binari legittimi di sistema per scopi malevoli tecnica living of the land o lotl

**stress test delle regole di correlazione**
- generazione progressiva di anomalie per identificare la soglia di blocco dei sstemi IPD/IDS
- verifica del corretto isolamento dei segmenti di rete critici (VLAN) tramite test di routing laterale

**garantire la conformità alle normative PCI-DSS GDPR**
l'obiettivo è verificare che l'infrastruttura rispetti i requisiti tecnici imposti dai framework legali e di sicurezza industriali

- mappatura dei requisiti (compilance mapping)
    - definizione dle perimetro di test basato sulla conformità
    - verifica presenza di crittografia forte sui dati in transito e a riposo
- metodologia NIST SP 800-15
    applicazione delle linee guida tecniche del nation institute of standards technology per l'esecuzione di test
    - ispezione formale delle configurazioni di sistema e delle policy di gestione delle password
- Gap analysis
    - confronto diretto tra le vulnerabilità riscontrate con gli articoli normativi violati
    - rilascio di un report di attestazione formale firmato

    - creazione dei canali di comunicazione cifrati in uscita non intercettati dai sistemi interni
    - utilizzo di tecniche di tunneling dns o icmp per trasferire pacche di dati fittizi all'esterno della rete
    - verifica dell'assenza di policy di data loss prevention DLP sul traffico uscente

- ransomware readiness test
    - simulazione della cifratura dei file in ambienti di staging controllati per misurare i tempi di propagazione
    - analisi dei sistemi di backup per verificare se sono raggiungibili e vulnerabili alla cancellazione da parte di un utente compromesso

- threat modeling basato sul rischio
    - calcolo del livello di rischio tramite framework standard come CVSS o DREAD
    - associazione di ogni vulnerabilità tecnica al potenziale danno finanziario

## testare la capacità di risposta del team di sicurezza (blue team)
l'obiettivo p valutare la prontezza la rapidita e l'efficacia del team di difesa aziendale durante un incidente informatico in corso con 

**esercitazioni di purple teaming**
- colalborazione diretta e in tempo reale tra gli attaccanti (red team) e i difensori (blue team)
- esecuzione di un attacco specifico seguita dalla verifica immediata sui log del SIEM (security information and event management)
- ottinizzazione immediata delle regole di alert del SIEM se l'attacco non è stato rilevato correttamente
**adoption della matrice MITRE ATTACK**
- pianificazione delle azioni di attacco mappandole sulle tattiche e tecniche reali censite a livello globale
- misurazione di quante tecniche della matrice vengono correttamente rilevae bloccate o ignorate dal blie team
**misurazione dei KPI**

## tipologie di penetration test black box
unico dato disponibile perimetro dell'azienda o dominio principale

**azione 1** 
metodologia raccolta informazioni passiva

- mappare da zero l'intera infrastruttura aziendale esposta su internet
- metodologia di raccolta ingormazioni passiva identificazione del perimetro tramite registri pubblici 
- mappatura DNS raccolta record piattaforma crt.sh
- data leak e credential harvesting ricercando credenziali aziendali compromessi in precedenti violazioni di terze parti all'interno del dark web o 
- repository pubblici e analisi metadati nei documenti esposti pdf docx per estrarre formati di usernam nomi server e software utilizzati

metodologia raccolta informazioni attiva

- port scanning perimetrale lancio di scnasioni Nmap massive ma silenziose sui blocchi IP individuati per mappare le porte TCP/UDP aperte identificando i servizi esposti
- banner grabbing interrogazione diretta dei servizi per catturare le intestazioni software determinando con precisione le versioni dei sistemi operativi e dei server web per identificare vulenrabilità note CVE

**azione 2 simulare un attacco esterno realistico**
l'obiettivo è replicare le esatte tecniche e procedure utilizzate dai cybercriminali reali per forzare il perimetro aziendale

metodologia di vulnerability assessment e exploitation esterna
- attacco ai servizi esposti analisi delle interfacce di login pubbliche pannelli amministrativi portali VPN piattaforme di smartworking per tentare attacchi di credential stuffing (uso di password violate note) o password spraying (test di passwrod deboli comuni come nome.cognome)ù
- sfruttamento di falle logiche e bug software tramite ricerca di esecuzione di exploit pubblici o custom per vulnerabilità di tipo Remote Code Execution RCE o violazioni OWASP top 10 presenti sulle applicazioni web perimetrali

metodologia initial access tramite social engineering
- phishing mirato (spear phishing) invio di email ingannevoli personalizzate ai dipendenti aziendali i cui contatti sono stati raccolti tramite OSINT tipo su linkedin instagram facebook ecc.. contenenti allegati malevoli o link a pagine di login clonate (-credential harvesting)
- bypassing dei controlli di sicurezza iniziali configurazione di domini simili a quello aiendale e utilizzo di server SMTP autenticati per eludere i filtri antispam e sistemi secure email gateway

**azione 3 richeide molto tempo per il riconoscimento**
metodologia di gestione e ottimizzazione dei tempi (time-boxing)
- pianificazione sequenziale rigorosa allocazione rigida delle prime fasi del progetto esclusivamente alle attività OSINT enumerazione e mappatura rimandando le attività di exploitation a una fase successiva
- uso di strumenti di automazione e correlazione impiegando framework di automazione per eseguire ricerche parallele su centinaia di fonti OSINT contemporaneamente accellerando la scoperta di asset nascosti
metodologia di evasione dei sistemi di monitoraggio (stealth technique)
- scansione temporizzate diluizione dei pacchetti nel tempo per evitare di generare picchi di traffico che farebbero scattare i detention control
- rotazione di indirizzi IP utilizzo di proxy VPN o infrastrutture temporanee per distribuire le richieste di scansione e di probing da indirizzi IP sorgente sempre differenti impedendo al blue team di bloccare l'intera attività con una singola regola di firewall

## le 5 fasi del pen test
la fase di ricognizione è il pilastro fondamentale raccogliere informazioni permette di capire i vettori d'attacco possibili per evitare il rilevamento

**azione 1**
raccolta informazioni sul bersaglio
- analisi dell'organigramma ricerca ruoli chiave
- identificaione della supply chain

metodologia tech stack discore 
- analisi dlele offerte di lavoro
- fingerprint passivo utilizzando piattaforme come builtwith o wappalyzer per analizzare l'architettura del sito web principale senza inviare pacchetti malevoli

**azione 2 utilizzo di fonti pubbliche per raccogliere dati**
l'obiettivo è raccogliere dati del bersaglio tramite ricerche di dominio pubblico come facebook ecc

metodologia di ricerca su motori di ricerca (google hacking / dorking)
- ricerca di file sensibili 
- scoperta di directory esposte 
metodologia di osint sui social mediae repository
- analisi linkedin
- analisi di github / gitlab

**azione 3**
definire con precisione matematica i confine del perimetro digitale dlel'azienda

metodologia di enumerazione
- brute force dei subdomini
- analisi dei certificati SSL interrogazione database pubblici

metodologia di email harvesting raccolta email
- estrazione automatizzata utilizzando tool come theharvest o hunter.io per raccogliere gli indirizzi email aziendali presenti sul web
- identificazione del patter di login

metodologia di mappatura degli indirizzi IP e ASN
- identificazione ASN autonomous system number
- infrastrutture cloud

**scansione e analisi**
interagire attivamente con gli asset individuati nella fase di ricognizione per mappare l'infrastruttura di rete indietificare i servizi esposti e rilevare le prime vulnerabilità potenziali

individuazione dei servizi attivi sulle porte
determinare quali porte logiche TCP/UDP sono aperte sul bersaglio

metodologia di port scanning
- TCP SYN SCAN invio di un pacchetto SYN se l'host risponde con SYN/ACK la porta è aperta il tester risponde subito con RST anziche completare l'handshake evitando di stabilire una sessione completa
- UDP scanning invio di pacchetti vuoti o specifici per protocollo alle porte UDP la mancata risposta indica che la porta è aperta
- analisi dello stato dei firewall utilizzo di pacchetti TCP ACK per dedurre se le porte sono protette da un firewall di tipo stateful o stateless in base ai codici ICMP di ritorno o alla mancanza di risposta

## utilizzo di strumenti automatici come Nmap
standardizzare e velocizzare la mappatura della rete esterna o interna tramite l'uso di comandi avanzati e script automatici

metodologia di esecuzione Nmap avanzata
- scansione di base ad alta efficenza uso del comando **nmap -sS -Pn -p- target** per scansionare tutte le 65535 porte TCP ignorando i blocchi ICMP
- automazione con Nmap scripting engine NSE **--script vuln** 

## identificazione dei sistemi operativi e delle versioni
metodoologia di service and os fingerprinting
- version detection uso del comando nmap -sV per analizzare risposta dei servizi e confrontarlo con database interno di firme software
- os detenction via TCP/IP Stack comando nmap -O per inviare un pacchetto TCP/UDP appositamente alterati il tool analizza le minime differenze nel modo in cui i diversi sistemi operativi linux windows ios festiscono i flag TCP la dimensione finestre e valori

**ottenimento dell'accesso**
sfruttamente attivo delle falle di sicurezza confermate per superare il perimetro di difesa ed eseguire un condice non autorizzato all'interno del sistema bersaglio

**sfruttamento vulnerabilità scoperte**
sfruttamente delle vulnerabilità per un accesso abusivo reale superando controlli di sicurezza

metodologia di exploitation mirata
- sfruttamento di falle note CVE 
- attacchi alla web application sfruttare vulnerabilità logiche per costringere il server web a restituire i dati del database o a eseguire comandi di sistema

**utilizzo di framework come metasploit**
ingegnerizzare l'attacco gestire i payload e stabilire sessioni di controllo stabili

metodologia di pen test assisti da framework
- selezione e configurazione ricerda del modulo di exploit corretto all'interno della console metaploit impostazione parametri dell'host remoto e della porta
- generazione del payload configurazione di un payload avanzata come una sessione meterpreter in modalità reverse TCP per far in modo che sia la macchina attaccata a collegarsi con il proprio pc del tester aggirando i blocchi del firewall aziendale

**violazione dei sitemi per dimostrareil rischio**
acquisire prove concrete dell'avvenuta intrusione senza causare danni

metodologia di validazione del rischio
- cattura di prove estrazione di informazioni non distruttive ma inconfutabili (per trovare nome utente whoami)
- data pillaging dimostrazione di capacità di accedere a tabelle contenenti dati confidenziali

mantenimento dell'accesso
- una volta penetrati nella macchina bisogna garantire che l'accesso rimanga disponibile anche dopo il riavvio della macchina

metodologia persistenza
- uso di task pianificati configurando un task che periodicamente crea una connessione al server del tester

metodologia di command e control
- utilizzo di beaconing mascherato configurando agenti locali affinche inviino segnali di controllo (beacon) all'esterno a intervalli di tempo irregolari o casuali (jittering) per confondere i sistemi di analisi del traffico di rete

protocolli leggitimi per c2
- transito del traffico di controllo all'interno di protocolli standard approvati per eludere i controlli di deep packet inspection(DPI) come richeiste https o query DNS apparentemente legittime

**movimento laterale**
l'obiettivo è utilizzare una macchina compromessa di basso livello per usarla come ponte per estendere il controllo a server superiori

metodologia di propagazione interna
- pivoting di rete configurando una macchina compromessa come proxy di rete per permettere ai tool del tester di raggiungere segmenti lan altrimenti inaccessibili come creare un SSH tunneling o usare tool come Chisel
- credential dumping (estrazioni credenziali) dei token di autenticazione o delle password memorizzate in memoria per riutilizzarle su altri computer della rete tramite tecniche di pass-the-hash o pass-the-ticket tool mimikatz 

## analisi e reportistica
trasfromare l'attività tecnica in reposrtistica che assume un valore per l'azienda fornendo alla dirigenza e al team IT i dati necessari per comprendere i rischi e sanare le vulnerabilità

**documentazione dettagliata**
l'obiettivo è strutturare un registro tecnico chiaro che descriva i passaggi esatti necessari a riprodurre le vulnerabilità scoperte

metodologia di stesura tecnica
- sezione walkthrough di attacco descrizione cronologica
- classificazione standardizzata CVE e CWE

valutazione dell'impatto aziendale

metodologia di calcolo del rischio
- scoring CVSS v3.1/v4.0 calcolando il punteggio di gravità combinando la complessità dell'attacco i privilegi richiesti 
- analisi dell'impatto sul business correlando la macchina vulnerabile con la sua effettiva funzione aziendale

**fornitura di linee guida per remediation**

metodologia remediation
- soluzioni specifiche (patching/hardening) indicazione precisa degli aggiornamenti software da installare o delle stringhe di configurazione da modificare
- contromisure temporanee workaround utilizzando regole di blocco temporanee sul WAF o sul furewall aziendale nel caso in cui una patch ufficiale non sia applicabile immediatamente per motivi di business o compatibilità software

regole d'ingaggio formali per conformità ad accesso a sistemi informatici

definizione contrattuale del perimetro (scope)
-  documento formale e legale firmato da entrambe per le parti che definisce i confini operativi dell'attività

metodologia di whitelisting degli Asset
- infrastruttura di rete elenco degli indirizzi IP subnet e fully qualified domani names inclusi nel test
- applicativi web elenco degli url esatti e delle API specificando anche gli endpoint su cui è permesso effettuare i test applicativi
- esclusioni esplicite (blacklist) indicazione formae di sistemi critici che non devono essere toccati come server pagamenti sistemi industriali servizi SaaS di terze parti 

**gestione delle tempistiche e delle modalità di attacco minimizzando il rischio di disservizi aziendali e pianificando impatto operativo**

metodologia di pianificazione temporale
- finestre temporali (maintenance windows) per orari di esecuzione dei test piu invasivi per non impattare sull'operatività
- livello di aggressività definizione della velcoità massima di scansione e divito o autorizzazione all'uso di tecniche distruttive Ddos o exploit che causano crash del servizio

**canali di comunicazione e clausa get out the jail**
Procedure in caso di emergenza o incidenti reali o blocchi di sistema durante l'attività

metodologia di esclation delle comunicazioni
- contatti di emergenza point of contact scambio di numeri di telefono tra responsabili tecnici sia red team che blue team 24/24
- lettera di manleva documento cartaceo o digitale firmato dall'amministratore delegato dell'azienda cliente per dimostrare autorizzazione formale qualora i sistemi di sorveglianza o le forze dell'ordine rilevino l'attacco

struttura report tecnico

matrice visiva, speigazione dell'impatto reale, dettagli delle vulnerabilità (punteggio CVSS, asset impattato, descrizione falla, proof of concept/passi per la produzione),inviare richiesta http modificata tramite proxy (burp suite), impatto tecnico, soluzoone consigliata remediation

# ambiti di aplicaizone del pen test

**network pen test**
valutare la sicurezza della rete identificando configurazioni errate nei dispositivi di rete protocolli insicuri o sistemi non aggiornati

metodologia per network pen test
- externa network identificazione e test degli host perimetrali firewall router gateway VPN per trovare porte aperte e servizi vulnerabili
- internal network simulando un attaccante che ha gia superato i sistemi di sicurezza perimetrali per verificare l'efficenza della segmentazione di rete
- analisi della ACL access control list per verificare regole di firewall per identificare permessi troppo permissivi
- test sui protocolli di routing e switching tentando di attacare i protocolli infrastrutturali come OSPF/BGP( route injection) o attacchi ARP spoofing e mac flooding per intercettare il traffico di rete sugli switch
- verifica delle interfacce di gestione controllando l'uso dei protocolli

**web application pen test analisi di siti API**

metodoologia per web applicatione pen test
- adozione del framework owasp struttuzaione dei testi attorno alla owasp top 10
- analisi e test delle API verifando autenticazione e autorizzazione per vulnerabilità BOLA modificando ID in una richiesta API o inserimento di "is_admin":true nel json di registrazione per scalare privilegi

manipolazione dei flussi applicativi
- utilizzo di proxy locali (burp suite, owasp zap) per intercettare analizzare e modificare le richieste http in transito
- test di input sanitization per forzare vulnerabilità di cross site scripting o sql injection

wireless pen test verifica delle reti wifi e protocolli radio
valutazione della robustezza delle reti senza fili

metodologia per wireless pen test
- ricognizione dello spettro radio mappando gli access point aziendali i canali utilizza e dei relativi protocolli di sicurezza tramite tool come Airodump-ng o kismet
- attacchi ai protocolli di autenticazione WPA2/WPA£ pre-shared key (PSK) de-autenticazione forzata dei client legittimi per catturare l'handshake e successivo cracking offline della password tramite dizionari o brute force
- enterprise authentication configurazione di un Rouge access point per indurre i dispositivi dipendenti a connettersi automaticamenti catturando le credenziali di dominio tramite tool come EAPHammer
- rilevamento di access point non autorizzati verificando la presenza di router o chiavette wifi non autorizzate ocllegate fisicamente alla rete aziendale dai dipendenti che aggirano le difese perimetrali

**social engineering test del personale tramite phishing o vishing**
valutare la consapevolezza della sicurezza del fattore umano simulando scenari di manipolazione logica

metodologia per social engineering
- campagne di phishin pianificando scenario con email contestuali e credibili configurando piattaforme di simulazione registrazione di domini inganenvoli e bypass dei filtri ed email e tenendo traccia di quanti dipendenti aprono l'email quanti click avvengono sul link e quanti inseriscono le credenziali nella apgina clone ( credential harvesting)
- vishing(voice) e smishing(sms) simulazioni telefoniche mirate ai dipendenti fingendosi tecnici o dirigenti per convincerli a rilevare password codici OTP o informazioni riservate
- tailgating/piggybacking tentativo di accedere fisicamente agli uffici aziendali seguendo dipendenti autorizzati attraverso i varchi valutando il livello di controllo del personale di vigilanza

**strumenti essenziali toolbox**
l'efficacia del pen tester dipende dalla conoscienza degli strumenti utilizzati

**kali linux**
- è una distribuzione open source basato su debian ingegnerizzato specificatamente per attività di pen test

metodologia d'uso ed elementi chiave
- gesitone centralizzata del toolset con oltre 600 strumenti specialistici preinstallati e preconfigurati caatalogati secondo le fasi della metodologia standard (information gathering, vulnerability analysis, web appplicaiton analysis , exploitation, post-exploitation)

metodologia di distribuzione e isolamento
- live boot con persistenza cifrata utilizzando il sistema operativo da supporti usb avviabili senza installazione su disco garantendo integrità dell'ambienti di test e la cancellazione delle tracce sul sistema ospite
- ambiente virtualizzati eseguendo kali linux all'interno di una virtual box impostando interfacce di rete in modalità bridge per interagire diretamente con la lan o host-only per test in laboratori isolati

kernel ottimizzato per l'iniezione di pacchetti poice include driver patchati nativamente per supportare la modalità monitor e l'iniezione di pacchetti sulla scheda di rete wifi indispensabili per i test radio

**Nmap**

scanner di rete e mappature porte script in linguaggio Lua

**burp suite applicazione per security test su applicazioni web funzionante come proxy**

intercettazione traffico  configurando il browser per instradare il traffico verso l'indirizzo locale installazione del certificato di Burp all'intenro del browser per consentire la decifratura e la successiva ricifratura del traffico SSL/TLS funziona da MAN IN THE MIDDLE ... isolamento di una singola richiesta HTTP e inoltro al module Repeater modifica manuale dei parametri (cookie intestazioni variabili post) per testare vulnerabilità di tipo idor o sqli osservando in tempo reale le variazioni nella risposta del server , definizione di posizioni specifiche all'intenro di una richeista http (payload position) iniezione automatica di liste di parole per effettuare attacchi di forza bruta brute force sulle password o per enumerare directory o file nascosti sul web server

**metasploit framework pe rlo sviluppo ed esecuzione di exploit**

framework open source per sviluppo testing ed esecuzione di exploit contro macchine note tramite exploit codice che sfrutta attivamente le vulnerabilità per creare un varco , payload codice malevolo eseguito sulla vittami, auxiliary moduli utilizzati per attività secondarie di scansione sniffing o enumerazione di servizi gestione avanzata delle sessioni meterpreter uso del payload per ottenere una shell estesa interamente residente nella memoria ram dell'host compromesso riducendo la scrittura di file su disco esecuzione di comandi di post-exploitation integrati come sysinfo per raccogliere dati sul sistema hashdump per estrarre hash delle password

**wireshark**
packet analyzer che permette do catturare e ispezionare capillarmente il traffico dati in transito su un interfaccia di rete catturando in modalita promiscua per forzare la scheda di rete a catturare tuti i pacchetti in transito , isolamento dei dati tramite filtri di visualizzazione isolamento del target, selezioni di un singolo pacchetto e utilizzo della funzione di tracciamente del flusso per riassemblare l''intera conversazione sequenziale questa metodologia permette di estrarre credenziali file trasferiti o comandi inviati in chiaro attraverso protocolli non sicuri (FTP, HTTP, TELENT)

