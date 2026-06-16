# Assets
Un asset in cybersecurity è qualsiasi elemento – fisico o digitale – che possiede valore per un’organizzazione e che deve essere protetto poiche è 
considerato un bene o una risorsa tangible o intangibile che ha valore la cui compromissione può causare DANNO
    - Asset fisici: server, computer, router, switch, dispositivi mobili, data center.
    - Asset digitali: software, sistemi operativi, applicazioni, database, documenti digitali, servizi cloud.
    - Dati e informazioni: dati personali, finanziari, proprietà intellettuale, segreti industriali.
    - Asset di rete: firewall, DNS, indirizzi IP, certificati SSL, infrastrutture di rete.
    - Persone: dipendenti, amministratori, utenti con privilegi, fornitori.

Le politiche di sicurezza devono essere pesate e organizzate in base al rischio e criticità delle possibili violazioni e/o malfunzionamenti involontari
causati da forza maggiore naturale quali incendi terremoti sovraccarico ecc. a seconda dell'asset stesso
    - Un server che ospita dati dei clienti → asset critico.
    - Un dipendente con accesso amministrativo → asset umano ad alto rischio.
    - Un certificato SSL scaduto → asset di rete che può esporre a attacchi MITM.
    - Un database con informazioni sensibili → asset informativo di massima priorità.

In principio deve essere stabilita una scala di valutazione basata su possedimenti aziendali (quali __software hardware dipendenti__ ecc.) 
per poter creare una valutazione oggettiva dell'impatto di rischio a cui deve far fronte l'azienda

Gli asset vengono classificati per permettere una gestione del rischio coerente e misurabile. Le categorie più utilizzate sono:
1. Per natura
    - Fisici — hardware, dispositivi, infrastrutture.
    - Logici/digitali — software, applicazioni, database.
    - Informativi — dati, documenti, proprietà intellettuale.
    - Umani — dipendenti, amministratori, fornitori.
    - Di rete — servizi, protocolli, certificati, indirizzi IP.
2. Per valore
    - Critici — la loro compromissione blocca l’operatività (es. server core).
    - Sensibili — contengono dati riservati o personali.
    - Operativi — necessari al funzionamento quotidiano.
    - Accessori — impatto minimo in caso di compromissione.
3. Per esposizione
    - Interni — asset non accessibili dall’esterno.
    - Esterni — esposti a Internet o a terze parti.
    - Ibridi — cloud, VPN, servizi condivisi.

## Tipologie di danno (Impatto)
La compromissione di un asset può generare diversi tipi di danno:
1. Danno economico
    - Perdita diretta di denaro
    - Costi di ripristino
    - Sanzioni (es. GDPR)
2. Danno operativo
    - Interruzione dei servizi
    - Impossibilità di lavorare
    - Malfunzionamenti a catena
3. Danno reputazionale
    - Perdita di fiducia dei clienti
    - Impatto sull’immagine aziendale
    - Difficoltà nel mercato
4. Danno legale
    - Violazioni normative
    - Contenziosi
    - Obbligo di notifica (es. data breach)
5. Danno sulla sicurezza fisica
    - Incidenti causati da malfunzionamenti
    - Rischi per persone o infrastrutture

## Valutazione del rischio (Risk Assessment)
Per ogni asset si valuta il rischio combinando:
1. Valore dell’asset
    - Quanto è importante per l’azienda.
2. Minacce
    - Cosa potrebbe attaccarlo (attaccanti, errori umani, eventi naturali).
3. Vulnerabilità
    - Debolezze sfruttabili (software non aggiornato, configurazioni errate).
4. Probabilità
    - Quanto è realistico che l’evento accada.
5. Impatto
    - Quanto danno causerebbe.

__formula di vlautazione__ RISCHIO EFFETTIVO (PROBABILITà x IMPATTO)

# Misure di protezione (Controlli di sicurezza)
Le misure di sicurezza vengono scelte in base alla criticità dell’asset.
1. Controlli tecnici
    - Firewall, IDS/IPS
    - Cifratura dei dati
    - Backup e disaster recovery
    - Patch management
    - Segmentazione di rete
    - MFA e gestione privilegi
2. Controlli organizzativi
    - Policy di sicurezza
    - Procedure operative
    - Gestione degli accessi
    - Classificazione dei dati
    - Audit periodici
3. Controlli fisici
    - Sorveglianza
    - Accesso controllato ai locali
    - Sistemi antincendio
    - UPS e protezioni elettriche
4. Controlli umani
    - Formazione del personale
    - Sensibilizzazione al phishing
    - Procedure di escalation


# CHIEF IT
Il Chief IT (o CIO, Chief Information Officer) è la figura che gestisce l’infrastruttura tecnologica dell’azienda.
È responsabile della sicurezza, dell’efficienza e dell’evoluzione dei sistemi informatici.
Compiti principali:
- Gestire reti, server, dispositivi e infrastrutture digitali.
- Garantire la sicurezza informatica e la continuità operativa.
- Coordinare il team IT e definire le strategie tecnologiche.
- Implementare soluzioni di sicurezza (firewall, backup, monitoraggio).
- Collaborare con il DPO per assicurare conformità e protezione dei dati.
Ruolo nella sicurezza:
- Il Chief IT è la figura tecnica che mette in pratica le misure di sicurezza, mentre il DPO verifica che siano conformi alle normative.

