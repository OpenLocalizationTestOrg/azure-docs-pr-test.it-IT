---
title: aaaCopy dati da e verso un file system utilizzando Data Factory di Azure | Documenti Microsoft
description: Informazioni su come toocopy tooand di dati da un sistema di file locale con Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Copiare tooand dati da un file system locale usando Azure Data Factory
Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toocopy a/da un file system locale. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

## <a name="supported-scenarios"></a>Scenari supportati
È possibile copiare dati **da un file system locale** toohello archivi dati seguenti:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

È possibile copiare dati da archivi dati seguenti hello **tooan locale sistema file**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Attività di copia non elimina i file di origine hello dopo che è la destinazione toohello copiati correttamente. Se è necessario toodelete file di origine hello dopo una copia ha esito positivo, creare un file di hello toodelete di attività personalizzata e utilizzare attività hello nella pipeline hello. 

## <a name="enabling-connectivity"></a>Abilitazione della connettività
Data Factory supporta tooand connessione da un file di sistema locale tramite **Gateway di gestione dati**. Nell'ambiente locale per hello Data Factory servizio tooconnect tooany supportate in locale archivio dati incluso il file system, è necessario installare hello Gateway di gestione dati. toolearn sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione di gateway di hello, vedere [spostare dati tra origini locali e cloud hello con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md). Oltre ai Gateway di gestione dati, nessun altro file binario necessario tooand toocommunicate toobe installato da un file system locale. È necessario installare e utilizzare hello Gateway di gestione dati, anche se hello file system sia in Azure IaaS con macchina virtuale. Per informazioni dettagliate sul gateway hello, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md).

installare una condivisione di file di Linux, toouse [Samba](https://www.samba.org/) sul server Linux e installare il Gateway di gestione di dati in un server Windows. L'installazione di un Gateway di gestione dati su un server Linux non è supportata.

## <a name="getting-started"></a>Introduzione
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un file system usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare una **data factory**. Una data factory può contenere una o più pipeline. 
2. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory. Ad esempio, se si copiano dati da un file system locale di blob di Azure storage tooan, creerai due servizi collegati toolink il locale file system e data factory tooyour account di archiviazione di Azure. Per le proprietà di servizio collegato che sono tooan specifico nel file sistema locale, vedere [servizio proprietà collegate](#linked-service-properties) sezione.
3. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello. E si crea un altro set di dati toospecify hello cartella e il nome (facoltativo) nel file system. Per le proprietà di set di dati specifici tooon locale del file system, vedere [proprietà set di dati](#dataset-properties) sezione.
4. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e FileSystemSink come sink per attività di copia hello. Analogamente, se si sta copiando tooAzure di sistema di file locale nell'archiviazione Blob, utilizzare FileSystemSource e BlobSink nell'attività di copia hello. Per le proprietà di attività di copia locale tooon specifico del file system, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione. Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un file system, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-file-system) sezione di questo articolo.

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON dal sistema utilizzati toodefine Data Factory entità toofile specifico:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
È possibile collegare una locale file system tooan data factory di Azure con hello **Server File locale** servizio collegato. Hello nella tabella seguente vengono fornite descrizioni per gli elementi JSON toohello specifico servizio locale di File Server collegato.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |Verificare che la proprietà di tipo hello sia impostata troppo**OnPremisesFileServer**. |Sì |
| host |Specifica il percorso radice hello della cartella hello che si desidera toocopy. Utilizzare il carattere di escape hello ' \ ' per i caratteri speciali nella stringa hello. Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) . |Sì |
| userid |Specificare ID utente hello con server di accesso toohello hello. |No (se si sceglie encryptedCredential) |
| password |Specificare la password hello per utente hello (userid). |No (se si sceglie encryptedCredential) |
| encryptedCredential |Specificare le credenziali crittografato hello che è possibile ottenere eseguendo il cmdlet New-AzureRmDataFactoryEncryptValue hello. |No (se si sceglie toospecify userid e password in testo normale) |
| gatewayName |Specifica il nome di hello del gateway hello che Data Factory deve usare tooconnect toohello ai file server locali. |Sì |


### <a name="sample-linked-service-and-dataset-definitions"></a>Servizio collegato di esempio e definizioni del set di dati
| Scenario | Host nella definizione del servizio collegato | folderPath nella definizione del set di dati |
| --- | --- | --- |
| Cartella locale nel computer del gateway di gestione dati:  <br/><br/>Esempi: D:\\\* o D:\cartella\sottocartella\\* |D:\\\\ (per Gateway di gestione dati versione 2.0 e successive) <br/><br/> localhost (per le versioni precedenti alla versione 2.0 di Gateway di gestione dati) |.\\\\ o cartella\\\\sottocartella (per Gateway di gestione dati 2.0 e versioni successive) <br/><br/>D:\\\\ o D:\\\\cartella\\\\sottocartella (per la versione del gateway precedente a 2.0) |
| Cartella condivisa remota:  <br/><br/>Esempi: \\\\myserver\\share\\\* o \\\\myserver\\share\\cartella\\sottocartella\\* |\\\\\\\\myserver\\\\share |.\\\\ o cartella\\\\sottocartella |


### <a name="example-using-username-and-password-in-plain-text"></a>Esempio: Uso di nome utente e password in testo normale

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Esempio: Uso di encryptedcredential

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo [Creazione di set di dati](data-factory-create-datasets.md). Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.

sezione typeProperties Hello è diverso per ogni tipo di set di dati. Fornisce informazioni quali il percorso di hello e il formato dei dati di hello nell'archivio dati hello. Hello typeProperties sezione hello set di dati di tipo **FileShare** ha hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Specifica hello sottopercorso toohello cartella. Utilizzare il carattere di escape hello ' \' per i caratteri speciali nella stringa hello. Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .<br/><br/>È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora. |Sì |
| fileName |Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello. Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.<br/><br/>Quando **fileName** non viene specificato per un set di dati di output e **preserveHierarchy** viene omesso in sink di attività, hello nome del file hello generato è hello seguente formato: <br/><br/>`Data.<Guid>.txt` Esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file. <br/><br/>I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).<br/><br/>Esempio 1: "fileFilter": "*. log"<br/>Esempio 2: "fileFilter": 2014 - 1-?. txt"<br/><br/>Si noti che fileFilter è applicabile per un set di dati di input FileShare. |No |
| partitionedBy |È possibile utilizzare partitionedBy toospecify dinamica folderPath/nome di file per i dati delle serie temporali. Un esempio è folderPath con parametri per ogni ora di dati. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

