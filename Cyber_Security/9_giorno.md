# Dispositivi IoT
I dispositivi IoT (Internet of Things) sono oggetti quotidiani o industriali capaci di raccogliere dati tramite sensori, comunicarli a un sistema centrale o al cloud, ricevere comandi ed eseguire azioni automatiche.

Un sistema IoT completo è composto da quattro elementi principali:
- Sensori/dispositivi → raccolgono dati (temperatura, movimento, posizione, ecc.)
- Connessione → Wi‑Fi, Bluetooth, LPWAN, Ethernet, rete cellulare
- Cloud / elaborazione → analisi dei dati e decisioni automatiche
- Interfaccia utente → app o pannello di controllo per monitorare e inviare comandi 

# Sicurezza dei dispositivi IoT
La sicurezza è un tema critico poiche molti dispositivi nascono con protezione minima e possono diventare punti di accesso per attacchi informatici
Le principali aree di sicurezza includono:

- Sicurezza del dispositivo come firmware aggiornato, protezione fisica
- Sicurezza di rete per cifratura, segmentazione, firewall
- Sicurezza dei dati per protezione delle informazioni raccolte
- Sicurezza delle applicazioni per evitare vulnerabilità software

**Catena di fornitura IoT <br>Progettazione->Produzione->Distribuzione->Utilizzo->Supporto->Smaltimento**

**Progettazione del Prodotto**<br>
Definire caratteristiche produzione circuiti elettronici e creazione prototipi per verificare il funzionamento, Sviluppo del firmware e delle funzionalità software valutazione **Rischi per la privacy**
Se la sicurezza non viene considerata fin dall'inizio il dispositivo potrebbe avere delle vulnerabilità difficili da correggere quindi bisogna decidere quanti dati raccogliere e come proteggerli utilizzando la **security-by-design** scelte sbagliate sull'utilizzo e la sicurezza dei dati possono creare rischi legali GDPR

**Produzione**<br>
I semiconduttori sono i cervelli dei dispositivi elettronici prodotti in ambienti speciali chiamati **fonderie** dove si trasformano materiali come il silicio in chip elettronici complessi. Una manomissione durante la fabbricazione può introdurre backdoor hardware impossibili da rilevare successivamente, Errori di produzione possono compromettere sicurezza, affidabilità e durata del dispositivo, Catene di fornitura globali aumentano il rischio di componenti contraffatti o non certificati

**Distribuzione**<br>
Il dispositivo lascia la fabbrica e passa attraverso vari intermediari per questioni di sicurezza bisogna usare sigilli anti-manomissione, firmware firmato digitalmente e avere il tracciamento della catena logistica poiche si è sottoposti a rischio di manipolazione durante il trasporto, installazione di firmware modificato o compromesso, sostituzione di componenti con versione non originale

**Utilizzo**<br>
Il dispositivo arriva all’utente finale o all’azienda ma Un singolo dispositivo vulnerabile può compromettere rete domestica, aziendale o altri dispositivi IoT per questo bisogna controllare le corrette configurazioni password forti porte chiuse ecc. aggiornare i firmware, cifrare le comunicazione e utilizzare la minimizzazione dei dati personali

**Supporto e Manutenzione**<br>
Il produttore deve garantire aggiornamenti e assistenza aggiornamento dei firmware certificati da firma digitale, mantenere un rapporto di assistenza nel tempo. In caso che l'azienda chiuda precocemente il supporto tecnico l'utente dovra cambiare dispositivo per non eccedere in possibili vulnerabilità.

**Smaltimento**<br>
Fase spesso ignorata ma fondamentale poiche un prodotto smaltimento male continua a mantenere all'interno della sua memoria dati personali del vecchio proprietario c'è quindi la possibilità di recuperare credenziali configurazione e log ed in piu ci sono componenti elettronici pericolosi per l'ambiente. Per ovviare a quest eproblematiche è indicato fare un wipe della memoria e un reset di fabbrica certificato ed effettuare lo smaltimento in centri autorizzati.

**Programmazione dei dispositivi**<br>
**<span style="color:blue">Sviluppo Software</span>** scrivendo il codice che farà funzionare il dispositivo dal firmware fino alle applicazioni che l'utente utilizza
**<span style="color:blue">Test di sicurezza</span>** verificando la vulnerabilità controllo dei permessi e si testano i sistemi di protezione implementati
Infine si prepara il sistema per ricevere **<span style="color:blue">aggiornamenti</span>** di sicurezza durante tutta la vita del dispositivo 