# POLITICHE GDPR (General Data Protection Regulation)
__Liceità, correttezza, trasparenza, minimizzazione dei dati(solo i dati strettamente necessari per un azione specifica)__
Le politiche GDPR rappresentano l’insieme strutturato di regole, procedure e misure che un’organizzazione adotta per garantire la conformità al 
Regolamento Europeo 2016/679 (GDPR).
Non sono un documento unico, ma un sistema di policy, procedure e registri che dimostrano come l’azienda gestisce i dati personali
Elementi fondamentali:
- Informative sulla privacy chiare e trasparenti facilmente accessibili scritte in linguaggio semplice è il documento pubblico principale:
    - quali dati vengono raccolti
    - perché vengono trattati
    - su quale base giuridica
    - per quanto tempo vengono conservati
    - chi può accedervi
    - come esercitare i propri diritti
    - come contattare il DPO
- Registro dei trattamenti dei dati personali.
- Procedure per la gestione dei consensi.
- Misure tecniche e organizzative per proteggere i dati (cifratura, accessi, backup).
- Procedure per la gestione dei data breach.
- Valutazioni d’impatto (DPIA) per trattamenti ad alto rischio.
- Formazione del personale sulla protezione dei dati.
Obiettivi:
- Garantire la tutela dei diritti degli interessati.
- Ridurre i rischi legati al trattamento dei dati.
- Dimostrare la conformità alle autorità competenti.
Le politiche GDPR vengono definite internamente dall’organizzazione, ma devono rispettare:
- Regolamento UE 2016/679 (GDPR)
- Linee guida del Comitato Europeo per la Protezione dei Dati (EDPB)
- Normativa nazionale (es. Codice Privacy italiano aggiornato)
- Best practice internazionali (ISO 27001, ISO 27701, NIST, CIS Controls)
## Consenso esplicito
Per trattamenti che lo richiedono (marketing, profilazione, newsletter).
Il consenso deve essere:
- libero
- specifico
- informato
- revocabile in ogni momento
## Moduli e interfacce utente
Ogni modulo che raccoglie dati deve indicare:
- finalità
- base giuridica
- obbligatorietà o meno dei dati
- link all’informativa privacy
# Cookie Policy e Cookie Banner
Obbligatori quando il sito utilizza cookie non tecnici.
Devono spiegare:
- quali cookie sono utilizzati
- finalità
- durata
- terze parti coinvolte
- possibilità di rifiutare o revocare il consenso
# Come devono essere documentate internamente
Le politiche GDPR devono essere:
- scritte
- approvate dalla direzione
- aggiornate periodicamente
- conservate e disponibili per audit
Documenti tipici:
- Manuale GDPR aziendale
- Registro dei trattamenti
- Procedure operative (SOP)
- Verbali di formazione
- DPIA (Data Protection Impact Assessment) è uno strumento previsto dal GDPR per analizzare e mitigare i rischi derivanti da trattamenti di dati personali che possono presentare un rischio elevato per i diritti e le libertà degli interessati
- Contratti con fornitori
-Log di sicurezza e accessi
## PRIVACY BY DESIGN
La Privacy by Design è un principio del GDPR secondo cui la protezione dei dati deve essere integrata fin dall’inizio nella progettazione 
di qualsiasi sistema, servizio, applicazione o processo aziendale.
- la privacy non è un’aggiunta finale, ma un requisito progettuale
- i rischi devono essere valutati prima di iniziare il trattamento
- le misure di sicurezza devono essere incorporate nella struttura del sistema
- ogni nuova funzionalità deve essere analizzata per il suo impatto sui dati personali
## PRIVACY BY DEFAULT
La Privacy by Default stabilisce che, per impostazione predefinita, un sistema deve trattare solo i dati strettamente necessari per la finalità prevista.
- le impostazioni iniziali devono essere le più protettive possibile
- l’utente non deve fare nulla per proteggere i propri dati
- i dati raccolti devono essere minimi e proporzionati
- funzionalità non essenziali (es. marketing, tracking) devono essere disattivate di default
# DPO
Il DPO (Data Protection Officer) è la figura prevista dal GDPR responsabile della supervisione della protezione dei dati personali all’interno di un’organizzazione.
Il suo ruolo è indipendente e deve garantire che l’azienda rispetti le normative sulla privacy.
Compiti principali:
- Monitorare l’applicazione del GDPR e delle normative nazionali.
- Informare e formare il personale sulle pratiche corrette di protezione dei dati.
- Effettuare audit e verifiche interne.
- Fornire consulenza sulla valutazione d’impatto (DPIA).
- Essere punto di contatto tra azienda e Garante della Privacy.
Caratteristiche del ruolo:
- Deve avere competenze giuridiche e tecniche.
- Non può avere conflitti di interesse.
- Deve operare con autonomia e indipendenza.
è obbligatorio avere un DPO solo in 3 casi specifici
1) Sei un ente publico
    - Tutti gli organismi pubblici devono avere un DPO, tranne i tribunali quando agiscono in funzione giudiziaria.
