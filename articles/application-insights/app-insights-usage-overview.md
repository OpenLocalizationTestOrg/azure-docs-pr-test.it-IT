---
title: analisi aaaUsage per le applicazioni web con Azure Application Insights | Documenti Microsoft
description: Informazioni sugli utenti e le operazioni eseguite con l'app Web.
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>Analisi dell'utilizzo per applicazioni Web con Application Insights

Quali sono le funzionalità dell'app Web più comuni? Gli utenti raggiungono i propri obiettivi con l'app? Escono in particolari punti e riaccedono in un secondo momento?  [Application Insights di Azure](app-insights-overview.md) consente di ottenere importanti informazioni approfondite sull'uso dell'app Web da parte degli utenti. Ogni volta che si aggiorna l'app, è possibile valutarne il funzionamento per gli utenti. Con queste informazioni è possibile prendere decisioni in base ai dati sui cicli di sviluppo successivi.

## <a name="send-telemetry-from-your-app"></a>Inviare dati di telemetria dall'app

migliore esperienza Hello viene ottenuta mediante l'installazione di Application Insights nel codice server dell'app e nelle pagine web. componenti client e server di Hello dell'app inviano toohello indietro telemetria portale di Azure per l'analisi.

1. **Il codice lato server:** modulo appropriato hello di installazione per il [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), o [altri](app-insights-platforms.md) app.

    * *Evitare di dover codice server tooinstall? [Creare una risorsa di Azure Application Insights](app-insights-create-new-resource.md).*

