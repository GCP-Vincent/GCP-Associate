
---

| **Scenario**                 | **Soluzione**                                           |
| -------------------------------- | ------------------------------------------------------------- |
|  Quali sono i pre-requisiti per creare una VM instance?       | **1. Project 2.Billing Account 3.Compute Engines API**                  |
| Vuoi avere hardware dedicato  | Sole-tenant nodes |
| Ci sono 1000 OS di VMs e voglio automatizzare la gestione delle patches, della configurazione e inventory. Gestione Software              | **VM Manager** |
| Voglio loggarmi alla VM per installare software   | Connect tramite SSH |
| Non vuoi esporre su internet la VM  | **Non assegnare un external IP address** |
| Voglio consentire il traffico HTTP/S sulla VM   | Nella creazione della VM, o configurando le regole del Firewall  |
