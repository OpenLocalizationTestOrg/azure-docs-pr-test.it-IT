---
title: aaaCopy dati in o dall'archiviazione Blob di Azure | Documenti Microsoft
description: 'Informazioni su come toocopy blob di dati in Azure Data Factory. Usare questo esempio: come toocopy tooand di dati dall''archiviazione Blob di Azure e Database SQL di Azure.'
keywords: dati blob, copia di blob di azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Copia dati tooor dall'archiviazione Blob di Azure usando Azure Data Factory
Questo articolo spiega come toouse hello attività di copia in Azure Data Factory toocopy dati tooand dall'archiviazione Blob di Azure. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

## <a name="overview"></a>Panoramica
È possibile copiare dati da qualsiasi origine supportati dati tooAzure nell'archiviazione Blob di archiviazione o da dati di archiviazione Blob di Azure supportata tooany sink archivio. Hello nella tabella seguente fornisce un elenco di archivi dati supportata come origini o sink dall'attività di copia hello. È ad esempio possibile spostare dati **da** un database di SQL Server o un database SQL di Azure **a** una risorsa di archiviazione BLOB di Azure. È anche possibile copiare dati **da** Archiviazione BLOB di Azure **a** un'istanza di Azure SQL Data Warehouse o una raccolta Azure Cosmos DB. 

## <a name="supported-scenarios"></a>Scenari supportati
È possibile copiare dati **dall'archiviazione Blob di Azure** toohello archivi dati seguenti:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

