---
title: acquisizioni di pacchetti aaaManage con Watcher di rete di Azure - portale di Azure | Documenti Microsoft
description: "Questa pagina viene illustrato come toomanage hello funzionalità di acquisizione di pacchetti di controllo di rete tramite il portale di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="5c303-103">Gestire le acquisizioni di pacchetti con Watcher di rete di Azure tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="5c303-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5c303-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5c303-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="5c303-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c303-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="5c303-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="5c303-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="5c303-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="5c303-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="5c303-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="5c303-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="5c303-109">Acquisizione di pacchetti di rete Watcher consente tooand toocreate acquisizione sessioni tootrack traffico da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c303-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="5c303-110">I filtri vengono forniti per hello acquisizione sessione tooensure che si acquisisce solo il traffico hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="5c303-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="5c303-111">Acquisizione di pacchetti consente toodiagnose anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="5c303-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="5c303-112">Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="5c303-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="5c303-113">Essendo in grado di tooremotely trigger pacchetto acquisizioni, questa funzionalità semplifica il carico di hello dell'esecuzione di acquisizione pacchetto eseguita manualmente e nel computer desiderato hello, che consente di risparmiare tempo prezioso.</span><span class="sxs-lookup"><span data-stu-id="5c303-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="5c303-114">In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5c303-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="5c303-115">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="5c303-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="5c303-116">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="5c303-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="5c303-117">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="5c303-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="5c303-118">**Scaricare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="5c303-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="5c303-119">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5c303-119">Before you begin</span></span>

