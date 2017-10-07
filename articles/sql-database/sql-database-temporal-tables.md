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
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Introduzione alle tabelle temporali nel database SQL di Azure
Le tabelle temporali sono una nuova funzionalità di programmabilità del Database SQL di Azure che consente di tootrack e analizzare hello cronologia completa delle modifiche nei dati, senza necessità di hello di codifica personalizzata. Tabelle temporali mantenere tootime strettamente correlati contesto dei dati in modo che i fatti archiviati possono essere interpretati come valido solo all'interno di periodo specifico di hello. Questa proprietà delle tabelle temporali consente di eseguire un'analisi efficace basata sul tempo e di ottenere informazioni accurate dall'evoluzione dei dati.

## <a name="temporal-scenario"></a>Scenario temporale
Questo articolo illustra i passaggi di hello tooutilize tabelle temporali in uno scenario di applicazione. Si supponga che tootrack attività dell'utente in un nuovo sito Web è in fase di sviluppo da zero o in un sito Web esistente che si desidera tooextend con analitica attività utente. In questo esempio semplificato, si presuppone che il numero di hello di pagine web visitate durante un periodo di tempo è un indicatore che deve toobe acquisiti e monitorato nel database del sito Web hello ospitato nel Database SQL Azure. obiettivo di Hello di analisi cronologica di hello dell'attività utente tooget input tooredesign sito e fornire una migliore esperienza per i visitatori hello.

modello di database Hello per questo scenario è molto semplice: metrica attività utente viene rappresentata con un campo integer singolo, **PageVisited**e vengono acquisiti con le informazioni di base sul profilo utente hello. Inoltre, per l'analisi di tempo in base, è consigliabile mantenere una serie di righe per ogni utente, in cui ogni riga rappresenta il numero di hello di pagine visitato un determinato utente all'interno di un determinato periodo di tempo.

![Schema](./media/sql-database-temporal-tables/AzureTemporal1.png)

Fortunatamente, non è necessario tooput alcuno sforzo in toomaintain l'app queste informazioni di attività. Le tabelle temporali con questo processo viene automatizzato - offrendo flessibilità completa durante la progettazione di siti Web e altre ora toofocus sull'analisi di dati hello stesso. Hello solo cosa toodo è tooensure che **WebSiteInfo** tabella è configurata come [temporale con controllo delle versioni del sistema](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). Hello esatta procedura tooutilize tabelle temporali in questo scenario sono descritti di seguito.

## <a name="step-1-configure-tables-as-temporal"></a>Passaggio 1: Configurare le tabelle come temporali
A seconda che si tratti dello sviluppo di una nuova applicazione o dell'aggiornamento di una esistente, creare le tabelle temporali o modificare tabelle esistenti aggiungendo attributi temporali. In genere, lo scenario può essere una combinazione di queste due opzioni. Eseguire queste azioni usando [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) o qualsiasi altro strumento di sviluppo Transact-SQL.

