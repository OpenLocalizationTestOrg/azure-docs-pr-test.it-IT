---
title: Uso dei dischi gestiti nei modelli di Azure Resource Manager | Microsoft Docs
description: Illustra come usare i dischi gestiti nei modelli di Azure Resource Manager
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: 4c502784a57850d6f11200e95f7432d2206e920a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="74b80-103">Uso di Managed Disks nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="74b80-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="74b80-104">Questo documento descrive le differenze tra dischi gestiti e non gestiti quando si usano i modelli di Azure Resource Manager per eseguire il provisioning di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="74b80-104">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="74b80-105">Le informazioni sono utili per aggiornare i modelli esistenti con dischi non gestiti per l'uso dei dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="74b80-105">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="74b80-106">A titolo di riferimento, come guida viene usato il modello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows).</span><span class="sxs-lookup"><span data-stu-id="74b80-106">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="74b80-107">Per un eventuale confronto diretto, è possibile visualizzare sia il modello per l'uso di [dischi gestiti](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json), sia una versione precedente per [dischi non gestiti](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="74b80-107">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="74b80-108">Formattazione del modello per dischi non gestiti</span><span class="sxs-lookup"><span data-stu-id="74b80-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="74b80-109">Per iniziare, viene esaminata la modalità di distribuzione dei dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="74b80-109">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="74b80-110">Quando si creano dischi non gestiti, è necessario un account di archiviazione in cui salvare i file VHD.</span><span class="sxs-lookup"><span data-stu-id="74b80-110">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="74b80-111">È possibile creare un nuovo account di archiviazione o usarne uno già esistente.</span><span class="sxs-lookup"><span data-stu-id="74b80-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="74b80-112">Questo articolo illustra come creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="74b80-112">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="74b80-113">A questo scopo, è necessario una risorsa account di archiviazione nel blocco delle risorse, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="74b80-113">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="74b80-114">All'interno dell'oggetto macchina virtuale è necessaria una dipendenza dall'account di archiviazione, per assicurarsi che venga creato prima della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="74b80-114">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="74b80-115">All'interno della sezione `storageProfile` viene quindi specificato l'URI completo del percorso del disco rigido virtuale, che fa riferimento all'account di archiviazione ed è necessario per il disco del sistema operativo e i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="74b80-115">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="74b80-116">Formattazione del modello per dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="74b80-116">Managed disks template formatting</span></span>

