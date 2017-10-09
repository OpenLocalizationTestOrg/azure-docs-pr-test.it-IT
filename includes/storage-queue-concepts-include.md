## <a name="what-is-queue-storage"></a>Informazioni sull'archiviazione di accodamento
Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS. Può essere un messaggio nella coda singola too64 KB di dimensioni e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione.

Di seguito sono riportati gli utilizzi più comuni per il servizio di archiviazione di accodamento.

* Creazione di un backlog di lavoro tooprocess in modo asincrono
* Passaggio di messaggi da un ruolo di lavoro di Azure tooan ruolo web di Azure

## <a name="queue-service-concepts"></a>Concetti del servizio di accodamento
servizio di Accodamento Hello contiene hello seguenti componenti:

![Queue1](./media/storage-queue-concepts-include/queue1.png)

* **Formato URL:** le code sono indirizzabili mediante hello seguendo il formato di URL:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    una coda nel diagramma hello è concepito Hello URL seguente:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Account di archiviazione:** tutti gli accessi tooAzure archiviazione viene eseguita tramite un account di archiviazione. Per informazioni sulla capacità dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../articles/storage/common/storage-scalability-targets.md) .
* **Coda:** una coda contiene un set di messaggi. Tutti i messaggi devono essere inclusi in una coda. Il che nome della coda hello debba essere tutti in lettere minuscole. Per altre informazioni, vedere [Denominazione di code e metadati](https://msdn.microsoft.com/library/azure/dd179349.aspx).
* **Messaggio:** un messaggio, in qualsiasi formato, di too64 KB. tempo massimo di Hello che un messaggio può rimanere nella coda di hello è 7 giorni.

