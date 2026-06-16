# FIREWALL (hardware e software)
Quando parliamo di firewall, ci riferiamo a sistemi — hardware o software — progettati per controllare il traffico di rete e impedire accessi non autorizzati.
Nel tempo si sono evoluti in quattro generazioni principali, ognuna più intelligente e sicura della precedente.
1) Firewall a filtro di pacchetti (prima generazione)
Questi sono i firewall più semplici e più antichi.
Analizzano solo i pacchetti in modo isolato, senza alcuna informazione sul contesto della comunicazione.

**Cosa controllano? I parametri statici:**
- IP sorgente
- IP destinazione
- Porta sorgente
- Porta destinazione
- Protocollo (TCP, UDP, ICMP…)

Questi campi sono “statici” perché appartengono all’header del pacchetto e non cambiano durante il viaggio.

**Perché non sono sufficienti?**

Perché possono essere facilmente ingannati tramite spoofing.

**Cos’è lo spoofing?**

Lo spoofing è una tecnica in cui un attaccante falsifica l’identità di un pacchetto, ad esempio modificando l’IP sorgente per farlo sembrare proveniente da una macchina affidabile.
È come se qualcuno ti inviasse una lettera firmata con il nome di un tuo amico: tu ti fidi, ma la lettera non è sua.
I firewall di prima generazione non hanno modo di accorgersene.

2) Stateful Inspection Firewall (seconda generazione)
Questi firewall rappresentano un enorme passo avanti.
A differenza dei precedenti, non guardano solo i pacchetti, ma tengono traccia dello stato della connessione.

**Cosa significa “stato”?**

Il firewall mantiene una tabella delle connessioni attive, dove registra:
- chi ha iniziato la comunicazione
- quali porte sono state aperte
- quali pacchetti appartengono alla stessa sessione

**Perché è più sicuro?**

- Perché può verificare se un pacchetto:
- appartiene a una connessione già esistente
- è coerente con la logica della comunicazione

In pratica impedisce che un host invii una risposta se non c’è stata una richiesta.
Questo blocca molti attacchi basati su pacchetti falsificati.

3) Proxy Firewall (Application Level Gateway)
Questi firewall lavorano a un livello ancora più alto: il livello applicativo.

**Come funzionano?**

Agiscono come intermediari:
- Client → Proxy → Server di destinazione
- Il client non comunica mai direttamente con il server esterno.

**Cosa possono fare?**

Analizzano il contenuto delle richieste, non solo gli header.
**Possono quindi bloccare:**
- richieste HTTP sospette
- comandi FTP pericolosi
- traffico non conforme ai protocolli

Sono molto efficaci per controllare applicazioni specifiche.

4) Next-Generation Firewall (NGFW)
I firewall più moderni combinano tutte le funzioni precedenti e aggiungono tecnologie avanzate.

**Cosa includono?**
- DPI (Deep Packet Inspection)  
    - Analisi approfondita del contenuto dei pacchetti, anche all’interno dei dati applicativi.

IPS (Intrusion Prevention System)  
- Sistema che riconosce e blocca attacchi in tempo reale, basandosi su firme e comportamenti anomali.

**Analisi malware  **
- Il firewall confronta il traffico con database di minacce note e può usare sandbox per analizzare file sospetti.

**Perché sono indispensabili oggi?**

Perché riconoscono l’uso anomalo degli stessi protocolli.
Esempio:
- HTTP legittimo vs HTTP usato per esfiltrare dati.
- Cosa sono le APT (Advanced Persistent Threat)?
- Le APT sono minacce avanzate e persistenti:
    - attacchi sofisticati, mirati e di lunga durata, spesso condotti da gruppi organizzati.

Caratteristiche:
- obiettivi specifici (aziende, enti governativi…)
- tecniche avanzate
- lunga permanenza nella rete senza essere scoperti
- furto di dati sensibili o sabotaggio
  
**I NGFW sono progettati proprio per contrastare questo tipo di attacchi.**

5) SSL Forward Proxy (Man-in-the-Middle legittimo)
L’SSL Forward Proxy è una tecnica utilizzata dai firewall aziendali per intercettare, decifrare, analizzare e ricifrare il traffico HTTPS dei dipendenti.
È un man-in-the-middle autorizzato, usato per motivi di sicurezza.

L’obiettivo è semplice:

controllare cosa passa dentro il traffico cifrato, che altrimenti sarebbe invisibile al firewall.
**PC Utente → Firewall → Internet → Firewall → PC Utente**

