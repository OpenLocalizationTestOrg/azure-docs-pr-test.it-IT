---
title: aaaChoose uno SKU o livello di prezzo per la ricerca di Azure | Documenti Microsoft
description: "È possibile effettuare il provisioning di Ricerca di Azure per questi SKU: Gratuito, Basic e Standard; il piano Standard è disponibile in più configurazioni di risorse e livelli di capacità."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>Scegliere uno SKU o un piano tariffario per Ricerca di Azure
In Ricerca di Azure, il [provisioning del servizio](search-create-service-portal.md) viene effettuato a livello di piano tariffario o SKU specifico. Le opzioni disponibili includono **Gratuito**, **Basic** o **Standard**. Il piano **Standard** è disponibile in più configurazioni e capacità.

Hello in questo articolo mira toohelp scelta di un piano. Se capacità di un livello è risultata toobe troppo basso, sarà anche necessario tooprovision un nuovo servizio di livello superiore di hello e quindi ricaricare gli indici. Non vi è alcun aggiornamento sul posto di hello da uno SKU tooanother del servizio stesso.

> [!NOTE]
> Dopo aver scelto un livello e [il provisioning di un servizio di ricerca](search-create-service-portal.md), si può aumentare la replica e i conteggi di partizione all'interno del servizio hello. Per indicazioni, vedere [Ridimensionare i livelli di risorse per le query e l'indicizzazione dei carichi di lavoro](search-capacity-planning.md) .
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>Come tooapproach prezzi di un livello delle decisioni
In ricerca di Azure, livello hello determina la capacità, non disponibilità delle funzionalità. In genere, le funzionalità, incluse le funzioni di anteprima, sono disponibili in ogni piano tariffario. un'eccezione di Hello non è supportato per gli indicizzatori HD S3.

> [!TIP]
> È consigliabile eseguire sempre il provisioning del servizio **Gratuito** (uno per sottoscrizione, senza scadenza), in modo che sia subito disponibile per progetti leggeri. Hello utilizzare **libero** servizio per il testing e valutazione; creare un secondo servizio fatturabile hello **base** o **Standard** livello per più grandi carichi di lavoro di test o produzione.
>
>

Capacità e costi di esecuzione del servizio hello andare in mano a mano. Informazioni in questo articolo consente di decidere quale SKU recapita giusto equilibrio hello, ma per una delle relative toobe utile, è necessario almeno approssimative stime sul seguente hello:

* Numero e le dimensioni degli indici Prevedi toocreate
* Numero e dimensione di tooupload documenti
* Stima generica del volume di query in termini di query al secondo (QPS, Queries Per Second)

Numero e le dimensioni sono importanti perché vengono raggiunti i limiti massimi attraverso un limite al numero di hello di indici o documenti in un servizio o sulle risorse (archiviazione o repliche) utilizzate dal servizio hello. Hello limite effettivo per il servizio è a seconda del valore viene utilizzato per primo: risorse oppure oggetti.

Le stime in mano, hello alla procedura seguente dovrebbe semplificare il processo di hello:

* **Passaggio 1** rivedere le descrizioni di SKU hello sotto toolearn sulle opzioni disponibili.
* **Passaggio 2** risposte hello sotto tooarrive a una decisione preliminare.
* **Passaggio 3** Prendere una decisione definitiva esaminando i limiti rigidi in termini di archiviazione e prezzi.

## <a name="sku-descriptions"></a>Descrizioni degli SKU
Hello nella tabella seguente vengono fornite descrizioni di ogni livello.

