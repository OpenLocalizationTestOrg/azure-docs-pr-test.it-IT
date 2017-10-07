---
title: Livelli di servizio e di prestazioni del database SQL di Azure | Microsoft Docs
description: Confronto dei livelli di servizio e di prestazioni del database SQL per database singoli e presentazione dei pool elastici SQL
keywords: opzioni di database,prestazioni del database
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Opzioni di prestazioni disponibili per un database SQL di Azure

Il [database SQL di Azure](sql-database-technical-overview.md) offre quattro livelli di servizio per i database sia singoli che [in pool](sql-database-elastic-pool.md): **Basic**, **Standard**, **Premium** e **Premium RS**. All'interno di ogni livello di servizio sono più livelli di prestazioni ([Dtu](sql-database-what-is-a-dtu.md)) e toohandle dimensioni di dati e i carichi di lavoro diverse opzioni di archiviazione. Livelli di prestazioni superiore forniscono di calcolo e le risorse di archiviazione progettata capacità e toodeliver aumento della velocità effettiva. È possibile cambiare i livelli di servizio e di prestazioni e lo spazio di archiviazione in modo dinamico senza tempi di inattività. 
- I livelli di servizio **Basic**, **Standard** e **Premium** garantiscono un tempo di attività previsto dal contratto di servizio del 99,99%, opzioni di continuità aziendale flessibili, funzionalità di sicurezza e fatturazione su base oraria. 
- Hello **Premium RS** livello fornisce hello stessi livelli di prestazioni come hello livello Premium con un contratto di servizio ridotto perché è in esecuzione con un numero inferiore di copie ridondanti rispetto a un database in hello altri livelli di servizio. In tal caso, nell'evento hello di un errore del servizio, potrebbe essere necessario toorecover il database da un backup con backup tooa ritardo di 5 minuti.

> [!IMPORTANT]
> Un database SQL di Azure Ottiene un set di risorse garantito e hello previsto caratteristiche delle prestazioni del database non sono interessate da qualsiasi altro database in Azure. 

## <a name="choosing-a-service-tier"></a>Scelta di un piano di servizio
Hello nella tabella seguente vengono forniti esempi dei livelli di hello migliori adatti per carichi di lavoro di applicazioni diverso.

| Livello di servizio | Carichi di lavoro di destinazione |
| :--- | --- |
| **Basic** | Più adatto per un database di piccole dimensioni, che supporta in genere una singola operazione attiva in un determinato momento. Ad esempio, database usati per lo sviluppo o i test oppure applicazioni su scala ridotta usate raramente. |
| **Standard** |toooption-Vai Hello per le applicazioni cloud con requisiti di prestazioni dei / o toomedium bassa, supporto di più query contemporaneamente. Ad esempio, applicazioni web o per gruppi di lavoro. |
| **Premium** | Progettato per volumi di transazioni elevati con alti requisiti di prestazioni I/O che supportano più utenti contemporaneamente. Ad esempio, database che supportano applicazioni mission-critical. |
| **Premium RS** | Progettato per carichi di lavoro con utilizzo intensivo dei / o che non richiedono le garanzie di disponibilità più elevate hello. Esempi di test ad alte prestazioni dei carichi di lavoro o un carico di lavoro analitico in database hello non sistema hello del record. |
|||

È possibile creare database singoli con risorse dedicate in un livello di servizio, con un [livello di prestazioni](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) specifico, oppure creare database in un [pool elastico SQL](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). In un pool elastico SQL, le risorse di calcolo e archiviazione hello sono condivise tra più database all'interno di un singolo server logico. 

Le risorse disponibili per i database singoli sono espresse in unità di transazione di database (DTU), mentre quelle per i pool elastici SQL sono espresse in unità di transazione di database elastico (eDTU). Per altre informazioni su DTU ed eDTU, vedere [Unità di transazione di database (DTU) e unità di transazione di database elastico (eDTU)](sql-database-what-is-a-dtu.md).