<span data-ttu-id="74b80-117">Con Azure Managed Disks, il disco diventa una risorsa di primo livello e non richiede più la creazione di un account di archiviazione da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="74b80-117">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="74b80-118">I dischi gestiti sono stati prima esposti nella versione `2016-04-30-preview` dell'API, sono disponibili in tutte le versioni API successive e sono ora il tipo di disco predefinito.</span><span class="sxs-lookup"><span data-stu-id="74b80-118">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="74b80-119">Le sezioni seguenti descrivono in modo dettagliato le impostazioni predefinite e illustrano come personalizzare ulteriormente i dischi.</span><span class="sxs-lookup"><span data-stu-id="74b80-119">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="74b80-120">È consigliabile usare una versione dell'API successiva rispetto a `2016-04-30-preview` poiché sono state eseguite delle modifiche di rilievo tra `2016-04-30-preview` e `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="74b80-120">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="74b80-121">Impostazioni predefinite per i dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="74b80-121">Default managed disk settings</span></span>

<span data-ttu-id="74b80-122">Per creare una macchina virtuale con dischi gestiti, non è più necessario creare la risorsa account di archiviazione ed è possibile aggiornare la risorsa macchina virtuale come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="74b80-122">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="74b80-123">Si noti in particolare che `apiVersion` corrisponde a `2017-03-30` e che `osDisk` e `dataDisks` non fanno più riferimento a uno specifico URI per il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="74b80-123">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="74b80-124">Quando si distribuisce senza specificare proprietà aggiuntive, il disco usa l'[archiviazione con ridondanza locale Standard](storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="74b80-124">When deploying without specifying additional properties, the disk will use [Standard LRS storage](storage-redundancy.md).</span></span> <span data-ttu-id="74b80-125">Se non si specifica un nome, assume il formato `<VMName>_OsDisk_1_<randomstring>` per il disco del sistema operativo e `<VMName>_disk<#>_<randomstring>` per ogni disco dati.</span><span class="sxs-lookup"><span data-stu-id="74b80-125">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="74b80-126">Per impostazione predefinita, la crittografia dischi di Azure è disattivata; la memorizzazione nella cache è impostata su lettura/scrittura per il disco del sistema operativo e disattivata per i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="74b80-126">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="74b80-127">Nell'esempio seguente si può osservare che è ancora presente una dipendenza dall'account di archiviazione, ma è solo per l'archiviazione della diagnostica e non è necessaria per l'archiviazione su disco.</span><span class="sxs-lookup"><span data-stu-id="74b80-127">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="74b80-128">Uso di una risorsa disco gestito di primo livello</span><span class="sxs-lookup"><span data-stu-id="74b80-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="74b80-129">Come alternativa alla specifica della configurazione del disco nell'oggetto macchina virtuale, è possibile creare una risorsa disco di primo livello e collegarla nell'ambito della creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="74b80-129">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="74b80-130">Ad esempio, è possibile creare una risorsa disco come segue per usarla come disco dati.</span><span class="sxs-lookup"><span data-stu-id="74b80-130">For example, we can create a disk resource as follows to use as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="74b80-131">All'interno dell'oggetto macchina virtuale, è quindi possibile fare riferimento all'oggetto disco da collegare.</span><span class="sxs-lookup"><span data-stu-id="74b80-131">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="74b80-132">Specificare l'ID risorsa del disco gestito creato nella proprietà `managedDisk` consente di collegare il disco non appena viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="74b80-132">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="74b80-133">Si noti che `apiVersion` per la risorsa della macchina virtuale è impostato su `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="74b80-133">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="74b80-134">Si noti inoltre che è stata creata una dipendenza dalla risorsa disco per garantire che sia correttamente creata prima della creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="74b80-134">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="74b80-135">Creare set di disponibilità gestiti con macchine virtuali che usano dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="74b80-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="74b80-136">Per creare set di disponibilità gestiti con macchine virtuali che usano dischi gestiti, aggiungere l'oggetto `sku` alla risorsa set di disponibilità e impostare la proprietà `name` su `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="74b80-136">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="74b80-137">In questo modo si garantisce che i dischi per ogni macchina virtuale siano sufficientemente isolati tra loro da evitare singoli punti di errore.</span><span class="sxs-lookup"><span data-stu-id="74b80-137">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="74b80-138">Si noti anche che `apiVersion` per la risorsa del set di disponibilità è impostato su `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="74b80-138">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="74b80-139">Altri scenari e personalizzazioni</span><span class="sxs-lookup"><span data-stu-id="74b80-139">Additional scenarios and customizations</span></span>

<span data-ttu-id="74b80-140">Per informazioni complete sulle specifiche dell'API REST, vedere la [documentazione dell'API REST per la creazione di un disco gestito](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="74b80-140">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="74b80-141">La documentazione contiene scenari aggiuntivi e informazioni sui valori predefiniti e accettabili che è possibile inviare all'API tramite distribuzioni di modelli.</span><span class="sxs-lookup"><span data-stu-id="74b80-141">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="74b80-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74b80-142">Next steps</span></span>

* <span data-ttu-id="74b80-143">Per modelli completi che usano dischi gestiti, visitare i collegamenti seguenti al repository di modelli di avvio rapido di Azure.</span><span class="sxs-lookup"><span data-stu-id="74b80-143">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="74b80-144">Macchina virtuale Windows con disco gestito</span><span class="sxs-lookup"><span data-stu-id="74b80-144">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="74b80-145">Macchina virtuale Linux con disco gestito</span><span class="sxs-lookup"><span data-stu-id="74b80-145">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="74b80-146">Elenco completo dei modelli con disco gestito</span><span class="sxs-lookup"><span data-stu-id="74b80-146">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="74b80-147">Per altre informazioni sui dischi gestiti, vedere [Panoramica di Azure Managed Disks](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74b80-147">Visit the [Azure Managed Disks Overview](storage-managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="74b80-148">La documentazione di riferimento del modello per le risorse macchina virtuale è disponibile alla pagina [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines).</span><span class="sxs-lookup"><span data-stu-id="74b80-148">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="74b80-149">La documentazione di riferimento del modello per le risorse disco è disponibile alla pagina [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks).</span><span class="sxs-lookup"><span data-stu-id="74b80-149">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
