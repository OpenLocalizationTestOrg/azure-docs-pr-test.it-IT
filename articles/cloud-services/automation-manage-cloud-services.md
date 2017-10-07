---
title: Servizi Cloud di Azure utilizzando l'automazione di Azure aaaManage | Documenti Microsoft
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage di servizi cloud di Azure su larga scala."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a>Gestione dei Servizi cloud di Azure mediante Automazione di Azure
Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione dei servizi cloud di Azure.

## <a name="what-is-azure-automation"></a>Informazioni su Automazione di Azure
[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi. Utilizzando l'automazione di Azure, le attività a esecuzione prolungata, manuale, soggetta a errori e ripetute spesso possono essere toovalue tempo per l'organizzazione, efficienza e affidabilità tooincrease automatizzati.

Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze, man mano che aumenta l'organizzazione. In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.

Liberare e ridurre i costi operativi IT / DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a>Come può Automazione di Azure aiutare nella gestione dei Servizi cloud di Azure?
Servizi cloud di Azure possono essere gestiti in automazione di Azure tramite i cmdlet di PowerShell hello disponibili in hello [gli strumenti di Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx). Automazione di Azure offre disponibili i cmdlet PowerShell di servizio cloud viene fornita hello, in modo che è possibile eseguire tutte le attività di gestione del servizio cloud all'interno del servizio hello. È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.

Alcuni esempi di utilizzo dei servizi Cloud di Azure includono toomanage di automazione di Azure:

* [Distribuzione continua di un servizio cloud ogni volta che il file cscfg o cspkg viene aggiornato nell'archivio BLOB di Azure](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [Riavvio di istanze del servizio cloud in parallelo, un dominio di aggiornamento alla volta](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage servizi cloud di Azure, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.

* [Panoramica di Automazione di Azure](../automation/automation-intro.md)
* [Il primo runbook](../automation/automation-first-runbook-graphical.md)
* [Mappa di apprendimento di Automazione di Azure](https://azure.microsoft.com/documentation/learning-paths/automation/)
