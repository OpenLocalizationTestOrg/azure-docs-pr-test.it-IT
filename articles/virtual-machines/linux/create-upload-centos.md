---
title: aaaCreate e caricare un basato su CentOS Linux VHD in Azure
description: Informazioni su toocreate e caricare un Azure disco rigido virtuale (VHD) che contiene un sistema operativo basato su CentOS Linux.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Preparare una macchina virtuale basata su CentOS per Azure
* [Preparare una macchina virtuale CentOS 6.x per Azure](#centos-6x)
* [Preparare una macchina virtuale CentOS 7.0+ per Azure](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone di aver già installato un CentOS (o simile derivato) il disco rigido virtuale di Linux del sistema operativo tooa. Più strumenti esistono toocreate file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V. Per istruzioni, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).

**Note sull'installazione di CentOS**

* Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.
* formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.  È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd. Se si utilizza VirtualBox ciò significa che la selezione di **dimensioni fisse** come anziché predefinito toohello allocata in modo dinamico durante la creazione del disco hello.
* Quando si installa il sistema di Linux hello è *consigliato* utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni). Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un disco del sistema operativo necessaria tooanother toobe collegato identici macchina virtuale per la risoluzione dei problemi. È possibile usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) su dischi di dati.
* Per l'installazione di file system UDF è necessario il supporto di kernel. Al primo avvio del hello Azure configurazione provisioning viene passato toohello VM Linux tramite supporti formattati funzione definita dall'utente che sono collegato toohello guest. l'agente Linux di Azure Hello deve essere in grado di toomount hello UDF file system tooread la configurazione e provisioning hello macchina virtuale.
* Le versioni di kernel Linux inferiori a 2.6.37 non supportano NUMA su Hyper-V con macchine virtuali di dimensioni maggiori. Questo problema principalmente impatti distribuzioni precedenti utilizzando hello monte kernel Red Hat 2.6.32 ed è stato corretto in RHEL 6.6 (kernel-2.6.32-504). I sistemi che eseguono personalizzato kernel meno recente 2.6.37 o basato su RHEL kernel precedenti rispetto a 2.6.32-504 è necessario impostare il parametro di avvio di hello `numa=off` sul kernel hello in grub.conf della riga di comando. Per altre informazioni, vedere l'articolo Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Non si configura una partizione di scambio su disco del sistema operativo hello. agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.  Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.
* Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.

## <a name="centos-6x"></a>CentOS 6.x

1. Nella console di gestione Hyper-V selezionare macchina virtuale hello.

2. Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.

3. CentOS 6, NetworkManager può interferire con l'agente Linux di Azure hello. Disinstallazione di questo pacchetto eseguendo hello comando seguente:
   
        # sudo rpm -e --nodeps NetworkManager

4. Creare o modificare file hello `/etc/sysconfig/network` e aggiungere hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Creare o modificare file hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere hello seguente testo:
   
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
   
        # sudo chkconfig network on

8. Se si desidera mirror di OpenLogic hello toouse ospitati all'interno di hello Data Center di Azure, quindi sostituire hello `/etc/yum.repos.d/CentOS-Base.repo` file con hello seguenti repository.  Verrà anche aggiunta hello **[openlogic]** repository che include i pacchetti aggiuntivi, ad esempio l'agente Linux di Azure hello:

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    Hello resto di questa Guida verrà si presuppone l'uso almeno hello `[openlogic]` repository, che sarà utilizzato tooinstall agente Linux di Azure di hello indicato di seguito.


9. Aggiungere hello too/etc/yum.conf riga seguente:
    
        http_caching=packages

10. Eseguire hello successivo comando tooclear hello yum metadati e aggiornamento hello sistema corrente con i pacchetti hello più recenti:
    
        # yum clean all

    A meno che non si sta creando un'immagine per una versione precedente di CentOS, è consigliabile tooupdate che tutti hello pacchetti toohello più recente:

        # sudo yum -y update

    Dopo l'esecuzione di questo comando potrebbe essere necessario un riavvio.

