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
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Preparare una macchina virtuale SLES o openSUSE per Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone che è già stato installato un SUSE o il disco rigido virtuale di Linux del sistema operativo tooa openSUSE. Più strumenti esistono toocreate file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V. Per istruzioni, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="sles--opensuse-installation-notes"></a>Note di installazione di SLES/openSUSE
* Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.
* formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.  È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd.
* Quando si installa il sistema di Linux hello è consigliabile utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni). Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un sistema operativo disco mai necessario tooanother toobe collegato VM per la risoluzione dei problemi. Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Non si configura una partizione di scambio su disco del sistema operativo hello. agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.  Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.
* Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.

## <a name="use-suse-studio"></a>Usare SUSE Studio
[SUSE Studio](http://www.susestudio.com) consente di creare e gestire facilmente le immagini SLES e openSUSE per Azure e Hyper-V. Si tratta di hello approccio per personalizzare le proprie immagini SLES e openSUSE consigliato.

Come un'alternativa toobuilding proprio file VHD, SUSE pubblica anche le immagini BYOS (portare il propria sottoscrizione) per SLES in [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>Preparare SUSE Linux Enterprise Server 11 SP4
1. Nel riquadro centrale di hello di gestione di Hyper-V, selezionare macchina virtuale hello.
2. Fare clic su **Connetti** finestra hello tooopen per la macchina virtuale hello.
3. Registrare il tooallow sistema SUSE Linux Enterprise è toodownload aggiornamenti e i pacchetti di installazione.
4. Aggiornare il sistema di hello con patch più recenti di hello:
   
        # sudo zypper update
5. Installare hello agente Linux di Azure dal repository SLES hello:
   
        # sudo zypper install WALinuxAgent
6. Controllare se waagent viene impostato troppo "on" in chkconfig e, in caso contrario, abilitare la funzionalità per l'avvio automatico:
   
        # sudo chkconfig waagent on
7. Controllare se il servizio waagent è in esecuzione e, in caso contrario, avviarlo: 
   
        # sudo service waagent start
8. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. aprire questo toodo "/ boot/grub/menu.lst" in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    In questo modo tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.
9. Verificare che fstab /boot/grub/menu.lst e via/entrambi disco hello riferimento utilizzando il relativo UUID (da-uuid) anziché l'ID disco hello (da-id). 
   
    Ottenere l'UUID disco
   
        # ls /dev/disk/by-uuid/
   
    Se /dev/disk/by-id è utilizzato, aggiornare fstab /boot/grub/menu.lst e via/con il valore appropriato da uuid hello
   
    Prima della modifica
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    Dopo la modifica
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet. Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. È consigliabile file hello tooedit "/ e così via e sysconfig/rete/dhcp" e modificare hello `DHCLIENT_SET_HOSTNAME` seguente toohello parametro:
    
     DHCLIENT_SET_HOSTNAME="no"
12. In "e così via/file", impostare come commento o rimuovere hello seguenti righe se sono presenti:
    
     Per impostazione predefinita targetpw # richiesta hello password dell'utente di destinazione hello radice, ovvero tutti ALL=(ALL) tutti # avviso! Usare solo insieme a "Defaults targetpw".
13. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.  Si tratta in genere predefinito hello.
14. Non creare lo spazio di swapping sul disco del sistema operativo hello.
    
    Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure. Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning. Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # Nota: impostare questo toowhatever è necessario toobe.
15. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
16. Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.

- - -
## <a name="prepare-opensuse-131"></a>Preparare openSUSE 13.1+
1. Nel riquadro centrale di hello di gestione di Hyper-V, selezionare macchina virtuale hello.
2. Fare clic su **Connetti** finestra hello tooopen per la macchina virtuale hello.
3. In shell hello, eseguire il comando di hello '`zypper lr`'. Se questo comando restituisce l'output seguente, quindi i repository hello sono configurati come previsto, non sono necessarie rettifiche toohello simile (si noti che i numeri di versione possono variare):
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Se il comando hello non restituisce "Alcun repository definito..." utilizzare hello tooadd i comandi seguenti questi repository:
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    È quindi possibile verificare il repository hello è stati aggiunti tramite il comando hello '`zypper lr`' nuovamente. Nel caso in cui uno degli archivi di hello rilevanti aggiornamento non è abilitato, abilitarla con il comando seguente:
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Aggiornare hello kernel toohello versione disponibile più recente:
   
        # sudo zypper up kernel-default
   
    Sistema di hello tooupdate con tutte le patch più recente di hello o:
   
        # sudo zypper update
5. Installare hello agente Linux di Azure.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper install WALinuxAgent
6. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo, aprire "/ boot/grub/menu.lst" in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:
   
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
   In questo modo tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi. Inoltre, rimuovere hello seguenti parametri dalla riga di avvio del kernel hello se esistono:
   
     libata.atapi_enabled=0 reserve=0x1f0,0x8
7. È consigliabile file hello tooedit "/ e così via e sysconfig/rete/dhcp" e modificare hello `DHCLIENT_SET_HOSTNAME` seguente toohello parametro:
   
     DHCLIENT_SET_HOSTNAME="no"
8. **Importante:** In "e così via/file", impostare come commento o rimuovere hello seguenti righe se sono presenti:
   
     Per impostazione predefinita targetpw # richiesta hello password dell'utente di destinazione hello radice, ovvero tutti ALL=(ALL) tutti # avviso! Usare solo insieme a "Defaults targetpw".
9. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.  Si tratta in genere predefinito hello.
10. Non creare lo spazio di swapping sul disco del sistema operativo hello.
    
    Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure. Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning. Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # Nota: impostare questo toowhatever è necessario toobe.
11. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
12. Verificare hello che agente Linux di Azure viene eseguito all'avvio:
    
        # sudo systemctl enable waagent.service
13. Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.

## <a name="next-steps"></a>Passaggi successivi
Si è ora pronto toouse SUSE Linux disco rigido virtuale toocreate nuove macchine virtuali in Azure. Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

