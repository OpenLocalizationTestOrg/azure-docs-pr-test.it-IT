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
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="859c4-103">Preparare una macchina virtuale Oracle Linux per Azure</span><span class="sxs-lookup"><span data-stu-id="859c4-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="859c4-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="859c4-104">Prerequisites</span></span>
<span data-ttu-id="859c4-105">Questo articolo si presuppone che un Oracle Linux del sistema operativo tooa disco virtuale è già stato installato.</span><span class="sxs-lookup"><span data-stu-id="859c4-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="859c4-106">Più strumenti esistono toocreate file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="859c4-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="859c4-107">Per istruzioni, vedere [hello ruolo Hyper-V di installare e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="859c4-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="859c4-108">Note generali sull'installazione di Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="859c4-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="859c4-109">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="859c4-110">Il kernel compatibile con Red Hat di Oracle e i relativi UEK3 (Unbreakable Enterprise Kernel) sono supportati sia su Hyper-V sia su Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="859c4-111">Per ottenere risultati ottimali, essere tooupdate che toohello più recente kernel durante la preparazione del disco rigido virtuale di Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="859c4-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="859c4-112">UEK2 Oracle non è supportata in Hyper-V e Azure che non includa i driver necessario hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="859c4-113">formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.</span><span class="sxs-lookup"><span data-stu-id="859c4-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="859c4-114">È possibile convertire il formato hello disco tooVHD con gestione Hyper-V o hello cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="859c4-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="859c4-115">Quando si installa il sistema di Linux hello è consigliabile utilizzare partizioni standard anziché LVM (spesso predefinito hello per numerose installazioni).</span><span class="sxs-lookup"><span data-stu-id="859c4-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="859c4-116">Questo modo si evita i conflitti di nome LVM con macchine virtuali clonate, in particolare se un sistema operativo disco mai necessario tooanother toobe collegato VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="859c4-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="859c4-117">Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="859c4-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="859c4-118">NUMA, non è supportato per dimensioni maggiori di macchina virtuale a causa di tooa bug nelle versioni di kernel Linux sotto 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="859c4-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="859c4-119">Questo problema influisce principalmente sul distribuzioni usando hello rosso a monte kernel 2.6.32 Hat.</span><span class="sxs-lookup"><span data-stu-id="859c4-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="859c4-120">Installazione manuale dell'agente Linux di Azure hello (waagent) disabilita automaticamente NUMA nella configurazione di GRUB hello per kernel Linux hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="859c4-121">Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="859c4-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="859c4-122">Non si configura una partizione di scambio su disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="859c4-123">agente Linux di Hello può essere configurato toocreate un file di swapping sul disco di risorse temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="859c4-124">Ulteriori informazioni su questo sono reperibile in passaggi hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="859c4-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="859c4-125">Tutti i dischi rigidi virtuali hello devono avere dimensioni che sono multipli di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="859c4-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="859c4-126">Verificare che tale hello `Addons` repository è abilitato.</span><span class="sxs-lookup"><span data-stu-id="859c4-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="859c4-127">Modificare il file hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) e modificare la riga hello `enabled=0` troppo`enabled=1` in **[ol6_addons]** o **[ol7_addons]** in questo file.</span><span class="sxs-lookup"><span data-stu-id="859c4-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="859c4-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="859c4-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="859c4-129">È necessario completare i passaggi di configurazione specifici nel sistema operativo hello per hello toorun di macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="859c4-130">Nel riquadro centrale di hello di gestione di Hyper-V, selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="859c4-131">Fare clic su **Connetti** finestra hello tooopen per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="859c4-132">Disinstallare NetworkManager eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="859c4-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="859c4-133">**Nota:** se il pacchetto di hello non è già installato, questo comando avrà esito negativo con un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="859c4-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="859c4-134">Si tratta di un comportamento previsto.</span><span class="sxs-lookup"><span data-stu-id="859c4-134">This is expected.</span></span>
4. <span data-ttu-id="859c4-135">Creare un file denominato **rete** in hello `/etc/sysconfig/` directory che contiene hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="859c4-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="859c4-136">Creare un file denominato **ifcfg eth0** in hello `/etc/sysconfig/network-scripts/` directory che contiene hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="859c4-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="859c4-137">Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet.</span><span class="sxs-lookup"><span data-stu-id="859c4-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="859c4-138">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="859c4-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="859c4-139">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="859c4-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="859c4-140">Installare python pyasn1 eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="859c4-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="859c4-141">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="859c4-142">aprire questo toodo "/ boot/grub/menu.lst" in un editor di testo e assicurarsi che kernel predefinito hello includa hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="859c4-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="859c4-143">In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="859c4-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="859c4-144">NUMA verrà disabilitato a causa di bug tooa nel kernel di Oracle Red Hat compatibile.</span><span class="sxs-lookup"><span data-stu-id="859c4-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="859c4-145">Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="859c4-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="859c4-146">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="859c4-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="859c4-147">Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="859c4-148">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="859c4-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="859c4-149">Si tratta in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-149">This is usually hello default.</span></span>
11. <span data-ttu-id="859c4-150">Installare l'agente Linux di Azure hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="859c4-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="859c4-151">la versione più recente di Hello è 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="859c4-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="859c4-152">Si noti che l'installazione pacchetto WALinuxAgent di hello rimuoverà hello NetworkManager pacchetti NetworkManager gnome se non sono stati già rimossi come descritto nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="859c4-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="859c4-153">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="859c4-154">Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="859c4-155">Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="859c4-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="859c4-156">Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="859c4-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="859c4-157">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="859c4-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="859c4-158">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="859c4-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="859c4-159">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="859c4-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="859c4-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="859c4-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="859c4-161">**Modifiche in Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="859c4-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="859c4-162">Preparazione di una macchina virtuale di Oracle Linux 7 per Azure è molto simile tooOracle Linux 6, esistono tuttavia alcune differenze importanti non degni di nota:</span><span class="sxs-lookup"><span data-stu-id="859c4-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="859c4-163">In modalità kernel compatibile di hello Red Hat e UEK3 Oracle sono supportate in Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="859c4-164">è consigliabile kernel UEK3 Hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="859c4-165">Hello NetworkManager del pacchetto non è in conflitto con l'agente Linux di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="859c4-166">Questo pacchetto viene installato per impostazione predefinita ed è consigliabile non rimuoverlo.</span><span class="sxs-lookup"><span data-stu-id="859c4-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="859c4-167">GRUB2 viene utilizzato come hello del caricatore di avvio predefinito, in modo procedure hello per la modifica di parametri del kernel è stato modificato (vedere sotto).</span><span class="sxs-lookup"><span data-stu-id="859c4-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="859c4-168">XFS è file system predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-168">XFS is now hello default file system.</span></span> <span data-ttu-id="859c4-169">Hello ext4 file sistema può comunque essere utilizzato se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="859c4-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="859c4-170">**Procedura di configurazione**</span><span class="sxs-lookup"><span data-stu-id="859c4-170">**Configuration steps**</span></span>

1. <span data-ttu-id="859c4-171">Nella console di gestione Hyper-V selezionare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="859c4-172">Fare clic su **Connetti** tooopen una finestra della console per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="859c4-173">Creare un file denominato **rete** in hello `/etc/sysconfig/` directory che contiene hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="859c4-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="859c4-174">Creare un file denominato **ifcfg eth0** in hello `/etc/sysconfig/network-scripts/` directory che contiene hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="859c4-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="859c4-175">Modificare udev regole tooavoid la generazione di regole statiche per hello interfacce Ethernet.</span><span class="sxs-lookup"><span data-stu-id="859c4-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="859c4-176">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="859c4-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="859c4-177">Verificare che il servizio di rete hello inizierà in fase di avvio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="859c4-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="859c4-178">Installare il pacchetto di python pyasn1 hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="859c4-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="859c4-179">Eseguire hello successivo comando tooclear hello corrente yum metadati e installare eventuali aggiornamenti:</span><span class="sxs-lookup"><span data-stu-id="859c4-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="859c4-180">Modificare i parametri di kernel aggiuntive tooinclude grub hello kernel avvio riga per Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="859c4-181">toodo questo aprire "/ e così via/predefinito/grub" in un hello editor e la modifica del testo `GRUB_CMDLINE_LINUX` parametro, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="859c4-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="859c4-182">In questo modo anche tutti i messaggi della console vengono inviati toohello prima porta seriale, che consentono di Azure supporto con il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="859c4-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="859c4-183">Disattiva anche hello nuove OEL 7 convenzioni di denominazione per le schede NIC.</span><span class="sxs-lookup"><span data-stu-id="859c4-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="859c4-184">Inoltre toohello precedente, è consigliabile troppo*rimuovere* hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="859c4-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="859c4-185">Avvio con interfaccia grafica e non interattiva non sono utili in un ambiente cloud in cui si desidera tutti toobe di registri hello inviati toohello della porta seriale.</span><span class="sxs-lookup"><span data-stu-id="859c4-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="859c4-186">Hello `crashkernel` opzione può essere configurato se si desidera sinistra, ma si noti che questo parametro consente di ridurre hello quantità di memoria disponibile in hello VM da 128 MB o più, che può essere problematico sulle dimensioni delle macchine Virtuali più piccoli hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="859c4-187">Dopo aver eseguito modifica "/ e così via/predefinito/grub" al precedente, eseguire hello seguente comando toorebuild hello grub configurazione:</span><span class="sxs-lookup"><span data-stu-id="859c4-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="859c4-188">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="859c4-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="859c4-189">Si tratta in genere predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-189">This is usually hello default.</span></span>
12. <span data-ttu-id="859c4-190">Installare l'agente Linux di Azure hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="859c4-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="859c4-191">Non creare lo spazio di swapping sul disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="859c4-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="859c4-192">Hello agente Linux di Azure può configurare automaticamente lo spazio di swapping utilizzando il disco di risorsa locale hello è collegato toohello VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="859c4-193">Si noti il disco di risorsa locale hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="859c4-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="859c4-194">Dopo l'installazione di hello agente Linux di Azure (vedere il passaggio precedente hello), modificare hello seguenti parametri in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="859c4-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="859c4-195">Eseguire hello seguente macchina virtuale di comandi toodeprovision hello e prepararlo per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="859c4-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="859c4-196">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="859c4-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="859c4-197">Il VHD Linux è ora pronto toobe caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="859c4-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="859c4-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="859c4-198">Next steps</span></span>
<span data-ttu-id="859c4-199">Si è ora pronto toouse Oracle Linux con estensione vhd toocreate nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="859c4-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="859c4-200">Se si tratta hello prima volta che si sta caricando tooAzure file con estensione vhd di hello, vedere i passaggi 2 e 3 in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="859c4-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

