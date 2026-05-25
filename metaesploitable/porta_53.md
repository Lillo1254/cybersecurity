# porta 53 domain
La porta 53 (DNS / Domain) è una delle più cruciali in qualsiasi infrastruttura di rete. Se compromessa o mal configurata, può esporre l'intera topologia di una rete o permettere attacchi di reindirizzamento del traffico. Il protocollo DNS (Domain Name System) è spesso definito come la "rubrica telefonica" di Internet o di una rete locale I computer comunicano tra loro utilizzando gli indirizzi IP (es. 192.168.56.102), mentre gli esseri umani ricordano più facilmente i nomi testuali (es. google.com o, nel caso di Metasploitable, metasploitable.localdomain). Quando un computer vuole comunicare con un nome testuale, interroga il server DNS sulla porta 53

Il DNS è uno dei pochi servizi che utilizza entrambi i protocolli di trasporto UDP e TCP. In una fase di Information Gathering e Penetration Testing, la porta 53 è una miniera d'oro per tre motivi principali Mappatura della Rete, Identificazione della Versione (Software Fingerprinting), Attacchi di Spoofing / Avvelenamento (Cache Poisoning) andiamo quindi ad effettuare un anali specifica come fatto in precedenza sulla porta 53 per verificare stato servizio e versione

- nmap -p 53 -sV 192.168.56.102
  - -p 53 indica la scansione su una specifica porta
  - -sV effettuato una scansione con pacchetti probs per verificare la stringa di risposta e accertarne la versione del software

otteniamo quindi un risultato simile a questo

Host is up (0.00055s latency).

PORT   STATE SERVICE VERSION
53/tcp open  domain  ISC BIND 9.4.2
MAC Address: 08:00:27:FA:55:6B (Oracle VirtualBox virtual NIC)

ci conferma pertanto lo stato della porta 53 su aperta il servizio utilizzato domain(DNS) e la versione ISC BIND 9.4.2

In una rete aziendale reale quando ci sono due server DNS uno primario ed uno secondario per sicurezza il secondo chiede periodicamente al primario di fargli avere una copia della rubrica dei dns e quest'azione avviene proprio sulla porta 53 se pertatno il sfotware è malconfigurato e non controlla da dove avviene la richiesta rischia di inviare la mappatura completa degli ip e dns della rete utilizzando Trasferimento di zona (zone transfer-AXFR). Kali linux ha uno strumento preinstallato chiamato "dig" ( domain information groper) che è il tool ufficiale per interrogare i server DNS utilizzando il comando

- dig @192.168.56.102 metasploitable.localdomain axfr
    - dig avvia lo strumento di diagnostica DNS
    - @192.168.56.102 indica a dig di utilizzare questo specifico ip per la scansione
    - metasploitable.localdomain È il nome della zona (del dominio) che vogliamo mappare
    - axfr È il comando specifico che richiede il "Trasferimento di Zona"

l'output che ci verra restituito sarà simile a questo

┌──(kali㉿kali)-[~]
└─$ dig @192.168.56.102 metasploitable.localdomain axfr

; <<>> DiG 9.20.22-1-Debian <<>> @192.168.56.102 metasploitable.localdomain axfr
; (1 server found)
;; global options: +cmd
; Transfer failed.
                       
il server DNS BIND sulla Metasploitable ha rifiutato la nostra richiesta di scaricare l'intera mappa del dominio Dal punto di vista della sicurezza del server, questa è una buona configurazione (chiamata Zone Transfer Restriction) il server è impostato per non rivelare la sua intera "rubrica" al primo sconosciuto che la richiede Tuttavia, nel penetration testing, quando il trasferimento di zona fallisce, non ci si arrende. Si passa al grado successivo di analisi chiamato "Banner grabbing del DNS" Molte versioni di BIND(versione del software trovata in precedenza) hanno una particolarità cioè memorizzano la loro versione esatta all'interno di un record di testo speciale chiamato version.bind all'interno della zona CHAOS Nmap ci ha già dato una stima della versione (9.4.2) ma per sicurezza spesso gli analisti camuffano o nascondono la reale versione (Defense in Depth) quindi invieremo una richiesta precisa per capire se il server risponde alle richieste di informazione di base

