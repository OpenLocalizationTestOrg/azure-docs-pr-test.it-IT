---
title: i nodi del cluster HPC Pack aaaAutoscale | Documenti Microsoft
description: Automaticamente aumentare e ridurre il numero di hello dei nodi di calcolo cluster HPC Pack in Azure
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
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="00dab-103">Aumentare e ridurre le risorse di cluster HPC Pack hello in Azure in base a carico di lavoro cluster toohello automaticamente</span><span class="sxs-lookup"><span data-stu-id="00dab-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="00dab-104">Se si distribuiscono nodi di "Potenziamento" di Azure nel cluster HPC Pack o si crea un cluster HPC Pack nelle macchine virtuali di Azure, è possibile aumentare o ridurre le risorse cluster hello, ad esempio nodi o core in base al carico di lavoro hello in cluster hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="00dab-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="00dab-105">Scalabilità delle risorse cluster hello in questo modo consente toouse le risorse di Azure in modo più efficiente e controllare i costi.</span><span class="sxs-lookup"><span data-stu-id="00dab-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="00dab-106">Questo articolo illustra due modalità di HPC Pack fornisce le risorse di calcolo tooautoscale:</span><span class="sxs-lookup"><span data-stu-id="00dab-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="00dab-107">proprietà del cluster HPC Pack Hello **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="00dab-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="00dab-108">Hello **AzureAutoGrowShrink.ps1** script di HPC PowerShell</span><span class="sxs-lookup"><span data-stu-id="00dab-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="00dab-109">Attualmente è possibile solo aumentare e ridurre automaticamente i nodi di calcolo HPC Pack che eseguono un sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="00dab-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="00dab-110">Impostare la proprietà di hello AutoGrowShrink cluster</span><span class="sxs-lookup"><span data-stu-id="00dab-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="00dab-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="00dab-111">Prerequisites</span></span>

