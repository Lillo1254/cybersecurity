# SPAZI DI NOMI
Policy per quanto riguarda l'identificativo dei nomi utente per esempio il nome utente di un dipendente di un azienda chiamato username puo avere applicata una policy al riguarda che per gestire l'unicità dello username stesso applica nome di battesimo + numero di matricola
Le policy delle password invece osno gestite direttamente da chi crea e gestisce il framework di sicurezza implementando policy standard e policy aggiuntive
NIST → standard statunitensi per sicurezza informatica
NSA → linee guida di sicurezza avanzate (USA)
NIS2 → direttiva europea per la sicurezza delle infrastrutture critiche

# SERVER
Un server è un dispositivo hardware o un software che fornisce servizi, dati o risorse ad altri dispositivi chiamati client attraverso una rete. In pratica, il server riceve richieste, le elabora e restituisce una risposta, secondo il modello client‑server
puo essere:
- Hardware: un computer fisico progettato per funzionare 24/7, con elevate prestazioni e affidabilità.
- Software: un programma che offre un servizio specifico (es. web server, mail server)
Come funziona un server:
- Un client invia una richiesta (es. aprire una pagina web).
- Il server la riceve e cerca la risorsa richiesta.
- Il server invia la risposta al client.
si puo gestire da remoto tramite protocolli TELNET ( non piu utilizzato poiche trasmetteva dati in chiaro), SSH con trasmissione cifrata

# IPSEC
IPsec (Internet Protocol Security) è una suite di protocolli progettata per rendere sicure le comunicazioni su reti IP, garantendo crittografia, autenticazione e integrità dei pacchetti dati. È utilizzato soprattutto nelle VPN, nelle comunicazioni tra router e nelle connessioni sicure tra dispositivi
cosa fa:
- Crittografia → impedisce che terzi leggano i dati
- Autenticazione → verifica l’identità del mittente
- Integrità → assicura che i pacchetti non siano stati modificati
- Base delle VPN moderne

# INFRASTRUTTURE PKI (public key infrastructure)
composte da 5 diversi tipi di componenti
- Autorità di certificazione
- Autorità di registrazione organizzativa
- Titolari dei certificati
- Client/verificatori (software che validano firme digitali)
- Repository dei certificati e delle CRL

Funzioni delle PKI
- Registrazione
- Inizializzazione
- Certificazione
- Recupero coppia di chiavi
- Generazione delle chiavi
- Aggiornamento delle chiavi
- Certificazione incrociata
- Revoca

# BIG DATA
Raccolta di dati utilizzata per verificare e attesta cosa è successo in passato , monitorare al presente e ad oggi utilizzati per predizioni future tramite dei "sensori" connessi ad internet tramite indirizzo IP e MAC address inviando dati ad un database(strutturati, schema rigido) o data lake(non strutturati o semi-strutturati, flessibili, usati per analisi avanzate), successivamente tramite software programmato per restituire risultati anche a livello predittivo
Utilizzi:
- Analisi del passato
- Monitoraggio del presente
- Predizioni future (machine learning)

# LDAP
LDAP è un protocollo che permette di:
- cercare e recuperare informazioni da una directory organizzata in modo gerarchico
- autenticare utenti e gestire autorizzazioni
- centralizzare la gestione di utenti, gruppi e risorse in una rete aziendale
- È ampiamente usato in sistemi come Active Directory, OpenLDAP, eDirectory
- Opera tipicamente sulla porta 389, mentre la versione sicura LDAPS usa la porta 636 e aggiunge crittografia SSL/TLS
LDAP E LDAPS
- LDAP → comunicazione in chiaro (porta 389)
- LDAPS crittografia SSL/TLS (porta 636), consigliato per credenziali e dati sensibili 

## voip (voice over IP)
Tecnologia che permette di trasmettere la voce tramite Internet anziché tramite rete telefonica tradizionale
Caratteristiche:
- utilizza protocolli come SIP, RTP, H.323
- permette chiamate, videochiamate, conferenze
- richiede banda minima e bassa latenza
Vantaggi:
- costi ridotti
- scalabilità
- integrazione con software (softphone, centralini IP)

# MINACCE INFORMATICHE
Per Malware si intende un software dannoso creato per danneggiare, infiltrarsi o prendere il controllo di dati di un utente senza il suo consenso

## VIRUS
Programma che si attacca a file eseguibili e si diffonde quando vengono aperti può replicarsi e diffondersi ad altri file o dispositivi può danneggiare dati, rallentare il sistema o aprire backdoor
Come si diffonde:
- allegati email
- chiavette USB
- software pirata
- macro infette (es. Office)

