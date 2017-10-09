Factory di dati è un servizio multi-tenant che ha hello seguendo i limiti predefiniti in toomake sul posto che le sottoscrizioni dei clienti sono protetti dalla funzionalità degli altri carichi di lavoro. Molti dei limiti di hello può essere facilmente generati per la sottoscrizione corrente backup toohello limite contattando il supporto tecnico.

| **Risorsa** | **Limite predefinito** | **Limite massimo** |
| --- | --- | --- |
| data factory in una sottoscrizione di Azure |50 |[Contattare il supporto tecnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| pipeline all'interno di una factory di dati |2500 |[Contattare il supporto tecnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| set di dati all'interno di una factory di dati |5000 |[Contattare il supporto tecnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| sezioni simultanee per ogni set di dati |10 |10 |
| byte per oggetto per gli oggetti pipeline<sup>1</sup> |200 KB |200 KB |
| byte per oggetto per oggetti set di dati e servizio collegato<sup>1</sup> |100 KB |2000 KB |
| Memorie centrali del cluster HDInsight su richiesta con una sottoscrizione<sup>2</sup> |60 |[Contattare il supporto tecnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Unità di spostamento dati cloud <sup>3</sup> |32 |[Contattare il supporto tecnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Numero di tentativi delle esecuzioni di attività pipeline |1000 |MaxInt (32 bit) |

<sup>1</sup>pipeline, set di dati e oggetti servizio collegato rappresentano un raggruppamento logico del carico di lavoro. I limiti per questi oggetti non riguardano le tooamount dei dati, è possibile spostare ed elaborare con il servizio di Azure Data Factory hello. Factory di dati è progettato tooscale toohandle petabyte di dati.

<sup>2</sup> HDInsight su richiesta core allocati fuori sottoscrizione hello che contiene una data factory di hello. Di conseguenza, hello supera il limite è hello Data Factory è applicato il limite di core per core di HDInsight su richiesta ed è diverso dal limite di core hello associati alla sottoscrizione di Azure.

<sup>3</sup> L'unità di spostamento dati cloud viene usata in un'operazione di copia da cloud a cloud. È una misura che rappresenta la potenza hello (una combinazione di CPU, memoria e di allocazione delle risorse di rete) di una singola unità nella Data Factory. È possibile ottenere una velocità effettiva di copia maggiore sfruttando un numero maggiore di unità di spostamento dati per alcuni scenari. Fare riferimento troppo[unità lo spostamento dei dati Cloud](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) sezione sui dettagli.

| **Risorsa** | **Limite inferiore predefinito** | **Limite minimo** |
| --- | --- | --- |
| Intervallo di pianificazione |15 minuti |15 minuti |
| Intervallo tra tentativi |1 secondo |1 secondo |
| Valore di timeout del tentativo |1 secondo |1 secondo |

### <a name="web-service-call-limits"></a>Limiti di chiamata del servizio Web
Azure Resource Manager presenta limiti per le chiamate API. È possibile effettuare chiamate di API con una frequenza all'interno di hello [API di gestione risorse di Azure limita](../articles/azure-subscription-service-limits.md#resource-group-limits).
