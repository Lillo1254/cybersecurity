# porta 25 protocollo smtp
scansiniamo la macchina vulnerabile con il comando

- nmap -Pn -PR 192.168.56.0/24
    - -Pn per dire ad nmap di non fare il ping
    - -PR per inviare solo pacchetti ARP
    - 192.168.56.0/24 per scansionare le vulnerabilità delle porte note di default 1000 porte su tutta la subnet

Ora che abbiamo nuovamente lo scanning delle porte possiamo procedere con analizzare una singola porta nello specifico...la porta 25

- nmap -p 25 -sV 192.168.56.102
  - -p 25 indica la porta che vogliamo scansionare nello specifico
  - -sV ci serve per inviare dei pacchetti "probs" alla porta 25 per analizzare il testo di risposta e capire quale software viene utilizzato e la verisone corretta
  - 192.168.56.102 ip della macchina vulnerabile sulla quale vogliamo scnasionare la porta

avremo un risultato come questo:

Nmap scan report for 192.168.56.102 (192.168.56.102)
Host is up (0.00053s latency).

PORT   STATE SERVICE VERSION
25/tcp open  smtp    Postfix smtpd
MAC Address: 08:00:27:FA:55:6B (Oracle VirtualBox virtual NIC)
Service Info: Host:  metasploitable.localdomain

in questo banner di risposta possiamo identificare molte informazioni in piu rispetto ad una normale scansione che abbiamo ottenuto grazie all'opzione -sV tr acui ovviamente lo stato della porta "attivo" il servizio "smtp" la verisone "postfix smtpd" il mac address "08:00..." e l'host "metaesploitable" ora procediamo prima di cercare exploit diretti continuando a verificare se possiamo instaurare una connessione con "netcat" con il comando 

- nc 192.168.56.102 25    
  - nc avvia netcat
  - 192.168.56.102 ip macchina vulnerabile
  - 25 la porta aperta

ci verra restituito un banner di benvenuti simile a questo

- 220 metasploitable.localdomain ESMTP Postfix (Ubuntu)
    - 220 indica che siamo su un servizio attivo e pronto all'uso precisamente che ha stabilito una connessione TCP con successo

il terminale di smtp non ha un interfaccia grafica quindi anche se siamo all'interno non vedremo scritte automatiche del terminale per poter sfruttare questo software interno dobbiamo usare il linguaggio nativo di smtp il cui comando principale che andremo ad utilizzare sarà quello per l'enumerazione degli utenti ovvero il test per verificare se un utente esiste o meno

- VRFY [nome_utente]

VRFY root
252 2.0.0 root
VRFY user
252 2.0.0 user
VRFY ciao
550 5.1.1 <ciao>: Recipient address rejected: User unknown in local recipient table

come possiamo notare abbiamo due tipologie di risposta diversa una con codice 252 ed un acon codice 550

- 252 indica che la richiesta per verifica è stata accettata ma non puo essere completata poiche manca qualcosa
- 550 indica invece che la richiesta non è stata accettata

questa è la stessa situazione in cui si puo ottenere un enumerazione degli utenti basandosi sui tempi di risposta del server web o sull'uso delle credenziali in cui viene specificato se ad essere sbagliati sono "la password" o l' "email" pertanto ora sappiamo che a tutti gli effetti gli utenti root e user sono utenti esistenti poiche ha riscontrato un match nelle richieste anche se non completato e viceversa non ha riscontrato un match su utente "ciao" poiche non presente. per fare questo processo a mano ci vorebbero giorni ma nel nostro laboratorio possiamo utilizzare uno script nativo di kali linux per l'enumerazione degli utenti smtp usciamo quindi dal terminale smtp con "quit" e utilizziamo di fatto il nostro framework d'attacco Metasploit

- msfconsole -q 
  - -q quest'opzione serve per non mostrare i banner di benvenuto 

 questa volta non dobbiamo fare la ricerca di un exploit pubblico ma dobbiamo utilizzare semplice un metodo di enumerazione già creato in precedenza ed integrato in kali linux quindi utilizziamo il comando per la ricerca del modulo

 - search smtp_enum
   - è un modulo gia creato in precedenza utilizzato per l'enumerazione degli utenti via smtp

ora abbiamo trovato il modulo gia pronto all'utilizzo quello che dobbiamo fare è appunto utilizzarlo (use)

- use auxiliary/scanner/smtp/smtp_enum

ora controlliamo i parametri richiesti con il comando

- show options

settiamo i parametri come RHOSTS THREADS

- set RHOSTS [ip_macchina_vulnerabile]
- set THREADS il numero di threads che volete utilizzare

un altro setting importante ma non necessario che possiamo sfruttare è il VERBOSE poiche il comando lavora in background non vedremo risultati fino alla fine della scansione completa per vedere invece l'interazione dello script possiamo utilizzare

- set VERBOSE true
  - questo setting mostrerà sul terminale l'esecuzione degli user controllati

successivamente possiamo avviare l'attacco con

- run

aspettando l'esecuzione completa del modulo avremo al suo termine un risultato come questo 

[+] 192.168.56.102:25     - 192.168.56.102:25 Users found: , backup, bin, daemon, distccd, ftp, games, gnats, irc, libuuid, list, lp, mail, man, mysql, news, nobody, postfix, postgres, postmaster, proxy, service, sshd, sync, sys, syslog, user, uucp, www-data
[*] 192.168.56.102:25     - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

la parte "user found" indica tutti gli utenti che ha effettivamente trovato e possiamo estrapolare da questo diverse informaizoni come la presenza di utenti generici la presenza di database e di un utente per il web ma cosa piu importante a livello pratico ora abbiamo una lista di utenti quindi non ci serve piu di fare un enumerazione degli utenti sui diversi servizi o perte poiche abbiamo già una lista completa d aporter utilizzare per forzare i login su una porta d'accesso come la porta 21 o la porta 22 facendo una ricerca con searchsploit in msfconsole non ci sono esploit disponibili per questa versione se ci fossero stati avremmo potuto utilizzarli per inviare email di phishing o cercare shell di accesso su punti vulnerabili quindi ad ora ci spostiamo su un altra porta per utilizzare i dati che ci sono stati forniti dall'enumerazione stessa