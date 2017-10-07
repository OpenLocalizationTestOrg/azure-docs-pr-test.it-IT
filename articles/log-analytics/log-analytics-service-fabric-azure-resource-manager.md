---
title: applicazioni di Service Fabric con Log Analitica aaaAssess hello portale di Azure | Documenti Microsoft
description: "È possibile utilizzare soluzioni di Service Fabric hello in Analitica Log utilizzando hello tooassess portale Azure hello rischio e l'integrità delle applicazioni di Service Fabric, micro servizi, nodi e i cluster."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="25c90-103">Valutare micro-servizi con hello portale di Azure e le applicazioni di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="25c90-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="25c90-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="25c90-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="25c90-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25c90-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Simbolo di Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="25c90-107">In questo articolo viene descritto come toouse hello soluzione Service Fabric in Log Analitica toohelp identificare e risolvere i problemi del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25c90-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="25c90-108">Hello soluzione Service Fabric utilizza i dati di diagnostica di Azure delle macchine virtuali dell'infrastruttura di servizio, raccogliendo i dati dalle tabelle di Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="25c90-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="25c90-109">Successivamente, Log Analytics legge gli eventi del framework di Service Fabric, tra cui: **Eventi del servizio affidabile**, **Eventi relativi agli attori**, **Eventi operativi** ed **Eventi ETW personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="25c90-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="25c90-110">Con dashboard soluzione hello, si tooview in grado di problemi e degli eventi di Service Fabric nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="25c90-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="25c90-111">tooget avviato con la soluzione hello, è necessario tooconnect Service Fabric cluster tooa Log Analitica area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="25c90-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="25c90-112">Ecco tre scenari tooconsider:</span><span class="sxs-lookup"><span data-stu-id="25c90-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="25c90-113">Se il cluster di Service Fabric non sono stati distribuiti, utilizzare i passaggi di hello in ***distribuire un'area di lavoro Cluster di Service Fabric connesso Analitica Log tooa*** toodeploy un nuovo cluster e aver configurato tooreport tooLog Analitica.</span><span class="sxs-lookup"><span data-stu-id="25c90-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="25c90-114">Se è necessario toocollect contatori delle prestazioni da toouse l'host altre soluzioni OMS, ad esempio sicurezza il cluster di infrastruttura del servizio, seguire passaggi hello ***distribuire un'area di lavoro Log Analitica tooa Cluster di Service Fabric connesso con l'estensione della macchina virtuale installato.***</span><span class="sxs-lookup"><span data-stu-id="25c90-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="25c90-115">Se si hanno già distribuito il cluster di Service Fabric e si desidera tooconnect è tooLog Analitica, seguire i passaggi hello ***aggiungendo un tooLog di account di archiviazione esistente Analitica.***</span><span class="sxs-lookup"><span data-stu-id="25c90-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="25c90-116">Distribuire un'area di lavoro di Cluster di Service Fabric connesso tooa Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="25c90-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="25c90-117">Questo modello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="25c90-117">This template does hello following:</span></span>

1. <span data-ttu-id="25c90-118">Consente di distribuire un'area di lavoro Log Analitica di tooa cluster già connessi di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25c90-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="25c90-119">È necessario hello opzione toocreate una nuova area di lavoro durante la distribuzione modello hello o nome hello input di un'area di lavoro Log Analitica già esistente.</span><span class="sxs-lookup"><span data-stu-id="25c90-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="25c90-120">Aggiunge l'area di lavoro hello archiviazione diagnostica account toohello Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="25c90-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="25c90-121">Consente di soluzioni di Service Fabric hello nell'area di lavoro Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="25c90-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="25c90-122">[![Distribuire tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="25c90-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="25c90-123">Dopo aver selezionato hello distribuire pulsante sopra riportato, hello apre portali Azure con i parametri per si tooedit.</span><span class="sxs-lookup"><span data-stu-id="25c90-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="25c90-124">Essere toocreate che un nuovo gruppo di risorse, se l'input di un nuovo nome dell'area di lavoro Analitica Log:</span><span class="sxs-lookup"><span data-stu-id="25c90-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="25c90-127">Accettare i termini legali specifici hello e fare clic su **crea** distribuzione hello toostart.</span><span class="sxs-lookup"><span data-stu-id="25c90-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="25c90-128">Al termine della distribuzione di hello, si dovrebbe vedere nuova area di lavoro hello e cluster creato e hello WADServiceFabric * eventi, WADWindowsEventLogs e WADETWEvent tabelle aggiunte:</span><span class="sxs-lookup"><span data-stu-id="25c90-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="25c90-130">Distribuire un'area di lavoro di Cluster di Service Fabric connesso tooa Analitica Log con l'estensione della macchina virtuale installato.</span><span class="sxs-lookup"><span data-stu-id="25c90-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="25c90-131">Questo modello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="25c90-131">This template does hello following:</span></span>

