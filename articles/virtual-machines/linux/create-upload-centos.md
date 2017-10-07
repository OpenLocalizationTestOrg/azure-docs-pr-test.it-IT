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
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="81f8e-103">Preparare una macchina virtuale basata su CentOS per Azure</span><span class="sxs-lookup"><span data-stu-id="81f8e-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="81f8e-104">Preparare una macchina virtuale CentOS 6.x per Azure</span><span class="sxs-lookup"><span data-stu-id="81f8e-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="81f8e-105">Preparare una macchina virtuale CentOS 7.0+ per Azure</span><span class="sxs-lookup"><span data-stu-id="81f8e-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="81f8e-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="81f8e-106">Prerequisites</span></span>
<span data-ttu-id="81f8e-107">Questo articolo si presuppone di aver già installato un CentOS (o simile derivato) il disco rigido virtuale di Linux del sistema operativo tooa.</span><span class="sxs-lookup"><span data-stu-id="81f8e-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="81f8e-108">Più strumenti esistono toocreate file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="81f8e-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="81f8e-109">Per istruzioni, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="81f8e-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="81f8e-110">**Note sull'installazione di CentOS**</span><span class="sxs-lookup"><span data-stu-id="81f8e-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="81f8e-111">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="81f8e-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="81f8e-112">formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.</span><span class="sxs-lookup"><span data-stu-id="81f8e-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="81f8e-113">È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="81f8e-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="81f8e-114">Se si utilizza VirtualBox ciò significa che la selezione di **dimensioni fisse** come anziché predefinito toohello allocata in modo dinamico durante la creazione del disco hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="81f8e-115">Quando si installa il sistema di Linux hello è *consigliato* utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni).</span><span class="sxs-lookup"><span data-stu-id="81f8e-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="81f8e-116">Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un disco del sistema operativo necessaria tooanother toobe collegato identici macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="81f8e-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="81f8e-117">È possibile usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) su dischi di dati.</span><span class="sxs-lookup"><span data-stu-id="81f8e-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="81f8e-118">Per l'installazione di file system UDF è necessario il supporto di kernel.</span><span class="sxs-lookup"><span data-stu-id="81f8e-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="81f8e-119">Al primo avvio del hello Azure configurazione provisioning viene passato toohello VM Linux tramite supporti formattati funzione definita dall'utente che sono collegato toohello guest.</span><span class="sxs-lookup"><span data-stu-id="81f8e-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="81f8e-120">l'agente Linux di Azure Hello deve essere in grado di toomount hello UDF file system tooread la configurazione e provisioning hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81f8e-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="81f8e-121">Le versioni di kernel Linux inferiori a 2.6.37 non supportano NUMA su Hyper-V con macchine virtuali di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="81f8e-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="81f8e-122">Questo problema principalmente impatti distribuzioni precedenti utilizzando hello monte kernel Red Hat 2.6.32 ed è stato corretto in RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="81f8e-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="81f8e-123">I sistemi che eseguono personalizzato kernel meno recente 2.6.37 o basato su RHEL kernel precedenti rispetto a 2.6.32-504 è necessario impostare il parametro di avvio di hello `numa=off` sul kernel hello in grub.conf della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="81f8e-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="81f8e-124">Per altre informazioni, vedere l'articolo Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="81f8e-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="81f8e-125">Non si configura una partizione di scambio su disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="81f8e-126">agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="81f8e-127">Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="81f8e-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="81f8e-128">Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="81f8e-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="81f8e-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="81f8e-129">CentOS 6.x</span></span>

