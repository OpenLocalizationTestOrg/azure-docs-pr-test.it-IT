---
title: domande frequenti (FAQ sulla ricerca di Azure) aaaFrequently | Documenti Microsoft
description: Ottenere risposte alle domande toocommon sul servizio di ricerca di Microsoft Azure
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Ricerca di Azure: Domande frequenti
 
 Trovare le risposte toocommonly domande frequenti sui concetti, codice e gli scenari correlati tooAzure ricerca.

## <a name="platform"></a>Piattaforma

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>In cosa si distingue Ricerca di Azure dalla ricerca full-text nel sistema di gestione di database (DBMS)?

Ricerca di Azure supporta più origini dati, [l'analisi linguistica per molti linguaggi](https://docs.microsoft.com/rest/api/searchservice/language-support), [l'analisi personalizzata per input di dati interessanti e insoliti](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), i controlli di classificazione delle ricerche mediante i [profili di punteggio](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) e le funzionalità di esperienza utente, ad esempio i completamenti automatici, l'evidenziazione dei riscontri e l'esplorazione in base a facet. Include anche altre funzionalità, come i sinonimi e la sintassi di query avanzata, ma queste non sono in genere funzionalità di differenziazione del servizio.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>Qual è la differenza hello tra ricerca di Azure ed Elasticsearch?

Quando si confrontano le tecnologie di ricerca, i clienti spesso chiedono informazioni sulle specifiche di Ricerca di Azure in confronto a Elasticsearch. I clienti che scelgono ricerca di Azure su Elasticsearch per la ricerca i progetti di applicazione in genere farlo perché sono stati apportati più facilmente un'attività chiave o necessarie integrazione incorporata specifica hello con altre tecnologie Microsoft:

