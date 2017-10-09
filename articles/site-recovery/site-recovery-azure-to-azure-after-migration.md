---
title: aaaPrepare macchine tooset ripristino di emergenza tra aree di Azure dopo la migrazione tooAzure tramite il ripristino del sito | Documenti Microsoft
description: In questo articolo viene descritto come tooprepare macchine tooset ripristino di emergenza tra aree di Azure dopo la migrazione tooAzure tramite Azure Site Recovery.
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
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="881c1-103">Replicare macchine virtuali di Azure tooanother area dopo la migrazione tooAzure tramite Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="881c1-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="881c1-104">La replica di Azure Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="881c1-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="881c1-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="881c1-105">Overview</span></span>

<span data-ttu-id="881c1-106">In questo articolo consente di macchine virtuali di Azure per preparare la replica tra due aree di Azure dopo che questi computer sono stati migrati da un tooAzure ambiente locale con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="881c1-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="881c1-107">Ripristino di emergenza e conformità</span><span class="sxs-lookup"><span data-stu-id="881c1-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="881c1-108">Oggi più le aziende stanno spostando tooAzure i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="881c1-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="881c1-109">Con le aziende lo spostamento di produzione critici in locale tooAzure i carichi di lavoro, configurare il ripristino di emergenza per questi carichi di lavoro è obbligatorio per la conformità e toosafeguard contro le interruzioni in un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="881c1-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="881c1-110">Preparazione delle macchine migrate per la replica</span><span class="sxs-lookup"><span data-stu-id="881c1-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="881c1-111">tooprepare della migrazione di macchine per la configurazione di replica tooanother area di Azure:</span><span class="sxs-lookup"><span data-stu-id="881c1-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="881c1-112">Completare la migrazione.</span><span class="sxs-lookup"><span data-stu-id="881c1-112">Complete migration.</span></span>
2. <span data-ttu-id="881c1-113">Installare l'agente di Azure, se necessario hello.</span><span class="sxs-lookup"><span data-stu-id="881c1-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="881c1-114">Rimuovere il servizio di mobilità hello.</span><span class="sxs-lookup"><span data-stu-id="881c1-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="881c1-115">Riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="881c1-115">Restart hello VM.</span></span>

