## INFORMAZIONE + AUTOMATICA ==> INFORMATICA
tutta l'informatica si basa su elettrica e codice binario dove gli 0 e gli 1 corrispondono ad interruttori chiusi (0) o aperti (1) 
## primi PC
I primi PC erano pc standalone sostanzialmente non aveva collegamente al suo esterno tramite nessuna rete
## reti 
- Rete wired ===> una rete compèosta da cavi fisici
- Rete wireless ====> una rete ad onde radio a bassa potenza
- Rete satellitare ===> una rete composta da satelliti a medio bassa potenza 

# glboal area network
## wide area network
### metropolitan area network
#### local area network

# PROTOCOLLI
negli anni dopo la creazione di diversi personal computer in diverse zone del mondo e di diverse reti che permettevano l'interconnessione tra dispositivi, per trasmettere dati comprensibili tra un PC ed un altro si è creata la necessita di dover sviluppare delle regole di comunicazione tra interlocutori chiamati PROTOCOLLI 

# TCP/IP
Il tcp/ip è l'insieme dei diversi protocolli utilizzati per la comunicazione tra macchine ed è diviso in 4 livelli differenti:
1) Network Access :
    -gestisce come viaggiano i dati
    -include ethernet, wifi, fibra, 4g/5g
    -cavi, onde radio, segnali, MAC address(indirizzo fisico)
2) Livello internet (IP)
    - indirizzi IP (indirizzo logico)
    - Instradamento (routing)
    - Serach and Find destinary
    protocolli IP(IPv4, IPv6), ICMP (ping), ARP(risolve IP-> MAC address)
3) Livello trasporto
    - TCP (transmission control protocol)
        - affidabilita
        - check error
        - ordine di arrivo dei dati
        - usato per web, email, file transfer
    - UDP (user datagram protocol)
        - velocità
        - non garantisce oridine dati
        - usato per streaming, giochi online, VoIP
4) Livello Applicazione
    - HTTP/HTPPS (utilizzato per siti web)
    - FTP/SFTP (per trasferimento file)
    - SMTP/IMAP/POP3 (ricezione ed invio email)
    - DNS (traduce nomi Domains in IP)
    - DHCP (assegna automaticamente un IP)
* quando si fa una richiesta tipo apertura sito web 
- Livello applicativo crea la richiesta
- Livello trasporto divide i pacchetti
- Livello internet decide il routing e l'instradamento
- Livello network invia i bit sulle rete
destinatario:
- Livello network riceve i bit sulle rete
- Livello internet decide il routing e l'instradamento
- Livello trasporto compatta i pacchetti
- Livello applicativo risolve la richiesta
### queste funzionalita sono standard a livello mondiale

esistono diverse topologie di rete:
1) Rete a bus ==> hanno un cavo principale che è chiamato dorsale la cui interruzione corrompe tutta la rete
2) Rete a stella ==> hanno uno switch che permette piu connessioni su uno stesso HUB danno possibilità di
                     di installare più switch collegati al principale la vulnerabilità risiede nel fatto che
                     tutta la rete è centralizzata su un unico hub salta quello salta tutto
3) Rete a MESH ==> una tipologia di rete che collega ogni nodo di rete ad un gruppi di altri nodi rendendo ogni PC
                   indipendente cosi da avere piu percorsi in caso di mancata connessione verso un nodo specifico

# TIPI DI COMUNICAZIONE
TRASMISSIONE + RICEZIONE = COMUNICAZIONE
## SIMPLEX 
un apparecchio può svolgere unasolo azione o è un apparecchio che trasmette o uno che riceve
## half duplex 
può svolgere entrambe le azioni ma una per volta in maniera sincrona o ricevi o trasmetti
## full duplex
può svolgere entrambe le azioni in maniera asincrona 
## BROADCAST
la trsmissione avviene a preiscindere se c'è un ricevente o meno 

INTERNET LAVORA SU UNA RETE FULL MESH utilizzando un sistema broadcast full duplex  acommutazione di pacchetto

# MODELLO ISO-OSI
il modello iso-osi regola le comunicazioni TCP/IP
per vedere se un server è funzionante si utilizza il comando "ping -a dns/ip" o "ping -t dns/ip" ma potrebbe anche essere bloccata la richiesta di risposta lato server

# server port
ci sono in totale 65535 porte virtuali lato server di cui dalla numero 1 alla 1024 sono chiamate know ports poiche il loro uso è conosciuto per la loro finalita
1) Porta 20 – FTP Data
Usata per il trasferimento dei file nella modalità attiva del protocollo FTP.
2) Porta 21 – FTP Control
Gestisce la connessione di controllo FTP: login, comandi, navigazione directory.
3) Porta 22 – SSH
Permette connessioni sicure e cifrate verso server remoti (terminali, SFTP, tunneling).
4) Porta 53 – DNS
Serve per le richieste DNS: traduce nomi di dominio → indirizzi IP.
5) Porta 80 – HTTP
È la porta standard del web non cifrato (siti http).
6) Porta 443 – HTTPS → web cifrato
7) Porta 25 – SMTP → invio email
8) Porta 110 – POP3 → ricezione email
9) Porta 143 – IMAP → gestione email su server
10) Porta 23 – Telnet → accesso remoto non cifrato (obsoleto)
con il codice "tracert "dns" possiamo vedere ti passaggi dei dati in trasferimento tra un server e un altro cosi da evidenziare dove ci sia un eventuale perdita di dati

# NAT => network address translation
Il NAT è un meccanismo del router che traduce gli indirizzi IP trovati sulla sua rete in un unico indirizzo IP pubblico usato in internet di conseguenza ogni apparecchio connesso a quella rete avra lo stesso IP facendo questo da esterno si puo vedere solo il router principale mentre le connessioni interne restano anonime mentre il router assegna ad ogni ip privato una porta di connessione che poi riassocia al suo ip pubblico