11. (Facoltativo) Installare i driver di hello per hello Linux Integration Services (LIS).
   
    >[!IMPORTANT]
    passaggio di Hello è **obbligatorio** per CentOS 6.3 e facoltativo per le versioni successive e precedenti.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    In alternativa, è possibile seguire le istruzioni di installazione manuale di hello in hello [pagina di download LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM nella macchina virtuale.
 
12. Installare hello agente Linux di Azure e le dipendenze:
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    pacchetto WALinuxAgent Hello rimuoverà hello NetworkManager e pacchetti NetworkManager gnome se non sono stati già rimossi come descritto nel passaggio 3.


13. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo, aprire `/boot/grub/menu.lst` in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.
    
    Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri:
    
        rhgb quiet crashkernel=auto
    
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.  Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.

    >[!Important]
    CentOS versione 6.5 e versioni precedenti è necessario impostare anche il parametro kernel hello `numa=off`. Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.

14. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.  Si tratta in genere predefinito hello.

15. Non creare lo spazio di swapping sul disco del sistema operativo hello.
    
    Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure. Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning. Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare i seguenti parametri in hello `/etc/waagent.conf` in modo appropriato:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.


- - -
## <a name="centos-70"></a>CentOS 7.0+
**Modifiche in CentOS 7 (e sistemi derivati simili)**

Preparazione di una macchina virtuale CentOS 7 per Azure è molto simile tooCentOS 6, esistono tuttavia alcune differenze importanti non degni di nota:

* Hello NetworkManager del pacchetto non è in conflitto con l'agente Linux di Azure hello. Questo pacchetto viene installato per impostazione predefinita ed è consigliabile non rimuoverlo.
* GRUB2 viene utilizzato come hello del caricatore di avvio predefinito, in modo procedure hello per la modifica di parametri del kernel è stato modificato (vedere sotto).
* XFS è file system predefinito hello. Hello ext4 file sistema può comunque essere utilizzato se lo si desidera.

**Procedura di configurazione**

1. Nella console di gestione Hyper-V selezionare macchina virtuale hello.

2. Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.

3. Creare o modificare file hello `/etc/sysconfig/network` e aggiungere hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Creare o modificare file hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet. Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Se si desidera mirror di OpenLogic hello toouse ospitati all'interno di hello Data Center di Azure, quindi sostituire hello `/etc/yum.repos.d/CentOS-Base.repo` file con hello seguenti repository.  Verrà anche aggiunta hello **[openlogic]** repository che include i pacchetti per l'agente Linux di Azure hello:
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    Hello resto di questa Guida verrà si presuppone l'uso almeno hello `[openlogic]` repository, che sarà utilizzato tooinstall agente Linux di Azure di hello indicato di seguito.

7. Eseguire hello successivo comando tooclear hello corrente yum metadati e installare eventuali aggiornamenti:
   
        # sudo yum clean all

    A meno che non si sta creando un'immagine per una versione precedente di CentOS, è consigliabile tooupdate che tutti hello pacchetti toohello più recente:

        # sudo yum -y update

    Dopo l'esecuzione di questo comando potrebbe essere necessario un riavvio.

8. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo, aprire `/etc/default/grub` in hello di editor e modificare un testo `GRUB_CMDLINE_LINUX` parametro, ad esempio:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi. Disattiva anche hello nuove CentOS 7 convenzioni di denominazione per le schede NIC. Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri:
   
        rhgb quiet crashkernel=auto
   
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale. Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.

9. Dopo aver eseguito modifica `/etc/default/grub` al precedente, eseguire hello seguente comando toorebuild hello grub configurazione:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Se la creazione di immagine hello da **VMWare, VirtualBox o KVM:** driver di hello Hyper-V verificare sono inclusi in initramfs hello:
   
   Modificare `/etc/dracut.conf`e aggiungere il contenuto:
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Ricompilare initramfs hello:
   
        # sudo dracut –f -v

11. Installare hello agente Linux di Azure e le dipendenze:

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Non creare lo spazio di swapping sul disco del sistema operativo hello.
   
   Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure. Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning. Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare i seguenti parametri in hello `/etc/waagent.conf` in modo appropriato:
   
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

## <a name="next-steps"></a>Passaggi successivi
Si è ora pronto toouse Linux CentOS disco rigido virtuale toocreate nuove macchine virtuali in Azure. Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

