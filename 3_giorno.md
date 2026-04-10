
# FILE SYSTEM
Struttura gerarchica ad albero
Il file system organizza file e directory in una struttura gerarchica simile a un albero rovesciato.

Concetti fondamentali
- Root: la directory principale (/ su Linux, C:\ su Windows).
- Directory: contenitori che possono includere file o altre directory.

Percorsi:
- Assoluti: partono dalla root (/home/alessandro/...)
- Relativi: partono dalla directory corrente (../documenti)

Tipi di file system
- FAT32 / exFAT: semplice, compatibile, ma con limiti.
- NTFS: journaling, permessi avanzati, cifratura (EFS).
- EXT4 / XFS / Btrfs: tipici di Linux, supportano journaling e snapshot.
- APFS: usato da macOS, ottimizzato per SSD.

Permessi e sicurezza
- Modello owner / group / others (Linux).
- ACL avanzate (Windows NTFS).
- Attributi speciali: SUID, SGID, sticky bit.
- Cifratura dei file o dell’intero disco (BitLocker, LUKS).

Rischi di sicurezza
- Escalation di privilegi tramite permessi errati.
- Accesso non autorizzato a file sensibili.
- File system non cifrati → rischio in caso di furto del dispositivo.

# AUTENTICAZIONE
1) Autenticazione locale
- L’autenticazione avviene direttamente sul dispositivo o sulla macchina locale, senza coinvolgere server esterni.
- Caratteristiche principali
- Le credenziali sono verificate confrontandole con un database locale (es. /etc/shadow su Linux, SAM su Windows).
- Tipica dei sistemi operativi, workstation offline, ambienti isolati.
- Può usare password, PIN, biometria, smart card.

Vantaggi
- Funziona anche senza rete.
- Più semplice da implementare.

Svantaggi
- Se l’host viene compromesso, l’attaccante ottiene l’intero database delle credenziali.
- Difficile da scalare in ambienti con molti utenti.

Rischi comuni
- Password hash rubati tramite attacchi offline.
- Brute force e dictionary attack.
- Credential stuffing se l’utente riutilizza password.

autenticazione tramite server
La verifica delle credenziali avviene su un server centralizzato o un servizio di identità

Vantaggi
- Gestione centralizzata degli utenti.
- Possibilità di MFA (Multi-Factor Authentication).
- Revoca immediata delle credenziali.

Svantaggi
- Richiede rete e disponibilità del server.
- Se il server di autenticazione cade, nessuno può accedere.

Rischi comuni
- Attacchi man-in-the-middle sulle sessioni di autenticazione.
- Furto di token o session hijacking.
- Attacchi al server di identità (single point of failure).

# PROTOCOLLI DI AUTENTICAZIONE

## TACACS+
Protocollo AAA sviluppato da Cisco, molto usato per l’accesso amministrativo ai dispositivi di rete.
Cosa fa
- Gestisce autenticazione, autorizzazione e accounting separatamente.
- Usa TCP (porta 49), quindi è più affidabile nelle comunicazioni rispetto a UDP.
- Cifra l’intero payload del pacchetto, aumentando la sicurezza.
Comportamento rispetto all’autenticazione
- Supporta scambi di autenticazione complessi e di lunghezza arbitraria.
- Può usare diversi metodi: password, CHAP, token, Kerberos, ecc.
- Ideale per controllare i comandi che un amministratore può eseguire su un router/switch.
l'autenticazione tacacs+ ha 3 tipi di pacchetto Start, continue, reply
- start -> l'autenticazione tacacs+ ha 3 tipi di pacchetto Start, continue, reply
“Voglio iniziare una procedura di autenticazione, ecco il tipo e il metodo che voglio usare.”
- continue -> Viene usato durante la procedura di autenticazione, dopo lo START. serve per continuare il dialogo tra client e server.
- reply ->È il pacchetto che il server TACACS+ manda al client per dare un esito (successo/fallimento), oppure chiedere altre informazioni.(SUCCESS , FAIL, CONTINUE(se servono altri dati))
1) START -> CLIENT RICHIEDE AUTENTICAZIONE ESPLICITANDO IL METODO
2) REPLY -> IL SERVER RISPONDE CON RICHIESTA DI INFROMAZIONI
3) CONTINUE -> A RICHIESTA GIA FATTA VIENE INOLTRATA UN ALTRA INFORMAZIONI RICHIESTA DAL REPLY
4) REPLY -> RICHIESTA DI INFORMAZIONI AGGIUNTIVE
5) CONTINUE -> RISPOSTA DEL CLIENT ALLE INFORMAZIONI AGGIUNTIVE
6) REPLY -> IL SERVER RESTITUISCE SUCCESS O FAIL

