---
title: topologia Watcher di rete di Azure aaaView - CLI di Azure | Documenti Microsoft
description: "In questo articolo descriverà come toouse CLI di Azure tooquery la topologia di rete."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a>Visualizzare la topologia di Network Watcher con l'interfaccia della riga di comando di Azure

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-topology-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-topology-cli.md)
> - [API REST](network-watcher-topology-rest.md)

funzionalità di topologia Hello del controllo di rete fornisce una rappresentazione visiva delle risorse di rete hello in una sottoscrizione. Nel portale di hello, questa visualizzazione viene presentata tooyou automaticamente. informazioni Hello dietro vista della topologia hello nel portale di hello è possibile recuperare tramite PowerShell.
Questa funzionalità rende più versatile come hello dati possono essere utilizzati da altri strumenti toobuild out visualizzazione hello informazioni sulla topologia di hello.

Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux. Network Watcher usa attualmente l'interfaccia della riga di comando di Azure 1.0 per il supporto dell'interfaccia della riga di comando.

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

In questo scenario, si usa hello `network watcher topology` informazioni sulla topologia di cmdlet tooretrieve hello. È inoltre disponibile un articolo su come troppo[recuperare la topologia di rete con l'API REST](network-watcher-topology-rest.md).

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo recupera risposta topologia hello per un gruppo di risorse specificato.

## <a name="retrieve-topology"></a>Recuperare una topologia

Hello `network watcher topology` cmdlet recupera la topologia di hello per un gruppo di risorse specificato. Aggiunto argomento hello "--json" tooview hello oput in formato json

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>Risultati

Hello risultati restituiti hanno una proprietà nome "Resources", che contiene corpo della risposta json hello per hello `network watcher topology` cmdlet.  risposta Hello contiene risorse hello hello il gruppo di sicurezza di rete e le relative associazioni (vale a dire, Contains, associate).

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>Passaggi successivi

Ulteriori informazioni sulle regole di sicurezza hello che sono risorse di rete applicati tooyour visitando [Visualizza panoramica gruppo di sicurezza](network-watcher-security-group-view-overview.md)
