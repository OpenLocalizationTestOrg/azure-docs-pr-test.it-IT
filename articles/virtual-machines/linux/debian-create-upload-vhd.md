---
title: Preparare un disco rigido virtuale di Linux Debian in Azure | Documentazione Microsoft
description: Informazioni su come creare i file Debian VHD 7 e 8 per la distribuzione in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 63970d162c12984d6476bf0b9fc4ab70160eccdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="5ad3c-103">Preparare un disco rigido virtuale Debian per Azure</span><span class="sxs-lookup"><span data-stu-id="5ad3c-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="5ad3c-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5ad3c-104">Prerequisites</span></span>
<span data-ttu-id="5ad3c-105">In questa sezione si presuppone che un sistema operativo Linux Debian sia già stato installato da un file .iso scaricato dal [sito Web di Debian](https://www.debian.org/distrib/) in un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from the [Debian website](https://www.debian.org/distrib/) to a virtual hard disk.</span></span> <span data-ttu-id="5ad3c-106">Sono disponibili vari strumenti per creare file con estensione .vhd; Hyper-V è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-106">Multiple tools exist to create .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="5ad3c-107">Per istruzioni sull’uso di Hyper-V, vedere [Installare il ruolo Hyper-V e configurare una macchina virtuale](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ad3c-107">For instructions using Hyper-V, see [Install the Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="5ad3c-108">Note sull'installazione</span><span class="sxs-lookup"><span data-stu-id="5ad3c-108">Installation notes</span></span>
* <span data-ttu-id="5ad3c-109">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="5ad3c-110">Il formato VHDX più recente non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-110">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="5ad3c-111">È possibile convertire il disco in formato VHD tramite la console di gestione di Hyper-V o il cmdlet **convert-vhd** .</span><span class="sxs-lookup"><span data-stu-id="5ad3c-111">You can convert the disk to VHD format using Hyper-V Manager or the **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="5ad3c-112">Durante l'installazione del sistema operativo Linux è consigliabile usare partizioni standard anziché LVM, che spesso è la scelta predefinita per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="5ad3c-113">In questo modo sarà possibile evitare conflitti di nome LVM con le macchine virtuali clonate, in particolare se fosse necessario collegare un disco del sistema operativo a un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="5ad3c-114">Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ad3c-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="5ad3c-115">Non configurare una partizione swap nel disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="5ad3c-116">L'agente Linux di Azure può essere configurato in modo da creare un file swap sul disco temporaneo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-116">The Azure Linux agent can be configured to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="5ad3c-117">Altre informazioni su questo argomento sono disponibili nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="5ad3c-118">Tutti i dischi rigidi virtuali devono avere dimensioni multiple di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-to-create-debian-vhds"></a><span data-ttu-id="5ad3c-119">Utilizzare Azure-Manage per creare dischi rigidi virtuali Debian</span><span class="sxs-lookup"><span data-stu-id="5ad3c-119">Use Azure-Manage to create Debian VHDs</span></span>
<span data-ttu-id="5ad3c-120">Per la generazione di dischi rigidi virtuali Debian per Azure sono disponibili alcuni strumenti, ad esempio gli script [azure-manage](https://github.com/credativ/azure-manage) di [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="5ad3c-120">There are tools available for generating Debian VHDs for Azure, such as the [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="5ad3c-121">Questo è l'approccio consigliato rispetto alla creazione di un'immagine da zero.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-121">This is the recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="5ad3c-122">Ad esempio, per creare un disco rigido virtuale Debian 8, eseguire i comandi seguenti per scaricare azure-manage (e le dipendenze) ed eseguire lo script azure_build_image:</span><span class="sxs-lookup"><span data-stu-id="5ad3c-122">For example, to create a Debian 8 VHD run the following commands to download azure-manage (and dependencies) and run the azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="5ad3c-123">Preparare manualmente un disco rigido virtuale Debian</span><span class="sxs-lookup"><span data-stu-id="5ad3c-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="5ad3c-124">Nella console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-124">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="5ad3c-125">Fare clic su **Connetti** per aprire una finestra della console per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-125">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="5ad3c-126">Impostare come commento la riga per **deb cdrom** in `/etc/apt/source.list` se si configura la macchina virtuale rispetto a un file ISO.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-126">Comment out the line for **deb cdrom** in `/etc/apt/source.list` if you set up the VM against an ISO file.</span></span>
4. <span data-ttu-id="5ad3c-127">Modificare il file `/etc/default/grub` e il parametro **GRUB_CMDLINE_LINUX** come indicato di seguito per includere parametri aggiuntivi del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-127">Edit the `/etc/default/grub` file and modify the **GRUB_CMDLINE_LINUX** parameter as follows to include additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="5ad3c-128">Ricompilare il grub ed eseguire:</span><span class="sxs-lookup"><span data-stu-id="5ad3c-128">Rebuild the grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="5ad3c-129">Aggiungere i repository Azure di Debian al file /etc/apt/sources.list per Debian 7 o 8:</span><span class="sxs-lookup"><span data-stu-id="5ad3c-129">Add Debian's Azure repositories to /etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="5ad3c-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="5ad3c-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="5ad3c-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="5ad3c-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="5ad3c-132">Installare l'agente Linux di Azure:</span><span class="sxs-lookup"><span data-stu-id="5ad3c-132">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="5ad3c-133">Per Debian 7, è necessario eseguire il kernel basato su 3.16 dal repository wheezy-backports.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-133">For Debian 7, it is required to run the 3.16-based kernel from the wheezy-backports repository.</span></span> <span data-ttu-id="5ad3c-134">Creare innanzitutto un file denominato /etc/apt/preferences.d/linux.pref con il seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="5ad3c-134">First create a file called /etc/apt/preferences.d/linux.pref with the following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="5ad3c-135">Quindi eseguire "sudo apt-get install linux-image-amd64" per l'installazione del nuovo kernel.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-135">Then run "sudo apt-get install linux-image-amd64" to install the new kernel.</span></span>
3. <span data-ttu-id="5ad3c-136">Effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure ed eseguire:</span><span class="sxs-lookup"><span data-stu-id="5ad3c-136">Deprovision the virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="5ad3c-137">Fare clic su **Azione** -> Arresta nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="5ad3c-138">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-138">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ad3c-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5ad3c-139">Next steps</span></span>
<span data-ttu-id="5ad3c-140">È ora possibile usare il disco rigido virtuale Debian per creare nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ad3c-140">You're now ready to use your Debian virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="5ad3c-141">Se è la prima volta che si carica il file VHD in Azure, vedere i passaggi 2 e 3 nell'articolo [Creazione e caricamento di un disco rigido virtuale che contiene il sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ad3c-141">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