**COME FUNZIONA**
1) Il client invia una richiesta HTTPS
- Il PC dell’utente vuole visitare un sito sicuro, ad esempio: https://www.google.it
- La richiesta arriva al firewall
2) Il firewall NON inoltra subito la richiesta
- Il firewall intercetta la connessione e non lascia che il client parli direttamente con il server esterno
- legge il nome del sito richiesto (SNI)
3) Il firewall crea un certificato “falso”
- Il firewall genera un certificato per https://www.google.it ma firmato dalla CA interna dell’azienda
- per funzionare deve essere installata la stessa CA sul pc che invia la richiesta marcata come attendibile
4) Il firewall invia il certificato falso al client
- Il PC dell’utente vede un certificato valido (perché la CA interna è fidata) e avvia l’handshake con il firewall, non con il server reale.
- il client cifra i dati con la chiave pubblica del firewall
- il firewall può decifrarli
5) Il firewall apre una seconda connessione verso il server reale
Ora il firewall si comporta come un client:
- si collega al vero server https://www.google.it
- fa un handshake SSL autentico
- riceve il certificato reale del sito
- **doppia connessione** Client ↔ Firewall  (HTTPS 1) e poi Firewall ↔ Server  (HTTPS 2)
6) Il firewall decifra, analizza e ricifra il traffico
Il firewall:
- decifra i dati provenienti dal client
- analizza il contenuto con i suoi motori di sicurezza
- se tutto è ok, ricifra i dati con la chiave del server reale
- li inoltra verso Internet
  
**E lo stesso processo avviene al ritorno.**

**Cosa analizza il firewall?**
1) Malware
- file scaricati
- script malevoli
- exploit
- payload nascosti nel traffico HTTPS

2) Violazioni della privacy o delle policy aziendali
Esempi:
- invio di dati sensibili verso siti non autorizzati
- upload di database aziendali su cloud personali
- utilizzo di protocolli vietati
- accesso a siti non conformi alle policy

3) Comportamenti anomali
- tunneling dentro HTTPS
- traffico cifrato usato per esfiltrare dati
- connessioni verso server Command & Control

Perché serve installare la CA interna?
Perché il firewall deve essere in grado di:
- generare certificati “al volo”
- farli accettare ai browser dei dipendenti
- evitare errori di sicurezza
- Senza la CA interna installata, Chrome/Firefox/Edge mostrerebbero:
**“La connessione non è privata”**

**Cos’è una Group Policy (GPO)?**
Le Group Policy sono regole amministrative usate nelle reti Windows aziendali per configurare automaticamente i computer del dominio.

Permettono di:
- installare certificati
- configurare browser
- impostare restrizioni
- distribuire software
- applicare policy di sicurezza

Una GPO viene applicata a:
- utenti
- gruppi
- computer
- intere OU (Organizational Unit)

In questo caso, la GPO serve per:
- Installare automaticamente il certificato della CA interna su tutti i PC aziendali e marcarlo come attendibile.

1) SNI — Server Name Indication
Lo SNI è un’estensione del protocollo TLS che permette al client di comunicare al server il nome del dominio che vuole raggiungere prima che inizi la cifratura esiste poiche molti server ospitano più siti sullo stesso indirizzo IP (hosting condiviso) quindi il server deve sapere quale certificato presentare.
è importante il firewall perche lo SNI è in chiaro quindi il firewall può vedere il dominio richiesto anche se il resto della comunicazione è cifrato ma questo permette il filtraggio del dominio la categorizzazione del traffico e l'applicazione delle policy come il blocco per i social il gambling ecc..

2) ETA — Encrypted Traffic Analytics
L’ETA è una tecnica avanzata che permette di analizzare il traffico cifrato senza decifrarlo.
**Come funziona?**

l firewall osserva metadati e pattern comportamentali, come:
- lunghezza dei pacchetti
- frequenza
- tempi tra i pacchetti
- caratteristiche dell’handshake TLS
- anomalie statistiche
Senza violare la privacy, può riconoscere:
- malware che usa HTTPS
- traffico verso server Command & Control
- tunneling nascosto dentro TLS
- comportamenti anomali rispetto al traffico legittimo
**Non richiede decifrazione → meno uso di risorse hardware e nessun impatto sulla privacy**

3) Uso di risorse hardware
L’ispezione SSL completa (SSL Forward Proxy) richiede:
- CPU per decifrare
- CPU per ricifrare
- memoria per mantenere le sessioni
- motori di analisi (IPS, antimalware, DLP)
Per questo molte aziende usano:
- ETA per il traffico generico
- SSL inspection solo per categorie ad alto rischio

4) Certificati Pinned (Certificate Pinning)
Il certificate pinning è una tecnica usata da app e siti per evitare attacchi MITM.

