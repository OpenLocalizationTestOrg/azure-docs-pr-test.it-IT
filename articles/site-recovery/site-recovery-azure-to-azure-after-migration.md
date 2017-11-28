---
title: Preparare le macchine per configurare il ripristino di emergenza tra le aree di Azure dopo la migrazione ad Azure usando Site Recovery | Microsoft Docs
description: Questo articolo descrive come preparare le macchine per configurare il ripristino di emergenza tra le aree di Azure dopo la migrazione a Azure usando Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: 2aee0fb8d1ba1ff1584bee91b4d1cc34b654d97f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-to-another-region-after-migration-to-azure-by-using-azure-site-recovery"></a><span data-ttu-id="931c5-103">Replicare le macchine virtuali di Azure in un'altra area dopo la migrazione ad Azure usando Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="931c5-103">Replicate Azure VMs to another region after migration to Azure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="931c5-104">La replica di Azure Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="931c5-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="931c5-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="931c5-105">Overview</span></span>

<span data-ttu-id="931c5-106">Questo articolo contiene le informazioni relative alla preparazione delle macchine virtuali di Azure per la replica tra due aeree di Azure dopo che queste macchine sono state migrate da un ambiente on-premises ad Azure usando Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="931c5-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment to Azure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="931c5-107">Ripristino di emergenza e conformità</span><span class="sxs-lookup"><span data-stu-id="931c5-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="931c5-108">Oggi sempre più aziende spostano i loro carichi di lavoro in Azure.</span><span class="sxs-lookup"><span data-stu-id="931c5-108">Today, more and more enterprises are moving their workloads to Azure.</span></span> <span data-ttu-id="931c5-109">Di fronte a un numero sempre crescente di aziende impegnate a spostare in Azure i carichi di lavoro di produzione on-premises mission-critical, configurare il ripristino di emergenza è diventato fondamentale ai fini della conformità e della protezione da potenziali interruzioni del servizio in un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="931c5-109">With enterprises moving mission-critical on-premises production workloads to Azure, setting up disaster recovery for these workloads is mandatory for compliance and to safeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="931c5-110">Preparazione delle macchine migrate per la replica</span><span class="sxs-lookup"><span data-stu-id="931c5-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="931c5-111">Per preparare le macchine migrate per la configurazione della replica in un'altra area di Azure:</span><span class="sxs-lookup"><span data-stu-id="931c5-111">To prepare migrated machines for setting up replication to another Azure region:</span></span>

1. <span data-ttu-id="931c5-112">Completare la migrazione.</span><span class="sxs-lookup"><span data-stu-id="931c5-112">Complete migration.</span></span>
2. <span data-ttu-id="931c5-113">Se necessario, installare l'agente di Azure.</span><span class="sxs-lookup"><span data-stu-id="931c5-113">Install the Azure agent if needed.</span></span>
3. <span data-ttu-id="931c5-114">Rimuovere il servizio Mobility.</span><span class="sxs-lookup"><span data-stu-id="931c5-114">Remove the Mobility service.</span></span>  
4. <span data-ttu-id="931c5-115">Riavviare la VM.</span><span class="sxs-lookup"><span data-stu-id="931c5-115">Restart the VM.</span></span>

<span data-ttu-id="931c5-116">Questi passaggi vengono descritti più dettagliatamente nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="931c5-116">These steps are described in more detail in the following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-to-run-on-azure-vms"></a><span data-ttu-id="931c5-117">Passaggio 1: eseguire la migrazione dei carichi di lavoro in esecuzione in macchine virtuali Hyper-V e VMware e in server fisici affinché vengano eseguiti in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="931c5-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers to run on Azure VMs</span></span>