**Software di terze parti**
I dispositivi IoT raramente funzionano solo con software sviluppato internamente: spesso integrano librerie, SDK, driver, moduli di comunicazione e servizi cloud creati da fornitori esterni, questi componenti accelerano lo sviluppo, ma introducono rischi significativi nella supply chain come Vulnerabilità ereditate dalle librerie esterne, Dipendenza dal fornitore per aggiornamenti, Possibili problemi legali legati alle licenze, Rischio di supply chain attack, Servizi cloud esterni che possono cambiare o cessare è buiona pratica quindi Usare solo librerie firmate e ufficiali, Mantenere un inventario delle dipendenze (SBOM), Aggiornare regolarmente i componenti, Testare la sicurezza anche delle librerie esterne, Verificare la conformità al GDPR

**La Piattaforma : cuore del sistema**<br>
La piattaforma IoT è dove confluiscono tutti i dati personali raccolti dai dispositivi e deve essere protetta con la massima sicurezza

**Distribuzione e logistica**<br>
I dispositivi devono essere conservati in depositi sicuri con accesso controllato il trasporto è consigliato effettuarlo direttamente al rivenditore o direttamente ai clienti, ogni movimento deve essere registrato per la tracciabilità per garantire la catena di trasporto

**Configurazione iniziale**
Il dispositivo viene connesso alla rete e alla piattaforma del produttore, si crea un account personale con password sicura e si aggiorna il dispositivo all'ultima versione del firmware software

**Supporto e manutenzione**
Il produttore può aggiornare il dispositivo e risolvere problemi a distanza attraverso connessione internet con il supporto remoto per aggiornamento di sicurezza, correzione malfunzionamenti, aggiunta nuove funzionalità, assistenza tecnica, o per problemi piu gravi un tecnico deve intervenire fisicamente sul dispositivo sostituendo componenti riparando hardware ripristinando il sistema o per aggiornamenti manuali tramite il supporto locale

**Furto di proprietà intellettuale**<br>
Informazioni riservate come progetti, codice sorgente e segreti commerciali possono essere rubati per questo bisogna proteggerli con la massima sicurezza poiche chi commette il furto potrebbe scoprire vulnerabilità , contraffarre prodotti, o inserire delle backdoor da mandare poi in produzione per avere delle vulnerabilità da sfruttare

# Sicurezza software
- Requistii di sistema definiti esplicitamente per il software e il suo funzionamento
- Modelli di minaccia identificabili per proteggere da possibili attacchi
- Revisione codice da parte di sviluppatori esterni per trovare errori
- test automatizzati con strumenti di ricerca autonoma per le vulnerabilità
- penetration testing tramite hacker etici per trovare falle non scoperte

# Software Bill of Materials (SBOM)
Un SBOM è come una lista che comprende tutti i componenti usati nel dispositivo del software per identificare rapidamente i dispositivi vulnerabili verificarne l'update controllare licenze e aumentare la trasparenza verso i clienti

# gestione della catena di custodia
La gestione della catena di custodia riguarda il controllo continuo e verificabile di ogni fase attraversata da un dispositivo IoT, dalla sua **origine** fino alla consegna finale. Tutto inizia nel luogo di **origine**, dove il dispositivo o i suoi componenti vengono registrati per la prima volta, creando una traccia iniziale che accompagnerà l’intero ciclo logistico. Durante la **produzione**, ogni passaggio deve essere documentato per garantire che nessun componente venga sostituito, manomesso o alterato. Anche il **trasporto** rappresenta un momento critico: il dispositivo deve viaggiare in **condizioni sicure**, con registrazioni puntuali di ogni spostamento, cambio di vettore o deposito temporaneo, così da mantenere una storia completa e **verificabile** del percorso effettuato. La fase di **consegna** chiude la catena, certificando che il dispositivo è arrivato al destinatario previsto senza alterazioni. Per rendere questa catena affidabile e non falsificabile, si utilizzano tecnologie come **codici QR, tag RFID e sistemi basati su blockchain, che permettono di creare registri immutabili** e consultabili in ogni momento. Grazie a questi strumenti, ogni evento della vita logistica del dispositivo diventa parte di un archivio trasparente, utile per garantire sicurezza, autenticità e tracciabilità dell’intero processo.

