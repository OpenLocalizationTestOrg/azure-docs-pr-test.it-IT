---
title: aaaMove dati da DB2 utilizzando Data Factory di Azure | Documenti Microsoft
description: "Informazioni su come toomove dati da un DB2 locale del database tramite l'attività di copia di Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Spostare dati da DB2 mediante l'attività di copia di Azure Data Factory
In questo articolo viene descritto come usare attività di copia dei dati toocopy Data Factory di Azure da un archivio di dati locale tooa database DB2. È possibile copiare l'archivio dati tooany elencato come un sink supportato in hello [attività lo spostamento dei dati di Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) articolo. Questo argomento si basa sull'articolo Data Factory di hello, che viene presentata una panoramica di spostamento dei dati tramite l'attività di copia e l'elenco delle combinazioni di archivio dati hello è supportato. 

Data Factory supporta attualmente solo lo spostamento dei dati da un tooa database DB2 [archivio dati sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Lo spostamento dei dati da altri dati archivia tooa DB2 database non è supportato.

## <a name="prerequisites"></a>Prerequisiti
Data Factory supporta connessione database DB2 locale di tooan utilizzando hello [gateway di gestione dati](data-factory-data-management-gateway.md). Per istruzioni dettagliate tooset dei dati gateway hello pipeline toomove i dati, vedere hello [spostare i dati da on-premise toocloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.

Anche se hello DB2 è ospitato in Azure IaaS con macchina virtuale, è necessario un gateway. È possibile installare il gateway hello in hello stessa VM IaaS come archivio dati hello. Se il gateway di hello possa connettersi toohello database, è possibile installare il gateway di hello in una macchina virtuale diversa.

gateway di gestione dati Hello fornisce un driver DB2 predefinito, pertanto non è necessario toomanually installare un driver toocopy dati da DB2.

> [!NOTE]
> Per suggerimenti sulla risoluzione dei problemi del gateway e connessione, vedere hello [risolvere i problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) articolo.


## <a name="supported-versions"></a>Versioni supportate
connettore Hello Data Factory DB2 supporta hello seguenti piattaforme IBM DB2 e le versioni con le versioni di gestione di accesso SQL Distributed Relational Database Architecture (DRDA) 9, 10 e 11:

* IBM DB2 per z/OS versione 11.1
* IBM DB2 per z/OS versione 10.1
* IBM DB2 per i (AS400) versione 7.2
* IBM DB2 per i (AS400) versione 7.1
* IBM DB2 per Linux, UNIX e Windows (LUW) versione 11
* IBM DB2 per LUW versione 10.5
* IBM DB2 per LUW versione 10.1

> [!TIP]
> Se si riceve il messaggio di errore hello "hello pacchetto corrispondente tooan SQL istruzione richiesta di esecuzione non è stato trovato. SQLSTATE = 51002 SQLCODE = a 805, "hello, infatti, non è viene creato un pacchetto necessario per utente normale hello hello del sistema operativo. tooresolve questo problema, seguire queste istruzioni per il tipo di server DB2:
> - DB2 per i (AS400): consentono a un utente di creare la raccolta di hello per utente normale hello prima di eseguire attività di copia. raccolta di hello toocreate, utilizzare hello comando:`create collection <username>`
> - DB2 per z/OS o LUW: utilizzare un account con privilegi elevati, un power user o l'amministratore che dispone di autorità di pacchetto e binding, BINDADD, disporre delle autorizzazioni EXECUTE tooPUBLIC - copia di hello toorun una volta. pacchetto necessario Hello viene creato automaticamente durante la copia di hello. In seguito, è possibile passare utente normale toohello indietro per le esecuzioni successive di copia.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con dati toomove di un attività di copia da un archivio di dati DB2 locale tramite diversi strumenti e API: 

- toocreate modo più semplice di Hello una pipeline è toouse hello Azure Data Factory Copia guidata. Per un'esercitazione rapida sulla creazione di una pipeline mediante Copia guidata hello, vedere hello [esercitazione: creare una pipeline mediante Copia guidata hello](data-factory-copy-data-wizard-tutorial.md). 
- È inoltre possibile utilizzare strumenti toocreate una pipeline, tra cui hello portale di Azure, Visual Studio, Azure PowerShell, un modello Gestione risorse di Azure, hello API .NET e hello API REST. Per istruzioni dettagliate toocreate una pipeline con attività di copia, vedere hello [esercitazione attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare servizi collegati toolink dati di input e output archivi tooyour data factory.
2. Creare set di dati toorepresent input e output dei dati per l'operazione di copia hello. 
3. Creare una pipeline con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza Copia guidata, le definizioni di JSON per i servizi di Data Factory collegato hello, hello vengono creati automaticamente set di dati e le entità di pipeline per l'utente. Quando si utilizzano strumenti o le API (ad eccezione di hello API .NET), per definire entità Data Factory di hello, utilizzando il formato JSON hello. Hello [esempio JSON: copiare i dati da DB2 tooAzure nell'archiviazione Blob](#json-example-copy-data-from-db2-to-azure-blob) Mostra le definizioni di JSON hello per hello entità Data Factory che vengono utilizzati toocopy dati da un archivio di dati DB2 locale.

Hello le sezioni seguenti fornisce dettagli sulle hello proprietà JSON che sono utilizzati toodefine hello Data Factory entità che sono l'archivio dati specifico tooa DB2.

## <a name="db2-linked-service-properties"></a>Proprietà del servizio collegato DB2
Hello nella tabella seguente elenca le proprietà JSON hello sono tooa specifico del servizio collegato DB2.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| **type** |Questa proprietà deve essere impostata troppo**OnPremisesDB2**. |Sì |
| **server** |nome di Hello del server DB2 hello. |Sì |
| **database** |nome di Hello del database DB2 hello. |Sì |
| **schema** |nome Hello dello schema di hello in database DB2 hello. Questa proprietà fa distinzione tra maiuscole e minuscole. |No |
| **authenticationType** |tipo di Hello di autenticazione è il database di DB2 toohello tooconnect utilizzato. Hello i valori possibili sono: anonima, base e Windows. |Sì |
| **username** |nome Hello per account utente di hello se si utilizza l'autenticazione di base o di Windows. |No |
| **password** |password di Hello per account utente di hello. |No |
| **gatewayName** |nome Hello del gateway hello hello servizio Data Factory deve usare database di DB2 tooconnect toohello locale. |Sì |

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco di sezioni hello e proprietà che sono disponibili per la definizione di set di dati, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni, ad esempio **struttura**, **disponibilità**, hello e **criteri** per un set di dati JSON, sono simili per tutti i tipi di set di dati (SQL Azure, archiviazione Blob di Azure, tabelle di Azure archiviazione e così via).

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. Hello **typeProperties** sezione per un set di dati di tipo **RelationalTable**, che include set di dati DB2 hello, ha hello seguenti proprietà:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| **tableName** |nome Hello della tabella di hello nell'istanza di database DB2 hello che hello servizio collegato fa riferimento a. Questa proprietà fa distinzione tra maiuscole e minuscole. |No (se hello **query** proprietà di un'attività di copia di tipo **RelationalSource** è specificato) |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco di sezioni di hello e le proprietà disponibili per la definizione delle attività di copia, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili le proprietà dell'attività di copia, come **name**, **description**, tabella **inputs**, tabella **outputs** e **policy**. le proprietà disponibili in hello Hello **typeProperties** sezione dell'attività hello per ogni tipo di attività. Per attività di copia, la proprietà hello varia a seconda di hello tipi di origini dati e sink.

Per attività di copia, l'origine hello è di tipo **RelationalSource** (che include DB2), hello le proprietà seguenti sono disponibile in hello **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| **query** |Utilizzare i dati di hello tooread query personalizzata hello. |Stringa di query SQL. Ad esempio: `"query": "select * from "MySchema"."MyTable""` |No (se hello **tableName** proprietà di un set di dati è specificato) |

> [!NOTE]
> I nomi di schemi e tabelle fanno distinzione tra maiuscole e minuscole. Nell'istruzione di query hello, racchiudere i nomi delle proprietà utilizzando "" (virgolette doppie). ad esempio:
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>Esempio JSON: copiare i dati da DB2 tooAzure nell'archiviazione Blob
In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). esempio Hello Mostra come toocopy dati da un DB2 tooBlob archiviazione del database. Tuttavia, i dati possono essere copiati troppo[tutti i dati supportati archiviano il tipo di sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tramite attività di copia di Azure Data Factory.

esempio Hello è hello entità Data Factory di seguito:

- Un servizio collegato DB2 di tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)
- Un servizio collegato di archiviazione BLOB di Azure di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
- Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)
- Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
- Oggetto [pipeline](data-factory-create-pipelines.md) con un'attività di copia che utilizza hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) proprietà