> [!IMPORTANT]
> È consigliabile utilizzare sempre hello versione più recente di Management Studio tooremain sincronizzati con gli aggiornamenti tooMicrosoft Azure e il Database SQL. [Aggiornare SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Creare una nuova tabella
Utilizzare l'elemento menu di scelta "Nuova tabella con controllo delle versioni del sistema" nell'editor di query di Esplora oggetti di SSMS tooopen hello con uno script modello per una tabella temporale e quindi usare il modello di hello toopopulate "Specificare valori per parametri modello" (Ctrl + MAIUSC + M):

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

In SSDT, scelto il modello "Tabella temporale (versioni di sistema)" quando si aggiunge di nuovo progetto di database toohello elementi. Che verrà aperto Progettazione tabelle e abilitare si tooeasily specificare hello layout di tabella:

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

È inoltre possibile una tabella temporale create specificando le istruzioni Transact-SQL hello direttamente, come illustrato nel seguente esempio hello. Si noti che gli elementi obbligatori hello di ogni tabella temporale definizione del periodo hello e clausola SYSTEM_VERSIONING hello con una tabella utente tooanother di riferimento utilizzato per archiviare le versioni di riga cronologiche:

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

Quando si crea una tabella temporale con controllo delle versioni del sistema, hello che accompagna la tabella di cronologia con la configurazione predefinita di hello viene creato automaticamente. tabella di cronologia predefinita Hello contiene un indice albero B cluster nelle colonne periodo hello (inizio fine) con abilitata la compressione di pagina. Questa configurazione è ottimale per la maggior parte di hello degli scenari in cui vengono utilizzate le tabelle temporali, soprattutto per [dati controllo](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

In questo caso specifico, siamo l'analisi delle tendenze basate sul tempo tooperform tramite una cronologia dei dati più lungo e con set di dati più grande, pertanto la scelta di archiviazione hello per la tabella di cronologia hello è un indice columnstore cluster. Un columnstore cluster offre ottimi livelli di compressione e prestazioni per le query analitiche. Consentono di tabelle temporale hello indici tooconfigure flessibilità nelle tabelle correnti e temporali di hello completamente in modo indipendente. 

> [!NOTE]
> Sono disponibili nel livello di servizio premium hello solo gli indici ColumnStore.
>

Hello lo script seguente viene illustrato come indice predefinito nella tabella di cronologia può essere modificato toohello clustered columnstore:

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

Le tabelle temporali sono rappresentate in Esplora oggetti di hello con icona specifica di hello per facilitarne l'identificazione, mentre la tabella di cronologia viene visualizzato come nodo figlio.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>ALTER tootemporal tabella esistente
Di seguito illustrano gli scenari alternativi hello in cui hello WebsiteUserInfo tabella esiste già, ma non è stato progettato tookeep una cronologia delle modifiche. In questo caso, è possibile estendere semplicemente hello esistente nella tabella toobecome temporali, come illustrato nell'esempio seguente hello:

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

## <a name="step-2-run-your-workload-regularly"></a>Passaggio 2: Eseguire regolarmente il carico di lavoro
vantaggio principale di Hello delle tabelle temporali è non necessario toochange o modificare il sito Web in qualsiasi modo tooperform di revisione. Dopo la creazione, le tabelle temporali mantengono in modo trasparente le versioni precedenti delle righe ogni volta che si apportano modifiche ai dati. 

In ordine tooleverage rilevamento automatico delle modifiche per questo particolare scenario, si aggiorna solo colonna **PagesVisited** ogni volta che quando l'utente termina proprio sessione sul sito Web di hello:

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

È importante toonotice che hello query di aggiornamento non è necessario ora esatta di hello tooknow quando si è verificato operazione effettiva hello né come verranno mantenuti i dati cronologici per analisi successive. Entrambi gli aspetti vengono gestiti automaticamente dal Database SQL di Azure hello. Hello diagramma seguente illustra la modalità di generazione dati di cronologia in ogni aggiornamento.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>Passaggio 3: Eseguire l'analisi dei dati cronologici
Quando il controllo delle versioni di sistema temporale è abilitato, per l'analisi dei dati cronologici è sufficiente eseguire una query. In questo articolo è fornire alcuni esempi di scenari comuni analysis - toolearn tutti i dettagli, provare varie opzioni introdotte con hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clausola.

toosee hello primi 10 utenti ordinati in base al numero di hello di pagine web visitate a partire da un'ora fa, eseguire la query:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

È possibile modificare facilmente questa query tooanalyze hello visite a partire da un giorno fa, un mese fa o in qualsiasi punto hello ultimi desiderato.

tooperform base l'analisi statistica per hello giorno precedente, utilizzare hello di esempio seguente:

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

toosearch per attività di un utente specifico, all'interno di un periodo di tempo, utilizzare hello CONTAINED IN clausola:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

La visualizzazione grafica risulta particolarmente utile per le query temporali, perché permette di visualizzare tendenze e modelli d'uso in modo molto semplice e intuitivo:

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>Evoluzione dello schema di tabella
In genere, sarà necessario schema della tabella temporale hello toochange mentre si esegue lo sviluppo di app. A tale scopo, è sufficiente eseguire istruzioni ALTER TABLE regolari e Database SQL di Azure verranno propagate in modo appropriato la tabella di cronologia toohello le modifiche. Hello script riportato di seguito viene illustrato come aggiungere un attributo aggiuntivo per il rilevamento:

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

Analogamente, è possibile modificare la definizione di colonna mentre il carico di lavoro è attivo:

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Infine, è possibile rimuovere una colonna non più necessaria.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

In alternativa, usare più recente [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) schema delle tabelle temporali toochange mentre si è connessi toohello database (modalità online) o come parte del progetto di database hello (modalità offline).

## <a name="controlling-retention-of-historical-data"></a>Controllo della conservazione dei dati cronologici
Con le tabelle temporali con controllo delle versioni del sistema, la tabella di cronologia hello può aumentare la dimensione del database hello più tabelle normali. Una tabella di cronologia di grandi dimensioni e in continua crescita può costituire un problema dovuto toopure i costi di archiviazione, nonché sulle prestazioni dell'impatto sulle query temporali. Di conseguenza, lo sviluppo di un criterio di conservazione dati per la gestione dei dati nella tabella di cronologia hello è un aspetto importante della pianificazione e gestione del ciclo di vita di hello di ogni tabella temporale. Database SQL di Azure, è necessario hello approcci per la gestione dei dati cronologici in una tabella temporale hello seguenti:

* [Partizionamento di tabelle](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Script di pulizia personalizzato](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Passaggi successivi
Per informazioni dettagliate sulle tabelle temporali, vedere la [documentazione MSDN](https://msdn.microsoft.com/library/dn935015.aspx).
Visita Channel 9 toohear un [reale implementazione temporale storie di successo](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ed espressioni di controllo un [live dimostrazione temporale](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

