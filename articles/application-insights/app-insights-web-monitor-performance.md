---
title: "aaaMonitor integrità dell'applicazione e l'utilizzo con Application Insights"
description: "Introduzione a Application Insights. Analizzare l'uso, la disponibilità e le prestazioni delle applicazioni locali o Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Monitorare le prestazioni di applicazioni Web


Questo prodotto consente di accertarsi che le prestazioni della propria applicazione siano ottimali e di scoprire rapidamente eventuali errori. [Application Insights] [ start] informare eventuali problemi di prestazioni e le eccezioni e consentono di trovare e diagnosticare hello cause principali.

Application Insights può monitorare sia le applicazioni web Java e ASP.NET che i servizi, i servizi WCF. Possono essere ospitati in locale, su macchine virtuali o come siti Web di Microsoft Azure. 

Sul lato client hello, Application Insights può richiedere dati di telemetria di pagine web e un'ampia gamma di dispositivi tra cui iOS, Android e App di Windows Store.

>[!Note]
> È ora disponibile una nuova funzionalità per la ricerca delle pagine a basse prestazioni nell'applicazione Web. Se non si dispone di accesso tooit, abilitarla per la configurazione delle opzioni di anteprima con hello [pannello Anteprima](app-insights-previews.md). Informazioni su questa nuova esperienza in [individuare e correggere eventuali colli di bottiglia con analisi delle prestazioni interattivo hello](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Configurare il monitoraggio delle prestazioni
Se non sono ancora stati aggiunti tooyour Application Insights (ovvero, se non dispone di Applicationinsights) del progetto, scegliere uno dei seguenti modi tooget avviato:

* [App Web ASP.NET](app-insights-asp-net.md)
  * [Aggiungere il monitoraggio delle eccezioni](app-insights-asp-net-exceptions.md)
  * [Aggiungere il monitoraggio delle dipendenze](app-insights-monitor-performance-live-website-now.md)
* [App web J2EE](app-insights-java-get-started.md)
  * [Aggiungere il monitoraggio delle dipendenze](app-insights-java-agent.md)

