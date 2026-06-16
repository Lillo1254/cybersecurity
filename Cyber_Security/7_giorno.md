# Backup
Il backup è un’attività pianificata che consiste nel creare copie dei dati per poterli ripristinare in caso di:

- perdita accidentale
- cancellazione involontaria
- guasto hardware
- errore umano
- ransomware
- corruzione dei file
**Il backup non serve a proteggere i dati da furto o accesso non autorizzato il backup serve invece a garantire integrità e disponibilità dei dati**

## Backup Full
copia tutti i dati ogni volta cosi si puo averre un ripristino rapido in caso di incidente con una copia completa e affidabile a svantaggio di questa operazione ci sono le tempestiche necessarie per il processo e lo spazio occupato dai dati stessi di elevato peso

## Backup Incrementale
Questa formula è utilizzata in due fasi per essere utilizzata poiche richiede un backup full di base e il backup incrementale salva solo le modifiche che sono state effettuate ai dati dell'ultimo buckup qualsiasi esso sia (full--> incrementale1 --> incrementale2 --> incrementale3 per il ripristino serve il full + tutti gli incrementali) rendendo il processo veloce non occupando molto spazio ma per il ripristino senrve prima ripristinare il backup full e poi l'incrementale

## Backup Differenziale
Un sistema di backup che utilizza un backup full di base e poi copia tutti file modificati da dopo il backup full conservando tutti i cambiamenti all'interno di un unico backup differenziale cosi per il ripristino sono necessari solo il backup full e l'ultimo backup differenziale 

## Backup Mirror
Una copia speculare dei dati senza versione, sostanzialmente si salva una copia completa dei dati a quel momento cosi da avere in caso di incidente un ripristino immediato ma ha delle controindicazioni poiche non avendo versione precedenti dei dati se si cancella un file non sarà recuperabile

## Backup continuo
Il salvataggio dei dati in tempo reale creando un ripristino praticamente immediato utilizzato in quelli ambienti critici quali banche ospedali ecc. questo buckup continuo ovviamente ha dei costi onerosi e richiede storage e infrastruttura avanzata

## Backup offsite/Cloud
Un backup conservato fuori sede su un datacenter esterno cosi da essere protetto da incendi furti disastri ed accesibile ovunque ma è sottoposto al corretto funzionamento della rete e dai costi di "stoccaggio"

## Backup locale (On-promise)
Un backup su NAS che  un dispositivo di archiviazione collegato alla rete che permette di condividere, salvare e proteggere dati tra più dispositivi, dischi esterni o server interni veloce e controllato totalmente dall'azienda ma è molto vulnerabile a disastri locali interni

**schema GFS (grandfather father son) backup full mensili, backup differenziali settimanali, backup incrementali giornalieri**
**il tempo di trascorso tra un backup e un altro si chiama FREQUENZA o SCHEDULE**
**il tempo per cui un backup viene conservatio prima di essere eliminato si chiama RETENTION**


### NAS (Network Attached Storage)
Un NAS è un dispositivo di archiviazione collegato alla rete che funziona come un server di file semplificato, progettato per conservare, condividere e proteggere dati all’interno di una rete locale. Sostanzialmente un hard disk intelligente collegato alla rete, accessibile da più dispositivi contemporaneamente composto da 1 o piu dischi (HDD,SDD), sistema operativo dedicato, processore e ram, porte ethernet, servizi integrati come backup cloud privati media server, utenti, permessi in pratica un mini-server semplificato per essere accessibile senza competenze avanzate

### RAID
RAID significa Redundant Array of Independent Disks è una tecnologia metodo per organizzare fisicamente i dischi che permette di usare più dischi come se fossero un unico sistema, per ottenere maggiore sicurezza dei dati (ridondanza), maggiori prestazioni, maggiore disponibilità non protegge da guasti di dischi, cancellazione dati, ransomware o errori umani.

