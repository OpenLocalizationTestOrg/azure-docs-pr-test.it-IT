---
title: Monitorare operazioni, eventi e contatori per Azure Load Balancer | Documentazione Microsoft
description: "Informazioni su come abilitare gli eventi di avviso e la registrazione dello stato di integrità del probe per il servizio di bilanciamento del carico di Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="583ff-103">Analisi dei log per il servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="583ff-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="583ff-104">In Azure è possibile usare diversi tipi di log per gestire e risolvere i problemi dei bilanciamenti del carico.</span><span class="sxs-lookup"><span data-stu-id="583ff-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="583ff-105">Alcuni di questi log sono accessibili tramite il portale</span><span class="sxs-lookup"><span data-stu-id="583ff-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="583ff-106">Tutti i log possono essere estratti da Archiviazione BLOB di Azure e visualizzati in strumenti differenti, ad esempio Excel e PowerBI.</span><span class="sxs-lookup"><span data-stu-id="583ff-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="583ff-107">L'elenco seguente contiene altre informazioni sui diversi tipi di log.</span><span class="sxs-lookup"><span data-stu-id="583ff-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="583ff-108">**Log di controllo:** è possibile usare i [log di controllo di Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (noti in precedenza come log operativi) per visualizzare tutte le operazioni da inviare alle sottoscrizioni di Azure e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="583ff-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="583ff-109">I log di controllo sono abilitati per impostazione predefinita e possono essere visualizzati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="583ff-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="583ff-110">**Log eventi di avviso:** è possibile usare questo log per visualizzare gli avvisi generati per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="583ff-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="583ff-111">Le informazioni di stato per il bilanciamento del carico vengono raccolte ogni cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="583ff-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="583ff-112">Questo log viene scritto solo se viene generato un evento di avviso del bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="583ff-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="583ff-113">**Log del probe di integrità:** è possibile usare questo registro per visualizzare i problemi rilevati dal probe di integrità, ad esempio il numero di istanze del pool di back-end che non stanno ricevendo richieste dal servizio di bilanciamento del carico a causa di problemi del probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="583ff-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="583ff-114">Questo log viene scritto quando si apporta una modifica nello stato del probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="583ff-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="583ff-115">Attualmente l'analisi di log funziona solo per i servizi di bilanciamento del carico con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="583ff-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="583ff-116">I log sono disponibili solo per le risorse distribuite nel modello di distribuzione di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="583ff-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="583ff-117">Non è possibile usare i log per le risorse nel modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="583ff-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="583ff-118">Per altre informazioni su questi modelli di distribuzione, vedere l'articolo relativo alle [informazioni sulla distribuzione di Gestione risorse e sulla distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="583ff-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="583ff-119">Abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="583ff-119">Enable logging</span></span>

<span data-ttu-id="583ff-120">La registrazione di controllo viene abilitata automaticamente per ogni risorsa di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="583ff-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="583ff-121">È necessario abilitare la registrazione di eventi e del probe di integrità per iniziare a raccogliere i dati disponibili in tali log.</span><span class="sxs-lookup"><span data-stu-id="583ff-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="583ff-122">Eseguire questa procedura per abilitare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="583ff-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="583ff-123">Accedere al [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="583ff-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="583ff-124">Prima di procedere, [creare un servizio di bilanciamento del carico](load-balancer-get-started-internet-arm-ps.md) , se non se ne ha già uno.</span><span class="sxs-lookup"><span data-stu-id="583ff-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="583ff-125">Nel Portale di Azure fare clic su **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="583ff-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="583ff-126">Selezionare **Bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="583ff-126">Select **Load Balancers**.</span></span>

    ![portale - bilanciamento del carico](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="583ff-128">Selezionare un bilanciamento del carico esistente >> **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="583ff-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="583ff-129">Sul lato destro della finestra di dialogo sotto il nome del servizio di bilanciamento del carico, scorrere fino a **Monitoraggio** e fare clic su **Diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="583ff-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![portale - impostazioni di bilanciamento del carico](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="583ff-131">Nel riquadro **Diagnostica**, in **Stato**, selezionare **On**.</span><span class="sxs-lookup"><span data-stu-id="583ff-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="583ff-132">Fare clic su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="583ff-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="583ff-133">In **LOG** selezionare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="583ff-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="583ff-134">Usare il dispositivo di scorrimento per stabilire per quanti giorni i dati dell'evento verranno archiviati nei registri eventi.</span><span class="sxs-lookup"><span data-stu-id="583ff-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="583ff-135">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="583ff-135">Click **Save**.</span></span>

    ![Portale - Log di diagnostica](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="583ff-137">I log di controllo non richiedono un account di archiviazione separato.</span><span class="sxs-lookup"><span data-stu-id="583ff-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="583ff-138">Per l'uso del servizio di archiviazione per la registrazione di eventi e del probe di integrità è previsto un addebito.</span><span class="sxs-lookup"><span data-stu-id="583ff-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="583ff-139">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="583ff-139">Audit log</span></span>

<span data-ttu-id="583ff-140">Il log di controllo viene generato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="583ff-140">The audit log is generated by default.</span></span> <span data-ttu-id="583ff-141">I log vengono conservati per 90 giorni nell'archivio dei log eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="583ff-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="583ff-142">Per altre informazioni su questi log, vedere l'articolo [Visualizzare eventi e log di controllo](../monitoring-and-diagnostics/insights-debugging-with-events.md) .</span><span class="sxs-lookup"><span data-stu-id="583ff-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="583ff-143">Log eventi di avviso</span><span class="sxs-lookup"><span data-stu-id="583ff-143">Alert event log</span></span>

<span data-ttu-id="583ff-144">Questo log viene generato solo se è stato abilitato per ogni bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="583ff-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="583ff-145">Gli eventi vengono registrati in formato JSON e archiviati nell'account di archiviazione specificato quando è stata abilitata la registrazione.</span><span class="sxs-lookup"><span data-stu-id="583ff-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="583ff-146">Di seguito è riportato un esempio di evento.</span><span class="sxs-lookup"><span data-stu-id="583ff-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="583ff-147">L'output JSON mostra la proprietà *eventname* che descrive il motivo per cui il bilanciamento del carico ha creato un avviso.</span><span class="sxs-lookup"><span data-stu-id="583ff-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="583ff-148">In questo caso, l'avviso è stato generato a causa dell'esaurimento delle porte TCP dovuto ai limiti NAT dell'IP di origine (SNAT).</span><span class="sxs-lookup"><span data-stu-id="583ff-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="583ff-149">Log del probe di integrità</span><span class="sxs-lookup"><span data-stu-id="583ff-149">Health probe log</span></span>

<span data-ttu-id="583ff-150">Questo log viene generato solo se è stato abilitato per ogni bilanciamento del carico, come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="583ff-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="583ff-151">I dati vengono archiviati nell'account di archiviazione specificato quando è stata abilitata la registrazione.</span><span class="sxs-lookup"><span data-stu-id="583ff-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="583ff-152">Viene creato un contenitore denominato 'insights-logs-loadbalancerprobehealthstatus' e vengono registrati i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="583ff-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="583ff-153">L'output JSON mostra nel campo proprietà le informazioni di base per lo stato di integrità del probe.</span><span class="sxs-lookup"><span data-stu-id="583ff-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="583ff-154">La proprietà *dipDownCount* indica il numero totale di istanze nel back-end che non ricevono traffico di rete a causa di risposte del probe non riuscite.</span><span class="sxs-lookup"><span data-stu-id="583ff-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="583ff-155">Visualizzare e analizzare il log di controllo</span><span class="sxs-lookup"><span data-stu-id="583ff-155">View and analyze the audit log</span></span>

<span data-ttu-id="583ff-156">È possibile visualizzare e analizzare i dati del log di controllo con uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="583ff-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="583ff-157">**Strumenti di Azure:** recuperare le informazioni dai log di controllo tramite Azure PowerShell, l'interfaccia della riga di comando di Azure, l'API REST di Azure o il portale di anteprima di Azure.</span><span class="sxs-lookup"><span data-stu-id="583ff-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="583ff-158">Per istruzioni dettagliate per ogni metodo, vedere l'articolo [Operazioni di controllo con Gestione risorse](../azure-resource-manager/resource-group-audit.md) .</span><span class="sxs-lookup"><span data-stu-id="583ff-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="583ff-159">**Power BI:** se non esiste ancora un account [Power BI](https://powerbi.microsoft.com/pricing) , è possibile crearne uno di prova gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="583ff-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="583ff-160">Con il [pacchetto di contenuto dei log di controllo di Azure per Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs) è possibile analizzare i dati con dashboard preconfigurati oppure personalizzare le viste in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="583ff-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="583ff-161">Visualizzare e analizzare il log eventi e del probe di integrità</span><span class="sxs-lookup"><span data-stu-id="583ff-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="583ff-162">È necessario connettersi all'account di archiviazione e recuperare le voci di log JSON per i log eventi e del probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="583ff-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="583ff-163">Dopo avere scaricato i file JSON, è possibile convertirli in CSV e visualizzarli in Excel, PowerBI o un altro strumento di visualizzazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="583ff-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="583ff-164">Se si ha familiarità con Visual Studio e i concetti di base della modifica dei valori di costanti e variabili in C#, è possibile usare i [convertitori di log](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponibili in GitHub.</span><span class="sxs-lookup"><span data-stu-id="583ff-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="583ff-165">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="583ff-165">Additional resources</span></span>

* <span data-ttu-id="583ff-166">[visualizzazione dei log di controllo di Azure con Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .</span><span class="sxs-lookup"><span data-stu-id="583ff-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="583ff-167">[visualizzazione e analisi dei log di controllo di Azure in Power BI e altri strumenti](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .</span><span class="sxs-lookup"><span data-stu-id="583ff-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="583ff-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="583ff-168">Next steps</span></span>

[<span data-ttu-id="583ff-169">Informazioni sui probe di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="583ff-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
