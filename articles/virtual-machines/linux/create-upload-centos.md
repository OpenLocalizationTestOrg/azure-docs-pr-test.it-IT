---
title: Creare e caricare un VHD Linux basato su CentOS in Azure
description: Come creare e caricare un disco rigido virtuale Azure (VHD) che contiene un sistema operativo Linux basato su CentOS.
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
ms.openlocfilehash: 010f4b05b35fa1f31c14f34a5fae9298fcd831e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="cee62-103">Preparare una macchina virtuale basata su CentOS per Azure</span><span class="sxs-lookup"><span data-stu-id="cee62-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="cee62-104">Preparare una macchina virtuale CentOS 6.x per Azure</span><span class="sxs-lookup"><span data-stu-id="cee62-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="cee62-105">Preparare una macchina virtuale CentOS 7.0+ per Azure</span><span class="sxs-lookup"><span data-stu-id="cee62-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="cee62-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cee62-106">Prerequisites</span></span>
<span data-ttu-id="cee62-107">In questo articolo si presuppone che l'utente abbia già installato un sistema operativo Linux CentOS (o un sistema derivato simile) in un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="cee62-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="cee62-108">Sono disponibili vari strumenti per creare file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cee62-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="cee62-109">Per istruzioni, vedere [Installare il ruolo Hyper-V e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="cee62-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="cee62-110">**Note sull'installazione di CentOS**</span><span class="sxs-lookup"><span data-stu-id="cee62-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="cee62-111">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="cee62-112">Il formato VHDX non è supportato in Azure, solo nei **VHD fissi**.</span><span class="sxs-lookup"><span data-stu-id="cee62-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="cee62-113">È possibile convertire il disco in formato VHD tramite la console di gestione di Hyper-V o il cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="cee62-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="cee62-114">Se si usa VirtualBox, ciò significa che è stato selezionato **Dimensioni fisse** anziché il valore predefinito allocato in modo dinamico durante la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="cee62-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="cee62-115">Durante l'installazione del sistema Linux è *consigliabile* usare partizioni standard anziché LVM, spesso la scelta predefinita per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="cee62-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="cee62-116">In questo modo sarà possibile evitare conflitti di nome LVM con le macchine virtuali clonate, in particolare se fosse necessario collegare un disco del sistema operativo a un'altra macchina virtuale identica per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="cee62-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="cee62-117">È possibile usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) su dischi di dati.</span><span class="sxs-lookup"><span data-stu-id="cee62-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="cee62-118">Per l'installazione di file system UDF è necessario il supporto di kernel.</span><span class="sxs-lookup"><span data-stu-id="cee62-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="cee62-119">Al primo avvio in Azure la configurazione del provisioning viene passata alla macchina virtuale Linux tramite supporti di memorizzazione formattati con UDF, collegati al guest.</span><span class="sxs-lookup"><span data-stu-id="cee62-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="cee62-120">È necessario che l'agente Linux di Azure possa montare il file system UDF per leggere la relativa configurazione ed eseguire il provisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cee62-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="cee62-121">Le versioni di kernel Linux inferiori a 2.6.37 non supportano NUMA su Hyper-V con macchine virtuali di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="cee62-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="cee62-122">Questo problema incide principalmente sulle distribuzioni precedenti che usavano il kernel upstream Red Hat 2.6.32. Il problema è stato risolto in RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="cee62-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="cee62-123">I sistemi che eseguono kernel personalizzati con versione precedente alla versione 2.6.37 o kernel basati su RHEL con versione precedente alla versione 2.6.32-504 devono impostare il parametro di avvio `numa=off` nella riga di comando del kernel in rub.conf.</span><span class="sxs-lookup"><span data-stu-id="cee62-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="cee62-124">Per altre informazioni, vedere l'articolo Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="cee62-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="cee62-125">Non configurare una partizione swap nel disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="cee62-125">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="cee62-126">L'agente Linux può essere configurato in modo da creare un file swap sul disco temporaneo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="cee62-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="cee62-127">Altre informazioni su questo argomento sono disponibili nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="cee62-127">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="cee62-128">Tutti i dischi rigidi virtuali devono avere dimensioni multiple di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="cee62-128">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="cee62-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="cee62-129">CentOS 6.x</span></span>

1. <span data-ttu-id="cee62-130">Nella console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cee62-130">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="cee62-131">Fare clic su **Connetti** per aprire una finestra della console per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cee62-131">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="cee62-132">In CentOS 6, NetworkManager può interferire con l'agente Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="cee62-133">Disinstallare il pacchetto eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="cee62-133">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="cee62-134">Creare o modificare il file `/etc/sysconfig/network` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="cee62-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="cee62-135">Creare o modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="cee62-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="cee62-136">Modificare le regole udev per evitare la generazione di regole statiche per l'interfaccia Ethernet.</span><span class="sxs-lookup"><span data-stu-id="cee62-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="cee62-137">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="cee62-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="cee62-138">Assicurarsi che il servizio di rete venga eseguito all'avvio eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cee62-138">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="cee62-139">Se si vogliono usare i mirror OpenLogic ospitati nei data center di Azure, sostituire il file `/etc/yum.repos.d/CentOS-Base.repo` con i repository seguenti.</span><span class="sxs-lookup"><span data-stu-id="cee62-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="cee62-140">Verrà così aggiunto anche il repository **[openlogic]** che include pacchetti aggiuntivi come l'agente Linux di Azure:</span><span class="sxs-lookup"><span data-stu-id="cee62-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span></span>

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
    <span data-ttu-id="cee62-141">La parte restante di questa guida presuppone che l'utente usi almeno il repository `[openlogic]`, con cui verrà installato l'agente Linux di Azure illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cee62-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>


