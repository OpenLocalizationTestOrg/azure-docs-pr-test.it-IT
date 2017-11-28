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
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="59a3b-103">Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni tramite Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="59a3b-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="59a3b-104">Portale</span><span class="sxs-lookup"><span data-stu-id="59a3b-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="59a3b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59a3b-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="59a3b-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="59a3b-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="59a3b-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="59a3b-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="59a3b-108">API REST</span><span class="sxs-lookup"><span data-stu-id="59a3b-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="59a3b-109">Watcher di rete fornisce numerose funzionalità toounderstanding in relazione le risorse di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="59a3b-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="59a3b-110">Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse.</span><span class="sxs-lookup"><span data-stu-id="59a3b-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="59a3b-111">Risoluzione dei problemi di risorse può essere chiamato tramite il portale di hello, PowerShell, CLI o API REST.</span><span class="sxs-lookup"><span data-stu-id="59a3b-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="59a3b-112">Quando viene chiamato, Watcher di rete Controlla integrità hello di un Gateway di rete virtuale o una connessione e restituisce i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="59a3b-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="59a3b-113">In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per la risoluzione dei problemi di risorse.</span><span class="sxs-lookup"><span data-stu-id="59a3b-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="59a3b-114">**Risolvere i problemi relativi a un gateway di rete virtuale**</span><span class="sxs-lookup"><span data-stu-id="59a3b-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="59a3b-115">**Risolvere i problemi relativi a una connessione**</span><span class="sxs-lookup"><span data-stu-id="59a3b-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="59a3b-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="59a3b-116">Before you begin</span></span>

<span data-ttu-id="59a3b-117">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59a3b-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="59a3b-118">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="59a3b-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="59a3b-119">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="59a3b-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="59a3b-120">Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="59a3b-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="59a3b-121">Panoramica</span><span class="sxs-lookup"><span data-stu-id="59a3b-121">Overview</span></span>

<span data-ttu-id="59a3b-122">Risoluzione dei problemi di controllo di rete consente di hello risolvere i problemi che si verificano con i gateway di rete virtuale e le connessioni.</span><span class="sxs-lookup"><span data-stu-id="59a3b-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="59a3b-123">Quando una richiesta viene effettuata la risorsa toohello risoluzione dei problemi, registri esegue una query e controllato.</span><span class="sxs-lookup"><span data-stu-id="59a3b-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="59a3b-124">Una volta completato controllo, vengono restituiti risultati hello.</span><span class="sxs-lookup"><span data-stu-id="59a3b-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="59a3b-125">Hello risolvere API richieste sono molto richieste, che potrebbe richiedere più minuti tooreturn un risultato in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="59a3b-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="59a3b-126">I log vengono archiviati in un contenitore di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="59a3b-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="59a3b-127">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="59a3b-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="59a3b-128">Risolvere i problemi relativi a un gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="59a3b-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="59a3b-129">Hello POST risolvere i problemi di richiesta</span><span class="sxs-lookup"><span data-stu-id="59a3b-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="59a3b-130">Hello seguente stato hello query di esempio di un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="59a3b-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="59a3b-131">Poiché questa operazione è lunga in esecuzione, hello URI per l'esecuzione di query operazione hello e hello URI per il risultato di hello viene restituito nell'intestazione di risposta hello, come illustrato nella seguente risposta hello:</span><span class="sxs-lookup"><span data-stu-id="59a3b-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="59a3b-132">**Valori importanti**</span><span class="sxs-lookup"><span data-stu-id="59a3b-132">**Important Values**</span></span>

* <span data-ttu-id="59a3b-133">**Azure AsyncOperation** -questa proprietà contiene hello URI tooquery hello Async risolvere i problemi di funzionamento</span><span class="sxs-lookup"><span data-stu-id="59a3b-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="59a3b-134">**Percorso** -questa proprietà contiene hello URI in cui i risultati di hello risultano hello operazione è stata completata</span><span class="sxs-lookup"><span data-stu-id="59a3b-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="59a3b-135">Hello async completamento dell'operazione di query</span><span class="sxs-lookup"><span data-stu-id="59a3b-135">Query hello async operation for completion</span></span>

<span data-ttu-id="59a3b-136">Utilizzare hello operazioni URI tooquery per lo stato di avanzamento hello dell'operazione di hello, come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="59a3b-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="59a3b-137">Durante l'operazione di hello è in corso, hello Mostra risposta **InProgress** come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="59a3b-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="59a3b-138">Quando un'operazione hello è modifiche dello stato di completamento hello troppo**Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="59a3b-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="59a3b-139">Recuperare i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="59a3b-139">Retrieve hello results</span></span>

