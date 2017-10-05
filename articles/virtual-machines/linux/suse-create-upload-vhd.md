---
title: Creazione e caricamento di un VHD SUSE Linux in Azure
description: Informazioni su come creare e caricare un disco rigido virtuale (VHD) di Azure che contiene un sistema operativo SUSE Linux.
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
ms.openlocfilehash: c829f5d9a90b4260c6f41b2d9e511a0c6cb48f18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="90aa2-103">Preparare una macchina virtuale SLES o openSUSE per Azure</span><span class="sxs-lookup"><span data-stu-id="90aa2-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="90aa2-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="90aa2-104">Prerequisites</span></span>
<span data-ttu-id="90aa2-105">In questo articolo si presuppone che l'utente abbia già installato un sistema operativo Linux SUSE od openSUSE in un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="90aa2-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="90aa2-106">Sono disponibili vari strumenti per creare file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="90aa2-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="90aa2-107">Per istruzioni, vedere [Installare il ruolo Hyper-V e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="90aa2-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="90aa2-108">Note di installazione di SLES/openSUSE</span><span class="sxs-lookup"><span data-stu-id="90aa2-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="90aa2-109">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="90aa2-110">Il formato VHDX non è supportato in Azure, solo nei **VHD fissi**.</span><span class="sxs-lookup"><span data-stu-id="90aa2-110">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="90aa2-111">È possibile convertire il disco in formato VHD tramite la console di gestione di Hyper-V o il cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="90aa2-111">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="90aa2-112">Durante l'installazione del sistema operativo Linux è consigliabile usare partizioni standard anziché LVM, che spesso è la scelta predefinita per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="90aa2-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="90aa2-113">In questo modo sarà possibile evitare conflitti di nome LVM con le macchine virtuali clonate, in particolare se fosse necessario collegare un disco del sistema operativo a un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="90aa2-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="90aa2-114">Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="90aa2-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="90aa2-115">Non configurare una partizione swap nel disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="90aa2-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="90aa2-116">L'agente Linux può essere configurato in modo da creare un file swap sul disco temporaneo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="90aa2-116">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="90aa2-117">Altre informazioni su questo argomento sono disponibili nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="90aa2-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="90aa2-118">Tutti i dischi rigidi virtuali devono avere dimensioni multiple di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="90aa2-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="90aa2-119">Usare SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="90aa2-119">Use SUSE Studio</span></span>
<span data-ttu-id="90aa2-120">[SUSE Studio](http://www.susestudio.com) consente di creare e gestire facilmente le immagini SLES e openSUSE per Azure e Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="90aa2-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="90aa2-121">Questo è l'approccio consigliato per personalizzare le proprie immagini SLES e openSUSE.</span><span class="sxs-lookup"><span data-stu-id="90aa2-121">This is the recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="90aa2-122">In alternativa alla creazione di un disco rigido virtuale, SUSE pubblica anche immagini BYOS (portare la propria sottoscrizione) per SLES in [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="90aa2-122">As an alternative to building your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="90aa2-123">Preparare SUSE Linux Enterprise Server 11 SP4</span><span class="sxs-lookup"><span data-stu-id="90aa2-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="90aa2-124">Nel riquadro centrale della console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90aa2-124">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="90aa2-125">Fare clic su **Connect** per aprire la finestra della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90aa2-125">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="90aa2-126">Registrare il sistema SUSE Linux Enterprise per scaricare gli aggiornamenti e installare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="90aa2-126">Register your SUSE Linux Enterprise system to allow it to download updates and install packages.</span></span>
4. <span data-ttu-id="90aa2-127">Aggiornare il sistema con tutte le patch più recenti:</span><span class="sxs-lookup"><span data-stu-id="90aa2-127">Update the system with the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="90aa2-128">Installare l'agente Linux di Azure dal repository SLES:</span><span class="sxs-lookup"><span data-stu-id="90aa2-128">Install the Azure Linux Agent from the SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="90aa2-129">Controllare se l'agente waagent è impostato su "on" in chkconfig e, in caso contrario, abilitarlo per l'avvio automatico:</span><span class="sxs-lookup"><span data-stu-id="90aa2-129">Check if waagent is set to "on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="90aa2-130">Controllare se il servizio waagent è in esecuzione e, in caso contrario, avviarlo:</span><span class="sxs-lookup"><span data-stu-id="90aa2-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="90aa2-131">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-131">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="90aa2-132">A questo scopo, aprire "/boot/grub/menu.lst" in un editor di testo e verificare che il kernel predefinito includa i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="90aa2-132">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="90aa2-133">In questo modo si garantisce che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="90aa2-133">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="90aa2-134">Verificare che /boot/grub/menu.lst e /etc/fstab facciano riferimento al disco tramite il relativo UUID (by-uuid) anziché l'ID disco (by-id).</span><span class="sxs-lookup"><span data-stu-id="90aa2-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference the disk using its UUID (by-uuid) instead of the disk ID (by-id).</span></span> 
   
    <span data-ttu-id="90aa2-135">Ottenere l'UUID disco</span><span class="sxs-lookup"><span data-stu-id="90aa2-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="90aa2-136">Se si usa /dev/disk/by-id/, aggiornare sia /boot/grub/menu.lst sia /etc/fstab con il valore by-uuid corretto</span><span class="sxs-lookup"><span data-stu-id="90aa2-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with the proper by-uuid value</span></span>
   
    <span data-ttu-id="90aa2-137">Prima della modifica</span><span class="sxs-lookup"><span data-stu-id="90aa2-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="90aa2-138">Dopo la modifica</span><span class="sxs-lookup"><span data-stu-id="90aa2-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="90aa2-139">Modificare le regole udev per evitare la generazione di regole statiche per l'interfaccia Ethernet.</span><span class="sxs-lookup"><span data-stu-id="90aa2-139">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="90aa2-140">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="90aa2-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="90aa2-141">Si consiglia di modificare il file "/etc/sysconfig/network/dhcp" e modificare il parametro `DHCLIENT_SET_HOSTNAME` come segue:</span><span class="sxs-lookup"><span data-stu-id="90aa2-141">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
    
     <span data-ttu-id="90aa2-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="90aa2-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="90aa2-143">In "/etc/sudoers" rimuovere o impostare come commento le righe seguenti, se esistenti:</span><span class="sxs-lookup"><span data-stu-id="90aa2-143">In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
    
     <span data-ttu-id="90aa2-144">Defaults targetpw   # chiedere la password dell'utente di destinazione vale a dire root ALL    ALL=(ALL) ALL   # WARNING!</span><span class="sxs-lookup"><span data-stu-id="90aa2-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="90aa2-145">Usare solo insieme a "Defaults targetpw".</span><span class="sxs-lookup"><span data-stu-id="90aa2-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="90aa2-146">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="90aa2-146">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="90aa2-147">Questo è in genere il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="90aa2-147">This is usually the default.</span></span>
14. <span data-ttu-id="90aa2-148">Non creare l'area di swap sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="90aa2-148">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="90aa2-149">L'agente Linux di Azure può configurare automaticamente l'area di swap utilizzando il disco risorse locale collegato alla VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-149">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="90aa2-150">Si noti che il disco risorse locale è un disco *temporaneo* e potrebbe essere svuotato in seguito al deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90aa2-150">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="90aa2-151">Dopo aver installato l'agente Linux di Azure come illustrato nel passaggio precedente, modificare i parametri seguenti in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="90aa2-151">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="90aa2-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTA: da impostare laddove richiesto.</span><span class="sxs-lookup"><span data-stu-id="90aa2-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
15. <span data-ttu-id="90aa2-153">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="90aa2-153">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="90aa2-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="90aa2-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="90aa2-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="90aa2-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="90aa2-156">logout</span><span class="sxs-lookup"><span data-stu-id="90aa2-156">logout</span></span>
16. <span data-ttu-id="90aa2-157">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="90aa2-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="90aa2-158">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-158">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="90aa2-159">Preparare openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="90aa2-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="90aa2-160">Nel riquadro centrale della console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90aa2-160">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="90aa2-161">Fare clic su **Connect** per aprire la finestra della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90aa2-161">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="90aa2-162">Nella shell eseguire il comando '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="90aa2-162">On the shell, run the command '`zypper lr`'.</span></span> <span data-ttu-id="90aa2-163">Se questo comando restituisce un output simile al seguente, i repository vengono configurati come previsto e non sono necessarie modifiche. Si noti che i numeri di versione possono variare:</span><span class="sxs-lookup"><span data-stu-id="90aa2-163">If this command returns output similar to the following, then the repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="90aa2-164">Se il comando restituisce un messaggio simile a "Nessun archivio definito..." usare i comandi seguenti per aggiungere gli archivi:</span><span class="sxs-lookup"><span data-stu-id="90aa2-164">If the command returns "No repositories defined..." then use the following commands to add these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="90aa2-165">Sarà quindi possibile verificare che i repository siano stati aggiunti eseguendo nuovamente il comando '`zypper lr`' .</span><span class="sxs-lookup"><span data-stu-id="90aa2-165">You can then verify the repositories have been added by running the command '`zypper lr`' again.</span></span> <span data-ttu-id="90aa2-166">Se uno degli archivi di aggiornamento pertinenti non è abilitato, abilitarlo con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="90aa2-166">In case one of the relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="90aa2-167">Aggiornare il kernel all'ultima versione disponibile:</span><span class="sxs-lookup"><span data-stu-id="90aa2-167">Update the kernel to the latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="90aa2-168">Oppure per aggiornare il sistema con tutte le patch più recenti:</span><span class="sxs-lookup"><span data-stu-id="90aa2-168">Or to update the system with all the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="90aa2-169">Installare l'agente Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-169">Install the Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="90aa2-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="90aa2-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="90aa2-171">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-171">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="90aa2-172">A questo scopo, aprire "/boot/grub/menu.lst" in un editor di testo e verificare che il kernel predefinito includa i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="90aa2-172">To do this, open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
     <span data-ttu-id="90aa2-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="90aa2-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="90aa2-174">In questo modo si garantisce che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="90aa2-174">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="90aa2-175">Rimuovere inoltre i messaggi seguenti dalla riga di avvio del kernel, se presenti:</span><span class="sxs-lookup"><span data-stu-id="90aa2-175">In addition, remove the following parameters from the kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="90aa2-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="90aa2-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="90aa2-177">Si consiglia di modificare il file "/etc/sysconfig/network/dhcp" e modificare il parametro `DHCLIENT_SET_HOSTNAME` come segue:</span><span class="sxs-lookup"><span data-stu-id="90aa2-177">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
   
     <span data-ttu-id="90aa2-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="90aa2-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="90aa2-179">**Importante** : in "/etc/sudoers" rimuovere o impostare come commento le righe seguenti, se esistenti:</span><span class="sxs-lookup"><span data-stu-id="90aa2-179">**Important:** In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
   
     <span data-ttu-id="90aa2-180">Defaults targetpw   # chiedere la password dell'utente di destinazione vale a dire root ALL    ALL=(ALL) ALL   # WARNING!</span><span class="sxs-lookup"><span data-stu-id="90aa2-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="90aa2-181">Usare solo insieme a "Defaults targetpw".</span><span class="sxs-lookup"><span data-stu-id="90aa2-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="90aa2-182">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="90aa2-182">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="90aa2-183">Questo è in genere il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="90aa2-183">This is usually the default.</span></span>
10. <span data-ttu-id="90aa2-184">Non creare l'area di swap sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="90aa2-184">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="90aa2-185">L'agente Linux di Azure può configurare automaticamente l'area di swap utilizzando il disco risorse locale collegato alla VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-185">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="90aa2-186">Si noti che il disco risorse locale è un disco *temporaneo* e potrebbe essere svuotato in seguito al deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90aa2-186">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="90aa2-187">Dopo aver installato l'agente Linux di Azure come illustrato nel passaggio precedente, modificare i parametri seguenti in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="90aa2-187">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="90aa2-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTA: da impostare laddove richiesto.</span><span class="sxs-lookup"><span data-stu-id="90aa2-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
11. <span data-ttu-id="90aa2-189">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="90aa2-189">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="90aa2-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="90aa2-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="90aa2-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="90aa2-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="90aa2-192">logout</span><span class="sxs-lookup"><span data-stu-id="90aa2-192">logout</span></span>
12. <span data-ttu-id="90aa2-193">Verificare che l'agente Linux di Azure venga eseguito all'avvio:</span><span class="sxs-lookup"><span data-stu-id="90aa2-193">Ensure the Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="90aa2-194">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="90aa2-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="90aa2-195">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-195">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90aa2-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90aa2-196">Next steps</span></span>
<span data-ttu-id="90aa2-197">È ora possibile usare il disco rigido virtuale SUSE Linux per creare nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="90aa2-197">You're now ready to use your SUSE Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="90aa2-198">Se è la prima volta che si carica il file VHD in Azure, vedere i passaggi 2 e 3 nell'articolo [Creazione e caricamento di un disco rigido virtuale che contiene il sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="90aa2-198">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