## <a name="view"></a>Esplorare le metriche delle prestazioni
In [hello Azure portal](https://portal.azure.com), Sfoglia risorsa di Application Insights toohello configurati per l'applicazione. pannello della panoramica Hello Mostra i dati sulle prestazioni di base:

Fare clic su qualsiasi toosee grafico ulteriori dettagli e toosee risultati per un periodo più lungo. Ad esempio, fare clic sul riquadro di richieste di hello e quindi selezionare un intervallo di tempo:

![Fare clic sui dati toomore e selezionare un intervallo di tempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Fare clic su un grafico toochoose le metriche Visualizza, o aggiungere un nuovo grafico e selezionare la metrica:

![Scegliere una metrica toochoose grafico](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Deselezionare tutte le metriche di hello** toosee hello selezione completa che è disponibile. le metriche Hello rientrano in gruppi. Quando viene selezionato qualsiasi membro di un gruppo, hello altri membri del gruppo vengono visualizzate solo.

## <a name="metrics"></a>Interpretazione dei dati riquadri e report sulle prestazioni
È possibile ottenere diverse metriche delle prestazioni. Iniziamo con quelli che vengono visualizzati per impostazione predefinita nel pannello applicazione hello.

### <a name="requests"></a>Requests
numero di Hello di richieste HTTP ricevute in un periodo specificato. Confrontare i risultati di hello sui toosee altri report come app si comporta come carico hello varia.

Le richieste HTTP includono tutte le richieste GET o POST di pagine, dati e immagini.

Fare clic sui conteggi di hello riquadro tooget URL specifici.

### <a name="average-response-time"></a>Tempo di risposta medio
Tempo di hello misure tra una richiesta web immettere la risposta dell'applicazione e hello restituita.

Hello punti indicano Media mobile. Se sono presenti numerose richieste, potrebbero esserci alcune si discostano da Media hello senza un picco ovvio o calo grafico hello.

Cercare picchi inconsueti. In generale, è probabile che toorise tempo di risposta con un aumento delle richieste. Se aumento hello è eccessivo, l'app potrebbe raggiungere un limite di risorse, ad esempio CPU o hello capacità di un servizio che viene utilizzato.

Fare clic su tempi di hello riquadro tooget per URL specifici.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Richieste lente
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Mostra quali richieste potrebbero necessitare di un'ottimizzazione delle prestazioni.

### <a name="failed-requests"></a>Richieste non riuscite
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

La quantità di richieste che hanno restituito eccezioni non rilevate.

Fare clic su hello riquadro toosee hello dettagli degli errori specifici e selezionare toosee una singola richiesta di dettagli. 

Viene conservato solo un campione di errori rappresentativi per l'analisi individuale.

### <a name="other-metrics"></a>Altre metriche
toosee quali altre metriche, è possibile visualizzare, fare clic su un grafico e quindi deselezionare tutte hello metriche toosee hello completo insieme disponibile. Fare clic su (i) toosee definizione di ogni metrica.

![Deselezionare tutte le metriche toosee hello intero insieme](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Selezionando qualsiasi hello Disabilita metrica ad altri utenti che non possono comparire in hello stesso grafico.

## <a name="set-alerts"></a>Impostazione di avvisi
toobe una notifica tramite posta elettronica di valori insoliti per le metriche, aggiungere un avviso. È possibile scegliere gli amministratori degli account toohello toosend hello posta elettronica o toospecific indirizzi di posta elettronica.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Impostare altre proprietà di risorsa hello prima hello. Non scegliere risorse webtest hello se si desidera ricevere avvisi di tooset relativi alle prestazioni o metrica di utilizzo.

Essere unità hello toonote attenzione in cui viene chiesto di valore di soglia tooenter hello.

*Pulsante di hello Aggiungi avviso non è presente.* -Si tratta di un toowhich di account di gruppo si dispone di accesso in sola lettura? Contattare l'amministratore account hello.

## <a name="diagnosis"></a>Diagnosi dei problemi
Di seguito vengono riportati alcuni suggerimenti su come trovare e diagnosticare i problemi di prestazioni:

* Impostare [test web] [ availability] toobe ricevere un avviso se il sito web diventa inattivo o risponde in modo non corretto o lenta. 
* Se gli errori o rallentamento della risposta è correlati tooload, confrontare il numero di richieste hello con toosee altre metriche.
* [Inserire e le istruzioni di traccia di ricerca] [ diagnostic] in toohelp il codice, individuare i problemi.
* Monitorare l'applicazione Web in esecuzione con [Live Metrics Stream][livestream].
* Acquisire lo stato di hello dell'applicazione .net con [Debugger Snapshot][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Individuare e risolvere i colli di bottiglia delle prestazioni con l'analisi interattiva delle prestazioni

È possibile utilizzare hello nuovo Application Insights prestazioni interattivo analisi toolocate aree dell'app Web che rallentano le prestazioni complessive. È possibile eseguire rapidamente queste pagine specifiche di ricerca che rallentano e utilizzare hello [dello strumento di profilatura](app-insights-profiler.md) toosee se è presente una correlazione tra le pagine.

### <a name="create-a-list-of-slow-performing-pages"></a>Creare un elenco delle pagine lente 

Hello primo passaggio per la ricerca di problemi di prestazioni consiste tooget un elenco di hello lenta risponde pagine. schermata di Hello seguito viene illustrato come utilizzare hello prestazioni pannello tooget un elenco di potenziali ulteriormente tooinvestigate di pagine. È possibile visualizzare rapidamente da questa pagina che si è verificato un rallentamento hello tempi di risposta dell'applicazione hello a circa 6:00 PM e nuovamente a circa 10 PM. È anche possibile vedere che hello/dettagli cliente operazione hanno operazioni a esecuzione prolungata alcune con un tempo di risposta mediano di 507.05 millisecondi. 

![Analisi interattiva delle prestazioni di Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Eseguire il drill-down in pagine specifiche

Dopo aver ottenuto uno snapshot delle prestazioni dell'app, è possibile visualizzare altri dettagli sulle singole operazioni lente. Fare clic su qualsiasi operazione nel hello toosee hello i dettagli dell'elenco come illustrato di seguito. Tipo di grafico hello è possibile vedere se le prestazioni di hello sono basata su una dipendenza. È inoltre possibile visualizzare quanti hello esperti di utenti diversi tempi di risposta. 

![Pannello delle operazioni di Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Eseguire il drill-in un periodo di tempo specifico

Dopo aver identificato un punto nel tempo tooinvestigate, eseguire il drill-down toolook ulteriormente a operazioni specifiche di hello che potrebbero aver causato l'errore rallentamento delle prestazioni hello. Quando si fa clic su uno specifico punto nel tempo recuperare i dettagli di hello della pagina di hello, come illustrato di seguito. In hello esempio riportato di seguito è possibile visualizzare le operazioni di hello elencate per un determinato periodo di tempo insieme ai codici di risposta server hello e durata dell'operazione hello. È inoltre possibile hello url per l'apertura di un elemento di lavoro TFS se è necessario toosend il team di sviluppo tooyour informazioni.

![Intervallo di tempo di Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Eseguire il drill-in un'operazione specifica

Dopo aver identificato un punto nel tempo tooinvestigate, eseguire il drill-down toolook ulteriormente a operazioni specifiche di hello che potrebbero aver causato l'errore rallentamento delle prestazioni hello. Fare clic su un'operazione da hello toosee hello i dettagli dell'elenco dell'operazione di hello, come illustrato di seguito. In questo esempio che è possibile vedere che hello operazione non riuscita e ha fornito le informazioni di hello di hello per Application Insights ha generato un'applicazione hello eccezione. È di nuovo possibile creare un elemento di lavoro TFS da questo pannello.

![Pannello dell'operazione di Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Passaggi successivi
[Test Web] [ availability] -sono le richieste web inviate applicazione tooyour a intervalli regolari dal mondo hello.

[Acquisire e cercare le tracce di diagnostica] [ diagnostic] : inserire chiamate di traccia e tra i problemi di toopinpoint risultati hello.

[Monitorare l'utilizzo][usage]: possibilità di scoprire come le persone usano l'applicazione.

[Domande e risposte e risoluzione dei problemi][qna]



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



