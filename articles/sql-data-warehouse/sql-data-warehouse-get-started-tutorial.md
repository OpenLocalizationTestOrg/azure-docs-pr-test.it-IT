---
title: iniziare aaaAzure SQL Data Warehouse - esercitazione | Documenti Microsoft
description: "Questa esercitazione viene illustrato come tooprovision e caricare i dati in Azure SQL Data Warehouse. Si apprenderà inoltre hello nozioni fondamentali per la scalabilità, la sospensione e l'ottimizzazione."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>Introduzione a SQL Data Warehouse

Questa esercitazione viene illustrato come tooprovision e caricare i dati in Azure SQL Data Warehouse. Si apprenderà inoltre hello nozioni fondamentali per la scalabilità, la sospensione e l'ottimizzazione. Al termine, che verrà tooquery pronto ed esplorare il data warehouse.

**Toocomplete tempo stimato:** si tratta di un'esercitazione end-to-end con codice di esempio che accetta toocomplete circa 30 minuti dopo che siano soddisfatti i prerequisiti di hello. 

## <a name="prerequisites"></a>Prerequisiti

esercitazione Hello presuppone che si ha familiarità con concetti di base di SQL Data Warehouse. Se sono necessarie informazioni introduttive, vedere [Informazioni su Azure SQL Data Warehouse](sql-data-warehouse-overview-what-is.md) 

### <a name="sign-up-for-microsoft-azure"></a>Iscrizione a Microsoft Azure
Se si dispone già di un account di Microsoft Azure, è necessario toosign per uno toouse questo servizio. Se si ha già un account, è possibile ignorare questo passaggio. 

1. Spostarsi tra le pagine di account toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. Creare un account Azure gratuito o acquistare un account.
3. Seguire le istruzioni di hello

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>Installare i driver del client SQL e gli strumenti appropriati

La maggior parte degli strumenti client di SQL è possono connettersi tooSQL Data Warehouse utilizzando JDBC, ODBC o ADO.NET. A causa di toohello numero elevato di funzionalità di T-SQL che supporta SQL Data Warehouse, alcune applicazioni client non sono completamente compatibili con SQL Data Warehouse.

Se si esegue un sistema operativo Windows, è consigliabile usare [Visual Studio] o [SQL Server Management Studio].

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>Creare un SQL Data Warehouse

SQL Data Warehouse è un tipo di database speciale, progettato per l'elaborazione parallela massiva (MPP, Massively Parallel Processing). database Hello è distribuita tra più nodi e di elaborazione delle query in parallelo. SQL Data Warehouse è un nodo del controllo che coordina le attività di hello di tutti i nodi di hello. i nodi di Hello utilizzano toomanage Database SQL i dati.  

> [!NOTE]
> La creazione di un'istanza di SQL Data Warehouse può avere come risultato un nuovo servizio fatturabile.  Per altre informazioni, vedere [SQL Data Warehouse Prezzi](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).
>

### <a name="create-a-data-warehouse"></a>Creare un data warehouse

