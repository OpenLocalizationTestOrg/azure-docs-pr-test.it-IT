---
title: strumento di migrazione aaaDatabase per Azure Cosmos DB | Documenti Microsoft
description: Informazioni su come toouse hello aprire origine Azure Cosmos DB dati migrazione strumenti tooimport dati tooAzure DB Cosmos da varie origini, inclusi i file di MongoDB, di SQL Server, archiviazione tabella, DynamoDB Amazon, CSV e JSON. Conversione di tooJSON CSV.
keywords: CSV toojson, strumenti di migrazione di database, convertire toojson csv
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>Come dati tooimport in Azure Cosmos DB per hello API DocumentDB?

In questa esercitazione vengono fornite istruzioni sull'utilizzo di hello Azure Cosmos DB: strumento di migrazione dei dati API DocumentDB, che è possibile importare dati da origini diverse, inclusi i file JSON, i file CSV, SQL, MongoDB, archiviazione tabelle di Azure, Amazon DynamoDB e Azure Cosmos DB DocumentDB Raccolte di API in raccolte per usare con Azure Cosmos DB e hello API DocumentDB. strumento di migrazione dei dati Hello è utilizzabile anche durante la migrazione da una raccolta di più partizioni tooa raccolta singola partizione per hello API DocumentDB.

strumento di migrazione dei dati Hello funziona solo se l'importazione di dati in Azure Cosmos DB per utilizzano con l'API DocumentDB hello. Importazione di dati per l'utilizzo con hello tabella API o l'API Graph non è supportato in questo momento. 

tooimport dati per l'utilizzo con hello MongoDB API, vedere [DB Cosmos Azure: come dati toomigrate per hello API MongoDB?](mongodb-migrate.md).

Questa esercitazione sono trattati hello seguenti attività:

> [!div class="checklist"]
> * Installazione dello strumento di migrazione dei dati hello
> * Importazione di dati da diverse origini dati
> * Esportazione da Azure Cosmos DB tooJSON

## <a id="Prerequisites"></a>Prerequisiti
Prima di seguire le istruzioni di hello in questo articolo, assicurarsi di aver installato quanto segue hello:

* [Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) o versione successiva.

## <a id="Overviewl"></a>Panoramica dello strumento di migrazione dei dati hello
strumento di migrazione dei dati Hello è una soluzione open source che importa dati tooAzure Cosmos DB da un'ampia gamma di origini, tra cui:

* File JSON
* MongoDB
* SQL Server
* File CSV
* Archiviazione tabelle di Azure
* DynamoDB Amazon
* HBase
* Raccolte di Azure Cosmos DB

Mentre lo strumento di importazione hello include un'interfaccia utente grafica (dtui.exe), può essere controllato anche dalla riga di comando hello (dt.exe). È in realtà, un comando di hello associata toooutput opzione dopo aver impostato un'importazione tramite hello dell'interfaccia utente. I dati di origine tabulari (ad esempio, file CSV o SQL Server) possono essere trasformati in modo da poter creare relazioni gerarchiche (documenti secondari) durante l'importazione. Mantenere la lettura di toolearn ulteriori informazioni sulle opzioni di origine, tooimport righe di comando di esempio da ogni origine, le opzioni di destinazione e la visualizzazione, importare i risultati.