- dig @192.168.56.102 version.bind txt chaos
  - dig avvia lo strumento di diagnostica DNS
  - @192.168.56.102 Interroghiamo sempre direttamente il server della Metasploitable
  - version.bind È la stringa standard che interroga la variabile interna del software BIND
  - txt Chiediamo la risposta in formato testuale (Text record)
  - chaos Specifichiamo la classe di rete "CH" (Chaosnet), una classe storica parallela a "IN" (Internet) usata quasi esclusivamente per compiti di amministrazione e diagnostica dei server DNS

il risultato sarà simile a questo

;; ANSWER SECTION:
version.bind.           0       CH      TXT     "9.4.2"

;; AUTHORITY SECTION:
version.bind.           0       CH      NS      version.bind.

;; Query time: 19 msec
;; SERVER: 192.168.56.102#53(192.168.56.102) (UDP)
;; WHEN: Mon May 25 06:05:52 EDT 2026
;; MSG SIZE  rcvd: 73



ci è stata confermata la versione del servizio In una macchina reale configurata per la massima sicurezza, questa opzione viene solitamente disattivata o camuffata (configurando BIND con una stringa falsa come "Versione non disponibile"), perché dare la versione esatta a un potenziale attaccante facilita enormemente il suo lavoro di ricerca Visto che il Trasferimento di Zona (AXFR) ha fallito e non ci ha permesso di scaricare la rubrica completa in un colpo solo, i penetration tester usano una tecnica alternativa per mappare comunque la rete: il Brute Force dei Sotto-domini. è molto simile ad un enumerazione degli utenti per farlo abbiamo bisogno di un file .txt contenente il dizionario dei sotto-domini che vogliamo testare e lanciare il comando

- dnsrecon -d metasploitable.localdomain -D /usr/share/wordlists/dnsmap.txt -t brt -n 192.168.56.102
  - dnsrecon è lo strumento avanzato per l'enumerazione e analisi dei servizi dns
  - -d metasploitable.localdomain è il "dominio di base" che vogliamo analizzare
  - -d percorso/del/file.txt che vogliamo utilizzare come dizionario
  - -t brt dice al programma di usare la modalità brute force
  - -n [ip_macchina_vulnerabile] forza lo strumento a fare queste prove sul server DNS specificato

il risultato sarà simile a questo

┌──(kali㉿kali)-[/usr/share/wordlists]
└─$ dnsrecon -d metasploitable.localdomain -D /usr/share/wordlists/dnsmap.txt -t brt -n 192.168.56.102
2026-05-25T06:16:45.619538-0400 INFO Using the dictionary file: /usr/share/wordlists/dnsmap.txt (provided by user)
2026-05-25T06:16:45.619702-0400 INFO Starting enumeration for domain: metasploitable.localdomain
2026-05-25T06:16:45.619875-0400 INFO brt: Performing host and subdomain brute force against metasploitable.localdomain...
2026-05-25T06:17:47.512815-0400 INFO 0 Records Found
2026-05-25T06:17:47.517756-0400 INFO Completed enumeration for domain: metasploitable.localdomain

poiche metaesploitable è una macchina virtuale autonoma che non gestisce nessun sotto-dominio ci restituirà come risultato 0 founds questo ci permette di capire due cose, la prima è che sapendo che non ci sono sotto-domini risparmiamo tempo e lasciamo perdere questa parte poiche jnon ha vulnerabilità legate alla mappatura, la seconda è che ora passiamo direttamente a verificare le vulnerabilità della versione specifica del software dove permette un chache poisioning in cui un attaccante inserisce la risoluzione di un DNS leggittimo reindirizzando il traffico in un suo ip pertanto successivamente tutto il traffico inviato verra reindirizzato verso di lui.

C'è un problema sul laboratorio in corso...la metaesploitable non può inviare richieste poiche sono terminael quindi non è possibile fare quest'operazione di poisioning