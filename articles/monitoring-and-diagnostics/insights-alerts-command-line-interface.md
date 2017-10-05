---
title: Creare avvisi per i servizi di Azure - Interfaccia della riga di comando multipiattaforma | Microsoft Docs
description: Attivare messaggi di posta elettronica o notifiche, chiamare URL di siti Web (webhook) o usare l'automazione quando vengono soddisfatte le condizioni specificate.
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
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="8010e-103">Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure - Interfaccia della riga di comando multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="8010e-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8010e-104">Portale</span><span class="sxs-lookup"><span data-stu-id="8010e-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="8010e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8010e-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="8010e-106">CLI</span><span class="sxs-lookup"><span data-stu-id="8010e-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="8010e-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8010e-107">Overview</span></span>
<span data-ttu-id="8010e-108">Questo articolo descrive come impostare gli avvisi sulle metriche di Azure tramite l'interfaccia della riga di comando multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="8010e-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="8010e-109">Dal 25 settembre 2016 Monitoraggio di Azure è il nuovo nome di "Azure Insights".</span><span class="sxs-lookup"><span data-stu-id="8010e-109">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="8010e-110">Tuttavia, gli spazi dei nomi e quindi i comandi seguenti contengono ancora il termine "insights".</span><span class="sxs-lookup"><span data-stu-id="8010e-110">However, the namespaces and thus the commands below still contain the "insights".</span></span>
>
>

