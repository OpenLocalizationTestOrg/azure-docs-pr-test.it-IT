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
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a>Installare i driver GPU NVIDIA in VM serie N che eseguono Linux

tootake le funzionalità GPU hello di N-serie Azure le macchine virtuali che eseguono Linux, installare i driver grafici NVIDIA è supportato. Questo articolo descrive la procedura di installazione dei driver dopo la distribuzione di una macchina virtuale serie N. Le informazioni di configurazione dei driver sono disponibili anche per le [VM Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


Per conoscere le specifiche, le capacità di archiviazione e i dettagli dei dischi delle macchine virtuali serie N, vedere [Dimensioni delle macchine virtuali Linux GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a>Installare i driver GRID per VM NV

i driver di griglia NVIDIA tooinstall nelle macchine virtuali NV, rendere un tooeach connessione SSH VM e seguire i passaggi di hello per le distribuzioni di Linux. 

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Eseguire hello `lspci` comando. Verificare che siano visibili come dispositivi PCI card hello M60 NVIDIA o schede.

2. Installare gli aggiornamenti.

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. Disabilitare i driver del kernel Nouveau hello, che è incompatibili con il driver NVIDIA hello. (Solo utilizzare driver NVIDIA hello in macchine virtuali non Volatile). toodo, creare un file in `/etc/modprobe.d `denominato `nouveau.conf` con hello seguente contenuto:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. Riavvio hello macchina virtuale e la riconnessione. Uscire dal server X:

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. Scaricare e installare i driver di griglia hello:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. Quando viene chiesto se si desidera toorun hello nvidia xconfig utilità tooupdate il file di configurazione di X, selezionare **Sì**.

7. Al termine dell'installazione, copiare /etc/nvidia/gridd.conf.template tooa nuova gridd.conf file nel percorso /etc/hosts nvidia /

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. Aggiungere il seguente di hello troppo`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Riavviare hello macchina virtuale e continuare l'installazione di hello tooverify.


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3


1. Aggiornare il kernel hello e DKMS.
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. Disabilitare i driver del kernel Nouveau hello, che è incompatibili con il driver NVIDIA hello. (Solo utilizzare driver NVIDIA hello in macchine virtuali non Volatile). toodo, creare un file in `/etc/modprobe.d `denominato `nouveau.conf` con hello seguente contenuto:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. Riavviare il computer hello macchina virtuale, riconnettersi e installare servizi di integrazione più recenti Linux per Hyper-v: hello
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. Riconnettersi toohello macchina virtuale ed eseguire hello `lspci` comando. Verificare che siano visibili come dispositivi PCI card hello M60 NVIDIA o schede.
 
5. Scaricare e installare i driver di griglia hello:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. Quando viene chiesto se si desidera toorun hello nvidia xconfig utilità tooupdate il file di configurazione di X, selezionare **Sì**.

7. Al termine dell'installazione, copiare /etc/nvidia/gridd.conf.template tooa nuova gridd.conf file nel percorso /etc/hosts nvidia /
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. Aggiungere il seguente di hello troppo`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Riavviare hello macchina virtuale e continuare l'installazione di hello tooverify.

### <a name="verify-driver-installation"></a>Verificare l'installazione del driver


tooquery hello dello stato del dispositivo GPU, SSH toohello VM e hello esecuzione [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) utilità della riga di comando installato con il driver hello. 

Viene visualizzato il seguente toohello simile di output:

![Stato del dispositivo NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a>Server X11
Se è necessario un X11 server per le connessioni remote tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) è consigliata perché consente l'accelerazione grafica hardware. Hello BusID del dispositivo hello M60 deve essere aggiunta manualmente file xconfig toohello (`etc/X11/xorg.conf` in Ubuntu 16.04 LTS, `/etc/X11/XF86config` CentOS 7.3 o Red Hat Enterprise Server 7.3). Aggiungere un `"Device"` sezione simile toohello seguenti:
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
Inoltre, per aggiornare il `"Screen"` sezione toouse questo dispositivo.
 
Hello BusID è reperibile eseguendo

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
Hello BusID può cambiare quando una macchina virtuale Ottiene riallocare o riavviata. Pertanto, è opportuno toouse un hello tooupdate script BusID nella configurazione hello X11 quando una macchina virtuale è stata riavviata. ad esempio:

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

Questo file può essere richiamato come radice all'avvio mediante la creazione di una voce in `/etc/rc.d/rc3.d`.


## <a name="install-cuda-drivers-for-nc-vms"></a>Installare i driver CUDA per macchine virtuali NC

Di seguito sono i driver NVIDIA tooinstall passaggi nelle macchine virtuali NC Linux da hello NVIDIA CUDA Toolkit 8.0. 

Gli sviluppatori di C e C++ è possono installare facoltativamente hello Toolkit toobuild accelerazione GPU applicazioni complete. Per ulteriori informazioni, vedere hello [Guida all'installazione CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).


> [!NOTE]
> I collegamenti ai download dei driver CUDA forniti qui sono quelli attivi al momento della pubblicazione. Per hello CUDA driver, visitare hello [NVIDIA](http://www.nvidia.com/) sito Web.
>

tooinstall CUDA Toolkit, rendere un tooeach connessione SSH macchina virtuale. tooverify che hello sistema disponga di una GPU che supporta CUDA, eseguire hello comando seguente:

```bash
lspci | grep -i NVIDIA
```
Si noterà toohello simili di output (rappresentato da una scheda NVIDIA Tesla R80) di esempio seguente:

![Output del comando Ispci](./media/n-series-driver-setup/lspci.png)

Quindi eseguire i comandi di installazione specifici per la distribuzione.

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Scaricare e installare i driver CUDA hello.
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  installazione di Hello può richiedere alcuni minuti.

2. toooptionally installazione hello CUDA toolkit completo, tipo:

  ```bash
  sudo apt-get install cuda
  ```

3. Riavviare hello macchina virtuale e continuare l'installazione di hello tooverify.

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3

1. Ottenere gli aggiornamenti. 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. Riconnettersi toohello macchina virtuale e installare hello più recente di servizi di integrazione Linux per Hyper-V.

  > [!IMPORTANT]
  > Se è installata un'immagine basata su CentOS HPC in una macchina virtuale NC24r, ignorare tooStep 3. Poiché i driver RDMA di Azure e servizi di integrazione Linux sono pre-installati nell'immagine di hello, LIS non deve essere aggiornato e gli aggiornamenti di kernel sono disabilitati per impostazione predefinita.
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. Riconnettersi toohello macchina virtuale e continuare l'installazione con hello seguenti comandi:

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

  installazione di Hello può richiedere alcuni minuti. 

4. toooptionally installazione hello CUDA toolkit completo, tipo:

  ```bash
  sudo yum install cuda
  ```

5. Riavviare hello macchina virtuale e continuare l'installazione di hello tooverify.


### <a name="verify-driver-installation"></a>Verificare l'installazione del driver


tooquery hello dello stato del dispositivo GPU, SSH toohello VM e hello esecuzione [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) utilità della riga di comando installato con il driver hello. 

Viene visualizzato il seguente toohello simile di output:

![Stato del dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a>Aggiornamenti dei driver CUDA

È consigliabile aggiornare periodicamente i driver CUDA dopo la distribuzione.

#### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Sistema operativo Linux basato su CentOS 7.3 o Red Hat Enterprise 7.3

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a>Risoluzione dei problemi

* Si verifica un problema noto con driver CUDA sulle macchine virtuali di Azure serie N eseguono kernel Linux di hello 4.4.0-75 Ubuntu 16.04 LTS. Se esegue l'aggiornamento da una versione precedente di kernel, eseguire l'aggiornamento tooat 4.4.0-77 di versione minima del kernel. 



## <a name="next-steps"></a>Passaggi successivi

* Per informazioni sulle GPU NVIDIA hello per le macchine virtuali serie N hello, vedere:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (per VM NC Azure)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (per VM NV Azure)

* toocapture un'immagine VM Linux con il driver NVIDIA installati, vedere [come toogeneralize e acquisire una macchina virtuale Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
