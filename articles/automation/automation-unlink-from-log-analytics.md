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
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="2b2f3-103">Come toounlink l'automazione dell'account da un'area di lavoro Log Analitica</span><span class="sxs-lookup"><span data-stu-id="2b2f3-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="2b2f3-104">Automazione di Azure si integra con Log Analitica toonot solo supporto il monitoraggio proattivo dei processi di runbook in tutti gli account di automazione, ma è necessario anche quando si importa hello soluzioni che dipendono da Analitica Log seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b2f3-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="2b2f3-105">Gestione degli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="2b2f3-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="2b2f3-106">Rilevamento delle modifiche</span><span class="sxs-lookup"><span data-stu-id="2b2f3-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="2b2f3-107">Avviare/arrestare le VM durante gli orari di minore attività</span><span class="sxs-lookup"><span data-stu-id="2b2f3-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="2b2f3-108">Se si decide di che non si desidera più toointegrate l'account di automazione con Log Analitica, è possibile scollegare l'account direttamente dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="2b2f3-109">Prima di procedere, è necessario innanzitutto soluzioni hello tooremove indicate in precedenza, in caso contrario questo processo verrà impedito procedere.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="2b2f3-110">Argomento hello revisione per una particolare soluzione hello sono stati importati i passaggi di hello toounderstand necessari tooremove è.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="2b2f3-111">Dopo la rimozione di queste soluzioni è possibile eseguire hello seguendo i passaggi toounlink l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="2b2f3-112">Unlink workspace (Scollega area di lavoro)</span><span class="sxs-lookup"><span data-stu-id="2b2f3-112">Unlink workspace</span></span>

1. <span data-ttu-id="2b2f3-113">Dal portale di Azure hello, aprire l'account di automazione e nel pannello account di automazione hello, nel Pannello di account hello, selezionare **scollegare l'area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="2b2f3-114">![Opzione Unlink workspace (Scollega area di lavoro)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="2b2f3-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="2b2f3-115">Nel pannello dell'area di lavoro di hello Scollega, fare clic su **scollegare l'area di lavoro di**.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="2b2f3-116">![Pannello Unlink workspace (Scollega area di lavoro)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="2b2f3-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="2b2f3-117">Si riceverà una richiesta di verifica per determinare se che si desidera tooproceed.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="2b2f3-118">Durante l'automazione di Azure tenta account hello toounlink l'area di lavoro Log Analitica, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="2b2f3-119">Se si utilizza di soluzione di gestione degli aggiornamenti di hello, facoltativamente, è consigliabile hello tooremove elementi che non sono più necessarie dopo la rimozione di soluzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="2b2f3-120">Aggiornare le pianificazioni.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-120">Update schedules.</span></span>  <span data-ttu-id="2b2f3-121">Ogni avranno nomi che corrispondono a distribuzioni di aggiornamenti hello creato)</span><span class="sxs-lookup"><span data-stu-id="2b2f3-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="2b2f3-122">Gruppi di lavoro ibridi creati per la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="2b2f3-123">Ogni verrà denominato in modo analogo troppo machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="2b2f3-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="2b2f3-124">Se è stata utilizzata durante la soluzione di orario di lavoro macchine virtuali di avvio/arresto hello, facoltativamente è hello tooremove elementi che non sono più necessarie dopo la rimozione di soluzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="2b2f3-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="2b2f3-125">Avviare e arrestare le pianificazioni di runbook delle VM</span><span class="sxs-lookup"><span data-stu-id="2b2f3-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="2b2f3-126">Avviare e arrestare i runbook delle VM</span><span class="sxs-lookup"><span data-stu-id="2b2f3-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="2b2f3-127">Variabili</span><span class="sxs-lookup"><span data-stu-id="2b2f3-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="2b2f3-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b2f3-128">Next steps</span></span>

<span data-ttu-id="2b2f3-129">vedere il toointegrate di account di automazione con OMS Log Analitica, tooreconfigure [inoltra lo stato del processo e i flussi di lavoro da automazione tooLog Analitica (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="2b2f3-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
