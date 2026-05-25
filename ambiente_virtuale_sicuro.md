## Impostare un ambiente di lavoro sicuro come alboratorio
Scaricare un contenitore virtuale come oracle virtual box o vmware per il giusto sistema operativo e le iso di interesse

- link per oracle virtual box windows https://download.virtualbox.org/virtualbox/7.2.8/VirtualBox-7.2.8-173730-Win.exe
- link per macOS https://download.virtualbox.org/virtualbox/7.2.8/VirtualBox-7.2.8-173730-macOSArm64.dmg

una volta effettuato il download e aver proceduto all'installazione si può procede con scaricare il sistema operativo di interesse o la macchina virtuale che vogliamo utilizzare

- link per scaricare kali linux in formato .vdkm per avere una macchina https://www.kali.org/get-kali/#kali-virtual-machines
    -  nome "a scelta" sistema **linux** distribuzione **debian**  versione **debian-64bit**
    -  all'apertura della macchina virtuale verranno richiesti i dati di accesso
       -  nome utente "kali"
       -  password "kali"
- link per scaricare metaeploitable come macchina virtuale vulnerabile https://sourceforge.net/projects/metasploitable/files/latest/download
    - nome "a scelta" sistema **linux** distribuzione **ubuntu** versione **ubuntu-64bit**
    - mentre la virtual box di kali linux comprende già un file in formato vdkm autoinstallabile la piattaforma metaesploitable deve essere importata nel pannello di controllo al momento della creazione di una nuova virtual machine andando in fondo e inserendo direttamenteil disco
    - all'apertura della macchina virtuale il terminale mostrerà la fase di login
      - nome utente "msfadmin"
      - password "msfadmin" (in questo terminale la password è nascosta mentre viene digitata)

## le impostazioni principale delle macchine virtuali 
arrivati alla scheda di rete dobbiamo impostare per un ambiente sicuro la rete di kali linux su **rete interna** per creare un ambiente contenitore locale all'interno della virtual box e attivare la modalita promiscua per utilizzare a pieno tutti i comandi nmap e la scheda di rete di metaesploitable sempre su **rete interna** per colelgarsi alla stessa rete vlan interna creata dalla virtual box stessa il nome della rete interna sulle macchine che vogliamo che comunichino tra loro deve essere uguale identico per entrambe

# connettività di rete
all'interno della nostra virtual box possiamo specificare per ogni macchina virtuale delle specifiche ben distinte per processori hardware GPU e scheda di reta.

## se vogliamo utilizzare internet...
Per poter utilizzare internet all'interno della nostra macchina virtuale (kali linux) dobbiamo impostare la scheda di rete 1 su "scheda con bridge" oppure su "NAT" utilizzando di fatto una connessione con ponte che parte dal router passa per la VPN di virtual box e successivamente arriva sulla nostra macchina virtuale con un indirizzo ip senza mascheramento del router ma utilizzando il mascheramento della virtual box.

utiliziamo invece la scheda con NAT se la rete a cui siamo collegati richiede specificatamente che gli ip delle connessioni sia mascherate con il NAT principale per una questione di sicurezza così facendo avremo l'ip mascherato dal router principale

entrambe queste tipologie di connessione portano all'utilizzo della rete principale per poter navigare in internet 

possiamo ora impostare le schede di rete per non aver accesso ad internet ma vedere comunque le altre macchine virtuali collegate alla stessa virtual box impostando la scheda di rete su "scheda solo host" oppure per mantenere l'accesso ad internet e poter utilizzare il collegamento con le altre virtual machine dobbiamo impostare la "scheda 1" su bgidge o NAT e la "scheda 2" su "solo host" e la scheda di rete della macchina vulnerabile anch'essa su "solo host" sulla scheda 1

per utilizzare determinati programmi all'interno di kali linux è necessario impostare sulla scheda di rete la modalità prmiscua su "permetti tutto"