# FODNAMENTI DI CRITTOGRAFIA
la necessita della crittografia è stata necessaria poiche inizialmente i dati venivano trsmessi in chiaro e attraverso router o connessioni utenti malevoli potevano porsi nel mezzo per intercettare i dati durante le trasmissioni (MAN IN THE MIDDLE) svolgendo poi delle truffe a carico delle persone che avevano trsmesso i dati. La codifica ncessita ovviamente di una chiave di decodifica per avere un messaggio chiaro e leggibile quindi successivamente furono create dei programmi di codifica e solo il ricevente specifico aveva la chiave di decodifica per decifrare il messaggio.

# CYBER SECURITY
protegge:
1) PERSONE
- 
2) SISTEMI 
- protegge il corretto funzionamento
3) DATI
- garantisce disponibilita(garantendo il funzionamento dell'hardware e del software e dei sistemi trasmissivi(rete ecc..) ), segretezza(confidenzialità)(mediante garanzia di predisposizione degli utenti idonei),integrità(affidabilità dei dati piu affidabile = piu valore) 

# LA CRITTOGRAFIA
La crittografia è la scienza che studia la scrittura e la lettura di messaggi cifrati ed è il fondamento sui chi basano autenticazione integrita e segretezza. La complessita in BIT di una chiave di cifratura ne da la difficoltà al suo decifraggio se non si conosce la chiave in partenza cosi da evitare che un attacco in __BRUTE FORCE__ dove vengono provate ripetutamente tutte le possibili combinazioni possa portare alla cifratura della chiave.
1) CHIAVE SIMMETRICA    
- utilizza un unica chiave sia per la codifica che per la decodifica

utente1 → messaggio → codifica → internet → messaggio codificato → decodifica → utente2

2) CHIAVE ASIMMETRICA
- utilizzo di due chiavi una pubblica e una privata

utente1 → chiave pubblica → utente2 → chiave pubblica2 → utente1
- gli utenti hanno ognuno 2 chiavi scambiano la chiave pubblica per codificare il messaggio e mantengono la propria chiave privata per decodificare il messaggio stesso quindi il secondo utente avra solo la parte per la codifica ma non quella per decodificare
3) HASH crittografia irreversibile
- posso da un testo in chiaro trasformarlo in una stringa criptata questa stringa è chiamata __HASH__ __DIGEST__ (funzioni irreversibili) ma non posso tornare indietro dalla password criptata alla stringa in chiaro poiche non fa una cifratura ma, trasforma la stringa, non usa una chiave specifica, produce sempre una stringa della stessa lunghezza    E AD UGUALE INPUT DEVE DARE UGUALE OUTPUT, avendo poche informazioni al riguardo non è possibile tornare alla stringa originale, le password vengono hashate prima di essere salvate o comparate al database in modo che inserendo la password in chiaro venga hashata prima di essere inserita o comparata quindi la comparazione avviene a password hashata
# AUTENTICAZIONE E AUTORIZZAZIONE
L’autenticazione è il processo attraverso il quale un sistema verifica l’identità di un utente tramite credenziali appropriate (password, token, smart card, dati biometrici).
Una volta autenticato, l’utente può essere autorizzato ad accedere a specifici dati o risorse in base ai suoi permessi.
I sistemi moderni adottano il modello di sicurezza Zero Trust, che si basa sul principio “Never trust, always verify”: nessun utente o dispositivo è considerato affidabile a priori, nemmeno se già all’interno della rete. Ogni accesso viene verificato continuamente e concesso solo con i privilegi minimi necessari.
Le grandi aziende non danno a tutti gli utenti gli stessi permessi.
Per evitare rischi, seguono due principi fondamentali:

1. Segmentazione per settori (o reparti)
Ogni reparto ha:
- i propri dati
- i propri sistemi
- i propri responsabili
- i propri livelli di accesso

2. Accesso limitato anche ai dirigenti
Essere dirigenti non significa avere accesso totale.
- Un dirigente può:
- avere accesso completo al proprio settore
- avere accesso parziale ad altri settori
- vedere solo ciò che è necessario per il suo ruolo (principio del least privilege)

3. Creazione di gruppi separati e privilegiati
Le aziende creano gruppi di sicurezza:
- gruppi standard (impiegati)
- gruppi avanzati (team leader, manager)
- gruppi ad alta fiducia (CISO, amministratori IT, auditor)
- Solo chi appartiene a un gruppo può:
- accedere a certi documenti
- modificare configurazioni
- vedere dati sensibili
- interagire con altri reparti ad alto livello

autenticazione → identità dell'individuo o periferica
autorizzazione → attività possibili da svolgere dopo essere stati autenticati

### Zero Trust significa
- il sistema non si fida mai di nessuno, nemmeno se è già dentro la rete.
- Ogni accesso viene verificato continuamente:
- identità dell’utente
- dispositivo utilizzato
- posizione geografica
- livello di rischio
- ruolo aziendale
- orario
- comportamento anomalo

