---
title: "toovertically di automazione di Azure aaaUse scalabilità di macchine virtuali di Windows | Documenti Microsoft"
description: Scalare verticalmente una macchina virtuale Windows negli avvisi toomonitoring risposta con automazione di Azure
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="e6e0f-103">Applicare la scalabilità verticale a macchine virtuali di Windows con Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e6e0f-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="e6e0f-104">La scalabilità verticale è il processo di hello di aumento o diminuzione risorse hello di un computer nel carico di lavoro di risposta toohello.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="e6e0f-105">In Azure può essere eseguita mediante la modifica delle dimensioni hello di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="e6e0f-106">Ciò consente in hello seguenti scenari</span><span class="sxs-lookup"><span data-stu-id="e6e0f-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="e6e0f-107">Se non viene utilizzato spesso hello macchina virtuale, è possibile ridimensionarla verso il basso tooreduce dimensioni più piccole tooa i costi mensili</span><span class="sxs-lookup"><span data-stu-id="e6e0f-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="e6e0f-108">Se hello macchina virtuale viene visualizzato un carico di picco, può essere ridimensionato tooa tooincrease di dimensioni maggiori capacità</span><span class="sxs-lookup"><span data-stu-id="e6e0f-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="e6e0f-109">struttura Hello per hello passaggi tooaccomplish si tratta di seguito</span><span class="sxs-lookup"><span data-stu-id="e6e0f-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="e6e0f-110">Programma di installazione tooaccess di automazione di Azure le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e6e0f-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="e6e0f-111">Importazione dei runbook di hello scalabilità verticale di automazione di Azure alla sottoscrizione di</span><span class="sxs-lookup"><span data-stu-id="e6e0f-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="e6e0f-112">Aggiungere un runbook tooyour webhook</span><span class="sxs-lookup"><span data-stu-id="e6e0f-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="e6e0f-113">Aggiungere un avviso tooyour macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e6e0f-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="e6e0f-114">A causa delle dimensioni di hello hello prima macchina virtuale, le dimensioni di hello possono essere ridimensionato, potrebbe risultare limitato a causa della disponibilità toohello di hello altre dimensioni cluster hello macchina virtuale corrente viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="e6e0f-115">In hello pubblicato il runbook di automazione usato in questo articolo si occuperà del case e applicare la scalabilità solo all'interno di hello di sotto di coppie di dimensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="e6e0f-116">Ciò significa che una macchina virtuale Standard_D1v2 verranno non improvvisamente ridimensionati tooStandard_G5 o scalabilità verso il basso tooBasic_A0.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="e6e0f-117">coppie di ridimensionamento di dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e6e0f-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="e6e0f-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="e6e0f-118">Basic_A0</span></span> |<span data-ttu-id="e6e0f-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="e6e0f-119">Basic_A4</span></span> |
> | <span data-ttu-id="e6e0f-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="e6e0f-120">Standard_A0</span></span> |<span data-ttu-id="e6e0f-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="e6e0f-121">Standard_A4</span></span> |
> | <span data-ttu-id="e6e0f-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="e6e0f-122">Standard_A5</span></span> |<span data-ttu-id="e6e0f-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="e6e0f-123">Standard_A7</span></span> |
> | <span data-ttu-id="e6e0f-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="e6e0f-124">Standard_A8</span></span> |<span data-ttu-id="e6e0f-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="e6e0f-125">Standard_A9</span></span> |
> | <span data-ttu-id="e6e0f-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="e6e0f-126">Standard_A10</span></span> |<span data-ttu-id="e6e0f-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="e6e0f-127">Standard_A11</span></span> |
> | <span data-ttu-id="e6e0f-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="e6e0f-128">Standard_D1</span></span> |<span data-ttu-id="e6e0f-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="e6e0f-129">Standard_D4</span></span> |
> | <span data-ttu-id="e6e0f-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="e6e0f-130">Standard_D11</span></span> |<span data-ttu-id="e6e0f-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="e6e0f-131">Standard_D14</span></span> |
> | <span data-ttu-id="e6e0f-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="e6e0f-132">Standard_DS1</span></span> |<span data-ttu-id="e6e0f-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="e6e0f-133">Standard_DS4</span></span> |
> | <span data-ttu-id="e6e0f-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="e6e0f-134">Standard_DS11</span></span> |<span data-ttu-id="e6e0f-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="e6e0f-135">Standard_DS14</span></span> |
> | <span data-ttu-id="e6e0f-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="e6e0f-136">Standard_D1v2</span></span> |<span data-ttu-id="e6e0f-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="e6e0f-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="e6e0f-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="e6e0f-138">Standard_D11v2</span></span> |<span data-ttu-id="e6e0f-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="e6e0f-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="e6e0f-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="e6e0f-140">Standard_G1</span></span> |<span data-ttu-id="e6e0f-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="e6e0f-141">Standard_G5</span></span> |
> | <span data-ttu-id="e6e0f-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="e6e0f-142">Standard_GS1</span></span> |<span data-ttu-id="e6e0f-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="e6e0f-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="e6e0f-144">Programma di installazione tooaccess di automazione di Azure le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e6e0f-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="e6e0f-145">Hello occorre innanzitutto toodo è creare un account di automazione di Azure che ospiterà hello runbook utilizzato tooscale una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale a Virtual Machine.</span></span> <span data-ttu-id="e6e0f-146">Servizio automazione hello introdotto di recente funzionalità "Esegui come account" hello che rende impostazione hello dell'entità servizio per l'esecuzione automatica hello runbook per conto dell'utente hello molto semplice.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="e6e0f-147">È possibile leggere altre informazioni nell'articolo hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e6e0f-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="e6e0f-148">Autenticare runbook con account RunAs di Azure</span><span class="sxs-lookup"><span data-stu-id="e6e0f-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="e6e0f-149">Importazione dei runbook di hello scalabilità verticale di automazione di Azure alla sottoscrizione di</span><span class="sxs-lookup"><span data-stu-id="e6e0f-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="e6e0f-150">runbook Hello che sono necessari per la scalabilità verticale della macchina virtuale sono già pubblicati in hello raccolta di Runbook di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="e6e0f-151">Sarà necessario tooimport nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="e6e0f-152">È possibile apprendere come tooimport runbook leggendo hello articolo seguente.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="e6e0f-153">Raccolte di runbook e moduli per l'automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e6e0f-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="e6e0f-154">i runbook Hello necessario toobe importati sono illustrati nella figura hello seguente</span><span class="sxs-lookup"><span data-stu-id="e6e0f-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Importazione runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="e6e0f-156">Aggiungere un runbook tooyour webhook</span><span class="sxs-lookup"><span data-stu-id="e6e0f-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="e6e0f-157">Dopo aver importato i runbook hello è necessario un runbook toohello webhook tooadd in modo che può essere attivata da un avviso da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="e6e0f-158">dettagli di Hello per la creazione di un webhook per i Runbook possono essere letti qui</span><span class="sxs-lookup"><span data-stu-id="e6e0f-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="e6e0f-159">Webhook di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e6e0f-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="e6e0f-160">Assicurarsi di copiare hello webhook prima della chiusura di finestra di dialogo webhook hello perché sarà necessaria nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="e6e0f-161">Aggiungere un avviso tooyour macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e6e0f-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="e6e0f-162">Selezionare le impostazioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e6e0f-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="e6e0f-163">Selezionare "Regole di avviso"</span><span class="sxs-lookup"><span data-stu-id="e6e0f-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="e6e0f-164">Selezionare "Aggiungi avviso"</span><span class="sxs-lookup"><span data-stu-id="e6e0f-164">Select "Add alert"</span></span>
4. <span data-ttu-id="e6e0f-165">Selezionare un avviso di hello toofire metrica in</span><span class="sxs-lookup"><span data-stu-id="e6e0f-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="e6e0f-166">Selezionare una condizione, che una volta soddisfatti verrà causare toofire avviso hello</span><span class="sxs-lookup"><span data-stu-id="e6e0f-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="e6e0f-167">Selezionare una soglia per la condizione hello nel passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="e6e0f-168">toobe soddisfatte</span><span class="sxs-lookup"><span data-stu-id="e6e0f-168">toobe fulfilled</span></span>
7. <span data-ttu-id="e6e0f-169">Selezionare un periodo di su quale hello monitoraggio del servizio verrà verificato per la condizione di hello e soglia in passaggi 5 e 6</span><span class="sxs-lookup"><span data-stu-id="e6e0f-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="e6e0f-170">Incollare in webhook hello copiato dalla sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="e6e0f-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Aggiungere avvisi tooVirtual 1 computer](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Aggiungere avvisi tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

