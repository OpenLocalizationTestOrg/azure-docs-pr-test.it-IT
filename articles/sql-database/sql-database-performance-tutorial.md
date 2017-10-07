---
title: prestazioni aaaTroubleshoot problemi e ottimizzare il database | Documenti Microsoft
description: "Applicare tooyour indicazioni sulle prestazioni del Database SQL, nonché Cancella come toogain informazioni dettagliate sul hello prestazioni delle query hello in esecuzione nel database"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Risolvere i problemi di prestazioni e ottimizzare il database

Spesso le prestazioni non ottimali del database sono dovute a indici mancanti e query non ottimizzate correttamente. In questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Esaminare, applicare e ripristinare le raccomandazioni per migliorare le prestazioni.
> * Trovare query con un utilizzo elevato delle risorse.
> * Trovare query con esecuzione prolungata.

> È necessario un carico di lavoro continua in un database con problemi di prestazioni: manca un indice, ad esempio tooreceive una raccomandazione.
>

## <a name="log-in-toohello-azure-portal"></a>Accedi toohello portale di Azure

Accedi toohello [portale di Azure](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Esaminare e applicare una raccomandazione

Seguire questi tooapply passaggi raccomandazione dal sistema hello per il database:

1. Fare clic su hello **consigli relativi alle prestazioni** menu nel pannello database hello.

    ![Raccomandazioni per le prestazioni](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Selezionare un'indicazione active hello elenco di indicazioni. In questo esempio si sceglie Crea indice.

    ![Selezionare una raccomandazione](./media/sql-database-performance-tutorial/create_index.png)

3. Applicare la raccomandazione hello facendo hello **applica** pulsante. Facoltativamente, rivedere i dettagli sulle raccomandazioni hello e vedere script T-SQL hello troppo essere eseguita facendo clic su **Visualizza Script** pulsante.

    ![Applicare una raccomandazione](./media/sql-database-performance-tutorial/apply.png)

4. [Facoltativo] Abilitare l'ottimizzazione automatica per indicazioni toobe applicati automaticamente.

    ![Ottimizzazione automatica](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Ripristinare una raccomandazione

Hello guidata Database consente di monitorare ogni raccomandazione implementato. Se una raccomandazione non migliora il carico di lavoro di hello verrà ripristinato automaticamente. Il ripristino manualmente di una raccomandazione è possibile, ma nella maggior parte dei casi non è necessario. toorevert un'indicazione:

1. Menu indicazioni sulle prestazioni di toohello scegliere uno dei consigli hello applicato.

    ![Selezionare una raccomandazione](./media/sql-database-performance-tutorial/select.png)

2. Nella visualizzazione dei dettagli hello, fare clic su **Revert**.

    ![Ripristinare una raccomandazione](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>La maggior parte delle risorse di query hello che utilizza hello

Eseguire la query di hello toofind questi passaggi utilizzo hello la maggior parte delle risorse:

1. Fare clic su hello **informazioni dettagliate prestazioni Query** menu nel pannello database hello.

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Selezionare un tipo di risorsa.

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Selezionare prima query hello nella tabella hello.

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_query.png)

4. Esaminare i dettagli di query hello.

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Trovare la query in esecuzione più lunga di hello

1. Informazioni dettagliate prestazioni tooQuery scegliere hello **query a esecuzione prolungata** scheda.

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/long_running.png)

3. Selezionare prima query hello nella tabella hello.

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_first_query.png)

4. Esaminare i dettagli di query hello.

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Passaggi successivi 
Spesso le prestazioni non ottimali del database sono dovute a indici mancanti e query non ottimizzate correttamente. Questa esercitazione illustra come:
> [!div class="checklist"]
> * Esaminare, applicare e ripristinare le raccomandazioni per migliorare le prestazioni.
> * Trovare query con un utilizzo elevato delle risorse.
> * Trovare query con esecuzione prolungata.

[Suggerimenti sull'ottimizzazione delle prestazioni del database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
