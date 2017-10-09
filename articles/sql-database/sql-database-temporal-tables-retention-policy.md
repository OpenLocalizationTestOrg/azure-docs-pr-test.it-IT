---
title: aaaManage i dati cronologici nelle tabelle temporali con criteri di conservazione | Documenti Microsoft
description: Informazioni su come toouse conservazione temporale criteri tookeep dati cronologici sotto il proprio controllo.
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>Gestire i dati cronologici nelle tabelle temporali con criteri di conservazione
Le tabelle temporali possono aumentare le dimensioni del database più delle tabelle normali, in particolare se si conservano i dati cronologici per un periodo di tempo più lungo. Di conseguenza, i criteri di conservazione dei dati cronologici sono un aspetto importante della pianificazione e gestione del ciclo di vita di hello di ogni tabella temporale. Le tabelle temporali nel database SQL Azure sono dotate di un meccanismo di conservazione di facile uso che aiuta a eseguire questa operazione.

Periodo memorizzazione cronologia temporale può essere configurate a livello di singola tabella hello, che consente agli utenti di criteri di durata flessibile toocreate. L'applicazione di memorizzazione temporale è semplice: è necessario un solo parametro toobe, impostato durante la modifica dello schema o di creazione tabella.

Dopo aver definito i criteri di conservazione, il database SQL di Azure avvia una verifica periodica per controllare se sono presenti righe di cronologia idonee alla pulizia automatica dei dati. Identificazione delle righe corrispondenti e la rimozione dalla tabella di cronologia hello si verificano in modo trasparente, attività in background pianificata, eseguire dal sistema hello hello. Condizione di validità per le righe nella tabella di cronologia hello viene controllato in base colonna hello che rappresenta di fine del periodo SYSTEM_TIME. Se il periodo di memorizzazione, ad esempio, è impostato toosix mesi, le righe della tabella idonee per la pulizia soddisfano hello seguente condizione:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

Nella finestra di hello sopra riportato, si presuppone che **ValidTo** colonna corrisponde toohello fine del periodo SYSTEM_TIME.

## <a name="how-tooconfigure-retention-policy"></a>Come criteri di conservazione tooconfigure?
Prima di configurare criteri di conservazione per una tabella temporale, controllare innanzitutto se è abilitato memorizzazione cronologia temporale *a livello di database hello*.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

Flag del database **is_temporal_history_retention_enabled** è tooON set per impostazione predefinita, ma gli utenti possono modificare con l'istruzione ALTER DATABASE. È inoltre automaticamente tooOFF set dopo [ripristino temporizzato](sql-database-recovery-using-backups.md) operazione. pulizia di memorizzazione cronologia temporale tooenable per il database, eseguire hello seguente istruzione:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> È possibile configurare la conservazione per le tabelle temporali anche se **is_temporal_history_retention_enabled** è impostato su OFF. Tuttavia in questo caso la pulizia automatica delle righe obsolete non verrà attivata.
> 
> 

Criteri di conservazione viene configurato durante la creazione della tabella, specificando un valore per il parametro HISTORY_RETENTION_PERIOD hello:

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

Database SQL di Azure consente il periodo di memorizzazione toospecify con unità di tempo diversi: giorni, settimane, mesi e anni. Se HISTORY_RETENTION_PERIOD viene omesso, viene usata la conservazione INFINITE. È inoltre possibile usare esplicitamente la parola chiave INFINITE.

In alcuni scenari, è opportuno tooconfigure conservazione dopo la creazione della tabella o toochange precedentemente configurato come valore. In questo caso usare l'istruzione ALTER TABLE:

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> Impostazione dell'attributo SYSTEM_VERSIONING tooOFF *non mantiene* valore del periodo di memorizzazione. Impostazione dell'attributo SYSTEM_VERSIONING tooON senza HISTORY_RETENTION_PERIOD specificato esplicitamente risultati nel periodo di conservazione infinito hello.
> 
> 

