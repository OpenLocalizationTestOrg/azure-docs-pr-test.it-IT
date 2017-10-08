---
title: Dischi di macchina virtuale scala set collegati dati aaaAzure | Documenti Microsoft
description: "Informazioni su come toouse collegati dischi di dati con il set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="200f3-103">Set di scalabilità di macchine virtuali di Azure e dischi di dati collegati</span><span class="sxs-lookup"><span data-stu-id="200f3-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="200f3-104">I [set di scalabilità di macchine virtuali](/azure/virtual-machine-scale-sets/) di Azure supportano ora macchine virtuali con dischi di dati collegati.</span><span class="sxs-lookup"><span data-stu-id="200f3-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="200f3-105">I dischi dati possono essere definiti nel profilo di archiviazione hello per set di scalabilità che sono stati creati con dischi gestiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="200f3-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="200f3-106">In precedenza hello solo le opzioni di archiviazione collegata direttamente disponibili con le macchine virtuali nel set di scalabilità sono state unità hello del sistema operativo e unità temporanea.</span><span class="sxs-lookup"><span data-stu-id="200f3-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="200f3-107">Quando si crea un set di scalabilità con i dischi dati collegati definiti, è comunque necessario toomount e hello formato dischi all'interno di una macchina virtuale toouse li (proprio come per le macchine virtuali di Azure autonoma).</span><span class="sxs-lookup"><span data-stu-id="200f3-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="200f3-108">Un modo pratico di toodo equivale toouse un'estensione di uno script personalizzato che chiama un toopartition script standard e formattazione tutti i dischi dati hello in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="200f3-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="200f3-109">Creare un set di scalabilità con dischi di dati collegati</span><span class="sxs-lookup"><span data-stu-id="200f3-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="200f3-110">Toocreate un modo semplice una scala impostata con i dischi collegati è hello toouse [CLI di Azure](https://github.com/Azure/azure-cli) _vmss creare_ comando.</span><span class="sxs-lookup"><span data-stu-id="200f3-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="200f3-111">Hello di esempio seguente crea un gruppo di risorse di Azure e un set di scalabilità della macchina virtuale delle macchine virtuali Ubuntu 10, ognuno con dischi dati collegati 2, 50 GB e 100 GB.</span><span class="sxs-lookup"><span data-stu-id="200f3-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="200f3-112">Si noti che hello _vmss creare_ comando per impostazione predefinita di determinati valori di configurazione, se non si specifica.</span><span class="sxs-lookup"><span data-stu-id="200f3-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="200f3-113">toosee hello opzioni disponibili che è possibile eseguire l'override di provare a:</span><span class="sxs-lookup"><span data-stu-id="200f3-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="200f3-114">Un altro modo toocreate, un set di scalabilità con dischi dati collegati è toodefine imposta una scala in un modello di gestione risorse di Azure, includere un _dataDisks_ sezione hello _storageProfile_e distribuire hello modello.</span><span class="sxs-lookup"><span data-stu-id="200f3-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="200f3-115">Hello 50 e 100 GB disco esempio sopra riportato sarebbe definire simile al seguente nel modello hello:</span><span class="sxs-lookup"><span data-stu-id="200f3-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="200f3-116">È possibile visualizzare un esempio completo e pronto toodeploy di un modello di set di scalabilità con un disco collegato, definito qui: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="200f3-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="200f3-117">Aggiunta di una scala dei dati su disco tooan esistente set</span><span class="sxs-lookup"><span data-stu-id="200f3-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="200f3-118">È possibile collegare solo set di scalabilità con i tooa dischi dati che è stata creata con [dischi gestiti di Azure](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="200f3-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="200f3-119">È possibile aggiungere un data disco tooa VM set di scalabilità mediante Azure CLI _collega disco vmss az_ comando.</span><span class="sxs-lookup"><span data-stu-id="200f3-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="200f3-120">Specificare un lun che non sia già in uso.</span><span class="sxs-lookup"><span data-stu-id="200f3-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="200f3-121">Hello CLI esempio seguente aggiunge un toolun di unità di 50 GB 3:</span><span class="sxs-lookup"><span data-stu-id="200f3-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="200f3-122">esempio di PowerShell seguente Hello aggiunge un toolun di unità di 50 GB 3:</span><span class="sxs-lookup"><span data-stu-id="200f3-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="200f3-123">Dimensioni delle macchine Virtuali diverse hanno limiti diversi in numeri hello di supportano le unità collegate.</span><span class="sxs-lookup"><span data-stu-id="200f3-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="200f3-124">Controllare hello [le caratteristiche di dimensioni di macchina virtuale](../virtual-machines/windows/sizes.md) prima di aggiungere un nuovo disco.</span><span class="sxs-lookup"><span data-stu-id="200f3-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="200f3-125">È inoltre possibile aggiungere un disco mediante l'aggiunta di un nuovo toohello voce _dataDisks_ proprietà hello _storageProfile_ di una scala impostare definizione e l'applicazione hello modifica.</span><span class="sxs-lookup"><span data-stu-id="200f3-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="200f3-126">tootest, trovare una definizione di set di scalabilità esistente nel hello [Esplora inventario risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="200f3-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="200f3-127">Selezionare _modifica_ e aggiungere un nuovo elenco toohello disco dei dischi dati.</span><span class="sxs-lookup"><span data-stu-id="200f3-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="200f3-128">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="200f3-128">E.g.</span></span> <span data-ttu-id="200f3-129">utilizzando l'esempio hello precedente:</span><span class="sxs-lookup"><span data-stu-id="200f3-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="200f3-130">Selezionare quindi _inserire_ tooapply hello cambia tooyour set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="200f3-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="200f3-131">Questo esempio funziona se si usano macchine virtuali con dimensioni che supportano più di due dischi di dati collegati.</span><span class="sxs-lookup"><span data-stu-id="200f3-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="200f3-132">Quando si effettua una scala tooa Modifica definizione, ad esempio aggiunta o rimozione di un disco dati del set, si applica a macchine virtuali tooall appena creato, ma si applica solo le macchine virtuali tooexisting se hello _upgradePolicy_ proprietà è impostata troppo "automatico".</span><span class="sxs-lookup"><span data-stu-id="200f3-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="200f3-133">Se è impostato troppo "manuale", è necessario toomanually applicare hello nuovo modello tooexisting macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="200f3-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="200f3-134">È possibile farlo nel portale di hello utilizzando hello _aggiornamento AzureRmVmssInstance_ PowerShell comando o tramite hello _az vmss update-istanze_ comando CLI.</span><span class="sxs-lookup"><span data-stu-id="200f3-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="200f3-135">Aggiunta di dati pre-popolato dischi tooan esistente scala set</span><span class="sxs-lookup"><span data-stu-id="200f3-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="200f3-136">Quando si aggiungono dischi tooan esistente set di scalabilità di modello, in base alla progettazione, hello verrà creato un disco sempre vuoto.</span><span class="sxs-lookup"><span data-stu-id="200f3-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="200f3-137">Questo scenario include anche nuove istanze create dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="200f3-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="200f3-138">Questo comportamento è perché definizione scaleset hello è un disco dati vuoto.</span><span class="sxs-lookup"><span data-stu-id="200f3-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="200f3-139">Nelle unità di dati pre-popolato toocreate ordine per un modello di set di scalabilità esistente, è possibile scegliere una delle due opzioni:</span><span class="sxs-lookup"><span data-stu-id="200f3-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="200f3-140">Copiare dati dai dischi di dati di hello istanza 0 VM toohello hello altre macchine virtuali eseguendo uno script personalizzato.</span><span class="sxs-lookup"><span data-stu-id="200f3-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="200f3-141">Creare un'immagine gestita con disco hello del sistema operativo più dischi di dati (con dati hello richiesto) e creare un nuovo scaleset con immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="200f3-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="200f3-142">In questo modo ogni nuova macchina virtuale creata disporrà di un tipo di dati su disco che viene fornito nella definizione di hello di hello scaleset.</span><span class="sxs-lookup"><span data-stu-id="200f3-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="200f3-143">Poiché questa definizione farà riferimento tooan immagine con un disco dati che contiene dati personalizzati, ogni macchina virtuale in hello scaleset automaticamente verrà visualizzata con queste modifiche.</span><span class="sxs-lookup"><span data-stu-id="200f3-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="200f3-144">Hello toocreate modo un'immagine personalizzata è disponibili qui: [creare un'immagine gestita di una macchina virtuale generalizzata in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="200f3-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="200f3-145">utente Hello deve hello toocapture istanza 0 macchina virtuale che dispone di hello dati necessari e quindi utilizzare tale disco rigido virtuale per la definizione dell'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="200f3-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="200f3-146">Rimuovere un disco dati da un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="200f3-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="200f3-147">È possibile rimuovere un disco dati da un set di scalabilità di macchine virtuali usando il comando _az vmss disk detach_ dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="200f3-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="200f3-148">Ad esempio hello comando che segue rimuove il disco di hello definito a lun 2:</span><span class="sxs-lookup"><span data-stu-id="200f3-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="200f3-149">Analogamente è possibile rimuovere un disco da un set tramite la rimozione di una voce da hello di scalabilità _dataDisks_ proprietà hello _storageProfile_ e applicazione hello modifica.</span><span class="sxs-lookup"><span data-stu-id="200f3-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="200f3-150">Note aggiuntive</span><span class="sxs-lookup"><span data-stu-id="200f3-150">Additional notes</span></span>
<span data-ttu-id="200f3-151">Il supporto per dischi dati collegati del set di dischi gestiti di Azure e la scala è disponibile nella versione dell'API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) di hello API Microsoft. COMPUTE o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="200f3-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="200f3-152">Nell'implementazione iniziale di hello del supporto di dischi collegati per set di scalabilità, è possibile collegare o scollegare i dischi dati di singole macchine virtuali in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="200f3-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="200f3-153">Il supporto del portale di Azure per i dischi di dati collegati nei set di scalabilità è inizialmente limitato.</span><span class="sxs-lookup"><span data-stu-id="200f3-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="200f3-154">A seconda dei requisiti che è possibile utilizzare modelli di Azure, i dischi collegati da toomanage CLI, PowerShell, gli SDK e API REST.</span><span class="sxs-lookup"><span data-stu-id="200f3-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