Nelle grandi aziende i modelli di fiducia si basano sulla segmentazione per settori e sulla gestione dei privilegi.
Ogni reparto ha un proprio responsabile che può accedere ai dati del suo settore, mentre l’accesso ai dati degli altri reparti è limitato e concesso solo in base al ruolo e alle necessità operative.
È possibile creare gruppi separati con livelli di fiducia diversi, così che solo gli utenti autorizzati possano interagire pienamente con più settori.
I sistemi moderni adottano il modello Zero Trust, secondo cui nessun utente o dispositivo è considerato affidabile a priori. Ogni accesso viene verificato continuamente e concesso solo con i privilegi minimi necessari.
IAM → IDENTITY ACCESS MANAGMENT
### SSO → single sign on
è un sistema che permette a un utente di autenticarsi una sola volta e poi accedere automaticamente a più applicazioni, servizi o piattaforme senza dover reinserire la password ogni volta. 
1. Migliora la sicurezza generale ma tiene un account privilegiato come "preda"
- Meno password da ricordare → meno password deboli
- Riduce il phishing
- Tutto è centralizzato e controllato
- Si integra con MFA (autenticazione a più fattori)
2. Migliora la produttività
- L’utente non perde tempo a fare login ovunque
- Accesso immediato a tutti i servizi aziendali
3. Gestione centralizzata
- Se un dipendente lascia l’azienda, basta disattivare un solo account
- Le autorizzazioni sono gestite per gruppi e ruoli

### SSO non significa fidarsi ciecamente
Nel modello Zero Trust:
- l’utente si autentica una volta (SSO)
- ma ogni accesso viene comunque verificato
- il token ha durata limitata
- il sistema controlla continuamente contesto e rischio

# GESTIONE DELLE CHIAVI
La gestione delle chiavi è prettamente umana spesso non viene considerato il lato umano. Una chiave diventa a rischio quando banalmente entrano in gioco emozioni umana negative ( rabbia, invidia, malcotento generale) il sistema di sicurezza dovrebbe essere controllato e consapevolmente anche in base a questo prendere iniziative per modifica accessi , password e attività

### certificati digitali
I certificati digitali sono uno degli elementi più importanti della sicurezza informatica moderna.
Servono a dimostrare l’identità di un sito, un server, un utente o un dispositivo in modo sicuro e verificabile.
Un certificato digitale è un documento elettronico firmato da un’autorità fidata (CA – Certificate Authority) che contiene:
- l’identità del soggetto (es. www.google.com)
- la chiave pubblica del soggetto
- la firma digitale della CA
- la data di validità
- informazioni tecniche (algoritmi, estensioni, ecc.)
SSL (Secure Sockets Layer) è un protocollo nato negli anni ’90 per rendere sicure le comunicazioni su Internet cifrando i dati tra client e server, autenticare il server tramite certificato digitale, impedir eintercettazioni MITM il precursore del certificato __HTTPS__
Oggi SSL è considerato obsoleto.
È stato sostituito da TLS (Transport Layer Security), che è essenzialmente piu sicuro piu veloce e piu aggiornato

Tipi di certificati
1. DV (Domain Validation)
- Verifica solo il dominio
- Usato per siti normali
- Rapido ed economico
2. OV (Organization Validation)
- Verifica anche l’azienda
- Più affidabile
3. EV (Extended Validation)
- Verifica approfondita dell’azienda
- Massima fiducia (banche, istituzioni)

A cosa serve un certificato digitale:
1. Autenticare l’identità
- Dimostra che un sito o un server è davvero chi dice di essere.
Quando si visita https://www.dns.it, il browser controlla il certificato per verificare che sia davvero Amazon.
2. Crittografare la comunicazione
Grazie alla chiave pubblica contenuta nel certificato, il browser può stabilire una connessione HTTPS sicura.
3. Garantire integrità
Assicura che i dati non siano stati modificati durante il trasferimento.

Come funziona
Ti colleghi a un sito HTTPS
Il sito ti invia il suo certificato digitale
Il browser controlla:
se è firmato da una CA fidata
se non è scaduto
se il dominio corrisponde
Se tutto è ok → connessione sicura
Browser e server si scambiano una chiave di sessione per cifrare i dati

Le Certificate Authority (CA)
- DigiCert
- Sectigo
- GlobalSign
- Let’s Encrypt (gratuita)
- Entrust
Sono enti riconosciuti a livello mondiale per il rilascio di certificati digitali.

# GARANTI DI CHIAVI
Il garante di chiavi è un sistema che trasferisce una chiave sensibile o privata ad un terzo soggetto finche delle determinate condizioni non vengono soddisfatte.
La problematica al riguarda di questo soggetto riguarda la fiducia e la valutazione dell'onestà rispetto a chi o cos'è il soggetto a cui viene inviata la chiave. La domanda sembra scontata...perche passare la mia chiave privata ad un terzo? poiche essendo umani potremmo perdere semplicemente la chiave, dimenticarla, subire un danno nella posizione di salvataggio della chiave...sostanzialmente è come avere un buckup della propria chiave privata in modo da non perderla mai definitivamente

# RIEPILOGO