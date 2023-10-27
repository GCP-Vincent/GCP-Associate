# Google Cloud Associate

Questo corso entra più in dettaglio, se qualcosa dovesse sembrare sconosciuta si faccia riferimento al corso entry level.

## Google Cloud Compute Engine
La parte Compute di GCP, riguarda il provisioning di potenza di calcolo. Nel settaggio della VM che si vuole creare è possibile identificare delle tipologie di macchine predefinite. Queste appartengono a diverse famiglie di macchine, ogni famigloa è adatta a workloads differenti.

In particolare troviamo queste famiglie:

- General Purpose (E2, N2, N2D, N1, ecc): Best price-performance 
            
    - sono indicate per ospitare web e application servers, piccoli-medi databases, ambienti di dev

- Memory Optimized (M1, M2, M3): Ultra high memory workloads
    - per large in-memory databases (si basano principalmente sulla memoria interna per l'archiviazione dei dati) e in-memory analytics 

- Compute Optimized (H3, C2, C2D)
    -  sono ideali per compute-intensive and high performance computing (HPC) workloads

- Accelerator Optimized (A2, G2)
    - per offrire prestazioni ed efficienza necessarie  per i carichi di lavoro con accelerazione GPU, come Artificial intelligence (AI), machine learning (ML), and high performance computing (HPC).

Per ogni famiglia di macchine sono disponibili diverse tipologie appunto, con caratteristiche differenti

![Alt text](<images/E2 type.png>)
*Nell'immagine un esempio per la tipologia E2 standard*


[Fare riferimento sempre alla tabella ufficiale, per la visione completa delle diverse famiglie ed eventuali cambiamenti ](https://cloud.google.com/compute/docs/machine-resource)

Per quanto riguarda le immagini da usare per il sistema operativo da installare, abbiamo:
- Public Images: fornite e manutenute da Google, oppure Open Source
- Custom Images: create personalmente per i propri progetti

## Custom Machine Types

Quando vogliamo utilizzare delle macchine diverse dalle tipologie predefinite, modificando la quantità di vCPU, memoria e GPUs.
Si parte dalle tipologie E2, N2, o N1. 

## GPUs

E' possibile aggiungere GPUs alle nostre macchine (solo alcune tipologie come N1), per quei workloads che richiedono calcoli matematici intensi o grafica, (es.AI/ML)

 - Chiaramente i costi aumentano
 - Occorre utilizzare GPU libraries sulle VMs altrimenti queste GPU non vengono usate
 - Non sono supportate per [live migration](#live-migration--availability-policy), quindi campo host maintenance settato su terminate. E' raccomandato però settare Automatic Restart=on
 - Posso utilizzare istanze munite di GPUs, o aggiungendola (tipo su N1), o utilizzando la famiglia Accelerator Optimized

## Indirizzi IP sulle VMs
Per quanto riguarda gli indirizzi IP assegnabili alla macchina, abbiamo detto che, l'External IP, (quello pubblico), è effimero. Per averlo sempre uguale occorre crearne uno statico, **Static external IP Address** e collegarlo alla macchina. Per quanto riguarda quello Internal invece (private), tutte le VM ne hanno associato almeno uno e non cambia. (Questi sono usati per far comunicare le istanze sulla stessa rete VPC, Virtual Private Cloud)

**Caratteristiche Static external IP Address**

- Static external IP può essere assegnato ad un'altra VM nello stesso progetto (togliendolo alla VM a cui era stato assegnato)
- Rimane collegato anche se cambio lo stato della VM
- **Pago per l'indirizzo anche quando non lo uso**, quindi meglio rilasciarlo se non lo si usa 

Per definire un indirizzo external statico: [Static *external* IP Address](https://cloud.google.com/compute/docs/ip-addresses/reserve-static-external-ip-address#reserve_new_static)

E' possibile anche riservare degli indirizzi IP internal statici:
[Static *internal* IP Address](https://cloud.google.com/compute/docs/ip-addresses/reserve-static-internal-ip-address)


## Billing per Google Compute Engine

Per quanto riguarda il costo delle risorse su Compute Engine, è bene ricordare che;
-**Si paga a secondo** (dopo minimo 1 minuto)

- **Non si paga quando una istanza è ferma**, ma si paga in questo caso invece lo storage connesso ad essa
- La raccomandazione è quella di **definire un Budget alerts**, nella sezione Billing. In questo modo saremo avvisati sui costi.

- E' sempre bene ricordare che **esistono delle scontistiche** sugli usi sostenuti applicate in automatico, e tipologie di VM committed use, preemptible (o spot), che consentono di risparmiare

## Live Migration & Availability Policy;

Per mantenere le istanze running quando ci sono degli aggiornamenti (lato Compute Engine)
 - Le istanze vengono migrate su di un altro host nella stessa Zone
 - Non vengono cambiati gli attributi o le proprietà della VM
 - Live Migration è supportata anche sulle istanze che hanno Local SSDs
 - NON SUPPORTATE preemptible instances, e istanze dove è stata aggiunta GPU

 Per abilitare questa funzionalità è necessario intervenire nella parte **Availability Policy**, che si può trovare nel form di creazione di una VM

 In particolare devo intervenire sulle voci:
 - **On host maintenance**: per manutenzione periodica dell'infrastruttura 
    - **Migrate** (default): Per migrare l'istanza su altro hardware 
    - **Terminate**: Stop l'istanza 
- **Automatic Restart**: (di default abilitata) per far ripartire l'istanza se termina a causa di ragioni non connesse all'utente (eventi di manutenzione, fallimenti hardware)

A default la live migration è quindi abilitata. Ma è sempre bene controllare la configurazione della macchina

# Piccolo reminder sulle VMs

- Sono associate ad un project, posso avere diversi projects
- La tipologia disponibile, varia da Region a Region
- E' possibile cambiare il tipo di macchina (editare il numero di vCPUs e memoria) solo a macchina ferma (Stop)
- E' possibile filtrare la ricerca nella lista delle VMs, per Name, Zone, Machine Types, Labels ecc
- Le instanze sono Zonal (sono running in una specifica zone, di una specifica Region)
    - Images sono Global (possono essere usate da progetti diversi)
    - Instance templates sono Global (*attenzione però: se si specificano risorse in una certa Zona o Region, allora il template sarà ristretto a quello*). 
    
    **Importante
    Per esempio se includi un read-only persistent disk, ad esempio da us-central1-b, nel tuo instance template, non puoi usare quel template in un'altra zona, perchè quel disco si trova in quella Zone specifica**

    - E' abilitato in automatico un monitoraggio di base della macchina (uso CPU e poco altro). Per avere una visione completa fare riferimento a Cloud Monitoring