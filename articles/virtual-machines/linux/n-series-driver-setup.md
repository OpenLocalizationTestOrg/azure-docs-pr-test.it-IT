---
title: aaaAzure N serie di installazione del driver per Linux | Documenti Microsoft
description: Come tooset i driver GPU NVIDIA per le macchine virtuali serie N che eseguono Linux in Azure
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
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="4b8c7-103">Installare i driver GPU NVIDIA in VM serie N che eseguono Linux</span><span class="sxs-lookup"><span data-stu-id="4b8c7-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="4b8c7-104">tootake le funzionalità GPU hello di N-serie Azure le macchine virtuali che eseguono Linux, installare i driver grafici NVIDIA è supportato.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="4b8c7-105">Questo articolo descrive la procedura di installazione dei driver dopo la distribuzione di una macchina virtuale serie N.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="4b8c7-106">Le informazioni di configurazione dei driver sono disponibili anche per le [VM Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4b8c7-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="4b8c7-107">Per conoscere le specifiche, le capacità di archiviazione e i dettagli dei dischi delle macchine virtuali serie N, vedere [Dimensioni delle macchine virtuali Linux GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4b8c7-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="4b8c7-108">Installare i driver GRID per VM NV</span><span class="sxs-lookup"><span data-stu-id="4b8c7-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="4b8c7-109">i driver di griglia NVIDIA tooinstall nelle macchine virtuali NV, rendere un tooeach connessione SSH VM e seguire i passaggi di hello per le distribuzioni di Linux.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="4b8c7-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4b8c7-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="4b8c7-111">Eseguire hello `lspci` comando.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-111">Run hello `lspci` command.</span></span> <span data-ttu-id="4b8c7-112">Verificare che siano visibili come dispositivi PCI card hello M60 NVIDIA o schede.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="4b8c7-113">Installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="4b8c7-114">Disabilitare i driver del kernel Nouveau hello, che è incompatibili con il driver NVIDIA hello.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="4b8c7-115">(Solo utilizzare driver NVIDIA hello in macchine virtuali non Volatile). toodo, creare un file in `/etc/modprobe.d `denominato `nouveau.conf` con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="4b8c7-116">Riavvio hello macchina virtuale e la riconnessione.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="4b8c7-117">Uscire dal server X:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="4b8c7-118">Scaricare e installare i driver di griglia hello:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="4b8c7-119">Quando viene chiesto se si desidera toorun hello nvidia xconfig utilità tooupdate il file di configurazione di X, selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="4b8c7-120">Al termine dell'installazione, copiare /etc/nvidia/gridd.conf.template tooa nuova gridd.conf file nel percorso /etc/hosts nvidia /</span><span class="sxs-lookup"><span data-stu-id="4b8c7-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="4b8c7-121">Aggiungere il seguente di hello troppo`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="4b8c7-122">Riavviare hello macchina virtuale e continuare l'installazione di hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="4b8c7-123">Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3</span><span class="sxs-lookup"><span data-stu-id="4b8c7-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="4b8c7-124">Aggiornare il kernel hello e DKMS.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="4b8c7-125">Disabilitare i driver del kernel Nouveau hello, che è incompatibili con il driver NVIDIA hello.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="4b8c7-126">(Solo utilizzare driver NVIDIA hello in macchine virtuali non Volatile). toodo, creare un file in `/etc/modprobe.d `denominato `nouveau.conf` con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="4b8c7-127">Riavviare il computer hello macchina virtuale, riconnettersi e installare servizi di integrazione più recenti Linux per Hyper-v: hello</span><span class="sxs-lookup"><span data-stu-id="4b8c7-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="4b8c7-128">Riconnettersi toohello macchina virtuale ed eseguire hello `lspci` comando.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="4b8c7-129">Verificare che siano visibili come dispositivi PCI card hello M60 NVIDIA o schede.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="4b8c7-130">Scaricare e installare i driver di griglia hello:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="4b8c7-131">Quando viene chiesto se si desidera toorun hello nvidia xconfig utilità tooupdate il file di configurazione di X, selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="4b8c7-132">Al termine dell'installazione, copiare /etc/nvidia/gridd.conf.template tooa nuova gridd.conf file nel percorso /etc/hosts nvidia /</span><span class="sxs-lookup"><span data-stu-id="4b8c7-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="4b8c7-133">Aggiungere il seguente di hello troppo`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="4b8c7-134">Riavviare hello macchina virtuale e continuare l'installazione di hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="4b8c7-135">Verificare l'installazione del driver</span><span class="sxs-lookup"><span data-stu-id="4b8c7-135">Verify driver installation</span></span>


<span data-ttu-id="4b8c7-136">tooquery hello dello stato del dispositivo GPU, SSH toohello VM e hello esecuzione [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) utilità della riga di comando installato con il driver hello.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="4b8c7-137">Viene visualizzato il seguente toohello simile di output:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-137">Output similar toohello following appears:</span></span>

