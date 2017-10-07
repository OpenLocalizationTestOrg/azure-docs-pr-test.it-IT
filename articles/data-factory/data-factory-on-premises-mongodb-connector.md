---
title: dati aaaMove MongoDB mediante Data Factory | Documenti Microsoft
description: Informazioni su come dati toomove MongoDB database usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Spostare i dati da MongoDB con Azure Data Factory
Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database di MongoDB locale. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

È possibile copiare dati da un archivio di dati di on-premise MongoDB dati archivio tooany supportati sink. Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. Data factory di attualmente supporta solo lo spostamento di dati da un MongoDB archiviano tooother archivi di dati, ma non per lo spostamento dei dati dall'archivio dati di MongoDB altri dati archivi tooan. 

## <a name="prerequisites"></a>Prerequisiti
Per hello Azure Data Factory servizio toobe tooconnect in grado di tooyour MongoDB database locale, è necessario installare hello seguenti componenti:

- Le versioni MongoDB supportate sono 2.4, 2.6, 3.0 e 3.2.
- Gateway di gestione di dati in hello nello stesso computer che ospita il database hello o tooavoid un computer separato competono per le risorse con i database di hello. Gateway di gestione dati è un software che si connette a servizi di toocloud origini dati locali in modo sicuro e gestito. Leggere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per i dettagli sul Gateway di gestione dati. Vedere [spostare i dati da on-premise toocloud](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate sulla configurazione di gateway hello una pipeline di dati toomove dati.

    Quando si installa il gateway di hello, viene automaticamente installato un tooMongoDB tooconnect di MongoDB Microsoft ODBC driver utilizzato.

    > [!NOTE]
    > È necessario toouse hello gateway tooconnect tooMongoDB anche se è ospitato in macchine virtuali IaaS di Azure. Se si sta tentando di istanza tooan tooconnect MongoDB ospitato nel cloud, è possibile installare anche l'istanza del gateway hello in hello VM IaaS.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un archivio dati MongoDB usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti: 

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati di MongoDB locale, vedere [esempio JSON: copiare i dati da tooAzure MongoDB Blob](#json-example-copy-data-from-mongodb-to-azure-blob) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che sono utilizzati toodefine Data Factory entità specifiche tooMongoDB origine:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello seguente tabella fornisce una descrizione per gli elementi JSON specifici troppo**OnPremisesMongoDB** servizio collegato.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **OnPremisesMongoDb** |Sì |
| server |IP il nome host o indirizzo del server di MongoDB hello. |Sì |
| port |La porta TCP che hello MongoDB server utilizza toolisten per le connessioni client. |Facoltativo, valore predefinito: 27017 |
| authenticationType |Di base o anonima. |Sì |
| username |Utente account tooaccess MongoDB. |Sì (se si usa l'autenticazione di base). |
| password |Password utente hello. |Sì (se si usa l'autenticazione di base). |
| authSource |Nome del database MongoDB hello che si desidera toouse toocheck le credenziali per l'autenticazione. |Facoltativo (se si usa l'autenticazione di base). impostazione predefinita: Usa l'account amministratore hello e database hello specificato utilizzando la proprietà databaseName. |
| databaseName |Nome del database MongoDB hello che si desidera tooaccess. |Sì |
| gatewayName |Nome del gateway hello che accede a hello archivio di dati. |Sì |
| encryptedCredential |Credenziali crittografate in base al gateway. |Facoltativo |

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per set di dati di tipo **MongoDbCollection** è hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| collectionName |Nome dell'insieme di hello nel database di MongoDB. |Sì |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Le proprietà disponibili nella hello **typeProperties** sezione di attività hello hello invece variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Quando origine hello è di tipo **MongoDbSource** hello le proprietà seguenti sono disponibile nella sezione typeProperties:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL-92. Ad esempio: selezionare * da MyTable. |No, se **collectionName** di **set di dati** è specificato |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>Esempio JSON: copiare i dati da tooAzure MongoDB Blob
In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Viene illustrato come toocopy dati da un tooan MongoDB locale archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

esempio Hello è hello entità factory di dati seguenti:

1. Un servizio collegato di tipo [OnPremisesMongoDb](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [MongoDbCollection](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [MongoDbSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da un risultato di query nell'oggetto blob tooa database MongoDB ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

Come primo passaggio, configurare il gateway di gestione dati hello in base alle istruzioni hello hello [Gateway di gestione dati](data-factory-data-management-gateway.md) articolo.

**Servizio collegato MongoDB:**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

**Servizio collegato Archiviazione di Azure:**

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Set di dati input MongoDB:** impostazione "external": "true" informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Set di dati di output del BLOB di Azure:**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Attività di copia in una pipeline con un'origine MongoDB e un sink BLOB:**

pipeline di Hello contiene un'attività di copia che è configurato toouse hello sopra i set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**MongoDbSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Schema da Data Factory
Servizio di Azure Data Factory deriva da una raccolta di MongoDB utilizzando documenti hello 100 più recente nella raccolta di hello. Se questi 100 documenti non contengono completo dello schema, è possibile ignorare alcune colonne durante l'operazione di copia hello.

## <a name="type-mapping-for-mongodb"></a>Mapping dei tipi per MongoDB
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Durante lo spostamento di hello tooMongoDB dati seguenti vengono utilizzati i mapping dai tipi di MongoDB tipi too.NET.

| Tipo di MongoDB | Tipo di .NET Framework |
| --- | --- |
| Binary |Byte[] |
| Boolean |Boolean |
| Date |DateTime |
| NumberDouble |Double |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |String |
| String |String |
| UUID |Guid |
| Oggetto |Rinormalizzato in colonne rese flat con "_" come separatore annidato |

> [!NOTE]
> toolearn sul supporto per le matrici con tabelle virtuali, vedere troppo[il supporto per i tipi complessi mediante tabelle virtuali](#support-for-complex-types-using-virtual-tables) sezione riportata di seguito.

Attualmente, non è supportato hello seguenti tipi di dati di MongoDB: DBPointer, JavaScript, minimo e massimo della chiave, espressioni regolari, simboli, Timestamp, non definito

## <a name="support-for-complex-types-using-virtual-tables"></a>Supporto per tipi complessi con tabelle virtuali
Data Factory di Azure Usa un ODBC driver tooconnect tooand copia dati predefinito del database MongoDB. Per i tipi complessi, ad esempio matrici o oggetti con tipi diversi in documenti hello, driver hello Normalizza nuovamente dati in tabelle virtuali corrispondenti. In particolare, se una tabella contiene colonne di tipo, il driver hello genera l'errore hello le tabelle virtuali seguenti:

* Oggetto **tabella di base**, che contiene hello stessi dati di tabella ad eccezione delle colonne di tipo complesso hello hello. tabella di base Hello utilizza hello stesso nome come tabella reale hello che rappresenta.
* Oggetto **tabella virtuale** per ogni colonna di tipo complesso, che espande dati hello annidato. tabelle virtuali Hello vengono denominate usando il nome di hello della tabella reale hello, un separatore "_" e nome hello della matrice hello o un oggetto.

Tabelle virtuali fare riferimento ai dati toohello nella tabella reale hello, abilitazione hello driver tooaccess hello dati denormalizzati. Per informazioni dettagliate, vedere la sezione riportata di seguito. È possibile accedere a contenuto hello di matrici di MongoDB eseguendo una query e join di tabelle virtuali hello.

È possibile utilizzare hello [Copia guidata](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively visualizzazione elenco di tabelle nel database di MongoDB inclusi tabelle virtuali hello hello e visualizzare l'anteprima dati hello all'interno. Inoltre, è possibile costruire una query nella copia guidata hello e convalidare i risultati di hello toosee.

### <a name="example"></a>Esempio
Ad esempio, "ExampleTable" di seguito è una tabella MongoDB che contiene una colonna con una matrice di oggetti in ogni cella (Fatture) e una colonna con una matrice di tipi scalari (Classificazioni).

| _id | Nome del cliente | Fatture | Contratto | Classificazioni |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id:"123", item:"toaster", price:"456", discount:"0.2"}, {invoice_id:"124", item:"oven", price: "1235", discount: "0.2"}] |Silver |[5,6] |
| 2222 |XYZ |[{invoice_id:"135", item:"fridge", price: "12543", discount: "0.0"}] |Gold |[1,2] |

driver Hello genera più tabelle virtuali toorepresent di questa tabella. Hello prima virtuale è hello base tabella denominata "ExampleTable", illustrato di seguito. tabella di base Hello contiene tutti i dati della tabella originale hello hello, ma i dati di hello da matrici di hello sono stato omesso e viene espanso nella tabelle virtuali hello.

| _id | Nome del cliente | Contratto |
| --- | --- | --- |
| 1111 |ABC |Silver |
| 2222 |XYZ |Gold |

Hello tabelle seguenti illustrano hello tabelle virtuali che rappresentano matrici originale di hello nell'esempio hello. Queste tabelle contengono seguente hello:

* Un riferimento toohello colonna chiave primaria corrispondente toohello riga originale della matrice originale hello (tramite colonna ID hello)
* Indicazione della posizione di hello dei dati di hello all'interno della matrice originale hello
* Hello espanso dati per ogni elemento all'interno della matrice hello

Tabella "ExampleTable_Invoices":

| _id | ExampleTable_Invoices_dim1_idx | invoice_id | item | price | Discount |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |toaster |456 |0,2 |
| 1111 |1 |124 |oven |1235 |0,2 |
| 2222 |0 |135 |fridge |12543 |0.0 |

Tabella "ExampleTable_Ratings":

| _id | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>Eseguire il mapping di colonne di origine toosink
toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lettura ripetibile da origini relazionali
Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione. Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.

## <a name="next-steps"></a>Passaggi successivi
Vedere [spostare i dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo per istruzioni dettagliate per la creazione di una pipeline di dati che consente di spostare dati da un locale tooan archiviano dati di Azure.
