---
title: Panoramica di DSC di automazione aaaAzure | Documenti Microsoft
description: Panoramica della piattaforma DSC (Desired State Configuration) di Automazione di Azure, dei termini a essa relativi e dei problemi noti
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powershell dsc, configurazione dello stato desiderato, powershell dsc azure
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Panoramica della piattaforma DSC di Automazione di Azure

DSC di automazione di Azure è un servizio di Azure che consente di toowrite, gestire e compilare PowerShell DSC Desired State Configuration () [configurazioni](https://msdn.microsoft.com/powershell/dsc/configurations), importare [risorse DSC](https://msdn.microsoft.com/powershell/dsc/resources)e assegnare configurazioni tootarget nodi, tutti i cloud hello.

## <a name="why-use-azure-automation-dsc"></a>Perché usare Automation DSC per Azure

Automation DSC per Azure offre diversi vantaggi rispetto all'uso di DSC al di fuori di Azure.

### <a name="built-in-pull-server"></a>Server di pull predefinito

Automazione di Azure fornisce un [server di pull DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) in modo che i nodi di destinazione ricevano automaticamente le configurazioni, stato toohello desiderato è conforme e segnalare la conformità.
server di pull predefinite Hello in automazione di Azure Elimina hello necessità tooset backup e gestire il proprio server di pull.
Automazione di Azure può far riferimento a computer virtuali o fisici Windows o Linux, in locale o cloud hello.

### <a name="management-of-all-your-dsc-artifacts"></a>Gestione di tutti gli elementi DSC

DSC di automazione di Azure offre hello stesso livello di gestione troppo[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) come l'automazione di Azure offre per lo script di PowerShell.

Dal portale di Azure hello o da PowerShell, è possibile gestire tutti i DSC le configurazioni, risorse e nodi di destinazione.

![Cattura di schermata del Pannello di automazione di Azure hello](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Importare i dati dei report in Log Analytics

Nodi gestiti con Automation DSC per Azure trasmissione dettagliata stato dati toohello pull predefinite server di report.
È possibile configurare automazione di Azure DSC toosend questa area di lavoro di dati tooyour Analitica di Log di Microsoft Operations Management Suite (OMS).
toolearn toosend DSC stato dati tooyour area di lavoro Analitica di Log, vedere [rollforward Automation DSC per Azure reporting dati tooOMS Analitica Log](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Video introduttivo

Se si preferisce guardare il video tooreading, Sono esaminati hello seguente video da maggio 2015, quando cui è stato annunciato Automation DSC per Azure.

>[!NOTE]
>Mentre i concetti di hello e ciclo di vita descritti in questo video sono corrette, DSC di automazione di Azure è molto avanzato poiché in questo video è stato registrato.
>È ora disponibile in genere, è un'interfaccia molto più ampia utente nel portale di Azure hello e supporta numerose funzionalità aggiuntive.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Passaggi successivi

* toolearn come tooonboard toobe di nodi gestiti con DSC di automazione di Azure, vedere [macchine di caricamento per la gestione da Automation DSC per Azure](automation-dsc-onboarding.md)
* tooget avviato tramite DSC di automazione di Azure, vedere [Introduzione a DSC di automazione di Azure](automation-dsc-getting-started.md)
* toolearn sulla compilazione di configurazioni DSC in modo che è possibile assegnarli tootarget nodi, vedere [compilazione delle configurazioni in automazione di Azure DSC](automation-dsc-compile.md)
* Per informazioni di riferimento sui cmdlet di PowerShell per Automation DSC per Azure, vedere [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation) (Cmdlet di Automation DSC per Azure)
* Per informazioni sui prezzi, vedere [Prezzi di Automation DSC per Azure](https://azure.microsoft.com/pricing/details/automation/)
* vedere un esempio di utilizzo di Automation DSC per Azure in una pipeline di distribuzione continua, toosee [tooIaaS distribuzione continua DSC di automazione di Azure utilizzando macchine virtuali e Chocolatey](automation-dsc-cd-chocolatey.md)
