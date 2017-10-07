---
title: aaaCreate un'istanza di controllo di rete di Azure | Documenti Microsoft
description: In questa pagina vengono hello passaggi toocreate un'istanza del controllo di rete tramite il portale di hello e API REST di Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Creare un'istanza di Azure Network Watcher

Watcher di rete è un servizio internazionale che consente di toomonitor e diagnosticare le condizioni di livello rete scenario, a e da Azure. Monitoraggio a livello di scenario consente problemi toodiagnose a una vista della rete tooend end livello. Diagnostica di rete e gli strumenti di visualizzazione disponibili con Watcher di rete consentono di comprendere, diagnosticare e ottenere rete tooyour insights in Azure.

> [!NOTE]
> Watcher di rete supporta attualmente solo 1.0 CLI, hello istruzioni toocreate viene fornita una nuova istanza di controllo di rete per CLI 1.0.

## <a name="create-a-network-watcher-in-hello-portal"></a>Creare un controllo di rete nel portale di hello

Passare troppo**più servizi** > **rete** > **Watcher di rete**. È possibile selezionare tutte le sottoscrizioni di hello da tooenable Watcher di rete per. Questa azione crea un'istanza di Network Watcher in ogni area in cui è disponibile.

![Creare un'istanza di Network Watcher][1]

Quando si abilita il Watcher di rete utilizzando hello portale, hello nome dell'istanza di hello Watcher di rete verrà automaticamente impostato tooNetworkWatcher_region_name dove region_name corrisponde toohello regione di Azure in cui è stata abilitata l'istanza di hello.  Ad esempio, un Network Watcher abilitato nell'area centro-occidentale degli Stati Uniti verrà denominato NetworkWatcher_westcentralus

Inoltre, istanza Watcher di rete hello verrà automaticamente aggiunto in un gruppo di risorse denominato NetworkWatcherRG.  Questo gruppo di risorse verrà creato se non esiste già.

Se si desidera nome hello toocustomize di un'istanza del controllo di rete e hello gruppo di risorse viene inserito in, è possibile usare Powershell, hello API REST o ARMClient metodi descritti di seguito.  Per ogni opzione, hello gruppo di risorse deve essere presente prima di effettuare hello Watcher di rete al suo interno.  

## <a name="create-a-network-watcher-with-powershell"></a>Creare un'istanza di Network Watcher con PowerShell

toocreate un'istanza del controllo di rete, eseguire hello di esempio seguente:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>Creare un controllo di rete con hello API REST

ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell. ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)

### <a name="log-in-with-armclient"></a>Accedere con ARMClient

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>Creare il watcher di rete hello

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un'istanza del controllo di rete, informazioni sulle funzionalità di hello disponibili:

* [Topologia](network-watcher-topology-overview.md)
* [Acquisizione pacchetti](network-watcher-packet-capture-overview.md)
* [Verifica del flusso IP](network-watcher-ip-flow-verify-overview.md)
* [Hop successivo](network-watcher-next-hop-overview.md)
* [Visualizzazione di un gruppo di sicurezza](network-watcher-security-group-view-overview.md)
* [Registrazione dei flussi dei gruppi di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md)
* [Risoluzione dei problemi del gateway di rete virtuale](network-watcher-troubleshoot-overview.md)

Dopo aver creata un'istanza del controllo di rete, l'acquisizione pacchetto può essere configurato dal seguente hello: [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











