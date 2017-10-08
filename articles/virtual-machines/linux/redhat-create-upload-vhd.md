---
title: aaaCreate e caricare un file di Red Hat Enterprise Linux VHD per l'uso in Azure | Documenti Microsoft
description: Informazioni su toocreate e caricare un Azure disco rigido virtuale (VHD) che contiene un sistema operativo Red Hat Linux.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Preparare una macchina virtuale basata su RedHat per Azure
In questo articolo si apprenderà come tooprepare una macchina virtuale Red Hat Enterprise Linux (RHEL) per l'uso in Azure. versioni di Hello di RHEL trattate in questo articolo sono 6.7 + e + 7.1. hypervisor di Hello per la preparazione che rientrano in questo articolo sono macchina virtuale Hyper-V, basata sul kernel (KVM) e VMware. Per altre informazioni sui requisiti di idoneità per partecipare al programma di accesso al cloud di Red Hat, vedere gli articoli relativi al [sito web di accesso al cloud di Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) e all'[esecuzione di RHEL in Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Preparare una macchina virtuale basata su Red Hat dalla console di gestione di Hyper-V

### <a name="prerequisites"></a>Prerequisiti
In questa sezione si presuppone che si possiede già un file ISO dal sito Web di Red Hat hello e installato hello RHEL immagine tooa disco rigido virtuale (VHD). Per ulteriori informazioni su come tooinstall di gestione di Hyper-V toouse un'immagine del sistema operativo, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).

**Note sull'installazione di RHEL**

* Azure non supporta il formato di file VHDX hello. Azure supporta solo dischi rigidi virtuali a dimensione fissa. È possibile usare Gestione di Hyper-V tooconvert hello disco tooVHD formato oppure è possibile utilizzare cmdlet convert-vhd hello. Se si utilizza VirtualBox, selezionare **dimensioni fisse** rispetto predefinito toohello allocati dinamicamente opzione quando si crea il disco di hello.
* Azure supporta solo macchine virtuali di prima generazione. Formato di file disco rigido virtuale VHDX toohello e dal disco di dimensioni fisse tooa a espansione dinamica, è possibile convertire una macchina virtuale di generazione 1. Non è possibile modificare la generazione di una macchina virtuale. Per altre informazioni, vedere [Creare una macchina virtuale di generazione 1 o 2 in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* dimensioni massime Hello che sono consentita per il disco rigido virtuale hello è 1023 GB.
* Quando si installa hello del sistema operativo Linux, è consigliabile utilizzare partizioni standard piuttosto che come Manager di Volume logico (LVM) è spesso predefinito hello per numerose installazioni. Questo modo, si eviteranno LVM nome in conflitto con le macchine virtuali clonate, in particolare se avrai bisogno di macchina virtuale identica un sistema operativo disco tooanother tooattach per la risoluzione dei problemi. È possibile usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) su dischi di dati.
* Per montare file system UDF (Universal Disk Format) è necessario il supporto del kernel. Al primo avvio in Azure, hello in formato UDF supporto che è collegato toohello guest passa hello provisioning configurazione toohello macchina virtuale Linux. Hello agente Linux di Azure deve essere in grado di toomount hello UDF file system tooread la configurazione e provisioning di macchina virtuale hello.
* Versioni del kernel Linux hello 2.6.37 precedenti non supportano (NUMA) non-uniform memory access in Hyper-V con dimensioni maggiori di macchina virtuale. Questo problema principalmente impatti distribuzioni precedenti che usano hello monte kernel Red Hat 2.6.32 ed è stato corretto in RHEL 6.6 (kernel-2.6.32-504). I sistemi che eseguono kernel personalizzato che risalgono a più 2.6.37 o directcompute basato su RHEL che risalgono a più 2.6.32-504 devono impostare hello `numa=off` parametro di avvio nella riga di comando di kernel hello in grub.conf. Per altre informazioni, vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.
* Non si configura una partizione di scambio su disco del sistema operativo hello. Hello agente Linux può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.  Ulteriori informazioni su questo sono reperibile in hello alla procedura seguente.
* Le dimensioni di tutti i dischi rigidi virtuali devono essere multipli di 1 MB.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Preparare una macchina virtuale RHEL 6 dalla console di gestione di Hyper-V

1. Nella console di gestione Hyper-V selezionare macchina virtuale hello.

2. Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.

3. RHEL 6, NetworkManager può interferire con l'agente Linux di Azure hello. Disinstallazione di questo pacchetto eseguendo hello comando seguente:
   
        # sudo rpm -e --nodeps NetworkManager

4. Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Spostare o rimuovere hello udev regole tooavoid la generazione di regole statiche per l'interfaccia Ethernet hello. Le regole seguenti provocano problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:

        # sudo chkconfig network on

8. Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat. Abilitare repository extra hello eseguendo hello comando seguente:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo questa modifica, aprire `/boot/grub/menu.lst` in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Questa operazione garantisce inoltre che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.
    
    Inoltre, è consigliabile rimuovere hello seguenti parametri:
    
        rhgb quiet crashkernel=auto
    
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.  È possibile lasciare hello `crashkernel` opzione configurato se si desidera. Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più. Questa configurazione potrebbe causare problemi in macchine virtuali di dimensioni inferiori.

    >[!Important]
    RHEL versione 6.5 e versioni precedenti è necessario impostare anche hello `numa=off` parametro kernel. Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.

11. Verificare che il server protetto shell (SSH) hello sia installato e configurato toostart in fase di avvio, è in genere predefinito hello. Modificare /etc/ssh/sshd_config tooinclude hello seguente riga:

        ClientAliveInterval 180

12. Installare l'agente Linux di Azure hello eseguendo hello comando seguente:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    Pacchetto di WALinuxAgent hello installazione rimuove hello NetworkManager e pacchetti NetworkManager gnome se non sono stati già rimossi nel passaggio 3.

13. Non creare lo spazio di swapping sul disco del sistema operativo hello.

    Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure. Si noti che hello locale disco di risorsa è un disco temporaneo e che può essere svuotato quando viene effettuato il deprovisioning macchina virtuale hello. Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Annullare la registrazione hello sottoscrizione (se necessario) eseguendo hello comando seguente:

        # sudo subscription-manager unregister

15. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Fare clic su **Azione** > **Arresta** nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Preparare una macchina virtuale RHEL 7 dalla console di gestione di Hyper-V

1. Nella console di gestione Hyper-V selezionare macchina virtuale hello.

2. Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.

3. Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:

        # sudo chkconfig network on

6. Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo questa modifica, aprirla `/etc/default/grub` in un editor di testo e modifica hello `GRUB_CMDLINE_LINUX` parametro. ad esempio:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Questa operazione garantisce inoltre che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi. Questa configurazione viene disattivata anche hello nuove RHEL 7 convenzioni di denominazione per le schede NIC. Inoltre, è consigliabile rimuovere hello seguenti parametri:
   
        rhgb quiet crashkernel=auto
   
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale. È possibile lasciare hello `crashkernel` opzione configurato se si desidera. Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.

8. Dopo avere completato modifica `/etc/default/grub`eseguire hello seguenti comando toorebuild hello grub configurazione:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio, è in genere predefinito hello. Modificare `/etc/ssh/sshd_config` hello tooinclude seguente riga:

        ClientAliveInterval 180

10. pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat. Abilitare repository extra hello eseguendo hello comando seguente:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Installare l'agente Linux di Azure hello eseguendo hello comando seguente:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Non creare lo spazio di swapping sul disco del sistema operativo hello.

    Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure. Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning. Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in `/etc/waagent.conf` in modo appropriato:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Se si desidera che toounregister hello sottoscrizione, eseguire hello comando seguente:

        # sudo subscription-manager unregister

14. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Fare clic su **Azione** > **Arresta** nella console di gestione di Hyper-V. Il VHD Linux è ora pronto toobe caricato tooAzure.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Preparare una macchina virtuale basata su Red Hat da KVM
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>Preparare una macchina virtuale RHEL 6 da KVM

1. Scaricare l'immagine KVM hello RHEL 6 dal sito Web di hello Red Hat.

2. Impostare una password radice.

    Generare una password crittografata e copiare l'output di hello del comando hello:

        # openssl passwd -1 changeme

    Impostare una password radice con guestfish:
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Secondo campo hello modifica dell'utente root hello da "." password crittografata toohello.

3. Creare una macchina virtuale KVM dall'immagine qcow2 hello. Impostare il tipo di disco hello troppo**qcow2**e impostare modello dispositivo dell'interfaccia di rete virtuale hello troppo**virtio**. Quindi, avviare la macchina virtuale hello e accedere come radice.

4. Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Spostare o rimuovere hello udev regole tooavoid la generazione di regole statiche per l'interfaccia Ethernet hello. Le regole seguenti causano problemi quando si clona una macchina virtuale in Azure o Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:

        # chkconfig network on

8. Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo questa configurazione, aprire `/boot/grub/menu.lst` in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Questa operazione garantisce inoltre che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.
    
    Inoltre, è consigliabile rimuovere hello seguenti parametri:
    
        rhgb quiet crashkernel=auto
    
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale. È possibile lasciare hello `crashkernel` opzione configurato se si desidera. Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.

    >[!Important]
    RHEL versione 6.5 e versioni precedenti è necessario impostare anche hello `numa=off` parametro kernel. Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.

10. Aggiungere tooinitramfs moduli Hyper-V:  

    Modifica `/etc/dracut.conf`e aggiungere hello seguente contenuto:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Ricompilare initramfs:

        # dracut -f -v

11. Disinstallare cloud-init:

        # yum remove cloud-init

12. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio:

        # chkconfig sshd on

    Modificare /etc/ssh/sshd_config tooinclude hello seguenti righe:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat. Abilitare repository extra hello eseguendo hello comando seguente:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Installare l'agente Linux di Azure hello eseguendo hello comando seguente:

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure. Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning. Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in **/etc/waagent.conf** in modo appropriato:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Annullare la registrazione hello sottoscrizione (se necessario) eseguendo hello comando seguente:

        # subscription-manager unregister

17. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Spegnere la macchina virtuale hello KVM.

19. Convertire il formato VHD toohello di hello qcow2 immagine.

    Prima di convertire formato tooraw di hello immagine:

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Assicurarsi che le dimensioni di hello dell'immagine non elaborati di hello sono allineata con 1 MB. In caso contrario, l'arrotondamento per eccesso hello dimensioni tooalign con 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertire hello disco raw tooa dimensione fissa disco rigido virtuale:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>Preparare una macchina virtuale RHEL 7 da KVM

1. Scaricare l'immagine KVM hello RHEL 7 dal sito Web di hello Red Hat. Questa procedura utilizza RHEL 7 come esempio hello.

2. Impostare una password radice.

    Generare una password crittografata e copiare l'output di hello del comando hello:

        # openssl passwd -1 changeme

    Impostare una password radice con guestfish:

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Secondo campo hello modifica dell'utente radice da "." password crittografata toohello.

3. Creare una macchina virtuale KVM dall'immagine qcow2 hello. Impostare il tipo di disco hello troppo**qcow2**e impostare modello dispositivo dell'interfaccia di rete virtuale hello troppo**virtio**. Quindi, avviare la macchina virtuale hello e accedere come radice.

4. Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:

        # chkconfig network on

7. Registrare l'installazione di tooenable Red Hat sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo questa configurazione, aprire `/etc/default/grub` in un editor di testo e modifica hello `GRUB_CMDLINE_LINUX` parametro. ad esempio:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Questo comando assicura anche che tutti i messaggi della console sono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi. comando Hello disattiva anche hello nuove RHEL 7 convenzioni di denominazione per le schede NIC. Inoltre, è consigliabile rimuovere hello seguenti parametri:
   
        rhgb quiet crashkernel=auto
   
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale. È possibile lasciare hello `crashkernel` opzione configurato se si desidera. Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.

9. Dopo avere completato modifica `/etc/default/grub`eseguire hello seguenti comando toorebuild hello grub configurazione:

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Aggiungere i moduli Hyper-V in initramfs.

    Modificare `/etc/dracut.conf` e aggiungere il contenuto:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Ricompilare initramfs:

        # dracut -f -v

11. Disinstallare cloud-init:

        # yum remove cloud-init

12. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio:

        # systemctl enable sshd

    Modificare /etc/ssh/sshd_config tooinclude hello seguenti righe:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat. Abilitare repository extra hello eseguendo hello comando seguente:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Installare l'agente Linux di Azure hello eseguendo hello comando seguente:

        # yum install WALinuxAgent

    Abilitare il servizio waagent hello:

        # systemctl enable waagent.service

15. Non creare lo spazio di swapping sul disco del sistema operativo hello.

    Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure. Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning. Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in `/etc/waagent.conf` in modo appropriato:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Annullare la registrazione hello sottoscrizione (se necessario) eseguendo hello comando seguente:

        # subscription-manager unregister

17. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Spegnere la macchina virtuale hello KVM.

19. Convertire il formato VHD toohello di hello qcow2 immagine.

    Prima di convertire formato tooraw di hello immagine:

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Assicurarsi che le dimensioni di hello dell'immagine non elaborati di hello sono allineata con 1 MB. In caso contrario, l'arrotondamento per eccesso hello dimensioni tooalign con 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertire hello disco raw tooa dimensione fissa disco rigido virtuale:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>Preparare una macchina virtuale basata su Red Hat da VMware
### <a name="prerequisites"></a>Prerequisiti
In questa sezione si presuppone che una macchina virtuale RHEL sia già stata installata in VMware. Per informazioni dettagliate su come tooinstall un sistema operativo in VMware, vedere [Guida all'installazione di sistema operativo Guest VMware](http://partnerweb.vmware.com/GOSIG/home.html).

* Quando si installa hello del sistema operativo Linux, è consigliabile utilizzare partizioni standard anziché LVM, è spesso predefinito hello per numerose installazioni. Questo modo si evita i conflitti di nome LVM con macchina virtuale clonata, in particolare se un disco del sistema operativo necessaria macchina virtuale di tooanother toobe associata per la risoluzione dei problemi. Se si preferisce, su dischi di dati si può usare LVM o RAID.
* Non si configura una partizione di scambio su disco del sistema operativo hello. È possibile configurare hello Linux agente toocreate un file di swapping sul disco di risorse temporaneo hello. È possibile trovare ulteriori informazioni su questo nei passaggi hello che seguono.
* Quando si crea il disco rigido virtuale di hello, selezionare **disco virtuale di archivio come un singolo file**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>Preparare una macchina virtuale RHEL 6 da VMware
1. RHEL 6, NetworkManager può interferire con l'agente Linux di Azure hello. Disinstallazione di questo pacchetto eseguendo hello comando seguente:
   
        # sudo rpm -e --nodeps NetworkManager

2. Creare un file denominato **rete** hello /etc/hosts sysconfig/directory che contiene hello seguente testo:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Spostare o rimuovere hello udev regole tooavoid la generazione di regole statiche per l'interfaccia Ethernet hello. Le regole seguenti causano problemi quando si clona una macchina virtuale in Azure o Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:

        # sudo chkconfig network on

6. Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat. Abilitare repository extra hello eseguendo hello comando seguente:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo, aprire `/etc/default/grub` in un editor di testo e modifica hello `GRUB_CMDLINE_LINUX` parametro. ad esempio:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Questa operazione garantisce inoltre che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi. Inoltre, è consigliabile rimuovere hello seguenti parametri:
   
        rhgb quiet crashkernel=auto
   
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale. È possibile lasciare hello `crashkernel` opzione configurato se si desidera. Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.

9. Aggiungere tooinitramfs moduli Hyper-V:

    Modifica `/etc/dracut.conf`e aggiungere hello seguente contenuto:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Ricompilare initramfs:

        # dracut -f -v

10. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio, è in genere predefinito hello. Modificare `/etc/ssh/sshd_config` hello tooinclude seguente riga:

    ClientAliveInterval 180

11. Installare l'agente Linux di Azure hello eseguendo hello comando seguente:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Non creare lo spazio di swapping sul disco del sistema operativo hello.

    Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure. Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning. Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in `/etc/waagent.conf` in modo appropriato:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Annullare la registrazione hello sottoscrizione (se necessario) eseguendo hello comando seguente:

        # sudo subscription-manager unregister

14. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Spegnere la macchina virtuale hello e convertire i file con estensione vhd tooa file VMDK hello.

    Prima di convertire formato tooraw di hello immagine:

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Assicurarsi che le dimensioni di hello dell'immagine non elaborati di hello sono allineata con 1 MB. In caso contrario, l'arrotondamento per eccesso hello dimensioni tooalign con 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertire hello disco raw tooa dimensione fissa disco rigido virtuale:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>Preparare una macchina virtuale RHEL 7 da VMware
1. Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:

        # sudo chkconfig network on

4. Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure. toodo questa modifica, aprirla `/etc/default/grub` in un editor di testo e modifica hello `GRUB_CMDLINE_LINUX` parametro. ad esempio:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Questa configurazione assicura anche che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi. Disattiva anche hello nuove RHEL 7 convenzioni di denominazione per le schede NIC. Inoltre, è consigliabile rimuovere hello seguenti parametri:
   
        rhgb quiet crashkernel=auto
   
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale. È possibile lasciare hello `crashkernel` opzione configurato se si desidera. Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.

6. Dopo avere completato modifica `/etc/default/grub`eseguire hello seguenti comando toorebuild hello grub configurazione:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Aggiungere tooinitramfs moduli Hyper-V.

    Modificare `/etc/dracut.conf`e aggiungere il contenuto:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Ricompilare initramfs:

        # dracut -f -v

8. Verificare che server SSH hello sia installato e configurato toostart in fase di avvio. Questa impostazione viene in genere predefinito hello. Modificare `/etc/ssh/sshd_config` hello tooinclude seguente riga:

        ClientAliveInterval 180

9. pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat. Abilitare repository extra hello eseguendo hello comando seguente:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Installare l'agente Linux di Azure hello eseguendo hello comando seguente:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Non creare lo spazio di swapping sul disco del sistema operativo hello.

    Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure. Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning. Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in `/etc/waagent.conf` in modo appropriato:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Se si desidera che toounregister hello sottoscrizione, eseguire hello comando seguente:

        # sudo subscription-manager unregister

13. Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Spegnere la macchina virtuale hello e convertire il formato VHD toohello di hello VMDK file.

    Prima di convertire formato tooraw di hello immagine:

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Assicurarsi che le dimensioni di hello dell'immagine non elaborati di hello sono allineata con 1 MB. In caso contrario, l'arrotondamento per eccesso hello dimensioni tooalign con 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertire hello disco raw tooa dimensione fissa disco rigido virtuale:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Preparare una macchina virtuale basata su Red Hat da un'immagine ISO usando un file kickstart automatico
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Preparare una macchina virtuale RHEL 7 da un file kickstart

1.  Creare un file di sviluppare un che include hello dopo contenuto e salvare file hello. Per informazioni dettagliate sull'installazione di sviluppare un, vedere hello [Guida all'installazione di sviluppare un](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. Posizionare i file di sviluppare un hello in sistema installazione hello può accedervi.

3. Creare una nuova macchina virtuale nella console di gestione di Hyper-V. In hello **connessione disco rigido virtuale** selezionare **collegare un disco rigido virtuale in un secondo momento**e hello Completamento creazione guidata macchina virtuale.

4. Aprire impostazioni della macchina virtuale hello:

    a.  Collegare una nuova macchina virtuale toohello di disco rigido virtuale. Verificare che tooselect **formato VHD** e **a dimensione fissa**.

    b.  Collegare installazione hello unità DVD toohello ISO.

    c.  Impostare hello BIOS tooboot dal CD-ROM.

5. Avviare la macchina virtuale hello. Quando viene visualizzata la Guida all'installazione hello, premere **scheda** tooconfigure opzioni di avvio hello.

6. Invio `inst.ks=<hello location of hello kickstart file>` alla fine di hello delle opzioni di avvio hello e premere **invio**.

7. Attendere toofinish installazione hello. Al termine, macchina virtuale hello verrà chiuso automaticamente. Il VHD Linux è ora pronto toobe caricato tooAzure.

## <a name="known-issues"></a>Problemi noti
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>driver di Hyper-V Hello potrebbero non essere incluse nel disco RAM iniziale hello quando si utilizza un hypervisor non Hyper-V

In alcuni casi, i programmi di installazione di Linux potrebbero non includere i driver di hello per Hyper-V in hello iniziale disco RAM (initrd o initramfs), a meno che Linux rileva che è in esecuzione in un ambiente Hyper-V.

Quando si utilizza un tooprepare di sistema (ovvero, Virtualbox, Xen e così via) di virtualizzazione diverso immagine Linux, potrebbe essere necessario toorebuild initrd tooensure che almeno hello hv_vmbus e sono disponibili su disco RAM iniziale hello hv_storvsc kernel moduli. Questo è un problema noto almeno nei sistemi basati su distribuzione Red Hat upstream hello.

tooresolve questo problema, aggiungere tooinitramfs moduli Hyper-V e ricompilarlo:

Modifica `/etc/dracut.conf`e aggiungere hello seguente contenuto:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Ricompilare initramfs:

        # dracut -f -v

Per ulteriori informazioni, vedere informazioni hello sul [ricompilazione initramfs](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Passaggi successivi
Si è ora pronto toouse Red Hat Enterprise Linux disco rigido virtuale toocreate nuove macchine virtuali in Azure. Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Per ulteriori dettagli su hypervisor hello che sono certificate toorun Red Hat Enterprise Linux, vedere [sito Web di Red Hat hello](https://access.redhat.com/certified-hypervisors).