toodecide in un livello di servizio, avviare mediante la determinazione delle funzionalità del database minima hello è necessario:

| **Funzionalità del livello di servizio** | **Basic** | **Standard** | **Premium** | **Premium RS**|
| :-- | --: | --: | --: | --: |
| Dimensioni massime del database singolo | 2 GB | 250 GB | 4 TB*  | 500 GB  |
| Dimensioni massime di un pool elastico | 156 GB | 2,9 TB | 4 TB* | 750 GB |
| Dimensioni massime dei database in un pool elastico | 2 GB | 250 GB | 500 GB | 500 GB |
| Numero massimo di database per pool | 500  | 500 | 100 | 100 |
| DTU massime del database singolo | 5 | 100 | 4000 | 1000 |
| DTU massime per database in un pool elastico | 5 | 3000 | 4000 | 1000 |
| Periodo di conservazione dei backup dei database | 7 giorni | 35 giorni | 35 giorni | 35 giorni |
||||||

> [!IMPORTANT]
> Archiviazione di backup too4 TB è attualmente disponibile in hello seguenti aree: ci East2, Stati Uniti occidentali, ci Gov Virginia, Europa occidentale, Germania centrale, Sud Asia sudorientale, Giappone orientale, Australia orientale, Canada centrale e Canada orientale. Vedere le [limitazioni correnti per l'opzione 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Dopo aver determinato il livello di servizio appropriato hello, si è pronti toodetermine livello di prestazioni hello (numero hello di Dtu) e la quantità di archiviazione hello per database hello. 

- livelli di prestazioni S2 e S3 in hello Hello **Standard** livello sono spesso un buon punto di partenza. 
- Per i database con requisiti elevati di utilizzo della CPU o dei / o, i livelli di prestazioni in hello hello **Premium** livello sono il punto di partenza destra di hello. 
- Hello **Premium** livello offre una quantità di CPU e inizia in base 10 volte più operazioni dei / o rispetto toohello massimo livello di prestazioni in hello **Standard** livello.
- Hello **PremiumRS** livello offre prestazioni di hello di hello **Premium** livello a un costo inferiore, ma con un contratto di servizio ridotto.

> [!IMPORTANT]
> Hello revisione [pool elastico SQL](sql-database-elastic-pool.md) per hello informazioni sul raggruppamento di database in elastico SQL pool di risorse di calcolo e archiviazione tooshare. resto Hello di questo argomento è incentrato sui livelli di servizio e livelli di prestazioni per i singoli database.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Livelli di servizio e di prestazioni per database singoli
Per i database singoli, all'interno di ogni livello di servizio sono disponibili più livelli di prestazioni e spazi di archiviazione. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Ridimensionamento di un singolo database

Dopo aver selezionato inizialmente un livello di servizio e di prestazioni, è possibile ridimensionare un singolo database in modo dinamico in base all'esperienza effettiva.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Modifica del livello hello servizio livello e/o le prestazioni di un database consente di creare una replica del database originale hello hello nuovo livello di prestazioni per poi passa connessioni toohello replica. Nessun dato venga perso durante questo processo, ma durante hello breve istante quando si passa sulla replica toohello, le connessioni toohello database sono disabilitate, pertanto possono essere eseguito il rollback alcune transazioni in corso. durata Hello per passare hello varia, ma è in genere meno di 4 secondi è inferiore a 30 secondi 99% di tempo hello. Se sono presenti un numero elevato di transazioni in corso in connessioni momento hello sono disabilitate, hello periodo di tempo per passare hello può essere più lungo.  

durata Hello dell'intero processo di scalabilità verticale hello dipende dalla dimensione entrambi hello e livello di servizio di hello database prima e dopo la modifica di hello. Ad esempio, il passaggio di un database di 250 GB al livello di servizio Standard o dal livello di servizio Standard a un altro livello o nell'ambito dello stesso livello di servizio Standard viene completato entro 6 ore. Per un database di hello stessa dimensione a modifica i livelli di prestazioni all'interno di livello di servizio Premium hello, l'operazione dovrebbe completarsi in 3 ore.

> [!TIP]
> toocheck stato hello di un database SQL in corso l'operazione di ridimensionamento, è possibile utilizzare hello seguente query: ```select * from sys.dm_operation_status```.
>

* Se si sta aggiornando tooa servizio livello o prestazioni livello superiore, hello dimensioni massime del database non aumenta a meno che non si specifichi una dimensione massima più grande.
* toodowngrade un database, database hello deve essere minore di hello dimensioni massime di consentite del livello di servizio di destinazione hello. 
* Quando si aggiorna un database con [-replica geografica](sql-database-geo-replication-portal.md) abilitata, di aggiornare il livello di prestazioni desiderati toohello database secondari prima di aggiornare il database primario hello (generale). Quando l'aggiornamento tooa edizione diversa aggiornamento dei hello database secondario prima di tutto è obbligatorio. 
* Quando il downgrade di un database con [-replica geografica](sql-database-geo-replication-portal.md) abilitato, effettuare il downgrade relativo livello di prestazioni desiderati toohello database primario prima del downgrade database secondario hello (generale). Quando downgrade tooa edizione diversa downgrade hello database primario per primo è obbligatorio. 

* Hello offerte di servizi di ripristino sono diverse per hello vari livelli di servizio. Se si effettua il downgrade toohello **base** livello, si disporrà di un periodo di conservazione dei backup inferiore - vedere [backup del Database SQL Azure](sql-database-automated-backups.md).
* Hello nuove proprietà hello database non vengono applicate fino al completamento delle modifiche hello.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>Limitazioni correnti dei database P11 e P15 con dimensioni massime di 4 TB

Come illustrato in precedenza, le dimensioni massime di 4 TB per i database P11 e P15 sono supportate in alcune aree. Hello considerazioni e le limitazioni seguenti si applicano tooP11 e database P15 con valore maxsize di 4 TB:

- Se si sceglie l'opzione maxsize di 4 TB hello durante la creazione di un database (tramite un valore da 4 TB o 4096 GB), hello creare comando non riesce con un errore se viene eseguito il provisioning di database hello in un'area non supportata.
- Per esistente P11 P15 database e che si trova in una delle aree di hello è supportato, è possibile aumentare hello maxsize archiviazione too4 TB. Ciò può essere verificato utilizzando hello [selezionare DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) o tramite l'analisi delle dimensioni del database nel portale di Azure hello hello. L'aggiornamento un P11 esistente o P15 database può essere eseguito solo dai membri del ruolo del database dbmanager hello o un account di accesso a livello di server principale. 
- Se viene eseguita un'operazione di aggiornamento una configurazione di hello area supportata viene aggiornata immediatamente. database Hello rimane online durante il processo di aggiornamento hello. Tuttavia, non è possibile utilizzare hello completo da 4 TB di spazio di archiviazione fino a quando non sono stati hello database effettivo file aggiornato toohello nuovo maxsize. lunghezza Hello di tempo necessaria dipende sulle dimensioni di hello del database hello in corso l'aggiornamento.  
- Durante la creazione o l'aggiornamento di un database P11 o P15, è possibile scegliere solamente 1 TB o 4 TB di dimensioni massime. Gli account di archiviazione intermedi non sono attualmente supportati. Quando si crea un P11/P15, opzione di archiviazione hello predefinito di 1 TB è già selezionato. Per i database che si trova in una delle aree di hello è supportato, è possibile aumentare hello too4TB massima di archiviazione per un singolo database nuovo o esistente. In tutte le altre aree, le dimensioni massime non possono essere aumentate oltre 1 TB. prezzo Hello non cambia quando si seleziona 4 TB di spazio di archiviazione incluso.
- Hello 4 TB database maxsize non può essere modificato too1 TB anche se hello spazio di archiviazione effettivo utilizzato è di sotto di 1 TB. Di conseguenza, è possibile effettuare il downgrade un tooa P11 - 4 TB/P15 - 4 TB P11 - 1 TB/P15 - 1 TB o un livello di prestazioni più basso, ad esempio, tooP1-P6) fino a quando non forniamo opzioni di archiviazione aggiuntive per il resto di hello di hello livelli di prestazioni. Questa restrizione si applica anche punto nel tempo, inclusi gli scenari di copia e ripristino di toohello geografica il ripristino a lungo termine-backup di conservazione e copia del database. Dopo aver configurato un database con l'opzione di 4 TB hello, tutte le operazioni di ripristino del database devono essere eseguite in un P11/P15 con valore maxsize di 4 TB.
- Quando la creazione o l'aggiornamento di un database P11/P15 in un'area non supportata, hello crea o si verifica un errore di operazione di aggiornamento con hello seguente messaggio di errore: **P11 e P15 database con backup too4TB di archiviazione sono disponibili in Microsoft East2, Stati Uniti occidentali, Virginia ci Gov, Europa occidentale, Germania centrali, Asia sudorientale, Giappone orientale, Australia orientale, Canada centrale e Canada orientale.**
- Per gli scenari di replica geografica attiva:
   - Impostazione di una relazione di replica geografica: se il database primario hello è P11 o P15, hello secondary(ies) deve anche essere P11 o P15; livelli di prestazioni inferiori vengono rifiutati come database secondari, poiché non sono in grado di supportare 4 TB.
   - L'aggiornamento del database primario hello in una relazione di replica geografica: hello maxsize too4 TB in un database primario modifica attiva hello stesso modifica nel database secondario hello. Entrambi gli aggiornamenti devono essere completate correttamente per la modifica di hello in effetto tootake primario hello. Area per l'opzione di 4TB hello limitazioni (vedere sopra). Se hello secondario si trova in un'area che non supporta 4 TB, hello primario non viene aggiornata.
