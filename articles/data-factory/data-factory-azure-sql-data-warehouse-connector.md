---
title: aaaCopy dati da e verso Azure SQL Data Warehouse | Documenti Microsoft
description: Informazioni su come toocopy dati da e verso Azure SQL Data Warehouse utilizzando Data Factory di Azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Copia dati tooand da usando Azure Data Factory di Azure SQL Data Warehouse
Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toomove a/da Azure SQL Data Warehouse. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.  

> [!TIP]
> tooachieve prestazioni ottimali, utilizzare i dati di PolyBase tooload in Azure SQL Data Warehouse. Hello [dati tooload usare PolyBase in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sezione include dettagli. Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).

## <a name="supported-scenarios"></a>Scenari supportati
È possibile copiare dati **da Azure SQL Data Warehouse** toohello archivi dati seguenti:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

È possibile copiare dati da archivi dati seguenti hello **tooAzure SQL Data Warehouse**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> Quando si copiano dati da tooAzure di SQL Server o Database SQL di Azure SQL Data Warehouse, se non esiste alcuna tabella hello nell'archivio di destinazione hello, Data Factory potrà creare automaticamente tabella hello in SQL Data Warehouse utilizzando lo schema di hello della tabella hello in origine hello archivio dati. Per informazioni dettagliate vedere [Creazione automatica della tabella](#auto-table-creation).

## <a name="supported-authentication-type"></a>Tipo di autenticazione supportato
È supportato il connettore Azure SQL Data Warehouse per l'autenticazione di base.

