---
title: 'Gestire le acquisizioni di pacchetti con Azure Network Watcher: portale di Azure | Microsoft Docs'
description: "Questa pagina illustra come gestire la funzionalità di acquisizione di pacchetti di Network Watcher usando il portale di Azure"
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
ms.openlocfilehash: 33390532cc4fc1129a4f960d589f41bc95e5a1ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-the-portal"></a><span data-ttu-id="21a9a-103">Gestire le acquisizioni di pacchetti con Azure Network Watcher usando il portale</span><span class="sxs-lookup"><span data-stu-id="21a9a-103">Manage packet captures with Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="21a9a-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="21a9a-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="21a9a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21a9a-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="21a9a-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="21a9a-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="21a9a-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="21a9a-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="21a9a-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="21a9a-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="21a9a-109">Il servizio di acquisizione di pacchetti di Network Watcher consente di creare sessioni di acquisizione per registrare il traffico da e verso una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="21a9a-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="21a9a-110">Sono disponibili filtri per la sessione di acquisizione per garantire che venga acquisito solo il traffico desiderato.</span><span class="sxs-lookup"><span data-stu-id="21a9a-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="21a9a-111">Il servizio di acquisizione di pacchetti consente di individuare eventuali anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="21a9a-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="21a9a-112">Altri utilizzi comprendono la raccolta di statistiche di rete, informazioni sulle intrusioni nella rete, debug delle comunicazioni client-server e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="21a9a-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="21a9a-113">La possibilità di attivare da remoto l'acquisizione di pacchetti evita di dover eseguire manualmente questa operazione sul computer desiderato, consentendo un notevole risparmio di tempo.</span><span class="sxs-lookup"><span data-stu-id="21a9a-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="21a9a-114">Questo articolo illustra le diverse attività di gestione attualmente disponibili per l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="21a9a-115">**Avviare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="21a9a-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="21a9a-116">**Interrompere un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="21a9a-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="21a9a-117">**Eliminare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="21a9a-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="21a9a-118">**Scaricare un'acquisizione di pacchetti**</span><span class="sxs-lookup"><span data-stu-id="21a9a-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="21a9a-119">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="21a9a-119">Before you begin</span></span>

<span data-ttu-id="21a9a-120">Questo articolo presuppone che l'utente disponga delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="21a9a-120">This article assumes that you have the following resources:</span></span>

