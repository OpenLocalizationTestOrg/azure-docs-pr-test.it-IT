---
title: "Distribuire più istanze delle risorse di Azure | Documentazione Microsoft"
description: "Usare l'operazione di copia e le matrici in un modello di Gestione risorse di Azure per eseguire più iterazioni durante la distribuzione delle risorse."
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
ms.openlocfilehash: ed8e3081d2b2e07938d7cf3aa5f95f6dde81bc66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="084ea-103">Distribuire più istanze di una risorsa o di una proprietà nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="084ea-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="084ea-104">Questo argomento illustra come eseguire un'iterazione del modello di Azure Resource Manager per creare più istanze di una risorsa o più istanze di una proprietà in una risorsa.</span><span class="sxs-lookup"><span data-stu-id="084ea-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="084ea-105">Se è necessario aggiungere una logica al modello per poter specificare se una risorsa è stata distribuita, vedere [Distribuire una risorsa in modo condizionale](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="084ea-105">If you need to add logic to your template that enables you to specify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="084ea-106">Iterazione delle risorse</span><span class="sxs-lookup"><span data-stu-id="084ea-106">Resource iteration</span></span>
<span data-ttu-id="084ea-107">Per creare più istanze di un tipo di risorsa, aggiungere un elemento `copy` al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="084ea-107">To create multiple instances of a resource type, add a `copy` element to the resource type.</span></span> <span data-ttu-id="084ea-108">Nell'elemento copy si specifica il numero di iterazioni e un nome per questo ciclo.</span><span class="sxs-lookup"><span data-stu-id="084ea-108">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="084ea-109">Il valore del conteggio deve essere un numero intero positivo e non può essere maggiore di 800.</span><span class="sxs-lookup"><span data-stu-id="084ea-109">The count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="084ea-110">Resource Manager crea le risorse in parallelo.</span><span class="sxs-lookup"><span data-stu-id="084ea-110">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="084ea-111">Pertanto l'ordine di creazione non è garantito.</span><span class="sxs-lookup"><span data-stu-id="084ea-111">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="084ea-112">Per creare risorse iterate in sequenza, vedere [Copia seriale](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="084ea-112">To create iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="084ea-113">La risorsa da ricreare più volte assume il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="084ea-113">The resource to create multiple times takes the following format:</span></span>

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

<span data-ttu-id="084ea-114">Si noti che il nome di ogni risorsa include la funzione `copyIndex()` che restituisce l'iterazione corrente nel ciclo.</span><span class="sxs-lookup"><span data-stu-id="084ea-114">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span> <span data-ttu-id="084ea-115">`copyIndex()` è in base zero.</span><span class="sxs-lookup"><span data-stu-id="084ea-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="084ea-116">Quindi l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="084ea-116">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="084ea-117">Crea questi nomi:</span><span class="sxs-lookup"><span data-stu-id="084ea-117">Creates these names:</span></span>

* <span data-ttu-id="084ea-118">storage0</span><span class="sxs-lookup"><span data-stu-id="084ea-118">storage0</span></span>
* <span data-ttu-id="084ea-119">storage1</span><span class="sxs-lookup"><span data-stu-id="084ea-119">storage1</span></span>
* <span data-ttu-id="084ea-120">storage2</span><span class="sxs-lookup"><span data-stu-id="084ea-120">storage2.</span></span>

<span data-ttu-id="084ea-121">Per eseguire l'offset del valore di indice, è possibile passare un valore nella funzione copyIndex().</span><span class="sxs-lookup"><span data-stu-id="084ea-121">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="084ea-122">Il numero di iterazioni da eseguire viene comunque specificato nell'elemento copia, ma il valore di copyIndex è compensato dal valore specificato.</span><span class="sxs-lookup"><span data-stu-id="084ea-122">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="084ea-123">Quindi l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="084ea-123">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="084ea-124">Crea questi nomi:</span><span class="sxs-lookup"><span data-stu-id="084ea-124">Creates these names:</span></span>

* <span data-ttu-id="084ea-125">storage1</span><span class="sxs-lookup"><span data-stu-id="084ea-125">storage1</span></span>
* <span data-ttu-id="084ea-126">storage2</span><span class="sxs-lookup"><span data-stu-id="084ea-126">storage2</span></span>
* <span data-ttu-id="084ea-127">storage3</span><span class="sxs-lookup"><span data-stu-id="084ea-127">storage3</span></span>

<span data-ttu-id="084ea-128">L'operazione di copia è utile quando si lavora con le matrici in quanto è possibile iterare ogni elemento della matrice.</span><span class="sxs-lookup"><span data-stu-id="084ea-128">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="084ea-129">Usare la funzione `length` nella matrice per specificare il conteggio per le iterazioni e `copyIndex` per recuperare l'indice corrente nella matrice.</span><span class="sxs-lookup"><span data-stu-id="084ea-129">Use the `length` function on the array to specify the count for iterations, and `copyIndex` to retrieve the current index in the array.</span></span> <span data-ttu-id="084ea-130">Quindi l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="084ea-130">So, the following example:</span></span>

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

<span data-ttu-id="084ea-131">Crea questi nomi:</span><span class="sxs-lookup"><span data-stu-id="084ea-131">Creates these names:</span></span>

* <span data-ttu-id="084ea-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="084ea-132">storagecontoso</span></span>
* <span data-ttu-id="084ea-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="084ea-133">storagefabrikam</span></span>
* <span data-ttu-id="084ea-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="084ea-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="084ea-135">Copia seriale</span><span class="sxs-lookup"><span data-stu-id="084ea-135">Serial copy</span></span>

<span data-ttu-id="084ea-136">Quando si usa l'elemento di copia per creare più istanze di un tipo di risorsa, Resource Manager distribuisce queste istanze in parallelo per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="084ea-136">When you use the copy element to create multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="084ea-137">Tuttavia è consigliabile specificare che le risorse vengano distribuite in sequenza.</span><span class="sxs-lookup"><span data-stu-id="084ea-137">However, you may want to specify that the resources are deployed in sequence.</span></span> <span data-ttu-id="084ea-138">Ad esempio, quando si aggiorna un ambiente di produzione, è consigliabile sfalsare gli aggiornamenti per aggiornarne solo un determinato numero in un dato momento.</span><span class="sxs-lookup"><span data-stu-id="084ea-138">For example, when updating a production environment, you may want to stagger the updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="084ea-139">Resource Manager fornisce proprietà sull'elemento di copia che consentono di distribuire più istanze in modo seriale.</span><span class="sxs-lookup"><span data-stu-id="084ea-139">Resource Manager provides properties on the copy element that enable you to serially deploy multiple instances.</span></span> <span data-ttu-id="084ea-140">Nell'elemento di copia impostare `mode` su **serial** e `batchSize` sul numero di istanze da distribuire contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="084ea-140">In the copy element, set `mode` to **serial** and `batchSize` to the number of instances to deploy at a time.</span></span> <span data-ttu-id="084ea-141">Con la modalità seriale, Resource Manager crea una dipendenza da istanze precedenti nel ciclo in modo un batch venga avviato solo dopo il completamento del batch precedente.</span><span class="sxs-lookup"><span data-stu-id="084ea-141">With serial mode, Resource Manager creates a dependency on earlier instances in the loop, so it does not start one batch until the previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="084ea-142">La proprietà mode accetta anche **parallel**, che è il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="084ea-142">The mode property also accepts **parallel**, which is the default value.</span></span>

<span data-ttu-id="084ea-143">Per testare la copia seriale senza creare risorse effettive, usare il modello seguente che distribuisce i modelli annidati vuoti:</span><span class="sxs-lookup"><span data-stu-id="084ea-143">To test serial copy without creating actual resources, use the following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="084ea-144">Nella cronologia di distribuzione notare che le distribuzioni annidate vengono elaborate in sequenza.</span><span class="sxs-lookup"><span data-stu-id="084ea-144">In the deployment history, notice that the nested deployments are processed in sequence.</span></span>

![distribuzione seriale](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="084ea-146">Per uno scenario più realistico, l'esempio seguente consente di distribuire due istanze alla volta di una VM Linux da un modello annidato:</span><span class="sxs-lookup"><span data-stu-id="084ea-146">For a more realistic scenario, the following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
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
                "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
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

## <a name="property-iteration"></a><span data-ttu-id="084ea-147">Iterazione delle proprietà</span><span class="sxs-lookup"><span data-stu-id="084ea-147">Property iteration</span></span>

<span data-ttu-id="084ea-148">Per creare più valori per una proprietà in una risorsa, aggiungere una matrice `copy` nell'elemento properties.</span><span class="sxs-lookup"><span data-stu-id="084ea-148">To create multiple values for a property on a resource, add a `copy` array in the properties element.</span></span> <span data-ttu-id="084ea-149">Questa matrice contiene oggetti ai quali sono associate le proprietà riportate di seguito.</span><span class="sxs-lookup"><span data-stu-id="084ea-149">This array contains objects, and each object has the following properties:</span></span>

* <span data-ttu-id="084ea-150">name: il nome della proprietà per la quale creare più valori</span><span class="sxs-lookup"><span data-stu-id="084ea-150">name - the name of the property to create multiple values for</span></span>
* <span data-ttu-id="084ea-151">count: il numero di valori da creare</span><span class="sxs-lookup"><span data-stu-id="084ea-151">count - the number of values to create</span></span>
* <span data-ttu-id="084ea-152">input: un oggetto che contiene i valori da assegnare alla proprietà</span><span class="sxs-lookup"><span data-stu-id="084ea-152">input - an object that contains the values to assign to the property</span></span>  

<span data-ttu-id="084ea-153">Nell'esempio seguente viene illustrato come applicare `copy` alla proprietà dataDisks in una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="084ea-153">The following example shows how to apply `copy` to the dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="084ea-154">Si noti che quando si usa `copyIndex` all'interno di un'iterazione di proprietà, è necessario specificare il nome dell'iterazione.</span><span class="sxs-lookup"><span data-stu-id="084ea-154">Notice that when using `copyIndex` inside a property iteration, you must provide the name of the iteration.</span></span> <span data-ttu-id="084ea-155">Non è necessario specificarlo quando l'elemento viene usato con un'iterazione di risorse.</span><span class="sxs-lookup"><span data-stu-id="084ea-155">You do not have to provide the name when used with resource iteration.</span></span>

<span data-ttu-id="084ea-156">Resource Manager espande la matrice `copy` durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="084ea-156">Resource Manager expands the `copy` array during deployment.</span></span> <span data-ttu-id="084ea-157">Il nome della matrice diventa il nome della proprietà.</span><span class="sxs-lookup"><span data-stu-id="084ea-157">The name of the array becomes the name of the property.</span></span> <span data-ttu-id="084ea-158">I valori di input diventano le proprietà dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="084ea-158">The input values become the object properties.</span></span> <span data-ttu-id="084ea-159">Il modello distribuito diventa:</span><span class="sxs-lookup"><span data-stu-id="084ea-159">The deployed template becomes:</span></span>

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

<span data-ttu-id="084ea-160">È possibile usare l'iterazione di risorse e di proprietà contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="084ea-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="084ea-161">Fare riferimento all'iterazione di proprietà con il nome.</span><span class="sxs-lookup"><span data-stu-id="084ea-161">Reference the property iteration by name.</span></span>

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

<span data-ttu-id="084ea-162">Per ogni risorsa è possibile includere nelle proprietà un solo elemento copy.</span><span class="sxs-lookup"><span data-stu-id="084ea-162">You can only include one copy element in the properties for each resource.</span></span> <span data-ttu-id="084ea-163">Per specificare un ciclo di iterazione per più proprietà, definire più oggetti nella matrice di copia.</span><span class="sxs-lookup"><span data-stu-id="084ea-163">To specify an iteration loop for more than one property, define multiple objects in the copy array.</span></span> <span data-ttu-id="084ea-164">Ogni oggetto viene iterato separatamente.</span><span class="sxs-lookup"><span data-stu-id="084ea-164">Each object is iterated separately.</span></span> <span data-ttu-id="084ea-165">Ad esempio, per creare più istanze di entrambe le proprietà `frontendIPConfigurations` e `loadBalancingRules` in un bilanciamento del carico, definire entrambi gli oggetti in un singolo elemento copy:</span><span class="sxs-lookup"><span data-stu-id="084ea-165">For example, to create multiple instances of both the `frontendIPConfigurations` property and the `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="084ea-166">In base alle risorse in un ciclo</span><span class="sxs-lookup"><span data-stu-id="084ea-166">Depend on resources in a loop</span></span>
<span data-ttu-id="084ea-167">L'elemento `dependsOn` consente di specificare che una risorsa sia distribuita dopo un'altra.</span><span class="sxs-lookup"><span data-stu-id="084ea-167">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="084ea-168">Per distribuire una risorsa che dipende dalla raccolta di risorse in un ciclo, usare il nome del ciclo di copia nell'elemento dependsOn.</span><span class="sxs-lookup"><span data-stu-id="084ea-168">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="084ea-169">L'esempio seguente illustra come distribuire tre account di archiviazione prima di distribuire la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="084ea-169">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="084ea-170">La definizione completa di macchina virtuale non viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="084ea-170">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="084ea-171">Si noti che la copia ha la proprietà name impostata su `storagecopy` e l'elemento dependsOn per le macchine virtuali impostato su `storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="084ea-171">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="084ea-172">Creare più istanze di una risorsa figlio</span><span class="sxs-lookup"><span data-stu-id="084ea-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="084ea-173">Non è possibile usare un ciclo di copia per una risorsa figlio.</span><span class="sxs-lookup"><span data-stu-id="084ea-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="084ea-174">Per creare più istanze di una risorsa cosiddetta "annidata" all'interno di un'altra risorsa, è invece necessario creare tale risorsa come una risorsa di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="084ea-174">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="084ea-175">La relazione con la risorsa padre si definisce con le proprietà type e name.</span><span class="sxs-lookup"><span data-stu-id="084ea-175">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="084ea-176">Si supponga, ad esempio, di definire in genere un set di dati come una risorsa figlio all'interno di una data factory.</span><span class="sxs-lookup"><span data-stu-id="084ea-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="084ea-177">Per creare più istanze di un set di dati, spostarlo all'esterno della data factory.</span><span class="sxs-lookup"><span data-stu-id="084ea-177">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="084ea-178">Il set di dati deve essere sullo stesso livello della data factory, di cui è comunque una risorsa figlio.</span><span class="sxs-lookup"><span data-stu-id="084ea-178">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="084ea-179">La relazione fra set di dati e data factory viene mantenuta con le proprietà type e name.</span><span class="sxs-lookup"><span data-stu-id="084ea-179">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="084ea-180">Poiché non è possibile dedurre il tipo dalla sua posizione nel modello, è necessario specificarne il nome completo nel formato: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="084ea-180">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="084ea-181">Per stabilire una relazione padre/figlio con un'istanza della data factory, specificare il nome del set di dati che include il nome della risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="084ea-181">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="084ea-182">Usare il formato: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="084ea-182">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="084ea-183">Nell'esempio seguente viene descritta l'implementazione:</span><span class="sxs-lookup"><span data-stu-id="084ea-183">The following example shows the implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="084ea-184">Distribuire una risorsa in modo condizionale</span><span class="sxs-lookup"><span data-stu-id="084ea-184">Conditionally deploy resource</span></span>

<span data-ttu-id="084ea-185">Per specificare se una risorsa è stata distribuita, usare l'elemento `condition`.</span><span class="sxs-lookup"><span data-stu-id="084ea-185">To specify whether a resource is deployed, use the `condition` element.</span></span> <span data-ttu-id="084ea-186">Il valore di questo elemento restituisce true o false.</span><span class="sxs-lookup"><span data-stu-id="084ea-186">The value for this element resolves to true or false.</span></span> <span data-ttu-id="084ea-187">Quando il valore è true, la risorsa viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="084ea-187">When the value is true, the resource is deployed.</span></span> <span data-ttu-id="084ea-188">Quando il valore è false, la risorsa non viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="084ea-188">When the value is false, the resource is not deployed.</span></span> <span data-ttu-id="084ea-189">Per indicare, ad esempio, se viene distribuito un nuovo account di archiviazione o se ne viene usato uno esistente, specificare:</span><span class="sxs-lookup"><span data-stu-id="084ea-189">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="084ea-190">Per un esempio di utilizzo di una risorsa nuova o esistente, vedere [Modello di condizione nuovo o esistente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="084ea-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="084ea-191">Per un esempio di utilizzo di una password o di una chiave SSH per la distribuzione di una macchina virtuale, vedere [Modello di condizione basato su nome utente o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="084ea-191">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="084ea-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="084ea-192">Next steps</span></span>
* <span data-ttu-id="084ea-193">Per altre informazioni sulle sezioni di un modello, vedere [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md) (Creazione di modelli di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="084ea-193">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="084ea-194">Per altre informazioni sulla distribuzione di modelli, vedere [Distribuire un'applicazione con il modello di Gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="084ea-194">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

