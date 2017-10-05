---
title: Installare il servizio Mobility (VMware o fisico in Azure) | Microsoft Docs
description: Informazioni su come installare l'agente del Servizio Mobility per proteggere i computer locali.
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
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="5168c-103">Installare il Servizio Mobility (VMware o fisico in Azure)</span><span class="sxs-lookup"><span data-stu-id="5168c-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="5168c-104">Il Servizio Mobility di Azure Site Recovery acquisisce le scritture dei dati in un computer e le inoltra al server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5168c-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="5168c-105">Distribuire il servizio Mobility in ogni computer, ovvero macchina virtuale VMware o server fisico, di cui si vuole eseguire la replica in Azure.</span><span class="sxs-lookup"><span data-stu-id="5168c-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="5168c-106">È possibile distribuire il Servizio Mobility per i server che si desidera proteggere tramite i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5168c-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* [<span data-ttu-id="5168c-107">Installare il Servizio Mobility con strumenti di distribuzione software come System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="5168c-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="5168c-108">Installare il Servizio Mobility tramite Automazione di Azure e la configurazione dello stato desiderato (Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="5168c-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="5168c-109">Installare manualmente il Servizio Mobility tramite interfaccia utente grafica (GUI)</span><span class="sxs-lookup"><span data-stu-id="5168c-109">Install Mobility Service manually by using the graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="5168c-110">Installare manualmente il Servizio Mobility tramite un prompt di comando</span><span class="sxs-lookup"><span data-stu-id="5168c-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="5168c-111">Installare il Servizio Mobility tramite installazione push da Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5168c-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="5168c-112">A partire dalla versione 9.7.0.0, nelle macchine virtuali Windows il programma di installazione del Servizio Mobility installa anche l'[agente di macchine virtuali di Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent) più recente.</span><span class="sxs-lookup"><span data-stu-id="5168c-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="5168c-113">Quando un computer esegue il failover in Azure, il computer soddisfa i prerequisiti per l'installazione dell'agente per l'uso dell'estensione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5168c-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5168c-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5168c-114">Prerequisites</span></span>
<span data-ttu-id="5168c-115">Completare questa procedura per i prerequisiti prima di iniziare a installare manualmente il Servizio Mobility nel server:</span><span class="sxs-lookup"><span data-stu-id="5168c-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="5168c-116">Accedere al server di configurazione e quindi aprire una finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5168c-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="5168c-117">Cambiare la directory nella cartella bin e creare un file passphrase:</span><span class="sxs-lookup"><span data-stu-id="5168c-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="5168c-118">Salvare il file passphrase in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="5168c-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="5168c-119">Usare il file durante l'installazione del Servizio Mobility.</span><span class="sxs-lookup"><span data-stu-id="5168c-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="5168c-120">I programmi di installazione del Servizio Mobility per tutti i sistemi operativi supportati sono nella cartella %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span><span class="sxs-lookup"><span data-stu-id="5168c-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="5168c-121">Programma di installazione del servizio Mobility per il mapping del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="5168c-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="5168c-122">Nome del modello del file del programma di installazione</span><span class="sxs-lookup"><span data-stu-id="5168c-122">Installer file template name</span></span>| <span data-ttu-id="5168c-123">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="5168c-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="5168c-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="5168c-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="5168c-125">Windows Server 2008 R2 SP1 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="5168c-126">Windows Server 2012 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="5168c-127">Windows Server 2012 R2 (64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="5168c-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="5168c-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="5168c-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="5168c-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="5168c-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="5168c-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="5168c-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="5168c-133">CentOS 7.0, 7.1, 7.2 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="5168c-134">CentOs 7.3 (solo per la migrazione)</span><span class="sxs-lookup"><span data-stu-id="5168c-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="5168c-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="5168c-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="5168c-136">SUSE Linux Enterprise Server 11 SP3 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="5168c-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="5168c-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="5168c-138">SUSE Linux Enterprise Server 11 SP4 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="5168c-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="5168c-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="5168c-140">Oracle Enterprise Linux 6.4, 6.5 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="5168c-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="5168c-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="5168c-142">Ubuntu Linux 14.04 (solo a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="5168c-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="5168c-143">Installare manualmente il Servizio Mobility tramite la GUI</span><span class="sxs-lookup"><span data-stu-id="5168c-143">Install Mobility Service manually by using the GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="5168c-144">Se si usa un **server di configurazione** per replicare le **macchine virtuali IaaS di Azure** da una sottoscrizione o area di Azure a un'altra, **usare il metodo di installazione basato sulla riga di comando**</span><span class="sxs-lookup"><span data-stu-id="5168c-144">If you are using a **Configuration Server** to replicate **Azure IaaS virtual machines** from one Azure Subscription/Region to another then **use the Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="5168c-145">Installare manualmente il Servizio Mobility tramite un prompt di comando</span><span class="sxs-lookup"><span data-stu-id="5168c-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="5168c-146">Installazione dalla riga di comando in un computer Windows</span><span class="sxs-lookup"><span data-stu-id="5168c-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="5168c-147">Installazione dalla riga di comando in un computer Linux</span><span class="sxs-lookup"><span data-stu-id="5168c-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="5168c-148">Installare il Servizio Mobility tramite installazione push da Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5168c-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="5168c-149">Per eseguire un'installazione push del Servizio Mobility tramite Site Recovery, tutti i computer di destinazione devono soddisfare i prerequisiti seguenti.</span><span class="sxs-lookup"><span data-stu-id="5168c-149">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="5168c-150">Dopo l'installazione del Servizio Mobility, nel portale di Azure, selezionare il pulsante **Replica** per iniziare a proteggere le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5168c-150">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="5168c-151">Disinstallare il servizio Mobility in un computer Windows Server</span><span class="sxs-lookup"><span data-stu-id="5168c-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="5168c-152">Usare uno dei metodi seguenti per disinstallare il Servizio Mobility in un computer Windows Server.</span><span class="sxs-lookup"><span data-stu-id="5168c-152">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="5168c-153">Disinstallare usando la GUI</span><span class="sxs-lookup"><span data-stu-id="5168c-153">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="5168c-154">Nel Pannello di controllo, selezionare **Programmi**.</span><span class="sxs-lookup"><span data-stu-id="5168c-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="5168c-155">Selezionare **Microsoft Azure Site Recovery Mobility Service/Master Target server** (Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master) e fare clic su **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="5168c-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="5168c-156">Disinstallare dal prompt dei comandi</span><span class="sxs-lookup"><span data-stu-id="5168c-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="5168c-157">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5168c-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="5168c-158">Eseguire il comando seguente per disinstallare il servizio Mobility:</span><span class="sxs-lookup"><span data-stu-id="5168c-158">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="5168c-159">Disinstallare il servizio Mobility in computer Linux</span><span class="sxs-lookup"><span data-stu-id="5168c-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="5168c-160">Sul server Linux, accedere come utente **Root**.</span><span class="sxs-lookup"><span data-stu-id="5168c-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="5168c-161">Nel terminale, passare a /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="5168c-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="5168c-162">Eseguire il comando seguente per disinstallare il servizio Mobility:</span><span class="sxs-lookup"><span data-stu-id="5168c-162">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
