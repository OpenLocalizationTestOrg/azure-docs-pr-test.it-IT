---
title: Analisi degli eventi dell'infrastruttura di servizio con Application Insights aaaAzure | Documenti Microsoft
description: Informazioni sulla visualizzazione e l'analisi di eventi con Application Insights per il monitoraggio e la diagnostica dei cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Analisi e visualizzazione degli eventi con Application Insights

Azure Application Insights è una piattaforma estendibile per la diagnostica e il monitoraggio dell'applicazione. Include un potente strumento di analisi ed esecuzione di query, visualizzazione e dashboard personalizzabili e altre opzioni tra cui gli avvisi automatizzati. È consigliata piattaforma per il monitoraggio e diagnostica per servizi e applicazioni di Service Fabric hello.

## <a name="setting-up-application-insights"></a>Configurazione di Application Insights

### <a name="creating-an-ai-resource"></a>Creazione di una risorsa AI

risorsa toocreate AI, head toohello Azure Marketplace e cercare "Application Insights". È necessario visualizzate come prima soluzione hello (si trova nella categoria "Web + Mobile"). Fare clic su **crea** quando si sta esaminando risorsa destro hello (verificare che il percorso corrisponde a immagine hello riportata di seguito).

![Nuova risorsa di Application Insights](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

È necessario toofill out alcune risorse di informazioni tooprovision hello correttamente. In hello *tipo di applicazione* campo, utilizzare "Applicazione web ASP.NET" Se si intende utilizzare uno qualsiasi di Service Fabric del modelli di programmazione o la pubblicazione di un cluster di toohello applicazione .NET. Se si intende distribuire contenitori e file eseguibili guest, usare "Generale". Predefinito toousing "Applicazione web ASP.NET" tookeep in generale, le opzioni di aprire in hello future. nome Hello è tooyour preferenza e sia il gruppo di risorse hello e la sottoscrizione siano modificabile post-distribuzione della risorsa hello. È consigliabile che la risorsa AI sia in hello stesso gruppo di risorse del cluster. Per altre informazioni, vedere [Creare una risorsa di Application Insights](../application-insights/app-insights-create-new-resource.md)

È necessario hello chiave di strumentazione AI tooconfigure AI con lo strumento di aggregazione di evento. Una volta configurata la risorsa AI è (richiede alcuni minuti dopo la convalida di distribuzione hello), passare tooit e trovare hello **proprietà** sezione hello barra di spostamento a sinistra. Verrà visualizzato un nuovo pannello che mostra una *CHIAVE DI STRUMENTAZIONE*. Se è necessario sottoscrizione hello toochange o gruppo di risorse della risorsa hello, può essere eseguita in questo caso anche.

### <a name="configuring-ai-with-wad"></a>Configurazione di AI con WAD

Esistono due modi principali dati toosend di WAD tooAzure AI, ottenuto mediante l'aggiunta di una configurazione di WAD AI sink toohello, come descritto in dettaglio nella [questo articolo](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Aggiungere una chiave di strumentazione AI durante la creazione di un cluster nel portale di Azure

![Aggiunta di un AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

Quando si crea un cluster, se è attivata la diagnostica "On", verrà visualizzato un campo facoltativo di tooenter una chiave di strumentazione di Application Insights. Se si incolla qui il IKey AI, sink hello AI verrà automaticamente configurato per consentire in modello di gestione risorse hello toodeploy utilizzati il cluster.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Aggiungere modello di gestione risorse AI Sink toohello hello

In hello "WadCfg" del modello di gestione risorse di hello, aggiungere "Sink" includendo hello seguenti due modifiche:

1. Aggiungere hello sink configurazione:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Includere hello Sink in hello DiagnosticMonitorConfiguration aggiungendo hello successiva riga in "DiagnosticMonitorConfiguration" di "WadCfg" hello:

    ```json
    "sinks": "applicationInsights"
    ```

In entrambi i frammenti di codice hello sopra, hello "applicationInsights" nome era sink hello toodescribe utilizzato. Questo non è un requisito e come nome di hello del sink hello è incluso in "sink", è possibile impostare tooany stringa del nome di hello.

Attualmente, i registri dal cluster hello verranno visualizzati come tracce nel Visualizzatore di log del AI. Poiché la maggior parte delle tracce hello provenienti da piattaforma hello è di livello "Informativo", è anche possibile provare a modificare registri hello sink configurazione tooonly trasmissione di tipo "Critico" o "Error". Questa operazione può essere eseguita aggiungendo sink tooyour "Canali", come illustrato in [questo articolo](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Se si utilizza un IKey AI errato nel portale o nel modello di gestione risorse, sarà necessario toomanually Modifica chiave hello e aggiornare il cluster hello / ridistribuirla. 

### <a name="configuring-ai-with-eventflow"></a>Configurazione di AI con EventFlow

Se si utilizza EventFlow tooaggregate eventi, assicurarsi che tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`pacchetto NuGet. seguente Hello è incluso in hello toobe *restituisce* sezione di hello *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Apportare modifiche di hello necessario toomake che nei filtri, nonché includere tutti gli altri input (insieme ai rispettivi pacchetti NuGet).

## <a name="aisdk"></a>AI.SDK

Si consiglia in genere toouse EventFlow e WAD come soluzioni di aggregazione, perché consentono un toodiagnostics approccio più modulare e non monitoraggio, ad esempio se si desidera toochange l'output da EventFlow, richiede tooyour alcuna modifica effettiva strumentazione, solo un file di configurazione tooyour semplice modifica. Se, tuttavia, si decide tooinvest con Application Insights e non sono probabilmente toochange tooa altra piattaforma, è consigliabile esaminare tramite AI nuovo SDK per l'aggregazione degli eventi e inviarli tooAI. Ciò significa che non sarà più possibile tooconfigure EventFlow toosend tooAI i dati, ma invece installerà pacchetto NuGet di Service Fabric del ApplicationInsight hello. Sono disponibili informazioni dettagliate sul pacchetto hello [qui](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Application Insights il supporto per i contenitori e Microservizi](https://azure.microsoft.com/app-insights-microservices/) vengono mostrate alcune hello nuove funzionalità che si sta lavorando (ancora attualmente in versione beta), che consentono di toohave più ricco di dialogo Opzioni di monitoraggio con AI. Sono inclusi il rilevamento delle dipendenze (utilizzato nella creazione di un AppMap di tutti i servizi e applicazioni in un cluster e hello comunicazione fra di esse) e una migliore correlazione di tracce provenienti dai servizi (tal modo è possibile una migliore individuazione di un problema di hello flusso di lavoro di un'applicazione o servizio).

Se si sviluppa in .NET e verrà probabilmente usato alcuni dei modelli di programmazione dell'infrastruttura servizio e sono disposti toouse AI come piattaforma per la visualizzazione e analisi dei dati di evento e di log, si consiglia di utilizzare attraverso hello route AI SDK come il monitoraggio e flusso di lavoro di diagnostica. Lettura [questo](../application-insights/app-insights-asp-net-more.md) e [questo](../application-insights/app-insights-asp-net-trace-logs.md) tooget introduttive sull'utilizzo AI toocollect e visualizzare i log.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Esplorazione della risorsa AI hello nel portale di Azure

Dopo aver configurato AI come output per gli eventi e registri, informazioni devono avviare tooshow nella risorsa AI tra qualche minuto. Passare toohello AI risorsa alla quale avrà si toohello AI dashboard risorse. Fare clic su **ricerca** hello AI barra delle applicazioni toosee hello più recente tracce che ha ricevuto e toofilter in grado di toobe al loro interno.

*Esplora metriche* è uno strumento utile per la creazione di dashboard personalizzati in base alle metriche che possono essere segnalate da applicazioni, servizi e cluster. Vedere [esplorazione metriche in Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset backup alcuni grafici per se stessi in base ai dati di hello raccogliere.

Fare clic su **Analitica** si passerà portale Application Insights Analitica toohello, in cui è possibile eseguire query eventi e le tracce con ambito e Facoltatività maggiori. Per altre informazioni su questo argomento leggere [Analytics in Application Insights](../application-insights/app-insights-analytics.md) (Analisi in Application Insights).

## <a name="next-steps"></a>Passaggi successivi

* [Impostazione di avvisi in AI](../application-insights/app-insights-alerts.md) toobe informato delle modifiche nell'utilizzo o di prestazioni
* [Rilevamento in Application Insights smart](../application-insights/app-insights-proactive-diagnostics.md) esegue un'analisi proattiva dei dati di telemetria hello inviati tooAI toowarn di potenziali problemi di prestazioni
