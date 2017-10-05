---
title: "Ridimensionare verticalmente set di scalabilità di macchine virtuali di Azure | Microsoft Docs"
description: "Come eseguire la scalabilità verticale di una macchina virtuale in risposta agli avvisi di monitoraggio tramite Automazione di Azure"
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
ms.openlocfilehash: 9159a5a9041864fe06785829121233379c46bb03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="84118-103">Ridimensionamento automatico verticale con set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="84118-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="84118-104">In questo articolo viene descritto come ridimensionare in verticale i [set di macchine virtuali](https://azure.microsoft.com/services/virtual-machine-scale-sets/) di Azure con o senza un nuovo provisioning.</span><span class="sxs-lookup"><span data-stu-id="84118-104">This article describes how to vertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="84118-105">Per il ridimensionamento verticale delle VM non incluse nei set di scalabilità, vedere l'articolo [Ridimensionamento verticale di macchine virtuali di Azure tramite Automazione di Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84118-105">For vertical scaling of VMs which are not in scale sets, refer to [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="84118-106">Per ridimensionamento verticale, detto anche *aumento delle prestazioni* e *riduzione delle prestazioni*, si intende l'aumento o la riduzione delle dimensioni delle macchine virtuali (VM) in risposta a un carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="84118-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response to a workload.</span></span> <span data-ttu-id="84118-107">Confrontare questo concetto con il [ridimensionamento orizzontale](virtual-machine-scale-sets-autoscale-overview.md), detto anche *aumento delle istanze* e *riduzione delle istanze*, in cui il numero di VM viene modificato in base al carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="84118-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred to as *scale out* and *scale in*, where the number of VMs is altered depending on the workload.</span></span>

<span data-ttu-id="84118-108">Per nuovo provisioning si intende la rimozione di una VM esistente e la relativa sostituzione con una nuova.</span><span class="sxs-lookup"><span data-stu-id="84118-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="84118-109">Quando si aumentano o riducono le dimensioni delle macchine virtuali in un set di scalabilità di macchine virtuali, in alcuni casi può rendersi necessario ridimensionare le VM esistenti e mantenere i dati, mentre in altri casi è necessario distribuire nuove VM con le nuove dimensioni.</span><span class="sxs-lookup"><span data-stu-id="84118-109">When you increase or decrease the size of VMs in a VM Scale Set, in some cases you want to resize existing VMs and retain your data, while in other cases you need to deploy new VMs of the new size.</span></span> <span data-ttu-id="84118-110">Questo documento illustra entrambi i casi.</span><span class="sxs-lookup"><span data-stu-id="84118-110">This document covers both cases.</span></span>

<span data-ttu-id="84118-111">Il ridimensionamento verticale, ovvero l'aumento o la riduzione delle prestazioni, può risultare utile quando:</span><span class="sxs-lookup"><span data-stu-id="84118-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="84118-112">Un servizio basato su macchine virtuali è sottoutilizzato, ad esempio nel fine settimana.</span><span class="sxs-lookup"><span data-stu-id="84118-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="84118-113">La riduzione delle dimensioni delle VM può ridurre i costi mensili.</span><span class="sxs-lookup"><span data-stu-id="84118-113">Reducing the VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="84118-114">L'aumento delle dimensioni delle VM consente di soddisfare una maggiore richiesta senza creare altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="84118-114">Increasing VM size to cope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="84118-115">È possibile configurare l'attivazione del ridimensionamento verticale secondo le metriche basate sugli avvisi del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="84118-115">You can set up vertical scaling to be triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="84118-116">Quando viene attivato l'avviso, genera un webhook che attiva un runbook in grado di aumentare o ridurre le prestazioni del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="84118-116">When the alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="84118-117">Il ridimensionamento verticale può essere configurato seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="84118-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="84118-118">Creare un account di Automazione di Azure con funzionalità RunAs.</span><span class="sxs-lookup"><span data-stu-id="84118-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="84118-119">Importare i runbook di scalabilità verticale di Automazione di Azure per i set di scalabilità di macchine virtuali nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="84118-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="84118-120">Aggiungere un webhook al runbook.</span><span class="sxs-lookup"><span data-stu-id="84118-120">Add a webhook to your runbook.</span></span>
4. <span data-ttu-id="84118-121">Aggiungere un avviso per il set di scalabilità di macchine virtuali con una notifica di un webhook.</span><span class="sxs-lookup"><span data-stu-id="84118-121">Add an alert to your VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="84118-122">Il ridimensionamento verticale può avvenire solo entro determinati intervalli di dimensioni delle VM.</span><span class="sxs-lookup"><span data-stu-id="84118-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="84118-123">Confrontare le specifiche di ogni dimensione prima di decidere il tipo di ridimensionamento (un numero più alto non sempre indica dimensioni della VM più grandi).</span><span class="sxs-lookup"><span data-stu-id="84118-123">Compare the specifications of each size before deciding to scale from one to another (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="84118-124">È possibile scegliere di applicare il ridimensionamento tra le seguenti coppie di dimensioni:</span><span class="sxs-lookup"><span data-stu-id="84118-124">You can choose to scale between the following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="84118-125">coppie di ridimensionamento di dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="84118-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="84118-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="84118-126">Standard_A0</span></span> |<span data-ttu-id="84118-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="84118-127">Standard_A11</span></span> |
> | <span data-ttu-id="84118-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="84118-128">Standard_D1</span></span> |<span data-ttu-id="84118-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="84118-129">Standard_D14</span></span> |
> | <span data-ttu-id="84118-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="84118-130">Standard_DS1</span></span> |<span data-ttu-id="84118-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="84118-131">Standard_DS14</span></span> |
> | <span data-ttu-id="84118-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="84118-132">Standard_D1v2</span></span> |<span data-ttu-id="84118-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="84118-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="84118-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="84118-134">Standard_G1</span></span> |<span data-ttu-id="84118-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="84118-135">Standard_G5</span></span> |
> | <span data-ttu-id="84118-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="84118-136">Standard_GS1</span></span> |<span data-ttu-id="84118-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="84118-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="84118-138">Creare un account di Automazione di Azure con funzionalità RunAs</span><span class="sxs-lookup"><span data-stu-id="84118-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="84118-139">La prima operazione da eseguire è creare l'account di Automazione di Azure che ospiterà i runbook usati per ridimensionare le istanze del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="84118-139">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span></span> <span data-ttu-id="84118-140">[Automazione di Azure](https://azure.microsoft.com/services/automation/) ha introdotto di recente la funzionalità "Account RunAs", che semplifica molto la configurazione dell'entità servizio per l'esecuzione automatica di runbook per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="84118-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="84118-141">Altre informazioni sono disponibili nell'articolo seguente.</span><span class="sxs-lookup"><span data-stu-id="84118-141">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="84118-142">Autenticare runbook con account RunAs di Azure</span><span class="sxs-lookup"><span data-stu-id="84118-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="84118-143">Importare i runbook di ridimensionamento verticale di Automazione di Azure nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="84118-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="84118-144">I runbook necessari per il ridimensionamento verticale del set di scalabilità di macchine virtuali sono già stati pubblicati nella raccolta dei runbook di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="84118-144">The runbooks needed to vertically scale your VM Scale Sets are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="84118-145">Per importarli nella sottoscrizione seguire la procedura descritta in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="84118-145">To import them into your subscription follow the steps in this article:</span></span>

* [<span data-ttu-id="84118-146">Raccolte di runbook e moduli per l'automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="84118-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="84118-147">Scegliere l'opzione Esplora raccolta dal menu Runbook:</span><span class="sxs-lookup"><span data-stu-id="84118-147">Choose the Browse Gallery option from the Runbooks menu:</span></span>

![Runbook da importare][runbooks]

<span data-ttu-id="84118-149">I runbook da importare sono visualizzati nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="84118-149">The runbooks that need to be imported are shown.</span></span> <span data-ttu-id="84118-150">Selezionare il runbook in base al tipo di ridimensionamento con o senza un nuovo provisioning che si vuole usare:</span><span class="sxs-lookup"><span data-stu-id="84118-150">Select the runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Raccolta di runbook][gallery]

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="84118-152">Aggiungere un webhook al runbook</span><span class="sxs-lookup"><span data-stu-id="84118-152">Add a webhook to your runbook</span></span>
<span data-ttu-id="84118-153">Dopo avere importato i runbook, è necessario aggiungere un webhook al runbook in modo che possa essere attivato da un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="84118-153">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="84118-154">Informazioni dettagliate sulla creazione di un webhook per il runbook sono disponibili in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="84118-154">The details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="84118-155">Webhook di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="84118-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="84118-156">Assicurarsi di copiare l'URI del webhook prima di chiudere la finestra di dialogo del webhook, perché sarà necessario nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="84118-156">Make sure you copy the webhook URI before closing the webhook dialog as you will need this in the next section.</span></span>
> 
> 

## <a name="add-an-alert-to-your-vm-scale-set"></a><span data-ttu-id="84118-157">Aggiungere un avviso al set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="84118-157">Add an alert to your VM Scale Set</span></span>
<span data-ttu-id="84118-158">Di seguito è riportato uno script di PowerShell che mostra come aggiungere un avviso a un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="84118-158">Below is a PowerShell script which shows how to add an alert to a VM Scale Set.</span></span> <span data-ttu-id="84118-159">Vedere l'articolo seguente per ottenere il nome della metrica in base alla quale attivare l'avviso: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) (Metriche comuni per il ridimensionamento automatico di Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="84118-159">Refer to the following article to get the name of the metric to fire the alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

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
> <span data-ttu-id="84118-160">È consigliabile configurare un intervallo di tempo ragionevole per l'avviso per evitare di attivare troppo spesso il ridimensionamento verticale e l'eventuale interruzione del servizio associato.</span><span class="sxs-lookup"><span data-stu-id="84118-160">It is recommended to configure a reasonable time window for the alert in order to avoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="84118-161">Considerare un intervallo minimo di 20-30 minuti.</span><span class="sxs-lookup"><span data-stu-id="84118-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="84118-162">Prendere in considerazione il ridimensionamento orizzontale se è necessario evitare qualsiasi interruzione.</span><span class="sxs-lookup"><span data-stu-id="84118-162">Consider horizontal scaling if you need to avoid any interruption.</span></span>
> 
> 

<span data-ttu-id="84118-163">Per altre informazioni su come creare gli avvisi, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="84118-163">For more information on how to create alerts refer to the following articles:</span></span>

* <span data-ttu-id="84118-164">[Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure)</span><span class="sxs-lookup"><span data-stu-id="84118-164">[Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="84118-165">[Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md) (Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma per Monitoraggio di Azure)</span><span class="sxs-lookup"><span data-stu-id="84118-165">[Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>

## <a name="summary"></a><span data-ttu-id="84118-166">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="84118-166">Summary</span></span>
<span data-ttu-id="84118-167">Questo articolo ha illustrato semplici esempi di ridimensionamento verticale.</span><span class="sxs-lookup"><span data-stu-id="84118-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="84118-168">Con questi blocchi predefiniti, ovvero account di automazione, runbook, webhook e avvisi, è possibile connettere una vasta gamma di eventi con un set di azioni personalizzato.</span><span class="sxs-lookup"><span data-stu-id="84118-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