<span data-ttu-id="931c5-118">Per configurare la replica ed eseguire la migrazione di carichi di lavoro Hyper-V, VMware on-premises e fisici in Azure, eseguire i passaggi riportati nell'articolo [Eseguire la migrazione delle macchine virtuali Iaas di Azure tra aeree di Azure con Azure Site Recovery](site-recovery-migrate-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="931c5-118">To set up replication and migrate your on-premises Hyper-V, VMware, and physical workloads to Azure, follow the steps in the [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="931c5-119">Dopo la migrazione, non è necessario eseguire il commit di un failover né eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="931c5-119">After migration, you don't need to commit or delete a failover.</span></span> <span data-ttu-id="931c5-120">In alternativa, selezionare l'opzione **Completa la migrazione** per ogni macchina di cui si desidera eseguire la migrazione:</span><span class="sxs-lookup"><span data-stu-id="931c5-120">Instead, select the **Complete Migration** option for each machine you want to migrate:</span></span>
1. <span data-ttu-id="931c5-121">In **Elementi replicati** fare clic con il pulsante destro del mouse sulla macchina virtuale e scegliere **Completa la migrazione**.</span><span class="sxs-lookup"><span data-stu-id="931c5-121">In **Replicated Items**, right-click the VM, and click **Complete Migration**.</span></span> <span data-ttu-id="931c5-122">Fare clic su **OK** per completare il passaggio.</span><span class="sxs-lookup"><span data-stu-id="931c5-122">Click **OK** to complete the step.</span></span> <span data-ttu-id="931c5-123">È possibile tenere traccia dei progressi nelle proprietà della VM monitorando il processo Completa la migrazione in **Processi di Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="931c5-123">You can track progress in the VM properties by monitoring the Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="931c5-124">L'azione **Completa la migrazione** conclude il processo di migrazione, rimuove la replica per la macchina e interrompe la fatturazione relativa di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="931c5-124">The **Complete Migration** action completes the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-the-azure-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="931c5-126">Passaggio 2: installare l'agente di macchine virtuali di Azure nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="931c5-126">Step 2: Install the Azure VM agent on the virtual machine</span></span>
<span data-ttu-id="931c5-127">L'[agente di macchine virtuali](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) di Azure deve essere installato nella macchina virtuale affinché l'estensione Site Recovery funzioni e ai fini della protezione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="931c5-127">The Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on the virtual machine for the Site Recovery extension to work and to help protect the VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="931c5-128">A partire dalla versione 9.7.0.0, nelle macchine virtuali di Windows il programma di installazione del servizio Mobility installa anche l'agente di macchine virtuali di Azure più recente.</span><span class="sxs-lookup"><span data-stu-id="931c5-128">Beginning with version 9.7.0.0, on Windows virtual machines, the Mobility service installer also installs the latest available Azure VM agent.</span></span> <span data-ttu-id="931c5-129">Durante la migrazione, la macchina virtuale soddisfa i prerequisiti di installazione dell'agente per l'uso di qualsiasi estensione della macchina virtuale, incluso Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="931c5-129">On migration, the virtual machine meets the agent installation prerequisite for using any VM extension, including the Site Recovery extension.</span></span> <span data-ttu-id="931c5-130">L'agente di macchine virtuali di Azure deve essere installato manualmente solo se il servizio Mobility installato nella macchina migrata è della versione 9.6 o precedente.</span><span class="sxs-lookup"><span data-stu-id="931c5-130">The Azure VM agent needs to be manually installed only if the Mobility service installed on the migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="931c5-131">La tabella seguente fornisce informazioni aggiuntive sull'installazione dell'agente di macchine virtuali e sulla conferma di avvenuta installazione:</span><span class="sxs-lookup"><span data-stu-id="931c5-131">The following table provides additional information about installing the VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="931c5-132">**Operazione**</span><span class="sxs-lookup"><span data-stu-id="931c5-132">**Operation**</span></span> | <span data-ttu-id="931c5-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="931c5-133">**Windows**</span></span> | <span data-ttu-id="931c5-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="931c5-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="931c5-135">Installazione dell'agente di VM</span><span class="sxs-lookup"><span data-stu-id="931c5-135">Installing the VM agent</span></span> |<span data-ttu-id="931c5-136">Scaricare e installare il file [MSI per l'agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="931c5-136">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="931c5-137">Per completare l'installazione è necessario disporre dei privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="931c5-137">You need administrator privileges to complete the installation.</span></span> |<span data-ttu-id="931c5-138">Installare l'[agente Linux](../virtual-machines/linux/agent-user-guide.md) più recente.</span><span class="sxs-lookup"><span data-stu-id="931c5-138">Install the latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="931c5-139">Per completare l'installazione è necessario disporre dei privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="931c5-139">You need administrator privileges to complete the installation.</span></span> <span data-ttu-id="931c5-140">È consigliabile installare l'agente dal repository di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="931c5-140">We recommend installing the agent from your distribution repository.</span></span> <span data-ttu-id="931c5-141">*Non è consigliabile* installare l'agente di macchine virtuali Linux direttamente da GitHub.</span><span class="sxs-lookup"><span data-stu-id="931c5-141">We *do not recommend* installing the Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="931c5-142">Convalida dell'installazione dell'agente di VM</span><span class="sxs-lookup"><span data-stu-id="931c5-142">Validating the VM agent installation</span></span> |<span data-ttu-id="931c5-143">1. Passare alla cartella C:\WindowsAzure\Packages nella macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="931c5-143">1. Browse to the C:\WindowsAzure\Packages folder in the Azure VM.</span></span> <span data-ttu-id="931c5-144">La cartella dovrebbe contenere il file WaAppAgent.exe.</span><span class="sxs-lookup"><span data-stu-id="931c5-144">You should see the WaAppAgent.exe file.</span></span> <br><span data-ttu-id="931c5-145">2. Fare clic con il pulsante destro del mouse sul file, scegliere **Proprietà** e quindi selezionare la scheda **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="931c5-145">2. Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="931c5-146">Il campo **Versione prodotto** dovrebbe contenere 2.6.1198.718 o un numero più elevato.</span><span class="sxs-lookup"><span data-stu-id="931c5-146">The **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="931c5-147">N/D</span><span class="sxs-lookup"><span data-stu-id="931c5-147">N/A</span></span> |