![Stato del dispositivo NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="4b8c7-139">Server X11</span><span class="sxs-lookup"><span data-stu-id="4b8c7-139">X11 server</span></span>
<span data-ttu-id="4b8c7-140">Se è necessario un X11 server per le connessioni remote tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) è consigliata perché consente l'accelerazione grafica hardware.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="4b8c7-141">Hello BusID del dispositivo hello M60 deve essere aggiunta manualmente file xconfig toohello (`etc/X11/xorg.conf` in Ubuntu 16.04 LTS, `/etc/X11/XF86config` CentOS 7.3 o Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="4b8c7-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="4b8c7-142">Aggiungere un `"Device"` sezione simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="4b8c7-143">Inoltre, per aggiornare il `"Screen"` sezione toouse questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="4b8c7-144">Hello BusID è reperibile eseguendo</span><span class="sxs-lookup"><span data-stu-id="4b8c7-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="4b8c7-145">Hello BusID può cambiare quando una macchina virtuale Ottiene riallocare o riavviata.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="4b8c7-146">Pertanto, è opportuno toouse un hello tooupdate script BusID nella configurazione hello X11 quando una macchina virtuale è stata riavviata.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="4b8c7-147">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="4b8c7-148">Questo file può essere richiamato come radice all'avvio mediante la creazione di una voce in `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="4b8c7-149">Installare i driver CUDA per macchine virtuali NC</span><span class="sxs-lookup"><span data-stu-id="4b8c7-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="4b8c7-150">Di seguito sono i driver NVIDIA tooinstall passaggi nelle macchine virtuali NC Linux da hello NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="4b8c7-151">Gli sviluppatori di C e C++ è possono installare facoltativamente hello Toolkit toobuild accelerazione GPU applicazioni complete.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="4b8c7-152">Per ulteriori informazioni, vedere hello [Guida all'installazione CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="4b8c7-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="4b8c7-153">I collegamenti ai download dei driver CUDA forniti qui sono quelli attivi al momento della pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="4b8c7-154">Per hello CUDA driver, visitare hello [NVIDIA](http://www.nvidia.com/) sito Web.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="4b8c7-155">tooinstall CUDA Toolkit, rendere un tooeach connessione SSH macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="4b8c7-156">tooverify che hello sistema disponga di una GPU che supporta CUDA, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="4b8c7-157">Si noterà toohello simili di output (rappresentato da una scheda NVIDIA Tesla R80) di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![Output del comando Ispci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="4b8c7-159">Quindi eseguire i comandi di installazione specifici per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="4b8c7-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4b8c7-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="4b8c7-161">Scaricare e installare i driver CUDA hello.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="4b8c7-162">installazione di Hello può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="4b8c7-163">toooptionally installazione hello CUDA toolkit completo, tipo:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="4b8c7-164">Riavviare hello macchina virtuale e continuare l'installazione di hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="4b8c7-165">Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3</span><span class="sxs-lookup"><span data-stu-id="4b8c7-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="4b8c7-166">Ottenere gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="4b8c7-167">Riconnettersi toohello macchina virtuale e installare hello più recente di servizi di integrazione Linux per Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4b8c7-168">Se è installata un'immagine basata su CentOS HPC in una macchina virtuale NC24r, ignorare tooStep 3.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="4b8c7-169">Poiché i driver RDMA di Azure e servizi di integrazione Linux sono pre-installati nell'immagine di hello, LIS non deve essere aggiornato e gli aggiornamenti di kernel sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="4b8c7-170">Riconnettersi toohello macchina virtuale e continuare l'installazione con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

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

  <span data-ttu-id="4b8c7-171">installazione di Hello può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="4b8c7-172">toooptionally installazione hello CUDA toolkit completo, tipo:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="4b8c7-173">Riavviare hello macchina virtuale e continuare l'installazione di hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="4b8c7-174">Verificare l'installazione del driver</span><span class="sxs-lookup"><span data-stu-id="4b8c7-174">Verify driver installation</span></span>


<span data-ttu-id="4b8c7-175">tooquery hello dello stato del dispositivo GPU, SSH toohello VM e hello esecuzione [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) utilità della riga di comando installato con il driver hello.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="4b8c7-176">Viene visualizzato il seguente toohello simile di output:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-176">Output similar toohello following appears:</span></span>

![Stato del dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="4b8c7-178">Aggiornamenti dei driver CUDA</span><span class="sxs-lookup"><span data-stu-id="4b8c7-178">CUDA driver updates</span></span>

<span data-ttu-id="4b8c7-179">È consigliabile aggiornare periodicamente i driver CUDA dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="4b8c7-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4b8c7-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="4b8c7-181">Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3</span><span class="sxs-lookup"><span data-stu-id="4b8c7-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="4b8c7-182">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="4b8c7-182">Troubleshooting</span></span>

* <span data-ttu-id="4b8c7-183">Si verifica un problema noto con driver CUDA sulle macchine virtuali di Azure serie N eseguono kernel Linux di hello 4.4.0-75 Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="4b8c7-184">Se esegue l'aggiornamento da una versione precedente di kernel, eseguire l'aggiornamento tooat 4.4.0-77 di versione minima del kernel.</span><span class="sxs-lookup"><span data-stu-id="4b8c7-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="4b8c7-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b8c7-185">Next steps</span></span>

* <span data-ttu-id="4b8c7-186">Per informazioni sulle GPU NVIDIA hello per le macchine virtuali serie N hello, vedere:</span><span class="sxs-lookup"><span data-stu-id="4b8c7-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="4b8c7-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (per VM NC Azure)</span><span class="sxs-lookup"><span data-stu-id="4b8c7-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="4b8c7-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (per VM NV Azure)</span><span class="sxs-lookup"><span data-stu-id="4b8c7-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="4b8c7-189">toocapture un'immagine VM Linux con il driver NVIDIA installati, vedere [come toogeneralize e acquisire una macchina virtuale Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4b8c7-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
