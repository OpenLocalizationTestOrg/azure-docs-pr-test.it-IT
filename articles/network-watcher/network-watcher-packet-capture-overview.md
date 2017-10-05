---
title: Introduzione all'acquisizione di pacchetti in Azure Network Watcher | Documentazione Microsoft
description: "Questa pagina fornisce una panoramica delle funzionalità di acquisizione di pacchetti di Network Watcher"
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
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="21e48-103">Introduzione all'acquisizione di pacchetti di variabili in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="21e48-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="21e48-104">Il servizio di acquisizione di pacchetti di variabili di Network Watcher consente di creare sessioni di acquisizione di pacchetti per registrare il traffico da e verso una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="21e48-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="21e48-105">Il servizio di acquisizione di pacchetti consente di individuare eventuali anomalie di rete in modo proattivo e reattivo.</span><span class="sxs-lookup"><span data-stu-id="21e48-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="21e48-106">Altri usi comprendono la raccolta di statistiche di rete, informazioni sulle intrusioni nella rete, debug delle comunicazioni client-server e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="21e48-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="21e48-107">L'acquisizione di pacchetti è un'estensione macchina virtuale che viene avviata da remoto tramite Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="21e48-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="21e48-108">Questa funzionalità evita di dover eseguire manualmente questa operazione sulla macchina virtuale desiderata, consentendo un notevole risparmio di tempo.</span><span class="sxs-lookup"><span data-stu-id="21e48-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="21e48-109">L'acquisizione di pacchetti può essere attivata tramite il portale, PowerShell, l'interfaccia della riga di comando o l'API REST.</span><span class="sxs-lookup"><span data-stu-id="21e48-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="21e48-110">Un esempio di modalità di attivazione è rappresentata dagli avvisi della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="21e48-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="21e48-111">Sono disponibili filtri per la sessione di acquisizione per garantire che venga acquisito il traffico che si desidera monitorare.</span><span class="sxs-lookup"><span data-stu-id="21e48-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="21e48-112">I filtri si basano su informazioni a 5 tuple (protocollo, indirizzo IP locale, indirizzo IP remoto, porta locale e porta remota).</span><span class="sxs-lookup"><span data-stu-id="21e48-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="21e48-113">I dati acquisiti vengono archiviati nel disco locale o in un BLOB di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="21e48-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="21e48-114">È previsto un limite di 10 sessioni di acquisizione dei pacchetti per area per sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="21e48-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="21e48-115">Questo limite si applica solo alle sessioni e non si applica ai file di acquisizione di pacchetti salvati in locale nella VM o in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="21e48-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21e48-116">L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="21e48-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="21e48-117">Per installare l'estensione in una VM Windows, vedere [Estensione macchina virtuale agente Azure Network Watcher per Windows](../virtual-machines/windows/extensions-nwa.md) e per una VM Linux VM vedere [Estensione macchina virtuale Azure Network Watcher Agent per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="21e48-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="21e48-118">Per limitare le informazioni acquisite alle sole informazioni desiderate, sono disponibili le opzioni seguenti per una sessione di acquisizione di pacchetti:</span><span class="sxs-lookup"><span data-stu-id="21e48-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="21e48-119">**Acquisisci configurazione**</span><span class="sxs-lookup"><span data-stu-id="21e48-119">**Capture configuration**</span></span>

