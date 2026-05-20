# QUESTA DISPENSA IN PARTICOLARE ILLUSTRA I COMANDI PRINCIPALI PER CONTROLLO E SCANSIONE, SONO A TITOLO INFROMATIVO COMERACCOGLITORE DI COMANDI TROVABILI ANCHE ONLINE MA RAGGRUPPATI IN UNA SINGOLA DISPENSA, NON VANNO USATI SENZA AUTORIZZAZIONE E NON VANNO UTILIZZATI IN MANIERA POCO SICURA A MENO DI ESSERE ESPERTI NELL'AMBIENTE DI CYBER SECURITY O ETICAL HACKING PERTANTO NON RISPONDO DELLE CONSEGUENZE DEL LORO USO E COME SCRITTO NEL FILE PRINCIPALE IL README DELLA REPOSITORY TUTTO IL MATERIALE DEVE ESSERE USATO PER DIFESA PROPRIA O AZIENDALE NON PER ESFILTRAZIONE O MODIFICA DI FILE NON DI NOSTRA PROPRIETA' 


1. Prompt dei Comandi Windows (CMD / PowerShell)
Utili per la ricognizione iniziale da una postazione Windows e per il networking di base.

ipconfig /all: Mostra la configurazione completa della rete (IP, Gateway, DNS, MAC).

netstat -ano: Visualizza tutte le connessioni attive e le porte in ascolto con il relativo PID (Process ID).

arp -a: Mostra la tabella ARP (mappatura IP-MAC) per identificare altri dispositivi nella sottorete.

nslookup [dominio]: Interroga i server DNS per risolvere nomi di dominio.

tracert [IP/Host]: Traccia il percorso dei pacchetti verso una destinazione.

systeminfo: Genera un report dettagliato sulla configurazione del sistema e sulle patch installate (fondamentale per trovare vulnerabilità di sistema).

tasklist: Elenca tutti i processi in esecuzione.

net user [nome]: Visualizza o modifica i dettagli degli account utente locali.

2. Prompt Comandi Linux (Generico)
Comandi fondamentali per la gestione del sistema, dei permessi e della rete su qualsiasi distribuzione (Ubuntu, Debian, CentOS).

sudo su: Passa all'utente root (amministratore).

ls -la: Elenca file e cartelle, inclusi i file nascosti, con permessi e proprietari.

chmod +x [file]: Rende un file eseguibile (es. script .sh o .py).

grep -r "testo" /percorso: Cerca ricorsivamente una stringa all'interno dei file.

find / -name [nome_file]: Cerca un file partendo dalla root del sistema.

ip a: La versione moderna di ifconfig; mostra indirizzi IP e stato delle interfacce.

sudo netdiscover -i eth0 -r 192.168.1.0/24

ss -tulnp: Mostra i socket in ascolto (TCP/UDP) e i processi associati.

cat /etc/passwd: Visualizza gli utenti del sistema.

history: Mostra gli ultimi comandi digitati (utile per riprendere sessioni di lavoro).

/var/log/auth.log : Registra i tentativi di login.

/var/log/lastlog : Registra l'ultimo accesso di ogni utente

sudo iftop -i eth0  : Mostra una tabella in tempo reale delle connessioni attive e quanta banda stanno consumando (in Mb/s o Kb/s), con delle barre grafiche orizzontali (eth0, wlan0, any) premere il tasto " p " per visualizzare le porte e il tasto " b " per avere la media dei MB al secondo per verificare quale porta consuma di piu

sudo apt install nload
sudo nload  : andamento globale del server (Dati in entrata vs Dati in uscita) espresso chiaramente in MB/s tramite un grafico ASCII animato che si muovono in tempo reale mostrando il picco attuale, medio e minimo di dati che lasciano il sistema

3. Prompt Comandi Kali Linux (Specifici Pentesting)
Kali include strumenti preinstallati che si richiamano direttamente da terminale.

sudo apt update && sudo apt full-upgrade: Aggiorna il sistema e tutti i tool di hacking.

msfconsole: Avvia il framework Metasploit.

airmon-ng start [interfaccia]: Attiva la modalità monitor sulla scheda Wi-Fi per lo sniffing.

