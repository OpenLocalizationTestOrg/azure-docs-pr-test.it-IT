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
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Distribuire più istanze di una risorsa o di una proprietà nei modelli di Azure Resource Manager
In questo argomento illustra come tooiterate nel toocreate modello di gestione risorse di Azure più istanze di una risorsa o più istanze di una proprietà su una risorsa.

Se è necessario tooadd logica tooyour modello che consente di toospecify se una risorsa è distribuita, vedere [distribuire in modo condizionale risorsa](#conditionally-deploy-resource).

## <a name="resource-iteration"></a>Iterazione delle risorse
aggiungere più istanze di un tipo di risorsa, toocreate un `copy` tipo di risorsa toohello elemento. Nell'elemento copy hello, specificare il numero di hello di iterazioni e un nome per il ciclo. valore del conteggio Hello deve essere un numero intero positivo e non può superare 800. Gestione risorse consente di creare risorse hello in parallelo. Pertanto, non è garantito ordine di hello in cui sono stati creati. risorse toocreate scorsi in sequenza, vedere [copia seriale](#serial-copy). 

Hello risorsa toocreate più volte accetta hello seguente formato:

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

Si noti che hello nome di ogni risorsa include hello `copyIndex()` funzione, che restituisce l'iterazione corrente hello in ciclo hello. `copyIndex()` è in base zero. In questo caso, hello di esempio seguente:

```json
"name": "[concat('storage', copyIndex())]",
```

Crea questi nomi:

* storage0
* storage1
* storage2

valore di indice toooffset hello, è possibile passare un valore nella funzione copyIndex() hello. Hello numero di iterazioni tooperform è ancora specificata nell'elemento copy hello, ma il valore di hello di copyIndex offset in base a hello specificato valore. In questo caso, hello di esempio seguente:

```json
"name": "[concat('storage', copyIndex(1))]",
```

Crea questi nomi:

* storage1
* storage2
* storage3

operazione di copia Hello è utile quando si utilizzano matrici in quanto è possibile scorrere ogni elemento nella matrice hello. Hello utilizzare `length` funzione attivazioni hello matrice toospecify hello per le iterazioni, e `copyIndex` tooretrieve hello corrente indice hello matrice. In questo caso, hello di esempio seguente:

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

Crea questi nomi:

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>Copia seriale

Quando si utilizza hello Copia elemento toocreate più istanze di un tipo di risorsa, Gestione risorse, per impostazione predefinita, distribuisce tali istanze in parallelo. Tuttavia, è consigliabile toospecify tale hello risorse distribuite in sequenza. Quando si aggiorna un ambiente di produzione, ad esempio, si consiglia di hello toostagger Aggiorna in modo che solo un determinato numero vengono aggiornate in qualsiasi momento.

Gestione risorse fornisce le proprietà sull'elemento copia hello che consentono di tooserially distribuiscono più istanze. Nell'elemento copy hello, impostare `mode` troppo**seriale** e `batchSize` toohello numero di istanze toodeploy alla volta. In modalità seriale Resource Manager crea una dipendenza su istanze precedenti nel ciclo di hello, in modo non si avvia un batch fino al completamento di batch precedente hello.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

Hello proprietà mode accetta inoltre **parallela**, ovvero il valore di predefinito hello.

tootest seriale copia senza creare risorse effettive, utilizzare hello seguente modello di distribuzione di modelli annidati vuoti:

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

Nella cronologia della distribuzione di hello, si noti che hello distribuzioni annidate vengono elaborate in sequenza.

![distribuzione seriale](./media/resource-group-create-multiple/serial-copy.png)

Per uno scenario più realistico, hello di esempio seguente consente di distribuire due istanze in un momento di una VM Linux da un modello annidato:

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

## <a name="property-iteration"></a>Iterazione delle proprietà

aggiungere più valori per una proprietà su una risorsa, toocreate un `copy` matrice nell'elemento proprietà hello. Questa matrice contiene gli oggetti e ogni oggetto dispone di hello le proprietà seguenti:

* name - nome hello di hello proprietà toocreate più valori per
* Count - il numero di hello di valori toocreate
* input: un oggetto contenente proprietà di toohello tooassign valori hello  

Hello seguente esempio viene illustrato come tooapply `copy` toohello dataDisks proprietà in una macchina virtuale:

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

Si noti che quando si utilizza `copyIndex` all'interno di un'iterazione di proprietà, è necessario specificare il nome di hello di iterazione hello. Nome di hello tooprovide se utilizzata con l'iterazione di risorse insufficienti.

Gestione risorse espande hello `copy` matrice durante la distribuzione. nome di Hello della matrice hello diventa il nome di hello della proprietà hello. i valori di input Hello diventano le proprietà dell'oggetto hello. modello Hello distribuito diventa:

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

È possibile usare l'iterazione di risorse e di proprietà contemporaneamente. Riferimento hello proprietà l'iterazione in base al nome.

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

È possibile includere un elemento di copia solo nelle proprietà hello per ogni risorsa. toospecify un ciclo di iterazione per più di una proprietà, definire più oggetti nella matrice copia hello. Ogni oggetto viene iterato separatamente. Ad esempio, toocreate più istanze di entrambi hello `frontendIPConfigurations` proprietà e hello `loadBalancingRules` proprietà in un bilanciamento del carico, definire entrambi gli oggetti in un elemento di sola copia: 

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

## <a name="depend-on-resources-in-a-loop"></a>In base alle risorse in un ciclo
Specificare che una risorsa è distribuita dopo un'altra risorsa con hello `dependsOn` elemento. toodeploy una risorsa che dipende dalla raccolta hello delle risorse in un ciclo, specificare il nome di hello del ciclo di copia hello nell'elemento dependsOn hello. Hello di esempio seguente viene illustrato come account di archiviazione prima di distribuire tre toodeploy hello macchina virtuale. definizione di Hello completa macchina virtuale non viene visualizzata. Si noti che dispone di tale elemento copia hello nome impostato troppo`storagecopy` e l'elemento dependsOn hello per le macchine virtuali hello è impostato troppo`storagecopy`.

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

## <a name="create-multiple-instances-of-a-child-resource"></a>Creare più istanze di una risorsa figlio
Non è possibile usare un ciclo di copia per una risorsa figlio. toocreate più istanze di una risorsa che definita in genere come annidate all'interno di un'altra risorsa, è invece necessario creare tale risorsa come una risorsa di primo livello. Definire la relazione hello con risorsa padre hello tramite le proprietà di tipo e il nome di hello.

Si supponga, ad esempio, di definire in genere un set di dati come una risorsa figlio all'interno di una data factory.

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

toocreate più istanze di set di dati, spostarla all'esterno di data factory di hello. Hello set di dati deve essere uguale a livello di data factory di hello hello, ma è comunque una risorsa figlio della data factory di hello. Consente di mantenere la relazione hello tra set di dati e data factory tramite le proprietà di tipo e il nome di hello. Poiché il tipo non può essere dedotto dalla relativa posizione nel modello di hello, è necessario fornire il tipo di hello completo in formato hello: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.

tooestablish una relazione padre/figlio con un'istanza di data factory di hello, specificare un nome per i set di dati hello che include il nome di risorsa del hello padre. Utilizzare il formato hello: `{parent-resource-name}/{child-resource-name}`.  

Hello riportato di seguito implementazione hello:

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

## <a name="conditionally-deploy-resource"></a>Distribuire una risorsa in modo condizionale

toospecify se una risorsa è stata distribuita, utilizzare hello `condition` elemento. un valore per questo elemento Hello risolve tootrue o false. Quando il valore di hello è true, la risorsa hello viene distribuita. Quando il valore di hello è false, la risorsa hello non verrà distribuita. Ad esempio, toospecify se è stato distribuito un nuovo account di archiviazione o viene utilizzato un account di archiviazione esistente, utilizzare:

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

Per un esempio di utilizzo di una risorsa nuova o esistente, vedere [Modello di condizione nuovo o esistente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

Per un esempio di utilizzo di una password o una macchina virtuale di toodeploy chiave SSH, vedere [nome utente o SSH modello condizione](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="next-steps"></a>Passaggi successivi
* Se si desidera toolearn sulle sezioni hello di un modello, vedere [la creazione di modelli di gestione risorse di Azure](resource-group-authoring-templates.md).
* toolearn come toodeploy il modello, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

