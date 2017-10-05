---
title: Manutenzione con mantenimento per macchine virtuali Windows in Azure | Microsoft Docs
description: Migrazione di macchine virtuali sul posto per aggiornamenti con mantenimento della memoria.
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 8888bafbc3aba24168312b611a9b4fbde25f376d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a><span data-ttu-id="e8be3-103">Manutenzione con mantenimento delle macchine virtuali tramite la migrazione delle macchine virtuali sul posto</span><span class="sxs-lookup"><span data-stu-id="e8be3-103">VM preserving maintenance with In-place VM migration</span></span>

<span data-ttu-id="e8be3-104">Sebbene la maggior parte degli aggiornamenti non abbia alcun impatto sulle macchine virtuali ospitate, vi sono casi in cui gli aggiornamenti ai componenti o ai servizi hanno un'interferenza minima sulle macchine virtuali in esecuzione (senza un riavvio completo della macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="e8be3-104">While the majority of updates have no impact to hosted VMs, there are cases where updates to components or services result in minimal interference to running VMs (without a full reboot of the virtual machine).</span></span>

<span data-ttu-id="e8be3-105">Questi aggiornamenti vengono eseguiti con la tecnologia che consente la migrazione sul posto in tempo reale, anche detta "aggiornamento con mantenimento della memoria".</span><span class="sxs-lookup"><span data-stu-id="e8be3-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="e8be3-106">Durante l'aggiornamento dell'host, la macchina virtuale viene messa in pausa, mantenendo la memoria nella RAM, mentre l'ambiente host, ad esempio il sistema operativo sottostante, applica gli aggiornamenti e le patch necessari.</span><span class="sxs-lookup"><span data-stu-id="e8be3-106">When updating the host, the virtual machine is placed into a “paused” state, preserving the memory in RAM, while the hosting environment (e.g. the underlying operating system) applies the necessary updates and patches.</span></span>
<span data-ttu-id="e8be3-107">La macchina virtuale riprende poi l'esecuzione dopo un periodo di pausa di 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="e8be3-107">The virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="e8be3-108">Dopo la ripresa, l’orologio della macchina virtuale viene sincronizzato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e8be3-108">After resuming, the clock of the virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="e8be3-109">Non tutti gli aggiornamenti possono essere distribuiti utilizzando questo meccanismo, ma dato il breve periodo di pausa, la distribuzione degli aggiornamenti in questo modo riduce notevolmente l’impatto sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e8be3-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact to virtual machines.</span></span>

<span data-ttu-id="e8be3-110">Gli aggiornamenti a istanza multipla (le macchine virtuali sono in un set di disponibilità) vengono applicati su un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="e8be3-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="e8be3-111">Alcune applicazioni potrebbero essere interessate da questi aggiornamenti più di altre.</span><span class="sxs-lookup"><span data-stu-id="e8be3-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="e8be3-112">Le applicazioni che eseguono l'elaborazione di eventi in tempo reale, i flussi multimediali o la transcodifica oppure scenari con velocità effettiva di rete, ad esempio, possono non essere progettate per tollerare una pausa di 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="e8be3-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed to tolerate a 30 second pause.</span></span> <span data-ttu-id="e8be3-113">Le applicazioni in esecuzione in una macchina virtuale ricevono le informazioni sugli aggiornamenti futuri chiamando le API degli [eventi pianificati](../virtual-machines-scheduled-events.md) del [servizio metadati di Azure](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8be3-113">Applications running in a virtual machine can learn about upcoming updates by calling the [Scheduled Events](../virtual-machines-scheduled-events.md) API of the [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