- RAID 0 – Striping (prestazioni, zero sicurezza) velocità altissima usa il 100% dello spazio a disposizione ma se un disco si rompe si perdono tutti i dati poiche non ha ridondanza
- RAID 1 - Mirroring (sicurezza alta) i dati vengono duplicati su due dischi in maniera tale che se un disco si rompe i dati sono sull'altro aumentanto la disponibilità e diminuendo pero lo spazio a disposizione poiche dimezza lo spazio totale per fare una copia quindi spazio disponibile 2gb di cui 1gb sul disco principale e 1gb sul disco secondario
- RAID 5 – Striping + Parità (equilibrio perfetto) servono minimo 3 dischi i dati vengono distribuiti e una parte viene usata per la parità che permette di ricostruire i dati se un disco si rompe offrendo un buon equilibrio tra spazio prestazioni e sicurezza della disponibilità dei dischi tollerando la rottura di 1 disco a discapito della possibile ricostruzione che avviene in maniera piu lenta e in caso di perdita di un secondo disco si perdono tutti i dati
- RAID 6 – Doppia Parità (molto sicuro) utilizza minimo 4 dschi effettuando le stesse oparazioni del raid 5 ma tollerando fino a 2 dischi guasti ovviamente avendo prestazioni inferiori al raid-5
- RAID 10 (1+0) – Mirroring + Striping utilizza minimo 4 dischi combinando raid 1 e raid 0 dumezzando lo spazio a disposizione ma aumentando la tollerrenza di guasto ai dischi poiche dipende da quali dischi si guastano aumentando la sicurezza della disponibilità dei dati e la velocità
  
**La parità è gestita da un algoritmo interno che si occupa di ricostruire i dati mancanti, poiche nei dischi vengono salvati come codice binario, la parità utilizza l'equazione [disco1 XOR disco2] quindi avendo anche solo con disco1 attivo e il disco di parità utilizzando questa equazione si estrapola il contenuto di disco2**

esempio. disco1 = ciao disco2=hello doscoparità = XOR(ciao,hello) disco1 si rompe il raid fa disco1= disco2 XOR parita il sistema funziona a blocchi ed ogni blocco viene ricostruito uno per volta

## Regola 3-2-1
Avere un backup su un unica unità di conservazione qualisiasi essa sia non è consigliato poiche se quella cessa di funzionare si perdono tutti i dati si segue invece la regola 3-2-1

**3 copie dei dati** 
- (copia 1 dati originali, copia 2 dati del primo backuo, copia 3 dati backup su altro dispositivo)
  
**2 supporti diversi**
- Le copie sono presenti in due supporti di storage diversi in modo da ovviare al fallimento del supporto principale
  
**1 copia offsite**
- almeno una copia deve essere offsite fuori sede cosi da avere un backup protetto da disastri quali incendio furto allagamento ransomware blackout ecc..

# test ripristino
A cadenza periodica va testato il ripristino del database tramite backup su server di test isolare per verificare l'avvio del database eseguire query di controllo verificare presenza dati recenti misurare il tempo totale di ripristino e fare una documentazione della procedura dettagliata questo per verificare che il il ripristino del database funzioni tecnicamente rientri nel tempo di RTO(Recovery Time Objective) cioè il tempo massimo entro cui un servizio sistema o un database deve essre ripristinato dopo un guasto,  si attesta che produca dati utilizzabili e che abbia procedure chiare e ripetibili poiche la documentazione creata sarà poi necessaria in caso di emergenza reale per ovviare alla problematica

# RTO(Recovery Time Objective)
Quando un ripristino supera l’RTO, la causa potrebbe essere 
- backup troppo lenti da scaricare
- storage lento
- rete insufficiente
- database troppo grande
- procedure non ottimizzate
- personale non addestrato
- documentazione incompleta
- hardware del server di test troppo debole
- tempi morti (attese, copie intermedie, decompresssioni, ecc.)

**Procedure per velocizzare i processi**

