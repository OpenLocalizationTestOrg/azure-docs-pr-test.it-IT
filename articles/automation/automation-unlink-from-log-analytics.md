---
title: Scollegare l'account di Automazione di Azure da Log Analytics | Documentazione Microsoft
description: Questo articolo offre una panoramica su come scollegare l'account di Automazione di Azure da un'area di lavoro di OMS.
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
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="40f01-103">Come scollegare l'account di automazione da un'area di lavoro di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="40f01-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="40f01-104">Automazione di Azure si integra con Log Analytics non solo per supportare il monitoraggio proattivo dei processi di runbook in tutti gli account di Automazione, ma l'integrazione è necessaria anche quando si importano le soluzioni seguenti che dipendono da Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="40f01-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="40f01-105">Gestione degli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="40f01-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="40f01-106">Rilevamento delle modifiche</span><span class="sxs-lookup"><span data-stu-id="40f01-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="40f01-107">Avviare/arrestare le VM durante gli orari di minore attività</span><span class="sxs-lookup"><span data-stu-id="40f01-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="40f01-108">Se si decide che non si vuole più integrare l'account di Automazione con Log Analytics, è possibile scollegare l'account direttamente dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40f01-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="40f01-109">Prima di procedere, è necessario rimuovere le soluzioni menzionate in precedenza; in caso contrario non sarà possibile continuare con il processo.</span><span class="sxs-lookup"><span data-stu-id="40f01-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="40f01-110">Esaminare l'argomento relativo alla soluzione specifica importata per comprendere i passaggi necessari per la rimozione.</span><span class="sxs-lookup"><span data-stu-id="40f01-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="40f01-111">Dopo la rimozione di queste soluzioni è possibile eseguire i passaggi seguenti per scollegare l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="40f01-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="40f01-112">Unlink workspace (Scollega area di lavoro)</span><span class="sxs-lookup"><span data-stu-id="40f01-112">Unlink workspace</span></span>

1. <span data-ttu-id="40f01-113">Nel portale di Azure aprire l'account di Automazione e nel pannello Account di automazione selezionare **Unlink workspace** (Scollega area di lavoro) nel pannello dell'account.</span><span class="sxs-lookup"><span data-stu-id="40f01-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="40f01-114">![Opzione Unlink workspace (Scollega area di lavoro)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="40f01-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="40f01-115">Nel pannello Unlink workspace (Scollega area di lavoro) fare clic su **Unlink workspace (Scollega area di lavoro)**.</span><span class="sxs-lookup"><span data-stu-id="40f01-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="40f01-116">![Pannello Unlink workspace (Scollega area di lavoro)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="40f01-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="40f01-117">Verrà richiesto di confermare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="40f01-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="40f01-118">Mentre Automazione di Azure tenta di scollegare l'account dall'area di lavoro di Log Analytics, è possibile tenere traccia dello stato di avanzamento in **Notifiche** dal menu.</span><span class="sxs-lookup"><span data-stu-id="40f01-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="40f01-119">Se è stata usata la soluzione di gestione degli aggiornamenti, facoltativamente è consigliabile rimuovere gli elementi seguenti che non sono più necessari dopo la rimozione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="40f01-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="40f01-120">Aggiornare le pianificazioni.</span><span class="sxs-lookup"><span data-stu-id="40f01-120">Update schedules.</span></span>  <span data-ttu-id="40f01-121">Ogni elemento avrà un nome corrispondente alle distribuzioni di aggiornamenti create.</span><span class="sxs-lookup"><span data-stu-id="40f01-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="40f01-122">Gruppi di ruoli di lavoro ibridi creati per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="40f01-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="40f01-123">Ogni elemento verrà denominato in modo analogo a machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8.</span><span class="sxs-lookup"><span data-stu-id="40f01-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="40f01-124">Se è stata usata la soluzione per avviare/arrestare VM durante gli orari di minore attività, facoltativamente è consigliabile rimuovere gli elementi seguenti che non sono più necessari dopo la rimozione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="40f01-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="40f01-125">Avviare e arrestare le pianificazioni di runbook delle VM</span><span class="sxs-lookup"><span data-stu-id="40f01-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="40f01-126">Avviare e arrestare i runbook delle VM</span><span class="sxs-lookup"><span data-stu-id="40f01-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="40f01-127">Variabili</span><span class="sxs-lookup"><span data-stu-id="40f01-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="40f01-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40f01-128">Next steps</span></span>

<span data-ttu-id="40f01-129">Per riconfigurare l'account di Automazione per l'integrazione con Log Analytics di OMS, vedere [Inoltrare lo stato e i flussi del processo da Automazione a Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="40f01-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 