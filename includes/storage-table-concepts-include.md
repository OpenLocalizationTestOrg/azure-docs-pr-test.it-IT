## <a name="what-is-table-storage"></a>Informazioni sull'Archiviazione tabelle
Il servizio Archiviazione tabelle di Azure consente di archiviare grandi quantità di dati strutturati. servizio Hello è autenticato di un archivio dati NoSQL che accetta chiamate dall'interno e all'esterno di hello cloud di Azure. Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali. Di seguito sono riportati gli usi più comuni per il servizio Archiviazione tabelle:

* Archiviazione di terabyte di dati strutturati in grado di servire applicazioni su scala Web
* Archiviazione di set di dati che non richiedono join complessi, chiavi esterne o stored procedure e che possono essere denormalizzati per l'accesso rapido
* Esecuzione rapida di query sui dati mediante un indice cluster
* L'accesso ai dati utilizzando il protocollo di OData hello e le query LINQ con le librerie .NET di servizio dati WCF

È possibile utilizzare una tabella archiviazione toostore e query enorme set di dati strutturati non relazionali e le tabelle verranno ridimensionate man mano che aumenta di richiesta.

## <a name="table-storage-concepts"></a>Concetti relativi all'Archiviazione tabelle
Archiviazione tabelle contiene hello seguenti componenti:

![Diagramma dei componenti di Archiviazione tabelle][Table1]

* **Formato dell'URL**: il codice fa riferimento alle tabelle in un account usando il formato di indirizzo seguente:   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  È possibile indirizzare le tabelle di Azure direttamente con questo indirizzo hello protocollo OData. Per altre informazioni, vedere [OData.org][OData.org].
* **Account di archiviazione:** tutti gli accessi tooAzure archiviazione viene eseguita tramite un account di archiviazione. Per informazioni sulla capacità dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../articles/storage/common/storage-scalability-targets.md) .
* **Tabella**: una tabella è una raccolta di entità. Le tabelle non impongono uno schema sulle entità, pertanto una singola tabella può contenere entità che presentano set di proprietà diversi. numero di Hello di tabelle contenenti un account di archiviazione è limitato solo dal limite della capacità dell'account di archiviazione hello.
* **Entità**: un'entità è un set di proprietà, la riga del database tooa simile. Un'entità può essere backup too1MB nella dimensione.
* **Proprietà**: una proprietà è una coppia nome-valore. Ogni entità possono includere i dati di toostore too252 proprietà. Ogni entità dispone inoltre di tre proprietà di sistema che specificano una chiave di partizione, una chiave di riga e un timestamp. Entità con hello stessa chiave di partizione può essere eseguita una query più velocemente e inseriti/aggiornati in operazioni atomiche. La chiave di riga di un'entità ne rappresenta l'identificatore univoco all'interno di una partizione.

Per ulteriori informazioni sulla denominazione di tabelle e le proprietà, vedere [hello comprensione modello di dati del servizio tabelle](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model).

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