proxychains [comando]: Esegue un comando (es. nmap) attraverso una catena di proxy per anonimizzare il traffico.

searchsploit [servizio_versione]: Cerca nel database offline di Exploit-DB vulnerabilità per un software specifico.

hashcat -m [tipo_hash] [file_hash] [wordlist]: Avvia il cracking delle password via GPU.

john --wordlist=[percorso] [file_hash]: Cracking di password via CPU (John the Ripper).

{
scp : Secure Copy (usa il protocollo SSH per spostare file)
nomemacchina@[IPmacchina]:[posizione/file] : Indica "prendi il file che si trova in questo percorso sulla macchina remota".
~/[posizione/di/salvataggio]: Indica "salvalo qui, sul mio desktop locale"

codice completo con esempio

nomemacchina@[IPmacchina]:[posizione/file] ~/[posizione/di/salvataggio]

scp msfadmin@192.168.56.102:/tmp/db_dump.txt ~/Desktop/bottino.txt

-o HostKeyAlgorithms=+ssh-rsa -o PubkeyAcceptedKeyTypes=+ssh-rsa => per accettare vecchi algoritmi di trasferimento

}

{
sudo tcpdump -i eth1 -A port 23  : Questo comando "ascolta" tutto ciò che passa sulla porta Telnet in formato leggibile

-i eth1: Assicurati che sia la tua interfaccia di rete (quella con l'IP 192.168.56.x).

-A: Fondamentale. Dice a tcpdump di stampare i dati in formato testo leggibile.

port 23: Filtra tutto il rumore e ti mostra solo il traffico Telnet.
}

dirb [IP]:[porta]  :  utilizzando un dizionario crea url tipo http/[ip]:porta/[admin, dashboard ecc] per testare se ci sono url nascosti o proibiti ma esistenti

1. Utilizzo di Nmap e Comandi Annessi
Nmap è lo standard per la scansione delle reti.

Scansioni di base:

nmap -sn [rete/24]: Ping Scan. Identifica quali host sono accesi senza scansionare le porte (scoperta host).

nmap -sS [IP]: SYN Scan (Stealth). È veloce e meno invasivo, non completa la connessione TCP.

nmap -sU [IP]: UDP Scan. Scansiona servizi come DNS o DHCP.

Scansioni di approfondimento:

nmap -sV [IP]: Service Version Detection. Tenta di determinare la versione esatta del software su ogni porta.

nmap -O [IP]: OS Detection. Tenta di identificare il sistema operativo dell'host.

nmap -A [IP]: Scansione "Aggressiva". Abilita OS detection, version detection, script scanning e traceroute.

nmap -p- [IP]: Scansiona tutte le 65.535 porte (di default nmap ne scansiona solo 1000).

nmap -T[0-5] [IP]: Imposta la velocità (0 è paranoico/lentissimo, 5 è velocissimo ma rumoroso).

sudo nmap -sV -sC -A [IP] : -sV: Rileva le versioni esatte dei servizi -sC: Esegue gli script di default di Nmap per trovare vulnerabilità note -A: Abilita il rilevamento del sistema operativo e il traceroute

5. Utilizzo NSE (Nmap Scripting Engine)
NSE permette di automatizzare compiti complessi come la ricerca di vulnerabilità o attacchi brute force.

Comandi principali:

nmap --script default [IP]: Esegue gli script standard di sicurezza.

nmap --script vuln [IP]: Esegue tutti gli script della categoria "vulnerability" per trovare bug noti.

nmap -sV -F -Pn --script vulners [IP] : esegue una scansione veloce delle vulnerabilità note saltanto la fase di ping

nmap --script auth [IP]: Testa le credenziali di default per vari servizi (HTTP, FTP, Telnet).

nmap --script brute [IP]: Tenta attacchi di forza bruta contro i servizi individuati.

Esempi specifici per servizio:

nmap --script http-enum [IP]: Enumera directory comuni su un server web.

nmap --script smb-os-discovery [IP]: Ottiene informazioni dettagliate su un sistema Windows via protocollo SMB.

nmap --script dns-brute --script-args dns-brute.domain=[dominio]: Tenta di scoprire sottodomini tramite brute force DNS.

6. Altri Comandi Utili (Web e OSINT) kali linux o shell linux
whatweb [URL]: 
- Identifica tecnologie, CMS e versioni di un sito web. Si usa durante la fase di ricognizione passiva/attiva. Serve a capire "cosa c'è sotto" un sito (es. se usa WordPress, Apache o librerie JavaScript specifiche)

sqlmap -u "[URL?id=1]" --dbs: 
- Testa automaticamente la presenza di SQL Injection e recupera i database.Si utilizza nella fase di exploitation. È un tool basato su Python che automatizza il test di vulnerabilità nei database

nikto -h [URL]: 
- Scansione di vulnerabilità specifiche per web server (configurazioni errate, file sensibili). Si usa per il vulnerability assessment dei server web. Cerca oltre 6700 file pericolosi e configurazioni errate del server

whois [dominio]: 
- Ottiene informazioni sul proprietario e sui record del dominio.È un comando standard della suite di networking di Linux. Si utilizza per la ricognizione (footprinting) per ottenere dati amministrativi su chi ha registrato un dominio, i server DNS utilizzati e le date di scadenza

# Passaggi chiave 
Reconnaissance: scansione porte aperte (Nmap).

Exploitation: Utilizzo di una backdoor per ingresso diretto tipo (porta 1524).

Data Theft: rubare dati sensibili.

Sniffing: intercettazione traffico.

Covering Tracks: Pulizia dei log.

# wireshark
Wireshark è il packet sniffer (analizzatore di protocolli di rete) più diffuso al mondo. In termini semplici, agisce come un "microscopio" per la rete: permette di catturare il traffico dati che attraversa un'interfaccia e di esaminare ogni singolo pacchetto in dettaglio Wireshark non è uno strumento di attacco diretto, ma un tool di analisi. Funziona intercettando i dati che viaggiano sul cavo o nell'aria e traducendo quei segnali binari (0 e 1) in un formato leggibile dagli esseri umani, suddividendoli per protocolli (come HTTP, TCP, DNS o TLS)

1. Selezione dell'Interfaccia e Cattura
Per iniziare, devi dire a Wireshark quale "orecchio" usare per ascoltare.

Scelta dell'interfaccia: Selezioni la scheda di rete attiva (es. Ethernet o Wi-Fi).  

Modalità Promiscua: Teoricamente, una scheda di rete ignora il traffico non destinato a lei. Attivando la "Promiscuous Mode", la scheda cattura tutto il traffico che passa nel suo dominio di collisione, indipendentemente dalla destinazione.  

2. Filtraggio (Capture vs Display Filters)
Dato che una rete genera migliaia di pacchetti al secondo, il rumore visivo è enorme.

Capture Filters: Impostati prima di iniziare, dicono a Wireshark di salvare solo determinati dati (es. "solo traffico dall'IP X").  

Display Filters: Impostati dopo la cattura, nascondono temporaneamente i pacchetti che non interessano senza eliminarli (es. scrivi http nella barra per vedere solo il traffico web).  

3. Analisi della struttura del pacchetto
Wireshark divide ogni pacchetto catturato in tre pannelli gerarchici:  

Packet List: Una tabella cronologica di tutti i pacchetti (chi parla con chi, che protocollo usa).  

Packet Details: Espande il pacchetto selezionato seguendo il modello OSI. Puoi vedere l'intestazione Ethernet (Layer 2), l'intestazione IP (Layer 3), il segmento TCP/UDP (Layer 4) e infine i dati applicativi (Layer 7).  

Packet Bytes: Mostra i dati grezzi in formato esadecimale.  

4. Ricostruzione del Flusso (Follow Stream)
Una delle funzioni teoriche più potenti è il "Follow TCP/UDP Stream". Poiché i dati (come un'immagine o una pagina HTML) vengono spezzettati in centinaia di pacchetti, questa funzione permette di riassemblarli per leggere la conversazione completa tra client e server come se fosse un unico testo continuo

Casi d'uso principali
Risoluzione dei problemi: Capire perché una connessione cade o perché un'applicazione è lenta.  

Analisi di sicurezza: Individuare traffico sospetto, malware che comunica con server esterni (C2) o tentativi di scansione sulla rete.  

Apprendimento: Studiare come funzionano realmente i protocolli di rete vedendo i dati "vivi"

**per lanciare correttamente wireshark bisogna avviarlo con "sudo wireshark" per accedere con permessi admin direttamente all'hardware della scheda di rete**

Passare dalla teoria alla pratica con Wireshark significa trasformare il terminale di Kali o la tua postazione di lavoro in una centrale di monitoraggio. Ecco i passaggi operativi esatti per eseguire una sessione di analisi.
1. Preparazione dell'Ambiente e LancioSu sistemi basati su Linux come Kali, Wireshark richiede permessi speciali per interagire direttamente con l'hardware della scheda di rete.
- Lancio da Terminale: 
- Apri la shell e digita sudo wireshark.  
- Selezione dell'Interfaccia: Nella schermata iniziale vedrai una lista di interfacce (es. eth0 per il cavo, wlan0 per il Wi-Fi). Se vedi una linea che "pulsa" accanto al nome, significa che c'è traffico attivo su quella porta.
-   Abilitazione Modalità Promiscua: Prima di cliccare sulla pinna blu (Start), assicurati nelle opzioni di cattura che la "Promiscuous Mode" sia attiva per intercettare anche i pacchetti non indirizzati specificamente a te.  
2. Cattura e Filtraggio in Tempo Reale
Una volta avviata la cattura, verrai sommerso da migliaia di righe colorate. La pratica corretta prevede l'uso dei filtri per non impazzire.
- Filtri di Visualizzazione (Display Filters): Digita il filtro nella barra in alto (diventa verde se la sintassi è corretta).  
  - http: mostra solo il traffico web non criptato.  
  - ip.addr == 192.168.1.10: isola solo le conversazioni che coinvolgono quel determinato IP.  
  - tcp.port == 443: visualizza solo il traffico HTTPS (criptato).  
- Colorazione: Wireshark colora i pacchetti automaticamente (es. nero per pacchetti con errori TCP, azzurro per UDP) per aiutarti a individuare anomalie a colpo d'occhio.  
3. Analisi Profonda del Pacchetto (I 3 Pannelli)
Quando trovi un pacchetto interessante, cliccaci sopra per analizzarlo nel dettaglio pratico usando il modello OSI come bussola.
- Pannello Superiore (Elenco): Identifica il flusso temporale. Cerca sequenze ripetute o messaggi di errore.  
- Pannello Centrale (Dettagli Protocollo): Qui espandi le sezioni:
  - Ethernet II: Vedi gli indirizzi MAC di origine e destinazione.  
  - Internet Protocol (IP): Controlla se gli indirizzi IP sono quelli previsti o se ci sono tentativi di spoofing.  
  - Transmission Control Protocol (TCP): Analizza i numeri di sequenza per capire se mancano dei pezzi alla comunicazione.  

Pannello Inferiore (Esadecimale): Utile per vedere stringhe di testo in chiaro all'interno di pacchetti non criptati (es. password inviate via Telnet o HTTP semplice).  

4. Ricostruire una Conversazione (Pratica Avanzata)Vedere i singoli pacchetti è come leggere lettere singole; ricostruire il flusso è come leggere l'intero libro.Follow Stream: Fai tasto destro su un pacchetto e seleziona 
- Follow -> TCP Stream.  
- Cosa succede: Wireshark aprirà una nuova finestra mostrando l'intera conversazione tra client e server, colorando in rosso ciò che ha inviato il client e in blu la risposta del server. Se il traffico non è criptato, qui potrai leggere intere email, pagine HTML o messaggi di chat.  
  
5. Esportazione e ReportisticaAl termine della sessione pratica, i dati devono essere salvati per analisi forense o confronto futuro.
- Salvataggio: I file vengono salvati in formato .pcapng o .pcap, lo standard universale leggibile anche da altri tool come tcpdump o tshark.  
- Esportazione Oggetti: Se hai catturato traffico HTTP, puoi andare su File -> Export Objects -> HTTP per "estrarre" dal traffico di rete i file reali (immagini, PDF, script) che l'utente ha scaricato durante la sessione