---
title: "Controllare la connettività con Azure Network Watcher - Interfaccia della riga di comando di Azure 2.0 | Microsoft Docs"
description: "Questa pagina descrive come eseguire il controllo della connettività con Network Watcher usando l'interfaccia della riga di comando di Azure 2.0"
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
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: c1deaa40bfda0bf3858ad56d3d6a90df34351278
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="c4ba2-103">Controllare la connettività con Azure Network Watcher usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c4ba2-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c4ba2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4ba2-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="c4ba2-105">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="c4ba2-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="c4ba2-106">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="c4ba2-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="c4ba2-107">Informazioni su come usare la connettività per verificare se è possibile stabilire una connessione TCP diretta da una macchina virtuale a uno specifico endpoint.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-107">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c4ba2-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c4ba2-108">Before you begin</span></span>

<span data-ttu-id="c4ba2-109">Questo articolo presuppone che l'utente disponga delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4ba2-109">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="c4ba2-110">Un'istanza di Network Watcher nell'area di cui si vuole controllare la connettività.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-110">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="c4ba2-111">Macchine virtuali con cui controllare la connettività.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-111">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="c4ba2-112">Il controllo della connettività richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="c4ba2-113">Per installare l'estensione in una VM Windows, vedere [Estensione macchina virtuale agente Azure Network Watcher per Windows](../virtual-machines/windows/extensions-nwa.md) e per una VM Linux VM vedere [Estensione macchina virtuale Azure Network Watcher Agent per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="c4ba2-113">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="c4ba2-114">Registrare la funzionalità in anteprima</span><span class="sxs-lookup"><span data-stu-id="c4ba2-114">Register the preview capability</span></span> 

<span data-ttu-id="c4ba2-115">Il controllo della connettività è attualmente disponibile in anteprima pubblica; per usare questa funzionalità, è necessario averne eseguito la registrazione.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-115">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="c4ba2-116">A tale scopo, usare l'esempio di interfaccia della riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c4ba2-116">To do this, run the following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="c4ba2-117">Per verificare se la registrazione è riuscita, eseguire questo comando dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="c4ba2-117">To verify the registration was successful, run the following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="c4ba2-118">Se la funzionalità è stata registrata correttamente, l'output deve corrispondere a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c4ba2-118">If the feature was properly registered, the output should match the following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="c4ba2-119">Controllare la connettività a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c4ba2-119">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="c4ba2-120">Questo esempio controlla la connettività a una macchina virtuale di destinazione sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-120">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="c4ba2-121">Esempio</span><span class="sxs-lookup"><span data-stu-id="c4ba2-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="c4ba2-122">Response</span><span class="sxs-lookup"><span data-stu-id="c4ba2-122">Response</span></span>

<span data-ttu-id="c4ba2-123">La risposta seguente è relativa all'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-123">The following response is from the previous example.</span></span>  <span data-ttu-id="c4ba2-124">In questa risposta `ConnectionStatus` è **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-124">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="c4ba2-125">Si noti che tutti i probe inviati presentano un errore.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-125">You can see that all the probes sent failed.</span></span> <span data-ttu-id="c4ba2-126">Si è verificato un problema di connettività nell'appliance virtuale a causa di un valore `NetworkSecurityRule` configurato dall'utente per bloccare il traffico in ingresso sulla porta 80, denominato **UserRule_Port80**.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-126">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="c4ba2-127">Queste informazioni possono essere usate per analizzare i problemi di connessione.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-127">This information can be used to research connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="c4ba2-128">Problemi relativi alla convalida del routing</span><span class="sxs-lookup"><span data-stu-id="c4ba2-128">Validate routing issues</span></span>

<span data-ttu-id="c4ba2-129">L'esempio verifica la connettività tra una macchina virtuale e un endpoint remoto.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-129">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="c4ba2-130">Esempio</span><span class="sxs-lookup"><span data-stu-id="c4ba2-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="c4ba2-131">Response</span><span class="sxs-lookup"><span data-stu-id="c4ba2-131">Response</span></span>

<span data-ttu-id="c4ba2-132">Nell'esempio seguente `connectionStatus` è **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-132">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="c4ba2-133">I dettagli relativi a `hops` sotto `issues` indicano che il traffico è stato bloccato a causa di un valore `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-133">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="c4ba2-134">Controllare la latenza del sito Web</span><span class="sxs-lookup"><span data-stu-id="c4ba2-134">Check website latency</span></span>

<span data-ttu-id="c4ba2-135">L'esempio seguente controlla la connettività a un sito Web.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-135">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="c4ba2-136">Esempio</span><span class="sxs-lookup"><span data-stu-id="c4ba2-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="c4ba2-137">Response</span><span class="sxs-lookup"><span data-stu-id="c4ba2-137">Response</span></span>

<span data-ttu-id="c4ba2-138">Nella risposta seguente il valore indicato per `connectionStatus` è **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-138">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="c4ba2-139">In caso di esito positivo della connessione vengono forniti i valori della latenza.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="c4ba2-140">Controllare la connettività a un endpoint di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c4ba2-140">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="c4ba2-141">L'esempio seguente controlla la connettività da una macchina virtuale a un account di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-141">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="c4ba2-142">Esempio</span><span class="sxs-lookup"><span data-stu-id="c4ba2-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="c4ba2-143">Response</span><span class="sxs-lookup"><span data-stu-id="c4ba2-143">Response</span></span>

<span data-ttu-id="c4ba2-144">Il codice JSON seguente è la risposta di esempio generata dall'esecuzione del cmdlet precedente.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-144">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="c4ba2-145">Poiché il controllo ha esito positivo, il valore indicato per la proprietà `connectionStatus` è **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-145">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="c4ba2-146">Vengono forniti i dettagli sul numero di hop necessari per raggiungere il BLOB di archiviazione e la latenza.</span><span class="sxs-lookup"><span data-stu-id="c4ba2-146">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="c4ba2-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4ba2-147">Next steps</span></span>

<span data-ttu-id="c4ba2-148">Per altre informazioni su come automatizzare le acquisizioni di pacchetti tramite gli avvisi della macchina virtuale, leggere l'articolo su come [creare un'acquisizione di pacchetti attivata da un avviso](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="c4ba2-148">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="c4ba2-149">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="c4ba2-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
