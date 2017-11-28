---
title: "aaaDeploy più istanze delle risorse di Azure | Documenti Microsoft"
description: "Utilizzare matrici in un tooiterate modello di gestione risorse di Azure e l'operazione di copia più volte durante la distribuzione di risorse."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="d8b81-103">Distribuire più istanze di una risorsa o di una proprietà nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8b81-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="d8b81-104">In questo argomento illustra come tooiterate nel toocreate modello di gestione risorse di Azure più istanze di una risorsa o più istanze di una proprietà su una risorsa.</span><span class="sxs-lookup"><span data-stu-id="d8b81-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="d8b81-105">Se è necessario tooadd logica tooyour modello che consente di toospecify se una risorsa è distribuita, vedere [distribuire in modo condizionale risorsa](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="d8b81-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="d8b81-106">Iterazione delle risorse</span><span class="sxs-lookup"><span data-stu-id="d8b81-106">Resource iteration</span></span>
<span data-ttu-id="d8b81-107">aggiungere più istanze di un tipo di risorsa, toocreate un `copy` tipo di risorsa toohello elemento.</span><span class="sxs-lookup"><span data-stu-id="d8b81-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="d8b81-108">Nell'elemento copy hello, specificare il numero di hello di iterazioni e un nome per il ciclo.</span><span class="sxs-lookup"><span data-stu-id="d8b81-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="d8b81-109">valore del conteggio Hello deve essere un numero intero positivo e non può superare 800.</span><span class="sxs-lookup"><span data-stu-id="d8b81-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="d8b81-110">Gestione risorse consente di creare risorse hello in parallelo.</span><span class="sxs-lookup"><span data-stu-id="d8b81-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="d8b81-111">Pertanto, non è garantito ordine di hello in cui sono stati creati.</span><span class="sxs-lookup"><span data-stu-id="d8b81-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="d8b81-112">risorse toocreate scorsi in sequenza, vedere [copia seriale](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="d8b81-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="d8b81-113">Hello risorsa toocreate più volte accetta hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d8b81-113">hello resource toocreate multiple times takes hello following format:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="d8b81-114">Si noti che hello nome di ogni risorsa include hello `copyIndex()` funzione, che restituisce l'iterazione corrente hello in ciclo hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="d8b81-115">`copyIndex()` è in base zero.</span><span class="sxs-lookup"><span data-stu-id="d8b81-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="d8b81-116">In questo caso, hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d8b81-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="d8b81-117">Crea questi nomi:</span><span class="sxs-lookup"><span data-stu-id="d8b81-117">Creates these names:</span></span>

* <span data-ttu-id="d8b81-118">storage0</span><span class="sxs-lookup"><span data-stu-id="d8b81-118">storage0</span></span>
* <span data-ttu-id="d8b81-119">storage1</span><span class="sxs-lookup"><span data-stu-id="d8b81-119">storage1</span></span>
* <span data-ttu-id="d8b81-120">storage2</span><span class="sxs-lookup"><span data-stu-id="d8b81-120">storage2.</span></span>

<span data-ttu-id="d8b81-121">valore di indice toooffset hello, è possibile passare un valore nella funzione copyIndex() hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="d8b81-122">Hello numero di iterazioni tooperform è ancora specificata nell'elemento copy hello, ma il valore di hello di copyIndex offset in base a hello specificato valore.</span><span class="sxs-lookup"><span data-stu-id="d8b81-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="d8b81-123">In questo caso, hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d8b81-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="d8b81-124">Crea questi nomi:</span><span class="sxs-lookup"><span data-stu-id="d8b81-124">Creates these names:</span></span>

* <span data-ttu-id="d8b81-125">storage1</span><span class="sxs-lookup"><span data-stu-id="d8b81-125">storage1</span></span>
* <span data-ttu-id="d8b81-126">storage2</span><span class="sxs-lookup"><span data-stu-id="d8b81-126">storage2</span></span>
* <span data-ttu-id="d8b81-127">storage3</span><span class="sxs-lookup"><span data-stu-id="d8b81-127">storage3</span></span>

<span data-ttu-id="d8b81-128">operazione di copia Hello è utile quando si utilizzano matrici in quanto è possibile scorrere ogni elemento nella matrice hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="d8b81-129">Hello utilizzare `length` funzione attivazioni hello matrice toospecify hello per le iterazioni, e `copyIndex` tooretrieve hello corrente indice hello matrice.</span><span class="sxs-lookup"><span data-stu-id="d8b81-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="d8b81-130">In questo caso, hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d8b81-130">So, hello following example:</span></span>

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

<span data-ttu-id="d8b81-131">Crea questi nomi:</span><span class="sxs-lookup"><span data-stu-id="d8b81-131">Creates these names:</span></span>

