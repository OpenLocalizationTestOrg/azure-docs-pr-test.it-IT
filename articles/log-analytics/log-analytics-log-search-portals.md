---
title: aaaPortals per la creazione e modifica delle query di log in Azure Log Analitica | Documenti Microsoft
description: "Questo articolo descrive i portali di hello che è possibile utilizzare in Azure Log Analitica toocreate e ricerche nei log di modifica."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portali per la creazione e la modifica di ricerche log in Azure Log Analytics

> [!NOTE]
> Questo articolo descrive i portali di Analitica di Log di Azure utilizzando il nuovo linguaggio di query hello.  È possibile acquisire familiarità con il nuovo linguaggio di hello e ottenere hello procedure tooupgrade l'area di lavoro in [aggiornare la ricerca di log di Azure Log Analitica dell'area di lavoro toonew](log-analytics-log-search-upgrade.md).  
>
> Se l'area di lavoro non è stato aggiornato toohello nuovo linguaggio di query, è consigliabile consultare troppo[trovare i dati tramite ricerche nei log nel Log Analitica](log-analytics-log-searches.md) per informazioni sulla versione corrente di hello del portale di ricerca nei Log hello.

Utilizzare ricerche nei log in diverse posizioni all'interno di dati di Log Analitica tooretrieve dall'area di lavoro hello.  Per effettivamente la creazione e modifica di query inoltre tooworking in modo interattivo con ha restituito dati tuttavia, sono disponibili due opzioni che sono descritte di seguito.  

## <a name="log-search-portal"></a>Portale per la ricerca log
portale di ricerca nei Log Hello è accessibile da hello portale di Azure o il portale di OMS hello.  È adatto per la creazione di query semplici su una singola riga.  portale di ricerca nei Log Hello può essere usato senza avviare un portale esterno ed è possibile utilizzarlo tooperform una varietà di funzioni con ricerche nei log inclusi la creazione di regole di avviso, la creazione di gruppi di computer e l'esportazione dei risultati della query hello hello.  

portale di ricerca nei Log Hello fornisce più funzionalità per la modifica di query hello senza una conoscenza completa del linguaggio di query hello.  È possibile ottenere un riepilogo di queste funzionalità in [ricerche nei log Create in Analitica di Log di Azure tramite il portale di ricerca nei Log hello](log-analytics-log-search-log-search-portal.md).


![Portale per la ricerca log](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Portale Advanced Analytics
portale Analitica avanzate Hello è un portale dedicato che offre funzionalità avanzate non disponibili nel portale di ricerca nei Log hello.  Le funzionalità includono hello possibilità tooedit una query su più righe, in modo selettivo eseguire codice, Intellisense sensibile al contesto e Analitica Smart.  portale di Advanced Analitica Hello è più adatto per la progettazione di query complesse che sono sia salvata come una ricerca di log o copiate e incollate in altri elementi Analitica di Log.  Si avvia portale avanzate Analitica hello da un collegamento nel portale di ricerca nei Log hello.

![Portale Advanced Analytics](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


A causa delle rispettive funzionalità avanzate, in genere userai portale Analitica avanzate hello come lo strumento principale per la creazione e modifica delle query.  Dopo aver stabilito che la query hello funziona come previsto, quindi copiare e incollare in un' posizione, ad esempio il portale di ricerca nei Log hello e Progettazione viste.  Poiché portale avanzate Analitica hello supporta tuttavia le query con più righe, è necessario seguente hello tootake in considerazione quando si copia una query in questo portale.

- Commenti devono essere rimossi dal query hello prima copiati e incollati in un'altra posizione.  È possibile impostare una riga come commento anteponendovi due barre (//).  Quando si incolla una query con più righe su una riga singola, le interruzioni di riga vengono rimosse.  Se i commenti sono inclusi, tutti i caratteri dopo il primo commento hello sono considerati parte del commento hello.


## <a name="next-steps"></a>Passaggi successivi

- Scorrere un'esercitazione sull'uso di hello [portale ricerca nei Log](log-analytics-log-search-log-search-portal.md) o hello [portale avanzate Analitica](https://go.microsoft.com/fwlink/?linkid=856587) toocreate query.
- Estrarre un [esercitazione sulla scrittura di query](https://go.microsoft.com/fwlink/?linkid=856078) utilizzando il nuovo linguaggio di query hello.