<span data-ttu-id="5c303-120">Questo articolo si presuppone di aver hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="5c303-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="5c303-121">Un'istanza del controllo di rete nell'area di hello desiderato toocreate un'acquisizione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5c303-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="5c303-122">Una macchina virtuale con i pacchetti hello acquisire estensione abilitata.</span><span class="sxs-lookup"><span data-stu-id="5c303-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c303-123">L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="5c303-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="5c303-124">Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="5c303-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="5c303-125">Estensione tramite il portale di hello agente acquisizione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5c303-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="5c303-126">acquisizione di pacchetti hello tooinstall agente della macchina virtuale tramite il portale di hello, passare una macchina virtuale tooyour, fare clic su **estensioni** > **Aggiungi** e cercare **rete Watcher agente per Windows**</span><span class="sxs-lookup"><span data-stu-id="5c303-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Visualizzazione agente][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="5c303-128">Panoramica dell'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="5c303-128">Packet Capture overview</span></span>

<span data-ttu-id="5c303-129">Passare toohello [portale di Azure](https://portal.azure.com) e fare clic su **rete** > **Watcher di rete** > **acquisizione pacchetti**</span><span class="sxs-lookup"><span data-stu-id="5c303-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="5c303-130">pagina di panoramica Hello mostra che un elenco di tutti i pacchetti acquisisce che esistono indipendentemente dal stato hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="5c303-131">Acquisizione pacchetto richiede account di archiviazione di connettività toohello sulla porta 443.</span><span class="sxs-lookup"><span data-stu-id="5c303-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![Schermata della panoramica di acquisizione di pacchetti][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="5c303-133">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="5c303-133">Start a packet capture</span></span>

<span data-ttu-id="5c303-134">Fare clic su **Aggiungi** toocreate un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5c303-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="5c303-135">sono proprietà Hello che può essere definita in un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5c303-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="5c303-136">**Impostazioni principali**</span><span class="sxs-lookup"><span data-stu-id="5c303-136">**Main settings**</span></span>

- <span data-ttu-id="5c303-137">**Sottoscrizione** -questo valore è una sottoscrizione di hello utilizzato, è necessaria un'istanza del controllo di rete in ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5c303-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="5c303-138">**Gruppo di risorse** -gruppo di risorse hello della macchina virtuale hello cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="5c303-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="5c303-139">**Macchina virtuale di destinazione** -macchina virtuale hello che esegue l'acquisizione di pacchetti hello</span><span class="sxs-lookup"><span data-stu-id="5c303-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="5c303-140">**Nome dell'acquisizione pacchetto** -questo valore è il nome di hello dell'acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="5c303-141">**Acquisisci configurazione**</span><span class="sxs-lookup"><span data-stu-id="5c303-141">**Capture configuration**</span></span>

- <span data-ttu-id="5c303-142">**Account di archiviazione**: determina se l'acquisizione di pacchetti viene salvata in un'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5c303-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="5c303-143">**File** -determina se un'acquisizione pacchetto viene salvata in locale nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="5c303-144">**Gli account di archiviazione** -hello selezionato acquisizione pacchetto nell'archiviazione account toosave hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="5c303-145">Il percorso predefinito è https://{nome account di archiviazione}.blob.core.windows.net/network-watcher-logs/subscriptions/{ID sottoscrizione}/resourcegroups/{nome gruppo di risorse}/providers/microsoft.compute/virtualmachines/{nome macchina virtuale}/{AA}/{MM}/{GG}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span><span class="sxs-lookup"><span data-stu-id="5c303-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="5c303-146">È abilitato solo se viene selezionato **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="5c303-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="5c303-147">**Percorso del file locale** -percorso locale di hello su un'acquisizione di pacchetti hello toosave macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c303-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="5c303-148">È abilitato solo se viene selezionato **File**.</span><span class="sxs-lookup"><span data-stu-id="5c303-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="5c303-149">È necessario specificare un percorso valido</span><span class="sxs-lookup"><span data-stu-id="5c303-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="5c303-150">**Numero massimo di byte per ogni pacchetto** -hello numero di byte da ogni pacchetto che vengono acquisiti, vengono acquisiti tutti i byte se lasciato vuoto.</span><span class="sxs-lookup"><span data-stu-id="5c303-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="5c303-151">**Numero massimo di byte per ogni sessione** - totale numero di byte che vengono acquisiti, una volta raggiunto il valore di hello arresta acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="5c303-152">**Il limite di tempo (secondi)** -imposta un limite di tempo per toostop di acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="5c303-153">Il valore predefinito è 18000 secondi.</span><span class="sxs-lookup"><span data-stu-id="5c303-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="5c303-154">Gli account di archiviazione Premium non sono attualmente supportati per l'archiviazione delle acquisizioni di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5c303-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="5c303-155">**Filtro (facoltativo)**</span><span class="sxs-lookup"><span data-stu-id="5c303-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="5c303-156">**Protocollo** -hello toofilter di protocollo per l'acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="5c303-157">i valori disponibili Hello sono TCP, UDP e qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="5c303-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="5c303-158">**L'indirizzo IP locale** -questo valore consente di filtrare toopackets acquisizione di pacchetti hello in cui l'indirizzo IP locale hello corrisponde a questo valore di filtro.</span><span class="sxs-lookup"><span data-stu-id="5c303-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="5c303-159">**Porta locale** -questo valore consente di filtrare toopackets acquisizione di pacchetti hello in cui la porta locale hello corrisponde a questo valore di filtro.</span><span class="sxs-lookup"><span data-stu-id="5c303-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="5c303-160">**Indirizzo IP remoto** -questo valore consente di filtrare toopackets acquisizione di pacchetti hello in IP remoti hello corrisponde a questo valore di filtro.</span><span class="sxs-lookup"><span data-stu-id="5c303-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="5c303-161">**Porta remota** -questo valore consente di filtrare toopackets acquisizione di pacchetti hello in cui la porta remota hello corrisponde a questo valore di filtro.</span><span class="sxs-lookup"><span data-stu-id="5c303-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="5c303-162">I valori di indirizzo IP e porta possono essere un valore singolo, un intervallo di valori o un set,</span><span class="sxs-lookup"><span data-stu-id="5c303-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="5c303-163">ovvero 80-1024 per la porta. È possibile definire tutti i filtri desiderati.</span><span class="sxs-lookup"><span data-stu-id="5c303-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="5c303-164">Una volta che vengono compilati i valori hello, fare clic su **OK** toocreate acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![Creare un'acquisizione di pacchetti][2]

<span data-ttu-id="5c303-166">Dopo aver impostato il limite di tempo hello in acquisizione pacchetti hello è scaduto, acquisizione pacchetti hello verrà interrotta e può essere esaminati.</span><span class="sxs-lookup"><span data-stu-id="5c303-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="5c303-167">È possibile arrestare manualmente sessioni di acquisizioni di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="5c303-168">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="5c303-168">Delete a packet capture</span></span>

<span data-ttu-id="5c303-169">Nel pacchetto di hello acquisizione visualizzazione, fare clic su hello **menu di scelta rapida** (...) o fare clic destro e fare clic su **eliminare** acquisizione di pacchetti hello toostop</span><span class="sxs-lookup"><span data-stu-id="5c303-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![Eliminare un'acquisizione di pacchetti][3]

> [!NOTE]
> <span data-ttu-id="5c303-171">L'eliminazione di un'acquisizione di pacchetti non elimina il file hello nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="5c303-172">Verrà chiesto tooconfirm desiderato di acquisizione di pacchetti hello toodelete, fare clic su **Sì**</span><span class="sxs-lookup"><span data-stu-id="5c303-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![Conferma][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="5c303-174">Interrompere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="5c303-174">Stop a packet capture</span></span>

<span data-ttu-id="5c303-175">Nel pacchetto di hello acquisizione visualizzazione, fare clic su hello **menu di scelta rapida** (...) o fare clic destro e fare clic su **arrestare** acquisizione di pacchetti hello toostop</span><span class="sxs-lookup"><span data-stu-id="5c303-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="5c303-176">Scaricare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="5c303-176">Download a packet capture</span></span>

<span data-ttu-id="5c303-177">Una volta completata la sessione di acquisizione di pacchetti, file di acquisizione hello è caricato tooblob tooa o archiviazione locale file hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5c303-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="5c303-178">percorso di archiviazione Hello dell'acquisizione di pacchetti hello è definito al momento della creazione della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="5c303-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="5c303-179">Tooaccess un utile strumento questi file di acquisizione di account di archiviazione tooa salvato è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="5c303-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="5c303-180">Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="5c303-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="5c303-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c303-181">Next steps</span></span>

<span data-ttu-id="5c303-182">Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="5c303-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="5c303-183">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="5c303-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













