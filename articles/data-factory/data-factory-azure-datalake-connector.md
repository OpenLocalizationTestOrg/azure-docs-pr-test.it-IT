---
title: aaaCopy tooand di dati dall'archivio Azure Data Lake | Documenti Microsoft
description: Informazioni su come toocopy tooand di dati dall'archivio Data Lake tramite Data Factory di Azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Copiare i dati tooand dall'archivio Data Lake tramite Data Factory
Questo articolo viene illustrato come toouse attività di copia in Azure Data Factory toomove dati tooand dall'archivio Azure Data Lake. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, una panoramica di spostamento dei dati con attività di copia.

## <a name="supported-scenarios"></a>Scenari supportati
È possibile copiare dati **dall'archivio Azure Data Lake** toohello archivi dati seguenti:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

È possibile copiare dati da archivi dati seguenti hello **tooAzure archivio Data Lake**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Creare un account Data Lake Store prima della creazione di una pipeline con l'attività di copia. Per altre informazioni, vedere l'[introduzione ad Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Tipi di autenticazione supportati
connettore di archivio Data Lake Hello supporta questi tipi di autenticazione:
* Autenticazione di un'entità servizio
* Autenticazione basata su credenziali dell'utente (OAuth) 

È consigliabile usare l'autenticazione basata su entità servizio, in particolare per una copia di dati pianificata. Con l'autenticazione basata sulle credenziali dell'utente può verificarsi la scadenza del token. Per informazioni sulla configurazione, vedere hello [servizio proprietà collegate](#linked-service-properties) sezione.

## <a name="get-started"></a>Attività iniziali
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso Azure Data Lake Store usando diversi strumenti/API.

toocreate modo più semplice di Hello toocopy una pipeline di dati è hello toouse **Copia guidata**. Per un'esercitazione sulla creazione di una pipeline mediante Copia guidata hello, vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md).

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare una **data factory**. Una data factory può contenere una o più pipeline. 
2. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory. Se, ad esempio, si copiano dati da un tooan di archiviazione blob di Azure archivio Azure Data Lake, due toolink servizi collegati creare l'account di archiviazione di Azure e la data factory di Azure Data Lake archivio tooyour. Per le proprietà di servizio collegato che sono specifici tooAzure archivio Data Lake, vedere [servizio proprietà collegate](#linked-service-properties) sezione. 
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello. E si crea un altro set di dati toospecify hello cartella e il percorso nell'archivio Data Lake hello che contiene dati hello copiati dall'archiviazione blob hello. Per le proprietà di set di dati che sono specifici tooAzure archivio Data Lake, vedere [proprietà set di dati](#dataset-properties) sezione.
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e AzureDataLakeStoreSink come sink per attività di copia hello. Analogamente, se si sta copiando l'archivio Azure Data Lake tooAzure nell'archiviazione Blob, utilizzare AzureDataLakeStoreSource e BlobSink nell'attività di copia hello. Per le proprietà di attività di copia che sono specifici tooAzure archivio Data Lake, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione. Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.  

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati dati da e verso un archivio Azure Data Lake, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) sezione di questo articolo.

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooData Lake archivio.

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Un servizio collegato di collegare una data factory tooa archivio di dati. Creare un servizio collegato di tipo **AzureDataLakeStore** toolink la data factory tooyour dati di archivio Data Lake. Hello nella tabella seguente vengono descritti i servizi tooData Lake archivio collegato specifici di JSON elementi. È possibile scegliere tra l'autenticazione basata su entità servizio e l'autenticazione basata su credenziali utente.

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| **type** | proprietà di tipo Hello deve essere impostata troppo**AzureDataLakeStore**. | Sì |
| **dataLakeStoreUri** | Informazioni sull'account archivio Azure Data Lake hello. Queste informazioni accetta uno dei seguenti formati hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`. | Sì |
| **subscriptionId** | Hello toowhich di ID sottoscrizione di Azure account archivio Data Lake appartiene. | Richiesto per il sink |
| **resourceGroupName** | Hello toowhich di nome gruppo risorse di Azure account archivio Data Lake appartiene. | Richiesto per il sink |

### <a name="service-principal-authentication-recommended"></a>Autenticazione basata su entità servizio (opzione consigliata)
toouse l'autenticazione dell'entità servizio, registrare un'entità di applicazione in Azure Active Directory (Azure AD) e concedere hello accedere all'archivio Lake tooData. Per la procedura dettaglia, vedere [Autenticazione da servizio a servizio](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Prendere nota dei seguenti valori, che permette di hello hello toodefine servizio collegato:
* ID applicazione
* Chiave applicazione 
* ID tenant

> [!IMPORTANT]
> Se si utilizza una pipeline di dati tooauthor Copia guidata hello, assicurarsi che la concessione delle entità servizio hello almeno un **lettore** ruolo di controllo di accesso (gestione delle identità e accesso) per l'account archivio Data Lake hello. Inoltre, concedere almeno un'entità servizio hello **lettura + Execute** autorizzazione tooyour archivio Data Lake radice ("/") e nei relativi elementi figlio. In caso contrario si potrebbe vedere il messaggio hello "hello credenziali specificate non sono validi".<br/><br/>
Dopo aver creato o aggiornare un'entità servizio in Azure AD, può richiedere alcuni minuti per effetto di tootake modifiche hello. Controllare l'entità servizio hello e le configurazioni di archivio Data Lake accesso controllo elenco (ACL). Se viene ancora visualizzato il messaggio hello "hello credenziali specificate non sono validi", attendere qualche minuto e riprovare.

Utilizzare l'autenticazione dell'entità servizio specificando hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| **servicePrincipalId** | Specificare un ID client. dell'applicazione hello | Sì |
| **servicePrincipalKey** | Specificare la chiave dell'applicazione hello. | Sì |
| **tenant** | Specificare le informazioni di hello tenant (dominio tenant o nome ID) in cui risiede l'applicazione. È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure. | Sì |

**Esempio: autenticazione basata su entità servizio**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticazione basata su credenziali utente
In alternativa, è possibile utilizzare toocopy di autenticazione delle credenziali utente da o archivio Lake tooData specificando hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| **authorization** | Fare clic su hello **Authorize** pulsante hello Editor delle Data Factory e immettere le credenziali dell'utente che assegna la proprietà toothis hello generato automaticamente autorizzazione URL. | Sì |
| **sessionId** | ID di sessione OAuth della sessione di autorizzazione OAuth hello. Ogni ID di sessione è univoco e può essere usato solo una volta. Questa impostazione viene generata automaticamente quando si utilizza hello Editor delle Data Factory. | Sì |

**Esempio: autenticazione basata su credenziali utente**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Scadenza del token
codice di autorizzazione generati utilizzando hello Hello **Authorize** pulsante scade dopo un determinato periodo di tempo. segue messaggio Hello significa che è scaduto il token di autenticazione hello:

Errore dell'operazione relativa alle credenziali: invalid_grant - AADSTS70002: Errore di convalida delle credenziali. AADSTS70008: hello fornito concessione di accesso è scaduto o revocato. ID traccia: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID correlazione: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.

Hello nella tabella seguente mostra le scadenze di hello di diversi tipi di account utente:


| Tipo di utente | Scade dopo |
|:--- |:--- |
| Account utente *non* gestiti da Azure Active Directory (ad esempio, @hotmail.com or @live.com) |12 ore |
| Account utente gestiti da Azure Active Directory |eseguire 14 giorni dopo l'ultima sezione di hello <br/><br/>90 giorni, se viene eseguita una sezione basata su un servizio collegato OAuth almeno una volta ogni 14 giorni |

Se si modifica la password precedente all'ora di scadenza del token hello, hello scadenza del token immediatamente. Verrà visualizzato il messaggio hello indicato in precedenza in questa sezione.

È possibile riautorizzare account hello utilizzando hello **Authorize** pulsante quando il token di hello scade hello tooredeploy servizio collegato. È anche possibile generare i valori per hello **sessionId** e **autorizzazione** hello delle proprietà a livello di codice mediante il codice seguente:


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Per ulteriori informazioni sulle classi di Data Factory hello utilizzate nel codice hello, vedere hello [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [ Classe AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) argomenti. Aggiungere un riferimento tooversion `2.9.10826.1824` di `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` per hello `WindowsFormsWebAuthenticationDialog` classe utilizzata nel codice hello.

## <a name="dataset-properties"></a>Proprietà dei set di dati
dati di input toorepresent un set di dati in un archivio Data Lake toospecify, impostare hello **tipo** proprietà del set di dati hello troppo**AzureDataLakeStore**. Set hello **linkedServiceName** proprietà del nome di toohello hello set di dati di archivio Data Lake hello servizio collegato. Per un elenco completo delle sezioni JSON e le proprietà disponibili per la definizione di set di dati, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni di un set di dati in JSON, quali **struttura**, **disponibilità**, e **criteri**, sono simili per tutti i tipi di set di dati (ad esempio database SQL di Azure, BLOB Azure e tabelle di Azure). Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni come percorso e il formato dei dati di hello nell'archivio dati hello. 

Hello **typeProperties** sezione per un set di dati di tipo **AzureDataLakeStore** contiene hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| **folderPath** |Percorso toohello contenitore e della cartella in archivio Data Lake. |Sì |
| **fileName** |Nome del file hello in archivio Azure Data Lake. Hello **fileName** proprietà è facoltativa tra maiuscole e minuscole. <br/><br/>Se si specifica **fileName**, attività hello (inclusi copia) funziona su file specifiche hello.<br/><br/>Quando **fileName** non viene specificato, copia include tutti i file **folderPath** nel set di dati input hello.<br/><br/>Quando **fileName** non viene specificato per un set di dati di output e **preserveHierarchy** non viene specificato nel sink di attività, il nome di hello del file hello generato è in formato hello dati. _GUID_. txt ". Ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |No |
| **partitionedBy** |Hello **partitionedBy** proprietà è facoltativa. È possibile utilizzare il toospecify un percorso dinamico e il nome di file per i dati delle serie temporali. Ad esempio, è possibile includere parametri per ogni ora di dati in **folderPath**. Per informazioni dettagliate ed esempi, vedere [hello proprietà partitionedBy](#using-partitionedby-property). |No |
| **format** | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, e  **ParquetFormat**. Set hello **tipo** proprietà in **formato** tooone di questi valori. Per ulteriori informazioni, vedere hello [formato testo](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) sezioni hello [compressione di File e formati supportati da Azure Data Factory](data-factory-supported-file-and-compression-formats.md) articolo. <br><br> Se si desidera toocopy file "come-è" basato su file tra archivi diversi (copia binaria), ignorare hello `format` sezione in entrambe le definizioni di set di dati di input e output. |No |
| **compression** | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione supportati da Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

### <a name="hello-partitionedby-property"></a>proprietà partitionedBy Hello
È possibile specificare dinamica **folderPath** e **fileName** proprietà per i dati delle serie temporali con hello **partitionedBy** proprietà, funzioni di Data Factory e sistema variabili. Per informazioni dettagliate, vedere hello [Data Factory di Azure - funzioni e variabili di sistema](data-factory-functions-variables.md) articolo.


Nel seguente esempio, hello `{Slice}` viene sostituito con il valore di hello della variabile di sistema di Data Factory hello `SliceStart` in formato hello specificato (`yyyyMMddHH`). nome Hello `SliceStart` fa riferimento toohello ora di inizio della sezione hello. Hello `folderPath` proprietà è diversa per ogni sezione, come in `wikidatagateway/wikisampledataout/2014100103` o `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Nel seguente esempio, hello anno, mese, giorno e ora di hello `SliceStart` vengono estratti in variabili distinte che vengono utilizzate da hello `folderPath` e `fileName` proprietà:
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Per ulteriori informazioni sul set di dati di serie temporali, la pianificazione e le sezioni, vedere hello [set di dati in Azure Data Factory](data-factory-create-datasets.md) e [Data Factory di pianificazione e l'esecuzione](data-factory-scheduling-and-execution.md) articoli. 


## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle sezioni e le proprietà disponibili per la definizione delle attività, vedere hello [creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

le proprietà disponibili nella hello Hello **typeProperties** sezione di un'attività variano in base a ogni tipo di attività. Per un'attività di copia, variano a seconda dei tipi di hello di origini e sink.

**AzureDataLakeStoreSource** supporta hello seguente proprietà in hello **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| **recursive** |Indica se hello i dati letti in modo ricorsivo dalle sottocartelle di hello o solo dalla cartella specificata hello. |True (valore predefinito), False |No |


**AzureDataLakeStoreSink** supporta hello seguenti proprietà in hello **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| **copyBehavior** |Specifica il comportamento di copia hello. |<b>PreserveHierarchy</b>: mantiene la gerarchia di file hello nella cartella di destinazione hello. percorso relativo di Hello origine toosource della cartella dei file è identico toohello percorso relativo della cartella tootarget file di destinazione.<br/><br/><b>FlattenHierarchy</b>: tutti i file dalla cartella di origine hello vengono creati nel primo livello di hello hello della cartella di destinazione. file di destinazione Hello vengono creati con nomi generati automaticamente.<br/><br/><b>Oggetto</b>: unisce tutti i file dal file tooone cartella di origine hello. Se hello Nome file o un blob è specificato, il nome di file sottoposto a merge hello è nome specificato hello. In caso contrario, il nome di file hello viene generato automaticamente. |No |

### <a name="recursive-and-copybehavior-examples"></a>esempi ricorsivi e copyBehavior
In questa sezione viene descritto il comportamento risultante hello dell'operazione di copia hello per diverse combinazioni di valori ricorsiva e copyBehavior.

| ricorsiva | copyBehavior | Comportamento risultante |
| --- | --- | --- |
| true |preserveHierarchy |Per una cartella di origine Cartella1 con hello seguente struttura: <br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>cartella di destinazione Hello Cartella1 viene creata con hello stessa struttura come origine di hello<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5. |
| true |flattenHierarchy |Per una cartella di origine Cartella1 con hello seguente struttura: <br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>destinazione Hello Cartella1 viene creata con hello seguente struttura: <br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File5 |
| true |mergeFiles |Per una cartella di origine Cartella1 con hello seguente struttura: <br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>destinazione Hello Cartella1 viene creata con hello seguente struttura: <br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 + File3 + File4 + File 5 viene unito in un file con nome file generato automaticamente |
| false |preserveHierarchy |Per una cartella di origine Cartella1 con hello seguente struttura: <br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/><br/>Sottocartella1 con File3, File4 e File5 non considerati. |
| false |flattenHierarchy |Per una cartella di origine Cartella1 con hello seguente struttura:<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2<br/><br/><br/>Sottocartella1 con File3, File4 e File5 non considerati. |
| false |mergeFiles |Per una cartella di origine Cartella1 con hello seguente struttura:<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 viene unito in un file con un nome file generato automaticamente. Nome generato automaticamente per File1<br/><br/>Sottocartella1 con File3, File4 e File5 non considerati. |

## <a name="supported-file-and-compression-formats"></a>Formati di file e di compressione supportati
Per informazioni dettagliate, vedere hello [formati di File e la compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) articolo.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>Esempi JSON per la copia di dati tooand dall'archivio Data Lake
seguono esempi Hello fornisce definizioni JSON di esempio. È possibile utilizzare questi toocreate di definizioni di esempio una pipeline mediante hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hello esempi viene illustrato come toocopy tooand di dati dall'archiviazione Blob di Azure e archivio Data Lake. Tuttavia, i dati possono essere copiati _direttamente_ da qualsiasi hello origini tooany di sink hello è supportato. Per ulteriori informazioni, vedere sezione hello "archivi di dati supportati e formati" in hello [spostare i dati utilizzando l'attività di copia](data-factory-data-movement-activities.md) articolo.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Esempio: Copiare i dati da archiviazione Blob di Azure tooAzure archivio Data Lake
codice di esempio Hello in questa sezione viene illustrato:

* Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un servizio collegato di tipo [AzureDataLakeStore](#linked-service-properties).
* Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureDataLakeStore](#dataset-properties).
* Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureDataLakeStoreSink](#copy-activity-properties).

Hello esempi mostrano come serie temporale dei dati dall'archiviazione Blob di Azure sono copiato tooData Lake archivio ogni ora. 

**Servizio collegato Archiviazione di Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Servizio collegato di Azure Data Lake Store**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Per informazioni sulla configurazione, vedere hello [servizio proprietà collegate](#linked-service-properties) sezione.
>

**Set di dati di input del BLOB di Azure**

Nell'esempio seguente di hello, dati viene prelevati da un nuovo blob ogni ora (`"frequency": "Hour", "interval": 1`). Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello utilizza hello anno, mese e dell'ora di inizio hello parte relativa al giorno. nome del file Hello utilizza ora hello parte hello ora di inizio. Hello `"external": true` impostazione informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Set di dati di output di Azure Data Lake Store**

Hello nel seguente archivio Lake tooData di esempio copie dei dati. I nuovi dati vengono copiati tooData Lake archivio ogni ora.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Attività di copia in una pipeline con un'origine BLOB e un sink Data Lake Store**

Nell'esempio seguente di hello, pipeline hello contiene un'attività di copia che è configurata toouse hello set di dati di input e output. attività di copia Hello è pianificato toorun ogni ora. Nella pipeline hello definizione JSON, hello `source` tipo è stato impostato troppo`BlobSource`, hello e `sink` tipo è stato impostato troppo`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Esempio: Copiare i dati dall'archivio Azure Data Lake tooan blob di Azure
codice di esempio Hello in questa sezione viene illustrato:

* Un servizio collegato di tipo [AzureDataLakeStore](#linked-service-properties).
* Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureDataLakeStore](#dataset-properties).
* Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [AzureDataLakeStoreSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

codice Hello copia dati delle serie temporali da archivio Data Lake tooan blob di Azure ogni ora. 

**Servizio collegato di Azure Data Lake Store**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Per informazioni sulla configurazione, vedere hello [servizio proprietà collegate](#linked-service-properties) sezione.
>

**Servizio collegato Archiviazione di Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Set di dati di input di Azure Data Lake**

In questo esempio, l'impostazione `"external"` troppo`true` informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
**Set di dati di output del BLOB di Azure**

Nell'esempio seguente di hello, i dati vengono scritti tooa nuovo blob ogni ora (`"frequency": "Hour", "interval": 1`). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello utilizza hello anno, mese, giorno e dell'ora di inizio hello sezione relativa all'ora.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Attività di copia in una pipeline con un'origine Azure Data Lake Store e un sink BLOB**

Nell'esempio seguente di hello, pipeline hello contiene un'attività di copia che è configurata toouse hello set di dati di input e output. attività di copia Hello è pianificato toorun ogni ora. Nella pipeline hello definizione JSON, hello `source` tipo è stato impostato troppo`AzureDataLakeStoreSource`, hello e `sink` tipo è stato impostato troppo`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

Nella definizione di attività di copia hello, è anche possibile mappare le colonne di toocolumns set di dati di origine hello nel set di dati di hello sink. Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestazioni e ottimizzazione
toolearn sui fattori di hello che influiscono sulle prestazioni delle attività di copia e la modalità toooptimize, vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md) articolo.
