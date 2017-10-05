---
title: Gestire le acquisizioni di pacchetti con Azure Network Watcher - Interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: "Questa pagina illustra come gestire la funzionalità di acquisizione di pacchetti di Network Watcher usando l'interfaccia della riga di comando di Azure 1.0"
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
ms.openlocfilehash: 91588910334859c1ea77186674d5bfb31b311b36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="da25e-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="da25e-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="da25e-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="da25e-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="da25e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da25e-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="da25e-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="da25e-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="da25e-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="da25e-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="da25e-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="da25e-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="da25e-109">Il servizio di acquisizione di pacchetti di Network Watcher consente di creare sessioni di acquisizione per registrare il traffico da e verso una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="da25e-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="da25e-110">Sono disponibili filtri per la sessione di acquisizione per garantire che venga acquisito solo il traffico desiderato.</span><span class="sxs-lookup"><span data-stu-id="da25e-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="da25e-111">Il servizio di acquisizione di pacchetti consente di individuare eventuali anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="da25e-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="da25e-112">Altri utilizzi comprendono la raccolta di statistiche di rete, informazioni sulle intrusioni nella rete, debug delle comunicazioni client-server e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="da25e-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="da25e-113">La possibilità di attivare da remoto l'acquisizione di pacchetti evita di dover eseguire manualmente questa operazione sul computer desiderato, consentendo un notevole risparmio di tempo.</span><span class="sxs-lookup"><span data-stu-id="da25e-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="da25e-114">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="da25e-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="da25e-115">Questo articolo illustra le diverse attività di gestione attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="da25e-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="da25e-116">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="da25e-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="da25e-117">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="da25e-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="da25e-118">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="da25e-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="da25e-119">**Scaricare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="da25e-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="da25e-120">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="da25e-120">Before you begin</span></span>

<span data-ttu-id="da25e-121">Questo articolo presuppone che l'utente disponga delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="da25e-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="da25e-122">Un'istanza di Network Watcher nell'area in cui creare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="da25e-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="da25e-123">Una macchina virtuale con l'estensione di acquisizione di pacchetti abilitata.</span><span class="sxs-lookup"><span data-stu-id="da25e-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da25e-124">L'acquisizione di pacchetti richiede un agente in esecuzione nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="da25e-124">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="da25e-125">L'agente viene installato come estensione.</span><span class="sxs-lookup"><span data-stu-id="da25e-125">The Agent is installed as an extension.</span></span> <span data-ttu-id="da25e-126">Per informazioni sulle estensioni di VM, leggere l'articolo sulle [estensioni e funzionalità della macchina virtuale](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="da25e-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="da25e-127">Installare un'estensione di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="da25e-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="da25e-128">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="da25e-128">Step 1</span></span>

<span data-ttu-id="da25e-129">Eseguire il cmdlet `azure vm extension set` per installare l'agente di acquisizione di pacchetti sulla macchina virtuale guest.</span><span class="sxs-lookup"><span data-stu-id="da25e-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="da25e-130">Per le macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="da25e-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="da25e-131">Per le macchine virtuali Linux:</span><span class="sxs-lookup"><span data-stu-id="da25e-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="da25e-132">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="da25e-132">Step 2</span></span>

<span data-ttu-id="da25e-133">Per verificare che l'agente sia stato installato, eseguire il cmdlet `vm extension get` e passare il gruppo di risorse e il nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="da25e-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="da25e-134">Controllare l'elenco risultante per verificare l'installazione dell'agente.</span><span class="sxs-lookup"><span data-stu-id="da25e-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="da25e-135">L'esempio seguente riporta una possibile risposta all'esecuzione di `azure vm extension get`.</span><span class="sxs-lookup"><span data-stu-id="da25e-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="da25e-136">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="da25e-136">Start a packet capture</span></span>

<span data-ttu-id="da25e-137">Dopo aver completato i passaggi precedenti, l'agente di acquisizione di pacchetti è installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="da25e-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="da25e-138">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="da25e-138">Step 1</span></span>

<span data-ttu-id="da25e-139">Il passaggio successivo consente di recuperare l'istanza di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="da25e-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="da25e-140">Questa variabile viene passata al cmdlet `network watcher show` nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="da25e-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="da25e-141">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="da25e-141">Step 2</span></span>

<span data-ttu-id="da25e-142">Recuperare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="da25e-142">Retrieve a storage account.</span></span> <span data-ttu-id="da25e-143">L'account di archiviazione viene usato per archiviare il file di acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="da25e-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="da25e-144">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="da25e-144">Step 3</span></span>

