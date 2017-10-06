---
title: aaaCreate e caricare un disco rigido virtuale di Oracle Linux | Documenti Microsoft
description: Informazioni su toocreate e caricare un Azure disco rigido virtuale (VHD) che contiene un sistema operativo Linux Oracle.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Preparare una macchina virtuale Oracle Linux per Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone che un Oracle Linux del sistema operativo tooa disco virtuale è già stato installato. Più strumenti esistono toocreate file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V. Per istruzioni, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Note generali sull'installazione di Oracle Linux
* Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.
* Il kernel compatibile con Red Hat di Oracle e i relativi UEK3 (Unbreakable Enterprise Kernel) sono supportati sia su Hyper-V sia su Azure. Per ottenere risultati ottimali, essere tooupdate che toohello più recente kernel durante la preparazione del disco rigido virtuale di Oracle Linux.
* UEK2 Oracle non è supportata in Hyper-V e Azure che non includa i driver necessario hello.
* formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.  È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd.
* Quando si installa il sistema di Linux hello è consigliabile utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni). Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un sistema operativo disco mai necessario tooanother toobe collegato VM per la risoluzione dei problemi. Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* NUMA, non è supportato per dimensioni maggiori di macchina virtuale a causa di tooa bug nelle versioni di kernel Linux sotto 2.6.37. Questo problema influisce principalmente sul distribuzioni usando hello rosso a monte kernel 2.6.32 Hat. Installazione manuale dell'agente Linux di Azure hello (waagent) disabilita automaticamente NUMA nella configurazione di GRUB hello per kernel Linux hello. Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.
* Non si configura una partizione di scambio su disco del sistema operativo hello. agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.  Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.
* Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.
* Verificare che tale hello `Addons` repository è abilitato. Modificare il file hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) e modificare la riga hello `enabled=0` troppo`enabled=1` in **[ol6_addons]** o **[ol7_addons]** in questo file.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4+
È necessario completare i passaggi di configurazione specifici nel sistema operativo hello per hello toorun di macchina virtuale in Azure.

1. Nel riquadro centrale di hello di gestione di Hyper-V, selezionare macchina virtuale hello.
2. Fare clic su **Connetti** finestra hello tooopen per la macchina virtuale hello.
3. Disinstallare NetworkManager eseguendo hello comando seguente:
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Nota:** se il pacchetto di hello non è già installato, questo comando avrà esito negativo con un messaggio di errore. Si tratta di un comportamento previsto.
4. Creare un file denominato **rete** in hello `/etc/sysconfig/` directory che contiene hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Creare un file denominato **ifcfg eth0** in hello `/etc/sysconfig/network-scripts/` directory che contiene hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet. Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:
   
        # chkconfig network on
8. Installare python pyasn1 eseguendo hello comando seguente:
   
        # sudo yum install python-pyasn1
9. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. aprire questo toodo "/ boot/grub/menu.lst" in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi. NUMA verrà disabilitato a causa di bug tooa nel kernel di Oracle Red Hat compatibile.
   
   Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri:
   
        rhgb quiet crashkernel=auto
   
   Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.
   
   Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.
10. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.  Si tratta in genere predefinito hello.
11. Installare l'agente Linux di Azure hello eseguendo hello comando seguente. la versione più recente di Hello è 2.0.15.
    
        # sudo yum install WALinuxAgent
    
    Si noti che l'installazione pacchetto WALinuxAgent di hello rimuoverà hello NetworkManager pacchetti NetworkManager gnome se non sono stati già rimossi come descritto nel passaggio 2.
12. Non creare lo spazio di swapping sul disco del sistema operativo hello.
    
    Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure. Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning. Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0+
**Modifiche in Oracle Linux 7**

Preparazione di una macchina virtuale di Oracle Linux 7 per Azure è molto simile tooOracle Linux 6, esistono tuttavia alcune differenze importanti non degni di nota:

* In modalità kernel compatibile di hello Red Hat e UEK3 Oracle sono supportate in Azure.  è consigliabile kernel UEK3 Hello.
* Hello NetworkManager del pacchetto non è in conflitto con l'agente Linux di Azure hello. Questo pacchetto viene installato per impostazione predefinita ed è consigliabile non rimuoverlo.
* GRUB2 viene utilizzato come hello del caricatore di avvio predefinito, in modo procedure hello per la modifica di parametri del kernel è stato modificato (vedere sotto).
* XFS è file system predefinito hello. Hello ext4 file sistema può comunque essere utilizzato se lo si desidera.

**Procedura di configurazione**

1. Nella console di gestione Hyper-V selezionare macchina virtuale hello.
2. Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.
3. Creare un file denominato **rete** in hello `/etc/sysconfig/` directory che contiene hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Creare un file denominato **ifcfg eth0** in hello `/etc/sysconfig/network-scripts/` directory che contiene hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet. Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:
   
        # sudo chkconfig network on
7. Installare il pacchetto di python pyasn1 hello eseguendo hello comando seguente:
   
        # sudo yum install python-pyasn1
8. Eseguire hello successivo comando tooclear hello corrente yum metadati e installare eventuali aggiornamenti:
   
        # sudo yum clean all
        # sudo yum -y update
9. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo questo aprire "/ e così via/predefinito/grub" in un hello editor e la modifica del testo `GRUB_CMDLINE_LINUX` parametro, ad esempio:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi. Disattiva anche hello nuove OEL 7 convenzioni di denominazione per le schede NIC. Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri:
   
       rhgb quiet crashkernel=auto
   
   Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.
   
   Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.
10. Dopo aver eseguito modifica "/ e così via/predefinito/grub" al precedente, eseguire hello seguente comando toorebuild hello grub configurazione:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.  Si tratta in genere predefinito hello.
12. Installare l'agente Linux di Azure hello eseguendo hello comando seguente:
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Non creare lo spazio di swapping sul disco del sistema operativo hello.
    
    Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure. Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning. Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente hello), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.

## <a name="next-steps"></a>Passaggi successivi
Si è ora pronto toouse Oracle Linux con estensione vhd toocreate nuove macchine virtuali in Azure. Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

