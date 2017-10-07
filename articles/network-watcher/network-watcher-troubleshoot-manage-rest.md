---
title: aaaTroubleshoot Gateway della rete virtuale e le connessioni utilizzando il Watcher di rete di Azure - REST | Documenti Microsoft
description: Questa pagina viene illustrato come tootroubleshoot gateway di rete virtuale e le connessioni con il Watcher di rete di Azure tramite REST
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a>Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni tramite Network Watcher di Azure

> [!div class="op_single_selector"]
> - [Portale](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Watcher di rete fornisce numerose funzionalità toounderstanding in relazione le risorse di rete in Azure. Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse. Risoluzione dei problemi di risorse può essere chiamato tramite il portale di hello, PowerShell, CLI o API REST. Quando viene chiamato, Watcher di rete Controlla integrità hello di un Gateway di rete virtuale o una connessione e restituisce i risultati della ricerca.

In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per la risoluzione dei problemi di risorse.

- [**Risolvere i problemi relativi a un gateway di rete virtuale**](#troubleshoot-a-virtual-network-gateway)
- [**Risolvere i problemi relativi a una connessione**](#troubleshoot-connections)

## <a name="before-you-begin"></a>Prima di iniziare

ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell. ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.

Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Panoramica

Risoluzione dei problemi di controllo di rete consente di hello risolvere i problemi che si verificano con i gateway di rete virtuale e le connessioni. Quando una richiesta viene effettuata la risorsa toohello risoluzione dei problemi, registri esegue una query e controllato. Una volta completato controllo, vengono restituiti risultati hello. Hello risolvere API richieste sono molto richieste, che potrebbe richiedere più minuti tooreturn un risultato in esecuzione. I log vengono archiviati in un contenitore di un account di archiviazione.

## <a name="log-in-with-armclient"></a>Accedere con ARMClient

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a>Risolvere i problemi relativi a un gateway di rete virtuale


### <a name="post-hello-troubleshoot-request"></a>Hello POST risolvere i problemi di richiesta

Hello seguente stato hello query di esempio di un gateway di rete virtuale.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

Poiché questa operazione è lunga in esecuzione, hello URI per l'esecuzione di query operazione hello e hello URI per il risultato di hello viene restituito nell'intestazione di risposta hello, come illustrato nella seguente risposta hello:

**Valori importanti**

* **Azure AsyncOperation** -questa proprietà contiene hello URI tooquery hello Async risolvere i problemi di funzionamento
* **Percorso** -questa proprietà contiene hello URI in cui i risultati di hello risultano hello operazione è stata completata

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>Hello async completamento dell'operazione di query

Utilizzare hello operazioni URI tooquery per lo stato di avanzamento hello dell'operazione di hello, come illustrato nel seguente esempio hello:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Durante l'operazione di hello è in corso, hello Mostra risposta **InProgress** come illustrato nel seguente esempio hello:

```json
{
  "status": "InProgress"
}
```

Quando un'operazione hello è modifiche dello stato di completamento hello troppo**Succeeded**.

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a>Recuperare i risultati di hello

Una volta lo stato di hello restituito è **Succeeded**, chiamare un metodo GET su hello operationResult URI tooretrieve risultati hello.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Hello risposte seguenti sono esempi di una tipica risposta ridotte restituito quando si eseguono query risultati hello di risoluzione dei problemi di un gateway. Vedere [informazioni sui risultati hello](#understanding-the-results) tooget chiarimento su quali proprietà hello in Media risposta hello.

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a>Risoluzione dei problemi relativi alle connessioni

Hello seguente stato hello query di esempio di una connessione.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> Hello risolvere i problemi di operazione non può essere eseguito in parallelo su una connessione e il relativo gateway corrispondente. operazione Hello deve essere completata prima toorunning sul precedente risorsa hello.

Poiché si tratta di una transazione con esecuzione prolungata, nell'intestazione di risposta hello, hello URI per l'esecuzione di query operazione hello e hello URI per il risultato di hello viene restituito come illustrato nella seguente risposta hello:

**Valori importanti**

* **Azure AsyncOperation** -questa proprietà contiene hello URI tooquery hello Async risolvere i problemi di funzionamento
* **Percorso** -questa proprietà contiene hello URI in cui i risultati di hello risultano hello operazione è stata completata

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>Hello async completamento dell'operazione di query

Utilizzare hello operazioni URI tooquery per lo stato di avanzamento hello dell'operazione di hello, come illustrato nel seguente esempio hello:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Durante l'operazione di hello è in corso, hello Mostra risposta **InProgress** come illustrato nel seguente esempio hello:

```json
{
  "status": "InProgress"
}
```

Quando l'operazione di hello è stata completata, lo stato di hello cambia troppo**Succeeded**.

```json
{
  "status": "Succeeded"
}
```

Hello risposte seguenti sono esempi di una tipica risposta restituito quando si eseguono query risultati hello di risoluzione dei problemi di una connessione.

### <a name="retrieve-hello-results"></a>Recuperare i risultati di hello

Una volta lo stato di hello restituito è **Succeeded**, chiamare un metodo GET su hello operationResult URI tooretrieve risultati hello.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Hello risposte seguenti sono esempi di una tipica risposta restituito quando si eseguono query risultati hello di risoluzione dei problemi di una connessione.

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a>Informazioni sui risultati hello

testo dell'azione Hello vengono fornite indicazioni generali su come tooresolve hello problema. Se è possibile eseguire un'azione per il problema di hello, viene fornito un collegamento con informazioni aggiuntive. In caso di hello in cui è presente alcun altro materiale sussidiario, risposta hello fornisce hello url tooopen un caso di supporto.  Per ulteriori informazioni sulle proprietà hello di risposta hello e cosa è inclusa, visitare [Panoramica monitoraggio risolvere i problemi di rete](network-watcher-troubleshoot-overview.md)

Per istruzioni sul download di file dall'account di archiviazione di azure, consultare troppo[Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Un altro strumento che può essere usato è Storage Explorer. Ulteriori informazioni su soluzioni di archiviazione sono reperibile qui in hello seguente collegamento: [Esplora archivi](http://storageexplorer.com/)

## <a name="next-steps"></a>Passaggi successivi

Se le impostazioni sono state modificate che arresta la connettività VPN, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza che possono essere in questione.
