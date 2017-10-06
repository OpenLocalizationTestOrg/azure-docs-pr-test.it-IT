---
title: "connettività aaaCheck con Watcher di rete di Azure - portale di Azure | Documenti Microsoft"
description: "Questa pagina viene illustrato come la connettività toocheck con Watcher di rete in hello portale di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="b6bb5-103">Verificare la connettività con Watcher di rete di Azure utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b6bb5-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b6bb5-104">Portale</span><span class="sxs-lookup"><span data-stu-id="b6bb5-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="b6bb5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6bb5-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="b6bb5-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="b6bb5-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="b6bb5-107">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="b6bb5-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="b6bb5-108">Informazioni su come è possibile stabilire toouse connettività tooverify se una connessione TCP diretta da una macchina virtuale di tooa dato endpoint.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6bb5-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b6bb5-109">Before you begin</span></span>

<span data-ttu-id="b6bb5-110">Questo articolo si presuppone di che aver hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="b6bb5-111">Un'istanza del controllo di rete nell'area di hello desiderato toocheck connettività.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="b6bb5-112">Connettività toocheck di macchine virtuali con.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="b6bb5-113">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="b6bb5-114">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey).</span><span class="sxs-lookup"><span data-stu-id="b6bb5-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="b6bb5-115">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="b6bb5-116">Il controllo della connettività richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="b6bb5-117">Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="b6bb5-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="b6bb5-118">Registrare la funzionalità di anteprima hello</span><span class="sxs-lookup"><span data-stu-id="b6bb5-118">Register hello preview capability</span></span>

<span data-ttu-id="b6bb5-119">Verifica della connettività è attualmente in anteprima pubblica, toouse questa funzionalità che è necessario toobe registrato.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="b6bb5-120">toodo, hello esecuzione seguente esempio di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="b6bb5-121">la registrazione di hello tooverify è stata completata correttamente, eseguire hello seguente esempio di Powershell:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="b6bb5-122">Se è stato registrato correttamente funzionalità hello, output di hello devono corrispondere seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="b6bb5-123">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="b6bb5-123">Log in with ARMClient</span></span>

<span data-ttu-id="b6bb5-124">Accedi tooarmclient con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="b6bb5-125">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b6bb5-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="b6bb5-126">Eseguire hello seguenti script tooreturn una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="b6bb5-127">Queste informazioni sono necessarie per eseguire la connettività.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="b6bb5-128">Hello seguente di codice deve valori per hello seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="b6bb5-129">**subscriptionId** -hello toouse ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="b6bb5-130">**resourceGroupName** : hello nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="b6bb5-131">Dall'output seguente hello, hello ID della macchina virtuale hello viene utilizzato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

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

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="b6bb5-132">Verificare la connettività tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="b6bb5-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="b6bb5-133">Questo esempio viene verificata la connettività tooa macchina virtuale di destinazione sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="b6bb5-134">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bb5-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="b6bb5-135">Poiché questa operazione è lunga in esecuzione, hello per risultato hello viene restituito l'URI nell'intestazione di risposta hello come illustrato nella seguente risposta hello:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="b6bb5-136">**Valori importanti**</span><span class="sxs-lookup"><span data-stu-id="b6bb5-136">**Important Values**</span></span>

* <span data-ttu-id="b6bb5-137">**Percorso** -questa proprietà contiene hello URI in cui i risultati di hello risultano hello operazione è stata completata</span><span class="sxs-lookup"><span data-stu-id="b6bb5-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="b6bb5-138">Response</span><span class="sxs-lookup"><span data-stu-id="b6bb5-138">Response</span></span>

<span data-ttu-id="b6bb5-139">Hello seguente risposta è tratto dall'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="b6bb5-140">Nella risposta, hello `ConnectionStatus` è **non raggiungibile**.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="b6bb5-141">Si noterà che tutti hello probe inviati non riuscite.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="b6bb5-142">connettività Hello non riuscita nel dispositivo virtuale hello tooa scadenza configurata dall'utente `NetworkSecurityRule` denominato **UserRule_Port80**, configurato tooblock il traffico in entrata sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="b6bb5-143">Queste informazioni possono essere utilizzati tooresearch i problemi di connessione.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-143">This information can be used tooresearch connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="b6bb5-144">Problemi relativi alla convalida del routing</span><span class="sxs-lookup"><span data-stu-id="b6bb5-144">Validate routing issues</span></span>

