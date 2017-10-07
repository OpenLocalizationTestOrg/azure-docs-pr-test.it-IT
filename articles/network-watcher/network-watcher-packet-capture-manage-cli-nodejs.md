---
title: acquisizioni di pacchetti aaaManage con Watcher di rete di Azure - CLI di Azure 1.0 | Documenti Microsoft
description: "Questa pagina viene illustrato come toomanage hello funzionalità di acquisizione di pacchetti di controllo di rete mediante Azure CLI 1.0"
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
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="ce009-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ce009-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ce009-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ce009-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="ce009-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce009-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="ce009-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="ce009-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="ce009-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="ce009-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="ce009-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="ce009-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="ce009-109">Acquisizione di pacchetti di rete Watcher consente tooand toocreate acquisizione sessioni tootrack traffico da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ce009-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="ce009-110">I filtri vengono forniti per hello acquisizione sessione tooensure che si acquisisce solo il traffico hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="ce009-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="ce009-111">Acquisizione di pacchetti consente toodiagnose anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="ce009-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="ce009-112">Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="ce009-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="ce009-113">Essendo in grado di tooremotely trigger pacchetto acquisizioni, questa funzionalità semplifica il carico di hello dell'esecuzione di acquisizione pacchetto eseguita manualmente e nel computer desiderato hello, che consente di risparmiare tempo prezioso.</span><span class="sxs-lookup"><span data-stu-id="ce009-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="ce009-114">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="ce009-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="ce009-115">In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ce009-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="ce009-116">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="ce009-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="ce009-117">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="ce009-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="ce009-118">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="ce009-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="ce009-119">**Scaricare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="ce009-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="ce009-120">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ce009-120">Before you begin</span></span>

