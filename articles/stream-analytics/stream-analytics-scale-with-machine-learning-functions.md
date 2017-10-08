---
title: "scalabilità con funzioni Analitica di flusso di Azure e Azure ml aaaJob | Documenti Microsoft"
description: "Informazioni su come tooproperly ridimensionare i processi di flusso Analitica (partizionamento, SU quantità e altro ancora) quando si utilizzano funzioni di Azure Machine Learning."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Ridimensionare il processo di Analisi di flusso con funzioni di Azure Machine Learning
È spesso molto semplice tooset backup di un processo di flusso Analitica e attraversare alcuni dati di esempio. Cosa è necessario creare quando è necessario toorun hello stesso processo con volume di dati maggiore? Richiede Microsoft toounderstand come tooconfigure hello Analitica di flusso del processo in modo che consente di scalare. In questo documento, esamineremo hello speciali aspetti ridimensionamento Analitica flusso i processi con funzioni di Machine Learning. Per informazioni su come i processi di flusso Analitica tooscale in genere vedere l'articolo di hello [scalabilità dei processi](stream-analytics-scale-jobs.md).

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>Che cos'è una funzione di Azure Machine Learning in Analisi di flusso?
Una funzione di Machine Learning in flusso Analitica può essere utilizzata come una normale chiamata di funzione nel linguaggio di query flusso Analitica hello. Dietro la scena hello, tuttavia, le chiamate di funzione hello sono effettivamente le richieste di servizio Web di Azure Machine Learning. Machine Learning ai servizi web "batch", più righe, che viene chiamato batch minima, in hello stesso web chiamata API al servizio, tooimprove velocità effettiva complessiva. Vedere i seguenti articoli per altri dettagli; hello [Le funzioni di azure Machine Learning in flusso Analitica](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) e [servizi Web di Azure Machine Learning](../machine-learning/machine-learning-consume-web-services.md).

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Configurare un processo di Analisi di flusso con funzioni di Machine Learning
Quando si configura una funzione di Machine Learning per il processo di flusso Analitica, esistono due parametri tooconsider, dimensioni dei batch hello di chiamate di funzione di Machine Learning hello hello unità (SUs), il provisioning per il processo di flusso Analitica hello di streaming. toodetermine hello i valori appropriati per questi, prima di tutto un occorre tra la latenza e velocità effettiva, vale a dire, latenza del processo di flusso Analitica hello e la velocità effettiva di ogni SU. SUs possono essere aggiunti sempre velocità effettiva di tooincrease processo tooa di una query con partizionamento efficiente flusso Analitica, sebbene SUs aggiuntive aumento del costo di hello di processo hello in esecuzione.

È pertanto importante toodetermine hello *tolleranza* di latenza in esecuzione un processo di flusso Analitica. Latenza aggiuntiva dall'esecuzione di richieste di servizio di Azure Machine Learning naturalmente aumenterà con dimensioni di batch, che verranno composto latenza hello del processo di flusso Analitica hello. Invece, l'aumento delle dimensioni del batch hello consente hello Analitica flusso processo tooprocess * più eventi con hello *stesso numero* di Machine Learning richieste di servizio web. Spesso il hello aumento della latenza di servizio web Machine Learning è Sub lineare toohello aumento delle dimensioni di batch, pertanto è importante tooconsider hello più dimensioni del batch per un servizio web Machine Learning in qualsiasi situazione specificata. dimensioni di batch Hello predefinite per il servizio web hello richieste è 1000 e può essere modificato tramite l'utilizzo di hello [API REST di flusso Analitica](https://msdn.microsoft.com/library/mt653706.aspx "API REST di flusso Analitica") o hello [PowerShell client per flusso Analitica](stream-analytics-monitor-and-manage-jobs-use-powershell.md "client di PowerShell per Analitica flusso").

Dopo aver determinato un batch di dimensioni, quantità hello di streaming unità (SUs) può essere determinata, in base hello numero di eventi che la funzione hello deve tooprocess al secondo. Per altre informazioni sulle unità di streaming, vedere [Processi di scalabilità di Analisi di flusso](stream-analytics-scale-jobs.md).

