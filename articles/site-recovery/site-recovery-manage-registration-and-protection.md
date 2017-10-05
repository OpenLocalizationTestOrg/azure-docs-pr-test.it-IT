---
title: Rimuovere server e disabilitare la protezione | Documentazione Microsoft
description: Questo articolo descrive come annullare la registrazione di server da un insieme di credenziali di Site Recovery e per disabilitare la protezione per le macchine virtuali e i server fisici.
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
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="47bae-103">Rimuovere server e disabilitare la protezione</span><span class="sxs-lookup"><span data-stu-id="47bae-103">Remove servers and disable protection</span></span>

<span data-ttu-id="47bae-104">Il servizio Azure Site Recovery contribuisce al miglioramento della strategia di continuità aziendale e ripristino di emergenza (BCDR),</span><span class="sxs-lookup"><span data-stu-id="47bae-104">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="47bae-105">coordinando la replica, il failover e il ripristino di macchine virtuali e server fisici.</span><span class="sxs-lookup"><span data-stu-id="47bae-105">The service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="47bae-106">È possibile replicare i computer in Azure o in un data center locale secondario.</span><span class="sxs-lookup"><span data-stu-id="47bae-106">Machines can be replicated to Azure, or to a secondary on-premises data center.</span></span> <span data-ttu-id="47bae-107">Per una rapida panoramica, leggere [Che cos'è Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="47bae-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="47bae-108">Questo articolo descrive come annullare la registrazione di server dall'insieme di credenziali di Servizi di ripristino nel portale di Azure e come disabilitare la protezione per le macchine virtuali protette da Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="47bae-108">This article describes how to unregister servers from a Recovery Services vault in the Azure portal, and how to disable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="47bae-109">Per inviare commenti o domande, è possibile usare la parte inferiore di questo articolo oppure il [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="47bae-109">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="47bae-110">Annullare la registrazione di un server di configurazione connesso</span><span class="sxs-lookup"><span data-stu-id="47bae-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="47bae-111">Se si replicano macchine virtuali VMware o server fisici Windows/Linux in Azure, è possibile annullare la registrazione di un server di configurazione connesso da un insieme di credenziali come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="47bae-111">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="47bae-112">Disabilitare la protezione delle macchine.</span><span class="sxs-lookup"><span data-stu-id="47bae-112">Disable machine protection.</span></span> <span data-ttu-id="47bae-113">In **Elementi protetti** > **Elementi replicati** fare clic sulla macchina > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-113">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="47bae-114">Annullare l'associazione di tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="47bae-114">Disassociate any policies.</span></span> <span data-ttu-id="47bae-115">In **Infrastruttura di Site Recovery** > **Per VMWare e computer fisici** > **Criteri di replica** fare doppio clic sui criteri associati.</span><span class="sxs-lookup"><span data-stu-id="47bae-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="47bae-116">Fare doppio clic su server di configurazione > **Annulla associazione**.</span><span class="sxs-lookup"><span data-stu-id="47bae-116">Right-click the configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="47bae-117">Rimuovere qualsiasi server di destinazione master o di elaborazione locale aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="47bae-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="47bae-118">In **Infrastruttura di Site Recovery** > **Per VMWare e computer fisici** > **Server di configurazione** fare clic con il pulsante destro del mouse sul server > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="47bae-119">Eliminare il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-119">Delete the configuration server.</span></span>
5. <span data-ttu-id="47bae-120">Disinstallare manualmente il servizio di mobilità in esecuzione nel server di destinazione master che sarà un server separato o in esecuzione nel server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-120">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
6. <span data-ttu-id="47bae-121">Disinstallare eventuali server di elaborazione aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="47bae-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="47bae-122">Disinstallare il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-122">Uninstall the configuration server.</span></span>
8. <span data-ttu-id="47bae-123">Nel server di configurazione disinstallare l'istanza di MySQL installata da Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="47bae-123">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="47bae-124">Eliminare la chiave ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery`` nel Registro di sistema del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-124">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="47bae-125">Annullare la registrazione di un server di configurazione non connesso</span><span class="sxs-lookup"><span data-stu-id="47bae-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="47bae-126">Se si replicano macchine virtuali VMware o server fisici Windows/Linux in Azure, è possibile annullare la registrazione di un server di configurazione non connesso da un insieme di credenziali come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="47bae-126">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="47bae-127">Disabilitare la protezione delle macchine.</span><span class="sxs-lookup"><span data-stu-id="47bae-127">Disable machine protection.</span></span> <span data-ttu-id="47bae-128">In **Elementi protetti** > **Elementi replicati** fare clic sulla macchina > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-128">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span> <span data-ttu-id="47bae-129">Selezionare **Interrompi gestione della macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="47bae-129">Select **Stop managing the machine**.</span></span>
2. <span data-ttu-id="47bae-130">Rimuovere qualsiasi server di destinazione master o di elaborazione locale aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="47bae-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="47bae-131">In **Infrastruttura di Site Recovery** > **Per VMWare e computer fisici** > **Server di configurazione** fare clic con il pulsante destro del mouse sul server > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
3. <span data-ttu-id="47bae-132">Eliminare il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-132">Delete the configuration server.</span></span>
4. <span data-ttu-id="47bae-133">Disinstallare manualmente il servizio di mobilità in esecuzione nel server di destinazione master che sarà un server separato o in esecuzione nel server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-133">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
5. <span data-ttu-id="47bae-134">Disinstallare eventuali server di elaborazione aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="47bae-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="47bae-135">Disinstallare il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-135">Uninstall the configuration server.</span></span>
7. <span data-ttu-id="47bae-136">Nel server di configurazione disinstallare l'istanza di MySQL installata da Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="47bae-136">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="47bae-137">Eliminare la chiave ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery`` nel Registro di sistema del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-137">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="47bae-138">Annullare la registrazione di un server VMM connesso</span><span class="sxs-lookup"><span data-stu-id="47bae-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="47bae-139">Come procedura consigliata, annullare la registrazione del server VMM quando è connesso ad Azure.</span><span class="sxs-lookup"><span data-stu-id="47bae-139">As a best practice, we recommend that you unregister the VMM server when it's connected to Azure.</span></span> <span data-ttu-id="47bae-140">In questo modo le impostazioni nei server VMM e in altri server VMM con cloud abbinati vengono rimosse correttamente.</span><span class="sxs-lookup"><span data-stu-id="47bae-140">This ensures that settings on the VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="47bae-141">Si consiglia di rimuovere un server non connesso solo in caso di problema di connettività permanente.</span><span class="sxs-lookup"><span data-stu-id="47bae-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="47bae-142">Se il server VMM non è connesso, è necessario eseguire manualmente uno script per rimuovere le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="47bae-142">If the VMM server isn’t connected, you will need to manually run a script to clean up settings.</span></span>

1. <span data-ttu-id="47bae-143">Arrestare la replica delle VM nei cloud presenti sul server VMM da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="47bae-143">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="47bae-144">Eliminare i mapping di rete usati dai cloud nel server VMM da eliminare.</span><span class="sxs-lookup"><span data-stu-id="47bae-144">Delete any network mappings used by clouds on the VMM server you want to delete.</span></span> <span data-ttu-id="47bae-145">In **Infrastruttura di Site Recovery** > **Per System Center VMM** > **Mapping di rete** fare clic con il pulsante destro del mouse sul mapping di rete > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="47bae-146">Annullare l'associazione dei criteri di replica dai cloud nel server VMM da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="47bae-146">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="47bae-147">In **Infrastruttura di Site Recovery** > **Per System Center VMM** >  **Criteri di replica** fare doppio clic sui criteri associati.</span><span class="sxs-lookup"><span data-stu-id="47bae-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="47bae-148">Fare clic con il pulsante destro del mouse sul cloud > **Annulla associazione**.</span><span class="sxs-lookup"><span data-stu-id="47bae-148">Right-click the cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="47bae-149">Eliminare il server VMM o il nodo VMM attivo.</span><span class="sxs-lookup"><span data-stu-id="47bae-149">Delete the VMM server or active VMM node.</span></span> <span data-ttu-id="47bae-150">In **Infrastruttura di Site Recovery** > **Per System Center VMM** > **Server VMM** fare clic con il pulsante destro del mouse sul server > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
5. <span data-ttu-id="47bae-151">Disinstallare manualmente il Provider nel server VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-151">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="47bae-152">Se si dispone di un cluster, eseguire la rimozione da tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="47bae-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="47bae-153">Se si esegue la replica in Azure, rimuovere manualmente l'agente di Servizi di ripristino di Microsoft dagli host Hyper-V nei cloud eliminati.</span><span class="sxs-lookup"><span data-stu-id="47bae-153">If you're replicating to Azure, manually remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="47bae-154">Annullare la registrazione di un server VMM non connesso</span><span class="sxs-lookup"><span data-stu-id="47bae-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="47bae-155">Arrestare la replica delle VM nei cloud presenti sul server VMM da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="47bae-155">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="47bae-156">Eliminare i mapping di rete usati dai cloud nel server VMM da eliminare.</span><span class="sxs-lookup"><span data-stu-id="47bae-156">Delete any network mappings used by clouds on the VMM server that you want to delete.</span></span> <span data-ttu-id="47bae-157">In **Infrastruttura di Site Recovery** > **Per System Center VMM** > **Mapping di rete** fare clic con il pulsante destro del mouse sul mapping di rete > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="47bae-158">Prendere nota dell'ID del server VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-158">Note the ID of the VMM server.</span></span>
4. <span data-ttu-id="47bae-159">Annullare l'associazione dei criteri di replica dai cloud nel server VMM da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="47bae-159">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="47bae-160">In **Infrastruttura di Site Recovery** > **Per System Center VMM** >  **Criteri di replica** fare doppio clic sui criteri associati.</span><span class="sxs-lookup"><span data-stu-id="47bae-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="47bae-161">Fare clic con il pulsante destro del mouse sul cloud > **Annulla associazione**.</span><span class="sxs-lookup"><span data-stu-id="47bae-161">Right-click the cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="47bae-162">Eliminare il server VMM o il nodo attivo.</span><span class="sxs-lookup"><span data-stu-id="47bae-162">Delete the VMM server or active node.</span></span> <span data-ttu-id="47bae-163">In **Infrastruttura di Site Recovery** > **Per System Center VMM** > **Server VMM** fare clic con il pulsante destro del mouse sul server > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
6. <span data-ttu-id="47bae-164">Nel server VMM scaricare ed eseguire lo [script di pulizia](http://aka.ms/asr-cleanup-script-vmm).</span><span class="sxs-lookup"><span data-stu-id="47bae-164">Download and run the [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on the VMM server.</span></span> <span data-ttu-id="47bae-165">Aprire PowerShell con l'opzione **Esegui come amministratore** per modificare i criteri di esecuzione per l'ambito predefinito (LocalMachine).</span><span class="sxs-lookup"><span data-stu-id="47bae-165">Open PowerShell with the **Run as Administrator** option, to change the execution policy for the default (LocalMachine) scope.</span></span> <span data-ttu-id="47bae-166">Nello script specificare l'ID del server VMM da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="47bae-166">In the script, specify the ID of the VMM server you want to remove.</span></span> <span data-ttu-id="47bae-167">Lo script rimuove le informazioni sulla registrazione e l'associazione del cloud dal server.</span><span class="sxs-lookup"><span data-stu-id="47bae-167">The script removes registration and cloud pairing information from the server.</span></span>
5. <span data-ttu-id="47bae-168">Eseguire lo script di pulizia in tutti gli altri server VMM che contengono cloud associati ai cloud nel server VMM da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="47bae-168">Run the cleanup script on any other VMM servers that contain clouds that are paired with clouds on the VMM server you want to remove.</span></span>
6. <span data-ttu-id="47bae-169">Eseguire lo script di pulizia in qualsiasi altro nodo cluster VMM passivo in cui è installato il Provider.</span><span class="sxs-lookup"><span data-stu-id="47bae-169">Run the  cleanup script on any other passive VMM cluster nodes that have the Provider installed.</span></span>
7. <span data-ttu-id="47bae-170">Disinstallare manualmente il Provider nel server VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-170">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="47bae-171">Se si dispone di un cluster, eseguire la rimozione da tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="47bae-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="47bae-172">Se si esegue la replica in Azure, è possibile rimuovere manualmente l'agente di Servizi di ripristino di Microsoft dagli host Hyper-V nei cloud eliminati.</span><span class="sxs-lookup"><span data-stu-id="47bae-172">If you replicating to Azure, you can remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="47bae-173">Annullare la registrazione di un host Hyper-V in un sito di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="47bae-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="47bae-174">Gli host Hyper-V non gestiti da VMM vengono raccolti in un sito di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="47bae-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="47bae-175">Rimuovere un host in un sito di Hyper-V nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="47bae-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="47bae-176">Disabilitare la replica per le VM Hyper-V presenti nell'host.</span><span class="sxs-lookup"><span data-stu-id="47bae-176">Disable replication for Hyper-V VMs located on the host.</span></span>
2. <span data-ttu-id="47bae-177">Annullare l'associazione dei criteri per il sito Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="47bae-177">Disassociate policies for the Hyper-V site.</span></span> <span data-ttu-id="47bae-178">In **Infrastruttura di Site Recovery** > **Per siti Hyper-V** >  **Criteri di replica** fare doppio clic sui criteri associati.</span><span class="sxs-lookup"><span data-stu-id="47bae-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="47bae-179">Fare clic con il pulsante destro del mouse sul cloud > **Annulla associazione**.</span><span class="sxs-lookup"><span data-stu-id="47bae-179">Right-click the site > **Disassociate**.</span></span>
3. <span data-ttu-id="47bae-180">Eliminare gli host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="47bae-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="47bae-181">In **Infrastruttura di Site Recovery** > **Per System Center VMM** > **Host Hyper-V** fare clic con il pulsante destro del mouse sul server > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="47bae-182">Eliminare il sito Hyper-V dopo che sono stati rimossi tutti gli host dal sito.</span><span class="sxs-lookup"><span data-stu-id="47bae-182">Delete the Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="47bae-183">In **Infrastruttura di Site Recovery** > **Per System Center VMM** > **Siti Hyper-V** fare clic con il pulsante destro del mouse sul sito > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click the site > **Delete**.</span></span>
5. <span data-ttu-id="47bae-184">Eseguire lo script seguente in ogni host Hyper-V che è stato rimosso.</span><span class="sxs-lookup"><span data-stu-id="47bae-184">Run the following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="47bae-185">Lo script pulisce le impostazioni del server e ne annulla la registrazione dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="47bae-185">The script cleans up settings on the server, and unregisters it from the vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
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
                "Stopping the Azure Site Recovery service..."
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

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
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



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="47bae-186">Disabilitare la protezione per una VM VMware o un server fisico</span><span class="sxs-lookup"><span data-stu-id="47bae-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="47bae-187">In **Elementi protetti** > **Elementi replicati** fare clic sulla macchina > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-187">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="47bae-188">In **Rimuovi macchina virtuale** selezionare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="47bae-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="47bae-189">**Disabilita protezione per la macchina virtuale (impostazione consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="47bae-189">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="47bae-190">Usare questa opzione per arrestare la replica della macchina.</span><span class="sxs-lookup"><span data-stu-id="47bae-190">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="47bae-191">Le impostazioni di Site Recovery verranno rimosse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="47bae-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="47bae-192">Questa opzione verrà visualizzata nelle circostanze seguenti:</span><span class="sxs-lookup"><span data-stu-id="47bae-192">You will only see this option in the following circumstances:</span></span>
        - <span data-ttu-id="47bae-193">**Il volume della VM è stato ridimensionato**: quando si ridimensiona un volume, la macchina virtuale entra in uno stato critico.</span><span class="sxs-lookup"><span data-stu-id="47bae-193">**You've resized the VM volume**—When you resize a volume the virtual machine goes into a critical state.</span></span> <span data-ttu-id="47bae-194">Selezionare questa opzione per disabilitare la protezione mantenendo i punti di ripristino in Azure.</span><span class="sxs-lookup"><span data-stu-id="47bae-194">Select this option to disables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="47bae-195">Quando si riabilita la protezione per la macchina virtuale, i dati per il volume ridimensionato verranno trasferiti in Azure.</span><span class="sxs-lookup"><span data-stu-id="47bae-195">When you enable protection for the machine again, the data for the resized volume will be transferred to Azure.</span></span>
        - <span data-ttu-id="47bae-196">**È stato eseguito recentemente un failover**: dopo avere eseguito un failover per testare l'ambiente, selezionare questa opzione per ripristinare la protezione delle macchine locali.</span><span class="sxs-lookup"><span data-stu-id="47bae-196">**You've recently run a failover**—After you've run a failover to test your environment, select this option to start protecting on-premises machines again.</span></span> <span data-ttu-id="47bae-197">Viene disabilitata ogni macchina virtuale ed è quindi necessario riabilitare la protezione.</span><span class="sxs-lookup"><span data-stu-id="47bae-197">It disables each virtual machine, and then you need to enable protection for them again.</span></span> <span data-ttu-id="47bae-198">La disabilitazione della macchina con questa impostazione non riguarda la macchina virtuale di replica in Azure.</span><span class="sxs-lookup"><span data-stu-id="47bae-198">Disabling the machine with this setting doesn't affect the replica virtual machine in Azure.</span></span> <span data-ttu-id="47bae-199">Non disinstallare il servizio Mobility dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47bae-199">Don't uninstall the Mobility service from the machine.</span></span>
    - <span data-ttu-id="47bae-200">**Interrompi gestione della macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="47bae-200">**Stop managing the machine**.</span></span> <span data-ttu-id="47bae-201">Se si seleziona questa opzione, la macchina virtuale verrà rimossa solo dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="47bae-201">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="47bae-202">Le impostazioni di protezione locali per la macchina virtuale non saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="47bae-202">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="47bae-203">Per rimuovere le impostazioni nella macchina e per rimuovere la macchina dalla sottoscrizione di Azure, è necessario rimuovere le impostazioni tramite la disinstallazione del servizio Mobility.</span><span class="sxs-lookup"><span data-stu-id="47bae-203">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings by uninstalling the Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="47bae-204">Disabilitare la protezione per una VM Hyper-V in un cloud VMM</span><span class="sxs-lookup"><span data-stu-id="47bae-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="47bae-205">In **Elementi protetti** > **Elementi replicati** fare clic sulla macchina > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-205">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="47bae-206">In **Rimuovi macchina virtuale** selezionare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="47bae-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="47bae-207">**Disabilita protezione per la macchina virtuale (impostazione consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="47bae-207">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="47bae-208">Usare questa opzione per arrestare la replica della macchina.</span><span class="sxs-lookup"><span data-stu-id="47bae-208">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="47bae-209">Le impostazioni di Site Recovery verranno rimosse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="47bae-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="47bae-210">**Interrompi gestione della macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="47bae-210">**Stop managing the machine**.</span></span> <span data-ttu-id="47bae-211">Se si seleziona questa opzione, la macchina virtuale verrà rimossa solo dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="47bae-211">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="47bae-212">Le impostazioni di protezione locali per la macchina virtuale non saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="47bae-212">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="47bae-213">Per rimuovere le impostazioni nella macchina e per rimuovere la macchina dalla sottoscrizione di Azure è necessario pulire manualmente le impostazioni usando le istruzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="47bae-213">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings up manually, using the instructions below.</span></span> <span data-ttu-id="47bae-214">Si noti che se si sceglie di eliminare la macchina virtuale e i relativi dischi rigidi, questi verranno rimossi dal percorso di destinazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-214">Note that if you select to delete the virtual machine and its hard disks, they'll be removed from the target location.</span></span>

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a><span data-ttu-id="47bae-215">Eseguire la pulizia delle impostazioni di protezione: replica in un sito VMM secondario</span><span class="sxs-lookup"><span data-stu-id="47bae-215">Clean up protection settings - replication to a secondary VMM site</span></span>

<span data-ttu-id="47bae-216">Se è stato selezionato **Interrompi gestione della macchina virtuale** e si sta eseguendo la replica in un sito secondario, eseguire questo script nel server primario per rimuovere le impostazioni per la macchina virtuale primaria.</span><span class="sxs-lookup"><span data-stu-id="47bae-216">If you selected **Stop managing the machine** and you replicating to a secondary site, run this script on the primary server to clean up the settings for the primary virtual machine.</span></span> <span data-ttu-id="47bae-217">Nella console VMM fare clic sul pulsante PowerShell per aprire la console PowerShell di VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-217">In the VMM console click the PowerShell button to open the VMM PowerShell console.</span></span> <span data-ttu-id="47bae-218">Sostituire SQLVM1 con il nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47bae-218">Replace SQLVM1 with the name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="47bae-219">Nel server VMM secondario eseguire questo script per pulire le impostazioni per la macchina virtuale secondaria:</span><span class="sxs-lookup"><span data-stu-id="47bae-219">On the secondary VMM server run this script to clean up the settings for the secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="47bae-220">Nel server VMM secondario aggiornare le macchine virtuali nel server host Hyper-V in modo che la VM secondaria venga rilevata di nuovo nella console VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-220">On the secondary VMM server, refresh the virtual machines on the Hyper-V host server, so that the secondary VM gets detected again in the VMM console.</span></span>
4. <span data-ttu-id="47bae-221">I passaggi sopra descritti cancellano le impostazioni di replica nel server VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-221">The above steps clear up the replication settings on the VMM server.</span></span> <span data-ttu-id="47bae-222">Se si vuole arrestare la replica per la macchina virtuale, eseguire lo script seguente nelle VM primarie e secondarie.</span><span class="sxs-lookup"><span data-stu-id="47bae-222">If you want to stop replication for the virtual machine, run the following script oh the primary and secondary VMs.</span></span> <span data-ttu-id="47bae-223">Sostituire SQLVM1 con il nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47bae-223">Replace SQLVM1 with the name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a><span data-ttu-id="47bae-224">Eseguire la pulizia delle impostazioni di protezione: replica in Azure</span><span class="sxs-lookup"><span data-stu-id="47bae-224">Clean up protection settings - replication to Azure</span></span>

1. <span data-ttu-id="47bae-225">Se è stato selezionato **Interrompi gestione della macchina virtuale** e si esegue la replica in Azure, eseguire questo script nel server VMM di origine usando PowerShell dalla console VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-225">If you selected **Stop managing the machine** and you replicate to Azure, run this script on the source VMM server, using PowerShell from the VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="47bae-226">I passaggi sopra descritti cancellano le impostazioni di replica del server VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-226">The above steps clear the replication settings on the VMM server.</span></span> <span data-ttu-id="47bae-227">Per arrestare la replica per la macchina virtuale in esecuzione nel server host Hyper-V, eseguire questo script.</span><span class="sxs-lookup"><span data-stu-id="47bae-227">To stop replication for the virtual machine running on the Hyper-V host server, run this script.</span></span> <span data-ttu-id="47bae-228">Sostituire SQLVM1 con il nome della macchina virtuale e host01.contoso.com con il nome del server host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="47bae-228">Replace SQLVM1 with the name of your virtual machine, and host01.contoso.com with the name of the Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="47bae-229">Disabilitare la protezione per una VM Hyper-V in un sito Hyper-V</span><span class="sxs-lookup"><span data-stu-id="47bae-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="47bae-230">Usare questa procedura se si esegue la replica di VM Hyper-V in Azure senza un server VMM.</span><span class="sxs-lookup"><span data-stu-id="47bae-230">Use this procedure if you're replicating Hyper-V VMs to Azure without a VMM server.</span></span>

1. <span data-ttu-id="47bae-231">In **Elementi protetti** > **Elementi replicati** fare clic sulla macchina > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="47bae-231">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="47bae-232">In **Rimuovi macchina virtuale** è possibile selezionare le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="47bae-232">In **Remove Machine**, you can select the following options:</span></span>

   - <span data-ttu-id="47bae-233">**Disabilita protezione per la macchina virtuale (impostazione consigliata)**.</span><span class="sxs-lookup"><span data-stu-id="47bae-233">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="47bae-234">Usare questa opzione per arrestare la replica della macchina.</span><span class="sxs-lookup"><span data-stu-id="47bae-234">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="47bae-235">Le impostazioni di Site Recovery verranno rimosse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="47bae-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="47bae-236">**Interrompi gestione della macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="47bae-236">**Stop managing the machine**.</span></span> <span data-ttu-id="47bae-237">Se si seleziona questa opzione, la macchina virtuale verrà rimossa solo dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="47bae-237">If you select this option the machine will only be removed from the vault.</span></span> <span data-ttu-id="47bae-238">Le impostazioni di protezione locali per la macchina virtuale non saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="47bae-238">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="47bae-239">Per rimuovere le impostazioni nella macchina e per rimuovere la macchina virtuale dalla sottoscrizione di Azure, è necessario pulire manualmente le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="47bae-239">To remove settings on the machine, and to remove the virtual machine from the Azure subscription, you need to clean the settings up manually.</span></span> <span data-ttu-id="47bae-240">Se si sceglie di eliminare la macchina virtuale e i relativi dischi rigidi, essi verranno rimossi dal percorso di destinazione.</span><span class="sxs-lookup"><span data-stu-id="47bae-240">If you select to delete the virtual machine and its hard disks they will be removed from the target location.</span></span>
3. <span data-ttu-id="47bae-241">Se è stato selezionato **Interrompi gestione della macchina virtuale**, eseguire questo script nel server host Hyper-V di origine per rimuovere la replica per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47bae-241">If you selected **Stop managing the machine**, run this script on the source Hyper-V host server, to remove replication for the virtual machine.</span></span> <span data-ttu-id="47bae-242">Sostituire SQLVM1 con il nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47bae-242">Replace SQLVM1 with the name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
