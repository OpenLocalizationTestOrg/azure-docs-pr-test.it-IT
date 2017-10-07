---
title: aaaLoad - archivio Azure Data Lake tooSQL Data Warehouse | Documenti Microsoft
description: Informazioni su come toouse PolyBase esterne nelle tabelle dati tooload dall'archivio Azure Data Lake in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Caricare dati da Azure Data Lake Store a SQL Data Warehouse
Questo documento offre tutte le operazioni necessarie tooload i propri dati da Azure Data Lake archivio (ADLS) in SQL Data Warehouse con PolyBase.
Mentre si è query ad hoc in grado di toorun sui dati hello archiviati in ADLS utilizzando le tabelle esterne hello, come procedura consigliata è consigliabile importare dati hello in hello SQL Data Warehouse.
Tempo stimato: 10 minuti, se che si dispone di prerequisiti hello necessario toocomplete.
In questa esercitazione si apprenderà come:

1. Creare tooload gli oggetti di Database esterno dall'archivio Azure Data Lake.
2. Connettersi tooan Directory dell'archivio Azure Data Lake.
3. Caricare i dati in Azure SQL Data Warehouse.

## <a name="before-you-begin"></a>Prima di iniziare
toorun questa esercitazione, è necessario:

* Azure toouse di applicazione di Active Directory per l'autenticazione al servizio. toocreate, seguire [l'autenticazione di Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> È necessario l'ID client hello, chiave e valore Endpoint Token OAuth 2.0 di tooyour di tooconnect l'applicazione di Active Directory Azure Data Lake SQL Data warehouse. Dettagli per la modalità tooget questi valori sono nel collegamento hello precedente.
>Nota per la registrazione di App di Azure Active Directory utilizzare "ID applicazione" hello come hello ID Client.

