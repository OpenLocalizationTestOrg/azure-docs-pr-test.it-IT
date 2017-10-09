---
title: le macchine virtuali Hyper-V nel sito secondario di VMM tooa con PowerShell (Gestione risorse di Azure) aaaReplicate | Documenti Microsoft
description: Viene descritto come replica tooorchestrate di Azure Site Recovery toodeploy, failover e il ripristino delle macchine virtuali Hyper-V in VMM cloud sito VMM secondario tooa tramite PowerShell, Gestione risorse)
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="a0e9f-103">Replicare le macchine virtuali Hyper-V in VMM cloud tooa sito VMM secondario tramite PowerShell, Gestione risorse)</span><span class="sxs-lookup"><span data-stu-id="a0e9f-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0e9f-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a0e9f-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="a0e9f-105">Portale classico</span><span class="sxs-lookup"><span data-stu-id="a0e9f-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="a0e9f-106">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="a0e9f-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="a0e9f-107">Benvenuti tooAzure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="a0e9f-108">Se si desidera tooreplicate locale Hyper-V le macchine virtuali gestite nel sito secondario tooa cloud di System Center Virtual Machine Manager (VMM), usare questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="a0e9f-109">Questo articolo illustra in che modo toouse PowerShell tooautomate comuni attività è necessario tooperform quando si configura macchine virtuali di Azure Site Recovery tooreplicate Hyper-V nei cloud VMM di System Center VMM cloud tooSystem Center nel sito secondario.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="a0e9f-110">articolo Hello sono inclusi i prerequisiti per scenario hello e Mostra</span><span class="sxs-lookup"><span data-stu-id="a0e9f-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="a0e9f-111">Come tooset di un insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="a0e9f-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="a0e9f-112">Installare hello Provider di Azure Site Recovery nel server VMM di origine hello e server VMM di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="a0e9f-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="a0e9f-113">Registrare i server VMM hello nell'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="a0e9f-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="a0e9f-114">Configurare i criteri di replica per hello Cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="a0e9f-115">le impostazioni di replica Hello nei criteri hello saranno applicati tooall protetto le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a0e9f-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="a0e9f-116">Abilitare la protezione per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="a0e9f-117">Test del failover delle macchine virtuali hello singolarmente o come parte del ripristino di un piano toomake che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="a0e9f-118">Eseguire un pianificato o un failover non pianificato di macchine virtuali, singolarmente o come parte di un toomake piano di ripristino che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="a0e9f-119">Se si verificano problemi durante l'impostazione di questo scenario, è possibile pubblicare domande sul hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="a0e9f-120">Azure offre due diversi [modelli di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md) per creare e usare le risorse: Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a0e9f-121">Azure offre inoltre due portali: hello portale di Azure classico che supporta il modello di distribuzione classica hello e hello portale di Azure con il supporto per entrambi i modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="a0e9f-122">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="a0e9f-123">Prerequisiti locali</span><span class="sxs-lookup"><span data-stu-id="a0e9f-123">On-premises prerequisites</span></span>
<span data-ttu-id="a0e9f-124">Ecco cosa è necessario in hello primario e secondario locale siti toodeploy questo scenario:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="a0e9f-125">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="a0e9f-125">**Prerequisites**</span></span> | <span data-ttu-id="a0e9f-126">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="a0e9f-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="a0e9f-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="a0e9f-127">**VMM**</span></span> |<span data-ttu-id="a0e9f-128">È consigliabile che distribuire un server VMM nel sito primario di hello e un server VMM nel sito secondario hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="a0e9f-129">È possibile anche [eseguire la replica tra cloud in un singolo server VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="a0e9f-130">toodo questo è necessario almeno due cloud configurati nei server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="a0e9f-131">Server VMM devono essere in esecuzione almeno System Center 2012 SP1 con gli aggiornamenti più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="a0e9f-132">Ogni server VMM deve avere uno o più cloud configurati e tutte le aree è necessario impostare il profilo di capacità Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="a0e9f-133">I cloud devono contenere uno o più gruppi host VMM.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="a0e9f-134">Ulteriori informazioni sull'impostazione dei cloud VMM in [hello configurazione VMM cloud dell'infrastruttura](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), e [procedura dettagliata: creazione di cloud privati con System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="a0e9f-135">I server VMM devono disporre di accesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="a0e9f-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="a0e9f-136">**Hyper-V**</span></span> |<span data-ttu-id="a0e9f-137">Server Hyper-V deve essere in esecuzione almeno Windows Server 2012 con il ruolo Hyper-V hello e avere hello installati aggiornamenti più recenti.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="a0e9f-138">Il server Hyper-V deve contenere una o più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="a0e9f-139">Server host Hyper-V devono essere distribuiti nei gruppi host nei cloud VMM primario e secondario di hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="a0e9f-140">Se si esegue Hyper-V in un cluster su Windows Server 2012 R2 è necessario installare l'[aggiornamento 2961977](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="a0e9f-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="a0e9f-141">Se si esegue Hyper-V in un cluster basato su indirizzi IP statici in Windows Server 2012, il gestore del cluster non viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="a0e9f-142">È necessario un gestore cluster hello tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="a0e9f-143">[Altre informazioni](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="a0e9f-144">**Provider**</span><span class="sxs-lookup"><span data-stu-id="a0e9f-144">**Provider**</span></span> |<span data-ttu-id="a0e9f-145">Durante la distribuzione di Site Recovery hello Provider di Azure Site Recovery viene installato nel server VMM.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="a0e9f-146">Hello Provider comunica con il ripristino del sito tramite replica tooorchestrate HTTPS 443.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="a0e9f-147">La replica dei dati si verifica tra i server di Hyper-V primari e secondari di hello su hello LAN o una connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="a0e9f-148">Hello Provider in esecuzione nel server VMM hello deve accedere URL toothese: *. c o m; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. n e t; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="a0e9f-149">Inoltre consentire le comunicazioni di firewall da hello VMM server toohello [intervalli IP Data Center di Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e consentire il protocollo HTTPS (443) di hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="a0e9f-150">Prerequisiti di mapping di rete</span><span class="sxs-lookup"><span data-stu-id="a0e9f-150">Network mapping prerequisites</span></span>
<span data-ttu-id="a0e9f-151">Rete viene eseguito il mapping tra i server VMM primari e secondari di hello per le reti VM di VMM:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="a0e9f-152">Posizionare in modo ottimale le macchine virtuali di replica in host Hyper-V secondari dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="a0e9f-153">Connettere le reti VM di tooappropriate macchine virtuali di replica.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="a0e9f-154">Se non si configura rete mapping replica le macchine virtuali non saranno connesse tooany rete dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="a0e9f-155">Se si desidera tooset rete mapping durante il ripristino del sito distribuzione qui è ciò che è necessario:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="a0e9f-156">Assicurarsi che le macchine virtuali di origine hello server host Hyper-V siano connesso tooa rete VM di VMM.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="a0e9f-157">La rete deve essere collegato tooa la rete logica associata al cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="a0e9f-158">Verificare che i cloud secondario hello che verrà utilizzato per il ripristino sia configurata una rete VM corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="a0e9f-159">Rete VM deve essere collegato tooa la rete logica associata a cloud secondario hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="a0e9f-160">Ulteriori informazioni sulla configurazione delle reti VMM in hello di sotto di articoli</span><span class="sxs-lookup"><span data-stu-id="a0e9f-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="a0e9f-161">Come tooconfigure reti logiche in VMM</span><span class="sxs-lookup"><span data-stu-id="a0e9f-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="a0e9f-162">Modalità VM tooconfigure reti e gateway in VMM</span><span class="sxs-lookup"><span data-stu-id="a0e9f-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="a0e9f-163">[Altre informazioni](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sul funzionamento del mapping di rete.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="a0e9f-164">Prerequisiti di PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0e9f-164">PowerShell prerequisites</span></span>
<span data-ttu-id="a0e9f-165">Assicurarsi di disporre di Azure PowerShell pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="a0e9f-166">Se si sta già usando PowerShell, è necessario tooupgrade tooversion 0.8.10 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="a0e9f-167">Per informazioni sull'impostazione di PowerShell, vedere hello [tooinstall della Guida e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a0e9f-168">Dopo aver impostato e configurato PowerShell, è possibile visualizzare tutti i cmdlet disponibili di hello per servizio hello [qui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="a0e9f-169">toolearn sui suggerimenti che consentono di utilizzare i cmdlet di hello, ad esempio come i valori dei parametri, input e output vengono in genere gestiti in Azure PowerShell, vedere hello [Guida introduttiva ai cmdlet di Azure tooget](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="a0e9f-170">Passaggio 1: Impostare una sottoscrizione di hello</span><span class="sxs-lookup"><span data-stu-id="a0e9f-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="a0e9f-171">Da Azure powershell, account di accesso tooyour account di Azure: hello seguente cmdlet utilizzando</span><span class="sxs-lookup"><span data-stu-id="a0e9f-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="a0e9f-172">Ottenere un elenco delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="a0e9f-173">Questo ID sottoscrizione hello elencherà anche per ognuna delle sottoscrizioni hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="a0e9f-174">Annotare l'ID sottoscrizione hello di sottoscrizione hello in cui si desidera l'insieme di credenziali toocreate hello recovery services</span><span class="sxs-lookup"><span data-stu-id="a0e9f-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="a0e9f-175">Impostare hello sottoscrizione in cui hello credenziali di servizi di ripristino sono toobe creato da citare hello ID di sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="a0e9f-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="a0e9f-176">Passaggio 2: Creare l'insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="a0e9f-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="a0e9f-177">Creare un gruppo di risorse di Azure Resource Manager, se non ne è già disponibile uno.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="a0e9f-178">Creare un nuovo insieme di credenziali di servizi di ripristino e salvare hello creato l'oggetto insieme di credenziali di ripristino automatico di sistema in una variabile (verrà utilizzata in un secondo momento).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="a0e9f-179">È inoltre possibile recuperare hello ripristino automatico di sistema dell'insieme di credenziali post di creazione di un oggetto utilizzando il cmdlet Get-AzureRMRecoveryServicesVault hello:-</span><span class="sxs-lookup"><span data-stu-id="a0e9f-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="a0e9f-180">Passaggio 3: Impostare il contesto di archivio di servizi di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="a0e9f-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="a0e9f-181">Se si dispone di un insieme di credenziali già creato, eseguire hello di sotto dell'insieme di credenziali di comando tooget hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="a0e9f-182">Impostare il contesto di insieme di credenziali hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="a0e9f-183">Passaggio 4: Installare il Provider di Azure Site Recovery hello</span><span class="sxs-lookup"><span data-stu-id="a0e9f-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="a0e9f-184">Nel computer VMM hello, creare una directory eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="a0e9f-185">Estrarre il file hello utilizzando provider hello scaricato eseguendo hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="a0e9f-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="a0e9f-186">Installare il provider di hello utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-186">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="a0e9f-187">Attendere toofinish installazione hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="a0e9f-188">Registrare server hello in hello insieme di credenziali hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="a0e9f-189">Passaggio 5: Creare e associare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="a0e9f-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="a0e9f-190">Creare un criterio di replica Hyper-V 2012 R2 eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="a0e9f-191">Hello cloud VMM può contenere host Hyper-V che eseguono versioni diverse di Windows Server (come indicato nei prerequisiti di Hyper-V hello), ma i criteri di replica hello sono versione del sistema operativo specifico.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="a0e9f-192">Se si dispone di diversi host in esecuzione in versioni diverse del sistema operativo, creare criteri di replica individuali per ogni tipo di versione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="a0e9f-193">Ad esempio: se si dispone di cinque host in esecuzione su Windows Server 2012 e tre su Windows Server 2012 R2, creare due criteri di replica, uno per ogni tipo di versione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="a0e9f-194">Ottenere il contenitore di protezione primaria hello (Cloud VMM primario) e il contenitore di protezione recovery (ripristino di VMM Cloud) eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="a0e9f-195">Recupero dei criteri di hello creato nel passaggio 1 con nome descrittivo di hello del criterio di hello</span><span class="sxs-lookup"><span data-stu-id="a0e9f-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="a0e9f-196">Avviare associazione hello del contenitore di protezione hello (Cloud VMM) con il criterio di replica hello:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="a0e9f-197">Attendere hello criteri associazione processo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="a0e9f-198">È possibile verificare se il processo di hello è stata completata con hello seguente frammento di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="a0e9f-199">Dopo il processo di hello ha terminato l'elaborazione, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="a0e9f-200">completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="a0e9f-201">Passaggio 6: Configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="a0e9f-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="a0e9f-202">Hello primo comando Ottiene i server per insieme di credenziali di hello corrente Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="a0e9f-203">comando Hello archivia i server di Microsoft Azure Site Recovery hello nella variabile di matrice hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="a0e9f-204">Hello seguito comandi ottenere hello sito ripristino rete per server VMM di origine hello e hello destinazione VMM.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="a0e9f-205">server VMM di origine Hello può essere hello prima o una matrice di hello secondo hello in un server.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="a0e9f-206">Controllare i nomi di hello del server VMM hello e recuperare le reti di hello in modo appropriato</span><span class="sxs-lookup"><span data-stu-id="a0e9f-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="a0e9f-207">Hello finale cmdlet crea un mapping tra la rete primaria hello e rete ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="a0e9f-208">cmdlet di Hello specifica rete primaria hello come primo elemento di hello della rete di ripristino $PrimaryNetworks e hello come primo elemento di hello di $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="a0e9f-209">Passaggio 7: Configurare il mapping di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a0e9f-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="a0e9f-210">Hello comando seguente ottiene l'elenco di hello di classificazioni di archiviazione nella variabile $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="a0e9f-211">Hello seguito comandi ottenere la classificazione di origine hello nella variabile $SourceClassificaion e la classificazione di destinazione nella variabile $TargetClassification.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="a0e9f-212">le classificazioni di origine e destinazione Hello possono essere qualsiasi elemento nella matrice hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="a0e9f-213">Fare riferimento toohello output di hello seguito indice hello toofigure di comando di classificazioni di origine e di destinazione nella matrice $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="a0e9f-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="a0e9f-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="a0e9f-215">Hello seguito cmdlet crea un mapping tra la classificazione di destinazione hello e classificazione di origine hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="a0e9f-216">Passaggio 8: Abilitare la protezione per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a0e9f-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="a0e9f-217">Dopo che le reti, cloud e i server hello sono configurate correttamente, è possibile abilitare la protezione per le macchine virtuali nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="a0e9f-218">protezione tooenable, eseguire hello contenitore di protezione hello tooget comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="a0e9f-219">Ottenere entità di protezione hello (VM) eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="a0e9f-220">Abilitare la replica per hello VM eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="a0e9f-221">Testare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a0e9f-221">Test your deployment</span></span>
<span data-ttu-id="a0e9f-222">pianificare la distribuzione, è possibile eseguire un failover di test per una singola macchina virtuale o creare un piano di ripristino costituita da più macchine virtuali ed eseguire un failover di test per hello tootest.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="a0e9f-223">Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e9f-224">È possibile creare un piano di ripristino per l'applicazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="a0e9f-225">completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a0e9f-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="a0e9f-226">Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="a0e9f-226">Run a test failover</span></span>
1. <span data-ttu-id="a0e9f-227">Eseguire hello seguito cmdlet tooget hello VM rete toowhich desiderato tootest failover le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="a0e9f-228">Eseguire un failover di test di una macchina virtuale eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="a0e9f-229">Eseguire un failover di test di un piano di ripristino eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="a0e9f-230">Eseguire un failover pianificato</span><span class="sxs-lookup"><span data-stu-id="a0e9f-230">Run a planned failover</span></span>
1. <span data-ttu-id="a0e9f-231">Eseguire un failover pianificato di una macchina virtuale eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="a0e9f-232">Eseguire un failover pianificato di un piano di ripristino eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="a0e9f-233">Eseguire un failover non pianificato</span><span class="sxs-lookup"><span data-stu-id="a0e9f-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="a0e9f-234">Eseguire un failover non pianificato di una macchina virtuale eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="a0e9f-235">2. eseguire un failover non pianificato di un piano di ripristino eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0e9f-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="a0e9f-236"><a name=monitor></a> Monitorare l'attività</span><span class="sxs-lookup"><span data-stu-id="a0e9f-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="a0e9f-237">Utilizzare hello attività hello toomonitor di comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="a0e9f-238">Si noti la presenza di toowait tra i processi per hello toofinish di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="a0e9f-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0e9f-239">Next steps</span></span>
<span data-ttu-id="a0e9f-240">[Altre informazioni](/powershell/module/azurerm.recoveryservices.backup/#recovery) su Azure Site Recovery con i cmdlet PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a0e9f-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
