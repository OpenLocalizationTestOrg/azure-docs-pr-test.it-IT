---
title: aaaMonitor operazioni, gli eventi e i contatori per il bilanciamento del carico | Documenti Microsoft
description: "Informazioni su come gli eventi di avviso, tooenable e verificare la presenza di registrazione dello stato di integrità servizio di bilanciamento del carico di Azure"
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
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="d6a84-103">Analisi dei log per il servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="d6a84-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="d6a84-104">È possibile utilizzare diversi tipi di registri in Azure toomanage e risolvere i problemi relativi a servizi di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d6a84-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="d6a84-105">Alcuni di questi log sono accessibili tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="d6a84-106">Tutti i log possono essere estratti da Archiviazione BLOB di Azure e visualizzati in strumenti differenti, ad esempio Excel e PowerBI.</span><span class="sxs-lookup"><span data-stu-id="d6a84-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="d6a84-107">È possibile ulteriori informazioni sui tipi diversi hello dei log dall'elenco di hello seguente.</span><span class="sxs-lookup"><span data-stu-id="d6a84-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="d6a84-108">**Log di controllo:** è possibile utilizzare [registri di controllo Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (precedentemente noto come registri) tooview tutte le operazioni vengono inviati tooyour sottoscrizioni Azure e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="d6a84-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="d6a84-109">I log di controllo sono abilitati per impostazione predefinita e possono essere visualizzati nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="d6a84-110">**I registri eventi di avviso:** è possibile utilizzare questo rasied gli avvisi di log tooview dal servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="d6a84-111">stato Hello di bilanciamento del carico hello verrà raccolti ogni cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="d6a84-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="d6a84-112">Questo log viene scritto solo se viene generato un evento di avviso del bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d6a84-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="d6a84-113">**I registri di probe di integrità:** è possibile utilizzare questo log tooview problemi per il probe di integrità, ad esempio il numero di hello di istanze del pool di back-end che non ricevano richieste dal bilanciamento del carico hello a causa di errori di probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="d6a84-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="d6a84-114">Questo log viene scritto toowhen viene apportata una modifica nello stato di probe di integrità hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6a84-115">Attualmente l'analisi di log funziona solo per i servizi di bilanciamento del carico con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="d6a84-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="d6a84-116">I log sono disponibili solo per le risorse distribuite nel modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="d6a84-117">Non è possibile utilizzare i log per le risorse nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="d6a84-118">Per ulteriori informazioni sui modelli di distribuzione hello, vedere [distribuzione classica e gestione di informazioni sulle risorse](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d6a84-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="d6a84-119">Abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="d6a84-119">Enable logging</span></span>