9. <span data-ttu-id="cee62-142">Aggiungere la seguente riga a /etc/yum.conf:</span><span class="sxs-lookup"><span data-stu-id="cee62-142">Add the following line to /etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="cee62-143">Eseguire questo comando per cancellare i metadati yum correnti e aggiornare il sistema con i pacchetti più recenti:</span><span class="sxs-lookup"><span data-stu-id="cee62-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="cee62-144">A meno che non si crei un'immagine per una versione precedente di CentOS, è consigliabile aggiornare tutti i pacchetti all'ultima versione:</span><span class="sxs-lookup"><span data-stu-id="cee62-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="cee62-145">Dopo l'esecuzione di questo comando potrebbe essere necessario un riavvio.</span><span class="sxs-lookup"><span data-stu-id="cee62-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="cee62-146">(Facoltativo) Installare i driver per Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="cee62-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="cee62-147">Questo passaggio è **obbligatorio** per CentOS 6.3 e le versioni precedenti e facoltativo per le versioni successive.</span><span class="sxs-lookup"><span data-stu-id="cee62-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="cee62-148">In alternativa, seguire le istruzioni per l'installazione manuale disponibili nella [pagina di download di LIS](https://go.microsoft.com/fwlink/?linkid=403033) per installare RPM nella VM.</span><span class="sxs-lookup"><span data-stu-id="cee62-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span></span>
 
12. <span data-ttu-id="cee62-149">Installare l'agente Linux di Azure e le dipendenze:</span><span class="sxs-lookup"><span data-stu-id="cee62-149">Install the Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="cee62-150">Il pacchetto WALinuxAgent rimuoverà i pacchetti NetworkManager e NetworkManager-gnome, se non sono già stati rimossi come descritto nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="cee62-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="cee62-151">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="cee62-152">A questo scopo, aprire `/boot/grub/menu.lst` in un editor di testo e verificare che il kernel predefinito includa i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="cee62-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="cee62-153">In questo modo si garantisce inoltre che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="cee62-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="cee62-154">Inoltre, è consigliabile *rimuovere* i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="cee62-154">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="cee62-155">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="cee62-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="cee62-156">L'opzione `crashkernel` può essere configurata, ma si tenga presente che questo parametro ridurrà la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB, il che potrebbe causare problemi con le macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="cee62-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="cee62-157">Per CentOS 6.5 e le versioni precedenti deve essere impostato anche il parametro del kernel `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="cee62-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span></span> <span data-ttu-id="cee62-158">Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="cee62-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="cee62-159">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="cee62-159">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="cee62-160">Questo è in genere il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="cee62-160">This is usually the default.</span></span>

15. <span data-ttu-id="cee62-161">Non creare l'area di swap sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="cee62-161">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="cee62-162">L'agente Linux di Azure può configurare automaticamente l'area di swap utilizzando il disco risorse locale collegato alla VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="cee62-163">Si noti che il disco risorse locale è un disco *temporaneo* e potrebbe essere svuotato in seguito al deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cee62-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="cee62-164">Dopo aver installato l'agente Linux di Azure come illustrato nel passaggio precedente, modificare i seguenti parametri di `/etc/waagent.conf` in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="cee62-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="cee62-165">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="cee62-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="cee62-166">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cee62-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="cee62-167">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="cee62-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="cee62-168">CentOS 7.0+</span></span>
<span data-ttu-id="cee62-169">**Modifiche in CentOS 7 (e sistemi derivati simili)**</span><span class="sxs-lookup"><span data-stu-id="cee62-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="cee62-170">La preparazione di una macchina virtuale CentOS 7 per Azure è molto simile a CentOS 6, tuttavia vi sono alcune importanti differenze da notare:</span><span class="sxs-lookup"><span data-stu-id="cee62-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="cee62-171">Il pacchetto NetworkManager e l'agente Linux di Azure non sono più in conflitto.</span><span class="sxs-lookup"><span data-stu-id="cee62-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="cee62-172">Questo pacchetto viene installato per impostazione predefinita ed è consigliabile non rimuoverlo.</span><span class="sxs-lookup"><span data-stu-id="cee62-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="cee62-173">GRUB2 viene ora usato come bootloader predefinito, quindi la procedura per la modifica dei parametri kernel è cambiata (vedere di seguito).</span><span class="sxs-lookup"><span data-stu-id="cee62-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="cee62-174">XFS è ora il file system predefinito.</span><span class="sxs-lookup"><span data-stu-id="cee62-174">XFS is now the default file system.</span></span> <span data-ttu-id="cee62-175">Se si vuole, è ancora possibile usare il file system ext4.</span><span class="sxs-lookup"><span data-stu-id="cee62-175">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="cee62-176">**Procedura di configurazione**</span><span class="sxs-lookup"><span data-stu-id="cee62-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="cee62-177">Nella console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cee62-177">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="cee62-178">Fare clic su **Connetti** per aprire una finestra della console per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cee62-178">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="cee62-179">Creare o modificare il file `/etc/sysconfig/network` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="cee62-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="cee62-180">Creare o modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="cee62-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="cee62-181">Modificare le regole udev per evitare la generazione di regole statiche per l'interfaccia Ethernet.</span><span class="sxs-lookup"><span data-stu-id="cee62-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="cee62-182">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="cee62-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="cee62-183">Se si vogliono usare i mirror OpenLogic ospitati nei data center di Azure, sostituire il file `/etc/yum.repos.d/CentOS-Base.repo` con i repository seguenti.</span><span class="sxs-lookup"><span data-stu-id="cee62-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="cee62-184">Verrà aggiunto anche il repository **[openlogic]** che include i pacchetti per l'agente Linux di Azure:</span><span class="sxs-lookup"><span data-stu-id="cee62-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="cee62-185">La parte restante di questa guida presuppone che l'utente usi almeno il repository `[openlogic]`, con cui verrà installato l'agente Linux di Azure illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cee62-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>

7. <span data-ttu-id="cee62-186">Eseguire il comando seguente per cancellare i metadati yum correnti e installare eventuali aggiornamenti:</span><span class="sxs-lookup"><span data-stu-id="cee62-186">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="cee62-187">A meno che non si crei un'immagine per una versione precedente di CentOS, è consigliabile aggiornare tutti i pacchetti all'ultima versione:</span><span class="sxs-lookup"><span data-stu-id="cee62-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="cee62-188">Dopo l'esecuzione di questo comando potrebbe essere necessario un riavvio.</span><span class="sxs-lookup"><span data-stu-id="cee62-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="cee62-189">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="cee62-190">A tale scopo, aprire `/etc/default/grub` in un editor di testo e modificare il parametro `GRUB_CMDLINE_LINUX`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cee62-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="cee62-191">In questo modo si garantisce inoltre che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="cee62-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="cee62-192">Disattiva anche nuove convenzioni di denominazione CentOS 7 per NIC.</span><span class="sxs-lookup"><span data-stu-id="cee62-192">It also turns off the new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="cee62-193">Inoltre, è consigliabile *rimuovere* i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="cee62-193">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="cee62-194">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="cee62-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="cee62-195">L'opzione `crashkernel` può essere configurata, ma si tenga presente che questo parametro ridurrà la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB, il che potrebbe causare problemi con le macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="cee62-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

9. <span data-ttu-id="cee62-196">Dopo aver terminato di modificare `/etc/default/grub` come sopra illustrato, eseguire il comando seguente per ricompilare la configurazione GRUB:</span><span class="sxs-lookup"><span data-stu-id="cee62-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="cee62-197">Se si compila l'immagine da **VMWare, VirtualBox o KVM**, verificare che i driver Hyper-V siano inclusi in initramfs:</span><span class="sxs-lookup"><span data-stu-id="cee62-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span></span>
   
   <span data-ttu-id="cee62-198">Modificare `/etc/dracut.conf`e aggiungere il contenuto:</span><span class="sxs-lookup"><span data-stu-id="cee62-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="cee62-199">Ricompilare l’initramfs:</span><span class="sxs-lookup"><span data-stu-id="cee62-199">Rebuild the initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="cee62-200">Installare l'agente Linux di Azure e le dipendenze:</span><span class="sxs-lookup"><span data-stu-id="cee62-200">Install the Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="cee62-201">Non creare l'area di swap sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="cee62-201">Do not create swap space on the OS disk.</span></span>
   
   <span data-ttu-id="cee62-202">L'agente Linux di Azure può configurare automaticamente l'area di swap utilizzando il disco risorse locale collegato alla VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="cee62-203">Si noti che il disco risorse locale è un disco *temporaneo* e potrebbe essere svuotato in seguito al deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cee62-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="cee62-204">Dopo aver installato l'agente Linux di Azure come illustrato nel passaggio precedente, modificare i seguenti parametri di `/etc/waagent.conf` in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="cee62-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="cee62-205">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="cee62-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="cee62-206">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cee62-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="cee62-207">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-207">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cee62-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cee62-208">Next steps</span></span>
<span data-ttu-id="cee62-209">È ora possibile usare il disco rigido virtuale CentOS Linux per creare nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="cee62-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="cee62-210">Se è la prima volta che si carica il file VHD in Azure, vedere i passaggi 2 e 3 nell'articolo [Creazione e caricamento di un disco rigido virtuale che contiene il sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cee62-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