<span data-ttu-id="8010e-111">È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.</span><span class="sxs-lookup"><span data-stu-id="8010e-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="8010e-112">**Valori metrici** : l'avviso si attiva quando il valore di una specifica metrica supera una soglia assegnata per eccesso o difetto.</span><span class="sxs-lookup"><span data-stu-id="8010e-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="8010e-113">Vale a dire che si attiva sia quando la condizione viene inizialmente soddisfatta e successivamente quando tale condizione non è più soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="8010e-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="8010e-114">**Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento.</span><span class="sxs-lookup"><span data-stu-id="8010e-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="8010e-115">Per altre informazioni sugli avvisi sui log attività [fare clic qui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="8010e-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="8010e-116">È possibile configurare un avviso sulle metriche affinché esegua queste operazioni al momento dell'attivazione:</span><span class="sxs-lookup"><span data-stu-id="8010e-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="8010e-117">inviare un messaggio di posta elettronica all'amministratore e ai coamministratori del servizio</span><span class="sxs-lookup"><span data-stu-id="8010e-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="8010e-118">inviare un messaggio di posta elettronica ad altri indirizzi specificati</span><span class="sxs-lookup"><span data-stu-id="8010e-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="8010e-119">chiamare un webhook</span><span class="sxs-lookup"><span data-stu-id="8010e-119">call a webhook</span></span>
* <span data-ttu-id="8010e-120">avviare l'esecuzione di un runbook di Azure; attualmente è possibile solo dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8010e-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="8010e-121">È possibile configurare e ottenere informazioni sulle regole degli avvisi sulle metriche tramite</span><span class="sxs-lookup"><span data-stu-id="8010e-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="8010e-122">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8010e-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="8010e-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8010e-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="8010e-124">interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="8010e-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="8010e-125">API REST di Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="8010e-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="8010e-126">È possibile ricevere assistenza per i comandi digitando un comando e inserendo -help al termine.</span><span class="sxs-lookup"><span data-stu-id="8010e-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="8010e-127">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8010e-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="8010e-128">Creare le regole di avviso tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="8010e-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="8010e-129">Controllare i prerequisiti e accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="8010e-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="8010e-130">Vedere gli [esempi dell'interfaccia della riga di comando di Monitoraggio di Azure](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8010e-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="8010e-131">In breve, installare l'interfaccia della riga di comando ed eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="8010e-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="8010e-132">Questi comandi eseguono l'accesso, indicano la sottoscrizione in uso e preparano l'esecuzione dei comandi di Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="8010e-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="8010e-133">Per elencare le regole esistenti in un gruppo di risorse, usare il seguente formato **azure insights alerts rule list** *[opzioni] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="8010e-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="8010e-134">Per creare una regola, per prima cosa è necessario disporre di alcune informazioni importanti.</span><span class="sxs-lookup"><span data-stu-id="8010e-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="8010e-135">L' **ID risorsa** della risorsa per la quale si intende impostare un avviso</span><span class="sxs-lookup"><span data-stu-id="8010e-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="8010e-136">Le **definizioni delle metriche** disponibili per tale risorsa</span><span class="sxs-lookup"><span data-stu-id="8010e-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="8010e-137">È possibile ottenere l'ID della risorsa tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8010e-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="8010e-138">Se la risorsa è già stata creata, selezionarla nel portale.</span><span class="sxs-lookup"><span data-stu-id="8010e-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="8010e-139">Nel pannello successivo, nella sezione *Impostazioni*, selezionare *Proprietà*.</span><span class="sxs-lookup"><span data-stu-id="8010e-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="8010e-140">*ID RISORSA* è un campo nel pannello successivo.</span><span class="sxs-lookup"><span data-stu-id="8010e-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="8010e-141">È anche possibile usare [Esplora risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8010e-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="8010e-142">Un esempio di ID risorsa per un'app Web è</span><span class="sxs-lookup"><span data-stu-id="8010e-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="8010e-143">Per ottenere un elenco delle metriche e delle unità per le metriche disponibili per l'esempio precedente di risorse, usare il comando dell'interfaccia della riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8010e-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="8010e-144">*PT1M* indica la granularità della misurazione disponibile, con intervalli di 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="8010e-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="8010e-145">L'uso di granularità diverse offre opzioni di metrica diverse.</span><span class="sxs-lookup"><span data-stu-id="8010e-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="8010e-146">Per creare una regola di avviso basata sulla metrica, usare un comando nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="8010e-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="8010e-147">**azure insights alerts rule metric set** *[opzioni] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="8010e-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="8010e-148">L'esempio seguente imposta un avviso relativo a una risorsa del sito Web.</span><span class="sxs-lookup"><span data-stu-id="8010e-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="8010e-149">L'avviso viene attivato ogni volta che si riceve il traffico costantemente per 5 minuti e di nuovo quando non si riceve traffico per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="8010e-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="8010e-150">Per creare il webhook o inviare un messaggio di posta elettronica all'attivazione di un avviso di metrica, creare prima il messaggio di posta elettronica e/o i webhook.</span><span class="sxs-lookup"><span data-stu-id="8010e-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="8010e-151">Creare la regola immediatamente dopo.</span><span class="sxs-lookup"><span data-stu-id="8010e-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="8010e-152">Non è possibile associare il webhook o messaggi di posta elettronica a regole già create tramite l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8010e-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="8010e-153">È possibile verificare che gli avvisi siano stati creati correttamente esaminando una singola regola.</span><span class="sxs-lookup"><span data-stu-id="8010e-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="8010e-154">Per eliminare le regole, usare un comando nel formato:</span><span class="sxs-lookup"><span data-stu-id="8010e-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="8010e-155">**insights alerts rule delete** [opzioni] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="8010e-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="8010e-156">Questi comandi eliminano le regole create in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8010e-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="8010e-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8010e-157">Next steps</span></span>
* <span data-ttu-id="8010e-158">[Leggere una panoramica del monitoraggio di Azure](monitoring-overview.md) che include anche i tipi di informazioni che è possibile raccogliere e monitorare.</span><span class="sxs-lookup"><span data-stu-id="8010e-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="8010e-159">Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8010e-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="8010e-160">Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8010e-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="8010e-161">Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="8010e-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="8010e-162">Leggere una [panoramica della raccolta dei log di diagnostica](monitoring-overview-of-diagnostic-logs.md) per raccogliere metriche dettagliate e ad alta frequenza sul servizio.</span><span class="sxs-lookup"><span data-stu-id="8010e-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="8010e-163">Leggere una [panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) per verificare che il servizio sia disponibile e reattivo.</span><span class="sxs-lookup"><span data-stu-id="8010e-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
