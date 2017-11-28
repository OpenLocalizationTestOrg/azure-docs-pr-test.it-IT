---
title: acquisizioni di pacchetti aaaManage con Watcher di rete di Azure - CLI di Azure 2.0 | Documenti Microsoft
description: "Questa pagina viene illustrato come toomanage hello funzionalità di acquisizione di pacchetti di controllo di rete mediante Azure CLI 2.0"
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
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="cdeca-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="cdeca-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="cdeca-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cdeca-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="cdeca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdeca-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="cdeca-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="cdeca-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="cdeca-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="cdeca-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="cdeca-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="cdeca-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="cdeca-109">Acquisizione di pacchetti di rete Watcher consente tooand toocreate acquisizione sessioni tootrack traffico da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cdeca-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="cdeca-110">I filtri vengono forniti per hello acquisizione sessione tooensure che si acquisisce solo il traffico hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="cdeca-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="cdeca-111">Acquisizione di pacchetti consente toodiagnose anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="cdeca-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="cdeca-112">Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="cdeca-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="cdeca-113">Essendo in grado di tooremotely trigger pacchetto acquisizioni, questa funzionalità semplifica il carico di hello dell'esecuzione di acquisizione pacchetto eseguita manualmente e nel computer desiderato hello, che consente di risparmiare tempo prezioso.</span><span class="sxs-lookup"><span data-stu-id="cdeca-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="cdeca-114">In questo articolo utilizza la nuova generazione CLI per modello di distribuzione Gestione risorse hello, CLI di Azure 2.0, che è disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="cdeca-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="cdeca-115">hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="cdeca-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="cdeca-116">In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cdeca-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="cdeca-117">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="cdeca-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="cdeca-118">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="cdeca-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="cdeca-119">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="cdeca-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="cdeca-120">**Scaricare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="cdeca-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="cdeca-121">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="cdeca-121">Before you begin</span></span>

<span data-ttu-id="cdeca-122">Questo articolo si presuppone di che aver hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="cdeca-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="cdeca-123">Un'istanza del controllo di rete nell'area di hello desiderato toocreate un'acquisizione pacchetti</span><span class="sxs-lookup"><span data-stu-id="cdeca-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="cdeca-124">Una macchina virtuale con i pacchetti hello acquisire estensione abilitata.</span><span class="sxs-lookup"><span data-stu-id="cdeca-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdeca-125">Acquisizione pacchetto richiede toobe un agente in esecuzione nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="cdeca-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="cdeca-126">Hello agente viene installato come un'estensione.</span><span class="sxs-lookup"><span data-stu-id="cdeca-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="cdeca-127">Per informazioni sulle estensioni di VM, leggere l'articolo sulle [estensioni e funzionalità della macchina virtuale](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="cdeca-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="cdeca-128">Installare un'estensione di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="cdeca-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="cdeca-129">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="cdeca-129">Step 1</span></span>

<span data-ttu-id="cdeca-130">Eseguire hello `az vm extension set` agente cmdlet tooinstall hello pacchetto acquisizione sulla macchina virtuale guest di hello.</span><span class="sxs-lookup"><span data-stu-id="cdeca-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="cdeca-131">Per le macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="cdeca-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="cdeca-132">Per le macchine virtuali Linux:</span><span class="sxs-lookup"><span data-stu-id="cdeca-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="cdeca-133">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="cdeca-133">Step 2</span></span>

<span data-ttu-id="cdeca-134">tooensure che hello agente è installato, eseguire hello `vm extension get` cmdlet e passarlo a gruppo di risorse hello e nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cdeca-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="cdeca-135">Controllare hello risultante elenco tooensure hello agente è installato.</span><span class="sxs-lookup"><span data-stu-id="cdeca-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="cdeca-136">Hello di esempio seguente è riportato un esempio di risposta hello esecuzione`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="cdeca-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="cdeca-137">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cdeca-137">Start a packet capture</span></span>

