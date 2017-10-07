---
title: Evitare interruzioni del servizio con i processi di Analisi di flusso di Azure | Microsoft Docs
description: Indicazioni per ottenere la resilienza nell'aggiornamento dei processi di Analisi di flusso.
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Garantire l'affidabilità dei processi di Analisi di flusso durante gli aggiornamenti del servizio

Parte del corso di un servizio completamente gestito è hello funzionalità toointroduce nuove funzionalità del servizio e i miglioramenti a un ritmo rapido. La distribuzione di aggiornamenti del servizio in Analisi di flusso può quindi essere eseguita con frequenza settimanale o superiore. Indipendentemente da quante attività di test viene eseguita sia ancora disponibile il rischio che un processo esistente, in esecuzione possono essere interrotte a causa di toohello introduzione di un bug. Per i clienti che eseguono processi di importanza critica per l'elaborazione streaming tali rischi necessario toobe evitato. Un meccanismo i clienti possono utilizzare tooreduce è il rischio di Azure  **[area abbinata](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modello. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Vantaggi delle aree abbinate di Azure per la risoluzione del problema

Analisi di flusso garantisce che i processi nelle aree abbinate vengano aggiornati in batch separati. È pertanto una distanza di tempo sufficiente tra gli aggiornamenti di hello tooidentify potenziale interruzione bug e aggiornarli.

_Con l'eccezione hello di India centrale_ (il cui area abbinata, India meridionale, non dispone di presenza di flusso Analitica), la distribuzione di hello di un aggiornamento di tooStream Analitica non verrà eseguite di hello stesso periodo di tempo in un set di aree abbinate. Le distribuzioni in più aree **in hello nello stesso gruppo** può verificarsi **in hello contemporaneamente**.

articolo Hello in  **[disponibilità e aree abbinate](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  presenta informazioni più aggiornate di hello in cui vengono combinate le aree.

I clienti sono toodeploy consigliato processi identici tooboth abbinato aree. Inoltre tooStream Analitica interno funzionalità, i clienti di monitoraggio è anche consigliabile processi hello toomonitor come se **entrambi** sono processi di produzione. Se toobe identificato un risultato hello Analitica di flusso di aggiornamento del servizio è un'interruzione, eseguire l'escalation in modo appropriato ed eseguire il failover alcun output di un processo integro toohello consumer a valle. Escalation toosupport impedirà area abbinata hello da siano interessati da una nuova distribuzione hello e hello l'integrità dei processi di hello abbinato.
