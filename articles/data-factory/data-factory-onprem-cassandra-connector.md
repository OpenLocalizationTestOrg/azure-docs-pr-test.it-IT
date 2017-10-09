---
title: dati aaaMove Cassandra utilizzando Data Factory | Documenti Microsoft
description: Informazioni sui database toomove dati da un Cassandra locali usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Spostare dati da un database Cassandra locale mediante Azure Data Factory
Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database Cassandra locale. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

È possibile copiare dati da un archivio di dati di on-premise Cassandra dati archivio tooany supportati sink. Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. Data factory di attualmente supporta solo lo spostamento di dati da un Cassandra archiviano tooother archivi di dati, ma non per lo spostamento dei dati da altro archivio dati di Cassandra tooa di archivi di dati. 

## <a name="supported-versions"></a>Versioni supportate
connettore Cassandra Hello supporta hello seguenti versioni di Cassandra: 2. x.

## <a name="prerequisites"></a>Prerequisiti
Per hello Azure Data Factory servizio toobe tooconnect in grado di tooyour Cassandra database locale, è necessario installare un Gateway di gestione di dati in hello stesso computer che ospita il database hello o tooavoid un computer separato competono per le risorse con hello database. Gateway di gestione dati è un componente che si connette a servizi di toocloud origini dati locali in modo sicuro e gestito. Leggere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per i dettagli sul Gateway di gestione dati. Vedere [spostare i dati da on-premise toocloud](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate sulla configurazione di gateway hello una pipeline di dati toomove dati.

È necessario utilizzare i database di hello gateway tooconnect tooa Cassandra anche se i database di hello è ospitato nel cloud hello, ad esempio, in una macchina virtuale IaaS di Azure. È possibile avere gateway hello su Y hello stessa macchina virtuale che ospita il database hello oppure in una macchina virtuale separata, purché il gateway hello possono connettersi toohello database.  

Quando si installa il gateway di hello, viene automaticamente installato un database di Microsoft Cassandra ODBC driver utilizzato tooconnect tooCassandra. Pertanto, non è necessario toomanually installare i driver nel computer gateway hello quando si copiano dati da database Cassandra hello. 

> [!NOTE]
> Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .

## <a name="getting-started"></a>Introduzione
È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API. 

- toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati. 
- È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio di dati Cassandra locale, vedere [esempio JSON: copiare i dati da tooAzure Cassandra Blob](#json-example-copy-data-from-cassandra-to-azure-blob) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooa Cassandra:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione del servizio specifico tooCassandra collegato gli elementi JSON.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **OnPremisesCassandra** |Sì |
| host |Uno o più indirizzi IP o nomi host di server Cassandra.<br/><br/>Specificare un elenco delimitato da virgole di indirizzi IP o host nomi tooconnect tooall server contemporaneamente. |Sì |
| port |la porta TCP che hello server Cassandra Hello utilizza toolisten per le connessioni client. |No, valore predefinito: 9042 |
| authenticationType |Di base o anonima |Sì |
| username |Specificare nome utente per l'account utente di hello. |Sì, se authenticationType impostata tooBasic. |
| password |Specificare la password per l'account utente di hello. |Sì, se authenticationType impostata tooBasic. |
| gatewayName |nome Hello del gateway hello tooconnect utilizzati toohello Cassandra database locale. |Sì |
| encryptedCredential |Credenziali crittografate dal gateway hello. |No |

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per set di dati di tipo **CassandraTable** è hello seguenti proprietà

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| keyspace |Nome di schema nel database Cassandra o di spazio delle chiavi hello. |Sì, se **query** per **CassandraSource** non è definito. |
| tableName |Nome della tabella hello Cassandra database. |Sì, se **query** per **CassandraSource** non è definito. |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Quando l'origine è di tipo **CassandraSource**, hello le proprietà seguenti sono disponibile nella sezione typeProperties:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Query SQL-92 o query CQL. Vedere il [riferimento a CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Quando si utilizza una query SQL, specificare **spazio delle chiavi name.table nome** toorepresent hello tabella tooquery. |No (se tableName e keyspace sul set di dati sono definiti). |
| consistencyLevel |livello di coerenza Hello specifica il numero di repliche deve rispondere tooa richiesta di lettura prima della restituzione dell'applicazione client toohello di dati. Controlli Cassandra hello specificato numero di repliche per hello toosatisfy dati richiesta di lettura. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Per informazioni dettagliate, vedere [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configurazione della coerenza dei dati). |No. Il valore predefinito è ONE. |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>Esempio JSON: copiare i dati da tooAzure Cassandra Blob
In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Viene illustrato come toocopy dati da un Cassandra locale database tooan archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

> [!IMPORTANT]
> Questo esempio fornisce frammenti di codice JSON. Non include istruzioni dettagliate per la creazione di data factory di hello. Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .

esempio Hello è hello entità factory di dati seguenti:

* Un servizio collegato di tipo [OnPremisesCassandra](#linked-service-properties).
* Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [set di dati](data-factory-create-datasets.md) di input di tipo [CassandraTable](#dataset-properties).
* Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [CassandraSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Servizio collegato Cassandra:**

Questo esempio viene utilizzato hello **Cassandra** servizio collegato. Vedere [servizio collegato Cassandra](#linked-service-properties) sezione per le proprietà di hello è supportato da questo servizio collegato.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
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

**Set di dati di input Cassandra:**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
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

Impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

**Set di dati di output del BLOB di Azure:**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Attività di copia in una pipeline con un'origine Cassandra e un sink BLOB:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**CassandraSource** e **sink** tipo è stato impostato troppo**BlobSink**.

Vedere [le proprietà del tipo RelationalSource](#copy-activity-properties) per elenco hello delle proprietà supportate da hello RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a>Mapping dei tipi per Cassandra
| Tipo Cassandra | Tipo basato su .Net |
| --- | --- |
| ASCII |String |
| BIGINT |Int64 |
| BLOB |Byte[] |
| BOOLEAN |BOOLEAN |
| DECIMAL |DECIMAL |
| DOUBLE |DOUBLE |
| FLOAT |Single |
| INET |String |
| INT |Int32 |
| TEXT |String |
| TIMESTAMP |DateTime |
| TIMEUUID |Guid |
| UUID |Guid |
| VARCHAR |String |
| VARINT |Decimal |

> [!NOTE]
> Per la raccolta di tipi (mappa, set, elenco, e così via), fare riferimento troppo[lavorare con i tipi di raccolta Cassandra utilizzando una tabella virtuale](#work-with-collections-using-virtual-table) sezione.
>
> I tipi definiti dall'utente non sono supportati.
>
> lunghezza Hello delle lunghezze di colonna di dati binari e di colonna stringa non può essere maggiore di 4000.
>
>

## <a name="work-with-collections-using-virtual-table"></a>Uso delle raccolte con una tabella virtuale
Data Factory di Azure Usa un ODBC driver tooconnect tooand copia dati predefinito dal database Cassandra. Per i tipi di raccolta inclusi mappa, set e un elenco, il driver hello rinormalizza dati hello in tabelle virtuali corrispondenti. In particolare, se una tabella contiene tutte le colonne della raccolta, il driver hello genera l'errore hello le tabelle virtuali seguenti:

* Oggetto **tabella di base**, che contiene hello stessi dati di tabella ad eccezione delle colonne insieme hello hello. tabella di base Hello utilizza hello stesso nome come tabella reale hello che rappresenta.
* Oggetto **tabella virtuale** per ogni colonna della raccolta, che espande dati hello annidato. tabelle virtuali Hello che rappresentano le raccolte vengono denominate usando hello Nome tabella hello reale, un separatore "*vt*" e il nome della colonna hello hello.

Tabelle virtuali fare riferimento ai dati toohello nella tabella reale hello, abilitazione hello driver tooaccess hello dati denormalizzati. Per i dettagli vedere la sezione Esempio. È possibile accedere a contenuto hello di raccolte Cassandra eseguendo una query e join di tabelle virtuali hello.

È possibile utilizzare hello [Copia guidata](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively visualizzazione elenco di tabelle nel database di Cassandra inclusi tabelle virtuali hello hello e visualizzare l'anteprima dati hello all'interno. Inoltre, è possibile costruire una query nella copia guidata hello e convalidare i risultati di hello toosee.

### <a name="example"></a>Esempio
Ad esempio, hello seguente "ExampleTable" è una tabella di database Cassandra che contiene una colonna chiave primaria integer denominate "pk_int", una colonna di testo denominato value, una colonna di elenco, una colonna della mappa e un set di colonne (denominato "StringSet").

| pk_int | Valore | Elenco | Mappa | StringSet |
| --- | --- | --- | --- | --- |
| 1 |"valore di esempio 1" |["1", "2", "3"] |{"S1": "a", "S2": "b"} |{"A", "B", "C"} |
| 3 |"valore di esempio 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"A", "E"} |

driver Hello genera più tabelle virtuali toorepresent di questa tabella. Hello le colonne chiave esterna nelle tabelle virtuali hello fare riferimento alle colonne chiave primaria hello nella tabella reale hello e indicare quali reale tabella hello tabella virtuale in una riga corrisponde a.

la tabella virtuale prima di Hello è denominata "ExampleTable" della tabella di base hello viene visualizzata in hello nella tabella seguente. tabella di base Hello contiene hello stessi dati della tabella del database originale hello ad eccezione di raccolte di hello, che vengono omessi dalla tabella ed espanso in altre tabelle virtuali.

| pk_int | Valore |
| --- | --- |
| 1 |"valore di esempio 1" |
| 3 |"valore di esempio 3" |

Hello tabelle seguenti illustrano tabelle virtuali hello che renormalize dati hello dalle colonne di elenco, mappa e StringSet hello. colonne di Hello con nomi che terminano con index"o Key" indicano la posizione di hello dei dati di hello all'interno di elenco originale hello o mappa. colonne di Hello con nomi che terminano con value"contengono dati hello espanso raccolta hello.

#### <a name="table-exampletablevtlist"></a>Tabella “ExampleTable_vt_List”:
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>Tabella “ExampleTable_vt_Map”:
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |Una  |
| 1 |S2 |b |
| 3 |S1 |t |

#### <a name="table-exampletablevtstringset"></a>Tabella “ExampleTable_vt_StringSet”:
| pk_int | StringSet_value |
| --- | --- |
| 1 |Una  |
| 1 |b |
| 1 |C |
| 3 |Una  |
| 3 |E |

## <a name="map-source-toosink-columns"></a>Eseguire il mapping di colonne di origine toosink
toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lettura ripetibile da origini relazionali
Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione. Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