In generale, vi sono 20 connessioni simultanee servizio web di Machine Learning toohello per ogni 6 SUs, ad eccezione del fatto che i processi di SU 1 e 3 SU verrà visualizzato anche 20 connessioni simultanee.  Se, ad esempio, velocità di dati di input hello è 200.000 eventi al secondo e dimensioni del batch hello viene lasciata toohello predefinito è 1000 hello risultante web servizio latenza con mini-batch di 1000 eventi è 200 ms. Ciò significa che ogni connessione può effettuare 5 richieste toohello servizio web di Machine Learning in un secondo. Con 20 connessioni, il processo di flusso Analitica hello può elaborare 20.000 eventi in 200 ms e pertanto a 100.000 eventi in un secondo. Pertanto tooprocess 200.000 eventi al secondo, il processo di flusso Analitica hello deve 40 connessioni simultanee, ossia too12 SUs. diagramma di Hello seguente illustra le richieste di hello hello Analitica flusso processo toohello Machine Learning endpoint di servizio web: ogni 6 SUs include servizio web di Learning tooMachine di 20 connessioni simultanee a max.

![Esempio di processo per ridimensionare Analisi di flusso con funzioni di Machine Learning 2](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "Esempio di processo per ridimensionare Analisi di flusso con funzioni di Machine Learning 2")

In generale, ***B*** per le dimensioni del batch, ***L*** per la latenza di servizio web hello dimensioni batch B in millisecondi, hello velocità effettiva di un processo di flusso Analitica con ***N*** SUs è:

![Formula per ridimensionare Analisi di flusso con funzioni di Machine Learning](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "Formula per ridimensionare Analisi di flusso con funzioni di Machine Learning")

Un'ulteriore considerazione potrebbe essere hello 'max concurrent calls' sul lato servizio web di Machine Learning hello, si consiglia di tooset questo valore massimo toohello (attualmente 200).

Per ulteriori informazioni su questa impostazione Controlla hello [articolo Scaling per servizi Web di Machine Learning](../machine-learning/machine-learning-scaling-webservice.md).

## <a name="example--sentiment-analysis"></a>Esempio: Analisi di valutazione
Hello esempio seguente include un processo di flusso Analitica con l'analisi del sentiment hello funzione Machine Learning, come descritto in hello [esercitazione integrazione flusso Analitica Machine Learning](stream-analytics-machine-learning-integration-tutorial.md).

query Hello è una semplice query completamente partizionata seguita da hello **sentiment** funzione, come illustrato di seguito:

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Prendere in considerazione hello seguente scenario. con una velocità effettiva di 10.000 TWEET al secondo un processo di flusso Analitica è necessario creare analisi del sentiment tooperform di tweet hello (eventi). Utilizzando 1 SU, il processo di flusso Analitica possibile toohandle in grado di traffico di hello? Utilizzando dimensioni batch predefinito di hello del processo di hello 1000 dovrebbe essere in grado di tookeep backup con input hello. Ulteriore hello aggiunto funzione Machine Learning deve generare non più di un secondo di latenza, ovvero la latenza hello predefinita generale di analisi del sentiment hello servizio web Machine Learning (con una dimensione di batch predefinito di 1000). processo di Hello Analitica flusso **complessivo** o latenza end-to-end in genere pochi secondi. Eseguire un'analisi più approfondita in questo processo di flusso Analitica, *particolarmente* hello chiamate di funzione di Machine Learning. Con dimensioni di batch hello 1000, una velocità effettiva di 10.000 eventi richiederà circa 10 richieste tooweb servizio. Anche con 1 SU, sono disponibili sufficienti tooaccommodate connessioni simultanee del traffico di input.

Ma cosa accade se aumenta la frequenza di eventi di input hello x 100 e ora il processo di flusso Analitica hello deve tooprocess 1.000.000 TWEET al secondo? Sono disponibili due opzioni:

1. Aumentare la dimensione di batch hello, o
2. Eventi partizione hello flusso di input tooprocess hello in parallelo

Con l'opzione prima di hello, hello processo **latenza** aumenterà.

Con l'opzione secondo hello, SUs ulteriori sarebbe necessario toobe il provisioning e pertanto genera simultanea di più richieste di servizio web Machine Learning. Ciò significa che il processo di hello **costo** aumenterà.

Si supponga di latenza hello di analisi del sentiment hello servizio web Machine Learning è 200 ms per i batch di 1000 eventi o di sotto, 250ms per i batch 5.000 eventi 300 MS di batch di eventi di 10.000 o 500ms per i batch di eventi di 25.000.

