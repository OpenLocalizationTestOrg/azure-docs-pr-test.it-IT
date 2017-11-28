---
title: acquisizioni di pacchetti aaaManage con Watcher di rete di Azure - API REST | Documenti Microsoft
description: "Questa pagina viene illustrato come toomanage hello funzionalità di acquisizione di pacchetti di controllo di rete utilizzando l'API REST di Azure"
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
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="67c60-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher usando l'API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="67c60-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="67c60-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="67c60-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="67c60-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67c60-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="67c60-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="67c60-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="67c60-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="67c60-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="67c60-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="67c60-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="67c60-109">Acquisizione di pacchetti di rete Watcher consente tooand toocreate acquisizione sessioni tootrack traffico da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67c60-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="67c60-110">I filtri vengono forniti per hello acquisizione sessione tooensure che si acquisisce solo il traffico hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="67c60-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="67c60-111">Acquisizione di pacchetti consente toodiagnose anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="67c60-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="67c60-112">Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="67c60-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="67c60-113">Essendo in grado di tooremotely trigger pacchetto acquisizioni, questa funzionalità semplifica il carico di hello dell'esecuzione di acquisizione pacchetto eseguita manualmente e nel computer desiderato hello, che consente di risparmiare tempo prezioso.</span><span class="sxs-lookup"><span data-stu-id="67c60-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="67c60-114">In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="67c60-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="67c60-115">**Ottenere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="67c60-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="67c60-116">**Elencare tutte le acquisizioni di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="67c60-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="67c60-117">**Query hello sullo stato di un'acquisizione pacchetti**</span><span class="sxs-lookup"><span data-stu-id="67c60-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="67c60-118">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="67c60-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="67c60-119">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="67c60-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="67c60-120">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="67c60-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="67c60-121">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="67c60-121">Before you begin</span></span>

<span data-ttu-id="67c60-122">In questo scenario, si chiama hello toorun di API Rest Watcher di rete IP flusso verificare.</span><span class="sxs-lookup"><span data-stu-id="67c60-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="67c60-123">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67c60-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="67c60-124">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="67c60-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="67c60-125">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="67c60-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="67c60-126">L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="67c60-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="67c60-127">Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="67c60-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="67c60-128">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="67c60-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="67c60-129">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="67c60-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="67c60-130">Eseguire hello seguenti script tooreturn una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67c60-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="67c60-131">Queste informazioni sono necessarie per avviare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="67c60-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="67c60-132">Hello codice riportato di seguito è necessario variabili:</span><span class="sxs-lookup"><span data-stu-id="67c60-132">hello following code needs variables:</span></span>

- <span data-ttu-id="67c60-133">**subscriptionId** -id sottoscrizione hello possono anche essere recuperati con hello **Get AzureRMSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="67c60-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="67c60-134">**resourceGroupName** : hello nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="67c60-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="67c60-135">Dall'output seguente hello, id di hello della macchina virtuale hello viene utilizzato nell'esempio riportato di seguito hello.</span><span class="sxs-lookup"><span data-stu-id="67c60-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="67c60-136">Ottenere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="67c60-136">Get a packet capture</span></span>

<span data-ttu-id="67c60-137">esempio Hello Ottiene hello stato di un'acquisizione singolo pacchetto</span><span class="sxs-lookup"><span data-stu-id="67c60-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="67c60-138">Hello risposte seguenti sono esempi di una tipica risposta restituito quando si eseguono query stato hello di un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="67c60-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="67c60-139">Elencare tutte le acquisizioni di pacchetti</span><span class="sxs-lookup"><span data-stu-id="67c60-139">List all packet captures</span></span>

<span data-ttu-id="67c60-140">Hello di esempio seguente ottiene tutte le sessioni di acquisizione di pacchetti in un'area.</span><span class="sxs-lookup"><span data-stu-id="67c60-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="67c60-141">Hello risposta seguente è riportato un esempio di una risposta tipica restituito durante il recupero di tutti i pacchetti acquisisce</span><span class="sxs-lookup"><span data-stu-id="67c60-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="67c60-142">Effettuare una query dello stato di acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="67c60-142">Query packet capture status</span></span>

<span data-ttu-id="67c60-143">Hello di esempio seguente ottiene tutte le sessioni di acquisizione di pacchetti in un'area.</span><span class="sxs-lookup"><span data-stu-id="67c60-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="67c60-144">Hello risposta seguente è riportato un esempio di una risposta tipica restituito quando si eseguono query stato hello di un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="67c60-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="67c60-145">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="67c60-145">Start packet capture</span></span>

<span data-ttu-id="67c60-146">Hello di esempio seguente crea una pacchetto di acquisizione in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67c60-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="67c60-147">esempio Hello è tooallow con parametri per la flessibilità per la creazione di un esempio.</span><span class="sxs-lookup"><span data-stu-id="67c60-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="67c60-148">Arrestare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="67c60-148">Stop packet capture</span></span>

<span data-ttu-id="67c60-149">Hello di esempio seguente viene arrestata un'acquisizione di pacchetti in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67c60-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="67c60-150">esempio Hello è tooallow con parametri per la flessibilità per la creazione di un esempio.</span><span class="sxs-lookup"><span data-stu-id="67c60-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="67c60-151">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="67c60-151">Delete packet capture</span></span>

<span data-ttu-id="67c60-152">Hello di esempio seguente elimina un'acquisizione di pacchetti in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67c60-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="67c60-153">esempio Hello è tooallow con parametri per la flessibilità per la creazione di un esempio.</span><span class="sxs-lookup"><span data-stu-id="67c60-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="67c60-154">L'eliminazione di un'acquisizione di pacchetti non elimina il file hello nell'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="67c60-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="67c60-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67c60-155">Next steps</span></span>

<span data-ttu-id="67c60-156">Per istruzioni sul download di file dall'account di archiviazione di azure, consultare troppo[Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="67c60-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="67c60-157">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="67c60-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="67c60-158">Ulteriori informazioni su soluzioni di archiviazione sono reperibile qui in hello seguente collegamento: [Esplora archivi](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="67c60-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="67c60-159">Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="67c60-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