- megliorare la tecnologia di backup passando a dischi piu veloci o NAS interni, cambiare tipologia di backup passando a backup incrementali con restore rapido ecc.

- ottimizzare i database tramite compressione riduzione log archiviazione dati vecchi partizionamente o tuning del motore DB

- migliorare le procedure eliminando passaggi inutili automatizzando parti del ripristino preparando script di restore ed evitando copie intermedie

- migliorare l'infrastruttura con una rete piu veloce uno storage piu performante server piu potente o ridurre la latenza tra repository backup e infrastruttura

- formazione del personale su restore del backup documentazione chiara della procedura con comandi e file in chiaro e semplice comprensione

Successivamente al test se non si riesce a risettare l'RTO e si hanno già proposte le iniziative per l'aggiornamento dell'infrastruttura si può ritrattare  l'RTO aumentandone il tempo richiesto dopo aver presentato i risultati dei test recovery

# Tipi di dati
Dati pubblici:
- dati giò pubblici o pubblicabili che non richiedono protezione particolare  Nessun impatto se divulgati
  
Dati interni:
- per uso interno ma non sensibili tipo rpcedure aziendali organigrammi accessibili solo ai dipendenti Rischio basso in caso di divulgazione

Dati confidenziali:
- dati sensibili del business come contratti database clienti  la cui divulgazione può causare danni economici o reputazionali accessibili solo agli autorizzati Crittografia consigliata

Dati riservati:
- dati critici come proprietà intellettuale brevetti ecc. la cui esposizione può causare danni gravi all’azienda che richiedono massima protezione Accesso limitato a pochissime persone Crittografia obbligatoria Monitoraggio degli accessi

Dati top-secret: 
- Il livello più alto di protezione la divulgazione comporterebbe danni catastrofici all’azienda o violazioni legali gravissime come algoritmi proprietari critici, chiavi crittografiche master, credenziali di amministrazione di sistemi core, documenti legati a fusioni/acquisizioni non pubbliche ecc. accesso solo a personale strettamente autorizzato crittografia forte sistemi isolati (air‑gap o segmentazione estrema) logging e monitoraggio continuo autenticazione multifattore obbligatoria procedure di gestione e distruzione controllate

# Cancellazione dei file
I file non si cancellano completamente dai dispositivi di supporto o dal file system il metodo migliore per eliminare il file o piu che altro il suo contenuto bisogna sovrascrivere il file piu e piu volte in maniera tale da perdere le versioni precedenti del file stesso in modo da non poter essere ripristinato con le informazioni corrette questo processo si chiama wiping o secure erase. Molti file osno facilmente recuperabili tramite software di terze parti.
Il sistema operativo segna lo spazio come “libero”, ma i dati restano fisicamente sul disco finché non vengono sovrascritti
in cyber-security  la cancellazione sicura è obbligatoria per dati confidenziali riservati top-secret
tutti gli SSD moderni hanno la funzionalità TRIM che pulisce gli spazi liberi che trova in questa maniera eliminando un file si crea uno spazio libero la funzionalità TRIM lo pulisce completamente rendendo lo spaizo nuovamente disponibile alla scrittura e così facendo cancella completamente il file. a seconda del sistema operativo può essere attivo di default come in windows, attivo solo su determinate marche come in macOS o attivo in modalità periodica o in modalità online su linux a seconda della distribuzione. TRIM potrebbe non funzionare su SSD esterni poiche i controller usb non lo supportano, se si usano fyle system non campatibili, se è stato disattivato manualmente, usando vecchie versioni di sistemi operativi o utilizzando SSD molto vecchi.
In ogni caso a livello aziendale per dati riservati che devono subire cancellazione sicura di file è indispensabile utilizzare un software di wiping per sovrascrivere in piu passaggi e cancellare in maniera completamente sicura un file esistente indifferentemente dall'utilizzo del TRIM stesso cosi da avere pieno controllo della sovrascrittura e cancellazione del file senza affidarsi al sistema nativo degli SSD