## RADIUS
Protocollo AAA molto diffuso per autenticare utenti che accedono a reti Wi-Fi, VPN, ISP, ecc.
Cosa fa
- Gestisce AAA, ma combina autenticazione e autorizzazione.
- Usa UDP (1812 per auth, 1813 per accounting).
- Cifra solo la password, lasciando altri campi in chiaro.
Comportamento rispetto all’autenticazione
- Funziona come intermediario: riceve le credenziali e le verifica localmente o tramite backend (LDAP, Active Directory).
- Ottimo per ambienti con molti utenti (Wi-Fi aziendale, VPN).
- Meno granulare di TACACS+ per i permessi.

## Kerberos
Protocollo di autenticazione basato su ticket e crittografia simmetrica, usato soprattutto in ambienti enterprise (es. Active Directory).
Cosa fa
- Permette autenticazione forte senza inviare password sulla rete.
- Usa un server centrale chiamato KDC (Key Distribution Center).
- Fornisce ticket di sessione che dimostrano l’identità dell’utente ai servizi.
Comportamento rispetto all’autenticazione
- L’utente si autentica una sola volta (SSO).
- Il KDC rilascia un TGT (Ticket Granting Ticket).
- I servizi verificano i ticket senza richiedere password aggiuntive.
- Molto sicuro contro replay e MITM se configurato correttamente.
- DCE (Distributed Computing Environment)
- Framework sviluppato da OSF per sistemi distribuiti, oggi poco diffuso.
Cosa fa
- Fornisce servizi di rete come RPC, directory, sicurezza.
- Include un proprio sistema di autenticazione basato su Kerberos.
- Comportamento rispetto all’autenticazione
- Usa un modello simile a Kerberos per verificare identità e permessi.
- Offre autenticazione centralizzata per applicazioni distribuite.
- Storicamente usato in ambienti UNIX enterprise.

## FORTEZZA
Sistema di sicurezza sviluppato dal governo USA, basato su hardware e crittografia forte.
Cosa fa
- Utilizza schede hardware (Fortezza cards) per autenticazione e cifratura.
- Basato sullo standard MISSI (Multilevel Information System Security Initiative).
- Usato in contesti militari e governativi.
Comportamento rispetto all’autenticazione
- L’autenticazione avviene tramite token hardware contenente chiavi e certificati.
- Garantisce elevata sicurezza fisica e logica.
- Non comune nel settore commerciale.

## AAA — Authentication, Authorization, Accounting
AAA è un modello fondamentale nella sicurezza delle reti.
Serve per gestire chi accede, cosa può fare, e cosa ha fatto.

1. Authentication (Autenticazione)
Verifica l’identità dell’utente.
Esempi:
- Password
- Certificati
- Token
- Kerbero
- TACACS+ / RADIUS

2. Authorization (Autorizzazione)
Stabilisce cosa può fare l’utente dopo essere stato autenticato.
Esempi:
- Può eseguire comandi su un router?
- Può accedere a una cartella?
- Può configurare un firewall?
- TACACS+ è molto forte in questo punto perché permette autorizzazioni granulari.

3. Accounting (Tracciamento)
Registra cosa ha fatto l’utente.
Esempi:
- Log di accesso
- Comandi eseguiti
- Durata della sessione
- Tentativi falliti
- Fondamentale per audit, forensics e incident response.

## CISCO 
Cisco è una delle aziende più importanti al mondo nel settore networking e sicurezza.
Produce router, switch, firewall, sistemi di autenticazione e protocolli proprietari come TACACS+.

Fornisce dispositivi di rete che usano protocolli AAA (TACACS+, RADIUS).
Offre soluzioni di sicurezza come Cisco ISE (Identity Services Engine) per autenticazione centralizzata.
Implementa standard industriali per reti aziendali, VPN, accesso remoto.
Perché è importante in cyber security
È lo standard de facto nelle infrastrutture enterprise.
I protocolli Cisco (es. TACACS+) sono fondamentali per controllare l’accesso degli amministratori ai dispositivi di rete.
Le certificazioni Cisco (CCNA, CCNP Security) sono tra le più richieste.

## UDP (User Datagram Protocol)
UDP è uno dei protocolli principali del livello Trasporto (Layer 4 del modello OSI).
Caratteristiche
- Connessione non orientata → non stabilisce una sessione come TCP.
- Nessun controllo di errore → niente ritrasmissioni, niente garanzie.
- Molto veloce, ma meno affidabile.
Perché è usato nell’autenticazione
- Alcuni protocolli AAA come RADIUS usano UDP perché:
devono essere veloci (autenticazione di molti utenti).
- la perdita di un pacchetto può essere gestita dall’applicazione.
Esempi di porte
- RADIUS: 1812/UDP (autenticazione), 1813/UDP (accounting)
- DNS: 53/UDP
- DHCP: 67/68 UDP

