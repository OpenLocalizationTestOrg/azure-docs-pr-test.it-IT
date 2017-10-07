---
title: aaaGetting avviato alle tabelle temporali nel Database SQL di Azure | Documenti Microsoft
description: Informazioni su come tooget iniziare con le tabelle temporali nel Database di SQL Azure.
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="29319-103">Introduzione alle tabelle temporali nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="29319-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="29319-104">Le tabelle temporali sono una nuova funzionalità di programmabilità del Database SQL di Azure che consente di tootrack e analizzare hello cronologia completa delle modifiche nei dati, senza necessità di hello di codifica personalizzata.</span><span class="sxs-lookup"><span data-stu-id="29319-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="29319-105">Tabelle temporali mantenere tootime strettamente correlati contesto dei dati in modo che i fatti archiviati possono essere interpretati come valido solo all'interno di periodo specifico di hello.</span><span class="sxs-lookup"><span data-stu-id="29319-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="29319-106">Questa proprietà delle tabelle temporali consente di eseguire un'analisi efficace basata sul tempo e di ottenere informazioni accurate dall'evoluzione dei dati.</span><span class="sxs-lookup"><span data-stu-id="29319-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="29319-107">Scenario temporale</span><span class="sxs-lookup"><span data-stu-id="29319-107">Temporal Scenario</span></span>
<span data-ttu-id="29319-108">Questo articolo illustra i passaggi di hello tooutilize tabelle temporali in uno scenario di applicazione.</span><span class="sxs-lookup"><span data-stu-id="29319-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="29319-109">Si supponga che tootrack attività dell'utente in un nuovo sito Web è in fase di sviluppo da zero o in un sito Web esistente che si desidera tooextend con analitica attività utente.</span><span class="sxs-lookup"><span data-stu-id="29319-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="29319-110">In questo esempio semplificato, si presuppone che il numero di hello di pagine web visitate durante un periodo di tempo è un indicatore che deve toobe acquisiti e monitorato nel database del sito Web hello ospitato nel Database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="29319-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="29319-111">obiettivo di Hello di analisi cronologica di hello dell'attività utente tooget input tooredesign sito e fornire una migliore esperienza per i visitatori hello.</span><span class="sxs-lookup"><span data-stu-id="29319-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="29319-112">modello di database Hello per questo scenario è molto semplice: metrica attività utente viene rappresentata con un campo integer singolo, **PageVisited**e vengono acquisiti con le informazioni di base sul profilo utente hello.</span><span class="sxs-lookup"><span data-stu-id="29319-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="29319-113">Inoltre, per l'analisi di tempo in base, è consigliabile mantenere una serie di righe per ogni utente, in cui ogni riga rappresenta il numero di hello di pagine visitato un determinato utente all'interno di un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="29319-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![Schema](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="29319-115">Fortunatamente, non è necessario tooput alcuno sforzo in toomaintain l'app queste informazioni di attività.</span><span class="sxs-lookup"><span data-stu-id="29319-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="29319-116">Le tabelle temporali con questo processo viene automatizzato - offrendo flessibilità completa durante la progettazione di siti Web e altre ora toofocus sull'analisi di dati hello stesso.</span><span class="sxs-lookup"><span data-stu-id="29319-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="29319-117">Hello solo cosa toodo è tooensure che **WebSiteInfo** tabella è configurata come [temporale con controllo delle versioni del sistema](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="29319-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="29319-118">Hello esatta procedura tooutilize tabelle temporali in questo scenario sono descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="29319-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="29319-119">Passaggio 1: Configurare le tabelle come temporali</span><span class="sxs-lookup"><span data-stu-id="29319-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="29319-120">A seconda che si tratti dello sviluppo di una nuova applicazione o dell'aggiornamento di una esistente, creare le tabelle temporali o modificare tabelle esistenti aggiungendo attributi temporali.</span><span class="sxs-lookup"><span data-stu-id="29319-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="29319-121">In genere, lo scenario può essere una combinazione di queste due opzioni.</span><span class="sxs-lookup"><span data-stu-id="29319-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="29319-122">Eseguire queste azioni usando [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) o qualsiasi altro strumento di sviluppo Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="29319-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29319-123">È consigliabile utilizzare sempre hello versione più recente di Management Studio tooremain sincronizzati con gli aggiornamenti tooMicrosoft Azure e il Database SQL.</span><span class="sxs-lookup"><span data-stu-id="29319-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="29319-124">[Aggiornare SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="29319-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="29319-125">Creare una nuova tabella</span><span class="sxs-lookup"><span data-stu-id="29319-125">Create new table</span></span>
<span data-ttu-id="29319-126">Utilizzare l'elemento menu di scelta "Nuova tabella con controllo delle versioni del sistema" nell'editor di query di Esplora oggetti di SSMS tooopen hello con uno script modello per una tabella temporale e quindi usare il modello di hello toopopulate "Specificare valori per parametri modello" (Ctrl + MAIUSC + M):</span><span class="sxs-lookup"><span data-stu-id="29319-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="29319-128">In SSDT, scelto il modello "Tabella temporale (versioni di sistema)" quando si aggiunge di nuovo progetto di database toohello elementi.</span><span class="sxs-lookup"><span data-stu-id="29319-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="29319-129">Che verrà aperto Progettazione tabelle e abilitare si tooeasily specificare hello layout di tabella:</span><span class="sxs-lookup"><span data-stu-id="29319-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="29319-131">È inoltre possibile una tabella temporale create specificando le istruzioni Transact-SQL hello direttamente, come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="29319-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="29319-132">Si noti che gli elementi obbligatori hello di ogni tabella temporale definizione del periodo hello e clausola SYSTEM_VERSIONING hello con una tabella utente tooanother di riferimento utilizzato per archiviare le versioni di riga cronologiche:</span><span class="sxs-lookup"><span data-stu-id="29319-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="29319-133">Quando si crea una tabella temporale con controllo delle versioni del sistema, hello che accompagna la tabella di cronologia con la configurazione predefinita di hello viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="29319-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="29319-134">tabella di cronologia predefinita Hello contiene un indice albero B cluster nelle colonne periodo hello (inizio fine) con abilitata la compressione di pagina.</span><span class="sxs-lookup"><span data-stu-id="29319-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="29319-135">Questa configurazione è ottimale per la maggior parte di hello degli scenari in cui vengono utilizzate le tabelle temporali, soprattutto per [dati controllo](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="29319-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="29319-136">In questo caso specifico, siamo l'analisi delle tendenze basate sul tempo tooperform tramite una cronologia dei dati più lungo e con set di dati più grande, pertanto la scelta di archiviazione hello per la tabella di cronologia hello è un indice columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="29319-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="29319-137">Un columnstore cluster offre ottimi livelli di compressione e prestazioni per le query analitiche.</span><span class="sxs-lookup"><span data-stu-id="29319-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="29319-138">Consentono di tabelle temporale hello indici tooconfigure flessibilità nelle tabelle correnti e temporali di hello completamente in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="29319-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="29319-139">Sono disponibili nel livello di servizio premium hello solo gli indici ColumnStore.</span><span class="sxs-lookup"><span data-stu-id="29319-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="29319-140">Hello lo script seguente viene illustrato come indice predefinito nella tabella di cronologia può essere modificato toohello clustered columnstore:</span><span class="sxs-lookup"><span data-stu-id="29319-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="29319-141">Le tabelle temporali sono rappresentate in Esplora oggetti di hello con icona specifica di hello per facilitarne l'identificazione, mentre la tabella di cronologia viene visualizzato come nodo figlio.</span><span class="sxs-lookup"><span data-stu-id="29319-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="29319-143">ALTER tootemporal tabella esistente</span><span class="sxs-lookup"><span data-stu-id="29319-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="29319-144">Di seguito illustrano gli scenari alternativi hello in cui hello WebsiteUserInfo tabella esiste già, ma non è stato progettato tookeep una cronologia delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="29319-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="29319-145">In questo caso, è possibile estendere semplicemente hello esistente nella tabella toobecome temporali, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="29319-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="29319-146">Passaggio 2: Eseguire regolarmente il carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="29319-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="29319-147">vantaggio principale di Hello delle tabelle temporali è non necessario toochange o modificare il sito Web in qualsiasi modo tooperform di revisione.</span><span class="sxs-lookup"><span data-stu-id="29319-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="29319-148">Dopo la creazione, le tabelle temporali mantengono in modo trasparente le versioni precedenti delle righe ogni volta che si apportano modifiche ai dati.</span><span class="sxs-lookup"><span data-stu-id="29319-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="29319-149">In ordine tooleverage rilevamento automatico delle modifiche per questo particolare scenario, si aggiorna solo colonna **PagesVisited** ogni volta che quando l'utente termina proprio sessione sul sito Web di hello:</span><span class="sxs-lookup"><span data-stu-id="29319-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="29319-150">È importante toonotice che hello query di aggiornamento non è necessario ora esatta di hello tooknow quando si è verificato operazione effettiva hello né come verranno mantenuti i dati cronologici per analisi successive.</span><span class="sxs-lookup"><span data-stu-id="29319-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="29319-151">Entrambi gli aspetti vengono gestiti automaticamente dal Database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="29319-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="29319-152">Hello diagramma seguente illustra la modalità di generazione dati di cronologia in ogni aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="29319-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="29319-154">Passaggio 3: Eseguire l'analisi dei dati cronologici</span><span class="sxs-lookup"><span data-stu-id="29319-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="29319-155">Quando il controllo delle versioni di sistema temporale è abilitato, per l'analisi dei dati cronologici è sufficiente eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="29319-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="29319-156">In questo articolo è fornire alcuni esempi di scenari comuni analysis - toolearn tutti i dettagli, provare varie opzioni introdotte con hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clausola.</span><span class="sxs-lookup"><span data-stu-id="29319-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="29319-157">toosee hello primi 10 utenti ordinati in base al numero di hello di pagine web visitate a partire da un'ora fa, eseguire la query:</span><span class="sxs-lookup"><span data-stu-id="29319-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="29319-158">È possibile modificare facilmente questa query tooanalyze hello visite a partire da un giorno fa, un mese fa o in qualsiasi punto hello ultimi desiderato.</span><span class="sxs-lookup"><span data-stu-id="29319-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="29319-159">tooperform base l'analisi statistica per hello giorno precedente, utilizzare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="29319-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="29319-160">toosearch per attività di un utente specifico, all'interno di un periodo di tempo, utilizzare hello CONTAINED IN clausola:</span><span class="sxs-lookup"><span data-stu-id="29319-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="29319-161">La visualizzazione grafica risulta particolarmente utile per le query temporali, perché permette di visualizzare tendenze e modelli d'uso in modo molto semplice e intuitivo:</span><span class="sxs-lookup"><span data-stu-id="29319-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="29319-163">Evoluzione dello schema di tabella</span><span class="sxs-lookup"><span data-stu-id="29319-163">Evolving table schema</span></span>
<span data-ttu-id="29319-164">In genere, sarà necessario schema della tabella temporale hello toochange mentre si esegue lo sviluppo di app.</span><span class="sxs-lookup"><span data-stu-id="29319-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="29319-165">A tale scopo, è sufficiente eseguire istruzioni ALTER TABLE regolari e Database SQL di Azure verranno propagate in modo appropriato la tabella di cronologia toohello le modifiche.</span><span class="sxs-lookup"><span data-stu-id="29319-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="29319-166">Hello script riportato di seguito viene illustrato come aggiungere un attributo aggiuntivo per il rilevamento:</span><span class="sxs-lookup"><span data-stu-id="29319-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="29319-167">Analogamente, è possibile modificare la definizione di colonna mentre il carico di lavoro è attivo:</span><span class="sxs-lookup"><span data-stu-id="29319-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="29319-168">Infine, è possibile rimuovere una colonna non più necessaria.</span><span class="sxs-lookup"><span data-stu-id="29319-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="29319-169">In alternativa, usare più recente [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) schema delle tabelle temporali toochange mentre si è connessi toohello database (modalità online) o come parte del progetto di database hello (modalità offline).</span><span class="sxs-lookup"><span data-stu-id="29319-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="29319-170">Controllo della conservazione dei dati cronologici</span><span class="sxs-lookup"><span data-stu-id="29319-170">Controlling retention of historical data</span></span>
<span data-ttu-id="29319-171">Con le tabelle temporali con controllo delle versioni del sistema, la tabella di cronologia hello può aumentare la dimensione del database hello più tabelle normali.</span><span class="sxs-lookup"><span data-stu-id="29319-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="29319-172">Una tabella di cronologia di grandi dimensioni e in continua crescita può costituire un problema dovuto toopure i costi di archiviazione, nonché sulle prestazioni dell'impatto sulle query temporali.</span><span class="sxs-lookup"><span data-stu-id="29319-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="29319-173">Di conseguenza, lo sviluppo di un criterio di conservazione dati per la gestione dei dati nella tabella di cronologia hello è un aspetto importante della pianificazione e gestione del ciclo di vita di hello di ogni tabella temporale.</span><span class="sxs-lookup"><span data-stu-id="29319-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="29319-174">Database SQL di Azure, è necessario hello approcci per la gestione dei dati cronologici in una tabella temporale hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="29319-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="29319-175">Partizionamento di tabelle</span><span class="sxs-lookup"><span data-stu-id="29319-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="29319-176">Script di pulizia personalizzato</span><span class="sxs-lookup"><span data-stu-id="29319-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="29319-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="29319-177">Next steps</span></span>
<span data-ttu-id="29319-178">Per informazioni dettagliate sulle tabelle temporali, vedere la [documentazione MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="29319-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="29319-179">Visita Channel 9 toohear un [reale implementazione temporale storie di successo](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ed espressioni di controllo un [live dimostrazione temporale](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="29319-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

