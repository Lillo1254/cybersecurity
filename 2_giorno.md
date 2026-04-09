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
# SPAZI DI NOME

# GESTIONE DELLE CHIAVI

# GARANTI DI CHIAVI

# RIEPILOGO