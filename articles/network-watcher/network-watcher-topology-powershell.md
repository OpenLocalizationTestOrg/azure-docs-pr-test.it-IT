---
title: topologia Watcher di rete di Azure aaaView - PowerShell | Documenti Microsoft
description: "In questo articolo descriverà come toouse PowerShell tooquery la topologia di rete."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a>Visualizzare la topologia di Network Watcher con PowerShell

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-topology-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-topology-cli.md)
> - [API REST](network-watcher-topology-rest.md)

funzionalità di topologia Hello del controllo di rete fornisce una rappresentazione visiva delle risorse di rete hello in una sottoscrizione. Nel portale di hello, questa visualizzazione viene presentata tooyou automaticamente. informazioni Hello dietro vista della topologia hello nel portale di hello è possibile recuperare tramite PowerShell.
Questa funzionalità rende più versatile come hello dati possono essere utilizzati da altri strumenti toobuild out visualizzazione hello informazioni sulla topologia di hello.

interconnessione Hello viene modellata in due relazioni.

- **Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda NIC
- **Associazione** - Esempio: la scheda NIC è associata a una macchina virtuale

Hello seguito sono le proprietà restituite quando si eseguono query hello API REST di topologia.

* **nome** : hello nome della risorsa hello
* **ID** -hello uri della risorsa hello.
* **percorso** -hello percorso in cui risiede la risorsa hello.
* **le associazioni** -un elenco di associazioni toohello fa riferimento a oggetto.
    * **nome** -nome hello di hello risorsa a cui viene fatto riferimento.
    * **resourceId** -resourceId hello è hello uri della risorsa hello a cui fa riferimento nell'associazione hello.
    * **associationType** -relazione hello tra l'oggetto figlio hello e padre hello fa riferimento a questo valore. I valori validi sono **Contains** o **Associated**.

## <a name="before-you-begin"></a>Prima di iniziare

In questo scenario, si usa hello `Get-AzureRmNetworkWatcherTopology` informazioni sulla topologia di cmdlet tooretrieve hello. È inoltre disponibile un articolo su come troppo[recuperare la topologia di rete con l'API REST](network-watcher-topology-rest.md).

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo recupera risposta topologia hello per un gruppo di risorse specificato.

## <a name="retrieve-network-watcher"></a>Recuperare Network Watcher

innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete. Hello `$networkWatcher` variabile viene passata toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a>Recuperare una topologia

Hello `Get-AzureRmNetworkWatcherTopology` cmdlet recupera la topologia di hello per un gruppo di risorse specificato.

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a>Risultati

Hello risultati restituiti hanno una proprietà nome "Resources", che contiene corpo della risposta json hello per hello `Get-AzureRmNetworkWatcherTopology` cmdlet.  risposta Hello contiene risorse hello hello il gruppo di sicurezza di rete e le relative associazioni (vale a dire, Contains, associate).

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


