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
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="e0631-103">Preparare una macchina virtuale basata su RedHat per Azure</span><span class="sxs-lookup"><span data-stu-id="e0631-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="e0631-104">In questo articolo si apprenderà come tooprepare una macchina virtuale Red Hat Enterprise Linux (RHEL) per l'uso in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="e0631-105">versioni di Hello di RHEL trattate in questo articolo sono 6.7 + e + 7.1.</span><span class="sxs-lookup"><span data-stu-id="e0631-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="e0631-106">hypervisor di Hello per la preparazione che rientrano in questo articolo sono macchina virtuale Hyper-V, basata sul kernel (KVM) e VMware.</span><span class="sxs-lookup"><span data-stu-id="e0631-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="e0631-107">Per altre informazioni sui requisiti di idoneità per partecipare al programma di accesso al cloud di Red Hat, vedere gli articoli relativi al [sito web di accesso al cloud di Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) e all'[esecuzione di RHEL in Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="e0631-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="e0631-108">Preparare una macchina virtuale basata su Red Hat dalla console di gestione di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e0631-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e0631-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e0631-109">Prerequisites</span></span>
<span data-ttu-id="e0631-110">In questa sezione si presuppone che si possiede già un file ISO dal sito Web di Red Hat hello e installato hello RHEL immagine tooa disco rigido virtuale (VHD).</span><span class="sxs-lookup"><span data-stu-id="e0631-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="e0631-111">Per ulteriori informazioni su come tooinstall di gestione di Hyper-V toouse un'immagine del sistema operativo, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0631-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="e0631-112">**Note sull'installazione di RHEL**</span><span class="sxs-lookup"><span data-stu-id="e0631-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="e0631-113">Azure non supporta il formato di file VHDX hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="e0631-114">Azure supporta solo dischi rigidi virtuali a dimensione fissa.</span><span class="sxs-lookup"><span data-stu-id="e0631-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="e0631-115">È possibile usare Gestione di Hyper-V tooconvert hello disco tooVHD formato oppure è possibile utilizzare cmdlet convert-vhd hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="e0631-116">Se si utilizza VirtualBox, selezionare **dimensioni fisse** rispetto predefinito toohello allocati dinamicamente opzione quando si crea il disco di hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="e0631-117">Azure supporta solo macchine virtuali di prima generazione.</span><span class="sxs-lookup"><span data-stu-id="e0631-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="e0631-118">Formato di file disco rigido virtuale VHDX toohello e dal disco di dimensioni fisse tooa a espansione dinamica, è possibile convertire una macchina virtuale di generazione 1.</span><span class="sxs-lookup"><span data-stu-id="e0631-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="e0631-119">Non è possibile modificare la generazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0631-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="e0631-120">Per altre informazioni, vedere [Creare una macchina virtuale di generazione 1 o 2 in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span><span class="sxs-lookup"><span data-stu-id="e0631-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="e0631-121">dimensioni massime Hello che sono consentita per il disco rigido virtuale hello è 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="e0631-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="e0631-122">Quando si installa hello del sistema operativo Linux, è consigliabile utilizzare partizioni standard piuttosto che come Manager di Volume logico (LVM) è spesso predefinito hello per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="e0631-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="e0631-123">Questo modo, si eviteranno LVM nome in conflitto con le macchine virtuali clonate, in particolare se avrai bisogno di macchina virtuale identica un sistema operativo disco tooanother tooattach per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e0631-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="e0631-124">È possibile usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) su dischi di dati.</span><span class="sxs-lookup"><span data-stu-id="e0631-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="e0631-125">Per montare file system UDF (Universal Disk Format) è necessario il supporto del kernel.</span><span class="sxs-lookup"><span data-stu-id="e0631-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="e0631-126">Al primo avvio in Azure, hello in formato UDF supporto che è collegato toohello guest passa hello provisioning configurazione toohello macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="e0631-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="e0631-127">Hello agente Linux di Azure deve essere in grado di toomount hello UDF file system tooread la configurazione e provisioning di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="e0631-128">Versioni del kernel Linux hello 2.6.37 precedenti non supportano (NUMA) non-uniform memory access in Hyper-V con dimensioni maggiori di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0631-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="e0631-129">Questo problema principalmente impatti distribuzioni precedenti che usano hello monte kernel Red Hat 2.6.32 ed è stato corretto in RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="e0631-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="e0631-130">I sistemi che eseguono kernel personalizzato che risalgono a più 2.6.37 o directcompute basato su RHEL che risalgono a più 2.6.32-504 devono impostare hello `numa=off` parametro di avvio nella riga di comando di kernel hello in grub.conf.</span><span class="sxs-lookup"><span data-stu-id="e0631-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="e0631-131">Per altre informazioni, vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="e0631-132">Non si configura una partizione di scambio su disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="e0631-133">Hello agente Linux può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="e0631-134">Ulteriori informazioni su questo sono reperibile in hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="e0631-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="e0631-135">Le dimensioni di tutti i dischi rigidi virtuali devono essere multipli di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0631-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="e0631-136">Preparare una macchina virtuale RHEL 6 dalla console di gestione di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e0631-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="e0631-137">Nella console di gestione Hyper-V selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="e0631-138">Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="e0631-139">RHEL 6, NetworkManager può interferire con l'agente Linux di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="e0631-140">Disinstallazione di questo pacchetto eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="e0631-141">Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="e0631-142">Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="e0631-143">Spostare o rimuovere hello udev regole tooavoid la generazione di regole statiche per l'interfaccia Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="e0631-144">Le regole seguenti provocano problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0631-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="e0631-145">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="e0631-146">Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="e0631-147">pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0631-148">Abilitare repository extra hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="e0631-149">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0631-150">toodo questa modifica, aprire `/boot/grub/menu.lst` in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e0631-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="e0631-151">Questa operazione garantisce inoltre che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e0631-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="e0631-152">Inoltre, è consigliabile rimuovere hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e0631-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="e0631-153">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="e0631-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="e0631-154">È possibile lasciare hello `crashkernel` opzione configurato se si desidera.</span><span class="sxs-lookup"><span data-stu-id="e0631-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0631-155">Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più.</span><span class="sxs-lookup"><span data-stu-id="e0631-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="e0631-156">Questa configurazione potrebbe causare problemi in macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="e0631-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="e0631-157">RHEL versione 6.5 e versioni precedenti è necessario impostare anche hello `numa=off` parametro kernel.</span><span class="sxs-lookup"><span data-stu-id="e0631-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="e0631-158">Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="e0631-159">Verificare che il server protetto shell (SSH) hello sia installato e configurato toostart in fase di avvio, è in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="e0631-160">Modificare /etc/ssh/sshd_config tooinclude hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="e0631-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="e0631-161">Installare l'agente Linux di Azure hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="e0631-162">Pacchetto di WALinuxAgent hello installazione rimuove hello NetworkManager e pacchetti NetworkManager gnome se non sono stati già rimossi nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="e0631-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="e0631-163">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0631-164">Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0631-165">Si noti che hello locale disco di risorsa è un disco temporaneo e che può essere svuotato quando viene effettuato il deprovisioning macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0631-166">Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="e0631-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="e0631-167">Annullare la registrazione hello sottoscrizione (se necessario) eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="e0631-168">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="e0631-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="e0631-169">Fare clic su **Azione** > **Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0631-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e0631-170">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e0631-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="e0631-171">Preparare una macchina virtuale RHEL 7 dalla console di gestione di Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e0631-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="e0631-172">Nella console di gestione Hyper-V selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="e0631-173">Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="e0631-174">Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="e0631-175">Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="e0631-176">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="e0631-177">Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="e0631-178">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0631-179">toodo questa modifica, aprirla `/etc/default/grub` in un editor di testo e modifica hello `GRUB_CMDLINE_LINUX` parametro.</span><span class="sxs-lookup"><span data-stu-id="e0631-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="e0631-180">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e0631-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="e0631-181">Questa operazione garantisce inoltre che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e0631-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e0631-182">Questa configurazione viene disattivata anche hello nuove RHEL 7 convenzioni di denominazione per le schede NIC.</span><span class="sxs-lookup"><span data-stu-id="e0631-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="e0631-183">Inoltre, è consigliabile rimuovere hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e0631-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="e0631-184">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="e0631-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0631-185">È possibile lasciare hello `crashkernel` opzione configurato se si desidera.</span><span class="sxs-lookup"><span data-stu-id="e0631-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0631-186">Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.</span><span class="sxs-lookup"><span data-stu-id="e0631-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="e0631-187">Dopo avere completato modifica `/etc/default/grub`eseguire hello seguenti comando toorebuild hello grub configurazione:</span><span class="sxs-lookup"><span data-stu-id="e0631-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="e0631-188">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio, è in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="e0631-189">Modificare `/etc/ssh/sshd_config` hello tooinclude seguente riga:</span><span class="sxs-lookup"><span data-stu-id="e0631-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="e0631-190">pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0631-191">Abilitare repository extra hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="e0631-192">Installare l'agente Linux di Azure hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="e0631-193">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0631-194">Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0631-195">Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e0631-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0631-196">Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in `/etc/waagent.conf` in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="e0631-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="e0631-197">Se si desidera che toounregister hello sottoscrizione, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="e0631-198">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="e0631-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="e0631-199">Fare clic su **Azione** > **Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0631-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e0631-200">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e0631-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="e0631-201">Preparare una macchina virtuale basata su Red Hat da KVM</span><span class="sxs-lookup"><span data-stu-id="e0631-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="e0631-202">Preparare una macchina virtuale RHEL 6 da KVM</span><span class="sxs-lookup"><span data-stu-id="e0631-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="e0631-203">Scaricare l'immagine KVM hello RHEL 6 dal sito Web di hello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="e0631-204">Impostare una password radice.</span><span class="sxs-lookup"><span data-stu-id="e0631-204">Set a root password.</span></span>

    <span data-ttu-id="e0631-205">Generare una password crittografata e copiare l'output di hello del comando hello:</span><span class="sxs-lookup"><span data-stu-id="e0631-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="e0631-206">Impostare una password radice con guestfish:</span><span class="sxs-lookup"><span data-stu-id="e0631-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="e0631-207">Secondo campo hello modifica dell'utente root hello da "."</span><span class="sxs-lookup"><span data-stu-id="e0631-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="e0631-208">password crittografata toohello.</span><span class="sxs-lookup"><span data-stu-id="e0631-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="e0631-209">Creare una macchina virtuale KVM dall'immagine qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="e0631-210">Impostare il tipo di disco hello troppo**qcow2**e impostare modello dispositivo dell'interfaccia di rete virtuale hello troppo**virtio**.</span><span class="sxs-lookup"><span data-stu-id="e0631-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="e0631-211">Quindi, avviare la macchina virtuale hello e accedere come radice.</span><span class="sxs-lookup"><span data-stu-id="e0631-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="e0631-212">Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="e0631-213">Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="e0631-214">Spostare o rimuovere hello udev regole tooavoid la generazione di regole statiche per l'interfaccia Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="e0631-215">Le regole seguenti causano problemi quando si clona una macchina virtuale in Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0631-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="e0631-216">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="e0631-217">Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="e0631-218">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0631-219">toodo questa configurazione, aprire `/boot/grub/menu.lst` in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e0631-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="e0631-220">Questa operazione garantisce inoltre che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e0631-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="e0631-221">Inoltre, è consigliabile rimuovere hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e0631-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="e0631-222">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="e0631-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0631-223">È possibile lasciare hello `crashkernel` opzione configurato se si desidera.</span><span class="sxs-lookup"><span data-stu-id="e0631-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0631-224">Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.</span><span class="sxs-lookup"><span data-stu-id="e0631-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="e0631-225">RHEL versione 6.5 e versioni precedenti è necessario impostare anche hello `numa=off` parametro kernel.</span><span class="sxs-lookup"><span data-stu-id="e0631-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="e0631-226">Vedere l'articolo [KB 436883](https://access.redhat.com/solutions/436883) di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="e0631-227">Aggiungere tooinitramfs moduli Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0631-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="e0631-228">Modifica `/etc/dracut.conf`e aggiungere hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="e0631-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="e0631-229">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0631-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="e0631-230">Disinstallare cloud-init:</span><span class="sxs-lookup"><span data-stu-id="e0631-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="e0631-231">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio:</span><span class="sxs-lookup"><span data-stu-id="e0631-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="e0631-232">Modificare /etc/ssh/sshd_config tooinclude hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="e0631-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="e0631-233">pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0631-234">Abilitare repository extra hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="e0631-235">Installare l'agente Linux di Azure hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="e0631-236">Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0631-237">Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e0631-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0631-238">Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in **/etc/waagent.conf** in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="e0631-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="e0631-239">Annullare la registrazione hello sottoscrizione (se necessario) eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="e0631-240">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="e0631-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="e0631-241">Spegnere la macchina virtuale hello KVM.</span><span class="sxs-lookup"><span data-stu-id="e0631-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="e0631-242">Convertire il formato VHD toohello di hello qcow2 immagine.</span><span class="sxs-lookup"><span data-stu-id="e0631-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="e0631-243">Prima di convertire formato tooraw di hello immagine:</span><span class="sxs-lookup"><span data-stu-id="e0631-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="e0631-244">Assicurarsi che le dimensioni di hello dell'immagine non elaborati di hello sono allineata con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0631-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="e0631-245">In caso contrario, l'arrotondamento per eccesso hello dimensioni tooalign con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="e0631-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="e0631-246">Convertire hello disco raw tooa dimensione fissa disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="e0631-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="e0631-247">Preparare una macchina virtuale RHEL 7 da KVM</span><span class="sxs-lookup"><span data-stu-id="e0631-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="e0631-248">Scaricare l'immagine KVM hello RHEL 7 dal sito Web di hello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="e0631-249">Questa procedura utilizza RHEL 7 come esempio hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="e0631-250">Impostare una password radice.</span><span class="sxs-lookup"><span data-stu-id="e0631-250">Set a root password.</span></span>

    <span data-ttu-id="e0631-251">Generare una password crittografata e copiare l'output di hello del comando hello:</span><span class="sxs-lookup"><span data-stu-id="e0631-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="e0631-252">Impostare una password radice con guestfish:</span><span class="sxs-lookup"><span data-stu-id="e0631-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="e0631-253">Secondo campo hello modifica dell'utente radice da "."</span><span class="sxs-lookup"><span data-stu-id="e0631-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="e0631-254">password crittografata toohello.</span><span class="sxs-lookup"><span data-stu-id="e0631-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="e0631-255">Creare una macchina virtuale KVM dall'immagine qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="e0631-256">Impostare il tipo di disco hello troppo**qcow2**e impostare modello dispositivo dell'interfaccia di rete virtuale hello troppo**virtio**.</span><span class="sxs-lookup"><span data-stu-id="e0631-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="e0631-257">Quindi, avviare la macchina virtuale hello e accedere come radice.</span><span class="sxs-lookup"><span data-stu-id="e0631-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="e0631-258">Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="e0631-259">Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="e0631-260">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="e0631-261">Registrare l'installazione di tooenable Red Hat sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="e0631-262">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0631-263">toodo questa configurazione, aprire `/etc/default/grub` in un editor di testo e modifica hello `GRUB_CMDLINE_LINUX` parametro.</span><span class="sxs-lookup"><span data-stu-id="e0631-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="e0631-264">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e0631-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="e0631-265">Questo comando assicura anche che tutti i messaggi della console sono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e0631-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e0631-266">comando Hello disattiva anche hello nuove RHEL 7 convenzioni di denominazione per le schede NIC.</span><span class="sxs-lookup"><span data-stu-id="e0631-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="e0631-267">Inoltre, è consigliabile rimuovere hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e0631-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="e0631-268">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="e0631-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0631-269">È possibile lasciare hello `crashkernel` opzione configurato se si desidera.</span><span class="sxs-lookup"><span data-stu-id="e0631-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0631-270">Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.</span><span class="sxs-lookup"><span data-stu-id="e0631-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="e0631-271">Dopo avere completato modifica `/etc/default/grub`eseguire hello seguenti comando toorebuild hello grub configurazione:</span><span class="sxs-lookup"><span data-stu-id="e0631-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="e0631-272">Aggiungere i moduli Hyper-V in initramfs.</span><span class="sxs-lookup"><span data-stu-id="e0631-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="e0631-273">Modificare `/etc/dracut.conf` e aggiungere il contenuto:</span><span class="sxs-lookup"><span data-stu-id="e0631-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="e0631-274">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0631-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="e0631-275">Disinstallare cloud-init:</span><span class="sxs-lookup"><span data-stu-id="e0631-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="e0631-276">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio:</span><span class="sxs-lookup"><span data-stu-id="e0631-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="e0631-277">Modificare /etc/ssh/sshd_config tooinclude hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="e0631-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="e0631-278">pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0631-279">Abilitare repository extra hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="e0631-280">Installare l'agente Linux di Azure hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="e0631-281">Abilitare il servizio waagent hello:</span><span class="sxs-lookup"><span data-stu-id="e0631-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="e0631-282">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0631-283">Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0631-284">Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e0631-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0631-285">Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in `/etc/waagent.conf` in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="e0631-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="e0631-286">Annullare la registrazione hello sottoscrizione (se necessario) eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="e0631-287">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="e0631-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="e0631-288">Spegnere la macchina virtuale hello KVM.</span><span class="sxs-lookup"><span data-stu-id="e0631-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="e0631-289">Convertire il formato VHD toohello di hello qcow2 immagine.</span><span class="sxs-lookup"><span data-stu-id="e0631-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="e0631-290">Prima di convertire formato tooraw di hello immagine:</span><span class="sxs-lookup"><span data-stu-id="e0631-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="e0631-291">Assicurarsi che le dimensioni di hello dell'immagine non elaborati di hello sono allineata con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0631-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="e0631-292">In caso contrario, l'arrotondamento per eccesso hello dimensioni tooalign con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="e0631-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="e0631-293">Convertire hello disco raw tooa dimensione fissa disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="e0631-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="e0631-294">Preparare una macchina virtuale basata su Red Hat da VMware</span><span class="sxs-lookup"><span data-stu-id="e0631-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="e0631-295">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e0631-295">Prerequisites</span></span>
<span data-ttu-id="e0631-296">In questa sezione si presuppone che una macchina virtuale RHEL sia già stata installata in VMware.</span><span class="sxs-lookup"><span data-stu-id="e0631-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="e0631-297">Per informazioni dettagliate su come tooinstall un sistema operativo in VMware, vedere [Guida all'installazione di sistema operativo Guest VMware](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="e0631-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="e0631-298">Quando si installa hello del sistema operativo Linux, è consigliabile utilizzare partizioni standard anziché LVM, è spesso predefinito hello per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="e0631-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="e0631-299">Questo modo si evita i conflitti di nome LVM con macchina virtuale clonata, in particolare se un disco del sistema operativo necessaria macchina virtuale di tooanother toobe associata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e0631-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="e0631-300">Se si preferisce, su dischi di dati si può usare LVM o RAID.</span><span class="sxs-lookup"><span data-stu-id="e0631-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="e0631-301">Non si configura una partizione di scambio su disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="e0631-302">È possibile configurare hello Linux agente toocreate un file di swapping sul disco di risorse temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="e0631-303">È possibile trovare ulteriori informazioni su questo nei passaggi hello che seguono.</span><span class="sxs-lookup"><span data-stu-id="e0631-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="e0631-304">Quando si crea il disco rigido virtuale di hello, selezionare **disco virtuale di archivio come un singolo file**.</span><span class="sxs-lookup"><span data-stu-id="e0631-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="e0631-305">Preparare una macchina virtuale RHEL 6 da VMware</span><span class="sxs-lookup"><span data-stu-id="e0631-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="e0631-306">RHEL 6, NetworkManager può interferire con l'agente Linux di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="e0631-307">Disinstallazione di questo pacchetto eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="e0631-308">Creare un file denominato **rete** hello /etc/hosts sysconfig/directory che contiene hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="e0631-309">Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="e0631-310">Spostare o rimuovere hello udev regole tooavoid la generazione di regole statiche per l'interfaccia Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="e0631-311">Le regole seguenti causano problemi quando si clona una macchina virtuale in Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0631-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="e0631-312">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="e0631-313">Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="e0631-314">pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0631-315">Abilitare repository extra hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="e0631-316">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0631-317">toodo, aprire `/etc/default/grub` in un editor di testo e modifica hello `GRUB_CMDLINE_LINUX` parametro.</span><span class="sxs-lookup"><span data-stu-id="e0631-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="e0631-318">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e0631-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="e0631-319">Questa operazione garantisce inoltre che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e0631-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e0631-320">Inoltre, è consigliabile rimuovere hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e0631-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="e0631-321">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="e0631-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0631-322">È possibile lasciare hello `crashkernel` opzione configurato se si desidera.</span><span class="sxs-lookup"><span data-stu-id="e0631-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0631-323">Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.</span><span class="sxs-lookup"><span data-stu-id="e0631-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="e0631-324">Aggiungere tooinitramfs moduli Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="e0631-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="e0631-325">Modifica `/etc/dracut.conf`e aggiungere hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="e0631-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="e0631-326">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0631-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="e0631-327">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio, è in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="e0631-328">Modificare `/etc/ssh/sshd_config` hello tooinclude seguente riga:</span><span class="sxs-lookup"><span data-stu-id="e0631-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="e0631-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="e0631-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="e0631-330">Installare l'agente Linux di Azure hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="e0631-331">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0631-332">Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0631-333">Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e0631-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0631-334">Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in `/etc/waagent.conf` in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="e0631-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="e0631-335">Annullare la registrazione hello sottoscrizione (se necessario) eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="e0631-336">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="e0631-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="e0631-337">Spegnere la macchina virtuale hello e convertire i file con estensione vhd tooa file VMDK hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="e0631-338">Prima di convertire formato tooraw di hello immagine:</span><span class="sxs-lookup"><span data-stu-id="e0631-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="e0631-339">Assicurarsi che le dimensioni di hello dell'immagine non elaborati di hello sono allineata con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0631-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="e0631-340">In caso contrario, l'arrotondamento per eccesso hello dimensioni tooalign con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="e0631-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="e0631-341">Convertire hello disco raw tooa dimensione fissa disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="e0631-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="e0631-342">Preparare una macchina virtuale RHEL 7 da VMware</span><span class="sxs-lookup"><span data-stu-id="e0631-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="e0631-343">Creare o modificare hello `/etc/sysconfig/network` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="e0631-344">Creare o modificare hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file e aggiungere hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="e0631-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="e0631-345">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="e0631-346">Registrare l'installazione di hello Red Hat tooenable sottoscrizione dei pacchetti dal repository RHEL hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="e0631-347">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="e0631-348">toodo questa modifica, aprirla `/etc/default/grub` in un editor di testo e modifica hello `GRUB_CMDLINE_LINUX` parametro.</span><span class="sxs-lookup"><span data-stu-id="e0631-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="e0631-349">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e0631-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="e0631-350">Questa configurazione assicura anche che tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e0631-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="e0631-351">Disattiva anche hello nuove RHEL 7 convenzioni di denominazione per le schede NIC.</span><span class="sxs-lookup"><span data-stu-id="e0631-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="e0631-352">Inoltre, è consigliabile rimuovere hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="e0631-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="e0631-353">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="e0631-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="e0631-354">È possibile lasciare hello `crashkernel` opzione configurato se si desidera.</span><span class="sxs-lookup"><span data-stu-id="e0631-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="e0631-355">Si noti che questo parametro consente di ridurre hello quantità di memoria disponibile nella macchina virtuale hello da 128 MB o più, che potrebbero essere problematici in macchine virtuali di dimensioni più piccole.</span><span class="sxs-lookup"><span data-stu-id="e0631-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="e0631-356">Dopo avere completato modifica `/etc/default/grub`eseguire hello seguenti comando toorebuild hello grub configurazione:</span><span class="sxs-lookup"><span data-stu-id="e0631-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="e0631-357">Aggiungere tooinitramfs moduli Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0631-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="e0631-358">Modificare `/etc/dracut.conf`e aggiungere il contenuto:</span><span class="sxs-lookup"><span data-stu-id="e0631-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="e0631-359">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0631-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="e0631-360">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="e0631-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="e0631-361">Questa impostazione viene in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-361">This setting is usually hello default.</span></span> <span data-ttu-id="e0631-362">Modificare `/etc/ssh/sshd_config` hello tooinclude seguente riga:</span><span class="sxs-lookup"><span data-stu-id="e0631-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="e0631-363">pacchetto WALinuxAgent Hello, `WALinuxAgent-<version>`, è stato inserito repository di funzionalità aggiuntive di toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="e0631-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="e0631-364">Abilitare repository extra hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="e0631-365">Installare l'agente Linux di Azure hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="e0631-366">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="e0631-367">Hello agente Linux di Azure è possibile configurare lo spazio di swapping automaticamente utilizzando il disco di risorsa locale hello di macchina virtuale associata toohello dopo il provisioning della macchina virtuale hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="e0631-368">Si noti che il disco di risorsa locale hello è un disco temporaneo e potrebbe essere stata svuotata quando la macchina virtuale di hello è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e0631-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="e0631-369">Dopo aver installato l'agente Linux di Azure hello nel passaggio precedente hello, modificare hello seguenti parametri in `/etc/waagent.conf` in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="e0631-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="e0631-370">Se si desidera che toounregister hello sottoscrizione, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0631-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="e0631-371">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="e0631-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="e0631-372">Spegnere la macchina virtuale hello e convertire il formato VHD toohello di hello VMDK file.</span><span class="sxs-lookup"><span data-stu-id="e0631-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="e0631-373">Prima di convertire formato tooraw di hello immagine:</span><span class="sxs-lookup"><span data-stu-id="e0631-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="e0631-374">Assicurarsi che le dimensioni di hello dell'immagine non elaborati di hello sono allineata con 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e0631-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="e0631-375">In caso contrario, l'arrotondamento per eccesso hello dimensioni tooalign con 1 MB:</span><span class="sxs-lookup"><span data-stu-id="e0631-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="e0631-376">Convertire hello disco raw tooa dimensione fissa disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="e0631-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="e0631-377">Preparare una macchina virtuale basata su Red Hat da un'immagine ISO usando un file kickstart automatico</span><span class="sxs-lookup"><span data-stu-id="e0631-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="e0631-378">Preparare una macchina virtuale RHEL 7 da un file kickstart</span><span class="sxs-lookup"><span data-stu-id="e0631-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="e0631-379">Creare un file di sviluppare un che include hello dopo contenuto e salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="e0631-380">Per informazioni dettagliate sull'installazione di sviluppare un, vedere hello [Guida all'installazione di sviluppare un](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="e0631-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

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

2. <span data-ttu-id="e0631-381">Posizionare i file di sviluppare un hello in sistema installazione hello può accedervi.</span><span class="sxs-lookup"><span data-stu-id="e0631-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="e0631-382">Creare una nuova macchina virtuale nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0631-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="e0631-383">In hello **connessione disco rigido virtuale** selezionare **collegare un disco rigido virtuale in un secondo momento**e hello Completamento creazione guidata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0631-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="e0631-384">Aprire impostazioni della macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="e0631-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="e0631-385">a.</span><span class="sxs-lookup"><span data-stu-id="e0631-385">a.</span></span>  <span data-ttu-id="e0631-386">Collegare una nuova macchina virtuale toohello di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0631-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="e0631-387">Verificare che tooselect **formato VHD** e **a dimensione fissa**.</span><span class="sxs-lookup"><span data-stu-id="e0631-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="e0631-388">b.</span><span class="sxs-lookup"><span data-stu-id="e0631-388">b.</span></span>  <span data-ttu-id="e0631-389">Collegare installazione hello unità DVD toohello ISO.</span><span class="sxs-lookup"><span data-stu-id="e0631-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="e0631-390">c.</span><span class="sxs-lookup"><span data-stu-id="e0631-390">c.</span></span>  <span data-ttu-id="e0631-391">Impostare hello BIOS tooboot dal CD-ROM.</span><span class="sxs-lookup"><span data-stu-id="e0631-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="e0631-392">Avviare la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-392">Start hello virtual machine.</span></span> <span data-ttu-id="e0631-393">Quando viene visualizzata la Guida all'installazione hello, premere **scheda** tooconfigure opzioni di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="e0631-394">Invio `inst.ks=<hello location of hello kickstart file>` alla fine di hello delle opzioni di avvio hello e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="e0631-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="e0631-395">Attendere toofinish installazione hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="e0631-396">Al termine, macchina virtuale hello verrà chiuso automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e0631-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="e0631-397">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e0631-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e0631-398">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="e0631-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="e0631-399">driver di Hyper-V Hello potrebbero non essere incluse nel disco RAM iniziale hello quando si utilizza un hypervisor non Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e0631-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="e0631-400">In alcuni casi, i programmi di installazione di Linux potrebbero non includere i driver di hello per Hyper-V in hello iniziale disco RAM (initrd o initramfs), a meno che Linux rileva che è in esecuzione in un ambiente Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e0631-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="e0631-401">Quando si utilizza un tooprepare di sistema (ovvero, Virtualbox, Xen e così via) di virtualizzazione diverso immagine Linux, potrebbe essere necessario toorebuild initrd tooensure che almeno hello hv_vmbus e sono disponibili su disco RAM iniziale hello hv_storvsc kernel moduli.</span><span class="sxs-lookup"><span data-stu-id="e0631-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="e0631-402">Questo è un problema noto almeno nei sistemi basati su distribuzione Red Hat upstream hello.</span><span class="sxs-lookup"><span data-stu-id="e0631-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="e0631-403">tooresolve questo problema, aggiungere tooinitramfs moduli Hyper-V e ricompilarlo:</span><span class="sxs-lookup"><span data-stu-id="e0631-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="e0631-404">Modifica `/etc/dracut.conf`e aggiungere hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="e0631-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="e0631-405">Ricompilare initramfs:</span><span class="sxs-lookup"><span data-stu-id="e0631-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="e0631-406">Per ulteriori informazioni, vedere informazioni hello sul [ricompilazione initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="e0631-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0631-407">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0631-407">Next steps</span></span>
<span data-ttu-id="e0631-408">Si è ora pronto toouse Red Hat Enterprise Linux disco rigido virtuale toocreate nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="e0631-409">Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0631-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="e0631-410">Per ulteriori dettagli su hypervisor hello che sono certificate toorun Red Hat Enterprise Linux, vedere [sito Web di Red Hat hello](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="e0631-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