<span data-ttu-id="da25e-145">È possibile usare i filtri per limitare i dati archiviati dall'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="da25e-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="da25e-146">L'esempio seguente imposta un'acquisizione di pacchetto con diversi filtri.</span><span class="sxs-lookup"><span data-stu-id="da25e-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="da25e-147">I primi tre filtri acquisiscono il traffico TCP in uscita solo dall'indirizzo IP 10.0.0.3 verso le porte di destinazione 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="da25e-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="da25e-148">L'ultimo filtro acquisisce solo il traffico UDP.</span><span class="sxs-lookup"><span data-stu-id="da25e-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="da25e-149">Per un'acquisizione di pacchetti è possibile definire più filtri.</span><span class="sxs-lookup"><span data-stu-id="da25e-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="da25e-150">Se si usa una struttura di filtro complessa, è preferibile usare i filtri come un file JSON, così da evitare errori di sintassi.</span><span class="sxs-lookup"><span data-stu-id="da25e-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="da25e-151">Usare ad esempio il flag "-r" (invece del flag "-f") e passare il percorso di un file JSON contenente i filtri seguenti:</span><span class="sxs-lookup"><span data-stu-id="da25e-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


<span data-ttu-id="da25e-152">L'esempio seguente riporta l'output previsto dall'esecuzione del cmdlet `network watcher packet-capture create`.</span><span class="sxs-lookup"><span data-stu-id="da25e-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="da25e-153">Ottenere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="da25e-153">Get a packet capture</span></span>

<span data-ttu-id="da25e-154">L'esecuzione del cmdlet `network watcher packet-capture show` consente di recuperare lo stato di un'acquisizione di pacchetti attualmente in esecuzione o completata.</span><span class="sxs-lookup"><span data-stu-id="da25e-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="da25e-155">L'esempio seguente riporta l'output ottenuto dall'esecuzione del cmdlet `network watcher packet-capture show`.</span><span class="sxs-lookup"><span data-stu-id="da25e-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="da25e-156">L'esempio seguente mostra il risultato ottenuto al completamento dell'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="da25e-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="da25e-157">Il valore PacketCaptureStatus è Stopped, mentre il valore StopReason corrisponde a TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="da25e-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="da25e-158">Questo valore indica che l'acquisizione di pacchetti ha avuto esito positivo ed è stata eseguita per il tempo necessario.</span><span class="sxs-lookup"><span data-stu-id="da25e-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="da25e-159">Interrompere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="da25e-159">Stop a packet capture</span></span>

<span data-ttu-id="da25e-160">L'esecuzione del cmdlet `network watcher packet-capture stop` consente di interrompere un'acquisizione di pacchetti in corso.</span><span class="sxs-lookup"><span data-stu-id="da25e-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="da25e-161">Il cmdlet non restituisce alcuna risposta se eseguito in una sessione di acquisizione in corso o in una sessione esistente che è già stata interrotta.</span><span class="sxs-lookup"><span data-stu-id="da25e-161">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="da25e-162">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="da25e-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="da25e-163">L'eliminazione di un'acquisizione di pacchetti non elimina il file nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="da25e-163">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="da25e-164">Scaricare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="da25e-164">Download a packet capture</span></span>

<span data-ttu-id="da25e-165">Dopo aver completato la sessione di acquisizione di pacchetti, è possibile scaricare il file di acquisizione nell'archiviazione BLOB o in un file locale nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="da25e-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="da25e-166">La posizione di archiviazione dell'acquisizione di pacchetti viene definita al momento della creazione della sessione.</span><span class="sxs-lookup"><span data-stu-id="da25e-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="da25e-167">Uno strumento utile per accedere ai file di acquisizione salvati in un account di archiviazione è Esplora archivi di Microsoft Azure, disponibile qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="da25e-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="da25e-168">Se viene specificato un account di archiviazione, i file di acquisizione di pacchetti vengono salvati in un account di archiviazione nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="da25e-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="da25e-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da25e-169">Next steps</span></span>

<span data-ttu-id="da25e-170">Per altre informazioni su come automatizzare le acquisizioni di pacchetti tramite gli avvisi della macchina virtuale, leggere l'articolo su come [creare un'acquisizione di pacchetti attivata da un avviso](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="da25e-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="da25e-171">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="da25e-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
