---
title: Copiare un disco gestito di Azure per il backup | Microsoft Docs
description: Informazioni su come creare una copia di un disco gestito di Azure da usare per il backup o sulla risoluzione dei problemi relativi al disco.
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
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="63d05-103">Creare una copia di un disco rigido virtuale archiviato come disco gestito di Azure usando snapshot gestiti</span><span class="sxs-lookup"><span data-stu-id="63d05-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="63d05-104">Creare uno snapshot di un disco gestito per il backup o creare un disco gestito dallo snapshot e collegarlo a una macchina virtuale di prova per risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="63d05-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="63d05-105">Uno snapshot gestito è una copia temporizzata completa di un disco gestito di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="63d05-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="63d05-106">Uno snapshot crea una copia di sola lettura del disco rigido virtuale che, per impostazione predefinita, viene memorizzato come disco gestito Standard.</span><span class="sxs-lookup"><span data-stu-id="63d05-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="63d05-107">Per altre informazioni sui dischi gestiti, vedere [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="63d05-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="63d05-108">Per informazioni sui prezzi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="63d05-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="63d05-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="63d05-109">Before you begin</span></span>
<span data-ttu-id="63d05-110">Se si usa PowerShell, verificare di avere la versione più recente del modulo di PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="63d05-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="63d05-111">Eseguire il comando seguente per installarlo.</span><span class="sxs-lookup"><span data-stu-id="63d05-111">Run the following command to install it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="63d05-112">Per altre informazioni, vedere [Azure PowerShell Versioning](/powershell/azure/overview) (Controllo delle versioni di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="63d05-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-the-vhd-with-a-snapshot"></a><span data-ttu-id="63d05-113">Copiare il disco rigido virtuale con uno snapshot</span><span class="sxs-lookup"><span data-stu-id="63d05-113">Copy the VHD with a snapshot</span></span>
<span data-ttu-id="63d05-114">Usare il portale di Azure o PowerShell per creare uno snapshot del disco gestito.</span><span class="sxs-lookup"><span data-stu-id="63d05-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span></span>

### <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="63d05-115">Usare il portale di Azure per creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="63d05-115">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="63d05-116">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="63d05-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="63d05-117">In alto a sinistra fare clic su **Nuovo** e cercare **Snapshot**.</span><span class="sxs-lookup"><span data-stu-id="63d05-117">Starting in the upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="63d05-118">Nel pannello Snapshot, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="63d05-118">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="63d05-119">Immettere un **Nome** per lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="63d05-119">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="63d05-120">Selezionare un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md#resource-groups) esistente o specificare il nome di un nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="63d05-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="63d05-121">Selezionare una località per il data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="63d05-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="63d05-122">Per **Disco di origine**, selezionare il disco gestito di cui creare lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="63d05-122">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="63d05-123">Selezionare il **tipo di account** da usare per archiviare lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="63d05-123">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="63d05-124">È consigliabile usare il tipo **Standard_LRS** a meno che non sia necessario archiviare lo snapshot su un disco a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="63d05-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="63d05-125">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="63d05-125">Click **Create**.</span></span>

### <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="63d05-126">Utilizzare PowerShell per creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="63d05-126">Use PowerShell to take a snapshot</span></span>
<span data-ttu-id="63d05-127">La procedura seguente mostra come ottenere il disco rigido virtuale da copiare, creare le configurazioni di snapshot e ottenere uno snapshot del disco tramite il cmdlet New-AzureRmSnapshot<!--Add link to cmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="63d05-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span></span> 

1. <span data-ttu-id="63d05-128">Impostare alcuni parametri.</span><span class="sxs-lookup"><span data-stu-id="63d05-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="63d05-129">Sostituire i valori dei parametri:</span><span class="sxs-lookup"><span data-stu-id="63d05-129">Replace the parameter values:</span></span>
  -  <span data-ttu-id="63d05-130">"myResourceGroup" con il gruppo di risorse della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="63d05-130">"myResourceGroup" with the VM's resource group.</span></span>
  -  <span data-ttu-id="63d05-131">"southeastasia" con la posizione geografica in cui si desidera archiviare lo snapshot gestito.</span><span class="sxs-lookup"><span data-stu-id="63d05-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="63d05-132">"ContosoMD_datadisk1" con il nome del disco del disco rigido virtuale da copiare.</span><span class="sxs-lookup"><span data-stu-id="63d05-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span></span>
  -  <span data-ttu-id="63d05-133">"ContosoMD_datadisk1_snapshot1" con il nome da utilizzare per il nuovo snapshot.</span><span class="sxs-lookup"><span data-stu-id="63d05-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span></span>

2. <span data-ttu-id="63d05-134">Ottenere il disco rigido virtuale da copiare.</span><span class="sxs-lookup"><span data-stu-id="63d05-134">Get the VHD disk to be copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="63d05-135">Creare le configurazioni di snapshot.</span><span class="sxs-lookup"><span data-stu-id="63d05-135">Create the snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="63d05-136">Ottenere lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="63d05-136">Take the snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="63d05-137">Se si prevede di usare lo snapshot per creare un disco gestito e associarlo a una macchina virtuale a prestazioni elevate, usare il parametro `-AccountType Premium_LRS` con il comando New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="63d05-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="63d05-138">Il parametro crea lo snapshot in modo tale che venga archiviato come un disco gestito Premium.</span><span class="sxs-lookup"><span data-stu-id="63d05-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="63d05-139">I dischi gestiti Premium sono più costosi di quelli Standard.</span><span class="sxs-lookup"><span data-stu-id="63d05-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="63d05-140">Pertanto, assicurarsi che l'opzione Premium sia realmente necessaria prima di usare tale parametro.</span><span class="sxs-lookup"><span data-stu-id="63d05-140">So be sure you really need Premium before using that parameter.</span></span>


