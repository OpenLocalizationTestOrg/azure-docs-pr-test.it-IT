---
title: aaaMigrate i dati di Azure esistenti warehouse archiviazione toopremium | Documenti Microsoft
description: Istruzioni per la migrazione di un'archiviazione toopremium esistente del data warehouse
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Eseguire la migrazione di archiviazione del data warehouse toopremium
Azure SQL Data Warehouse ha recentemente introdotto l'[archiviazione Premium per una maggiore prevedibilità delle prestazioni][premium storage for greater performance predictability]. Dati esistenti magazzini attualmente nell'archivio standard è ora possibile eseguire la migrazione archiviazione toopremium. È possibile sfruttare la migrazione automatica, oppure se si preferisce toocontrol quando toomigrate (che implicano tempi di inattività), è possibile eseguire hello migrazione manualmente.

Se si dispone di più di un data warehouse, utilizzare hello [pianificazione migrazione automatica] [ automatic migration schedule] toodetermine quando verranno inoltre migrato.

## <a name="determine-storage-type"></a>Determinare il tipo di archiviazione
Se è stato creato un data warehouse prima hello seguenti date, archiviazione standard attualmente in uso.

| **Area** | **Data warehouse creato prima di questa data** |
|:--- |:--- |
| Australia orientale |Archiviazione Premium non ancora disponibile |
| Cina orientale |1 novembre 2016 |
| Cina settentrionale |1 novembre 2016 |
| Germania centrale |1 novembre 2016 |
| Germania nord-orientale |1 novembre 2016 |
| India occidentale |Archiviazione Premium non ancora disponibile |
| Giappone occidentale |Archiviazione Premium non ancora disponibile |
| Stati Uniti centro-settentrionali |10 novembre 2016 |

## <a name="automatic-migration-details"></a>Dettagli sulla migrazione automatica
Per impostazione predefinita, si verrà eseguita la migrazione del database è compreso tra 6:00 e le 6.00 nell'ora locale dell'area durante hello [pianificazione migrazione automatica][automatic migration schedule]. Il data warehouse esistente non sarà utilizzabile durante la migrazione di hello. migrazione Hello richiederà circa un'ora per terabyte di archiviazione per ogni del data warehouse. Non ti durante qualsiasi parte della migrazione automatica hello.

> [!NOTE]
> Una volta completata la migrazione di hello, il data warehouse sarà nuovamente online e utilizzabile.
>
>