esempio Hello copia dati da un risultato di query in un tooan database DB2 blob di Azure ogni ora. le proprietà JSON Hello utilizzati nell'esempio hello descritti nelle sezioni hello che seguono le definizioni di entità hello.

Innanzitutto installare e configurare un gateway dati. Le istruzioni sono in hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.

**Servizio collegato DB2**

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

**Servizio collegato di archiviazione BLOB di Azure**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Set di dati di input DB2**

esempio Hello presuppone che sia stato creato una tabella in DB2 denominata "MyTable" che dispone di una colonna con etichetta "timestamp" per i dati della serie temporale hello.

Hello **esterno** proprietà è impostata su troppo "true". Questa impostazione indica a servizio Data Factory hello di questo set di dati è esterna toohello data factory non viene generato da un'attività nella data factory di hello. Si noti che hello **tipo** impostata troppo**RelationalTable**.


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

I dati vengono scritti tooa nuovo blob ogni ora per l'impostazione hello **frequenza** proprietà troppo "Ora" e hello **intervallo** too1 di proprietà. Hello **folderPath** proprietà per il blob hello viene valutato dinamicamente in base ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ora hello hello ora di inizio.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pipeline per attività di copia hello**

pipeline di Hello contiene un'attività di copia che è configurata toouse specificato set di dati di input e output e che è pianificato toorun ogni ora. Nella definizione JSON per la pipeline di hello hello, hello **origine** tipo è stato impostato troppo**RelationalSource** hello e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello dalla tabella "Orders" hello.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>Mapping dei tipi per DB2
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, l'attività di copia esegue le conversioni dal tipo di origine tipo toosink automatica tramite hello approccio in due passaggi:

