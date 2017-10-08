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
# <a name="prepare-a-debian-vhd-for-azure"></a>Preparare un disco rigido virtuale Debian per Azure
## <a name="prerequisites"></a>Prerequisiti
Questa sezione si presuppone che già stato installato un sistema operativo Debian Linux da un file con estensione ISO scaricato da hello [sito Web Debian](https://www.debian.org/distrib/) disco rigido virtuale tooa. File con estensione vhd toocreate; sono disponibili più strumenti Hyper-V è solo un esempio. Per istruzioni relative all'utilizzo di Hyper-V, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Note sull'installazione
* Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.
* il formato VHDX più recente di Hello non è supportato in Azure. È possibile convertire hello disco tooVHD formato Hyper-V Manager oppure hello **convert-vhd** cmdlet.
* Quando si installa il sistema di Linux hello è consigliabile utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni). Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un sistema operativo disco mai necessario tooanother toobe collegato VM per la risoluzione dei problemi. Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Non si configura una partizione di scambio su disco del sistema operativo hello. l'agente Linux di Azure Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello. Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.
* Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Usare Gestione di Azure toocreate Debian dischi rigidi virtuali
Sono disponibili strumenti per la generazione di dischi rigidi virtuali Debian per Azure, ad esempio hello [azure-Gestisci](https://github.com/credativ/azure-manage) script tra [credativ](http://www.credativ.com/). Si tratta di hello consigliato approccio rispetto alla creazione di un'immagine da zero. Ad esempio, toocreate un disco rigido virtuale di 8 Debian eseguito hello seguenti comandi di gestione di azure toodownload (e le dipendenze) ed eseguire script azure_build_image hello:

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>Preparare manualmente un disco rigido virtuale Debian
1. Nella console di gestione Hyper-V selezionare macchina virtuale hello.
2. Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.
3. Impostare come commento la riga hello per **deb cdrom** in `/etc/apt/source.list` se si configurano hello VM rispetto a un file ISO.
4. Modifica hello `/etc/default/grub` file e modificare hello **GRUB_CMDLINE_LINUX** parametro come indicato di seguito i parametri aggiuntivi kernel tooinclude per Azure.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Ricompilare grub hello ed eseguire:
   
        # sudo update-grub
6. Aggiungere repository Azure too/etc/apt/sources.list del Debian per Debian 7 o 8:
   
    **Debian 7.x "Wheezy"**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x "Jessie"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Installare l'agente Linux di Azure hello:
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Per Debian 7, è necessario toorun kernel basato su 3.16 hello dal repository wheezy backports hello. Creare innanzitutto un file denominato /etc/apt/preferences.d/linux.pref con hello seguente contenuto:
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    Quindi eseguire di nuovo kernel di "sudo apt-get installare linux-image-amd64" tooinstall hello.
3. Eseguire il deprovisioning macchina virtuale hello e prepararlo per il provisioning in Azure ed eseguire:
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. Fare clic su **Azione** -> Arresta nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.

## <a name="next-steps"></a>Passaggi successivi
Si è ora pronto toouse Debian disco rigido virtuale toocreate nuove macchine virtuali in Azure. Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

