---
title: Accedere ad applicazioni Service Fabric con Log Analytics mediante il portale di Azure | Microsoft Docs
description: "È possibile usare la soluzione Service Fabric in Log Analytics mediante il portale di Azure per valutare i rischi e l'integrità delle applicazioni Service Fabric, dei microservizi, dei nodi e dei cluster."
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
ms.openlocfilehash: 8c564c0dcbb2f9be286917b2f4d8a40da5406fae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-the-azure-portal"></a><span data-ttu-id="90b39-103">Valutare le applicazioni e i microservizi Service Fabric con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="90b39-103">Assess Service Fabric applications and micro-services with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="90b39-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="90b39-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="90b39-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90b39-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Simbolo di Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="90b39-107">In questo articolo viene descritto come usare la soluzione Service Fabric in Log Analytics per identificare e risolvere i problemi nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="90b39-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="90b39-108">La soluzione Service Fabric usa i dati della Diagnostica di Azure provenienti dalle macchine virtuali Service Fabric, raccogliendo questi dati dalle tabelle di Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="90b39-108">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="90b39-109">Successivamente, Log Analytics legge gli eventi del framework di Service Fabric, tra cui: **Eventi del servizio affidabile**, **Eventi relativi agli attori**, **Eventi operativi** ed **Eventi ETW personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="90b39-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="90b39-110">Grazie al dashboard della soluzione Service Fabric è possibile vedere i problemi degni di nota e gli eventi rilevanti nell'ambiente Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="90b39-110">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="90b39-111">Per iniziare a usare la soluzione, è necessario connettere il cluster di Service Fabric a un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-111">To get started with the solution, you need to connect your Service Fabric cluster to a Log Analytics workspace.</span></span> <span data-ttu-id="90b39-112">Ecco i tre scenari da prendere in considerazione:</span><span class="sxs-lookup"><span data-stu-id="90b39-112">Here are three scenarios to consider:</span></span>

1. <span data-ttu-id="90b39-113">Se il cluster di Service Fabric non è stato distribuito, eseguire i passaggi descritti nella sezione ***Distribuire un cluster di Service Fabric connesso a un'area di lavoro di Log Analytics*** per distribuire un nuovo cluster e configurarlo per il reporting in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-113">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span></span>
2. <span data-ttu-id="90b39-114">Se si desidera raccogliere i dati dei contatori delle prestazioni dagli host per usare altre soluzioni OMS, ad esempio Security nel cluster di Service Fabric, seguire i passaggi descritti nella sezione ***Distribuire un cluster di Service Fabric connesso a un'area di lavoro di Log Analytics con installata l'estensione VM.***</span><span class="sxs-lookup"><span data-stu-id="90b39-114">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="90b39-115">Se il cluster di Service Fabric è già stato distribuito e si desidera connetterlo a Log Analytics, seguire i passaggi descritti nella sezione ***Aggiunta di un account di archiviazione esistente a Log Analytics.***</span><span class="sxs-lookup"><span data-stu-id="90b39-115">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace"></a><span data-ttu-id="90b39-116">Distribuire un cluster di Service Fabric connesso a un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-116">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span></span>
<span data-ttu-id="90b39-117">Questo modello consente di:</span><span class="sxs-lookup"><span data-stu-id="90b39-117">This template does the following:</span></span>

