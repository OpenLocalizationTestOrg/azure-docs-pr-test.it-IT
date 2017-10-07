---
title: consigli relativi alle prestazioni di preparazione di aaaAzure | Documenti Microsoft
description: Utilizzare Advisor toooptimize hello prestazioni delle distribuzioni di Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>Consigli di Advisor sulle prestazioni

Consigli relativi alle prestazioni di Azure Advisor consentono al miglioramento di hello velocità e la velocità di risposta delle applicazioni business-critical. È possibile ottenere indicazioni relative alle prestazioni da Advisor in hello **prestazioni** scheda dashboard Advisor hello.

![Scheda Prestazioni di Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>Migliorare le prestazioni del database con Advisor per database SQL

Advisor fornisce una visualizzazione coerente e consolidata dei consigli per tutte le risorse di Azure. Si integra con toobring guidata Database SQL di indicazioni per migliorare le prestazioni di hello del database di SQL Azure. Preparazione del Database SQL valuta le prestazioni di hello dei database di SQL Azure analizzando alla cronologia di utilizzo. Quindi offre indicazioni più adatti per l'esecuzione del carico di lavoro tipico del database hello. 

> [!NOTE]
> indicazioni tooget, un database deve avere circa una settimana di utilizzo e all'interno di tale settimana deve essere un'attività coerenza. Advisor per database SQL può essere più facilmente ottimizzato per modelli di query coerenti anziché picchi irregolari casuali di attività.

Per altre informazioni su Advisor per database SQL, vedere [Advisor per database SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).

![Consigli sul database SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>Migliorare affidabilità e prestazioni di Cache Redis

Advisor identifica le istanze di Cache Redis in cui le prestazioni potrebbero aver subito effetti negativi a causa di uso di memoria, carico del server, larghezza di banda di rete e numero di connessioni client elevati. Advisor fornisce inoltre procedure consigliate toohelp suggerimenti evitare potenziali problemi. Per altre informazioni relative ai consigli su Cache Redis, vedere [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>Migliorare affidabilità e prestazioni di Servizi app

Azure Advisor integra consigli sulle procedure consigliate per migliorare l'esperienza di Servizi app e scoprire le funzionalità della piattaforma pertinente. Esempi di consigli per Servizi app sono:
* Rilevamento delle istanze in cui le risorse di CPU o memoria vengono esaurite dai runtime delle app con opzioni di migrazione.
* Rilevamento delle istanze in cui la collocazione delle risorse come App Web e database può aumentare le prestazioni e ridurre il costo. 

Per altre informazioni sui consigli per Servizi app, vedere [Procedure consigliate per Servizio app di Azure](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).
![Consigli per Servizi app](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>Come tooaccess consigli relativi alle prestazioni Advisor

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Nel riquadro di sinistra hello, fare clic su **più servizi**.

3. Hello servizio dei menu, in **monitoraggio e gestione**, fare clic su **Advisor Azure**.  
 Hello Advisor dashboard viene visualizzato.

4. Nel dashboard di Advisor hello, fare clic su hello **prestazioni** scheda.

5. Selezionare hello sottoscrizione per il quale desidera tooreceive indicazioni e quindi fare clic su **consigli**.

> [!NOTE]
> tooaccess raccomandazioni di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor. Una sottoscrizione viene registrata quando un *sottoscrizione proprietario* avvia hello hello di dashboard e fa clic su Advisor **consigli** pulsante. Si tratta di un'*operazione una tantum*. Dopo la sottoscrizione hello è registrata, è possibile accedere raccomandazioni di Advisor come *proprietario*, *collaboratore*, o *lettore* per una sottoscrizione, un gruppo di risorse, o risorsa specifica.

## <a name="next-steps"></a>Passaggi successivi

toolearn sulle raccomandazioni di Advisor, vedere:

* [Introduzione tooAdvisor](advisor-overview.md)
* [Introduzione ad Advisor](advisor-get-started.md)
* [Advisor Cost recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sui costi)
* [Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)
* [Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza)

