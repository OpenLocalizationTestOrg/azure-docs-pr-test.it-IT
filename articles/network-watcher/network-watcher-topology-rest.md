---
title: topologia Watcher di rete di Azure aaaView - API REST | Documenti Microsoft
description: In questo articolo viene descritto come toouse REST API tooquery la topologia di rete.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>Visualizzare la topologia di Network Watcher con l'API REST

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

In questo scenario è recuperare le informazioni sulla topologia di hello. ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell. ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo recupera risposta topologia hello per un gruppo di risorse specificato.

## <a name="log-in-with-armclient"></a>Accedere con ARMClient

Accedi tooarmclient con le credenziali di Azure.

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>Recuperare una topologia

Hello di esempio seguente richiede topologia hello hello API REST.  esempio Hello è tooallow con parametri per la flessibilità per la creazione di un esempio.  Sostituire tutti i valori con \< \> intorno a essi.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

Hello risposta seguente è riportato un esempio di una risposta abbreviato che viene restituito quando recuperare topologia per un gruppo di risorse:

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