| Livello | Scenari principali |
| --- | --- |
| **Free** |Servizio condiviso gratuito usato per la valutazione, l'analisi o piccoli carichi di lavoro. Perché è condiviso con altri sottoscrittori, velocità effettiva di query e indicizzazione varia in base che l'altro utilizza il servizio di hello. La capacità è ridotta (50 MB o 3 indici con un massimo di 10.000 documenti l'uno). |
| **Basic** |Piccoli carichi di lavoro di produzione su hardware dedicato. Disponibilità elevata. Capacità è too3 repliche e della 1 partizione (2 GB). |
| **S1** |Lo Standard 1 supporta combinazioni flessibili di partizioni (12) e repliche (12). Viene usato per i carichi di lavoro di produzione medi su hardware dedicato. È possibile allocare partizioni e repliche in combinazioni supportate da un numero massimo di 36 unità di ricerca fatturabili. In questo piano le partizioni sono da 25 GB e il valore QPS è pari a circa 15 query al secondo. |
| **S2** |2 standard esegue maggiori i carichi di lavoro tramite le unità di ricerca hello 36 stesso S1 ma con le repliche e le partizioni di dimensioni maggiori. In questo piano le partizioni sono da 100 GB e il valore QPS è pari a circa 60 query al secondo. |
| **S3** |3 standard viene eseguito proporzionalmente maggiore carichi di lavoro di produzione su sistemi end superiore, in configurazioni di backup di partizioni too12 o 12 repliche in 36 unità di ricerca. In questo piano le partizioni sono da 200 GB e il valore QPS è pari a circa 60 query al secondo. |
| **S3 HD** |Lo Standard 3 ad alta densità è progettato per un numero elevato di indici più piccoli. È possibile avere partizioni too3, da 200 GB. Il valore QPS è pari a più di 60 query al secondo. |

> [!NOTE]
> Valori massimi di replica e di partizione vengono fatturati come unità di ricerca (36 unità massime per ogni servizio), che impone un limite inferiore efficace rispetto a quale massimo hello implica per scontata. Ad esempio, toouse hello al massimo 12 repliche, è possibile al massimo di 3 partizioni (3 * 12 = 36 unità di misura). Partizioni massime toouse, ridurre in modo analogo, too3 repliche. Per un grafico delle combinazioni consentite, vedere [Ridimensionare i livelli di risorse per le query e l'indicizzazione dei carichi di lavoro in Ricerca di Azure](search-capacity-planning.md).
>
>

## <a name="review-limits-per-tier"></a>Esaminare i limiti per ogni piano
il grafico seguente Hello è un subset dei limiti di hello da [limiti dei servizi in ricerca di Azure](search-limits-quotas-capacity.md). Vengono elencati hello fattori probabilmente tooimpact una decisione di SKU. È possibile fare riferimento toothis grafico durante la revisione domande hello riportate di seguito.

| Risorsa | Free | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contratto di servizio (SLA) |No <sup>1</sup> |Sì |Sì |Sì |Sì |Sì |
| Limiti per gli indici |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| Limiti per i documenti |10.000 in totale |1 milione per servizio |15 milioni per partizione |60 milioni per partizione |120 milioni per partizione |1 milione per indice |
| Partizioni massime |N/D |1 |12 |12 |12 |3 <sup>2</sup> |
| Dimensioni della partizione |50 MB totali |2 GB per servizio |25 GB per partizione |100 GB per partizione (backup tooa massimo 1,2 TB per ogni servizio) |200 GB per partizione (backup tooa massimo 2,4 TB per ogni servizio) |200 GB (backup tooa massimo 600 GB per ogni servizio) |
| Repliche massime |N/D |3 |12 |12 |12 |12 |
| Query al secondo |N/D |~3 per replica |~15 per replica |~60 per replica |>60 per replica |>60 per replica |

<sup>1</sup> Con il Contratto di servizio non sono incluse funzionalità di anteprima e il livello gratuito. Per tutti i livelli fatturabili, i contratti di servizio diventano effettivi quando viene effettuato il provisioning di una ridondanza sufficiente per il servizio. Per il Contratto di servizio di query (lettura) sono necessarie due o più repliche. Per il contratto di servizio di query e indicizzazione (lettura-scrittura) sono necessarie tre o più repliche. numero di Hello di partizioni non è un fattore di contratto di servizio. 

<sup>2</sup> S3 e S3 HD sono supportati da un'infrastruttura identica ad alta capacità, tuttavia ciascuno raggiunge il limite massimo in modi diversi. S3 è destinato a un numero minore di indici di dimensioni molto grandi. Di conseguenza, il limite massimo è associato alle risorse (2,4 TB per ogni servizio). S3 HD è destinato a un numero elevato di indici di dimensioni molto ridotte. 1.000 indici, S3 HD raggiungere i limiti in forma di hello dei vincoli di indice. Nel caso di un cliente S3 HD che richiede più di 1.000 indici, contattare il supporto Microsoft per informazioni su come tooproceed.

## <a name="eliminate-skus-that-dont-meet-requirements"></a>Eliminare gli SKU che non soddisfano i requisiti
Hello domande seguenti consentono di ottenere hello SKU scelta per il carico di lavoro.

1. Si hanno requisiti in termini di **contratti di servizio** ? È possibile usare qualsiasi livello fatturabile (di base o superiore), ma è necessario configurare il servizio per la ridondanza. Per il Contratto di servizio di query (lettura) sono necessarie due o più repliche. Per il contratto di servizio di query e indicizzazione (lettura-scrittura) sono necessarie tre o più repliche. numero di Hello di partizioni non è un fattore di contratto di servizio.
2. **Quanti indici** sono necessari? Una delle variabili principali di hello factoring all'interno di una decisione di SKU è il numero di hello degli indici per ogni SKU è supportata. Il supporto di indice è notevolmente diversi livelli di hello inferiore ai livelli di prezzo. Il requisito relativo al numero di indici può essere determinante nella scelta dello SKU.
3. **Il numero di documenti** verrà caricato in ogni indice? hello numero e le dimensioni dei documenti determinerà dimensioni finali del hello dell'indice hello. Supponendo che è possibile stimare hello previste dimensioni dell'indice di hello, è possibile confrontare tale numero con la dimensione della partizione hello per ogni SKU, prorogato numero hello di toostore necessarie partizioni di un indice di tale dimensione.
4. **Che cos'è il carico di query prevista hello**? Dopo aver determinato i requisiti di archiviazione, prendere in considerazione i carichi di lavoro di query. S2 ed entrambi gli SKU S3 offrono una velocità effettiva quasi equivalente, ma i requisiti in termini di contratto di servizio escludono gli SKU di anteprima.
5. Se si prevede di hello S2 o S3 livello, determinare se è richiesto [indicizzatori](search-indexer-overview.md). Gli indicizzatori non sono ancora disponibili per il livello di hello HD S3. Approccio alternativo consiste toouse un modello push per gli aggiornamenti dell'indice, in cui scrivere toopush codice dell'applicazione un indice tooan set di dati.

La maggior parte dei clienti possono regola uno SKU specifico in o out in base alle loro toohello risposte sopra domande. Se si è ancora sicuri di quali toogo SKU con, è possibile pubblicare domande tooMSDN o StackOverflow forum o contattare il supporto tecnico di Azure per ulteriori informazioni sulla.

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>La decisione di convalida: hello SKU offre sufficiente spazio di archiviazione e query al secondo?
L'ultimo passaggio, rivedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/search/) hello e [sezioni per ogni servizio e per indice limiti dei servizi](search-limits-quotas-capacity.md) toodouble controllo le stime rispetto ai limiti di sottoscrizione e il servizio.

Se i requisiti di prezzo o archiviazione entrambi hello sono compresa nell'intervallo, è possibile, ad esempio, i carichi di lavoro di toorefactor hello tra più servizi più piccoli. Livello più granulare, è possibile riprogettare toobe indici più piccoli o usare filtri toomake query più efficiente.

> [!NOTE]
> I requisiti di archiviazione possono apparire maggiori del necessario se i documenti contengono dati estranei. I documenti contengono idealmente solo da dati o metadati ricercabili. Dati binari non ricerche e devono essere archiviati separatamente (ad esempio in un blob o tabelle di archiviazione Azure) con un campo in hello indice toohold un dati esterni di toohello URL di riferimento. dimensione massima di Hello di un singolo documento è 16 MB (o meno in caso si più documenti in una richiesta di caricamento bulk). Per altre informazioni, vedere [Limiti dei servizi in Ricerca di Azure](search-limits-quotas-capacity.md) .
>
>

## <a name="next-step"></a>Passaggio successivo
Quando si è certi che SKU è hello adatta a destra, continuare con questi passaggi:

* [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md)
* [Modificare il servizio di allocazione di hello di tooscale partizioni e repliche](search-capacity-planning.md)
