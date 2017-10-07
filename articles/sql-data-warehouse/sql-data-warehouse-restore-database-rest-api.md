---
title: aaaRestore un Azure SQL Data Warehouse (API REST) | Documenti Microsoft
description: "Attività dell'API REST per il ripristino di un'istanza di Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>Ripristinare un'istanza di Azure SQL Data Warehouse (API REST)
> [!div class="op_single_selector"]
> * [Panoramica][Overview]
> * [Portale][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

In questo articolo si apprenderà come toorestore un Azure SQL Data Warehouse utilizzando hello API REST.

## <a name="before-you-begin"></a>Prima di iniziare
**Verificare la capacità in DTU.** Ogni SQL Data Warehouse è ospitato in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota DTU predefinita.  Prima di poter ripristinare un SQL Data Warehouse, verificare che hello che di SQL server è sufficientemente rimanente quota DTU per database hello da ripristinare. toolearn come toocalculate DTU necessarie o toorequest più DTU, vedere [richiedere una modifica della quota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Ripristinare un database attivo o sospeso
toorestore un database:

1. Ottenere l'elenco di hello dei punti di ripristino di database tramite l'operazione Get punti di ripristino di Database hello.
2. Iniziare il ripristino utilizzando hello [richiesta di ripristino di database crea] [ Create database restore request] operazione.
3. Tenere traccia dello stato di hello del ripristino utilizzando hello [dello stato dell'operazione di Database] [ Database operation status] operazione.

> [!NOTE]
> Al termine del ripristino di hello, è possibile configurare il database ripristinato seguendo [configura il database dopo il ripristino][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Ripristino di un database eliminato
un database eliminato toorestore:

1. Elencare tutti i database eliminati ripristinabili utilizzando hello [elenco ripristinabile eliminati database] [ List restorable dropped databases] operazione.
2. Ottenere i dettagli di hello per database hello eliminato da toorestore utilizzando hello [Get restorable eliminati database] [ Get restorable dropped database] operazione.
3. Iniziare il ripristino utilizzando hello [richiesta di ripristino di database crea] [ Create database restore request] operazione.
4. Tenere traccia dello stato di hello del ripristino utilizzando hello [dello stato dell'operazione di Database] [ Database operation status] operazione.

> [!NOTE]
> vedere il database al termine del ripristino di hello, tooconfigure [configura il database dopo il ripristino][Configure your database after recovery].
> 
> 

## <a name="next-steps"></a>Passaggi successivi
toolearn sulle funzionalità di continuità aziendale hello delle edizioni di Database SQL di Azure, leggere hello [Panoramica di continuità aziendale di Database SQL di Azure][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
