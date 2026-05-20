## Impostare un ambiente di lavoro sicuro come alboratorio
Scaricare un contenitore virtuale come oracle virtual box o vmware per il giusto sistema operativo e le iso di interesse

- link per oracle virtual box windows https://download.virtualbox.org/virtualbox/7.2.8/VirtualBox-7.2.8-173730-Win.exe
- link per macOS https://download.virtualbox.org/virtualbox/7.2.8/VirtualBox-7.2.8-173730-macOSArm64.dmg

una volta effettuato il download e aver proceduto all'installazione si può procede con scaricare il sistema operativo di interesse o la macchina virtuale che vogliamo utilizzare

- link per scaricare kali linux in formato .vdkm per avere una macchina https://www.kali.org/get-kali/#kali-virtual-machines
    -  nome "a scelta" sistema **linux** distribuzione **debian**  versione **debian-64bit**
- link per scaricare metaeploitable come macchina virtuale vulnerabile https://sourceforge.net/projects/metasploitable/files/latest/download
    - nome "a scelta" sistema **linux** distribuzione **ubuntu** versione **ubuntu-64bit**
    - mentre la virtual box di kali linux comprende già un file in formato vdkm autoinstallabile la piattaforma metaesploitable deve essere importata nel pannello di controllo al momento della creazione di una nuova virtual machine andando in fondo e inserendo direttamenteil disco

## le impostazioni principale delle macchine virtuali 
arrivati alla scheda di rete dobbiamo impostare per un ambiente sicuro la rete di kali linux su rete interna per creare un ambiente contenitore locale all'interno della virtual box e attivare la modalita promiscua per utilizzare a pieno tutti i comandi nmap e la scheda di rete di metaesploitable sempre su rete interna per colelgarsi alla stessa rete vlan interna creata dalla virtual box stessa

