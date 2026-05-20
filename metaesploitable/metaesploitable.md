# sfruttamento vulnerabilità
primo passo identificazione del nostro IP kali linux e verifica dell'interfaccia locale

- ip a 
    - troveremo il nostro IP kali linux da cui possiamo gia ottenere varie informazioni tra cui la base(subnet) della rete locale a cui siamo connessi per esempio se il nostro IP è 192.168.56.101/24 significa che la rete locale (subnet) è posizionata su un IP 192.168.56.0/24(bit) dove gli IP collegati variano da .0 a .255 

ora bisogna controllare gli indirizzi IP collegati a quella subnet specifica

per farlo possiamo utilizzare due comandi "sudo netdiscover -r [IP]" o "nmap -sn [IP]"

utilizziamo il comando 
- nmap -sn [IP.0/24]     (-sn è l'opzione che dice ad nmpa di effettuare il rilevamento degli host senza contorllare le porte -scan no port)
    - otteniamo una lista di IP con MAC address dei dispositivi connessi alla subnet citata in precedenza

poiche alcuni firewall potrebbero non rispondere alla ricezione di pacchetti TCP SYN si utilizza l'opzione "sudo" all'inizio del comando per eseguire quel comando come amministratore supremo e il risultato sarà l'invio di pacchetti ARP ignorando l'invio di pacchetti TCP ICMP per farlo possiamo  scrivere un comando ancora piu specifico

- sudo nmap -sn -PR [IP]
    - -sn blocca la scansione delle porte
    - -PR significa ARP ping per utilizzare solo ed esclusivamente pacchetti ARP

in questo modo tutti gli IP sono "obbligati a rispondere" e pertanto possiamo visualizzare anche dispositivi con firewall piu restrittivi

abbiamo scoperto che la metaesploitable vulnerabile ha IP 192.168.56.101 poiche sappiamo il nostro ip, ma per verificare che sia effettivamente quella la macchina virtuale possiamo effettuare una scansione delle porte aperte su quell'IP con il comando

- sudo nmap -sS -Pn -p- 192.168.56.101
    - -sS invia dei pacchetti TCP SYN anche chiamati half open poiche manda la richiesta di connessione ad una determinata porta se la porta è aperta il bersaglio accettera la connessione ma proprio in quel momento kali inviera un pacchetto RST (reset) per chiudere bruscamente la connessione  in modo da capire che la porta è aperta senza completare la sessione intera questo per evitare che la connessione lasci "log" standard e aumentare la velocità di controllo
    - -Pn questa opzione dice a nmap di non fare il ping visto che gia sappiamo che l'host è attivo quindi passa direttamente al controllo delle porte
    - -p- questa parte del comando serve a dire a nmap di effettuare la scansione su tutte le 65535 porte poiche di base nmap scansiona solo le 1000 porte standard

# RISULTATO DELLA SCANSIONE

    ──(kali㉿kali)-[~]
└─$ sudo nmap -sS -Pn -p- 192.168.56.101
[sudo] password for kali: 
Starting Nmap 7.98 ( https://nmap.org ) at 2026-05-20 15:21 -0400
Stats: 0:00:06 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 82.28% done; ETC: 15:21 (0:00:01 remaining)
Nmap scan report for 192.168.56.101
Host is up (0.00017s latency).
Not shown: 65505 closed tcp ports (reset)
PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
23/tcp    open  telnet
25/tcp    open  smtp
53/tcp    open  domain
80/tcp    open  http
111/tcp   open  rpcbind
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
512/tcp   open  exec
513/tcp   open  login
514/tcp   open  shell
1099/tcp  open  rmiregistry
1524/tcp  open  ingreslock
2049/tcp  open  nfs
2121/tcp  open  ccproxy-ftp
3306/tcp  open  mysql
3632/tcp  open  distccd
5432/tcp  open  postgresql
5900/tcp  open  vnc
6000/tcp  open  X11
6667/tcp  open  irc
6697/tcp  open  ircs-u
8009/tcp  open  ajp13
8180/tcp  open  unknown
8787/tcp  open  msgsrvr
33385/tcp open  unknown
33460/tcp open  unknown
38108/tcp open  unknown
57665/tcp open  unknown
MAC Address: 08:00:27:62:23:8A (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 8.55 seconds


ora abbiamo ottenuto lo scan di tutte le porte che risultano aperte sulla nostra macchina bersaglio nei prossimi file saranno elencate le vulnerabilità 

