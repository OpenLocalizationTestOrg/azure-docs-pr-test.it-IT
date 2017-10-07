---
title: macchine virtuali aaaReplicate Hyper-V nei cloud VMM usando Azure Site Recovery e PowerShell di gestione risorse () | Documenti Microsoft
description: Replicare le macchine virtuali Hyper-V nei cloud VMM usando Azure Site Recovery e PowerShell
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="8a162-103">Replica delle macchine virtuali Hyper-V in VMM cloud tooAzure tramite PowerShell e Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="8a162-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a162-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8a162-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="8a162-105">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="8a162-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="8a162-106">Portale classico</span><span class="sxs-lookup"><span data-stu-id="8a162-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="8a162-107">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="8a162-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="8a162-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8a162-108">Overview</span></span>
<span data-ttu-id="8a162-109">Azure Site Recovery favorisce strategia ripristino emergenza e continuità tooyour aziendale gestendo la replica, il failover e ripristino delle macchine virtuali in un numero di scenari di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8a162-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="8a162-110">Per un elenco completo di distribuzione di scenari di vedere hello [Panoramica di Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a162-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="8a162-111">Questo articolo illustra come attività comuni di toouse PowerShell tooautomate occorre tooperform per la configurazione di macchine virtuali di Azure Site Recovery tooreplicate Hyper-V nel servizio di archiviazione tooAzure cloud System Center VMM.</span><span class="sxs-lookup"><span data-stu-id="8a162-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="8a162-112">articolo Hello sono inclusi i prerequisiti per scenario hello e Mostra</span><span class="sxs-lookup"><span data-stu-id="8a162-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="8a162-113">Come tooset di un insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="8a162-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="8a162-114">Installare hello Provider di Azure Site Recovery nel server VMM di origine hello</span><span class="sxs-lookup"><span data-stu-id="8a162-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="8a162-115">Registrare server hello nell'insieme di credenziali hello, aggiungere un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8a162-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="8a162-116">Installare l'agente di servizi di ripristino di Azure hello nei server host Hyper-V</span><span class="sxs-lookup"><span data-stu-id="8a162-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="8a162-117">Configurare le impostazioni di protezione per i cloud VMM, che verrà applicato tooall protetto le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="8a162-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="8a162-118">Abilitare la protezione di queste macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="8a162-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="8a162-119">Test toomake failover hello che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="8a162-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="8a162-120">Se si verificano problemi durante l'impostazione di questo scenario, è possibile pubblicare domande sul hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8a162-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="8a162-121">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8a162-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8a162-122">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="8a162-123">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8a162-123">Before you start</span></span>
<span data-ttu-id="8a162-124">Assicurarsi che siano rispettati i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a162-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="8a162-125">Prerequisiti di Azure</span><span class="sxs-lookup"><span data-stu-id="8a162-125">Azure prerequisites</span></span>
* <span data-ttu-id="8a162-126">È necessario un account [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="8a162-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="8a162-127">Se non si ha un account, creare un [account gratuito](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="8a162-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="8a162-128">Inoltre, per ulteriori informazioni hello [dei prezzi di Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="8a162-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="8a162-129">Se si sta tentando di out scenario di hello replica tooa CSP sottoscrizione, è necessario un abbonamento di CSP.</span><span class="sxs-lookup"><span data-stu-id="8a162-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="8a162-130">Ulteriori informazioni sul programma CSP hello in [come tooenroll nel programma CSP hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a162-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="8a162-131">È necessario un tooAzure di Azure v2 (Resource Manager) di archiviazione account toostore dati replicati.</span><span class="sxs-lookup"><span data-stu-id="8a162-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="8a162-132">account di Hello deve replica geografica abilitata.</span><span class="sxs-lookup"><span data-stu-id="8a162-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="8a162-133">Deve essere in hello stessa area hello servizio Azure Site Recovery e può essere associata a hello stessa sottoscrizione o hello CSP.</span><span class="sxs-lookup"><span data-stu-id="8a162-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="8a162-134">toolearn più sulla configurazione di archiviazione di Azure, vedere hello [tooMicrosoft introduzione di archiviazione di Azure](../storage/common/storage-introduction.md) per riferimento.</span><span class="sxs-lookup"><span data-stu-id="8a162-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="8a162-135">È necessario assicurarsi che le macchine virtuali da tooprotect rispettino hello toomake [macchina virtuale di Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="8a162-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="8a162-136">Attualmente è possibile eseguire tramite Powershell solo le operazioni a livello di VM.</span><span class="sxs-lookup"><span data-stu-id="8a162-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="8a162-137">Il supporto per le operazioni a livello di piano di ripristino sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="8a162-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="8a162-138">Per il momento, si è limitati tooperforming fail-passaggi solo a un livello di granularità 'protected VM' e non a livello di un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8a162-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="8a162-139">Prerequisiti di VMM</span><span class="sxs-lookup"><span data-stu-id="8a162-139">VMM prerequisites</span></span>
* <span data-ttu-id="8a162-140">È necessario un server VMM in esecuzione su System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="8a162-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="8a162-141">Nei server VMM contenenti macchine virtuali desiderate tooprotect deve essere in esecuzione hello Provider di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8a162-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="8a162-142">Viene installato durante la distribuzione di Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="8a162-143">È necessario almeno un cloud nel server VMM si desidera tooprotect hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="8a162-144">cloud Hello deve contenere:</span><span class="sxs-lookup"><span data-stu-id="8a162-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="8a162-145">Uno o più gruppi host VMM.</span><span class="sxs-lookup"><span data-stu-id="8a162-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="8a162-146">Uno o più cluster o server host Hyper-V in ogni gruppo host.</span><span class="sxs-lookup"><span data-stu-id="8a162-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="8a162-147">Uno o più macchine virtuali nel server Hyper-V di origine hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="8a162-148">Per altre informazioni sulla configurazione dei cloud VMM:</span><span class="sxs-lookup"><span data-stu-id="8a162-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="8a162-149">Ulteriori informazioni sui cloud privati di VMM in [novità del Cloud privato con System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) e [cloud VMM 2012 e hello](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="8a162-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="8a162-150">Informazioni su [hello configurazione VMM cloud dell'infrastruttura](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="8a162-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="8a162-151">Dopo avere definito gli elementi dell'infrastruttura cloud, leggere le informazioni su come creare i cloud privati in [Creazione di un cloud privato in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) e [Procedura dettagliata: creazione di cloud privati con System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="8a162-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="8a162-152">Prerequisiti di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="8a162-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="8a162-153">Hello Server host Hyper-V deve essere in esecuzione almeno **Windows Server 2012** con ruolo Hyper-V o **Microsoft Hyper-V Server 2012** e avere hello installati aggiornamenti più recenti.</span><span class="sxs-lookup"><span data-stu-id="8a162-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="8a162-154">Se si esegue Hyper-V in un cluster, si noti che il gestore del cluster non viene creato automaticamente se viene usato un cluster basato su indirizzi IP statici.</span><span class="sxs-lookup"><span data-stu-id="8a162-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="8a162-155">È necessario un gestore cluster hello tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="8a162-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="8a162-156">Ad</span><span class="sxs-lookup"><span data-stu-id="8a162-156">For</span></span>
* <span data-ttu-id="8a162-157">Per istruzioni, vedere [come gestore di Replica Hyper-V tooConfigure](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a162-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="8a162-158">Qualsiasi server host Hyper-V o cluster di cui si desidera toomanage protezione deve essere incluso in un cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="8a162-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="8a162-159">Prerequisiti di mapping di rete</span><span class="sxs-lookup"><span data-stu-id="8a162-159">Network mapping prerequisites</span></span>
<span data-ttu-id="8a162-160">Quando si proteggono macchine virtuali in Azure, viene eseguito il mapping di rete di hello reti di macchine virtuali hello nel server VMM di hello origine e destinazione reti Azure tooenable hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a162-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="8a162-161">Tutti i computer in cui eseguire il failover su hello stesso può connettersi tooeach altri, indipendentemente dal piano di ripristino si trovano in rete.</span><span class="sxs-lookup"><span data-stu-id="8a162-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="8a162-162">Se un gateway di rete è configurato nella rete Azure di destinazione hello, macchine virtuali possono connettersi le macchine virtuali tooother locale.</span><span class="sxs-lookup"><span data-stu-id="8a162-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="8a162-163">Se non si configura il mapping di rete, hello solo macchine virtuali che il failover hello stesso piano di ripristino saranno in grado di tooconnect tooeach altri dopo tooAzure di failover.</span><span class="sxs-lookup"><span data-stu-id="8a162-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="8a162-164">Se si desidera che il mapping di rete toodeploy, occorre seguente hello:</span><span class="sxs-lookup"><span data-stu-id="8a162-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="8a162-165">Hello le macchine virtuali da tooprotect nel server VMM di origine hello deve essere una rete VM tooa connesso.</span><span class="sxs-lookup"><span data-stu-id="8a162-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="8a162-166">La rete deve essere collegato tooa la rete logica associata al cloud hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="8a162-167">Le macchine virtuali toowhich replicata una rete di Azure possono connettersi dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="8a162-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="8a162-168">Selezionare la rete in fase di hello del failover.</span><span class="sxs-lookup"><span data-stu-id="8a162-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="8a162-169">rete Hello devono trovarsi in hello stessa area la sottoscrizione di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8a162-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="8a162-170">Altre informazioni sul mapping di rete sono disponibili negli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a162-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="8a162-171">Come tooconfigure reti logiche in VMM</span><span class="sxs-lookup"><span data-stu-id="8a162-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="8a162-172">Modalità VM tooconfigure reti e gateway in VMM</span><span class="sxs-lookup"><span data-stu-id="8a162-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="8a162-173">Come tooconfigure e monitorare reti virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="8a162-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="8a162-174">Prerequisiti di PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a162-174">PowerShell prerequisites</span></span>
<span data-ttu-id="8a162-175">Assicurarsi di disporre di Azure PowerShell pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="8a162-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="8a162-176">Se si sta già usando PowerShell, è necessario tooupgrade tooversion 0.8.10 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8a162-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="8a162-177">Per informazioni sull'impostazione di PowerShell, vedere hello [tooinstall della Guida e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8a162-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="8a162-178">Dopo aver impostato e configurato PowerShell, è possibile visualizzare tutti i cmdlet disponibili di hello per servizio hello [qui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a162-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="8a162-179">toolearn sui suggerimenti che consentono di utilizzare i cmdlet di hello, ad esempio come i valori dei parametri, input e output vengono in genere gestiti in Azure PowerShell, vedere hello [Guida introduttiva ai cmdlet di Azure tooget](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="8a162-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="8a162-180">Passaggio 1: Impostare una sottoscrizione di hello</span><span class="sxs-lookup"><span data-stu-id="8a162-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="8a162-181">Da Azure powershell, account di accesso tooyour account di Azure: hello seguente cmdlet utilizzando</span><span class="sxs-lookup"><span data-stu-id="8a162-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="8a162-182">Ottenere un elenco delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="8a162-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="8a162-183">Questo ID sottoscrizione hello elencherà anche per ognuna delle sottoscrizioni hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="8a162-184">Annotare l'ID sottoscrizione hello di sottoscrizione hello in cui si desidera l'insieme di credenziali toocreate hello recovery services</span><span class="sxs-lookup"><span data-stu-id="8a162-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="8a162-185">Impostare hello sottoscrizione in cui hello credenziali di servizi di ripristino sono toobe creato da citare hello ID di sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="8a162-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="8a162-186">Passaggio 2: Creare l'insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="8a162-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="8a162-187">Creare un gruppo di risorse di Azure Resource Manager, qualora non ce ne sia già uno disponibile</span><span class="sxs-lookup"><span data-stu-id="8a162-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="8a162-188">Creare un nuovo insieme di credenziali di servizi di ripristino e salvare hello creato l'oggetto insieme di credenziali di ripristino automatico di sistema in una variabile (verrà utilizzata in un secondo momento).</span><span class="sxs-lookup"><span data-stu-id="8a162-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="8a162-189">È inoltre possibile recuperare hello ripristino automatico di sistema dell'insieme di credenziali post di creazione di un oggetto utilizzando il cmdlet Get-AzureRMRecoveryServicesVault hello:-</span><span class="sxs-lookup"><span data-stu-id="8a162-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="8a162-190">Passaggio 3: Impostare il contesto di archivio di servizi di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="8a162-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="8a162-191">Impostare il contesto di insieme di credenziali hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8a162-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="8a162-192">Passaggio 4: Installare il Provider di Azure Site Recovery hello</span><span class="sxs-lookup"><span data-stu-id="8a162-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="8a162-193">Nel computer VMM hello, creare una directory eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="8a162-194">Estrarre il file hello utilizzando provider hello scaricato eseguendo hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="8a162-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="8a162-195">Installare il provider di hello utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="8a162-195">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="8a162-196">Attendere toofinish installazione hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="8a162-197">Registrare server hello in hello insieme di credenziali hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="8a162-198">Passaggio 5: creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8a162-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="8a162-199">Se non si dispone di un account di archiviazione di Azure, creare un account di replica geografica abilitata in hello stessa area geografica di hello insieme di credenziali eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="8a162-200">Si noti che l'account di archiviazione hello deve essere nella stessa area geografica del servizio Azure Site Recovery hello hello e associato hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8a162-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="8a162-201">Passaggio 6: Installare hello Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="8a162-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="8a162-202">Scaricare l'agente di servizi di ripristino di Azure hello in [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) e installazione su ogni server host Hyper-V disponibile in VMM hello cloud che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="8a162-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="8a162-203">Eseguire hello comando seguente in tutti gli host VMM:</span><span class="sxs-lookup"><span data-stu-id="8a162-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="8a162-204">Passaggio 7: configurare le impostazioni di protezione del cloud</span><span class="sxs-lookup"><span data-stu-id="8a162-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="8a162-205">Creare un tooAzure di criteri di replica eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="8a162-206">Ottenere un contenitore di protezione eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="8a162-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="8a162-207">Ottenere hello criteri dettagli tooa variabile utilizzando processo hello che è stato creato e ricordare il nome di criterio descrittivo hello:</span><span class="sxs-lookup"><span data-stu-id="8a162-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="8a162-208">Avviare associazione hello del contenitore di protezione hello con criteri di replica hello:</span><span class="sxs-lookup"><span data-stu-id="8a162-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="8a162-209">Al termine, il processo di hello eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="8a162-210">Dopo il processo di hello ha terminato l'elaborazione, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="8a162-211">completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="8a162-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="8a162-212">Passaggio 8: configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="8a162-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="8a162-213">Prima di iniziare il mapping di rete verificare che le macchine virtuali nel server VMM di origine hello rete VM tooa connesso.</span><span class="sxs-lookup"><span data-stu-id="8a162-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="8a162-214">Inoltre, creare una o più rete virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a162-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="8a162-215">Altre informazioni sulle modalità di rete tramite Gestione risorse di Azure e PowerShell, in toocreate un virtuale [creare una rete virtuale con una connessione VPN site-to-site tramite Gestione risorse di Azure e PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8a162-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="8a162-216">Si noti che più reti di macchine virtuali possono essere mappate tooa singola rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a162-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="8a162-217">Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="8a162-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="8a162-218">Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="8a162-219">Hello primo comando Ottiene i server per insieme di credenziali di hello corrente Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8a162-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="8a162-220">comando Hello archivia i server di Microsoft Azure Site Recovery hello nella variabile di matrice hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="8a162-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="8a162-221">Hello secondo comando Recupera hello sito ripristino rete per il primo server di hello nella matrice hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="8a162-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="8a162-222">comando Hello archivia reti hello nella variabile di hello $Networks.</span><span class="sxs-lookup"><span data-stu-id="8a162-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="8a162-223">Hello terzo comando recupera le reti virtuali di Azure e quindi tale valore nella variabile hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="8a162-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="8a162-224">Hello finale cmdlet crea un mapping tra la rete primaria hello e di rete di macchina virtuale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="8a162-225">cmdlet di Hello specifica rete primaria hello come primo elemento di hello di $Networks.</span><span class="sxs-lookup"><span data-stu-id="8a162-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="8a162-226">cmdlet di Hello specifica una rete di macchina virtuale al primo elemento hello di $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="8a162-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="8a162-227">Passaggio 9: abilitare la protezione per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="8a162-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="8a162-228">Dopo che le reti, cloud e i server hello sono configurate correttamente, è possibile abilitare la protezione per le macchine virtuali nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="8a162-229">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="8a162-229">Note hello following:</span></span>

* <span data-ttu-id="8a162-230">Le macchine virtuali devono essere conformi ai requisiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a162-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="8a162-231">Archiviare queste [prerequisiti e supporto](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) nella Guida alla pianificazione di hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="8a162-232">per la macchina virtuale hello, è necessario impostare tooenable protezione, sistema operativo hello e proprietà del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="8a162-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="8a162-233">Quando si crea una macchina virtuale in VMM utilizzando un modello di macchina virtuale è possibile impostare proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="8a162-234">È inoltre possibile impostare queste proprietà per le macchine virtuali esistenti in hello **generale** e **configurazione Hardware** schede delle proprietà di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8a162-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="8a162-235">Se le proprietà non impostate in VMM sarà in grado di tooconfigure nel portale di Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="8a162-236">protezione tooenable, eseguire hello contenitore di protezione hello tooget comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="8a162-237">Ottenere entità di protezione hello (VM) eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="8a162-238">Abilitare hello ripristino di emergenza per hello VM eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="8a162-239">Testare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="8a162-239">Test your deployment</span></span>
<span data-ttu-id="8a162-240">tootest la distribuzione è possibile eseguire un test di failover per una singola macchina virtuale, o creare un piano di ripristino costituita da più macchine virtuali ed eseguire un test di failover per il piano di hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="8a162-241">Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata.</span><span class="sxs-lookup"><span data-stu-id="8a162-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="8a162-242">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="8a162-242">Note that:</span></span>

* <span data-ttu-id="8a162-243">Se si desidera tooconnect toohello macchina virtuale di Azure tramite Desktop remoto dopo il failover hello, abilitare connessione Desktop remoto sulla macchina virtuale hello prima di eseguire il failover di test hello.</span><span class="sxs-lookup"><span data-stu-id="8a162-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="8a162-244">Dopo il failover, si utilizzerà una macchina di virtuale toohello pubblica del tooconnect indirizzo IP in Azure tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="8a162-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="8a162-245">Se si desidera toodo, assicurarsi che tutti i criteri che impediscono la connessione tooa virtual machine tramite un indirizzo pubblico dominio non è.</span><span class="sxs-lookup"><span data-stu-id="8a162-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="8a162-246">completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="8a162-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="8a162-247">Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="8a162-247">Run a test failover</span></span>
- <span data-ttu-id="8a162-248">Avviare il failover di test hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="8a162-249">Eseguire un failover pianificato</span><span class="sxs-lookup"><span data-stu-id="8a162-249">Run a planned failover</span></span>
- <span data-ttu-id="8a162-250">Avviare il failover pianificato hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="8a162-251">Eseguire un failover non pianificato</span><span class="sxs-lookup"><span data-stu-id="8a162-251">Run an unplanned failover</span></span>
- <span data-ttu-id="8a162-252">Avviare hello failover non pianificato eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a162-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="8a162-253"><a name=monitor></a> Monitorare l'attività</span><span class="sxs-lookup"><span data-stu-id="8a162-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="8a162-254">Utilizzare hello attività hello toomonitor di comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="8a162-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="8a162-255">Si noti la presenza di toowait tra i processi per hello toofinish di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="8a162-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="8a162-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a162-256">Next steps</span></span>
<span data-ttu-id="8a162-257">[Altre informazioni](/powershell/module/azurerm.recoveryservices.backup/#recovery) su Azure Site Recovery con i cmdlet PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8a162-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
