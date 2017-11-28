---
title: nodi di calcolo cluster HPC Pack aaaManage | Documenti Microsoft
description: Informazioni su tooadd strumenti di script PowerShell, rimuovere, avviare e arrestare i nodi di calcolo cluster HPC Pack 2012 R2 in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="05278-103">Gestire il numero di hello e la disponibilità dei nodi di calcolo in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="05278-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="05278-104">Se si crea un cluster HPC Pack 2012 R2 in macchine virtuali di Azure, è possibile modi tooeasily aggiungere, rimuovere, avviare (provisioning) o arrestare (effettuarne il deprovisioning) alcune macchine virtuali del nodo del cluster di calcolo.</span><span class="sxs-lookup"><span data-stu-id="05278-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="05278-105">toodo queste attività, eseguire gli script di PowerShell di Azure che vengono installati nella macchina virtuale del nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="05278-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="05278-106">Questi script consente di controllare il numero di hello e disponibilità delle risorse di cluster HPC Pack in modo che è possibile controllare i costi.</span><span class="sxs-lookup"><span data-stu-id="05278-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="05278-107">In questo articolo si applica solo a tooHPC Pack 2012 R2 cluster in Azure creato utilizzando il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="05278-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="05278-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="05278-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="05278-109">Inoltre, gli script di PowerShell hello descritti in questo articolo non sono disponibili in HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="05278-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05278-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="05278-110">Prerequisites</span></span>
* <span data-ttu-id="05278-111">**Cluster HPC Pack 2012 R2 in macchine virtuali di Azure**: creare un cluster HPC Pack 2012 R2 nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="05278-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="05278-112">Ad esempio, è possibile automatizzare distribuzione hello utilizzando l'immagine di macchina virtuale di HPC Pack 2012 R2 hello in hello Azure Marketplace e uno script di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="05278-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="05278-113">Per informazioni e i prerequisiti, vedere [creare un Cluster HPC con lo script di distribuzione IaaS di HPC Pack hello](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="05278-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="05278-114">Dopo la distribuzione, trovare hello script di gestione di nodo % hello CCP\_nella cartella bin % HOME nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="05278-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="05278-115">Eseguire ogni script hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="05278-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="05278-116">**Certificato di gestione o di file di impostazioni di pubblicazione Azure**: È necessario uno dei seguenti hello toodo nel nodo head hello:</span><span class="sxs-lookup"><span data-stu-id="05278-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="05278-117">**File di impostazioni di pubblicazione hello importazione Azure**.</span><span class="sxs-lookup"><span data-stu-id="05278-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="05278-118">toodo, hello esecuzione seguendo i cmdlet PowerShell di Azure nel nodo head hello:</span><span class="sxs-lookup"><span data-stu-id="05278-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="05278-119">**Configurare il certificato di gestione di Azure hello nel nodo head hello**.</span><span class="sxs-lookup"><span data-stu-id="05278-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="05278-120">Se si dispone di file con estensione cer hello, importarlo nell'archivio certificati CurrentUser\My di hello e quindi eseguire hello seguente cmdlet di Azure PowerShell per l'ambiente di Azure (cloud o AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="05278-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="05278-121">Aggiungere le macchine virtuali dei nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="05278-121">Add compute node VMs</span></span>
<span data-ttu-id="05278-122">Aggiungere nodi di calcolo con hello **Add-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="05278-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="05278-123">Sintassi</span><span class="sxs-lookup"><span data-stu-id="05278-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="05278-124">parameters</span><span class="sxs-lookup"><span data-stu-id="05278-124">Parameters</span></span>
* <span data-ttu-id="05278-125">**ServiceName**: nome del servizio cloud hello nuove macchine virtuali del nodo di calcolo vengono aggiunti.</span><span class="sxs-lookup"><span data-stu-id="05278-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="05278-126">**ImageName**: nome dell'immagine di macchina virtuale di Azure, che può essere ottenuto tramite hello portale di Azure classico o i cmdlet di Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="05278-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="05278-127">immagine di Hello deve soddisfare hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="05278-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="05278-128">Deve essere installato un sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="05278-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="05278-129">HPC Pack deve essere installato nel ruolo del nodo calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="05278-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="05278-130">immagine di Hello deve essere un'immagine privata della categoria di utente hello, non un'immagine di macchina virtuale di Azure pubblica.</span><span class="sxs-lookup"><span data-stu-id="05278-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="05278-131">**Quantità**: numero di calcolo nodo macchine virtuali toobe aggiunto.</span><span class="sxs-lookup"><span data-stu-id="05278-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="05278-132">**InstanceSize**: dimensione di hello macchine virtuali del nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="05278-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="05278-133">**DomainUserName**: il nome utente di dominio, ovvero toojoin utilizzati hello nuove macchine virtuali toohello dominio.</span><span class="sxs-lookup"><span data-stu-id="05278-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="05278-134">**DomainUserPassword**: la Password dell'utente di dominio hello.</span><span class="sxs-lookup"><span data-stu-id="05278-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="05278-135">**NodeNameSeries** (facoltativo): modello di denominazione per hello nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="05278-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="05278-136">deve essere formato Hello &lt; *radice\_nome*&gt;&lt;*avviare\_numero*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="05278-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="05278-137">Ad esempio, MyCN % 10% significa una serie di hello consente di calcolare i nomi dei nodi a partire da MyCN11.</span><span class="sxs-lookup"><span data-stu-id="05278-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="05278-138">Se non specificato, hello script utilizza hello configurato serie di denominazione di nodo nel cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="05278-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="05278-139">Esempio</span><span class="sxs-lookup"><span data-stu-id="05278-139">Example</span></span>
<span data-ttu-id="05278-140">Hello esempio seguente viene aggiunta nodo di calcolo grandi dimensioni 20 macchine virtuali nel servizio cloud hello *hpcservice1*, in base all'immagine di macchina virtuale hello *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="05278-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="05278-141">Rimuovere le macchine virtuali dei nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="05278-141">Remove compute node VMs</span></span>
<span data-ttu-id="05278-142">Rimuovere i nodi di calcolo con hello **Remove-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="05278-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="05278-143">Sintassi</span><span class="sxs-lookup"><span data-stu-id="05278-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="05278-144">parameters</span><span class="sxs-lookup"><span data-stu-id="05278-144">Parameters</span></span>
* <span data-ttu-id="05278-145">**Nome**: rimuovere i nomi di toobe i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="05278-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="05278-146">Sono supportati caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="05278-146">Wildcards are supported.</span></span> <span data-ttu-id="05278-147">nome del set di parametri Hello è nome.</span><span class="sxs-lookup"><span data-stu-id="05278-147">hello parameter set name is Name.</span></span> <span data-ttu-id="05278-148">Non è possibile specificare entrambi hello **nome** e **nodo** parametri.</span><span class="sxs-lookup"><span data-stu-id="05278-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="05278-149">**Nodo**: oggetto HpcNode hello per hello nodi toobe rimossa, che può essere ottenuto tramite i cmdlet di HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="05278-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="05278-150">nome del set di parametri Hello è nodo.</span><span class="sxs-lookup"><span data-stu-id="05278-150">hello parameter set name is Node.</span></span> <span data-ttu-id="05278-151">Non è possibile specificare entrambi hello **nome** e **nodo** parametri.</span><span class="sxs-lookup"><span data-stu-id="05278-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="05278-152">**DeleteVHD** (facoltativo): l'impostazione toodelete dischi hello associata per hello macchine virtuali che sono state rimosse.</span><span class="sxs-lookup"><span data-stu-id="05278-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="05278-153">**Force** (facoltativo): l'impostazione tooforce offline i nodi HPC prima di rimuoverli.</span><span class="sxs-lookup"><span data-stu-id="05278-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="05278-154">**Conferma** (facoltativo): Richiedi conferma prima di eseguire il comando hello.</span><span class="sxs-lookup"><span data-stu-id="05278-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="05278-155">**WhatIf**: impostazione toodescribe cosa accadrebbe se venisse eseguito il comando di hello senza eseguire effettivamente il comando hello.</span><span class="sxs-lookup"><span data-stu-id="05278-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="05278-156">Esempio</span><span class="sxs-lookup"><span data-stu-id="05278-156">Example</span></span>
<span data-ttu-id="05278-157">Hello esempio seguente viene forzato nodi offline hello cui nomi iniziano con *HPCNode-CN,* e li rimuove i nodi di hello e i dischi associati.</span><span class="sxs-lookup"><span data-stu-id="05278-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="05278-158">Avviare le macchine virtuali dei nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="05278-158">Start compute node VMs</span></span>
<span data-ttu-id="05278-159">Inizio nodi con hello **Start-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="05278-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="05278-160">Sintassi</span><span class="sxs-lookup"><span data-stu-id="05278-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="05278-161">parameters</span><span class="sxs-lookup"><span data-stu-id="05278-161">Parameters</span></span>
* <span data-ttu-id="05278-162">**Nome**: i nomi di hello cluster nodi toobe avviato.</span><span class="sxs-lookup"><span data-stu-id="05278-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="05278-163">Sono supportati caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="05278-163">Wildcards are supported.</span></span> <span data-ttu-id="05278-164">nome del set di parametri Hello è nome.</span><span class="sxs-lookup"><span data-stu-id="05278-164">hello parameter set name is Name.</span></span> <span data-ttu-id="05278-165">Non è possibile specificare entrambi hello **nome** e **nodo** parametri.</span><span class="sxs-lookup"><span data-stu-id="05278-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="05278-166">**Nodo**-oggetto HpcNode hello per hello nodi toobe avviato, che può essere ottenuto tramite i cmdlet di HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="05278-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="05278-167">nome del set di parametri Hello è nodo.</span><span class="sxs-lookup"><span data-stu-id="05278-167">hello parameter set name is Node.</span></span> <span data-ttu-id="05278-168">Non è possibile specificare entrambi hello **nome** e **nodo** parametri.</span><span class="sxs-lookup"><span data-stu-id="05278-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="05278-169">Esempio</span><span class="sxs-lookup"><span data-stu-id="05278-169">Example</span></span>
<span data-ttu-id="05278-170">Hello esempio seguente viene avviato nodi cui nomi iniziano con *HPCNode-CN,*.</span><span class="sxs-lookup"><span data-stu-id="05278-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="05278-171">Arrestare le macchine virtuali dei nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="05278-171">Stop compute node VMs</span></span>
<span data-ttu-id="05278-172">Arresta nodi di calcolo con hello **Stop-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="05278-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="05278-173">Sintassi</span><span class="sxs-lookup"><span data-stu-id="05278-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="05278-174">parameters</span><span class="sxs-lookup"><span data-stu-id="05278-174">Parameters</span></span>
* <span data-ttu-id="05278-175">**Nome**-i nomi di toobe di nodi cluster hello arrestato.</span><span class="sxs-lookup"><span data-stu-id="05278-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="05278-176">Sono supportati caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="05278-176">Wildcards are supported.</span></span> <span data-ttu-id="05278-177">nome del set di parametri Hello è nome.</span><span class="sxs-lookup"><span data-stu-id="05278-177">hello parameter set name is Name.</span></span> <span data-ttu-id="05278-178">Non è possibile specificare entrambi hello **nome** e **nodo** parametri.</span><span class="sxs-lookup"><span data-stu-id="05278-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="05278-179">**Nodo**: oggetto HpcNode hello per hello nodi toobe arrestato, che può essere ottenuto tramite i cmdlet di HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="05278-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="05278-180">nome del set di parametri Hello è nodo.</span><span class="sxs-lookup"><span data-stu-id="05278-180">hello parameter set name is Node.</span></span> <span data-ttu-id="05278-181">Non è possibile specificare entrambi hello **nome** e **nodo** parametri.</span><span class="sxs-lookup"><span data-stu-id="05278-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="05278-182">**Force** (facoltativo): l'impostazione tooforce offline i nodi HPC prima di arrestarli.</span><span class="sxs-lookup"><span data-stu-id="05278-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="05278-183">Esempio</span><span class="sxs-lookup"><span data-stu-id="05278-183">Example</span></span>
<span data-ttu-id="05278-184">Hello esempio seguente viene forzato nodi non in linea con i nomi che iniziano *HPCNode-CN,* e quindi si arresta hello nodi.</span><span class="sxs-lookup"><span data-stu-id="05278-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="05278-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05278-185">Next steps</span></span>
* <span data-ttu-id="05278-186">tooautomatically aumentare o ridurre i nodi del cluster in base al carico di lavoro corrente hello dei processi e attività in cluster hello hello, vedere [automaticamente aumentare e ridurre le risorse di cluster HPC Pack hello Azure secondo toohello cluster del carico di lavoro](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="05278-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