2. **Codice della pagina Web:** hello aprire [portale di Azure](https://portal.azure.com), aprire la risorsa di Application Insights hello per l'app e quindi aprire **introduzione > monitoraggio e diagnosi lato Client**. 

    ![Copiare script hello in head hello della pagina master web.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **Ottenere dati di telemetria:** eseguire il progetto in modalità di debug per alcuni minuti e quindi cercare i risultati nel pannello della panoramica hello in Application Insights.

    Pubblicare l'app toomonitor le prestazioni dell'app e scoprire operazioni con l'app agli utenti.

## <a name="include-user-and-session-id-in-your-telemetry"></a>Includere l'ID di utente e sessione nei dati di telemetria
tootrack gli utenti nel tempo, Application Insights è necessario un modo tooidentify li. gli eventi di Hello strumento hello solo strumento in uso non richiede un ID utente o un ID sessione.

Per iniziare a inviare questi ID, vedere [qui](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).

## <a name="explore-usage-demographics-and-statistics"></a>Esplorare le statistiche e i dati demografici di uso
Scoprire quando le persone usano l'app, a quali pagine sono più interessati, dove si trovano, quali browser e sistemi operativi usano. 

report di utenti e sessioni Hello filtrare i dati nelle pagine o eventi personalizzati e li segmento da proprietà quali posizione, l'ambiente e pagina. È anche possibile aggiungere filtri personalizzati.

![Utenti](./media/app-insights-usage-overview/users.png)  

Informazioni dettagliate sui hello destro specificare schemi interessanti nei set di hello di dati.  

* Hello **utenti** report conta il numero di hello di utenti univoci che accedere alle pagine durante i periodi di tempo scelto. Gli utenti vengono conteggiati usando i cookie. Se un utente accede al sito con browser o computer client diversi o cancella i cookie, verrà conteggiato più volte.
* Hello **sessioni** report conta il numero di hello delle sessioni che accedono al sito. Una sessione è un periodo di attività dell'utente, che termina quando si verifica un periodo di inattività di più di mezz'ora.

[Informazioni sugli strumenti di utenti, sessioni e gli eventi di hello](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>Visualizzazioni pagina

Dal Pannello di utilizzo di hello, fare clic sulle hello visualizzazioni pagina riquadro tooget una suddivisione delle pagine più diffusi:

![Dal pannello della panoramica hello, fare clic su hello grafico visualizzazioni pagina](./media/app-insights-usage-overview/05-games.png)

esempio Hello sopra si trova in un sito web di giochi. Da grafici hello, è possibile vedere immediatamente:

* Utilizzo non è stata migliorata in hello settimana precedente. Potrebbe essere utile ottimizzare il motore di ricerca.
* Tennis è la pagina di gioco più diffuso di hello. Concentriamoci pagina ulteriori miglioramenti toothis.
* In Media, gli utenti visitano pagina Tennis hello circa tre volte per ogni settimana. Il numero delle sessioni è tre volte superiore al numero di utenti.
* La maggior parte degli utenti sito hello durante la settimana lavorativa di hello Stati Uniti e in orario di lavoro. Forse dovremmo offriamo un pulsante "Nascondi rapido" nella pagina web hello.
* Hello [annotazioni](app-insights-annotations.md) sul grafico hello vengono visualizzati quando le nuove versioni del sito Web di hello distribuite. Nessuna delle distribuzioni recenti hello aveva un impatto negativo sulle utilizzo.

Cosa accade se si desidera tooinvestigate sito tooyour il traffico di hello in modo più dettagliato, ad esempio suddivisione di una proprietà personalizzata che del sito invia nei relativi dati di telemetria di visualizzazione pagina?

1. Aprire hello **eventi** strumento nel menu di risorsa di Application Insights hello. Questo strumento consente di analizzare il numero di visualizzazioni della pagina ed eventi personalizzati inviati dall'app, in base a diverse opzioni di filtro, coorte e segmentazione.
2. Nell'elenco a discesa delle "Chi ha utilizzato" hello, selezionare "Qualsiasi visualizzazione pagina".
3. Nell'elenco a discesa "Divisione" hello, selezionare una proprietà da cui toosplit pagina consente di visualizzare dati di telemetria.

## <a name="retention---how-many-users-come-back"></a>Conservazione: numero di utenti che ritornano

Conservazione consente di comprendere la frequenza con cui gli utenti restituiscono toouse la propria applicazione, in base a coorti di utenti di eseguire un'azione di business durante un determinato intervallo di tempo. 

- Comprendere quali funzionalità specifiche causare la back toocome più rispetto ad altri utenti 
- Fare ipotesi in base a dati utente reali 
- Determinare se la conservazione è un problema per il prodotto 

![Conservazione](./media/app-insights-usage-overview/retention.png) 

i controlli di conservazione Hello nella parte superiore consentono si toodefine eventi specifici e conservazione toocalculate intervallo di tempo. grafico centro hello Hello fornisce una rappresentazione visiva di hello percentuale complessiva di conservazione per hello intervallo di tempo specificato. grafico Hello nella parte inferiore di hello rappresenta memorizzazione singola in un determinato periodo di tempo. Questo livello di dettaglio consente toounderstand quali gli utenti eseguono e cosa possono influire degli utenti in una granularità più dettagliata.  

[Informazioni sullo strumento di conservazione hello](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>Eventi aziendali personalizzati

tooget una chiara comprensione di ciò che gli utenti di eseguire l'App web, è utile tooinsert righe degli eventi personalizzati toolog di codice. Questi eventi possono tenere traccia nulla da azioni dell'utente dettagliato, ad esempio facendo clic sui pulsanti specifici, eventi di business significativo toomore come effettuare l'acquisto o vincente un gioco. 

Sebbene in alcuni casi, le visualizzazioni della pagina possano rappresentare eventi utili, questo non è vero in generale. Un utente può aprire una pagina di prodotto senza dover acquistare il prodotto hello. 

Con eventi aziendali specifici, è possibile rappresentare in un grafico lo stato di avanzamento degli utenti all'interno del sito. È possibile scoprirne le preferenze per le diverse opzioni e i punti in cui abbandonano il sito o hanno difficoltà. Con queste informazioni, è possibile prendere decisioni informate sulla priorità hello nel backlog di sviluppo.

Gli eventi possono essere registrati nella pagina web hello:

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

O sul lato server hello dell'app web hello:

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

È possibile collegare eventi toothese valori di proprietà, in modo che è possibile filtrare o suddividere gli eventi di hello quando si verifica nel portale di hello. Inoltre, un set standard di proprietà è associata tooeach evento, ad esempio ID utente anonimo, consentendo la sequenza di hello tootrace delle attività di un singolo utente.

Altre informazioni sugli [eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent) e le [proprietà](app-insights-api-custom-events-metrics.md#properties).

### <a name="slice-and-dice-events"></a>Analisi approfondita degli eventi

In strumenti di utenti, sessioni e gli eventi hello, è possibile sezionare e ripartiscono eventi personalizzati dall'utente, nome dell'evento e le proprietà.
![Utenti](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>Dati di telemetria di progettazione hello con app hello

Quando si progetta ogni funzionalità dell'app, considerare come verrà toomeasure il suo successo con gli utenti. Decidere quali avviare gli eventi di business è necessario toorecord e codice hello chiamate per gli eventi di rilevamento nell'app da hello.

## <a name="a--b-testing"></a>Test A | B
Se non si conosce variante di una funzionalità sarà più efficace, rilasciare entrambe, rendere gli utenti di ogni toodifferent accessibile. Misurare il successo di hello di ogni e quindi spostare tooa unificata versione.

Questa tecnica, si collega la telemetria proprietà distinti valori tooall hello inviato da ogni versione dell'app. È possibile farlo mediante la definizione di proprietà in hello TelemetryContext attivo. Queste proprietà predefinite vengono aggiunte Invia messaggio di dati di telemetria tooevery applicazione hello - non solo i messaggi personalizzati, ma anche telemetria standard hello.

Nel portale Application Insights hello, filtrare e dividere i dati per valori di proprietà hello, in modo da versioni diverse di toocompare hello.

toodo, [impostare un inizializzatore di telemetria](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

Nell'inizializzatore di app web hello, ad esempio Global.asax.cs:

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

TelemetryClients di nuovo tutti aggiunge automaticamente il valore di proprietà hello specificato. Gli eventi di telemetria singoli possono eseguire l'override di valori predefiniti di hello.

## <a name="next-steps"></a>Passaggi successivi
   - [Utenti, sessioni ed eventi](app-insights-usage-segmentation.md)
   - [Grafici a imbuto](usage-funnels.md)
   - [Conservazione](app-insights-usage-retention.md)
   - [Flussi degli utenti](app-insights-usage-flows.md)
   - [Cartelle di lavoro](app-insights-usage-workbooks.md)
   - [Aggiungere il contesto utente](app-insights-usage-send-user-context.md)
