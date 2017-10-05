---
title: Replicare le macchine virtuali Hyper-V nei cloud VMM usando Azure Site Recovery e PowerShell (Resource Manager) | Documentazione Microsoft
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
ms.openlocfilehash: 34086044db752f09f1282517b59856091e85c2fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="d6fdc-103">Replicare macchine virtuali Hyper-V nei cloud VMM in Azure con PowerShell e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d6fdc-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6fdc-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d6fdc-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="d6fdc-105">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="d6fdc-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="d6fdc-106">Portale classico</span><span class="sxs-lookup"><span data-stu-id="d6fdc-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="d6fdc-107">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="d6fdc-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="d6fdc-108">Overview</span><span class="sxs-lookup"><span data-stu-id="d6fdc-108">Overview</span></span>
<span data-ttu-id="d6fdc-109">Azure Site Recovery favorisce la strategia di continuità aziendale e ripristino di emergenza (BCDR) gestendo la replica, il failover e il ripristino delle macchine virtuali in diversi scenari di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="d6fdc-110">Per un elenco completo degli scenari di distribuzione, vedere [Panoramica di Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="d6fdc-111">In questo articolo viene illustrato come utilizzare PowerShell per automatizzare attività comuni, che è necessario eseguire quando si configura Azure Site Recovery per replicare le macchine virtuali Hyper-V nei cloud VMM di System Center VMM nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="d6fdc-112">Questo articolo include i prerequisiti per lo scenario e illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-112">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="d6fdc-113">Come configurare un insieme di credenziali dei Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="d6fdc-113">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="d6fdc-114">Installare il provider di Azure Site Recovery nel server VMM di origine</span><span class="sxs-lookup"><span data-stu-id="d6fdc-114">Install the Azure Site Recovery Provider on the source VMM server</span></span>
* <span data-ttu-id="d6fdc-115">Registrare il server nell'insieme di credenziali e aggiungere un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d6fdc-115">Register the server in the vault, add an Azure storage account</span></span>
* <span data-ttu-id="d6fdc-116">Installare l'agente di Servizi di ripristino di Azure in server host Hyper-V</span><span class="sxs-lookup"><span data-stu-id="d6fdc-116">Install the Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="d6fdc-117">Configurare le impostazioni di protezione per cloud VMM da applicare a tutte le macchine virtuali protette</span><span class="sxs-lookup"><span data-stu-id="d6fdc-117">Configure protection settings for VMM clouds, that will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="d6fdc-118">Abilitare la protezione di queste macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d6fdc-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="d6fdc-119">Eseguire il test del failover per accertarsi che tutti gli elementi funzionino come previsto</span><span class="sxs-lookup"><span data-stu-id="d6fdc-119">Test the fail-over to make sure everything's working as expected.</span></span>

<span data-ttu-id="d6fdc-120">Nel caso di problemi di configurazione di questo scenario, inviare le proprie domande al [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-120">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="d6fdc-121">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d6fdc-122">Questo articolo illustra l’utilizzo del modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-122">This article covers using the Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="d6fdc-123">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d6fdc-123">Before you start</span></span>
<span data-ttu-id="d6fdc-124">Assicurarsi che siano rispettati i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="d6fdc-125">Prerequisiti di Azure</span><span class="sxs-lookup"><span data-stu-id="d6fdc-125">Azure prerequisites</span></span>
* <span data-ttu-id="d6fdc-126">È necessario un account [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="d6fdc-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="d6fdc-127">Se non si ha un account, creare un [account gratuito](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="d6fdc-128">È anche possibile leggere le informazioni sui [prezzi di Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-128">In addition, you can read about the [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="d6fdc-129">Se si prova a usare la replica in uno scenario di sottoscrizione di CSP, sarà necessaria una sottoscrizione di CSP.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-129">You'll need a CSP subscription if you are trying out the replication to a CSP subscription scenario.</span></span> <span data-ttu-id="d6fdc-130">Per altre informazioni sul programma CSP, vedere [Iscriversi al programma CSP (Cloud Solution Provider)](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-130">Learn more about the CSP program in [how to enroll in the CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="d6fdc-131">Per archiviare dati replicati in Azure, è necessario un account di archiviazione di Azure v2 (Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-131">You'll need an Azure v2 storage (Resource Manager) account to store data replicated to Azure.</span></span> <span data-ttu-id="d6fdc-132">Nell'account deve essere abilitata la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-132">The account needs geo-replication enabled.</span></span> <span data-ttu-id="d6fdc-133">L'account deve trovarsi nella stessa area geografica in cui si trova il servizio Azure Site Recovery e deve essere associato alla stessa sottoscrizione o alla sottoscrizione di CSP.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-133">It should be in the same region as the Azure Site Recovery service, and be associated with the same subscription or the CSP subscription.</span></span> <span data-ttu-id="d6fdc-134">Per altre informazioni sulla configurazione dell'archiviazione di Azure, vedere [Introduzione ad Archiviazione di Microsoft Azure](../storage/common/storage-introduction.md) come riferimento.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-134">To learn more about setting up Azure storage, see the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="d6fdc-135">È necessario assicurarsi che le macchine virtuali da proteggere soddisfino i [prerequisiti delle macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-135">You'll need to make sure that virtual machines you want to protect comply with the [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="d6fdc-136">Attualmente è possibile eseguire tramite Powershell solo le operazioni a livello di VM.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="d6fdc-137">Il supporto per le operazioni a livello di piano di ripristino sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="d6fdc-138">Attualmente è possibile eseguire i failover solo a livello di granularità di "VM protetta", non a livello di piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-138">For now, you are limited to performing fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="d6fdc-139">Prerequisiti di VMM</span><span class="sxs-lookup"><span data-stu-id="d6fdc-139">VMM prerequisites</span></span>
* <span data-ttu-id="d6fdc-140">È necessario un server VMM in esecuzione su System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="d6fdc-141">Nei server VMM contenenti macchine virtuali che si desidera proteggere deve essere in esecuzione il provider di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-141">Any VMM server containing virtual machines you want to protect must be running the Azure Site Recovery Provider.</span></span> <span data-ttu-id="d6fdc-142">Viene installato durante la distribuzione di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-142">This is installed during the Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="d6fdc-143">È necessario almeno un cloud nel server VMM da proteggere.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-143">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="d6fdc-144">Il cloud deve contenere:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-144">The cloud should contain:</span></span>
  * <span data-ttu-id="d6fdc-145">Uno o più gruppi host VMM.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="d6fdc-146">Uno o più cluster o server host Hyper-V in ogni gruppo host.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="d6fdc-147">Una o più macchine virtuali nel server Hyper-V di origine.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-147">One or more virtual machines on the source Hyper-V server.</span></span>
* <span data-ttu-id="d6fdc-148">Per altre informazioni sulla configurazione dei cloud VMM:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="d6fdc-149">Per altre informazioni sui cloud privati VMM, leggere [Novità del cloud privato con System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) e [VMM 2012 e i cloud](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and the clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="d6fdc-150">Per altre informazioni, vedere [Configurare l'infrastruttura cloud VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="d6fdc-150">Learn about [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="d6fdc-151">Dopo avere definito gli elementi dell'infrastruttura cloud, leggere le informazioni su come creare i cloud privati in [Creazione di un cloud privato in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) e [Procedura dettagliata: creazione di cloud privati con System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="d6fdc-152">Prerequisiti di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="d6fdc-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="d6fdc-153">I server Hyper-V host devono eseguire almeno **Windows Server 2012** con ruolo Hyper-V oppure **Microsoft Hyper-V Server 2012** e disporre degli ultimi aggiornamenti installati.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-153">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="d6fdc-154">Se si esegue Hyper-V in un cluster, si noti che il gestore del cluster non viene creato automaticamente se viene usato un cluster basato su indirizzi IP statici.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="d6fdc-155">Sarà necessario configurare manualmente il broker del cluster.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-155">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="d6fdc-156">Ad</span><span class="sxs-lookup"><span data-stu-id="d6fdc-156">For</span></span>
* <span data-ttu-id="d6fdc-157">Per istruzioni, vedere [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx)(Come configurare il Gestore di replica Hyper).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-157">For instructions see [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="d6fdc-158">Qualsiasi server o cluster Hyper-V per cui si vuole gestire la protezione deve essere incluso in un cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-158">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="d6fdc-159">Prerequisiti di mapping di rete</span><span class="sxs-lookup"><span data-stu-id="d6fdc-159">Network mapping prerequisites</span></span>
<span data-ttu-id="d6fdc-160">Quando si proteggono le macchine virtuali in Azure, il mapping di rete collega le reti di macchine virtuali nel server VMM di origine e le reti di Azure in un server VMM di destinazione per eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-160">When you protect virtual machines in Azure, the network mapping  maps the virtual machine networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="d6fdc-161">Tutte le macchine virtuali di cui viene eseguito il failover nella stessa rete possono connettersi tra loro, indipendentemente dal piano di ripristino di appartenenza.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-161">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="d6fdc-162">Se nella rete di Azure di destinazione è configurato un gateway di rete, le macchine virtuali possono connettersi ad altre macchine virtuali locali.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-162">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="d6fdc-163">Se non si configura il mapping delle reti, solo le macchine virtuali di cui viene eseguito il failover nello stesso piano di ripristino possono connettersi tra loro dopo il failover in Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-163">If you don’t configure network mapping, only the virtual machines that fail over in the same recovery plan will be able to connect to each other after fail-over to Azure.</span></span>

<span data-ttu-id="d6fdc-164">Per distribuire il mapping di rete sarà necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-164">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="d6fdc-165">Le macchine virtuali che si vuole proteggere nel server VMM di origine devono essere connesse a una rete VM.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-165">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="d6fdc-166">È necessario che tale rete sia collegata a una rete logica associata al cloud.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-166">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="d6fdc-167">Una rete di Azure a cui le macchine virtuali replicate possono connettersi dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-167">An Azure network to which replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="d6fdc-168">Questa rete viene selezionata al momento del failover.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-168">You'll select this network at the time of fail-over.</span></span> <span data-ttu-id="d6fdc-169">La rete deve trovarsi nella stessa area della sottoscrizione di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-169">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="d6fdc-170">Altre informazioni sul mapping di rete sono disponibili negli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="d6fdc-171">Come configurare le reti logiche in VMM</span><span class="sxs-lookup"><span data-stu-id="d6fdc-171">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="d6fdc-172">Come configurare reti VM e gateway in VMM</span><span class="sxs-lookup"><span data-stu-id="d6fdc-172">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="d6fdc-173">Come configurare e monitorare le reti virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="d6fdc-173">How to configure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="d6fdc-174">Prerequisiti di PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6fdc-174">PowerShell prerequisites</span></span>
<span data-ttu-id="d6fdc-175">Assicurarsi che Azure PowerShell sia pronto all'uso.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-175">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="d6fdc-176">Se già si utilizza PowerShell, è necessario eseguire l'aggiornamento alla versione 0.8.10 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-176">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="d6fdc-177">Per informazioni sulla configurazione di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-177">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="d6fdc-178">Dopo avere impostato e configurato PowerShell, è possibile vedere tutti i cmdlet disponibili per il servizio [qui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-178">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="d6fdc-179">Per informazioni sui suggerimenti che facilitano l'uso dei cmdlet, ad esempio i valori dei parametri, sugli input e sugli output che vengono in genere gestiti in Azure PowerShell, vedere [Iniziare a utilizzare i cmdlet di Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-179">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="d6fdc-180">Passaggio 1: impostare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d6fdc-180">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="d6fdc-181">Da Azure PowerShell accedere all'account di Azure con i cmdlet seguenti</span><span class="sxs-lookup"><span data-stu-id="d6fdc-181">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="d6fdc-182">Ottenere un elenco delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="d6fdc-183">Verranno elencati anche i valori subscriptionID per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-183">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="d6fdc-184">Annotare il valore subscriptionID della sottoscrizione in cui si vuole creare l'insieme di credenziali dei Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="d6fdc-184">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="d6fdc-185">Configurare la sottoscrizione in cui deve essere creato l'insieme di credenziali dei Servizi di ripristino, indicando l'ID della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d6fdc-185">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="d6fdc-186">Passaggio 2: Creare l'insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="d6fdc-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="d6fdc-187">Creare un gruppo di risorse di Azure Resource Manager, qualora non ce ne sia già uno disponibile</span><span class="sxs-lookup"><span data-stu-id="d6fdc-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="d6fdc-188">Creare un nuovo insieme di credenziali di Servizi di ripristino e salvare l'oggetto insieme di credenziali di ASR creato in una variabile. Verrà usato in seguito.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-188">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="d6fdc-189">È anche possibile recuperare l'oggetto insieme di credenziali di ASR dopo la creazione usando il cmdlet Get-AzureRMRecoveryServicesVault:-</span><span class="sxs-lookup"><span data-stu-id="d6fdc-189">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="d6fdc-190">Passaggio 3: Impostare il contesto dell'insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="d6fdc-190">Step 3: Set the Recovery Services Vault context</span></span>

<span data-ttu-id="d6fdc-191">Impostare il contesto dell'insieme eseguendo il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-191">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="d6fdc-192">Passaggio 4: installare il provider di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d6fdc-192">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="d6fdc-193">Nel computer VMM, creare una directory eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-193">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="d6fdc-194">Estrarre i file utilizzando il provider scaricato eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-194">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="d6fdc-195">Installare il provider utilizzando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-195">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="d6fdc-196">Attendere la fine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-196">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="d6fdc-197">Registrare il server nell'insieme di credenziali utilizzando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-197">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="d6fdc-198">Passaggio 5: creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d6fdc-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="d6fdc-199">Se non si ha un account di archiviazione di Azure, creare un account con la replica geografica abilitata nella stessa area in cui si trova l'insieme di credenziali eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-199">If you don't have an Azure storage account, create a geo-replication enabled account in the same geo as the vault by running the following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="d6fdc-200">Si noti che l'account di archiviazione deve trovarsi nella stessa area geografica in cui si trova il servizio Azure Site Recovery e deve essere associato alla stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-200">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="d6fdc-201">Passaggio 6: installare l'agente di Servizi di ripristino di Azure</span><span class="sxs-lookup"><span data-stu-id="d6fdc-201">Step 6: Install the Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="d6fdc-202">Scaricare l'agente di Servizi di ripristino di Azure all'indirizzo [http:/aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) e installarlo in ogni server host Hyper-V disponibile nei cloud VMM da proteggere.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-202">Download the Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>
2. <span data-ttu-id="d6fdc-203">Eseguire il comando seguente in tutti gli host VMM:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-203">Run the following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="d6fdc-204">Passaggio 7: configurare le impostazioni di protezione del cloud</span><span class="sxs-lookup"><span data-stu-id="d6fdc-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="d6fdc-205">Creare un criterio di replica per Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-205">Create a replication policy to Azure by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="d6fdc-206">Ottenere un contenitore di protezione eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-206">Get a protection container by running the following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="d6fdc-207">Ottenere i dettagli del criterio per una variabile usando il processo creato e indicando il nome descrittivo del criterio:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-207">Get the policy details to a variable using the job that was created and mentioning the friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="d6fdc-208">Avviare l'associazione del contenitore di protezione al criterio di replica:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-208">Start the association of the protection container with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="d6fdc-209">Al termine del processo, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-209">After the job has finished, run the following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="d6fdc-210">Al termine del processo, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-210">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="d6fdc-211">Per verificare il completamento dell'operazione, attenersi alla procedura descritta in [Monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-211">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="d6fdc-212">Passaggio 8: configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="d6fdc-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="d6fdc-213">Prima di iniziare il mapping di rete, verificare che le macchine virtuali nel server VMM di origine siano connesse a una rete VM.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-213">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="d6fdc-214">Inoltre, creare una o più rete virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="d6fdc-215">Per altre informazioni su come creare una rete virtuale con Azure Resource Manager e PowerShell, vedere [Creare una rete virtuale con una connessione VPN da sito a sito usando PowerShell e Azure Resource Manager](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d6fdc-215">Learn more about how to create a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="d6fdc-216">Si noti che è possibile eseguire il mapping di più reti di macchine virtuali a una singola rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-216">Note that multiple Virtual Machine networks can be mapped to a single Azure network.</span></span> <span data-ttu-id="d6fdc-217">Se la rete di destinazione ha più subnet e una di esse ha lo stesso nome di una subnet in cui si trova la macchina virtuale di origine, la macchina virtuale di replica sarà connessa a tale subnet di destinazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-217">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after fail-over.</span></span> <span data-ttu-id="d6fdc-218">Se non è presente una subnet di destinazione con un nome corrispondente, la macchina virtuale sarà connessa alla prima subnet della rete.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-218">If there is no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

1. <span data-ttu-id="d6fdc-219">Il primo comando ottiene i server per l’insieme di credenziali corrente di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-219">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="d6fdc-220">Il comando archivia i server di Microsoft Azure Site Recovery nella variabile di matrice $Servers.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-220">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="d6fdc-221">Il secondo comando ottiene la rete di ripristino del sito per il primo server nella matrice $Servers.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-221">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="d6fdc-222">Il comando archivia le reti nella variabile $Networks.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-222">The command stores the networks in the $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="d6fdc-223">Il terzo comando ottiene le reti virtuali di Azure e quindi il valore nella variabile $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-223">The third command gets Azure virtual networks, and then that value in the $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="d6fdc-224">Il cmdlet finale crea un mapping tra la rete primaria e la rete delle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-224">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="d6fdc-225">Il cmdlet specifica la rete primaria come primo elemento di $Networks.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-225">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="d6fdc-226">Il cmdlet specifica una rete di macchine virtuali come primo elemento di $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-226">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="d6fdc-227">Passaggio 9: abilitare la protezione per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="d6fdc-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="d6fdc-228">Dopo la configurazione corretta di server, cloud e reti, sarà possibile abilitare la protezione per le macchine virtuali sul cloud.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-228">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

 <span data-ttu-id="d6fdc-229">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-229">Note the following:</span></span>

* <span data-ttu-id="d6fdc-230">Le macchine virtuali devono essere conformi ai requisiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="d6fdc-231">Vedere tali requisiti nei collegamenti relativi a [prerequisiti e supporto](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) nella guida alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in the planning guide.</span></span>
* <span data-ttu-id="d6fdc-232">Per abilitare la protezione, è necessario che le proprietà del sistema operativo e del disco del sistema operativo siano impostate per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-232">To enable protection, the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="d6fdc-233">Quando si crea una macchina virtuale basata su un modello di macchina virtuale VMM è possibile impostare la proprietà.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-233">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="d6fdc-234">È possibile impostare queste proprietà anche per le macchine virtuali esistenti nelle schede **Generale** e **Configurazione hardware** delle proprietà delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-234">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="d6fdc-235">Se queste proprietà non vengono impostate in VMM, sarà possibile configurarle nel portale di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-235">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="d6fdc-236">Per abilitare la protezione, eseguire il comando seguente per ottenere il contenitore di protezione:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-236">To enable protection, run the following command to get the protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="d6fdc-237">Ottenere l'entità di protezione (VM) eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-237">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="d6fdc-238">Abilitare il ripristino di emergenza per la macchina virtuale eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-238">Enable the DR for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="d6fdc-239">Testare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d6fdc-239">Test your deployment</span></span>
<span data-ttu-id="d6fdc-240">Per testare la distribuzione, è possibile eseguire un failover di test per una singola macchina virtuale oppure creare un piano di ripristino costituito da più macchine virtuali ed eseguire un failover di test per il piano.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-240">To test your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for the plan.</span></span> <span data-ttu-id="d6fdc-241">Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="d6fdc-242">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-242">Note that:</span></span>

* <span data-ttu-id="d6fdc-243">Per eseguire la connessione alla macchina virtuale in Azure tramite Desktop remoto dopo il failover, abilitare Connessione Desktop remoto sulla macchina virtuale prima di eseguire il failover di test.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-243">If you want to connect to the virtual machine in Azure using Remote Desktop after the fail-over, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="d6fdc-244">Dopo il failover si userà un indirizzo IP pubblico per connettersi alla macchina virtuale in Azure tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-244">After fail-over, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="d6fdc-245">Se si vuole procedere in questo senso, assicurarsi che non siano presenti criteri di dominio che impediscono la connessione a una macchina virtuale mediante un indirizzo pubblico.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-245">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="d6fdc-246">Per verificare il completamento dell'operazione, attenersi alla procedura descritta in [Monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="d6fdc-246">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="d6fdc-247">Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="d6fdc-247">Run a test failover</span></span>
- <span data-ttu-id="d6fdc-248">Avviare il failover di test eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-248">Start the test failover by running the following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="d6fdc-249">Eseguire un failover pianificato</span><span class="sxs-lookup"><span data-stu-id="d6fdc-249">Run a planned failover</span></span>
- <span data-ttu-id="d6fdc-250">Avviare il failover pianificato eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-250">Start the planned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="d6fdc-251">Eseguire un failover non pianificato</span><span class="sxs-lookup"><span data-stu-id="d6fdc-251">Run an unplanned failover</span></span>
- <span data-ttu-id="d6fdc-252">Avviare il failover non pianificato eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6fdc-252">Start the unplanned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="d6fdc-253"><a name=monitor></a> Monitorare l'attività</span><span class="sxs-lookup"><span data-stu-id="d6fdc-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="d6fdc-254">Utilizzare i comandi seguenti per monitorare l'attività.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-254">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="d6fdc-255">Si noti che è necessario attendere l'esecuzione dei processi per il completamento dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-255">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="d6fdc-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6fdc-256">Next steps</span></span>
<span data-ttu-id="d6fdc-257">[Altre informazioni](/powershell/module/azurerm.recoveryservices.backup/#recovery) su Azure Site Recovery con i cmdlet PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6fdc-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
