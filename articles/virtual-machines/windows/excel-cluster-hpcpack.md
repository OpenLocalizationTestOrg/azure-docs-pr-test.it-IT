---
title: Cluster HPC Pack per Excel e SOA | Microsoft Docs
description: Introduzione all'esecuzione di carichi di lavoro Excel e SOA su larga scala in un cluster HPC Pack in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 63babd94fdab15217cfb0757e4cd6efe458a628d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="ec458-103">Introduzione all'esecuzione di carichi di lavoro Excel e SOA in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="ec458-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="ec458-104">Questo articolo illustra come distribuire un cluster Microsoft HPC Pack 2012 R2 nelle macchine virtuali di Azure con un modello di avvio rapido di Azure o uno script di distribuzione di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec458-104">This article shows you how to deploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="ec458-105">Il cluster usa le immagini VM di Azure Marketplace progettate per l'esecuzione di Microsoft Excel o carichi di lavoro di architettura orientata ai servizi (SOA) con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ec458-105">The cluster uses Azure Marketplace VM images designed to run Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="ec458-106">È possibile usare il cluster per eseguire servizi Excel HPC e SOA da un computer client locale.</span><span class="sxs-lookup"><span data-stu-id="ec458-106">You can use the cluster to run Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="ec458-107">I servizi Excel HPC includono l'offload di cartelle di lavoro di Excel e funzioni definite dall'utente di Excel o UDF.</span><span class="sxs-lookup"><span data-stu-id="ec458-107">The Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ec458-108">Questo articolo si basa su funzionalità, modelli e script per HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="ec458-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="ec458-109">Questo scenario non è attualmente supportato in HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="ec458-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ec458-110">Il seguente diagramma illustra in modo generale il cluster HPC Pack che verrà creato.</span><span class="sxs-lookup"><span data-stu-id="ec458-110">At a high level, the following diagram shows the HPC Pack cluster you create.</span></span>

