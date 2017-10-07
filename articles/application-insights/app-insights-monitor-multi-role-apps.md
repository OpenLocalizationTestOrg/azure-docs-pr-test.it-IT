---
title: "aaaAzure Application Insights il supporto per più componenti, microservizi e contenitori | Documenti Microsoft"
description: "Monitoraggio di applicazioni costituite da più componenti o ruoli per le prestazioni e l'uso."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>Monitorare le applicazioni multi-componente con Application Insights (anteprima)

È possibile monitorare le app che sono costituite da più componenti, ruoli o servizi del server con [Azure Application Insights](app-insights-overview.md). stato di Hello dei componenti di hello e le reciproche relazioni hello vengono visualizzati in un singolo mapping di applicazioni. È possibile tracciare le singole operazioni tramite più componenti con correlazione automatica HTTP. È possibile integrare e correlare la diagnostica del contenitore con i dati di telemetria dell'applicazione. Utilizzare una singola risorsa di Application Insights per tutti i componenti dell'applicazione hello. 

![Mappa dell'applicazione multi-componente](./media/app-insights-monitor-multi-role-apps/app-map.png)

Utilizziamo 'componente' toomean qui qualsiasi parte di un'applicazione di grandi dimensioni funzionante. Ad esempio, una tipica applicazione aziendale può essere costituito da codice client in esecuzione nel browser, parlando tooone o più servizi web di app, che a sua volta utilizza nuovamente terminano i servizi. I componenti del server possono essere ospitato localmente nel cloud hello, potrebbero essere Azure ruoli web e di lavoro o possono essere eseguite in contenitori, ad esempio Docker o Service Fabric. 

### <a name="sharing-a-single-application-insights-resource"></a>Condivisione di una singola risorsa di Application Insights 

chiave tecnica qui Hello è telemetria toosend da ogni componente di toohello l'applicazione stessa risorsa di Application Insights, ma utilizzare hello `cloud_RoleName` componenti toodistinguish di proprietà quando necessario. Hello Application Insights SDK aggiunge hello `cloud_RoleName` creare componenti di telemetria toohello di proprietà. Ad esempio, hello SDK si aggiungerà un nome del sito web o servizio ruolo nome toohello `cloud_RoleName` proprietà. È possibile eseguire l'override di questo valore con un Telemetryinitializer. Hello mappa delle applicazioni utilizza hello `cloud_RoleName` componenti hello tooidentify di proprietà sulla mappa hello.

Per ulteriori informazioni su come eseguire l'override hello `cloud_RoleName` vedere proprietà [aggiungere proprietà: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

In alcuni casi, ciò potrebbe non essere appropriato e potrebbe essere preferibile toouse risorse diverse per diversi gruppi di componenti. È ad esempio, potrebbe essere necessario toouse diverse risorse per la gestione o ai fini della fatturazione. Utilizzo di risorse separate significa che non viene visualizzato tutti i componenti di hello visualizzati in un singolo mapping di applicazioni; e che è possibile eseguire query tra componenti [Analitica](app-insights-analytics.md). È inoltre possibile tooset delle risorse separato hello.

Con tale problema, si presupporrà che il resto di hello di questo documento che si desidera toosend dati da più componenti tooone risorsa di Application Insights.

## <a name="configure-multi-component-applications"></a>Configurare le applicazioni multi-componente

eseguire il mapping di un'applicazione con più componente tooget, è necessario tooachieve questi obiettivi:

* **Installare la versione precedente più recente di hello** pacchetto Application Insights in ogni componente dell'applicazione hello. 
* **Condividere una singola risorsa di Application Insights** per tutti i componenti dell'applicazione di hello.
* **Abilitare multi-ruolo applicazione mappa** nel Pannello di anteprime hello.

Configurare ogni componente dell'applicazione metodo hello appropriato per il relativo tipo. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)

### <a name="1-install-hello-latest-pre-release-package"></a>1. Installare il pacchetto di pre-release più recente di hello

Aggiornare o installare i pacchetti hello Application Insights nel progetto hello per ogni componente. Se si usa Visual Studio:

1. Fare clic con il pulsante destro del mouse sul progetto e selezionare **Gestisci pacchetti NuGet**. 
2. Selezionare **Includi versione preliminare**.
3. Se i pacchetti di Application Insights vengono visualizzati negli aggiornamenti, selezionarli. 

    In caso contrario, individuare e installare il pacchetto appropriato hello:
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric - per componenti in esecuzione come file eseguibili guest e contenitori Docker in esecuzione nell'applicazione Service Fabric
    * Microsoft.ApplicationInsights.ServiceFabric.Native - per reliable services nelle applicazioni di ServiceFabric
    * Microsoft.ApplicationInsights.Kubernetes per i componenti in esecuzione in Docker su Kubernetes

### <a name="2-share-a-single-application-insights-resource"></a>2. Condividere una singola risorsa di Application Insights

* In Visual Studio fare clic con il pulsante destro del mouse sul progetto e selezionare **Configura Application Insights** oppure **Application Insights > Configurare**. Per il progetto prima di hello, utilizzare hello guidata toocreate una risorsa di Application Insights. Per i progetti successivi, selezionare hello stessa risorsa.
* Se non è presente alcun menu di Application Insights, configurare manualmente:

   1. In [portale di Azure](https://portal,azure.com), aprire una risorsa di Application Insights hello già stato creato per un altro componente.
   2. Nel pannello della panoramica hello, scheda hello Apri menu a discesa Essentials e hello copia **chiave di strumentazione.**
   3. Nel progetto aprire ApplicationInsights.config e inserire:`<InstrumentationKey>your copied key</InstrumentationKey>`

![Copiare i file con estensione config hello strumentazione toohello chiave](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Abilitare la Mappa delle applicazioni multiruolo

Nel portale di Azure hello, aprire la risorsa hello per l'applicazione. Nel Pannello di anteprime hello, abilitare *con più ruoli applicazione mappa*.

### <a name="4-enable-docker-metrics-optional"></a>4. Abilitare la metrica di Docker (facoltativo) 

Se un componente viene eseguito una Docker ospitata in una macchina virtuale Windows Azure, è possibile raccogliere metriche aggiuntive dal contenitore hello. Inserire nel file di configurazione di [Diagnostica di Azure](../monitoring-and-diagnostics/azure-diagnostics.md):

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Utilizzare i componenti tooseparate cloud_RoleName

Hello `cloud_RoleName` proprietà è telemetria tooall associata. Identifica un componente hello - ruolo hello o un servizio, che ha origine dati di telemetria hello. (È non hello stesso come cloud_RoleInstance, che separa identici ruoli che sono in esecuzione in parallelo in più processi del server o computer).

Nel portale di hello, è possibile filtrare o segmento di dati di telemetria utilizzando questa proprietà. In questo esempio, pannello errori hello è filtrato tooshow informazioni solo dal servizio web front-end hello, filtrando gli errori di back-end CRM API hello:

![Grafico della metrica segmentata in base al nome del ruolo Cloud](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Tracciare le operazioni tra i componenti

È possibile tracciare da un componente tooanother, chiamate hello effettuate durante l'elaborazione di una singola operazione.


![Mostrare i dati di telemetria per operazione](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Fare clic su server web front-end hello e API back-end hello tooa elenco correlato di dati di telemetria per questa operazione:

![Ricerca tra i componenti](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Passaggi successivi

* [Separare la telemetria da sviluppo, test e produzione](app-insights-separate-resources.md)