## <a name="getting-started"></a>Introduzione
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un Azure SQL Data Warehouse usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline che copia i dati da e verso Azure SQL Data Warehouse è toouse hello copia dati guidata. Vedere [esercitazione: caricare i dati in SQL Data Warehouse con Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare una **data factory**. Una data factory può contenere una o più pipeline. 
2. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory. Ad esempio, se si copiano dati da un data warehouse di Azure blob storage tooan SQL di Azure, è creare due servizi collegati toolink l'account di archiviazione di Azure e la data factory di Azure SQL data warehouse tooyour. Per le proprietà di servizio collegato che sono specifici tooAzure SQL Data Warehouse, vedere [servizio proprietà collegate](#linked-service-properties) sezione. 
3. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello. E si crea un altro set di dati nella tabella toospecify hello hello Azure SQL data warehouse contenente dati hello copiati dall'archiviazione blob hello. Per le proprietà di set di dati che sono specifici tooAzure SQL Data Warehouse, vedere [proprietà set di dati](#dataset-properties) sezione.
4. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e SqlDWSink come sink per attività di copia hello. Analogamente, se si sta copiando tooAzure Azure SQL Data Warehouse nell'archiviazione Blob, utilizzare SqlDWSource e BlobSink nell'attività di copia hello. Per le proprietà di attività di copia che sono specifici tooAzure SQL Data Warehouse, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione. Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un Data Warehouse di SQL Azure, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sezione di questo articolo.

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure SQL Data Warehouse:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione JSON tooAzure specifico di elementi del servizio collegato SQL Data Warehouse.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **AzureSqlDW** |Sì |
| connectionString |Specificare l'istanza di Azure SQL Data Warehouse toohello tooconnect necessarie informazioni per la proprietà connectionString hello. È supportata solo l'autenticazione di base. |Sì |

> [!IMPORTANT]
> Configurare [Firewall di Database SQL di Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) e hello server di database troppo[consentire a servizi di Azure tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Inoltre, se si copiano dati tooAzure SQL Data Warehouse da inclusi Azure esterno da origini dati locali con gateway factory di dati, configurare l'intervallo di indirizzi IP appropriata per la macchina hello che invia dati tooAzure SQL Data Warehouse.

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. Hello **typeProperties** sezione per hello set di dati di tipo **AzureSqlDWTable** è hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello o della vista nel database di Azure SQL Data Warehouse hello che hello servizio collegato fa riferimento a. |Sì |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

> [!NOTE]
> Hello attività di copia accetta un solo input e produce un solo output.

Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

### <a name="sqldwsource"></a>SqlDWSource
Quando l'origine è di tipo **SqlDWSource**, hello le proprietà seguenti sono disponibile in **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: selezionare * da MyTable. |No |
| sqlReaderStoredProcedureName |Nome di hello stored procedure che legge i dati dalla tabella di origine hello. |Nome di hello stored procedure. ultima istruzione SQL di Hello deve essere un'istruzione SELECT nella procedura hello archiviato. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |

Se hello **sqlReaderQuery** specificato per hello SqlDWSource, hello attività di copia viene eseguita questa query hello dati di Azure SQL Data Warehouse origine tooget hello.

In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).

Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello del set di dati hello JSON sono utilizzati toobuild toorun una query su hello Azure SQL Data Warehouse. Esempio: `select column1, column2 from mytable`. Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.

#### <a name="sqldwsource-example"></a>Esempio SqlDWSource

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
**definizione della stored procedure Hello archiviato:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** supporta hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica. Per informazioni dettagliate, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy). |Istruzione di query. |No |
| allowPolyBase |Indica se toouse PolyBase (se applicabile) anziché meccanismo BULKINSERT. <br/><br/> **Utilizzo di PolyBase è hello consigliato dei dati tooload in SQL Data Warehouse.** Vedere [dati tooload usare PolyBase in Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sezione per i vincoli e i dettagli. |True  <br/>False (impostazione predefinita) |No |
| polyBaseSettings |Un gruppo di proprietà che possono essere specificati quando hello **allowPolybase** impostata troppo**true**. |&nbsp; |No |
| rejectValue |Specifica il numero di hello o la percentuale di righe che può essere rifiutata prima di hello query ha esito negativo. <br/><br/>Informazioni su ulteriori informazioni su del PolyBase hello rifiutare le opzioni di hello **argomenti** sezione [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) argomento. |0 (impostazione predefinita), 1, 2, … |No |
| rejectType |Specifica se l'opzione rejectValue hello è specificato come valore letterale o percentuale. |Value (impostazione predefinita), Percentage |No |
| rejectSampleValue |Determina il numero di hello di tooretrieve righe prima di hello PolyBase Ricalcola percentuale hello di righe rifiutate. |1, 2, … |Sì se **rejectType** è **percentage** |
| useTypeDefault |Specifica la modalità toohandle mancano i valori nel file di testo delimitati quando PolyBase recupera i dati da file di testo hello.<br/><br/>Altre informazioni su questa proprietà dalla sezione argomenti hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (valore predefinito) |No |
| writeBatchSize |Inserisce i dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| writeBatchTimeout |Tempo di attesa per hello batch insert operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |

#### <a name="sqldwsink-example"></a>Esempio SqlDWSink

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>Utilizzare i dati di PolyBase tooload in Azure SQL Data Warehouse
**[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** consente di caricare con efficacia grandi quantità di dati in Azure SQL Data Warehouse con una velocità effettiva elevata. È possibile visualizzare un miglioramento della velocità effettiva hello grandi dimensioni tramite PolyBase anziché meccanismo BULKINSERT di hello predefinito. Vedere [Copiare il numero di riferimento prestazioni](data-factory-copy-activity-performance.md#performance-reference) con il confronto dettagliato. Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).

* Se i dati di origine si trova in **Blob di Azure o archivio Azure Data Lake**e il formato di hello è compatibile con PolyBase, è possibile copiare direttamente tooAzure SQL Data Warehouse tramite PolyBase. Vedere **[Copia diretta tramite PolyBase](#direct-copy-using-polybase)** con i relativi dettagli.
* Se l'archivio dati di origine e il formato non è supportata in origine da PolyBase, è possibile utilizzare hello  **[copia gestita usando PolyBase](#staged-copy-using-polybase)**  funzionalità alternativa. Vengono inoltre una migliore velocità effettiva eseguendo automaticamente la conversione dei dati di hello nel formato compatibile con PolyBase e l'archiviazione dei dati di hello nell'archiviazione Blob di Azure. Vengono quindi caricati i dati in SQL Data Warehouse.

Set hello `allowPolyBase` proprietà troppo**true** come illustrato nel seguente esempio per Data Factory di Azure toouse PolyBase toocopy dati in Azure SQL Data Warehouse hello. Quando si imposta allowPolyBase tootrue, è possibile specificare proprietà specifiche di PolyBase con hello `polyBaseSettings` gruppo di proprietà. vedere hello [SqlDWSink](#SqlDWSink) per ulteriori informazioni sulle proprietà che è possibile utilizzare con impostazioni polyBaseSettings.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>Copia diretta tramite PolyBase
PolyBase di SQL Data Warehouse supporta direttamente Archiviazione BLOB di Azure e Azure Data Lake Store (mediante l'entità servizio) come origine e con requisiti di formato di file specifico. Se i dati di origine soddisfino i criteri di hello descritti in questa sezione, è possibile copiare direttamente dall'origine dati archivio tooAzure che SQL Data Warehouse tramite PolyBase. In caso contrario è possibile usare la [copia di staging tramite PolyBase](#staged-copy-using-polybase).

> [!TIP]
> toocopy dati dall'archivio Data Lake tooSQL Data Warehouse in modo efficiente, altre informazioni da [Data Factory di Azure rende anche più semplice e pratico toouncover informazioni significative dai dati quando si utilizza l'archivio Data Lake con SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Se non vengono soddisfatti i requisiti di hello, Data Factory di Azure controlla le impostazioni di hello e passa automaticamente meccanismo BULKINSERT toohello per lo spostamento dei dati di hello.

1. Il **servizio collegato all'origine** è di tipo: **AzureStorage** o **AzureDataLakeStore con autenticazione entità servizio**.  
2. Hello **set di dati input** è di tipo: **AzureBlob** o **AzureDataLakeStore**, e hello in tipo di formato `type` è di proprietà **OrcFormat** , o **TextFormat** con hello seguenti configurazioni:

   1. `rowDelimiter` deve essere **\n**.
   2. `nullValue`è stato impostato troppo**una stringa vuota** (""), o `treatEmptyAsNull` è troppo**true**.
   3. `encodingName`è stato impostato troppo**utf-8**, ovvero **predefinito** valore.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader` e `skipLineCount` non sono specificati.
   5. `compression` può essere **no compression**, **GZip** o **Deflate**.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. Non esiste alcun `skipHeaderLineCount` in **BlobSource** o **AzureDataLakeStore** per attività di copia nella pipeline hello hello.
4. Non esiste alcun `sliceIdentifierColumnName` in **SqlDWSink** per attività di copia nella pipeline hello hello. PolyBase garantisce che tutti i dati verranno aggiornati o che nessun dato verrà aggiornato in una singola esecuzione. tooachieve **ripetibilità**, è possibile utilizzare `sqlWriterCleanupScript`).
5. Non esiste alcun `columnMapping` utilizzata in hello associata nell'attività di copia.

### <a name="staged-copy-using-polybase"></a>copia di staging tramite PolyBase
Quando i dati di origine non soddisfano i criteri di hello introdotti nella sezione precedente di hello, è possibile abilitare una copia dei dati tramite un archivio di Blob di Azure staging provvisorio (non può essere archiviazione Premium). In questo caso, Azure Data Factory automaticamente consente di eseguire trasformazioni hello dati toomeet dati formato requisiti di PolyBase, quindi utilizzare i dati di tooload PolyBase in SQL Data Warehouse e ultimo pulizia dei dati dall'archiviazione Blob hello temp. Per informazioni dettagliate sul funzionamento generale della copia dei dati tramite un BLOB di Azure di staging, vedere la sezione [Copia di staging](data-factory-copy-activity-performance.md#staged-copy) .

> [!NOTE]
> Quando archiviano la copia di dati da un locale in Azure SQL Data Warehouse tramite PolyBase e sul gateway di gestione temporanea, se la versione del Gateway di gestione dati è di sotto di 2.4, è necessario JRE (Java Runtime Environment) del computer che viene utilizzato tootransform i dati di origine in formato corretto. Suggerire che tooavoid più recente di toohello il gateway si aggiorna tale dipendenza.
>

toouse tale funzionalità, creare un [servizio collegato di archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) che fa riferimento l'Account di archiviazione di Azure che ha l'archiviazione blob provvisorio hello toohello, quindi specificare hello `enableStaging` e `stagingSettings` le proprietà per hello attività di copia come illustrato nel seguente codice hello:

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>Procedure consigliate per l'uso di PolyBase
Hello nelle sezioni seguenti forniscono ulteriori toohello consigliate migliore quelli citati in [procedure consigliate per Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Autorizzazione database obbligatoria
toouse PolyBase, è necessario hello utente viene utilizzato tooload dati in SQL Data Warehouse è hello [autorizzazione "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) nel database di destinazione hello. Unidirezionale tooachieve tooadd che tale utente come membro del ruolo "db_owner". Informazioni su come toodo che seguendo [in questa sezione](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Limitazione alle dimensioni di righe e al tipo di dati
Carica Polybase è limitati tooloading righe sia inferiore a **1 MB** e non è possibile caricare tooVARCHR(MAX), nvarchar (max) o varbinary (max). Fare riferimento troppo[qui](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Se si dispone di dati di origine con le righe di dimensioni maggiori di 1 MB, è consigliabile tabelle di origine hello toosplit verticalmente in più piccole in hello riga massime di ognuno di essi non superi il limite di hello. le tabelle più piccole Hello possono quindi essere caricate usando PolyBase e uniti in Azure SQL Data Warehouse.

### <a name="sql-data-warehouse-resource-class"></a>Classe di risorse di SQL Data Warehouse
tooachieve migliori prestazioni possibili, prendere in considerazione tooassign maggiori risorse classe toohello utente viene usato il tooload dati in SQL Data Warehouse tramite PolyBase. Informazioni su come toodo che seguendo [un esempio di classe di risorse utente di modificare](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>tableName in Azure SQL Data Warehouse
Hello nella tabella seguente vengono forniti esempi su come hello toospecify **tableName** proprietà nel set di dati JSON per diverse combinazioni di nome di tabella e dello schema.

| Schema di database | Nome tabella | Proprietà JSON tableName |
| --- | --- | --- |
| dbo |MyTable |MyTable o dbo.MyTable o [dbo].[MyTable] |
| dbo1 |MyTable |dbo1.MyTable o [dbo1].[MyTable] |
| dbo |My.Table |[My.Table] o [dbo].[My.Table] |
| dbo1 |My.Table |[dbo1].[My.Table] |

Se viene visualizzato il seguente errore hello, può costituire un problema con il valore di hello che è specificato per la proprietà tableName di hello. Vedere la tabella hello per i valori di toospecify hello modo corretto per la proprietà di hello tableName JSON.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Colonne con valori predefiniti
Attualmente, PolyBase accetta solo funzionalità di Data Factory hello stesso numero di colonne come tabella di destinazione hello. Se si ha una tabella con quattro colonne di cui una definita con un valore predefinito, ad esempio, dati di input Hello devono comunque contenere quattro colonne. Fornisce un set di dati colonna 3 input produrrebbe un toohello simile di errore seguente messaggio:

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
Il valore NULL è una forma speciale di valore predefinito. Se la colonna hello ammette valori null, i dati di input di hello (in blob) per tale colonna potrebbe essere vuoti (non può essere mancante dal set di dati input hello). PolyBase consente di inserire NULL relativa hello Azure SQL Data Warehouse.  

## <a name="auto-table-creation"></a>Creazione automatica della tabella
Se si utilizza Copia guidata toocopy dati da SQL Server o Database SQL di Azure tooAzure SQL Data Warehouse e hello tabella corrispondente toohello tabella di origine non esiste nell'archivio di destinazione hello, Data Factory può creare automaticamente tabella hello in hello del data warehouse con schema di tabella di origine hello.

Data Factory Crea tabella hello nell'archivio di destinazione hello con hello stesso nome nell'archivio dati di origine hello di tabella. tipi di dati Hello per le colonne vengono scelti in base ai mapping dei tipi seguenti di hello. Se necessario, esegue toofix conversioni di tipo eventuali incompatibilità tra gli archivi di origine e di destinazione. Usa inoltre la distribuzione di tabella Round Robin.

| Tipo di colonna di origine del Database SQL | Tipo di colonna SQL DW di destinazione del Database (limitazione delle dimensioni) |
| --- | --- |
| int | int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| Bit | Bit |
| Decimal | Decimal |
| Numeric | Decimal |
| Float | Float |
| Money | Money |
| Real | Real |
| SmallMoney | SmallMoney |
| Binary | Binary |
| Varbinary | Varbinary (backup too8000) |
| Date | Data |
| DateTime | DateTime |
| DateTime2 | DateTime2 |
| Time | Time |
| Datetimeoffset | Datetimeoffset |
| SmallDateTime | SmallDateTime |
| Text | Varchar (backup too8000) |
| NText | NVarChar (backup too4000) |
| Image | VarBinary (backup too8000) |
| UniqueIdentifier | UniqueIdentifier |
| Char | Char |
| NChar | NChar |
| VarChar | VarChar (backup too8000) |
| NVarChar | NVarChar (backup too4000) |
| xml | Varchar (backup too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Mapping dei tipi per Azure SQL Data Warehouse
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando si spostano dati troppo & da Azure SQL Data Warehouse, hello mapping seguenti vengono utilizzate dal tipo too.NET di tipo SQL e viceversa.

mapping di Hello è uguale a hello [mapping dei tipi di dati di SQL Server per ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).

| Tipo di motore di database di SQL Server | Tipo di .NET Framework |
| --- | --- |
| bigint |Int64 |
| binary |Byte[] |
| bit |Boolean |
| char |String, Char[] |
| date |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| Decimale |Decimale |
| FILESTREAM attribute (varbinary(max)) |Byte[] |
| Float |Double |
| immagine |Byte[] |
| int |Int32 |
| money |Decimale |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numeric |Decimale |
| nvarchar |String, Char[] |
| real |Single |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |Decimale |
| sql_variant |Object * |
| text |String, Char[] |
| time |Intervallo di tempo |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

È anche possibile mappare le colonne di origine toocolumns di set di dati dal set di dati di sink nella definizione di attività di copia hello. Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>Esempi JSON per la copia di dati tooand da SQL Data Warehouse
Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Vengono visualizzate come toocopy tooand di dati da Azure SQL Data Warehouse e di archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>Esempio: Copiare i dati da Azure SQL Data Warehouse tooAzure Blob
esempio Hello definisce hello entità Data Factory di seguito:

1. Un servizio collegato di tipo [AzureSqlDW](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlDWTable](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [SqlDWSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati della serie temporale (orari, giornalieri, ecc.) da una tabella nell'oggetto blob tooa database Azure SQL Data Warehouse ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato di Azure SQL Data Warehouse:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Servizio collegato di archiviazione BLOB di Azure:**

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
**Set di dati di input di Azure SQL Data Warehouse:**

esempio Hello presuppone di aver creato una tabella "MyTable" in Azure SQL Data Warehouse e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.

L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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

**Attività di copia in una pipeline con SqlDWSource e BlobSink:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlDWSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> Nell'esempio hello **sqlReaderQuery** specificato per hello SqlDWSource. Hello attività di copia esegue query su dati di Azure SQL Data Warehouse origine tooget hello hello.
>
> In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).
>
> Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello del set di dati hello JSON sono toobuild utilizzata una query (selezionare column1, column2 da mytable) toorun contro hello Azure SQL Data Warehouse. Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>Esempio: Copiare i dati da tooAzure Blob di Azure SQL Data Warehouse
esempio Hello definisce hello entità Data Factory di seguito:

1. Un servizio collegato di tipo [AzureSqlDW](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlDWTable](#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlDWSink](#copy-activity-properties).

esempio Hello copia dati della serie temporale (oraria, giornaliera, ecc.) dalla tabella tooa blob di Azure nel database di Azure SQL Data Warehouse ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato di Azure SQL Data Warehouse:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Servizio collegato di archiviazione BLOB di Azure:**

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
**Set di dati di input del BLOB di Azure:**

I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1). Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio. "external": "true" impostazione informa il servizio di Data Factory hello che questa tabella è data factory di toohello esterni e non viene generata da un'attività nella data factory di hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
**Set di dati di output di Azure SQL Data Warehouse:**

esempio Hello copia tabella tooa dati denominata "MyTable" in Azure SQL Data Warehouse. Creare la tabella hello in Azure SQL Data Warehouse con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello. Aggiunta di nuove righe nella tabella toohello ogni ora.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
**Copiare attività in una pipeline con BlobSource e SqlDWSink:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlDWSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
Per una procedura dettagliata, vedere hello [caricare 1 TB in Azure SQL Data Warehouse in 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md) e [caricano dati con Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) articolo hello Azure SQL Data Warehouse documentazione.

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
