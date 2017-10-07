---
title: backup di SQL Data Warehouse aaaAzure - gli snapshot, con ridondanza geografica | Documenti Microsoft
description: Per informazioni sui backup di database predefiniti SQL Data Warehouse che consentono di toorestore un punto di ripristino di Azure SQL Data Warehouse tooa oppure un'area geografica diversa.
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>Backup di SQL Data Warehouse
SQL Data Warehouse offre il backup sia locale che geografico come parte delle sue funzionalità di backup del data warehouse. Queste includono gli snapshot dei BLOB di Archiviazione di Azure e l'archiviazione con ridondanza geografica. Utilizzare dati warehouse backup toorestore il ripristino di data warehouse tooa punto nell'area primaria hello o ripristinare l'area geografica diversa tooa. Questo articolo illustra le specifiche di hello di backup in SQL Data Warehouse.

## <a name="what-is-a-data-warehouse-backup"></a>Cos'è un backup di data warehouse?
Un backup dei dati del warehouse è dati hello che è possibile utilizzare toorestore un'ora specifica di data warehouse tooa.  Poiché SQL Data Warehouse è un sistema distribuito, un backup di data warehouse è costituito da molti file archiviati in BLOB di Azure. 

I backup dei database sono una parte essenziale di qualsiasi strategia di continuità aziendale e ripristino di emergenza, perché proteggono i dati dal danneggiamento o dall'eliminazione accidentale. Per altre informazioni, vedere [Panoramica sulla continuità aziendale](../sql-database/sql-database-business-continuity.md).

## <a name="data-redundancy"></a>Ridondanza dei dati
SQL Data Warehouse protegge i dati archiviandoli in Archiviazione Premium di Azure con ridondanza locale. Questa funzionalità di archiviazione di Azure archivia sincrone copie dei dati hello nella protezione dei dati trasparenti tooguarantee centro dati locale hello se sono presenti errori localizzati. La ridondanza dei dati garantisce che i dati non subiscano l'impatto di problemi dell'infrastruttura, ad esempio errori del disco. La ridondanza dei dati assicura la continuità aziendale con un'infrastruttura a tolleranza di errore e disponibilità elevata.

toolearn ulteriori informazioni:

* Archiviazione Premium di Azure, vedere [tooAzure introduzione archiviazione Premium](../storage/common/storage-premium-storage.md).
* Archiviazione con ridondanza locale, vedere [Replica di Archiviazione di Azure](../storage/common/storage-redundancy.md#locally-redundant-storage).

## <a name="azure-storage-blob-snapshots"></a>Snapshot dei BLOB di Archiviazione di Azure
Il vantaggio dell'utilizzo di archiviazione Premium di Azure SQL Data Warehouse utilizza localmente il Blob di archiviazione di Azure snapshot toobackup hello data warehouse. È possibile ripristinare un punto di ripristino dati warehouse tooa dello snapshot. Gli snapshot vengono eseguiti come minimo ogni quattro-otto ore e sono disponibili per sette giorni.  

toolearn ulteriori informazioni:

* Snapshot BLOB di Azure, vedere [Creare uno snapshot BLOB](../storage/blobs/storage-blob-snapshots.md).

## <a name="geo-redundant-backups"></a>Backup con ridondanza geografica
Ogni 24 ore, SQL Data Warehouse archivia hello completa del data warehouse nel servizio di archiviazione Standard. Hello completo data warehouse viene creato toomatch hello ora dell'ultimo snapshot hello. archiviazione standard Hello appartiene tooa account di archiviazione con ridondanza geografica con accesso in lettura (RA-GRS). funzionalità di archiviazione di Azure RA-GRS Hello replica hello i file di backup tooa [centro dati associato](../best-practices-availability-paired-regions.md). Questa replica geografica assicura che nel caso in cui non è possibile accedere snapshot hello nell'area primaria, è possibile ripristinare del data warehouse. 

Questa funzionalità è attivata per impostazione predefinita. Se non si desidera toouse backup con ridondanza geografica, è possibile [rifiutare esplicitamente] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn). 

> [!NOTE]
> Nell'archiviazione di Azure, il termine hello *replica* fa riferimento il file toocopying da tooanother un'unica posizione. SQL *replica di database* fa riferimento a database secondari toomultiple tookeeping sincronizzati con un database primario. 
> 
> 

> [!NOTE]
> È possibile rifiutare esplicitamente i backup con ridondanza geografica con 9000 DWU e 18000 DWU. 
>
> 

toolearn ulteriori informazioni:

