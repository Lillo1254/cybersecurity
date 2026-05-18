**Le informazioni, i comandi, gli script e gli scenari descritti in questo documento sono rilasciati esclusivamente a scopo didattico, di studio, di ricerca accademica e per il test autorizzato della sicurezza dei sistemi (Ethical Hacking / Penetration Testing). Questo materiale ha l'unico obiettivo di far comprendere i meccanismi di difesa e vulnerabilità dei sistemi informatici.**

# situazione ipotetica
Sei stato assunto come consulente di sicurezza (Ethical Hacker) da una piccola azienda. Il manager è preoccupato perché ha notato strani rallentamenti nella rete interna. Ti viene chiesto di collegarti alla LAN aziendale, identificare i dispositivi connessi, trovare porte aperte potenzialmente pericolose sul server principale (es. 192.168.1.1) e verificare se ci sono vulnerabilità note (CVE) che un malintenzionato potrebbe sfruttare.

**Identificare la rete e i dispositivi connessi (Host Discovery)**

Bisogna capire cosa c'è nella rete a cui si è collegati

- sudo nmap -sn 192.168.1.0/24
  - questo comando esegue un ping scan (host discovery tramite pacchetti ICMP) senza scansionamento delle porte (-sn è l'opzione per non scansionare le porte) ma solo verificando quali IP rispondono. /24 indica l'intera sottorete(subnet) poiche effettua un range da 0 a 24 bit quindi scansionera da 192.168.1.0 fino a 192.168.1.255
  - in questa maniera si otterra una lista di tutti i dispositivi accesie connessi alla rete in quel momento co i relativi indiriziz IP, MAC address con nome produttore schedaa di rete

**Scansione delle porte dell'IP bersaglio**

Trovato l'IP di nostro interesse l'obiettivo è quello di capire quale porte e quali servizi sono attive

- sudo nmap -sV -sC -O -v 192.168.1.1
  - -sV tenta di determinare l'esatta versione del software che gira su ogni porta
  - -sC Esegue gli script predefiniti di NSE (quelli considerati sicuri e non distruttivi) per raccogliere più info
  - -O Tenta di indovinare il Sistema Operativo del bersaglio (OS Detection)
  - -v Mostra i risultati in tempo reale mentre Nmap lavora
  - con la sequenza di questi comandi si ottiene una tbaella dettagliata dei risultati precedenti e presumibilmente quale sistema operativo è attivo su ogni porta se ce ne so

**Scansione delle Vulnerabilità delle porte (Uso dei primi script NSE)**

Abbiamo trovato i punti di nostri interesse ora dobbiamo effettuare una scansione delle vulnerabilità per capire quali servizi hanno errate configurazioni o falle evidenti

- sudo nmap --script vuln 192.168.1.1
  - questo comando utilizza lo script (--script) chiamato vuln NSE ha migliaia di script divisi in categorie; questa categoria controlla se il bersaglio è affetto dalle vulnerabilità più note e diffuse (come password di default, configurazioni errate, o software vecchi)
  - eseguendo questo comando si ottiene un report che si aggiunge alla classica lista delle porte mostrando per l'apputno vulnerabilità note come per esempio la porta 445 potrebbe aver attivo il protocollo SMB v1.0 che crea un grave rischio di sicurezza o che il servizio FTP permette l'accesso ftp-anon quindi senza bisogno di password quindi chiunque potrebbe leggere i file sul server senza bisogno di log

**Scansione approfondita per vulnerabilità note (CVE)**
Abbiamo bisogno di estrarre un report profesionale andando a scnasionare sul sicuro le vulnerabilità e dobbiamo usare degli script NSE di terze parti integrati in kali linux come vulscan o nmap-vulners che collegano le versioni dei servizi direttamente ai database dei CVE

- sudo nma -sV --script vulners 192.168.1.1
  - con questo comando colleghiamo la scoperta delle versioni dei software ( -sv) con le vulnerabilita interrogate nel database ( vulners) tramite lo --script
  - otteniamo un elenco dettagliato di codici CVE associati ad un punteggio di gravità CVSS da 1 a 10 e mostra esattamente quali exploit pubblici esistono per quella vulnerabilità

**Report Finale**
con questa sequenza di comandi abbiamo mappato lo scenario della rete e della subnet abbiamo interrogato il punto di rete che a noi interessa scoprendo vulnerabilità note che potrebbero fornire metodi a malintenzionati di accesso senza autorizzazione o l'invio di payload tramite porta di comunicazione per corrompere la rete aziendale. strutturiamo il report per renderlo il piu chiaro possibile e facilemtne interpretabile fornendo le fasi esplicitate di ciò che abbiamo fatto fatto e dei risultati trovati con la gravità e la priority necessaria fornendo anche linee guida o codici possibili da utilizzare per la remediation in modo da poter fornire un report completo con soluzione ai problemi della rete aziendale.



# situazione ipotetica 2 (stesso scenario ma..)
il ping non risponde poiche i firewall blocca i pacchetti ICMP per questione di sicurezza per evitare che un malintenzionato sdcansioni facilmente la rete quindi bisogna utilizzare una scansione "stealth e TCP SYN"

- sudo nmap -sn -PR 192.168.1.0/24
  - l'opzione -PR utilizza solo richiesta paccehtti ARP i dispositivi connessi alla rete devono rispondere alla richeista ARP per poter comunicare ed un firewall standard non può interrompere questa connessione a meno che non venga interrotta la connettività di rete stessa
- sudo nmap -sn -PS22,80,443 192.168.1.0/24
  - l'opzione -PS invia un paccehtto TCP SYN a porte specifiche dell'indirizzo IP associato, ciclando gli ip e provando questo invio a tutti gli IP da 1 a 255 il firewall o il sistema di protezione restituira un SYN-ACK o un RST questa risposta basta per far interpretare ad Nmap che quell'IP è attivo e vivo 

**La Scansione Stealth (TCP SYN Scan)**

Una volta indentificato l'IP che risulta attivo nonostante il blocco del ping procediamo con la scansione stealth usando SYN Scan (half-open scan)

- sudo nmap -sS -Pn -p- -T4 192.168.1.50
  - -sS attiva il TCP SYN Scan inviando un pacchetto SYN se riceve un SYN-ACK la porta è aperta e nmpa risponde con un pacchetto RST senza completare la connessione con un ACK questo comportamento non stabilendo mia una connessione completa è molto piu difficile da registrare nei log applicativi i moderni firewall o IDS invece vedono comunque il tentativo di connessione
  - -Pn è fondamentale poiche dice ad Nmap di saltare completamente il controllo iniziale del ping trattando l'host come s efosse completamente acceso
  - -p- scansiona tutte le 65535 porte possibili
  - -T4 è la velocità di scansione variabile da T1 a T5 dove 1 è il minimo e 5 è il massimo della velocità

Ad ora.. abbiamo effettuato lo scan delle porte della rete aziendale ma poiche ci bloccava i ping abbiamo utilizzato il metodo stealth SYN-ACK  scoprendo invece che nonostante i blocchi c'è una porta insolita aperta es. 8180 che ospita un vecchio pannello di controllo e la porta 3306 (mysql) che pero accetta connesisone solo dall'interno

Bisogna capire esattamente cosa gira nella porta 8180

- sudo nmap -sV --script http-enum,http-vuln-cve2014-6271 -p 8180 192.168.1.50
  - -sV per determinare la versiona esatta del software
  - --script http-enum fa un ispezione delle directory nascoste del server web (http://sito.it/variabile) 
  - http-vuln-cve2014-6271 questa parte del codice controlla effettivamente la presenza di una vulnerabilita nota chiamata Shellshock con codice CVE2014-6271 che permette l'accesso ad un terminale remoto con privilegi limitati sul server
  - -p 8180 192.168.1.50 scansione la porta ( -p ) numero di porta (8180) sull'IP (192.168.1.50)

**Esplorazione interna (Post-Exploitation & Pivoting)**

avendo sfruttato la vulnerabilità nota siamo all'interno di un terminale con permessi ridotti dobbiamo diventare "root" per avere accesso da amministratore  effettuando una "Privilege escalation" per esplorare il database e verificare la sicurezza al fine di evitare questa possibilità al di fuori dell'azienda

- dal terminale intenro interno della macchina attaccata eseguiamo il comando 
  - ss -tulpn | grep 3306
    - ss comando socket statistics
    - -tulpn racchiude 5 comandi diversi
      - -t mostra i socket che usano il protocollo TCP
      - -u mostra i socket che utilizzano il protocollo UDP
      - -l Filtra i risultati mostrando solo le porte che sono attivamente "in ascolto" di connessioni in entrata
      - -p  Mostra il nome del processo e il relativo PID (Process ID) che possiede quel determinato socket
      - -n Impedisce la risoluzione dei nomi dei servizi e degli indirizzi IP, mostrando direttamente i numeri (es. mostra 22 invece di ssh). Questo rende il comando molto più veloce
- | la pipeline serve ad avviare i comandi contemporaneamente riportando i risultati del primo comandi all'inetnro del secondo comando in tempo reale quindi grep prenderà solo le porte con 3306
- grep 3306 utilizziamo questo comando per prendere solo la parte che ci interessa quindi i servizi che utilizzano quella specifica porta 3306
- scopriamo dove si trova il database Mysql che per esempio si trova su IP 127.0.0.1 dall'esterno non sarebbe potuto essere interrogabile ma dall'interno si ovviamente con relativi privilegi di amministratore

**Identificazione della vulnerabilità di Privilegio (CVE Locale)**

Bisogna controllare la versione del Kernel della macchina attaccata per verificare se ci sono vulnerabilità note come la "Dirty Cow"

- uname -a per scoprire la versione del Kernel 
  - se presente la vulnerabilità Dirty Cow possiamo utilizzarla per diventare root amministratore supremo effettuando di fatto la privilege escalation

**Report finale**
L'obiettivo era bypassare le difese dei blocchi ICMP usando poaccehtti ARP (-PR) o TCP SYN(-Pn -PS) per effettuare una mappatura stealth con SYN Scan(-sS) per non rendere piu difficile la creaizone di log di comunicazione una volta effettuata questa scansione abbiamo puntato ad un servizio specifico indentificando una CVE remota e tramite questa CVE ci siamo mossi lateralmente entrando nella Shell superando il perimetro aziendale e successivamente scansionato il Kernel effettuato un privilege escaltion per avere controllo completo della macchina 

# situazione ipotetica 3
entriamo in azienda ed il monitoraggio d'ufficio segnala delle anomalie un server interno sta subendo un trasferimento di dati verso l'esterno in grande quantità quindi ci colleghiamo ala rete

**primo comando per identificare il nostro indirizzo IP**
- ip a 
  - controlliamo la nostra scheda di rete eth' o wlan0 cosi da poter leggere IP e sottorete 

successivamente abbimao necessita di capire quale sia il router principale e per saperlo dobbiamo controllar ela tabella di routing
- ip route show 
  - ci fornire un risultato simile a "default [IP] dev eth0 dove l'IP sarà proprio l'indirizzo del router principale dove passa ogni pacchetto verso internet

purtroppo la rete è complessa poiche ci sono altri switch e router in diversi uffici prima di arrivare all'esterno quindi per controllare quale sia il gateway principale dobbiamo vedere quanti "salti" fanno i pacchetti per raggiungere l'esterno e per fare questo manderemo dei pacchetti verso un indirizzo IP esterno come per esempio google che ha IP 8.8.8.8 con il comando 
- traceroute 8.8.8.8
  - questo comando restituisce un IP per ogni router intermedio che attraversa prima di arrivare all'esterno della nsotra rete cosi da capire quali sono gli IP intermedi che vengono attraversati

abbiamo trovato il router principale e ora dobbiamo effettuare una scansione di massa per trovare i server e tutti i dispositivi connessi accesi e capirne le funzioni per capire se sono pc dei dipendenti stampanti o server per fare questo utilizziamo il comando 
- sudo nmap -sn -F --traceroute [IP]
  - -sn controlla se un ip risponde
  - -F fa un controllo veloce sulle 100 porte note piu utilizzate per dare un indizio su quale dispositivo sia connesso
  - --traceroute traccia la mappa geografica/logica dei collegamenti tra il nostro kali linux e i dispositivi trovati
- otteniamo quindi una lista di IP dove possiamo trovare il router principale i pc connessi e i server riconoscibili da nomi host MAC address e utilizzo di porte specifiche

**Ispezione Rapida delle Porte Aperte (Investigazione)**

abbiamo capito che il server ha un IP es. 10.0.0.50 dobbiamo capire subito quali porte sono attive in questo momento e stanno scambiando traffico se abbiamo possibilità di accedere direttamente al terminale del server inserendo nome utente e ip del server creando una connessione SSH
- ssh nome_utente@10.0.0.50
- se la porta ssh non è la porta di default (22) bisogna specificarlo con l'opzione -p quindi il comando sara **ssh nome_utente@10.0.0.50 -p [numero porta]**


ora possiamo utilizzare il terminale del server dopo aver effettuato ovviamente l'accesso per farlo utilizziamo il comando
- sudo ss -tupn
  - questo comando ci mostrera tutte le connessioni TCP/UDP attive i relativi processi e gli IP remoti connessi
  - ovviamente in uno scenario di esfiltrazione dati avremo una riga anomala tipo **ESTAB  0  45210  10.0.0.50:4444  ->  198.51.100.7:53211 (proc: nc)**
    - ESTAB indica lo stato della connessione "Established"
    - 0 indica che non ci sono dati bloccati in attesa di essere lavorati e che pertanto il traffico scorre normalmente
    - 45210 indica i bytes trasferiti oppure l'ID interno di connessione
    - 10.0.0.50:4444 è l'ip sorgente e il numero di porta utilizzata per l'esfiltrazione
    - -> indica la connessio il verso del trasferimento dei dati
    - 198.51.100.7:53211 è il punto di destinazione remoto e la porta utilizzata
    - (proc: nc) processo netcat ovvero uno strumento di rete per creare una connessione da parte dell'hacker per inviare dati al suo server

ora abbiamo la certezza che un IP remoto che non fa parte della rete aziendale viene usato come punto di arrivo per estrapolare dati dal nostro server

se invece non fosse possibile utilizzare il server direttamente tramite terminale dobbiamo ispezionare le connessioni dall'esterno cercando con Nmap servizi insoliti per fare questo utilizziamo il comando 
- sudo nmap -sV -p- --open 10.0.0.50
  - -sV identifica il servizio
  - -p- scansiona tutte le 65535 porte
  - --open mostra solo le porte aperte
questo comando identifichera una prota sospetta ovviamente come in precedenza la 4444 ma adesso abbiamo isolato il problema e dobbiamo attuare il blocco per impedire un ulteriore esfiltrazione di dati

**abbiamo due opzioni per esempio dettate dalla policy di sicurezza**

opzione 1:
- bloccare immediamente le connessione esterne su quella porta senza spegnere brutalmente il server ( per analizzare la memoria volatile del processo in un secondo momento)
  - sudo iptables -A INPUT -p tcp --dport 4444 -j DROP
    - questo comando scarta qualsiasi pacchetto in entrata o in uscita dalla prota 4444 direttamente dal kernel interrompendo la comunicaizone immediamente

opzione 2:
- bloccare direttamente il software che tiene aperta la porta per eradicare la minaccia
  - identifichiamo precisamente il PID (process ID) con il comando
    - sudo lsof -t -i :4444 che ci restituisce un PID
  - chiudiamo il processo in corso 
    - sudo kill -9 [PID]
      - il -9 è un segnale inviato al sistema operativo che dice al software di interrompere istantaneamente il processo segnato
        - normalmente il comando sudo kill [PID] invia un segnale al sistema operativo con la richiesta di chiusura del processo ma i malware e trojan ignorano questa richeista
    - cosi facendo il processo viene terminato e la porta passa dallo stato di open a closed automaticamente e l'attaccante ha perso il controllo del server

poiche l'attacante potrebbe intervenire nuovamente su altre porte dello stesso IP su cui ha trovato una vulnerabilita dobbiamo intervenire sul router principale configurando una nuova regola che impedisce (DENY) IP sorgente(ANY qualsiasi) porta sorgente (ANY) IP destinazione (10.0.0.50) e anche una regola a livello globale sul router o firewall per bloccare l'ip dell'attacnte inserendolo in una blacklsit