* <span data-ttu-id="d8b81-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="d8b81-132">storagecontoso</span></span>
* <span data-ttu-id="d8b81-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="d8b81-133">storagefabrikam</span></span>
* <span data-ttu-id="d8b81-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="d8b81-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="d8b81-135">Copia seriale</span><span class="sxs-lookup"><span data-stu-id="d8b81-135">Serial copy</span></span>

<span data-ttu-id="d8b81-136">Quando si utilizza hello Copia elemento toocreate più istanze di un tipo di risorsa, Gestione risorse, per impostazione predefinita, distribuisce tali istanze in parallelo.</span><span class="sxs-lookup"><span data-stu-id="d8b81-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="d8b81-137">Tuttavia, è consigliabile toospecify tale hello risorse distribuite in sequenza.</span><span class="sxs-lookup"><span data-stu-id="d8b81-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="d8b81-138">Quando si aggiorna un ambiente di produzione, ad esempio, si consiglia di hello toostagger Aggiorna in modo che solo un determinato numero vengono aggiornate in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="d8b81-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="d8b81-139">Gestione risorse fornisce le proprietà sull'elemento copia hello che consentono di tooserially distribuiscono più istanze.</span><span class="sxs-lookup"><span data-stu-id="d8b81-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="d8b81-140">Nell'elemento copy hello, impostare `mode` troppo**seriale** e `batchSize` toohello numero di istanze toodeploy alla volta.</span><span class="sxs-lookup"><span data-stu-id="d8b81-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="d8b81-141">In modalità seriale Resource Manager crea una dipendenza su istanze precedenti nel ciclo di hello, in modo non si avvia un batch fino al completamento di batch precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="d8b81-142">Hello proprietà mode accetta inoltre **parallela**, ovvero il valore di predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="d8b81-143">tootest seriale copia senza creare risorse effettive, utilizzare hello seguente modello di distribuzione di modelli annidati vuoti:</span><span class="sxs-lookup"><span data-stu-id="d8b81-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

<span data-ttu-id="d8b81-144">Nella cronologia della distribuzione di hello, si noti che hello distribuzioni annidate vengono elaborate in sequenza.</span><span class="sxs-lookup"><span data-stu-id="d8b81-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![distribuzione seriale](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="d8b81-146">Per uno scenario più realistico, hello di esempio seguente consente di distribuire due istanze in un momento di una VM Linux da un modello annidato:</span><span class="sxs-lookup"><span data-stu-id="d8b81-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a><span data-ttu-id="d8b81-147">Iterazione delle proprietà</span><span class="sxs-lookup"><span data-stu-id="d8b81-147">Property iteration</span></span>

<span data-ttu-id="d8b81-148">aggiungere più valori per una proprietà su una risorsa, toocreate un `copy` matrice nell'elemento proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="d8b81-149">Questa matrice contiene gli oggetti e ogni oggetto dispone di hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8b81-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="d8b81-150">name - nome hello di hello proprietà toocreate più valori per</span><span class="sxs-lookup"><span data-stu-id="d8b81-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="d8b81-151">Count - il numero di hello di valori toocreate</span><span class="sxs-lookup"><span data-stu-id="d8b81-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="d8b81-152">input: un oggetto contenente proprietà di toohello tooassign valori hello</span><span class="sxs-lookup"><span data-stu-id="d8b81-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="d8b81-153">Hello seguente esempio viene illustrato come tooapply `copy` toohello dataDisks proprietà in una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="d8b81-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="d8b81-154">Si noti che quando si utilizza `copyIndex` all'interno di un'iterazione di proprietà, è necessario specificare il nome di hello di iterazione hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="d8b81-155">Nome di hello tooprovide se utilizzata con l'iterazione di risorse insufficienti.</span><span class="sxs-lookup"><span data-stu-id="d8b81-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="d8b81-156">Gestione risorse espande hello `copy` matrice durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d8b81-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="d8b81-157">nome di Hello della matrice hello diventa il nome di hello della proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="d8b81-158">i valori di input Hello diventano le proprietà dell'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-158">hello input values become hello object properties.</span></span> <span data-ttu-id="d8b81-159">modello Hello distribuito diventa:</span><span class="sxs-lookup"><span data-stu-id="d8b81-159">hello deployed template becomes:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="d8b81-160">È possibile usare l'iterazione di risorse e di proprietà contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="d8b81-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="d8b81-161">Riferimento hello proprietà l'iterazione in base al nome.</span><span class="sxs-lookup"><span data-stu-id="d8b81-161">Reference hello property iteration by name.</span></span>

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

