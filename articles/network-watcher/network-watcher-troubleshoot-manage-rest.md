---
title: Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni tramite Network Watcher di Azure - REST | Documentazione Microsoft
description: Questa pagina illustra come risolvere i problemi relativi al gateway di rete virtuale e alle connessioni con Network Watcher di Azure tramite REST
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
ms.openlocfilehash: bc61be74d85a309c158716460b918baaf4fa94dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="651f4-103">Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni tramite Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="651f4-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="651f4-104">Portale</span><span class="sxs-lookup"><span data-stu-id="651f4-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="651f4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="651f4-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="651f4-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="651f4-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="651f4-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="651f4-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="651f4-108">API REST</span><span class="sxs-lookup"><span data-stu-id="651f4-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="651f4-109">Network Watcher offre numerose funzionalità che consentono di comprendere le risorse di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="651f4-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="651f4-110">Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse.</span><span class="sxs-lookup"><span data-stu-id="651f4-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="651f4-111">La funzionalità può essere chiamata dal portale, da PowerShell, dall'interfaccia della riga di comando o dall'API REST.</span><span class="sxs-lookup"><span data-stu-id="651f4-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="651f4-112">Quando chiamata, Network Watcher controlla l'integrità di un gateway di rete virtuale o di una connessione e restituisce i risultati.</span><span class="sxs-lookup"><span data-stu-id="651f4-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="651f4-113">Questo articolo illustra le diverse attività di gestione attualmente disponibili per la risoluzione dei problemi relativi alle risorse.</span><span class="sxs-lookup"><span data-stu-id="651f4-113">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="651f4-114">**Risolvere i problemi relativi a un gateway di rete virtuale**</span><span class="sxs-lookup"><span data-stu-id="651f4-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="651f4-115">**Risolvere i problemi relativi a una connessione**</span><span class="sxs-lookup"><span data-stu-id="651f4-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="651f4-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="651f4-116">Before you begin</span></span>

<span data-ttu-id="651f4-117">ARMclient viene usato per chiamare l'API REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="651f4-117">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="651f4-118">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="651f4-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="651f4-119">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="651f4-119">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="651f4-120">Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="651f4-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="651f4-121">Panoramica</span><span class="sxs-lookup"><span data-stu-id="651f4-121">Overview</span></span>

<span data-ttu-id="651f4-122">La risoluzione dei problemi relativi a Network Watcher consente di risolvere i problemi che si verificano con i gateway di rete virtuale e le connessioni.</span><span class="sxs-lookup"><span data-stu-id="651f4-122">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="651f4-123">Quando viene inviata una richiesta di risoluzione dei problemi delle risorse, i log vengono sottoposti a query e controllati.</span><span class="sxs-lookup"><span data-stu-id="651f4-123">When a request is made to the resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="651f4-124">Dopo aver completato l'ispezione, vengono restituiti i risultati.</span><span class="sxs-lookup"><span data-stu-id="651f4-124">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="651f4-125">Le richieste di risoluzione dei problemi delle API sono richieste a esecuzione prolungata, che possono richiedere anche diversi minuti per restituire un risultato.</span><span class="sxs-lookup"><span data-stu-id="651f4-125">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="651f4-126">I log vengono archiviati in un contenitore di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="651f4-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="651f4-127">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="651f4-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="651f4-128">Risolvere i problemi relativi a un gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="651f4-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-the-troubleshoot-request"></a><span data-ttu-id="651f4-129">PUBBLICARE la richiesta di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="651f4-129">POST the troubleshoot request</span></span>

<span data-ttu-id="651f4-130">Nell'esempio seguente viene eseguita una query sullo stato di un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="651f4-130">The following example queries the status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="651f4-131">Poiché questa operazione ha una lunga esecuzione, l'URI per le query dell'operazione e l'URI per il risultato vengono restituiti nell'intestazione della risposta come illustrato nella risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="651f4-131">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="651f4-132">**Valori importanti**</span><span class="sxs-lookup"><span data-stu-id="651f4-132">**Important Values**</span></span>

* <span data-ttu-id="651f4-133">**Azure-AsyncOperation**: questa proprietà contiene l'URI per eseguire le query sull'operazione di risoluzione dei problemi asincrona</span><span class="sxs-lookup"><span data-stu-id="651f4-133">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="651f4-134">**Location**: questa proprietà contiene l'URI in cui si trovano i risultati una volta completata l'operazione</span><span class="sxs-lookup"><span data-stu-id="651f4-134">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="651f4-135">Eseguire una query all'operazione asincrona per il completamento</span><span class="sxs-lookup"><span data-stu-id="651f4-135">Query the async operation for completion</span></span>

<span data-ttu-id="651f4-136">Usare l'URI delle operazioni per eseguire query sullo stato di avanzamento dell'operazione, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="651f4-136">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="651f4-137">Mentre l'operazione è in corso, la risposta mostra **InProgress** come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="651f4-137">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="651f4-138">Al termine dell'operazione, lo stato diventa **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="651f4-138">When the operation is complete the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-the-results"></a><span data-ttu-id="651f4-139">Recuperare i risultati</span><span class="sxs-lookup"><span data-stu-id="651f4-139">Retrieve the results</span></span>

