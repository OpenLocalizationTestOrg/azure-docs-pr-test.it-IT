---
title: l'acquisizione tooPacket aaaIntroduction Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica della funzionalità di acquisizione dei pacchetti di hello Watcher di rete"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="ee539-103">Acquisizione di pacchetti toovariable introduzione in Watcher di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="ee539-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="ee539-104">Acquisizione pacchetto variabile Watcher di rete consente toocreate pacchetto acquisizione sessioni tootrack traffico tooand da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ee539-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="ee539-105">Acquisizione di pacchetti consente toodiagnose anomalie di rete sia reattivo e proactivity.</span><span class="sxs-lookup"><span data-stu-id="ee539-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="ee539-106">Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="ee539-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="ee539-107">L'acquisizione di pacchetti è un'estensione macchina virtuale che viene avviata da remoto tramite Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="ee539-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="ee539-108">Questa funzionalità semplifica il compito di hello di esecuzione manuale di acquisizione pacchetto eseguita nella macchina virtuale desiderata hello, che consente di risparmiare tempo prezioso.</span><span class="sxs-lookup"><span data-stu-id="ee539-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="ee539-109">Acquisizione pacchetto può essere attivato tramite il portale di hello, PowerShell, CLI o API REST.</span><span class="sxs-lookup"><span data-stu-id="ee539-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="ee539-110">Un esempio di modalità di attivazione è rappresentata dagli avvisi della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ee539-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="ee539-111">I filtri vengono forniti per tooensure sessione di acquisizione hello è acquisire il traffico si desidera toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ee539-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="ee539-112">I filtri si basano su informazioni a 5 tuple (protocollo, indirizzo IP locale, indirizzo IP remoto, porta locale e porta remota).</span><span class="sxs-lookup"><span data-stu-id="ee539-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="ee539-113">Hello acquisito vengono archiviati nel disco locale hello o un blob di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee539-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="ee539-114">È previsto un limite di 10 sessioni di acquisizione dei pacchetti per area per sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ee539-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="ee539-115">Questo limite si applica solo le sessioni toohello e non toohello salvato il file di acquisizione di pacchetti in hello VM locale o in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee539-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee539-116">L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="ee539-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="ee539-117">Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="ee539-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="ee539-118">informazioni di hello tooreduce di acquisire le informazioni di hello tooonly desiderato, hello le opzioni seguenti sono disponibile per una sessione di acquisizione di pacchetti:</span><span class="sxs-lookup"><span data-stu-id="ee539-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="ee539-119">**Acquisisci configurazione**</span><span class="sxs-lookup"><span data-stu-id="ee539-119">**Capture configuration**</span></span>

|<span data-ttu-id="ee539-120">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ee539-120">Property</span></span>|<span data-ttu-id="ee539-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ee539-121">Description</span></span>|
|---|---|
|<span data-ttu-id="ee539-122">**Numero massimo di byte per pacchetto (byte)**</span><span class="sxs-lookup"><span data-stu-id="ee539-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="ee539-123">Hello numero di byte da ogni pacchetto che vengono acquisiti, vengono acquisiti tutti i byte se lasciato vuoto.</span><span class="sxs-lookup"><span data-stu-id="ee539-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="ee539-124">Hello numero di byte da ogni pacchetto che vengono acquisiti, vengono acquisiti tutti i byte se lasciato vuoto.</span><span class="sxs-lookup"><span data-stu-id="ee539-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="ee539-125">Se è necessario solo intestazione IPv4 di hello: indicare 34 qui</span><span class="sxs-lookup"><span data-stu-id="ee539-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="ee539-126">**Numero massimo di byte per sessione (byte)**</span><span class="sxs-lookup"><span data-stu-id="ee539-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="ee539-127">Numero totale di byte in cui viene acquisito, una volta raggiunto il valore di hello hello sessione termina.</span><span class="sxs-lookup"><span data-stu-id="ee539-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="ee539-128">**Limite di tempo (secondi)**</span><span class="sxs-lookup"><span data-stu-id="ee539-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="ee539-129">Imposta un vincolo di tempo per i pacchetti hello sessione di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="ee539-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="ee539-130">valore predefinito di Hello è 18000 secondi o 5 ore.</span><span class="sxs-lookup"><span data-stu-id="ee539-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="ee539-131">**Filtro (facoltativo)**</span><span class="sxs-lookup"><span data-stu-id="ee539-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="ee539-132">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ee539-132">Property</span></span>|<span data-ttu-id="ee539-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ee539-133">Description</span></span>|
|---|---|
|<span data-ttu-id="ee539-134">**Protocollo**</span><span class="sxs-lookup"><span data-stu-id="ee539-134">**Protocol**</span></span> | <span data-ttu-id="ee539-135">acquisire Hello toofilter di protocollo per pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="ee539-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="ee539-136">i valori disponibili Hello sono TCP, UDP e tutti.</span><span class="sxs-lookup"><span data-stu-id="ee539-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="ee539-137">**Indirizzo IP locale**</span><span class="sxs-lookup"><span data-stu-id="ee539-137">**Local IP address**</span></span> | <span data-ttu-id="ee539-138">Questo valore consente di filtrare toopackets acquisizione di pacchetti hello in cui l'indirizzo IP locale hello corrisponde a questo valore di filtro.</span><span class="sxs-lookup"><span data-stu-id="ee539-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="ee539-139">**Porta locale**</span><span class="sxs-lookup"><span data-stu-id="ee539-139">**Local port**</span></span> | <span data-ttu-id="ee539-140">Questo valore filtri hello pacchetto acquisizione toopackets in cui la porta locale hello corrisponde a questo valore di filtro.</span><span class="sxs-lookup"><span data-stu-id="ee539-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="ee539-141">**Indirizzo IP remoto**</span><span class="sxs-lookup"><span data-stu-id="ee539-141">**Remote IP address**</span></span> | <span data-ttu-id="ee539-142">Questo valore filtri hello pacchetto acquisizione toopackets dove IP remoti hello corrisponde a questo valore di filtro.</span><span class="sxs-lookup"><span data-stu-id="ee539-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="ee539-143">**Porta remota**</span><span class="sxs-lookup"><span data-stu-id="ee539-143">**Remote port**</span></span> | <span data-ttu-id="ee539-144">Questo valore filtri hello pacchetto acquisizione toopackets in cui la porta remota hello corrisponde a questo valore di filtro.</span><span class="sxs-lookup"><span data-stu-id="ee539-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="ee539-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee539-145">Next steps</span></span>

<span data-ttu-id="ee539-146">Informazioni su come è possibile gestire le acquisizioni di pacchetti tramite il portale di hello visitando [gestire l'acquisizione di pacchetti nel portale di Azure hello](network-watcher-packet-capture-manage-portal.md) o con PowerShell visitando [gestire pacchetti acquisire con PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ee539-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="ee539-147">Informazioni su come pacchetto proattiva toocreate acquisisce in base agli avvisi di macchina virtuale, visitare il sito [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="ee539-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













