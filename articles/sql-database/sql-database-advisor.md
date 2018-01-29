---
title: Raccomandazioni per le prestazioni - Database SQL di Azure | Microsoft Docs
description: Il database SQL di Azure offre raccomandazioni per i database SQL esistenti che consentono di migliorare le prestazioni correnti delle query.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: On Demand
ms.date: 09/20/2017
ms.author: sstein
ms.openlocfilehash: ea1069d4ec29ad66562a6798a8b13998d0d2ef89
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="performance-recommendations"></a>Raccomandazioni per le prestazioni

Il database SQL di Azure apprende e si adatta all'applicazione e offre raccomandazioni personalizzate che consentono di ottimizzare le prestazioni dei database SQL. Le prestazioni vengono valutate continuamente analizzando la cronologia relativa all'utilizzo del database SQL. Le raccomandazioni fornite si basano su un modello di carico di lavoro univoco del database e consentono di migliorarne le prestazioni.

> [!TIP]
> L'[ottimizzazione automatica](sql-database-automatic-tuning.md) è il metodo consigliato per l'ottimizzazione delle prestazioni. [Intelligent Insights](sql-database-intelligent-insights.md) è il metodo consigliato per il monitoraggio delle prestazioni. 
>

## <a name="create-index-recommendations"></a>Raccomandazioni relative alla creazione di indici
Il database SQL di Azure esegue un monitoraggio continuo delle query eseguite e identifica gli indici che potrebbero migliorare le prestazioni. Dopo aver raccolto dati sufficienti per confermare la mancanza di un determinato indice, verrà creata una nuova raccomandazione **Crea indice**. Il database SQL di Azure conferma l'attendibilità dei rilevamenti stimando il miglioramento delle prestazioni che potrebbe offrire l'indice nel tempo. A seconda del miglioramento delle prestazioni stimato, le raccomandazioni vengono classificate come Alta, Media o Bassa. 

Gli indici creati usando le raccomandazioni vengono sempre contrassegnati come indici auto_created. È possibile scoprire quali indici sono auto_created esaminando la vista sys.indexes. Gli indici creati automaticamente non bloccano i comandi ALTER/RENAME. Se si tenta di eliminare la colonna su cui si basa un indice creato automaticamente, il comando viene eseguito ed elimina anche l'indice creato automaticamente. Gli indici normali bloccano il comando ALTER/RENAME sulle colonne indicizzate.

Dopo aver applicato la raccomandazione per l'indice, il database SQL di Azure confronterà le prestazioni delle query con la baseline. Se il nuovo indice ha introdotto miglioramenti delle prestazioni, la raccomandazione verrà contrassegnata come positiva e sarà disponibile un report dell'impatto. Se l'indice non offre vantaggi, verrà annullato automaticamente. In questo modo il database SQL di Azure garantisce che l'uso delle raccomandazioni consenta solo di ottenere miglioramenti delle prestazioni del database.

Per qualsiasi raccomandazione **Crea indice** esiste un criterio di sicurezza che non consente di applicare la raccomandazione se l'utilizzo delle risorse di un database o pool è elevato. Il criterio di sicurezza tiene conto di CPU, I/O dati, I/O log e dell'archiviazione disponibile. Se la CPU, l'I/O dati o l'I/O log risulta superiore all'80% negli ultimi 30 minuti, la creazione dell'indice verrà posticipata. Se l'archiviazione disponibile è inferiore al 10% dopo aver creato l'indice, la raccomandazione passerà allo stato di errore. Se dopo due giorni l'ottimizzazione automatica considera ancora utile un indice, il processo verrà avviato nuovamente. Questo processo viene ripetuto fino a quando non c'è sufficiente spazio di archiviazione disponibile per creare un indice o l'indice non è più considerato utile.

## <a name="drop-index-recommendations"></a>Raccomandazioni relative all'eliminazione di indici
Oltre a rilevare un indice mancante, i database SQL di Azure analizzano continuamente le prestazioni degli indici esistenti. Se un indice è inutilizzato, il database SQL di Azure proporrà di eliminarlo. L'eliminazione di un indice è consigliabile in due casi:
* L'indice è un duplicato di un altro indice (include colonna, schema di partizione e filtri identici)
* L'indice risulta inutilizzato per un periodo prolungato (93 giorni)

Anche le raccomandazioni relative all'eliminazione di indici sono sottoposte a verifica dopo l'implementazione. Se le prestazioni risultano migliorate sarà disponibile il report di impatto. Se viene invece rilevata una riduzione delle prestazioni, la raccomandazione verrà annullata.


## <a name="parameterize-queries-recommendations"></a>Raccomandazioni relative alla creazione di query con parametri
Le raccomandazioni relative alla **creazione di query con parametri** vengono visualizzate quando sono presenti una o più query che vengono ricompilate costantemente ma finiscono con lo stesso piano di esecuzione di query. Questa condizione fa emergere l'opportunità di applicare l'impostazione forzata di parametri, in modo da permettere la memorizzazione nella cache e il riutilizzo delle query in futuro, con conseguente miglioramento delle prestazioni e riduzione dell'utilizzo delle risorse. 