<span data-ttu-id="d6a84-120">La registrazione di controllo viene abilitata automaticamente per ogni risorsa di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6a84-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="d6a84-121">È necessario evento tooenable e integrità probe registrazione toostart la raccolta dei dati di hello disponibili tramite tali log.</span><span class="sxs-lookup"><span data-stu-id="d6a84-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="d6a84-122">Utilizzare hello registrazione tooenable i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d6a84-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="d6a84-123">Accedi toohello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6a84-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="d6a84-124">Prima di procedere, [creare un servizio di bilanciamento del carico](load-balancer-get-started-internet-arm-ps.md) , se non se ne ha già uno.</span><span class="sxs-lookup"><span data-stu-id="d6a84-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="d6a84-125">Nel portale di hello, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="d6a84-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="d6a84-126">Selezionare **Bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="d6a84-126">Select **Load Balancers**.</span></span>

    ![portale - bilanciamento del carico](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="d6a84-128">Selezionare un bilanciamento del carico esistente >> **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d6a84-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="d6a84-129">Sul lato destro di hello di hello nella finestra di dialogo Nome hello di bilanciamento del carico hello, scorrere troppo**monitoraggio**, fare clic su **diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="d6a84-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![portale - impostazioni di bilanciamento del carico](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="d6a84-131">In hello **diagnostica** riquadro, in **stato**selezionare **su**.</span><span class="sxs-lookup"><span data-stu-id="d6a84-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="d6a84-132">Fare clic su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="d6a84-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="d6a84-133">In **LOG** selezionare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="d6a84-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="d6a84-134">Utilizzare hello dispositivo di scorrimento toodetermine quanti giorni verranno archiviati i dati di eventi relativi a nei registri eventi di hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="d6a84-135">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d6a84-135">Click **Save**.</span></span>

    ![Portale - Log di diagnostica](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="d6a84-137">I log di controllo non richiedono un account di archiviazione separato.</span><span class="sxs-lookup"><span data-stu-id="d6a84-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="d6a84-138">utilizzo di Hello di archiviazione per l'evento e l'integrità probe registrazione spese del servizio.</span><span class="sxs-lookup"><span data-stu-id="d6a84-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="d6a84-139">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="d6a84-139">Audit log</span></span>

<span data-ttu-id="d6a84-140">Per impostazione predefinita, viene generato il log di controllo di Hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-140">hello audit log is generated by default.</span></span> <span data-ttu-id="d6a84-141">Hello registri vengono mantenuti per 90 giorni nell'archivio di registri eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6a84-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="d6a84-142">Altre informazioni su questi registri leggendo hello [visualizzare eventi e log di controllo](../monitoring-and-diagnostics/insights-debugging-with-events.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d6a84-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="d6a84-143">Log eventi di avviso</span><span class="sxs-lookup"><span data-stu-id="d6a84-143">Alert event log</span></span>

<span data-ttu-id="d6a84-144">Questo log viene generato solo se è stato abilitato per ogni bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d6a84-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="d6a84-145">gli eventi di Hello vengono registrati in formato JSON e archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="d6a84-146">Hello Ecco un esempio di un evento.</span><span class="sxs-lookup"><span data-stu-id="d6a84-146">hello following is an example of an event.</span></span>

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

<span data-ttu-id="d6a84-147">Hello JSON output illustrato hello *eventname* proprietà che descrivono il motivo di hello di bilanciamento del carico hello creato un avviso.</span><span class="sxs-lookup"><span data-stu-id="d6a84-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="d6a84-148">In questo caso, l'avviso di hello generato è stato scadenza tooTCP esaurimento delle porte causato da un'origine che IP NAT limita (SNAT).</span><span class="sxs-lookup"><span data-stu-id="d6a84-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="d6a84-149">Log del probe di integrità</span><span class="sxs-lookup"><span data-stu-id="d6a84-149">Health probe log</span></span>

<span data-ttu-id="d6a84-150">Questo log viene generato solo se è stato abilitato per ogni bilanciamento del carico, come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d6a84-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="d6a84-151">Hello dati vengono archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="d6a84-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="d6a84-152">Viene creato un contenitore denominato 'insights-log-loadbalancerprobehealthstatus' e viene registrato hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6a84-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

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

<span data-ttu-id="d6a84-153">l'output JSON Hello Mostra hello proprietà campo hello informazioni di base per lo stato di integrità di hello probe.</span><span class="sxs-lookup"><span data-stu-id="d6a84-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="d6a84-154">Hello *dipDownCount* numero totale di hello di istanze vengono visualizzate le proprietà nel back-end di hello che non ricevano il traffico di rete a causa delle risposte probe toofailed.</span><span class="sxs-lookup"><span data-stu-id="d6a84-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="d6a84-155">Visualizzare e analizzare i log di controllo hello</span><span class="sxs-lookup"><span data-stu-id="d6a84-155">View and analyze hello audit log</span></span>

<span data-ttu-id="d6a84-156">È possibile visualizzare e analizzare i dati di log di controllo utilizzando uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="d6a84-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="d6a84-157">**Gli strumenti di Azure:** recuperare informazioni dai log di controllo hello tramite Azure PowerShell, hello interfaccia della riga di comando (CLI di Azure), l'API REST di Azure hello o hello portale di anteprima di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6a84-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="d6a84-158">Istruzioni dettagliate per ogni metodo sono descritti in dettaglio in hello [controllare le operazioni con Gestione risorse](../azure-resource-manager/resource-group-audit.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d6a84-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="d6a84-159">**Power BI:** se non esiste ancora un account [Power BI](https://powerbi.microsoft.com/pricing) , è possibile crearne uno di prova gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="d6a84-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="d6a84-160">Utilizzo di hello [di contenuto log di controllo di Azure per Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), è possibile analizzare i dati con i dashboard configurati in precedenza oppure è possibile personalizzare le visualizzazioni toosuit i requisiti.</span><span class="sxs-lookup"><span data-stu-id="d6a84-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="d6a84-161">Visualizzare e analizzare i probe di integrità hello e registro eventi</span><span class="sxs-lookup"><span data-stu-id="d6a84-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="d6a84-162">È necessario un archivio tooyour tooconnect account e recupero delle voci di log hello JSON per i log di probe di evento e l'integrità.</span><span class="sxs-lookup"><span data-stu-id="d6a84-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="d6a84-163">Dopo avere scaricato i file JSON hello, è possibile convertirli tooCSV e view in Excel, Power BI o qualsiasi altro strumento di visualizzazione di dati.</span><span class="sxs-lookup"><span data-stu-id="d6a84-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="d6a84-164">Se si ha familiarità con Visual Studio e concetti di base di modificare i valori costanti e variabili in c#, è possibile utilizzare hello [log strumenti convertitore](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponibili da GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6a84-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6a84-165">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d6a84-165">Additional resources</span></span>

* <span data-ttu-id="d6a84-166">[visualizzazione dei log di controllo di Azure con Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d6a84-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="d6a84-167">[visualizzazione e analisi dei log di controllo di Azure in Power BI e altri strumenti](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .</span><span class="sxs-lookup"><span data-stu-id="d6a84-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6a84-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6a84-168">Next steps</span></span>

[<span data-ttu-id="d6a84-169">Informazioni sui probe di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d6a84-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
