---
title: aaaConvert Azure gestito archiviazione dischi da toopremium standard e viceversa | Documenti Microsoft
description: Come archivio dischi tooconvert Azure gestito da toopremium standard e viceversa, tramite l'interfaccia CLI di Azure.
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c4a72-103">Convertire Azure archiviazione dischi gestiti da toopremium standard e viceversa</span><span class="sxs-lookup"><span data-stu-id="c4a72-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c4a72-104">Managed Disks offre due opzioni di archiviazione: [Premium](../../storage/storage-premium-storage.md) (basata su SSD) e [Standard](../../storage/storage-standard-storage.md) (basata su HDD).</span><span class="sxs-lookup"><span data-stu-id="c4a72-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="c4a72-105">Consente di commutatore tooeasily tra le opzioni di hello due con tempo di inattività minimo in base alle proprie esigenze di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c4a72-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="c4a72-106">Questa funzionalità non è disponibile per i dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="c4a72-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="c4a72-107">Ma è possibile facilmente [convertire dischi toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily commutatore tra le opzioni di hello due.</span><span class="sxs-lookup"><span data-stu-id="c4a72-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="c4a72-108">Questo articolo illustra come tooconvert dischi gestiti da toopremium standard e viceversa utilizzando CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4a72-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="c4a72-109">Se è necessario tooinstall o eseguirne l'aggiornamento, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c4a72-109">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="c4a72-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c4a72-110">Before you begin</span></span>

* <span data-ttu-id="c4a72-111">la conversione di Hello richiede un riavvio della macchina virtuale hello, pertanto, pianificare la migrazione di hello dello spazio di archiviazione dischi durante una finestra di manutenzione preesistente.</span><span class="sxs-lookup"><span data-stu-id="c4a72-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="c4a72-112">Se si utilizza innanzitutto i dischi non gestiti, [convertire dischi toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch questo articolo tra le opzioni di archiviazione hello due.</span><span class="sxs-lookup"><span data-stu-id="c4a72-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c4a72-113">Converti tutti hello gestiti dischi di una macchina virtuale da toopremium standard e viceversa</span><span class="sxs-lookup"><span data-stu-id="c4a72-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c4a72-114">Nell'esempio seguente di hello, ecco come tooswitch tutti hello dischi di una macchina virtuale dall'archiviazione toopremium standard.</span><span class="sxs-lookup"><span data-stu-id="c4a72-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="c4a72-115">dischi gestiti toouse premium, la macchina virtuale è necessario utilizzare un [dimensioni delle macchine Virtuali](sizes.md) che supporta l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="c4a72-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="c4a72-116">Questo esempio imposta anche dimensioni tooa che supporta l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="c4a72-116">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c4a72-117">Convertire un disco gestito da toopremium standard e viceversa</span><span class="sxs-lookup"><span data-stu-id="c4a72-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c4a72-118">Il carico di lavoro di sviluppo/test, è consigliabile toohave combinazione di dischi standard e premium tooreduce i costi.</span><span class="sxs-lookup"><span data-stu-id="c4a72-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="c4a72-119">È possibile ottenere questo risultato con l'aggiornamento di archiviazione toopremium, solo i dischi di hello che richiedono prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="c4a72-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="c4a72-120">Nell'esempio seguente di hello, ecco come tooswitch un singolo disco di una macchina virtuale dall'archiviazione toopremium standard e viceversa.</span><span class="sxs-lookup"><span data-stu-id="c4a72-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="c4a72-121">dischi gestiti toouse premium, la macchina virtuale è necessario utilizzare un [dimensioni delle macchine Virtuali](sizes.md) che supporta l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="c4a72-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="c4a72-122">Questo esempio imposta anche dimensioni tooa che supporta l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="c4a72-122">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a><span data-ttu-id="c4a72-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4a72-123">Next steps</span></span>

<span data-ttu-id="c4a72-124">Eseguire una copia di sola lettura di una VM usando [snapshot](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="c4a72-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

