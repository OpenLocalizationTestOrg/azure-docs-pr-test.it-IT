## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurare l'archiviazione di Azure di tooaccess applicazione
Esistono due modi tooauthenticate il tooaccess applicazione Servizi di archiviazione:

* Chiave condivisa: usare la Chiave condivisa solo a scopo di test
* Firma di accesso condiviso: usare la firma di accesso condiviso per le applicazioni per la produzione

### <a name="shared-key"></a>Chiave condivisa
L'autenticazione chiave condivisa significa che l'applicazione verrà utilizzare il nome dell'account e tooaccess chiave dell'account servizi di archiviazione. Ai fini di hello di rapidamente che mostra come toouse questa libreria, verrà usato l'autenticazione chiave condivisa in questa Guida introduttiva.

> [!WARNING] 
> **Per scopi di test, usare solo l'autenticazione con chiave condivisa.** Il nome account e la chiave dell'account, che consentono di toohello di accesso in lettura/scrittura account di archiviazione associato, sarà persona tooevery distribuita che consente di scaricare l'app. Questa procedura **non** è consigliabile perché si rischia che la chiave venga compromessa da client non attendibili.
> 
> 

Quando si usa l'autenticazione con la chiave condivisa, si creerà una [stringa di connessione](../articles/storage/common/storage-configure-connection-string.md). stringa di connessione Hello è costituita da:  

* Hello **DefaultEndpointsProtocol** -è possibile scegliere HTTP o HTTPS. Tuttavia, è vivamente consigliato l'uso di HTTPS.
* Hello **nome Account** : hello nome dell'account di archiviazione
* Hello **chiave dell'Account** - in hello [portale Azure](https://portal.azure.com)passare tooyour account di archiviazione e fare clic su hello **chiavi** toofind icona queste informazioni.
* (Facoltativo) **EndpointSuffix** : usata per i servizi di archiviazione in aree con suffissi dell'endpoint diversi, ad esempio per Azure China o Azure Governance.

Ecco un esempio di stringa di connessione che usa l'autenticazione con la chiave condivisa:

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>Firme di accesso condiviso
Per un'applicazione per dispositivi mobili, hello consigliato metodo per l'autenticazione di una richiesta da un client a fronte del servizio di archiviazione di Azure hello è tramite una firma di accesso condiviso (SAS). Firma di accesso condiviso consente toogrant una risorsa tooa di accesso client per un periodo di tempo, specificato con un set specificato di autorizzazioni.
Come proprietario dell'account di archiviazione hello, sarà necessario toogenerate una firma di accesso condiviso per il tooconsume client mobili. toogenerate hello firma di accesso condiviso, è opportuno toowrite un servizio separato che genera l'errore hello SAS toobe distributed tooyour client. A scopo di test, è possibile utilizzare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) o hello [portale Azure](https://portal.azure.com) toogenerate una firma di accesso condiviso. Quando si crea hello SAS, è possibile specificare l'intervallo di tempo hello in cui hello firma di accesso condiviso è valida e autorizzazioni di hello hello client toohello di firma di accesso condiviso concede il.

Hello di esempio seguente viene illustrato come toouse hello Microsoft Azure Storage Explorer toogenerate una firma di accesso condiviso.

1. Se hai già fatto, [hello installa Microsoft Azure Storage Explorer](http://storageexplorer.com)
2. Connettersi tooyour sottoscrizione.
3. Fare clic su account di archiviazione e fare clic sulla scheda azioni"hello" nella parte inferiore di hello a sinistra. Fare clic su "Ottenere firma di accesso condiviso" toogenerate "stringa di connessione" per la firma di accesso condiviso.
4. Di seguito è riportato un esempio di una stringa di connessione della firma di accesso condiviso che concede autorizzazioni lettura e scrittura a livello di oggetto per il servizio blob hello hello dell'account di archiviazione, contenitore e il servizio di hello.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

Come si può osservare, quando si usa una firma di accesso condiviso, non si espone la chiave dell'account nell'applicazione. È possibile approfondire SAS e procedure consigliate per l'utilizzo di SAS consultando [firme di accesso condiviso: modello di firma di accesso condiviso hello comprensione](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md).

