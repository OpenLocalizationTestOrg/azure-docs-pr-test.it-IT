---
title: aaaCreate e caricare un disco rigido virtuale di Ubuntu Linux in Azure
description: Informazioni su toocreate e caricare un Azure disco rigido virtuale (VHD) che contiene un sistema operativo Ubuntu Linux.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="d4291-103">Preparare una macchina virtuale Ubuntu per Azure</span><span class="sxs-lookup"><span data-stu-id="d4291-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="d4291-104">Immagini di Ubuntu Cloud ufficiali</span><span class="sxs-lookup"><span data-stu-id="d4291-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="d4291-105">Attualmente, Ubuntu pubblica VHD di Azure ufficiali per il download all'indirizzo [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="d4291-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="d4291-106">Se è necessario toobuild la propria immagine Ubuntu specializzata per Azure, anziché utilizzare la procedura manuale di hello sottostanti è consigliato toostart con questi noti l'utilizzo di dischi rigidi virtuali e personalizzare in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="d4291-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="d4291-107">Hello immagine più recenti sono sempre reperibile in hello posizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4291-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="d4291-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="d4291-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="d4291-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="d4291-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="d4291-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="d4291-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4291-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d4291-111">Prerequisites</span></span>
<span data-ttu-id="d4291-112">Questo articolo si presuppone che un Ubuntu Linux del sistema operativo tooa disco virtuale è già stato installato.</span><span class="sxs-lookup"><span data-stu-id="d4291-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="d4291-113">Più strumenti esistono toocreate file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d4291-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="d4291-114">Per istruzioni, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4291-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="d4291-115">**Note sull'installazione di Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="d4291-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="d4291-116">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="d4291-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="d4291-117">formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.</span><span class="sxs-lookup"><span data-stu-id="d4291-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="d4291-118">È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="d4291-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="d4291-119">Quando si installa il sistema di Linux hello è consigliabile utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni).</span><span class="sxs-lookup"><span data-stu-id="d4291-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="d4291-120">Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un sistema operativo disco mai necessario tooanother toobe collegato VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="d4291-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="d4291-121">Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4291-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="d4291-122">Non si configura una partizione di scambio su disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="d4291-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="d4291-123">agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="d4291-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="d4291-124">Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="d4291-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="d4291-125">Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="d4291-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="d4291-126">Passaggi manuali</span><span class="sxs-lookup"><span data-stu-id="d4291-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="d4291-127">Prima di tentare di toocreate la propria immagine Ubuntu personalizzati per Azure, è consigliabile utilizzando hello predefinite e testata le immagini da [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) invece.</span><span class="sxs-lookup"><span data-stu-id="d4291-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="d4291-128">Nel riquadro centrale di hello di gestione di Hyper-V, selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="d4291-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="d4291-129">Fare clic su **Connetti** finestra hello tooopen per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="d4291-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="d4291-130">Sostituire repository corrente di hello nel repository di hello immagine toouse Ubuntu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4291-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="d4291-131">passaggi di Hello variano leggermente a seconda della versione di hello Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d4291-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="d4291-132">Prima di modificare `/etc/apt/sources.list`, è consigliabile toomake una copia di backup:</span><span class="sxs-lookup"><span data-stu-id="d4291-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="d4291-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="d4291-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="d4291-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="d4291-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="d4291-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="d4291-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="d4291-136">Hello immagini Ubuntu Azure sono ora seguenti hello *abilitazione hardware* kernel (HWE).</span><span class="sxs-lookup"><span data-stu-id="d4291-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="d4291-137">Aggiornare kernel più recente di hello del sistema operativo toohello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="d4291-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="d4291-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="d4291-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="d4291-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="d4291-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="d4291-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="d4291-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="d4291-141">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="d4291-141">**See also:**</span></span>
    - [<span data-ttu-id="d4291-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="d4291-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="d4291-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="d4291-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="d4291-144">Modifica linea di avvio di hello del kernel per i parametri aggiuntivi kernel tooinclude Grub per Azure.</span><span class="sxs-lookup"><span data-stu-id="d4291-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="d4291-145">aprire questo toodo `/etc/default/grub` in un editor di testo, trovare la variabile di hello denominata `GRUB_CMDLINE_LINUX_DEFAULT` (o aggiungerlo se necessario) e modificarlo hello tooinclude seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="d4291-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="d4291-146">Salvare e chiudere il file e quindi eseguire `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="d4291-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="d4291-147">In questo modo che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono il supporto tecnico Azure con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="d4291-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="d4291-148">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="d4291-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="d4291-149">Si tratta in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="d4291-149">This is usually hello default.</span></span>

7. <span data-ttu-id="d4291-150">Installare l'agente Linux di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="d4291-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="d4291-151">Hello `walinuxagent` pacchetto può rimuovere hello `NetworkManager` e `NetworkManager-gnome` pacchetti, se sono installati.</span><span class="sxs-lookup"><span data-stu-id="d4291-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="d4291-152">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="d4291-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="d4291-153">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d4291-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="d4291-154">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d4291-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4291-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4291-155">Next steps</span></span>
<span data-ttu-id="d4291-156">Si è ora pronto toouse Ubuntu Linux disco rigido virtuale toocreate nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="d4291-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="d4291-157">Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4291-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="d4291-158">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="d4291-158">References</span></span>
<span data-ttu-id="d4291-159">Kernel HWE di Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d4291-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="d4291-160">http://blog.utlemming.org/2015/01/Ubuntu-1404-Azure-Images-Now-Tracking.HTML</span><span class="sxs-lookup"><span data-stu-id="d4291-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="d4291-161">http://blog.utlemming.org/2015/02/1204-Azure-cloud-Images-Now-using-Hwe.HTML</span><span class="sxs-lookup"><span data-stu-id="d4291-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

