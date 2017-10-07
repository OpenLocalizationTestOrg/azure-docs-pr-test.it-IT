---
title: "set di scalabilità di macchine virtuali di Azure scala aaaVertically | Documenti Microsoft"
description: Come toovertically ridimensionare una macchina virtuale negli avvisi toomonitoring risposta con automazione di Azure
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="1d110-103">Ridimensionamento automatico verticale con set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1d110-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="1d110-104">In questo articolo vengono descritte le modalità di scalabilità di Azure toovertically [set di scalabilità di macchine virtuali](https://azure.microsoft.com/services/virtual-machine-scale-sets/) con o senza la riconfigurazione.</span><span class="sxs-lookup"><span data-stu-id="1d110-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="1d110-105">Per la scalabilità verticale delle macchine virtuali che non sono presenti nel set di scalabilità, vedere troppo[scalare verticalmente macchina virtuale di Azure con automazione di Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d110-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="1d110-106">La scalabilità verticale, anche noto come *scalabilità verticale* e *scalare verso il basso*indica aumentando o riducendo le dimensioni di macchina virtuale (VM) del carico di lavoro di risposta tooa.</span><span class="sxs-lookup"><span data-stu-id="1d110-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="1d110-107">Confronto con [scalabilità orizzontale](virtual-machine-scale-sets-autoscale-overview.md), definita anche tooas *scalabilità* e *ridimensionare in*, in cui è stato modificato il numero di hello di macchine virtuali a seconda del carico di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="1d110-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="1d110-108">Per nuovo provisioning si intende la rimozione di una VM esistente e la relativa sostituzione con una nuova.</span><span class="sxs-lookup"><span data-stu-id="1d110-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="1d110-109">Quando si aumentare o diminuire le dimensioni di hello di macchine virtuali in un Set di scalabilità della macchina virtuale, in alcuni casi si desidera tooresize le macchine virtuali esistenti e mantenere i dati, mentre in altri casi è necessario toodeploy nuove macchine virtuali della nuova dimensione hello.</span><span class="sxs-lookup"><span data-stu-id="1d110-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="1d110-110">Questo documento illustra entrambi i casi.</span><span class="sxs-lookup"><span data-stu-id="1d110-110">This document covers both cases.</span></span>

<span data-ttu-id="1d110-111">Il ridimensionamento verticale, ovvero l'aumento o la riduzione delle prestazioni, può risultare utile quando:</span><span class="sxs-lookup"><span data-stu-id="1d110-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="1d110-112">Un servizio basato su macchine virtuali è sottoutilizzato, ad esempio nel fine settimana.</span><span class="sxs-lookup"><span data-stu-id="1d110-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="1d110-113">Riduzione delle dimensioni di VM hello, è possibile ridurre i costi mensili.</span><span class="sxs-lookup"><span data-stu-id="1d110-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="1d110-114">Aumento toocope dimensioni di macchina virtuale con richiesta di dimensioni maggiore senza creare altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1d110-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="1d110-115">È possibile impostare verticale scalabilità toobe attivato basati sugli avvisi di base metrica dal Set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d110-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="1d110-116">Quando viene attivato hello avviso viene generato un webhook che attiva un runbook che è possibile ridimensionare la scala è impostato su o giù.</span><span class="sxs-lookup"><span data-stu-id="1d110-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="1d110-117">Il ridimensionamento verticale può essere configurato seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d110-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="1d110-118">Creare un account di Automazione di Azure con funzionalità RunAs.</span><span class="sxs-lookup"><span data-stu-id="1d110-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="1d110-119">Importare i runbook di scalabilità verticale di Automazione di Azure per i set di scalabilità di macchine virtuali nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1d110-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="1d110-120">Aggiungere un runbook tooyour webhook.</span><span class="sxs-lookup"><span data-stu-id="1d110-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="1d110-121">Aggiungere un avviso tooyour Set di scalabilità macchina virtuale utilizza la notifica di un webhook.</span><span class="sxs-lookup"><span data-stu-id="1d110-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="1d110-122">Il ridimensionamento verticale può avvenire solo entro determinati intervalli di dimensioni delle VM.</span><span class="sxs-lookup"><span data-stu-id="1d110-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="1d110-123">Confronto delle specifiche di hello di ogni dimensione prima di decidere tooscale da uno tooanother (numero più alto non indicare sempre più grande dimensione della macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="1d110-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="1d110-124">È possibile scegliere tooscale tra hello coppie di dimensioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d110-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="1d110-125">coppie di ridimensionamento di dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1d110-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="1d110-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="1d110-126">Standard_A0</span></span> |<span data-ttu-id="1d110-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="1d110-127">Standard_A11</span></span> |
> | <span data-ttu-id="1d110-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="1d110-128">Standard_D1</span></span> |<span data-ttu-id="1d110-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="1d110-129">Standard_D14</span></span> |
> | <span data-ttu-id="1d110-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="1d110-130">Standard_DS1</span></span> |<span data-ttu-id="1d110-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="1d110-131">Standard_DS14</span></span> |
> | <span data-ttu-id="1d110-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="1d110-132">Standard_D1v2</span></span> |<span data-ttu-id="1d110-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="1d110-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="1d110-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="1d110-134">Standard_G1</span></span> |<span data-ttu-id="1d110-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="1d110-135">Standard_G5</span></span> |
> | <span data-ttu-id="1d110-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="1d110-136">Standard_GS1</span></span> |<span data-ttu-id="1d110-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="1d110-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="1d110-138">Creare un account di Automazione di Azure con funzionalità RunAs</span><span class="sxs-lookup"><span data-stu-id="1d110-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="1d110-139">Hello occorre innanzitutto toodo è creare un account di automazione di Azure che ospiterà hello runbook utilizzato tooscale hello Set di scalabilità della macchina virtuale istanze.</span><span class="sxs-lookup"><span data-stu-id="1d110-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="1d110-140">Recentemente [automazione di Azure](https://azure.microsoft.com/services/automation/) introdotte funzionalità "Esegui come account" hello che rende impostazione hello dell'entità servizio per l'esecuzione automatica hello runbook per conto dell'utente molto semplice.</span><span class="sxs-lookup"><span data-stu-id="1d110-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="1d110-141">È possibile leggere altre informazioni nell'articolo hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1d110-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="1d110-142">Autenticare runbook con account RunAs di Azure</span><span class="sxs-lookup"><span data-stu-id="1d110-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="1d110-143">Importare i runbook di ridimensionamento verticale di Automazione di Azure nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="1d110-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="1d110-144">i runbook Hello necessario scala toovertically che il set di scalabilità di macchine Virtuali sono già pubblicati nella raccolta di Runbook di automazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1d110-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="1d110-145">nella sottoscrizione seguono hello tooimport passaggi riportati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1d110-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="1d110-146">Raccolte di runbook e moduli per l'automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1d110-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="1d110-147">Scegliere l'opzione Sfoglia raccolta hello dal menu di runbook hello:</span><span class="sxs-lookup"><span data-stu-id="1d110-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![Toobe runbook importati][runbooks]

<span data-ttu-id="1d110-149">i runbook Hello necessario toobe importati vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="1d110-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="1d110-150">Selezionare il runbook hello in base che si voglia con o senza la riconfigurazione della scalabilità verticale:</span><span class="sxs-lookup"><span data-stu-id="1d110-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Raccolta di runbook][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="1d110-152">Aggiungere un runbook tooyour webhook</span><span class="sxs-lookup"><span data-stu-id="1d110-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="1d110-153">Dopo aver importato i runbook hello è necessario un runbook toohello webhook tooadd in modo che può essere attivata da un avviso generato da un Set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d110-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="1d110-154">in questo articolo sono descritti i dettagli di Hello per la creazione di un webhook per il Runbook:</span><span class="sxs-lookup"><span data-stu-id="1d110-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="1d110-155">Webhook di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1d110-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="1d110-156">Assicurarsi di copiare hello webhook URI prima della chiusura di finestra di dialogo webhook hello perché sarà necessaria nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="1d110-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="1d110-157">Aggiungere un avviso tooyour Set di scalabilità della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1d110-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="1d110-158">Di seguito è riportato un PowerShell script che mostra come tooadd un avviso tooa Set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d110-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="1d110-159">Fare riferimento toohello dopo il nome di hello articolo tooget di avviso di hello toofire metrica hello: [comuni metriche di monitoraggio di Azure per la scalabilità automatica](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="1d110-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> <span data-ttu-id="1d110-160">È consigliabile tooconfigure un intervallo di tempo ragionevole per avviso hello in ordine tooavoid attivando la scalabilità verticale e qualsiasi associata un'interruzione del servizio, troppo spesso.</span><span class="sxs-lookup"><span data-stu-id="1d110-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="1d110-161">Considerare un intervallo minimo di 20-30 minuti.</span><span class="sxs-lookup"><span data-stu-id="1d110-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="1d110-162">È consigliabile se è necessario tooavoid interruzione la scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="1d110-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="1d110-163">Per ulteriori informazioni su come toocreate avvisi fare riferimento toohello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="1d110-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* <span data-ttu-id="1d110-164">[Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure)</span><span class="sxs-lookup"><span data-stu-id="1d110-164">[Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="1d110-165">[Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md) (Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma per Monitoraggio di Azure)</span><span class="sxs-lookup"><span data-stu-id="1d110-165">[Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>

## <a name="summary"></a><span data-ttu-id="1d110-166">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="1d110-166">Summary</span></span>
<span data-ttu-id="1d110-167">Questo articolo ha illustrato semplici esempi di ridimensionamento verticale.</span><span class="sxs-lookup"><span data-stu-id="1d110-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="1d110-168">Con questi blocchi predefiniti, ovvero account di automazione, runbook, webhook e avvisi, è possibile connettere una vasta gamma di eventi con un set di azioni personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1d110-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
