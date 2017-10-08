---
title: un disco gestito da un disco rigido virtuale in Azure aaaCreate | Documenti Microsoft
description: "Creare un disco gestito da un disco rigido virtuale che è attualmente in un account di archiviazione Azure tramite hello modello di distribuzione di gestione delle risorse."
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
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="3bbb7-103">Creare dischi gestiti da dischi non gestiti in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3bbb7-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="3bbb7-104">Un disco gestito può essere creato da un disco dati esistente o da un disco del sistema operativo che si trova attualmente in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="3bbb7-105">È anche possibile creare un disco vuoto da usare come nuovo disco dati per una VM.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="3bbb7-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3bbb7-106">Before you begin</span></span>
<span data-ttu-id="3bbb7-107">Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="3bbb7-108">Eseguire hello seguenti comando tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="3bbb7-109">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3bbb7-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="3bbb7-110">Creare un disco gestito da un disco rigido virtuale in un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3bbb7-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="3bbb7-111">Nell'esempio hello è creare un disco da un file VHD come disco gestito e assegnarlo parametro toohello **$Disco1** toouse in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="3bbb7-112">Hello gestito verrà creato un disco in hello **degli Stati Uniti occidentali** percorso, in un gruppo di risorse denominato **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="3bbb7-113">verrà denominato disco Hello **myDisk** e verrà creato da un file di disco rigido virtuale denominato **myDisk.vhd** è caricato in precedenza denominato account di archiviazione di tooa **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="3bbb7-114">disco gestito Hello verrà creata nel servizio di archiviazione con ridondanza locale premium (LRS).</span><span class="sxs-lookup"><span data-stu-id="3bbb7-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="3bbb7-115">StandardLRS e PremiumLRS sono solo hello **- AccountType** opzioni disponibili per i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="3bbb7-116">Impostare alcuni parametri</span><span class="sxs-lookup"><span data-stu-id="3bbb7-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="3bbb7-117">Creare il disco di dati hello.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="3bbb7-118">Creare un disco dati vuoto come disco gestito</span><span class="sxs-lookup"><span data-stu-id="3bbb7-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="3bbb7-119">Nell'esempio hello verrà creato un disco dati vuoto come disco gestito e assegnarlo parametro toohello **$dataDisk2** toouse in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="3bbb7-120">Un disco dati vuoto sarà necessario toobe inizializzato accesso toohello macchina virtuale e utilizzare diskmgmt.msc o [in modalità remota tramite Gestione remota Windows e uno script](attach-disk-ps.md#initialize-the-disk), una volta collegato tooa in esecuzione sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="3bbb7-121">verrà creato un disco dati vuoto Hello in hello **occidentale Stati Uniti centro** percorso, in un gruppo di risorse denominato **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="3bbb7-122">verrà denominato disco Hello **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="3bbb7-123">verrà creato un disco vuoto Hello in archiviazione con ridondanza locale premium (LRS).</span><span class="sxs-lookup"><span data-stu-id="3bbb7-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="3bbb7-124">StandardLRS e PremiumLRS sono solo hello **- AccountType** opzioni disponibili per i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="3bbb7-125">dimensioni del disco Hello in questo esempio sono 128GB, ma è consigliabile scegliere una dimensione soddisfa le esigenze di hello di tutte le applicazioni in esecuzione nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="3bbb7-126">Impostare alcuni parametri</span><span class="sxs-lookup"><span data-stu-id="3bbb7-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="3bbb7-127">Creare il disco di dati hello.</span><span class="sxs-lookup"><span data-stu-id="3bbb7-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="3bbb7-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3bbb7-128">Next Steps</span></span>   
- <span data-ttu-id="3bbb7-129">Se si dispone già di una macchina virtuale, è possibile [collegare un disco dati](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3bbb7-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