1. Opzione hello prima, (**non** provisioning più SUs), potrebbero aumentare le dimensioni di batch hello troppo**25.000**. Ciò a sua volta consente hello processo tooprocess 1.000.000 eventi con 20 connessioni simultanee toohello servizio web Machine Learning (con una latenza di 500 ms per ogni chiamata). Pertanto hello latenza aggiuntiva del processo di flusso Analitica hello a causa di richieste di funzione sentiment toohello contro hello aumenterebbe da richieste di servizio web di Machine Learning **200 ms** troppo**500ms**. Si noti, tuttavia, tali dimensioni di batch **Impossibile** aumentato all'infinito come servizi web Machine Learning hello richiede hello payload dimensioni di una richiesta di 4 MB o più piccolo web timeout delle richieste di servizio dopo 100 secondi dell'operazione.
2. Opzione hello secondo, dimensioni del batch hello viene lasciata 1000, con una latenza di servizio web di 200 ms, tutti i servizi web toohello 20 connessioni simultanee sarebbe in grado di tooprocess 1000 * 20 * 5 eventi = 100.000 al secondo. Pertanto gli eventi di 1.000.000 tooprocess per processo hello secondo, sarebbe necessario 60 SUs. Toohello confrontati prima opzione Analitica flusso processo renderebbe più web evadere le richieste batch, a sua volta la generazione di un aumento dei costi.

Di seguito è una tabella per la velocità effettiva di hello del processo di flusso Analitica hello per SUs diverso e le dimensioni di batch (in numero di eventi al secondo).

| Dimensioni batch (latenza ML) | 500 (200 ms) | 1.000 (200 ms) | 5.000 (250 ms) | 10.000 (300 ms) | 25.000 (500 ms) |
| --- | --- | --- | --- | --- | --- |
| **1 unità di archiviazione** |2.500 |5.000 |20.000 |30.000 |50.000 |
| **3 unità di archiviazione** |2.500 |5.000 |20.000 |30.000 |50.000 |
| **6 unità di archiviazione** |2.500 |5.000 |20.000 |30.000 |50.000 |
| **12 unità di archiviazione** |5.000 |10.000 |40.000 |60.000 |100.000 |
| **18 unità di archiviazione** |7.500 |15.000 |60.000 |90.000 |150.000 |
| **24 unità di archiviazione** |10.000 |20.000 |80.000 |120.000 |200.000 |
| **…** |… |… |… |… |… |
| **60 unità di archiviazione** |25.000 |50.000 |200.000 |300.000 |500.000 |

A questo punto dovrebbe essere chiaro il funzionamento delle funzioni di Machine Learning in Analisi di flusso. È probabile che anche comprendere che "pull" di dati da origini dati e ogni "pull" restituisce un batch di eventi per i processi di flusso Analitica hello tooprocess processo flusso Analitica. Impatto di richieste del servizio web Machine Learning hello modello pull

In genere, le dimensioni di batch hello che è impostati per le funzioni di Machine Learning sarà esattamente divisibile per hello numero di eventi restituiti da ogni processo di flusso Analitica "pull". Quando ciò si verifica con batch "parziale" verrà chiamato il servizio web Machine Learning hello. Questa operazione viene eseguita toonot comportano la latenza di processi aggiuntivi overhead negli eventi coalescing da toopull pull.

## <a name="new-function-related-monitoring-metrics"></a>Nuove metriche di monitoraggio correlate alle funzioni
Nell'area di monitoraggio di un processo di flusso Analitica hello, sono state aggiunte tre altre metriche correlate alla funzione. Sono le richieste di funzioni, gli eventi di funzione e richieste non riuscite di funzione, come illustrato nella figura hello riportato di seguito.

![Metriche per ridimensionare Analisi di flusso con funzioni di Machine Learning](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "Metriche per ridimensionare Analisi di flusso con funzioni di Machine Learning")

Hello sono definiti come segue:

**Le richieste di funzioni**: hello numero di richieste di funzione.

**Eventi relativi a funzioni**: numero di eventi hello in hello funzioni richieste.

**RICHIESTE non riuscite di funzione**: hello numero di richieste di funzione non riuscita.

## <a name="key-takeaways"></a>Risultati principali
toosummarize punti principali hello, in ordine tooscale un processo di flusso Analitica con funzioni di Machine Learning, hello seguenti elementi da considerare:

1. frequenza degli eventi di input Hello
2. Hello tollerata latenza per l'esecuzione del processo di flusso Analitica hello (e pertanto le dimensioni di batch hello del servizio web di Machine Learning hello richieste)
3. il provisioning di Hello flusso Analitica SUs e il numero di hello delle richieste di servizio web Machine Learning (hello correlati alla funzione costi aggiuntivi)

È stata usata come esempio una query di Analisi di flusso completamente partizionata. Se è necessaria una query più complessa hello [forum di Azure flusso Analitica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) è un'ottima risorsa per ottenere ulteriori informazioni dal team di flusso Analitica hello.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su Analitica di flusso, vedere:

* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
