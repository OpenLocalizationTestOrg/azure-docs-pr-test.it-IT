---
title: Macchine virtuali in un modello di Azure Resource Manager | Microsoft Azure
description: Altre informazioni su come definire la risorsa della macchina virtuale in un modello di Azure Resource Manager.
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
ms.openlocfilehash: d9b9121bc5e38396ba4def6c17f9b373c2b48056
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="1bf26-103">Macchine virtuali in un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1bf26-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="1bf26-104">Questo articolo descrive gli aspetti di un modello di Azure Resource Manager che si applicano alle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1bf26-104">This article describes aspects of an Azure Resource Manager template that apply to virtual machines.</span></span> <span data-ttu-id="1bf26-105">L'articolo descrive un modello completo per la creazione di una macchina virtuale; a tale scopo sono necessarie definizioni di risorse per gli account di archiviazione, le interfacce di rete, gli indirizzi IP pubblici e le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="1bf26-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="1bf26-106">Per altre informazioni su come queste risorse possono essere definite insieme, vedere [Procedura dettagliata per un modello di Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="1bf26-106">For more information about how these resources can be defined together, see the [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="1bf26-107">Sono disponibili numerosi [modelli nella raccolta](https://azure.microsoft.com/documentation/templates/?term=VM) che includono la risorsa di VM.</span><span class="sxs-lookup"><span data-stu-id="1bf26-107">There are many [templates in the gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include the VM resource.</span></span> <span data-ttu-id="1bf26-108">Di seguito sono descritti solo alcuni elementi che possono essere inclusi in un modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="1bf26-109">Questo esempio mostra una sezione di risorse tipica di un modello per la creazione di un numero specificato di VM:</span><span class="sxs-lookup"><span data-stu-id="1bf26-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="1bf26-110">Questo esempio si basa su un account di archiviazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1bf26-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="1bf26-111">È possibile creare l'account di archiviazione mediante la distribuzione dal modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-111">You could create the storage account by deploying it from the template.</span></span> <span data-ttu-id="1bf26-112">L'esempio si basa anche su un'interfaccia di rete e le risorse dipendenti definite nel modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-112">The example also relies on a network interface and its dependent resources that would be defined in the template.</span></span> <span data-ttu-id="1bf26-113">Queste risorse non vengono visualizzate nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="1bf26-113">These resources are not shown in the example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="1bf26-114">Versione dell'API</span><span class="sxs-lookup"><span data-stu-id="1bf26-114">API Version</span></span>

<span data-ttu-id="1bf26-115">Quando si distribuiscono risorse usando un modello, è necessario specificare una versione dell'API da usare.</span><span class="sxs-lookup"><span data-stu-id="1bf26-115">When you deploy resources using a template, you have to specify a version of the API to use.</span></span> <span data-ttu-id="1bf26-116">L'esempio illustra l'uso di questa risorsa di macchina virtuale usando l'elemento apiVersion:</span><span class="sxs-lookup"><span data-stu-id="1bf26-116">The example shows the virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="1bf26-117">La versione dell'API specificata nel modello influisce sulle proprietà che è possibile definire nel modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-117">The version of the API you specify in your template affects which properties you can define in the template.</span></span> <span data-ttu-id="1bf26-118">In generale, è opportuno selezionare la versione più recente dell'API durante la creazione di modelli.</span><span class="sxs-lookup"><span data-stu-id="1bf26-118">In general, you should select the most recent API version when creating templates.</span></span> <span data-ttu-id="1bf26-119">Per i modelli esistenti, è possibile decidere se si desidera continuare a usare una versione precedente dell'API o aggiornare il modello alla versione più recente per sfruttare i vantaggi delle nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1bf26-119">For existing templates, you can decide whether you want to continue using an earlier API version, or update your template for the latest version to take advantage of new features.</span></span>

<span data-ttu-id="1bf26-120">Per ottenere le versioni dell'API più aggiornate:</span><span class="sxs-lookup"><span data-stu-id="1bf26-120">Use these opportunities for getting the latest API versions:</span></span>

- <span data-ttu-id="1bf26-121">API REST: [Elencare tutti i provider di risorse](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="1bf26-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="1bf26-122">PowerShell: [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="1bf26-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="1bf26-123">Interfaccia della riga di comando di Azure 2.0: [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="1bf26-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="1bf26-124">Parametri e variabili</span><span class="sxs-lookup"><span data-stu-id="1bf26-124">Parameters and variables</span></span>

<span data-ttu-id="1bf26-125">I [parametri](../../resource-group-authoring-templates.md) semplificano la specifica di valori per il modello quando viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="1bf26-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you to specify values for the template when you run it.</span></span> <span data-ttu-id="1bf26-126">Nell'esempio viene usata questa sezione dei parametri:</span><span class="sxs-lookup"><span data-stu-id="1bf26-126">This parameters section is used in the example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="1bf26-127">Quando si distribuisce il modello di esempio, si immettono valori per il nome e la password dell'account amministratore in ogni VM e il numero di VM da creare.</span><span class="sxs-lookup"><span data-stu-id="1bf26-127">When you deploy the example template, you enter values for the name and password of the administrator account on each VM and the number of VMs to create.</span></span> <span data-ttu-id="1bf26-128">È possibile scegliere di specificare i valori di parametri in un file separato gestito con il modello o fornire i valori quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="1bf26-128">You have the option of specifying parameter values in a separate file that's managed with the template, or providing values when prompted.</span></span>

<span data-ttu-id="1bf26-129">Le [variabili](../../resource-group-authoring-templates.md) semplificano la configurazione di valori nel modello usati ripetutamente o che possono cambiare nel tempo.</span><span class="sxs-lookup"><span data-stu-id="1bf26-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you to set up values in the template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="1bf26-130">L'esempio usa questa sezione delle variabili:</span><span class="sxs-lookup"><span data-stu-id="1bf26-130">This variables section is used in the example:</span></span>

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

<span data-ttu-id="1bf26-131">Quando si distribuisce il modello di esempio, vengono usati valori di variabili per il nome e l'identificatore dell'account di archiviazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1bf26-131">When you deploy the example template, variable values are used for the name and identifier of the previously created storage account.</span></span> <span data-ttu-id="1bf26-132">Le variabili consentono anche di fornire le impostazioni per l'estensione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="1bf26-132">Variables are also used to provide the settings for the diagnostic extension.</span></span> <span data-ttu-id="1bf26-133">Usare le [procedure consigliate per la creazione di Azure Resource Manager](../../resource-manager-template-best-practices.md) per decidere come si vuole organizzare i parametri e le variabili del modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-133">Use the [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) to help you decide how you want to structure the parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="1bf26-134">cicli di risorse</span><span class="sxs-lookup"><span data-stu-id="1bf26-134">Resource loops</span></span>

<span data-ttu-id="1bf26-135">Quando sono necessarie più macchine virtuali per l'applicazione, è possibile usare un elemento di copia in un modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="1bf26-136">Questo elemento facoltativo esegue il ciclo di creazione del numero di VM specificato come parametro:</span><span class="sxs-lookup"><span data-stu-id="1bf26-136">This optional element loops through creating the number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="1bf26-137">Si noti anche nell'esempio che l'indice di ciclo viene usato quando si specificano alcuni valori per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="1bf26-137">Also, notice in the example that the loop index is used when specifying some of the values for the resource.</span></span> <span data-ttu-id="1bf26-138">Ad esempio, se è stato immesso un numero di istanze pari a tre, i nomi dei dischi del sistema operativo sono myOSDisk1, myOSDisk2 e myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="1bf26-138">For example, if you entered an instance count of three, the names of the operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="1bf26-139">Questo esempio usa dischi gestiti per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1bf26-139">This example uses managed disks for the virtual machines.</span></span>
>
>

<span data-ttu-id="1bf26-140">Tenere presente che la creazione di un ciclo per una risorsa nel modello potrebbe richiedere di usare il ciclo quando si crea o si accede ad altre risorse.</span><span class="sxs-lookup"><span data-stu-id="1bf26-140">Keep in mind that creating a loop for one resource in the template may require you to use the loop when creating or accessing other resources.</span></span> <span data-ttu-id="1bf26-141">Ad esempio, più VM non possono usare la stessa interfaccia di rete; pertanto se esegue il ciclo di creazione di tre VM, il modello deve anche eseguire il ciclo di creazione di tre interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="1bf26-141">For example, multiple VMs can’t use the same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="1bf26-142">Quando si assegna un'interfaccia di rete a una VM, l'indice di ciclo viene usato per la relativa identificazione:</span><span class="sxs-lookup"><span data-stu-id="1bf26-142">When assigning a network interface to a VM, the loop index is used to identify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="1bf26-143">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="1bf26-143">Dependencies</span></span>

<span data-ttu-id="1bf26-144">Il corretto funzionamento della maggior parte delle risorse dipende dalle altre risorse.</span><span class="sxs-lookup"><span data-stu-id="1bf26-144">Most resources depend on other resources to work correctly.</span></span> <span data-ttu-id="1bf26-145">Le macchine virtuali deve essere associate a una rete virtuale e a tale scopo è necessaria un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="1bf26-145">Virtual machines must be associated with a virtual network and to do that it needs a network interface.</span></span> <span data-ttu-id="1bf26-146">L'elemento [dependsOn](../../resource-group-define-dependencies.md) viene usato per verificare che l'interfaccia di rete sia pronta per essere usata prima che vengano create le VM:</span><span class="sxs-lookup"><span data-stu-id="1bf26-146">The [dependsOn](../../resource-group-define-dependencies.md) element is used to make sure that the network interface is ready to be used before the VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="1bf26-147">Resource Manager consente di distribuire in parallelo le risorse la cui distribuzione non dipende da un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="1bf26-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="1bf26-148">Prestare attenzione quando si impostano le dipendenze in quanto si può rallentare inavvertitamente la distribuzione, specificando dipendenze non necessarie.</span><span class="sxs-lookup"><span data-stu-id="1bf26-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="1bf26-149">Le dipendenze possono concatenare più risorse.</span><span class="sxs-lookup"><span data-stu-id="1bf26-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="1bf26-150">Ad esempio, l'interfaccia di rete dipende dall'indirizzo IP pubblico e dalle risorse della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1bf26-150">For example, the network interface depends on the public IP address and virtual network resources.</span></span>

<span data-ttu-id="1bf26-151">Come è possibile stabilire se è necessaria una dipendenza?</span><span class="sxs-lookup"><span data-stu-id="1bf26-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="1bf26-152">Esaminare i valori impostati nel modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-152">Look at the values you set in the template.</span></span> <span data-ttu-id="1bf26-153">Una dipendenza è necessaria se un elemento nella definizione di risorsa della macchina virtuale punta a un'altra risorsa distribuita nello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-153">If an element in the virtual machine resource definition points to another resource that is deployed in the same template, you need a dependency.</span></span> <span data-ttu-id="1bf26-154">Ad esempio, la macchina virtuale di esempio definisce un profilo di rete:</span><span class="sxs-lookup"><span data-stu-id="1bf26-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="1bf26-155">Per impostare questa proprietà, è necessario che esista l'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="1bf26-155">To set this property, the network interface must exist.</span></span> <span data-ttu-id="1bf26-156">Pertanto, è necessaria una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="1bf26-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="1bf26-157">È inoltre necessario impostare una dipendenza quando viene definita una risorsa (figlio) all'interno di un'altra risorsa (padre).</span><span class="sxs-lookup"><span data-stu-id="1bf26-157">You also need to set a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="1bf26-158">Ad esempio, le estensioni dello script personalizzate e le impostazioni di diagnostica vengono entrambe definite come risorse figlio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1bf26-158">For example, the diagnostic settings and custom script extensions are both defined as child resources of the virtual machine.</span></span> <span data-ttu-id="1bf26-159">Non possono essere create fino a quando non esiste la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1bf26-159">They cannot be created until the virtual machine exists.</span></span> <span data-ttu-id="1bf26-160">Pertanto, entrambe le risorse sono contrassegnate come dipendenti nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1bf26-160">Therefore, both resources are marked as dependent on the virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="1bf26-161">Profili</span><span class="sxs-lookup"><span data-stu-id="1bf26-161">Profiles</span></span>

<span data-ttu-id="1bf26-162">Quando si definisce una risorsa di macchina virtuale, vengono usati diversi elementi di profilo.</span><span class="sxs-lookup"><span data-stu-id="1bf26-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="1bf26-163">Alcuni sono necessari e alcuni sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="1bf26-163">Some are required and some are optional.</span></span> <span data-ttu-id="1bf26-164">Ad esempio, sono necessari gli elementi hardwareProfile, osProfile, storageProfile e networkProfile, ma diagnosticsProfile è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1bf26-164">For example, the hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but the diagnosticsProfile is optional.</span></span> <span data-ttu-id="1bf26-165">Questi profili definiscono impostazioni, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1bf26-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="1bf26-166">dimensione</span><span class="sxs-lookup"><span data-stu-id="1bf26-166">size</span></span>](sizes.md)
- <span data-ttu-id="1bf26-167">[nome](/architecture/best-practices/naming-conventions) e credenziali</span><span class="sxs-lookup"><span data-stu-id="1bf26-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="1bf26-168">disco e [impostazioni del sistema operativo](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="1bf26-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="1bf26-169">interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="1bf26-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="1bf26-170">diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="1bf26-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="1bf26-171">Dischi e immagini</span><span class="sxs-lookup"><span data-stu-id="1bf26-171">Disks and images</span></span>
   
<span data-ttu-id="1bf26-172">In Azure i file del disco rigido virtuale possono rappresentare [dischi o immagini](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1bf26-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1bf26-173">Quando il sistema operativo in un file di disco rigido virtuale è specializzato per essere una VM specifica, vi viene fatto riferimento come disco.</span><span class="sxs-lookup"><span data-stu-id="1bf26-173">When the operating system in a vhd file is specialized to be a specific VM, it is referred to as a disk.</span></span> <span data-ttu-id="1bf26-174">Quando il sistema operativo in un file di disco rigido virtuale è generalizzato per essere usato per creare più VM, viene considerato un'immagine.</span><span class="sxs-lookup"><span data-stu-id="1bf26-174">When the operating system in a vhd file is generalized to be used to create many VMs, it is referred to as an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="1bf26-175">Creare nuove macchine virtuali e nuovi dischi da un'immagine della piattaforma</span><span class="sxs-lookup"><span data-stu-id="1bf26-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="1bf26-176">Quando si crea una VM, è necessario decidere quale sistema operativo usare.</span><span class="sxs-lookup"><span data-stu-id="1bf26-176">When you create a VM, you must decide what operating system to use.</span></span> <span data-ttu-id="1bf26-177">L'elemento imageReference viene usato per definire il sistema operativo di una nuova VM.</span><span class="sxs-lookup"><span data-stu-id="1bf26-177">The imageReference element is used to define the operating system of a new VM.</span></span> <span data-ttu-id="1bf26-178">L'esempio illustra una definizione per un sistema operativo Windows Server:</span><span class="sxs-lookup"><span data-stu-id="1bf26-178">The example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="1bf26-179">Se si vuole creare un sistema operativo Linux, è possibile usare questa definizione:</span><span class="sxs-lookup"><span data-stu-id="1bf26-179">If you want to create a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="1bf26-180">Le impostazioni di configurazione per il disco del sistema operativo vengono assegnate con l'elemento osDisk.</span><span class="sxs-lookup"><span data-stu-id="1bf26-180">Configuration settings for the operating system disk are assigned with the osDisk element.</span></span> <span data-ttu-id="1bf26-181">L'esempio definisce un nuovo disco gestito con la modalità di memorizzazione nella cache impostata su **ReadWrite** e con il disco creato da un'[immagine della piattaforma](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="1bf26-181">The example defines a new managed disk with the caching mode set to **ReadWrite** and that the disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="1bf26-182">Creare nuove macchine virtuali da dischi gestiti esistenti</span><span class="sxs-lookup"><span data-stu-id="1bf26-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="1bf26-183">Se si vuole creare macchine virtuali da dischi esistenti, rimuovere gli elementi imageReference e osProfile e definire le impostazioni del disco:</span><span class="sxs-lookup"><span data-stu-id="1bf26-183">If you want to create virtual machines from existing disks, remove the imageReference and the osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="1bf26-184">Creare nuove macchine virtuali da un'immagine gestita</span><span class="sxs-lookup"><span data-stu-id="1bf26-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="1bf26-185">Se si vuole creare una macchina virtuale da un'immagine gestita, cambiare l'elemento imageReference e definire queste impostazioni del disco:</span><span class="sxs-lookup"><span data-stu-id="1bf26-185">If you want to create a virtual machine from a managed image, change the imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="1bf26-186">Collegare i dischi dei dati</span><span class="sxs-lookup"><span data-stu-id="1bf26-186">Attach data disks</span></span>

<span data-ttu-id="1bf26-187">È facoltativamente possibile aggiungere dischi di dati alle VM.</span><span class="sxs-lookup"><span data-stu-id="1bf26-187">You can optionally add data disks to the VMs.</span></span> <span data-ttu-id="1bf26-188">Il [numero di dischi](sizes.md) dipende dalle dimensioni del disco del sistema operativo in uso.</span><span class="sxs-lookup"><span data-stu-id="1bf26-188">The [number of disks](sizes.md) depends on the size of operating system disk that you use.</span></span> <span data-ttu-id="1bf26-189">Con le dimensioni delle VM impostate su Standard_DS1_v2, il numero massimo di dischi dati che possono essere aggiunti è due.</span><span class="sxs-lookup"><span data-stu-id="1bf26-189">With the size of the VMs set to Standard_DS1_v2, the maximum number of data disks that could be added to the them is two.</span></span> <span data-ttu-id="1bf26-190">Nell'esempio viene aggiunto un disco dati gestito a ogni VM:</span><span class="sxs-lookup"><span data-stu-id="1bf26-190">In the example, one managed data disk is being added to each VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="1bf26-191">Estensioni</span><span class="sxs-lookup"><span data-stu-id="1bf26-191">Extensions</span></span>

<span data-ttu-id="1bf26-192">Sebbene siano una risorsa separata, le [estensioni](extensions-features.md) sono strettamente legate alle VM.</span><span class="sxs-lookup"><span data-stu-id="1bf26-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied to VMs.</span></span> <span data-ttu-id="1bf26-193">Le estensioni possono essere aggiunte come risorsa figlio della VM o come risorsa separata.</span><span class="sxs-lookup"><span data-stu-id="1bf26-193">Extensions can be added as a child resource of the VM or as a separate resource.</span></span> <span data-ttu-id="1bf26-194">L'esempio illustra l'aggiunta dell'[estensione Diagnostica](extensions-diagnostics-template.md) alle VM:</span><span class="sxs-lookup"><span data-stu-id="1bf26-194">The example shows the [Diagnostics Extension](extensions-diagnostics-template.md) being added to the VMs:</span></span>

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

<span data-ttu-id="1bf26-195">Questa risorsa di estensione usa la variabile storageName e le variabili di diagnostica per fornire i valori.</span><span class="sxs-lookup"><span data-stu-id="1bf26-195">This extension resource uses the storageName variable and the diagnostic variables to provide values.</span></span> <span data-ttu-id="1bf26-196">Se si vuole modificare i dati raccolti da questa estensione, è possibile aggiungere altri contatori delle prestazioni alla variabile wadperfcounters.</span><span class="sxs-lookup"><span data-stu-id="1bf26-196">If you want to change the data that is collected by this extension, you can add more performance counters to the wadperfcounters variable.</span></span> <span data-ttu-id="1bf26-197">È possibile anche scegliere di inserire i dati di diagnostica in un account di archiviazione diverso rispetto a quello in cui sono archiviati i dischi della VM.</span><span class="sxs-lookup"><span data-stu-id="1bf26-197">You could also choose to put the diagnostics data into a different storage account than where the VM disks are stored.</span></span>

<span data-ttu-id="1bf26-198">Sono disponibili numerose estensioni che è possibile installare in una VM, ma la più utile è probabilmente l'[estensione dello script personalizzata](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="1bf26-198">There are many extensions that you can install on a VM, but the most useful is probably the [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="1bf26-199">Nell'esempio, al primo avvio in ogni VM viene eseguito uno script PowerShell denominato start.ps1:</span><span class="sxs-lookup"><span data-stu-id="1bf26-199">In the example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="1bf26-200">Lo script start.ps1 può eseguire molte attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1bf26-200">The start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="1bf26-201">Ad esempio, i dischi di dati aggiunti alle VM nell'esempio non vengono inizializzati; è possibile usare uno script personalizzato per inizializzarli.</span><span class="sxs-lookup"><span data-stu-id="1bf26-201">For example, the data disks that are added to the VMs in the example are not initialized; you can use a custom script to initialize them.</span></span> <span data-ttu-id="1bf26-202">Se si devono eseguire più attività di avvio, è possibile usare il file start.ps1 per chiamare altri script PowerShell in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1bf26-202">If you have multiple startup tasks to do, you can use the start.ps1 file to call other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="1bf26-203">L'esempio usa PowerShell, ma è possibile usare qualsiasi metodo di scripting disponibile nel sistema operativo in uso.</span><span class="sxs-lookup"><span data-stu-id="1bf26-203">The example uses PowerShell, but you can use any scripting method that is available on the operating system that you are using.</span></span>

<span data-ttu-id="1bf26-204">È possibile visualizzare lo stato delle estensioni installate dalle impostazioni Estensioni nel portale:</span><span class="sxs-lookup"><span data-stu-id="1bf26-204">You can see the status of the installed extensions from the Extensions settings in the portal:</span></span>

![Recuperare lo stato dell'estensione](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="1bf26-206">È possibile anche ottenere informazioni sull'estensione tramite il comando **Get-AzureRmVMExtension** di PowerShell, il comando **vm extension get** dell'interfaccia della riga di comando di Azure 2.0 oppure l'API REST **Get extension information**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-206">You can also get extension information by using the **Get-AzureRmVMExtension** PowerShell command, the **vm extension get** Azure CLI 2.0 command, or the **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="1bf26-207">Distribuzioni</span><span class="sxs-lookup"><span data-stu-id="1bf26-207">Deployments</span></span>

<span data-ttu-id="1bf26-208">Quando si distribuisce un modello, Azure tiene traccia delle risorse distribuite come gruppo e assegna automaticamente un nome a questo gruppo distribuito.</span><span class="sxs-lookup"><span data-stu-id="1bf26-208">When you deploy a template, Azure tracks the resources that you deployed as a group and automatically assigns a name to this deployed group.</span></span> <span data-ttu-id="1bf26-209">Il nome della distribuzione corrisponde a quello del modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-209">The name of the deployment is the same as the name of the template.</span></span>

<span data-ttu-id="1bf26-210">Per conoscere lo stato delle risorse nella distribuzione, è possibile usare il pannello Gruppo di risorse nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="1bf26-210">If you are curious about the status of resources in the deployment, you can use the Resource Group blade in the Azure portal:</span></span>

![Ottenere informazioni sulla distribuzione](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="1bf26-212">Non è un problema usare lo stesso modello per creare risorse o per aggiornare le risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="1bf26-212">It’s not a problem to use the same template to create resources or to update existing resources.</span></span> <span data-ttu-id="1bf26-213">Quando si usano comandi per distribuire i modelli, si ha la possibilità di indicare la [modalità](../../resource-group-template-deploy.md) da usare.</span><span class="sxs-lookup"><span data-stu-id="1bf26-213">When you use commands to deploy templates, you have the opportunity to say which [mode](../../resource-group-template-deploy.md) you want to use.</span></span> <span data-ttu-id="1bf26-214">La modalità può essere impostata su **Completa** o **Incrementale**.</span><span class="sxs-lookup"><span data-stu-id="1bf26-214">The mode can be set to either **Complete** or **Incremental**.</span></span> <span data-ttu-id="1bf26-215">Gli aggiornamenti incrementali sono il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="1bf26-215">The default is to do incremental updates.</span></span> <span data-ttu-id="1bf26-216">Prestare attenzione quando si usa la modalità **Completa** perché è possibile eliminare accidentalmente le risorse.</span><span class="sxs-lookup"><span data-stu-id="1bf26-216">Be careful when using the **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="1bf26-217">Quando si imposta la modalità su **Completa**, Resource Manager elimina tutte le risorse nel gruppo di risorse che non sono presenti nel modello.</span><span class="sxs-lookup"><span data-stu-id="1bf26-217">When you set the mode to **Complete**, Resource Manager deletes any resources in the resource group that are not in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bf26-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1bf26-218">Next Steps</span></span>

- <span data-ttu-id="1bf26-219">È possibile creare un modello personalizzato usando le informazioni presenti in [Creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1bf26-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="1bf26-220">Distribuire il modello creato usando [Creare una macchina virtuale Windows con un modello di Resource Manager](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="1bf26-220">Deploy the template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="1bf26-221">Per informazioni su come gestire le macchine virtuali create, vedere [Creare e gestire macchine virtuali di Windows con il modulo Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1bf26-221">Learn how to manage the VMs that you created by reviewing [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