* <span data-ttu-id="00dab-112">**HPC Pack 2012 R2 Update 2 o versioni successive cluster** -nodo head del cluster hello può essere distribuito in locale o in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="00dab-113">Vedere [configurazione di un cluster ibrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget avviato con un nodo head locale e i nodi di "Potenziamento" di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="00dab-114">Vedere hello [script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly distribuire un cluster HPC Pack nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="00dab-115">**Per un cluster con un nodo head in Azure (modello di distribuzione di Resource Manager)**: a partire da HPC Pack 2016, l'autenticazione del certificato in un'applicazione Azure Active Directory viene usata per aumentare o ridurre automaticamente le macchine virtuali del cluster distribuite tramite Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="00dab-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="00dab-116">Configurare un certificato come segue:</span><span class="sxs-lookup"><span data-stu-id="00dab-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="00dab-117">Dopo la distribuzione di cluster, la connessione dal nodo head tooone di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="00dab-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="00dab-118">Caricamento del nodo head di hello certificato (in formato PFX con la chiave privata) tooeach e installare tooCert:\LocalMachine\My e Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="00dab-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="00dab-119">Avviare PowerShell di Azure come amministratore ed eseguire hello seguenti comandi in un nodo head:</span><span class="sxs-lookup"><span data-stu-id="00dab-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="00dab-120">Se l'account è in più di un tenant di Azure Active Directory o di sottoscrizione di Azure, è possibile eseguire l'esempio hello tooselect hello corretto tenant e una sottoscrizione di comando:</span><span class="sxs-lookup"><span data-stu-id="00dab-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="00dab-121">Eseguire hello successivo comando tooview hello selezionato tenant e sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="00dab-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="00dab-122">Eseguire lo script seguente hello</span><span class="sxs-lookup"><span data-stu-id="00dab-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="00dab-123">dove</span><span class="sxs-lookup"><span data-stu-id="00dab-123">where</span></span>

    <span data-ttu-id="00dab-124">**DisplayName**: nome visualizzato dell'applicazione Azure Active.</span><span class="sxs-lookup"><span data-stu-id="00dab-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="00dab-125">Se un'applicazione hello non esiste, viene creato in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="00dab-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="00dab-126">**Home page** -hello home page di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="00dab-127">È possibile configurare un URL fittizi, come hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="00dab-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="00dab-128">**IdentifierUri** -identificatore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="00dab-129">È possibile configurare un URL fittizi, come hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="00dab-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="00dab-130">**CertificateThumbprint** -identificazione personale del certificato hello installato nel nodo head di hello nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="00dab-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="00dab-131">**TenantId**: ID tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="00dab-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="00dab-132">È possibile ottenere l'ID Tenant hello dal portale di Azure Active Directory hello **proprietà** pagina.</span><span class="sxs-lookup"><span data-stu-id="00dab-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="00dab-133">Per altre informazioni su **ConfigARMAutoGrowShrinkCert.ps1**, eseguire `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="00dab-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="00dab-134">**Per un cluster con un nodo head in Azure (modello di distribuzione classica)** : se si utilizza del cluster di hello toocreate script distribuzione IaaS di HPC Pack hello in hello classico modello di distribuzione, abilitare hello **AutoGrowShrink** cluster proprietà impostando l'opzione AutoGrowShrink hello nel file di configurazione del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="00dab-135">Per informazioni dettagliate, vedere la documentazione di hello che accompagna hello [download dello script](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="00dab-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="00dab-136">In alternativa, abilitare hello **AutoGrowShrink** proprietà cluster dopo la distribuzione di cluster hello utilizzando HPC PowerShell i comandi descritti nella seguente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="00dab-137">tooprepare per questo, primo hello completo seguendo i passaggi:</span><span class="sxs-lookup"><span data-stu-id="00dab-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="00dab-138">Configurare un certificato di gestione di Azure nel nodo head hello e in hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="00dab-139">Per una distribuzione di test, è possibile usare hello predefinito Microsoft HPC Azure certificato autofirmato che consente di installare HPC Pack nel nodo head hello e quindi caricare tale tooyour certificato sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="00dab-140">Per le opzioni e procedure, vedere hello [linee guida della libreria TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="00dab-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="00dab-141">Eseguire **regedit** nel nodo head hello passare tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo e aggiungere un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="00dab-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="00dab-142">Impostare il nome di valore hello troppo "Identificazione personale" e l'identificazione personale toohello di dati di valore del certificato hello nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="00dab-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="00dab-143">Proprietà di HPC PowerShell commands tooset hello AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="00dab-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="00dab-144">Di seguito sono tooset i comandi di PowerShell HPC esempio **AutoGrowShrink** tootune e il comportamento di altri parametri.</span><span class="sxs-lookup"><span data-stu-id="00dab-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="00dab-145">Vedere [AutoGrowShrink parametri](#AutoGrowShrink-parameters) più avanti in questo articolo per l'elenco completo di hello delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="00dab-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="00dab-146">toorun questi comandi, avviare PowerShell HPC nel nodo head del cluster hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="00dab-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="00dab-147">**hello tooenable AutoGrowShrink proprietà**</span><span class="sxs-lookup"><span data-stu-id="00dab-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="00dab-148">**hello toodisable AutoGrowShrink proprietà**</span><span class="sxs-lookup"><span data-stu-id="00dab-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="00dab-149">**hello toochange aumentare l'intervallo in minuti**</span><span class="sxs-lookup"><span data-stu-id="00dab-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="00dab-150">**hello toochange ridurre l'intervallo in minuti**</span><span class="sxs-lookup"><span data-stu-id="00dab-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="00dab-151">**configurazione corrente di hello tooview di AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="00dab-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="00dab-152">**gruppi di nodi tooexclude da AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="00dab-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="00dab-153">Questo parametro è supportato a partire da HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="00dab-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="00dab-154">Parametri di AutoGrowShrink </span><span class="sxs-lookup"><span data-stu-id="00dab-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="00dab-155">di seguito Hello sono AutoGrowShrink parametri che è possibile modificare tramite hello **Set HpcClusterProperty** comando.</span><span class="sxs-lookup"><span data-stu-id="00dab-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="00dab-156">**EnableGrowShrink** : passare tooenable o disabilitare hello **AutoGrowShrink** proprietà.</span><span class="sxs-lookup"><span data-stu-id="00dab-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="00dab-157">**ParamSweepTasksPerCore** -numero di sweep parametrico attività toogrow uno dei core.</span><span class="sxs-lookup"><span data-stu-id="00dab-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="00dab-158">valore predefinito di Hello è toogrow un core per ogni attività.</span><span class="sxs-lookup"><span data-stu-id="00dab-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="00dab-159">Modifiche di HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** troppo**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="00dab-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="00dab-160">È basato sul tipo di risorsa di processo hello e può essere nodo, socket o core.</span><span class="sxs-lookup"><span data-stu-id="00dab-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="00dab-161">**GrowThreshold** -soglia di attività in coda tootrigger aumento automatico delle dimensioni.</span><span class="sxs-lookup"><span data-stu-id="00dab-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="00dab-162">valore predefinito di Hello è 1, che significa che se sono presenti 1 o più attività in hello in coda, aumenta automaticamente i nodi.</span><span class="sxs-lookup"><span data-stu-id="00dab-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="00dab-163">**GrowInterval** -intervallo in minuti tootrigger aumento automatico delle dimensioni.</span><span class="sxs-lookup"><span data-stu-id="00dab-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="00dab-164">intervallo di Hello predefinito è 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="00dab-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="00dab-165">**ShrinkInterval** -intervallo in minuti tootrigger la compattazione automatica.</span><span class="sxs-lookup"><span data-stu-id="00dab-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="00dab-166">intervallo di Hello predefinito è 5 minuti. |</span><span class="sxs-lookup"><span data-stu-id="00dab-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="00dab-167">**ShrinkIdleTimes** -numero di controlli continua tooshrink tooindicate hello nodi è inattivo.</span><span class="sxs-lookup"><span data-stu-id="00dab-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="00dab-168">valore predefinito di Hello è pari a 3 volte.</span><span class="sxs-lookup"><span data-stu-id="00dab-168">hello default is 3 times.</span></span> <span data-ttu-id="00dab-169">Ad esempio, se hello **ShrinkInterval** è 5 minuti, HPC Pack controlla se il nodo hello è inattivo ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="00dab-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="00dab-170">Se i nodi di hello sono in stato di inattività hello dopo 3 continua controlla (15 minuti), HPC Pack compatta tale nodo.</span><span class="sxs-lookup"><span data-stu-id="00dab-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="00dab-171">**ExtraNodesGrowRatio** -percentuale aggiuntiva di toogrow nodi per i processi di interfaccia MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="00dab-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="00dab-172">valore predefinito di Hello è 1, il che significa che HPC Pack aumenta nodi % 1 per i processi MPI.</span><span class="sxs-lookup"><span data-stu-id="00dab-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="00dab-173">**GrowByMin** -Switch tooindicate se il criterio di aumento automatico delle dimensioni hello si basa su risorse di hello minime necessarie per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="00dab-174">valore predefinito di Hello è false, il che significa che HPC Pack aumenta i nodi per i processi in base alle risorse di hello massimo richiesto per i processi di hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="00dab-175">**SoaJobGrowThreshold** -soglia di arrivo SOA richieste tootrigger hello automatico aumento delle dimensioni di processo.</span><span class="sxs-lookup"><span data-stu-id="00dab-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="00dab-176">valore predefinito di Hello è 50000.</span><span class="sxs-lookup"><span data-stu-id="00dab-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="00dab-177">Questo parametro è supportato a partire da HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="00dab-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="00dab-178">**SoaRequestsPerCore** -numero di SOA in ingresso richieste toogrow uno dei core.</span><span class="sxs-lookup"><span data-stu-id="00dab-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="00dab-179">valore predefinito di Hello è 20000.</span><span class="sxs-lookup"><span data-stu-id="00dab-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="00dab-180">Questo parametro è supportato a partire da HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="00dab-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="00dab-181">**ExcludeNodeGroups** : i nodi in hello specificati gruppi di nodi non automaticamente aumentare e ridurre.</span><span class="sxs-lookup"><span data-stu-id="00dab-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="00dab-182">Questo parametro è supportato a partire da HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="00dab-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="00dab-183">Esempio MPI</span><span class="sxs-lookup"><span data-stu-id="00dab-183">MPI example</span></span>
<span data-ttu-id="00dab-184">Per impostazione predefinita HPC Pack aumenta di 1% nodi aggiuntivi per i processi MPI (**ExtraNodesGrowRatio** è impostato too1).</span><span class="sxs-lookup"><span data-stu-id="00dab-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="00dab-185">motivo di Hello è MPI potrebbe richiedere più nodi che il processo di hello può essere eseguito solo quando tutti i nodi sono pronti.</span><span class="sxs-lookup"><span data-stu-id="00dab-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="00dab-186">Quando Azure avvia nodi, in alcuni casi un nodo potrebbe essere necessario più tempo toostart rispetto ad altri, causando toobe altri nodi inattivo durante l'attesa di tale nodo tooget pronto.</span><span class="sxs-lookup"><span data-stu-id="00dab-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="00dab-187">Aumentando i nodi supplementari, HPC Pack riduce il tempo di attesa delle risorse, riducendo potenzialmente i costi.</span><span class="sxs-lookup"><span data-stu-id="00dab-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="00dab-188">percentuale di hello tooincrease di nodi aggiuntivi per i processi MPI (ad esempio, % too10), eseguire un comando simile a</span><span class="sxs-lookup"><span data-stu-id="00dab-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="00dab-189">Esempio SOA</span><span class="sxs-lookup"><span data-stu-id="00dab-189">SOA example</span></span>
<span data-ttu-id="00dab-190">Per impostazione predefinita, **SoaJobGrowThreshold** è impostato too50000 e **SoaRequestsPerCore** è impostato too200000.</span><span class="sxs-lookup"><span data-stu-id="00dab-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="00dab-191">Se si invia un processo SOA con 70000 richieste, ci sarà una sola attività in coda e le richieste in ingresso saranno 70000.</span><span class="sxs-lookup"><span data-stu-id="00dab-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="00dab-192">In questo caso HPC Pack aumenta 1 core per hello in coda attività e per le richieste in ingresso, aumento delle dimensioni (70000 50000) / core 20000 = 1, in totale aumenta 2 core per questo processo SOA.</span><span class="sxs-lookup"><span data-stu-id="00dab-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="00dab-193">Eseguire script AzureAutoGrowShrink.ps1 hello</span><span class="sxs-lookup"><span data-stu-id="00dab-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="00dab-194">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="00dab-194">Prerequisites</span></span>

* <span data-ttu-id="00dab-195">**HPC Pack 2012 R2 Update 1 o versioni successive cluster** : hello **AzureAutoGrowShrink.ps1** script viene installato nella cartella di hello % CCP_HOME % bin.</span><span class="sxs-lookup"><span data-stu-id="00dab-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="00dab-196">nodo head del cluster Hello può essere distribuito in locale o in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="00dab-197">Vedere [configurazione di un cluster ibrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget avviato con un nodo head locale e i nodi di "Potenziamento" di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="00dab-198">Vedere hello [script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly distribuire un cluster HPC Pack nelle macchine virtuali di Azure oppure usare un [modello di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="00dab-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="00dab-199">**Azure PowerShell 1.4.0** -script hello attualmente dipende da questa versione specifica di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00dab-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="00dab-200">**Per un cluster con Azure burst nodi** -Esegui script hello in un computer client in cui è installato HPC Pack o nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="00dab-201">Se in esecuzione in un computer client, assicurarsi di impostare hello variabile $env: nodo head di CCP_SCHEDULER toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="00dab-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="00dab-202">i nodi di Azure "potenziamento" Hello devono essere aggiunte toohello cluster, ma possono risultare non distribuiti hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="00dab-203">**Per un cluster distribuito in macchine virtuali di Azure (modello di distribuzione di gestione delle risorse)** -per un cluster di macchine virtuali di Azure distribuite nel modello di distribuzione di gestione risorse di hello, script hello supporta due metodi per l'autenticazione di Azure: Accedi tooyour account Azure script hello toorun ogni ora (eseguendo `Login-AzureRmAccount`, o configurare un tooauthenticate dell'entità servizio con un certificato.</span><span class="sxs-lookup"><span data-stu-id="00dab-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="00dab-204">HPC Pack fornisce script hello **ConfigARMAutoGrowShrinkCert.ps** toocreate un'entità servizio con certificato.</span><span class="sxs-lookup"><span data-stu-id="00dab-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="00dab-205">script Hello crea un'applicazione Azure Active Directory (Azure AD) e un'entità servizio e assegna l'entità di servizio toohello ruolo Collaboratore hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="00dab-206">script di hello toorun, avviare Azure PowerShell come amministratore ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="00dab-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="00dab-207">Per altre informazioni su **ConfigARMAutoGrowShrinkCert.ps1**, eseguire `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="00dab-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="00dab-208">**Per un cluster distribuito in macchine virtuali di Azure (modello di distribuzione classica)** -Esegui script hello nel nodo head hello macchina virtuale, perché dipende da hello **Start-hpciaasnode.ps1** e **Stop-hpciaasnode.ps1**script che vi sono installati.</span><span class="sxs-lookup"><span data-stu-id="00dab-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="00dab-209">Per questi script è inoltre necessario un certificato di gestione di Azure o un file delle impostazioni di pubblicazione (vedere [Gestire i nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="00dab-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="00dab-210">Verificare che hello tutte le macchine virtuali è necessario del nodo sono già state aggiunte toohello cluster di calcolo.</span><span class="sxs-lookup"><span data-stu-id="00dab-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="00dab-211">Possono essere nello stato Stopped hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="00dab-212">Sintassi</span><span class="sxs-lookup"><span data-stu-id="00dab-212">Syntax</span></span>
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
### <a name="parameters"></a><span data-ttu-id="00dab-213">parameters</span><span class="sxs-lookup"><span data-stu-id="00dab-213">Parameters</span></span>
* <span data-ttu-id="00dab-214">**NodeTemplates** -i nomi di hello nodo modelli toodefine hello ambito per toogrow nodi hello e compatta.</span><span class="sxs-lookup"><span data-stu-id="00dab-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="00dab-215">Se non specificato (valore predefinito di hello è @()), tutti i nodi hello **AzureNodes** gruppo di nodi sono nell'ambito quando **NodeType** ha un valore di AzureNodes e tutti i nodi in hello **ComputeNodes** gruppo di nodi sono nell'ambito quando **NodeType** ha un valore di ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="00dab-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="00dab-216">**Le entità Jobtemplate** -processo di nomi di hello modelli toodefine hello ambito toogrow nodi hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="00dab-217">**Tipo di nodo** - tipo di nodo toogrow hello e compattazione.</span><span class="sxs-lookup"><span data-stu-id="00dab-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="00dab-218">I valori supportati sono:</span><span class="sxs-lookup"><span data-stu-id="00dab-218">Supported values are:</span></span>

  * <span data-ttu-id="00dab-219">**AzureNodes** - Per i nodi di Azure PaaS (burst) in un cluster locale o IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="00dab-220">**ComputeNodes** - Solo per le macchine virtuali dei nodi di calcolo in un cluster IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="00dab-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="00dab-221">**NumOfQueuedJobsPerNodeToGrow** -numero di processi in coda necessari toogrow un nodo.</span><span class="sxs-lookup"><span data-stu-id="00dab-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="00dab-222">**NumOfQueuedJobsToGrowThreshold** -processo di aumento delle dimensioni hello soglia numero hello toostart processi in coda.</span><span class="sxs-lookup"><span data-stu-id="00dab-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="00dab-223">**NumOfActiveQueuedTasksPerNodeToGrow** -numero di hello di attività attive in coda necessari toogrow un nodo.</span><span class="sxs-lookup"><span data-stu-id="00dab-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="00dab-224">Se si specifica un valore maggiore di 0 per **NumOfQueuedJobsPerNodeToGrow** , questo parametro viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="00dab-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="00dab-225">**NumOfActiveQueuedTasksToGrowThreshold** -processo di aumento delle dimensioni hello soglia numero hello toostart attività attive in coda.</span><span class="sxs-lookup"><span data-stu-id="00dab-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="00dab-226">**NumOfInitialNodesToGrow** : hello iniziale numero minimo di nodi toogrow se tutti i nodi di hello nell'ambito sono **non distribuiti** o **arrestato (deallocato)**.</span><span class="sxs-lookup"><span data-stu-id="00dab-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="00dab-227">**GrowCheckIntervalMins** -intervallo hello in minuti tra i controlli toogrow.</span><span class="sxs-lookup"><span data-stu-id="00dab-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="00dab-228">**ShrinkCheckIntervalMins** -intervallo hello in minuti tra i controlli tooshrink.</span><span class="sxs-lookup"><span data-stu-id="00dab-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="00dab-229">**ShrinkCheckIdleTimes** -hello numero di controlli di riduzione continui (separati da **ShrinkCheckIntervalMins**) tooindicate hello nodi sono inattivi.</span><span class="sxs-lookup"><span data-stu-id="00dab-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="00dab-230">**UseLastConfigurations** -hello configurazioni precedenti salvate nel file hello degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="00dab-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="00dab-231">**ArgFile**: nome di hello argomento file utilizzato toosave hello e hello configurazioni toorun hello script di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="00dab-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="00dab-232">**LogFilePrefix** -hello prefisso del nome del file di log hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="00dab-233">È possibile specificare un percorso.</span><span class="sxs-lookup"><span data-stu-id="00dab-233">You can specify a path.</span></span> <span data-ttu-id="00dab-234">Per impostazione predefinita il log di hello è scritto toohello directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="00dab-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="00dab-235">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="00dab-235">Example 1</span></span>
<span data-ttu-id="00dab-236">Hello seguente esempio mostra come configurare hello Azure burst nodi distribuiti con toogrow il modello AzureNode predefinito e la riduzione automatica.</span><span class="sxs-lookup"><span data-stu-id="00dab-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="00dab-237">Se tutti i nodi sono inizialmente in hello **non distribuiti** stato, vengono avviati almeno 3 nodi.</span><span class="sxs-lookup"><span data-stu-id="00dab-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="00dab-238">Se il numero di hello di processi in coda è superiore a 8, script hello avvia nodi fino a quando il numero supera il rapporto hello di processi in coda per **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="00dab-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="00dab-239">Se un nodo risulta inattivo in periodi di inattività consecutivi 3 toobe, viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="00dab-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="00dab-240">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="00dab-240">Example 2</span></span>
<span data-ttu-id="00dab-241">Hello seguente esempio mostra come configurare hello Azure distribuite con hello modello ComputeNode predefinito toogrow macchine virtuali del nodo di calcolo e la riduzione automatica.</span><span class="sxs-lookup"><span data-stu-id="00dab-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="00dab-242">processi di Hello configurati dal modello di processo predefinito di hello definiscono l'ambito di hello del carico di lavoro nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="00dab-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="00dab-243">Se tutti i nodi di hello inizialmente vengono arrestati, vengono avviati almeno 5 nodi.</span><span class="sxs-lookup"><span data-stu-id="00dab-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="00dab-244">Se il numero di hello di attività attive in coda è superiore a 15, script hello avvia nodi fino a quando il numero supera il rapporto di hello di attività attive in coda troppo**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="00dab-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="00dab-245">Se un nodo risulta inattivo in 10 periodi di inattività consecutivi toobe, viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="00dab-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
