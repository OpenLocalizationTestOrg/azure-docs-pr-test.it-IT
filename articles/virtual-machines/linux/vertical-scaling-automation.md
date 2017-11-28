---
title: "Scalabilità verticale di macchine virtuali di Azure tramite Automazione di Azure | Microsoft Docs"
description: "Come eseguire la scalabilità verticale di una macchina virtuale Linux in risposta agli avvisi di monitoraggio tramite Automazione di Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1ffcecf1e61fc0cd9ee668514fbb913dafe39bd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="ce094-103">Scalabilità verticale di macchine virtuali di Linux in Azure tramite Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ce094-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="ce094-104">La scalabilità verticale è il processo di aumento o riduzione delle risorse di una macchina in risposta al carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ce094-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="ce094-105">In Azure tale operazione può essere eseguita modificando le dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ce094-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="ce094-106">Può essere utile negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="ce094-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="ce094-107">Se la macchina virtuale non viene usata di frequente, è possibile diminuirne le dimensioni per ridurre i costi mensili</span><span class="sxs-lookup"><span data-stu-id="ce094-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="ce094-108">Se nella macchina virtuale si osserva un picco di carico, è possibile aumentarne le dimensioni per una maggiore capacità</span><span class="sxs-lookup"><span data-stu-id="ce094-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="ce094-109">Per eseguire questa operazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ce094-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="ce094-110">Configurare Automazione di Azure per l'accesso alle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ce094-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="ce094-111">Importare i runbook di scalabilità verticale di Automazione di Azure nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ce094-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="ce094-112">Aggiungere un webhook al runbook</span><span class="sxs-lookup"><span data-stu-id="ce094-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="ce094-113">Aggiungere un avviso alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ce094-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="ce094-114">A causa delle dimensioni della prima macchina virtuale, le dimensioni a cui la macchina può essere ridimensionata possono essere limitate a seconda della disponibilità di altre dimensioni nel cluster in cui viene distribuita la macchina virtuale corrente.</span><span class="sxs-lookup"><span data-stu-id="ce094-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="ce094-115">Nei runbook di automazione pubblicati usati in questo articolo viene considerato questo caso e la scalabilità viene applicata solo all'interno delle coppie di dimensioni delle macchine virtuali seguenti.</span><span class="sxs-lookup"><span data-stu-id="ce094-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="ce094-116">Pertanto, una macchina virtuale Standard_D1v2 non verrà improvvisamente ridimensionata verso l'alto a una Standard_G5 o verso il basso a una Basic_A0.</span><span class="sxs-lookup"><span data-stu-id="ce094-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="ce094-117">coppie di ridimensionamento di dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ce094-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="ce094-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="ce094-118">Basic_A0</span></span> |<span data-ttu-id="ce094-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="ce094-119">Basic_A4</span></span> |
> | <span data-ttu-id="ce094-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="ce094-120">Standard_A0</span></span> |<span data-ttu-id="ce094-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="ce094-121">Standard_A4</span></span> |
> | <span data-ttu-id="ce094-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="ce094-122">Standard_A5</span></span> |<span data-ttu-id="ce094-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="ce094-123">Standard_A7</span></span> |
> | <span data-ttu-id="ce094-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="ce094-124">Standard_A8</span></span> |<span data-ttu-id="ce094-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="ce094-125">Standard_A9</span></span> |
> | <span data-ttu-id="ce094-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="ce094-126">Standard_A10</span></span> |<span data-ttu-id="ce094-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="ce094-127">Standard_A11</span></span> |
> | <span data-ttu-id="ce094-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="ce094-128">Standard_D1</span></span> |<span data-ttu-id="ce094-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="ce094-129">Standard_D4</span></span> |
> | <span data-ttu-id="ce094-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="ce094-130">Standard_D11</span></span> |<span data-ttu-id="ce094-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="ce094-131">Standard_D14</span></span> |
> | <span data-ttu-id="ce094-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="ce094-132">Standard_DS1</span></span> |<span data-ttu-id="ce094-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="ce094-133">Standard_DS4</span></span> |
> | <span data-ttu-id="ce094-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="ce094-134">Standard_DS11</span></span> |<span data-ttu-id="ce094-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="ce094-135">Standard_DS14</span></span> |
> | <span data-ttu-id="ce094-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="ce094-136">Standard_D1v2</span></span> |<span data-ttu-id="ce094-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="ce094-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="ce094-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="ce094-138">Standard_D11v2</span></span> |<span data-ttu-id="ce094-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="ce094-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="ce094-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="ce094-140">Standard_G1</span></span> |<span data-ttu-id="ce094-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="ce094-141">Standard_G5</span></span> |
> | <span data-ttu-id="ce094-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="ce094-142">Standard_GS1</span></span> |<span data-ttu-id="ce094-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="ce094-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="ce094-144">Configurare Automazione di Azure per l'accesso alle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ce094-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="ce094-145">La prima operazione da eseguire è creare l'account di Automazione di Azure che ospiterà i runbook usati per ridimensionare le istanze del set di scalabilità VM.</span><span class="sxs-lookup"><span data-stu-id="ce094-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span></span> <span data-ttu-id="ce094-146">Il servizio Automazione ha introdotto di recente la funzionalità "Account RunAs", che semplifica molto l'impostazione dell'entità servizio per l'esecuzione automatica di runbook per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ce094-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="ce094-147">Altre informazioni sono disponibili nell'articolo seguente.</span><span class="sxs-lookup"><span data-stu-id="ce094-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="ce094-148">Autenticare runbook con account RunAs di Azure</span><span class="sxs-lookup"><span data-stu-id="ce094-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="ce094-149">Importare i runbook di scalabilità verticale di Automazione di Azure nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ce094-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="ce094-150">I runbook necessari per la scalabilità verticale della macchina virtuale sono già stati pubblicati nella raccolta dei runbook di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce094-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="ce094-151">Sarà necessario importarli nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ce094-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="ce094-152">Per informazioni sull'importazione dei runbook, vedere l'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="ce094-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="ce094-153">Raccolte di runbook e moduli per l'automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ce094-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="ce094-154">I runbook da importare sono visualizzati nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="ce094-154">The runbooks that need to be imported are shown in the image below</span></span>

