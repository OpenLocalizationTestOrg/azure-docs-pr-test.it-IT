---
title: aaaCreate e caricare un disco rigido virtuale di SUSE Linux in Azure
description: Informazioni su toocreate e caricare un Azure disco rigido virtuale (VHD) che contiene un sistema operativo SUSE Linux.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="1518a-103">Preparare una macchina virtuale SLES o openSUSE per Azure</span><span class="sxs-lookup"><span data-stu-id="1518a-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="1518a-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1518a-104">Prerequisites</span></span>
<span data-ttu-id="1518a-105">Questo articolo si presuppone che è già stato installato un SUSE o il disco rigido virtuale di Linux del sistema operativo tooa openSUSE.</span><span class="sxs-lookup"><span data-stu-id="1518a-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="1518a-106">Più strumenti esistono toocreate file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1518a-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="1518a-107">Per istruzioni, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="1518a-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="1518a-108">Note di installazione di SLES/openSUSE</span><span class="sxs-lookup"><span data-stu-id="1518a-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="1518a-109">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="1518a-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="1518a-110">formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.</span><span class="sxs-lookup"><span data-stu-id="1518a-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="1518a-111">È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="1518a-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="1518a-112">Quando si installa il sistema di Linux hello è consigliabile utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni).</span><span class="sxs-lookup"><span data-stu-id="1518a-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="1518a-113">Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un sistema operativo disco mai necessario tooanother toobe collegato VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="1518a-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="1518a-114">Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1518a-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="1518a-115">Non si configura una partizione di scambio su disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="1518a-116">agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="1518a-117">Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="1518a-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="1518a-118">Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1518a-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="1518a-119">Usare SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="1518a-119">Use SUSE Studio</span></span>
<span data-ttu-id="1518a-120">[SUSE Studio](http://www.susestudio.com) consente di creare e gestire facilmente le immagini SLES e openSUSE per Azure e Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1518a-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="1518a-121">Si tratta di hello approccio per personalizzare le proprie immagini SLES e openSUSE consigliato.</span><span class="sxs-lookup"><span data-stu-id="1518a-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="1518a-122">Come un'alternativa toobuilding proprio file VHD, SUSE pubblica anche le immagini BYOS (portare il propria sottoscrizione) per SLES in [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="1518a-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="1518a-123">Preparare SUSE Linux Enterprise Server 11 SP4</span><span class="sxs-lookup"><span data-stu-id="1518a-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="1518a-124">Nel riquadro centrale di hello di gestione di Hyper-V, selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="1518a-125">Fare clic su **Connetti** finestra hello tooopen per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="1518a-126">Registrare il tooallow sistema SUSE Linux Enterprise è toodownload aggiornamenti e i pacchetti di installazione.</span><span class="sxs-lookup"><span data-stu-id="1518a-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="1518a-127">Aggiornare il sistema di hello con patch più recenti di hello:</span><span class="sxs-lookup"><span data-stu-id="1518a-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="1518a-128">Installare hello agente Linux di Azure dal repository SLES hello:</span><span class="sxs-lookup"><span data-stu-id="1518a-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="1518a-129">Controllare se waagent viene impostato troppo "on" in chkconfig e, in caso contrario, abilitare la funzionalità per l'avvio automatico:</span><span class="sxs-lookup"><span data-stu-id="1518a-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="1518a-130">Controllare se il servizio waagent è in esecuzione e, in caso contrario, avviarlo:</span><span class="sxs-lookup"><span data-stu-id="1518a-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="1518a-131">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="1518a-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="1518a-132">aprire questo toodo "/ boot/grub/menu.lst" in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="1518a-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="1518a-133">In questo modo tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="1518a-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="1518a-134">Verificare che fstab /boot/grub/menu.lst e via/entrambi disco hello riferimento utilizzando il relativo UUID (da-uuid) anziché l'ID disco hello (da-id).</span><span class="sxs-lookup"><span data-stu-id="1518a-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="1518a-135">Ottenere l'UUID disco</span><span class="sxs-lookup"><span data-stu-id="1518a-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="1518a-136">Se /dev/disk/by-id è utilizzato, aggiornare fstab /boot/grub/menu.lst e via/con il valore appropriato da uuid hello</span><span class="sxs-lookup"><span data-stu-id="1518a-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="1518a-137">Prima della modifica</span><span class="sxs-lookup"><span data-stu-id="1518a-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="1518a-138">Dopo la modifica</span><span class="sxs-lookup"><span data-stu-id="1518a-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="1518a-139">Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1518a-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="1518a-140">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="1518a-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="1518a-141">È consigliabile file hello tooedit "/ e così via e sysconfig/rete/dhcp" e modificare hello `DHCLIENT_SET_HOSTNAME` seguente toohello parametro:</span><span class="sxs-lookup"><span data-stu-id="1518a-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="1518a-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="1518a-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="1518a-143">In "e così via/file", impostare come commento o rimuovere hello seguenti righe se sono presenti:</span><span class="sxs-lookup"><span data-stu-id="1518a-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="1518a-144">Per impostazione predefinita targetpw # richiesta hello password dell'utente di destinazione hello radice, ovvero tutti ALL=(ALL) tutti # avviso!</span><span class="sxs-lookup"><span data-stu-id="1518a-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="1518a-145">Usare solo insieme a "Defaults targetpw".</span><span class="sxs-lookup"><span data-stu-id="1518a-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="1518a-146">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="1518a-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="1518a-147">Si tratta in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-147">This is usually hello default.</span></span>
14. <span data-ttu-id="1518a-148">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="1518a-149">Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="1518a-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="1518a-150">Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="1518a-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="1518a-151">Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="1518a-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="1518a-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # Nota: impostare questo toowhatever è necessario toobe.</span><span class="sxs-lookup"><span data-stu-id="1518a-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="1518a-153">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="1518a-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="1518a-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="1518a-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="1518a-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="1518a-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="1518a-156">logout</span><span class="sxs-lookup"><span data-stu-id="1518a-156">logout</span></span>
16. <span data-ttu-id="1518a-157">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1518a-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="1518a-158">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1518a-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="1518a-159">Preparare openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="1518a-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="1518a-160">Nel riquadro centrale di hello di gestione di Hyper-V, selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="1518a-161">Fare clic su **Connetti** finestra hello tooopen per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="1518a-162">In shell hello, eseguire il comando di hello '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="1518a-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="1518a-163">Se questo comando restituisce l'output seguente, quindi i repository hello sono configurati come previsto, non sono necessarie rettifiche toohello simile (si noti che i numeri di versione possono variare):</span><span class="sxs-lookup"><span data-stu-id="1518a-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="1518a-164">Se il comando hello non restituisce "Alcun repository definito..." utilizzare hello tooadd i comandi seguenti questi repository:</span><span class="sxs-lookup"><span data-stu-id="1518a-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="1518a-165">È quindi possibile verificare il repository hello è stati aggiunti tramite il comando hello '`zypper lr`' nuovamente.</span><span class="sxs-lookup"><span data-stu-id="1518a-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="1518a-166">Nel caso in cui uno degli archivi di hello rilevanti aggiornamento non è abilitato, abilitarla con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1518a-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="1518a-167">Aggiornare hello kernel toohello versione disponibile più recente:</span><span class="sxs-lookup"><span data-stu-id="1518a-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="1518a-168">Sistema di hello tooupdate con tutte le patch più recente di hello o:</span><span class="sxs-lookup"><span data-stu-id="1518a-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="1518a-169">Installare hello agente Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="1518a-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="1518a-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="1518a-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="1518a-171">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="1518a-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="1518a-172">toodo, aprire "/ boot/grub/menu.lst" in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="1518a-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="1518a-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="1518a-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="1518a-174">In questo modo tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="1518a-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="1518a-175">Inoltre, rimuovere hello seguenti parametri dalla riga di avvio del kernel hello se esistono:</span><span class="sxs-lookup"><span data-stu-id="1518a-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="1518a-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="1518a-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="1518a-177">È consigliabile file hello tooedit "/ e così via e sysconfig/rete/dhcp" e modificare hello `DHCLIENT_SET_HOSTNAME` seguente toohello parametro:</span><span class="sxs-lookup"><span data-stu-id="1518a-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="1518a-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="1518a-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="1518a-179">**Importante:** In "e così via/file", impostare come commento o rimuovere hello seguenti righe se sono presenti:</span><span class="sxs-lookup"><span data-stu-id="1518a-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="1518a-180">Per impostazione predefinita targetpw # richiesta hello password dell'utente di destinazione hello radice, ovvero tutti ALL=(ALL) tutti # avviso!</span><span class="sxs-lookup"><span data-stu-id="1518a-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="1518a-181">Usare solo insieme a "Defaults targetpw".</span><span class="sxs-lookup"><span data-stu-id="1518a-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="1518a-182">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="1518a-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="1518a-183">Si tratta in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-183">This is usually hello default.</span></span>
10. <span data-ttu-id="1518a-184">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="1518a-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="1518a-185">Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="1518a-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="1518a-186">Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="1518a-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="1518a-187">Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="1518a-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="1518a-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # Nota: impostare questo toowhatever è necessario toobe.</span><span class="sxs-lookup"><span data-stu-id="1518a-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="1518a-189">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="1518a-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="1518a-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="1518a-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="1518a-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="1518a-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="1518a-192">logout</span><span class="sxs-lookup"><span data-stu-id="1518a-192">logout</span></span>
12. <span data-ttu-id="1518a-193">Verificare hello che agente Linux di Azure viene eseguito all'avvio:</span><span class="sxs-lookup"><span data-stu-id="1518a-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="1518a-194">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1518a-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="1518a-195">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1518a-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1518a-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1518a-196">Next steps</span></span>
<span data-ttu-id="1518a-197">Si è ora pronto toouse SUSE Linux disco rigido virtuale toocreate nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="1518a-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="1518a-198">Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1518a-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