<span data-ttu-id="d8b81-162">È possibile includere un elemento di copia solo nelle proprietà hello per ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="d8b81-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="d8b81-163">toospecify un ciclo di iterazione per più di una proprietà, definire più oggetti nella matrice copia hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="d8b81-164">Ogni oggetto viene iterato separatamente.</span><span class="sxs-lookup"><span data-stu-id="d8b81-164">Each object is iterated separately.</span></span> <span data-ttu-id="d8b81-165">Ad esempio, toocreate più istanze di entrambi hello `frontendIPConfigurations` proprietà e hello `loadBalancingRules` proprietà in un bilanciamento del carico, definire entrambi gli oggetti in un elemento di sola copia:</span><span class="sxs-lookup"><span data-stu-id="d8b81-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="d8b81-166">In base alle risorse in un ciclo</span><span class="sxs-lookup"><span data-stu-id="d8b81-166">Depend on resources in a loop</span></span>
<span data-ttu-id="d8b81-167">Specificare che una risorsa è distribuita dopo un'altra risorsa con hello `dependsOn` elemento.</span><span class="sxs-lookup"><span data-stu-id="d8b81-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="d8b81-168">toodeploy una risorsa che dipende dalla raccolta hello delle risorse in un ciclo, specificare il nome di hello del ciclo di copia hello nell'elemento dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="d8b81-169">Hello di esempio seguente viene illustrato come account di archiviazione prima di distribuire tre toodeploy hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d8b81-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="d8b81-170">definizione di Hello completa macchina virtuale non viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="d8b81-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="d8b81-171">Si noti che dispone di tale elemento copia hello nome impostato troppo`storagecopy` e l'elemento dependsOn hello per le macchine virtuali hello è impostato troppo`storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="d8b81-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="d8b81-172">Creare più istanze di una risorsa figlio</span><span class="sxs-lookup"><span data-stu-id="d8b81-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="d8b81-173">Non è possibile usare un ciclo di copia per una risorsa figlio.</span><span class="sxs-lookup"><span data-stu-id="d8b81-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="d8b81-174">toocreate più istanze di una risorsa che definita in genere come annidate all'interno di un'altra risorsa, è invece necessario creare tale risorsa come una risorsa di primo livello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="d8b81-175">Definire la relazione hello con risorsa padre hello tramite le proprietà di tipo e il nome di hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="d8b81-176">Si supponga, ad esempio, di definire in genere un set di dati come una risorsa figlio all'interno di una data factory.</span><span class="sxs-lookup"><span data-stu-id="d8b81-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

<span data-ttu-id="d8b81-177">toocreate più istanze di set di dati, spostarla all'esterno di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="d8b81-178">Hello set di dati deve essere uguale a livello di data factory di hello hello, ma è comunque una risorsa figlio della data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="d8b81-179">Consente di mantenere la relazione hello tra set di dati e data factory tramite le proprietà di tipo e il nome di hello.</span><span class="sxs-lookup"><span data-stu-id="d8b81-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="d8b81-180">Poiché il tipo non può essere dedotto dalla relativa posizione nel modello di hello, è necessario fornire il tipo di hello completo in formato hello: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="d8b81-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="d8b81-181">tooestablish una relazione padre/figlio con un'istanza di data factory di hello, specificare un nome per i set di dati hello che include il nome di risorsa del hello padre.</span><span class="sxs-lookup"><span data-stu-id="d8b81-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="d8b81-182">Utilizzare il formato hello: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="d8b81-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="d8b81-183">Hello riportato di seguito implementazione hello:</span><span class="sxs-lookup"><span data-stu-id="d8b81-183">hello following example shows hello implementation:</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="d8b81-184">Distribuire una risorsa in modo condizionale</span><span class="sxs-lookup"><span data-stu-id="d8b81-184">Conditionally deploy resource</span></span>

<span data-ttu-id="d8b81-185">toospecify se una risorsa è stata distribuita, utilizzare hello `condition` elemento.</span><span class="sxs-lookup"><span data-stu-id="d8b81-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="d8b81-186">un valore per questo elemento Hello risolve tootrue o false.</span><span class="sxs-lookup"><span data-stu-id="d8b81-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="d8b81-187">Quando il valore di hello è true, la risorsa hello viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="d8b81-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="d8b81-188">Quando il valore di hello è false, la risorsa hello non verrà distribuita.</span><span class="sxs-lookup"><span data-stu-id="d8b81-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="d8b81-189">Ad esempio, toospecify se è stato distribuito un nuovo account di archiviazione o viene utilizzato un account di archiviazione esistente, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="d8b81-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="d8b81-190">Per un esempio di utilizzo di una risorsa nuova o esistente, vedere [Modello di condizione nuovo o esistente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="d8b81-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="d8b81-191">Per un esempio di utilizzo di una password o una macchina virtuale di toodeploy chiave SSH, vedere [nome utente o SSH modello condizione](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="d8b81-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8b81-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8b81-192">Next steps</span></span>
* <span data-ttu-id="d8b81-193">Se si desidera toolearn sulle sezioni hello di un modello, vedere [la creazione di modelli di gestione risorse di Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d8b81-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d8b81-194">toolearn come toodeploy il modello, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d8b81-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

