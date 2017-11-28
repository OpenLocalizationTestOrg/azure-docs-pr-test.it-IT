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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="070f7-103">Configurare i driver GPU NVIDIA per le VM serie N che eseguono Windows Server</span><span class="sxs-lookup"><span data-stu-id="070f7-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="070f7-104">tootake le funzionalità GPU hello di N-serie Azure le macchine virtuali che eseguono Windows Server 2016 o Windows Server 2012 R2, installare i driver grafici NVIDIA è supportato.</span><span class="sxs-lookup"><span data-stu-id="070f7-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="070f7-105">Questo articolo descrive la procedura di installazione dei driver dopo la distribuzione di una macchina virtuale serie N.</span><span class="sxs-lookup"><span data-stu-id="070f7-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="070f7-106">Le informazioni di configurazione dei driver sono disponibili anche per le [VM Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="070f7-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="070f7-107">Per conoscere le specifiche base, le capacità di archiviazione e i dettagli relativi ai dischi, vedere [Dimensioni delle macchine virtuali Windows GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="070f7-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="070f7-108">Installazione del driver</span><span class="sxs-lookup"><span data-stu-id="070f7-108">Driver installation</span></span>

1. <span data-ttu-id="070f7-109">Connessione Desktop remoto tooeach N serie VM.</span><span class="sxs-lookup"><span data-stu-id="070f7-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="070f7-110">Scaricare, estrarre e installare il driver hello è supportato per il sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="070f7-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="070f7-111">Nelle VM NV Azure, è necessario eseguire il riavvio dopo l'installazione del driver.</span><span class="sxs-lookup"><span data-stu-id="070f7-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="070f7-112">Nelle VM NC, non è necessario riavviare il sistema.</span><span class="sxs-lookup"><span data-stu-id="070f7-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="070f7-113">Verificare l'installazione del driver</span><span class="sxs-lookup"><span data-stu-id="070f7-113">Verify driver installation</span></span>

<span data-ttu-id="070f7-114">È possibile verificare l'installazione del driver in Gestione dispositivi.</span><span class="sxs-lookup"><span data-stu-id="070f7-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="070f7-115">Hello seguente illustra la corretta configurazione della scheda hello Tesla R80 in una macchina virtuale NC di Azure.</span><span class="sxs-lookup"><span data-stu-id="070f7-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![Proprietà del driver GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="070f7-117">hello tooquery dello stato del dispositivo GPU, eseguire hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) utilità della riga di comando installato con il driver hello.</span><span class="sxs-lookup"><span data-stu-id="070f7-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="070f7-118">Aprire un prompt dei comandi e modificare toohello **c:\Programmi\Microsoft Files\NVIDIA Corporation\NVSMI** directory.</span><span class="sxs-lookup"><span data-stu-id="070f7-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="070f7-119">Eseguire **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="070f7-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="070f7-120">Se è installato il driver hello toobelow simili di output verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="070f7-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="070f7-121">Si noti che **GPU Util** Mostra **0%** a meno che non è in esecuzione un carico di lavoro GPU in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="070f7-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![Stato del dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="070f7-123">Rete RDMA per VM NC24r</span><span class="sxs-lookup"><span data-stu-id="070f7-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="070f7-124">È possibile abilitare la connettività di rete RDMA in macchine virtuali NC24r distribuite in hello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="070f7-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="070f7-125">estensione HpcVmDrivers Hello deve essere aggiunti tooinstall Windows driver dispositivi di rete che consentono la connettività RDMA.</span><span class="sxs-lookup"><span data-stu-id="070f7-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="070f7-126">tooadd hello VM estensione tooan NC24r VM, utilizzare [Azure PowerShell](/powershell/azure/overview) cmdlet per Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="070f7-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="070f7-127">Attualmente, solo Windows Server 2012 R2 supporta rete RDMA hello in macchine virtuali NC24r.</span><span class="sxs-lookup"><span data-stu-id="070f7-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="070f7-128">tooinstall hello più recente versione 1.1 estensione HpcVMDrivers in una macchina virtuale che supportano RDMA esistente denominata myVM nell'area Stati Uniti occidentali hello:</span><span class="sxs-lookup"><span data-stu-id="070f7-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="070f7-129">Per altre informazioni, vedere [Estensioni e funzionalità della macchina virtuale per Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="070f7-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="070f7-130">rete RDMA Hello supporta il traffico dell'interfaccia MPI (Message Passing) per le applicazioni in esecuzione con [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) o Intel MPI 5. x.</span><span class="sxs-lookup"><span data-stu-id="070f7-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="070f7-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="070f7-131">Next steps</span></span>

* <span data-ttu-id="070f7-132">Per informazioni sulle GPU NVIDIA hello per le macchine virtuali serie N hello, vedere:</span><span class="sxs-lookup"><span data-stu-id="070f7-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="070f7-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (per VM NC Azure)</span><span class="sxs-lookup"><span data-stu-id="070f7-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="070f7-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (per VM NV Azure)</span><span class="sxs-lookup"><span data-stu-id="070f7-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="070f7-135">Gli sviluppatori che creano applicazioni con accelerazione GPU per hello le Tesla GPU NVIDIA possono anche scaricare e installare hello CUDA Toolkit 8 per [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) o [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="070f7-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="070f7-136">Per ulteriori informazioni, vedere hello [Guida all'installazione CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="070f7-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