![Importazione runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="ce094-156">Aggiungere un webhook al runbook</span><span class="sxs-lookup"><span data-stu-id="ce094-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="ce094-157">Dopo aver importato i runbook, è necessario aggiungere un webhook al runbook in modo che possa essere attivato da un avviso da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ce094-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="ce094-158">Informazioni dettagliate sulla creazione di un webhook per il runbook sono disponibili nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="ce094-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="ce094-159">Webhook di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ce094-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="ce094-160">Assicurarsi di copiare il webhook prima di chiudere la finestra di dialogo del webhook, in quanto sarà necessario nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="ce094-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="ce094-161">Aggiungere un avviso alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ce094-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="ce094-162">Selezionare le impostazioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ce094-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="ce094-163">Selezionare "Regole di avviso"</span><span class="sxs-lookup"><span data-stu-id="ce094-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="ce094-164">Selezionare "Aggiungi avviso"</span><span class="sxs-lookup"><span data-stu-id="ce094-164">Select "Add alert"</span></span>
4. <span data-ttu-id="ce094-165">Selezionare una metrica per attivare l'avviso</span><span class="sxs-lookup"><span data-stu-id="ce094-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="ce094-166">Selezionare una condizione che, se soddisfatta, farà generare l'avviso</span><span class="sxs-lookup"><span data-stu-id="ce094-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="ce094-167">Selezionare una soglia affinché la condizione nel passaggio 5</span><span class="sxs-lookup"><span data-stu-id="ce094-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="ce094-168">sia soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="ce094-168">to be fulfilled</span></span>
7. <span data-ttu-id="ce094-169">Selezionare un periodo in cui il servizio di monitoraggio verificherà la condizione e la soglia dei passaggi 5 e 6</span><span class="sxs-lookup"><span data-stu-id="ce094-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="ce094-170">Incollare il webhook copiato dalla sezione precedente</span><span class="sxs-lookup"><span data-stu-id="ce094-170">Paste in the webhook you copied from the previous section.</span></span>

![Aggiunta di un avviso alla macchina virtuale 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Aggiunta di un avviso alla macchina virtuale 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

