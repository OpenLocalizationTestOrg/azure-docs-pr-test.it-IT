---
title: applicazioni di aaaMonitor Docker in Azure Application Insights | Documenti Microsoft
description: Eccezioni, eventi e contatori delle prestazioni di docker possono essere visualizzate in Application Insights, insieme ai dati di telemetria hello da app hello contenitore.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Monitoraggio di applicazioni Docker in Application Insights
I contatori delle prestazioni e degli eventi del ciclo di vita da contenitori [Docker](https://www.docker.com/) possono essere disegnati in Application Insights. Installare hello [Application Insights](app-insights-overview.md) immagine in un contenitore dell'host e visualizzerà i contatori delle prestazioni per host hello, come anche di hello altre immagini.

Con Docker si distribuiscono le app in contenitori leggeri completi di tutte le dipendenze. Verranno eseguite su tutti i computer host che eseguono un motore Docker.

Quando si esegue hello [immagine di Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) sull'host Docker, si possono ottenere questi vantaggi:

* Dati di telemetria di ciclo di vita su tutti i contenitori di hello in esecuzione nell'host di hello - avviare, arrestare e così via.
* Contatori delle prestazioni per tutti i contenitori di hello. CPU, memoria, utilizzo della rete e altro ancora.
* Se si [installati Application Insights SDK per Java](app-insights-java-live.md) hello le App in esecuzione in contenitori hello, tutti i dati di telemetria hello di tali App hanno proprietà aggiuntive che identifica il contenitore di hello e computer host. Ad esempio, se si dispone di istanze di un'app in esecuzione in più host, è possibile filtrare facilmente dall'host i dati di telemetria dell'app.

![esempio](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Configurare la risorsa di Application Insights
1. Accedere a [portale Microsoft Azure](https://azure.com) e aprire la risorsa di Application Insights hello per l'app; o [crearne uno nuovo](app-insights-create-new-resource.md). 
   
    *Quale risorsa si deve usare?* Se sono state sviluppate hello App in esecuzione sull'host da un altro utente, quindi è necessario troppo[creare una nuova risorsa di Application Insights](app-insights-create-new-resource.md). Si tratta in cui si consente di visualizzare e analizzare dati di telemetria hello. (Selezionare "Generale" per il tipo di app hello).
   
    Ma se lo sviluppatore di hello di hello App, quindi ci auguriamo che [aggiungere Application Insights SDK](app-insights-java-live.md) tooeach di essi. Se sono tutti effettivamente i componenti di un'applicazione di business, quindi è possibile configurare tutte le risorse di tooone toosend telemetria e si utilizzerà gli stessi risorsa toodisplay hello Docker ciclo di vita e delle prestazioni dati. 
   
    Un terzo scenario è che è stato sviluppato la maggior parte delle App hello, ma si utilizza risorse diverse toodisplay i dati di telemetria. In tal caso, è probabile che anche desidera toocreate una risorsa distinta per hello dati Docker. 
2. Aggiungi riquadro Docker di hello: scegliere **aggiungere riquadro**, trascinare il riquadro di Docker hello dalla raccolta di hello e quindi fare clic su **eseguita**. 
   
    ![esempio](./media/app-insights-docker/03.png)
3. Fare clic su hello **Essentials** elenco a discesa e copiare hello chiave di strumentazione. Utilizzare questo hello tootell SDK in cui toosend la telemetria.

    ![esempio](./media/app-insights-docker/02-props.png)

Mantenere la finestra del browser utili, come si ritornerà tooit appena toolook su dati di telemetria.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>Esegui monitoraggio di Application Insights hello sull'host
Ora che hai in un punto dati di telemetria hello toodisplay, è possibile impostare l'app nei contenitori hello che raccoglierà e inviarlo.

1. Connettere l'host Docker tooyour. 
2. Modificare la chiave di strumentazione in questo comando, e poi eseguirlo:
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

Solo un'immagine di Application Insights è obbligatoria per ogni host Docker. Se l'applicazione viene distribuita su più host Docker, quindi ripetere il comando di hello in ogni host.

## <a name="update-your-app"></a>Aggiornamento dell'app
Se l'applicazione è instrumentato con hello [Application Insights SDK per Java](app-insights-java-get-started.md), aggiungere hello seguente riga nel file ApplicationInsights.xml hello nel progetto, in hello `<TelemetryInitializers>` elemento:

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

Aggiunge informazioni di Docker, ad esempio contenitore e host id tooevery telemetria item inviati dall'app.

## <a name="view-your-telemetry"></a>Visualizzare i dati di telemetria
Tornare indietro di risorsa di Application Insights tooyour in hello portale di Azure.

Scorrere il riquadro di Docker hello.

Si noterà subito dati provenienti da app Docker hello, soprattutto se si dispone di altri contenitori in esecuzione nel motore di Docker.

Ecco alcune delle viste hello che è possibile ottenere.

### <a name="perf-counters-by-host-activity-by-image"></a>Contatori delle prestazioni per host, attività per immagine
![esempio](./media/app-insights-docker/10.png)

![esempio](./media/app-insights-docker/11.png)

Fare clic su un nome dell’host o dell’immagine per altri dettagli.

visualizzazione di hello toocustomize, fare clic su qualsiasi grafico, l'intestazione della griglia di hello oppure utilizzare Aggiungi grafico. 

[Altre informazioni su Esplora metriche](app-insights-metrics-explorer.md)

### <a name="docker-container-events"></a>Eventi del contenitore Docker
![esempio](./media/app-insights-docker/13.png)

tooinvestigate singoli eventi, fare clic su [ricerca](app-insights-diagnostic-search.md). Ricerca e filtro toofind hello eventi desiderati. Fare clic su qualsiasi tooget evento maggiori dettagli.

### <a name="exceptions-by-container-name"></a>Eccezioni per nome del contenitore
![esempio](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>Il contesto di docker aggiunto tooapp telemetria
Telemetria di richiesta inviato da un'applicazione hello instrumentata con AI SDK, sono stati arricchiti con contesto Docker:

![esempio](./media/app-insights-docker/16.png)

Tempo di elaborazione e contatori delle prestazioni di memoria disponibile, arricchiti e raggruppati per nome del contenitore Docker:

![esempio](./media/app-insights-docker/15.png)

## <a name="q--a"></a>Domande e risposte
*Quali sono i vantaggi di Application Insights rispetto a Docker?*

* Suddivisione dettagliata dei contatori delle prestazioni in base al contenitore e all'immagine.
* Integrazione dei dati dell'app e dei contenitori in un unico dashboard.
* [Esportare i dati di telemetria](app-insights-export-telemetry.md) per database di tooa ulteriore analisi, Power BI o altri dashboard.

*Come ottenere dati di telemetria da app hello stessa?*

* Installare Application Insights SDK hello hello app. Per informazioni, vedere [App Web Java](app-insights-java-get-started.md) e [App Web Windows](app-insights-asp-net.md).

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Passaggi successivi

* [Application Insights per Java](app-insights-java-get-started.md)
* [Application Insights per Node.js](app-insights-nodejs.md)
* [Application Insights per ASP.NET](app-insights-asp-net.md)
