# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="122bb-101">Uso di Managed Disks nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="122bb-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="122bb-102">Questo documento descrive come differenze hello tra dischi gestiti e quando si usano macchine virtuali di Azure Resource Manager modelli tooprovision.</span><span class="sxs-lookup"><span data-stu-id="122bb-102">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="122bb-103">Ciò consentirà di modelli tooupdate esistenti con i dischi toomanaged di dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="122bb-103">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="122bb-104">Per riferimento, usiamo hello [windows semplice di vm 101](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) modello come guida.</span><span class="sxs-lookup"><span data-stu-id="122bb-104">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="122bb-105">È possibile visualizzare il modello di hello utilizzando entrambi [dischi gestiti](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) e una versione precedente utilizzando [non gestita dischi](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) se si desidera toodirectly confrontarli.</span><span class="sxs-lookup"><span data-stu-id="122bb-105">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="122bb-106">Formattazione del modello per dischi non gestiti</span><span class="sxs-lookup"><span data-stu-id="122bb-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="122bb-107">toobegin, verranno esaminate in dischi come non gestiti vengono distribuiti.</span><span class="sxs-lookup"><span data-stu-id="122bb-107">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="122bb-108">Durante la creazione di dischi non gestiti, è necessario un file VHD di hello toohold di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="122bb-108">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="122bb-109">È possibile creare un nuovo account di archiviazione o usarne uno già esistente.</span><span class="sxs-lookup"><span data-stu-id="122bb-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="122bb-110">In questo articolo viene illustrato come toocreate un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="122bb-110">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="122bb-111">tooaccomplish, è necessario una risorsa di account di archiviazione in blocco di risorse hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="122bb-111">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

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

<span data-ttu-id="122bb-112">Oggetto macchina virtuale hello, abbiamo bisogno di una dipendenza tooensure di account di archiviazione hello che ha creato prima macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="122bb-112">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="122bb-113">All'interno di hello `storageProfile` sezione, è quindi possibile specificare un URI completo della posizione del disco rigido virtuale che fa riferimento all'account di archiviazione hello ed è necessario per il disco del sistema operativo hello e qualsiasi disco dati hello hello.</span><span class="sxs-lookup"><span data-stu-id="122bb-113">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="122bb-114">Formattazione del modello per dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="122bb-114">Managed disks template formatting</span></span>

<span data-ttu-id="122bb-115">Con i dischi gestiti di Azure, disco hello diventa una risorsa di primo livello e non richiede più un toobe di account di archiviazione creato dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="122bb-115">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="122bb-116">Dischi gestiti prima esposte nel hello `2016-04-30-preview` versione dell'API, sono disponibili in tutte le versioni API successive e sono di tipo di disco predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="122bb-116">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="122bb-117">Hello nelle sezioni seguenti vengono dettagliatamente le impostazioni predefinite di hello e in dettaglio come toofurther personalizzare i dischi.</span><span class="sxs-lookup"><span data-stu-id="122bb-117">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="122bb-118">È consigliabile toouse un'API versione successiva a quella `2016-04-30-preview` come sono state eseguite modifiche di rilievo tra `2016-04-30-preview` e `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="122bb-118">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="122bb-119">Impostazioni predefinite per i dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="122bb-119">Default managed disk settings</span></span>

<span data-ttu-id="122bb-120">toocreate una macchina virtuale con dischi gestiti, non sono più necessari risorsa account di archiviazione hello toocreate e può aggiornare la risorsa di macchina virtuale come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="122bb-120">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="122bb-121">In particolare si noti che hello `apiVersion` riflette `2017-03-30` hello e `osDisk` e `dataDisks` non è più fare riferimento tooa URI specifico per hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="122bb-121">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="122bb-122">Quando si distribuisce senza specificare proprietà aggiuntive, verrà utilizzato il disco hello [archiviazione con ridondanza locale Standard](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="122bb-122">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="122bb-123">Se viene specificato alcun nome, ha formato hello `<VMName>_OsDisk_1_<randomstring>` per il disco del sistema operativo hello e `<VMName>_disk<#>_<randomstring>` per ogni disco dati.</span><span class="sxs-lookup"><span data-stu-id="122bb-123">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="122bb-124">Per impostazione predefinita, la crittografia del disco di Azure è disabilitata; la memorizzazione nella cache è di lettura/scrittura per il disco del sistema operativo hello e Nessuno per i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="122bb-124">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="122bb-125">È possibile riscontrare nel seguente esempio hello che sia ancora disponibile una dipendenza di account di archiviazione, anche se questo è solo per l'archiviazione di diagnostica e non è necessaria per l'archiviazione su disco.</span><span class="sxs-lookup"><span data-stu-id="122bb-125">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="122bb-126">Uso di una risorsa disco gestito di primo livello</span><span class="sxs-lookup"><span data-stu-id="122bb-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="122bb-127">Come una configurazione del disco hello toospecifying alternativo nell'oggetto macchina virtuale hello, è possibile creare una risorsa disco di primo livello e associarlo come parte della creazione della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="122bb-127">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="122bb-128">Ad esempio, è possibile creare una risorsa disco, come indicato di seguito toouse come disco dati.</span><span class="sxs-lookup"><span data-stu-id="122bb-128">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

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