Ogni query eseguita inizialmente su SQL Server deve essere compilata per generare un piano di esecuzione. Ogni piano generato viene aggiunto alla cache dei piani e le esecuzioni successive della stessa query possono riusare il piano dalla cache, eliminando la necessità di un'ulteriore compilazione. 

Le applicazioni che inviano query che includono valori senza parametri possono causare un overhead delle prestazioni, in cui per ogni query di questo tipo con valori di parametri diversi viene compilato di nuovo il piano di esecuzione. In molti casi le stesse query con valori di parametri diversi generano gli stessi di piani di esecuzione, ma questi piani vengono comunque aggiunti separatamente alla cache dei piani. La ricompilazione dei piani di esecuzione determina l'uso delle risorse del database, l'aumento della durata della query e l'overflow della cache dei piani con conseguente rimozione dei piani dalla cache. Questo comportamento di SQL Server può essere modificato impostando l'opzione di parametrizzazione forzata nel database. 

Per stimare l'impatto di questa raccomandazione, viene illustrato un confronto tra l'uso effettivo e quello previsto della CPU (nel caso di applicazione della raccomandazione). Oltre al risparmio della CPU, anche la durata della query diminuisce per il tempo impiegato nella compilazione. Anche il sovraccarico della cache dei piani sarà nettamente ridotto, consentendo alla maggioranza dei piani di rimanere nella cache e di essere riusati. Questa raccomandazione può essere applicata rapidamente e facilmente facendo clic sul comando **Applica**. 

Dopo l'applicazione, questa raccomandazione abiliterà la parametrizzazione forzata sul database entro pochi minuti e inizierà il processo di monitoraggio che dura circa 24 ore. Trascorso questo intervallo di tempo, sarà possibile visualizzare il report di convalida che mostra l'utilizzo della CPU del database nelle 24 ore prima e dopo l'applicazione la raccomandazione. SQL Database Advisor include un meccanismo di sicurezza che ripristina automaticamente la raccomandazione applicata in caso di rilevamento di una regressione delle prestazioni.

## <a name="fix-schema-issues-recommendations-preview"></a>Raccomandazioni relative alla correzione di problemi di schema (anteprima)

> [!IMPORTANT]
> Microsoft sta provvedendo alla deprecazione delle raccomandazioni relative alla correzione di problemi di schema. È consigliabile iniziare a usare [Intelligent Insights](sql-database-intelligent-insights.md) per il monitoraggio automatico dei problemi di prestazioni del database, inclusi i problemi di schema trattati in precedenza nelle raccomandazioni relative alla correzione di problemi di schema.
> 

Le raccomandazioni relative alla **correzione di problemi di schema** vengono visualizzate quando il servizio del database SQL rileva un'anomalia nel numero di errori SQL correlati allo schema nel database SQL di Azure. In genere questa indicazione viene visualizzata quando il database rileva più errori correlati allo schema (nome di colonna non valido, nome di oggetto non valido e così via) nell'arco di un'ora.

I "problemi di schema" rappresentano una classe di errori di sintassi in SQL Server che si verificano quando la definizione della query SQL e la definizione dello schema del database non sono allineate. Ad esempio, una delle colonne previste dalla query può essere assente nella tabella di destinazione o viceversa. 

Le raccomandazioni relative alla "correzione di problemi di schema" vengono visualizzate quando il servizio del database SQL di Azure rileva un'anomalia nel numero di errori SQL correlati allo schema nel database SQL di Azure. La tabella seguente illustra gli errori correlati ai problemi di schema:

| Codice di errore SQL | Messaggio |
| --- | --- |
| 201 |La procedura o funzione '*' richiede il parametro '*', che non è stato specificato. |
| 207 |Il nome di colonna '*' non è valido. |
| 208 |Il nome di oggetto '*' non è valido. |
| 213 |Il nome della colonna o il numero dei valori specificati non corrisponde alla definizione della tabella. |
| 2812 |Non è stato possibile trovare la stored procedure '*'. |
| 8144 |Numero eccessivo di argomenti specificati per la procedura o la funzione *. |

## <a name="next-steps"></a>Passaggi successivi
Monitorare le raccomandazioni e continuare ad applicarle in modo da migliorare le prestazioni. I carichi di lavoro dei database sono dinamici e cambiano in modo continuo. SQL Database Advisor continua a monitorare e offrire raccomandazioni potenzialmente utili per migliorare le prestazioni del database. 

* Vedere [Ottimizzazione automatica del database SQL di Azure](sql-database-automatic-tuning.md) per l'ottimizzazione automatica degli indici di database e dei piani di esecuzione delle query.
* Vedere [Intelligent Insights del database SQL di Azure](sql-database-intelligent-insights.md) per monitorare automaticamente le prestazioni del database con diagnostica automatizzata e analisi della causa radice dei problemi di prestazioni.
* Vedere [Applicare le raccomandazioni per le prestazioni](sql-database-advisor-portal.md) per istruzioni su come usare le raccomandazioni per le prestazioni nel portale di Azure.
* Per imparare a esaminare l'impatto sulle prestazioni delle query principali, vedere [Query Performance Insight del database SQL di Azure](sql-database-query-performance.md).


