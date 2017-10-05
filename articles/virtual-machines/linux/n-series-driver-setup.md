---
title: Installazione di driver per serie N di Azure per Linux | Microsoft Docs
description: Informazioni su come installare driver GPU NVIDIA per macchine virtuali serie N che eseguono Linux in Azure
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bdeb4d5ca1d9ff4d7dfd0961690412dd7530572a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="5acd1-103">Installare i driver GPU NVIDIA in VM serie N che eseguono Linux</span><span class="sxs-lookup"><span data-stu-id="5acd1-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="5acd1-104">Per usufruire delle funzionalità GPU delle VM serie N di Azure che eseguono Linux, installare i driver della scheda grafica NVIDIA supportati.</span><span class="sxs-lookup"><span data-stu-id="5acd1-104">To take advantage of the GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="5acd1-105">Questo articolo descrive la procedura di installazione dei driver dopo la distribuzione di una macchina virtuale serie N.</span><span class="sxs-lookup"><span data-stu-id="5acd1-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="5acd1-106">Le informazioni di configurazione dei driver sono disponibili anche per le [VM Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5acd1-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="5acd1-107">Per conoscere le specifiche, le capacità di archiviazione e i dettagli dei dischi delle macchine virtuali serie N, vedere [Dimensioni delle macchine virtuali Linux GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5acd1-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="5acd1-108">Installare i driver GRID per VM NV</span><span class="sxs-lookup"><span data-stu-id="5acd1-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="5acd1-109">Per installare i driver NVIDIA GRID nelle macchine virtuali NV, stabilire una connessione SSH a ogni macchina virtuale e seguire la procedura per la distribuzione di Linux.</span><span class="sxs-lookup"><span data-stu-id="5acd1-109">To install NVIDIA GRID drivers on NV VMs, make an SSH connection to each VM and follow the steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="5acd1-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="5acd1-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="5acd1-111">Eseguire il comando `lspci`.</span><span class="sxs-lookup"><span data-stu-id="5acd1-111">Run the `lspci` command.</span></span> <span data-ttu-id="5acd1-112">Verificare che la scheda o le schede NVIDIA M60 siano visualizzate come dispositivi PCI.</span><span class="sxs-lookup"><span data-stu-id="5acd1-112">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="5acd1-113">Installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="5acd1-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="5acd1-114">Disabilitare il driver del kernel Nouveau, che è incompatibile con il driver NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="5acd1-114">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="5acd1-115">Nelle macchine virtuali NV usare solo il driver NVIDIA. A tale scopo, creare un file in `/etc/modprobe.d ` denominato `nouveau.conf` con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="5acd1-115">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="5acd1-116">Riavviare la macchina virtuale ed eseguire nuovamente la connessione.</span><span class="sxs-lookup"><span data-stu-id="5acd1-116">Reboot the VM and reconnect.</span></span> <span data-ttu-id="5acd1-117">Uscire dal server X:</span><span class="sxs-lookup"><span data-stu-id="5acd1-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="5acd1-118">Scaricare e installare il driver GRID:</span><span class="sxs-lookup"><span data-stu-id="5acd1-118">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="5acd1-119">Quando viene chiesto se si vuole eseguire l'utilità nvidia-xconfig per aggiornare il file di configurazione di X, selezionare **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="5acd1-119">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="5acd1-120">Al termine dell'installazione, copiare /etc/nvidia/gridd.conf.template in un nuovo file gridd.conf nel percorso /etc/nvidia/</span><span class="sxs-lookup"><span data-stu-id="5acd1-120">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="5acd1-121">Aggiungere quanto segue a `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="5acd1-121">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="5acd1-122">Riavviare la VM e procedere a verificare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="5acd1-122">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="5acd1-123">Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3</span><span class="sxs-lookup"><span data-stu-id="5acd1-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="5acd1-124">Aggiornare il kernel e DKMS.</span><span class="sxs-lookup"><span data-stu-id="5acd1-124">Update the kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="5acd1-125">Disabilitare il driver del kernel Nouveau, che è incompatibile con il driver NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="5acd1-125">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="5acd1-126">Nelle macchine virtuali NV usare solo il driver NVIDIA. A tale scopo, creare un file in `/etc/modprobe.d ` denominato `nouveau.conf` con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="5acd1-126">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="5acd1-127">Riavviare la macchina virtuale e installare i servizi di integrazione di Linux più recenti per Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="5acd1-127">Reboot the VM, reconnect, and install the latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="5acd1-128">Ristabilire la connessione alla macchina virtuale ed eseguire il comando `lspci`.</span><span class="sxs-lookup"><span data-stu-id="5acd1-128">Reconnect to the VM and run the `lspci` command.</span></span> <span data-ttu-id="5acd1-129">Verificare che la scheda o le schede NVIDIA M60 siano visualizzate come dispositivi PCI.</span><span class="sxs-lookup"><span data-stu-id="5acd1-129">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="5acd1-130">Scaricare e installare il driver GRID:</span><span class="sxs-lookup"><span data-stu-id="5acd1-130">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="5acd1-131">Quando viene chiesto se si vuole eseguire l'utilità nvidia-xconfig per aggiornare il file di configurazione di X, selezionare **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="5acd1-131">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="5acd1-132">Al termine dell'installazione, copiare /etc/nvidia/gridd.conf.template in un nuovo file gridd.conf nel percorso /etc/nvidia/</span><span class="sxs-lookup"><span data-stu-id="5acd1-132">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="5acd1-133">Aggiungere quanto segue a `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="5acd1-133">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="5acd1-134">Riavviare la VM e procedere a verificare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="5acd1-134">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="5acd1-135">Verificare l'installazione del driver</span><span class="sxs-lookup"><span data-stu-id="5acd1-135">Verify driver installation</span></span>


<span data-ttu-id="5acd1-136">Per controllare lo stato del dispositivo GPU, eseguire una connessione SSH alla VM ed eseguire l'utilità della riga di comando [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) installata con il driver.</span><span class="sxs-lookup"><span data-stu-id="5acd1-136">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="5acd1-137">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5acd1-137">Output similar to the following appears:</span></span>

![Stato del dispositivo NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="5acd1-139">Server X11</span><span class="sxs-lookup"><span data-stu-id="5acd1-139">X11 server</span></span>
<span data-ttu-id="5acd1-140">Se è necessario un server X11 per le connessioni remote a una macchina virtuale NV, è consigliabile usare [x11vnc](http://www.karlrunge.com/x11vnc/) perché consente l'accelerazione hardware della grafica.</span><span class="sxs-lookup"><span data-stu-id="5acd1-140">If you need an X11 server for remote connections to an NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="5acd1-141">Il BusID del dispositivo M60 deve essere aggiunto manualmente al file xconfig (`etc/X11/xorg.conf` in Ubuntu 16.04 LTS, `/etc/X11/XF86config` in CentOS 7.3 o Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="5acd1-141">The BusID of the M60 device must be manually added to the xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="5acd1-142">Aggiungere una sezione `"Device"` simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="5acd1-142">Add a `"Device"` section similar to the following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="5acd1-143">Aggiornare anche la sezione `"Screen"` per l'uso del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5acd1-143">Additionally, update your `"Screen"` section to use this device.</span></span>
 
<span data-ttu-id="5acd1-144">Per individuare il BusID, eseguire</span><span class="sxs-lookup"><span data-stu-id="5acd1-144">The BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="5acd1-145">Il BusID può cambiare quando una macchina virtuale viene riallocata o riavviata.</span><span class="sxs-lookup"><span data-stu-id="5acd1-145">The BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="5acd1-146">Pertanto, è consigliabile usare uno script per aggiornare il BusID nella configurazione di X11 quando una macchina virtuale viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="5acd1-146">Therefore, you may want to use a script to update the BusID in the X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="5acd1-147">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5acd1-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed to ${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="5acd1-148">Questo file può essere richiamato come radice all'avvio mediante la creazione di una voce in `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="5acd1-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="5acd1-149">Installare i driver CUDA per macchine virtuali NC</span><span class="sxs-lookup"><span data-stu-id="5acd1-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="5acd1-150">Ecco i passaggi per installare i driver NVIDIA nelle VM NC Linux dal Toolkit 8.0 di NVIDIA CUDA.</span><span class="sxs-lookup"><span data-stu-id="5acd1-150">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="5acd1-151">Gli sviluppatori C++ e C possono facoltativamente installare il toolkit completo per creare applicazioni con accelerazione GPU.</span><span class="sxs-lookup"><span data-stu-id="5acd1-151">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span></span> <span data-ttu-id="5acd1-152">Per altre informazioni, vedere la [guida di installazione di CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="5acd1-152">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="5acd1-153">I collegamenti ai download dei driver CUDA forniti qui sono quelli attivi al momento della pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="5acd1-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="5acd1-154">Per i driver CUDA più aggiornati, visitare il sito Web [NVIDIA](http://www.nvidia.com/).</span><span class="sxs-lookup"><span data-stu-id="5acd1-154">For the latest CUDA drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="5acd1-155">Per installare il toolkit di CUDA, eseguire una connessione SSH a ciascuna VM.</span><span class="sxs-lookup"><span data-stu-id="5acd1-155">To install CUDA Toolkit, make an SSH connection to each VM.</span></span> <span data-ttu-id="5acd1-156">Per verificare che nel sistema sia presente una GPU con supporto per core CUDA, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5acd1-156">To verify that the system has a CUDA-capable GPU, run the following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="5acd1-157">Verrà visualizzato un output simile all'esempio seguente (che rappresenta una scheda NVIDIA Tesla K80):</span><span class="sxs-lookup"><span data-stu-id="5acd1-157">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span></span>

![Output del comando Ispci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="5acd1-159">Quindi eseguire i comandi di installazione specifici per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5acd1-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="5acd1-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="5acd1-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="5acd1-161">Scaricare e installare i driver CUDA.</span><span class="sxs-lookup"><span data-stu-id="5acd1-161">Download and install the CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="5acd1-162">L'installazione può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="5acd1-162">The installation can take several minutes.</span></span>

2. <span data-ttu-id="5acd1-163">Per installare facoltativamente il toolkit di CUDA completo, digitare:</span><span class="sxs-lookup"><span data-stu-id="5acd1-163">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="5acd1-164">Riavviare la VM e procedere a verificare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="5acd1-164">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="5acd1-165">Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3</span><span class="sxs-lookup"><span data-stu-id="5acd1-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="5acd1-166">Ottenere gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="5acd1-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="5acd1-167">Ristabilire la connessione alla macchina virtuale e installare i Linux Integration Services più recenti per Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="5acd1-167">Reconnect to the VM and install the latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5acd1-168">Se è installata un'immagine HPC basata su CentOS in una macchina virtuale NC24r, andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="5acd1-168">If you installed a CentOS-based HPC image on an NC24r VM, skip to Step 3.</span></span> <span data-ttu-id="5acd1-169">Poiché i driver RDMA di Azure e Linux Integration Services sono pre-installati nell'immagine, non è necessario aggiornare i servizi LIS e gli aggiornamenti del kernel sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5acd1-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in the image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="5acd1-170">Riconnettersi alla macchina virtuale e continuare l'installazione con i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5acd1-170">Reconnect to the VM and continue installation with the following commands:</span></span>

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  <span data-ttu-id="5acd1-171">L'installazione può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="5acd1-171">The installation can take several minutes.</span></span> 

4. <span data-ttu-id="5acd1-172">Per installare facoltativamente il toolkit di CUDA completo, digitare:</span><span class="sxs-lookup"><span data-stu-id="5acd1-172">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="5acd1-173">Riavviare la VM e procedere a verificare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="5acd1-173">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="5acd1-174">Verificare l'installazione del driver</span><span class="sxs-lookup"><span data-stu-id="5acd1-174">Verify driver installation</span></span>


<span data-ttu-id="5acd1-175">Per controllare lo stato del dispositivo GPU, eseguire una connessione SSH alla VM ed eseguire l'utilità della riga di comando [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) installata con il driver.</span><span class="sxs-lookup"><span data-stu-id="5acd1-175">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="5acd1-176">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5acd1-176">Output similar to the following appears:</span></span>

![Stato del dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="5acd1-178">Aggiornamenti dei driver CUDA</span><span class="sxs-lookup"><span data-stu-id="5acd1-178">CUDA driver updates</span></span>

<span data-ttu-id="5acd1-179">È consigliabile aggiornare periodicamente i driver CUDA dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5acd1-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="5acd1-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="5acd1-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="5acd1-181">Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3</span><span class="sxs-lookup"><span data-stu-id="5acd1-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="5acd1-182">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="5acd1-182">Troubleshooting</span></span>

* <span data-ttu-id="5acd1-183">Esiste un problema noto con i driver CUDA sulle macchine virtuali serie N di Azure che eseguono il kernel Linux 4.4.0-75 su Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="5acd1-183">There is a known issue with CUDA drivers on Azure N-series VMs running the 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="5acd1-184">Se si usa una versione precedente del kernel, eseguire l'aggiornamento almeno alla versione 4.4.0-77.</span><span class="sxs-lookup"><span data-stu-id="5acd1-184">If you are upgrading from an earlier kernel version, upgrade to at least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="5acd1-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5acd1-185">Next steps</span></span>

* <span data-ttu-id="5acd1-186">Per altre informazioni sulle GPU NVIDIA nelle macchine virtuali serie N, vedere:</span><span class="sxs-lookup"><span data-stu-id="5acd1-186">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="5acd1-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (per VM NC Azure)</span><span class="sxs-lookup"><span data-stu-id="5acd1-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="5acd1-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (per macchine virtuali NC di Azure)</span><span class="sxs-lookup"><span data-stu-id="5acd1-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="5acd1-189">Se si intende acquisire un'immagine di una VM Linux in cui sono installati driver NVIDIA, vedere [Come generalizzare e acquisire una macchina virtuale Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5acd1-189">To capture a Linux VM image with your installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
