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