Come funziona?
L’applicazione memorizza:
- l’hash del certificato
- o la chiave pubblica del server
- o un certificato specifico
- Se il certificato ricevuto non corrisponde, la connessione viene bloccata.

**Perché è un problema per i firewall?**
Perché il firewall, facendo MITM, presenta un certificato diverso.
Risultato:
- l’app rileva l’anomalia
- la connessione fallisce
- il firewall non può ispezionare quel traffico
Esempi tipici:
- app bancarie
- app governative
- servizi di sicurezza
- alcune app di messaggistica

5) Creazione di una Whitelist SSL
Le aziende creano una whitelist di domini o applicazioni che:
- non devono essere ispezionati
- devono essere lasciati passare con SSL originale

Esempi:
- home banking
- servizi sanitari
- servizi governativi
- app con certificate pinning
- siti che trattano dati sensibili (privacy)

**Perché serve?**
Per evitare:
- problemi legali
- problemi di privacy
- malfunzionamenti delle app
- errori di certificato

6) Bypass SSL
Il bypass SSL significa che il firewall:
- NON intercetta
- NON decifra
- NON analizza
il traffico verso determinati domini.

**È una conseguenza della whitelist.**

7) Identificazione SSL
Quando il firewall non può decifrare il traffico (per pinning, privacy, whitelist), può comunque:
- identificare l’applicazione
- categorizzare il traffico
- applicare policy di controllo

Usa:
- SNI
- certificato del server
- fingerprint TLS
- ETA
- analisi comportamentale

Quindi anche senza vedere il contenuto, può:
- bloccare categorie (es. gambling, adult, cloud storage)
- applicare QoS (**QUALITY OF SERVICES** priorità a servizi specifici togliendo banda a servizi superflui es. priorità a voip videocall e meno banda per social streaming e download)
- registrare log
- rilevare anomalie

# policy BYOD ( bring your own device)

La BYOD è una politica aziendale che permette ai dipendenti di usare i propri dispositivi personali (smartphone, tablet, laptop) per lavorare: accedere alle email aziendali, ai documenti, alle app interne, ai sistemi gestionali **Invece di darti un telefono aziendale, puoi usare il tuo. Ma seguendo regole precise**

**Le motivazioni principali sono tre: costi, produttività, flessibilità**
1) Riduzione dei costi
- L’azienda non deve comprare smartphone, tablet o PC per tutti.
- Non deve gestire manutenzione, sostituzioni, aggiornamenti hardware
  
2) Aumento della produttività
- Le persone lavorano più velocemente con un dispositivo che conoscono già.
- Esempio: un dipendente risponde alle email dal proprio smartphone anche fuori ufficio
  
3) Maggiore flessibilità
Perfetto per:
- smart working
- lavoro ibrido
- tecnici e commerciali sempre in movimento

Per implementare questa policy aziendale servono delle regole ben specifiche stipulate dall'azienda stessa per:
- quali dispositivi sono ammessi
- quali sistemi operativi minimi
- quali app aziendali si possono installare
- quali comportamenti sono vietati

**MDM / MAM – Mobile Device Management**

L’azienda installa una gestione separata sul dispositivo del dipendente.
Serve per:
- separare dati personali e aziendali
- poter cancellare solo i dati aziendali in caso di furto
- imporre PIN, cifratura, aggiornamenti
- controllare l’accesso alle app aziendali
- Esempi: Microsoft Intune, VMware Workspace ONE, MobileIron.

**Cifratura e autenticazione forte**

La policy richiede:
- PIN o biometria obbligatori
- cifratura del dispositivo
- autenticazione a due fattori (MFA)

**Segmentazione dei dati**

I dati aziendali devono essere contenuti in un’area protetta, separata da foto, app personali, WhatsApp, ecc.

**Formazione del personale**

La BYOD funziona solo se i dipendenti capiscono:
- cosa possono fare
- cosa non possono fare
- perché le regole esistono

## Monitoraggio e Statuto dei Lavoratori
L’azienda può utilizzare strumenti che possono controllare l’attività del lavoratore solo per esigenze organizzative, produttive, di sicurezza o tutela del patrimonio aziendale quindi "non è vietato il controllo, ma è vietato il controllo “per controllare il lavoratore” e Il controllo è ammesso solo come effetto collaterale dell’uso di strumenti necessari al lavoro

## Accountability
L’accountability è il principio secondo cui ogni attività deve avere un responsabile chiaro, che risponde delle decisioni prese e delle conseguenze che ne derivano