Microsoft sta diventando hello passaggi toocomplete hello migrazione (questi non richiedono alcun intervento da parte dell'utente). In questo esempio, immaginare che il data warehouse esistente in archiviazione Standard sia attualmente denominato "MyDW".

1. Microsoft Rinomina "MyDW" troppo "MyDW_DO_NOT_USE_ [Timestamp]".
2. Microsoft sospende "MyDW" in "MyDW_DO_NOT_USE_[Timestamp]". Nel mentre, viene eseguito il backup. In caso di problemi, il processo potrebbe essere sospeso e riprendere più volte.
3. Microsoft consente di creare un nuovo data warehouse, denominato "MyDW" in archiviazione premium da backup hello prese nel passaggio 2. "MyDW" non verranno visualizzati fino a dopo il ripristino di hello.
4. Dopo il ripristino di hello, "MyDW" restituisce toohello stessi dati del data warehouse di unità e sullo stato (sospesa o attiva) in cui si trovava prima della migrazione hello.
5. Al termine della migrazione hello, Microsoft eliminerà "MyDW_DO_NOT_USE_ [Timestamp]".

> [!NOTE]
> Hello seguenti impostazioni non vengono trasferiti durante la migrazione di hello:
>
> * Il controllo a livello di database hello deve toobe nuovamente abilitata.
> * Regole del firewall a livello di database hello necessario toobe aggiunto di nuovo. Regole del firewall a livello di server hello non sono interessate.
>
>

### <a name="automatic-migration-schedule"></a>pianificazione della migrazione automatica
Migrazioni automatiche durante hello base alla pianificazione di interruzione tra 6:00 e 6:00:00 (ora locale per ogni area).

| **Area** | **Data di inizio prevista** | **Data di fine prevista** |
|:--- |:--- |:--- |
| Australia orientale |Non ancora determinata |Non ancora determinata |
| Cina orientale |9 gennaio 2017 |13 gennaio 2017 |
| Cina settentrionale |9 gennaio 2017 |13 gennaio 2017 |
| Germania centrale |9 gennaio 2017 |13 gennaio 2017 |
| Germania nord-orientale |9 gennaio 2017 |13 gennaio 2017 |
| India occidentale |Non ancora determinata |Non ancora determinata |
| Giappone occidentale |Non ancora determinata |Non ancora determinata |
| Stati Uniti centro-settentrionali |9 gennaio 2017 |13 gennaio 2017 |

## <a name="self-migration-toopremium-storage"></a>Archiviazione toopremium migrazione automatica
Se si desidera toocontrol quando si verifica il tempo di inattività, è possibile utilizzare hello seguire passaggi toomigrate un data warehouse esistente di archiviazione toopremium archiviazione standard. Se si sceglie questa opzione, è necessario completare la migrazione automatica hello prima di inizia la migrazione automatica hello in tale area. In questo modo di evitare i rischi della migrazione automatica di hello causando un conflitto (vedere toohello [pianificazione migrazione automatica][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Istruzioni per la migrazione self-service
toomigrate i dati del warehouse manualmente, utilizzano hello backup e ripristino funzionalità. parte relativa al ripristino Hello della migrazione hello è previsto tootake circa un'ora per terabyte di archiviazione per data warehouse di. Se si vuole hello tookeep stesso nome, al termine della migrazione, seguire hello [toorename passaggi durante la migrazione][steps toorename during migration].

1. [Sospendere][Pause] il data warehouse. Questa operazione richiede un backup automatico.
2. [Eseguire il ripristino][Restore] dallo snapshot più recente.
3. Eliminare il data warehouse esistente in archiviazione Standard. **Se non si toodo questo passaggio, verrà addebitato entrambi i data warehouse.**

> [!NOTE]
> Hello seguenti impostazioni non vengono trasferiti durante la migrazione di hello:
>
> * Il controllo a livello di database hello deve toobe nuovamente abilitata.
> * Regole del firewall a livello di database hello necessario toobe aggiunto di nuovo. Regole del firewall a livello di server hello non sono interessate.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Rinominare il data warehouse durante la migrazione (facoltativa)
Due database nella hello devono avere lo stesso server logico hello stesso nome. SQL Data Warehouse supporta ora la possibilità di hello toorename un data warehouse.

In questo esempio, immaginare che il data warehouse esistente in archiviazione Standard sia attualmente denominato "MyDW".

1. Rinominare "MyDW" utilizzando il comando ALTER DATABASE seguente hello. (In questo esempio, è possibile rinominarlo "MyDW_BeforeMigration.")  Questo comando Arresta tutte le transazioni esistenti e deve essere effettuato in hello toosucceed di database master.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Sospendere][Pause] "MyDW_BeforeMigration." Questa operazione richiede un backup automatico.
3. [Ripristinare] [ Restore] dallo snapshot più recente di un nuovo database con nome hello e utilizzato toobe (ad esempio, "MyDW").
4. Eliminare "MyDW_BeforeMigration". **Se non si toodo questo passaggio, verrà addebitato entrambi i data warehouse.**


## <a name="next-steps"></a>Passaggi successivi
Con hello modificare toopremium archiviazione, è necessario anche un maggior numero di file di database blob nell'architettura sottostante di hello del data warehouse. vantaggi per le prestazioni di questa modifica, toomaximize hello ricompilare gli indici columnstore cluster utilizzando lo script seguente hello. script di Hello funziona forzando alcuni dei blob aggiuntive toohello di dati esistente. Se viene eseguita alcuna azione, dati hello naturalmente ridistribuire nel tempo quando si caricano più dati in tabelle.

**Prerequisiti:**

- Hello del data warehouse deve essere eseguito con le unità di 1.000 data warehouse o versione successiva (vedere [potenza di calcolo di scala][scale compute power]).
- Hello utente l'esecuzione dello script hello deve trovarsi nella hello [mediumrc ruolo] [ mediumrc role] o versione successiva. un ruolo utente toothis tooadd eseguire hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Se si verificano problemi con il data warehouse, [creare un ticket di supporto] [ create a support ticket] e fare riferimento a "migrazione toopremium risorsa di archiviazione" causa possibile hello.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
