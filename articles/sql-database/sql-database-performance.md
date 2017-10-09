---
title: aaaMonitor e migliorare le prestazioni - Database SQL di Azure | Documenti Microsoft
description: Database SQL di Azure offre prestazioni Hello strumenti toohelp si identificano le aree che possono migliorare le prestazioni delle query corrente.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>Monitorare e migliorare le prestazioni
Il database SQL di Azure identifica potenziali problemi in un database e propone azioni che consentono di migliorare le prestazioni del carico di lavoro tramite azioni e raccomandazioni per l'ottimizzazione intelligente.

tooreview le prestazioni del database, utilizzare hello **prestazioni** riquadro nella pagina di panoramica hello o spostarsi verso il basso troppo "Supporto + risoluzione dei problemi" sezione:

   ![Visualizzare le prestazioni](./media/sql-database-performance/entries.png)

Nella sezione hello "Supporto + risoluzione dei problemi", è possibile utilizzare hello seguenti pagine:


1. [Cenni preliminari sulle prestazioni](#performance-overview) toomonitor delle prestazioni del database. 
2. [Consigli relativi alle prestazioni](#performance-recommendations) toofind suggerimenti relativi alle prestazioni che può migliorare le prestazioni del carico di lavoro.
3. [Informazioni dettagliate prestazioni query](#query-performance-insight) toofind query per consumo di risorse superiore.
4. [L'ottimizzazione automatica](#automatic-tuning) toolet Database SQL di Azure ottimizzare automaticamente il database.

## <a name="performance-overview"></a>Panoramica sulle prestazioni
Questa vista offre una panoramica delle prestazioni del database e facilita le operazioni di ottimizzazione delle prestazioni e risoluzione dei problemi. 

![Prestazioni](./media/sql-database-performance/performance.png)

* Hello **indicazioni** riquadro fornisce un riepilogo di indicazioni per il database di ottimizzazione (prime tre raccomandazioni vengono visualizzati se sono presenti più). Fare clic su questo riquadro consente di passare troppo**[consigli relativi alle prestazioni](#performance-recommendations)**. 
* Hello **ottimizzazione attività** riquadro fornisce un riepilogo di hello in corso e completata ottimizzazione azioni per il database, consentendo di visualizzare rapidamente cronologia hello delle attività di ottimizzazione. Fare clic su questo riquadro consente di passare toohello completo ottimizzazione visualizzazione della cronologia per il database.
* Hello **ottimizzazione automatica** riquadro Mostra hello [ottimizzazione automatica della configurazione](sql-database-automatic-tuning-enable.md) per il database (ottimizzazione opzioni che vengono automaticamente applicati tooyour database). Fare clic su questo riquadro, verrà visualizzata la finestra di dialogo Configurazione automazione hello.
* Hello **le query su Database** riquadro riepiloga hello hello le prestazioni delle query per il database (generale DTU utilizzo e top resource query per consumo). Fare clic su questo riquadro consente di passare troppo**[informazioni dettagliate prestazioni Query](#query-performance-insight)**.

## <a name="performance-recommendations"></a>Raccomandazioni per le prestazioni
Questa pagina offre [raccomandazioni per l'ottimizzazione](sql-database-advisor.md) intelligenti che consentono di migliorare le prestazioni del database. in questa pagina viene visualizzato i seguenti tipi di suggerimenti Hello:

* Suggerimenti su quale toocreate indici o drop.
* Suggerimenti quando vengono identificati i problemi dello schema nel database di hello.
* Consigli sui casi in cui trarre vantaggio dalle query con parametri.

![Prestazioni](./media/sql-database-performance/recommendations.png)

È inoltre possibile trovare cronologia completa di ottimizzazione di azioni che sono state applicate in hello precedente.

Informazioni su come toofind apply consigli relativi alle prestazioni in [cercare e applicare i consigli relativi alle prestazioni](sql-database-advisor-portal.md) articolo.

## <a name="automatic-tuning"></a>Ottimizzazione automatica
Il database SQL di Azure può ottimizzare automaticamente le prestazioni del database tramite l'applicazione di [raccomandazioni per le prestazioni](sql-database-advisor.md). leggere più, toolearn [articolo ottimizzazione automatica](sql-database-automatic-tuning.md). tooenable, leggere [come l'ottimizzazione automatica tooenable](sql-database-automatic-tuning-enable.md).

## <a name="query-performance-insight"></a>Informazioni dettagliate prestazioni query
[Informazioni dettagliate prestazioni query](sql-database-query-performance.md) toospend consente tempi di risoluzione dei problemi di prestazioni del database fornendo:

* Informazioni più approfondite sull'utilizzo delle risorse del database (DTU). 
* Hello superiore che utilizzano la CPU query, è potenzialmente possibile ottimizzare per migliorare le prestazioni. 
* Hello possibilità toodrill verso il basso in dettagli hello di una query. 

  ![dashboard prestazioni](./media/sql-database-query-performance/performance.png)

Ulteriori informazioni su questa pagina dell'articolo hello  **[come toouse informazioni dettagliate prestazioni Query](sql-database-query-performance.md)**.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Indicazioni sulle prestazioni del database SQL di Azure per i singoli database](sql-database-performance-guidance.md)
* [Quando usare un pool elastico](sql-database-elastic-pool-guidance.md)