<span data-ttu-id="122bb-129">Oggetto VM hello, è possibile fare riferimento questo toobe di oggetto disco collegato.</span><span class="sxs-lookup"><span data-stu-id="122bb-129">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="122bb-130">Specifica dell'ID di risorsa hello di hello gestiti disco creata in hello `managedDisk` proprietà consente di collegare hello unità disco hello come hello viene creata la VM.</span><span class="sxs-lookup"><span data-stu-id="122bb-130">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="122bb-131">Si noti che hello `apiVersion` per hello risorsa macchina virtuale è troppo`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="122bb-131">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="122bb-132">Si noti inoltre che abbiamo creato una dipendenza su hello disco risorse tooensure che è stato creato correttamente prima della creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="122bb-132">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="122bb-133">Creare set di disponibilità gestiti con macchine virtuali che usano dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="122bb-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="122bb-134">toocreate gestiti disponibilità set con macchine virtuali con dischi gestiti, aggiungere hello `sku` disponibilità toohello oggetto set di risorse e set hello `name` proprietà troppo`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="122bb-134">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="122bb-135">In questo modo si garantisce che i dischi di hello per ogni macchina virtuale sono sufficientemente isolati tra loro tooavoid singoli punti di errore.</span><span class="sxs-lookup"><span data-stu-id="122bb-135">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="122bb-136">Si noti inoltre che hello `apiVersion` per risorsa del set di disponibilità hello è troppo`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="122bb-136">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="122bb-137">Altri scenari e personalizzazioni</span><span class="sxs-lookup"><span data-stu-id="122bb-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="122bb-138">toofind informazioni complete sulle specifiche di hello API REST, vedere hello [creare un disco gestito documentazione dell'API REST](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="122bb-138">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="122bb-139">Sono disponibili ulteriori scenari, così come impostazione predefinita e i valori accettabili che possono essere inviati toohello API tramite distribuzioni modello.</span><span class="sxs-lookup"><span data-stu-id="122bb-139">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="122bb-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="122bb-140">Next steps</span></span>

* <span data-ttu-id="122bb-141">Per i modelli completi che usano dischi gestiti visitare hello seguenti collegamenti repository Guida introduttiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="122bb-141">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="122bb-142">Macchina virtuale Windows con disco gestito</span><span class="sxs-lookup"><span data-stu-id="122bb-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="122bb-143">Macchina virtuale Linux con disco gestito</span><span class="sxs-lookup"><span data-stu-id="122bb-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="122bb-144">Elenco completo dei modelli con disco gestito</span><span class="sxs-lookup"><span data-stu-id="122bb-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="122bb-145">Visitare hello [Panoramica di dischi gestiti di Azure](../articles/virtual-machines/windows/managed-disks-overview.md) documento toolearn ulteriori informazioni sui dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="122bb-145">Visit hello [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="122bb-146">Esaminare la documentazione di riferimento di modello hello per le risorse della macchina virtuale, visitare hello [riferimento a un modello Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) documento.</span><span class="sxs-lookup"><span data-stu-id="122bb-146">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="122bb-147">Esaminare la documentazione di riferimento di modello hello per le risorse disco visitando hello [riferimento a un modello Microsoft.Compute/disks](/templates/microsoft.compute/disks) documento.</span><span class="sxs-lookup"><span data-stu-id="122bb-147">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
