---
title: Creare e caricare un disco rigido virtuale Red Hat Enterprise Linux da usare in Azure | Microsoft Docs
description: Informazioni su come creare e caricare un disco rigido virtuale (VHD) di Azure contenente un sistema operativo Linux RedHat.
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
ms.openlocfilehash: b753c76b8c3d789c681d7fbff6aa07590b860be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="02770-103">Preparare una macchina virtuale basata su RedHat per Azure</span><span class="sxs-lookup"><span data-stu-id="02770-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="02770-104">In questo articolo verrà descritto come preparare una macchina virtuale Red Hat Enterprise Linux (RHEL) per l'utilizzo in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="02770-105">Le versioni di RHEL trattate in questo articolo sono la 6.7+ e la 7.1+.</span><span class="sxs-lookup"><span data-stu-id="02770-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="02770-106">Gli hypervisor per la preparazione illustrati in questo articolo sono Hyper-V, KVM (Kernel-based Virtual Machine) e VMware.</span><span class="sxs-lookup"><span data-stu-id="02770-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="02770-107">Per altre informazioni sui requisiti di idoneità per partecipare al programma di accesso al cloud di Red Hat, vedere gli articoli relativi al [sito web di accesso al cloud di Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) e all'[esecuzione di RHEL in Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="02770-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="02770-108">Preparare una macchina virtuale basata su Red Hat dalla console di gestione di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="02770-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="02770-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02770-109">Prerequisites</span></span>
<span data-ttu-id="02770-110">In questa sezione si presuppone che si sia già ottenuto un file ISO dal sito Web Red Hat e che sia già stata installata un'immagine RHEL in un disco rigido virtuale (VHD).</span><span class="sxs-lookup"><span data-stu-id="02770-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="02770-111">Per altri dettagli su come usare la console di gestione di Hyper-V per installare un'immagine del sistema operativo, vedere l'articolo su come [installare il ruolo Hyper-V e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="02770-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="02770-112">**Note sull'installazione di RHEL**</span><span class="sxs-lookup"><span data-stu-id="02770-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="02770-113">Azure non supporta il formato VHDX.</span><span class="sxs-lookup"><span data-stu-id="02770-113">Azure does not support the VHDX format.</span></span> <span data-ttu-id="02770-114">Azure supporta solo dischi rigidi virtuali a dimensione fissa.</span><span class="sxs-lookup"><span data-stu-id="02770-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="02770-115">È possibile usare la console di gestione di Hyper-V o il cmdlet convert-vhd per convertire il disco in formato VHD.</span><span class="sxs-lookup"><span data-stu-id="02770-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="02770-116">Se si usa VirtualBox, durante la creazione del disco selezionare **Fixed size** (A dimensione fissa) anziché l'opzione predefinita di allocazione dinamica.</span><span class="sxs-lookup"><span data-stu-id="02770-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="02770-117">Azure supporta solo macchine virtuali di prima generazione.</span><span class="sxs-lookup"><span data-stu-id="02770-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="02770-118">È possibile convertire una macchina virtuale di prima generazione da VHDX al formato di file VHD e da disco a espansione dinamica a disco a dimensione fissa.</span><span class="sxs-lookup"><span data-stu-id="02770-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="02770-119">Non è possibile modificare la generazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="02770-120">Per altre informazioni, vedere [Creare una macchina virtuale di generazione 1 o 2 in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span><span class="sxs-lookup"><span data-stu-id="02770-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="02770-121">La dimensione massima consentita per il disco rigido virtuale è 1.023 GB.</span><span class="sxs-lookup"><span data-stu-id="02770-121">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="02770-122">Quando si installa il sistema operativo Linux è consigliabile usare partizioni standard anziché LVM (Logical Volume Manager), che è spesso l'impostazione predefinita per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="02770-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="02770-123">Questa procedura consentirà di evitare conflitti di nome LVM con le macchine virtuali clonate, in particolare se fosse eventualmente necessario collegare un disco del sistema operativo a un'altra macchina virtuale identica per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="02770-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="02770-124">È possibile usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) su dischi di dati.</span><span class="sxs-lookup"><span data-stu-id="02770-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="02770-125">Per montare file system UDF (Universal Disk Format) è necessario il supporto del kernel.</span><span class="sxs-lookup"><span data-stu-id="02770-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="02770-126">Al primo avvio in Azure, i supporti con formattazione UDF collegati al guest passano la configurazione di provisioning alla macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="02770-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="02770-127">L'agente Linux di Azure deve poter montare il file system UDF per leggerne la configurazione ed effettuare il provisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="02770-128">Le versioni del kernel Linux precedenti alla 2.6.37 non supportano l'accesso non uniforme alla memoria (NUMA) in Hyper-V con macchine virtuali di dimensioni superiori.</span><span class="sxs-lookup"><span data-stu-id="02770-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="02770-129">Questo problema influisce principalmente sulle distribuzioni precedenti che usano il kernel upstream Red Hat 2.6.32 ed è stato risolto in RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="02770-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="02770-130">Nei sistemi che eseguono kernel personalizzati precedenti alla versione 2.6.37 o kernel basati su RHEL precedenti alla versione 2.6.32-504 deve essere impostato il parametro di avvio `numa=off` nella riga di comando del kernel in grub.conf.</span><span class="sxs-lookup"><span data-stu-id="02770-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span></span> <span data-ttu-id="02770-131">Per altre informazioni, vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="02770-132">Non configurare una partizione di swapping sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02770-132">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="02770-133">L'agente Linux può essere configurato in modo da creare un file di scambio sul disco risorse temporaneo.</span><span class="sxs-lookup"><span data-stu-id="02770-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="02770-134">Altre informazioni su questo argomento sono disponibili nei passaggi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="02770-134">More information about this can be found in the following steps.</span></span>
* <span data-ttu-id="02770-135">Le dimensioni di tutti i dischi rigidi virtuali devono essere multipli di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="02770-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="02770-136">Preparare una macchina virtuale RHEL 6 dalla console di gestione di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="02770-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="02770-137">Nella console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-137">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="02770-138">Fare clic su **Connetti** per aprire una finestra della console per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-138">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="02770-139">In RHEL 6, NetworkManager può interferire con l'agente Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="02770-140">Disinstallare il pacchetto eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-140">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="02770-141">Creare o modificare il file `/etc/sysconfig/network` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="02770-142">Creare o modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="02770-143">Spostare o eliminare le regole udev per evitare la generazione di regole statiche per l'interfaccia Ethernet.</span><span class="sxs-lookup"><span data-stu-id="02770-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="02770-144">Le regole seguenti provocano problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="02770-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="02770-145">Assicurarsi che il servizio di rete venga eseguito all'avvio attivando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-145">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="02770-146">Registrare la propria sottoscrizione Red Hat per abilitare l'installazione dei pacchetti dall'archivio RHEL eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="02770-147">È stato effettuato il push del pacchetto WALinuxAgent `WALinuxAgent-<version>` nel repository di funzionalità aggiuntive di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="02770-148">Abilitare il repository di funzionalità aggiuntive eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-148">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="02770-149">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="02770-150">Per eseguire questa modifica, aprire `/boot/grub/menu.lst` in un editor di testo e verificare che il kernel predefinito includa i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="02770-151">In questo modo si garantisce inoltre che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="02770-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="02770-152">È consigliabile anche rimuovere i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-152">In addition, we recommended that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="02770-153">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="02770-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="02770-154">È possibile mantenere l'opzione `crashkernel` configurata, se necessario.</span><span class="sxs-lookup"><span data-stu-id="02770-154">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="02770-155">Si noti che questo parametro riduce la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB.</span><span class="sxs-lookup"><span data-stu-id="02770-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span></span> <span data-ttu-id="02770-156">Questa configurazione potrebbe causare problemi in macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="02770-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="02770-157">Per RHEL 6.5 e versioni precedenti deve essere impostato anche il parametro del kernel `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="02770-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="02770-158">Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="02770-159">Verificare che il server SSH (Secure Shell) sia installato e configurato per l'esecuzione all'avvio, che è in genere l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="02770-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="02770-160">Modificare /etc/ssh/sshd_config per includere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-160">Modify /etc/ssh/sshd_config to include the following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="02770-161">Installare l'agente Linux di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-161">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="02770-162">L'installazione del pacchetto WALinuxAgent determina la rimozione dei pacchetti NetworkManager e NetworkManager-gnome, se non sono già stati rimossi nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="02770-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="02770-163">Non creare lo spazio di swapping sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02770-163">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="02770-164">L'agente Linux di Azure può configurare automaticamente lo spazio di swapping usando il disco risorse locale collegato alla macchina virtuale dopo il provisioning della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="02770-165">Si noti che il disco risorse locale è un disco temporaneo e può essere svuotato con il deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="02770-166">Dopo aver installato l'agente Linux di Azure nel passaggio precedente, modificare nel modo appropriato i parametri seguenti in /etc/waagent.conf:</span><span class="sxs-lookup"><span data-stu-id="02770-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

14. <span data-ttu-id="02770-167">Annullare la sottoscrizione (se necessario) eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-167">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="02770-168">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="02770-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="02770-169">Fare clic su **Azione** > **Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="02770-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="02770-170">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-170">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="02770-171">Preparare una macchina virtuale RHEL 7 dalla console di gestione di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="02770-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="02770-172">Nella console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-172">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="02770-173">Fare clic su **Connetti** per aprire una finestra della console per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-173">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="02770-174">Creare o modificare il file `/etc/sysconfig/network` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="02770-175">Creare o modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="02770-176">Assicurarsi che il servizio di rete venga eseguito all'avvio attivando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-176">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="02770-177">Registrare la propria sottoscrizione Red Hat per abilitare l'installazione dei pacchetti dall'archivio RHEL eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="02770-178">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="02770-179">Per eseguire questa modifica, aprire `/etc/default/grub` in un editor di testo e modificare il parametro `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="02770-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="02770-180">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="02770-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="02770-181">In questo modo si garantisce inoltre che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="02770-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="02770-182">Questa configurazione disattiva anche le nuove convenzioni di denominazione di RHEL 7 per le schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="02770-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="02770-183">È consigliabile anche rimuovere i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-183">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="02770-184">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="02770-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="02770-185">È possibile mantenere l'opzione `crashkernel` configurata, se necessario.</span><span class="sxs-lookup"><span data-stu-id="02770-185">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="02770-186">Si noti che questo parametro riduce la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB e questo potrebbe causare problemi in macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="02770-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="02770-187">Dopo aver terminato di modificare `/etc/default/grub`, eseguire questo comando per ricompilare la configurazione GRUB:</span><span class="sxs-lookup"><span data-stu-id="02770-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="02770-188">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio, che è in genere l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="02770-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="02770-189">Modificare `/etc/ssh/sshd_config` per poter includere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-189">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="02770-190">È stato effettuato il push del pacchetto WALinuxAgent `WALinuxAgent-<version>` nel repository di funzionalità aggiuntive di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="02770-191">Abilitare il repository di funzionalità aggiuntive eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-191">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="02770-192">Installare l'agente Linux di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-192">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="02770-193">Non creare lo spazio di swapping sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02770-193">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="02770-194">L'agente Linux di Azure può configurare automaticamente lo spazio di swapping usando il disco risorse locale collegato alla macchina virtuale dopo il provisioning della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="02770-195">Si noti che il disco risorse locale è un disco temporaneo e può essere svuotato con il deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="02770-196">Dopo aver installato l'agente Linux di Azure nel passaggio precedente, modificare nel modo appropriato i parametri seguenti in `/etc/waagent.conf`:</span><span class="sxs-lookup"><span data-stu-id="02770-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="02770-197">Se si vuole annullare la registrazione della sottoscrizione, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-197">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="02770-198">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="02770-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="02770-199">Fare clic su **Azione** > **Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="02770-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="02770-200">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-200">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="02770-201">Preparare una macchina virtuale basata su Red Hat da KVM</span><span class="sxs-lookup"><span data-stu-id="02770-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="02770-202">Preparare una macchina virtuale RHEL 6 da KVM</span><span class="sxs-lookup"><span data-stu-id="02770-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="02770-203">Scaricare l'immagine KVM di RHEL 6 dal sito Web Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-203">Download the KVM image of RHEL 6 from the Red Hat website.</span></span>

2. <span data-ttu-id="02770-204">Impostare una password radice.</span><span class="sxs-lookup"><span data-stu-id="02770-204">Set a root password.</span></span>

    <span data-ttu-id="02770-205">Generare una password crittografata e copiare l'output del comando:</span><span class="sxs-lookup"><span data-stu-id="02770-205">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="02770-206">Impostare una password radice con guestfish:</span><span class="sxs-lookup"><span data-stu-id="02770-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="02770-207">Modificare il secondo campo dell'utente radice da "!!"</span><span class="sxs-lookup"><span data-stu-id="02770-207">Change the second field of the root user from "!!"</span></span> <span data-ttu-id="02770-208">con la password crittografata.</span><span class="sxs-lookup"><span data-stu-id="02770-208">to the encrypted password.</span></span>

3. <span data-ttu-id="02770-209">Creare una macchina virtuale in KVM dall'immagine qcow2.</span><span class="sxs-lookup"><span data-stu-id="02770-209">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="02770-210">Impostare il tipo di disco su **qcow2** e il modello del dispositivo di interfaccia di rete virtuale su **virtio**.</span><span class="sxs-lookup"><span data-stu-id="02770-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="02770-211">Avviare quindi la macchina virtuale e accedere come utente ROOT.</span><span class="sxs-lookup"><span data-stu-id="02770-211">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="02770-212">Creare o modificare il file `/etc/sysconfig/network` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="02770-213">Creare o modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="02770-214">Spostare o eliminare le regole udev per evitare la generazione di regole statiche per l'interfaccia Ethernet.</span><span class="sxs-lookup"><span data-stu-id="02770-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="02770-215">Le regole seguenti causano problemi quando si clona una macchina virtuale in Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="02770-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="02770-216">Assicurarsi che il servizio di rete venga eseguito all'avvio attivando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-216">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="02770-217">Registrare la propria sottoscrizione Red Hat per abilitare l'installazione dei pacchetti dall'archivio RHEL eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="02770-218">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="02770-219">Per eseguire questa configurazione, aprire `/boot/grub/menu.lst` in un editor di testo e verificare che il kernel predefinito includa i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="02770-220">In questo modo si garantisce inoltre che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="02770-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="02770-221">È consigliabile anche rimuovere i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-221">In addition, we recommend that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="02770-222">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="02770-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="02770-223">È possibile mantenere l'opzione `crashkernel` configurata, se necessario.</span><span class="sxs-lookup"><span data-stu-id="02770-223">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="02770-224">Si noti che questo parametro riduce la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB e questo potrebbe causare problemi in macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="02770-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="02770-225">Per RHEL 6.5 e versioni precedenti deve essere impostato anche il parametro del kernel `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="02770-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="02770-226">Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="02770-227">Aggiungere i moduli Hyper-V a initramfs:</span><span class="sxs-lookup"><span data-stu-id="02770-227">Add Hyper-V modules to initramfs:</span></span>  

    <span data-ttu-id="02770-228">Modificare `/etc/dracut.conf` e aggiungere il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-228">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="02770-229">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="02770-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="02770-230">Disinstallare cloud-init:</span><span class="sxs-lookup"><span data-stu-id="02770-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="02770-231">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio:</span><span class="sxs-lookup"><span data-stu-id="02770-231">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="02770-232">Modificare /etc/ssh/sshd_config per includere le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-232">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="02770-233">È stato effettuato il push del pacchetto WALinuxAgent `WALinuxAgent-<version>` nel repository di funzionalità aggiuntive di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="02770-234">Abilitare il repository di funzionalità aggiuntive eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-234">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="02770-235">Installare l'agente Linux di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-235">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="02770-236">L'agente Linux di Azure può configurare automaticamente lo spazio di swapping usando il disco risorse locale collegato alla macchina virtuale dopo il provisioning della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="02770-237">Si noti che il disco risorse locale è un disco temporaneo e può essere svuotato con il deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="02770-238">Dopo aver installato l'agente Linux di Azure nel passaggio precedente, modificare nel modo appropriato i parametri seguenti in **/etc/waagent.conf**:</span><span class="sxs-lookup"><span data-stu-id="02770-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="02770-239">Annullare la sottoscrizione (se necessario) eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-239">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="02770-240">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="02770-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="02770-241">Arrestare la macchina virtuale in KVM.</span><span class="sxs-lookup"><span data-stu-id="02770-241">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="02770-242">Convertire l'immagine qcow2 nel formato VHD.</span><span class="sxs-lookup"><span data-stu-id="02770-242">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="02770-243">Convertire innanzitutto l'immagine in formato non elaborato:</span><span class="sxs-lookup"><span data-stu-id="02770-243">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="02770-244">Verificare che le dimensioni dell'immagine non elaborata siano pari a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="02770-244">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="02770-245">In caso contrario, arrotondare le dimensioni a 1 MB:</span><span class="sxs-lookup"><span data-stu-id="02770-245">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="02770-246">Convertire il disco non formattato in un disco rigido virtuale a dimensione fissa:</span><span class="sxs-lookup"><span data-stu-id="02770-246">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="02770-247">Preparare una macchina virtuale RHEL 7 da KVM</span><span class="sxs-lookup"><span data-stu-id="02770-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="02770-248">Scaricare l'immagine KVM di RHEL 7 dal sito Web di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-248">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="02770-249">Questa procedura usa come esempio RHEL 7.</span><span class="sxs-lookup"><span data-stu-id="02770-249">This procedure uses RHEL 7 as the example.</span></span>

2. <span data-ttu-id="02770-250">Impostare una password radice.</span><span class="sxs-lookup"><span data-stu-id="02770-250">Set a root password.</span></span>

    <span data-ttu-id="02770-251">Generare una password crittografata e copiare l'output del comando:</span><span class="sxs-lookup"><span data-stu-id="02770-251">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="02770-252">Impostare una password radice con guestfish:</span><span class="sxs-lookup"><span data-stu-id="02770-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="02770-253">Modificare il secondo campo dell'utente radice da "!!"</span><span class="sxs-lookup"><span data-stu-id="02770-253">Change the second field of root user from "!!"</span></span> <span data-ttu-id="02770-254">con la password crittografata.</span><span class="sxs-lookup"><span data-stu-id="02770-254">to the encrypted password.</span></span>

3. <span data-ttu-id="02770-255">Creare una macchina virtuale in KVM dall'immagine qcow2.</span><span class="sxs-lookup"><span data-stu-id="02770-255">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="02770-256">Impostare il tipo di disco su **qcow2** e il modello del dispositivo di interfaccia di rete virtuale su **virtio**.</span><span class="sxs-lookup"><span data-stu-id="02770-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="02770-257">Avviare quindi la macchina virtuale e accedere come utente ROOT.</span><span class="sxs-lookup"><span data-stu-id="02770-257">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="02770-258">Creare o modificare il file `/etc/sysconfig/network` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="02770-259">Creare o modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="02770-260">Assicurarsi che il servizio di rete venga eseguito all'avvio attivando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-260">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="02770-261">Registrare la propria sottoscrizione Red Hat per abilitare l’installazione dei pacchetti dall’archivio RHEL eseguendo il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="02770-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="02770-262">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="02770-263">Per eseguire questa configurazione, aprire `/etc/default/grub` in un editor di testo e modificare il parametro `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="02770-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="02770-264">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="02770-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="02770-265">Questo comando, inoltre, garantisce che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="02770-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="02770-266">Il comando disattiva anche le nuove convenzioni di denominazione di RHEL 7 per le schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="02770-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="02770-267">È consigliabile anche rimuovere i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-267">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="02770-268">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="02770-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="02770-269">È possibile mantenere l'opzione `crashkernel` configurata, se necessario.</span><span class="sxs-lookup"><span data-stu-id="02770-269">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="02770-270">Si noti che questo parametro riduce la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB e questo potrebbe causare problemi in macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="02770-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="02770-271">Dopo aver terminato di modificare `/etc/default/grub`, eseguire questo comando per ricompilare la configurazione GRUB:</span><span class="sxs-lookup"><span data-stu-id="02770-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="02770-272">Aggiungere i moduli Hyper-V in initramfs.</span><span class="sxs-lookup"><span data-stu-id="02770-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="02770-273">Modificare `/etc/dracut.conf` e aggiungere il contenuto:</span><span class="sxs-lookup"><span data-stu-id="02770-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="02770-274">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="02770-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="02770-275">Disinstallare cloud-init:</span><span class="sxs-lookup"><span data-stu-id="02770-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="02770-276">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio:</span><span class="sxs-lookup"><span data-stu-id="02770-276">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="02770-277">Modificare /etc/ssh/sshd_config per includere le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-277">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="02770-278">È stato effettuato il push del pacchetto WALinuxAgent `WALinuxAgent-<version>` nel repository di funzionalità aggiuntive di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="02770-279">Abilitare il repository di funzionalità aggiuntive eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-279">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="02770-280">Installare l'agente Linux di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-280">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="02770-281">Abilitare il servizio waagent:</span><span class="sxs-lookup"><span data-stu-id="02770-281">Enable the waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="02770-282">Non creare lo spazio di swapping sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02770-282">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="02770-283">L'agente Linux di Azure può configurare automaticamente lo spazio di swapping usando il disco risorse locale collegato alla macchina virtuale dopo il provisioning della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="02770-284">Si noti che il disco risorse locale è un disco temporaneo e può essere svuotato con il deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="02770-285">Dopo aver installato l'agente Linux di Azure nel passaggio precedente, modificare nel modo appropriato i parametri seguenti in `/etc/waagent.conf`:</span><span class="sxs-lookup"><span data-stu-id="02770-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="02770-286">Annullare la sottoscrizione (se necessario) eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-286">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="02770-287">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="02770-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="02770-288">Arrestare la macchina virtuale in KVM.</span><span class="sxs-lookup"><span data-stu-id="02770-288">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="02770-289">Convertire l'immagine qcow2 nel formato VHD.</span><span class="sxs-lookup"><span data-stu-id="02770-289">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="02770-290">Convertire innanzitutto l'immagine in formato non elaborato:</span><span class="sxs-lookup"><span data-stu-id="02770-290">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="02770-291">Verificare che le dimensioni dell'immagine non elaborata siano pari a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="02770-291">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="02770-292">In caso contrario, arrotondare le dimensioni a 1 MB:</span><span class="sxs-lookup"><span data-stu-id="02770-292">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="02770-293">Convertire il disco non formattato in un disco rigido virtuale a dimensione fissa:</span><span class="sxs-lookup"><span data-stu-id="02770-293">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="02770-294">Preparare una macchina virtuale basata su Red Hat da VMware</span><span class="sxs-lookup"><span data-stu-id="02770-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="02770-295">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02770-295">Prerequisites</span></span>
<span data-ttu-id="02770-296">In questa sezione si presuppone che una macchina virtuale RHEL sia già stata installata in VMware.</span><span class="sxs-lookup"><span data-stu-id="02770-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="02770-297">Per informazioni dettagliate su come installare un sistema operativo in VMware, vedere la [guida all'installazione del sistema operativo guest VMware](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="02770-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="02770-298">Quando si installa il sistema operativo Linux è consigliabile usare partizioni standard anziché LVM, che è spesso l'impostazione predefinita per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="02770-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="02770-299">Questo consentirà di evitare conflitti di nome LVM con la macchina virtuale clonata, in particolare se fosse eventualmente necessario collegare un disco del sistema operativo a un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="02770-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="02770-300">Se si preferisce, su dischi di dati si può usare LVM o RAID.</span><span class="sxs-lookup"><span data-stu-id="02770-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="02770-301">Non configurare una partizione di swapping sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02770-301">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="02770-302">È possibile configurare l'agente Linux per poter creare un file di scambio sul disco temporaneo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="02770-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="02770-303">Altre informazioni su questo argomento sono disponibili nei passaggi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="02770-303">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="02770-304">Quando si crea il disco rigido virtuale, selezionare **Store virtual disk as a single file**(Archivia disco virtuale come singolo file).</span><span class="sxs-lookup"><span data-stu-id="02770-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="02770-305">Preparare una macchina virtuale RHEL 6 da VMware</span><span class="sxs-lookup"><span data-stu-id="02770-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="02770-306">In RHEL 6, NetworkManager può interferire con l'agente Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="02770-307">Disinstallare il pacchetto eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-307">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="02770-308">Creare nella directory /etc/sysconfig/ un file denominato **network** contenente il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="02770-309">Creare o modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="02770-310">Spostare o eliminare le regole udev per evitare la generazione di regole statiche per l'interfaccia Ethernet.</span><span class="sxs-lookup"><span data-stu-id="02770-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="02770-311">Le regole seguenti causano problemi quando si clona una macchina virtuale in Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="02770-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="02770-312">Assicurarsi che il servizio di rete venga eseguito all'avvio attivando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-312">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="02770-313">Registrare la propria sottoscrizione Red Hat per abilitare l'installazione dei pacchetti dall'archivio RHEL eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="02770-314">È stato effettuato il push del pacchetto WALinuxAgent `WALinuxAgent-<version>` nel repository di funzionalità aggiuntive di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="02770-315">Abilitare il repository di funzionalità aggiuntive eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-315">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="02770-316">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="02770-317">A tale scopo, aprire `/etc/default/grub` in un editor di testo e modificare il parametro `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="02770-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="02770-318">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="02770-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="02770-319">In questo modo si garantisce inoltre che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="02770-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="02770-320">È consigliabile anche rimuovere i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-320">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="02770-321">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="02770-321">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="02770-322">È possibile mantenere l'opzione `crashkernel` configurata, se necessario.</span><span class="sxs-lookup"><span data-stu-id="02770-322">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="02770-323">Si noti che questo parametro riduce la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB e questo potrebbe causare problemi in macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="02770-323">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="02770-324">Aggiungere i moduli Hyper-V a initramfs:</span><span class="sxs-lookup"><span data-stu-id="02770-324">Add Hyper-V modules to initramfs:</span></span>

    <span data-ttu-id="02770-325">Modificare `/etc/dracut.conf` e aggiungere il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-325">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="02770-326">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="02770-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="02770-327">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio, che è in genere l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="02770-327">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="02770-328">Modificare `/etc/ssh/sshd_config` per poter includere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-328">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    <span data-ttu-id="02770-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="02770-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="02770-330">Installare l'agente Linux di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-330">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="02770-331">Non creare lo spazio di swapping sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02770-331">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="02770-332">L'agente Linux di Azure può configurare automaticamente lo spazio di swapping usando il disco risorse locale collegato alla macchina virtuale dopo il provisioning della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-332">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="02770-333">Si noti che il disco risorse locale è un disco temporaneo e può essere svuotato con il deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-333">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="02770-334">Dopo aver installato l'agente Linux di Azure nel passaggio precedente, modificare nel modo appropriato i parametri seguenti in `/etc/waagent.conf`:</span><span class="sxs-lookup"><span data-stu-id="02770-334">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="02770-335">Annullare la sottoscrizione (se necessario) eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-335">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="02770-336">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="02770-336">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="02770-337">Arrestare la macchina virtuale e convertire il file VMDK in un file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="02770-337">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span></span>

    <span data-ttu-id="02770-338">Convertire innanzitutto l'immagine in formato non elaborato:</span><span class="sxs-lookup"><span data-stu-id="02770-338">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="02770-339">Verificare che le dimensioni dell'immagine non elaborata siano pari a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="02770-339">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="02770-340">In caso contrario, arrotondare le dimensioni a 1 MB:</span><span class="sxs-lookup"><span data-stu-id="02770-340">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="02770-341">Convertire il disco non formattato in un disco rigido virtuale a dimensione fissa:</span><span class="sxs-lookup"><span data-stu-id="02770-341">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="02770-342">Preparare una macchina virtuale RHEL 7 da VMware</span><span class="sxs-lookup"><span data-stu-id="02770-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="02770-343">Creare o modificare il file `/etc/sysconfig/network` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-343">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="02770-344">Creare o modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` e aggiungere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-344">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="02770-345">Assicurarsi che il servizio di rete venga eseguito all'avvio attivando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-345">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="02770-346">Registrare la propria sottoscrizione Red Hat per abilitare l'installazione dei pacchetti dall'archivio RHEL eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-346">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="02770-347">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-347">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="02770-348">Per eseguire questa modifica, aprire `/etc/default/grub` in un editor di testo e modificare il parametro `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="02770-348">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="02770-349">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="02770-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="02770-350">Questa configurazione, inoltre, garantisce che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="02770-350">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="02770-351">Disattiva anche le nuove convenzioni di denominazione RHEL 7 per le schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="02770-351">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="02770-352">È consigliabile anche rimuovere i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="02770-352">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="02770-353">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="02770-353">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="02770-354">È possibile mantenere l'opzione `crashkernel` configurata, se necessario.</span><span class="sxs-lookup"><span data-stu-id="02770-354">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="02770-355">Si noti che questo parametro riduce la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB e questo potrebbe causare problemi in macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="02770-355">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="02770-356">Dopo aver terminato di modificare `/etc/default/grub`, eseguire questo comando per ricompilare la configurazione GRUB:</span><span class="sxs-lookup"><span data-stu-id="02770-356">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="02770-357">Aggiungere i moduli Hyper-V a initramfs.</span><span class="sxs-lookup"><span data-stu-id="02770-357">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="02770-358">Modificare `/etc/dracut.conf`e aggiungere il contenuto:</span><span class="sxs-lookup"><span data-stu-id="02770-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="02770-359">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="02770-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="02770-360">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="02770-360">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="02770-361">Questa è in genere l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="02770-361">This setting is usually the default.</span></span> <span data-ttu-id="02770-362">Modificare `/etc/ssh/sshd_config` per poter includere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-362">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="02770-363">È stato effettuato il push del pacchetto WALinuxAgent `WALinuxAgent-<version>` nel repository di funzionalità aggiuntive di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-363">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="02770-364">Abilitare il repository di funzionalità aggiuntive eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="02770-364">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="02770-365">Installare l'agente Linux di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-365">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="02770-366">Non creare lo spazio di swapping sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02770-366">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="02770-367">L'agente Linux di Azure può configurare automaticamente lo spazio di swapping usando il disco risorse locale collegato alla macchina virtuale dopo il provisioning della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-367">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="02770-368">Si noti che il disco risorse locale è un disco temporaneo e può essere svuotato con il deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-368">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="02770-369">Dopo aver installato l'agente Linux di Azure nel passaggio precedente, modificare nel modo appropriato i parametri seguenti in `/etc/waagent.conf`:</span><span class="sxs-lookup"><span data-stu-id="02770-369">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

12. <span data-ttu-id="02770-370">Se si vuole annullare la registrazione della sottoscrizione, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-370">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="02770-371">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="02770-371">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="02770-372">Arrestare la macchina virtuale e convertire il file VMDK nel formato VHD.</span><span class="sxs-lookup"><span data-stu-id="02770-372">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    <span data-ttu-id="02770-373">Convertire innanzitutto l'immagine in formato non elaborato:</span><span class="sxs-lookup"><span data-stu-id="02770-373">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="02770-374">Verificare che le dimensioni dell'immagine non elaborata siano pari a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="02770-374">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="02770-375">In caso contrario, arrotondare le dimensioni a 1 MB:</span><span class="sxs-lookup"><span data-stu-id="02770-375">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="02770-376">Convertire il disco non formattato in un disco rigido virtuale a dimensione fissa:</span><span class="sxs-lookup"><span data-stu-id="02770-376">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="02770-377">Preparare una macchina virtuale basata su Red Hat da un'immagine ISO usando un file kickstart automatico</span><span class="sxs-lookup"><span data-stu-id="02770-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="02770-378">Preparare una macchina virtuale RHEL 7 da un file kickstart</span><span class="sxs-lookup"><span data-stu-id="02770-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="02770-379">Creare e salvare un file kickstart con il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="02770-379">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="02770-380">Per informazioni dettagliate sull'installazione di kickstart, vedere la [guida all'installazione di kickstart](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="02770-380">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run the Setup Agent on first boot
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

        # Clear the MBR
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

        # Power down the machine after install
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

        # Disable the root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set the cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build the grub cfg
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

2. <span data-ttu-id="02770-381">Posizionare il file kickstart in un percorso in cui sia accessibile per il sistema di installazione.</span><span class="sxs-lookup"><span data-stu-id="02770-381">Place the kickstart file where the installation system can access it.</span></span>

3. <span data-ttu-id="02770-382">Creare una nuova macchina virtuale nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="02770-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="02770-383">Nella pagina **Connessione disco rigido virtuale** selezionare **Connetti un disco rigido virtuale successivamente** e completare la creazione guidata della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-383">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="02770-384">Aprire le impostazioni della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="02770-384">Open the virtual machine settings:</span></span>

    <span data-ttu-id="02770-385">a.</span><span class="sxs-lookup"><span data-stu-id="02770-385">a.</span></span>  <span data-ttu-id="02770-386">Collegare un nuovo disco rigido virtuale alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-386">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="02770-387">Accertarsi di selezionare **Formato VHD** e **A dimensione fissa**.</span><span class="sxs-lookup"><span data-stu-id="02770-387">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="02770-388">b.</span><span class="sxs-lookup"><span data-stu-id="02770-388">b.</span></span>  <span data-ttu-id="02770-389">Collegare l'ISO di installazione all'unità DVD.</span><span class="sxs-lookup"><span data-stu-id="02770-389">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="02770-390">c.</span><span class="sxs-lookup"><span data-stu-id="02770-390">c.</span></span>  <span data-ttu-id="02770-391">Impostare il BIOS per l'avvio da CD.</span><span class="sxs-lookup"><span data-stu-id="02770-391">Set the BIOS to boot from CD.</span></span>

5. <span data-ttu-id="02770-392">Avviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02770-392">Start the virtual machine.</span></span> <span data-ttu-id="02770-393">Quando viene visualizzata la guida all'installazione, premere **Tab** per configurare le opzioni di avvio.</span><span class="sxs-lookup"><span data-stu-id="02770-393">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

6. <span data-ttu-id="02770-394">Inserire `inst.ks=<the location of the kickstart file>` alla fine di opzioni di avvio e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="02770-394">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="02770-395">Attendere la fine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="02770-395">Wait for the installation to finish.</span></span> <span data-ttu-id="02770-396">Al termine, la macchina virtuale verrà arrestata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="02770-396">When it's finished, the virtual machine will be shut down automatically.</span></span> <span data-ttu-id="02770-397">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-397">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="02770-398">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="02770-398">Known issues</span></span>
### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="02770-399">Non è possibile includere il driver Hyper-V nel disco RAM iniziale quando si usa un hypervisor non Hyper-V</span><span class="sxs-lookup"><span data-stu-id="02770-399">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="02770-400">In alcuni casi, i programmi di installazione di Linux potrebbero non includere i driver per Hyper-V nel disco RAM iniziale (initrd o initramfs), a meno che Linux non rilevi di essere in esecuzione in un ambiente Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="02770-400">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="02770-401">Quando si usa un sistema di virtualizzazione diverso (Virtualbox, Xen e così via) per preparare l'immagine Linux, potrebbe essere necessario ricompilare initrd per assicurarsi che almeno i moduli del kernel hv_vmbus e hv_storvsc siano disponibili nel disco RAM iniziale.</span><span class="sxs-lookup"><span data-stu-id="02770-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="02770-402">Questo è un problema noto, almeno nei sistemi basati sulla distribuzione upstream di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="02770-402">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="02770-403">Per risolvere questo problema, aggiungere i moduli Hyper-V a initramfs e ricompilarlo:</span><span class="sxs-lookup"><span data-stu-id="02770-403">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="02770-404">Modificare `/etc/dracut.conf` e aggiungere il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="02770-404">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="02770-405">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="02770-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="02770-406">Per altri dettagli, vedere le informazioni sulla [ricompilazione di initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="02770-406">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02770-407">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02770-407">Next steps</span></span>
<span data-ttu-id="02770-408">È ora possibile usare il disco rigido virtuale Red Hat Enterprise Linux per creare nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="02770-408">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="02770-409">Se è la prima volta che si carica il file VHD in Azure, vedere i passaggi 2 e 3 nell'articolo [Creazione e caricamento di un disco rigido virtuale che contiene il sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="02770-409">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="02770-410">Per altre informazioni sugli hypervisor certificati per l'esecuzione di Red Hat Enterprise Linux, visitare [il sito Web di Red Hat](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="02770-410">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
