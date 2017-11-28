---
title: aaaCopy del disco per il backup di un gestito di Azure | Documenti Microsoft
description: Informazioni su come toocreate una copia di un toouse disco gestito di Azure per eseguire il backup o sulla risoluzione dei problemi di disco problemi.
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
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="7f452-103">Creare una copia di un disco rigido virtuale archiviato come disco gestito di Azure usando snapshot gestiti</span><span class="sxs-lookup"><span data-stu-id="7f452-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="7f452-104">Creare uno snapshot di un disco gestito per il backup o creare un disco gestito da snapshot hello e collegarlo tootroubleshoot macchina virtuale di test tooa.</span><span class="sxs-lookup"><span data-stu-id="7f452-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="7f452-105">Uno snapshot gestito è una copia temporizzata completa di un disco gestito di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7f452-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="7f452-106">Uno snapshot crea una copia di sola lettura del disco rigido virtuale che, per impostazione predefinita, viene memorizzato come disco gestito Standard.</span><span class="sxs-lookup"><span data-stu-id="7f452-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="7f452-107">Per informazioni sui prezzi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="7f452-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="7f452-108">Utilizzare entrambi hello Azure tootake di CLI di Azure 2.0 portale o hello uno snapshot di hello disco gestito.</span><span class="sxs-lookup"><span data-stu-id="7f452-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="7f452-109">Utilizzare Azure CLI 2.0 tootake uno snapshot</span><span class="sxs-lookup"><span data-stu-id="7f452-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="7f452-110">Hello esempio seguente richiede hello Azure CLI 2.0 installati e registrati nell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="7f452-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="7f452-111">Hello passaggi seguenti viene illustrato come tooobtain e creare uno snapshot di un sistema operativo gestito disco utilizzando hello `az snapshot create` con hello `--source-disk` parametro.</span><span class="sxs-lookup"><span data-stu-id="7f452-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="7f452-112">Hello seguente si presuppone che sia presente una macchina virtuale denominata `myVM` creato con un disco del sistema operativo gestito in hello `myResourceGroup` gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7f452-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="7f452-113">output di Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="7f452-113">hello output should look something like:</span></span>

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

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="7f452-114">Utilizzare tootake portale Azure uno snapshot</span><span class="sxs-lookup"><span data-stu-id="7f452-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="7f452-115">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f452-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7f452-116">A partire da hello angolo superiore sinistro, fare clic su **New** e cercare **snapshot**.</span><span class="sxs-lookup"><span data-stu-id="7f452-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="7f452-117">Nel Pannello di Snapshot hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="7f452-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="7f452-118">Immettere un **nome** per snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="7f452-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="7f452-119">Selezionare un oggetto esistente [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md#resource-groups) o nome di tipo hello uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="7f452-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="7f452-120">Selezionare una località per il data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f452-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="7f452-121">Per **disco di origine**, selezionare hello toosnapshot disco gestito.</span><span class="sxs-lookup"><span data-stu-id="7f452-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="7f452-122">Seleziona hello **tipo di Account** snapshot di hello toostore toouse.</span><span class="sxs-lookup"><span data-stu-id="7f452-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="7f452-123">È consigliabile usare il tipo **Standard_LRS** a meno che non sia necessario archiviare lo snapshot su un disco a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="7f452-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="7f452-124">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7f452-124">Click **Create**.</span></span>

<span data-ttu-id="7f452-125">Se si prevede toouse hello snapshot toocreate un disco gestito e collegarlo a una macchina virtuale che deve toobe a prestazioni elevate, utilizzare il parametro hello `--sku Premium_LRS` con hello `az snapshot create` comando.</span><span class="sxs-lookup"><span data-stu-id="7f452-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="7f452-126">Questo crea snapshot hello in modo che viene archiviato come un disco gestito Premium.</span><span class="sxs-lookup"><span data-stu-id="7f452-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="7f452-127">Managed Disks Premium offre prestazioni migliori perché consiste in unità SSD, ma con un costo superiore rispetto ai dischi Standard (HDD).</span><span class="sxs-lookup"><span data-stu-id="7f452-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