### <a name="step-3-remove-the-mobility-service-from-the-migrated-virtual-machine"></a><span data-ttu-id="931c5-148">Passaggio 3: rimuovere il servizio Mobility dalla macchina virtuale migrata</span><span class="sxs-lookup"><span data-stu-id="931c5-148">Step 3: Remove the Mobility service from the migrated virtual machine</span></span>

<span data-ttu-id="931c5-149">Se le macchine VMware on-premises o i server fisici sono stati migrati in Windows/Linux,è necessario rimuovere/disinstallare manualmente il servizio Mobility dalla macchina virtuale migrata.</span><span class="sxs-lookup"><span data-stu-id="931c5-149">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need to manually remove/uninstall the Mobility service from the migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="931c5-150">Questo passaggio non è necessario le macchine Hyper-V migrate in Azure.</span><span class="sxs-lookup"><span data-stu-id="931c5-150">This step is not required for Hyper-V VMs migrated to Azure.</span></span>

#### <a name="uninstall-the-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="931c5-151">Disinstallare il servizio Mobility in una macchina virtuale Windows Server</span><span class="sxs-lookup"><span data-stu-id="931c5-151">Uninstall the Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="931c5-152">Usare uno dei metodi seguenti per disinstallare il servizio Mobility in una macchina Windows Server.</span><span class="sxs-lookup"><span data-stu-id="931c5-152">Use one of the following methods to uninstall the Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-the-windows-ui"></a><span data-ttu-id="931c5-153">Eseguire la disinstallazione usando l'interfaccia utente di Windows</span><span class="sxs-lookup"><span data-stu-id="931c5-153">Uninstall by using the Windows UI</span></span>
1. <span data-ttu-id="931c5-154">Nel Pannello di controllo, selezionare **Programmi**.</span><span class="sxs-lookup"><span data-stu-id="931c5-154">In the Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="931c5-155">Selezionare **Microsoft Azure Site Recovery Mobility Service/Master Target server** (Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master) e fare clic su **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="931c5-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="931c5-156">Disinstallare dal prompt dei comandi</span><span class="sxs-lookup"><span data-stu-id="931c5-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="931c5-157">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="931c5-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="931c5-158">Per disinstallare il servizio Mobility, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="931c5-158">To uninstall the Mobility service, run the following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-the-mobility-service-on-a-linux-computer"></a><span data-ttu-id="931c5-159">Disinstallare il servizio Mobility in un computer Linux</span><span class="sxs-lookup"><span data-stu-id="931c5-159">Uninstall the Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="931c5-160">Sul server Linux, accedere come utente **Root**.</span><span class="sxs-lookup"><span data-stu-id="931c5-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="931c5-161">Nel terminale, passare a /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="931c5-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="931c5-162">Per disinstallare il servizio Mobility, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="931c5-162">To uninstall the Mobility service, run the following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-the-vm"></a><span data-ttu-id="931c5-163">Passaggio 4: riavviare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="931c5-163">Step 4: Restart the VM</span></span>

<span data-ttu-id="931c5-164">Dopo avere disinstallato il servizio Mobility, riavviare la macchina virtuale prima di configurare la replica in un'altra area di Azure.</span><span class="sxs-lookup"><span data-stu-id="931c5-164">After you uninstall the Mobility service, restart the VM before you set up replication to another Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="931c5-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="931c5-165">Next steps</span></span>
- <span data-ttu-id="931c5-166">Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="931c5-166">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="931c5-167">Altre informazioni sulle [indicazioni di connettività di rete per la replica delle macchine virtuali di Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="931c5-167">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
