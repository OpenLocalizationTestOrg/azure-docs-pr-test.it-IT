---
title: Database SQL di Azure utilizzando l'automazione di Azure aaaManage | Documenti Microsoft
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage di database SQL di Azure su larga scala."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Gestire i database SQL usando Automazione di Azure
Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione dei database SQL di Azure.

## <a name="what-is-azure-automation"></a>Informazioni su Automazione di Azure
[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi. Utilizzando l'automazione di Azure, le attività a esecuzione prolungata, manuale, soggetta a errori e ripetute spesso possono essere toovalue tempo per l'organizzazione, efficienza e affidabilità tooincrease automatizzati.

Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze, man mano che aumenta l'organizzazione. In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.

Liberare e ridurre i costi operativi IT / DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Come può Automazione di Azure aiutare nella gestione dei database SQL?
Database SQL di Azure possono essere gestito in automazione di Azure con hello [i cmdlet di PowerShell per Azure SQL Database](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) che sono disponibili in hello [gli strumenti di Azure PowerShell](/powershell/azure/overview). Automazione di Azure dispone di questi cmdlet di PowerShell per Azure SQL Database disponibili predefinito hello, che è possibile eseguire tutte le attività di gestione di database di SQL Server all'interno del servizio di hello. È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.

Automazione di Azure dispone inoltre hello possibilità toocommunicate con istanze di SQL Server direttamente, eseguendo i comandi SQL con PowerShell.

Hello [raccolta di runbook di automazione di Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene un'ampia gamma di prodotti team e community runbook tooget avviato l'automazione della gestione di database SQL di Azure, gli altri servizi di Azure e sistemi di terze parti 3rd. I Runbook della raccolta includono i seguenti:

* [Eseguire query SQL su un database SQL Server](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [Scalabilità verticale (verso l’alto o il basso) di un database di SQL Azure in una pianificazione](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Troncare una tabella SQL se il database si avvicina alla dimensione massima](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Tabelle dell’indice in un database SQL di Azure se sono molto frammentati](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso hello nozioni di base automazione di Azure e come può essere toomanage utilizzati database di SQL Azure, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.

* [Panoramica di Automazione di Azure](../automation/automation-intro.md)
* [Il primo runbook](../automation/automation-first-runbook-graphical.md)
* [Mappa di apprendimento di Automazione di Azure](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Automazione di Azure: L'agente SQL in hello Cloud](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