# VLAN
Le VLAN permettono di suddividere una rete fisica in più reti logiche separate, migliorando la sicurezza e l’efficienza complessiva dell’infrastruttura. Attraverso la segmentazione, i dispositivi vengono isolati in gruppi distinti, riducendo la superficie di attacco e impedendo che utenti o sistemi non autorizzati possano accedere a risorse sensibili. Questa separazione logica contribuisce anche alla riduzione dei costi, perché evita la necessità di creare reti fisiche dedicate: la stessa infrastruttura può essere riutilizzata per più reparti, servizi o livelli di accesso, semplificando la gestione e diminuendo la quantità di hardware necessario. Un altro vantaggio fondamentale riguarda il traffico di broadcast, che viene confinato all’interno della singola VLAN, evitando che si propaghi in tutta la rete e migliorando così le prestazioni complessive. In questo modo la rete diventa più ordinata, più sicura e più scalabile, adattandosi facilmente alle esigenze di aziende, scuole, enti pubblici e ambienti complessi.
A livello operativo, la configurazione delle VLAN avviene principalmente sugli switch gestiti. Il concetto è semplice: si assegna un numero di VLAN e si decide quali porte dello switch appartengono a quella VLAN. Ogni porta può essere configurata come access (appartiene a una sola VLAN) oppure come trunk (trasporta più VLAN contemporaneamente). Gli switch comunicano tra loro usando il protocollo 802.1Q(lo standard ethernet che gestisce come aggiungere gli id alle vlan per gli vid), che inserisce un “tag” nei pacchetti per indicare a quale VLAN appartengono.
In pratica, si parte creando la VLAN sullo switch, assegnandole un ID numerico. Poi si scelgono le porte che devono farne parte: per esempio, tutte le porte dove colleghi i PC dell’ufficio possono essere messe nella VLAN 10, mentre le porte dove colleghi le telecamere IP possono essere nella VLAN 20. Le porte che collegano gli switch tra loro o che collegano lo switch al router vengono configurate come trunk, così possono trasportare più VLAN contemporaneamente senza confonderle.
Il router o il firewall gestisce l’intercomunicazione tra le VLAN: senza una regola esplicita, le VLAN restano isolate. Questo isolamento è ciò che garantisce sicurezza e controllo del traffico. Se vuoi permettere alla VLAN 10 di accedere a Internet ma non alla VLAN 20, basta configurare le regole di routing e firewall di conseguenza.
In un ambiente reale, la configurazione può essere fatta tramite interfaccia web dello switch oppure tramite riga di comando. Il principio però non cambia: si definiscono le VLAN, si assegnano alle porte, si configurano i trunk e si stabiliscono le regole di comunicazione. Una volta impostate, la rete diventa più ordinata, più sicura e molto più facile da gestire, perché ogni gruppo di dispositivi vive nella sua “bolla” logica pur usando la stessa infrastruttura fisica.

# Proxy
Un proxy è un server intermediario che si posiziona tra il tuo dispositivo e Internet, filtrando, inoltrando o modificando le richieste per migliorare privacy, controllo e sicurezza Un server proxy è un sistema che riceve le richieste dei client (come il browser) e le inoltra ai server di destinazione usando il proprio indirizzo IP, mascherando quello reale dell’utente Questo meccanismo permette di nascondere la posizione geografica, filtrare il traffico e aggiungere un livello di protezione alla rete.
Quando navighi senza proxy, il tuo dispositivo invia richieste direttamente ai server web, mostrando il tuo indirizzo IP.
Con un proxy, invece:

- il tuo dispositivo invia la richiesta al server proxy;
- il proxy inoltra la richiesta al sito web usando il suo IP;
- il sito risponde al proxy;
- il proxy rimanda la risposta al tuo dispositivo.

Questo processo avviene in modo trasparente per l’utente, che continua a navigare normalmente.
ACS spiega che il proxy può anche modificare richieste e risposte per aggiungere funzioni come caching o filtraggio del traffico

I proxy hanno diversi utilizzi, sia personali che aziendali:

- Privacy e anonimato: mascherano l’indirizzo IP reale dell’utente, rendendo più difficile tracciare la sua attività online. Aranzulla sottolinea che i proxy permettono di camuffare la posizione geografica e accedere a contenuti con restrizioni regionali .
- Sicurezza: possono filtrare traffico malevolo, bloccare siti pericolosi e agire come firewall aggiuntivo, come indicato da Fortinet .
- Controllo aziendale: permettono di monitorare e limitare l’accesso ai siti web, gestire la banda e applicare policy centralizzate.
- Caching: memorizzano copie locali di contenuti web per velocizzare la navigazione e ridurre il carico sulla rete.
- Accesso a contenuti bloccati: permettono di aggirare restrizioni geografiche o filtri locali.

<span style="font:bold;color:red">Proxy HTTP/HTTPS: filtrano solo il traffico web del browser <br> Proxy trasparenti: usati per monitoraggio o filtraggio senza modificare l’IP dell’utente <br> Proxy SOCKS: più versatili, funzionano con app diverse dal browser (email, giochi, P2P) <br> Reverse proxy: proteggono i server, non i client, distribuendo carico e filtrando richieste <br>Proxy anonimi o d’élite: nascondono completamente l’IP dell’utente </span>