È possibile copiare dati da archivi dati seguenti hello **tooAzure nell'archiviazione Blob**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Supporta la copia dei dati da attività di copia / tooboth account generici di archiviazione di Azure e a caldo/raffreddare nell'archiviazione Blob. supporta attività Hello **letto dal blocco, Accodamento o BLOB di pagine**, ma supporta **scrittura BLOB in blocchi tooonly**. Archiviazione Premium di Azure non è supportata come sink poiché si basa sui BLOB di pagine.
> 
> Attività di copia non elimina dati dall'origine hello dopo hello dati vengono correttamente copiati toohello destinazione. Se sono necessari dati di origine toodelete dopo una copia ha esito positivo, creare un [attività personalizzata](data-factory-use-custom-activities.md) toodelete hello dati e utilizzare attività hello nella pipeline hello. Per un esempio, vedere hello [esempio blob o una cartella di eliminazione in GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a>Attività iniziali
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un archivio BLOB di Azure usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. In questo articolo ha un [procedura dettagliata](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) per la creazione di una pipeline toocopy dati da un tooanother di percorso di archiviazione Blob di Azure il percorso di archiviazione Blob di Azure. Per un'esercitazione sulla creazione di una pipeline toocopy dati da un Database SQL di tooAzure di archiviazione Blob di Azure, vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md).

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare una **data factory**. Una data factory può contenere una o più pipeline. 
2. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory. Ad esempio, se si copiano dati da un database di SQL Azure tooan di archiviazione blob di Azure, è creare due servizi collegati toolink l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour. Per le proprietà di servizio collegato che sono tooAzure specifico nell'archiviazione Blob, vedere [servizio proprietà collegate](#linked-service-properties) sezione. 
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello. E, alla creazione di un altro set di dati toospecify hello SQL nella tabella nel database di SQL Azure hello che contiene dati hello copiati dall'archiviazione blob hello. Per le proprietà di set di dati che sono tooAzure specifico nell'archiviazione Blob, vedere [proprietà set di dati](#dataset-properties) sezione.
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e di SqlSink come sink per attività di copia hello. Analogamente, se si sta copiando tooAzure Database SQL di Azure nell'archiviazione Blob, utilizzare SqlSource e BlobSink nell'attività di copia hello. Per le proprietà di attività di copia che sono tooAzure specifico nell'archiviazione Blob, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione. Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.  

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un archivio Blob di Azure, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) sezione di questo articolo.

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure nell'archiviazione Blob.

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Esistono due tipi di servizi collegati è possibile utilizzare toolink un servizio di archiviazione Azure tooan data factory di Azure. I due tipi di servizi sono il servizio collegato **AzureStorage** e il servizio collegato **AzureStorageSas**. Hello servizio collegato di archiviazione di Azure fornisce data factory di hello con accesso globale toohello di archiviazione di Azure. Mentre, hello Azure archiviazione SAS (firma di accesso condiviso) collegati servizio fornisce data factory di hello con accesso limitato/scadenza toohello di archiviazione di Azure. Non esistono altre differenze tra questi due servizi collegati. Scegliere servizio hello collegato alle proprie esigenze. Hello nelle sezioni seguenti vengono forniscono ulteriori informazioni su questi due servizi collegati.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Proprietà dei set di dati
toospecify toorepresent un set di dati dati di input o outpui in un archivio Blob di Azure, impostare proprietà di tipo hello del set di dati hello: **AzureBlob**. Set hello **linkedServiceName** servizio collegato di proprietà del nome di toohello hello set di dati di hello SAS di archiviazione di Azure o di archiviazione di Azure.  proprietà del tipo di set di dati hello Hello specificare hello **contenitore blob** hello e **cartella** nell'archiviazione blob hello.

Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni di JSON, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Data factory di supporta hello seguente i valori di tipo basata su .NET conformi a CLS per fornire informazioni sul tipo di "struttura" per le origini dati in lettura-schema come blob di Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan. Data Factory esegue automaticamente le conversioni di tipo quando si spostano dati da un'origine tooa archiviano dati sink.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e vengono fornite informazioni sulla posizione di hello, formattare e così via, dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per set di dati di tipo **AzureBlob** set di dati è hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Percorso toohello contenitore e della cartella nell'archiviazione blob hello. Esempio: myblobcontainer\myblobfolder\ |Sì |
| fileName |Nome del blob hello. fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole.<br/><br/>Se si specifica un nome di file, hello attività (incluso copia) funziona su hello Blob specifico.<br/><br/>Quando non è stato specificato il nome del file, copia include tutti i BLOB in folderPath hello per input set di dati.<br/><br/>Quando **fileName** non viene specificato per un set di dati di output e **preserveHierarchy** non è specificato nel sink di attività, hello nome del file hello generato potrebbe essere in hello segue questo formato: dati.<Guid>. txt (ad esempio:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| partitionedBy |partitionedBy è una proprietà facoltativa. È possibile utilizzare è toospecify un dinamica folderPath e filename per dati della serie temporale. Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath. Vedere hello [utilizzando sezione proprietà partitionedBy](#using-partitionedBy-property) per informazioni dettagliate ed esempi. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

### <a name="using-partitionedby-property"></a>Uso della proprietà partitionedBy
Come indicato nella sezione precedente di hello, è possibile specificare un folderPath dinamico e il nome di dati della serie temporale con hello **partitionedBy** proprietà [funzioni di Data Factory e le variabili di sistema hello](data-factory-functions-variables.md).

Per maggiori informazioni sui set di dati delle serie temporali, sulla pianificazione e sulle sezioni, leggere gli articoli [Creazione di set di dati](data-factory-create-datasets.md) e [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).

#### <a name="sample-1"></a>Esempio 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

In questo esempio, {Slice} viene sostituito con valore hello della variabile di sistema di Data Factory SliceStart nel formato hello (YYYYMMDDHH) specificato. Hello SliceStart fa riferimento l'ora toostart sezione hello. Hello folderPath è diversa per ogni sezione. For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104

#### <a name="sample-2"></a>Esempio 2

```json
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

In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività. Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink. Se si spostano dati da un archivio Blob di Azure, impostare il tipo di origine di hello nell'attività di copia hello troppo**BlobSource**. Analogamente, se si stanno spostando i dati tooan archiviazione Blob di Azure, impostare il tipo di sink hello nell'attività di copia hello troppo**BlobSink**. Questa sezione presenta un elenco delle proprietà supportate da BlobSource e BlobSink.

**BlobSource** supporta hello seguenti proprietà in hello **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello. |True (valore predefinito), False |No |

**BlobSink** supporta le proprietà seguenti hello **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| copyBehavior |Definisce il comportamento di copia hello quando origine hello è BlobSource o file System. |<b>PreserveHierarchy</b>: mantiene hello gerarchia del file nella cartella di destinazione hello. percorso relativo di Hello origine toosource della cartella dei file è identico toohello percorso relativo della cartella tootarget file di destinazione.<br/><br/><b>FlattenHierarchy</b>: tutti i file dalla cartella di origine hello presenti hello primo livelli della cartella di destinazione. i file di destinazione Hello hanno nome generato automaticamente. <br/><br/><b>Oggetto</b>: unisce tutti i file dal file tooone cartella di origine hello. Se viene specificato il nome di File/Blob hello, il nome di file sottoposto a merge hello sarebbe nome specificato hello. in caso contrario, potrebbe essere il nome file generato automaticamente. |No |

**BlobSource** supporta anche le due proprietà seguenti per la compatibilità con le versioni precedenti.

* **treatEmptyAsNull**: Specifica se tootreat una stringa vuota o null come valore null.
* **skipHeaderLineCount** : specifica il numero di righe che devono essere ignorate. È applicabile solo quando il set di dati di input usa TextFormat.

Analogamente, **BlobSink** supporta hello seguenti proprietà per la compatibilità con le versioni precedenti.

* **blobWriterAddHeader**: Specifica se un'intestazione di definizioni di colonna durante la scrittura tooan tooadd set di dati di output.

Stessa funzionalità di hello hello supporto ora di set di dati seguenti proprietà che implementano: **treatEmptyAsNull**, **skipLineCount**, **prima riga come intestazione**.

Hello nella tabella seguente fornisce informazioni aggiuntive sull'utilizzo delle proprietà dei set di dati al posto di queste proprietà di origine/sink blob nuovo hello.

| Proprietà dell'attività di copia | Proprietà del set di dati |
|:--- |:--- |
| skipHeaderLineCount in BlobSource |skipLineCount e firstRowAsHeader. Le righe vengono ignorate prima e quindi di lettura di hello prima della riga come intestazione. |
| treatEmptyAsNull in BlobSource |treatEmptyAsNull nel set di dati di input |
| blobWriterAddHeader in BlobSink |firstRowAsHeader nel set di dati di output |

Per informazioni dettagliate su queste proprietà, vedere la sezione [Specifica di TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) .    

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

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>Procedura dettagliata: Utilizzare Copia guidata toocopy dati da e verso l'archiviazione Blob
Esaminare la modalità di archiviazione blob tooquickly copia dati da e verso un Azure. In questa procedura dettagliata gli archivi dati sia di origine che di destinazione sono di tipo archivio BLOB di Azure. Hello pipeline in questa procedura dettagliata consente di copiare dati da una cartella tooanother cartella hello stesso contenitore di blob. Questa procedura dettagliata è intenzionalmente semplice tooshow impostazioni o proprietà quando si utilizza l'archiviazione Blob come origine o sink. 

### <a name="prerequisites"></a>Prerequisiti
1. Creare un **account di archiviazione di Azure** per utilizzo generico, se necessario. Usare l'archiviazione blob hello sia **origine** e **destinazione** archivio dati in questa procedura dettagliata. Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo per passaggi toocreate uno.
2. Creare un contenitore blob denominato **adfblobconnector** nell'account di archiviazione hello. 
4. Creare una cartella denominata **input** in hello **adfblobconnector** contenitore.
5. Creare un file denominato **emp.txt** con hello dopo il contenuto e caricarla toohello **input** cartella tramite strumenti [Esplora archivi Azure](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Creare hello data factory
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **+ nuovo** dall'angolo superiore sinistro di hello, fare clic su **Intelligence + analitica**, fare clic su **Data Factory**.
3. In hello **nuova data factory** pannello:   
    1. Immettere **ADFBlobConnectorDF** per hello **nome**. nome Hello di hello Azure data factory deve essere globalmente univoco. Se viene visualizzato l'errore hello: `*Data factory name “ADFBlobConnectorDF” is not available`, modificare il nome di hello di hello data factory (ad esempio, yournameADFBlobConnectorDF) e provare a creare di nuovo. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .
    2. Selezionare la **sottoscrizione**di Azure.
    3. Per il gruppo di risorse, selezionare **Usa esistente** tooselect un esistente risorsa gruppo (o) selezionare **Crea nuovo** tooenter un nome per un gruppo di risorse.
    4. Selezionare un **percorso** per data factory di hello.
    5. Selezionare **toodashboard Pin** casella di controllo nella parte inferiore di hello del pannello hello.
    6. Fare clic su **Crea**.
3. Una volta completata la creazione di hello, vedrai hello **Data Factory** pannello, come illustrato nella seguente immagine hello: ![home page di Data factory](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>Copia guidata
1. Nella home page di hello Data Factory, fare clic su hello **copia dei dati [anteprima]** riquadro toolaunch **copia dati guidata** in una scheda separata.    
    
    > [!NOTE]
    >    Se viene visualizzato il browser web hello è bloccata su "Autorizzazione …", disabilitare o deselezionare **bloccare i cookie di terze parti e i dati del sito** (oppure) mantenere abilitato e creare un'eccezione per **login.microsoftonline.com**e quindi provare ad avviare la procedura guidata hello nuovamente.
2. In hello **proprietà** pagina:
    1. Immettere **CopyPipeline** in **Nome attività**. Nome attività Hello è hello della pipeline hello nella data factory.
    2. Immettere un **descrizione** per attività hello (facoltativo).
    3. Per **ritmo di attività o l'utilità di pianificazione**, mantenere hello **esecuzione a intervalli regolari su pianificazione** opzione. Se si desidera toorun questa attività una sola volta anziché eseguire ripetutamente una pianificazione, selezionare **Esegui una volta**. Se si seleziona l'opzione **Run once now** (Esegui una volta ora), viene creata una [pipeline con esecuzione singola](data-factory-create-pipelines.md#onetime-pipeline). 
    4. Mantenere le impostazioni di hello per **periodica modello**. Questa attività viene eseguito ogni giorno tra hello iniziare e termina volte è specificata al passaggio successivo di hello.
    5. Hello modifica **data ora di inizio** troppo**21/04/2017**. 
    6. Hello modifica **data e ora fine** troppo**25/04/2017**. È opportuno data hello tootype invece di dover passare attraverso il calendario hello.     
    8. Fare clic su **Avanti**.
      ![Strumento di copia - Pagina Proprietà](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. In hello **archivio dati di origine** pagina, fare clic su **archiviazione Blob di Azure** riquadro. Usare l'archivio dati di origine di pagina toospecify hello per attività di copia hello. È possibile usare un servizio collegato di archivio dati esistente oppure specificare un nuovo archivio dati. servizio collegato toouse esistente, selezionare **da servizi esistenti collegati** e selezionare hello destra servizio collegato. 
    ![Strumento di copia - Pagina Archivio dati di origine](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. In hello **specificare account di archiviazione Blob di Azure hello** pagina:
   1. Nome generato automaticamente hello per mantenere **nome connessione**. nome della connessione Hello è il nome di hello del servizio di hello collegato di tipo: archiviazione di Azure. 
   2. Verificare che in **Account selection method** (Metodo di selezione dell'account) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).
   3. Selezionare la sottoscrizione di Azure o mantenere **Seleziona tutte** per **Sottoscrizione di Azure**.   
   4. Selezionare un **account di archiviazione Azure** da hello account disponibile nella sottoscrizione selezionata hello l'elenco di archiviazione di Azure. È anche possibile scegliere tooenter impostazioni dell'account di archiviazione manualmente selezionando **immettere manualmente** opzione per hello **metodo di selezione dell'Account**.
   5. Fare clic su **Avanti**. 
      ![Strumento Copia: specificare l'account di archiviazione Blob di Azure hello](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. In **cartella o file di input hello scegliere** pagina:
   1. Fare doppio clic su **adfblobcontainer**.
   2. Selezionare **input** e fare clic su **Scegli**. In questa procedura dettagliata, si seleziona una cartella di input hello. È anche possibile selezionare file emp.txt hello nella cartella hello invece. 
      ![Strumento Copia - scegliere i file di input hello o cartella](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. In hello **cartella o file di input hello scegliere** pagina:
    1. Verificare che hello **file o cartella** è troppo**adfblobconnector/input**. Se il file hello si trovano in sottocartelle, ad esempio, 2017/04/01 2017/04/02 e così via, immettere adfblobconnector / / {year} / {month} / {day} per file o cartella. Quando si preme TAB dalla casella di testo hello, vengono visualizzati tre formati di tooselect elenchi a discesa per anno (aaaa), month (MM) e giorno (gg). 
    2. Non impostare **Copy file recursively** (Copia file in modo ricorsivo). Selezionare questo incrociato toorecursively opzione all'interno delle cartelle per i file toobe toohello copiato di destinazione. 
    3. Non hello **copia binaria** opzione. Selezionare questo tooperform opzione una copia binaria della destinazione toohello file di origine. Non selezionare per questa procedura dettagliata in modo che è possibile visualizzare altre opzioni nelle pagine successive hello. 
    4. Verificare che hello **tipo di compressione** è troppo**Nessuno**. Selezionare un valore per questa opzione se i file di origine vengono compressi in uno dei formati di hello è supportato. 
    5. Fare clic su **Avanti**.
    ![Strumento Copia - scegliere i file di input hello o cartella](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. In hello **impostazioni del File di formato** visualizzata delimitatori hello e lo schema di hello che viene rilevata automaticamente dalla procedura guidata hello mediante l'analisi di file hello. 
    1. Confermare le opzioni seguenti hello: una. Hello **formato** è troppo**formato testo**. È possibile visualizzare tutti i formati di hello è supportato nell'elenco a discesa hello. Ad esempio: JSON, Avro, ORC, Parquet.
        b. Hello **delimitatore di colonna** è troppo`Comma (,)`. È possibile visualizzare hello altri delimitatori di colonna nell'elenco a discesa hello è supportati da Data Factory. È anche possibile specificare un delimitatore personalizzato.
        c. Hello **delimitatore di riga** è troppo`Carriage Return + Line feed (\r\n)`. È possibile visualizzare hello altri delimitatori di riga nell'elenco a discesa hello è supportati da Data Factory. È anche possibile specificare un delimitatore personalizzato.
        d. Hello **ignorare conteggio delle righe** è troppo**0**. Se si desidera qualche toobe righe ignorate all'inizio di hello del file hello, immettere il numero di hello qui.
        e.  Hello **prima riga di dati contiene nomi di colonna** non è impostata. Se il file di origine hello contengono nomi di colonna nella prima riga hello, selezionare questa opzione.
        f. Hello **considerare il valore di colonna vuota come null** opzione è impostata.
    2. Espandere **impostazioni avanzate** toosee disponibili opzioni avanzate.
    3. Nella parte inferiore di hello della pagina hello, vedere hello **anteprima** di dati da file emp.txt hello.
    4. Fare clic su **SCHEMA** scheda in schema di hello inferiore toosee hello tale procedura guidata copia hello dedotto osservando i dati di hello nel file di origine hello.
    5. Fare clic su **Avanti** dopo aver esaminato i delimitatori di hello e anteprima dei dati.
    ![Strumento di copia - Impostazioni di formattazioni del file](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. In hello **memorizzazione di dati di destinazione della pagina**selezionare **archiviazione Blob di Azure**, fare clic su **Avanti**. Si utilizza hello archiviazione Blob di Azure come entrambi hello origine e destinazione gli archivi dati in questa procedura dettagliata.    
    ![Strumento di copia - Selezionare l'archivio dati di destinazione](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. In **specificare account di archiviazione Blob di Azure hello** pagina:
   1. Immettere **AzureStorageLinkedService** per hello **nome connessione** campo.
   2. Verificare che in **Account selection method** (Metodo di selezione dell'account) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).
   3. Selezionare la **sottoscrizione**di Azure.  
   4. Selezionare l'account di archiviazione di Azure. 
   5. Fare clic su **Avanti**.     
10. In hello **hello Scegli file o una cartella di output** pagina: 
    6. In **Percorso cartella** specificare **adfblobconnector/output/{year}/{month}/{day}** (adfblobconnector/output/{anno}/{mese}/{giorno}). Premere **TAB**.
    7. Per hello **anno**selezionare **aaaa**.
    8. Per hello **mese**, verificare che sia impostato troppo**MM**.
    9. Per hello **giorno**, verificare che sia impostato troppo**gg**.
    10. Verificare che hello **tipo di compressione** è troppo**Nessuno**.
    11. Verificare che hello **copiare comportamento** è troppo**unire file**. Se l'output di hello file con hello stesso nome esiste già, hello nuovo contenuto è toohello aggiunto lo stesso file alla fine di hello.
    12. Fare clic su **Avanti**.
    ![Strumento di copia - Scegliere il file o la cartella di output](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. In hello **impostazioni del File di formato** pagina, rivedere le impostazioni di hello e fare clic su **Avanti**. Una delle opzioni aggiuntive di hello qui è un file di output intestazione toohello tooadd. Se si seleziona questa opzione, viene aggiunta una riga di intestazione con nomi di colonne hello dallo schema hello dell'origine hello. È possibile rinominare i nomi di colonna predefiniti hello durante la visualizzazione schema hello hello origine. Ad esempio, è possibile modificare hello prima colonna tooFirst nome e secondo tooLast colonna nome. Quindi, viene generato il file di output di hello con un'intestazione con questi nomi come nomi di colonna. 
    ![Strumento di copia - Impostazioni di formatto file per la destinazione](media/data-factory-azure-blob-connector/file-format-destination.png)
12. In hello **le impostazioni delle prestazioni** pagina, verificare che **cloud unità** e **parallela copie** sono troppo**automatica**, fare clic su Avanti. Per informazioni dettagliate su queste impostazioni, vedere [Guida alle prestazioni dell'attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md#parallel-copy).
    ![Strumento di copia - Impostazioni relative alle prestazioni](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. In hello **riepilogo** pagina, esaminare tutte le impostazioni di protezione (le proprietà dell'attività, le impostazioni per l'origine e di destinazione e le impostazioni di copia) e fare clic su **Avanti**.
    ![Strumento di copia - Pagina Riepilogo](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Esaminare le informazioni nella hello **riepilogo** pagina e fare clic su **fine**. procedura guidata di Hello crea due servizi collegati, due set di dati (input e output) e una pipeline in data factory di hello (dalla quale è stata avviata la procedura guidata copia hello).
    ![Strumento di copia - Pagina di distribuzione](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>Pipeline di hello monitoraggio (attività di copia)

1. Fare clic sul collegamento hello `Click here toomonitor copy pipeline` su hello **distribuzione** pagina. 
2. Dovrebbe essere hello **monitorare e gestire applicazioni** in una scheda separata.  ![App Monitoraggio e gestione](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. Hello modifica **avviare** tempo nella parte superiore di hello troppo`04/19/2017` e **fine** troppo tempo`04/27/2017`, quindi fare clic su **applica**. 
4. Dovrebbe essere cinque le finestre attività in hello **attività WINDOWS** elenco. Hello **WindowStart** volte dovrebbero coprire tutti i giorni dall'ora di fine toopipeline di inizio della pipeline. 
5. Fare clic su **aggiornamento** pulsante per hello **attività WINDOWS** elenco più volte fino a visualizzare lo stato di hello di tutte le finestre attività hello è tooReady. 
6. A questo punto, verificare che nella cartella di output di hello del contenitore adfblobconnector vengono generati file di output di hello. È necessario visualizzare hello seguente struttura di cartelle nella cartella di output di hello: 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
Per informazioni dettagliate sul monitoraggio e la gestione delle data factory, vedere l'articolo [Monitorare e gestire le pipeline di Data Factory](data-factory-monitor-manage-app.md). 
 
### <a name="data-factory-entities"></a>Entità di Data factory
A questo punto, passare toohello back-scheda home page di hello Data Factory. Si noti che ora nella data factory sono presenti due servizi collegati, due set di dati e una pipeline. 

![Home page di Data Factory con entità](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

Fare clic su **autore e distribuire** toolaunch Editor delle Data Factory. 

![Editor di Data factory](media/data-factory-azure-blob-connector/data-factory-editor.png)

È necessario visualizzare hello dopo la data factory di entità Data Factory: 

 - Due servizi collegati, Uno per l'origine di hello e hello un'altra destinazione hello. Entrambi i servizi collegato hello vedere toohello stesso account di archiviazione di Azure in questa procedura dettagliata. 
 - Due set di dati, uno di input e uno di output. In questa procedura dettagliata, entrambi utilizzano hello stesso contenitore di blob, ma fare riferimento a cartelle toodifferent (input e output).
 - Una pipeline. pipeline Hello contiene un'attività di copia che utilizza un'origine blob e un blob sink toocopy di dati da un tooanother percorso blob di Azure percorso blob di Azure. 

Hello nelle sezioni seguenti vengono forniscono ulteriori informazioni su queste entità. 

#### <a name="linked-services"></a>Servizi collegati
Verranno visualizzati due servizi collegati, Uno per l'origine di hello e hello un'altra destinazione hello. In questa procedura dettagliata, entrambe le definizioni di aspetto hello stessa ad eccezione dei nomi hello. Hello **tipo** di hello servizio collegato è troppo**AzureStorage**. Proprietà più importante della definizione di servizio collegato hello è hello **connectionString**, che viene utilizzato da Data Factory tooconnect tooyour account di archiviazione di Azure in fase di esecuzione. Proprietà hubName hello nella definizione di hello ignorata. 

##### <a name="source-blob-storage-linked-service"></a>Servizio collegato di archiviazione BLOB di origine
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>Servizio collegato di archiviazione BLOB di destinazione

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Per altre informazioni sui servizi collegati di archiviazione di Azure, vedere la sezione [Proprietà del servizio collegato](#linked-service-properties). 

#### <a name="datasets"></a>Set di dati
Sono presenti due set di dati, uno di input e uno di output. tipo di Hello del set di dati hello è impostato troppo**AzureBlob** per entrambi. 

set di dati input Hello punta toohello **input** cartella di hello **adfblobconnector** contenitore blob. Hello **esterno** impostata troppo**true** per questo set di dati come hello dati non viene generati dalla pipeline hello con attività di copia hello che accetta questo set di dati come input. 

toohello punti set di dati di output di Hello **output** cartella di hello stesso contenitore di blob. Hello set di dati di output utilizza inoltre hello anno, mese e giorno di hello **SliceStart** toodynamically variabile di sistema valutare hello percorso hello file di output. Per un elenco di funzioni e variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md). Hello **esterno** impostata troppo**false** (valore predefinito) perché questo set di dati viene generato dalla pipeline hello. 

Per altre informazioni sulle proprietà supportate dal set di dati del BLOB di Azure, vedere la sezione [Proprietà dei set di dati](#dataset-properties).

##### <a name="input-dataset"></a>Set di dati di input

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>Set di dati di output

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>Pipeline
pipeline Hello è semplicemente un'attività. Hello **tipo** di hello attività è troppo**copia**.  In proprietà del tipo hello per attività hello, sono presenti due sezioni, una per l'origine e di hello un'altra per il sink. tipo di origine Hello è troppo**BlobSource** come attività hello sta copiando i dati da un'archiviazione blob. Hello il tipo di sink è impostato troppo**BlobSink** come attività hello la copia di archiviazione blob di dati tooa. attività di copia Hello accetta InputDataset z4y come input hello e OutputDataset-z4y come output di hello. 

Per altre informazioni sulle proprietà supportate da BlobSource e BlobSink, vedere la sezione [Proprietà dell'attività di copia](#copy-activity-properties). 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>Esempi JSON per la copia dei dati tooand dall'archiviazione Blob  
Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Vengono visualizzate come toocopy tooand di dati dall'archiviazione Blob di Azure e Database SQL di Azure. Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>Esempio JSON: Copiare i dati da archiviazione Blob tooSQL Database
Hello nel seguente esempio viene illustrato:

1. Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](#copy-activity-properties) e [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).

esempio Hello copia i dati delle serie temporali da una tabella di SQL Azure tooan blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato SQL di Azure:**

```json
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
**Servizio collegato Archiviazione di Azure:**

```json
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
Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**. Per hello prima, specificare una stringa di connessione hello che include una chiave dell'account di hello e per la versione più recente di hello, specificare hello Uri di firma di accesso condiviso (SAS). Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .  

**Set di dati di input del BLOB di Azure:**

I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1). Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio. "external": "true" impostazione informa Data Factory di tale tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
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
**Set di dati di output SQL Azure:**

esempio Hello copia tabella tooa dati denominata "MyTable" in un database SQL di Azure. Crea tabella hello nel database SQL di Azure con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello. Aggiunta di nuove righe nella tabella toohello ogni ora.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Un'attività di copia in una pipeline con un'origine BLOB e un sink SQL:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>Esempio JSON: Copiare i dati da SQL Azure tooAzure Blob
Hello nel seguente esempio viene illustrato:

1. Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) e [BlobSink](#copy-activity-properties).

esempio Hello copia i dati delle serie temporali da un tooan tabella SQL di Azure blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato SQL di Azure:**

```json
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
**Servizio collegato Archiviazione di Azure:**

```json
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
Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**. Per hello prima, specificare una stringa di connessione hello che include una chiave dell'account di hello e per la versione più recente di hello, specificare hello Uri di firma di accesso condiviso (SAS). Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .  

**Set di dati di input SQL Azure:**

esempio Hello presuppone di aver creato una tabella "MyTable" in SQL Azure e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.

L'impostazione "external": "true" informa il servizio Data Factory tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

```json
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

**Set di dati di output del BLOB di Azure:**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

**Un'attività di copia in una pipeline con un'origine SQL e un sink BLOB:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

> [!NOTE]
> colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