> [!NOTE]
> Non è possibile usare fileName e fileFilter contemporaneamente.

### <a name="using-partitionedby-property"></a>Uso della proprietà partitionedBy
Come indicato nella sezione precedente di hello, è possibile specificare un folderPath dinamico e il nome di dati della serie temporale con hello **partitionedBy** proprietà [funzioni di Data Factory e le variabili di sistema hello](data-factory-functions-variables.md).

toounderstand ulteriori informazioni sul set di dati di serie temporali, la pianificazione e le sezioni, vedere [creazione dei DataSet](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md), e [creazione di pipeline](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Esempio 1.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

In questo esempio, {Slice} viene sostituito con il valore di hello della variabile sistema hello Data Factory SliceStart nel formato hello (YYYYMMDDHH). SliceStart fa riferimento all'ora toostart sezione hello. Hello folderPath è diversa per ogni sezione. Ad esempio: wikisampledataout/wikidatagateway/2014100103 o wikisampledataout/wikidatagateway/2014100104.

#### <a name="sample-2"></a>Esempio 2:

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

In questo esempio, anno, mese, giorno e ora della proprietà SliceStart vengono estratti in variabili distinte che utilizzano proprietà folderPath e fileName hello.

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività. Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.

Per attività di copia, variano a seconda dei tipi di hello di origini e sink. Se si stanno spostando i dati da un file system locale, impostare il tipo di origine hello nell'attività di copia hello troppo**FileSystemSource**. Analogamente, se si spostano dati tooan locale del file system, impostare il tipo di sink hello in attività di copia hello troppo**FileSystemSink**. Questa sezione presenta un elenco delle proprietà supportate da FileSystemSource e FileSystemSink.

**FileSystemSource** supporta hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dalle sottocartelle di hello o solo dalla cartella specificata hello. |True, False (valore predefinito) |No |

**FileSystemSink** supporta hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| copyBehavior |Definisce il comportamento di copia hello quando origine hello è BlobSource o file System. |**PreserveHierarchy:** mantiene la gerarchia di file hello nella cartella di destinazione hello. Percorso relativo di hello hello origine toohello origine della cartella dei file, ovvero è hello come percorso relativo di hello hello file toohello destinazione della cartella di destinazione.<br/><br/>**FlattenHierarchy:** tutti i file dalla cartella di origine hello vengono creati nel primo livello di hello della cartella di destinazione. file di destinazione Hello vengono creati con un nome generato automaticamente.<br/><br/>**Oggetto:** unisce tutti i file dal file tooone cartella di origine hello. Se viene specificato nome di nome/blob file hello, nome di file uniti hello è nome specificato hello. In caso contrario, verrà usato un nome file generato automaticamente. |No |

### <a name="recursive-and-copybehavior-examples"></a>esempi ricorsivi e copyBehavior
In questa sezione viene descritto il comportamento risultante hello dell'operazione di copia hello per diverse combinazioni di valori per le proprietà ricorsiva e copyBehavior hello.

| valore ricorsivo | valore di copyBehavior | Comportamento risultante |
| --- | --- | --- |
| true |preserveHierarchy |Per una cartella di origine Cartella1 con hello seguente struttura,<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>cartella di destinazione Hello Cartella1 viene creata con hello stessa struttura come origine di hello:<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5 |
| true |flattenHierarchy |Per una cartella di origine Cartella1 con hello seguente struttura,<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>destinazione Hello Cartella1 viene creata con hello seguente struttura: <br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File5 |
| true |mergeFiles |Per una cartella di origine Cartella1 con hello seguente struttura,<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>destinazione Hello Cartella1 viene creata con hello seguente struttura: <br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 + File3 + File4 + File 5 viene unito in un file con nome generato automaticamente. |
| false |preserveHierarchy |Per una cartella di origine Cartella1 con hello seguente struttura,<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura:<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/>La sottocartella1 con File3, File4 e File5 non viene considerata. |
| false |flattenHierarchy |Per una cartella di origine Cartella1 con hello seguente struttura,<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura:<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2<br/><br/>La sottocartella1 con File3, File4 e File5 non viene considerata. |
| false |mergeFiles |Per una cartella di origine Cartella1 con hello seguente struttura,<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura:<br/><br/>Cartella1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 viene unito in un file con un nome file generato automaticamente.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1<br/><br/>La sottocartella1 con File3, File4 e File5 non viene considerata. |

## <a name="supported-file-and-compression-formats"></a>Formati di file e di compressione supportati
Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>Esempi JSON per la copia dei dati tooand dal file system
Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Vengono visualizzate come toocopy tooand di dati da un file system in locale e l'archiviazione Blob di Azure. Tuttavia, è possibile copiare dati *direttamente* da qualsiasi hello origini tooany di sink hello elencati in [origini e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tramite attività di copia in Azure Data Factory.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Esempio: Copiare i dati da un tooAzure di sistema di file locale nell'archiviazione Blob
Questo esempio viene illustrato come dati toocopy tooAzure di sistema un file locale nell'archiviazione Blob. esempio Hello è hello entità Data Factory di seguito:

* Un servizio collegato di tipo [OnPremisesFileServer](#linked-service-properties).
* Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).
* Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Dopo l'esempio Hello copia dati delle serie temporali da tooAzure di sistema un file locale nell'archiviazione Blob ogni ora. le proprietà JSON Hello utilizzati in questi esempi vengono descritte nelle sezioni hello dopo gli esempi di hello.

Come primo passaggio, configurare il Gateway di gestione dati in base alle istruzioni hello [spostare dati tra origini locali e cloud hello con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).

**Servizio collegato del file server locale:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

È consigliabile utilizzare hello **encryptedCredential** proprietà hello invece **userid** e **password** proprietà. Per informazioni dettagliate su questo servizio collegato, vedere l'articolo relativo al [servizio collegato del file server](#linked-service-properties).

**Servizio collegato Archiviazione di Azure:**

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

**Set di dati di input del file system locale:**

I dati vengono prelevati da un nuovo file ogni ora. Hello folderPath e fileName proprietà sono determinate in base a ora di inizio hello della sezione hello.  

Impostazione `"external": "true"` informa Data Factory di set di dati hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**Set di dati di ouput di Archiviazione BLOB di Azure**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ora hello hello ora di inizio.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource**, e **sink** tipo è stato impostato troppo**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Esempio: Copia i dati dal Database SQL di Azure tooan locale file system
Hello nel seguente esempio viene illustrato:

* Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
* Un servizio collegato di tipo [OnPremisesFileServer](#linked-service-properties).
* Un set di dati di input di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Un set di dati di output di tipo [FileShare](#dataset-properties).
* Una pipeline con attività di copia che usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) e [FileSystemSink](#copy-activity-properties).

esempio Hello copia dati delle serie temporali da un file system locale di SQL Azure tabella tooan ogni ora. le proprietà JSON Hello utilizzati in questi esempi sono descritti nelle sezioni dopo gli esempi di hello.

**Servizio collegato per il database SQL Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

**Servizio collegato del file server locale:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

È consigliabile utilizzare hello **encryptedCredential** proprietà anziché hello **userid** e **password** proprietà. Per informazioni dettagliate su questo servizio collegato, vedere l'articolo relativo al [servizio collegato del file system](#linked-service-properties).

**Set di dati di input SQL Azure:**

esempio Hello presuppone che si crea una tabella "MyTable" in SQL Azure e che contiene una colonna denominata "timestampcolumn" per i dati delle serie temporali.

Impostazione ``“external”: ”true”`` informa Data Factory di set di dati hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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

**Set di dati di output del file system locale:**

Dati viene copiato tooa nuovo file ogni ora. folderPath Hello e il nome di blob hello vengono determinate in base all'ora di inizio hello del sezione hello.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**Un'attività di copia in una pipeline con un'origine SQL e un sink di file system:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource**, hello e **sink** tipo è stato impostato troppo**FileSystemSink**. query SQL Hello specificato per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


È anche possibile mappare le colonne di origine toocolumns di set di dati dal set di dati di sink nella definizione di attività di copia hello. Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestazioni e ottimizzazione
 toolearn sulla chiave di fattori che influiscono sulle prestazioni di hello spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize, vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md).
