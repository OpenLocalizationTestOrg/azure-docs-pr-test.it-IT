---
title: Creare avvisi per i servizi di Azure - PowerShell | Microsoft Docs
description: Attivare messaggi di posta elettronica o notifiche, chiamare URL di siti Web (webhook) o usare l'automazione quando vengono soddisfatte le condizioni specificate.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 50127242cdf156771d0610e58cf2fc41281adae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="5b8a7-103">Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure: PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b8a7-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b8a7-104">Portale</span><span class="sxs-lookup"><span data-stu-id="5b8a7-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="5b8a7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b8a7-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="5b8a7-106">CLI</span><span class="sxs-lookup"><span data-stu-id="5b8a7-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="5b8a7-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5b8a7-107">Overview</span></span>
<span data-ttu-id="5b8a7-108">Questo articolo descrive come impostare gli avvisi sulle metriche tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-108">This article shows you how to set up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="5b8a7-109">È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="5b8a7-110">**Valori metrici** : l'avviso si attiva quando il valore di una specifica metrica supera una soglia assegnata per eccesso o difetto.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="5b8a7-111">Vale a dire che si attiva sia quando la condizione viene inizialmente soddisfatta e successivamente quando tale condizione non è più soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="5b8a7-112">**Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="5b8a7-113">Per altre informazioni sugli avvisi sui log attività [fare clic qui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="5b8a7-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="5b8a7-114">È possibile configurare un avviso sulle metriche affinché esegua queste operazioni al momento dell'attivazione:</span><span class="sxs-lookup"><span data-stu-id="5b8a7-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="5b8a7-115">inviare un messaggio di posta elettronica all'amministratore e ai coamministratori del servizio</span><span class="sxs-lookup"><span data-stu-id="5b8a7-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="5b8a7-116">inviare un messaggio di posta elettronica ad altri indirizzi specificati</span><span class="sxs-lookup"><span data-stu-id="5b8a7-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="5b8a7-117">chiamare un webhook</span><span class="sxs-lookup"><span data-stu-id="5b8a7-117">call a webhook</span></span>
* <span data-ttu-id="5b8a7-118">avviare l'esecuzione di un runbook di Azure (solo dal portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="5b8a7-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="5b8a7-119">È possibile configurare e ottenere informazioni sulle regole degli avvisi tramite</span><span class="sxs-lookup"><span data-stu-id="5b8a7-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="5b8a7-120">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5b8a7-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="5b8a7-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b8a7-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="5b8a7-122">interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="5b8a7-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="5b8a7-123">API REST di Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="5b8a7-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="5b8a7-124">Per altre informazioni è sempre possibile digitare ```Get-Help``` e quindi il comando di PowerShell da approfondire.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-124">For additional information, you can always type ```Get-Help``` and then the PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="5b8a7-125">Creare regole di avviso in PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b8a7-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="5b8a7-126">Accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-126">Log in to Azure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="5b8a7-127">Visualizzare l'elenco delle sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-127">Get a list of the subscriptions you have available.</span></span> <span data-ttu-id="5b8a7-128">Assicurarsi di lavorare con la giusta sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-128">Verify that you are working with the right subscription.</span></span> <span data-ttu-id="5b8a7-129">In caso contrario, impostare la sottoscrizione giusta usando l'output di `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-129">If not, set it to the right one using the output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="5b8a7-130">Per elencare le regole esistenti in un gruppo di risorse, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b8a7-130">To list existing rules on a resource group, use the following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="5b8a7-131">Per creare una regola, per prima cosa è necessario disporre di alcune informazioni importanti.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-131">To create a rule, you need to have several important pieces of information first.</span></span>

  * <span data-ttu-id="5b8a7-132">L' **ID risorsa** della risorsa per la quale si intende impostare un avviso</span><span class="sxs-lookup"><span data-stu-id="5b8a7-132">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="5b8a7-133">Le **definizioni delle metriche** disponibili per tale risorsa</span><span class="sxs-lookup"><span data-stu-id="5b8a7-133">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="5b8a7-134">È possibile ottenere l'ID della risorsa tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-134">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="5b8a7-135">Se la risorsa è già stata creata, selezionarla nel portale.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-135">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="5b8a7-136">Nel pannello successivo, nella sezione *Impostazioni*, selezionare *Proprietà*.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-136">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="5b8a7-137">**ID RISORSA** è un campo del pannello successivo.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-137">**RESOURCE ID** is a field in the next blade.</span></span> <span data-ttu-id="5b8a7-138">È anche possibile usare [Esplora risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5b8a7-138">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="5b8a7-139">Un esempio di ID risorsa per un'app web è</span><span class="sxs-lookup"><span data-stu-id="5b8a7-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="5b8a7-140">Usare `Get-AzureRmMetricDefinition` per visualizzare l'elenco di tutte le definizioni delle metriche per una specifica risorsa.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-140">You can use `Get-AzureRmMetricDefinition` to view the list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="5b8a7-141">L'esempio seguente genera una tabella con la metrica Name e il relativo valore Unit.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-141">The following example generates a table with the metric Name and the Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="5b8a7-142">Un elenco completo delle opzioni disponibili per Get-AzureRmMetricDefinition è visualizzabile eseguendo Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="5b8a7-143">L'esempio seguente imposta un avviso relativo a una risorsa del sito Web.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-143">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="5b8a7-144">L'avviso viene attivato ogni volta che si riceve il traffico costantemente per 5 minuti e di nuovo quando non si riceve traffico per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-144">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="5b8a7-145">Per creare il webhook o inviare un messaggio di posta elettronica quando viene attivato l'avviso, creare prima il messaggio di posta elettronica e/o i webhook.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-145">To create webhook or send email when an alert triggers, first create the email and/or webhooks.</span></span> <span data-ttu-id="5b8a7-146">Subito dopo creare la regola con il tag -Actions, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-146">Then immediately create the rule afterwards with the -Actions tag and as shown in the following example.</span></span> <span data-ttu-id="5b8a7-147">Non è possibile associare webhook o messaggi di posta elettronica a regole già create tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="5b8a7-148">Verificare che gli avvisi siano stati creati correttamente esaminando le singole regole.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-148">To verify that your alerts have been created properly by looking at the individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="5b8a7-149">Eliminare gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-149">Delete your alerts.</span></span> <span data-ttu-id="5b8a7-150">Questi comandi eliminano le regole create in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-150">These commands delete the rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="5b8a7-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b8a7-151">Next steps</span></span>
* <span data-ttu-id="5b8a7-152">[Leggere una panoramica del monitoraggio di Azure](monitoring-overview.md) che include anche i tipi di informazioni che è possibile raccogliere e monitorare.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-152">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="5b8a7-153">Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="5b8a7-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="5b8a7-154">Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="5b8a7-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="5b8a7-155">Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="5b8a7-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="5b8a7-156">Leggere una [panoramica della raccolta dei log di diagnostica](monitoring-overview-of-diagnostic-logs.md) per raccogliere metriche dettagliate e ad alta frequenza sul servizio.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="5b8a7-157">Leggere una [panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) per verificare che il servizio sia disponibile e reattivo.</span><span class="sxs-lookup"><span data-stu-id="5b8a7-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