stato corrente di tooreview del criterio di conservazione hello, tale flag di abilitazione della memorizzazione temporale join a livello di database hello con periodi di memorizzazione per le singole tabelle di query utilizzare hello seguente:

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a>In che modo vengono eliminate le righe obsolete dal database SQL?
il processo di pulizia Hello dipende dal layout indice hello della tabella di cronologia hello. È importante toonotice che *solo le tabelle di cronologia con un indice cluster (albero B o columnstore) possono avere criteri di conservazione finito configurato*. Un'attività in background viene creata tooperform pulizia dei dati obsoleti per tutte le tabelle temporali con periodo di memorizzazione finito.
Logica di pulizia per l'indice cluster rowstore (albero B) di hello Elimina riga obsoleto in blocchi più piccoli (backup too10K) riducendo al minimo l'utilizzo nei log del database e il sottosistema dei / o. Anche se viene utilizzata la logica di pulizia necessarie indice B-tree, ordine di eliminazioni di righe hello anteriore al periodo di conservazione non può essere garantito sia ben. Di conseguenza, *non accettano tutte le dipendenze nell'ordine di pulizia hello nelle applicazioni*.

Hello attività di pulizia per hello clustered columnstore rimuove intero [gruppi di righe](https://msdn.microsoft.com/library/gg492088.aspx) in una sola volta (in genere contiene 1 milione di righe ogni), che è molto efficiente, in particolare quando i dati cronologici viene generati a un ritmo elevato.

![Conservazione di columnstore in cluster](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

Un'ottima compressione dei dati e un'efficace pulizia per la conservazione fanno dell'indice columnstore in cluster la scelta ideale per gli scenari in cui il carico di lavoro genera rapidamente elevate quantità di dati cronologici. Tale modello è tipico per un l'[elaborazione transazionale intensiva dei carichi di lavoro che usano tabelle temporali](https://msdn.microsoft.com/library/mt631669.aspx) per il rilevamento delle modifiche e il controllo, l'analisi delle tendenze o l'inserimento dei dati IoT.

## <a name="index-considerations"></a>Considerazioni sull'indice
attività di pulizia Hello per le tabelle con indice cluster rowstore richiede indice toostart con estremità corrispondente hello hello colonna di periodo SYSTEM_TIME. Se questa colonna non esiste, non è possibile configurare un periodo di conservazione finito:

*Msg 13765, livello 16, stato 1 <br> </br> impostazione periodo di memorizzazione finito non è riuscita nella tabella temporale con controllo delle versioni del sistema 'temporalstagetestdb.dbo.WebsiteUserInfo' perché la tabella di cronologia hello ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' non contiene alcun indice cluster richiesto. È consigliabile creare una columnstore cluster o un indice albero B a partire dalla colonna hello corrispondente alla fine di SYSTEM_TIME period, nella tabella di cronologia hello.*

È importante toonotice che hello tabella di cronologia predefinita creata dal Database di SQL Azure è già un indice, che è conforme a criteri di conservazione è cluster. Se si tenta di tooremove tale indice in una tabella con periodo di memorizzazione finito, operazione non riesce con hello errore seguente:

*Msg 13766, livello 16, stato 1 <br> </br> non è possibile eliminare l'indice cluster hello 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' perché è utilizzato per la pulizia automatica dei dati obsoleti. Prendere in considerazione impostazione HISTORY_RETENTION_PERIOD tooINFINITE sulla tabella di temporale con controllo delle versioni del sistema corrispondente hello se è necessario toodrop questo indice.*

Pulizia sull'indice columnstore cluster hello funziona in modo ottimale se vengono inserite righe cronologiche in ordine crescente (ordinati in base al fine di hello della colonna periodo), che avviene sempre hello quando la tabella di cronologia hello viene popolata in modo esclusivo da hello System _ hello Meccanismo VERSIONIOING. Se righe nella tabella di cronologia hello non vengono ordinate dalla fine della colonna periodo (che può essere case hello se sono stati migrati i dati cronologici esistenti), è necessario ricreare un indice columnstore cluster in indice rowstore con albero B ordinata correttamente, tooachieve ottimale prestazioni.

Evitare di ricompilare l'indice columnstore cluster nella tabella di cronologia hello con periodo di memorizzazione finito di hello, poiché potrebbe essere modificato l'ordinamento in gruppi di righe hello naturalmente imposti dall'operazione di controllo delle versioni di sistema hello. Se si desidera toorebuild l'indice columnstore cluster nella tabella di cronologia hello, a tale scopo crearne uno nuovo nella parte superiore conformi indice albero B, mantenendo l'ordinamento in rowgroup hello necessarie per la pulizia dei dati regolare. Hello stesso approccio deve essere eseguita se si crea una tabella temporale con tabella di cronologia esistente che dispone di un indice di colonna senza ordine dei dati garantita cluster:

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

Quando il periodo di memorizzazione finito è configurato per la tabella di cronologia hello con indice columnstore cluster hello, è possibile creare indici albero B non cluster aggiuntivi in tale tabella:

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

Un tentativo tooexecute prima istruzione non riesce con hello errore seguente:

*Msg 13772, Level 16, State 1 <br></br> Impossibile creare un indice non in cluster in una tabella di cronologia temporale 'WebsiteUserInfoHistory' perché ha un periodo di conservazione definito e l'indice columnstore in cluster è definito.*

## <a name="querying-tables-with-retention-policy"></a>Esecuzione di query su tabelle con criteri di conservazione
Tutte le query sulla tabella temporale hello filtrare automaticamente le righe di cronologia corrispondente di criteri di conservazione finito tooavoid risultati imprevedibili e incoerente, poiché è possono eliminare le righe obsolete tramite attività di pulizia hello, *in qualsiasi punto nel tempo e in ordine arbitrario*.

Hello immagine riportata di seguito viene illustrato il piano di query hello per una query semplice:

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

query Hello piano include ulteriore filtro applicato tooend della colonna periodo (ValidTo) nell'operatore Clustered Index Scan hello nella tabella di cronologia hello (evidenziata). Questo esempio presuppone che il periodo di conservazione di un MONTH sia stato impostato nella tabella WebsiteUserInfo.

![Filtro di query di conservazione](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

Tuttavia, se si esegue una query direttamente in una tabella di cronologia, è possibile vedere le righe precedenti al periodo di conservazione specificato, ma senza alcuna garanzia relativa ai risultati ripetibili. Hello immagine seguente viene illustrato un piano di esecuzione per query hello nella tabella di cronologia hello senza filtri aggiuntivi applicati:

![Esecuzione di query senza filtro di conservazione](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

Non affidare la logica di business alla lettura della tabella di cronologia oltre il periodo di conservazione, perché si potrebbero ottenere risultati incoerenti o imprevisti. È consigliabile usare query temporali con la clausola FOR SYSTEM_TIME per l'analisi dei dati nelle tabelle temporali.

## <a name="point-in-time-restore-considerations"></a>Considerazioni sul ripristino temporizzato
Quando si crea nuovo database da [ripristino esistente database tooa temporizzato nel tempo](sql-database-recovery-using-backups.md), dispone di conservazione temporale disabilitato a livello di database hello. (**is_temporal_history_retention_enabled** tooOFF impostato flag). Questa funzionalità consente tutte le righe di cronologia al momento del ripristino, senza doversi righe obsoleti vengono rimossi prima di ottenere tooquery tooexamine li. È possibile utilizzare anche*controllare i dati cronologici supera il periodo di memorizzazione configurato*.

Si supponga che per una tabella temporale sia specificato il periodo di conservazione MONTH. Se il database è stato creato nel livello di servizio Premium, sarà in grado di toocreate copia del database con stato del database hello dei giorni too35 in hello precedente. Che in modo efficace consentirebbe righe di cronologia tooanalyze di backup too65 giorni eseguendo una query sulla tabella di cronologia hello direttamente.

Se si desidera la pulizia di memorizzazione temporale tooactivate, eseguire hello seguente istruzione Transact-SQL dopo il ripristino temporizzato:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>Passaggi successivi
come le tabelle temporali toouse nelle applicazioni, estrarre toolearn [Introduzione alle tabelle temporali nel Database SQL di Azure](sql-database-temporal-tables.md).

Visita Channel 9 toohear un [reale implementazione temporale storie di successo](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ed espressioni di controllo un [live dimostrazione temporale](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

Per informazioni dettagliate sulle tabelle temporali, esaminare la [documentazione su MSDN](https://msdn.microsoft.com/library/dn935015.aspx).