1. <span data-ttu-id="81f8e-130">Nella console di gestione Hyper-V selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="81f8e-131">Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="81f8e-132">CentOS 6, NetworkManager può interferire con l'agente Linux di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="81f8e-133">Disinstallazione di questo pacchetto eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="81f8e-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="81f8e-134">Creare o modificare file hello `/etc/sysconfig/network` e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="81f8e-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="81f8e-135">Creare o modificare file hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="81f8e-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="81f8e-136">Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet.</span><span class="sxs-lookup"><span data-stu-id="81f8e-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="81f8e-137">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="81f8e-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="81f8e-138">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="81f8e-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="81f8e-139">Se si desidera mirror di OpenLogic hello toouse ospitati all'interno di hello Data Center di Azure, quindi sostituire hello `/etc/yum.repos.d/CentOS-Base.repo` file con hello seguenti repository.</span><span class="sxs-lookup"><span data-stu-id="81f8e-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="81f8e-140">Verrà anche aggiunta hello **[openlogic]** repository che include i pacchetti aggiuntivi, ad esempio l'agente Linux di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="81f8e-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

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
    <span data-ttu-id="81f8e-141">Hello resto di questa Guida verrà si presuppone l'uso almeno hello `[openlogic]` repository, che sarà utilizzato tooinstall agente Linux di Azure di hello indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="81f8e-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="81f8e-142">Aggiungere hello too/etc/yum.conf riga seguente:</span><span class="sxs-lookup"><span data-stu-id="81f8e-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="81f8e-143">Eseguire hello successivo comando tooclear hello yum metadati e aggiornamento hello sistema corrente con i pacchetti hello più recenti:</span><span class="sxs-lookup"><span data-stu-id="81f8e-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="81f8e-144">A meno che non si sta creando un'immagine per una versione precedente di CentOS, è consigliabile tooupdate che tutti hello pacchetti toohello più recente:</span><span class="sxs-lookup"><span data-stu-id="81f8e-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="81f8e-145">Dopo l'esecuzione di questo comando potrebbe essere necessario un riavvio.</span><span class="sxs-lookup"><span data-stu-id="81f8e-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="81f8e-146">(Facoltativo) Installare i driver di hello per hello Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="81f8e-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="81f8e-147">passaggio di Hello è **obbligatorio** per CentOS 6.3 e facoltativo per le versioni successive e precedenti.</span><span class="sxs-lookup"><span data-stu-id="81f8e-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="81f8e-148">In alternativa, è possibile seguire le istruzioni di installazione manuale di hello in hello [pagina di download LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81f8e-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="81f8e-149">Installare hello agente Linux di Azure e le dipendenze:</span><span class="sxs-lookup"><span data-stu-id="81f8e-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="81f8e-150">pacchetto WALinuxAgent Hello rimuoverà hello NetworkManager e pacchetti NetworkManager gnome se non sono stati già rimossi come descritto nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="81f8e-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="81f8e-151">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="81f8e-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="81f8e-152">toodo, aprire `/boot/grub/menu.lst` in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="81f8e-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="81f8e-153">In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="81f8e-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="81f8e-154">Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="81f8e-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="81f8e-155">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="81f8e-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="81f8e-156">Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="81f8e-157">CentOS versione 6.5 e versioni precedenti è necessario impostare anche il parametro kernel hello `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="81f8e-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="81f8e-158">Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="81f8e-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="81f8e-159">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="81f8e-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="81f8e-160">Si tratta in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-160">This is usually hello default.</span></span>

15. <span data-ttu-id="81f8e-161">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="81f8e-162">Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="81f8e-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="81f8e-163">Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="81f8e-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="81f8e-164">Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare i seguenti parametri in hello `/etc/waagent.conf` in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="81f8e-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="81f8e-165">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="81f8e-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="81f8e-166">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="81f8e-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="81f8e-167">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="81f8e-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="81f8e-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="81f8e-168">CentOS 7.0+</span></span>
<span data-ttu-id="81f8e-169">**Modifiche in CentOS 7 (e sistemi derivati simili)**</span><span class="sxs-lookup"><span data-stu-id="81f8e-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="81f8e-170">Preparazione di una macchina virtuale CentOS 7 per Azure è molto simile tooCentOS 6, esistono tuttavia alcune differenze importanti non degni di nota:</span><span class="sxs-lookup"><span data-stu-id="81f8e-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="81f8e-171">Hello NetworkManager del pacchetto non è in conflitto con l'agente Linux di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="81f8e-172">Questo pacchetto viene installato per impostazione predefinita ed è consigliabile non rimuoverlo.</span><span class="sxs-lookup"><span data-stu-id="81f8e-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="81f8e-173">GRUB2 viene utilizzato come hello del caricatore di avvio predefinito, in modo procedure hello per la modifica di parametri del kernel è stato modificato (vedere sotto).</span><span class="sxs-lookup"><span data-stu-id="81f8e-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="81f8e-174">XFS è file system predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-174">XFS is now hello default file system.</span></span> <span data-ttu-id="81f8e-175">Hello ext4 file sistema può comunque essere utilizzato se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="81f8e-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="81f8e-176">**Procedura di configurazione**</span><span class="sxs-lookup"><span data-stu-id="81f8e-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="81f8e-177">Nella console di gestione Hyper-V selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="81f8e-178">Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="81f8e-179">Creare o modificare file hello `/etc/sysconfig/network` e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="81f8e-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="81f8e-180">Creare o modificare file hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="81f8e-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="81f8e-181">Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet.</span><span class="sxs-lookup"><span data-stu-id="81f8e-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="81f8e-182">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="81f8e-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="81f8e-183">Se si desidera mirror di OpenLogic hello toouse ospitati all'interno di hello Data Center di Azure, quindi sostituire hello `/etc/yum.repos.d/CentOS-Base.repo` file con hello seguenti repository.</span><span class="sxs-lookup"><span data-stu-id="81f8e-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="81f8e-184">Verrà anche aggiunta hello **[openlogic]** repository che include i pacchetti per l'agente Linux di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="81f8e-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="81f8e-185">Hello resto di questa Guida verrà si presuppone l'uso almeno hello `[openlogic]` repository, che sarà utilizzato tooinstall agente Linux di Azure di hello indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="81f8e-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="81f8e-186">Eseguire hello successivo comando tooclear hello corrente yum metadati e installare eventuali aggiornamenti:</span><span class="sxs-lookup"><span data-stu-id="81f8e-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="81f8e-187">A meno che non si sta creando un'immagine per una versione precedente di CentOS, è consigliabile tooupdate che tutti hello pacchetti toohello più recente:</span><span class="sxs-lookup"><span data-stu-id="81f8e-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="81f8e-188">Dopo l'esecuzione di questo comando potrebbe essere necessario un riavvio.</span><span class="sxs-lookup"><span data-stu-id="81f8e-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="81f8e-189">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="81f8e-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="81f8e-190">toodo, aprire `/etc/default/grub` in hello di editor e modificare un testo `GRUB_CMDLINE_LINUX` parametro, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="81f8e-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="81f8e-191">In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="81f8e-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="81f8e-192">Disattiva anche hello nuove CentOS 7 convenzioni di denominazione per le schede NIC.</span><span class="sxs-lookup"><span data-stu-id="81f8e-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="81f8e-193">Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="81f8e-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="81f8e-194">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="81f8e-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="81f8e-195">Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="81f8e-196">Dopo aver eseguito modifica `/etc/default/grub` al precedente, eseguire hello seguente comando toorebuild hello grub configurazione:</span><span class="sxs-lookup"><span data-stu-id="81f8e-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="81f8e-197">Se la creazione di immagine hello da **VMWare, VirtualBox o KVM:** driver di hello Hyper-V verificare sono inclusi in initramfs hello:</span><span class="sxs-lookup"><span data-stu-id="81f8e-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="81f8e-198">Modificare `/etc/dracut.conf`e aggiungere il contenuto:</span><span class="sxs-lookup"><span data-stu-id="81f8e-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="81f8e-199">Ricompilare initramfs hello:</span><span class="sxs-lookup"><span data-stu-id="81f8e-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="81f8e-200">Installare hello agente Linux di Azure e le dipendenze:</span><span class="sxs-lookup"><span data-stu-id="81f8e-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="81f8e-201">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="81f8e-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="81f8e-202">Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="81f8e-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="81f8e-203">Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="81f8e-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="81f8e-204">Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare i seguenti parametri in hello `/etc/waagent.conf` in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="81f8e-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="81f8e-205">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="81f8e-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="81f8e-206">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="81f8e-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="81f8e-207">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="81f8e-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81f8e-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81f8e-208">Next steps</span></span>
<span data-ttu-id="81f8e-209">Si è ora pronto toouse Linux CentOS disco rigido virtuale toocreate nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="81f8e-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="81f8e-210">Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="81f8e-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