1. <span data-ttu-id="90b39-118">Distribuire un cluster di Azure Service Fabric già connesso a un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-118">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="90b39-119">È possibile scegliere tra creare una nuova area di lavoro durante la distribuzione del modello e immettere il nome di un'area di lavoro di Log Analytics esistente.</span><span class="sxs-lookup"><span data-stu-id="90b39-119">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="90b39-120">Aggiungere l'account di archiviazione per la diagnostica all'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-120">Adds the diagnostic storage account to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="90b39-121">Abilitare la soluzione Service Fabric nell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-121">Enables the Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="90b39-122">[![Distribuzione in Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="90b39-122">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="90b39-123">Dopo aver selezionato il pulsante di distribuzione indicato sopra, il portale di Azure si apre con i parametri da modificare.</span><span class="sxs-lookup"><span data-stu-id="90b39-123">Once you select the deploy button above, the Azure portal opens with parameters for you to edit.</span></span> <span data-ttu-id="90b39-124">Assicurarsi di creare un nuovo gruppo di risorse se si immette un nuovo nome dell'area di lavoro di Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="90b39-124">Be sure to create a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="90b39-127">Accettare le note legali e fare clic su **Crea** per avviare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="90b39-127">Accept the legal terms and click **Create** to start the deployment.</span></span> <span data-ttu-id="90b39-128">Una volta completata la distribuzione, la nuova area di lavoro e il cluster creati dovrebbero apparire e le tabelle WADServiceFabric*Event, WADWindowsEventLogs e WADETWEvent dovrebbero essere state aggiunte:</span><span class="sxs-lookup"><span data-stu-id="90b39-128">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="90b39-130">Distribuire un cluster di Service Fabric connesso a un'area di lavoro di Log Analytics con installata l'estensione VM.</span><span class="sxs-lookup"><span data-stu-id="90b39-130">Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="90b39-131">Questo modello consente di:</span><span class="sxs-lookup"><span data-stu-id="90b39-131">This template does the following:</span></span>

1. <span data-ttu-id="90b39-132">Distribuire un cluster di Azure Service Fabric già connesso a un'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-132">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="90b39-133">È possibile creare una nuova area di lavoro o usarne una esistente.</span><span class="sxs-lookup"><span data-stu-id="90b39-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="90b39-134">Aggiungere gli account di archiviazione per la diagnostica all'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-134">Adds the diagnostic storage accounts to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="90b39-135">Abilitare la soluzione Service Fabric nell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-135">Enables the Service Fabric solution in the Log Analytics workspace.</span></span>
4. <span data-ttu-id="90b39-136">Installare l'estensione agente MMA in ciascun set di scalabilità di macchine virtuali nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="90b39-136">Installs the MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="90b39-137">Avendo installato l'agente MMA, è possibile visualizzare le metriche delle prestazioni relative ai nodi.</span><span class="sxs-lookup"><span data-stu-id="90b39-137">With the MMA agent installed, you are able to view performance metrics about your nodes.</span></span>