- Non è possibile utilizzare il servizio di importazione/esportazione hello per caricare i database P11 - 4TB/P15 - 4TB. Utilizzare SqlPackage.exe troppo[importare](sql-database-import.md) e [esportare](sql-database-export.md) dati.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>Gestire i livelli di servizio singolo database e i livelli di prestazioni utilizzando hello portale di Azure

tooset o modifica hello a livello di servizio, il livello di prestazioni o la quantità di archiviazione per un database SQL di Azure nuova o esistente utilizzando hello portale di Azure, aprire hello **configurare prestazioni** finestra per il database, fare clic su ** Piano tariffario (scala Dtu)** , come illustrato nella seguente schermata hello. 

- Impostare o modificare il livello di servizio hello selezionando il livello di servizio hello il carico di lavoro. 
- Impostare o modificare il livello di prestazioni hello (**Dtu**) all'interno di un livello di servizio utilizzando hello **DTU** dispositivo di scorrimento.
- Impostare o modificare la quantità di archiviazione hello per il livello di prestazioni hello utilizzando hello **archiviazione** dispositivo di scorrimento. 

  ![Configurare il livello di servizio e di prestazioni](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Se si seleziona un livello di servizio P11 o P15, vedere [Limitazioni correnti dei database P11 e P15 con dimensioni massime di 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Gestire i livelli di servizio e di prestazioni per database singoli con PowerShell

tooset o modificare livelli di servizio di database SQL di Azure, i livelli di prestazioni e la quantità di archiviazione usando PowerShell, utilizzare i cmdlet di PowerShell seguente hello. Se è necessario tooinstall o l'aggiornamento di PowerShell, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps). 

| Cmdlet | Descrizione |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Crea un database |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Recupera uno o più database|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Imposta le proprietà per un database oppure sposta un database esistente in un pool elastico|


> [!TIP]
> Per uno script di esempio di PowerShell che consente di monitorare le metriche delle prestazioni di hello di un database, si ridimensiona il livello di prestazioni superiore tooa e crea una regola di avviso su una delle metriche delle prestazioni di hello, vedere [monitoraggio e la scala di un singolo SQL database mediante PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>Gestire i livelli di servizio singolo database e i livelli di prestazioni utilizzando hello CLI di Azure

tooset o modificare livelli di servizio di database SQL di Azure, i livelli di prestazioni e la quantità di archiviazione utilizzando l'interfaccia CLI di Azure, hello utilizza hello [Database SQL di Azure CLI](/cli/azure/sql/db) comandi. Hello utilizzare [Shell Cloud](/azure/cloud-shell/overview) toorun hello CLI nel browser o [installare](/cli/azure/install-azure-cli) sul macOS, Linux o Windows. Per creare e gestire i pool elastici SQL, vedere [Pool elastici](sql-database-elastic-pool.md).

| Cmdlet | Descrizione |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |Crea un database|
|[az sql db list](/cli/azure/sql/db#list)|Elenca tutti i database e i data warehouse in un server o tutti i database in un pool elastico|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|Elenca gli obiettivi di servizio e i limiti di archiviazione disponibili|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|Restituisce gli utilizzi del database|
|[az sql db show](/cli/azure/sql/db#show)|Recupera un database o un data warehouse|
|[az sql db update](/cli/azure/sql/db#update)|Aggiorna un database|

> [!TIP]
> Per uno script di esempio CLI di Azure che viene ridimensionata in un unico livello di prestazioni diverse tooa database SQL di Azure dopo l'esecuzione di query su informazioni sulle dimensioni hello del database di hello, vedere [toomonitor CLI di utilizzo e la scala di un singolo database SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Gestire i livelli di servizio e di prestazioni per database singoli con Transact-SQL

tooset o modificare livelli di servizio di database SQL di Azure, i livelli di prestazioni e la quantità di archiviazione con Transact-SQL, utilizzare i comandi T-SQL seguente hello. È possibile eseguire questi comandi utilizzando il portale di Azure, hello [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [codice di Visual Studio](https://code.visualstudio.com/docs), o qualsiasi altro programma che è possibile connettere il server di Database SQL di Azure tooan e passare a Transact-SQL comandi. 

| Comando | Descrizione |
| --- | --- |
|[CREATE DATABASE (database SQL di Azure)](/sql/t-sql/statements/create-database-azure-sql-database)|Crea un nuovo database. È necessario essere connessi toohello database master toocreate un nuovo database.|
| [ALTER DATABASE (database SQL di Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifica un database SQL di Azure. |
|[sys.database_service_objectives (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Restituisce hello edizione (livello di servizio), l'obiettivo di servizio (livello di prezzo) e nome del pool elastico, se presente, per un database SQL di Azure o un Data Warehouse di SQL Azure. Se connesso al database master di toohello in un server di Database SQL di Azure, restituisce informazioni su tutti i database. Per Azure SQL Data Warehouse, è necessario essere connessi toohello database master.|
|[sys.database_usage (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Elenca il numero di hello, tipo e durata di database in un server di Database SQL di Azure.|

Hello riportato di seguito hello maxsize viene modificata utilizzando il comando di ALTER DATABASE hello:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Gestire singoli database utilizzando l'API REST hello

vedere tooset o modificare livelli di servizio di database SQL di Azure, i livelli di prestazioni e la quantità di archiviazione utilizzando l'API REST di hello [API REST di Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Passaggi successivi

* Altre informazioni sulle [DTU](sql-database-what-is-a-dtu.md).
* toolearn sul monitoraggio dell'utilizzo DTU, vedere [monitoraggio e ottimizzazione delle prestazioni](sql-database-troubleshoot-performance.md).