1. <span data-ttu-id="25c90-132">Consente di distribuire un'area di lavoro Log Analitica di tooa cluster già connessi di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25c90-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="25c90-133">È possibile creare una nuova area di lavoro o usarne una esistente.</span><span class="sxs-lookup"><span data-stu-id="25c90-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="25c90-134">Aggiunge l'area di lavoro hello archiviazione diagnostica account toohello Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="25c90-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="25c90-135">Consente di soluzioni di Service Fabric hello nell'area di lavoro Log Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="25c90-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="25c90-136">Installa l'estensione hello MMA agente in ogni scalabilità della macchina virtuale impostato nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25c90-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="25c90-137">Agente hello MMA installato, le metriche delle prestazioni in grado di tooview si sta i nodi.</span><span class="sxs-lookup"><span data-stu-id="25c90-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="25c90-138">[![Distribuire tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="25c90-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="25c90-139">Di seguito hello stessi passaggi illustrati in precedenza, i parametri necessari hello input e avviano una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="25c90-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="25c90-140">Verrà visualizzato nuovamente nuova area di lavoro hello del cluster e create tutte le tabelle di diagnostica AZURE:</span><span class="sxs-lookup"><span data-stu-id="25c90-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="25c90-142">Visualizzazione dei dati sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="25c90-142">Viewing Performance Data</span></span>

<span data-ttu-id="25c90-143">tooview dati delle prestazioni dai nodi:</span><span class="sxs-lookup"><span data-stu-id="25c90-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="25c90-144">Avviare l'area di lavoro Log Analitica hello da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="25c90-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="25c90-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="25c90-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="25c90-146">Passare tooSettings hello riquadro a sinistra e selezionare dati >> i contatori delle prestazioni di Windows >> "Aggiungi hello selezionato i contatori delle prestazioni": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="25c90-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="25c90-147">Nella ricerca di Log, utilizzare hello seguente query toodelve nelle metriche principali relative i nodi:</span><span class="sxs-lookup"><span data-stu-id="25c90-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="25c90-148">a.</span><span class="sxs-lookup"><span data-stu-id="25c90-148">a.</span></span> <span data-ttu-id="25c90-149">Confronto hello utilizzo medio della CPU in tutti i nodi di hello toosee di un'ora ultimo i nodi che hanno problemi e in quale intervallo di tempo un nodo ha un picco:</span><span class="sxs-lookup"><span data-stu-id="25c90-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="25c90-151">b.</span><span class="sxs-lookup"><span data-stu-id="25c90-151">b.</span></span> <span data-ttu-id="25c90-152">Visualizzare i grafici a linee simili relativi alla memoria disponibile in ciascun nodo con questa query:</span><span class="sxs-lookup"><span data-stu-id="25c90-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="25c90-153">tooview un elenco di tutti i nodi, che mostra il valore medio hello esatto per MByte disponibili per ogni nodo, usare questa query:</span><span class="sxs-lookup"><span data-stu-id="25c90-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="25c90-155">c.</span><span class="sxs-lookup"><span data-stu-id="25c90-155">c.</span></span> <span data-ttu-id="25c90-156">In caso di hello che si desidera toodrill verso il basso in un nodo specifico esaminando Media oraria hello, utilizzo della CPU minimo, massimo e di 75 percentile, si è in grado di toodo il problema, utilizzare questa query (sostituire campo del Computer):</span><span class="sxs-lookup"><span data-stu-id="25c90-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="25c90-158">Altre informazioni sulle metriche delle prestazioni nel Log Analitica a hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="25c90-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="25c90-159">Aggiunta di un tooLog di account di archiviazione esistente Analitica</span><span class="sxs-lookup"><span data-stu-id="25c90-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="25c90-160">Questo modello aggiunge semplicemente l'archiviazione account tooa nuovo o esistente Log Analitica area di lavoro esistente.</span><span class="sxs-lookup"><span data-stu-id="25c90-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="25c90-161">[![Distribuire tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="25c90-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="25c90-162">La selezione di un gruppo di risorse, se si utilizza un'area di lavoro Log Analitica già esistente, selezionare "Usa esistente" e cercare il gruppo di risorse hello contenente l'area di lavoro di hello Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="25c90-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="25c90-163">Altrimenti, crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="25c90-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="25c90-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="25c90-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="25c90-165">Dopo la distribuzione di questo modello, sarà in grado di toosee hello archiviazione account connesso tooyour Log Analitica dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="25c90-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="25c90-166">In questo caso, aggiunto uno più storage account toohello Exchange area di lavoro che è stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="25c90-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="25c90-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="25c90-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="25c90-168">Visualizzare gli eventi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="25c90-168">View Service Fabric events</span></span>

