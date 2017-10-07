---
title: contatori aaaPerformance in Application Insights | Documenti Microsoft
description: Sistema di monitoraggio e contatori delle prestazioni .NET personalizzati in Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a>Contatori delle prestazioni di sistema in Application Insights
Windows offre un'ampia gamma di [contatori delle prestazioni](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), ad esempio su occupazione della CPU, memoria, disco e utilizzo di rete. È anche possibile definire contatori personalizzati. [Application Insights](app-insights-overview.md) consente di visualizzare i contatori delle prestazioni se l'applicazione è in esecuzione in IIS in un toowhich di host o macchina virtuale locale si dispone dell'accesso amministrativo. grafici di Hello indicano un'applicazione in tempo reale hello risorse tooyour disponibili e possono semplificare tooidentify sbilanciamento del carico tra le istanze del server.

I contatori delle prestazioni vengono visualizzati nel Pannello di server hello, che include una tabella che Segmenta dall'istanza del server.

![Contatori delle prestazioni segnalati in Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

I contatori delle prestazioni non sono disponibili per App Web di Azure. Ma è possibile [inviare informazioni di diagnostica Azure tooApplication](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>Visualizzare i contatori
Pannello server Hello viene illustrato un set predefinito di contatori delle prestazioni. 

toosee altri contatori, modificare i grafici di hello nel pannello server hello o aprire una nuova [Esplora metriche](app-insights-metrics-explorer.md) pannello e aggiungere nuovi grafici. 

contatori di Hello disponibili sono elencati come metriche quando si modifica un grafico.

![Contatori delle prestazioni segnalati in Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

creare tutti i grafici più utili in un'unica posizione, toosee un [dashboard](app-insights-dashboards.md) e aggiungerli tooit.

## <a name="add-counters"></a>Aggiungere contatori
Se il contatore delle prestazioni hello desiderato non è visualizzato nell'elenco di hello delle metriche, sono perché hello Application Insights SDK non è raccolta nel server web. È possibile configurarlo toodo così.

1. Scoprire quali i contatori sono disponibili nel server tramite questo comando di PowerShell nel server di hello:
   
    `Get-Counter -ListSet *`
   
    Vedere [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).
2. Aprire ApplicationInsights.config.
   
   * Se si aggiungono Application Insights tooyour app durante lo sviluppo, modificare Applicationinsights nel progetto e quindi ridistribuirlo tooyour server.
   * Se si utilizza monitoraggio stato tooinstrument un'app web in fase di esecuzione, è possibile trovare Applicationinsights nella directory radice hello dell'app hello in IIS. Aggiornarlo qui in ogni istanza del server.
3. Modifica della direttiva di agente di raccolta dati prestazioni hello:
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

È possibile acquisire contatori standard e quelli implementati manualmente. `\Objects\Processes` è un esempio di contatore standard, disponibile in tutti i sistemi Windows. `\Sales(photo)\# Items Sold` è un esempio di contatore personalizzato che può essere implementato in un servizio Web. 

formato hello è `\Category(instance)\Counter"`, o per le categorie che non includono istanze, semplicemente `\Category\Counter`.

`ReportAs`è necessario per i nomi dei contatori che non corrispondono a `[a-zA-Z()/-_ \.]+` -, ovvero contengono caratteri che non si trovano in hello set seguenti: lettere, arrotondare tra parentesi quadre, barra (/), trattino, carattere di sottolineatura, spazio, punto.

Se si specifica un'istanza, verranno raccolti come una dimensione "CounterInstanceName" di hello riportato metrica.

### <a name="collecting-performance-counters-in-code"></a>Raccogliere contatori delle prestazioni nel codice
le prestazioni del sistema toocollect contatori e inviarle tooApplication Insights, è possibile adattare frammento hello seguente:


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

Oppure è possibile eseguire la stessa cosa con metriche personalizzate creato hello:

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Contatori delle prestazioni in Analytics
È possibile cercare e visualizzare report dei contatori delle prestazioni in [Analytics](app-insights-analytics.md).

Hello **performanceCounters** schema espone hello `category`, `counter` nome, e `instance` nome di ogni contatore delle prestazioni.  Nei dati di telemetria hello per ogni applicazione, verrà visualizzato solo i contatori di hello per tale applicazione. Ad esempio, toosee i contatori sono disponibili: 

![Contatori delle prestazioni in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-performance-counters.png)

("Instance" qui si riferisce toohello istanza del contatore delle prestazioni, non hello istanza macchina ruolo o del server. nome dell'istanza del contatore delle prestazioni Hello in genere i segmenti di contatori, ad esempio il tempo del processore in base al nome hello del processo di hello o dell'applicazione.)

un grafico di memoria disponibile nel periodo recente hello tooget: 

![Timechart delle metriche in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-available-memory.png)

Come altri dati di telemetria, **performanceCounters** contiene anche una colonna `cloud_RoleInstance` che indica l'identità di hello hello server dell'istanza dell'host in cui l'app è in esecuzione. Ad esempio, toocompare hello prestazioni dell'app in computer diversi hello: 

![Prestazioni segmentate per istanze del ruolo in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>Conteggi di ASP.NET e Application Insights
*Qual è la differenza hello tra velocità eccezione hello e metriche eccezioni?*

* *Tasso di eccezione* è un contatore delle prestazioni del sistema. Hello CLR conta hello gestite le eccezioni non gestite che vengono generate e divide totale hello in un intervallo di campionamento per lunghezza hello dell'intervallo di hello. raccoglie il risultato Hello Application Insights SDK e lo invia toohello portale.
* *Eccezioni* è un conteggio di hello TrackException report ricevuti dal portale hello nell'intervallo di campionamento hello del grafico hello. Include solo hello gestite le eccezioni in cui è stato scritto TrackException chiama nel codice e non include tutti [le eccezioni non gestite](app-insights-asp-net-exceptions.md). 

## <a name="alerts"></a>Avvisi
Ad esempio altre metriche, è possibile [impostare un avviso](app-insights-alerts.md) toowarn se un contatore delle prestazioni è di fuori di un limite specificato. Aprire il pannello di avvisi hello e fare clic su Aggiungi avviso.

## <a name="next"></a>Passaggi successivi
* [Rilevamento delle dipendenze](app-insights-asp-net-dependencies.md)
* [Rilevamento delle eccezioni](app-insights-asp-net-exceptions.md)