* SQL Server Management Studio o SQL Server Data Tools, toodownload SQL Server Management Studio e connettersi vedere [Query SQL Server Management Studio](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Un Data Warehouse SQL Azure, toocreate uno seguire: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Un'istanza di Azure Data Lake Store, con o senza crittografia abilitata. una seguire toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Configurare l'origine dati hello
PolyBase Usa percorso hello toodefine oggetti esterni di T-SQL e degli attributi di dati esterni hello. gli oggetti esterni Hello vengono archiviati in SQL Data Warehouse e hello dati di riferimento che th vengono archiviati esternamente.


###  <a name="create-a-credential"></a>Creare una credenziale
Archiviare la Data Lake di Azure tooaccess, sarà necessario toocreate tooencrypt una chiave Master del Database il segreto di credenziale utilizzato nel passaggio successivo hello.
È quindi possibile creare una credenziale con ambito Database, che memorizza credenziali dell'entità servizio hello configurate in AAD. Per gli utenti che hanno utilizzato PolyBase tooconnect tooWindows BLOB di archiviazione di Azure, si noti che le credenziali hello sintassi è diversa.
tooconnect tooAzure archivio Data Lake, è necessario **prima** creare un'applicazione di Azure Active Directory, creare una chiave di accesso e concedere una risorsa di Azure Data Lake toohello accesso dell'applicazione hello. Instrucitons tooperform questi passaggi si trovano [qui](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a>Creare l'origine dati esterna hello
Utilizzare questo [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando percorso hello toostore di dati hello e hello tipo di dati.
È possibile trovare hello ADL URI nel portale di Azure hello e www.portal.azure.com.

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a>Configurare il formato dei dati
dati di hello tooimport di ADLS, è necessario toospecify formato di file esterno hello. Questo comando è toodescribe opzioni relative al formato dei dati.
Di seguito è riportato un esempio di formato file comunemente usato, ovvero un file di testo delimitato da barre verticali.
Esaminare la documentazione di T-SQL per un elenco completo di [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```

## <a name="create-hello-external-tables"></a>Creare tabelle esterne di hello
Ora che è stata specificata l'origine e file di formato di dati di hello, si è pronti toocreate tabelle esterne di hello. Le tabelle esterne rappresentano la modalità di interazione con i dati esterni. PolyBase, viene utilizzato per tutti i file in tutte le sottodirectory della directory hello specificata nel parametro di percorso hello ricorsiva directory attraversamento tooread. Inoltre, hello di esempio seguente viene illustrato come toocreate hello oggetto. È necessario toocustomize hello istruzione toowork dati hello che dispongono di ADLS.

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a>Considerazioni sulle tabelle esterne
Creazione di una tabella esterna è semplice, ma sono presenti alcuni aspetti correlati necessari toobe descritto.

Il caricamento dei dati con PolyBase è fortemente tipizzato. Ciò significa che ogni riga di dati hello il caricamento deve soddisfare definizione dello schema di tabella hello.
Se una determinata riga non corrisponde alla definizione dello schema hello, riga hello viene rifiutata dal carico hello.

Hello REJECT_TYPE e REJECT_VALUE opzioni consentono di toodefine il numero di righe o la percentuale di dati hello deve essere presente nella tabella finale hello.
Durante il caricamento, se viene raggiunto il valore di rifiuto di hello, hello caricamento non riesce. causa più comune di Hello di righe rifiutate è una mancata corrispondenza della definizione dello schema.
Ad esempio, se una colonna in modo non corretto di schema hello di int quando i dati di hello nel file hello sono una stringa, ogni riga avrà esito negativo tooload.

Hello percorso Specifica directory hello in primo piano da dati tooread da.
In questo caso, se si sono verificati sottodirectory /DimProduct/ PolyBase importazione tutti i dati all'interno di sottodirectory di hello hello.

## <a name="load-hello-data"></a>Caricare i dati di hello
dati tooload dall'archivio Azure Data Lake utilizzano hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] istruzione. Caricamento con un'istruzione CTAS utilizza hello fortemente tipizzati tabella esterna che è stata creata.

Un'istruzione CTAS crea una nuova tabella e popolarla con i risultati di hello di un'istruzione select. Un'istruzione CTAS definisce hello nuova tabella toohave hello stessi colonne e tipi di dati come risultato di hello hello istruzione select. Se si selezionano tutte le colonne di hello da una tabella esterna, nuova tabella hello è una replica di colonne di hello e tipi di dati nella tabella esterna hello.

In questo esempio viene creata una tabella con distribuzione hash chiamata DimProduct dalla tabella esterna DimProduct_external.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Ottimizzare la compressione columnstore
Per impostazione predefinita, SQL Data Warehouse vengono archiviati nella tabella hello come un indice columnstore cluster. Al termine di un carico, alcune righe di dati hello potrebbe non compresso nel columnstore hello.  Esiste una serie di motivi per cui questo può verificarsi. vedere, più toolearn [gestire gli indici columnstore][manage columnstore indexes].

le prestazioni delle query toooptimize e la compressione columnstore dopo un caricamento, ricompilare tutte le righe di hello hello tabella tooforce hello columnstore indice toocompress.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Per ulteriori informazioni sulla gestione degli indici columnstore, vedere hello [gestire gli indici columnstore] [ manage columnstore indexes] articolo.

## <a name="optimize-statistics"></a>Ottimizzare le statistiche
Le statistiche di colonna singola toocreate è immediatamente dopo un carico. Sono disponibili alcune opzioni per le statistiche. Ad esempio, se si creano statistiche a colonna singola su tutte le colonne potrebbe richiedere un tempo toorebuild tutte le statistiche di hello. Se si è certi di che alcune colonne non stanno toobe nei predicati di query, è possibile ignorare la creazione di statistiche di tali colonne.

Se si decide di statistiche di colonna singola toocreate ogni colonna di ogni tabella, è possibile utilizzare l'esempio di codice hello stored procedure `prc_sqldw_create_stats` in hello [statistiche] [ statistics] articolo.

Hello di esempio seguente è un buon punto di partenza per la creazione di statistiche. Crea statistiche a colonna singola su ogni colonna nella tabella delle dimensioni hello e su ogni colonna di join nelle tabelle dei fatti hello. È sempre possibile aggiungere colonne della tabella dei fatti tooother le statistiche di uno o più colonne in un secondo momento.


## <a name="achievement-unlocked"></a>Obiettivo raggiunto
I dati sono stati caricati correttamente in Azure SQL Data Warehouse. Ottimo lavoro.

##<a name="next-steps"></a>Passaggi successivi
Il caricamento dei dati è hello primo passaggio toodeveloping una soluzione di data warehouse con SQL Data Warehouse. Vedere le risorse di sviluppo in [Tabelle](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) e [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).


<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
