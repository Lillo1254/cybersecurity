1. Prompt dei Comandi Windows (CMD & PowerShell)
Utilizzati principalmente per l'analisi di rete locale e la configurazione del sistema in ambienti Microsoft.

ipconfig /all: Mostra tutti i dettagli delle interfacce di rete, inclusi indirizzi IP, MAC e DNS.  

netstat -ano: Visualizza le connessioni attive e le porte in ascolto, mostrando il PID (Process ID) associato.  

arp -a: Mostra la tabella ARP, utile per mappare gli indirizzi IP agli indirizzi MAC dei dispositivi nella rete locale.  

nslookup <dominio>: Interroga i server DNS per risolvere nomi di dominio o trovare record specifici.  

tracert <IP/host>: Traccia il percorso dei pacchetti verso una destinazione, mostrando ogni salto (hop).  

systeminfo: Genera un riepilogo dettagliato della configurazione hardware e software del sistema.  

tasklist: Elenca tutti i processi in esecuzione sul sistema locale.  

2. Shell Linux (Comandi di Base)
I blocchi fondamentali per navigare e gestire qualsiasi sistema Linux.

ls -la: Elenca file e directory, inclusi quelli nascosti, con permessi e dettagli del proprietario.  

cd <percorso>: Cambia la directory di lavoro corrente.  

pwd: Mostra il percorso assoluto della directory in cui ti trovi.  

grep: Cerca stringhe di testo all'interno di file o output di altri comandi.  

chmod: Modifica i permessi di accesso di file o cartelle (es. chmod +x per rendere un file eseguibile).  

sudo: Esegue un comando con i privilegi dell'amministratore (root).  

cat: Visualizza il contenuto di un file di testo direttamente nel terminale.  

3. Shell Kali Linux (Pentesting & Network)
Specifici per l'analisi di rete e la sicurezza, preinstallati nella distribuzione Kali.

ip a: Visualizza gli indirizzi IP e lo stato di tutte le interfacce di rete.  

ss -tulnp: Mostra i socket (porte) TCP e UDP in ascolto e i relativi processi.  

msfconsole: Avvia l'interfaccia a riga di comando di Metasploit Framework per l'exploitation.  

searchsploit <software>: Interroga offline il database Exploit-DB alla ricerca di exploit noti.  

airmon-ng: Gestisce le interfacce Wi-Fi per abilitare la modalità monitor durante i test wireless.  

proxychains <comando>: Esegue un comando attraverso una catena di proxy per anonimizzare il traffico.  

4. Utilizzo di Nmap
Nmap (Network Mapper) è lo standard per la scansione delle porte e la scoperta di servizi.  

Scansioni Principali
nmap -sn <rete/24>: Ping Scan: scopre quali host sono attivi senza scansionare le singole porte.  

nmap -sS <IP>: SYN Scan: tecnica "stealth" veloce che non completa la connessione TCP.  

nmap -sV <IP>: Version Detection: interroga le porte aperte per determinare la versione del servizio.  

nmap -O <IP>: OS Detection: tenta di identificare il sistema operativo dell'host remoto.  

nmap -A <IP>: Aggressive Scan: combina rilevamento versione, OS, script scanning e traceroute.  

nmap -p- <IP>: Scansiona tutte le 65.535 porte possibili invece delle 1000 più comuni.  

5. Utilizzo NSE (Nmap Scripting Engine)
L'NSE permette di estendere Nmap per automatizzare compiti come la ricerca di vulnerabilità o l'auditing.

nmap --script default <IP>: Esegue gli script di base (sicuri e veloci) per raccogliere informazioni generali.  

nmap --script vuln <IP>: Controlla se il target è affetto da vulnerabilità note incluse nel database di Nmap.  

nmap --script auth <IP>: Testa le credenziali di default o tenta di aggirare l'autenticazione su vari servizi.  

nmap --script brute <IP>: Tenta attacchi di forza bruta (brute force) per indovinare le credenziali di servizi come SSH o FTP.  

nmap --script http-enum <IP>: Enumera directory e file comuni su server web per trovare aree sensibili.  

## Utilizzo Avanzato di Nmap
Nmap è lo strumento principe per lo scanning. Ecco come si combinano i parametri:

Scansione Stealth: nmap -sS <IP> (invia pacchetti SYN senza completare la connessione).  

Rilevamento Versioni e OS: nmap -sV -O <IP> (scopre quali servizi girano e quale sistema operativo è installato).  

Scansione Completa: nmap -p- -A <IP> (scansiona tutte le 65.535 porte con rilevamento aggressivo).

6. Comandi di Diagnostica e Ricognizione
whois <dominio>: Ottiene informazioni sulla registrazione del dominio e sul proprietario.  

dig <dominio>: Strumento avanzato per l'analisi dei record DNS.  

whatweb <URL>: Identifica le tecnologie utilizzate da un sito web (CMS, server, librerie).  

curl -I <URL>: Visualizza solo gli header HTTP di risposta di un server.</IP/host>