<span data-ttu-id="ce009-121">Questo articolo si presuppone di che aver hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="ce009-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="ce009-122">Un'istanza del controllo di rete nell'area di hello desiderato toocreate un'acquisizione pacchetti</span><span class="sxs-lookup"><span data-stu-id="ce009-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="ce009-123">Una macchina virtuale con i pacchetti hello acquisire estensione abilitata.</span><span class="sxs-lookup"><span data-stu-id="ce009-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce009-124">Acquisizione pacchetto richiede toobe un agente in esecuzione nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ce009-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="ce009-125">Hello agente viene installato come un'estensione.</span><span class="sxs-lookup"><span data-stu-id="ce009-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="ce009-126">Per informazioni sulle estensioni di VM, leggere l'articolo sulle [estensioni e funzionalità della macchina virtuale](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="ce009-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="ce009-127">Installare un'estensione di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ce009-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="ce009-128">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="ce009-128">Step 1</span></span>

<span data-ttu-id="ce009-129">Eseguire hello `azure vm extension set` agente cmdlet tooinstall hello pacchetto acquisizione sulla macchina virtuale guest di hello.</span><span class="sxs-lookup"><span data-stu-id="ce009-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="ce009-130">Per le macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="ce009-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="ce009-131">Per le macchine virtuali Linux:</span><span class="sxs-lookup"><span data-stu-id="ce009-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="ce009-132">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="ce009-132">Step 2</span></span>

<span data-ttu-id="ce009-133">tooensure che hello agente è installato, eseguire hello `vm extension get` cmdlet e passarlo a gruppo di risorse hello e nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ce009-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="ce009-134">Controllare hello risultante elenco tooensure hello agente è installato.</span><span class="sxs-lookup"><span data-stu-id="ce009-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="ce009-135">Hello di esempio seguente è riportato un esempio di risposta hello esecuzione`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="ce009-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="ce009-136">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ce009-136">Start a packet capture</span></span>

<span data-ttu-id="ce009-137">Una volta hello passaggi precedenti, agente di acquisizione di pacchetti hello è installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ce009-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="ce009-138">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="ce009-138">Step 1</span></span>

<span data-ttu-id="ce009-139">passaggio successivo Hello è istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="ce009-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="ce009-140">Questa variabile viene passata toohello `network watcher show` cmdlet nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="ce009-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="ce009-141">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="ce009-141">Step 2</span></span>

<span data-ttu-id="ce009-142">Recuperare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ce009-142">Retrieve a storage account.</span></span> <span data-ttu-id="ce009-143">Questo account di archiviazione è file di acquisizione di pacchetti hello toostore utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ce009-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="ce009-144">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="ce009-144">Step 3</span></span>

<span data-ttu-id="ce009-145">I filtri possono essere utilizzati toolimit hello i dati archiviati dall'acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="ce009-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="ce009-146">Hello questo esempio viene impostata un'acquisizione pacchetto con diversi filtri.</span><span class="sxs-lookup"><span data-stu-id="ce009-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="ce009-147">Hello innanzitutto tre filtri raccolgono il traffico TCP in uscita solo da indirizzo IP locale 10.0.0.3 toodestination porte 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="ce009-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="ce009-148">ultimo filtro Hello raccoglie solo il traffico UDP.</span><span class="sxs-lookup"><span data-stu-id="ce009-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="ce009-149">Per un'acquisizione di pacchetti è possibile definire più filtri.</span><span class="sxs-lookup"><span data-stu-id="ce009-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="ce009-150">Se si utilizza una struttura di filtro complesse, è meglio toouse filtri come un errori di sintassi tooavoid file json.</span><span class="sxs-lookup"><span data-stu-id="ce009-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="ce009-151">Ad esempio, utilizzare hello flag "-r" (invece di "-f") e passare il percorso di hello di un file json contenente hello seguenti filtri:</span><span class="sxs-lookup"><span data-stu-id="ce009-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

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


<span data-ttu-id="ce009-152">esempio Hello è output di hello prevista dell'esecuzione hello `network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ce009-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="ce009-153">Ottenere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ce009-153">Get a packet capture</span></span>

<span data-ttu-id="ce009-154">Esecuzione hello `network watcher packet-capture show` cmdlet recupera informazioni sullo stato hello di un'acquisizione di pacchetti attualmente in esecuzione o è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ce009-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="ce009-155">esempio Hello è output hello hello `network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ce009-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="ce009-156">Hello seguito è riportata al termine dell'acquisizione hello.</span><span class="sxs-lookup"><span data-stu-id="ce009-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="ce009-157">valore PacketCaptureStatus Hello viene arrestato, con un StopReason di TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="ce009-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="ce009-158">Questo valore indica che acquisizione pacchetti hello ha avuto esito positivo e il tempo di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ce009-158">This value shows that hello packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="ce009-159">Interrompere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ce009-159">Stop a packet capture</span></span>

<span data-ttu-id="ce009-160">Eseguendo hello `network watcher packet-capture stop` cmdlet, se una sessione di acquisizione è in corso viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="ce009-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="ce009-161">cmdlet di Hello non restituisce alcuna risposta quando è stato eseguito in una sessione di acquisizione attualmente in esecuzione o di una sessione esistente che è già stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="ce009-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="ce009-162">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ce009-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="ce009-163">L'eliminazione di un'acquisizione di pacchetti non elimina il file hello nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="ce009-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="ce009-164">Scaricare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ce009-164">Download a packet capture</span></span>

<span data-ttu-id="ce009-165">Una volta completata la sessione di acquisizione di pacchetti, hello acquisizione file può essere caricato tooblob tooa o archiviazione locale nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ce009-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="ce009-166">percorso di archiviazione Hello dell'acquisizione di pacchetti hello è definito al momento della creazione della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="ce009-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="ce009-167">Tooaccess un utile strumento questi file di acquisizione di account di archiviazione tooa salvato è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="ce009-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="ce009-168">Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="ce009-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="ce009-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ce009-169">Next steps</span></span>

<span data-ttu-id="ce009-170">Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="ce009-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="ce009-171">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="ce009-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