## <a id="Install"></a>Installare lo strumento di migrazione dei dati hello
codice sorgente dello strumento di migrazione Hello è disponibile su GitHub in [questo repository](https://github.com/azure/azure-documentdb-datamigrationtool) ed è disponibile una versione compilata [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d). È possibile compilare la soluzione hello o semplicemente il download ed estrarre hello versione compilata tooa directory desiderata. Eseguire quindi:

* **Dtui.exe**: versione con interfaccia grafica dello strumento hello
* **DT.exe**: la versione della riga di comando dello strumento hello

## <a name="import-data"></a>Importa dati

Dopo aver installato lo strumento di hello, è ora tooimport i dati. Il tipo di dati si desidera tooimport?

* [File JSON](#JSON)
* [MongoDB](#MongoDB)
* [File di esportazione MongoDB](#MongoDBExport)
* [SQL Server](#SQL)
* [File CSV](#CSV)
* [Archivio tabelle di Azure](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [BLOB](#BlobImport)
* [Raccolte di Azure Cosmos DB](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Importazione in blocco di Azure Cosmos DB](#DocumentDBBulkImport)
* [Importazione di record sequenziali di Azure Cosmos DB](#DocumentDSeqTarget)


## <a id="JSON"></a>file JSON tooimport
opzione dell'utilità di importazione dell'origine di file JSON Hello consente tooimport uno o più file JSON singolo documento o i file JSON, ciascuna delle quali contiene una matrice di documenti JSON. Quando si aggiungono cartelle che contengono tooimport file JSON, è possibile hello in modo ricorsivo la ricerca dei file nelle sottocartelle.

![Schermata delle opzioni dell'origine file JSON - Strumenti di migrazione del database](./media/import-data/jsonsource.png)

Ecco alcuni file JSON tooimport esempi della riga di comando:

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <a id="MongoDB"></a>tooimport da MongoDB

> [!IMPORTANT]
> Se si importano account Azure Cosmos DB tooan con supporto per MongoDB, attenersi alla seguente [istruzioni](mongodb-migrate.md).
> 
> 

opzione dell'utilità di importazione dell'origine di MongoDB Hello consente tooimport da un singolo insieme di MongoDB e, facoltativamente, filtrare i documenti utilizzando una query e/o modificare struttura del documento hello utilizzando una proiezione.  

![Screenshot delle opzioni relative all'origine per MongoDB](./media/import-data/mongodbsource.png)

stringa di connessione Hello è nel formato standard di MongoDB hello:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Utilizzare hello verificare comando tooensure che hello MongoDB istanza specificata nel campo stringa di connessione hello è accessibile.
> 
> 

Immettere il nome di hello dell'insieme di hello da cui verranno importati i dati. È facoltativamente possibile specificare o fornire un file per una query (ad esempio {pop: {$gt: 5000}}) e/o proiezione (ad esempio {loc:0}) tooboth filtro e la forma hello dati toobe importati.

Ecco alcuni tooimport esempi della riga di comando da MongoDB:

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>file di esportazione tooimport MongoDB

> [!IMPORTANT]
> Se si importano account Azure Cosmos DB tooan con supporto per MongoDB, attenersi alla seguente [istruzioni](mongodb-migrate.md).
> 
> 

opzione di esportazione JSON file sorgente dell'utilità di importazione MongoDB Hello consente tooimport uno o più file JSON generato dall'utilità mongoexport hello.  

![Screenshot delle opzioni relative all'origine per file di esportazione MongoDB](./media/import-data/mongodbexportsource.png)

Quando si aggiungono cartelle contenenti file JSON di esportazione MongoDB per l'importazione, è possibile hello in modo ricorsivo la ricerca dei file nelle sottocartelle.

Ecco un tooimport di esempio della riga di comando da esportazione MongoDB file JSON:

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>tooimport da SQL Server
opzione dell'utilità di importazione dell'origine SQL Hello consente tooimport da un singolo database di SQL Server e facoltativamente il filtro hello record toobe importati utilizzando una query. Inoltre, è possibile modificare struttura del documento hello specificando un separatore di annidamento (ulteriori informazioni in proposito).  

![Schermata delle opzioni dell'origine SQL - Strumenti di migrazione del database](./media/import-data/sqlexportsource.png)

Hello della stringa di connessione hello è hello standard SQL connessione stringa formato.

> [!NOTE]
> Utilizzare hello verificare comando tooensure che l'istanza di SQL Server specificato nel campo stringa di connessione hello hello è accessibile.
> 
> 

la nidificazione di proprietà separatore Hello è relazioni gerarchiche toocreate utilizzato (documenti secondari) durante l'importazione. Prendere in considerazione hello seguente query SQL:

*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*

Restituisce hello successivo di risultati (parziali):

![Schermata dei risultati della query SQL](./media/import-data/sqlqueryresults.png)

Si noti, ad esempio Address.AddressType e Address.Location.StateProvinceName gli alias di hello. Specificando un separatore di nidificazione '.', lo strumento di importazione hello Crea indirizzo e importare i documenti secondari Address.Location durante hello. Ecco un esempio di documento risultante in Azure Cosmos DB:

*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*

Ecco alcuni tooimport esempi della riga di comando da SQL Server:

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>file CSV tooimport e tooJSON CSV convert
opzione dell'utilità di importazione dell'origine di file CSV Hello consente si tooimport uno o più file CSV. Quando si aggiungono cartelle contenenti file CSV per l'importazione, è possibile hello in modo ricorsivo la ricerca dei file nelle sottocartelle.

![Opzioni origine schermata di CSV - tooJSON CSV](media/import-data/csvsource.png)

Origine SQL toohello simile, hello nidificazione proprietà separatore può essere utilizzato toocreate relazioni gerarchiche (documenti secondari) durante l'importazione. Prendere in considerazione hello seguente riga di intestazione CSV e le righe di dati:

![Record di esempio di schermata di CSV - tooJSON CSV](./media/import-data/csvsample.png)

Si noti, ad esempio DomainInfo.Domain_Name e RedirectInfo.Redirecting gli alias di hello. Specificando un separatore di nidificazione '.', lo strumento di importazione hello creerà DomainInfo e importare i documenti secondari RedirectInfo durante hello. Ecco un esempio di documento risultante in Azure Cosmos DB:

*{"DomainInfo": {"Nome_dominio": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"}"Agenzie federali":"Conferenza amministrativa di hello United States","RedirectInfo": {"Reindirizzamento":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*

lo strumento di importazione Hello tenterà tooinfer informazioni sul tipo per valori non racchiusi tra virgolette nei file CSV (valori tra virgolette vengono sempre considerati come stringhe).  Tipi vengono identificati nel seguente ordine hello: numero, datetime, boolean.  

Esistono due altri toonote operazioni sull'importazione di file CSV:

1. Per impostazione predefinita, nei valori non racchiusi tra virgolette vengono sempre rimossi spazi e tabulazioni, mentre i valori tra virgolette vengono mantenuti così come sono. Questo comportamento può essere sostituito con hello che Trim racchiuso tra virgolette i valori casella di controllo o hello /s.TrimQuoted opzione riga di comando.
2. Per impostazione predefinita, un valore Null non racchiuso tra virgolette viene considerato come valore Null. Questo comportamento può essere ignorato (ovvero considerare un null non racchiusi tra virgolette come una stringa "null") con hello Treat non racchiusi tra virgolette NULL come stringa Casella di controllo o hello /s.NoUnquotedNulls opzione riga di comando.

Ecco un esempio di riga di comando per l'importazione CSV:

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>tooimport dall'archiviazione tabelle di Azure
Hello opzione dell'utilità di importazione di origine archiviazione tabelle di Azure consente tooimport da una singola tabella di archiviazione tabelle di Azure e, facoltativamente, filtrare hello tabella entità toobe importati. Si noti che non è possibile utilizzare dati di archiviazione Azure Table strumento tooimport hello migrazione dei dati in Azure Cosmos DB per l'utilizzo con hello API di tabella. Solo l'importazione tooAzure Cosmos DB da utilizzare con l'API DocumentDB hello è supportato in questo momento.

![Schermata delle opzioni dell'origine Archiviazione tabelle di Azure](./media/import-data/azuretablesource.png)

Hello formato di stringa di connessione di archiviazione Azure Table hello è:

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Utilizzare hello verificare comando tooensure che l'istanza di archiviazione tabelle di Azure specificato nel campo stringa di connessione hello hello è accessibile.
> 
> 

Immettere il nome di hello di hello Azure da cui verranno importati i dati nella tabella. Se si preferisce, si può specificare un [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).

opzione dell'utilità di importazione di tabelle di Azure storage origine Hello ha hello le opzioni aggiuntive seguenti:

1. Include Internal Fields
   1. All: include tutti i campi interni (PartitionKey, RowKey e Timestamp)
   2. None: esclude tutti i campi interni
   3. RowKey - includere solo campi di hello RowKey
2. Select Columns
   1. I filtri di Archiviazione tabelle di Azure non supportano le proiezioni. Se si desidera tooonly importazione specifica tabelle di Azure le proprietà delle entità, aggiungerli toohello elenco di colonne selezionate. Tutte le altre proprietà delle entità verranno ignorate.

Di seguito è riportato un tooimport di esempio della riga di comando da Archiviazione tabelle di Azure:

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>tooimport da DynamoDB Amazon
opzione dell'utilità di importazione dell'origine di Amazon DynamoDB Hello consente tooimport da una singola tabella DynamoDB Amazon e facoltativamente il filtro hello entità toobe importati. Sono disponibili vari modelli in modo che l'impostazione di un'importazione è più semplice possibile.

![Schermata delle opzioni dell'origine Amazon DynamoDB - Strumenti di migrazione del database](./media/import-data/dynamodbsource1.png)

![Schermata delle opzioni dell'origine Amazon DynamoDB - Strumenti di migrazione del database](./media/import-data/dynamodbsource2.png)

Hello formato di stringa di connessione DynamoDB Amazon hello è:

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Utilizzare hello verificare comando tooensure che hello Amazon DynamoDB istanza specificata nel campo stringa di connessione hello è accessibile.
> 
> 

Di seguito è riportato un tooimport di esempio della riga di comando da Amazon DynamoDB:

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>tooimport file dall'archiviazione Blob di Azure
Hello file JSON, i file di esportazione MongoDB e le opzioni dell'utilità di importazione di codice sorgente file CSV consentono tooimport uno o più file dall'archiviazione Blob di Azure. Dopo aver specificato un URL del contenitore Blob e la chiave dell'Account, è sufficiente fornire un file tooimport di espressione regolare tooselect hello.

![Schermata delle opzioni dell'origine file JSON](./media/import-data/blobsource.png)

Ecco i file JSON di riga di comando esempio tooimport dall'archiviazione Blob di Azure:

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>tooimport da un insieme di API di Azure Cosmos DB DocumentDB
opzione dell'utilità di importazione di Azure Cosmos DB origine Hello consente tooimport dati da una o più raccolte di Azure Cosmos DB e, facoltativamente, filtrare i documenti utilizzando una query.  

![Screenshot delle opzioni relative all'origine per Azure Cosmos DB](./media/import-data/documentdbsource.png)

Hello formato di stringa di connessione Azure Cosmos DB hello è:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hello stringa di connessione di database di Azure Cosmos account può essere recuperato dal Pannello di chiavi hello di hello portale di Azure, come descritto in [come un account Azure Cosmos DB toomanage](manage-account.md), ma il nome di hello del database hello deve toohello toobe aggiunto stringa di connessione in hello seguente formato:

    Database=<CosmosDB Database>;

> [!NOTE]
> Utilizzare hello verificare comando tooensure che hello Azure Cosmos DB istanza specificata nel campo stringa di connessione hello è accessibile.
> 
> 

tooimport da una singola raccolta DB Cosmos Azure, immettere il nome di hello dell'insieme di hello da cui verranno importati i dati. tooimport da più database di Azure Cosmos raccolte, fornire un toomatch di espressione regolare uno o più nomi di raccolta (ad esempio collection01 | collection02 | collection03). Facoltativamente, è possibile specificare, o fornire un file in un filtro di query tooboth e forma hello toobe di dati importati.

> [!NOTE]
> Poiché il campo raccolta hello accetta espressioni regolari, se si desidera importare da un'unica raccolta il cui nome contiene caratteri di espressioni regolari, devono pertanto escape tali caratteri.
> 
> 

opzione dell'utilità di importazione di Azure Cosmos DB origine Hello presenta opzioni avanzate seguenti hello:

1. Includere campi interni: Specifica se consentire o meno tooinclude Azure Cosmos DB documento proprietà del sistema hello Esporta (ad esempio RID, TS).
2. Numero di tentativi in caso di errore: Specifica il numero di hello di volte in cui tooretry hello connessione tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).
3. Intervallo tra tentativi: Specifica il tempo toowait tra tentativi di connessione di hello tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).
4. Modalità di connessione: Specifica toouse modalità di connessione hello con Azure Cosmos DB. le scelte disponibili Hello sono DirectTcp, DirectHttps e Gateway. modalità di connessione diretta Hello sono più velocemente, mentre la modalità di gateway di hello è firewall più descrittivo, in quanto utilizza solo la porta 443.

![Screenshot delle opzioni avanzate per origini Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> Hello strumento predefinite tooconnection modalità importazione DirectTcp. Se si verificano problemi di firewall, passare in modalità tooconnection Gateway, poiché richiede solo la porta 443.
> 
> 

Ecco alcuni tooimport esempi della riga di comando da Azure Cosmos DB:

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> Strumento di importazione di Azure Cosmos DB dati Hello supporta inoltre l'importazione di dati da hello [emulatore di Azure Cosmos DB](local-emulator.md). Quando si importano dati da un emulatore locale, impostare endpoint hello troppo`https://localhost:<port>`. 
> 
> 

## <a id="HBaseSource"></a>tooimport da HBase
opzione dell'utilità di importazione dell'origine di HBase Hello consente tooimport dati da una tabella HBase e, facoltativamente, filtrare i dati di hello. Sono disponibili vari modelli in modo che l'impostazione di un'importazione è più semplice possibile.

![Schermata di HBase opzioni del codice sorgente](./media/import-data/hbasesource1.png)

![Schermata di HBase opzioni del codice sorgente](./media/import-data/hbasesource2.png)

Hello formato di stringa di connessione di HBase Stargate hello è:

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Utilizzare hello verificare comando tooensure che hello HBase istanza specificata nel campo stringa di connessione hello è accessibile.
> 
> 

Di seguito è riportato un tooimport di esempio della riga di comando da HBase:

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello API DocumentDB (importazione in blocco)
utilità di importazione Bulk di DB Cosmos Azure Hello consente tooimport da qualsiasi delle opzioni di origine disponibile hello, utilizzando una routine di Azure Cosmos DB archiviati per una maggiore efficienza. strumento Hello supporta importazione tooone partizionata singolo Azure Cosmos DB raccolta, nonché importazione partizionati in base al quale i dati vengono partizionati in più raccolte di Azure Cosmos DB partizionata singolo. Per altre informazioni sul partizionamento dei dati, vedere l'articolo relativo a [partizionamento e ridimensionamento in Azure Cosmos DB](partition-data.md). strumento Hello crea, eseguire e quindi eliminare procedure hello archiviato dalle raccolte di destinazione hello.  

![Screenshot delle opzioni relative all'importazione in blocco di Azure Cosmos DB](./media/import-data/documentdbbulk.png)

Hello formato di stringa di connessione Azure Cosmos DB hello è:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hello stringa di connessione di database di Azure Cosmos account può essere recuperato dal Pannello di chiavi hello di hello portale di Azure, come descritto in [come un account Azure Cosmos DB toomanage](manage-account.md), ma il nome di hello del database hello deve toohello toobe aggiunto stringa di connessione in hello seguente formato:

    Database=<CosmosDB Database>;

> [!NOTE]
> Utilizzare hello verificare comando tooensure che hello Azure Cosmos DB istanza specificata nel campo stringa di connessione hello è accessibile.
> 
> 

tooimport tooa singola raccolta, immettere il nome di hello di hello toowhich di raccolta dati verranno importati e fare clic sul pulsante Aggiungi hello. raccolte toomultiple tooimport, immettere il nome di ogni raccolta singolarmente o utilizzare hello segue sintassi toospecify più raccolte: *collection_prefix*[inizio indice - indice finale]. Quando si specificano più raccolte tramite sintassi di hello menzionati in precedenza, tenere presente hello segue:

1. Sono supportati solo criteri di denominazione con intervalli interi. Ad esempio, l'indicazione insieme [0-3] produrrà hello seguenti raccolte: collection0, collection1, collection2, collection3.
2. È possibile usare una sintassi abbreviata: collection[3] restituirà lo stesso set di raccolte citato nel passaggio 1.
3. È possibile specificare più di una sostituzione. Ad esempio, collection[0-1] [0-9] genererà 20 nomi di raccolte con zeri iniziali (collection01, ..02, ..03).

Una volta hello nomi di raccolta sono stati specificati, scegliere velocità effettiva desiderata hello di raccolte di hello (400 RUs too10, russo 000). Per ottimizzare le prestazioni di importazione, scegliere una velocità effettiva superiore. Per altre informazioni sui livelli di prestazioni, vedere l'articolo relativo ai [livelli di prestazioni in Azure Cosmos DB](performance-levels.md).

> [!NOTE]
> impostazione della velocità effettiva delle prestazioni di Hello solo toocollection creazione. Se hello specificato raccolta esiste già, la velocità effettiva non verrà modificata.
> 
> 

Quando si importano toomultiple raccolte, lo strumento di importazione hello supporta il partizionamento orizzontale basato su hash. In questo scenario, specificare proprietà del documento hello desiderato toouse come chiave di partizione hello (se la chiave di partizione viene lasciata vuota, documenti verrà partizionati in modo casuale fra le raccolte di destinazione hello).

Facoltativamente, è possibile specificare il campo nell'origine di importazione hello deve essere utilizzato come hello proprietà id di database di Azure Cosmos documento durante l'importazione di hello (si noti che se questa proprietà non contengono documenti, quindi lo strumento di importazione hello genererà un GUID come valore della proprietà id hello).

Durante l'importazione sono disponibili numerose opzioni avanzate. Prima di tutto, mentre lo strumento hello include un blocco predefinito importare stored procedure (BulkInsert.js), è possibile scegliere toospecify importazione stored procedure personalizzate:

 ![Screenshot dell'opzione relativa alla stored procedure di inserimento in blocco per Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

Inoltre, quando si importano i tipi di data (ad esempio, da SQL Server o MongoDB), è possibile scegliere tra tre opzioni di importazione:

 ![Screenshot delle opzioni di importazione relative a data e ora per Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* String: persiste come valore di stringa.
* Epoch: persiste come valore numerico di periodo.
* Both: persiste come valore di stringa e numerico di periodo. Questa opzione creerà un documento secondario, ad esempio: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }

utilità di importazione Bulk di DB Cosmos Azure Hello è hello ulteriori opzioni avanzate seguenti:

1. Dimensione batch: hello strumento predefinite tooa dimensione di batch di 50.  Se hello documenti toobe importati è di grandi dimensioni, considerare la riduzione delle dimensioni del batch hello. Al contrario hello documenti toobe importati è troppo piccoli, è consigliabile generare dimensioni batch hello.
2. Max Script dimensione (byte): valore predefinito è lo strumento hello tooa dimensione massima di 512KB
3. Disattiva generazione automatica di Id: Se toobe ogni documento importato contiene un campo id, questa opzione può migliorare le prestazioni. I documenti in cui manca un campo ID univoco non verranno importati.
4. Documenti di aggiornamento esistente: hello strumento predefinite toonot sostituendo i documenti esistenti con id in conflitto. Questa opzione consentirà di sovrascrivere i documenti esistenti con ID corrispondenti. Questa funzionalità è utile per le migrazioni dei dati pianificate che aggiornano i documenti esistenti.
5. Numero di tentativi in caso di errore: Specifica il numero di hello di volte in cui tooretry hello connessione tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).
6. Intervallo tra tentativi: Specifica il tempo toowait tra tentativi di connessione di hello tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).
7. Modalità di connessione: Specifica toouse modalità di connessione hello con Azure Cosmos DB. le scelte disponibili Hello sono DirectTcp, DirectHttps e Gateway. modalità di connessione diretta Hello sono più velocemente, mentre la modalità di gateway di hello è firewall più descrittivo, in quanto utilizza solo la porta 443.

![Screenshot delle opzioni avanzate di importazione in blocco di Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> Hello strumento predefinite tooconnection modalità importazione DirectTcp. Se si verificano problemi di firewall, passare in modalità tooconnection Gateway, poiché richiede solo la porta 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello API DocumentDB (importazione di Record sequenziali)
unità di importazione dei record sequenziali Hello Azure Cosmos DB consente tooimport da una qualsiasi delle opzioni di origine disponibile hello su una base di un record. È possibile scegliere questa opzione se si importano tooan la raccolta esistente che ha raggiunto la quota di stored procedure. importazione tooa di Hello strumento supporta una singola raccolta Azure Cosmos DB (singola partizione e più partizioni), nonché importazione partizionati in base al quale i dati vengono partizionati in più raccolte di Azure Cosmos DB singola partizione e/o più partizioni. Per altre informazioni sul partizionamento dei dati, vedere l'articolo relativo a [partizionamento e ridimensionamento in Azure Cosmos DB](partition-data.md).

![Screenshot delle opzioni di importazione di record sequenziali per Azure Cosmos DB](./media/import-data/documentdbsequential.png)

Hello formato di stringa di connessione Azure Cosmos DB hello è:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hello stringa di connessione di database di Azure Cosmos account può essere recuperato dal Pannello di chiavi hello di hello portale di Azure, come descritto in [come un account Azure Cosmos DB toomanage](manage-account.md), ma il nome di hello del database hello deve toohello toobe aggiunto stringa di connessione in hello seguente formato:

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Utilizzare hello verificare comando tooensure che hello Azure Cosmos DB istanza specificata nel campo stringa di connessione hello è accessibile.
> 
> 

tooimport tooa singola raccolta, immettere il nome di hello di hello toowhich di raccolta dati verranno importati e fare clic sul pulsante Aggiungi hello. raccolte toomultiple tooimport, immettere il nome di ogni raccolta singolarmente o utilizzare hello segue sintassi toospecify più raccolte: *collection_prefix*[inizio indice - indice finale]. Quando si specificano più raccolte tramite sintassi di hello menzionati in precedenza, tenere presente hello segue:

1. Sono supportati solo criteri di denominazione con intervalli interi. Ad esempio, l'indicazione insieme [0-3] produrrà hello seguenti raccolte: collection0, collection1, collection2, collection3.
2. È possibile usare una sintassi abbreviata: collection[3] restituirà lo stesso set di raccolte citato nel passaggio 1.
3. È possibile specificare più di una sostituzione. Ad esempio, collection[0-1] [0-9] genererà 20 nomi di raccolte con zeri iniziali (collection01, ..02, ..03).

Una volta hello nomi di raccolta sono stati specificati, scegliere velocità effettiva desiderata hello di raccolte di hello (400 RUs too250, russo 000). Per ottimizzare le prestazioni di importazione, scegliere una velocità effettiva superiore. Per altre informazioni sui livelli di prestazioni, vedere l'articolo relativo ai [livelli di prestazioni in Azure Cosmos DB](performance-levels.md). Qualsiasi importazione toocollections con velocità effettiva > 10.000 RUs richiederà una chiave di partizione. Se si sceglie toohave 250.000 russo, occorre toofile una richiesta di hello portale toohave aumentato l'account.

> [!NOTE]
> impostazione della velocità effettiva di Hello solo toocollection creazione. Se hello specificato raccolta esiste già, la velocità effettiva non verrà modificata.
> 
> 

Quando si importano toomultiple raccolte, lo strumento di importazione hello supporta il partizionamento orizzontale basato su hash. In questo scenario, specificare proprietà del documento hello desiderato toouse come chiave di partizione hello (se la chiave di partizione viene lasciata vuota, documenti verrà partizionati in modo casuale fra le raccolte di destinazione hello).

Facoltativamente, è possibile specificare il campo nell'origine di importazione hello deve essere utilizzato come hello proprietà id di database di Azure Cosmos documento durante l'importazione di hello (si noti che se questa proprietà non contengono documenti, quindi lo strumento di importazione hello genererà un GUID come valore della proprietà id hello).

Durante l'importazione sono disponibili numerose opzioni avanzate. Innanzitutto, quando si importano i tipi di data (ad esempio, da SQL Server o MongoDB), è possibile scegliere tra tre opzioni di importazione:

 ![Screenshot delle opzioni di importazione relative a data e ora per Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* String: persiste come valore di stringa.
* Epoch: persiste come valore numerico di periodo.
* Both: persiste come valore di stringa e numerico di periodo. Questa opzione creerà un documento secondario, ad esempio: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }

Hello Azure Cosmos DB - utilità di importazione di record sequenziale ha hello ulteriori opzioni avanzate seguenti:

1. Numero di richieste in parallelo: strumento di hello per impostazione predefinita le richieste parallele too2. Se hello documenti toobe importati è troppo piccoli, prendere in considerazione elevamento hello numero di richieste in parallelo. Si noti che se questo numero viene generato eccessivamente elevato, hello importazione che verifichi la limitazione delle richieste.
2. Disattiva generazione automatica di Id: Se toobe ogni documento importato contiene un campo id, questa opzione può migliorare le prestazioni. I documenti in cui manca un campo ID univoco non verranno importati.
3. Documenti di aggiornamento esistente: hello strumento predefinite toonot sostituendo i documenti esistenti con id in conflitto. Questa opzione consentirà di sovrascrivere i documenti esistenti con ID corrispondenti. Questa funzionalità è utile per le migrazioni dei dati pianificate che aggiornano i documenti esistenti.
4. Numero di tentativi in caso di errore: Specifica il numero di hello di volte in cui tooretry hello connessione tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).
5. Intervallo tra tentativi: Specifica il tempo toowait tra tentativi di connessione di hello tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).
6. Modalità di connessione: Specifica toouse modalità di connessione hello con Azure Cosmos DB. le scelte disponibili Hello sono DirectTcp, DirectHttps e Gateway. modalità di connessione diretta Hello sono più velocemente, mentre la modalità di gateway di hello è firewall più descrittivo, in quanto utilizza solo la porta 443.

![Screenshot delle opzioni avanzate di importazione di record sequenziali di Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> Hello strumento predefinite tooconnection modalità importazione DirectTcp. Se si verificano problemi di firewall, passare in modalità tooconnection Gateway, poiché richiede solo la porta 443.
> 
> 

## <a id="IndexingPolicy"></a>Specificare un criterio di indicizzazione durante la creazione di raccolte di Azure Cosmos DB
Quando si consentono la migrazione di hello raccolte toocreate strumento durante l'importazione, è possibile specificare criteri di indicizzazione hello di raccolte di hello. In hello avanzate sezione Opzioni di importazione Bulk di DB Cosmos Azure hello e Azure Cosmos DB sequenziale opzioni di registrazione, passare toohello sezione relativa ai criteri di indicizzazione.

![Screenshot delle opzioni avanzate relative ai criteri di indicizzazione di Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

Utilizza hello opzione criteri di indicizzazione avanzati, è possibile selezionare un file di criteri di indicizzazione, manualmente immettere criteri di indicizzazione o selezionare da un set di modelli predefiniti (facendo clic destro del mouse nella casella di testo criteri di indicizzazione hello).

lo strumento hello fornisce modelli di criteri di Hello sono:

* Default. Questo criterio è migliore quando si eseguono query di uguaglianza su stringhe e utilizzando ORDER BY, l'intervallo e le query di uguaglianza per i numeri. Questo criterio ha un overhead di archiviazione indice inferiore rispetto a intervallo.
* Intervallo. Questo criterio è consigliabile quando si sta utilizzando query ORDER BY, intervallo e uguaglianza su stringhe e numeri. Questo criterio ha un overhead di archiviazione indice superiore rispetto a predefinito o Hash.

![Screenshot delle opzioni avanzate relative ai criteri di indicizzazione di Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> Se non si specifica un criterio di indicizzazione, verranno applicati criteri predefiniti hello. Per altre informazioni sui criteri di indicizzazione, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md).
> 
> 

## <a name="export-toojson-file"></a>File di esportazione tooJSON
esportazione di Azure Cosmos DB JSON Hello consente tooexport qualsiasi hello disponibili opzioni tooa JSON file di origine che contiene una matrice di documenti JSON. strumento Hello gestirà esportazione hello automaticamente oppure è possibile scegliere il comando di migrazione tooview hello risultante ed eseguire il comando hello manualmente. file JSON risultante Hello può essere archiviati in locale o nel servizio di archiviazione Blob di Azure.

![Screenshot dell'opzione di esportazione in file JSON locale di Azure Cosmos DB](./media/import-data/jsontarget.png)

![Screenshot dell'opzione di esportazione in file JSON in un archivio BLOB di Azure di Azure Cosmos DB](./media/import-data/jsontarget2.png)

Facoltativamente, è possibile scegliere hello tooprettify risultante JSON, che aumenta la dimensione hello del documento risultante hello mentre effettua hello contenuto più leggibili.

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a>Configurazione avanzata
Nella schermata di configurazione avanzate hello, specificare il percorso di hello di hello toowhich di file di log che si desidera che gli eventuali errori scritti. Hello seguendo regole si applica toothis pagina:

1. Se non viene fornito un nome di file, verranno restituiti tutti gli errori nella pagina di risultati hello.
2. Se viene specificato un nome di file senza una directory, quindi il file hello sarà creato (o sovrascritto) nella directory di ambiente corrente hello.
3. Se si seleziona un oggetto esistente verrà sovrascritto file, quindi il file hello, vi è alcuna possibilità di Accodamento.

Quindi, scegliere se toolog tutti critico, o nessun messaggio di errore. Infine, decidere di frequenza hello nel messaggio di trasferimento dello schermo verrà aggiornato con lo stato di avanzamento.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>Confermare le impostazioni di importazione e visualizzare la riga di comando
1. Dopo aver specificato le informazioni sull'origine, le informazioni di destinazione e configurazione avanzata, verificare la migrazione di hello riepilogo e, facoltativamente, visualizzazione o copia hello risultante comando migration (copia comando hello è utile tooautomate operazioni di importazione):
   
    ![Schermata della pagina di riepilogo](./media/import-data/summary.png)
   
    ![Schermata della pagina di riepilogo](./media/import-data/summarycommand.png)
2. Una volta verificate le opzioni di origine e di destinazione, fare clic su **Import**. tempo trascorso Hello, conteggio trasferito e informazioni sull'errore (se si non specifica un nome di file di configurazione avanzate hello) verranno aggiornati come importazione hello è in corso. Al termine dell'operazione, è possibile esportare risultati hello (ad esempio toodeal gli eventuali errori di importazione).
   
    ![Screenshot dell'opzione di esportazione in JSON di Azure Cosmos DB](./media/import-data/viewresults.png)
3. È possibile anche avviare una nuova importazione hello esistente le stesse impostazioni (ad esempio informazioni di origine e destinazione scelta di stringa di connessione e così via) o la reimpostazione di tutti i valori.
   
    ![Screenshot dell'opzione di esportazione in JSON di Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Lo strumento di migrazione dei dati hello installato
> * Importazione di dati da diverse origini dati
> * Esportato da Azure Cosmos DB tooJSON

È ora possibile continuare l'esercitazione successiva toohello e acquisire informazioni come dati tooquery tramite Azure Cosmos DB. 

> [!div class="nextstepaction"]
>[Come tooquery dati?](../cosmos-db/tutorial-query-documentdb.md)
