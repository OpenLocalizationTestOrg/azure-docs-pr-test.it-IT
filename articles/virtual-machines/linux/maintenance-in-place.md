---
title: mantenimento di manutenzione per le macchine virtuali Windows in Azure aaaVM | Documenti Microsoft
description: Migrazione di macchine virtuali sul posto per aggiornamenti con mantenimento della memoria.
services: virtual-machines-windows
documentationcenter: 
author: 
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
ms.author: 
ms.openlocfilehash: 544a2dcca52bb3ac51d341bceaf4ba3e7c71fd82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a><span data-ttu-id="7f95f-103">Manutenzione con mantenimento delle macchine virtuali (migrazione della macchina virtuale sul posto)</span><span class="sxs-lookup"><span data-stu-id="7f95f-103">VM preserving maintenance (In-place VM migration)</span></span>

<span data-ttu-id="7f95f-104">Mentre la maggior parte hello degli aggiornamenti non toohosted impatto macchine virtuali, vi sono casi in cui toocomponents aggiornamenti o i servizi comportare interferenze minimo toorunning macchine virtuali (senza un riavvio completo della macchina virtuale hello).</span><span class="sxs-lookup"><span data-stu-id="7f95f-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="7f95f-105">Questi aggiornamenti vengono eseguiti con la tecnologia che consente la migrazione sul posto in tempo reale, anche detta "aggiornamento con mantenimento della memoria".</span><span class="sxs-lookup"><span data-stu-id="7f95f-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="7f95f-106">Quando si aggiorna host hello, macchina virtuale hello viene inserito in uno stato di "sospensione", mantenendo memoria hello nella RAM, mentre hello hosting ambiente (ad esempio, il sistema operativo sottostante) si applica patch e aggiornamenti necessari hello.</span><span class="sxs-lookup"><span data-stu-id="7f95f-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="7f95f-107">macchina virtuale Hello viene quindi ripreso entro 30 secondi di in pausa.</span><span class="sxs-lookup"><span data-stu-id="7f95f-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="7f95f-108">Dopo la ripresa, clock hello della macchina virtuale hello viene sincronizzato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7f95f-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="7f95f-109">Non tutti gli aggiornamenti possono essere distribuiti tramite questo meccanismo, ma è specificato il periodo breve pausa, la distribuzione degli aggiornamenti in questo modo è notevolmente riduce macchine toovirtual impatto.</span><span class="sxs-lookup"><span data-stu-id="7f95f-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="7f95f-110">Gli aggiornamenti a istanza multipla (le macchine virtuali sono in un set di disponibilità) vengono applicati su un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="7f95f-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="7f95f-111">Alcune applicazioni potrebbero essere interessate da questi aggiornamenti più di altre.</span><span class="sxs-lookup"><span data-stu-id="7f95f-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="7f95f-112">Applicazioni che eseguono l'elaborazione di eventi in tempo reale, i flussi multimediali o transcodifica o ad alta velocità effettiva di rete scenari, ad esempio, potrebbero non essere tootolerate progettato una pausa secondo 30.</span><span class="sxs-lookup"><span data-stu-id="7f95f-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="7f95f-113">Le applicazioni in esecuzione in una macchina virtuale possono informati sugli aggiornamenti futuri tramite chiamata hello [agli eventi pianificati](../virtual-machines-scheduled-events.md) API di hello [servizio metadati Azure](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7f95f-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