## Finalità ammesse del monitoraggio
Le finalità ammesse sono solo queste quattro:
- Esigenze organizzative  
    - garantire continuità del servizio, bilanciare carichi di lavoro.

- Esigenze produttive  
    - monitorare performance dei sistemi, non delle persone.

- Sicurezza del lavoro e delle infrastrutture  
    - prevenire intrusioni, malware, accessi non autorizzati.

- Tutela del patrimonio aziendale  
    - proteggere dati, asset, proprietà intellettuale.

**Qualsiasi monitoraggio che esce da queste finalità è illegittimo**

## Filtraggio e analisi dei log
Il filtraggio del traffico Internet, l’analisi dei log, il controllo degli accessi sono leciti se rispettano tre condizioni:
1) Finalità legittima
Devono servire a:
- sicurezza informatica
- prevenzione incidenti
- continuità operativa
- tutela del patrimonio aziendale

2) Proporzionalità
- Non si possono raccogliere più dati del necessario.
Esempio:
Log di accesso → ok
Registrare ogni singolo sito visitato con dettaglio minuto per minuto → eccessivo

3) Minimizzazione dei dati personali
I log devono essere:
- anonimizzati quando possibile
- conservati per un tempo limitato
- accessibili solo a personale autorizzato
  
## Obbligo di informativa al lavoratore
L’azienda deve informare i lavoratori in modo chiaro e comprensibile su:
- quali strumenti usano
- quali dati vengono raccolti
- per quali finalità
- per quanto tempo
- chi può accedere ai dati
- quali controlli possono derivare dagli strumenti
- 
## Internet Policy: perché è obbligatoria
L’Internet Policy è il documento che spiega:
- come si può usare Internet in azienda
- quali comportamenti sono vietati
- quali controlli tecnici vengono effettuati
- come vengono gestiti i log
- quali rischi si vogliono prevenire

Serve a:
- tutelare l’azienda
- tutelare il lavoratore
- rendere trasparente il monitoraggio
- garantire conformità a GDPR e Statuto dei Lavoratori

## Sicurezza delle infrastrutture: perché giustifica il monitoraggio
La sicurezza informatica è una delle finalità più forti che legittimano il monitoraggio.

controlli ammessi:
- firewall che registra traffico sospetto
- sistemi IDS/IPS
- antivirus e antimalware
- sistemi di autenticazione e log di accesso
- monitoraggio delle anomalie di rete

Questi strumenti non servono a controllare il lavoratore, ma a proteggere:
- dati aziendali
- infrastrutture
- clienti
- continuità del servizio

## Open Internet UE
Tutti gli utenti devono poter accedere ai contenuti, servizi e applicazioni online senza blocchi, discriminazioni o rallentamenti ingiustificati

**Neutralità della rete**
Tutto il traffico Internet deve essere trattato allo stesso modo, indipendentemente da chi lo invia, da cosa contiene o da quale servizio utilizzi

La normativa UE permette alcune eccezioni, ma solo se giustificate

**Gestione del traffico per motivi tecnici**
- congestione temporanea della rete
- attacchi DDoS
- guasti o emergenze

**Servizi specializzati**
- telemedicina
- auto connesse
- servizi industriali critici

# Windows Server
windows server offre la possibilità di creare gruppi interni per organizzare utenti dispositivi ecc. e per assegnare autorizzazioni in modo centralizzato

Tipi principali di gruppi:
- Gruppi di sicurezza  
    - Servono per dare o negare permessi (cartelle, stampanti, login, policy).

- Gruppi di distribuzione  
    - Usati per email e comunicazioni, non per autorizzazioni.

Ambito dei gruppi
- Domain Local → permessi su risorse locali del dominio
- Global → gruppi di utenti della stessa organizzazione
- Universal → gruppi che attraversano più domini

**In Windows Server è normale e corretto che un utente appartenga a più gruppi**

## Policy di certificati tramite Group Policy
Le GPO permettono di distribuire automaticamente:

- certificati aziendali
- certificati per Wi‑Fi 802.1X
- certificati per VPN
- certificati per firma digitale
- certificati per server e servizi

è molto importante poiche permette di autenticare utenti e dispositivi abilitare connessioni sicure applicare crittografia firmare emial o documenti

le GPO permentto di assegnare permessi su cartella specifiche configurare firewall distribuire software impostare password policy configurare desktop menu drive mappati e bloccare funzioni su utilizzo usb pannello di controllo command line powershell

## Principio di isolamento
è il principio fondamentale con il quale una macchina virtuale rimane isolata dalle altre macchine per evitare propagazione malware accessi non autorizzati fuga di dati o escalation laterale