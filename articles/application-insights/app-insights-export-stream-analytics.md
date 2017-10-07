---
title: aaaExport tramite flusso Analitica da Azure Application Insights | Documenti Microsoft
description: "Flusso Analitica è possibile trasformare in modo continuo, filtro e dati della route hello esportare da Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Utilizzare Analitica flusso tooprocess esportati dati da Application Insights
[Azure Analitica flusso](https://azure.microsoft.com/services/stream-analytics/) hello strumento ideale per l'elaborazione dati [esportato da Application Insights](app-insights-export-telemetry.md). L'analisi di flusso può eseguire il pull di dati da un'ampia gamma di origini. Può trasformare e filtrare i dati di hello e quindi distribuirla tooa svariati sink.

In questo esempio, si creerà un adattatore che accetta dati da Application Insights, ridenominazioni ed elabora alcuni campi, hello e invia tramite pipe a Power BI.

> [!WARNING]
> Esistono molto migliore e più facile [consigliati per i dati di Application Insights toodisplay in Power BI](app-insights-export-power-bi.md). percorso illustrato di seguito Hello è semplicemente un tooillustrate esempio tooprocess come i dati esportati.
> 
> 

![Diagramma a blocchi per l'esportazione tramite tooPBI SA](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Creare l'archivio in Azure
L'esportazione continua restituisce sempre l'account di archiviazione Azure tooan di dati, pertanto è necessario innanzitutto archiviazione hello toocreate.

1. Creare un account di archiviazione "classiche" nella sottoscrizione in hello [portale di Azure](https://portal.azure.com).
   
   ![Nel portale di Azure scegliere Nuovo, Dati, Archiviazione](./media/app-insights-export-stream-analytics/030.png)
2. Creare un contenitore
   
    ![In hello nuova risorsa di archiviazione, selezionare i contenitori, fare clic su riquadro contenitori hello, quindi su Aggiungi](./media/app-insights-export-stream-analytics/040.png)
3. Chiave di accesso di archiviazione hello copia
   
    È necessario prima tooset hello toohello input flusso analitica servizio.
   
    ![Nel servizio di archiviazione hello, aprire le impostazioni, chiavi e richiedere una copia della chiave di accesso primaria hello](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>Avviare l'esportazione continua tooAzure archiviazione
[Esportazione continua](app-insights-export-telemetry.md) sposta i dati da Application Insights nell'archiviazione di Azure.

1. Nel portale di Azure hello, Sfoglia risorsa di Application Insights toohello creata per l'applicazione.
   
    ![Scegliere Sfoglia, Application Insights e quindi l'applicazione](./media/app-insights-export-stream-analytics/050.png)
2. Creare un'esportazione continua.
   
    ![Scegliere Impostazioni, Esportazione continua, Aggiungi](./media/app-insights-export-stream-analytics/060.png)

    Selezionare l'account di archiviazione hello creato in precedenza:

    ![Set di destinazione dell'esportazione hello](./media/app-insights-export-stream-analytics/070.png)

    Impostare i tipi di evento hello da toosee:

    ![Scegliere i tipi di eventi](./media/app-insights-export-stream-analytics/080.png)

1. Lasciare che alcuni dati si accumulino. Attendere che gli utenti usino l'applicazione per qualche tempo. Verranno restituiti i dati di telemetria e sarà possibile esaminare i grafici statistici in [Esplora metriche](app-insights-metrics-explorer.md) e i singoli eventi in [Ricerca diagnostica](app-insights-diagnostic-search.md). 
   
    E inoltre dati hello esporterà tooyour archiviazione. 
2. Esaminare i dati di hello esportata. In Visual Studio, scegliere **Visualizza/Cloud Explorer**e aprire Azure/Archiviazione. (Se non si dispone di questa opzione, è necessario tooinstall hello Azure SDK: aprire finestra di dialogo Nuovo progetto hello e Visual c# / Cloud / ottenere Microsoft Azure SDK per .NET.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Prendere nota di parte in comune hello del nome di percorso hello, che viene derivato dalla chiave di nome e la strumentazione dell'applicazione hello. 

gli eventi di Hello vengono scritti i file tooblob in formato JSON. Ogni file può contenere uno o più eventi. In modo desideriamo tooread hello dati dell'evento e filtro campi hello desiderato. Sono disponibili tutti i tipi di operazioni che è possibile farlo con dati hello, ma il piano è oggi toouse flusso Analitica toopipe hello dati tooPower BI.

## <a name="create-an-azure-stream-analytics-instance"></a>Creare un'istanza di analisi di flusso di Azure
Da hello [portale di Azure classico](https://manage.windowsazure.com/), selezionare il servizio di Azure flusso Analitica hello e creare un nuovo processo di flusso Analitica:

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Quando viene creato il nuovo processo di hello, espandere i dettagli:

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Impostare il percorso BLOB
Impostarlo input tootake dal blob di esportazione continua:

![](./media/app-insights-export-stream-analytics/120.png)

A questo punto è necessario hello chiave di accesso primaria dall'Account di archiviazione, annotati in precedenza. Impostare come hello chiave Account di archiviazione.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Impostare lo schema prefisso percorso
![](./media/app-insights-export-stream-analytics/140.png)

**Impossibile verificare tooset hello formato data tooYYYY-MM-GG (con i trattini).**

Hello modello prefisso del percorso specifica in cui flusso Analitica Individua file di input hello nel servizio di archiviazione hello. È necessario tooset è toohow toocorrespond esportazione continua archivia dati hello. Impostarlo come segue:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Esempio:

* `webapplication27`è il nome di hello della risorsa di Application Insights hello **lettere minuscole**.
* `1234...`è la chiave di strumentazione hello della risorsa di Application Insights, hello **l'omissione di trattini**. 
* `PageViews`hello tipo di dati si desidera tooanalyze. tipi di Hello disponibili dipendono dal filtro hello impostato nell'esportazione continua. Esaminare altri tipi disponibili di hello toosee di dati esportati hello e vedere hello [Esporta modello di dati](app-insights-export-data-model.md).
* `/{date}/{time}` è uno schema scritto letteralmente.

> [!NOTE]
> Controllare toomake archiviazione hello si ottiene il percorso di hello destra.
> 
> 

### <a name="finish-initial-setup"></a>Completare l'installazione iniziale
Verificare il formato di serializzazione hello:

![Confermare e chiudere la procedura guidata](./media/app-insights-export-stream-analytics/150.png)

Chiudere la procedura guidata hello e attendere hello toocomplete di programma di installazione.

> [!TIP]
> Utilizzare toodownload comando di esempio hello alcuni dati. Mantenerlo come un toodebug di esempio di test della query.
> 
> 

## <a name="set-hello-output"></a>Output di hello set
Selezionare il processo e impostare l'output di hello.

![Selezionare il nuovo canale di hello, fare clic su output, Add, Power BI](./media/app-insights-export-stream-analytics/160.png)

Fornire il **di lavoro o scuola account** tooauthorize tooaccess Analitica di flusso della risorsa di Power BI. Creare quindi un nome per l'output di hello e per la tabella e il set di dati di hello destinazione Power BI.

![Inventare tre nomi](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>Set hello query
query Hello regola traduzione hello da toooutput input.

![Selezionare il processo di hello e fare clic su Query. Incollare l'esempio hello riportato di seguito.](./media/app-insights-export-stream-analytics/180.png)

Utilizzare hello toocheck di funzione di Test che si otterrà un output di destra hello. Assegnare i dati di esempio hello impiegato dalla pagina input hello. 

### <a name="query-toodisplay-counts-of-events"></a>Query toodisplay conteggi di eventi
Incollare questa query:

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* input di esportazione è alias hello è stato assegnato l'input del flusso toohello
* output di PBI è l'alias di output di hello è definiti
* Utilizziamo [OUTER GetElements applicare](https://msdn.microsoft.com/library/azure/dn706229.aspx) nome di evento hello è in un arrray JSON annidati. Quindi seleziona selezionare hello hello nome dell'evento, con un conteggio del numero di hello di istanze con lo stesso nome in hello periodo di tempo. Hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clausola Raggruppa elementi hello in periodi di tempo di 1 minuto.

### <a name="query-toodisplay-metric-values"></a>Valori della metrica toodisplay query
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* Questa query drill-ora dell'evento hello tooget telemetria metriche hello e valore della metrica hello. valori della metrica Hello sono all'interno di una matrice, righe di hello OUTER GetElements Applica modello tooextract hello permette di usare. in questo caso, "myMetric" è il nome di hello della metrica di hello. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>Valori delle proprietà di dimensione tooinclude di query
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* La query include i valori delle proprietà di dimensione hello senza in base a una dimensione specifica in un indice nella matrice di dimensione hello fisso.

## <a name="run-hello-job"></a>Eseguire il processo di hello
È possibile selezionare una data in hello oltre toostart hello processo da. 

![Selezionare il processo di hello e fare clic su Query. Incollare l'esempio hello riportato di seguito.](./media/app-insights-export-stream-analytics/190.png)

Attendere fino a quando non è in esecuzione il processo di hello.

## <a name="see-results-in-power-bi"></a>Visualizzare i risultati in Power BI
> [!WARNING]
> Esistono molto migliore e più facile [consigliati per i dati di Application Insights toodisplay in Power BI](app-insights-export-power-bi.md). percorso illustrato di seguito Hello è semplicemente un tooillustrate esempio tooprocess come i dati esportati.
> 
> 

Aprire Power BI con l'account dell'istituto di istruzione e set di dati selezionare hello e o tabella in cui è definito come output di hello del processo di flusso Analitica hello.

![In Power BI selezionare il set di dati e i campi.](./media/app-insights-export-stream-analytics/200.png)

È ora possibile usare questo set di dati nei report e nei dashboard in [Power BI](https://powerbi.microsoft.com).

![In Power BI selezionare il set di dati e i campi.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>Dati non visualizzati
* Verificare che si [formato di data set hello](#set-path-prefix-pattern) correttamente tooYYYY-MM-GG (con i trattini).

## <a name="video"></a>Video
Noam Ben Zeev viene illustrata la modalità di esportazione di dati tramite flusso Analitica tooprocess.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Esportazione continua](app-insights-export-telemetry.md)
* [Riferimento per i tipi di proprietà hello e i valori del modello di dati dettagliati.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