Come proteggersi:
- antivirus aggiornato  rileva firme note e comportamenti sospetti
- evitare allegati sospetti  i virus spesso si mascherano da documenti innocui
- aggiornare il sistema molte infezioni sfruttano vulnerabilità già risolte
- Disabilitare macro non necessarie vettore comune nei virus moderni
## WORM
Simile al virus, ma si diffonde autonomamente tramite rete senza intervento umano sfrutta vulnerabilità nei protocolli o nei sistemi operativi può generare traffico enorme e causare DDoS involontari
Protezione:
- firewall attivo blocca connessioni non autorizzate che i worm usano per propagarsi
- patch di sicurezza  i worm sfruttano vulnerabilità note (es. WannaCry → SMBv1)
- IDS/IPS  rilevano traffico anomalo tipico dei worm (scansioni massicce, tentativi ripetuti)
- Segmentazione di rete limita la diffusione interna
## RANSOMWARE
Cripta i dati rendendoli inaccessibili alla vittima per chiedere un riscatto alla stessa per riaverli indietro tramite chiave di decrittazione ma non c'è garanzia che questo avvenga
Protezione:
- backup offline unica vera garanzia di recupero
- aggiornamenti chiudono vulnerabilità sfruttate dai ransomware
- non aprire allegati sospetti questi sono vettore principale
- MFA  riduce compromissioni tramite credenziali rubate
- Least privilege un utente senza privilegi non può cifrare tutto il sistema
- Application whitelisting blocca eseguibili non autorizzati
## SPYWARE
Raccoglie informazioni dell’utente senza consenso monitora attività, tasti premuti, siti visitati può rubare credenziali, dati bancari, cookie di sessione
Protezione:
- antispyware rilevano comportamenti di keylogging o esfiltrazione
- evitare software pirata spesso contiene spyware nascosto
- controllare permessi app molte app mobili chiedono accessi non necessari
- Browser aggiornato riduce exploit che installano spywar
## PHISHING
Tecnica per rubare credenziali tramite email o siti falsi induce l’utente a inserire credenziali o dati sensibili può installare malware tramite allegati
Protezione:
- verificare mittente  controllare dominio reale
- cercare possibili incongruenze  errori, loghi falsi, domini simili (es. rnicrosoft invece di microsoft)
- non cliccare link sospetti usare sempre il sito ufficiale
- attivare MFA anche se rubano la password, non possono accedere
- Filtro antiphishing del browser blocca siti noti come malevoli
## ATTACCHI DDOS
Un attacco Distributed Denial of Service sovraccaricano un server con traffico massiccio inoltrando richieste tramite botnet(computer compromessi controllati da remoto ) o exploit di indirizzamento può sfruttare amplification attacks (DNS, NTP, SSDP)
Protezione:
- CDN distribuisce il traffico su più server
- Firewall avanzati / WAF → filtrano richieste malevole
- sistemi anti-DDoS  mitigano automaticamente picchi anomali
- Rate limiting che limita richieste per IP
- Anycast routing che distribuisce il carico su più nodi globali
## ATTACCO BRUTE FORCE
Tentativi ripetuti di indovinare password tramite script che prova tutte le possibili combinazioni utilizzando a volte in principio un "dizionario" una raccolta di parole possibili date di nascita ecc quindi non colpendo alla cieca o sfruttando credenziali rubate da altri siti (credential stuffing)
Protezione:
- password robuste lunghe, complesse, non riutilizzate
- blocco tentativi impedisce tentativi infiniti
- MFA anche con password indovinata, l’accesso fallisce
- Captcha che blocca tentativi automatizzati
- Monitoraggio accessi che rileva tentativi sospetti

# Application Whitelist
L’Application Whitelist è una delle difese più potenti contro malware e ransomware È una lista di applicazioni autorizzate che possono essere eseguite su un sistema.
Tutto ciò che non è nella lista viene bloccato automaticamente
- un malware non può avviarsi se non è nella whitelist
- blocca ransomware, virus, worm e spyware anche se non sono ancora conosciuti
- impedisce l’esecuzione di file .exe, .js, .vbs, .ps1 non autorizzati
- limita l’uso di software pirata o non controllato

# INGEGNERIA SOCIALE
Una delle minacce piu pericole e piu impattante poiche non richiede utilizzo di software o competenze tecniche digitali particolare ma una valutazione della vittima psicologica e l'utilizzo di tecniche di persuasione basate su:
- impersonificazione L’attaccante si finge una persona affidabile (collega, tecnico IT, banca, fornitore, ente pubblico) per ottenere informazioni o accessi.
- creazione di fiducia L’attaccante usa leve psicologiche come urgenza, paura, autorità, curiosità o empatia per convincere la vittima ad agire senza riflettere.
- Una volta ottenuta la fiducia, l’attaccante utilizza le informazioni recuperate (spesso trovate anche online o nei sistemi aziendali) per:
    - richiedere denaro
    - rubare credenziali
    - accedere ai sistemi informatici
    - impossessarsi dei dati della vittima
    - chiedere un riscatto (estorsione)
__L’obiettivo finale è ingannare la persona, non il computer__