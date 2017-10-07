---
title: un database SQL di Azure da un backup aaaRestore | Documenti Microsoft
description: Informazioni sul ripristino punto nel tempo, che consente di tooroll back un punto precedente tooa di Database SQL di Azure nel tempo (in alto too35 giorni).
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>Ripristinare un database SQL di Azure mediante i backup automatici del database
Il database SQL prevede queste opzioni per il ripristino del database mediante [backup automatici del database](sql-database-automated-backups.md) e [backup nella conservazione a lungo termine](sql-database-long-term-retention.md). È possibile ripristinare un backup di database in:

* Un nuovo database nello stesso server logico recuperato hello specificato tooa temporizzazione entro il periodo di memorizzazione hello. 
* Un database hello stesso server logico recuperato toohello ora di eliminazione per un database eliminato.
* Un nuovo database in qualsiasi server logico in qualsiasi area recuperato toohello punto di backup giornaliero più recente di hello nell'archiviazione blob di replica geografica (RA-GRS).

> [!IMPORTANT]
> Non è possibile sovrascrivere un database esistente durante il ripristino.
>

È inoltre possibile utilizzare [database backup automatici](sql-database-automated-backups.md) toocreate un [copia del database](sql-database-copy.md) in qualsiasi server logico in qualsiasi area. 

## <a name="recovery-time"></a>Tempo di ripristino
Hello toorestore ora ripristino un database tramite backup automatizzati del database è stato interessato da diversi fattori: 

* dimensioni di Hello del database hello
* livello di prestazioni Hello del database hello
* numero di Hello dei log delle transazioni coinvolte
* quantità di Hello di attività che deve toobe riprodotti toorecover toohello punto di ripristino
* larghezza di banda Hello se Ripristina hello è tooa altra area geografica 
* numero di Hello di richieste simultanee ripristino elaborate nell'area di destinazione hello. 
  
  Per un database molto grandi e/o attivo, il ripristino di hello potrebbe richiedere diverse ore. Nel caso di un'interruzione prolungata in un'area, è possibile che in altre aree vengano elaborate molte richieste di ripristino geografico. Quando sono presenti numerose richieste, può aumentare il tempo di recupero hello per i database in tale area. Per la maggior parte dei database, il ripristino richiede al massimo 12 ore.
  
Non è il ripristino di massa non toodo funzionalità incorporata. Hello [Database SQL di Azure: Server di recupero con registrazione completa](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) script è un esempio di un modo per eseguire questa attività.

> [!IMPORTANT]
> toorecover utilizzando backup automatici, è necessario essere un membro del ruolo di collaboratore di SQL Server hello nella sottoscrizione hello o essere proprietario della sottoscrizione hello. È possibile ripristinare utilizzando hello portale di Azure, PowerShell o hello API REST. Non è possibile usare Transact-SQL. 
> 

## <a name="point-in-time-restore"></a>Ripristino temporizzato