* Archiviazione con ridondanza geografica, vedere [Replica di Archiviazione di Azure](../storage/common/storage-redundancy.md).
* Archiviazione con ridondanza geografica e accesso in lettura, vedere [Archiviazione con ridondanza geografica e accesso in lettura](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>Pianificazione dei backup del data warehouse e periodo di conservazione
SQL Data Warehouse Crea snapshot nel warehouse dati online ogni quattro ore tooeight e mantenere ogni snapshot per sette giorni. È possibile ripristinare il tooone database online hello dei punti di ripristino in hello ultimi sette giorni. 

toosee all'avvio dell'ultimo snapshot hello, eseguire questa query per la versione online di SQL Data Warehouse. 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

Se è necessario tooretain uno snapshot per più di sette giorni, è possibile ripristinare un ripristino punto tooa nuovo data warehouse. Al termine, il ripristino di hello SQL Data Warehouse avvia la creazione di snapshot nel nuovo data warehouse di hello. Se non si apporta modifiche toohello nuovo data warehouse, gli snapshot hello rimangono vuoti e pertanto hello snapshot costo minimo. È anche possibile sospendere hello database tookeep SQL Data Warehouse dalla creazione di snapshot.

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>Conservazione dei backup toomy cosa accade quando viene sospeso il personale del data warehouse?
Mentre un data warehouse è in pausa SQL Data Warehouse non crea snapshot e non fa scadere gli snapshot. età di Hello snapshot non cambia quando viene sospeso il data warehouse di hello. Memorizzazione degli snapshot in base hello numero di giorni hello data warehouse è online, non i giorni di calendario.

Ad esempio, se uno snapshot inizia il 1 ottobre PM 4 e data warehouse di hello è in pausa il 3 ottobre 4 ore, hello è due giorni. Ogni volta che viene riportato online data warehouse di hello snapshot hello da due giorni. Se data warehouse di hello online ottobre 5 4 ore, snapshot hello da due giorni e rimane per cinque giorni.

Quando il data warehouse di hello torna online, SQL Data Warehouse riprende nuovi snapshot e scade snapshot quando dispongono di più di sette giorni di dati.

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>Quanto tempo è il periodo di memorizzazione hello per rilasciarlo data warehouse?
Quando viene eliminato un data warehouse, data warehouse di hello e gli snapshot hello vengono salvati per sette giorni e quindi rimosso. È possibile ripristinare hello dati warehouse tooany hello salvato dei punti di ripristino.

> [!IMPORTANT]
> Se si elimina un'istanza SQL server logica, tutti i database appartenenti a toohello istanza vengono inoltre eliminati e non possono essere recuperati. Non è possibile ripristinare un server eliminato.
> 
> 

## <a name="data-warehouse-backup-costs"></a>Costi di backup del data warehouse
Hello totale costi per il warehouse di dati primario e sette giorni di snapshot di Blob di Azure è arrotondato toohello più vicino TB. Ad esempio, se il data warehouse è 1,5 TB e snapshot hello utilizzare 100 GB, vengono fatturati per 2 TB di dati in base alle tariffe di archiviazione Premium di Azure. 

> [!NOTE]
> Ogni snapshot è inizialmente vuota e aumenta man mano che si apportata warehouse di dati primario toohello le modifiche. Tutti gli snapshot di aumentano delle dimensioni come modifiche di hello data warehouse. Di conseguenza, i costi di archiviazione hello per gli snapshot aumentano secondo toohello tasso di variazione.
> 
> 

Se si usa l'archiviazione con ridondanza geografica, sarà addebitato un costo di archiviazione separato. archiviazione con ridondanza geografica Hello viene fatturato alla tariffa di archiviazione accesso in lettura geograficamente ridondante (RA-GRS) standard hello.

Per altre informazioni sui prezzi di SQL Data Warehouse, vedere [Prezzi di SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="using-database-backups"></a>Uso dei backup di database
uso principale di Hello per i backup SQL data warehouse è toorestore hello dati warehouse tooone hello dei punti di ripristino entro il periodo di memorizzazione hello.  

* toorestore un SQL data warehouse, vedere [ripristino configurazione di un data warehouse SQL](sql-data-warehouse-restore-database-overview.md).

## <a name="related-topics"></a>Argomenti correlati
### <a name="scenarios"></a>Scenari
* Per una panoramica sulla continuità aziendale, vedere [Panoramica sulla continuità aziendale](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

* toorestore un data warehouse, vedere [ripristinare un SQL data warehouse](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

