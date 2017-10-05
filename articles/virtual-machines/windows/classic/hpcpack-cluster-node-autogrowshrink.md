---
title: "Scalabilità automatica dei nodi di calcolo del cluster HPC Pack | Microsoft Docs"
description: Aumentare e ridurre automaticamente il numero di nodi di calcolo del cluster HPC Pack in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0dc0d15c64d8951c3c457df73588c37418a3c8a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-grow-and-shrink-the-hpc-pack-cluster-resources-in-azure-according-to-the-cluster-workload"></a><span data-ttu-id="8f59d-103">Aumentare e ridurre automaticamente le risorse del cluster HPC Pack in Azure in base al carico di lavoro del cluster</span><span class="sxs-lookup"><span data-stu-id="8f59d-103">Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload</span></span>
<span data-ttu-id="8f59d-104">Se si distribuiscono nodi "burst" di Azure nel cluster HPC Pack o si crea un cluster HPC Pack nelle macchine virtuali di Azure, può essere necessario avere a disposizione un modo per aumentare o ridurre automaticamente le risorse del cluster di Azure, ad esempio i nodi o core, in base al carico di lavoro del cluster.</span><span class="sxs-lookup"><span data-stu-id="8f59d-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink the cluster resources such as nodes or cores according to the workload on the cluster.</span></span> <span data-ttu-id="8f59d-105">Ridimensionando le risorse del cluster in questo modo, è possibile usare le risorse di Azure in modo più efficiente e controllare i costi.</span><span class="sxs-lookup"><span data-stu-id="8f59d-105">Scaling the cluster resources in this way allows you to use your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="8f59d-106">Questo articolo illustra due modalità offerte da HPC Pack per la scalabilità automatica delle risorse di calcolo:</span><span class="sxs-lookup"><span data-stu-id="8f59d-106">This article shows you two ways that HPC Pack provides to autoscale compute resources:</span></span>

* <span data-ttu-id="8f59d-107">Proprietà del cluster HPC Pack **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8f59d-107">The HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="8f59d-108">Script di HPC PowerShell **AzureAutoGrowShrink.ps1**</span><span class="sxs-lookup"><span data-stu-id="8f59d-108">The **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8f59d-109">Attualmente è possibile solo aumentare e ridurre automaticamente i nodi di calcolo HPC Pack che eseguono un sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8f59d-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-the-autogrowshrink-cluster-property"></a><span data-ttu-id="8f59d-110">Impostare la proprietà del cluster AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="8f59d-110">Set the AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="8f59d-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8f59d-111">Prerequisites</span></span>