<span data-ttu-id="651f4-140">Quando lo stato restituito è **Succeeded**, chiamare un metodo GET sull'URI operationResult per recuperare i risultati.</span><span class="sxs-lookup"><span data-stu-id="651f4-140">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="651f4-141">Le risposte seguenti sono esempi di una tipica risposta ridotta, restituita quando si eseguono query sui risultati della risoluzione dei problemi relativi a un gateway.</span><span class="sxs-lookup"><span data-stu-id="651f4-141">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span></span> <span data-ttu-id="651f4-142">Vedere [Informazioni sui risultati](#understanding-the-results) per chiarimenti sul significato delle proprietà nella risposta.</span><span class="sxs-lookup"><span data-stu-id="651f4-142">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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


## <a name="troubleshoot-connections"></a><span data-ttu-id="651f4-143">Risoluzione dei problemi relativi alle connessioni</span><span class="sxs-lookup"><span data-stu-id="651f4-143">Troubleshoot Connections</span></span>

<span data-ttu-id="651f4-144">Nell'esempio seguente viene eseguita una query sullo stato di una connessione.</span><span class="sxs-lookup"><span data-stu-id="651f4-144">The following example queries the status of a Connection.</span></span>

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
> <span data-ttu-id="651f4-145">L'operazione di risoluzione dei problemi non può essere eseguita in parallelo su una connessione e sui gateway corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="651f4-145">The troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="651f4-146">L'operazione deve essere completata prima di eseguire il gateway sulla risorsa precedente.</span><span class="sxs-lookup"><span data-stu-id="651f4-146">The operation must complete prior to running it on the previous resource.</span></span>

<span data-ttu-id="651f4-147">Poiché questa transazione ha una lunga esecuzione, nell'intestazione della risposta l'URI per le query dell'operazione e l'URI per il risultato vengono restituiti come illustrato nella risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="651f4-147">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span></span>

<span data-ttu-id="651f4-148">**Valori importanti**</span><span class="sxs-lookup"><span data-stu-id="651f4-148">**Important Values**</span></span>

* <span data-ttu-id="651f4-149">**Azure-AsyncOperation**: questa proprietà contiene l'URI per eseguire le query sull'operazione di risoluzione dei problemi asincrona</span><span class="sxs-lookup"><span data-stu-id="651f4-149">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="651f4-150">**Location**: questa proprietà contiene l'URI in cui si trovano i risultati una volta completata l'operazione</span><span class="sxs-lookup"><span data-stu-id="651f4-150">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="651f4-151">Eseguire una query all'operazione asincrona per il completamento</span><span class="sxs-lookup"><span data-stu-id="651f4-151">Query the async operation for completion</span></span>

<span data-ttu-id="651f4-152">Usare l'URI delle operazioni per eseguire query sullo stato di avanzamento dell'operazione, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="651f4-152">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="651f4-153">Mentre l'operazione è in corso, la risposta mostra **InProgress** come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="651f4-153">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="651f4-154">Al termine dell'operazione, lo stato diventa **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="651f4-154">When the operation is complete, the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="651f4-155">Le risposte seguenti sono esempi di una tipica risposta restituita quando si eseguono query sui risultati della risoluzione dei problemi relativi a una connessione.</span><span class="sxs-lookup"><span data-stu-id="651f4-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

### <a name="retrieve-the-results"></a><span data-ttu-id="651f4-156">Recuperare i risultati</span><span class="sxs-lookup"><span data-stu-id="651f4-156">Retrieve the results</span></span>

<span data-ttu-id="651f4-157">Quando lo stato restituito è **Succeeded**, chiamare un metodo GET sull'URI operationResult per recuperare i risultati.</span><span class="sxs-lookup"><span data-stu-id="651f4-157">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="651f4-158">Le risposte seguenti sono esempi di una tipica risposta restituita quando si eseguono query sui risultati della risoluzione dei problemi relativi a una connessione.</span><span class="sxs-lookup"><span data-stu-id="651f4-158">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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

## <a name="understanding-the-results"></a><span data-ttu-id="651f4-159">Informazioni sui risultati</span><span class="sxs-lookup"><span data-stu-id="651f4-159">Understanding the results</span></span>

<span data-ttu-id="651f4-160">Il testo dell'azione offre indicazioni generiche su come risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="651f4-160">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="651f4-161">Se è possibile eseguire un'azione per il problema, viene fornito un collegamento con altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="651f4-161">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="651f4-162">Nel caso in cui non siano presenti altre indicazioni, la risposta include l'URL per aprire una richiesta di assistenza.</span><span class="sxs-lookup"><span data-stu-id="651f4-162">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="651f4-163">Per altre informazioni sulle proprietà della risposta e ciò che vie è incluso, consultare la [panoramica sulla risoluzione dei problemi in Network Watcher](network-watcher-troubleshoot-overview.md).</span><span class="sxs-lookup"><span data-stu-id="651f4-163">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="651f4-164">Per istruzioni sul download di file dall'account di archiviazione di Azure, consultare [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="651f4-164">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="651f4-165">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="651f4-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="651f4-166">Altre informazioni su Storage Explorer sono reperibili facendo clic sul collegamento seguente: [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="651f4-166">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="651f4-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="651f4-167">Next steps</span></span>

<span data-ttu-id="651f4-168">Se sono state modificate le impostazioni che arrestano la connettività VPN, vedere [Gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) per tenere traccia del gruppo di sicurezza di rete e delle regole di sicurezza in questione.</span><span class="sxs-lookup"><span data-stu-id="651f4-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
