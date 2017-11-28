---
title: gli avvisi aaaCreate per servizi di Azure - CLI multipiattaforma | Documenti Microsoft
description: Attivare l'automazione, notifiche, gli URL di siti Web di chiamata (webhook) o messaggi di posta elettronica quando vengono soddisfatte le condizioni di hello specificate.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="8f0a4-103">Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure - Interfaccia della riga di comando multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="8f0a4-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f0a4-104">Portale</span><span class="sxs-lookup"><span data-stu-id="8f0a4-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="8f0a4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f0a4-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="8f0a4-106">CLI</span><span class="sxs-lookup"><span data-stu-id="8f0a4-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="8f0a4-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8f0a4-107">Overview</span></span>
<span data-ttu-id="8f0a4-108">Questo articolo illustra come tooset di Azure avvisi metrica utilizzando hello multipiattaforma interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="8f0a4-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="8f0a4-109">Monitoraggio di Azure è hello nuovo nome per ciò che è stato chiamato "Azure Insights" fino a 25 settembre 2016.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="8f0a4-110">Tuttavia, gli spazi dei nomi hello e pertanto comandi hello seguenti comunque contengono approfondite"hello".</span><span class="sxs-lookup"><span data-stu-id="8f0a4-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="8f0a4-111">È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="8f0a4-112">**Valori della metrica** : hello trigger un avviso quando il valore di hello di una specifica metrica supera una soglia è assegnare in entrambe le direzioni.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="8f0a4-113">Ovvero, entrambi attiva quando hello prima condizione e quindi successivamente non condizione when che è non è più in grado di soddisfare.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="8f0a4-114">**Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="8f0a4-115">ulteriori informazioni sugli avvisi di log attività toolearn [fare clic qui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="8f0a4-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="8f0a4-116">È possibile configurare una metrica toodo avviso hello seguenti attiva:</span><span class="sxs-lookup"><span data-stu-id="8f0a4-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="8f0a4-117">inviare coamministratore e amministratore del servizio toohello le notifiche tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="8f0a4-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="8f0a4-118">Invia messaggio di posta elettronica tooadditional messaggi di posta elettronica specificato.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="8f0a4-119">chiamare un webhook</span><span class="sxs-lookup"><span data-stu-id="8f0a4-119">call a webhook</span></span>
* <span data-ttu-id="8f0a4-120">avviare l'esecuzione di un runbook di Azure (solo dal portale di Azure in questo momento hello)</span><span class="sxs-lookup"><span data-stu-id="8f0a4-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="8f0a4-121">È possibile configurare e ottenere informazioni sulle regole degli avvisi sulle metriche tramite</span><span class="sxs-lookup"><span data-stu-id="8f0a4-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="8f0a4-122">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8f0a4-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="8f0a4-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f0a4-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="8f0a4-124">interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="8f0a4-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="8f0a4-125">API REST di Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="8f0a4-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="8f0a4-126">Si può sempre ricevere Guida per i comandi, digitare un comando e la messa - Guida alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="8f0a4-127">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8f0a4-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="8f0a4-128">Creare regole di avviso utilizzando hello CLI</span><span class="sxs-lookup"><span data-stu-id="8f0a4-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="8f0a4-129">Eseguire prerequisiti hello e tooAzure account di accesso.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="8f0a4-130">Vedere gli [esempi dell'interfaccia della riga di comando di Monitoraggio di Azure](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8f0a4-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="8f0a4-131">In breve, hello CLI di installare ed eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="8f0a4-132">E ottenere l'accesso, mostra quale sottoscrizione utilizza e preparazione toorun i comandi di monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="8f0a4-133">le regole esistenti toolist in un gruppo di risorse, utilizzare hello seguente modulo **azure insights elenco di regole avvisi** *[opzioni] &lt;gruppo di risorse&gt;*</span><span class="sxs-lookup"><span data-stu-id="8f0a4-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="8f0a4-134">toocreate una regola, è necessario toohave importanti di varie informazioni prima di tutto.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="8f0a4-135">Hello **ID risorsa** per la risorsa hello desiderato tooset un avviso per</span><span class="sxs-lookup"><span data-stu-id="8f0a4-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="8f0a4-136">Hello **le definizioni delle metriche** disponibili per tale risorsa</span><span class="sxs-lookup"><span data-stu-id="8f0a4-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="8f0a4-137">Un modo tooget hello ID risorsa è toouse hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="8f0a4-138">Supponendo che la risorsa hello è già stata creata, selezionarlo nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="8f0a4-139">Selezionare nel pannello successivo hello *proprietà* in hello *impostazioni* sezione.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="8f0a4-140">Hello *ID risorsa* è un campo nel pannello successivo hello.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="8f0a4-141">Un altro modo consiste hello toouse [Esplora inventario risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8f0a4-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="8f0a4-142">Un esempio di ID risorsa per un'app Web è</span><span class="sxs-lookup"><span data-stu-id="8f0a4-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="8f0a4-143">tooget un elenco delle metriche disponibili hello e unità per le metriche per hello precedente esempio di risorse, hello di utilizzare il comando CLI seguente:</span><span class="sxs-lookup"><span data-stu-id="8f0a4-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="8f0a4-144">*PT1M* è hello granularità di misura disponibili hello (intervalli di 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="8f0a4-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="8f0a4-145">L'uso di granularità diverse offre opzioni di metrica diverse.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="8f0a4-146">toocreate una regola di avviso basata su metrica, utilizzare un comando di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="8f0a4-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="8f0a4-147">**azure insights alerts rule metric set** *[opzioni] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="8f0a4-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="8f0a4-148">Hello nel seguente esempio impostare un avviso su una risorsa di sito web.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="8f0a4-149">trigger avviso Hello ogni volta che riceve il traffico in modo coerente per 5 minuti e nuovamente quando non riceve alcun traffico per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="8f0a4-150">toocreate webhook o Invia messaggio di posta elettronica quando viene generato un avviso di metrica, creare innanzitutto la posta elettronica hello e/o webhook.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="8f0a4-151">Quindi creare immediatamente regola hello in seguito.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="8f0a4-152">Non è possibile associare webhook o messaggi di posta elettronica con già creato le regole utilizzando hello CLI.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="8f0a4-153">È possibile verificare che gli avvisi siano stati creati correttamente esaminando una singola regola.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="8f0a4-154">toodelete regole, utilizzare un comando del modulo hello:</span><span class="sxs-lookup"><span data-stu-id="8f0a4-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="8f0a4-155">**insights alerts rule delete** [opzioni] &lt;resourceGroup&gt;&lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="8f0a4-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="8f0a4-156">Questi comandi eliminano regole hello create in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="8f0a4-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f0a4-157">Next steps</span></span>
* <span data-ttu-id="8f0a4-158">[Panoramica di Azure monitoring](monitoring-overview.md) inclusi i tipi di informazioni è possibile raccogliere e monitorare hello.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="8f0a4-159">Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8f0a4-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="8f0a4-160">Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8f0a4-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="8f0a4-161">Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="8f0a4-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="8f0a4-162">Ottenere un [Panoramica di raccogliere i log di diagnostica](monitoring-overview-of-diagnostic-logs.md) toocollect dettagliate ad alta frequenza metriche sul servizio.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="8f0a4-163">Ottenere un [Panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.</span><span class="sxs-lookup"><span data-stu-id="8f0a4-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
