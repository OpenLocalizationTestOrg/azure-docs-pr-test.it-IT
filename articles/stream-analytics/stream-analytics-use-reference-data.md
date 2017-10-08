---
title: aaaUse dati e ricerca tabelle di riferimento nel flusso Analitica | Documenti Microsoft
description: Usare i dati di riferimento in una query di Analisi di flusso
keywords: tabella di ricerca, dati di riferimento
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Uso dei dati di riferimento o delle tabelle di ricerca in un flusso di input di Analisi di flusso
Dati di riferimento (noto anche come una tabella di ricerca) sono un set di dati limitato è statico o rallentando modifica in natura, utilizza tooperform una ricerca o toocorrelate con il flusso dei dati. utilizzo di toomake di dati di riferimento nel processo Analitica di flusso di Azure, in genere si utilizzerà un [Join dei dati di riferimento](https://msdn.microsoft.com/library/azure/dn949258.aspx) nella Query. Analitica di flusso usa l'archiviazione Blob di Azure come livello di archiviazione hello per dati di riferimento e con riferimento a Data Factory di Azure i dati possono essere archiviazione Blob tooAzure trasformato e/o copiato, per utilizzarli come dati di riferimento, di [un numero qualsiasi di basato su cloud e archivi dati locali](../data-factory/data-factory-data-movement-activities.md). Dati di riferimento viene modellati come una sequenza di oggetti BLOB (definita nella configurazione di input hello) in ordine crescente di hello data/ora specificato nel nome di blob hello. Si **solo** supporta l'aggiunta di toohello fine della sequenza di hello utilizzando una data/ora **maggiore** rispetto a quello specificato dal blob ultimo hello in sequenza hello hello.

Flusso Analitica ha un **limite di 100 MB per ogni blob** ma processi possono elaborare più BLOB di riferimento utilizzando hello **il modello del percorso** proprietà.


## <a name="configuring-reference-data"></a>Configurazione dei dati di riferimento
tooconfigure i dati di riferimento, è necessario innanzitutto un input di tipo toocreate **dati di riferimento**. tabella Hello riportata di seguito viene illustrato ogni proprietà che è necessario tooprovide durante la creazione di input di dati di riferimento hello con la relativa descrizione:


<table>
<tbody>
<tr>
<td>Nome proprietà</td>
<td>Descrizione</td>
</tr>
<tr>
<td>Alias di input</td>
<td>Nome descrittivo che può essere utilizzato nei hello processo query tooreference che questo input.</td>
</tr>
<tr>
<td>Account di archiviazione</td>
<td>nome Hello hello dell'account di archiviazione in cui si trovano i BLOB. Se si trova in hello stessa sottoscrizione del processo di flusso Analitica, è possibile selezionarlo dall'elenco a discesa hello.</td>
</tr>
<tr>
<td>Chiave dell'account di archiviazione</td>
<td>chiave segreta Hello associata con l'account di archiviazione hello. Ciò viene compilata automaticamente se l'account di archiviazione hello in hello stessa sottoscrizione del processo di flusso Analitica.</td>
</tr>
<tr>
<td>Contenitore di archiviazione</td>
<td>I contenitori forniscono un raggruppamento logico dei blob archiviati nel servizio Blob di Microsoft Azure hello. Quando si carica un toohello blob del servizio Blob, è necessario specificare un contenitore per il blob.</td>
</tr>
<tr>
<td>Modello di percorso</td>
<td>Utilizzare il percorso di Hello toolocate i BLOB nel contenitore specificato hello. Nel percorso di hello, è possibile scegliere toospecify uno o più istanze di hello 2 variabili seguenti:<BR>{date}, {time}<BR>Esempio 1: products/{date}/{time}/product-list.csv<BR>Esempio 2: products/{date}/product-list.csv
</tr>
<tr>
<td>Formato data [facoltativo]</td>
<td>Se è stato usato {date} all'interno di hello il modello del percorso specificato, è possibile selezionare il formato di data hello in cui i BLOB sono organizzati da hello elenco a discesa dei formati supportati.<BR>Esempio: AAAA/MM/GG, MM/GG/AAAA e così via</td>
</tr>
<tr>
<td>Formato ora [facoltativo]</td>
<td>Se è stato usato {time} all'interno di hello il modello del percorso specificato, è possibile selezionare il formato di ora hello in cui i BLOB sono organizzati da hello elenco a discesa dei formati supportati.<BR>Esempio: HH, HH/mm o HH-mm</td>
</tr>
<tr>
<td>Formato di serializzazione eventi</td>
<td>toomake che le query funzionino come hello che previsto, flusso Analitica deve tooknow il formato di serializzazione per i flussi di dati in ingresso in uso. Per i dati di riferimento, i formati di hello supportato sono CSV e JSON.</td>
</tr>
<tr>
<td>Codifica</td>
<td>UTF-8 è hello formato di codifica è supportata solo in questo momento</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Generazione di dati di riferimento in una pianificazione
Se i dati di riferimento sono un set di dati a modifica lenta, è abilitato il supporto per l'aggiornamento dei dati di riferimento specificando un modello del percorso nella configurazione di input hello utilizzando hello {date} e il token di sostituzione {time}. Flusso Analitica preleva dalle definizioni dei dati di riferimento hello aggiornato in base a questo modello del percorso. Ad esempio, un modello di `sample/{date}/{time}/products.csv` con un formato di data **"Aaaa-MM-GG"** e un formato di ora di **"HH: mm"** indica toopick Analitica flusso BLOB hello aggiornato `sample/2015-04-16/17-30/products.csv` 5:30 PM aprile fuso orario di 16, 2015 UTC.

> [!NOTE]
> Attualmente i processi di flusso Analitica cercano aggiornamento blob hello solo quando l'ora macchina hello anticipa il tempo di toohello codificato nel nome di blob hello. Ad esempio, il processo di hello cercherà `sample/2015-04-16/17-30/products.csv` non appena possibile ma non precedente rispetto a 5:30 PM il 16 aprile 2015 UTC il fuso orario. Si verifica un *mai* cercare un blob con un tempo codificato anteriori hello ultima che viene individuato.
> 
> Ad esempio, una volta processo hello rilevata blob hello `sample/2015-04-16/17-30/products.csv` lo ignora tutti i file con una data con codifica precedente a 5:30 PM il 16 aprile 2015, pertanto se un che arrivano in ritardo `sample/2015-04-16/17-25/products.csv` blob viene creato in hello stesso processo hello contenitore non verrà utilizzate.
> 
> Allo stesso modo se `sample/2015-04-16/17-30/products.csv` viene generato solo 10:03 PM il 16 aprile 2015, ma nessun blob con una data precedente è presente nel contenitore di hello, processo hello utilizzerà questo file a partire da 10:03 PM il 16 aprile 2015 e utilizzare dati di riferimento precedente hello fino a quel momento.
> 
> Toothis un'eccezione è quando il processo di hello deve toore elaborare dati indietro nel tempo o al primo avvio processo hello. All'inizio processo hello ora esegue la ricerca di blob più recente di hello prodotti prima del processo di hello ora di inizio specificata. Questa operazione viene eseguita tooensure che vi sia un **non vuoto** fanno riferimento a set di dati quando viene avviato il processo di hello. Se non viene trovato uno, il processo di hello Visualizza hello seguente diagnostica: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) può essere utilizzato tooorchestrate hello attività di creazione BLOB hello aggiornato necessari per le definizioni dei dati di riferimento tooupdate Analitica di flusso. Data Factory è un servizio di integrazione di dati basato su cloud che Orchestra e automatizza lo spostamento di hello e trasformazione dei dati. Data Factory supporta [connessione tooa numerosi basato sul cloud e archivi dati locali](../data-factory/data-factory-data-movement-activities.md) e spostare facilmente i dati a intervalli regolari specificato. Per ulteriori informazioni e istruzioni dettagliate su come tooset di una Data Factory pipeline toogenerate dati di riferimento per Analitica di flusso che viene aggiornato a intervalli predefiniti, vedere questo [esempio GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Suggerimenti sull'aggiornamento dei dati di riferimento
1. Sovrascrivere il BLOB di dati di riferimento non comporterà Analitica flusso tooreload hello blob e in alcuni casi può causare toofail processo hello. Hello consigliabile dei dati di riferimento toochange sono tooadd un nuovo blob utilizzando hello stesso modello di contenitore e il percorso definito nell'input processo hello e utilizzano una data/ora **maggiore** rispetto a quello specificato dal blob ultimo hello in sequenza hello hello.
2. I BLOB di dati di riferimento sono **non** ordinati in base al tempo del blob hello "Ultima modifica", ma solo data specificata nel nome di blob hello utilizzando sostituzioni di {time} e {date} hello e l'ora di hello.
3. In alcuni casi un processo deve tornare indietro nel tempo, quindi i BLOB dei dati di riferimento non devono essere modificati o eliminati.

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
Sono state introdotte tooStream Analitica, un servizio gestito per lo streaming analitica dei dati di hello Internet delle cose. toolearn ulteriori informazioni su questo servizio, vedere:

* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
