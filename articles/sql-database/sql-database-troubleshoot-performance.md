---
title: aaaMonitoring & ottimizzazione delle prestazioni - Database SQL di Azure | Documenti Microsoft
description: Suggerimenti per l'ottimizzazione delle prestazioni nel database SQL di Azure tramite valutazione e miglioramento.
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: ottimizzazione delle prestazioni di sql, ottimizzazione delle prestazioni del database, suggerimenti di ottimizzazione delle prestazioni di sql ottimizzazione delle prestazioni del database sql
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a>Monitoraggio e ottimizzazione delle prestazioni

Database SQL di Azure viene gestito automaticamente e di servizio dati flessibile in cui è possibile monitorare l'utilizzo, aggiungere o rimuovere facilmente le risorse (CPU, memoria, io), trovare indicazioni che possono migliorare le prestazioni del database, o si lascia database adattare il carico di lavoro tooyour e ottimizzare automaticamente le prestazioni.

Questo articolo offre una panoramica delle opzioni di monitoraggio e di ottimizzazione delle prestazioni disponibili nel database SQL di Azure.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a>Monitoraggio e risoluzione dei problemi relativi alle prestazioni del database

Abilita Database SQL Azure è tooeasily monitorare l'utilizzo del database e identificare le query che potrebbero causare problemi di prestazioni hello. È possibile monitorare le prestazioni del database usando le visualizzazioni di sistema o il portale di Azure. È necessario hello le opzioni per il monitoraggio e risoluzione dei problemi di prestazioni del database seguenti:

1. In hello [portale di Azure](https://portal.azure.com), fare clic su **database SQL**, selezionare il database di hello e quindi utilizzare toolook grafico di monitoraggio hello per le risorse per raggiungere la massima. L'utilizzo di DTU viene visualizzato per impostazione predefinita. Fare clic su **modifica** toochange hello intervallo di tempo e sui valori indicati.
2. Utilizzare [informazioni dettagliate prestazioni Query](sql-database-query-performance.md) query hello tooidentify spesa hello più risorse.
3. È possibile utilizzare viste a gestione dinamica (DMV), eventi estesi (`XEvents`), e hello archivio Query nei parametri di prestazioni di SQL Server Management Studio tooget in tempo reale.

Vedere hello [argomento Guida prestazioni](sql-database-performance-guidance.md) toofind tecniche che è possibile utilizzare tooimprove delle prestazioni del Database SQL di Azure, se si individua un problema con questi report o viste.

> [!IMPORTANT] 
> È consigliabile utilizzare sempre hello versione più recente di Management Studio tooremain sincronizzati con gli aggiornamenti tooMicrosoft Azure e il Database SQL. [Aggiornare SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>

## <a name="optimize-database-tooimprove-performance"></a>Ottimizzare le prestazioni del database tooimprove

Database SQL di Azure consente tooidentify opportunità tooimprove e ottimizzare le prestazioni delle query senza modificare le risorse, è consigliabile consultare [indicazioni di ottimizzazione delle prestazioni](sql-database-advisor.md). Spesso le prestazioni non ottimali del database sono dovute a indici mancanti e query non ottimizzate correttamente. È possibile applicare questi ottimizzazione delle prestazioni di tooimprove indicazioni del carico di lavoro.
È anche possibile consentire i database SQL di Azure troppo[automaticamente ottimizzare le prestazioni delle query](sql-database-automatic-tuning.md) applicando tutte identificate indicazioni e verifica che è migliorare le prestazioni del database. È possibile utilizzare hello opzioni tooimprove delle prestazioni del database seguenti:

1. Utilizzare [guidata Database SQL](sql-database-advisor-portal.md) tooview indicazioni per la creazione e l'eliminazione degli indici, la parametrizzazione delle query e risolvere i problemi dello schema.
2. [Abilitare l'ottimizzazione automatica](sql-database-automatic-tuning-enable.md) e consentire al database SQL di Azure di correggere automaticamente i problemi di prestazioni identificati.

## <a name="improving-database-performance-with-more-resources"></a>Miglioramento delle prestazioni del database con più risorse

Infine, se non esistono elementi eseguibili che possono migliorare le prestazioni del database, è possibile modificare la quantità hello delle risorse disponibili nel Database di SQL Azure. È possibile assegnare più risorse modificando hello [livello di servizio](sql-database-service-tiers.md) di autonoma del database o aumentare hello Edtu di un pool elastico in qualsiasi momento.
1. Per database autonomi, è possibile [modificare i livelli di servizio](sql-database-service-tiers.md) tooimprove su richiesta delle prestazioni del database.
2. Per più database, è consigliabile usare [pool elastici](sql-database-elastic-pool-guidance.md) tooscale risorse automaticamente.

## <a name="tune-and-refactor-application-or-database-code"></a>Ottimizzare ed eseguire il refactoring del codice del database o dell'applicazione

È possibile modificare in modo ottimale toomore codice applicazione utilizzare hello database, modificare gli indici, forzare piani o utilizzare i parametri toomanually adattare il carico di lavoro di hello database tooyour. Trovare alcuni suggerimenti e indicazioni per l'ottimizzazione manuale e riscrivere il codice hello in hello [argomento Guida prestazioni](sql-database-performance-guidance.md) articolo.


## <a name="next-steps"></a>Passaggi successivi

- ottimizzazione in Database SQL di Azure e consentire automatico automatica tooenable funzionalità di ottimizzazione completamente gestire il carico di lavoro, vedere [abilitare la regolazione automatica](sql-database-automatic-tuning-enable.md).
- toouse di ottimizzazione manuale, è possibile esaminare [le indicazioni nel portale di Azure di ottimizzazione](sql-database-advisor-portal.md) e applicare manualmente hello varianti che migliorano le prestazioni delle query.
- Modificare le risorse disponibili nel database modificando i [livelli di servizio Database SQL di Azure](sql-database-performance-guidance.md)