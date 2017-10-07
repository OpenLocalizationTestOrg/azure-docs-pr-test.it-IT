---
title: aaaRestore Azure SQL Data Warehouse (portale di Azure) | Documenti Microsoft
description: "Attività del portale di Azure per il ripristino di Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Ripristinare Azure SQL Data Warehouse (portale)
> [!div class="op_single_selector"]
> * [Panoramica][Overview]
> * [Portale][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
In questo articolo si apprenderà come toorestore Azure SQL Data Warehouse utilizzando hello portale di Azure.

## <a name="before-you-begin"></a>Prima di iniziare
**Verificare la capacità in DTU.** Ogni istanza di SQL Data Warehouse è ospitata in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota di unità elaborate di dati (DTU) predefinita. Prima di poter ripristinare SQL Data Warehouse, verificare che SQL server disponga di sufficiente rimanente quota DTU per database hello che si esegue il ripristino. toolearn quota DTU toocalculate o toorequest più Dtu, vedere [richiedere una modifica della quota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Ripristinare un database attivo o sospeso
toorestore un database:

1. Accedi toohello [portale di Azure][Azure portal].
2. Nel riquadro sinistro hello selezionare **Sfoglia**, quindi selezionare **istanze di SQL Server**.

    ![Selezionare Esplora > SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Trovare il server e selezionarlo.

    ![Selezionare il server](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Trovare l'istanza di hello di SQL Data Warehouse che si desidera toorestore da e selezionarlo.

    ![Selezionare l'istanza hello toorestore SQL Data Warehouse](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. Nella parte superiore di hello del Pannello di hello del Data Warehouse, selezionare **ripristinare**.

    ![Selezionare Ripristina](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Specificare un nuovo **nome database**.
7. Versione più recente hello seleziona **punto di ripristino**.

   Assicurarsi di scegliere il punto di ripristino più recente di hello. Poiché i punti di ripristino sono visibili in Coordinated Universal Time (UTC), opzione predefinita hello potrebbe non essere il punto di ripristino più recente di hello.

      ![Selezionare un punto di ripristino](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Selezionare **OK**.
9. processo di ripristino del database Hello verrà avviata ed è possibile utilizzare **notifiche** processo hello toomonitor.

> [!NOTE]
> Al termine di ripristino di hello, è possibile configurare il database ripristinato seguendo [configura il database dopo il ripristino][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Ripristino di un database eliminato
un database eliminato toorestore:

1. Accedi toohello [portale di Azure][Azure portal].
2. Nel riquadro sinistro hello selezionare **Sfoglia**, quindi selezionare **istanze di SQL Server**.

    ![Selezionare Esplora > SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Trovare il server e selezionarlo.

    ![Selezionare il server](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Scorrere verso il basso toohello **operazioni** sezione nel pannello del server.
5. Seleziona hello **database eliminati** riquadro.

    ![Selezionare hello eliminati database riquadro](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Selezionare il database di hello eliminato che si desidera toorestore.

    ![Selezionare un database toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Specificare un nuovo **nome database**.

    ![Aggiungere un nome per il database hello](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Selezionare **OK**.
9. processo di ripristino del database Hello verrà avviata ed è possibile utilizzare **notifiche** processo hello toomonitor.

> [!NOTE]
> vedere il database al termine, il ripristino di hello tooconfigure [configura il database dopo il ripristino][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Passaggi successivi
toolearn sulle funzionalità di continuità aziendale hello delle edizioni di Database SQL di Azure, leggere hello [Panoramica di continuità aziendale di Database SQL di Azure][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
