---
title: aaaFind Hop successivo con Azure rete Watcher Hop successivo - REST | Documenti Microsoft
description: "In questo articolo descrive come è possibile trovare quale hello tipo dell'hop successivo è e indirizzo ip utilizzando di Hop successivo hello API REST di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>Individuare il tipo dell'hop successivo hello sta utilizzando funzionalità Hop successivo hello in Watcher di rete di Azure utilizzando l'API REST di Azure

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST di Azure](network-watcher-check-next-hop-rest.md)

Hop successivo è una funzionalità di controllo di rete che consente di hello ottenere il tipo dell'hop successivo di hello e l'indirizzo IP in base a una macchina virtuale specificata. Questa funzionalità è utile per determinare se il traffico da una macchina virtuale consente di scorrere un gateway, internet o reti virtuali tooget tooits destinazione.

## <a name="before-you-begin"></a>Prima di iniziare

ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell. ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo Usa Hop successivo, una funzionalità del controllo di rete che consente di trovare il tipo dell'hop successivo hello e indirizzo IP per una risorsa. toolearn su più Hop successivo, visitare [panoramica dell'Hop successivo](network-watcher-next-hop-overview.md).

In questo scenario si apprenderà come:

* Recuperare l'hop successivo di hello per una macchina virtuale.

## <a name="log-in-with-armclient"></a>Accedere con ARMClient

Accedi tooarmclient con le credenziali di Azure.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Recuperare una macchina virtuale

Eseguire hello seguenti script tooreturn una macchina virtuale. Queste informazioni sono necessarie per eseguire l'hop successivo.

Hello seguente di codice deve valori per hello seguenti variabili:

- **subscriptionId** -hello toouse Id sottoscrizione.
- **resourceGroupName** : hello nome di un gruppo di risorse contenente le macchine virtuali.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Dall'output seguente hello, id di hello della macchina virtuale hello viene utilizzato nell'esempio seguente hello:

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>Ottenere l'hop successivo

Dopo aver creata un'intestazione authorization hello, hop successivo di hello da una macchina virtuale può essere recuperato. Hello valori seguenti devono essere sostituiti per toowork di esempio di codice hello.

> [!Important]
> Per l'API REST di controllo rete chiamate hello Nome gruppo di risorse nella richiesta di hello che URI è gruppo di risorse hello contenente hello Watcher di rete, non le risorse hello si eseguono operazioni di diagnostica hello in.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Hop successivo è necessario che risorsa macchina virtuale hello è allocato toorun.

## <a name="results"></a>Risultati

Hello frammento di codice seguente è riportato un esempio dell'output di hello ricevuto. risultati di Hello contengono hello seguenti valori:

* **nextHopType** -questo valore è uno dei seguenti valori hello: Internet, VirtualAppliance, gateway di rete virtuale, VnetLocal, HyperNetGateway o nessuno.
* **nextHopIpAddress** -indirizzo IP dell'hop successivo hello hello.
* **routeTableId** - valore hello è l'uri per la tabella di route hello associato hello route o se non definita dall'utente route è il valore di hello definito di *sistema Route* viene restituito.

di seguito Hello sono risultati hello in formato json.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>Passaggi successivi

Una volta che è stato in grado di toofind all'hop successivo di hello per una macchina virtuale, è possibile visualizzare sicurezza hello delle risorse di rete, visitare il sito [Panoramica di vista della sicurezza](network-watcher-security-group-view-overview.md)