* <span data-ttu-id="8f59d-112">**Cluster HPC Pack 2012 R2 Update 2 o versione successiva** : il nodo head del cluster può essere distribuito in locale o in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-112">**HPC Pack 2012 R2 Update 2 or later cluster** - The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="8f59d-113">Vedere [Configurare un cluster ibrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) per iniziare con un nodo head locale e i nodi "burst" di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="8f59d-114">Vedere lo [script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md) per distribuire velocemente un cluster HPC Pack in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-114">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="8f59d-115">**Per un cluster con un nodo head in Azure (modello di distribuzione di Resource Manager)**: a partire da HPC Pack 2016, l'autenticazione del certificato in un'applicazione Azure Active Directory viene usata per aumentare o ridurre automaticamente le macchine virtuali del cluster distribuite tramite Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8f59d-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="8f59d-116">Configurare un certificato come segue:</span><span class="sxs-lookup"><span data-stu-id="8f59d-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="8f59d-117">Dopo la distribuzione del cluster, connettersi a un solo nodo head da desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="8f59d-117">After cluster deployment, connect by Remote Desktop to one head node.</span></span>

  2. <span data-ttu-id="8f59d-118">Caricare il certificato (formato PFX con chiave privata) su ogni nodo head e installarlo in Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="8f59d-118">Upload the certificate (PFX format with private key) to each head node and install to Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="8f59d-119">Avviare Azure PowerShell come amministratore ed eseguire i comandi seguenti in un nodo head:</span><span class="sxs-lookup"><span data-stu-id="8f59d-119">Start Azure PowerShell as an administrator and run the following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="8f59d-120">Se l'account si trova in più di un tenant di Azure Active Directory o in più sottoscrizioni di Azure, è possibile eseguire il comando seguente per selezionare il tenant e la sottoscrizione corretti:</span><span class="sxs-lookup"><span data-stu-id="8f59d-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run the following command to select the correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="8f59d-121">Eseguire questo comando per visualizzare il tenant e la sottoscrizione attualmente selezionati:</span><span class="sxs-lookup"><span data-stu-id="8f59d-121">Run the following command to view the currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="8f59d-122">Eseguire lo script seguente</span><span class="sxs-lookup"><span data-stu-id="8f59d-122">Run the following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="8f59d-123">dove</span><span class="sxs-lookup"><span data-stu-id="8f59d-123">where</span></span>

    <span data-ttu-id="8f59d-124">**DisplayName**: nome visualizzato dell'applicazione Azure Active.</span><span class="sxs-lookup"><span data-stu-id="8f59d-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="8f59d-125">Se l'applicazione non esiste, viene creata in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f59d-125">If the application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="8f59d-126">**Home page**: home page dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f59d-126">**HomePage** - The home page of the application.</span></span> <span data-ttu-id="8f59d-127">È possibile configurare un URL fittizio, come nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="8f59d-127">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="8f59d-128">**IdentifierUri**: identificatore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f59d-128">**IdentifierUri** - Identifier of the application.</span></span> <span data-ttu-id="8f59d-129">È possibile configurare un URL fittizio, come nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="8f59d-129">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="8f59d-130">**CertificateThumbprint**: identificazione personale del certificato installato nel nodo head nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="8f59d-130">**CertificateThumbprint** - Thumbprint of the certificate you installed on the head node in Step 1.</span></span>

    <span data-ttu-id="8f59d-131">**TenantId**: ID tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f59d-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="8f59d-132">È possibile ottenere l'ID tenant dalla pagina **Proprietà** del portale di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f59d-132">You can get the Tenant ID from the Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="8f59d-133">Per altre informazioni su **ConfigARMAutoGrowShrinkCert.ps1**, eseguire `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="8f59d-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="8f59d-134">**Per un cluster con un nodo head in Azure (modello di distribuzione classica)** se usa lo script di distribuzione IaaS di HPC Pack per creare il cluster nel modello di distribuzione classica, abilitare la proprietà del cluster **AutoGrowShrink** impostando l'opzione AutoGrowShrink nel file di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="8f59d-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use the HPC Pack IaaS deployment script to create the cluster in the classic deployment model, enable the **AutoGrowShrink** cluster property by setting the AutoGrowShrink option in the cluster configuration file.</span></span> <span data-ttu-id="8f59d-135">Per informazioni dettagliate, vedere la documentazione che accompagna il [download dello script](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="8f59d-135">For details, see the documentation accompanying the [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="8f59d-136">In alternativa, abilitare la proprietà del cluster **AutoGrowShrink** dopo aver distribuito il cluster con i comandi di HPC PowerShell descritti nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="8f59d-136">Alternatively, enable the **AutoGrowShrink** cluster property after you deploy the cluster by using HPC PowerShell commands described in the following section.</span></span> <span data-ttu-id="8f59d-137">Per prepararsi, completare prima i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f59d-137">To prepare for this, first complete the following steps:</span></span>

  1. <span data-ttu-id="8f59d-138">Configurare un certificato di gestione di Azure nel nodo head e nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-138">Configure an Azure management certificate on the head node and in the Azure subscription.</span></span> <span data-ttu-id="8f59d-139">Per una distribuzione di prova, è possibile usare il certificato autofirmato Microsoft HPC Azure predefinito che consente di installare HPC Pack nel nodo head e quindi caricare il certificato nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-139">For a test deployment, you can use the Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on the head node, and then upload that certificate to your Azure subscription.</span></span> <span data-ttu-id="8f59d-140">Per le opzioni e i passaggi, vedere le [informazioni aggiuntive nella libreria TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f59d-140">For options and steps, see the [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="8f59d-141">Eseguire **regedit** nel nodo head, passare a HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo e aggiungere un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="8f59d-141">Run **regedit** on the head node, go to HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="8f59d-142">Impostare il nome valore su "Identificazione personale" e dati valore sull'identificazione personale del certificato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="8f59d-142">Set the Value name to “ThumbPrint”, and Value data to the thumbprint of the certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-to-set-the-autogrowshrink-property"></a><span data-ttu-id="8f59d-143">Comandi di HPC PowerShell per impostare la proprietà AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="8f59d-143">HPC PowerShell commands to set the AutoGrowShrink property</span></span>
<span data-ttu-id="8f59d-144">Di seguito sono riportati i comandi di HPC PowerShell di esempio per impostare **AutoGrowShrink** e ottimizzare il comportamento con parametri aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="8f59d-144">Following are sample HPC PowerShell commands to set **AutoGrowShrink** and to tune its behavior with additional parameters.</span></span> <span data-ttu-id="8f59d-145">Vedere [Parametri di AutoGrowShrink](#AutoGrowShrink-parameters) più avanti in questo articolo per l'elenco completo delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="8f59d-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for the complete list of settings.</span></span>

<span data-ttu-id="8f59d-146">Per eseguire questi comandi, avviare HPC PowerShell nel nodo head del cluster come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8f59d-146">To run these commands, start HPC PowerShell on the cluster head node as an administrator.</span></span>

<span data-ttu-id="8f59d-147">**Per abilitare la proprietà AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8f59d-147">**To enable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="8f59d-148">**Per disabilitare la proprietà AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8f59d-148">**To disable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="8f59d-149">**Per modificare l'intervallo di aumento in minuti**</span><span class="sxs-lookup"><span data-stu-id="8f59d-149">**To change the grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="8f59d-150">**Per modificare l'intervallo di riduzione in minuti**</span><span class="sxs-lookup"><span data-stu-id="8f59d-150">**To change the shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="8f59d-151">**Per visualizzare la configurazione corrente di AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8f59d-151">**To view the current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="8f59d-152">**Per escludere i gruppi di nodi da AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8f59d-152">**To exclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="8f59d-153">Questo parametro è supportato a partire da HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="8f59d-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="8f59d-154">Parametri di AutoGrowShrink </span><span class="sxs-lookup"><span data-stu-id="8f59d-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="8f59d-155">Di seguito sono riportati i parametri di AutoGrowShrink che è possibile modificare tramite il comando **Set HpcClusterProperty** .</span><span class="sxs-lookup"><span data-stu-id="8f59d-155">The following are AutoGrowShrink parameters that you can modify by using the **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="8f59d-156">**EnableGrowShrink**: opzione per abilitare o disabilitare la proprietà **AutoGrowShrink**.</span><span class="sxs-lookup"><span data-stu-id="8f59d-156">**EnableGrowShrink** - Switch to enable or disable the **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="8f59d-157">**ParamSweepTasksPerCore** : numero di attività di sweep parametrico per l'aumento di un core.</span><span class="sxs-lookup"><span data-stu-id="8f59d-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks to grow one core.</span></span> <span data-ttu-id="8f59d-158">Il valore predefinito è l'aumento di un core per ogni attività.</span><span class="sxs-lookup"><span data-stu-id="8f59d-158">The default is to grow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8f59d-159">HPC Pack QFE KB3134307 modifica **ParamSweepTasksPerCore** in **TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="8f59d-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** to **TasksPerResourceUnit**.</span></span> <span data-ttu-id="8f59d-160">Si basa sul tipo di risorsa del processo e può essere un nodo, un socket o un core.</span><span class="sxs-lookup"><span data-stu-id="8f59d-160">It is based on the job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="8f59d-161">**GrowThreshold** : soglia di attività in coda per attivare l'aumento automatico.</span><span class="sxs-lookup"><span data-stu-id="8f59d-161">**GrowThreshold** - Threshold of queued tasks to trigger automatic growth.</span></span> <span data-ttu-id="8f59d-162">Il valore predefinito è 1 e significa che se sono presenti una o più attività in coda, i nodi vengono aumentati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8f59d-162">The default is 1, which means that if there are 1 or more tasks in the queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="8f59d-163">**GrowInterval** : intervallo in minuti per attivare l'aumento automatico.</span><span class="sxs-lookup"><span data-stu-id="8f59d-163">**GrowInterval** - Interval in minutes to trigger automatic growth.</span></span> <span data-ttu-id="8f59d-164">L'intervallo predefinito è 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="8f59d-164">The default interval is 5 minutes.</span></span>
* <span data-ttu-id="8f59d-165">**ShrinkInterval** : intervallo in minuti per attivare la riduzione automatica.</span><span class="sxs-lookup"><span data-stu-id="8f59d-165">**ShrinkInterval** - Interval in minutes to trigger automatic shrinking.</span></span> <span data-ttu-id="8f59d-166">L'intervallo predefinito è 5 minuti.|</span><span class="sxs-lookup"><span data-stu-id="8f59d-166">The default interval is 5 minutes.|</span></span>
* <span data-ttu-id="8f59d-167">**ShrinkIdleTimes** : numero di controlli continui da ridurre per indicare i nodi sono inattivi.</span><span class="sxs-lookup"><span data-stu-id="8f59d-167">**ShrinkIdleTimes** - Number of continuous checks to shrink to indicate the nodes are idle.</span></span> <span data-ttu-id="8f59d-168">Il valore predefinito è 3 volte.</span><span class="sxs-lookup"><span data-stu-id="8f59d-168">The default is 3 times.</span></span> <span data-ttu-id="8f59d-169">Ad esempio, se **ShrinkInterval** è di 5 minuti, HPC Pack controlla se il nodo è inattivo ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="8f59d-169">For example, if the **ShrinkInterval** is 5 minutes, HPC Pack checks whether the node is idle every 5 minutes.</span></span> <span data-ttu-id="8f59d-170">Se i nodi sono in uno stato di inattività dopo 3 controlli continui (15 minuti), HPC Pack riduce quel nodo.</span><span class="sxs-lookup"><span data-stu-id="8f59d-170">If the nodes are in the idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="8f59d-171">**ExtraNodesGrowRatio** -percentuale aggiuntiva di nodi da aumentare per i processi MPI (Message Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="8f59d-171">**ExtraNodesGrowRatio** - Additional percentage of nodes to grow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="8f59d-172">Il valore predefinito è 1 e significa che HPC Pack aumenta l'1% dei nodi per i processi MPI.</span><span class="sxs-lookup"><span data-stu-id="8f59d-172">The default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="8f59d-173">**GrowByMin** : opzione che indica se i criteri di aumento automatico sono basati sulle risorse minime necessarie per il processo.</span><span class="sxs-lookup"><span data-stu-id="8f59d-173">**GrowByMin** - Switch to indicate whether the autogrow policy is based on the minimum resources required for the job.</span></span> <span data-ttu-id="8f59d-174">Il valore predefinito è false e significa che HPC Pack aumenta i nodi per i processi in base alle risorse massime richieste per i processi.</span><span class="sxs-lookup"><span data-stu-id="8f59d-174">The default is false, which means that HPC Pack grows nodes for jobs based on the maximum resources required for the jobs.</span></span>
* <span data-ttu-id="8f59d-175">**SoaJobGrowThreshold** : soglia di richieste SOA in ingresso per attivare il processo di aumento automatico.</span><span class="sxs-lookup"><span data-stu-id="8f59d-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests to trigger the automatic grow process.</span></span> <span data-ttu-id="8f59d-176">Il valore predefinito è 50000.</span><span class="sxs-lookup"><span data-stu-id="8f59d-176">The default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8f59d-177">Questo parametro è supportato a partire da HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="8f59d-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="8f59d-178">**SoaRequestsPerCore** : numero di richieste SOA in ingresso per l'aumento di un core.</span><span class="sxs-lookup"><span data-stu-id="8f59d-178">**SoaRequestsPerCore** -Number of incoming SOA requests to grow one core.</span></span> <span data-ttu-id="8f59d-179">The default value is 20000.</span><span class="sxs-lookup"><span data-stu-id="8f59d-179">The default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8f59d-180">Questo parametro è supportato a partire da HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="8f59d-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="8f59d-181">**ExcludeNodeGroups**: i nodi nei gruppi di nodi specificati non vengono aumentati e ridotti in automatico.</span><span class="sxs-lookup"><span data-stu-id="8f59d-181">**ExcludeNodeGroups** – Nodes in the specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8f59d-182">Questo parametro è supportato a partire da HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="8f59d-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="8f59d-183">Esempio MPI</span><span class="sxs-lookup"><span data-stu-id="8f59d-183">MPI example</span></span>
<span data-ttu-id="8f59d-184">Per impostazione predefinita HPC Pack aumenta di 1% i nodi aggiuntivi per i processi MPI. **ExtraNodesGrowRatio** è impostato su 1.</span><span class="sxs-lookup"><span data-stu-id="8f59d-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set to 1).</span></span> <span data-ttu-id="8f59d-185">Il motivo è che MPI può richiedere più nodi e il processo può essere eseguito solo quando tutti i nodi sono pronti.</span><span class="sxs-lookup"><span data-stu-id="8f59d-185">The reason is that MPI may require multiple nodes, and the job can only run when all nodes are ready.</span></span> <span data-ttu-id="8f59d-186">Quando Azure avvia i nodi, in alcuni casi l'avvio di un nodo può richiedere più tempo rispetto ad altri, causando l'inattività degli altri nodi in attesa che quel nodo sia pronto.</span><span class="sxs-lookup"><span data-stu-id="8f59d-186">When Azure starts nodes, occasionally one node might need more time to start than others, causing other nodes to be idle while waiting for that node to get ready.</span></span> <span data-ttu-id="8f59d-187">Aumentando i nodi supplementari, HPC Pack riduce il tempo di attesa delle risorse, riducendo potenzialmente i costi.</span><span class="sxs-lookup"><span data-stu-id="8f59d-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="8f59d-188">Per aumentare la percentuale di nodi aggiuntivi per i processi MPI, ad esempio del 10%, eseguire un comando simile a</span><span class="sxs-lookup"><span data-stu-id="8f59d-188">To increase the percentage of extra nodes for MPI jobs (for example, to 10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="8f59d-189">Esempio SOA</span><span class="sxs-lookup"><span data-stu-id="8f59d-189">SOA example</span></span>
<span data-ttu-id="8f59d-190">Per impostazione predefinita, **SoaJobGrowThreshold** è impostata su 50000 e **SoaRequestsPerCore** è impostato su 200000.</span><span class="sxs-lookup"><span data-stu-id="8f59d-190">By default, **SoaJobGrowThreshold** is set to 50000 and **SoaRequestsPerCore** is set to 200000.</span></span> <span data-ttu-id="8f59d-191">Se si invia un processo SOA con 70000 richieste, ci sarà una sola attività in coda e le richieste in ingresso saranno 70000.</span><span class="sxs-lookup"><span data-stu-id="8f59d-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="8f59d-192">In questo caso HPC Pack aumenta 1 core per l'attività in coda e per le richieste in ingresso aumenta (70000 - 50000)/20000 = 1 core, in modo da aumentare in totale 2 core per questo processo SOA.</span><span class="sxs-lookup"><span data-stu-id="8f59d-192">In this case HPC Pack grows 1 core for the queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-the-azureautogrowshrinkps1-script"></a><span data-ttu-id="8f59d-193">Eseguire lo script AzureAutoGrowShrink.ps1</span><span class="sxs-lookup"><span data-stu-id="8f59d-193">Run the AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="8f59d-194">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8f59d-194">Prerequisites</span></span>

* <span data-ttu-id="8f59d-195">**Cluster HPC Pack 2012 R2 Update 1 o versione successiva**: lo script **AzureAutoGrowShrink.ps1** è installato nella cartella %CCP_HOME%bin.</span><span class="sxs-lookup"><span data-stu-id="8f59d-195">**HPC Pack 2012 R2 Update 1 or later cluster** - The **AzureAutoGrowShrink.ps1** script is installed in the %CCP_HOME%bin folder.</span></span> <span data-ttu-id="8f59d-196">Il nodo head del cluster può essere distribuito in locale o in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-196">The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="8f59d-197">Vedere [Configurare un cluster ibrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) per iniziare con un nodo head locale e i nodi "burst" di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="8f59d-198">Vedere lo [script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md) per distribuire velocemente un cluster HPC Pack in macchine virtuali di Azure o usare un [modello di avvio rapido di Azur](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="8f59d-198">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="8f59d-199">**Azure PowerShell 1.4.0**: lo script attualmente dipende da questa versione specifica di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f59d-199">**Azure PowerShell 1.4.0** - The script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="8f59d-200">**Per un cluster con nodi burst di Azure** - Eseguire lo script in un computer client in cui è installato HPC Pack o nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="8f59d-200">**For a cluster with Azure burst nodes** - Run the script on a client computer where HPC Pack is installed, or on the head node.</span></span> <span data-ttu-id="8f59d-201">In caso di esecuzione in un computer client, assicurarsi di impostare la variabile $env:CCP_SCHEDULER in modo che punti al nodo head.</span><span class="sxs-lookup"><span data-stu-id="8f59d-201">If running on a client computer, ensure that you set the variable $env:CCP_SCHEDULER to point to the head node.</span></span> <span data-ttu-id="8f59d-202">I nodi "burst" di Azure devono essere aggiunti al cluster, ma possono essere nello stato Non distribuito.</span><span class="sxs-lookup"><span data-stu-id="8f59d-202">The Azure “burst” nodes must be added to the cluster, but they may be in the Not-Deployed state.</span></span>
* <span data-ttu-id="8f59d-203">**Per un cluster distribuito in macchine virtuali di Azure (modello di distribuzione di Resource Manager)**: per un cluster di macchine virtuali di Azure distribuite nel modello di distribuzione di Resource Manager, lo script supporta due metodi per l'autenticazione di Azure: accedere al proprio account Azure per eseguire lo script ogni volta, eseguendo `Login-AzureRmAccount`, oppure configurare un'entità servizio per l'autenticazione con un certificato.</span><span class="sxs-lookup"><span data-stu-id="8f59d-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in the Resource Manager deployment model, the script supports two methods for Azure authentication: sign in to your Azure account to run the script every time (by running `Login-AzureRmAccount`, or configure a service principal to authenticate with a certificate.</span></span> <span data-ttu-id="8f59d-204">HPC Pack fornisce lo script **ConfigARMAutoGrowShrinkCert.ps** per creare un'entità servizio con certificato.</span><span class="sxs-lookup"><span data-stu-id="8f59d-204">HPC Pack provides the script **ConfigARMAutoGrowShrinkCert.ps** to create a service principal with certificate.</span></span> <span data-ttu-id="8f59d-205">Lo script crea un'applicazione Azure Active Directory (Azure AD) e un'entità servizio e assegna il ruolo di collaboratore all'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="8f59d-205">The script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns the Contributor role to the service principal.</span></span> <span data-ttu-id="8f59d-206">Per eseguire lo script, avviare Azure PowerShell come amministratore ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f59d-206">To run the script, start Azure PowerShell  as administrator and run the following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="8f59d-207">Per altre informazioni su **ConfigARMAutoGrowShrinkCert.ps1**, eseguire `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="8f59d-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="8f59d-208">**Per un cluster distribuito in macchine virtuali di Azure (modello di distribuzione classica)**: eseguire lo script nella macchina virtuale del nodo head, perché dipende dagli script **Start-HpcIaaSNode.ps1** e **Stop-HpcIaaSNode.ps1** installati in tale posizione.</span><span class="sxs-lookup"><span data-stu-id="8f59d-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run the script on the head node VM, because it depends on the **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="8f59d-209">Per questi script è inoltre necessario un certificato di gestione di Azure o un file delle impostazioni di pubblicazione (vedere [Gestire i nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="8f59d-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="8f59d-210">Assicurarsi che tutte le macchine virtuali del nodo di calcolo necessarie siano già aggiunte al cluster.</span><span class="sxs-lookup"><span data-stu-id="8f59d-210">Make sure all the compute node VMs you need are already added to the cluster.</span></span> <span data-ttu-id="8f59d-211">Potrebbero essere in stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="8f59d-211">They may be in the Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="8f59d-212">Sintassi</span><span class="sxs-lookup"><span data-stu-id="8f59d-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="8f59d-213">Parametri</span><span class="sxs-lookup"><span data-stu-id="8f59d-213">Parameters</span></span>
* <span data-ttu-id="8f59d-214">**NodeTemplates** - Nomi dei modelli di nodo per definire l'ambito per i nodi da ingrandire o ridurre.</span><span class="sxs-lookup"><span data-stu-id="8f59d-214">**NodeTemplates** - Names of the node templates to define the scope for the nodes to grow and shrink.</span></span> <span data-ttu-id="8f59d-215">Se non specificato (il valore predefinito è @()), tutti i nodi nel gruppo di nodi **AzureNodes** rientrano nell'ambito quando il valore di **NodeType** è AzureNodes e tutti i nodi nel gruppo di nodi **ComputeNodes** rientrano nell'ambito quando il valore di **NodeType** è ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="8f59d-215">If not specified (the default value is @()), all nodes in the **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in the **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="8f59d-216">**JobTemplates** : nomi dei modelli di processo per definire l'ambito per i nodi da ingrandire.</span><span class="sxs-lookup"><span data-stu-id="8f59d-216">**JobTemplates** - Names of the job templates to define the scope for the nodes to grow.</span></span>
* <span data-ttu-id="8f59d-217">**NodeType** - Il tipo di nodo da ingrandire o ridurre.</span><span class="sxs-lookup"><span data-stu-id="8f59d-217">**NodeType** - The type of node to grow and shrink.</span></span> <span data-ttu-id="8f59d-218">I valori supportati sono:</span><span class="sxs-lookup"><span data-stu-id="8f59d-218">Supported values are:</span></span>

  * <span data-ttu-id="8f59d-219">**AzureNodes** - Per i nodi di Azure PaaS (burst) in un cluster locale o IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="8f59d-220">**ComputeNodes** - Solo per le macchine virtuali dei nodi di calcolo in un cluster IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59d-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="8f59d-221">**NumOfQueuedJobsPerNodeToGrow** - Numero di processi in coda richiesti per ingrandire un nodo.</span><span class="sxs-lookup"><span data-stu-id="8f59d-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required to grow one node.</span></span>
* <span data-ttu-id="8f59d-222">**NumOfQueuedJobsToGrowThreshold** - Numero di processi in coda di soglia per avviare il processo di ingrandimento.</span><span class="sxs-lookup"><span data-stu-id="8f59d-222">**NumOfQueuedJobsToGrowThreshold** - The threshold number of queued jobs to start the grow process.</span></span>
* <span data-ttu-id="8f59d-223">**NumOfActiveQueuedTasksPerNodeToGrow** - Numero di attività in coda attive richieste per ingrandire un nodo.</span><span class="sxs-lookup"><span data-stu-id="8f59d-223">**NumOfActiveQueuedTasksPerNodeToGrow** - The number of active queued tasks required to grow one node.</span></span> <span data-ttu-id="8f59d-224">Se si specifica un valore maggiore di 0 per **NumOfQueuedJobsPerNodeToGrow** , questo parametro viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="8f59d-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="8f59d-225">**NumOfActiveQueuedTasksToGrowThreshold** - Numero di attività in coda attive di soglia per avviare il processo di ingrandimento.</span><span class="sxs-lookup"><span data-stu-id="8f59d-225">**NumOfActiveQueuedTasksToGrowThreshold** - The threshold number of active queued tasks to start the grow process.</span></span>
* <span data-ttu-id="8f59d-226">**NumOfInitialNodesToGrow** - Numero minimo iniziale dei nodi, da ingrandire se lo stato di tutti i nodi nell'ambito è **Non distribuito** o **Arrestato (deallocato)**.</span><span class="sxs-lookup"><span data-stu-id="8f59d-226">**NumOfInitialNodesToGrow** - The initial minimum number of nodes to grow if all the nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="8f59d-227">**GrowCheckIntervalMins** - Intervallo in minuti tra i controlli dell'ingrandimento.</span><span class="sxs-lookup"><span data-stu-id="8f59d-227">**GrowCheckIntervalMins** - The interval in minutes between checks to grow.</span></span>
* <span data-ttu-id="8f59d-228">**ShrinkCheckIntervalMins** - Intervallo in minuti tra i controlli della riduzione.</span><span class="sxs-lookup"><span data-stu-id="8f59d-228">**ShrinkCheckIntervalMins** - The interval in minutes between checks to shrink.</span></span>
* <span data-ttu-id="8f59d-229">**ShrinkCheckIdleTimes**: numero di controlli continui della riduzione, separati da **ShrinkCheckIntervalMins**, per indicare che i nodi sono inattivi.</span><span class="sxs-lookup"><span data-stu-id="8f59d-229">**ShrinkCheckIdleTimes** - The number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) to indicate the nodes are idle.</span></span>
* <span data-ttu-id="8f59d-230">**UseLastConfigurations** : configurazioni precedenti salvate nel file di argomenti.</span><span class="sxs-lookup"><span data-stu-id="8f59d-230">**UseLastConfigurations** - The previous configurations saved in the argument file.</span></span>
* <span data-ttu-id="8f59d-231">**ArgFile**- Nome del file di argomenti usato per salvare e aggiornare le configurazioni per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="8f59d-231">**ArgFile**- The name of the argument file used to save and update the configurations to run the script.</span></span>
* <span data-ttu-id="8f59d-232">**LogFilePrefix** : prefisso del nome del file di log.</span><span class="sxs-lookup"><span data-stu-id="8f59d-232">**LogFilePrefix** - The prefix name of the log file.</span></span> <span data-ttu-id="8f59d-233">È possibile specificare un percorso.</span><span class="sxs-lookup"><span data-stu-id="8f59d-233">You can specify a path.</span></span> <span data-ttu-id="8f59d-234">Per impostazione predefinita il log viene scritto nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="8f59d-234">By default the log is written to the current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="8f59d-235">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="8f59d-235">Example 1</span></span>
<span data-ttu-id="8f59d-236">Nell'esempio seguente, i nodi burst di Azure distribuiti con il modello Default AzureNode Template vengono configurati per l'ingrandimento e la riduzione automatici.</span><span class="sxs-lookup"><span data-stu-id="8f59d-236">The following example configures the Azure burst nodes deployed with the Default AzureNode Template to grow and shrink automatically.</span></span> <span data-ttu-id="8f59d-237">Se tutti i nodi sono inizialmente nello stato **Non distribuito** vengono avviati almeno 3 nodi.</span><span class="sxs-lookup"><span data-stu-id="8f59d-237">If all the nodes are initially in the **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="8f59d-238">Se il numero di processi in coda è maggiore di 8, lo script avvia i nodi fino a quando il numero non supera il rapporto tra processi in coda e **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="8f59d-238">If the number of queued jobs exceeds 8, the script starts nodes until their number exceeds the ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="8f59d-239">Se viene trovato un nodo inattivo in 3 tempi di inattività consecutivi, il nodo viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="8f59d-239">If a node is found to be idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="8f59d-240">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="8f59d-240">Example 2</span></span>
<span data-ttu-id="8f59d-241">Nell'esempio seguente, le macchine virtuali dei nodi di calcolo di Azure distribuite con il modello Default ComputeNode Template vengono configurate per l'ingrandimento e la riduzione automatici.</span><span class="sxs-lookup"><span data-stu-id="8f59d-241">The following example configures the Azure compute node VMs deployed with the Default ComputeNode Template to grow and shrink automatically.</span></span>
<span data-ttu-id="8f59d-242">I processi configurati dal modello di processo predefinito definiscono l'ambito del carico di lavoro nel cluster.</span><span class="sxs-lookup"><span data-stu-id="8f59d-242">The jobs configured by the Default job template define the scope of the workload on the cluster.</span></span> <span data-ttu-id="8f59d-243">Se tutti i nodi sono inizialmente arrestati, vengono avviati almeno 5 nodi.</span><span class="sxs-lookup"><span data-stu-id="8f59d-243">If all the nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="8f59d-244">Se il numero delle attività in coda attive è maggiore di 15, lo script avvia i nodi fino a quando il numero non supera il rapporto tra le attività in coda attive e **NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="8f59d-244">If the number of active queued tasks exceeds 15, the script starts nodes until their number exceeds the ratio of active queued tasks to **NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="8f59d-245">Se viene trovato un nodo inattivo in 10 tempi di inattività consecutivi, il nodo viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="8f59d-245">If a node is found to be idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
