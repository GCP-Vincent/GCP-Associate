## Elenco di comandi utili eseguiti

```bash

# per creare una vm a partire da un instance template
- gcloud compute instances create my-test-vm --source-instance-template=my-instance-template-with-custom-image

# listato mig
- gcloud compute instance-groups managed list

# eliminazione mig
- gcloud compute instance-groups managed delete my-managed-instance-group

# creazione mig con target size 1
- gcloud compute instance-groups managed create my-mig --zone us-central1-a --template my-instance-template-with-custom-image --size 1

# settaggio autoscaling di un mig
- gcloud compute instance-groups managed set-autoscaling my-mig --max-num-replicas=2 --zone us-central1-a

# autoscaling off
- gcloud compute instance-groups managed stop-autoscaling my-mig --zone us-central1-a

# modifica target size 
- gcloud compute instance-groups managed resize my-mig --size=1 --zone=us-central1-a

# recreate mig
- gcloud compute instance-groups managed recreate-instances my-mig --instances=my-mig-85fb --zone us-central1-a

# eliminazione mig
- gcloud compute instance-groups managed delete my-managed-instance-group --region=us-central1

```