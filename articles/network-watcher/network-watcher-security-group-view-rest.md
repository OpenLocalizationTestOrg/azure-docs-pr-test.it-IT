---
title: sicurezza di rete aaaAnalyze con visualizzazione gruppo di sicurezza di controllo di rete di Azure - API REST | Documenti Microsoft
description: In questo articolo viene descritto come toouse PowerShell tooanalyze un virtuale macchine protezione con visualizzazione del gruppo di sicurezza.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a>Analizzare la protezione della macchina virtuale visualizzando un gruppo di sicurezza con l'API REST

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-security-group-view-cli.md)
> - [API REST](network-watcher-security-group-view-rest.md)

Visualizzazione del gruppo di sicurezza restituisce regole di sicurezza di rete configurate ed efficace di macchina virtuale tooa applicato. Questa funzionalità è utile tooaudit e diagnosticare i gruppi di sicurezza di rete e le regole configurate per il traffico tooensure una macchina virtuale viene correttamente consentito o negato. In questo articolo viene illustrata la funzionamento delle regole di sicurezza efficace e applicato di hello tooretrieve macchina virtuale tooa tramite l'API REST

## <a name="before-you-begin"></a>Prima di iniziare

In questo scenario, chiamare visualizzazione del gruppo protezione tooget hello hello API Rest Watcher di rete per una macchina virtuale. ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell. ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete. scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.

## <a name="scenario"></a>Scenario

scenario Hello illustrato in questo articolo consente di recuperare le regole di sicurezza efficace e applicato hello per una determinata macchina virtuale.

## <a name="log-in-with-armclient"></a>Accedere con ARMClient

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Recuperare una macchina virtuale

Eseguire i seguenti script tooreturn un machineThe virtuale hello seguente di codice deve variabili:

- **subscriptionId** -id sottoscrizione hello possono anche essere recuperati con hello **Get AzureRMSubscription** cmdlet.
- **resourceGroupName** : hello nome di un gruppo di risorse contenente le macchine virtuali.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

le informazioni necessarie Hello sono hello **id** in tipo hello `Microsoft.Compute/virtualMachines` in risposta, come illustrato nel seguente esempio hello:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a>Ottenere la visualizzazione del gruppo di sicurezza per la macchina virtuale

Hello di esempio seguente richiede vista gruppo di sicurezza hello di una macchina virtuale di destinazione. risultati dell'esempio Hello possono essere utilizzato toocompare toohello regole e sicurezza definiti da hello origine toolook deviazione della configurazione.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a>Visualizzazione hello risposta

Dopo l'esempio Hello è risposta hello restituita dal comando precedente hello. Hello risultati mostrano tutte le regole di sicurezza efficace e applicato hello nella macchina virtuale hello suddiviso in gruppi di **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a>Passaggi successivi

Visitare [il controllo di sicurezza gruppi (rete) con Watcher di rete](network-watcher-security-group-view-powershell.md) toolearn come tooautomate convalida dei gruppi di sicurezza di rete.