<span data-ttu-id="cdeca-138">Una volta hello passaggi precedenti, agente di acquisizione di pacchetti hello è installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="cdeca-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="cdeca-139">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="cdeca-139">Step 1</span></span>

<span data-ttu-id="cdeca-140">passaggio successivo Hello è istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="cdeca-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="cdeca-141">Il nome TImpossibile di hello Watcher di rete viene passato toohello `az network watcher show` cmdlet nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="cdeca-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="cdeca-142">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="cdeca-142">Step 2</span></span>

<span data-ttu-id="cdeca-143">Recuperare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cdeca-143">Retrieve a storage account.</span></span> <span data-ttu-id="cdeca-144">Questo account di archiviazione è file di acquisizione di pacchetti hello toostore utilizzato.</span><span class="sxs-lookup"><span data-stu-id="cdeca-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="cdeca-145">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="cdeca-145">Step 3</span></span>

<span data-ttu-id="cdeca-146">I filtri possono essere utilizzati toolimit hello i dati archiviati dall'acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="cdeca-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="cdeca-147">Hello questo esempio viene impostata un'acquisizione pacchetto con diversi filtri.</span><span class="sxs-lookup"><span data-stu-id="cdeca-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="cdeca-148">Hello innanzitutto tre filtri raccolgono il traffico TCP in uscita solo da indirizzo IP locale 10.0.0.3 toodestination porte 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="cdeca-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="cdeca-149">ultimo filtro Hello raccoglie solo il traffico UDP.</span><span class="sxs-lookup"><span data-stu-id="cdeca-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="cdeca-150">esempio Hello è output di hello prevista dell'esecuzione hello `az network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cdeca-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="cdeca-151">Ottenere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cdeca-151">Get a packet capture</span></span>

<span data-ttu-id="cdeca-152">Esecuzione hello `az network watcher packet-capture show` cmdlet recupera informazioni sullo stato hello di un'acquisizione di pacchetti attualmente in esecuzione o è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cdeca-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="cdeca-153">esempio Hello è output hello hello `az network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cdeca-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="cdeca-154">Hello seguito è riportata al termine dell'acquisizione hello.</span><span class="sxs-lookup"><span data-stu-id="cdeca-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="cdeca-155">valore PacketCaptureStatus Hello viene arrestato, con un StopReason di TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="cdeca-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="cdeca-156">Questo valore indica che acquisizione pacchetti hello ha avuto esito positivo e il tempo di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cdeca-156">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="cdeca-157">Interrompere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cdeca-157">Stop a packet capture</span></span>

<span data-ttu-id="cdeca-158">Eseguendo hello `az network watcher packet-capture stop` cmdlet, se una sessione di acquisizione è in corso viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="cdeca-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="cdeca-159">cmdlet di Hello non restituisce alcuna risposta quando è stato eseguito in una sessione di acquisizione attualmente in esecuzione o di una sessione esistente che è già stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="cdeca-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="cdeca-160">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cdeca-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="cdeca-161">L'eliminazione di un'acquisizione di pacchetti non elimina il file hello nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="cdeca-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="cdeca-162">Scaricare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cdeca-162">Download a packet capture</span></span>

<span data-ttu-id="cdeca-163">Una volta completata la sessione di acquisizione di pacchetti, hello acquisizione file può essere caricato tooblob tooa o archiviazione locale nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="cdeca-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="cdeca-164">percorso di archiviazione Hello dell'acquisizione di pacchetti hello è definito al momento della creazione della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="cdeca-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="cdeca-165">Tooaccess un utile strumento questi file di acquisizione di account di archiviazione tooa salvato è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="cdeca-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="cdeca-166">Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="cdeca-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="cdeca-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cdeca-167">Next steps</span></span>

<span data-ttu-id="cdeca-168">Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="cdeca-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="cdeca-169">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="cdeca-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