1. Convertire un tipo di origine nativa tipo tooa .NET
2. Convertire un tipo di sink native tooa tipo .NET

i seguenti mapping Hello vengono utilizzati quando l'attività di copia converte dati hello da un tipo di DB2 tipo tooa .NET:

| Tipo di database DB2 | Tipo di .NET Framework |
| --- | --- |
| SmallInt |Int16 |
| Integer |Int32 |
| BigInt |Int64 |
| Real |Single |
| Double |Double |
| Float |Double |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Numeric |Decimal |
| Date |DateTime |
| Time |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |String |
| VarChar |String |
| LongVarChar |String |
| DB2DynArray |String |
| Binary |Byte[] |
| VarBinary |Byte[] |
| LongVarBinary |Byte[] |
| Graphic |String |
| VarGraphic |String |
| LongVarGraphic |String |
| Clob |String |
| BLOB |Byte[] |
| DbClob |String |
| SmallInt |Int16 |
| Integer |Int32 |
| BigInt |Int64 |
| Real |Single |
| Double |Double |
| Float |Double |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Numeric |Decimal |
| Date |DateTime |
| Time |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |String |

## <a name="map-source-toosink-columns"></a>Eseguire il mapping di colonne di origine toosink
colonne toomap toocolumns set di dati di origine hello hello sink set di dati, vedere toolearn [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>Letture ripetibili da origini relazionali
Quando si copiano dati da un archivio dati relazionale, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È inoltre possibile configurare i tentativi di hello **criteri** proprietà per toorerun un set di dati una sezione quando si verifica un errore. Assicurarsi che hello stessi dati non vengono letti questione come sezione hello molte volte sia eseguire di nuovo, indipendentemente dalla modalità con cui si esegue nuovamente sezione hello. Per altre informazioni, vedere [Letture ripetibili da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestazioni e ottimizzazione
Informazioni sui fattori che influiscono sulle prestazioni di hello delle attività di copia e le modalità prestazioni toooptimize in hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md).
