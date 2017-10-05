---
title: Creazione e caricamento di un VHD Ubuntu Linux in Azure
description: Informazioni su come creare e caricare un disco rigido virtuale (VHD) di Azure che contiene un sistema operativo Ubuntu Linux.
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
ms.openlocfilehash: 4496b34ff88ca1e08cc74788ae09d787d4399eaf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="e15a4-103">Preparare una macchina virtuale Ubuntu per Azure</span><span class="sxs-lookup"><span data-stu-id="e15a4-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="e15a4-104">Immagini di Ubuntu Cloud ufficiali</span><span class="sxs-lookup"><span data-stu-id="e15a4-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="e15a4-105">Attualmente, Ubuntu pubblica VHD di Azure ufficiali per il download all'indirizzo [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="e15a4-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="e15a4-106">Se si deve creare un'immagine Ubuntu specializzata per Azure, piuttosto che seguire la procedura manuale riportata sotto si consiglia di iniziare con questi noti VHD funzionanti e personalizzarli in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e15a4-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="e15a4-107">Le ultime versioni delle immagini sono sempre disponibili nei seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="e15a4-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="e15a4-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e15a4-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="e15a4-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e15a4-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="e15a4-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e15a4-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e15a4-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e15a4-111">Prerequisites</span></span>
<span data-ttu-id="e15a4-112">In questo articolo si presuppone che l'utente abbia già installato un sistema operativo Ubuntu Linux in un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="e15a4-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="e15a4-113">Sono disponibili vari strumenti per creare file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e15a4-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="e15a4-114">Per istruzioni, vedere [Installare il ruolo Hyper-V e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e15a4-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="e15a4-115">**Note sull'installazione di Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e15a4-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="e15a4-116">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="e15a4-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="e15a4-117">Il formato VHDX non è supportato in Azure, solo nei **VHD fissi**.</span><span class="sxs-lookup"><span data-stu-id="e15a4-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="e15a4-118">È possibile convertire il disco in formato VHD tramite la console di gestione di Hyper-V o il cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="e15a4-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="e15a4-119">Durante l'installazione del sistema operativo Linux è consigliabile usare partizioni standard anziché LVM, che spesso è la scelta predefinita per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="e15a4-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="e15a4-120">In questo modo sarà possibile evitare conflitti di nome LVM con le macchine virtuali clonate, in particolare se fosse necessario collegare un disco del sistema operativo a un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e15a4-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="e15a4-121">Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e15a4-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="e15a4-122">Non configurare una partizione swap nel disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e15a4-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="e15a4-123">L'agente Linux può essere configurato in modo da creare un file swap sul disco temporaneo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="e15a4-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="e15a4-124">Altre informazioni su questo argomento sono disponibili nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="e15a4-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="e15a4-125">Tutti i dischi rigidi virtuali devono avere dimensioni multiple di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e15a4-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="e15a4-126">Passaggi manuali</span><span class="sxs-lookup"><span data-stu-id="e15a4-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="e15a4-127">Prima di provare a creare un'immagine personalizzata di Ubuntu per Azure, valutare in alternativa la possibilità di usare le immagini predefinite e testate di [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="e15a4-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="e15a4-128">Nel riquadro centrale della console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e15a4-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="e15a4-129">Fare clic su **Connect** per aprire la finestra della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e15a4-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="e15a4-130">Sostituire gli archivi correnti nell'immagine in modo da usare quelli Azure di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e15a4-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="e15a4-131">La procedura varia leggermente in base alla versione di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e15a4-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="e15a4-132">Prima di modificare `/etc/apt/sources.list`, è consigliabile eseguire un backup:</span><span class="sxs-lookup"><span data-stu-id="e15a4-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="e15a4-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="e15a4-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="e15a4-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="e15a4-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="e15a4-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="e15a4-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="e15a4-136">Le immagini di Ubuntu Azure ora seguono il kernel *HWE* (Hardware Enablement).</span><span class="sxs-lookup"><span data-stu-id="e15a4-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="e15a4-137">Aggiornare il sistema operativo al kernel più recente eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e15a4-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="e15a4-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="e15a4-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="e15a4-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="e15a4-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="e15a4-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="e15a4-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="e15a4-141">**Vedere anche:**</span><span class="sxs-lookup"><span data-stu-id="e15a4-141">**See also:**</span></span>
    - [<span data-ttu-id="e15a4-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="e15a4-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="e15a4-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="e15a4-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="e15a4-144">Modificare la riga di avvio del kernel per Grub in modo da includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="e15a4-144">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="e15a4-145">A questo scopo, aprire `/etc/default/grub` in un editor di testo, trovare la variabile denominata `GRUB_CMDLINE_LINUX_DEFAULT` (o aggiungerla, se necessario) e modificarla in modo da includere i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="e15a4-145">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="e15a4-146">Salvare e chiudere il file e quindi eseguire `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="e15a4-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="e15a4-147">In questo modo si garantisce che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto tecnico di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="e15a4-147">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="e15a4-148">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="e15a4-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="e15a4-149">Questo è in genere il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="e15a4-149">This is usually the default.</span></span>

7. <span data-ttu-id="e15a4-150">Installare l'agente Linux di Azure:</span><span class="sxs-lookup"><span data-stu-id="e15a4-150">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="e15a4-151">Il pacchetto `walinuxagent` potrebbe rimuovere i pacchetti `NetworkManager` e `NetworkManager-gnome`, se installati.</span><span class="sxs-lookup"><span data-stu-id="e15a4-151">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="e15a4-152">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="e15a4-152">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="e15a4-153">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e15a4-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e15a4-154">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="e15a4-154">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e15a4-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e15a4-155">Next steps</span></span>
<span data-ttu-id="e15a4-156">È ora possibile usare il disco rigido virtuale Ubuntu Linux per creare nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="e15a4-156">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="e15a4-157">Se è la prima volta che si carica il file VHD in Azure, vedere i passaggi 2 e 3 nell'articolo [Creazione e caricamento di un disco rigido virtuale che contiene il sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e15a4-157">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="e15a4-158">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="e15a4-158">References</span></span>
<span data-ttu-id="e15a4-159">Kernel HWE di Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e15a4-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="e15a4-160">http://blog.utlemming.org/2015/01/Ubuntu-1404-Azure-Images-Now-Tracking.HTML</span><span class="sxs-lookup"><span data-stu-id="e15a4-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="e15a4-161">http://blog.utlemming.org/2015/02/1204-Azure-cloud-Images-Now-using-Hwe.HTML</span><span class="sxs-lookup"><span data-stu-id="e15a4-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

