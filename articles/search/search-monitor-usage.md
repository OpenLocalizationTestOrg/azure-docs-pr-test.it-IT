---
title: aaaMonitor informazioni sull'utilizzo e le statistiche in un servizio di ricerca di Azure | Documenti Microsoft
description: Tenere traccia delle dimensioni di indice e consumo delle risorse per la Ricerca di Azure, un servizio di ricerca ospitato sul cloud in Microsoft Azure.
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Monitoraggio di un servizio di Ricerca di Azure

Ricerca di Azure offre varie risorse per tenere traccia dell'utilizzo e delle prestazioni dei servizi di ricerca. Consente di accedere a toometrics, log, le statistiche dell'indice e le funzionalità di monitoraggio estese in Power BI. In questo articolo viene descritto come tooenable hello diverse strategie di monitoraggio e la modalità toointerpret hello dati risultanti.

## <a name="azure-search-metrics"></a>Metriche di Ricerca di Azure
Le metriche offrono una visibilità quasi in tempo reale nel servizio di ricerca e sono disponibili per ogni servizio, senza alcuna impostazione aggiuntiva. Consentono di tenere traccia delle prestazioni di hello del servizio per impostare i giorni too30.

Ricerca di Azure raccoglie i dati per tre metriche diverse:

* Latenza di ricerca: ora il servizio di ricerca hello necessari tooprocess query di ricerca, aggregate per minuto.
* Query di ricerca al secondo: numero di query di ricerca ricevute al secondo, aggregate per minuto.
* Percentuale query di ricerca limitate: percentuale di query di ricerca che sono state limitate, aggregate per minuto.

