---
title: 'Gestire le acquisizioni di pacchetti con Azure Network Watcher: API REST | Microsoft Docs'
description: "Questa pagina illustra come gestire la funzionalità di acquisizione di pacchetti di Network Watcher usando l'API REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="f5ab7-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher usando l'API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="f5ab7-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f5ab7-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f5ab7-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="f5ab7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ab7-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="f5ab7-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="f5ab7-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="f5ab7-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="f5ab7-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="f5ab7-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="f5ab7-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="f5ab7-109">Il servizio di acquisizione di pacchetti di Network Watcher consente di creare sessioni di acquisizione per registrare il traffico da e verso una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="f5ab7-110">Sono disponibili filtri per la sessione di acquisizione per garantire che venga acquisito solo il traffico desiderato.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="f5ab7-111">Il servizio di acquisizione di pacchetti consente di individuare eventuali anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="f5ab7-112">Altri utilizzi comprendono la raccolta di statistiche di rete, informazioni sulle intrusioni nella rete, debug delle comunicazioni client-server e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="f5ab7-113">La possibilità di attivare da remoto l'acquisizione di pacchetti evita di dover eseguire manualmente questa operazione sul computer desiderato, consentendo un notevole risparmio di tempo.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="f5ab7-114">Questo articolo illustra le diverse attività di gestione attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="f5ab7-115">**Ottenere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="f5ab7-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="f5ab7-116">**Elencare tutte le acquisizioni di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="f5ab7-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="f5ab7-117">**Effettuare una query dello stato di un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="f5ab7-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="f5ab7-118">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="f5ab7-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="f5ab7-119">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="f5ab7-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="f5ab7-120">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="f5ab7-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="f5ab7-121">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="f5ab7-121">Before you begin</span></span>

<span data-ttu-id="f5ab7-122">In questo scenario si chiama l'API REST Network Watcher per eseguire la verifica del flusso IP.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="f5ab7-123">ARMclient viene usato per chiamare l'API REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="f5ab7-124">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="f5ab7-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="f5ab7-125">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="f5ab7-126">L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="f5ab7-127">Per installare l'estensione in una VM Windows, vedere [Estensione macchina virtuale agente Azure Network Watcher per Windows](../virtual-machines/windows/extensions-nwa.md) e per una VM Linux VM vedere [Estensione macchina virtuale Azure Network Watcher Agent per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="f5ab7-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="f5ab7-128">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="f5ab7-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="f5ab7-129">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f5ab7-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="f5ab7-130">Eseguire lo script seguente per restituire la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="f5ab7-131">Queste informazioni sono necessarie per avviare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="f5ab7-132">Per il codice seguente sono necessarie alcune variabili:</span><span class="sxs-lookup"><span data-stu-id="f5ab7-132">The following code needs variables:</span></span>

- <span data-ttu-id="f5ab7-133">**subscriptionId**: l'ID sottoscrizione può essere recuperato anche con il cmdlet **Get-AzureRMSubscription**.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="f5ab7-134">**resourceGroupName**: il nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="f5ab7-135">L'ID della macchina virtuale dell'output seguente viene usato nell'esempio successivo.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="f5ab7-136">Ottenere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5ab7-136">Get a packet capture</span></span>

<span data-ttu-id="f5ab7-137">L'esempio seguente ottiene lo stato di una singola acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5ab7-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="f5ab7-138">Le risposte seguenti sono esempi di una tipica risposta restituita quando si effettua una query sullo stato di un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="f5ab7-139">Elencare tutte le acquisizioni di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5ab7-139">List all packet captures</span></span>

<span data-ttu-id="f5ab7-140">L'esempio seguente ottiene tutte le sessioni di acquisizione di pacchetti in un'area.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="f5ab7-141">La risposta seguente è un esempio di una tipica risposta restituita quando si ottengono tutte le acquisizioni di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5ab7-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="f5ab7-142">Effettuare una query dello stato di acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5ab7-142">Query packet capture status</span></span>

<span data-ttu-id="f5ab7-143">L'esempio seguente ottiene tutte le sessioni di acquisizione di pacchetti in un'area.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="f5ab7-144">La risposta seguente è un esempio di una tipica risposta restituita quando si effettua una query sullo stato di un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="f5ab7-145">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5ab7-145">Start packet capture</span></span>

<span data-ttu-id="f5ab7-146">L'esempio seguente crea un'acquisizione di pacchetti in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="f5ab7-147">Nell'esempio vengono impostati parametri per consentire flessibilità nella creazione di un esempio.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="f5ab7-148">Arrestare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5ab7-148">Stop packet capture</span></span>

<span data-ttu-id="f5ab7-149">L'esempio seguente arresta un'acquisizione di pacchetti in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="f5ab7-150">Nell'esempio vengono impostati parametri per consentire flessibilità nella creazione di un esempio.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="f5ab7-151">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5ab7-151">Delete packet capture</span></span>

<span data-ttu-id="f5ab7-152">L'esempio seguente elimina un'acquisizione di pacchetti in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="f5ab7-153">Nell'esempio vengono impostati parametri per consentire flessibilità nella creazione di un esempio.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="f5ab7-154">L'eliminazione di un'acquisizione di pacchetti non elimina il file nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f5ab7-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5ab7-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5ab7-155">Next steps</span></span>

<span data-ttu-id="f5ab7-156">Per istruzioni sul download di file dall'account di archiviazione di Azure, vedere [Introduzione all'archivio BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f5ab7-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f5ab7-157">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="f5ab7-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="f5ab7-158">Altre informazioni su Storage Explorer sono reperibili facendo clic sul collegamento seguente: [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f5ab7-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="f5ab7-159">Per altre informazioni su come automatizzare le acquisizioni di pacchetti tramite gli avvisi della macchina virtuale, leggere l'articolo su come [creare un'acquisizione di pacchetti attivata da un avviso](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="f5ab7-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













