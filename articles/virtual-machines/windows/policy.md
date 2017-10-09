---
title: sicurezza aaaEnforce con i criteri in macchine virtuali di Windows in Azure | Documenti Microsoft
description: Come tooapply tooan un criterio macchina virtuale di Windows Azure Resource Manager
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: b31c8a03ecf8eed6a929f97fe4146ea14364404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a>Applicare i criteri tooWindows macchine virtuali con Gestione risorse di Azure
Con i criteri di un'organizzazione può applicare varie convenzioni e le regole di organizzazione hello. Imposizione del comportamento desiderato hello può ridurre i rischi contribuendo toohello successo dell'organizzazione hello stesso. In questo articolo si descrivono come utilizzare il comportamento di gestione risorse di Azure criteri toodefine hello desiderato per le macchine virtuali dell'organizzazione.

Per toopolicies un'introduzione, vedere [risorse toomanage criteri di utilizzo e controllare l'accesso](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>Macchine virtuali permesse
tooensure che le macchine virtuali per l'organizzazione sono compatibili con un'applicazione, è possibile limitare hello sistemi operativi è consentito. Nel seguente esempio di criterio di hello, si consente solo toobe di macchine virtuali di Windows Server 2012 R2 Datacenter creato:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Utilizzare un hello toomodify con caratteri jolly precedente tooallow criteri qualsiasi immagine di Windows Server Datacenter:

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

Utilizzare anyOf toomodify hello precedente tooallow criteri qualsiasi Data Center di Windows Server 2012 R2 o immagine superiore:

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

Per informazioni sui campi dei criteri, vedere [Alias dei criteri](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Dischi gestiti

toorequire hello utilizzo di dischi gestiti, utilizzare hello seguenti criteri:

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a>Immagini per macchine virtuali

Per motivi di sicurezza, è possibile richiedere che solo le immagini personalizzate approvate vengano distribuite nell'ambiente in uso. È possibile specificare gruppo di risorse hello contenente immagini hello approvato o immagini approvate specifico hello.

Hello di esempio seguente richiede le immagini da un gruppo di risorse approvati:

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

Hello esempio seguente specifica immagine hello approvato ID:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Estensioni di macchina virtuale

È opportuno tooforbid utilizzo di determinati tipi di estensioni. Un'estensione potrebbe non essere ad esempio compatibile con determinate immagini di macchina virtuale personalizzata. Hello seguente esempio viene illustrato come tooblock un'estensione specifica. Usa toodetermine server di pubblicazione e il tipo cui tooblock di estensione.

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="azure-hybrid-use-benefit"></a>Vantaggio Azure Hybrid Use

Quando si dispone di una licenza in locale, è possibile salvare l'onere di licenza hello nelle macchine virtuali. Quando non si dispone di licenza di hello, si dovrebbe proibire l'opzione hello. Hello seguente criteri impedisce l'uso del vantaggio di utilizzare Azure ibrida (AHUB):

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito. Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa. criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](../../azure-resource-manager/resource-manager-policy-portal.md). criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Per i criteri di tooresource un'introduzione, vedere [Panoramica criteri delle risorse](../../azure-resource-manager/resource-manager-policy.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](../../azure-resource-manager/resource-manager-subscription-governance.md).
