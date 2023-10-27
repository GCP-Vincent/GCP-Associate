Esaminiamo la CLI per interagire con le risorse di Google Cloud Platform: **Gcloud**

Molti dei servizi di GCP possono essere gestiti da CLI

- E' possibile creare/eliminare/aggiornare/leggere risorse ed eseguire azioni su di esse

N.B 
Alcuni servizi GCP hanno specifici strumenti (che ritrovo in Gcloud)
- Cloud Storage -> gsutil
- Cloud BigQuery -> bq
- Cloud BigTable -> cbt
- Kubernetes -> kubectl (per gestire il cluster)
## Installation
Non necessaria perchè accessibile dalla piattaforma

Gcloud è parte di Google Cloud SDK
    
- Cloud SDK richiede Python
- [Istruzioni per installare Cloud SDK (e Gcloud)](https://cloud.google.com/sdk/docs/install). 

N.B non è necessario farlo perchè

Puoi utilizzare Gcloud su Cloud Shell (la CLI di Google Cloud Platform)

In alto a destra vi è l'icona di Cloud Shell

```bash
# Per inizializzare o reinizializzare gcloud
gcloud init
# permette di autorizzare gcloud ad usare le credenziali dell'utente
# setup della configurazione: (si può lasciare quella presente, al massimo settare il progetto se questo deve essere un altro) current project, default zone ecc

#per avere la versione e gli strumenti installati come kubectl,bq,gsutil ecc
gcloud --version 

#per avere una lista di tutte le proprietà e le configurazioni attive
gcloud config list 
```

[Comandi utili su Gcloud](Sezione_2bis.md)




