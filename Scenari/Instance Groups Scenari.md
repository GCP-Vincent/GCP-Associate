
---

| **Scenario**                 | **Soluzione**                                           |
| -------------------------------- | ------------------------------------------------------------- |
|  Vuoi un applicazione su di un MIG che possa sopravvivere a Zone failures    | **Regional MIG, anche chiamato multiple zone MIG**                  |
| Vuoi creare VMs di diverse configurazioni nello stesso gruppo  | Un-managed Instance Group |
| Vuoi preservare lo stato delle VMs in un MIG              | **Stateful MIG** |
| Vuoi avere alta disponibilità in un MIG anche quando ci sono aggiornamenti hw o software   | Bisogna usare Instance Template che abbiano availability policy di automatic restart: enabled e on-host maintenance: migrate. Quindi automatic restarts e live migration attive |
| Vuoi che le istanze unhealthy siano automaticamente rimpiazzate  | **Configurare health check sul MIG (self healing)** |
| Evitare frequenti scale up & downs   | Configurare al meglio cool-down period (tempo per ricontrollo metriche) e initial delay (tempo prima di controllare healthy check)|