![Screenshot dell'attività delle query al secondo][1]

### <a name="set-up-alerts"></a>Impostare gli avvisi
Dalla pagina di dettaglio metrica hello, è possibile configurare avvisi tootrigger una notifica di posta elettronica oppure un'azione automatica quando una metrica supera una soglia che sono state definite.

Per ulteriori informazioni sui dati di metrica, controllare la documentazione completa di hello su Monitor di Azure.  

## <a name="how-tootrack-resource-usage"></a>La modalità dell'utilizzo delle risorse tootrack
Rilevamento crescita hello di indici e delle dimensioni del documento consentono di modificare in modo proattivo capacità prima di raggiungere un limite di hello che scelti per il servizio. È possibile farlo nel portale di hello o a livello di programmazione tramite hello API REST.

### <a name="using-hello-portal"></a>Tramite il portale di hello

utilizzo delle risorse toomonitor, visualizzare i conteggi di hello e le statistiche per il servizio in hello [portale](https://portal.azure.com).

1. Accedi toohello [portale](https://portal.azure.com).
2. Aprire il dashboard del servizio hello del servizio di ricerca di Azure. Riquadri per servizio hello sono reperibile nella Home page di hello oppure è possibile esplorare toohello servizio su hello JumpBar Sfoglia.

la sezione Utilizzo Hello include un indicatore che indica la quantità di risorse disponibili sono attualmente in uso. Per informazioni sui limiti dei servizi per indici, documenti e archiviazione, vedere [Limiti dei servizi](search-limits-quotas-capacity.md).

  ![Riquadro Utilizzo][2]

> [!NOTE]
> schermata di Hello precedente per il servizio gratuito hello, che dispone di un massimo di una replica e ogni partizione può solo gli indici di host, 3, 10.000 documenti o 50 MB di dati, verifica per primo. I servizi creati con piano Basic o Standard hanno limiti più elevati. Per altre informazioni sulla scelta di un piano, vedere [Scegliere uno SKU o un piano](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>Tramite l'API REST hello
Hello API REST di ricerca di Azure sia hello .NET SDK fornire metriche tooservice accesso a livello di codice.  Se si utilizza [indicizzatori](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload un indice dal Database SQL di Azure o Azure Cosmos DB, un'API aggiuntiva è numeri hello tooget disponibili è necessario.

* [Ottenere le statistiche di un indice](/rest/api/searchservice/get-index-statistics)
* [Conteggio documenti](/rest/api/searchservice/count-documents)
* [Ottenere lo stato dell'indicizzatore](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Modalità di registrazione tooexport e metriche

È possibile esportare i log delle operazioni hello per i dati non elaborati del servizio e hello per le metriche di hello descritte nella precedente sezione hello. Registri operazioni consentono di sapere come servizio hello è in uso e può essere utilizzata da Power BI quando i dati sono copiati tooa account di archiviazione. Ricerca di Azure include per questo scopo un pacchetto di contenuti Power BI per il monitoraggio.


### <a name="enabling-monitoring"></a>Abilitazione del monitoraggio
Aprire il servizio di ricerca di Azure in hello [portale di Azure](http://portal.azure.com) in hello opzione Abilita monitoraggio.

Scegliere i dati di hello desiderato tooexport: log, le metriche o entrambi. Si può copiare account di archiviazione tooa, inviarlo hub eventi tooan o si esporta tooLog Analitica.

![La modalità di monitoraggio nel portale di hello tooenable][3]

tooenable tramite PowerShell o hello CLI di Azure, vedere la documentazione di hello [qui](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Schemi di log e di metriche
Quando si copia tooa archiviazione dei dati hello conto, hello dati vengono formattati come JSON e il luogo in due contenitori:

* insights-logs-operationlogs: per i log relativi al traffico ricerca
* insights-metrics-pt1m: per le metriche

È presente un BLOB ogni ora per ciascun contenitore.

Percorso di esempio: `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Schema del log
BLOB di log Hello contengono i log di traffico del servizio di ricerca.
Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.
Ciascun blob contiene record in tutte le operazioni di hello avvenute hello stessa ora.

| Nome | Tipo | Esempio | Note |
| --- | --- | --- | --- |
| time |datetime |"2015-12-07T00:00:43.6872559Z" |Timestamp dell'operazione hello |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/> MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |resourceId in uso |
| operationName |string |"Query.Search" |nome Hello dell'operazione di hello |
| operationVersion |string |"2015-02-28" |versione dell'api Hello utilizzato |
| category |string |"OperationLogs" |costante |
| resultType |string |"Esito positivo" |Valori possibili: esito positivo o negativo |
| resultSignature |int |200 |Codice risultato HTTP |
| durationMS |int |50 |Durata dell'operazione di hello in millisecondi |
| properties |object |vedere hello nella tabella seguente |Oggetto contenente dati specifici dell'operazione |

**Schema delle proprietà**
| Nome | Tipo | Esempio | Note |
| --- | --- | --- | --- |
| Descrizione |string |"GET /indexes('content')/docs" |endpoint dell'operazione Hello |
| Query |string |"?search=AzureSearch&$count=true&api-version=2015-02-28" |parametri di query Hello |
| Documenti |int |42 |Numero di documenti elaborati |
| IndexName |string |"testindex" |Nome dell'indice hello associato all'operazione hello |

#### <a name="metrics-schema"></a>Schema delle metriche
| Nome | Tipo | Esempio | Note |
| --- | --- | --- | --- |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/>MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |ID risorsa in uso |
| metricName |string |"Latenza" |nome Hello della metrica di hello |
| time |datetime |"2015-12-07T00:00:43.6872559Z" |timestamp dell'operazione Hello |
| average |int |64 |valore medio di Hello di campioni non elaborati di hello nell'intervallo di tempo metrica hello |
| minimum |int |37 |valore minimo di Hello di campioni non elaborati di hello nell'intervallo di tempo metrica hello |
| maximum |int |78 |valore massimo di Hello di campioni non elaborati di hello nell'intervallo di tempo metrica hello |
| total |int |258 |valore totale di Hello di campioni non elaborati di hello nell'intervallo di tempo metrica hello |
| count |int |4 |il numero di Hello di campioni non elaborati usato metrica hello toogenerate |
| timegrain |string |"PT1M" |intervallo di tempo Hello metrica hello nello standard ISO 8601 |

Tutte le metriche vengono segnalate in intervalli di un minuto. Ogni metrica espone i valori minimi, massimi e medi al minuto.

Metrica SearchQueriesPerSecond hello, valore minimo è il valore più basso di hello per le query di ricerca al secondo in cui è stato registrato il minuto. Hello vale toohello massimo. Media è hello aggregazione tra minuto intero hello.
Considerare questo scenario un minuto: un secondo di carico elevato è hello massimo per SearchQueriesPerSecond, seguita da 58 secondi di carico medio, e infine un secondo con una sola query, ovvero hello minimo.

Per ThrottledSearchQueriesPercentage, minimo, massimo, Media e totale, hanno hello stesso valore: hello percentuale di query di ricerca che sono state limitate dal numero totale di hello di query di ricerca durante un minuto.

## <a name="analyzing-your-data-with-power-bi"></a>Analisi dei dati con Power BI

Si consiglia di utilizzare [Power BI](https://powerbi.microsoft.com) tooexplore e visualizzare i dati. È possibile connettersi facilmente tooyour Account di archiviazione di Azure e avviare rapidamente l'analisi dei dati.

Ricerca di Azure offre un [pacchetto di contenuto di Power BI](https://app.powerbi.com/getdata/services/azure-search) che consente di toomonitor e comprendere il traffico di ricerca con tabelle e grafici predefiniti. Contiene un set di report di Power BI che automaticamente la connessione dati tooyour e forniscono informazioni dettagliate visual sul servizio di ricerca. Per ulteriori informazioni, vedere hello [pagina della Guida di pacchetto di contenuto](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Dashboard di Power BI per Ricerca di Azure][4]

## <a name="next-steps"></a>Passaggi successivi
Revisione [scalare partizioni e repliche](search-limits-quotas-capacity.md) per indicazioni su come toobalance hello allocazione di partizioni e repliche per un servizio esistente.

Visitare [Amministrazione del servizio per Ricerca di Azure nel portale di Azure](search-manage.md) per altre informazioni sull'amministrazione del servizio o [Prestazioni e ottimizzazione](search-performance-optimization.md) per indicazioni sull'ottimizzazione.

Altre informazioni sulla creazione di report utili Per informazioni dettagliate, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
