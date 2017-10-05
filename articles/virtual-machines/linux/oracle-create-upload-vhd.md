---
title: Creazione e caricamento di un VHD Oracle Linux | Microsoft Docs
description: Informazioni su come creare e caricare un disco rigido virtuale (VHD) di Azure che contiene un sistema operativo Oracle Linux.
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
ms.openlocfilehash: c631ddf3acf6df7364c03eb4691b78be0493e0d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="58aad-103">Preparare una macchina virtuale Oracle Linux per Azure</span><span class="sxs-lookup"><span data-stu-id="58aad-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="58aad-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="58aad-104">Prerequisites</span></span>
<span data-ttu-id="58aad-105">In questo articolo si presuppone che l'utente abbia già installato un sistema operativo Oracle Linux in un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="58aad-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="58aad-106">Sono disponibili vari strumenti per creare file con estensione vhd, ad esempio una soluzione di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="58aad-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="58aad-107">Per istruzioni, vedere [Installare il ruolo Hyper-V e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="58aad-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="58aad-108">Note generali sull'installazione di Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="58aad-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="58aad-109">Vedere anche [Note generali sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per altri suggerimenti sulla preparazione di Linux per Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="58aad-110">Il kernel compatibile con Red Hat di Oracle e i relativi UEK3 (Unbreakable Enterprise Kernel) sono supportati sia su Hyper-V sia su Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="58aad-111">Per ottenere i migliori risultati, assicurarsi di eseguire l'aggiornamento al kernel più recente durante la preparazione del VHD Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="58aad-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="58aad-112">UEK2 di Oracle non è supportato su Hyper-V e Azure perché non include i driver necessari.</span><span class="sxs-lookup"><span data-stu-id="58aad-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span></span>
* <span data-ttu-id="58aad-113">Il formato VHDX non è supportato in Azure, solo nei **VHD fissi**.</span><span class="sxs-lookup"><span data-stu-id="58aad-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="58aad-114">È possibile convertire il disco in formato VHD tramite la console di gestione di Hyper-V o il cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="58aad-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="58aad-115">Durante l'installazione del sistema operativo Linux è consigliabile usare partizioni standard anziché LVM, che spesso è la scelta predefinita per numerose installazioni.</span><span class="sxs-lookup"><span data-stu-id="58aad-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="58aad-116">In questo modo sarà possibile evitare conflitti di nome LVM con le macchine virtuali clonate, in particolare se fosse necessario collegare un disco del sistema operativo a un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="58aad-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="58aad-117">Se si preferisce, su dischi di dati si può usare [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58aad-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="58aad-118">NUMA non è supportato per macchine virtuali di dimensioni maggiori a causa di un bug presente nelle versioni del kernel di Linux inferiori a 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="58aad-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="58aad-119">Questo problema incide principalmente sulle distribuzioni che utilizzano il kernel upstream Red Hat 2.6.32.</span><span class="sxs-lookup"><span data-stu-id="58aad-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="58aad-120">L'installazione manuale dell'agente Linux di Azure (waagent) disabiliterà automaticamente NUMA nella configurazione GRUB per il kernel Linux.</span><span class="sxs-lookup"><span data-stu-id="58aad-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span></span> <span data-ttu-id="58aad-121">Altre informazioni su questo argomento sono disponibili nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="58aad-121">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="58aad-122">Non configurare una partizione swap nel disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="58aad-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="58aad-123">L'agente Linux può essere configurato in modo da creare un file swap sul disco temporaneo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="58aad-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="58aad-124">Altre informazioni su questo argomento sono disponibili nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="58aad-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="58aad-125">Tutti i dischi rigidi virtuali devono avere dimensioni multiple di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="58aad-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="58aad-126">Verificare che il repository `Addons` sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="58aad-126">Make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="58aad-127">Modificare il file `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux 6) o `enabled=0`(Oracle Linux ) e cambiare la riga `enabled=1` in **in `/etc/yum.repo.d/public-yum-ol6.repo`[ol6_addons]** o **[ol7_addons]** in questo file.</span><span class="sxs-lookup"><span data-stu-id="58aad-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="58aad-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="58aad-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="58aad-129">Per l'esecuzione della macchina virtuale in Azure è necessario eseguire specifici passaggi di configurazione nel sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="58aad-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span></span>