<span data-ttu-id="90b39-138">[![Distribuisci in Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="90b39-138">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="90b39-139">Seguendo la stessa procedura descritta sopra, immettere i parametri necessari e avviare una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="90b39-139">Following the same steps above, input the necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="90b39-140">Anche questa volta verranno visualizzati la nuova area di lavoro, il cluster e le tabelle WAD create:</span><span class="sxs-lookup"><span data-stu-id="90b39-140">Once again you should see the new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="90b39-142">Visualizzazione dei dati sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="90b39-142">Viewing Performance Data</span></span>

<span data-ttu-id="90b39-143">Per visualizzare i dati sulle prestazioni dai nodi:</span><span class="sxs-lookup"><span data-stu-id="90b39-143">To view Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="90b39-144">Avviare l'area di lavoro di Log Analytics dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90b39-144">Launch the Log Analytics workspace from the Azure portal.</span></span>
  <span data-ttu-id="90b39-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="90b39-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="90b39-146">Andare a Impostazioni nel riquadro a sinistra e selezionare dati >> Contatori delle prestazioni di Windows >> "Aggiungi i contatori delle prestazioni selezionati": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="90b39-146">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="90b39-147">In Ricerca log, usare le query seguenti per approfondire le metriche principali relative ai nodi:</span><span class="sxs-lookup"><span data-stu-id="90b39-147">In Log Search, use the following queries to delve into key metrics about your nodes:</span></span>

    <span data-ttu-id="90b39-148">a.</span><span class="sxs-lookup"><span data-stu-id="90b39-148">a.</span></span> <span data-ttu-id="90b39-149">Confrontare l'uso medio della CPU in tutti i nodi nell'ultima ora per determinare i nodi che hanno avuto problemi e l'intervallo di tempo in cui un nodo ha avuto un picco:</span><span class="sxs-lookup"><span data-stu-id="90b39-149">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="90b39-151">b.</span><span class="sxs-lookup"><span data-stu-id="90b39-151">b.</span></span> <span data-ttu-id="90b39-152">Visualizzare i grafici a linee simili relativi alla memoria disponibile in ciascun nodo con questa query:</span><span class="sxs-lookup"><span data-stu-id="90b39-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="90b39-153">Per visualizzare un elenco di tutti i nodi, indicante il valore medio esatto relativo ai MByte disponibili per ciascun nodo, usare questa query:</span><span class="sxs-lookup"><span data-stu-id="90b39-153">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="90b39-155">c.</span><span class="sxs-lookup"><span data-stu-id="90b39-155">c.</span></span> <span data-ttu-id="90b39-156">Se si desidera eseguire un'analisi approfondita di un nodo specifico esaminando la media oraria, il valore minimo e massimo e il 75° percentile riguardo all'uso della CPU, è possibile farlo mediante la query seguente (sostituire campo uso):</span><span class="sxs-lookup"><span data-stu-id="90b39-156">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="90b39-158">Altre informazioni sulle metriche delle prestazioni in Log Analytics nel [Blog di Operations Management Suite](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="90b39-158">Read more information about performance metrics in Log Analytics at the [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-to-log-analytics"></a><span data-ttu-id="90b39-159">Aggiunta di un account di archiviazione esistente a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="90b39-159">Adding an existing storage account to Log Analytics</span></span>

<span data-ttu-id="90b39-160">Questo modello aggiunge semplicemente gli account di archiviazione esistenti a un'area di lavoro di Log Analytics nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="90b39-160">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="90b39-161">[![Distribuzione in Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="90b39-161">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="90b39-162">Per la selezione di un gruppo di risorse, se si usa un'area di lavoro di Log Analytics già esistente, selezionare "Usa esistente" e cercare il gruppo di risorse che contiene l'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for the resource group containing the Log Analytics workspace.</span></span> <span data-ttu-id="90b39-163">Altrimenti, crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="90b39-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="90b39-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="90b39-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="90b39-165">Dopo avere distribuito il modello, sarà possibile visualizzare l'account di archiviazione connesso all'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90b39-165">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span></span> <span data-ttu-id="90b39-166">In questo esempio, all'area di lavoro di Exchange è stato aggiunto un ulteriore account di archiviazione, creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="90b39-166">In this instance, I added one more storage account to the Exchange workspace I created above.</span></span>
<span data-ttu-id="90b39-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="90b39-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="90b39-168">Visualizzare gli eventi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="90b39-168">View Service Fabric events</span></span>

<span data-ttu-id="90b39-169">Una volta completate le distribuzioni e dopo aver abilitato la soluzione Service Fabric nell'area di lavoro, selezionare il riquadro **Service Fabric** nel portale di Log Analytics per avviare il dashboard di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="90b39-169">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span></span> <span data-ttu-id="90b39-170">Il dashboard include le colonne nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="90b39-170">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="90b39-171">Ogni colonna elenca i primi dieci eventi per numero corrispondente ai criteri della colonna per l'intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="90b39-171">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="90b39-172">È possibile eseguire una ricerca di log che fornisce l'intero elenco facendo clic su **Visualizza tutto** nella parte inferiore destra di ciascuna colonna o facendo clic sull'intestazione di colonna.</span><span class="sxs-lookup"><span data-stu-id="90b39-172">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="90b39-173">**Evento di Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="90b39-173">**Service Fabric event**</span></span> | <span data-ttu-id="90b39-174">**description**</span><span class="sxs-lookup"><span data-stu-id="90b39-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="90b39-175">Errori rilevanti</span><span class="sxs-lookup"><span data-stu-id="90b39-175">Notable Issues</span></span> |<span data-ttu-id="90b39-176">Visualizzazione dei problemi, ad esempio RunAsyncFailures RunAsynCancellations e Node Downs.</span><span class="sxs-lookup"><span data-stu-id="90b39-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="90b39-177">Eventi operativi</span><span class="sxs-lookup"><span data-stu-id="90b39-177">Operational Events</span></span> |<span data-ttu-id="90b39-178">Eventi operativi rilevanti, ad esempio l'aggiornamento dell'applicazione e le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="90b39-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="90b39-179">Eventi del servizio affidabile</span><span class="sxs-lookup"><span data-stu-id="90b39-179">Reliable Service Events</span></span> |<span data-ttu-id="90b39-180">Eventi del servizio affidabile rilevanti come Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="90b39-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="90b39-181">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="90b39-181">Actor Events</span></span> |<span data-ttu-id="90b39-182">Gli eventi relativi agli attori rilevanti generati dai micro-servizi, ad esempio le eccezioni generate da un metodo attore, le attivazioni e disattivazioni relative all'attore e così via.</span><span class="sxs-lookup"><span data-stu-id="90b39-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="90b39-183">Eventi dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="90b39-183">Application Events</span></span> |<span data-ttu-id="90b39-184">Tutti gli eventi ETW personalizzati che sono stati generati dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90b39-184">All custom ETW events generated by your applications.</span></span> |

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="90b39-187">La tabella seguente illustra i metodi di raccolta dei dati e altri dettagli sulla modalità di raccolta dei dati per Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="90b39-187">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="90b39-188">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="90b39-188">platform</span></span> | <span data-ttu-id="90b39-189">Agente diretto</span><span class="sxs-lookup"><span data-stu-id="90b39-189">Direct Agent</span></span> | <span data-ttu-id="90b39-190">Agente di Operations Manager</span><span class="sxs-lookup"><span data-stu-id="90b39-190">Operations Manager agent</span></span> | <span data-ttu-id="90b39-191">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="90b39-191">Azure Storage</span></span> | <span data-ttu-id="90b39-192">È necessario Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="90b39-192">Operations Manager required?</span></span> | <span data-ttu-id="90b39-193">Dati dell'agente Operations Manager inviati con il gruppo di gestione</span><span class="sxs-lookup"><span data-stu-id="90b39-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="90b39-194">Frequenza della raccolta</span><span class="sxs-lookup"><span data-stu-id="90b39-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="90b39-195">Windows</span><span class="sxs-lookup"><span data-stu-id="90b39-195">Windows</span></span> |  |  | <span data-ttu-id="90b39-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="90b39-196">&#8226;</span></span> |  |  |<span data-ttu-id="90b39-197">10 minuti</span><span class="sxs-lookup"><span data-stu-id="90b39-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="90b39-198">È possibile modificare l'ambito di questi eventi nella soluzione Service Fabric facendo clic su **Dati basati sugli ultimi 7 giorni** nella parte superiore del dashboard.</span><span class="sxs-lookup"><span data-stu-id="90b39-198">You can change the scope of these events in the Service Fabric solution by clicking **Data based on last 7 days** at the top of the dashboard.</span></span> <span data-ttu-id="90b39-199">È anche possibile mostrare gli eventi generati negli ultimi sette giorni, nell'ultimo giorno o nelle ultime sei ore.</span><span class="sxs-lookup"><span data-stu-id="90b39-199">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="90b39-200">In alternativa, è possibile selezionare **Personalizzato** e specificare un intervallo di date personalizzato.</span><span class="sxs-lookup"><span data-stu-id="90b39-200">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="90b39-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90b39-201">Next steps</span></span>

* <span data-ttu-id="90b39-202">Per visualizzare i dati dettagliati sugli eventi Service Fabric usare [Ricerche log in Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="90b39-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
