---
title: aaaVirtual macchine in un modello di gestione risorse di Azure | Microsoft Azure
description: "Altre informazioni su come risorsa di macchina virtuale hello è definito in un modello di gestione risorse di Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="75607-103">Macchine virtuali in un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="75607-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="75607-104">In questo articolo descrive alcuni aspetti di un modello di gestione risorse di Azure che si applicano toovirtual macchine.</span><span class="sxs-lookup"><span data-stu-id="75607-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="75607-105">L'articolo descrive un modello completo per la creazione di una macchina virtuale; a tale scopo sono necessarie definizioni di risorse per gli account di archiviazione, le interfacce di rete, gli indirizzi IP pubblici e le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="75607-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="75607-106">Per ulteriori informazioni su come queste risorse possono essere definite insieme, vedere hello [procedura dettagliata di modello di gestione risorse](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="75607-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="75607-107">Esistono molti [modelli raccolta hello](https://azure.microsoft.com/documentation/templates/?term=VM) che includono una risorsa di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="75607-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="75607-108">Di seguito sono descritti solo alcuni elementi che possono essere inclusi in un modello.</span><span class="sxs-lookup"><span data-stu-id="75607-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="75607-109">Questo esempio mostra una sezione di risorse tipica di un modello per la creazione di un numero specificato di VM:</span><span class="sxs-lookup"><span data-stu-id="75607-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
><span data-ttu-id="75607-110">Questo esempio si basa su un account di archiviazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="75607-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="75607-111">È possibile creare account di archiviazione hello mediante la distribuzione da modello hello.</span><span class="sxs-lookup"><span data-stu-id="75607-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="75607-112">esempio Hello si basa inoltre su un'interfaccia di rete e le risorse dipendenti che deve essere definite nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="75607-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="75607-113">Queste risorse non vengono visualizzate nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="75607-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="75607-114">Versione dell'API</span><span class="sxs-lookup"><span data-stu-id="75607-114">API Version</span></span>

<span data-ttu-id="75607-115">Quando si distribuiscono un modello di risorse, è possibile toospecify una versione di hello API toouse.</span><span class="sxs-lookup"><span data-stu-id="75607-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="75607-116">esempio Hello Mostra una risorsa di macchina virtuale hello tramite questo elemento apiVersion:</span><span class="sxs-lookup"><span data-stu-id="75607-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="75607-117">versione di Hello di API specificate nel modello di hello interessa le proprietà che è possibile definire nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="75607-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="75607-118">In generale, selezionare versione API più recente di hello durante la creazione di modelli.</span><span class="sxs-lookup"><span data-stu-id="75607-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="75607-119">Per i modelli esistenti, è possibile decidere se si desidera toocontinue utilizzando una versione precedente di API o aggiornare il modello per hello più recente versione tootake le nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="75607-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="75607-120">Utilizzare queste opportunità per ottenere le versioni dell'API più recente hello:</span><span class="sxs-lookup"><span data-stu-id="75607-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="75607-121">API REST: [Elencare tutti i provider di risorse](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="75607-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="75607-122">PowerShell: [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="75607-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="75607-123">Interfaccia della riga di comando di Azure 2.0: [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="75607-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="75607-124">Parametri e variabili</span><span class="sxs-lookup"><span data-stu-id="75607-124">Parameters and variables</span></span>

<span data-ttu-id="75607-125">[I parametri](../../resource-group-authoring-templates.md) semplificano automaticamente toospecify valori per il modello di hello al momento dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="75607-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="75607-126">In questa sezione parametri viene utilizzata nell'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="75607-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="75607-127">Quando si distribuisce il modello di esempio hello, immettere valori per nome hello e la password dell'account amministratore hello in ogni macchina virtuale e hello il numero di macchine virtuali toocreate.</span><span class="sxs-lookup"><span data-stu-id="75607-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="75607-128">È possibile hello specificando i valori dei parametri in un file distinto che viene gestito con il modello di hello o fornire valori quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="75607-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="75607-129">[Le variabili](../../resource-group-authoring-templates.md) semplificano automaticamente tooset i valori nel modello di hello utilizzate ripetutamente in corso o che possono cambiare nel tempo.</span><span class="sxs-lookup"><span data-stu-id="75607-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="75607-130">In questa sezione variabili viene utilizzata nell'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="75607-130">This variables section is used in hello example:</span></span>

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

<span data-ttu-id="75607-131">Quando si distribuisce il modello di esempio hello, vengono utilizzati i valori delle variabili per nome hello e l'identificatore dell'account di archiviazione hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="75607-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="75607-132">Le variabili sono anche le impostazioni di hello tooprovide utilizzato per l'estensione di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="75607-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="75607-133">Hello utilizzare [procedure consigliate per la creazione di modelli di Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp si decide come toostructure hello parametri e variabili del modello.</span><span class="sxs-lookup"><span data-stu-id="75607-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="75607-134">cicli di risorse</span><span class="sxs-lookup"><span data-stu-id="75607-134">Resource loops</span></span>

<span data-ttu-id="75607-135">Quando sono necessarie più macchine virtuali per l'applicazione, è possibile usare un elemento di copia in un modello.</span><span class="sxs-lookup"><span data-stu-id="75607-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="75607-136">Questo elemento facoltativo consente di scorrere la creazione di hello numero di macchine virtuali che è specificato come parametro:</span><span class="sxs-lookup"><span data-stu-id="75607-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="75607-137">Inoltre, si noti nell'esempio hello che hello indice ciclo viene utilizzato quando alcuni hello specificando i valori per la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="75607-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="75607-138">Ad esempio, se è stato immesso un numero di istanze di tre, i nomi di hello dei dischi del sistema operativo hello sono myOSDisk1 myOSDisk2 e myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="75607-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="75607-139">In questo esempio utilizza dischi gestiti per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="75607-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="75607-140">Tenere presente che la creazione di un ciclo per una risorsa modello di hello potrebbe richiedere si toouse hello ciclo durante la creazione o l'accesso alle altre risorse.</span><span class="sxs-lookup"><span data-stu-id="75607-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="75607-141">Ad esempio, più macchine virtuali non è possibile utilizzare hello stessa interfaccia di rete in modo se il modello esegue un ciclo tramite la creazione di tre macchine virtuali anche necessario scorrere la creazione di tre interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="75607-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="75607-142">Quando si assegna un tooa di interfaccia di rete VM, indice ciclo hello è tooidentify utilizzato è:</span><span class="sxs-lookup"><span data-stu-id="75607-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="75607-143">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="75607-143">Dependencies</span></span>

<span data-ttu-id="75607-144">La maggior parte delle risorse dipendono altri toowork risorse correttamente.</span><span class="sxs-lookup"><span data-stu-id="75607-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="75607-145">Macchine virtuali deve essere associate a una rete virtuale e toodo richiede che un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="75607-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="75607-146">Hello [dependsOn](../../resource-group-define-dependencies.md) elemento è utilizzato toomake interfaccia di rete hello sia pronto toobe utilizzato prima della creazione di macchine virtuali hello:</span><span class="sxs-lookup"><span data-stu-id="75607-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="75607-147">Resource Manager consente di distribuire in parallelo le risorse la cui distribuzione non dipende da un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="75607-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="75607-148">Prestare attenzione quando si impostano le dipendenze in quanto si può rallentare inavvertitamente la distribuzione, specificando dipendenze non necessarie.</span><span class="sxs-lookup"><span data-stu-id="75607-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="75607-149">Le dipendenze possono concatenare più risorse.</span><span class="sxs-lookup"><span data-stu-id="75607-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="75607-150">Ad esempio, l'interfaccia di rete hello dipende indirizzo IP pubblico hello e risorse di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="75607-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="75607-151">Come è possibile stabilire se è necessaria una dipendenza?</span><span class="sxs-lookup"><span data-stu-id="75607-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="75607-152">Esaminare i valori hello che è impostato nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="75607-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="75607-153">Se un elemento nella definizione di risorsa di macchina virtuale hello punta tooanother risorsa che viene distribuito in hello stesso modello, è necessario una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="75607-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="75607-154">Ad esempio, la macchina virtuale di esempio definisce un profilo di rete:</span><span class="sxs-lookup"><span data-stu-id="75607-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="75607-155">tooset questa proprietà, l'interfaccia di rete hello deve esistere.</span><span class="sxs-lookup"><span data-stu-id="75607-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="75607-156">Pertanto, è necessaria una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="75607-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="75607-157">È necessario anche tooset una dipendenza quando è definita una risorsa (figlio) all'interno di un'altra risorsa (un elemento padre).</span><span class="sxs-lookup"><span data-stu-id="75607-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="75607-158">Ad esempio, le impostazioni di diagnostica hello e le estensioni degli script personalizzati sono entrambi definiti come risorse figlio di una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="75607-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="75607-159">Non è possibile creare fino a quando non esistono macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="75607-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="75607-160">Di conseguenza, entrambe le risorse sono contrassegnate come dipendenti nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="75607-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="75607-161">Profili</span><span class="sxs-lookup"><span data-stu-id="75607-161">Profiles</span></span>

<span data-ttu-id="75607-162">Quando si definisce una risorsa di macchina virtuale, vengono usati diversi elementi di profilo.</span><span class="sxs-lookup"><span data-stu-id="75607-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="75607-163">Alcuni sono necessari e alcuni sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="75607-163">Some are required and some are optional.</span></span> <span data-ttu-id="75607-164">Ad esempio, gli elementi hardwareProfile, osProfile, storageProfile e profilo di hello sono obbligatori, ma diagnosticsProfile hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="75607-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="75607-165">Questi profili definiscono impostazioni, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="75607-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="75607-166">dimensione</span><span class="sxs-lookup"><span data-stu-id="75607-166">size</span></span>](sizes.md)
- <span data-ttu-id="75607-167">[nome](/architecture/best-practices/naming-conventions) e credenziali</span><span class="sxs-lookup"><span data-stu-id="75607-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="75607-168">disco e [impostazioni del sistema operativo](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="75607-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="75607-169">interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="75607-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="75607-170">diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="75607-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="75607-171">Dischi e immagini</span><span class="sxs-lookup"><span data-stu-id="75607-171">Disks and images</span></span>
   
<span data-ttu-id="75607-172">In Azure i file del disco rigido virtuale possono rappresentare [dischi o immagini](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75607-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="75607-173">Quando il sistema operativo hello in un file vhd è specializzato toobe una macchina virtuale specifica, è tooas di cui si fa riferimento un disco.</span><span class="sxs-lookup"><span data-stu-id="75607-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="75607-174">Il sistema operativo hello in un file di disco rigido virtuale generalizzato toobe usato toocreate più macchine virtuali, è un'immagine di tooas cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="75607-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="75607-175">Creare nuove macchine virtuali e nuovi dischi da un'immagine della piattaforma</span><span class="sxs-lookup"><span data-stu-id="75607-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="75607-176">Quando si crea una macchina virtuale, è necessario decidere quali toouse del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="75607-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="75607-177">elemento imageReference Hello è usato toodefine hello operativo di una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="75607-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="75607-178">esempio Hello viene illustrata una definizione per un sistema operativo Windows Server:</span><span class="sxs-lookup"><span data-stu-id="75607-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="75607-179">Se si desidera toocreate un sistema operativo Linux, è possibile utilizzare questa definizione:</span><span class="sxs-lookup"><span data-stu-id="75607-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="75607-180">Impostazioni di configurazione per disco del sistema operativo hello assegnate con elemento osDisk hello.</span><span class="sxs-lookup"><span data-stu-id="75607-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="75607-181">Hello esempio definisce un nuovo disco gestito con la memorizzazione nella cache in modalità set troppo hello**ReadWrite** e tale disco hello viene creato da un [immagine della piattaforma](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="75607-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="75607-182">Creare nuove macchine virtuali da dischi gestiti esistenti</span><span class="sxs-lookup"><span data-stu-id="75607-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="75607-183">Se si desidera toocreate le macchine virtuali dai dischi esistenti, rimuovere imageReference hello e gli elementi di osProfile hello e definire queste impostazioni del disco:</span><span class="sxs-lookup"><span data-stu-id="75607-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="75607-184">Creare nuove macchine virtuali da un'immagine gestita</span><span class="sxs-lookup"><span data-stu-id="75607-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="75607-185">Se si desidera toocreate una macchina virtuale da un'immagine gestita, modificare l'elemento imageReference hello e definire queste impostazioni del disco:</span><span class="sxs-lookup"><span data-stu-id="75607-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a><span data-ttu-id="75607-186">Collegare i dischi dei dati</span><span class="sxs-lookup"><span data-stu-id="75607-186">Attach data disks</span></span>

<span data-ttu-id="75607-187">È possibile aggiungere facoltativamente toohello dischi dati le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="75607-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="75607-188">Hello [numero di dischi](sizes.md) dipende dalle dimensioni hello del disco del sistema operativo in uso.</span><span class="sxs-lookup"><span data-stu-id="75607-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="75607-189">Dimensioni delle macchine virtuali hello hello impostare tooStandard_DS1_v2, numero massimo di hello di dischi dati che è stato possibile aggiungere toohello li è due.</span><span class="sxs-lookup"><span data-stu-id="75607-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="75607-190">Nell'esempio hello, un disco dati gestiti viene aggiunto tooeach VM:</span><span class="sxs-lookup"><span data-stu-id="75607-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a><span data-ttu-id="75607-191">Estensioni</span><span class="sxs-lookup"><span data-stu-id="75607-191">Extensions</span></span>

<span data-ttu-id="75607-192">Sebbene [estensioni](extensions-features.md) sono una risorsa distinta, tooVMs strettamente collegati.</span><span class="sxs-lookup"><span data-stu-id="75607-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="75607-193">Le estensioni possono essere aggiunte come risorsa figlio di hello macchina virtuale o come una risorsa distinta.</span><span class="sxs-lookup"><span data-stu-id="75607-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="75607-194">esempio Hello Mostra hello [estensione diagnostica](extensions-diagnostics-template.md) da aggiungere le macchine virtuali toohello:</span><span class="sxs-lookup"><span data-stu-id="75607-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

<span data-ttu-id="75607-195">Questa risorsa di estensione Usa variabile storageName hello e i valori di tooprovide di hello delle variabili di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="75607-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="75607-196">Se si desiderano toochange hello i dati raccolti da questa estensione, è possibile aggiungere più variabile di wadperfcounters toohello di contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="75607-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="75607-197">È anche possibile scegliere i dati di diagnostica hello tooput in un account di spazio di archiviazione diverso da quello in cui sono archiviati i dischi di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="75607-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="75607-198">Sono disponibili numerose estensioni che è possibile installare in una macchina virtuale, ma hello più utile è probabilmente hello [estensione Script personalizzata](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="75607-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="75607-199">Nell'esempio hello in ogni macchina virtuale all'avvio viene eseguito uno script di PowerShell denominato start.ps1:</span><span class="sxs-lookup"><span data-stu-id="75607-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

<span data-ttu-id="75607-200">script start.ps1 Hello può eseguire molte attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="75607-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="75607-201">Ad esempio, non vengono inizializzati i dischi dati hello toohello macchine virtuali aggiunte nell'esempio hello; è possibile utilizzare un tooinitialize script personalizzato li.</span><span class="sxs-lookup"><span data-stu-id="75607-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="75607-202">Se si dispone di più toodo di attività di avvio, è possibile utilizzare hello start.ps1 file toocall altri script di PowerShell nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="75607-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="75607-203">esempio Hello Usa PowerShell, ma è possibile utilizzare qualsiasi metodo di scripting che sono disponibile nel sistema operativo hello che si sta utilizzando.</span><span class="sxs-lookup"><span data-stu-id="75607-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="75607-204">È possibile visualizzare lo stato di hello delle estensioni di hello installato dalle impostazioni di estensioni hello nel portale di hello:</span><span class="sxs-lookup"><span data-stu-id="75607-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![Recuperare lo stato dell'estensione](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="75607-206">È anche possibile ottenere informazioni sull'estensione utilizzando hello **Get AzureRmVMExtension** PowerShell comando hello **get estensione vm** comando CLI di Azure 2.0 o hello **ottenere informazioni sull'estensione**  API REST.</span><span class="sxs-lookup"><span data-stu-id="75607-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="75607-207">Deployments</span><span class="sxs-lookup"><span data-stu-id="75607-207">Deployments</span></span>

<span data-ttu-id="75607-208">Quando si distribuisce un modello di risorse hello Azure rileva che è stato distribuito come un gruppo e automaticamente assegna un nome di gruppo toothis distribuito.</span><span class="sxs-lookup"><span data-stu-id="75607-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="75607-209">nome Hello della distribuzione di hello è hello corrisponde al nome hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="75607-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="75607-210">Se si desidera conoscere lo stato di hello delle risorse nella distribuzione di hello, è possibile utilizzare il pannello di gruppo di risorse hello in hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="75607-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![Ottenere informazioni sulla distribuzione](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="75607-212">Non è un problema toouse hello stesso modello toocreate le risorse o le risorse esistenti tooupdate.</span><span class="sxs-lookup"><span data-stu-id="75607-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="75607-213">Quando si utilizzano comandi toodeploy modelli, è necessario hello opportunità toosay che [modalità](../../resource-group-template-deploy.md) desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="75607-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="75607-214">è possibile impostare modalità Hello tooeither **completa** o **incrementale**.</span><span class="sxs-lookup"><span data-stu-id="75607-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="75607-215">valore predefinito di Hello è aggiornamenti incrementali toodo.</span><span class="sxs-lookup"><span data-stu-id="75607-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="75607-216">Prestare attenzione nell'utilizzo hello **completa** modalità perché accidentalmente eliminate le risorse.</span><span class="sxs-lookup"><span data-stu-id="75607-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="75607-217">Quando si imposta la modalità hello troppo**completa**, Gestione risorse consente di eliminare tutte le risorse nel gruppo di risorse hello che non sono presenti nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="75607-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75607-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75607-218">Next Steps</span></span>

- <span data-ttu-id="75607-219">È possibile creare un modello personalizzato usando le informazioni presenti in [Creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="75607-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="75607-220">Distribuire il modello di hello creati usando [creare una macchina virtuale Windows con un modello di gestione risorse](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="75607-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="75607-221">Informazioni su come toomanage hello macchine virtuali creato esaminando [creare e gestire macchine virtuali di Windows con il modulo di Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75607-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
