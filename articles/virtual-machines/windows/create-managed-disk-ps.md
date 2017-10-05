---
title: Creare un disco gestito da un disco rigido virtuale in Azure | Documentazione Microsoft
description: Creare un disco gestito da un disco rigido virtuale che si trova attualmente in un account di archiviazione di Azure, usando il modello di distribuzione di Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="8b43d-103">Creare dischi gestiti da dischi non gestiti in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8b43d-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="8b43d-104">Un disco gestito può essere creato da un disco dati esistente o da un disco del sistema operativo che si trova attualmente in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b43d-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="8b43d-105">È anche possibile creare un disco vuoto da usare come nuovo disco dati per una VM.</span><span class="sxs-lookup"><span data-stu-id="8b43d-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="8b43d-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8b43d-106">Before you begin</span></span>
<span data-ttu-id="8b43d-107">Se si usa PowerShell, verificare di avere la versione più recente del modulo di PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="8b43d-107">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="8b43d-108">Eseguire il comando seguente per installarlo.</span><span class="sxs-lookup"><span data-stu-id="8b43d-108">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="8b43d-109">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8b43d-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="8b43d-110">Creare un disco gestito da un disco rigido virtuale in un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8b43d-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="8b43d-111">Nell'esempio viene creato un disco da un disco rigido virtuale come disco gestito e viene assegnato al parametro **$disk1** da usare in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8b43d-111">In the example we create a disk from a VHD as managed disk and assign it to the parameter **$disk1** to use later.</span></span> 

<span data-ttu-id="8b43d-112">l disco gestito verrà creato nella posizione **West-US** all'interno di un gruppo di risorse denominato **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="8b43d-112">The managed disk will be created in the **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="8b43d-113">Il disco verrà denominato **myDisk** e verrà creato da un file di disco rigido virtuale denominato **myDisk.vhd** precedentemente caricato in un account di archiviazione denominato **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="8b43d-113">The disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded to a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="8b43d-114">Il disco gestito verrà creato nell'archiviazione con ridondanza locale Premium.</span><span class="sxs-lookup"><span data-stu-id="8b43d-114">The managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="8b43d-115">StandardLRS e PremiumLRS sono le uniche opzioni del **tipo di account** disponibili per gestire i dischi.</span><span class="sxs-lookup"><span data-stu-id="8b43d-115">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="8b43d-116">Impostare alcuni parametri</span><span class="sxs-lookup"><span data-stu-id="8b43d-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="8b43d-117">Creare il disco dati.</span><span class="sxs-lookup"><span data-stu-id="8b43d-117">Create the data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="8b43d-118">Creare un disco dati vuoto come disco gestito</span><span class="sxs-lookup"><span data-stu-id="8b43d-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="8b43d-119">Nell'esempio viene creato un disco dati vuoto da un disco gestito e viene assegnato al parametro **$dataDisk2** da usare in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8b43d-119">In the example we create an empty data disk as managed disk and assign it to the parameter **$dataDisk2** to use later.</span></span> <span data-ttu-id="8b43d-120">Sarà necessario inizializzare un disco dati vuoto accedendo alla macchina virtuale e usando diskmgmt.msc o [con WinRM da remoto e uno script](attach-disk-ps.md#initialize-the-disk), una volta collegato il disco a una macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8b43d-120">An empty data disk will need to be initialized logging in to the VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached to a running VM.</span></span>

<span data-ttu-id="8b43d-121">l disco dati vuoto verrà creato nella posizione **Stati Uniti centro-occidentali** all'interno di un gruppo di risorse denominato **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="8b43d-121">The empty data disk will be created in the **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="8b43d-122">Il disco verrà denominato **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="8b43d-122">The disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="8b43d-123">Il disco vuoto verrà creato nell'archiviazione con ridondanza locale Premium.</span><span class="sxs-lookup"><span data-stu-id="8b43d-123">The empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="8b43d-124">StandardLRS e PremiumLRS sono le uniche opzioni del **tipo di account** disponibili per gestire i dischi.</span><span class="sxs-lookup"><span data-stu-id="8b43d-124">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="8b43d-125">Le dimensioni del disco in questo esempio sono pari a 128 GB, ma è consigliabile scegliere una dimensione che soddisfi le esigenze di tutte le applicazioni in esecuzione nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8b43d-125">The disk size in this example is 128GB, but you should choose a size that meets the needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="8b43d-126">Impostare alcuni parametri</span><span class="sxs-lookup"><span data-stu-id="8b43d-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="8b43d-127">Creare il disco dati.</span><span class="sxs-lookup"><span data-stu-id="8b43d-127">Create the data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="8b43d-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b43d-128">Next Steps</span></span>   
- <span data-ttu-id="8b43d-129">Se si dispone già di una macchina virtuale, è possibile [collegare un disco dati](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8b43d-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