<span data-ttu-id="25c90-169">Una volta completate le distribuzioni di hello e hello soluzione Service Fabric è stata abilitata nell'area di lavoro, selezionare hello **Service Fabric** riquadro nel dashboard di hello Analitica Log toolaunch portale hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25c90-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="25c90-170">dashboard Hello sono incluse colonne hello hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="25c90-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="25c90-171">Ogni colonna elenca gli eventi di 10 superiore di hello associando conteggio che i criteri della colonna per hello specificato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="25c90-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="25c90-172">È possibile eseguire una ricerca di log che fornisce l'intero elenco hello facendo **tutti** hello in basso a destra di ogni colonna, oppure facendo clic sull'intestazione di colonna hello.</span><span class="sxs-lookup"><span data-stu-id="25c90-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="25c90-173">**Evento di Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="25c90-173">**Service Fabric event**</span></span> | <span data-ttu-id="25c90-174">**description**</span><span class="sxs-lookup"><span data-stu-id="25c90-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="25c90-175">Errori rilevanti</span><span class="sxs-lookup"><span data-stu-id="25c90-175">Notable Issues</span></span> |<span data-ttu-id="25c90-176">Visualizzazione dei problemi, ad esempio RunAsyncFailures RunAsynCancellations e Node Downs.</span><span class="sxs-lookup"><span data-stu-id="25c90-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="25c90-177">Eventi operativi</span><span class="sxs-lookup"><span data-stu-id="25c90-177">Operational Events</span></span> |<span data-ttu-id="25c90-178">Eventi operativi rilevanti, ad esempio l'aggiornamento dell'applicazione e le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="25c90-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="25c90-179">Eventi del servizio affidabile</span><span class="sxs-lookup"><span data-stu-id="25c90-179">Reliable Service Events</span></span> |<span data-ttu-id="25c90-180">Eventi del servizio affidabile rilevanti come Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="25c90-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="25c90-181">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="25c90-181">Actor Events</span></span> |<span data-ttu-id="25c90-182">Gli eventi relativi agli attori rilevanti generati dai micro-servizi, ad esempio le eccezioni generate da un metodo attore, le attivazioni e disattivazioni relative all'attore e così via.</span><span class="sxs-lookup"><span data-stu-id="25c90-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="25c90-183">Eventi dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="25c90-183">Application Events</span></span> |<span data-ttu-id="25c90-184">Tutti gli eventi ETW personalizzati che sono stati generati dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="25c90-184">All custom ETW events generated by your applications.</span></span> |

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="25c90-187">Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per l'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="25c90-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="25c90-188">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="25c90-188">platform</span></span> | <span data-ttu-id="25c90-189">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="25c90-189">Direct Agent</span></span> | <span data-ttu-id="25c90-190">Agente di Operations Manager</span><span class="sxs-lookup"><span data-stu-id="25c90-190">Operations Manager agent</span></span> | <span data-ttu-id="25c90-191">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="25c90-191">Azure Storage</span></span> | <span data-ttu-id="25c90-192">È necessario Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="25c90-192">Operations Manager required?</span></span> | <span data-ttu-id="25c90-193">Dati dell'agente Operations Manager inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="25c90-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="25c90-194">Frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="25c90-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="25c90-195">Windows</span><span class="sxs-lookup"><span data-stu-id="25c90-195">Windows</span></span> |  |  | <span data-ttu-id="25c90-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="25c90-196">&#8226;</span></span> |  |  |<span data-ttu-id="25c90-197">10 minuti</span><span class="sxs-lookup"><span data-stu-id="25c90-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="25c90-198">È possibile modificare l'ambito di hello di questi eventi in una soluzione di Service Fabric hello facendo **i dati basati su ultimi 7 giorni** nella parte superiore di hello del dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="25c90-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="25c90-199">È inoltre possibile visualizzare gli eventi generati all'interno di hello ultimi sette giorni, un giorno o sei ore.</span><span class="sxs-lookup"><span data-stu-id="25c90-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="25c90-200">In alternativa, è possibile selezionare **personalizzato** toospecify un intervallo di date personalizzato.</span><span class="sxs-lookup"><span data-stu-id="25c90-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="25c90-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25c90-201">Next steps</span></span>

* <span data-ttu-id="25c90-202">Utilizzare [ricerche nei Log nel Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati di evento di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25c90-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
