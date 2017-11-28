---
title: gli avvisi aaaCreate per servizi di Azure - PowerShell | Documenti Microsoft
description: Attivare l'automazione, notifiche, gli URL di siti Web di chiamata (webhook) o messaggi di posta elettronica quando vengono soddisfatte le condizioni di hello specificate.
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
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="45014-103">Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure: PowerShell</span><span class="sxs-lookup"><span data-stu-id="45014-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45014-104">Portale</span><span class="sxs-lookup"><span data-stu-id="45014-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="45014-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45014-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="45014-106">CLI</span><span class="sxs-lookup"><span data-stu-id="45014-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="45014-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="45014-107">Overview</span></span>
<span data-ttu-id="45014-108">Questo articolo illustra come tooset backup Azure metrica avvisi tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45014-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="45014-109">È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.</span><span class="sxs-lookup"><span data-stu-id="45014-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="45014-110">**Valori della metrica** : hello trigger un avviso quando il valore di hello di una specifica metrica supera una soglia è assegnare in entrambe le direzioni.</span><span class="sxs-lookup"><span data-stu-id="45014-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="45014-111">Ovvero, entrambi attiva quando hello prima condizione e quindi successivamente non condizione when che è non è più in grado di soddisfare.</span><span class="sxs-lookup"><span data-stu-id="45014-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="45014-112">**Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento.</span><span class="sxs-lookup"><span data-stu-id="45014-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="45014-113">ulteriori informazioni sugli avvisi di log attività toolearn [fare clic qui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="45014-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="45014-114">È possibile configurare una metrica toodo avviso hello seguenti attiva:</span><span class="sxs-lookup"><span data-stu-id="45014-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="45014-115">inviare coamministratore e amministratore del servizio toohello le notifiche tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="45014-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="45014-116">Invia messaggio di posta elettronica tooadditional messaggi di posta elettronica specificato.</span><span class="sxs-lookup"><span data-stu-id="45014-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="45014-117">chiamare un webhook</span><span class="sxs-lookup"><span data-stu-id="45014-117">call a webhook</span></span>
* <span data-ttu-id="45014-118">avviare l'esecuzione di un runbook di Azure (solo da hello portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="45014-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="45014-119">È possibile configurare e ottenere informazioni sulle regole degli avvisi tramite</span><span class="sxs-lookup"><span data-stu-id="45014-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="45014-120">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="45014-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="45014-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45014-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="45014-122">interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="45014-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="45014-123">API REST di Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="45014-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="45014-124">Per ulteriori informazioni, è possibile digitare sempre ```Get-Help``` e quindi hello si vogliono informazioni sul comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45014-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="45014-125">Creare regole di avviso in PowerShell</span><span class="sxs-lookup"><span data-stu-id="45014-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="45014-126">Accedi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="45014-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="45014-127">Ottenere un elenco di sottoscrizioni hello disponibile.</span><span class="sxs-lookup"><span data-stu-id="45014-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="45014-128">Verificare che si lavora con sottoscrizione destra hello.</span><span class="sxs-lookup"><span data-stu-id="45014-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="45014-129">In caso contrario, impostarla toohello destra di un utilizzo di output di hello da `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="45014-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="45014-130">le regole esistenti toolist in un gruppo di risorse, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="45014-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="45014-131">toocreate una regola, è necessario toohave importanti di varie informazioni prima di tutto.</span><span class="sxs-lookup"><span data-stu-id="45014-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="45014-132">Hello **ID risorsa** per la risorsa hello desiderato tooset un avviso per</span><span class="sxs-lookup"><span data-stu-id="45014-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="45014-133">Hello **le definizioni delle metriche** disponibili per tale risorsa</span><span class="sxs-lookup"><span data-stu-id="45014-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="45014-134">Un modo tooget hello ID risorsa è toouse hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="45014-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="45014-135">Supponendo che la risorsa hello è già stata creata, selezionarlo nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="45014-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="45014-136">Selezionare nel pannello successivo hello *proprietà* in hello *impostazioni* sezione.</span><span class="sxs-lookup"><span data-stu-id="45014-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="45014-137">**ID di risorsa** è un campo nel pannello successivo hello.</span><span class="sxs-lookup"><span data-stu-id="45014-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="45014-138">Un altro modo consiste hello toouse [Esplora inventario risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="45014-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="45014-139">Un esempio di ID risorsa per un'app web è</span><span class="sxs-lookup"><span data-stu-id="45014-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="45014-140">È possibile utilizzare `Get-AzureRmMetricDefinition` elenco hello tooview di tutte le definizioni di metrica per una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="45014-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="45014-141">Hello esempio seguente genera una tabella con nome metrica di hello e hello unità per tale metrica.</span><span class="sxs-lookup"><span data-stu-id="45014-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="45014-142">Un elenco completo delle opzioni disponibili per Get-AzureRmMetricDefinition è visualizzabile eseguendo Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="45014-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="45014-143">Hello nel seguente esempio impostare un avviso su una risorsa di sito web.</span><span class="sxs-lookup"><span data-stu-id="45014-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="45014-144">trigger avviso Hello ogni volta che riceve il traffico in modo coerente per 5 minuti e nuovamente quando non riceve alcun traffico per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="45014-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="45014-145">toocreate webhook o Invia messaggio di posta elettronica quando viene generato un avviso, creare innanzitutto la posta elettronica hello e/o webhook.</span><span class="sxs-lookup"><span data-stu-id="45014-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="45014-146">Quindi creare immediatamente regola hello in seguito con hello - tag azioni e, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="45014-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="45014-147">Non è possibile associare webhook o messaggi di posta elettronica a regole già create tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45014-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="45014-148">tooverify che gli avvisi siano stati creati correttamente esaminando le singole regole hello.</span><span class="sxs-lookup"><span data-stu-id="45014-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="45014-149">Eliminare gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="45014-149">Delete your alerts.</span></span> <span data-ttu-id="45014-150">Questi comandi eliminano regole hello create in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="45014-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="45014-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45014-151">Next steps</span></span>
* <span data-ttu-id="45014-152">[Panoramica di Azure monitoring](monitoring-overview.md) inclusi i tipi di informazioni è possibile raccogliere e monitorare hello.</span><span class="sxs-lookup"><span data-stu-id="45014-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="45014-153">Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="45014-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="45014-154">Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="45014-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="45014-155">Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="45014-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="45014-156">Ottenere un [Panoramica di raccogliere i log di diagnostica](monitoring-overview-of-diagnostic-logs.md) toocollect dettagliate ad alta frequenza metriche sul servizio.</span><span class="sxs-lookup"><span data-stu-id="45014-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="45014-157">Ottenere un [Panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.</span><span class="sxs-lookup"><span data-stu-id="45014-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
