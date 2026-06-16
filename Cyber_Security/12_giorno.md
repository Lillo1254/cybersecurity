# Gestione Rapporto Costi/Benefici nella sicurezza
La sicurezza – informatica o fisica – non è solo “spesa”, ma un modo per trasformare il rischio in numeri e prendere decisioni intelligenti L’obiettivo è capire quanto costa proteggere e quanto costa NON proteggere

## Identificazione e Classificazione degli Asset
Prima di parlare di costi, devi sapere cosa stai proteggendo.

Tipi di asset:
- Asset fisici: server, PC, dispositivi mobili.
- Asset software: licenze, applicazioni, servizi cloud.
- Asset informativi: database, dati clienti, proprietà intellettuale.
- Asset umani: competenze, ruoli critici.

**Domanda chiave “Se questo asset si rompe o viene rubato, quanto ci costa in 24 ore?”**

## Analisi Quantitativa del Rischio

Indicatori fondamentali
- SLE (Single Loss Expectancy)  
    - Quanto perdi per un singolo incidente.
    - “Se accade questo incidente oggi, quanto ci costa esattamente?”

Formula: SLE = AV × EF  
Dove:

AV = valore dell’asset

EF = percentuale di danno (0–1)

- ARO (Annualized Rate of Occurrence)  
    - Quante volte l’evento può accadere in un anno.
      - utilizzo dati storici per verifica probabilità
      - threat intelligence
      - vulnerabilità note

ALE (Annualized Loss Expectancy)  
- La perdita annua prevista.
  - serve per giustificare investimenti
  - decidere priorità
  - scegliere tra mitigare, trasferire accettare o evitare il rischio
  
Formula: ALE = SLE × ARO

## Valutazione delle Misure di Sicurezza
Una contromisura non costa solo il prezzo di acquisto Include licenze, manutenzione, formazione, energia, spazio, dismissione 
- TCO (Total Cost of Ownership) Il TCO è la somma di costi diretti e indiretti lungo tutto il ciclo di vita
- Impatto operativo Una misura troppo rigida può rallentare il lavoro e creare “attrito” Una misura di sicurezza è efficace solo se non blocca il lavoro.

## Calcolo del ROSI (Return on Security Investment)
Il ROSI misura quanto rischio eviti grazie alla sicurezza sostanzialmente quanti soldi **non escono** a causa di un incidente

ROSI > 0 conviene fare l'investimento

ROSI < 0 la spesa per la sicurezza supera quella del rischi di incidente

## Asset Management
L’Asset Management serve a sapere cosa possiedi, dove si trova, quanto vale e come proteggerlo.

1. Identificazione degli asset
- Non solo hardware: anche software, dati, ruoli critici.

2. Modello operativo
- Manuale (Excel) → economico ma impreciso
- Automatizzato (CMDB/ITAM) → preciso e scalabile

3. Ciclo di vita dell’asset
- Acquisto (CapEx o OpEx?)
  - CapEx Spesa iniziale grande → acquisti hardware o licenze perpetue. Si ammortizza negli anni.
  - OpEX Spesa ricorrente → abbonamenti, cloud, servizi gestiti.Più flessibile e scalabile
- Configurazione sicura
- Manutenzione e patch
- Dismissione sicura (wipe certificato, distruzione, riciclo)
- utilizzo KPI
    - KPI di utilizzo — misurano quanto un asset viene usato
    - KPI di sicurezza — misurano incidenti, vulnerabilità, patching
    - KPI di rischio — misurano esposizione e rischio residuo
    - KPI di compliance — misurano aderenza a policy e norme
    - KPI operativi — misurano tempi, efficienza, processi

1. Ownership
- Asset Owner → responsabile del valore è la figura che decide, approva, valuta il rischio e stabilisce le priorità.
- Asset Custodian → responsabile tecnico È la figura operativa che implementa, configura, monitora, aggiorna

## Risk Appetite (Propensione al Rischio)
È il livello di rischio che l’azienda è disposta ad accettare e prendere contromisure se l'ALE quindi l'aspettativa di rischio annuo è superiore al risk Appetite

Esempio:

“Se l’ALE è 120.000€ ma il Risk Appetite è 50.000€, bisogna investire per ridurre il rischio.”

## Shadow IT
La Shadow IT nasce quando i dipendenti usano strumenti non autorizzati perché l'IT è lento o gli strumenti ufficiali sono scomodi oppure il cloud è facile da attivare o anche manca consapevolezza dei rischi ... caricare un file excel su un convertitore online sta fornendo quei dati del file al servizio di terze parti

## ROSI vs ROI
il ROI misura il guadagno generato da un investimento mentre il ROSI misura la perdita evitata

ROI => (guadagno netto - costo investimento) / costo investimento
MITIGAZIONE => (ALE(senza controllo) - ALE(con controllo)) / ALE(senza controllo)
ROSI => ((ALE x %mitigazione) - TCO) / TCO = perdite evitate 

## RIEPILOGO FORMULE
1) SLE – Single Loss Expectancy => 

**SLE = AV x EF**

2) ARO – Annualized Rate of Occurrence => 

**ARO = frequenza annuale stimata** 

3) ALE – Annualized Loss Expectancy => 

**ALE = SLE x ARO**

4) %Mitigazione => 

**%mitigazione = (ALE(senza controllo) - ALE(con controllo)) / ALE(senza controllo)**

5) TCO – Total Cost of Ownership

**TCO = costi diretti e indiretti**

6) ROI – Return on Investment
**ROI = (guadagno netto - costo investimento) / costo investimento**

7) ROSI – Return on Security Investment
**((ALE x %mitigazione) - TCO) / TCO**