1. Sign in hello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo** > **Database** > **SQL Data Warehouse**.

    ![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png)![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. Compilare i dettagli della distribuzione

    **Nome database**: scegliere un nome qualsiasi. Se si dispone di più data warehouse, è consigliabile che i nomi di includono i dettagli, ad esempio area hello, ambiente, ad esempio *mydw-westus-1-test*.

    **Sottoscrizione**: sottoscrizione di Azure.

    **Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente.
    > [!NOTE]
    > I gruppi di risorse sono utili per l'amministrazione delle risorse, ad esempio per la definizione dell'ambito del controllo di accesso e per la distribuzione basata su modelli. Per altre informazioni sui gruppi di risorse di Azure e sulle procedure consigliate, vedere [qui](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)

    **Origine**: database vuoto.

    **Server**: creato nel server di selezionare hello [prerequisiti].

    **Regole di confronto**: lasciare regole di confronto predefinite hello SQL_Latin1_General_CP1_CI_AS.

    **Selezionare prestazioni**: È consigliabile iniziare con 400DWU standard hello.

4. Scegliere **Pin toodashboard** ![tooDashboard Pin](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. Tranquillamente e attendere il toodeploy warehouse dati! È norma per questo processo tootake alcuni minuti. portale Hello notifica quando il data warehouse è toouse pronto. 

## <a name="connect-toosql-data-warehouse"></a>Connettersi tooSQL Data Warehouse

In questa esercitazione utilizza SQL Server Management Studio (SSMS) tooconnect toohello data warehouse. È possibile connettere tooSQL Data Warehouse tramite questi connettori supportati: ADO.NET, JDBC, ODBC e PHP. È possibile che le funzionalità siano limitate per gli strumenti non supportati da Microsoft.


### <a name="get-connection-information"></a>Ottenere informazioni di connessione

data warehouse di tooconnect tooyour, è necessario tooconnect tramite hello logico SQL server è stato creato in [prerequisiti].

1. Selezionare il data warehouse dal dashboard di hello o cercare le risorse.

    ![Dashboard di SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. Trovare il nome completo di hello per server SQL logico hello.

    ![Selezionare il nome del server](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. Aprire SQL Server Management Studio e utilizzare un oggetto explorer tooconnect toothis server usando credenziali di amministratore server hello è stato creato in [prerequisiti]

    ![Connettersi con SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

Se viene eseguito correttamente, è ora connesso tooyour logico SQL server. Poiché è stato eseguito l'accesso hello amministratore del server, è possibile connettersi a database tooany ospitato dal server di hello, tra cui database master hello. 

Account di amministratore di un solo server e dispone di hello la maggior parte dei privilegi di qualsiasi utente. Prestare attenzione tooallow non Troppi utenti la password di amministratore dell'organizzazione tooknow hello. 

È anche possibile usare un account di amministratore di Azure Active Directory. Microsoft non fornire qui i dettagli di hello. Se si desidera toolearn ulteriori informazioni sull'utilizzo di autenticazione di Azure Active Directory, vedere [autenticazione di Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

Verrà ora illustrata la creazione di altri account di accesso e utenti.


## <a name="create-a-database-user"></a>Creare un utente database

In questo passaggio viene creato un tooaccess di account utente del data warehouse. Viene inoltre illustrata la modalità toogive toorun di possibilità hello tale utente esegue una query con una grande quantità di memoria e risorse della CPU.

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>Note sulle classi di risorse per l'allocazione delle risorse tooqueries

- tookeep dati sicuri, non utilizzare query toorun amministratore del server hello nei database di produzione. Ha hello la maggior parte dei privilegi di qualsiasi utente e utilizzarlo tooperform operazioni sui dati utente inserisce i dati a rischio. Inoltre, poiché l'amministratore del server hello deve tooperform le operazioni di gestione, viene eseguito operazioni con solo una piccola allocazione di memoria e risorse della CPU. 

- SQL Data Warehouse vengono utilizzati i ruoli di database predefiniti, chiamata tooallocate quantità di memoria, le risorse della CPU e concorrenza slot toousers diverse classi di risorse. Ogni utente può appartenere a classe di risorse di piccola, Media, grande o molto grande tooa. Hello classe di risorse dell'utente determina hello risorse hello utente è toorun query e operazioni di caricamento.

- Per la compressione dati ottimale, utente hello potrebbe essere necessario tooload di grandi dimensioni o allocazioni di dimensioni molto grandi. Per altre informazioni sulle classi di risorse, vedere [qui](./sql-data-warehouse-develop-concurrency.md#resource-classes):

### <a name="create-an-account-that-can-control-a-database"></a>Creare un account che possa controllare un database

Poiché si è connessi in hello amministratore del server è necessario utenti e accessi toocreate autorizzazioni.

1. Usando SSMS o un altro client di query, aprire una nuova query per **master**.

    ![Nuova query nel master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nuova query nel master 1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. Nella finestra query hello, eseguire questo toocreate comando T-SQL, un account di accesso denominato MedRCLogin e un utente denominato LoadingUser. Questo account di accesso può connettersi toohello logico SQL server.

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. Ora l'esecuzione di query hello *database SQL Data Warehouse*, creare un utente del database basato su account di accesso creato tooaccess hello ed eseguire operazioni sul database hello.

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. Assegnare hello database controllo autorizzazioni toohello database utente denominato NYT. 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > Se il nome del database contiene segni meno, toowrap assicurarsi di essere in parentesi quadre. 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>Assegnare le allocazioni di hello utente medio di risorse

1. Eseguire questo toomake comando T-SQL it un membro della classe di risorse medium hello, che viene chiamato mediumrc. 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > Fare clic su [qui](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn ulteriori informazioni sulle classi di concorrenza e la risorsa. 
    >

2. Connessione server logico toohello con nuove credenziali hello

    ![Accedere con il nuovo account](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>Caricare dati dall'archiviazione BLOB di Azure

Si è ora dati tooload pronto in data warehouse. Questo passaggio illustra come blob di dati di file cab di tooload New York City taxi da un'archiviazione di Azure pubblico. 

- Un modo comune dati tooload in SQL Data Warehouse sono toofirst spostare risorse di archiviazione blob tooAzure dati hello e caricarla in un data warehouse. toomake è più facile toounderstand come tooload, sono disponibili dati di file cab taxi New York già ospitati in un blob di archiviazione di Azure pubblico. 

- Per riferimento futuro, toolearn come tooget tooAzure i dati blob di archiviazione o tooload direttamente dall'origine in SQL Data Warehouse, vedere hello [durante il caricamento di panoramica](sql-data-warehouse-overview-load.md).


### <a name="define-external-data"></a>Definire i dati esterni

1. Creare una chiave master. È necessario solo toocreate una chiave master una sola volta per ogni database. 

    ```sql
    CREATE MASTER KEY;
    ```

2. Definire il percorso di hello del blob di Azure che contiene i dati di file cab taxi hello hello.  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. Definire i formati di file esterni hello

    Hello ```CREATE EXTERNAL FILE FORMAT``` comando è toospecify utilizzato il formato di file che contengono dati esterni hello. Questi file includono testo delimitato da uno o più caratteri, definiti delimitatori. A scopo dimostrativo, i dati di file cab di hello taxi vengono archiviati come dati non compressi e come dati compressi gzip.

    Eseguire questi comandi di T-SQL toodefine due formati: non compressi e compressi.

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  Creare uno schema per il formato di file esterni. 

    ```sql
    CREATE SCHEMA ext;
    ```
5. Creare tabelle esterne di hello. Queste tabelle fanno riferimento a dati archiviati nell'archivio BLOB di Azure. Eseguire hello toocreate comandi T-SQL seguente diverse tabelle esterne che toohello punto tutti i blob di Azure è stato definito in precedenza nell'origine dati esterna.

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>Importare dati hello dall'archiviazione blob di Azure.

SQL Data Warehouse supporta un'istruzione chiave denominata CREATE TABLE AS SELECT (CTAS). Questa istruzione crea una nuova tabella in base ai risultati di hello di un'istruzione select. Hello nuova tabella include hello stessi colonne e tipi di dati come risultato di hello hello istruzione select.  Si tratta di un dati tooimport modo elegante dall'archiviazione blob di Azure in SQL Data Warehouse.

1. Eseguire questo script tooimport i dati.

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. Visualizzare i dati man mano che vengono caricati.

   Vengono caricati alcuni GB di dati, che vengono compressi in indici cluster columnstore a prestazioni elevate. Eseguire hello seguente query che utilizza uno stato di hello tooshow viste a gestione dinamica del carico hello. Dopo avere avviato la query hello, trascinare un caffè e un allenamento mentre SQL Data Warehouse non alcuni pesante.
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. Visualizzare tutte le query di sistema.

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. I dati vengono caricati in Azure SQL Data Warehouse.

    ![Visualizzare i dati caricati](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>Ottimizzare le prestazioni di query

Esistono diversi le prestazioni delle query tooimprove modi e tooachieve hello velocità delle prestazioni di SQL Data Warehouse progettato tooprovide.  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>Vedere l'effetto di hello dell'aumento delle prestazioni delle query 

Le prestazioni delle query tooimprove unidirezionale sono tooscale risorse modificando hello DWU servizio livello per il data warehouse. Ogni livello di servizio ha un costo maggiore, ma è possibile ridurre o sospendere le risorse in qualsiasi momento. 

In questo passaggio si confrontano le prestazioni in due diverse impostazioni DWU.

Innanzitutto, consente di ridimensionare ridimensionamento hello verso il basso too100 DWU in modo è possibile ottenere un'idea di come un nodo di calcolo potrebbe eseguire autonomamente.

1. Passare toohello portale e selezionare il Data Warehouse di SQL.

2. Selezione scala nel Pannello di hello SQL Data Warehouse. 

    ![Ridimensionare SQL Data Warehouse dal portale](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. Riscontri di salvataggio e ridurre le prestazioni di hello barra too100 DWU.

    ![Ridimensionare e salvare](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. Attendere il toofinish operazione di scala.

    > [!NOTE]
    > Non è possibile eseguire query durante la modifica scala hello. Il ridimensionamento **termina** tutte le query attualmente in esecuzione. È possibile riavviarle al termine dell'operazione di hello.
    >
    
5. Eseguire un'operazione di analisi sui dati di andata e ritorno hello, selezionando hello milioni voci superiore per tutte le colonne di hello. Se si è rapidamente toomove eager su, è disponibile tooselect meno righe. Prendere nota di hello tempo toorun questa operazione.

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. Ridimensionare il data warehouse di eseguire il backup too400 DWU. Tenere presente che ogni 100 DWU consiste nell'aggiunta di un altro calcolo nodo tooyour Azure SQL Data Warehouse.

7. Eseguire di nuovo la query hello! La differenza dovrebbe essere significativa. 

    > [!NOTE]
    > Poiché query hello restituisce una grande quantità di dati, la disponibilità di larghezza di banda hello della macchina di hello in esecuzione SQL Server Management Studio potrebbe essere un collo di bottiglia delle prestazioni. e ciò potrebbe impedire di notare miglioramenti delle prestazioni.

> [!NOTE]
> Questo perché SQL Data Warehouse fa uso dell'elaborazione parallela massiva (Massively Parallel Processing, MPP). Le query che analizzano o eseguono le funzioni analitiche milioni di righe potenza hello true di Azure SQL Data Warehouse.
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>Vedere l'effetto di hello delle statistiche sulle prestazioni delle query

1. Eseguire una query che join hello tabella data con la tabella di andata e ritorno di hello

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    Questa query richiede un certo tempo, in quanto SQL Data Warehouse contiene dati tooshuffle prima di eseguire il join hello. Join non hanno dati tooshuffle se sono dati progettato toojoin hello allo stesso modo, viene distribuito. L'argomento non viene approfondito oltre in questo articolo. 

2. Le statistiche fanno la differenza. 
3. Eseguire le statistiche toocreate istruzione sulle colonne di join hello.

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > SQL Data Warehouse non gestisce automaticamente le statistiche. Le statistiche sono importanti per le prestazioni delle query ed è consigliabile creare e aggiornare le statistiche.
    > 
    > **La maggior parte dei vantaggi hello si ottengono con le statistiche su colonne coinvolte nel join, le colonne utilizzate nelle hello dove clausola e le colonne disponibili in GROUP BY.**
    >

3. Eseguire di nuovo query hello dai prerequisiti e osservare le differenze di prestazioni. Anche se le differenze di hello delle prestazioni delle query non come delicate come la scalabilità verticale, si noterà un velocizzare. 

## <a name="next-steps"></a>Passaggi successivi

È ora pronto tooquery ed esplorare. Vedere le procedure consigliate o i suggerimenti.

Se il termine esplorazione per giorno hello, rendere toopause che l'istanza. Nell'ambiente di produzione, si può verificare un notevole risparmio per la sospensione e la scalabilità toomeet le esigenze aziendali.

![Sospendi](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>Vedere anche

[Gestione della concorrenza e del carico di lavoro][]

[Procedure consigliate per Azure SQL Data Warehouse][]

[Monitoraggio delle query][]

[Post di blog Prime 10 procedure consigliate per la creazione di un data warehouse relazionale di dimensioni elevate][]

[La migrazione dei dati tooAzure SQL Data Warehouse][]

[Gestione della concorrenza e del carico di lavoro]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Procedure consigliate per Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Monitoraggio delle query]: sql-data-warehouse-manage-monitor.md
[Post di blog Prime 10 procedure consigliate per la creazione di un data warehouse relazionale di dimensioni elevate]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[La migrazione dei dati tooAzure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[prerequisiti]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
