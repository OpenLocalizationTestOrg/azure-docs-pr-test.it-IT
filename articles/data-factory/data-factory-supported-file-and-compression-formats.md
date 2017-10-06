---
title: formati aaaFile e compressione nella Data Factory di Azure | Documenti Microsoft
description: "Informazioni sui formati di file hello è supportati da Azure Data Factory."
keywords: dati blob, copia di blob di azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a>Informazioni sui formati di compressione e sui file supportati da Azure Data Factory
*Questo argomento si applica toohello segue connettori: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Blob di Azure](data-factory-azure-blob-connector.md), [archivio Azure Data Lake](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), e [SFTP](data-factory-sftp-connector.md).*

Data Factory di Azure supporta i seguenti tipi di formato di file hello:

* [Formato testo](#text-format)
* [Formato JSON](#json-format)
* [Formato Avro](#avro-format)
* [Formato ORC](#orc-format)
* [Formato Parquet](#parquet-format)

## <a name="text-format"></a>Formato testo
Se si desidera tooread da un file di testo o scrivere file di testo tooa, impostare hello `type` proprietà hello `format` sezione del set di dati hello troppo**TextFormat**. È inoltre possibile specificare i seguenti hello **facoltativo** proprietà hello `format` sezione. Vedere [esempio TextFormat](#textformat-example) sezione su come tooconfigure.

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| columnDelimiter |carattere Hello usato tooseparate colonne in un file. È possibile considerare toouse un carattere non stampabile raro che potrebbero essere probabilmente non esiste nei dati. Ad esempio, specificare "\u0001", che rappresenta l'inizio intestazione (SOH). |È consentito un solo carattere. Hello **predefinito** valore **virgola (',')**. <br/><br/>toouse un carattere Unicode, vedere troppo[caratteri Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello codice corrispondente per tale. |No |
| rowDelimiter |carattere Hello usato tooseparate righe in un file. |È consentito un solo carattere. Hello **predefinito** valore è uno dei seguenti valori in lettura hello: **["\r\n", "\r", "\n"]** e **"\r\n"** durante la scrittura. |No |
| escapeChar |carattere speciale di Hello utilizzato tooescape un delimitatore di colonna nel contenuto di hello del file di input. <br/><br/>Per una tabella, è possibile specificare sia escapeChar che quoteChar. |È consentito un solo carattere. Nessun valore predefinito. <br/><br/>Esempio: se è presente una virgola (', ') come delimitatore di colonna hello ma si desidera aggiungere un carattere virgola toohave hello in testo hello (esempio: "Hello, world"), è possibile definire '$' come carattere di escape hello e utilizzare una stringa "Hello$, world" nell'origine hello. |No |
| quoteChar |carattere di Hello utilizzato tooquote un valore stringa. delimitatori di colonna e riga Hello all'interno di virgolette singole hello verrebbero considerati come parte del valore di stringa hello. Questa proprietà è applicabile tooboth input e output di set di dati.<br/><br/>Per una tabella, è possibile specificare sia escapeChar che quoteChar. |È consentito un solo carattere. Nessun valore predefinito. <br/><br/>Ad esempio, se è presente una virgola (', ') come delimitatore di colonna hello ma si desidera assegnare il carattere virgola toohave nel testo hello (esempio: < Hello, world >), è possibile definire "(virgolette doppie) come hello virgolette e utilizzare la stringa hello"Hello, world"nell'origine hello. |No |
| nullValue |Uno o più caratteri utilizzati toorepresent un valore null. |Uno o più caratteri. Hello **predefinito** i valori sono **"\N" e "NULL"** in lettura e **"\N"** durante la scrittura. |No |
| encodingName |Specificare il nome della codifica di hello. |Un nome di codifica valido. Vedere [Proprietà Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Esempio: windows-1250 o shift_jis. Hello **predefinito** valore **UTF-8**. |No |
| firstRowAsHeader |Specifica se tooconsider hello prima riga come intestazione. In un set di dati di input Data factory legge la prima riga come intestazione. In un set di dati di output Data factory scrive la prima riga come intestazione. <br/><br/>Vedere [Scenari per l'uso di `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) per gli scenari di esempio. |True<br/><b>False (impostazione predefinita)</b> |No |
| skipLineCount |Indica il numero di hello di tooskip righe durante la lettura di dati da file di input. Se vengono specificati sia skipLineCount e prima riga come intestazione, le righe di hello vengono ignorate prima e quindi le informazioni di intestazione hello viene letto dal file di input hello. <br/><br/>Vedere [Scenari per l'uso di `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) per gli scenari di esempio. |Integer |No |
| treatEmptyAsNull |Consente di specificare se una stringa vuota o null tootreat come un valore null durante la lettura dei dati da un file di input. |**True (impostazione predefinita)**<br/>False |No |

### <a name="textformat-example"></a>Esempio di TextFormat
In hello seguente definizione JSON per un set di dati, alcune delle proprietà facoltative hello vengono specificati.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse un `escapeChar` anziché `quoteChar`, sostituire la riga hello con `quoteChar` con hello escapeChar seguenti:

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Scenari di utilizzo di firstRowAsHeader e skipLineCount
* Si sta copiando un file di testo di origine file non tooa e tooadd una riga di intestazione che contiene i metadati dello schema hello (ad esempio: schema SQL). Specificare `firstRowAsHeader` come true nel set di dati per questo scenario di output di hello.
* Si sta copiando un file di testo contenente un sink non basate su file di intestazione riga tooa e toodrop che riga. Specificare `firstRowAsHeader` come true nella hello di un set di dati dell'input.
* Si sta copiando un file di testo e si desiderano tooskip alcune righe all'inizio di hello che non contengono dati o intestazione informazioni. Specificare `skipLineCount` tooindicate hello numero di righe toobe ignorati. Se il resto di hello del file hello contiene una riga di intestazione, è inoltre possibile specificare `firstRowAsHeader`. Se entrambi `skipLineCount` e `firstRowAsHeader` sono specificate, le righe di hello vengono ignorate prima e quindi le informazioni di intestazione hello viene letto dal file di input hello

## <a name="json-format"></a>Formato JSON
troppo**importazione/esportazione di un file JSON come-è in/da Azure Cosmos DB**, vedere hello [documenti JSON di importazione/esportazione](data-factory-azure-documentdb-connector.md#importexport-json-documents) sezione [spostare i dati da e verso Azure Cosmos DB](data-factory-azure-documentdb-connector.md) articolo.

Se si desidera che i file JSON hello tooparse o scrivono dati hello in formato JSON, impostare hello `type` proprietà hello `format` sezione troppo**JsonFormat**. È inoltre possibile specificare i seguenti hello **facoltativo** proprietà hello `format` sezione. Vedere [JsonFormat esempio](#jsonformat-example) sezione su come tooconfigure.

| Proprietà | Descrizione | Obbligatoria |
| --- | --- | --- |
| filePattern |Indicano il motivo di hello dei dati archiviati in ogni file JSON. I valori consentiti sono: **setOfObjects** e **arrayOfObjects**. Hello **predefinito** valore **setOfObjects**. Vedere la sezione [Modelli di file JSON](#json-file-patterns) per i dettagli su questi modelli. |No |
| jsonNodeReference | Se si desidera tooiterate ed estrarre i dati da oggetti hello all'interno di una matrice di un campo con hello stesso schema, specificare il percorso JSON hello della matrice. Questa proprietà è supportata solo quando si copiano i dati dai file JSON. | No |
| jsonPathDefinition | Specificare l'espressione di percorso JSON hello per ogni mapping di colonna con un nome di colonna personalizzati (inizia con lettere minuscole). Questa proprietà è supportata solo quando si copiano i dati dai file JSON ed è possibile estrarre i dati dall'oggetto o dalla matrice. <br/><br/> Per i campi nell'oggetto radice, iniziare con $ radice; per i campi nella matrice hello scelto da `jsonNodeReference` proprietà inizio dall'elemento di matrice hello. Vedere [JsonFormat esempio](#jsonformat-example) sezione su come tooconfigure. | No |
| encodingName |Specificare il nome della codifica di hello. Per hello l'elenco di nomi di codifica validi, vedere: [EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) proprietà. Ad esempio: windows-1250 o shift_jis. Hello **predefinito** valore: **UTF-8**. |No |
| nestingSeparator |Carattere usato tooseparate livelli di annidamento. valore predefinito di Hello è '.' (punto). |No |

### <a name="json-file-patterns"></a>Modelli di file JSON

Attività di copia può analizzare hello seguito modelli di file JSON:

- **Tipo I: setOfObjects**

    Ogni file contiene un solo oggetto o più oggetti con delimitatori di riga/concatenati. Quando si sceglie questa opzione in un set di dati di output, l'attività di copia produce un singolo file JSON con un oggetto per riga (delimitato da riga).

    * **Esempio di JSON a oggetto singolo**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **Esempio di JSON con delimitatori di riga**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **Esempio di JSON concatenati**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **Tipo II: arrayOfObjects**

    Ogni file contiene una matrice di oggetti.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a>Esempio JsonFormat

**Caso 1: Copia di dati dai file JSON**

Vedere hello seguito due esempi di quando si copiano dati da file JSON. Hello toonote punti generico:

**Esempio 1: Estrarre i dati dall'oggetto e dalla matrice**

In questo esempio, si prevede un oggetto JSON radice esegue il mapping di record toosingle risultati tabulari. Se si dispone di un file JSON con hello seguente contenuto:  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
e si desidera toocopy in una tabella SQL di Azure seguenti hello formattare, estrarre dati da entrambi gli oggetti e di matrice:

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 1/13/2017 11:24:37 AM |

set di dati input Hello con **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello). Più in particolare:

- `structure`Definisce i nomi di colonna hello personalizzato e il tipo di dati corrispondente hello durante la conversione dei dati tootabular. Questa sezione è **facoltativo** a meno che non è necessario toodo mapping della colonna. Vedere [eseguire il mapping di colonne di set di dati di origine del dataset colonne toodestination](data-factory-map-columns.md) sezione per ulteriori dettagli.
- `jsonPathDefinition`Specifica il percorso JSON hello per ogni colonna che indica dove tooextract hello dati. dati toocopy dalla matrice, è possibile utilizzare **Property matrice [x]** tooextract valore hello data proprietà dall'oggetto x hello oppure è possibile utilizzare  **matrice [*] Property** toofind valore di Hello da qualsiasi oggetto che contiene questo tipo proprietà.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**Esempio 2:: applicare più oggetti con hello stesso modello di matrice**

In questo esempio, si prevede un oggetto tootransform JSON radice in più record nel risultato tabulare. Se si dispone di un file JSON con hello seguente contenuto:  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
e si desidera toocopy in una tabella SQL di Azure seguenti hello formatta, per rendere bidimensionali i dati di hello all'interno di matrice hello e cross join con informazioni radice comune hello:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

set di dati input Hello con **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello). Più in particolare:

- `structure`Definisce i nomi di colonna hello personalizzato e il tipo di dati corrispondente hello durante la conversione dei dati tootabular. Questa sezione è **facoltativo** a meno che non è necessario toodo mapping della colonna. Vedere [eseguire il mapping di colonne di set di dati di origine del dataset colonne toodestination](data-factory-map-columns.md) sezione per ulteriori dettagli.
- `jsonNodeReference`indica tooiterate ed estrarre i dati da oggetti hello con hello stesso modello in **matrice** orderlines.
- `jsonPathDefinition`Specifica il percorso JSON hello per ogni colonna che indica dove tooextract hello dati. In questo esempio, "ordernumber", "orderdate" e "city" sono in oggetto di primo livello con JSON inizi con "$"., mentre "order_pd" e "order_price" sono definiti con percorso derivata dall'elemento di matrice hello senza "$"..

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**Si noti hello seguenti punti:**

* Se hello `structure` e `jsonPathDefinition` non sono definiti nel set di dati con Data Factory di hello hello attività di copia rileva hello schema dal primo oggetto hello e rendere flat intero oggetto hello.
* Se l'input JSON hello dispone di una matrice, per impostazione predefinita hello attività di copia converte il valore di matrice intera hello in una stringa. È possibile scegliere i dati tooextract tramite `jsonNodeReference` e/o `jsonPathDefinition`, o ignorarlo se non viene specificata in `jsonPathDefinition`.
* Se sono presenti duplicati nomi hello allo stesso livello, hello attività di copia selezioni hello ultimo.
* I nomi delle proprietà distinguono tra maiuscole e minuscole. Due proprietà con lo stesso nome ma con una combinazione differente di maiuscole e minuscole vengono considerate come due proprietà diverse.

**Caso 2: Scrittura del file di dati tooJSON**

Se si dispone di hello in Database SQL nella tabella seguente:

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

e per ogni record, si supponga che oggetto JSON di toowrite tooa hello seguente formato:
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

set di dati con output di Hello **JsonFormat** tipo viene definito come segue: (definizione parziale con solo parti pertinenti di hello). In particolare, `structure` sezione definisce i nomi delle proprietà hello personalizzata nel file di destinazione, `nestingSeparator` (valore predefinito è ".") sono a livello di nidificazione hello tooidentify utilizzato dal nome hello. Questa sezione è **facoltativo** a meno che si desidera toochange hello proprietà nome, il confronto con il nome di colonna di origine o annidare alcune proprietà hello.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a>Formato AVRO
Se si desidera tooparse hello Avro file o scrivono dati hello in formato Avro, impostare hello `format` `type` proprietà troppo**AvroFormat**. Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello. Esempio:

```json
"format":
{
    "type": "AvroFormat",
}
```

formato Avro di toouse in una tabella Hive, è possibile fare riferimento troppo[esercitazione su Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Si noti hello seguenti punti:  

* I [tipi di dati complessi](http://avro.apache.org/docs/current/spec.html#schema_complex) non sono supportati (record, enumerazioni, matrici, mappe, unioni e dati fissi).

## <a name="orc-format"></a>Formato ORC
Se si desidera tooparse hello ORC file o scrivono dati hello in formato ORC, impostare hello `format` `type` proprietà troppo**OrcFormat**. Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello. Esempio:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Se non si desidera copiare i file ORC **come-è** tra sedi locali e cloud archivi dati, è necessario tooinstall hello 8 JRE (Java Runtime Environment) nel computer gateway. Per un gateway a 64 bit è necessario JRE a 64 bit, mentre per un gateway a 32 bit è necessario JRE a 32 bit. Entrambe le versioni sono disponibili [qui](http://go.microsoft.com/fwlink/?LinkId=808605). Scegliere hello più appropriato.
>
>

Si noti hello seguenti punti:

* Tipi di dati complessi non sono supportati (STRUCT, MAP, LIST, UNION)
* Il file ORC dispone di tre [opzioni relative alla compressione](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY. Data Factory supporta la lettura dei dati dal file ORC in uno di questi formati compressi. Usa compressione hello codec è nei dati di hello metadati tooread hello. Tuttavia, durante la scrittura di file ORC tooan, Data Factory sceglie ZLIB, hello predefinito per ORC. Attualmente non è disponibile alcuna opzione toooverride questo comportamento.

## <a name="parquet-format"></a>Formato Parquet
Se si desidera tooparse hello Parquet file o scrivono dati hello in formato Parquet, impostare hello `format` `type` proprietà troppo**ParquetFormat**. Non è necessario toospecify delle proprietà nella sezione formato hello nella sezione typeProperties hello. Esempio:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Se non si desidera copiare i file Parquet **come-è** tra sedi locali e cloud archivi dati, è necessario tooinstall hello 8 JRE (Java Runtime Environment) nel computer gateway. Per un gateway a 64 bit è necessario JRE a 64 bit, mentre per un gateway a 32 bit è necessario JRE a 32 bit. Entrambe le versioni sono disponibili [qui](http://go.microsoft.com/fwlink/?LinkId=808605). Scegliere hello più appropriato.
>
>

Si noti hello seguenti punti:

* Tipi di dati complessi non sono supportati (MAP, LIST)
* Dispone di file parquet hello relativi alla compressione le opzioni seguenti: NONE, SNAPPY GZIP e LZO. Data Factory supporta la lettura dei dati dal file ORC in uno di questi formati compressi. Usa il codec di compressione hello nei dati di hello metadati tooread hello. Tuttavia, durante la scrittura di file Parquet tooa, Data Factory sceglie SNAPPY, hello predefinito per il formato Parquet. Attualmente non è disponibile alcuna opzione toooverride questo comportamento.

## <a name="compression-support"></a>Supporto della compressione
L'elaborazione di set di dati di grandi dimensioni può causare colli di bottiglia I/O e di rete. Di conseguenza, i dati compressi in archivi possano non solo velocizzare il trasferimento dei dati attraverso la rete hello e risparmiare spazio su disco, ma anche visualizzare miglioramenti significativi delle prestazioni di elaborazione di big data. Attualmente, la compressione è supportata per gli archivi di dati basati su file, ad esempio BLOB di Azure o il file system locale.  

la compressione toospecify per un set di dati, utilizzare hello **compressione** proprietà hello set di dati JSON come hello di esempio seguente:   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

Si supponga che il set di dati di hello esempio viene utilizzato come output di hello di un'attività di copia, hello Copia attività comprime hello i dati di output con i codec GZIP con rapporto ottimale e quindi scrivere dati hello compresso in un file denominato pagecounts.csv.gz in hello archiviazione Blob di Azure.

> [!NOTE]
> Le impostazioni di compressione non sono supportate per i dati in hello **AvroFormat**, **OrcFormat**, o **ParquetFormat**. Durante la lettura di file in tali formati, Data Factory rileva e utilizza il codec di compressione hello nei metadati hello. Quando si scrivono toofiles in questi formati, Data Factory sceglie codec di compressione hello predefinito per tale formato. ad esempio ZLIB per OrcFormat e SNAPPY per ParquetFormat.   

Hello **compressione** sezione ha due proprietà:  

* **Tipo:** codec di compressione hello, che può essere **GZIP**, **Deflate**, **BZIP2**, o **ZipDeflate**.  
* **Livello:** rapporto di compressione hello, che può essere **ottimale** o **Fastest**.

  * **Più veloce:** hello compressione deve completare l'operazione più rapidamente possibile, anche se non viene compresso in modo ottimale file risultante hello.
  * **Ottimale**: operazione di compressione hello deve essere in modo ottimale compresso, anche se l'operazione di hello accetta un toocomplete di tempo più lungo.

    Per maggiori informazioni, vedere l'argomento relativo al [livello di compressione](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .

Quando si specifica `compression` proprietà in un set di dati input JSON, pipeline hello può leggere dati compressi di origine di hello e quando si specificano proprietà hello in un set di dati di output JSON, l'attività di copia hello può scrivere destinazione toohello dati compressi. Di seguito vengono forniti alcuni scenari di esempio:

* Leggere i dati compressi GZIP da un blob di Azure, decomprimono e scrivere i database SQL di Azure tooan dati dei risultati. Definire i set di dati input per i Blob di Azure hello con hello `compression` `type` proprietà JSON come GZIP.
* Leggere dati da un file di testo dal File System di on-premise, comprimere utilizzando il formato GZip e scrivere hello compresso tooan di dati blob di Azure. Si definisce un set di dati di output Blob di Azure con hello `compression` `type` proprietà JSON come GZip.
* File con estensione zip di lettura dal server FTP, decomprimono i file hello tooget all'interno e inserite tali file in archivio Azure Data Lake. Si definisce un set di dati input FTP con hello `compression` `type` proprietà JSON come ZipDeflate.
* Leggere i dati compressi GZIP da un blob di Azure, decomprimono, comprimerlo BZIP2 e scrivere dati di risultati tooan blob di Azure. Definire i set di dati input per i Blob di Azure hello con `compression` `type` impostare tooGZIP e set di dati di output con hello `compression` `type` impostare tooBZIP2 in questo caso.   


## <a name="next-steps"></a>Passaggi successivi
Vedere i seguenti articoli per gli archivi di dati basati su file supportati da Azure Data Factory hello:

- [Archiviazione BLOB di Azure](data-factory-azure-blob-connector.md)
- [Archivio Data Lake di Azure](data-factory-azure-datalake-connector.md)
- [FTP](data-factory-ftp-connector.md)
- [HDFS](data-factory-hdfs-connector.md)
- [File system](data-factory-onprem-file-system-connector.md)
- [Amazon S3](data-factory-amazon-simple-storage-service-connector.md)
