---
title: "i problemi di disponibilità aaaApplication e assistenza per domande frequenti sui servizi Cloud di Microsoft Azure | Documenti Microsoft"
description: "Questo articolo vengono elencati hello domande frequenti sull'applicazione e la disponibilità del servizio per servizi Cloud di Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemi di disponibilità di applicazioni e servizi per Servizi cloud di Azure: domande frequenti

Questo articolo include le domande frequenti relative ai problemi di disponibilità di applicazioni e servizi per [Servizi cloud di Microsoft Azure](https://azure.microsoft.com/services/cloud-services). È anche possibile consultare hello [pagina dimensione di macchina virtuale di servizi Cloud](cloud-services-sizes-specs.md) per informazioni sulle dimensioni.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>Il ruolo è stato riciclato. È stato implementato un aggiornamento per il servizio cloud?
Circa una volta al mese, Microsoft rilascia una nuova versione del sistema operativo guest per VM PaaS di Microsoft Azure. Il sistema operativo Guest è solo uno di tali aggiornamenti nella pipeline hello. Una versione può essere influenzata da molti altri fattori. Inoltre, Azure è in esecuzione su centinaia di migliaia di computer. È pertanto impossibile toopredict data esatta di hello e l'ora quando verranno riavviati i ruoli. Hello Guest del sistema operativo Feed RSS di aggiornamento viene aggiornato con informazioni più recenti hello che abbiamo, ma è necessario considerare che riportato toobe ora un valore approssimativo. Siamo tenere presente che questo rappresenta un problema per i clienti e sta lavorando in un piano toolimit o con precisione i riavvii di tempo.

Per informazioni complete sugli aggiornamenti recenti del sistema operativo guest vedere [Rilasci del sistema operativo guest Azure e matrice di compatibilità dell'SDK](cloud-services-guestos-update-matrix.md).

Per informazioni utili sui riavvii e sui puntatori dettagli tootechnical degli aggiornamenti di Guest e del sistema operativo Host, vedere il blog MSDN hello post [istanza del ruolo viene riavviato dovuti tooOS aggiornamenti](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>Perché richiede più tempo del solito hello prima richiesta toomy servizio cloud dopo che il servizio di hello è rimasto inattivo per diverso tempo?
Quando hello Server Web riceve hello prima richiesta, innanzitutto Ricompila codice hello e quindi elabora hello richiesta. Che perché è hello altri prima richiesta impiegherà più di hello. Per impostazione predefinita, il pool di applicazioni hello Ottiene arrestato in caso di inattività dell'utente. pool di applicazioni Hello verranno riciclati anche per impostazione predefinita ogni 1,740 minuti (29 ore).

Pool di applicazioni Internet Information Services (IIS) possono essere stati instabili tooavoid periodicamente riciclato che possono causare perdite di memoria, blocchi o arresti anomali del sistema tooapplication.

Hello documenti seguenti consentono di comprendere e ovviare a questo problema:
* [Fixing slow initial load for IIS](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis) (Correzione del problema di caricamento iniziale lento per IIS)
* [IIS 7.5 web application first request after app-pool recycle very slow](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow) (La prima richiesta all'applicazione Web IIS 7.5 dopo il riciclo del pool di app è molto lenta)

Se si desidera il comportamento predefinito di hello toochange di IIS, è necessario toouse le attività di avvio, poiché se si applicano manualmente le istanze di ruolo Web toohello modifiche, le modifiche di hello infine andranno perse.

Per ulteriori informazioni, vedere [modalità di avvio tooconfigure ed eseguire attività per un servizio cloud](cloud-services-startup-tasks.md).
