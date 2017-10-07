---
title: account di automazione di Azure dal Log Analitica aaaUnlink | Documenti Microsoft
description: In questo articolo viene fornita una panoramica di come toounlink account di automazione di Azure da un'area di lavoro OMS.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>Come toounlink l'automazione dell'account da un'area di lavoro Log Analitica

Automazione di Azure si integra con Log Analitica toonot solo supporto il monitoraggio proattivo dei processi di runbook in tutti gli account di automazione, ma è necessario anche quando si importa hello soluzioni che dipendono da Analitica Log seguenti:

* [Gestione degli aggiornamenti](../operations-management-suite/oms-solution-update-management.md)
* [Rilevamento delle modifiche](../log-analytics/log-analytics-change-tracking.md)
* [Avviare/arrestare le VM durante gli orari di minore attività](automation-solution-vm-management.md)
 
Se si decide di che non si desidera più toointegrate l'account di automazione con Log Analitica, è possibile scollegare l'account direttamente dal portale di Azure hello.  Prima di procedere, è necessario innanzitutto soluzioni hello tooremove indicate in precedenza, in caso contrario questo processo verrà impedito procedere.  Argomento hello revisione per una particolare soluzione hello sono stati importati i passaggi di hello toounderstand necessari tooremove è.  

Dopo la rimozione di queste soluzioni è possibile eseguire hello seguendo i passaggi toounlink l'account di automazione.

## <a name="unlink-workspace"></a>Unlink workspace (Scollega area di lavoro)

1. Dal portale di Azure hello, aprire l'account di automazione e nel pannello account di automazione hello, nel Pannello di account hello, selezionare **scollegare l'area di lavoro**.<br><br> ![Opzione Unlink workspace (Scollega area di lavoro)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. Nel pannello dell'area di lavoro di hello Scollega, fare clic su **scollegare l'area di lavoro di**.<br><br> ![Pannello Unlink workspace (Scollega area di lavoro)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  Si riceverà una richiesta di verifica per determinare se che si desidera tooproceed.<br><br>
3. Durante l'automazione di Azure tenta account hello toounlink l'area di lavoro Log Analitica, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.

Se si utilizza di soluzione di gestione degli aggiornamenti di hello, facoltativamente, è consigliabile hello tooremove elementi che non sono più necessarie dopo la rimozione di soluzioni di hello.

* Aggiornare le pianificazioni.  Ogni avranno nomi che corrispondono a distribuzioni di aggiornamenti hello creato)

* Gruppi di lavoro ibridi creati per la soluzione hello.  Ogni verrà denominato in modo analogo troppo machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

Se è stata utilizzata durante la soluzione di orario di lavoro macchine virtuali di avvio/arresto hello, facoltativamente è hello tooremove elementi che non sono più necessarie dopo la rimozione di soluzioni di hello.

* Avviare e arrestare le pianificazioni di runbook delle VM 
* Avviare e arrestare i runbook delle VM
* Variabili   

## <a name="next-steps"></a>Passaggi successivi

vedere il toointegrate di account di automazione con OMS Log Analitica, tooreconfigure [inoltra lo stato del processo e i flussi di lavoro da automazione tooLog Analitica (OMS)](automation-manage-send-joblogs-log-analytics.md). 
