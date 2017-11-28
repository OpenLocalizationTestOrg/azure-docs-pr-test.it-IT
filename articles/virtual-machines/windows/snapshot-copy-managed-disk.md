---
title: aaaCreate una copia di un disco gestito di Azure per eseguire il backup | Documenti Microsoft
description: Informazioni su come toocreate una copia di un toouse disco gestito di Azure per eseguire il backup o sulla risoluzione dei problemi di disco problemi.
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="549af-103">Creare una copia di un disco rigido virtuale archiviato come disco gestito di Azure usando snapshot gestiti</span><span class="sxs-lookup"><span data-stu-id="549af-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="549af-104">Creare uno snapshot di un disco gestito per il backup o creare un disco gestito da snapshot hello e collegarlo tootroubleshoot macchina virtuale di test tooa.</span><span class="sxs-lookup"><span data-stu-id="549af-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="549af-105">Uno snapshot gestito è una copia temporizzata completa di un disco gestito di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="549af-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="549af-106">Uno snapshot crea una copia di sola lettura del disco rigido virtuale che, per impostazione predefinita, viene memorizzato come disco gestito Standard.</span><span class="sxs-lookup"><span data-stu-id="549af-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="549af-107">Per altre informazioni sui dischi gestiti, vedere [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="549af-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="549af-108">Per informazioni sui prezzi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="549af-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="549af-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="549af-109">Before you begin</span></span>
<span data-ttu-id="549af-110">Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="549af-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="549af-111">Eseguire hello seguenti comando tooinstall.</span><span class="sxs-lookup"><span data-stu-id="549af-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="549af-112">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="549af-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="549af-113">Copiare hello disco rigido virtuale con uno snapshot</span><span class="sxs-lookup"><span data-stu-id="549af-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="549af-114">Utilizzare hello portale di Azure o PowerShell tootake uno snapshot di hello disco gestito.</span><span class="sxs-lookup"><span data-stu-id="549af-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="549af-115">Utilizzare tootake portale Azure uno snapshot</span><span class="sxs-lookup"><span data-stu-id="549af-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="549af-116">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="549af-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="549af-117">A partire da in alto a sinistra di hello, fare clic su **New** e cercare **snapshot**.</span><span class="sxs-lookup"><span data-stu-id="549af-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="549af-118">Nel Pannello di Snapshot hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="549af-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="549af-119">Immettere un **nome** per snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="549af-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="549af-120">Selezionare un oggetto esistente [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md#resource-groups) o nome di tipo hello uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="549af-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="549af-121">Selezionare una località per il data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="549af-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="549af-122">Per **disco di origine**, selezionare hello toosnapshot disco gestito.</span><span class="sxs-lookup"><span data-stu-id="549af-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="549af-123">Seleziona hello **tipo di Account** snapshot di hello toostore toouse.</span><span class="sxs-lookup"><span data-stu-id="549af-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="549af-124">È consigliabile usare il tipo **Standard_LRS** a meno che non sia necessario archiviare lo snapshot su un disco a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="549af-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="549af-125">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="549af-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="549af-126">Utilizzare PowerShell tootake uno snapshot</span><span class="sxs-lookup"><span data-stu-id="549af-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="549af-127">Hello passaggi seguenti mostrano come tooget hello VHD disco toobe copiati, creare configurazioni di snapshot di hello e uno snapshot del disco hello utilizzando il cmdlet New-AzureRmSnapshot hello<!--Add link toocmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="549af-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="549af-128">Impostare alcuni parametri.</span><span class="sxs-lookup"><span data-stu-id="549af-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="549af-129">Sostituire i valori di parametro hello:</span><span class="sxs-lookup"><span data-stu-id="549af-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="549af-130">"myResourceGroup" con il gruppo di risorse della macchina virtuale di hello.</span><span class="sxs-lookup"><span data-stu-id="549af-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="549af-131">"southeastasia" con l'area geografica hello in cui si desidera lo Snapshot gestito archiviato.</span><span class="sxs-lookup"><span data-stu-id="549af-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="549af-132">"ContosoMD_datadisk1" con il nome di hello del disco VHD hello che si desidera toocopy.</span><span class="sxs-lookup"><span data-stu-id="549af-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="549af-133">"ContosoMD_datadisk1_snapshot1" con hello nome che si desidera toouse del nuovo snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="549af-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="549af-134">Ottenere hello VHD disco toobe copiati.</span><span class="sxs-lookup"><span data-stu-id="549af-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="549af-135">Creare configurazioni di snapshot di hello.</span><span class="sxs-lookup"><span data-stu-id="549af-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="549af-136">Creare snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="549af-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="549af-137">Se si prevede toouse hello snapshot toocreate un disco gestito e collegarlo a una macchina virtuale che deve toobe a prestazioni elevate, utilizzare il parametro hello `-AccountType Premium_LRS` con il comando New-AzureRmSnapshot hello.</span><span class="sxs-lookup"><span data-stu-id="549af-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="549af-138">il parametro Hello Crea snapshot hello in modo che viene archiviato come un disco gestito Premium.</span><span class="sxs-lookup"><span data-stu-id="549af-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="549af-139">I dischi gestiti Premium sono più costosi di quelli Standard.</span><span class="sxs-lookup"><span data-stu-id="549af-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="549af-140">Pertanto, assicurarsi che l'opzione Premium sia realmente necessaria prima di usare tale parametro.</span><span class="sxs-lookup"><span data-stu-id="549af-140">So be sure you really need Premium before using that parameter.</span></span>