<span data-ttu-id="b6bb5-145">esempio Hello controlla la connettività tra una macchina virtuale e un endpoint remoto.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="b6bb5-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bb5-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="b6bb5-147">Poiché questa operazione è lunga in esecuzione, hello per risultato hello viene restituito l'URI nell'intestazione di risposta hello come illustrato nella seguente risposta hello:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="b6bb5-148">**Valori importanti**</span><span class="sxs-lookup"><span data-stu-id="b6bb5-148">**Important Values**</span></span>

* <span data-ttu-id="b6bb5-149">**Percorso** -questa proprietà contiene hello URI in cui i risultati di hello risultano hello operazione è stata completata</span><span class="sxs-lookup"><span data-stu-id="b6bb5-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="b6bb5-150">Response</span><span class="sxs-lookup"><span data-stu-id="b6bb5-150">Response</span></span>

<span data-ttu-id="b6bb5-151">Nell'esempio seguente di hello, hello `connectionStatus` viene visualizzato come **non raggiungibile**.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="b6bb5-152">In hello `hops` informazioni dettagliate, è possibile visualizzare in `issues` che è stato bloccato scadenza traffico hello tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="b6bb5-153">Controllare la latenza del sito Web</span><span class="sxs-lookup"><span data-stu-id="b6bb5-153">Check website latency</span></span>

<span data-ttu-id="b6bb5-154">Hello esempio controlla sito Web di tooa connettività hello.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="b6bb5-155">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bb5-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="b6bb5-156">Poiché questa operazione è lunga in esecuzione, hello per risultato hello viene restituito l'URI nell'intestazione di risposta hello come illustrato nella seguente risposta hello:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="b6bb5-157">**Valori importanti**</span><span class="sxs-lookup"><span data-stu-id="b6bb5-157">**Important Values**</span></span>

* <span data-ttu-id="b6bb5-158">**Percorso** -questa proprietà contiene hello URI in cui i risultati di hello risultano hello operazione è stata completata</span><span class="sxs-lookup"><span data-stu-id="b6bb5-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="b6bb5-159">Response</span><span class="sxs-lookup"><span data-stu-id="b6bb5-159">Response</span></span>

<span data-ttu-id="b6bb5-160">In hello seguente risposta, è possibile vedere hello `connectionStatus` viene illustrato come **raggiungibile**.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="b6bb5-161">In caso di esito positivo della connessione vengono forniti i valori della latenza.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="b6bb5-162">Controllare la connettività tooa archiviazione endpoint</span><span class="sxs-lookup"><span data-stu-id="b6bb5-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="b6bb5-163">Hello esempio seguente verifica la connettività di hello da un account di archiviazione blog tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="b6bb5-164">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bb5-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="b6bb5-165">Poiché questa operazione è lunga in esecuzione, hello per risultato hello viene restituito l'URI nell'intestazione di risposta hello come illustrato nella seguente risposta hello:</span><span class="sxs-lookup"><span data-stu-id="b6bb5-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="b6bb5-166">**Valori importanti**</span><span class="sxs-lookup"><span data-stu-id="b6bb5-166">**Important Values**</span></span>

* <span data-ttu-id="b6bb5-167">**Percorso** -questa proprietà contiene hello URI in cui i risultati di hello risultano hello operazione è stata completata</span><span class="sxs-lookup"><span data-stu-id="b6bb5-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="b6bb5-168">Response</span><span class="sxs-lookup"><span data-stu-id="b6bb5-168">Response</span></span>

<span data-ttu-id="b6bb5-169">Hello riportato di seguito è risposta hello dall'esecuzione precedente chiamata all'API hello.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="b6bb5-170">Come controllo hello ha esito positivo, hello `connectionStatus` vengono visualizzate le proprietà come **raggiungibile**.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="b6bb5-171">Vengono fornite informazioni hello riguardanti hello numero di hop tooreach obbligatorio hello archiviazione blob e latenza.</span><span class="sxs-lookup"><span data-stu-id="b6bb5-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="b6bb5-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6bb5-172">Next steps</span></span>

<span data-ttu-id="b6bb5-173">Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="b6bb5-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="b6bb5-174">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="b6bb5-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














