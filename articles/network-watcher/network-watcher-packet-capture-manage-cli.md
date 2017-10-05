---
title: Gestire le acquisizioni di pacchetti con Azure Network Watcher - Interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: "Questa pagina illustra come gestire la funzionalità di acquisizione di pacchetti di Network Watcher usando l'interfaccia della riga di comando di Azure 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c94eb46f31f2f19b843ccd7bf77b8a39943a07d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="03698-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="03698-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="03698-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="03698-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="03698-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="03698-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="03698-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="03698-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="03698-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="03698-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="03698-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="03698-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="03698-109">Il servizio di acquisizione di pacchetti di Network Watcher consente di creare sessioni di acquisizione per registrare il traffico da e verso una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="03698-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="03698-110">Sono disponibili filtri per la sessione di acquisizione per garantire che venga acquisito solo il traffico desiderato.</span><span class="sxs-lookup"><span data-stu-id="03698-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="03698-111">Il servizio di acquisizione di pacchetti consente di individuare eventuali anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="03698-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="03698-112">Altri utilizzi comprendono la raccolta di statistiche di rete, informazioni sulle intrusioni nella rete, debug delle comunicazioni client-server e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="03698-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="03698-113">La possibilità di attivare da remoto l'acquisizione di pacchetti evita di dover eseguire manualmente questa operazione sul computer desiderato, consentendo un notevole risparmio di tempo.</span><span class="sxs-lookup"><span data-stu-id="03698-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="03698-114">Questo articolo usa l'interfaccia della riga di comando di nuova generazione per il modello di distribuzione di gestione delle risorse, ovvero l'interfaccia della riga di comando di Azure 2.0, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="03698-114">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="03698-115">Per eseguire i passaggi indicati in questo articolo è necessario [installare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (interfaccia della riga di comando di Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="03698-115">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="03698-116">Questo articolo illustra le diverse attività di gestione attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="03698-116">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="03698-117">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="03698-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="03698-118">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="03698-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="03698-119">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="03698-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="03698-120">**Scaricare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="03698-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="03698-121">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="03698-121">Before you begin</span></span>

<span data-ttu-id="03698-122">Questo articolo presuppone che l'utente disponga delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="03698-122">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="03698-123">Un'istanza di Network Watcher nell'area in cui creare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="03698-123">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="03698-124">Una macchina virtuale con l'estensione di acquisizione di pacchetti abilitata.</span><span class="sxs-lookup"><span data-stu-id="03698-124">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03698-125">L'acquisizione di pacchetti richiede un agente in esecuzione nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="03698-125">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="03698-126">L'agente viene installato come estensione.</span><span class="sxs-lookup"><span data-stu-id="03698-126">The Agent is installed as an extension.</span></span> <span data-ttu-id="03698-127">Per informazioni sulle estensioni di VM, leggere l'articolo sulle [estensioni e funzionalità della macchina virtuale](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="03698-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="03698-128">Installare un'estensione di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="03698-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="03698-129">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="03698-129">Step 1</span></span>

<span data-ttu-id="03698-130">Eseguire il cmdlet `az vm extension set` per installare l'agente di acquisizione di pacchetti sulla macchina virtuale guest.</span><span class="sxs-lookup"><span data-stu-id="03698-130">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="03698-131">Per le macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="03698-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="03698-132">Per le macchine virtuali Linux:</span><span class="sxs-lookup"><span data-stu-id="03698-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="03698-133">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="03698-133">Step 2</span></span>

<span data-ttu-id="03698-134">Per verificare che l'agente sia stato installato, eseguire il cmdlet `vm extension get` e passare il gruppo di risorse e il nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="03698-134">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="03698-135">Controllare l'elenco risultante per verificare l'installazione dell'agente.</span><span class="sxs-lookup"><span data-stu-id="03698-135">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="03698-136">L'esempio seguente riporta una possibile risposta all'esecuzione di `az vm extension show`.</span><span class="sxs-lookup"><span data-stu-id="03698-136">The following sample is an example of the response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="03698-137">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="03698-137">Start a packet capture</span></span>

<span data-ttu-id="03698-138">Dopo aver completato i passaggi precedenti, l'agente di acquisizione di pacchetti è installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="03698-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="03698-139">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="03698-139">Step 1</span></span>

<span data-ttu-id="03698-140">Il passaggio successivo consente di recuperare l'istanza di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="03698-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="03698-141">Il nome dell'istanza di Network Watcher viene passato al cmdlet `az network watcher show` nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="03698-141">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="03698-142">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="03698-142">Step 2</span></span>

<span data-ttu-id="03698-143">Recuperare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="03698-143">Retrieve a storage account.</span></span> <span data-ttu-id="03698-144">L'account di archiviazione viene usato per archiviare il file di acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="03698-144">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="03698-145">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="03698-145">Step 3</span></span>

<span data-ttu-id="03698-146">È possibile usare i filtri per limitare i dati archiviati dall'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="03698-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="03698-147">L'esempio seguente imposta un'acquisizione di pacchetto con diversi filtri.</span><span class="sxs-lookup"><span data-stu-id="03698-147">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="03698-148">I primi tre filtri acquisiscono il traffico TCP in uscita solo dall'indirizzo IP 10.0.0.3 verso le porte di destinazione 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="03698-148">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="03698-149">L'ultimo filtro acquisisce solo il traffico UDP.</span><span class="sxs-lookup"><span data-stu-id="03698-149">The last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="03698-150">L'esempio seguente riporta l'output previsto dall'esecuzione del cmdlet `az network watcher packet-capture create`.</span><span class="sxs-lookup"><span data-stu-id="03698-150">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="03698-151">Ottenere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="03698-151">Get a packet capture</span></span>

<span data-ttu-id="03698-152">L'esecuzione del cmdlet `az network watcher packet-capture show` consente di recuperare lo stato di un'acquisizione di pacchetti attualmente in esecuzione o completata.</span><span class="sxs-lookup"><span data-stu-id="03698-152">Running the `az network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="03698-153">L'esempio seguente riporta l'output ottenuto dall'esecuzione del cmdlet `az network watcher packet-capture show`.</span><span class="sxs-lookup"><span data-stu-id="03698-153">The following example is the output from the `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="03698-154">L'esempio seguente mostra il risultato ottenuto al completamento dell'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="03698-154">The following example is after the capture is complete.</span></span> <span data-ttu-id="03698-155">Il valore PacketCaptureStatus è Stopped, mentre il valore StopReason corrisponde a TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="03698-155">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="03698-156">Questo valore indica che l'acquisizione di pacchetti ha avuto esito positivo ed è stata eseguita per il tempo necessario.</span><span class="sxs-lookup"><span data-stu-id="03698-156">This value shows that the packet capture was successful and ran its time.</span></span>

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="03698-157">Interrompere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="03698-157">Stop a packet capture</span></span>

<span data-ttu-id="03698-158">L'esecuzione del cmdlet `az network watcher packet-capture stop` consente di interrompere un'acquisizione di pacchetti in corso.</span><span class="sxs-lookup"><span data-stu-id="03698-158">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="03698-159">Il cmdlet non restituisce alcuna risposta se eseguito in una sessione di acquisizione in corso o in una sessione esistente che è già stata interrotta.</span><span class="sxs-lookup"><span data-stu-id="03698-159">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="03698-160">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="03698-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="03698-161">L'eliminazione di un'acquisizione di pacchetti non elimina il file nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="03698-161">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="03698-162">Scaricare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="03698-162">Download a packet capture</span></span>

<span data-ttu-id="03698-163">Dopo aver completato la sessione di acquisizione di pacchetti, è possibile scaricare il file di acquisizione nell'archiviazione BLOB o in un file locale nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="03698-163">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="03698-164">La posizione di archiviazione dell'acquisizione di pacchetti viene definita al momento della creazione della sessione.</span><span class="sxs-lookup"><span data-stu-id="03698-164">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="03698-165">Uno strumento utile per accedere ai file di acquisizione salvati in un account di archiviazione è Esplora archivi di Microsoft Azure, disponibile qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="03698-165">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="03698-166">Se viene specificato un account di archiviazione, i file di acquisizione di pacchetti vengono salvati in un account di archiviazione nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="03698-166">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="03698-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03698-167">Next steps</span></span>

<span data-ttu-id="03698-168">Per altre informazioni su come automatizzare le acquisizioni di pacchetti tramite gli avvisi della macchina virtuale, leggere l'articolo su come [creare un'acquisizione di pacchetti attivata da un avviso](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="03698-168">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="03698-169">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="03698-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