2) Tratti dati personali su larga scala che richiedono monitoraggio regolare e sistematico
    - piattaforme che tracciano utenti
    - sistemi di videosorveglianza estesa
    - servizi online che profilano comportamenti
    - aziende che monitorano dipendenti o clienti in modo continuativo
3) Tratti su larga scala categorie particolari di dati o dati giudiziari:
    - salute
    - dati biometrici
    - dati genetici
    - orientamento religioso o politico
    - vita sessuale
    - appartenenza sindacale

# Produzione software proprietario
IT department:
1) Dipartimento di sviluppo:
    - Analisi di fattibilità e valutazione delle tempistiche, delle tecnologie da utilizzare e delle risorse necessarie
    - Allineamento con il reparto vendite attesa dell’approvazione commerciale e conferma dei requisiti richiesti dal cliente o dal mercato
    - Avvio dello sviluppo implementazione del software secondo specifiche tecniche e funzionali
    - UAT – User Acceptance Test al termine dello sviluppo viene eseguito il test di accettazione da parte degli utenti o del reparto incaricato
    - Validazione finale se funzionalità, requisiti e performance risultano conformi, il software può passare allo step successivo
2) Pre-Produzione (Ambiente Intermedio)
    - È un ambiente separato dalla produzione, utilizzato per testare il software in condizioni simili a quelle reali
    - Riproduce l’infrastruttura di produzione ma con risorse ridotte per contenere i costi
    - Permette di individuare problemi non rilevati in sviluppo o UAT.
    - Consente test di integrazione, performance e compatibilità.
    - Garantisce che il software sia stabile prima del rilascio pubblico.
3) Canary test
    - Tecnica di rilascio controllato per ridurre il rischio di errori in produzione
    - Il software viene distribuito a un gruppo ristretto di utenti reali
    - Si monitorano comportamento, performance, errori e possibili vulnerabilità
    - In caso di problemi, il rilascio può essere immediatamente interrotto senza impattare l’intera utenza
    - Se il test è positivo, si procede con il rollout completo
4) Dipartimento di produzione:
    - È il reparto responsabile della messa in esercizio del software e della sua gestione operativa
    - Deployment in ambiente di produzione: rilascio ufficiale del software agli utenti finali.
    - Monitoraggio continuo: controllo costante di performance, sicurezza, stabilità e disponibilità del sistema.
    - Gestione incidenti: intervento rapido in caso di malfunzionamenti, vulnerabilità o interruzioni del servizio.
    - Manutenzione e aggiornamenti: applicazione di patch, miglioramenti e nuove versioni del software.
    - Coordinamento con sviluppo: segnalazione di bug, richieste di miglioramento e feedback operativo.
    - Garanzia della sicurezza: applicazione delle policy interne, gestione accessi, logging e conformità normativa.

# DISASTER RECOVERY
Il Disaster Recovery (DR) è l’insieme di strategie, procedure e tecnologie che un’organizzazione mette in atto per ripristinare sistemi, 
dati e servizi IT dopo un evento catastrofico.
È una componente fondamentale della continuità operativa e della sicurezza informatica
Il Disaster Recovery è il piano tecnico che permette di riportare in funzione l’infrastruttura IT dopo eventi che ne compromettono la disponibilità
- guasti hardware gravi
- incendi, allagamenti, terremoti
- blackout prolungati
- attacchi informatici (ransomware, DDoS, compromissioni)
- errori umani critici
- malfunzionamenti di rete o data center
__L’obiettivo è ridurre al minimo i tempi di fermo e limitare la perdita di dati__
Componenti principali del Disaster Recovery
1. Backup e ripristino
    - copie dei dati locali o remote
    - backup incrementali, differenziali o completi
    - verifica periodica dei backup
    - procedure di restore testate
2. Infrastruttura alternativa
    - data center secondario
    - server di emergenza
    - cloud di failover  per garantire la continuità dei servizi quando l’infrastruttura principale non è più disponibile se avviene un guasto, 
    un attacco o un disastro, il sistema commuta automaticamente sul cloud
    - sistemi ridondati
3. Procedure operative
    - istruzioni passo‑passo per il ripristino
    - ruoli e responsabilità del personale
    - contatti di emergenza
    - priorità dei servizi da ripristinare
4. Metriche fondamentali
    - RTO (Recovery Time Objective): tempo massimo accettabile di fermo
    - RPO (Recovery Point Objective): quantità massima di dati che si può perdere
5. Test periodici
    - simulazioni di disastro
    - verifica dei tempi reali di ripristino
    - aggiornamento del piano in base ai risultati
## In CyberSecurity
Il Disaster Recovery è strettamente collegato alla sicurezza informatica perché:
- limita i danni di un attacco ransomware
- garantisce continuità ai servizi critici
- evita perdita di dati sensibili
- riduce l’impatto economico e reputazionale
- supporta la conformità normativa (GDPR, ISO 27001)