---
title: aaaHPC Pack del cluster per Excel e SOA | Documenti Microsoft
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
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="f6200-103">Introduzione all'esecuzione di carichi di lavoro Excel e SOA in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="f6200-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="f6200-104">Questo articolo illustra come cluster toodeploy Microsoft HPC Pack 2012 R2 in macchine virtuali di Azure utilizzando un modello di avvio rapido di Azure o, facoltativamente, uno script di distribuzione di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6200-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="f6200-105">cluster Hello utilizza toorun progettate immagini di macchina virtuale di Azure Marketplace Microsoft Excel o i carichi di lavoro di architettura orientata ai servizi (SOA) con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="f6200-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="f6200-106">È possibile utilizzare hello toorun di cluster HPC di Excel e di servizi SOA da un computer client locale.</span><span class="sxs-lookup"><span data-stu-id="f6200-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="f6200-107">servizi di HPC Excel Hello includono offload cartella di lavoro di Excel e funzioni definite dall'utente di Excel o funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="f6200-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f6200-108">Questo articolo si basa su funzionalità, modelli e script per HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="f6200-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="f6200-109">Questo scenario non è attualmente supportato in HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="f6200-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f6200-110">In generale, hello diagramma seguente mostra cluster HPC Pack hello create.</span><span class="sxs-lookup"><span data-stu-id="f6200-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Cluster HPC con nodi che eseguono carichi di lavoro di Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="f6200-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f6200-112">Prerequisites</span></span>
* <span data-ttu-id="f6200-113">**Computer client** -è necessario un cluster di toohello processi basati su Windows client computer toosubmit esempio SOA ed Excel.</span><span class="sxs-lookup"><span data-stu-id="f6200-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="f6200-114">È necessario anche un hello toorun computer di Windows Azure PowerShell script di distribuzione di cluster (se si sceglie il metodo di distribuzione).</span><span class="sxs-lookup"><span data-stu-id="f6200-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="f6200-115">**Sottoscrizione di Azure** : se non è disponibile una sottoscrizione di Azure, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="f6200-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="f6200-116">**Quota di core** -potrebbe essere necessario quota hello tooincrease di core, soprattutto se si distribuiscono più nodi del cluster con dimensioni delle macchine Virtuali multicore.</span><span class="sxs-lookup"><span data-stu-id="f6200-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="f6200-117">Se si utilizza un modello di avvio rapido di Azure, la quota di core hello in Gestione risorse è per ogni area di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6200-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="f6200-118">In tal caso, si potrebbe essere necessario quota hello tooincrease in un'area specifica.</span><span class="sxs-lookup"><span data-stu-id="f6200-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="f6200-119">Vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f6200-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="f6200-120">una quota, tooincrease [aprire una richiesta di supporto clienti online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) senza alcun costo.</span><span class="sxs-lookup"><span data-stu-id="f6200-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="f6200-121">**Licenza di Microsoft Office** : se si distribuiscono nodi di calcolo usando un'immagine di VM di HPC Pack 2012 R2 di Marketplace con Microsoft Excel, viene installata una versione di valutazione di Microsoft Excel Professional Plus 2013 di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="f6200-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="f6200-122">Dopo il periodo di valutazione di hello, è necessario tooprovide uno valido Microsoft Office licenza tooactivate Excel toocontinue toorun carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f6200-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="f6200-123">Vedere [Attivazione di Excel](#excel-activation) più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f6200-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="f6200-124">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="f6200-124">Step 1.</span></span> <span data-ttu-id="f6200-125">Configurazione di un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="f6200-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="f6200-126">Vengono illustrati due opzioni tooset di cluster HPC Pack 2012 R2 hello: prima, utilizzando un modello di avvio rapido di Azure e hello portale di Azure quindi, usando uno script di distribuzione di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6200-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="f6200-127">Opzione 1.</span><span class="sxs-lookup"><span data-stu-id="f6200-127">Option 1.</span></span> <span data-ttu-id="f6200-128">Uso di un modello di Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="f6200-128">Use a quickstart template</span></span>
<span data-ttu-id="f6200-129">Utilizzare un tooquickly modello di avvio rapido di Azure di distribuire un cluster HPC Pack nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="f6200-130">Quando si apre il modello di hello nel portale di hello, si ottiene un'interfaccia utente semplice in cui è immettere impostazioni hello per il cluster.</span><span class="sxs-lookup"><span data-stu-id="f6200-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="f6200-131">Ecco i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="f6200-132">È possibile usare un [modello di Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) che crea un cluster simile, specifico per i carichi di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="f6200-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="f6200-133">Hello procedura leggermente diversa dal successivo hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="f6200-134">Visitare hello [pagina modello di creazione del Cluster HPC in GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="f6200-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="f6200-135">Se si desidera, è possibile esaminare informazioni sul modello hello e il codice sorgente hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="f6200-136">Fare clic su **distribuire tooAzure** toostart una distribuzione con il modello di hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6200-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Distribuire tooAzure modello][github]
3. <span data-ttu-id="f6200-138">Nel portale di hello, seguire questi parametri di hello tooenter passaggi per il modello di cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="f6200-139">a.</span><span class="sxs-lookup"><span data-stu-id="f6200-139">a.</span></span> <span data-ttu-id="f6200-140">In hello **parametri** pagina, immettere o modificare i valori per parametri modello hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="f6200-141">(Fare clic su hello icona Avanti tooeach impostazione per le informazioni della Guida). Nella seguente schermata hello vengono visualizzati i valori di esempio.</span><span class="sxs-lookup"><span data-stu-id="f6200-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="f6200-142">Questo esempio viene creato un cluster denominato *hpc01* in hello *hpc.local* dominio costituito da un nodo head e 2 nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="f6200-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="f6200-143">nodi di calcolo Hello vengono creati da un'immagine di macchina virtuale di HPC Pack che include Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="f6200-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Immettere i parametri][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="f6200-145">nodo head di Hello macchina virtuale viene creato automaticamente da hello [più recente immagine del Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) di HPC Pack 2012 R2 in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="f6200-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="f6200-146">Attualmente l'immagine di hello è basato su HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="f6200-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="f6200-147">Macchine virtuali del nodo calcolo vengono create dall'immagine più recente di hello della famiglia di nodo di calcolo hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="f6200-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="f6200-148">Seleziona hello **ComputeNodeWithExcel** opzione hello più recente HPC Pack calcolo nodo immagine che include una versione di valutazione di Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="f6200-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="f6200-149">toodeploy un cluster per le sessioni SOA generale o per l'offload di UDF di Excel, scegliere hello **ComputeNode** opzione (senza Excel installato).</span><span class="sxs-lookup"><span data-stu-id="f6200-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="f6200-150">b.</span><span class="sxs-lookup"><span data-stu-id="f6200-150">b.</span></span> <span data-ttu-id="f6200-151">Scegliere la sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="f6200-152">c.</span><span class="sxs-lookup"><span data-stu-id="f6200-152">c.</span></span> <span data-ttu-id="f6200-153">Creare un gruppo di risorse cluster hello, ad esempio *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="f6200-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="f6200-154">d.</span><span class="sxs-lookup"><span data-stu-id="f6200-154">d.</span></span> <span data-ttu-id="f6200-155">Scegliere un percorso per il gruppo di risorse hello, ad esempio Stati Uniti centrali.</span><span class="sxs-lookup"><span data-stu-id="f6200-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="f6200-156">e.</span><span class="sxs-lookup"><span data-stu-id="f6200-156">e.</span></span> <span data-ttu-id="f6200-157">In hello **legali** pagina, esaminare le condizioni di hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="f6200-158">Se si accettano le condizioni, fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="f6200-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="f6200-159">Quindi, dopo aver impostato i valori hello per modello di hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="f6200-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="f6200-160">Quando viene completata la distribuzione di hello (in genere richiede circa 30 minuti), esportare file del certificato hello cluster dal nodo head del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="f6200-161">Successivamente, importare il certificato pubblico hello client tooprovide hello sul lato server dell'autenticazione del computer per l'associazione HTTP protetta.</span><span class="sxs-lookup"><span data-stu-id="f6200-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="f6200-162">a.</span><span class="sxs-lookup"><span data-stu-id="f6200-162">a.</span></span> <span data-ttu-id="f6200-163">Nel portale di Azure hello, andare toohello dashboard nodo head hello selezionare e fare clic su **Connetti** nella parte superiore di hello di hello pagina tooconnect tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="f6200-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="f6200-164">b.</span><span class="sxs-lookup"><span data-stu-id="f6200-164">b.</span></span> <span data-ttu-id="f6200-165">Usare le procedure standard in Gestione certificati tooexport hello nodo head certificato (che si trova in Cert: \LocalMachine\My) senza chiave privata hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="f6200-166">In questo esempio esportare *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="f6200-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Esportare il certificato di hello][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="f6200-168">Opzione 2.</span><span class="sxs-lookup"><span data-stu-id="f6200-168">Option 2.</span></span> <span data-ttu-id="f6200-169">Utilizzare script di distribuzione IaaS di HPC Pack hello</span><span class="sxs-lookup"><span data-stu-id="f6200-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="f6200-170">script di distribuzione IaaS di HPC Pack Hello fornisce un altro modo versatile toodeploy un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="f6200-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="f6200-171">Viene creato un cluster nel modello di distribuzione classica hello, mentre il modello di hello modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f6200-172">Inoltre, script hello è compatibile con una sottoscrizione in hello Azure globale o il servizio Cina di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6200-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="f6200-173">**Ulteriori prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="f6200-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="f6200-174">**Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.</span><span class="sxs-lookup"><span data-stu-id="f6200-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="f6200-175">**Script di distribuzione IaaS di HPC Pack** : scaricare e decomprimere hello versione dello script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="f6200-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="f6200-176">Controllare la versione di hello dello script di hello eseguendo `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="f6200-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="f6200-177">In questo articolo si basa sulla versione 4.5.0 o successiva di script hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="f6200-178">**Creare il file di configurazione di hello**</span><span class="sxs-lookup"><span data-stu-id="f6200-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="f6200-179">script di distribuzione IaaS di HPC Pack Hello viene utilizzato un file di configurazione XML come input che descrive l'infrastruttura di hello del cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="f6200-180">toodeploy creati dall'immagine di nodo di calcolo hello che include Microsoft Excel, i nodi di calcolo di un cluster costituito da un nodo head e 18 sostituire i valori per l'ambiente in hello seguenti il file di configurazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="f6200-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="f6200-181">Per ulteriori informazioni sul file di configurazione di hello, vedere il file Manual.rtf hello nella cartella script hello e [creare un cluster HPC con lo script di distribuzione IaaS di HPC Pack hello](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6200-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="f6200-182">**Note sul file di configurazione hello**</span><span class="sxs-lookup"><span data-stu-id="f6200-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="f6200-183">Hello **VMName** del nodo head hello **deve** essere hello stesso come hello **ServiceName**, o i processi SOA di esito negativo toorun.</span><span class="sxs-lookup"><span data-stu-id="f6200-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="f6200-184">Assicurarsi di specificare **EnableWebPortal** in modo che hello certificato del nodo head viene generato ed esportato.</span><span class="sxs-lookup"><span data-stu-id="f6200-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="f6200-185">file Hello specifica uno script di PowerShell di post-configurazione PostConfig.ps1 in esecuzione sul nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="f6200-186">Hello lo script di esempio seguente configura stringa di connessione di archiviazione di Azure hello, ruolo del nodo calcolo hello viene rimosso dal nodo head di hello e visualizza tutti i nodi in linea quando vengono distribuiti.</span><span class="sxs-lookup"><span data-stu-id="f6200-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
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

<span data-ttu-id="f6200-187">**Eseguire script hello**</span><span class="sxs-lookup"><span data-stu-id="f6200-187">**Run hello script**</span></span>

1. <span data-ttu-id="f6200-188">Aprire la console di PowerShell hello in computer client hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f6200-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="f6200-189">Modifica directory toohello cartella di script (E:\IaaSClusterScript in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="f6200-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="f6200-190">toodeploy hello HPC Pack cluster esegue hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="f6200-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="f6200-191">Si presuppone che si trova il file di configurazione hello in E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="f6200-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="f6200-192">script di distribuzione di HPC Pack Hello viene eseguito per un certo tempo.</span><span class="sxs-lookup"><span data-stu-id="f6200-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="f6200-193">Uno script di hello cosa esegue è tooexport e scaricare il certificato di cluster hello e salvarla nella cartella documenti dell'utente corrente hello hello client computer.</span><span class="sxs-lookup"><span data-stu-id="f6200-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="f6200-194">script di Hello genera di seguito toohello simile messaggio.</span><span class="sxs-lookup"><span data-stu-id="f6200-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="f6200-195">In un passaggio seguente, importare certificato hello nell'archivio certificati appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="f6200-196">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="f6200-196">Step 2.</span></span> <span data-ttu-id="f6200-197">Offload di cartelle di lavoro di Excel ed esecuzione di funzioni definite dall'utente da un client locale</span><span class="sxs-lookup"><span data-stu-id="f6200-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="f6200-198">Attivazione di Excel</span><span class="sxs-lookup"><span data-stu-id="f6200-198">Excel activation</span></span>
<span data-ttu-id="f6200-199">Quando si usa l'immagine VM ComputeNodeWithExcel hello per carichi di lavoro di produzione, è necessario un valido Microsoft Office licenza chiave tooactivate Excel sui nodi di calcolo hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="f6200-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="f6200-200">In caso contrario, la versione di valutazione hello di Excel scade dopo 30 giorni e in esecuzione le cartelle di lavoro di Excel avrà esito negativo con hello COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="f6200-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="f6200-201">È possibile rearm Excel per altri 30 giorni del periodo di valutazione: accedere al nodo head toohello e clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` su Excel tutti i nodi di calcolo di tramite HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="f6200-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="f6200-202">La riattivazione del periodo di prova può avvenire al massimo due volte.</span><span class="sxs-lookup"><span data-stu-id="f6200-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="f6200-203">Successivamente occorre fornire un codice di licenza di Office valido.</span><span class="sxs-lookup"><span data-stu-id="f6200-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="f6200-204">Hello Office Professional Plus 2013 installato nell'immagine di macchina virtuale hello è un'edizione con contratti multilicenza con una chiave (Multilicenza generico).</span><span class="sxs-lookup"><span data-stu-id="f6200-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="f6200-205">Per attivarla, è possibile usare il Servizio di gestione delle chiavi, l'attivazione basata su Active Directory o il codice ad attivazione multipla.</span><span class="sxs-lookup"><span data-stu-id="f6200-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="f6200-206">toouse AD/KMS-BA, utilizzare un server di gestione delle CHIAVI esistente o configurarne uno nuovo con hello pacchetto licenze Volume di Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="f6200-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="f6200-207">(Se si desidera, è possibile configurare il server di hello nel nodo head di hello.) Quindi, attivare hello codice Product key host tramite hello Internet o telefono.</span><span class="sxs-lookup"><span data-stu-id="f6200-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="f6200-208">Quindi clusrun `ospp.vbs` tooset hello porta e il server di gestione delle CHIAVI e attivare di Office su tutti i nodi di calcolo Excel hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="f6200-209">toouse MAK, clusrun prima `ospp.vbs` tooinput hello chiave e quindi attivare tutti i nodi di calcolo Excel hello tramite hello Internet o telefono.</span><span class="sxs-lookup"><span data-stu-id="f6200-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="f6200-210">Con questa immagine di VM non è possibile usare codici Product Key di Office Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="f6200-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="f6200-211">Se si dispone di codici e supporti di installazione validi per edizioni di Office o Excel diverse dall'edizione multilicenza di Office Professional Plus 2013, è possibile usarli in alternativa.</span><span class="sxs-lookup"><span data-stu-id="f6200-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="f6200-212">Prima disinstallare questa edizione di volume e installare l'edizione hello in uso.</span><span class="sxs-lookup"><span data-stu-id="f6200-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="f6200-213">Hello reinstallato Excel del nodo di calcolo può essere acquisito in un toouse immagine di macchina virtuale personalizzata in una distribuzione su larga scala.</span><span class="sxs-lookup"><span data-stu-id="f6200-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="f6200-214">Offload di cartelle di lavoro di Excel</span><span class="sxs-lookup"><span data-stu-id="f6200-214">Offload Excel workbooks</span></span>
<span data-ttu-id="f6200-215">Seguire questi toooffload passaggi una cartella di lavoro di Excel in modo che venga eseguito nel cluster HPC Pack hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6200-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="f6200-216">toodo, è necessario disporre di Excel 2010 o 2013 già installato nel computer client hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="f6200-217">Utilizzare una delle opzioni di hello nel passaggio 1 toodeploy un cluster HPC Pack con Excel hello immagine del nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="f6200-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="f6200-218">Ottenere hello cluster certificato (. cer) e nome utente del cluster e la password.</span><span class="sxs-lookup"><span data-stu-id="f6200-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="f6200-219">Computer client hello importare certificati cluster hello in Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="f6200-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="f6200-220">Verificare che Excel sia installato.</span><span class="sxs-lookup"><span data-stu-id="f6200-220">Make sure Excel is installed.</span></span> <span data-ttu-id="f6200-221">Creare un file Excel.exe. config con hello seguente contenuto hello stessa cartella Excel.exe nel computer client hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="f6200-222">Questo passaggio garantisce che hello del componente aggiuntivo di HPC Pack 2012 R2 Excel COM viene caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="f6200-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="f6200-223">Configurare il cluster di HPC Pack toohello hello client toosubmit processi.</span><span class="sxs-lookup"><span data-stu-id="f6200-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="f6200-224">Un'opzione è hello toodownload completo [HPC Pack 2012 R2 Update 3 installazione](http://www.microsoft.com/download/details.aspx?id=49922) e installare il client di HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="f6200-225">In alternativa, scaricare e installare hello [utilità client di HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) e hello appropriato Visual C++ 2010 redistributable per il computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="f6200-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="f6200-226">In questo esempio viene usata una cartella di lavoro di Excel di esempio denominata ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="f6200-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="f6200-227">È possibile scaricarlo [qui](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="f6200-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="f6200-228">Copiare hello Excel cartella di lavoro tooa cartella di lavoro, ad esempio D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="f6200-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="f6200-229">Aprire una cartella di lavoro di Excel hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-229">Open hello Excel workbook.</span></span> <span data-ttu-id="f6200-230">In hello **sviluppare** della barra multifunzione, fare clic su **componenti aggiuntivi COM** e verificare che hello HPC Pack Excel componente aggiuntivo viene caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="f6200-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Componente aggiuntivo Excel per HPC Pack][addin]
8. <span data-ttu-id="f6200-232">Le righe di commento macro VBA modifica hello HPCControlMacros in Excel modificando hello come illustrato nell'hello lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="f6200-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="f6200-233">Sostituire con i valori appropriati per il proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="f6200-233">Substitute appropriate values for your environment.</span></span>
   
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
9. <span data-ttu-id="f6200-235">Copiare directory upload tooan hello Excel cartella di lavoro, ad esempio D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="f6200-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="f6200-236">La directory specificata nella costante HPC_DependsFiles hello nella macro VBA hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="f6200-237">cartella di lavoro hello toorun in cluster hello in Azure, fare clic su hello **Cluster** pulsante foglio di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="f6200-238">Esecuzione delle funzioni definite dall'utente di Excel</span><span class="sxs-lookup"><span data-stu-id="f6200-238">Run Excel UDFs</span></span>
<span data-ttu-id="f6200-239">toorun Excel funzioni definite dall'utente, seguire passaggi precedenti, hello tooset 1-3 backup computer client hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="f6200-240">Per funzioni definite dall'utente di Excel, non è necessaria un'applicazione Excel toohave hello installata sui nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="f6200-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="f6200-241">Pertanto, quando si crea il cluster di nodi di calcolo, è possibile scegliere un'immagine del nodo di calcolo normale anziché hello calcolo immagine del nodo con Excel.</span><span class="sxs-lookup"><span data-stu-id="f6200-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="f6200-242">È presente un limite di 34 caratteri in hello Excel 2010 e 2013 cluster connettore finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f6200-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="f6200-243">Utilizzare questa finestra di dialogo casella toospecify hello cluster che esegue hello funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="f6200-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="f6200-244">Se il nome completo del cluster hello è più lungo (ad esempio, hpcexcelhn01.southeastasia.cloudapp.azure.com), non è possibile inserirlo nella finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="f6200-245">Hello soluzione alternativa è tooset una variabile a livello di computer, ad esempio *CCP_IAASHN* con valore hello hello lungo nome di cluster.</span><span class="sxs-lookup"><span data-stu-id="f6200-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="f6200-246">Quindi, immettere *CCP_IAASHN %* nella finestra di dialogo hello come nome del nodo head del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="f6200-247">Dopo la distribuzione di cluster hello è completata, continuare con hello seguendo i passaggi toorun incorporato esempio UDF di Excel.</span><span class="sxs-lookup"><span data-stu-id="f6200-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="f6200-248">Per UDF di Excel personalizzati, vedere questi [risorse](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLL e distribuirli nei cluster IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="f6200-249">Aprire una nuova cartella di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="f6200-249">Open a new Excel workbook.</span></span> <span data-ttu-id="f6200-250">In hello **sviluppare** della barra multifunzione, fare clic su **Add-Ins**. Quindi, nella finestra di dialogo hello, fare clic su **Sfoglia**, passare toohello %CCP_HOME%Bin\XLL32 cartella e selezionare l'esempio hello ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="f6200-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="f6200-251">Se hello ClusterUDF32 non esiste nel computer client hello, copiarlo nella cartella %CCP_HOME%Bin\XLL32 hello nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Selezionare hello funzione definita dall'utente][udf]
2. <span data-ttu-id="f6200-253">Fare clic su **File** > **Opzioni** > **Avanzate**.</span><span class="sxs-lookup"><span data-stu-id="f6200-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="f6200-254">In **formule**, controllare **consentono di un cluster di calcolo definito dall'utente XLL funzioni toorun**.</span><span class="sxs-lookup"><span data-stu-id="f6200-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="f6200-255">Quindi fare clic su **opzioni** e immettere il nome completo del cluster hello in **nome nodo head del Cluster**.</span><span class="sxs-lookup"><span data-stu-id="f6200-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="f6200-256">(Come indicato in precedenza questa casella di input è limitato too34 caratteri, in modo da un nome lungo cluster potrebbe non essere adatto.</span><span class="sxs-lookup"><span data-stu-id="f6200-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="f6200-257">Per i nomi di cluster lunghi, è possibile usare una variabile a livello di computer).</span><span class="sxs-lookup"><span data-stu-id="f6200-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configurare hello funzione definita dall'utente][options]
3. <span data-ttu-id="f6200-259">hello toorun calcolo funzione definita dall'utente nel cluster hello, fare clic su una cella con il valore =XllGetComputerNameC() hello e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="f6200-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="f6200-260">funzione Hello recupera semplicemente il nome di hello del nodo di calcolo hello in cui hello funzione definita dall'utente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f6200-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="f6200-261">Per eseguire prima di hello, una finestra di dialogo credenziali richiede hello nome utente e password tooconnect toohello cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="f6200-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![Eseguire una UDF][run]
   
   <span data-ttu-id="f6200-263">Quando sono presenti molti toocalculate celle, premere Maiusc-Alt-Ctrl + calcolo di hello toorun F9 su tutte le celle.</span><span class="sxs-lookup"><span data-stu-id="f6200-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="f6200-264">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="f6200-264">Step 3.</span></span> <span data-ttu-id="f6200-265">Esecuzione di un carico di lavoro SOA da un client locale</span><span class="sxs-lookup"><span data-stu-id="f6200-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="f6200-266">applicazioni SOA generali toorun cluster IaaS di HPC Pack hello innanzitutto utilizzare uno dei metodi di hello in cluster di hello toodeploy passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="f6200-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="f6200-267">Specificare un'immagine di un nodo di calcolo generico in questo caso, poiché non è necessario Excel sui nodi di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="f6200-268">Attenersi quindi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f6200-268">Then follow these steps.</span></span>

1. <span data-ttu-id="f6200-269">Dopo aver recuperato il certificato di cluster hello, importarlo nel computer client hello in Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="f6200-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="f6200-270">Installare hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) e [utilità client di HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="f6200-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="f6200-271">Questi strumenti consentono di toodevelop ed eseguono applicazioni SOA.</span><span class="sxs-lookup"><span data-stu-id="f6200-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="f6200-272">Scaricare hello HelloWorldR2 [codice di esempio](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="f6200-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="f6200-273">Aprire hello HelloWorldR2.sln in Visual Studio 2010 o 2012.</span><span class="sxs-lookup"><span data-stu-id="f6200-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="f6200-274">Questo esempio non è attualmente compatibile con le versioni più recenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6200-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="f6200-275">Prima di compilazione progetto EchoService hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-275">Build hello EchoService project first.</span></span> <span data-ttu-id="f6200-276">Quindi, distribuire cluster IaaS di hello servizio toohello in hello stesso modo in cui si distribuiscono tooan locale del cluster.</span><span class="sxs-lookup"><span data-stu-id="f6200-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="f6200-277">Per informazioni dettagliate, vedere hello Readme in HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="f6200-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="f6200-278">Modificare e compilare hello HellWorldR2 e da altri progetti, come descritto nella seguente sezione toogenerate hello SOA applicazioni client eseguite in un cluster IaaS di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="f6200-279">Uso dell'associazione Http con coda di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f6200-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="f6200-280">associazione Http toouse con una coda di archiviazione di Azure, apportare alcune modifiche toohello codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="f6200-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="f6200-281">Aggiornare il nome del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="f6200-282">Facoltativamente, utilizzare predefinito hello TransportScheme SessionStartInfo o impostare in modo esplicito tooHttp.</span><span class="sxs-lookup"><span data-stu-id="f6200-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="f6200-283">Utilizzare l'associazione predefinita per hello BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="f6200-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="f6200-284">O impostare in modo esplicito utilizzando basicHttpBinding hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="f6200-285">Facoltativamente, impostare hello UseAzureQueue flag tootrue in SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="f6200-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="f6200-286">Se non impostato, verrà impostato tootrue per impostazione predefinita quando il nome del cluster hello suffissi di dominio di Azure e hello TransportScheme è Http.</span><span class="sxs-lookup"><span data-stu-id="f6200-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="f6200-287">Uso dell'associazione Http senza coda di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f6200-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="f6200-288">associazione Http toouse senza una coda di archiviazione di Azure, in modo esplicito set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="f6200-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="f6200-289">Uso dell'associazione NetTcp</span><span class="sxs-lookup"><span data-stu-id="f6200-289">Use NetTcp binding</span></span>
<span data-ttu-id="f6200-290">toouse NetTcp associazione configurazione hello è cluster locale di simili tooconnecting tooan.</span><span class="sxs-lookup"><span data-stu-id="f6200-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="f6200-291">È necessario tooopen alcuni endpoint nella macchina virtuale del nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="f6200-292">Se si utilizza del cluster di hello toocreate hello IaaS di HPC Pack distribuzione script, ad esempio, set di endpoint hello in hello portale di Azure come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f6200-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="f6200-293">Arrestare VM hello.</span><span class="sxs-lookup"><span data-stu-id="f6200-293">Stop hello VM.</span></span>
2. <span data-ttu-id="f6200-294">Aggiungere le porte TCP hello 9090, 9087, 9091, 9094 per sessione, hello Broker, rispettivamente di Service Broker worker e servizi di dati,</span><span class="sxs-lookup"><span data-stu-id="f6200-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configurare gli endpoint][endpoint-new-portal]
3. <span data-ttu-id="f6200-296">Avviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6200-296">Start hello VM.</span></span>

<span data-ttu-id="f6200-297">applicazione client SOA Hello è necessario apportare alcuna modifica, ad eccezione di modifica hello head toohello IaaS completa nome cluster.</span><span class="sxs-lookup"><span data-stu-id="f6200-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6200-298">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6200-298">Next steps</span></span>
* <span data-ttu-id="f6200-299">Per altre informazioni sull'esecuzione di carichi di lavoro di Excel con HPC Pack, vedere [queste risorse](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f6200-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="f6200-300">Vedere l'articolo relativo alla [gestione dei servizi SOA in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) per altre informazioni sulla distribuzione e sulla gestione dei servizi SOA con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="f6200-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

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