|<span data-ttu-id="21e48-120">Proprietà</span><span class="sxs-lookup"><span data-stu-id="21e48-120">Property</span></span>|<span data-ttu-id="21e48-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="21e48-121">Description</span></span>|
|---|---|
|<span data-ttu-id="21e48-122">**Numero massimo di byte per pacchetto (byte)**</span><span class="sxs-lookup"><span data-stu-id="21e48-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="21e48-123">Numero di byte acquisiti da ogni pacchetto. Se lasciato vuoto, vengono acquisiti tutti i byte.</span><span class="sxs-lookup"><span data-stu-id="21e48-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="21e48-124">Numero di byte acquisiti da ogni pacchetto. Se lasciato vuoto, vengono acquisiti tutti i byte.</span><span class="sxs-lookup"><span data-stu-id="21e48-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="21e48-125">Se è necessaria solo l'intestazione IPv4, indicare qui 34</span><span class="sxs-lookup"><span data-stu-id="21e48-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="21e48-126">**Numero massimo di byte per sessione (byte)**</span><span class="sxs-lookup"><span data-stu-id="21e48-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="21e48-127">Numero totale di byte acquisiti, quando viene raggiunto il valore di termine della sessione.</span><span class="sxs-lookup"><span data-stu-id="21e48-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="21e48-128">**Limite di tempo (secondi)**</span><span class="sxs-lookup"><span data-stu-id="21e48-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="21e48-129">Imposta un vincolo di tempo per la sessione di acquisizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="21e48-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="21e48-130">Il valore predefinito è 18000 secondi o 5 ore.</span><span class="sxs-lookup"><span data-stu-id="21e48-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="21e48-131">**Filtro (facoltativo)**</span><span class="sxs-lookup"><span data-stu-id="21e48-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="21e48-132">Proprietà</span><span class="sxs-lookup"><span data-stu-id="21e48-132">Property</span></span>|<span data-ttu-id="21e48-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="21e48-133">Description</span></span>|
|---|---|
|<span data-ttu-id="21e48-134">**Protocollo**</span><span class="sxs-lookup"><span data-stu-id="21e48-134">**Protocol**</span></span> | <span data-ttu-id="21e48-135">Protocollo per filtrare l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="21e48-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="21e48-136">I valori disponibili sono TCP, UDP e Tutti.</span><span class="sxs-lookup"><span data-stu-id="21e48-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="21e48-137">**Indirizzo IP locale**</span><span class="sxs-lookup"><span data-stu-id="21e48-137">**Local IP address**</span></span> | <span data-ttu-id="21e48-138">Questo valore filtra l'acquisizione di pacchetti per ottenere i pacchetti in cui l'indirizzo IP locale corrisponde a questo valore del filtro.</span><span class="sxs-lookup"><span data-stu-id="21e48-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="21e48-139">**Porta locale**</span><span class="sxs-lookup"><span data-stu-id="21e48-139">**Local port**</span></span> | <span data-ttu-id="21e48-140">Questo valore filtra l'acquisizione di pacchetti per ottenere i pacchetti in cui la porta locale corrisponde a questo valore del filtro.</span><span class="sxs-lookup"><span data-stu-id="21e48-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="21e48-141">**Indirizzo IP remoto**</span><span class="sxs-lookup"><span data-stu-id="21e48-141">**Remote IP address**</span></span> | <span data-ttu-id="21e48-142">Questo valore filtra l'acquisizione di pacchetti per ottenere i pacchetti in cui l'indirizzo IP remoto corrisponde a questo valore del filtro.</span><span class="sxs-lookup"><span data-stu-id="21e48-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="21e48-143">**Porta remota**</span><span class="sxs-lookup"><span data-stu-id="21e48-143">**Remote port**</span></span> | <span data-ttu-id="21e48-144">Questo valore filtra l'acquisizione di pacchetti per ottenere i pacchetti in cui la porta remota corrisponde a questo valore del filtro.</span><span class="sxs-lookup"><span data-stu-id="21e48-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="21e48-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21e48-145">Next steps</span></span>

<span data-ttu-id="21e48-146">Le informazioni su come gestire le acquisizioni di pacchetti tramite il portale sono disponibili in [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) (Gestire l'acquisizione di pacchetti nel portale di Azure) o con PowerShell in [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md) (Gestire l'acquisizione di pacchetti con PowerShell).</span><span class="sxs-lookup"><span data-stu-id="21e48-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="21e48-147">Le informazioni su come creare acquisizioni di pacchetti proattive tramite gli avvisi della macchina virtuale sono disponibili in [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md) (Creare un'acquisizione di pacchetti attivata da un avviso)</span><span class="sxs-lookup"><span data-stu-id="21e48-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













