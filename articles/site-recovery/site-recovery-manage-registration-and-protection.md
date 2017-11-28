---
title: Server aaaRemove e disabilitare la protezione | Documenti Microsoft
description: In questo articolo descrive come insieme di credenziali server toounregister da un ripristino del sito e protezione toodisable per le macchine virtuali e server fisici.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="48666-103">Rimuovere server e disabilitare la protezione</span><span class="sxs-lookup"><span data-stu-id="48666-103">Remove servers and disable protection</span></span>

<span data-ttu-id="48666-104">servizio Azure Site Recovery Hello contribuisce tooyour continuità aziendale e strategia di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="48666-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="48666-105">servizio Hello Orchestra la replica, failover e il ripristino delle macchine virtuali e server fisici.</span><span class="sxs-lookup"><span data-stu-id="48666-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="48666-106">Macchine possono essere replicati tooAzure o tooa locale secondario data center.</span><span class="sxs-lookup"><span data-stu-id="48666-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="48666-107">Per una rapida panoramica, leggere [Che cos'è Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="48666-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="48666-108">In questo articolo viene descritto come server toounregister da servizi di ripristino di un insieme di credenziali nel portale di Azure hello e come toodisable protezione per i computer protetti da Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="48666-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="48666-109">Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="48666-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="48666-110">Annullare la registrazione di un server di configurazione connesso</span><span class="sxs-lookup"><span data-stu-id="48666-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="48666-111">Se si replica le macchine virtuali VMware o tooAzure server fisici Windows/Linux, è possibile annullare la registrazione di un server di configurazione connessa da un insieme di credenziali come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="48666-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="48666-112">Disabilitare la protezione delle macchine.</span><span class="sxs-lookup"><span data-stu-id="48666-112">Disable machine protection.</span></span> <span data-ttu-id="48666-113">In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="48666-114">Annullare l'associazione di tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="48666-114">Disassociate any policies.</span></span> <span data-ttu-id="48666-115">In **infrastruttura di Site Recovery** > **per VMWare & macchine fisiche** > **criteri di replica**, fare doppio clic su hello criteri associati.</span><span class="sxs-lookup"><span data-stu-id="48666-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="48666-116">Server di configurazione rapida hello > **Dissocia**.</span><span class="sxs-lookup"><span data-stu-id="48666-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="48666-117">Rimuovere qualsiasi server di destinazione master o di elaborazione locale aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="48666-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="48666-118">In **infrastruttura di Site Recovery** > **per VMWare & macchine fisiche** > **server di configurazione**, server hello pulsante destro del mouse > **Eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="48666-119">Eliminare il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="48666-120">Disinstallare manualmente il servizio di mobilità hello in esecuzione nel server di destinazione master hello (sarà entrambi un apposito server o in esecuzione nel server di configurazione hello).</span><span class="sxs-lookup"><span data-stu-id="48666-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="48666-121">Disinstallare eventuali server di elaborazione aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="48666-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="48666-122">Disinstallare il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="48666-123">Nel server di configurazione hello, disinstallare l'istanza di hello di MySQL che è stata installata mediante il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="48666-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="48666-124">Nel Registro di sistema di hello hello del server di configurazione eliminare la chiave di hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="48666-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="48666-125">Annullare la registrazione di un server di configurazione non connesso</span><span class="sxs-lookup"><span data-stu-id="48666-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="48666-126">Se si replica le macchine virtuali VMware o tooAzure server fisici Windows/Linux, è possibile annullare la registrazione di un server di configurazione non è connesso da un insieme di credenziali come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="48666-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="48666-127">Disabilitare la protezione delle macchine.</span><span class="sxs-lookup"><span data-stu-id="48666-127">Disable machine protection.</span></span> <span data-ttu-id="48666-128">In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="48666-129">Selezionare **Interrompi gestione macchina hello**.</span><span class="sxs-lookup"><span data-stu-id="48666-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="48666-130">Rimuovere qualsiasi server di destinazione master o di elaborazione locale aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="48666-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="48666-131">In **infrastruttura di Site Recovery** > **per VMWare & macchine fisiche** > **server di configurazione**, server hello pulsante destro del mouse > **Eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="48666-132">Eliminare il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="48666-133">Disinstallare manualmente il servizio di mobilità hello in esecuzione nel server di destinazione master hello (sarà entrambi un apposito server o in esecuzione nel server di configurazione hello).</span><span class="sxs-lookup"><span data-stu-id="48666-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="48666-134">Disinstallare eventuali server di elaborazione aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="48666-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="48666-135">Disinstallare il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="48666-136">Nel server di configurazione hello, disinstallare l'istanza di hello di MySQL che è stata installata mediante il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="48666-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="48666-137">Nel Registro di sistema di hello hello del server di configurazione eliminare la chiave di hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="48666-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="48666-138">Annullare la registrazione di un server VMM connesso</span><span class="sxs-lookup"><span data-stu-id="48666-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="48666-139">Come procedura consigliata, è consigliabile annullare la registrazione server VMM hello quando è connesso tooAzure.</span><span class="sxs-lookup"><span data-stu-id="48666-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="48666-140">In questo modo si garantisce che le impostazioni nel server VMM hello (e su altri server VMM con i cloud associati) vengano pulite correttamente.</span><span class="sxs-lookup"><span data-stu-id="48666-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="48666-141">Si consiglia di rimuovere un server non connesso solo in caso di problema di connettività permanente.</span><span class="sxs-lookup"><span data-stu-id="48666-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="48666-142">Se non è connesso il server VMM hello, sarà necessario toomanually un tooclean script le impostazioni di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="48666-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="48666-143">Arrestare la replica delle macchine virtuali nel cloud nel server VMM si desidera tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="48666-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="48666-144">Eliminare tutti i mapping di rete utilizzati dal cloud nel server VMM si desidera toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="48666-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="48666-145">In **infrastruttura di Site Recovery** > **per System Center VMM** > **Mapping di rete**, fare doppio clic su mapping di rete hello >  **Eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="48666-146">Annullare l'associazione dei criteri di replica dal cloud nel server VMM si desidera tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="48666-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="48666-147">In **infrastruttura di Site Recovery** > **per System Center VMM** >  **criteri di replica**, fare doppio clic sul criterio hello associata.</span><span class="sxs-lookup"><span data-stu-id="48666-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="48666-148">Fare doppio clic su cloud hello > **Dissocia**.</span><span class="sxs-lookup"><span data-stu-id="48666-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="48666-149">Eliminare il server VMM hello o nodo attivo di VMM.</span><span class="sxs-lookup"><span data-stu-id="48666-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="48666-150">In **infrastruttura di Site Recovery** > **per System Center VMM** > **server VMM**, server hello rapida >  **Eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="48666-151">Disinstallare hello Provider manualmente nel server VMM di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="48666-152">Se si dispone di un cluster, eseguire la rimozione da tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="48666-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="48666-153">Se si esegue la replica tooAzure, rimuovere manualmente l'agente di servizi di ripristino di Microsoft hello dagli host Hyper-V nei cloud hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="48666-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="48666-154">Annullare la registrazione di un server VMM non connesso</span><span class="sxs-lookup"><span data-stu-id="48666-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="48666-155">Arrestare la replica delle macchine virtuali nel cloud nel server VMM si desidera tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="48666-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="48666-156">Eliminare tutti i mapping di rete utilizzati dal cloud nel server VMM hello che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="48666-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="48666-157">In **infrastruttura di Site Recovery** > **per System Center VMM** > **Mapping di rete**, fare doppio clic su mapping di rete hello >  **Eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="48666-158">Annotare l'ID di hello del server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="48666-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="48666-159">Annullare l'associazione dei criteri di replica dal cloud nel server VMM si desidera tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="48666-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="48666-160">In **infrastruttura di Site Recovery** > **per System Center VMM** >  **criteri di replica**, fare doppio clic sul criterio hello associata.</span><span class="sxs-lookup"><span data-stu-id="48666-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="48666-161">Fare doppio clic su cloud hello > **Dissocia**.</span><span class="sxs-lookup"><span data-stu-id="48666-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="48666-162">Eliminare il server VMM hello o nodo attivo.</span><span class="sxs-lookup"><span data-stu-id="48666-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="48666-163">In **infrastruttura di Site Recovery** > **per System Center VMM** > **server VMM**, server hello rapida >  **Eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="48666-164">Scaricare ed eseguire hello [script di pulizia](http://aka.ms/asr-cleanup-script-vmm) nel server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="48666-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="48666-165">Aprire PowerShell con hello **Esegui come amministratore** opzione criteri di esecuzione hello toochange per l'ambito predefinito (LocalMachine) hello.</span><span class="sxs-lookup"><span data-stu-id="48666-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="48666-166">Nello script hello, specificare ID hello del server VMM si desidera tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="48666-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="48666-167">script Hello rimuove la registrazione e le informazioni dal server hello associazione cloud.</span><span class="sxs-lookup"><span data-stu-id="48666-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="48666-168">Eseguire script di pulizia hello in qualsiasi altro server VMM che contengono cloud che vengono associati a cloud nel server VMM si desidera tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="48666-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="48666-169">Eseguire script di pulizia hello in qualsiasi altro passivi nodi cluster VMM contenenti hello che provider installato.</span><span class="sxs-lookup"><span data-stu-id="48666-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="48666-170">Disinstallare hello Provider manualmente nel server VMM di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="48666-171">Se si dispone di un cluster, eseguire la rimozione da tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="48666-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="48666-172">Se si replica tooAzure, è possibile rimuovere l'agente di servizi di ripristino di Microsoft hello dagli host Hyper-V nei cloud hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="48666-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="48666-173">Annullare la registrazione di un host Hyper-V in un sito di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="48666-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="48666-174">Gli host Hyper-V non gestiti da VMM vengono raccolti in un sito di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="48666-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="48666-175">Rimuovere un host in un sito di Hyper-V nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="48666-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="48666-176">Disabilitare la replica per le macchine virtuali Hyper-V nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="48666-177">Annullare l'associazione di criteri per il sito Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="48666-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="48666-178">In **infrastruttura di Site Recovery** > **per i siti Hyper-V** >  **criteri di replica**, fare doppio clic sul criterio hello associata.</span><span class="sxs-lookup"><span data-stu-id="48666-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="48666-179">Sito hello rapida > **Dissocia**.</span><span class="sxs-lookup"><span data-stu-id="48666-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="48666-180">Eliminare gli host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="48666-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="48666-181">In **infrastruttura di Site Recovery** > **per System Center VMM** > **host Hyper-V**, server hello rapida >  **Eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="48666-182">Eliminare il sito Hyper-V hello dopo tutti gli host sono state rimosse da quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="48666-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="48666-183">In **infrastruttura di Site Recovery** > **per System Center VMM** > **siti Hyper-V**, sito hello rapida >  **Eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="48666-184">Eseguire lo script seguente in ogni host Hyper-V che è stata rimossa hello.</span><span class="sxs-lookup"><span data-stu-id="48666-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="48666-185">script di Hello pulisce le impostazioni nel server di hello e ne annulla la registrazione dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="48666-186">Disabilitare la protezione per una VM VMware o un server fisico</span><span class="sxs-lookup"><span data-stu-id="48666-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="48666-187">In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="48666-188">In **Rimuovi macchina virtuale** selezionare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="48666-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="48666-189">**Disabilitare la protezione per macchina hello (scelta consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="48666-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="48666-190">Utilizzare questa opzione toostop replica macchina hello.</span><span class="sxs-lookup"><span data-stu-id="48666-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="48666-191">Le impostazioni di Site Recovery verranno rimosse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="48666-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="48666-192">Viene visualizzata solo l'opzione hello seguenti circostanze:</span><span class="sxs-lookup"><span data-stu-id="48666-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="48666-193">**È stato ridimensionato volume VM hello**: quando si ridimensiona un hello volume virtuale computer entra in uno stato critico.</span><span class="sxs-lookup"><span data-stu-id="48666-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="48666-194">Selezionare questa protezione toodisables opzione mantenendo i punti di ripristino in Azure.</span><span class="sxs-lookup"><span data-stu-id="48666-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="48666-195">Quando si abilita di nuovo la protezione per macchina hello, i dati per il volume ridimensionato hello hello sono tooAzure trasferiti.</span><span class="sxs-lookup"><span data-stu-id="48666-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="48666-196">**Eseguire un failover recente**, dopo aver eseguito un failover tootest l'ambiente, selezionare questa opzione toostart proteggere nuovamente il computer locale.</span><span class="sxs-lookup"><span data-stu-id="48666-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="48666-197">Disabilita ogni macchina virtuale e quindi è necessario tooenable protezione per tali nuovamente.</span><span class="sxs-lookup"><span data-stu-id="48666-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="48666-198">Disabilitazione macchina hello con questa impostazione non influisce sulla macchina virtuale di replica hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="48666-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="48666-199">Non disinstallare il servizio di mobilità hello dalla macchina di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="48666-200">**Interrompi gestione macchina hello**.</span><span class="sxs-lookup"><span data-stu-id="48666-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="48666-201">Se si seleziona questa opzione, verrà rimossa solo macchina hello dall'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="48666-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="48666-202">Le impostazioni di protezione locali per la macchina hello non saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="48666-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="48666-203">impostazioni tooremove macchina hello e tooremove hello macchina da hello sottoscrizione di Azure, è necessario impostazioni hello tooclean, disinstallare il servizio di mobilità hello.</span><span class="sxs-lookup"><span data-stu-id="48666-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="48666-204">Disabilitare la protezione per una VM Hyper-V in un cloud VMM</span><span class="sxs-lookup"><span data-stu-id="48666-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="48666-205">In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="48666-206">In **Rimuovi macchina virtuale** selezionare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="48666-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="48666-207">**Disabilitare la protezione per macchina hello (scelta consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="48666-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="48666-208">Utilizzare questa opzione toostop replica macchina hello.</span><span class="sxs-lookup"><span data-stu-id="48666-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="48666-209">Le impostazioni di Site Recovery verranno rimosse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="48666-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="48666-210">**Interrompi gestione macchina hello**.</span><span class="sxs-lookup"><span data-stu-id="48666-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="48666-211">Se si seleziona questa opzione, verrà rimossa solo macchina hello dall'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="48666-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="48666-212">Le impostazioni di protezione locali per la macchina hello non saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="48666-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="48666-213">impostazioni tooremove macchina hello e tooremove hello macchina da hello sottoscrizione di Azure, sono necessarie tooclean hello impostazioni backup manualmente, usando le istruzioni di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="48666-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="48666-214">Si noti che se si seleziona macchina virtuale di toodelete hello e relativi dischi rigidi, essi verranno essere rimosso dal percorso di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="48666-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="48666-215">Pulire le impostazioni di protezione - sito di replica tooa secondario VMM</span><span class="sxs-lookup"><span data-stu-id="48666-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="48666-216">Se si seleziona **Interrompi gestione macchina hello** ed è la replica tooa sito secondario, eseguire questo script su hello server primario tooclean le impostazioni di hello per una macchina virtuale primaria hello.</span><span class="sxs-lookup"><span data-stu-id="48666-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="48666-217">Nella console VMM hello fare clic sulla console di VMM PowerShell hello hello PowerShell pulsante tooopen.</span><span class="sxs-lookup"><span data-stu-id="48666-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="48666-218">Sostituire SQLVM1 con nome hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="48666-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="48666-219">Nel server VMM secondario hello eseguire questo script tooclean le impostazioni di hello per una macchina virtuale secondaria hello:</span><span class="sxs-lookup"><span data-stu-id="48666-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="48666-220">Nel server VMM secondario hello, aggiornare hello le macchine virtuali nel server host Hyper-V di hello, in modo che hello secondario VM Ottiene rilevato nuovamente nella console VMM hello.</span><span class="sxs-lookup"><span data-stu-id="48666-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="48666-221">cancellare le impostazioni di replica hello nel server VMM hello Hello sopra passaggi.</span><span class="sxs-lookup"><span data-stu-id="48666-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="48666-222">Se si desidera che la replica per la macchina virtuale hello, eseguire lo script seguente oh hello toostop hello macchine virtuali primarie e secondarie.</span><span class="sxs-lookup"><span data-stu-id="48666-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="48666-223">Sostituire SQLVM1 con nome hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="48666-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="48666-224">Pulire le impostazioni di protezione dati - replica tooAzure</span><span class="sxs-lookup"><span data-stu-id="48666-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="48666-225">Se si seleziona **Interrompi gestione macchina hello** e replicare tooAzure, eseguire questo script nel server VMM di origine hello, usando PowerShell dalla console VMM hello.</span><span class="sxs-lookup"><span data-stu-id="48666-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="48666-226">Hello sopra passaggi cancellare le impostazioni di replica hello nel server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="48666-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="48666-227">replica toostop per la macchina virtuale hello in esecuzione nel server host Hyper-V di hello, eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="48666-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="48666-228">Sostituire SQLVM1 con nome hello di macchina virtuale e host01.contoso.com con nome hello del server host Hyper-V di hello.</span><span class="sxs-lookup"><span data-stu-id="48666-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="48666-229">Disabilitare la protezione per una VM Hyper-V in un sito Hyper-V</span><span class="sxs-lookup"><span data-stu-id="48666-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="48666-230">Utilizzare questa procedura se si esegue la replica di macchine virtuali Hyper-V tooAzure senza un server VMM.</span><span class="sxs-lookup"><span data-stu-id="48666-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="48666-231">In **elementi protetti** > **elementi replicati**, macchina hello rapida > **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="48666-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="48666-232">In **Rimuovi macchina**, è possibile selezionare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="48666-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="48666-233">**Disabilitare la protezione per macchina hello (scelta consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="48666-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="48666-234">Utilizzare questa opzione toostop replica macchina hello.</span><span class="sxs-lookup"><span data-stu-id="48666-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="48666-235">Le impostazioni di Site Recovery verranno rimosse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="48666-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="48666-236">**Interrompi gestione macchina hello**.</span><span class="sxs-lookup"><span data-stu-id="48666-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="48666-237">Se si seleziona questa opzione solo macchina hello verrà rimosso dall'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="48666-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="48666-238">Le impostazioni di protezione locali per la macchina hello non saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="48666-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="48666-239">impostazioni tooremove macchina hello e tooremove hello della macchina virtuale da hello sottoscrizione di Azure, sono necessarie tooclean hello impostazioni backup manualmente.</span><span class="sxs-lookup"><span data-stu-id="48666-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="48666-240">Se si seleziona macchina virtuale di toodelete hello e relativi dischi rigidi che verranno rimossi dal percorso di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="48666-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="48666-241">Se si seleziona **Interrompi gestione macchina hello**, eseguire questo script nel server host Hyper-V di origine di hello, tooremove replica per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="48666-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="48666-242">Sostituire SQLVM1 con nome hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="48666-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
