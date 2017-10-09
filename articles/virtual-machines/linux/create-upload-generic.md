---
title: aaaCreate e caricamento di un VHD Linux in Azure
description: Informazioni su toocreate e caricare un Azure disco rigido virtuale (VHD) che contiene un sistema operativo Linux.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>Informazioni per le distribuzioni non approvate
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

contratto di servizio di piattaforma Azure Hello applica toovirtual computer hello del sistema operativo Linux solo quando uno di hello [approvate per le distribuzioni](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) viene utilizzato. Tutte le distribuzioni di Linux che vengono fornite in hello Azure raccolta immagini sono approvate per le distribuzioni con la configurazione richiesta hello.

* [Linux in Azure - Distribuzioni supportate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Supporto delle immagini Linux in Microsoft Azure](https://support.microsoft.com/kb/2941892)

Tutte le distribuzioni in esecuzione in Azure saranno necessario un numero di prerequisiti toohave tooproperly una possibilità eseguire sulla piattaforma hello toomeet.  In questo articolo non è completo come ogni distribuzione è diverso. ed è molto probabile che anche se vengono soddisfatti tutti hello i seguenti criteri che dovranno comunque toosignificantly modificare il tooensure sistema Linux che viene eseguito correttamente sulla piattaforma hello.

Per questo motivo, è consigliabile iniziare, laddove possibile, con una delle [distribuzioni approvate di Linux su Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) . Hello articoli seguenti guiderà come tooprepare hello vari approvate per distribuzioni di Linux che sono supportate in Azure:

* **[Distribuzioni basate su CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES e openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

rest Hello di questo articolo verranno evidenziate le indicazioni generali per eseguire la distribuzione di Linux in Azure.

## <a name="general-linux-installation-notes"></a>Note generali sull'installazione di Linux
* formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.  È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd. Se si utilizza VirtualBox ciò significa che la selezione di **dimensioni fisse** come anziché predefinito toohello allocata in modo dinamico durante la creazione del disco hello.
* Azure supporta solo macchine virtuali di generazione 1. È possibile convertire una generazione 1 macchina virtuale dal formato del file disco rigido virtuale VHDX toohello e da tooa fissata a espansione dinamica dimensioni su disco. Tuttavia non è possibile modificare la generazione di una macchina virtuale. Per ulteriori informazioni, vedere [Creare una macchina virtuale di prima o seconda generazione in Hyper-V](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* dimensione massima di Hello consentite per hello che VHD è 1023 GB.
* Quando si installa il sistema di Linux hello è *consigliato* utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni). Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un disco del sistema operativo necessaria tooanother toobe collegato identici macchina virtuale per la risoluzione dei problemi. È possibile usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) su dischi di dati.
* Per l'installazione di file system UDF è necessario il supporto di kernel. Al primo avvio del hello Azure configurazione provisioning viene passato toohello VM Linux tramite supporti formattati funzione definita dall'utente che sono collegato toohello guest. l'agente Linux di Azure Hello deve essere in grado di toomount hello UDF file system tooread la configurazione e provisioning hello macchina virtuale.
* Le versioni di kernel Linux inferiori a 2.6.37 non supportano NUMA su Hyper-V con macchine virtuali di dimensioni maggiori. Questo problema principalmente impatti distribuzioni precedenti utilizzando hello monte kernel Red Hat 2.6.32 ed è stato corretto in RHEL 6.6 (kernel-2.6.32-504). I sistemi che eseguono personalizzato kernel meno recente 2.6.37 o basato su RHEL kernel precedenti rispetto a 2.6.32-504 è necessario impostare il parametro di avvio di hello `numa=off` sul kernel hello in grub.conf della riga di comando. Per altre informazioni, vedere l'articolo Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Non si configura una partizione di scambio su disco del sistema operativo hello. agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.  Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.
* Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.

### <a name="installing-kernel-modules-without-hyper-v"></a>Installazione dei moduli kernel senza Hyper-V
Azure viene eseguito nell'hypervisor Hyper-V hello, in modo Linux è necessario che alcuni moduli kernel siano installati in ordine toorun in Azure. Se si dispone di una macchina virtuale che è stata creata all'esterno di Hyper-V, i programmi di installazione di hello Linux non può includere i driver di hello per Hyper-V in hello ramdisk iniziale (initrd o initramfs) a meno che non viene rilevato che è in esecuzione un un ambiente Hyper-V. Quando si utilizza un tooprepare di sistema (ad esempio Virtualbox, KVM, e così via) di virtualizzazione diverso come immagine Linux, potrebbe essere necessario toorebuild hello initrd tooensure che almeno hello `hv_vmbus` e `hv_storvsc` sono disponibili su ramdisk iniziale hello moduli del kernel.  Questo è un problema noto almeno sui sistemi basati su distribuzione Red Hat upstream hello.

il meccanismo di Hello per la ricompilazione hello initrd initramfs l'immagine o può variare a seconda della distribuzione di hello. Consultare la documentazione della distribuzione o il supporto per la procedura appropriata hello.  Ecco un esempio per come toorebuild hello initrd utilizzando hello `mkinitrd` utilità:

Per eseguire il backup immagine initrd esistente hello:

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

Successivamente, ricompilare initrd hello con hello `hv_vmbus` e `hv_storvsc` moduli kernel:

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>Ridimensionamento dei dischi rigidi virtuali
Immagini del disco rigido virtuale in Azure devono avere un too1MB dimensioni virtuali allineata.  Solitamente, i VHD creati usando Hyper-V sono già allineati correttamente.  Se hello disco rigido virtuale non è allineato correttamente, quindi è possibile che venga visualizzato un errore messaggio simili toohello seguenti quando si tenta di toocreate un *immagine* dal disco rigido virtuale:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy questo è possibile ridimensionare hello VM utilizzando la console di gestione di Hyper-V di hello o hello [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) cmdlet di Powershell.  Se non si esegue in un ambiente Windows è consigliabile toouse qemu img tooconvert (se necessario) e ridimensionare hello disco rigido virtuale.

> [!NOTE]
> Esiste un bug noto nelle versioni qemu-img > = 2.2.1 risultante in un disco rigido virtuale non formattato correttamente. problema di Hello è stato risolto in QEMU 2.6. È consigliabile toouse qemu-img 2.2.0 o inferiore o aggiornamento too2.6 o versione successiva. Riferimento: https://bugs.launchpad.net/qemu/+bug/1490611.
> 
> 

1. Ridimensionamento hello VHD direttamente tramite strumenti come `qemu-img` o `vbox-manage` può comportare un disco rigido virtuale di avvio.  È consigliabile toofirst convert hello immagine del disco rigido virtuale tooa disco non ELABORATO.  Se l'immagine di macchina virtuale hello è già stato creato come immagine del disco non ELABORATO (impostazione predefinita hello per alcuni hypervisor, ad esempio KVM) è possibile saltare questo passaggio:
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Calcolare hello richiesto pari a tooensure di immagine disco hello che hello dimensioni virtuali too1MB allineati.  con questo consentono di Hello seguente script della shell bash.  utilizza script Hello "`qemu-img info`" toodetermine hello virtuale dimensioni dell'immagine disco hello e quindi Calcola hello dimensioni toohello avanti 1 MB:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. Ridimensionamento del disco non elaborato di hello utilizzando $rounded_size come set di hello sopra script:
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. A questo punto, convertire hello disco RAW indietro tooa disco rigido virtuale a dimensione fissa:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   Oppure, con versione qemu **2.6 +** includono hello `force_size` opzione:

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Requisiti del kernel Linux
Hello driver Linux Integration Services (LIS) per Hyper-V e Azure vengono forniti toohello direttamente a monte kernel di Linux. Per molte distribuzioni che includono una versione recente del kernel Linux (cioè 3.x) questi driver sono già disponibili; in alternativa, fornire versioni backport dei driver con i relativi kernel.  Questi driver vengono continuamente aggiornati nel kernel di upstream hello con nuove correzioni e funzionalità, quando possibile è consigliabile toorun un [approvate distribuzione](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) che includerà le correzioni e gli aggiornamenti.

Se si utilizza una variante di Red Hat Enterprise Linux versioni **6.0-6.3**, sarà necessario tooinstall hello LIS driver per Hyper-V. sono disponibili driver Hello [in questa posizione](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409). A partire da RHEL **6.4 +** (e derivati) driver LIS hello sono già inclusi in kernel hello e pertanto non sono pacchetti di installazione aggiuntive sono necessarie toorun tali sistemi in Azure.

Se un kernel personalizzato è necessario, è consigliabile toouse una versione più recente di kernel (ad esempio **3.8 +**). Per tali distribuzioni o i fornitori che gestiscono le proprie kernel, alcune attività sarà obbligatorio tooregularly backport hello LIS driver dal kernel di hello kernel upstream tooyour personalizzato.  Anche se già in esecuzione una versione del kernel relativamente più recenti, è consigliabile tookeep tenere traccia di qualsiasi a monte correzioni in backport e i driver LIS hello quelli in base alle esigenze. percorso di Hello dei file di origine di hello LIS driver è disponibile in hello [gestori](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) file nell'albero di origine kernel Linux hello:

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

Nel caso minimo, assenza hello di hello seguenti patch è noto toocause problemi in Azure e così queste deve essere incluso nel kernel di hello. L'elenco non è esaustivo o completo per tutte le distribuzioni:

* [ata_piix: rinviare i driver di dischi toohello Hyper-V per impostazione predefinita](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc: Account per i pacchetti in transito nel percorso di ripristino hello](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc: avoid usage of WRITE_SAME](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc: Disable WRITE SAME for RAID and virtual host adapter drivers](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc: NULL pointer dereference fix](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc: ring buffer failures may result in I/O freeze](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs: protect against double execution of __scsi_remove_device](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>Hello agente Linux di Azure
Hello [agente Linux di Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) è necessario tooproperly effettuare il provisioning di una macchina virtuale di Linux in Azure. È possibile ottenere la versione più recente di hello, file problemi o inviare richieste pull in hello [repository GitHub agente Linux](https://github.com/Azure/WALinuxAgent).

* agente Linux di Hello viene rilasciato con licenza di Apache 2.0 hello. Molte distribuzioni già forniscono RPM o deb pacchetti per hello agente e pertanto in alcuni casi si possono essere installato e aggiornato con un minimo sforzo.
* Hello agente Linux di Azure richiede Python versione 2.6 +.
* l'agente Hello richiede anche il modulo di python pyasn1 hello. che nella maggior parte delle distribuzioni viene fornito come pacchetto separato installabile.
* In alcuni casi potrebbe non essere compatibile con NetworkManager hello agente Linux di Azure. Molti dei pacchetti RPM o Deb hello forniti da distribuzioni configurare NetworkManager come pacchetto waagent toohello conflitto e pertanto verrà disinstallato NetworkManager quando si installa pacchetto dell'agente Linux di hello.

## <a name="general-linux-system-requirements"></a>Requisiti generali di sistema relativi a Linux

* Modifica linea di avvio di kernel hello in GRUB o GRUB2 hello tooinclude seguenti parametri. In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi:
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.
  
    Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri se esistono:
  
        rhgb quiet crashkernel=auto
  
    Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale. Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.

* L'installazione di hello agente Linux di Azure
  
    Hello agente Linux di Azure è necessaria per il provisioning di un'immagine Linux in Azure.  Molte distribuzioni forniscono agente hello come un pacchetto RPM o Deb (pacchetto hello viene in genere chiamato 'WALinuxAgent' o 'walinuxagent').  Hello agente può anche essere installato manualmente seguendo procedure hello hello [Guida agente Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

* Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.  Si tratta in genere predefinito hello.

* Non creare lo spazio di swapping sul disco del sistema operativo hello
  
    Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure. Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning. Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* Come passaggio finale, eseguire hello macchina virtuale di hello toodeprovision i comandi seguenti:
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > In Virtualbox venga visualizzato il seguente errore dopo l'esecuzione di hello ' waagent-force - deprovisioning ': `[Errno 5] Input/output error`. Questo messaggio di errore non è critico e può essere ignorato.
  > 
  > 

* Sarà quindi anche necessario tooshut verso il basso macchina virtuale hello e caricare hello tooAzure di disco rigido virtuale.