<span data-ttu-id="59a3b-140">Una volta lo stato di hello restituito è **Succeeded**, chiamare un metodo GET su hello operationResult URI tooretrieve risultati hello.</span><span class="sxs-lookup"><span data-stu-id="59a3b-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="59a3b-141">Hello risposte seguenti sono esempi di una tipica risposta ridotte restituito quando si eseguono query risultati hello di risoluzione dei problemi di un gateway.</span><span class="sxs-lookup"><span data-stu-id="59a3b-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="59a3b-142">Vedere [informazioni sui risultati hello](#understanding-the-results) tooget chiarimento su quali proprietà hello in Media risposta hello.</span><span class="sxs-lookup"><span data-stu-id="59a3b-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

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


## <a name="troubleshoot-connections"></a><span data-ttu-id="59a3b-143">Risoluzione dei problemi relativi alle connessioni</span><span class="sxs-lookup"><span data-stu-id="59a3b-143">Troubleshoot Connections</span></span>

<span data-ttu-id="59a3b-144">Hello seguente stato hello query di esempio di una connessione.</span><span class="sxs-lookup"><span data-stu-id="59a3b-144">hello following example queries hello status of a Connection.</span></span>

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
> <span data-ttu-id="59a3b-145">Hello risolvere i problemi di operazione non può essere eseguito in parallelo su una connessione e il relativo gateway corrispondente.</span><span class="sxs-lookup"><span data-stu-id="59a3b-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="59a3b-146">operazione Hello deve essere completata prima toorunning sul precedente risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="59a3b-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="59a3b-147">Poiché si tratta di una transazione con esecuzione prolungata, nell'intestazione di risposta hello, hello URI per l'esecuzione di query operazione hello e hello URI per il risultato di hello viene restituito come illustrato nella seguente risposta hello:</span><span class="sxs-lookup"><span data-stu-id="59a3b-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="59a3b-148">**Valori importanti**</span><span class="sxs-lookup"><span data-stu-id="59a3b-148">**Important Values**</span></span>

* <span data-ttu-id="59a3b-149">**Azure AsyncOperation** -questa proprietà contiene hello URI tooquery hello Async risolvere i problemi di funzionamento</span><span class="sxs-lookup"><span data-stu-id="59a3b-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="59a3b-150">**Percorso** -questa proprietà contiene hello URI in cui i risultati di hello risultano hello operazione è stata completata</span><span class="sxs-lookup"><span data-stu-id="59a3b-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="59a3b-151">Hello async completamento dell'operazione di query</span><span class="sxs-lookup"><span data-stu-id="59a3b-151">Query hello async operation for completion</span></span>

<span data-ttu-id="59a3b-152">Utilizzare hello operazioni URI tooquery per lo stato di avanzamento hello dell'operazione di hello, come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="59a3b-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="59a3b-153">Durante l'operazione di hello è in corso, hello Mostra risposta **InProgress** come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="59a3b-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="59a3b-154">Quando l'operazione di hello è stata completata, lo stato di hello cambia troppo**Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="59a3b-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="59a3b-155">Hello risposte seguenti sono esempi di una tipica risposta restituito quando si eseguono query risultati hello di risoluzione dei problemi di una connessione.</span><span class="sxs-lookup"><span data-stu-id="59a3b-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="59a3b-156">Recuperare i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="59a3b-156">Retrieve hello results</span></span>

<span data-ttu-id="59a3b-157">Una volta lo stato di hello restituito è **Succeeded**, chiamare un metodo GET su hello operationResult URI tooretrieve risultati hello.</span><span class="sxs-lookup"><span data-stu-id="59a3b-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="59a3b-158">Hello risposte seguenti sono esempi di una tipica risposta restituito quando si eseguono query risultati hello di risoluzione dei problemi di una connessione.</span><span class="sxs-lookup"><span data-stu-id="59a3b-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="59a3b-159">Informazioni sui risultati hello</span><span class="sxs-lookup"><span data-stu-id="59a3b-159">Understanding hello results</span></span>

<span data-ttu-id="59a3b-160">testo dell'azione Hello vengono fornite indicazioni generali su come tooresolve hello problema.</span><span class="sxs-lookup"><span data-stu-id="59a3b-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="59a3b-161">Se è possibile eseguire un'azione per il problema di hello, viene fornito un collegamento con informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="59a3b-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="59a3b-162">In caso di hello in cui è presente alcun altro materiale sussidiario, risposta hello fornisce hello url tooopen un caso di supporto.</span><span class="sxs-lookup"><span data-stu-id="59a3b-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="59a3b-163">Per ulteriori informazioni sulle proprietà hello di risposta hello e cosa è inclusa, visitare [Panoramica monitoraggio risolvere i problemi di rete](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="59a3b-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="59a3b-164">Per istruzioni sul download di file dall'account di archiviazione di azure, consultare troppo[Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="59a3b-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="59a3b-165">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="59a3b-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="59a3b-166">Ulteriori informazioni su soluzioni di archiviazione sono reperibile qui in hello seguente collegamento: [Esplora archivi](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="59a3b-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="59a3b-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59a3b-167">Next steps</span></span>

<span data-ttu-id="59a3b-168">Se le impostazioni sono state modificate che arresta la connettività VPN, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza che possono essere in questione.</span><span class="sxs-lookup"><span data-stu-id="59a3b-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
