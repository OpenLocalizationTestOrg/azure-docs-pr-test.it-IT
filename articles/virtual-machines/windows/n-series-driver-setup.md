---
title: installazione del driver aaaAzure N serie per Windows | Documenti Microsoft
description: Come tooset i driver GPU NVIDIA per le macchine virtuali serie N Windows in esecuzione in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Configurare i driver GPU NVIDIA per le VM serie N che eseguono Windows Server
tootake le funzionalità GPU hello di N-serie Azure le macchine virtuali che eseguono Windows Server 2016 o Windows Server 2012 R2, installare i driver grafici NVIDIA è supportato. Questo articolo descrive la procedura di installazione dei driver dopo la distribuzione di una macchina virtuale serie N. Le informazioni di configurazione dei driver sono disponibili anche per le [VM Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Per conoscere le specifiche base, le capacità di archiviazione e i dettagli relativi ai dischi, vedere [Dimensioni delle macchine virtuali Windows GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Installazione del driver

1. Connessione Desktop remoto tooeach N serie VM.

2. Scaricare, estrarre e installare il driver hello è supportato per il sistema operativo Windows.

Nelle VM NV Azure, è necessario eseguire il riavvio dopo l'installazione del driver. Nelle VM NC, non è necessario riavviare il sistema.

## <a name="verify-driver-installation"></a>Verificare l'installazione del driver

È possibile verificare l'installazione del driver in Gestione dispositivi. Hello seguente illustra la corretta configurazione della scheda hello Tesla R80 in una macchina virtuale NC di Azure.

![Proprietà del driver GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

hello tooquery dello stato del dispositivo GPU, eseguire hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) utilità della riga di comando installato con il driver hello.

1. Aprire un prompt dei comandi e modificare toohello **c:\Programmi\Microsoft Files\NVIDIA Corporation\NVSMI** directory.

2. Eseguire **nvidia-smi**. Se è installato il driver hello toobelow simili di output verrà visualizzato. Si noti che **GPU Util** Mostra **0%** a meno che non è in esecuzione un carico di lavoro GPU in hello macchina virtuale.

![Stato del dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>Rete RDMA per VM NC24r

È possibile abilitare la connettività di rete RDMA in macchine virtuali NC24r distribuite in hello stesso set di disponibilità. estensione HpcVmDrivers Hello deve essere aggiunti tooinstall Windows driver dispositivi di rete che consentono la connettività RDMA. tooadd hello VM estensione tooan NC24r VM, utilizzare [Azure PowerShell](/powershell/azure/overview) cmdlet per Gestione risorse di Azure.

> [!NOTE]
> Attualmente, solo Windows Server 2012 R2 supporta rete RDMA hello in macchine virtuali NC24r.
> 

tooinstall hello più recente versione 1.1 estensione HpcVMDrivers in una macchina virtuale che supportano RDMA esistente denominata myVM nell'area Stati Uniti occidentali hello:
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Per altre informazioni, vedere [Estensioni e funzionalità della macchina virtuale per Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

rete RDMA Hello supporta il traffico dell'interfaccia MPI (Message Passing) per le applicazioni in esecuzione con [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) o Intel MPI 5. x. 


## <a name="next-steps"></a>Passaggi successivi

* Per informazioni sulle GPU NVIDIA hello per le macchine virtuali serie N hello, vedere:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (per VM NC Azure)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (per VM NV Azure)

* Gli sviluppatori che creano applicazioni con accelerazione GPU per hello le Tesla GPU NVIDIA possono anche scaricare e installare hello CUDA Toolkit 8 per [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) o [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Per ulteriori informazioni, vedere hello [Guida all'installazione CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


