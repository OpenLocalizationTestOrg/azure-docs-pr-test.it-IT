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
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a>Manutenzione con mantenimento delle macchine virtuali (migrazione della macchina virtuale sul posto)

Mentre la maggior parte hello degli aggiornamenti non toohosted impatto macchine virtuali, vi sono casi in cui toocomponents aggiornamenti o i servizi comportare interferenze minimo toorunning macchine virtuali (senza un riavvio completo della macchina virtuale hello).

Questi aggiornamenti vengono eseguiti con la tecnologia che consente la migrazione sul posto in tempo reale, anche detta "aggiornamento con mantenimento della memoria". Quando si aggiorna host hello, macchina virtuale hello viene inserito in uno stato di "sospensione", mantenendo memoria hello nella RAM, mentre hello hosting ambiente (ad esempio, il sistema operativo sottostante) si applica patch e aggiornamenti necessari hello.
macchina virtuale Hello viene quindi ripreso entro 30 secondi di in pausa.
Dopo la ripresa, clock hello della macchina virtuale hello viene sincronizzato automaticamente.

Non tutti gli aggiornamenti possono essere distribuiti tramite questo meccanismo, ma è specificato il periodo breve pausa, la distribuzione degli aggiornamenti in questo modo è notevolmente riduce macchine toovirtual impatto.

Gli aggiornamenti a istanza multipla (le macchine virtuali sono in un set di disponibilità) vengono applicati su un dominio di aggiornamento alla volta.

Alcune applicazioni potrebbero essere interessate da questi aggiornamenti più di altre. Applicazioni che eseguono l'elaborazione di eventi in tempo reale, i flussi multimediali o transcodifica o ad alta velocità effettiva di rete scenari, ad esempio, potrebbero non essere tootolerate progettato una pausa secondo 30. Le applicazioni in esecuzione in una macchina virtuale possono informati sugli aggiornamenti futuri tramite chiamata hello [agli eventi pianificati](../virtual-machines-scheduled-events.md) API di hello [servizio metadati Azure](../virtual-machines-instancemetadataservice-overview.md).