1. <span data-ttu-id="58aad-130">Nel riquadro centrale della console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58aad-130">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="58aad-131">Fare clic su **Connect** per aprire la finestra della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58aad-131">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="58aad-132">Disinstallare NetworkManager attivando il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="58aad-132">Uninstall NetworkManager by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="58aad-133">**Nota:** se il pacchetto non è già installato, questo comando avrà esito negativo e verrà visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="58aad-133">**Note:** If the package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="58aad-134">Si tratta di un comportamento previsto.</span><span class="sxs-lookup"><span data-stu-id="58aad-134">This is expected.</span></span>
4. <span data-ttu-id="58aad-135">Creare un file denominato **network** in the `/etc/sysconfig/` contenente il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="58aad-136">Creare un file denominato **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` contenente il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="58aad-137">Modificare le regole udev per evitare la generazione di regole statiche per l'interfaccia Ethernet.</span><span class="sxs-lookup"><span data-stu-id="58aad-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="58aad-138">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="58aad-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="58aad-139">Assicurarsi che il servizio di rete venga eseguito all'avvio eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-139">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="58aad-140">Installare python-pyasn1 eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-140">Install python-pyasn1 by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="58aad-141">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="58aad-142">A questo scopo, aprire "/boot/grub/menu.lst" in un editor di testo e verificare che il kernel predefinito includa i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="58aad-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="58aad-143">In questo modo si garantisce inoltre che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="58aad-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="58aad-144">Verrà disabilitato NUMA, a causa di un bug nel kernel compatibile con Red Hat di Oracle.</span><span class="sxs-lookup"><span data-stu-id="58aad-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="58aad-145">Inoltre, è consigliabile *rimuovere* i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="58aad-145">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="58aad-146">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="58aad-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="58aad-147">L'opzione `crashkernel` può essere configurata, ma si tenga presente che questo parametro ridurrà la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB, il che potrebbe causare problemi con le macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="58aad-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="58aad-148">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="58aad-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="58aad-149">Questo è in genere il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="58aad-149">This is usually the default.</span></span>
11. <span data-ttu-id="58aad-150">Installare l'agente Linux di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-150">Install the Azure Linux Agent by running the following command.</span></span> <span data-ttu-id="58aad-151">La versione più recente è la 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="58aad-151">The latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="58aad-152">Si noti che, installando il pacchetto WALinuxAgent, i pacchetti NetworkManager e NetworkManager-gnome verranno rimossi, se l'operazione non è già stata eseguita come descritto nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="58aad-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="58aad-153">Non creare l'area di swap sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="58aad-153">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="58aad-154">L'agente Linux di Azure può configurare automaticamente l'area di swap utilizzando il disco risorse locale collegato alla VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="58aad-155">Si noti che il disco risorse locale è un disco *temporaneo* e potrebbe essere svuotato in seguito al deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58aad-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="58aad-156">Dopo aver installato l'agente Linux di Azure come illustrato nel passaggio precedente, modificare i parametri seguenti in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="58aad-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
13. <span data-ttu-id="58aad-157">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="58aad-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="58aad-158">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="58aad-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="58aad-159">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-159">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="58aad-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="58aad-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="58aad-161">**Modifiche in Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="58aad-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="58aad-162">La preparazione di una macchina virtuale Oracle Linux 7 per Azure è molto simile a Oracle Linux 6, tuttavia vi sono alcune importanti differenze da notare:</span><span class="sxs-lookup"><span data-stu-id="58aad-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="58aad-163">Sia il kernel compatibile con Red Hat di Oracle sia UEK3 di Oracle sono supportati in Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="58aad-164">È consigliato il kernel UEK3.</span><span class="sxs-lookup"><span data-stu-id="58aad-164">The UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="58aad-165">Il pacchetto NetworkManager e l'agente Linux di Azure non sono più in conflitto.</span><span class="sxs-lookup"><span data-stu-id="58aad-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="58aad-166">Questo pacchetto viene installato per impostazione predefinita ed è consigliabile non rimuoverlo.</span><span class="sxs-lookup"><span data-stu-id="58aad-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="58aad-167">GRUB2 viene ora usato come bootloader predefinito, quindi la procedura per la modifica dei parametri kernel è cambiata (vedere di seguito).</span><span class="sxs-lookup"><span data-stu-id="58aad-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="58aad-168">XFS è ora il file system predefinito.</span><span class="sxs-lookup"><span data-stu-id="58aad-168">XFS is now the default file system.</span></span> <span data-ttu-id="58aad-169">Se si vuole, è ancora possibile usare il file system ext4.</span><span class="sxs-lookup"><span data-stu-id="58aad-169">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="58aad-170">**Procedura di configurazione**</span><span class="sxs-lookup"><span data-stu-id="58aad-170">**Configuration steps**</span></span>

1. <span data-ttu-id="58aad-171">Nella console di gestione di Hyper-V selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58aad-171">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="58aad-172">Fare clic su **Connetti** per aprire una finestra della console per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58aad-172">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="58aad-173">Creare un file denominato **network** in the `/etc/sysconfig/` contenente il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="58aad-174">Creare un file denominato **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` contenente il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="58aad-175">Modificare le regole udev per evitare la generazione di regole statiche per l'interfaccia Ethernet.</span><span class="sxs-lookup"><span data-stu-id="58aad-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="58aad-176">Le regole seguenti possono provocare problemi quando si clona una macchina virtuale in Microsoft Azure o Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="58aad-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="58aad-177">Assicurarsi che il servizio di rete venga eseguito all'avvio eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-177">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="58aad-178">Installare il pacchetto python-pyasn1 eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-178">Install the python-pyasn1 package by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="58aad-179">Eseguire il comando seguente per cancellare i metadati yum correnti e installare eventuali aggiornamenti:</span><span class="sxs-lookup"><span data-stu-id="58aad-179">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="58aad-180">Modificare la riga di avvio del kernel nella configurazione GRUB per includere ulteriori parametri del kernel per Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="58aad-181">A tale scopo, aprire "/etc/default/grub" in un editor di testo e modificare il parametro `GRUB_CMDLINE_LINUX` , ad esempio:</span><span class="sxs-lookup"><span data-stu-id="58aad-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="58aad-182">In questo modo si garantisce inoltre che tutti i messaggi della console vengano inviati alla prima porta seriale, agevolando così il supporto di Azure nella risoluzione dei problemi di debug.</span><span class="sxs-lookup"><span data-stu-id="58aad-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="58aad-183">Disattiva anche nuove convenzioni di denominazione OEL 7 per NIC.</span><span class="sxs-lookup"><span data-stu-id="58aad-183">It also turns off the new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="58aad-184">Inoltre, è consigliabile *rimuovere* i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="58aad-184">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="58aad-185">L'avvio grafico e l'avvio silenzioso non sono utili in un ambiente cloud se tutti i log devono essere inviati alla porta seriale.</span><span class="sxs-lookup"><span data-stu-id="58aad-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="58aad-186">L'opzione `crashkernel` può essere configurata, ma si tenga presente che questo parametro ridurrà la quantità di memoria disponibile nella macchina virtuale di almeno 128 MB, il che potrebbe causare problemi con le macchine virtuali di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="58aad-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="58aad-187">Dopo aver terminato di modificare "/etc/default/grub" come sopra illustrato, eseguire il comando seguente per ricompilare la configurazione GRUB:</span><span class="sxs-lookup"><span data-stu-id="58aad-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="58aad-188">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="58aad-188">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="58aad-189">Questo è in genere il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="58aad-189">This is usually the default.</span></span>
12. <span data-ttu-id="58aad-190">Installare l'agente Linux di Azure eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="58aad-190">Install the Azure Linux Agent by running the following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="58aad-191">Non creare l'area di swap sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="58aad-191">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="58aad-192">L'agente Linux di Azure può configurare automaticamente l'area di swap utilizzando il disco risorse locale collegato alla VM dopo il provisioning in Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="58aad-193">Si noti che il disco risorse locale è un disco *temporaneo* e potrebbe essere svuotato in seguito al deprovisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58aad-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="58aad-194">Dopo aver installato l'agente Linux di Azure come illustrato nel passaggio precedente, modificare i parametri seguenti in /etc/waagent.conf in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="58aad-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
14. <span data-ttu-id="58aad-195">Eseguire i comandi seguenti per effettuare il deprovisioning della macchina virtuale e prepararla per il provisioning in Azure:</span><span class="sxs-lookup"><span data-stu-id="58aad-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="58aad-196">Fare clic su **Azione -> Arresta** nella console di gestione di Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="58aad-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="58aad-197">Il file VHD Linux è ora pronto per il caricamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-197">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58aad-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58aad-198">Next steps</span></span>
<span data-ttu-id="58aad-199">È ora possibile usare il file con estensione vhd Oracle Linux per creare nuove macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="58aad-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span></span> <span data-ttu-id="58aad-200">Se è la prima volta che si carica il file VHD in Azure, vedere i passaggi 2 e 3 nell'articolo [Creazione e caricamento di un disco rigido virtuale che contiene il sistema operativo Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58aad-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