<span data-ttu-id="881c1-116">Questi passaggi sono descritti in dettaglio nelle sezioni che seguono hello.</span><span class="sxs-lookup"><span data-stu-id="881c1-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="881c1-117">Passaggio 1: Eseguire la migrazione dei carichi di lavoro in esecuzione su macchine virtuali Hyper-V, le macchine virtuali VMware e toorun server fisici in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="881c1-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="881c1-118">tooset la replica di backup ed eseguire la migrazione locale Hyper-V, VMware e carichi di lavoro fisici tooAzure, seguire hello passi in hello [IaaS di Azure di eseguire la migrazione di macchine virtuali tra le aree di Azure con Azure Site Recovery](site-recovery-migrate-to-azure.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="881c1-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="881c1-119">Dopo la migrazione, è non necessario toocommit o eliminare un failover.</span><span class="sxs-lookup"><span data-stu-id="881c1-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="881c1-120">Selezionare, invece, hello **completare la migrazione** opzione per ogni computer si desidera toomigrate:</span><span class="sxs-lookup"><span data-stu-id="881c1-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="881c1-121">In **elementi replicati**, fare doppio clic su hello macchina virtuale e fare clic su **completare la migrazione**.</span><span class="sxs-lookup"><span data-stu-id="881c1-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="881c1-122">Fare clic su **OK** passaggio hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="881c1-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="881c1-123">È possibile monitorare i progressi nelle proprietà di hello macchina virtuale mediante il monitoraggio di processo di migrazione completa hello in **i processi di ripristino del sito**.</span><span class="sxs-lookup"><span data-stu-id="881c1-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="881c1-124">Hello **completare la migrazione** azione completa il processo di migrazione hello, rimuove la replica per macchina hello e viene arrestata la fatturazione di Site Recovery per la macchina hello.</span><span class="sxs-lookup"><span data-stu-id="881c1-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="881c1-126">Passaggio 2: Installare l'agente VM di Azure hello nella macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="881c1-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="881c1-127">Hello Azure [agente VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) deve essere installato nella macchina virtuale hello per hello Site Recovery estensione toowork e toohelp proteggere hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="881c1-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="881c1-128">A partire dalla versione 9.7.0.0, nelle macchine virtuali di Windows, il programma di installazione di hello mobilità servizio installa anche hello più recente disponibile agente VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="881c1-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="881c1-129">Sulla migrazione, macchina virtuale hello soddisfi i prerequisiti per l'utilizzo di qualsiasi estensione della macchina virtuale, inclusi l'estensione Site Recovery hello l'installazione dell'agente.</span><span class="sxs-lookup"><span data-stu-id="881c1-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="881c1-130">toobe esigenze di Hello macchina virtuale di Azure agente installato manualmente solo se il servizio di mobilità installato hello hello migrazione macchina è 9,6 o versione precedente.</span><span class="sxs-lookup"><span data-stu-id="881c1-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="881c1-131">Hello nella tabella seguente fornisce informazioni aggiuntive sull'installazione dell'agente VM hello e convalida che è stato installato:</span><span class="sxs-lookup"><span data-stu-id="881c1-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="881c1-132">**Operazione**</span><span class="sxs-lookup"><span data-stu-id="881c1-132">**Operation**</span></span> | <span data-ttu-id="881c1-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="881c1-133">**Windows**</span></span> | <span data-ttu-id="881c1-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="881c1-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="881c1-135">L'installazione dell'agente VM hello</span><span class="sxs-lookup"><span data-stu-id="881c1-135">Installing hello VM agent</span></span> |<span data-ttu-id="881c1-136">Scaricare e installare hello [agente MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="881c1-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="881c1-137">È necessario installazione hello toocomplete privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="881c1-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="881c1-138">Installare più recente hello [agente Linux](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="881c1-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="881c1-139">È necessario installazione hello toocomplete privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="881c1-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="881c1-140">Si consiglia di installare l'agente di hello dal proprio archivio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="881c1-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="881c1-141">Abbiamo *non è consigliabile* installa agente VM Linux hello direttamente da GitHub.</span><span class="sxs-lookup"><span data-stu-id="881c1-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="881c1-142">Convalida di installazione dell'agente VM hello</span><span class="sxs-lookup"><span data-stu-id="881c1-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="881c1-143">1. Sfoglia cartella C:\WindowsAzure\Packages toohello hello macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="881c1-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="881c1-144">Dovrebbe essere file WaAppAgent.exe hello.</span><span class="sxs-lookup"><span data-stu-id="881c1-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="881c1-145">2. Fare clic sul file hello, andare troppo**proprietà**, quindi selezionare hello **dettagli** hello scheda **versione prodotto** campo deve essere 2.6.1198.718 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="881c1-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="881c1-146">N/D</span><span class="sxs-lookup"><span data-stu-id="881c1-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="881c1-147">Passaggio 3: Rimuovere hello servizio di mobilità dalla hello migrazione di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="881c1-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="881c1-148">Se la migrazione dei computer VMware locali o dei server fisici in Windows/Linux, è necessario toomanually installazione/disinstallazione hello servizio di mobilità dalla macchina virtuale migrata hello.</span><span class="sxs-lookup"><span data-stu-id="881c1-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="881c1-149">Questo passaggio non è necessario per tooAzure stata eseguita la migrazione di macchine virtuali Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="881c1-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="881c1-150">Disinstallare il servizio di mobilità hello in una macchina virtuale di Windows Server</span><span class="sxs-lookup"><span data-stu-id="881c1-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="881c1-151">Utilizzare uno dei hello seguente servizio di mobilità hello toouninstall metodi in un computer Windows Server.</span><span class="sxs-lookup"><span data-stu-id="881c1-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="881c1-152">Disinstallare tramite l'interfaccia utente di Windows hello</span><span class="sxs-lookup"><span data-stu-id="881c1-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="881c1-153">Nel Pannello di controllo hello, selezionare **programmi**.</span><span class="sxs-lookup"><span data-stu-id="881c1-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="881c1-154">Selezionare **Microsoft Azure Site Recovery Mobility Service/Master Target server** (Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master) e fare clic su **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="881c1-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="881c1-155">Disinstallare dal prompt dei comandi</span><span class="sxs-lookup"><span data-stu-id="881c1-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="881c1-156">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="881c1-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="881c1-157">servizio di mobilità di hello di toouninstall, eseguire il comando seguente hello:</span><span class="sxs-lookup"><span data-stu-id="881c1-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="881c1-158">Disinstallare il servizio di mobilità hello in un computer Linux</span><span class="sxs-lookup"><span data-stu-id="881c1-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="881c1-159">Sul server Linux, accedere come utente **Root**.</span><span class="sxs-lookup"><span data-stu-id="881c1-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="881c1-160">In un terminal, andare troppo/utente/locale/ripristino automatico di sistema.</span><span class="sxs-lookup"><span data-stu-id="881c1-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="881c1-161">servizio di mobilità di hello di toouninstall, eseguire il comando seguente hello:</span><span class="sxs-lookup"><span data-stu-id="881c1-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="881c1-162">Passaggio 4: Riavviare hello VM</span><span class="sxs-lookup"><span data-stu-id="881c1-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="881c1-163">Dopo avere disinstallato il servizio di mobilità hello, riavvio hello VM prima di configurare replica tooanother area di Azure.</span><span class="sxs-lookup"><span data-stu-id="881c1-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="881c1-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="881c1-164">Next steps</span></span>
- <span data-ttu-id="881c1-165">Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="881c1-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="881c1-166">Altre informazioni sulle [indicazioni di connettività di rete per la replica delle macchine virtuali di Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="881c1-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
