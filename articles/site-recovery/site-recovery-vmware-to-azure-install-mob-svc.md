---
title: "Servizio di mobilità (VMware o fisici tooAzure) aaaInstall | Documenti Microsoft"
description: "Informazioni su come tooinstall hello servizio di mobilità agente tooprotect computer locale."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="de4ea-103">Installare il servizio di mobilità (VMware o fisici tooAzure)</span><span class="sxs-lookup"><span data-stu-id="de4ea-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="de4ea-104">Servizio di mobilità di Azure Site Recovery acquisisce scritture di dati in un computer e quindi li inoltra toohello server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="de4ea-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="de4ea-105">Distribuire il servizio di mobilità tooevery (VMware VM o server fisico) che si desidera tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="de4ea-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="de4ea-106">È possibile distribuire server toohello servizio di mobilità che si desidera tooprotect utilizzando hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="de4ea-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="de4ea-107">Installare il Servizio Mobility con strumenti di distribuzione software come System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="de4ea-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="de4ea-108">Installare il Servizio Mobility tramite Automazione di Azure e la configurazione dello stato desiderato (Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="de4ea-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="de4ea-109">Installare manualmente il servizio Mobility tramite l'interfaccia utente grafica di hello (GUI)</span><span class="sxs-lookup"><span data-stu-id="de4ea-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="de4ea-110">Installare manualmente il Servizio Mobility tramite un prompt di comando</span><span class="sxs-lookup"><span data-stu-id="de4ea-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="de4ea-111">Installare il Servizio Mobility tramite installazione push da Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="de4ea-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="de4ea-112">A partire dalla versione 9.7.0.0, nelle macchine virtuali di Windows (VM), programma di installazione del servizio di mobilità hello viene installato anche hello più recente disponibile [agente VM di Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="de4ea-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="de4ea-113">Quando un computer viene eseguito il failover tooAzure, computer hello soddisfa hello agente prerequisito di installazione per l'utilizzo di qualsiasi estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="de4ea-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de4ea-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="de4ea-114">Prerequisites</span></span>
<span data-ttu-id="de4ea-115">Completare questa procedura per i prerequisiti prima di iniziare a installare manualmente il Servizio Mobility nel server:</span><span class="sxs-lookup"><span data-stu-id="de4ea-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="de4ea-116">Accedi a server di configurazione tooyour e quindi aprire una finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="de4ea-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="de4ea-117">Cambiare cartella bin di hello directory toohello e quindi creare un file passphrase:</span><span class="sxs-lookup"><span data-stu-id="de4ea-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="de4ea-118">File dell'archivio hello passphrase in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="de4ea-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="de4ea-119">Utilizzare file hello durante l'installazione del servizio di mobilità hello.</span><span class="sxs-lookup"><span data-stu-id="de4ea-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="de4ea-120">Installazione di servizi di mobilità per tutti i sistemi operativi supportati sono nella cartella %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository hello.</span><span class="sxs-lookup"><span data-stu-id="de4ea-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="de4ea-121">Programma di installazione del servizio Mobility per il mapping del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="de4ea-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="de4ea-122">Nome del modello del file del programma di installazione</span><span class="sxs-lookup"><span data-stu-id="de4ea-122">Installer file template name</span></span>| <span data-ttu-id="de4ea-123">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="de4ea-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="de4ea-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="de4ea-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="de4ea-125">Windows Server 2008 R2 SP1 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="de4ea-126">Windows Server 2012 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="de4ea-127">Windows Server 2012 R2 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="de4ea-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="de4ea-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="de4ea-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="de4ea-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="de4ea-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="de4ea-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="de4ea-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="de4ea-133">CentOS 7.0, 7.1, 7.2 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="de4ea-134">CentOs 7.3 (solo per la migrazione)</span><span class="sxs-lookup"><span data-stu-id="de4ea-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="de4ea-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="de4ea-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="de4ea-136">SUSE Linux Enterprise Server 11 SP3 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="de4ea-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="de4ea-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="de4ea-138">SUSE Linux Enterprise Server 11 SP4 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="de4ea-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="de4ea-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="de4ea-140">Oracle Enterprise Linux 6.4, 6.5 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="de4ea-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="de4ea-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="de4ea-142">Ubuntu Linux 14.04 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="de4ea-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="de4ea-143">Installare manualmente il servizio Mobility tramite interfaccia utente grafica hello</span><span class="sxs-lookup"><span data-stu-id="de4ea-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="de4ea-144">Se si utilizza un **Server di configurazione** tooreplicate **macchine virtuali IaaS di Azure** da una sottoscrizione di Azure/area geografica, tooanother quindi **usare l'installazione da riga di comando basata su hello**  (metodo)</span><span class="sxs-lookup"><span data-stu-id="de4ea-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="de4ea-145">Installare manualmente il Servizio Mobility tramite un prompt di comando</span><span class="sxs-lookup"><span data-stu-id="de4ea-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="de4ea-146">Installazione dalla riga di comando in un computer Windows</span><span class="sxs-lookup"><span data-stu-id="de4ea-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="de4ea-147">Installazione dalla riga di comando in un computer Linux</span><span class="sxs-lookup"><span data-stu-id="de4ea-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="de4ea-148">Installare il Servizio Mobility tramite installazione push da Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="de4ea-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="de4ea-149">toodo un'installazione push del servizio di mobilità tramite il ripristino del sito, tutti i computer di destinazione devono soddisfare i seguenti prerequisiti hello.</span><span class="sxs-lookup"><span data-stu-id="de4ea-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="de4ea-150">Dopo aver installato il servizio di mobilità, nel portale di Azure hello selezionare hello **replicare** toostart pulsante proteggere queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="de4ea-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="de4ea-151">Disinstallare il servizio Mobility in un computer Windows Server</span><span class="sxs-lookup"><span data-stu-id="de4ea-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="de4ea-152">Utilizzare uno dei seguenti metodi toouninstall servizio di mobilità in un computer Server di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="de4ea-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="de4ea-153">Disinstallare utilizzando l'interfaccia utente grafica hello</span><span class="sxs-lookup"><span data-stu-id="de4ea-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="de4ea-154">Nel Pannello di controllo, selezionare **Programmi**.</span><span class="sxs-lookup"><span data-stu-id="de4ea-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="de4ea-155">Selezionare **Microsoft Azure Site Recovery Mobility Service/Master Target server** (Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master) e fare clic su **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="de4ea-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="de4ea-156">Disinstallare dal prompt dei comandi</span><span class="sxs-lookup"><span data-stu-id="de4ea-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="de4ea-157">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="de4ea-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="de4ea-158">toouninstall servizio di mobilità, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="de4ea-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="de4ea-159">Disinstallare il servizio Mobility in computer Linux</span><span class="sxs-lookup"><span data-stu-id="de4ea-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="de4ea-160">Sul server Linux, accedere come utente **Root**.</span><span class="sxs-lookup"><span data-stu-id="de4ea-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="de4ea-161">In un terminal, andare troppo/utente/locale/ripristino automatico di sistema.</span><span class="sxs-lookup"><span data-stu-id="de4ea-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="de4ea-162">toouninstall servizio di mobilità, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="de4ea-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
