---
title: un disco rigido virtuale in Azure a Debian Linux aaaPrepare | Documenti Microsoft
description: Informazioni su come toocreate Debian 7 & VHD 8 file per la distribuzione in Azure.
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
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="ebdf0-103">Preparare un disco rigido virtuale Debian per Azure</span><span class="sxs-lookup"><span data-stu-id="ebdf0-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="ebdf0-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ebdf0-104">Prerequisites</span></span>
<span data-ttu-id="ebdf0-105">Questa sezione si presuppone che già stato installato un sistema operativo Debian Linux da un file con estensione ISO scaricato da hello [sito Web Debian](https://www.debian.org/distrib/) disco rigido virtuale tooa.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="ebdf0-106">File con estensione vhd toocreate; sono disponibili più strumenti Hyper-V è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="ebdf0-107">Per istruzioni relative all'utilizzo di Hyper-V, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebdf0-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="ebdf0-108">Note sull'installazione</span><span class="sxs-lookup"><span data-stu-id="ebdf0-108">Installation notes</span></span>
* <span data-ttu-id="ebdf0-109">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="ebdf0-110">il formato VHDX più recente di Hello non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="ebdf0-111">È possibile convertire hello disco tooVHD formato Hyper-V Manager oppure hello **convert-vhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="ebdf0-112">Quando si installa il sistema di Linux hello è consigliabile utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni).</span><span class="sxs-lookup"><span data-stu-id="ebdf0-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="ebdf0-113">Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un sistema operativo disco mai necessario tooanother toobe collegato VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="ebdf0-114">Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ebdf0-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="ebdf0-115">Non si configura una partizione di scambio su disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="ebdf0-116">l'agente Linux di Azure Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="ebdf0-117">Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="ebdf0-118">Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="ebdf0-119">Usare Gestione di Azure toocreate Debian dischi rigidi virtuali</span><span class="sxs-lookup"><span data-stu-id="ebdf0-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="ebdf0-120">Sono disponibili strumenti per la generazione di dischi rigidi virtuali Debian per Azure, ad esempio hello [azure-Gestisci](https://github.com/credativ/azure-manage) script tra [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="ebdf0-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="ebdf0-121">Si tratta di hello consigliato approccio rispetto alla creazione di un'immagine da zero.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="ebdf0-122">Ad esempio, toocreate un disco rigido virtuale di 8 Debian eseguito hello seguenti comandi di gestione di azure toodownload (e le dipendenze) ed eseguire script azure_build_image hello:</span><span class="sxs-lookup"><span data-stu-id="ebdf0-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="ebdf0-123">Preparare manualmente un disco rigido virtuale Debian</span><span class="sxs-lookup"><span data-stu-id="ebdf0-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="ebdf0-124">Nella console di gestione Hyper-V selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="ebdf0-125">Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="ebdf0-126">Impostare come commento la riga hello per **deb cdrom** in `/etc/apt/source.list` se si configurano hello VM rispetto a un file ISO.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="ebdf0-127">Modifica hello `/etc/default/grub` file e modificare hello **GRUB_CMDLINE_LINUX** parametro come indicato di seguito i parametri aggiuntivi kernel tooinclude per Azure.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="ebdf0-128">Ricompilare grub hello ed eseguire:</span><span class="sxs-lookup"><span data-stu-id="ebdf0-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="ebdf0-129">Aggiungere repository Azure too/etc/apt/sources.list del Debian per Debian 7 o 8:</span><span class="sxs-lookup"><span data-stu-id="ebdf0-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="ebdf0-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="ebdf0-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="ebdf0-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="ebdf0-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="ebdf0-132">Installare l'agente Linux di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="ebdf0-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="ebdf0-133">Per Debian 7, è necessario toorun kernel basato su 3.16 hello dal repository wheezy backports hello.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="ebdf0-134">Creare innanzitutto un file denominato /etc/apt/preferences.d/linux.pref con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="ebdf0-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="ebdf0-135">Quindi eseguire di nuovo kernel di "sudo apt-get installare linux-image-amd64" tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="ebdf0-136">Eseguire il deprovisioning macchina virtuale hello e prepararlo per il provisioning in Azure ed eseguire:</span><span class="sxs-lookup"><span data-stu-id="ebdf0-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="ebdf0-137">Fare clic su **Azione** -> Arresta nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="ebdf0-138">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebdf0-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ebdf0-139">Next steps</span></span>
<span data-ttu-id="ebdf0-140">Si è ora pronto toouse Debian disco rigido virtuale toocreate nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="ebdf0-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="ebdf0-141">Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ebdf0-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

