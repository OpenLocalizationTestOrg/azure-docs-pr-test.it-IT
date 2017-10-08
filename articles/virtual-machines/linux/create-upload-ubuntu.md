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
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Preparare una macchina virtuale Ubuntu per Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Immagini di Ubuntu Cloud ufficiali
Attualmente, Ubuntu pubblica VHD di Azure ufficiali per il download all'indirizzo [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Se è necessario toobuild la propria immagine Ubuntu specializzata per Azure, anziché utilizzare la procedura manuale di hello sottostanti è consigliato toostart con questi noti l'utilizzo di dischi rigidi virtuali e personalizzare in base alle esigenze. Hello immagine più recenti sono sempre reperibile in hello posizioni seguenti:

* Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone che un Ubuntu Linux del sistema operativo tooa disco virtuale è già stato installato. Più strumenti esistono toocreate file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V. Per istruzioni, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).

**Note sull'installazione di Ubuntu**

* Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.
* formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.  È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd.
* Quando si installa il sistema di Linux hello è consigliabile utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni). Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un sistema operativo disco mai necessario tooanother toobe collegato VM per la risoluzione dei problemi. Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Non si configura una partizione di scambio su disco del sistema operativo hello. agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.  Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.
* Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.

## <a name="manual-steps"></a>Passaggi manuali
> [!NOTE]
> Prima di tentare di toocreate la propria immagine Ubuntu personalizzati per Azure, è consigliabile utilizzando hello predefinite e testata le immagini da [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) invece.
> 
> 

1. Nel riquadro centrale di hello di gestione di Hyper-V, selezionare macchina virtuale hello.

2. Fare clic su **Connetti** finestra hello tooopen per la macchina virtuale hello.

3. Sostituire repository corrente di hello nel repository di hello immagine toouse Ubuntu Azure. passaggi di Hello variano leggermente a seconda della versione di hello Ubuntu.
   
    Prima di modificare `/etc/apt/sources.list`, è consigliabile toomake una copia di backup:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Hello immagini Ubuntu Azure sono ora seguenti hello *abilitazione hardware* kernel (HWE). Aggiornare kernel più recente di hello del sistema operativo toohello eseguendo hello seguenti comandi:

    Ubuntu 12.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **Vedere anche:**
    - [https://wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Modifica linea di avvio di hello del kernel per i parametri aggiuntivi kernel tooinclude Grub per Azure. aprire questo toodo `/etc/default/grub` in un editor di testo, trovare la variabile di hello denominata `GRUB_CMDLINE_LINUX_DEFAULT` (o aggiungerlo se necessario) e modificarlo hello tooinclude seguenti parametri:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Salvare e chiudere il file e quindi eseguire `sudo update-grub`. In questo modo che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono il supporto tecnico Azure con il debug dei problemi.

6. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.  Si tratta in genere predefinito hello.

7. Installare l'agente Linux di Azure hello:
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Hello `walinuxagent` pacchetto può rimuovere hello `NetworkManager` e `NetworkManager-gnome` pacchetti, se sono installati.

8. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.

## <a name="next-steps"></a>Passaggi successivi
Si è ora pronto toouse Ubuntu Linux disco rigido virtuale toocreate nuove macchine virtuali in Azure. Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Riferimenti
Kernel HWE di Ubuntu

* [http://blog.utlemming.org/2015/01/Ubuntu-1404-Azure-Images-Now-Tracking.HTML](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-Azure-cloud-Images-Now-using-Hwe.HTML](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