È possibile ripristinare un database esistente tooan precedente punto nel tempo come un nuovo database nei hello stesso server logico tramite il portale di Azure, di hello [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), o hello [API REST](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Per uno script di PowerShell di esempio che illustra come tooperform un punto nel tempo ripristino di un database, vedere [ripristinare un database SQL tramite PowerShell](scripts/sql-database-restore-database-powershell.md).
>

database Hello può essere ripristinato tooany livello di servizio o di prestazioni di livello e come un singolo database o in un pool elastico. Assicurarsi di disporre di risorse sufficienti sul server logico hello o hello pool elastico toowhich si ripristinano database hello. Al termine dell'operazione, il database ripristinato hello è un database normale, completamente accessibile, in linea. database ripristinato Hello viene addebitato in base alle tariffe normale in base al livello di prestazioni e di servizio. Si è previsto alcun addebito fino al completamento del ripristino del database hello.

È in genere ripristinare un database tooan punti precedenti per scopi di ripristino. Quando si esegue questa operazione, è possibile trattare hello database ripristinato come una sostituzione per il database originale hello o utilizzarlo tooretrieve dati da e quindi aggiornare il database originale di hello. 

* ***Sostituzione del database:*** se il database ripristinato hello è inteso come una sostituzione per il database originale hello, è necessario verificare il livello di prestazioni hello e/o livello di servizio appropriati e ridimensionare il database di hello, se necessario. È possibile rinominare il database originale hello e quindi assegnare hello ripristinato hello originale nome del database tramite comando ALTER DATABASE hello in T-SQL. 
* ***Ripristino dei dati:*** se si prevede di dati tooretrieve toorecover database hello ripristinato da un errore utente o dell'applicazione, è necessario toowrite ed eseguire hello necessarie ripristino script tooextract dati da hello ripristinata database toohello database originale. Anche se l'operazione di ripristino hello può richiedere un toocomplete molto tempo, è visibile nell'elenco di database hello in tutto il processo di ripristino hello hello il ripristino di database. Se si elimina il database di hello durante il ripristino di hello, viene annullata l'operazione di ripristino hello e non vengono addebitate le spese per database hello che non viene completato il ripristino di hello. 

### <a name="azure-portal"></a>Portale di Azure

toorecover tooa punto nel tempo usando hello portale di Azure, pagina hello open per il database e fare clic su **ripristinare** sulla barra degli strumenti hello.

![ripristino a un determinato momento nel tempo](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>Ripristino di un database eliminato
È possibile ripristinare un tempo di eliminazione toohello database eliminati per un database eliminato su hello stesso server logico utilizzando hello portale di Azure [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), o hello [REST (createMode = Ripristina)](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Per un esempio di PowerShell eseguire lo script che mostra come toorestore un database eliminato, vedere [ripristinare un database SQL tramite PowerShell](scripts/sql-database-restore-database-powershell.md).
>

> [!IMPORTANT]
> Se si elimina un'istanza del server di database SQL di Azure, anche tutti i database relativi vengono eliminati e non possono essere recuperati. Non è attualmente disponibile alcun supporto per il ripristino di un server eliminato.
> 

### <a name="azure-portal"></a>Portale di Azure

toorecover un eliminati database durante il relativo [periodo di memorizzazione](sql-database-service-tiers.md) usando hello portale di Azure, pagina hello open per il server e nell'area di operazioni di hello, fare clic su **database eliminati**.

![deleted-database-restore-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![deleted-database-restore-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>Ripristino geografico
È possibile ripristinare un database SQL in qualsiasi server in qualsiasi area di Azure da hello più recente con replica geografica backup completi e differenziali. Ripristino a livello geografico utilizza un backup con ridondanza geografica come origine e può essere utilizzato toorecover un database anche se database hello o Data Center non è accessibile a causa di un'interruzione di tooan. 

Ripristino a livello geografico è recovery-opzione predefinita hello quando il database è disponibile a causa di un evento imprevisto nell'area di hello in cui è ospitato il database di hello. Se un evento imprevisto su larga scala nei risultati di un'area non disponibilità dell'applicazione di database, è possibile ripristinare un database dal server di tooa i backup di replica geografica hello in qualsiasi altra area. Si verifica un ritardo tra quando viene eseguito un backup differenziale e quando è replicato geograficamente tooan Azure blob in un'area diversa. Questo ritardo può essere backup tooan ora, in tal caso, se si verifica un'emergenza, è possibile che di perdita di dati ora tooone. Hello seguente figura mostra il ripristino del database hello dall'ultimo backup disponibile hello in un'altra area.

![Ripristino geografico](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> Per un esempio di PowerShell eseguire lo script che mostra come tooperform un ripristino a livello geografico, vedere [ripristinare un database SQL tramite PowerShell](scripts/sql-database-restore-database-powershell.md).
> 

Il ripristino temporizzato in un database di replica geografica secondaria non è attualmente supportato. Il ripristino temporizzato può essere eseguito solo in un database primario. Per informazioni dettagliate sull'utilizzo di ripristino a livello geografico toorecover da un'interruzione del servizio, vedere [recuperare da un'interruzione](sql-database-disaster-recovery.md).

> [!IMPORTANT]
> Ripristino da backup è più semplice di emergenza hello hello soluzioni di ripristino disponibili nel Database SQL con hello RPO più lungo e tempo di ripristino di stima (ERT). Per soluzioni che usano i database Basic, il ripristino geografico è spesso una soluzione ragionevole di ripristino di emergenza con un ERT di 12 ore. Per soluzioni che usano i database Standard o Premium di dimensioni maggiori, che richiedono tempi di ripristino inferiori, è consigliabile usare la [replica geografica attiva](sql-database-geo-replication-overview.md). Replica geografica attiva offre molto inferiore RPO ed ERT quanto sono necessarie solo per avviare un database secondario viene replicata continuamente tooa di failover. Per altre informazioni sulle opzioni di continuità aziendale, vedere [Overview of business continuity](sql-database-business-continuity.md) (Panoramica sulla continuità aziendale).
> 

### <a name="azure-portal"></a>Portale di Azure

toogeo-ripristinare un database durante il relativo [periodo di memorizzazione](sql-database-service-tiers.md) utilizzando hello portale di Azure, aprire una pagina di database SQL di hello e quindi fare clic su **Aggiungi**. In hello **Seleziona origine** casella di testo, selezionare **Backup**. Specificare hello di backup da cui recovery hello tooperform nell'area di hello e nel server di hello di propria scelta. 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>Esecuzione a livello di codice del ripristino tramite backup automatici
Come illustrato in precedenza, è inoltre toohello portale di Azure, il ripristino del database può essere eseguita a livello di programmazione mediante Azure PowerShell o hello API REST. Hello le tabelle seguenti vengono descritti i set di hello di comandi disponibili.

### <a name="powershell"></a>PowerShell
| Cmdlet | Descrizione |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Ottiene uno o più database. |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | Ottiene un database eliminato che è possibile ripristinare. |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |Ottiene una copia di backup con ridondanza geografica di un database. |
| [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |Ripristina un database SQL. |
|  | |

### <a name="rest-api"></a>API REST
| API | Descrizione |
| --- | --- |
| [REST (createMode=Recovery)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |Ripristina un database |
| [Get Create or Update Database Status](https://msdn.microsoft.com/library/azure/mt643934.aspx) |Restituisce lo stato di hello durante un'operazione di ripristino |
|  | |

## <a name="summary"></a>Riepilogo
I backup automatici proteggono i database da errori dell'utente e delle applicazioni, dall'eliminazione accidentale e da interruzioni prolungate. Questa funzionalità incorporata è disponibile per tutti i livelli di servizio e di prestazioni. 

## <a name="next-steps"></a>Passaggi successivi
* Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md)
* toolearn sui backup di Database di SQL Azure automatizzati, vedere [backup automatici di Database SQL](sql-database-automated-backups.md)
* toolearn sulla conservazione dei backup a lungo termine, vedere [conservazione dei backup a lungo termine](sql-database-long-term-retention.md)
* tooconfigure, gestire e ripristinare da conservazione a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure utilizzando hello Azure portale, vedere [Configura e a lungo termine utilizza backup memorizzazione](sql-database-long-term-backup-retention-configure.md). 
* toolearn sulle opzioni di ripristino più veloce, vedere [replica geografica attiva](sql-database-geo-replication-overview.md)  