## Amministrazione siti web tramite provider diretto
Accedi al pannello del provider tramite browser e gestisci tutto da lì:

File manager integrato
- Database
- Email
- DNS
- Backup
- Installazione CMS (WordPress, Joomla, ecc.)
Vantaggi
- Semplice e immediato: tutto accessibile da interfaccia grafica.
- Sicurezza maggiore: connessione HTTPS, autenticazione forte, MFA.
- Backup integrati: spesso automatici.
- Gestione completa: non solo file, ma anche database, certificati SSL, utenti, ecc.
- Nessun software da installare: basta un browser.

Svantaggi
- Meno controllo tecnico rispetto all’accesso diretto ai file.
- Limitazioni del provider: alcune operazioni avanzate potrebbero non essere disponibili.
- Dipendenza totale dal pannello: se il pannello ha problemi, non puoi lavorare.

## Amministrazione siti web tramite FTP / SFTP / FTPS
Usi un client FTP per collegarti al server e gestire direttamente i file del sito.

Differenze tra FTP, FTPS e SFTP
- FTP → NON cifrato (sconsigliato)
- FTPS → FTP + TLS (cifrato)
- SFTP → basato su SSH, molto sicuro

Vantaggi
- Controllo totale sui file: puoi modificare, cancellare, caricare tutto.
- Perfetto per sviluppatori: utile per deploy manuali o debugging.
- Indipendente dal pannello: funziona anche se il provider ha problemi.

Svantaggi
- FTP classico è insicuro: password in chiaro → MITM, sniffing.
- Rischio errori: basta cancellare un file sbagliato e il sito cade.
- Nessuna gestione avanzata: niente database, DNS, email, backup.
- Richiede software esterno. 

# PROTOCOLLO TELNET E SSH
Telnet è un protocollo ed un applicativo di rete molto vecchio (anni ’70) che permette di collegarsi a un dispositivo remoto tramite connessione testuale.
È stato fondamentale nella storia di Internet, ma oggi è considerato insicuro perché non cifra nulla: tutto passa in chiaro (password comprese).
Ad oggi è stato sostituito da SSH che cifra completamente i dati supporto utilizzo di chiavi, tunneling ed agent forwarding.
applicazioni SSH
ssh (client da terminale Linux/macOS/Windows)

- OpenSSH (server e client)
- PuTTY (client SSH per Windows)
- Termius, MobaXterm, ecc.
Quindi:
- Telnet = protocollo
- telnet.exe = programma che usa quel protocollo
- SSH = protocollo
- OpenSSH = programma che usa quel protocollo

A cosa serve SSH
Accedere in modo sicuro a un server remoto.
Gestire file, configurazioni, servizi.
Fare tunneling, forwarding, backup, deploy.
SSH cifra tutto, Telnet no.
Ogni servizio usa una porta standard:

Servizio	Porta	Protocollo
Telnet	     23	     Telnet
SSH	         22	     SSH
HTTP	     80	     Web non cifrato
HTTPS	    443	     Web cifrato
FTP	         21	     File Transfer
DNS	         53	     Risoluzione nomi
RDP	       3389	     Desktop remoto
porta aperta = schermo nero ------- porta chiusa = errore di connessione

## PROXY 
Un proxy è un “intermediario” tra te e Internet.
utente → Proxy → Internet
Internet → Proxy → utente
Il proxy riceve le tue richieste, le inoltra al server finale e poi ti restituisce la risposta.

1) PER COSA SI USA UN PROXY (scopi reali)
- Nascondere il tuo IP
Il sito vede l’IP del proxy, non il tuo.
- Filtrare o bloccare siti
Usato in scuole, aziende, reti pubbliche.
- Controllare il traffico
Log, monitoraggio, sicurezza.
- Velocizzare la navigazione
Proxy caching → salva copie dei contenuti.
- Accedere a risorse interne
Proxy aziendali per accedere a server interni.
- Bypassare restrizioni
Es. contenuti non disponibili nel tuo paese.

Esistono diverse tipologie di PROXY
1) HTTP Proxy
   - Per navigazione web
   - Non gestisce altri protocolli
2) SOCKS5 PROXY
    - flessibilità
    - supporta tutti i protocolli (SSH, giochi, app)

3) REVERSE PROXY
    - sta davanti al serve per gestire caching, sicurezza, bilanciamento, routing
si può utilizzare con il comando "curl"

SOCKS5 è un tipo di proxy avanzato che instrada il traffico a livello di trasporto, non a livello applicativo.
- Il server vede l’IP del proxy, non il tuo.
- Molto usato per accedere a contenuti bloccati.
Il __BROWSER TOR__ crea all'accesso un proxy SOKCS5 e viene utilizzato per anonimato, bypass censure e blocchi, accesso dark web e ricerca e studio per cyber security