+ Ricerca di Azure è un servizio cloud completamente gestito con contratti di servizio (SLA) al 99,9% quando offerto in provisioning con una ridondanza sufficiente (2 repliche per l'accesso in lettura, 3 repliche per l'accesso in lettura e scrittura).
+ I [processori di linguaggio naturale](https://docs.microsoft.com/rest/api/searchservice/language-support) offrono l'analisi linguistica all'avanguardia.  
+ Gli [indicizzatori di Ricerca di Azure](search-indexer-overview.md) possono eseguire ricerche di un'ampia gamma di origini dati di Azure per l'indicizzazione iniziale e incrementale.
+ Se è necessario toofluctuations rapidi tempi di risposta query o l'indicizzazione di volumi, è possibile utilizzare [controlli dispositivo di scorrimento](search-manage.md#scale-up-or-down) nel portale di Azure, o esecuzione hello un [script di PowerShell](search-manage-powershell.md), ignorando direttamente di gestione di partizioni.  
+ [Assegnazione di punteggi e le funzionalità di ottimizzazione](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) forniscono hello consente per modificare i punteggi di pertinenza ricerca oltre può fornire solo il motore di ricerca hello. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>È possibile sospendere il servizio Ricerca di Azure e interrompere la fatturazione?

È possibile sospendere il servizio di hello. Risorse di calcolo e archiviazione vengono allocate per l'uso esclusivo quando viene creato il servizio di hello. Non è possibile toorelease e recuperare le risorse su richiesta. 

## <a name="indexing-operations"></a>Operazioni di indicizzazione

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>È possibile eseguire il backup e il ripristino (o il download e lo spostamento) degli indici o degli snapshot dell'indice?

Sebbene sia possibile [ottenere una definizione di indice](https://docs.microsoft.com/rest/api/searchservice/get-index) in qualsiasi momento, non vi è alcun estrazione indice, snapshot o funzionalità di ripristino di backup per il download una *popolato* in esecuzione nel sistema locale tooa cloud hello, indice o spostarlo tooanother servizio di ricerca di Azure. 

Gli indici vengono compilati e popolati dal codice da scrivere ed eseguire solo sulla ricerca di Azure nel cloud hello. In genere, i clienti che desiderano un servizio di indicizzazione tooanother toomove modificando i toouse di codice un nuovo endpoint e quindi eseguire di nuovo l'indicizzazione. Se si desidera hello possibilità tootake uno snapshot o eseguire il backup di un indice, il cast di un voto [Uservoice](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>È possibile indicizzare da repliche di database SQL (si applica troppo[gli indicizzatori di Database SQL di Azure](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 Non esistono restrizioni sull'utilizzo di hello delle repliche primarie o secondarie come origine dati quando si compila un indice da zero. Tuttavia, l'aggiornamento di un indice con gli aggiornamenti incrementali (basati su record modificati) richiede la replica primaria hello. Questo requisito deriva dal database SQL, che garantisce il rilevamento delle modifiche solo nelle repliche primarie. Se si tenta di utilizzo delle repliche secondarie per un carico di lavoro di aggiornamento di indice, non c'è garanzia che ottenere tutti i dati di hello.

## <a name="search-operations"></a>Operazioni di ricerca

### <a name="can-i-search-across-multiple-indexes"></a>È possibile eseguire ricerche tra più indici?

No, questa operazione non è supportata. La ricerca è sempre tooa con ambito singolo indice.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>È possibile limitare l'accesso ai dati delle ricerche in base all'identità dell'utente?

Ricerca di Azure non dispone di un modello di sicurezza basato sui ruoli che consenta l'accesso ai dati in base all'utente. L'autenticazione è entrambi diritti completi di sola lettura a livello di servizio hello. Alcuni clienti hanno implementato soluzioni basate sul [parametro di ricerca `$filter`](https://docs.microsoft.com/rest/api/searchservice/search-documents), ma è solo un espediente. Se si desidera questa funzionalità, esprimere un voto in [User Voice](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>Perché ci sono zero corrisponde alle condizioni che so toobe valido?

caso più comune di Hello è non sapere che ogni tipo di query supporta livelli di analisi linguistiche e i comportamenti di ricerca diverso. Ricerca full-text, vale a dire il carico di lavoro predominante hello, include una fase di analisi language che causa l'interruzione termini verso il basso tooroot form. Questo aspetto di analisi delle query esegue il cast di una rete più ampia tramite le corrispondenze possibili, perché in formato token termine hello corrisponde un maggior numero di varianti.

Se si richiamano [altri tipi di query](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (ricerca con caratteri jolly, ricerca di corrispondenze parziali, ricerca per prossimità, suggerimenti, per citarne alcuni), non vi è alcuna analisi linguistica. Termini vengono aggiunti ad albero di query toohello come-è. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>Perché è la classificazione di ricerca hello un punteggio di costante o uguale di 1.0 per ogni occorrenza?

Per impostazione predefinita, i risultati della ricerca sono assegnati dei punteggi in base su hello [proprietà statistiche dei termini corrispondenti](search-lucene-query-architecture.md#stage-4-scoring)e ordinate toolow elevato nel set di risultati hello. Tuttavia, per alcune query di tipo (carattere jolly, prefisso, regex) contribuiscono sempre un punteggio costante punteggio toohello complessivo del documento. Questo comportamento dipende dalla progettazione. Ricerca di Azure impone una costante di assegnare un punteggio tooallow corrispondenza tramite query espansione toobe inclusi nei risultati di hello, senza influire sul calcolo della pertinenza hello. 

Si supponga ad esempio che un input "viaggi*" in una ricerca con caratteri jolly produca corrispondenze come "viaggio", "viaggiatore" e "viaggiare". Data la natura hello di questi risultati, non è possibile dedurre tooreasonably quali termini sono più utili rispetto ad altri. Per questo motivo, verranno ignorate le frequenze di termini durante l'assegnazione dei punteggi dei risultati nelle query di tipo con caratteri jolly, prefisso e regex. Risultati della ricerca in base a un input parziale vengono assegnati a una costante di assegnare un punteggio distorsione tooavoid verso risultati imprevisti.

## <a name="design-patterns"></a>Modelli di progettazione

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>Che cos'è l'approccio migliore di hello per l'implementazione della localizzata ricerca?

La maggior parte dei clienti scegliere campi dedicati in una raccolta per quanto riguarda toosupporting diverse impostazioni locali (lingue) in hello stesso indice. Campi di specifica delle impostazioni locali rendono possibili tooassign un analizzatore appropriato. Ad esempio, l'assegnazione di campo tooa di Microsoft francese Analyzer hello contenente le stringhe in francese. Viene anche semplificata l'applicazione dei filtri. Se si conosce che una query viene avviata in una pagina fr-fr, si rischia di campo toothis risultati della ricerca. In alternativa, creare un [profilo di punteggio](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive hello campo più peso relativo.

## <a name="next-steps"></a>Passaggi successivi

La domanda riguarda una funzione o una funzionalità mancante? Richiedere funzionalità hello in hello [sito Uservoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Vedere anche

 [StackOverflow: Ricerca di Azure](https://stackoverflow.com/questions/tagged/azure-search)   
 [Funzionamento della ricerca full-text in Ricerca di Azure](search-lucene-query-architecture.md)  
 [Che cos'è la Ricerca di Azure?](search-what-is-azure-search.md)

 