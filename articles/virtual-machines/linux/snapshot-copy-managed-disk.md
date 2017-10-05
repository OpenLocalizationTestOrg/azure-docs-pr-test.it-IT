---
title: Copiare un disco gestito di Azure per il backup | Documentazione Microsoft
description: Informazioni su come creare una copia di un disco gestito di Azure da usare per il backup o sulla risoluzione dei problemi relativi al disco.
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: c91367ef11c9d531bebac7c069d2df586607ec29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="f949e-103">Creare una copia di un disco rigido virtuale archiviato come disco gestito di Azure usando snapshot gestiti</span><span class="sxs-lookup"><span data-stu-id="f949e-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="f949e-104">Creare uno snapshot di un disco gestito per il backup o creare un disco gestito dallo snapshot e collegarlo a una macchina virtuale di prova per risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="f949e-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="f949e-105">Uno snapshot gestito è una copia temporizzata completa di un disco gestito di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f949e-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="f949e-106">Uno snapshot crea una copia di sola lettura del disco rigido virtuale che, per impostazione predefinita, viene memorizzato come disco gestito Standard.</span><span class="sxs-lookup"><span data-stu-id="f949e-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="f949e-107">Per informazioni sui prezzi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="f949e-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link to topic or blog post that explains managed disks. -->

<span data-ttu-id="f949e-108">Usare il portale di Azure o l'interfaccia della riga di comando Azure 2.0 per creare uno snapshot del disco gestito.</span><span class="sxs-lookup"><span data-stu-id="f949e-108">Use either the Azure portal or the Azure CLI 2.0 to take a snapshot of the Managed Disk.</span></span>

## <a name="use-azure-cli-20-to-take-a-snapshot"></a><span data-ttu-id="f949e-109">Usare l'interfaccia della riga di comando Azure 2.0 per creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="f949e-109">Use Azure CLI 2.0 to take a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="f949e-110">L'esempio seguente richiede che sia installata l'interfaccia della riga di comando Azure 2.0 e che venga eseguito l'accesso all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="f949e-110">The following example requires the Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="f949e-111">La procedura seguente illustra come ottenere e creare uno snapshot di un disco del sistema operativo gestito usando il comando `az snapshot create` con il parametro `--source-disk`.</span><span class="sxs-lookup"><span data-stu-id="f949e-111">The following steps show how to obtain and take a snapshot of a managed OS disk using the `az snapshot create` command with the `--source-disk` parameter.</span></span> <span data-ttu-id="f949e-112">Nell'esempio seguente si presuppone che esista una macchina virtuale denominata `myVM` creata con un disco del sistema operativo gestito nel gruppo di risorse `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="f949e-112">The following example assumes that there is a VM called `myVM` created with a managed OS disk in the `myResourceGroup` resource group.</span></span>

```azure-cli
# take the disk id with which to create a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="f949e-113">L'output dovrebbe essere simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f949e-113">The output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="f949e-114">Usare il portale di Azure per creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="f949e-114">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="f949e-115">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f949e-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f949e-116">In alto a sinistra fare clic su **Nuovo** e cercare **Snapshot**.</span><span class="sxs-lookup"><span data-stu-id="f949e-116">Starting in the upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="f949e-117">Nel pannello Snapshot, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f949e-117">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="f949e-118">Immettere un **Nome** per lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="f949e-118">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="f949e-119">Selezionare un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md#resource-groups) esistente o specificare il nome di un nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="f949e-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="f949e-120">Selezionare una località per il data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="f949e-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="f949e-121">Per **Disco di origine**, selezionare il disco gestito di cui creare lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="f949e-121">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="f949e-122">Selezionare il **tipo di account** da usare per archiviare lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="f949e-122">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="f949e-123">È consigliabile usare il tipo **Standard_LRS** a meno che non sia necessario archiviare lo snapshot su un disco a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="f949e-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="f949e-124">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f949e-124">Click **Create**.</span></span>

<span data-ttu-id="f949e-125">Se si prevede di usare lo snapshot per creare un disco gestito e associarlo a una macchina virtuale a prestazioni elevate, usare il parametro `--sku Premium_LRS` con il comando `az snapshot create`.</span><span class="sxs-lookup"><span data-stu-id="f949e-125">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `--sku Premium_LRS` with the `az snapshot create` command.</span></span> <span data-ttu-id="f949e-126">In questo modo si crea lo snapshot in modo tale che venga archiviato come un disco gestito Premium.</span><span class="sxs-lookup"><span data-stu-id="f949e-126">This creates the snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="f949e-127">Managed Disks Premium offre prestazioni migliori perché consiste in unità SSD, ma con un costo superiore rispetto ai dischi Standard (HDD).</span><span class="sxs-lookup"><span data-stu-id="f949e-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