- <span data-ttu-id="21a9a-121">Un'istanza di Network Watcher nell'area in cui creare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="21a9a-122">Una macchina virtuale con l'estensione di acquisizione di pacchetti abilitata.</span><span class="sxs-lookup"><span data-stu-id="21a9a-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21a9a-123">L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="21a9a-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="21a9a-124">Per installare l'estensione in una VM Windows, vedere [Estensione macchina virtuale agente Azure Network Watcher per Windows](../virtual-machines/windows/extensions-nwa.md) e per una VM Linux VM vedere [Estensione macchina virtuale Azure Network Watcher Agent per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="21a9a-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-the-portal"></a><span data-ttu-id="21a9a-125">Estensione agente di acquisizione di pacchetti tramite il portale</span><span class="sxs-lookup"><span data-stu-id="21a9a-125">Packet Capture agent extension through the portal</span></span>

<span data-ttu-id="21a9a-126">Per installare l'agente di VM per l'acquisizione di pacchetti tramite il portale, andare alla macchina virtuale, fare clic su **Estensioni** > **Aggiungi** e cercare **Network Watcher Agent for Windows** (Agente Network Watcher per Windows)</span><span class="sxs-lookup"><span data-stu-id="21a9a-126">To install the packet capture VM agent through the portal, navigate to your virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Visualizzazione agente][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="21a9a-128">Panoramica dell'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="21a9a-128">Packet Capture overview</span></span>

<span data-ttu-id="21a9a-129">Andare al [portale di Azure](https://portal.azure.com) e fare clic su **Rete** > **Network Watcher** > **Acquisizione pacchetti**</span><span class="sxs-lookup"><span data-stu-id="21a9a-129">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="21a9a-130">La pagina della panoramica visualizza un elenco di tutte le acquisizioni di pacchetti esistenti indipendentemente dallo stato.</span><span class="sxs-lookup"><span data-stu-id="21a9a-130">The overview page shows a list of all packet captures that exist no matter the state.</span></span>

> [!NOTE]
> <span data-ttu-id="21a9a-131">L'acquisizione di pacchetti richiede la connettività all'account di archiviazione tramite la porta 443.</span><span class="sxs-lookup"><span data-stu-id="21a9a-131">Packet capture requires connectivity to the storage account over port 443.</span></span>

![Schermata della panoramica di acquisizione di pacchetti][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="21a9a-133">Avviare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="21a9a-133">Start a packet capture</span></span>

<span data-ttu-id="21a9a-134">Fare clic su **Aggiungi** per creare un'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-134">Click **Add** to create a packet capture.</span></span>

<span data-ttu-id="21a9a-135">Le proprietà che possono essere definite in un'acquisizione di pacchetti sono:</span><span class="sxs-lookup"><span data-stu-id="21a9a-135">The properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="21a9a-136">**Impostazioni principali**</span><span class="sxs-lookup"><span data-stu-id="21a9a-136">**Main settings**</span></span>

- <span data-ttu-id="21a9a-137">**Sottoscrizione**: questo valore è la sottoscrizione usata. Un'istanza di Network Watcher è necessaria in ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="21a9a-137">**Subscription** - This value is the subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="21a9a-138">**Gruppo di risorse**: gruppo di risorse della macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="21a9a-138">**Resource group** - The resource group of the virtual machine that is being targeted.</span></span>
- <span data-ttu-id="21a9a-139">**Macchina virtuale di destinazione**: macchina virtuale che esegue l'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="21a9a-139">**Target virtual machine** - The virtual machine that is running the packet capture</span></span>
- <span data-ttu-id="21a9a-140">**Nome acquisizione pacchetti**: questo valore è il nome dell'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-140">**Packet capture name** - This value is the name of the packet capture.</span></span>

<span data-ttu-id="21a9a-141">**Acquisisci configurazione**</span><span class="sxs-lookup"><span data-stu-id="21a9a-141">**Capture configuration**</span></span>

- <span data-ttu-id="21a9a-142">**Account di archiviazione**: determina se l'acquisizione di pacchetti viene salvata in un'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="21a9a-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="21a9a-143">**File**: determina se un'acquisizione di pacchetti viene salvata in locale nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="21a9a-143">**File** - Determines if a packet capture is saved locally on the virtual machine.</span></span>
- <span data-ttu-id="21a9a-144">**Account di archiviazione**: account di archiviazione selezionato in cui salvare l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-144">**Storage Accounts** - The selected storage account to save the packet capture in.</span></span> <span data-ttu-id="21a9a-145">Il percorso predefinito è https://{nome account di archiviazione}.blob.core.windows.net/network-watcher-logs/subscriptions/{ID sottoscrizione}/resourcegroups/{nome gruppo di risorse}/providers/microsoft.compute/virtualmachines/{nome macchina virtuale}/{AA}/{MM}/{GG}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span><span class="sxs-lookup"><span data-stu-id="21a9a-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="21a9a-146">È abilitato solo se viene selezionato **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="21a9a-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="21a9a-147">**Percorso file locale**: percorso locale in una macchina virtuale in cui salvare l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-147">**Local file path** - The local path on a virtual machine to save the packet capture.</span></span> <span data-ttu-id="21a9a-148">È abilitato solo se viene selezionato **File**.</span><span class="sxs-lookup"><span data-stu-id="21a9a-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="21a9a-149">È necessario specificare un percorso valido</span><span class="sxs-lookup"><span data-stu-id="21a9a-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="21a9a-150">**Numero massimo di byte per pacchetto**: numero di byte acquisiti da ogni pacchetto. Se lasciato vuoto, vengono acquisiti tutti i byte.</span><span class="sxs-lookup"><span data-stu-id="21a9a-150">**Maximum bytes per packet** - The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="21a9a-151">**Numero massimo di byte per sessione**: numero totale di byte acquisiti. Con il raggiungimento di questo valore l'acquisizione dei pacchetti si arresta.</span><span class="sxs-lookup"><span data-stu-id="21a9a-151">**Maximum bytes per session** - Total number of bytes that are captured, once the value is reached the packet capture stops.</span></span>
- <span data-ttu-id="21a9a-152">**Limite di tempo (secondi)**: imposta un limite di tempo per l'arresto dell'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-152">**Time limit (seconds)** - Sets a time limit for the packet capture to stop.</span></span> <span data-ttu-id="21a9a-153">Il valore predefinito è 18000 secondi.</span><span class="sxs-lookup"><span data-stu-id="21a9a-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="21a9a-154">Gli account di archiviazione Premium non sono attualmente supportati per l'archiviazione delle acquisizioni di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="21a9a-155">**Filtro (facoltativo)**</span><span class="sxs-lookup"><span data-stu-id="21a9a-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="21a9a-156">**Protocollo**: protocollo per filtrare l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-156">**Protocol** - The protocol to filter for the packet capture.</span></span> <span data-ttu-id="21a9a-157">I valori disponibili sono TCP, UDP e Qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="21a9a-157">The available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="21a9a-158">**Indirizzo IP locale**: questo valore filtra l'acquisizione di pacchetti per ottenere i pacchetti in cui l'indirizzo IP locale corrisponde a questo valore del filtro.</span><span class="sxs-lookup"><span data-stu-id="21a9a-158">**Local IP address** - This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>
- <span data-ttu-id="21a9a-159">**Porta locale**: questo valore filtra l'acquisizione di pacchetti per ottenere i pacchetti in cui la porta locale corrisponde a questo valore del filtro.</span><span class="sxs-lookup"><span data-stu-id="21a9a-159">**Local port** - This value filters the packet capture to packets where the local port matches this filter value.</span></span>
- <span data-ttu-id="21a9a-160">**Indirizzo IP remoto**: questo valore filtra l'acquisizione di pacchetti per ottenere i pacchetti in cui l'IP remoto corrisponde a questo valore del filtro.</span><span class="sxs-lookup"><span data-stu-id="21a9a-160">**Remote IP address** - This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>
- <span data-ttu-id="21a9a-161">**Porta remota**: questo valore filtra l'acquisizione di pacchetti per ottenere i pacchetti in cui la porta remota corrisponde a questo valore del filtro.</span><span class="sxs-lookup"><span data-stu-id="21a9a-161">**Remote port** - This value filters the packet capture to packets where the remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="21a9a-162">I valori di indirizzo IP e porta possono essere un valore singolo, un intervallo di valori o un set,</span><span class="sxs-lookup"><span data-stu-id="21a9a-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="21a9a-163">ovvero 80-1024 per la porta. È possibile definire tutti i filtri desiderati.</span><span class="sxs-lookup"><span data-stu-id="21a9a-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="21a9a-164">Dopo che tutti i valori sono stati immessi, fare clic su **OK** per creare l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-164">Once the values are filled out, click **OK** to create the packet capture.</span></span>

![Creare un'acquisizione di pacchetti][2]

<span data-ttu-id="21a9a-166">Alla scadenza del limite di tempo impostato, l'acquisizione di pacchetti viene arrestata e può essere esaminata.</span><span class="sxs-lookup"><span data-stu-id="21a9a-166">After the time limit set on the packet capture has expired, the packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="21a9a-167">È anche possibile arrestare manualmente le sessioni delle acquisizioni di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21a9a-167">You can also manually stop the packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="21a9a-168">Eliminare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="21a9a-168">Delete a packet capture</span></span>

<span data-ttu-id="21a9a-169">Nella visualizzazione dell'acquisizione di pacchetti fare clic sul **menu contestuale** (...) o fare clic con il pulsante destro del mouse e scegliere **Elimina** per arrestare l'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="21a9a-169">In the packet capture view, click the **context menu** (...) or right click, and click **delete** to stop the packet capture</span></span>

![Eliminare un'acquisizione di pacchetti][3]

> [!NOTE]
> <span data-ttu-id="21a9a-171">L'eliminazione di un'acquisizione di pacchetti non elimina il file nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="21a9a-171">Deleting a packet capture does not delete the file in the storage account.</span></span>

<span data-ttu-id="21a9a-172">Viene chiesto di confermare se si vuole eliminare l'acquisizione del pacchetto. Fare clic su **Sì**</span><span class="sxs-lookup"><span data-stu-id="21a9a-172">You are asked to confirm you want to delete the packet capture, click **Yes**</span></span>

![Conferma][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="21a9a-174">Interrompere un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="21a9a-174">Stop a packet capture</span></span>

<span data-ttu-id="21a9a-175">Nella visualizzazione dell'acquisizione di pacchetti fare clic sul **menu contestuale** (...) o fare clic con il pulsante destro del mouse e scegliere **Arresta** per arrestare l'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="21a9a-175">In the packet capture view, click the **context menu** (...) or right click, and click **Stop** to stop the packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="21a9a-176">Scaricare un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="21a9a-176">Download a packet capture</span></span>

<span data-ttu-id="21a9a-177">Dopo aver completato la sessione di acquisizione di pacchetti, il file di acquisizione viene caricato nell'archivio BLOB o in un file locale nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="21a9a-177">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="21a9a-178">La posizione di archiviazione dell'acquisizione di pacchetti viene definita al momento della creazione della sessione.</span><span class="sxs-lookup"><span data-stu-id="21a9a-178">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="21a9a-179">Uno strumento utile per accedere ai file di acquisizione salvati in un account di archiviazione è Esplora archivi di Microsoft Azure, disponibile qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="21a9a-179">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="21a9a-180">Se viene specificato un account di archiviazione, i file di acquisizione di pacchetti vengono salvati in un account di archiviazione nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="21a9a-180">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="21a9a-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21a9a-181">Next steps</span></span>

<span data-ttu-id="21a9a-182">Per altre informazioni su come automatizzare le acquisizioni di pacchetti tramite gli avvisi della macchina virtuale, leggere l'articolo su come [creare un'acquisizione di pacchetti attivata da un avviso](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="21a9a-182">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="21a9a-183">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="21a9a-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













