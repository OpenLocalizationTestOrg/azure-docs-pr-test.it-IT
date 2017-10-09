Archiviazione è vincolata da spazio su disco o da un limite rigido per hello *massimo* di indici o documenti, verifica per primo.

| Risorsa | Free | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contratto di servizio (SLA) |No <sup>1</sup> |Sì |Sì |Sì |Sì |Sì |
| Archiviazione per partizione |50 MB |2 GB |25 GB |100 GB |200 GB |200 GB |
| Partizioni per servizio |N/D |1 |12 |12 |12 |3 <sup>2</sup> |
| Dimensioni della partizione |N/D |2 GB |25 GB |100 GB |200 GB |200 GB |
| Repliche |N/D |3 |12 |12 |12 |12 |
| Numero massimo di indici |3 |5 |50 |200 |200 |1000 per partizione o 3000 per servizio |
| Numero massimo di indicizzatori |3 |5 |50 |200 |200 |Nessun supporto per l'indicizzatore |
| Numero massimo di origini dati |3 |5 |50 |200 |200 |Nessun supporto per l'indicizzatore |
| Numero massimo di documenti |10.000 |1 milione |15 milioni per partizione o 180 milioni per servizio |60 milioni per partizione o 720 milioni per servizio |120 milioni per partizione o 1,4 miliardi per servizio |1 milione per indice o 200 milioni per partizione |
| Query al secondo stimate |N/D |~3 per replica |~15 per replica |~60 per replica |~60 per replica |>60 per replica |

<sup>1</sup> Con il Contratto di servizio non sono incluse funzionalità di anteprima e il livello gratuito. Per tutti i livelli fatturabili, i contratti di servizio diventano effettivi quando viene effettuato il provisioning di una ridondanza sufficiente per il servizio. Per il Contratto di servizio di query (lettura) sono necessarie due o più repliche. Per il contratto di servizio di query e indicizzazione (lettura-scrittura) sono necessarie tre o più repliche. numero di Hello di partizioni non è un fattore di contratto di servizio. 

<sup>2</sup> S3 HD ha un limite di 3 partizioni, che è inferiore al limite di partizione hello per S3. limite partizione Hello viene imposto perché il numero di indice hello per S3 HD è notevolmente superiore. Dato che esistono limitazioni di servizio per entrambe le risorse di elaborazione (elaborazione e archiviazione) e gli indici e documenti, hello contenuto limite del contenuto venga raggiunta per prima.