![Cluster HPC con nodi che eseguono carichi di lavoro di Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="ec458-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ec458-112">Prerequisites</span></span>
* <span data-ttu-id="ec458-113">**Computer client** : per inviare i processi di Excel e SOA di esempio al cluster, è necessario un computer client basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="ec458-113">**Client computer** - You need a Windows-based client computer to submit sample Excel and SOA jobs to the cluster.</span></span> <span data-ttu-id="ec458-114">Per eseguire lo script di distribuzione del cluster di Azure PowerShell (se si sceglie tale metodo di distribuzione), è necessario anche un computer Windows.</span><span class="sxs-lookup"><span data-stu-id="ec458-114">You also need a Windows computer to run the Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="ec458-115">**Sottoscrizione di Azure** : se non è disponibile una sottoscrizione di Azure, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="ec458-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="ec458-116">**Quota di core** : potrebbe essere necessario aumentare la quota di core, soprattutto se si distribuiscono più nodi del cluster con dimensioni delle macchine virtuali multicore.</span><span class="sxs-lookup"><span data-stu-id="ec458-116">**Cores quota** - You might need to increase the quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="ec458-117">Se si utilizza un modello di avvio rapido di Azure, la quota di core in Resource Manager è riferita a ogni area di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec458-117">If you are using an Azure quickstart template, the cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="ec458-118">In tal caso, potrebbe essere necessario aumentare la quota per una determinata area.</span><span class="sxs-lookup"><span data-stu-id="ec458-118">In that case, you might need to increase the quota in a specific region.</span></span> <span data-ttu-id="ec458-119">Vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="ec458-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="ec458-120">Per aumentare una quota, è possibile [aprire una richiesta di assistenza clienti online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) senza alcun addebito.</span><span class="sxs-lookup"><span data-stu-id="ec458-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="ec458-121">**Licenza di Microsoft Office** : se si distribuiscono nodi di calcolo usando un'immagine di VM di HPC Pack 2012 R2 di Marketplace con Microsoft Excel, viene installata una versione di valutazione di Microsoft Excel Professional Plus 2013 di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="ec458-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="ec458-122">Scaduto il periodo di valutazione, per continuare a eseguire i carichi di lavoro è necessario attivare Excel con una licenza valida di Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="ec458-122">After the evaluation period, you need to provide a valid Microsoft Office license to activate Excel to continue to run workloads.</span></span> <span data-ttu-id="ec458-123">Vedere [Attivazione di Excel](#excel-activation) più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ec458-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="ec458-124">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="ec458-124">Step 1.</span></span> <span data-ttu-id="ec458-125">Configurazione di un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="ec458-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="ec458-126">Verranno mostrate due possibili configurazioni del cluster HPC Pack 2012 R2: nella prima vengono usati un modello di avvio rapido e il portale di Azure, mentre nella seconda viene usato uno script di distribuzione di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec458-126">We show two options to set up the HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and the Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="ec458-127">Opzione 1.</span><span class="sxs-lookup"><span data-stu-id="ec458-127">Option 1.</span></span> <span data-ttu-id="ec458-128">Uso di un modello di Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="ec458-128">Use a quickstart template</span></span>
<span data-ttu-id="ec458-129">Usare un modello di Guida introduttiva di Azure per distribuire con rapidità un cluster HPC Pack nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec458-129">Use an Azure quickstart template to quickly deploy an HPC Pack cluster in the Azure portal.</span></span> <span data-ttu-id="ec458-130">Aprendo il modello nel portale, si ottiene un'interfaccia utente semplice in cui è possibile immettere le impostazioni per il cluster.</span><span class="sxs-lookup"><span data-stu-id="ec458-130">When you open the template in the portal, you get a simple UI where you enter the settings for your cluster.</span></span> <span data-ttu-id="ec458-131">Di seguito sono riportati i passaggi necessari.</span><span class="sxs-lookup"><span data-stu-id="ec458-131">Here are the steps.</span></span> 

> [!TIP]
> <span data-ttu-id="ec458-132">È possibile usare un [modello di Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) che crea un cluster simile, specifico per i carichi di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="ec458-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="ec458-133">La procedura è leggermente diversa da quella che segue.</span><span class="sxs-lookup"><span data-stu-id="ec458-133">The steps differ slightly from the following.</span></span>
> 
> 

1. <span data-ttu-id="ec458-134">Visitare la [pagina del modello per la creazione del cluster HPC su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="ec458-134">Visit the [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="ec458-135">Se lo si desidera, esaminare le informazioni sul modello e il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="ec458-135">If you want, review information about the template and the source code.</span></span>
2. <span data-ttu-id="ec458-136">Fare clic su **Distribuisci in Azure** per avviare una distribuzione con il modello nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec458-136">Click **Deploy to Azure** to start a deployment with the template in the Azure portal.</span></span>
   
   ![Modello di distribuzione in Azure][github]
3. <span data-ttu-id="ec458-138">Nel portale, attenersi alla procedura seguente per immettere i parametri del modello di cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="ec458-138">In the portal, follow these steps to enter the parameters for the HPC cluster template.</span></span>
   
   <span data-ttu-id="ec458-139">a.</span><span class="sxs-lookup"><span data-stu-id="ec458-139">a.</span></span> <span data-ttu-id="ec458-140">Nella pagina **Parametri** , immettere o modificare i valori dei parametri del modello.</span><span class="sxs-lookup"><span data-stu-id="ec458-140">On the **Parameters** page, enter or modify values for the template parameters.</span></span> <span data-ttu-id="ec458-141">(Per visualizzare informazioni della Guida, fare clic sull'icona accanto a ogni impostazione). Nella seguente schermata vengono visualizzati valori di esempio.</span><span class="sxs-lookup"><span data-stu-id="ec458-141">(Click the icon next to each setting for help information.) Sample values are shown in the following screen.</span></span> <span data-ttu-id="ec458-142">In questo esempio viene creato un cluster denominato *hpc01* nel dominio *hpc.local*, composto da un nodo head e 2 nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ec458-142">This example creates a cluster named *hpc01* in the *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="ec458-143">I nodi di calcolo vengono creati da un'immagine di VM di HPC Pack che include Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="ec458-143">The compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Immettere i parametri][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="ec458-145">La VM del nodo head viene creata automaticamente dall' [immagine più recente del Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) di HPC Pack 2012 R2 su Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="ec458-145">The head node VM is created automatically from the [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="ec458-146">Attualmente l'immagine è basata su HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="ec458-146">Currently the image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="ec458-147">Le VM del nodo di calcolo vengono create dall'immagine più recente della famiglia di nodi di calcolo selezionata.</span><span class="sxs-lookup"><span data-stu-id="ec458-147">Compute node VMs are created from the latest image of the selected compute node family.</span></span> <span data-ttu-id="ec458-148">Selezionare l'opzione **ComputeNodeWithExcel** per l'immagine del nodo di calcolo di HPC Pack più recente che include una versione di valutazione di Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="ec458-148">Select the **ComputeNodeWithExcel** option for the latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="ec458-149">Per distribuire un cluster per sessioni SOA generiche o per l'offload di UDF di Excel, scegliere l'opzione **ComputeNode** (senza Excel installato).</span><span class="sxs-lookup"><span data-stu-id="ec458-149">To deploy a cluster for general SOA sessions or for Excel UDF offloading, choose the **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="ec458-150">b.</span><span class="sxs-lookup"><span data-stu-id="ec458-150">b.</span></span> <span data-ttu-id="ec458-151">Selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ec458-151">Choose the subscription.</span></span>
   
   <span data-ttu-id="ec458-152">c.</span><span class="sxs-lookup"><span data-stu-id="ec458-152">c.</span></span> <span data-ttu-id="ec458-153">Creare un gruppo di risorse per il cluster, ad esempio *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="ec458-153">Create a resource group for the cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="ec458-154">d.</span><span class="sxs-lookup"><span data-stu-id="ec458-154">d.</span></span> <span data-ttu-id="ec458-155">Scegliere un percorso per il gruppo di risorse, ad esempio gli Stati Uniti centrali.</span><span class="sxs-lookup"><span data-stu-id="ec458-155">Choose a location for the resource group, such as Central US.</span></span>
   
   <span data-ttu-id="ec458-156">e.</span><span class="sxs-lookup"><span data-stu-id="ec458-156">e.</span></span> <span data-ttu-id="ec458-157">Nella pagina **Note legali** esaminare le condizioni.</span><span class="sxs-lookup"><span data-stu-id="ec458-157">On the **Legal terms** page, review the terms.</span></span> <span data-ttu-id="ec458-158">Se si accettano le condizioni, fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="ec458-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="ec458-159">Quindi, dopo aver impostato i valori per il modello, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ec458-159">Then, when you are finished setting the values for the template, click **Create**.</span></span>
4. <span data-ttu-id="ec458-160">Al termine della distribuzione (in genere richiede circa 30 minuti), esportare il file del certificato del cluster dal nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="ec458-160">When the deployment completes (it typically takes around 30 minutes), export the cluster certificate file from the cluster head node.</span></span> <span data-ttu-id="ec458-161">Successivamente questo certificato pubblico viene importato nel computer client per fornire l'autenticazione sul lato server per l'associazione HTTP protetta.</span><span class="sxs-lookup"><span data-stu-id="ec458-161">In a later step, you import this public certificate on the client computer to provide the server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="ec458-162">a.</span><span class="sxs-lookup"><span data-stu-id="ec458-162">a.</span></span> <span data-ttu-id="ec458-163">Nel portale di Azure passare al dashboard, selezionare il nodo head e fare clic su **Connetti** nella parte superiore della pagina per connettersi tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="ec458-163">In the Azure portal, go to the dashboard, select the head node, and click **Connect** at the top of the page to connect using Remote Desktop.</span></span>
   
    <!-- ![Connect to the head node][connect] -->
   
   <span data-ttu-id="ec458-164">b.</span><span class="sxs-lookup"><span data-stu-id="ec458-164">b.</span></span> <span data-ttu-id="ec458-165">Seguire le procedure standard in usare Gestione certificati per esportare il certificato del nodo head (situato in Cert: \LocalMachine\My) senza la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="ec458-165">Use standard procedures in Certificate Manager to export the head node certificate (located under Cert:\LocalMachine\My) without the private key.</span></span> <span data-ttu-id="ec458-166">In questo esempio esportare *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="ec458-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Esportare il certificato][cert]

### <a name="option-2-use-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="ec458-168">Opzione 2.</span><span class="sxs-lookup"><span data-stu-id="ec458-168">Option 2.</span></span> <span data-ttu-id="ec458-169">Uso dello script di distribuzione di HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="ec458-169">Use the HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="ec458-170">Lo script di distribuzione di HPC Pack IaaS offre un altro modo versatile per distribuire un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ec458-170">The HPC Pack IaaS deployment script provides another versatile way to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="ec458-171">Esso crea un cluster nel modello di distribuzione classica, mentre il modello usa il modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec458-171">It creates a cluster in the classic deployment model, whereas the template uses the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="ec458-172">Lo script è inoltre compatibile con una sottoscrizione nel servizio Azure globale o per la Cina.</span><span class="sxs-lookup"><span data-stu-id="ec458-172">Also, the script is compatible with a subscription in either the Azure Global or Azure China service.</span></span>

<span data-ttu-id="ec458-173">**Ulteriori prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="ec458-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="ec458-174">**Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.</span><span class="sxs-lookup"><span data-stu-id="ec458-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="ec458-175">**Script di distribuzione di HPC Pack IaaS** : scaricare e decomprimere la versione più recente dello script dal [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="ec458-175">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="ec458-176">Controllare la versione dello script eseguendolo `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="ec458-176">Check the version of the script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="ec458-177">Questo articolo si basa sulla versione dello script 4.5.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="ec458-177">This article is based on version 4.5.0 or later of the script.</span></span>

<span data-ttu-id="ec458-178">**Creazione del file di configurazione**</span><span class="sxs-lookup"><span data-stu-id="ec458-178">**Create the configuration file**</span></span>

 <span data-ttu-id="ec458-179">Lo script di distribuzione di HPC Pack IaaS usa come input un file di configurazione XML che descrive l'infrastruttura del cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="ec458-179">The HPC Pack IaaS deployment script uses an XML configuration file as input that describes the infrastructure of the HPC cluster.</span></span> <span data-ttu-id="ec458-180">Per distribuire un cluster costituito da un nodo head e 18 nodi di calcolo creati dall'immagine del nodo di calcolo che include Microsoft Excel, sostituire i valori per il proprio ambiente nel file di configurazione di esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ec458-180">To deploy a cluster consisting of a head node and 18 compute nodes created from the compute node image that includes Microsoft Excel, substitute values for your environment into the following sample configuration file.</span></span> <span data-ttu-id="ec458-181">Per altre informazioni sul file di configurazione, vedere il file Manual.rtf nella cartella dello script e l'articolo relativo alla [creazione di un cluster HPC con lo script di distribuzione IaaS di HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ec458-181">For more information about the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="ec458-182">**Note sul file di configurazione**</span><span class="sxs-lookup"><span data-stu-id="ec458-182">**Notes about the configuration file**</span></span>

* <span data-ttu-id="ec458-183">Il valore di **VMName** del nodo head **DEVE** essere identico al valore di **ServiceName**. In caso contrario non è possibile eseguire i processi SOA.</span><span class="sxs-lookup"><span data-stu-id="ec458-183">The **VMName** of the head node **MUST** be the same as the **ServiceName**, or SOA jobs fail to run.</span></span>
* <span data-ttu-id="ec458-184">Assicurarsi di specificare **EnableWebPortal** per consentire la generazione e l'esportazione del certificato del nodo head.</span><span class="sxs-lookup"><span data-stu-id="ec458-184">Make sure you specify **EnableWebPortal** so that the head node certificate is generated and exported.</span></span>
* <span data-ttu-id="ec458-185">Il file specifica lo script PowerShell post-configurazione PostConfig.ps1 eseguito nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="ec458-185">The file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on the head node.</span></span> <span data-ttu-id="ec458-186">Lo script di esempio seguente consente di configurare la stringa di connessione dell'archiviazione di Azure, rimuovere il ruolo del nodo di calcolo dal nodo head e portare online tutti i nodi distribuiti.</span><span class="sxs-lookup"><span data-stu-id="ec458-186">THe following sample script configures the Azure storage connection string, removes the compute node role from the head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add the HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set the Azure storage connection string for the cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove the compute node role for head node to make sure the Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in the deployment including the head node and compute nodes, which should match the number specified in the XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="ec458-187">**Esecuzione dello script**</span><span class="sxs-lookup"><span data-stu-id="ec458-187">**Run the script**</span></span>

1. <span data-ttu-id="ec458-188">Aprire la console di PowerShell nel computer client come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ec458-188">Open the PowerShell console on the client computer as an administrator.</span></span>
2. <span data-ttu-id="ec458-189">Passare alla cartella dello script (E:\IaaSClusterScript in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="ec458-189">Change directory to the script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="ec458-190">Per distribuire il cluster HPC Pack, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="ec458-190">To deploy the HPC Pack cluster, run the following command.</span></span> <span data-ttu-id="ec458-191">In questo esempio si presuppone che il file di configurazione si trovi in E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="ec458-191">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="ec458-192">Per qualche istante viene eseguito lo script di distribuzione di HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ec458-192">The HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="ec458-193">Con l'esecuzione dello script, il certificato del cluster viene esportato, scaricato e salvato nell'attuale cartella Documenti dell'utente sul computer client.</span><span class="sxs-lookup"><span data-stu-id="ec458-193">One thing the script does is to export and download the cluster certificate and save it in the current user’s Documents folder on the client computer.</span></span> <span data-ttu-id="ec458-194">Lo script genera un messaggio simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="ec458-194">The script generates a message similar to the following.</span></span> <span data-ttu-id="ec458-195">In un passaggio successivo, il certificato viene importato nell'archivio certificati appropriato.</span><span class="sxs-lookup"><span data-stu-id="ec458-195">In a following step, you import the certificate in the appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import the following certificate in the Trusted Root Certification Authorities certificate store on the computer where you are submitting job or accessing the HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="ec458-196">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="ec458-196">Step 2.</span></span> <span data-ttu-id="ec458-197">Offload di cartelle di lavoro di Excel ed esecuzione di funzioni definite dall'utente da un client locale</span><span class="sxs-lookup"><span data-stu-id="ec458-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="ec458-198">Attivazione di Excel</span><span class="sxs-lookup"><span data-stu-id="ec458-198">Excel activation</span></span>
<span data-ttu-id="ec458-199">Quando si usa l'immagine di VM ComputeNodeWithExcel per carichi di lavoro di produzione, per attivare Excel per i nodi di calcolo è necessario disporre di un codice di licenza di Microsoft Office valido.</span><span class="sxs-lookup"><span data-stu-id="ec458-199">When using the ComputeNodeWithExcel VM image for production workloads, you need to provide a valid Microsoft Office license key to activate Excel on the compute nodes.</span></span> <span data-ttu-id="ec458-200">In caso contrario, la versione di valutazione di Excel scade dopo 30 giorni e l'esecuzione delle cartelle di lavoro di Excel restituisce l'errore COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="ec458-200">Otherwise, the evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with the COMException (0x800AC472).</span></span> 

<span data-ttu-id="ec458-201">Il periodo di prova di Excel può essere riattivato per altri 30 giorni. Per farlo, accedere al nodo head e usare clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` per tutti i nodi di calcolo di Excel tramite Gestione cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="ec458-201">You can rearm Excel for another 30 days of evaluation time: Log on to the head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="ec458-202">La riattivazione del periodo di prova può avvenire al massimo due volte.</span><span class="sxs-lookup"><span data-stu-id="ec458-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="ec458-203">Successivamente occorre fornire un codice di licenza di Office valido.</span><span class="sxs-lookup"><span data-stu-id="ec458-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="ec458-204">Il pacchetto Office Professional Plus 2013 installato nell'immagine VM è un'edizione di volume con un codice Product Key generico per contratti multilicenza.</span><span class="sxs-lookup"><span data-stu-id="ec458-204">The Office Professional Plus 2013 installed on the VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="ec458-205">Per attivarla, è possibile usare il Servizio di gestione delle chiavi, l'attivazione basata su Active Directory o il codice ad attivazione multipla.</span><span class="sxs-lookup"><span data-stu-id="ec458-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="ec458-206">Per usare KMS/AD-BA, usare un server KMS esistente oppure configurarne uno nuovo con Microsoft Office 2013 Volume License Pack.</span><span class="sxs-lookup"><span data-stu-id="ec458-206">To use KMS/AD-BA, use an existing KMS server or set up a new one by using the Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="ec458-207">Se lo si desidera, è possibile configurare il server nel nodo head. Quindi, attivare il codice Product Key host KMS tramite Internet o telefono.</span><span class="sxs-lookup"><span data-stu-id="ec458-207">(If you want to, set up the server on the head node.) Then, activate the KMS host key via the Internet or telephone.</span></span> <span data-ttu-id="ec458-208">Quindi usare clusrun `ospp.vbs` per impostare il server e la porta KMS e attivare Office per tutti nodi di calcolo di Excel.</span><span class="sxs-lookup"><span data-stu-id="ec458-208">Then clusrun `ospp.vbs` to set the KMS server and port and activate Office on all the Excel compute nodes.</span></span> 

    * <span data-ttu-id="ec458-209">Per usare MAK, usare prima clusrun `ospp.vbs` per immettere il codice e quindi attivare tutti i nodi di calcolo di Excel tramite Internet o telefono.</span><span class="sxs-lookup"><span data-stu-id="ec458-209">To use MAK, first clusrun `ospp.vbs` to input the key and then activate all the Excel compute nodes via the Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="ec458-210">Con questa immagine di VM non è possibile usare codici Product Key di Office Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="ec458-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="ec458-211">Se si dispone di codici e supporti di installazione validi per edizioni di Office o Excel diverse dall'edizione multilicenza di Office Professional Plus 2013, è possibile usarli in alternativa.</span><span class="sxs-lookup"><span data-stu-id="ec458-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="ec458-212">Disinstallare innanzitutto l'edizione multilicenza, quindi installare l'edizione in proprio possesso.</span><span class="sxs-lookup"><span data-stu-id="ec458-212">First uninstall this volume edition and install the edition that you have.</span></span> <span data-ttu-id="ec458-213">Il nodo di calcolo di Excel reinstallato può essere acquisito come immagine di VM personalizzata da usare in una distribuzione su vasta scala.</span><span class="sxs-lookup"><span data-stu-id="ec458-213">The reinstalled Excel compute node can be captured as a customized VM image to use in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="ec458-214">Offload di cartelle di lavoro di Excel</span><span class="sxs-lookup"><span data-stu-id="ec458-214">Offload Excel workbooks</span></span>
<span data-ttu-id="ec458-215">Per eseguire l'offload di una cartella di lavoro di Excel in modo da eseguirla nel cluster HPC Pack in Azure, attenersi alla procedura riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="ec458-215">Follow these steps to offload an Excel workbook so that it runs on the HPC Pack cluster in Azure.</span></span> <span data-ttu-id="ec458-216">A tale scopo, è necessario disporre di Excel 2010 o 2013 già installato nel computer client.</span><span class="sxs-lookup"><span data-stu-id="ec458-216">To do this, you must have Excel 2010 or 2013 already installed on the client computer.</span></span>

1. <span data-ttu-id="ec458-217">Usare una delle opzioni illustrate nel Passaggio 1 per distribuire un cluster HPC Pack con l'immagine del nodo di calcolo di Excel.</span><span class="sxs-lookup"><span data-stu-id="ec458-217">Use one of the options in Step 1 to deploy an HPC Pack cluster with the Excel compute node image.</span></span> <span data-ttu-id="ec458-218">Ottenere il file del certificato del cluster (con estensione cer) e nome utente e password del cluster.</span><span class="sxs-lookup"><span data-stu-id="ec458-218">Obtain the cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="ec458-219">Nel computer client, importare il certificato del cluster in Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="ec458-219">On the client computer, import the cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="ec458-220">Verificare che Excel sia installato.</span><span class="sxs-lookup"><span data-stu-id="ec458-220">Make sure Excel is installed.</span></span> <span data-ttu-id="ec458-221">Creare un file Excel.exe.config con i seguenti contenuti nella stessa cartella di Excel.exe del computer client.</span><span class="sxs-lookup"><span data-stu-id="ec458-221">Create an Excel.exe.config file with the following contents in the same folder as Excel.exe on the client computer.</span></span> <span data-ttu-id="ec458-222">Così facendo, il componente aggiuntivo di HPC Pack 2012 R2 Excel COM viene caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="ec458-222">This step ensures that the HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="ec458-223">Configurare il client per l'invio di processi al cluster di HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ec458-223">Set up the client to submit jobs to the HPC Pack cluster.</span></span> <span data-ttu-id="ec458-224">Per farlo, è possibile scaricare [HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) e installare il client di HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ec458-224">One option is to download the full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install the HPC Pack client.</span></span> <span data-ttu-id="ec458-225">In alternativa, scaricare e installare le utilità client [HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) e il file ridistribuibile di Visual C++ 2010 appropriato per il computer in uso ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="ec458-225">Alternatively, download and install the [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and the appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="ec458-226">In questo esempio viene usata una cartella di lavoro di Excel di esempio denominata ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="ec458-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="ec458-227">È possibile scaricarlo [qui](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="ec458-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="ec458-228">Copiare la cartella di lavoro di Excel in una cartella di lavoro, ad esempio D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="ec458-228">Copy the Excel workbook to a working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="ec458-229">Aprire la cartella di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="ec458-229">Open the Excel workbook.</span></span> <span data-ttu-id="ec458-230">Nella barra multifunzione **Sviluppo** fare clic su **COM Add-Ins** e verificare che il componente aggiuntivo HPC Pack Excel COM venga caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="ec458-230">On the **Develop** ribbon, click **COM Add-Ins** and confirm that the HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Componente aggiuntivo Excel per HPC Pack][addin]
8. <span data-ttu-id="ec458-232">Modificare la macro VBA HPCControlMacros in Excel cambiando le righe commentate, come illustrato nello script seguente.</span><span class="sxs-lookup"><span data-stu-id="ec458-232">Edit the VBA macro HPCControlMacros in Excel by changing the commented lines as shown in the following script.</span></span> <span data-ttu-id="ec458-233">Sostituire con i valori appropriati per il proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="ec458-233">Substitute appropriate values for your environment.</span></span>
   
   ![Macro Excel per HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="ec458-235">Copiare la cartella di lavoro di Excel in una directory di caricamento, ad esempio D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="ec458-235">Copy the Excel workbook to an upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="ec458-236">Questa directory viene specificata nella costante HPC_DependsFiles della macro VBA.</span><span class="sxs-lookup"><span data-stu-id="ec458-236">This directory is specified in the HPC_DependsFiles constant in the VBA macro.</span></span>
10. <span data-ttu-id="ec458-237">Per eseguire la cartella di lavoro nel cluster di Azure, fare clic sul pulsante **Cluster** nel foglio di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ec458-237">To run the workbook on the cluster in Azure, click the **Cluster** button on the worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="ec458-238">Esecuzione delle funzioni definite dall'utente di Excel</span><span class="sxs-lookup"><span data-stu-id="ec458-238">Run Excel UDFs</span></span>
<span data-ttu-id="ec458-239">Per eseguire funzioni definite dall'utente di Excel, seguire i passaggi da 1 a 3 della precedente configurazione del computer client.</span><span class="sxs-lookup"><span data-stu-id="ec458-239">To run Excel UDFs, follow the preceding steps 1 – 3 to set up the client computer.</span></span> <span data-ttu-id="ec458-240">Per le funzioni UDF di Excel, non è necessario che l'applicazione di Excel sia installata nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ec458-240">For Excel UDFs, you don't need to have the Excel application installed on compute nodes.</span></span> <span data-ttu-id="ec458-241">Pertanto, quando si creano i nodi di calcolo del cluster, è possibile scegliere un'immagine del nodo di calcolo normale, anziché l'immagine del nodo di calcolo con Excel.</span><span class="sxs-lookup"><span data-stu-id="ec458-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of the compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="ec458-242">Esiste un limite di 34 caratteri nella finestra di dialogo del connettore del cluster di Excel 2010 e 2013.</span><span class="sxs-lookup"><span data-stu-id="ec458-242">There is a 34 character limit in the Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="ec458-243">Usare questa finestra di dialogo per specificare il cluster che esegue le funzioni UDF.</span><span class="sxs-lookup"><span data-stu-id="ec458-243">You use this dialog box to specify the cluster that runs the UDFs.</span></span> <span data-ttu-id="ec458-244">Se il nome completo del cluster è più lungo, ad esempio hpcexcelhn01.southeastasia.cloudapp.azure.com, lo spazio disponibile nella finestra di dialogo non sarà sufficiente.</span><span class="sxs-lookup"><span data-stu-id="ec458-244">If the full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in the dialog box.</span></span> <span data-ttu-id="ec458-245">La soluzione alternativa consiste nell'impostare una variabile a livello di computer, ad esempio *CCP_IAASHN* con il valore del nome di cluster lungo.</span><span class="sxs-lookup"><span data-stu-id="ec458-245">The workaround is to set a machine-wide variable such as *CCP_IAASHN* with the value of the long cluster name.</span></span> <span data-ttu-id="ec458-246">Dopodiché, immettere *%CCP_IAASHN%* nella finestra di dialogo come nome del nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="ec458-246">Then, enter *%CCP_IAASHN%* in the dialog box as the cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="ec458-247">Dopo aver correttamente distribuito il cluster, continuare con la procedura seguente per eseguire una funzione definita dall'utente di Excel integrata di esempio.</span><span class="sxs-lookup"><span data-stu-id="ec458-247">After the cluster is successfully deployed, continue with the following steps to run a sample built-in Excel UDF.</span></span> <span data-ttu-id="ec458-248">Per funzioni definite dall'utente di Excel personalizzate, consultare queste [risorse](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) per compilare librerie XLL e distribuirle sul cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="ec458-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) to build the XLLs and deploy them on the IaaS cluster.</span></span>

1. <span data-ttu-id="ec458-249">Aprire una nuova cartella di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="ec458-249">Open a new Excel workbook.</span></span> <span data-ttu-id="ec458-250">Nella barra multifunzione **Sviluppo** fare clic su **Componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="ec458-250">On the **Develop** ribbon, click **Add-Ins**.</span></span> <span data-ttu-id="ec458-251">Quindi, nella finestra di dialogo fare clic su **Sfoglia**, accedere alla cartella %CCP_HOME%Bin\XLL32 e selezionare il ClusterUDF32.xll di esempio.</span><span class="sxs-lookup"><span data-stu-id="ec458-251">Then, in the dialog box, click **Browse**, navigate to the %CCP_HOME%Bin\XLL32 folder, and select the sample ClusterUDF32.xll.</span></span> <span data-ttu-id="ec458-252">Se il ClusterUDF32 non esiste nel computer client, copiarlo dalla cartella %CCP_HOME%Bin\XLL32 nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="ec458-252">If the ClusterUDF32 doesn't exist on the client machine, copy it from the %CCP_HOME%Bin\XLL32 folder on the head node.</span></span>
   
   ![Selezionare la UDF][udf]
2. <span data-ttu-id="ec458-254">Fare clic su **File** > **Opzioni** > **Avanzate**.</span><span class="sxs-lookup"><span data-stu-id="ec458-254">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="ec458-255">In **Formule** selezionare **Allow user-defined XLL functions to run a compute cluster** (Consenti l'esecuzione di funzioni XLL definite dall'utente in un cluster di elaborazione).</span><span class="sxs-lookup"><span data-stu-id="ec458-255">Under **Formulas**, check **Allow user-defined XLL functions to run a compute cluster**.</span></span> <span data-ttu-id="ec458-256">Fare clic su **Opzioni** e immettere il nome completo del cluster in **Nome del nodo head del cluster**.</span><span class="sxs-lookup"><span data-stu-id="ec458-256">Then click **Options** and enter the full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="ec458-257">(Come indicato in precedenza la casella di immissione è limitata a 34 caratteri, pertanto un nome di cluster lungo potrebbe non essere adatto.</span><span class="sxs-lookup"><span data-stu-id="ec458-257">(As noted previously this input box is limited to 34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="ec458-258">Per i nomi di cluster lunghi, è possibile usare una variabile a livello di computer).</span><span class="sxs-lookup"><span data-stu-id="ec458-258">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configurare la UDF][options]
3. <span data-ttu-id="ec458-260">Per eseguire il calcolo della funzione UDF nel cluster, fare clic sulla cella con valore =XllGetComputerNameC() e premere Invio.</span><span class="sxs-lookup"><span data-stu-id="ec458-260">To run the UDF calculation on the cluster, click the cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="ec458-261">La funzione recupera semplicemente il nome del nodo di calcolo in cui viene eseguita la funzione UDF.</span><span class="sxs-lookup"><span data-stu-id="ec458-261">The function simply retrieves the name of the compute node on which the UDF runs.</span></span> <span data-ttu-id="ec458-262">Per la prima esecuzione, una finestra di dialogo per l'immissione delle credenziali richiede nome utente e password per connettersi al cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="ec458-262">For the first run, a credentials dialog box prompts for the username and password to connect to the IaaS cluster.</span></span>
   
   ![Eseguire una UDF][run]
   
   <span data-ttu-id="ec458-264">Quando le celle da elaborare sono molte, premere ALT-MAIUSC-CTRL + F9 per eseguire il calcolo su tutte le celle.</span><span class="sxs-lookup"><span data-stu-id="ec458-264">When there are many cells to calculate, press Alt-Shift-Ctrl + F9 to run the calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="ec458-265">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="ec458-265">Step 3.</span></span> <span data-ttu-id="ec458-266">Esecuzione di un carico di lavoro SOA da un client locale</span><span class="sxs-lookup"><span data-stu-id="ec458-266">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="ec458-267">Per eseguire applicazioni SOA generiche nel cluster IaaS di HPC Pack, distribuire innanzitutto il cluster usando uno dei metodi descritti nel Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="ec458-267">To run general SOA applications on the HPC Pack IaaS cluster, first use one of the methods in Step 1 to deploy the cluster.</span></span> <span data-ttu-id="ec458-268">In questo caso specificare l'immagine di un nodo di calcolo generico, poiché nei nodi di calcolo non è necessario Excel.</span><span class="sxs-lookup"><span data-stu-id="ec458-268">Specify a generic compute node image in this case, because you do not need Excel on the compute nodes.</span></span> <span data-ttu-id="ec458-269">Attenersi quindi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ec458-269">Then follow these steps.</span></span>

1. <span data-ttu-id="ec458-270">Dopo avere recuperato il certificato del cluster, importarlo nel computer client, in Cert:\CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="ec458-270">After retrieving the cluster certificate, import it on the client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="ec458-271">Installare l'[SDK di HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49921) e le [utilità client di HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="ec458-271">Install the [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="ec458-272">Questi strumenti consentono di sviluppare ed eseguire applicazioni client SOA.</span><span class="sxs-lookup"><span data-stu-id="ec458-272">These tools enable you to develop and run SOA client applications.</span></span>
3. <span data-ttu-id="ec458-273">Scaricare il [codice di esempio](https://www.microsoft.com/download/details.aspx?id=41633)HelloWorldR2.</span><span class="sxs-lookup"><span data-stu-id="ec458-273">Download the HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="ec458-274">Aprire HelloWorldR2.sln in Visual Studio 2010 o 2012.</span><span class="sxs-lookup"><span data-stu-id="ec458-274">Open the HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="ec458-275">Questo esempio non è attualmente compatibile con le versioni più recenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec458-275">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="ec458-276">Compilare innanzitutto il progetto EchoService.</span><span class="sxs-lookup"><span data-stu-id="ec458-276">Build the EchoService project first.</span></span> <span data-ttu-id="ec458-277">Dopodiché, distribuire il servizio nel cluster IaaS con le stesse modalità di distribuzione in un cluster locale.</span><span class="sxs-lookup"><span data-stu-id="ec458-277">Then, deploy the service to the IaaS cluster in the same way you deploy to an on-premises cluster.</span></span> <span data-ttu-id="ec458-278">Per informazioni dettagliate, vedere il file Readme.doc in HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="ec458-278">For detailed steps, see the Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="ec458-279">Modificare e compilare HelloWorldR2 e altri progetti come descritto nella sezione seguente per generare le applicazioni client SOA da eseguire in un cluster IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec458-279">Modify and build the HellWorldR2 and other projects as described in the following section to generate the SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="ec458-280">Uso dell'associazione Http con coda di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ec458-280">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="ec458-281">Per usare l'associazione Http con una coda di archiviazione di Azure, apportare alcune modifiche al codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="ec458-281">To use Http binding with an Azure storage queue, make a few changes to the sample code.</span></span>

* <span data-ttu-id="ec458-282">Aggiornare il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="ec458-282">Update the cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="ec458-283">Facoltativamente, usare il nome predefinito TransportScheme in SessionStartInfo o impostarlo in modo esplicito su Http.</span><span class="sxs-lookup"><span data-stu-id="ec458-283">Optionally, use the default TransportScheme in SessionStartInfo or explicitly set it to Http.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="ec458-284">Usare l'associazione predefinita per il BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="ec458-284">Use default binding for the BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="ec458-285">Oppure impostare in modo esplicito usando l'associazione basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="ec458-285">Or set explicitly using the basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="ec458-286">Facoltativamente, impostare il flag UseAzureQueue su true in SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="ec458-286">Optionally, set the UseAzureQueue flag to true in SessionStartInfo.</span></span> <span data-ttu-id="ec458-287">Se non lo si imposta, verrà impostato in modo predefinito su true quando il nome del cluster dispone di suffissi di dominio di Azure e il TransportScheme è Http.</span><span class="sxs-lookup"><span data-stu-id="ec458-287">If not set, it will be set to true by default when the cluster name has Azure domain suffixes and the TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="ec458-288">Uso dell'associazione Http senza coda di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ec458-288">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="ec458-289">Per utilizzare l'associazione Http senza una coda di archiviazione di Azure, in SessionStartInfo impostare in modo esplicito il flag UseAzureQueue su false.</span><span class="sxs-lookup"><span data-stu-id="ec458-289">To use Http binding without an Azure storage queue, explicitly set the UseAzureQueue flag to false in the SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="ec458-290">Uso dell'associazione NetTcp</span><span class="sxs-lookup"><span data-stu-id="ec458-290">Use NetTcp binding</span></span>
<span data-ttu-id="ec458-291">Per usare l'associazione NetTcp, la configurazione è simile alla connessione a un cluster locale.</span><span class="sxs-lookup"><span data-stu-id="ec458-291">To use NetTcp binding, the configuration is similar to connecting to an on-premises cluster.</span></span> <span data-ttu-id="ec458-292">È necessario aprire alcuni endpoint nella VM del nodo head.</span><span class="sxs-lookup"><span data-stu-id="ec458-292">You need to open a few endpoints on the head node VM.</span></span> <span data-ttu-id="ec458-293">Se ad esempio è stato usato lo script di distribuzione IaaS di HPC Pack per creare il cluster, impostare gli endpoint nel portale di Azure come di seguito descritto.</span><span class="sxs-lookup"><span data-stu-id="ec458-293">If you used the HPC Pack IaaS deployment script to create the cluster, for example, set the endpoints in the Azure portal as follows.</span></span>

1. <span data-ttu-id="ec458-294">Arrestare la VM.</span><span class="sxs-lookup"><span data-stu-id="ec458-294">Stop the VM.</span></span>
2. <span data-ttu-id="ec458-295">Aggiungere le porte TCP 9090, 9087, 9091, 9094 rispettivamente per Sessione, Broker, Broker worker e Servizi dati</span><span class="sxs-lookup"><span data-stu-id="ec458-295">Add the TCP ports 9090, 9087, 9091, 9094 for the Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configurare gli endpoint][endpoint-new-portal]
3. <span data-ttu-id="ec458-297">Avviare la VM.</span><span class="sxs-lookup"><span data-stu-id="ec458-297">Start the VM.</span></span>

<span data-ttu-id="ec458-298">L'applicazione client SOA non richiede alcuna modifica, ad eccezione della modifica al nome head per il nome completo del cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="ec458-298">The SOA client application requires no changes except altering the head name to the IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec458-299">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ec458-299">Next steps</span></span>
* <span data-ttu-id="ec458-300">Per altre informazioni sull'esecuzione di carichi di lavoro di Excel con HPC Pack, vedere [queste risorse](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ec458-300">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="ec458-301">Vedere l'articolo relativo alla [gestione dei servizi SOA in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) per altre informazioni sulla distribuzione e sulla gestione dei servizi SOA con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ec458-301">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
