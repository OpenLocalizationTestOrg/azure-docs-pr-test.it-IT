---
title: le applicazioni con Azure Application Insights in Visual Studio aaaDebug | Documenti Microsoft
description: Diagnostica e analisi delle prestazioni delle app Web durante il debug e nell'ambiente di produzione.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Eseguire il debug delle applicazioni con Azure Application Insights in Visual Studio
In Visual Studio 2015 e versioni successive è possibile analizzare le prestazioni e diagnosticare i problemi nell'app Web ASP.NET sia durante il debug che nell'ambiente di produzione, usando i dati di telemetria di [Azure Application Insights](app-insights-overview.md).

Se è stato creato l'app web ASP.NET utilizzando Visual Studio 2017 o versioni successive, ha già hello Application Insights SDK. In caso contrario, se non è già fatto, [aggiungere Application Insights tooyour app](app-insights-asp-net.md).

toomonitor l'app quando è in produzione, è in genere visualizzare telemetria di Application Insights hello in hello [portale di Azure](https://portal.azure.com), in cui è possibile impostare gli avvisi e applicare i potenti strumenti di monitoraggio. Ma per il debug, è inoltre possibile cercare e analizzare dati di telemetria hello in Visual Studio. È possibile utilizzare i dati di telemetria di Visual Studio tooanalyze dal sito di produzione e di debug viene eseguito nel computer di sviluppo. In quest'ultimo caso hello, è possibile analizzare il debug viene eseguito anche se è ancora stata configurata hello SDK toosend telemetria toohello portale di Azure. 

## <a name="run"></a> Eseguire il debug del progetto
Per eseguire l'app Web in modalità di debug locale, premere F5. Aprire pagine diverse toogenerate alcuni dati di telemetria.

In Visual Studio, viene visualizzato un conteggio di eventi di hello che sono stati registrati dal modulo di Application Insights hello nel progetto.

![In Visual Studio, hello Application Insights è raffigurata durante il debug.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Fare clic su questo pulsante toosearch dati di telemetria. 

## <a name="application-insights-search"></a>Ricerca in Application Insights
finestra di ricerca di Application Insights Hello Mostra gli eventi che sono stati registrati. (Se non hai effettuato tooAzure quando si configura Application Insights, è possibile cercare hello stessi eventi nel portale di Azure hello.)

![Fare clic sul progetto hello e scegliere di Application Insights, ricerca](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> Dopo aver selezionare o deselezionare i filtri, fare clic su pulsante di ricerca hello alla fine di hello del campo di ricerca di testo hello.
>

ricerca di testo libero Hello funziona su tutti i campi negli eventi hello. Ad esempio, cercare parte di hello URL di una pagina. il valore di hello di una proprietà, ad esempio città client; o o parole specifiche in un log di traccia.

Fare clic su qualsiasi toosee evento le proprietà dettagliate.

Per le richieste tooyour web app, è possibile fare clic su tramite codice toohello.

![In Dettagli richiesta, fare clic su tramite codice toohello](./media/app-insights-visual-studio/31.png)

È inoltre possibile aprire elementi correlati toohelp diagnosticare le richieste non riuscite o le eccezioni.

![In Dettagli richiesta, scorrere verso il basso toorelated elementi](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Visualizzare le eccezioni e le richieste non riuscite
Mostra i report di eccezione nella finestra di ricerca hello. (In alcuni tipi precedenti dell'applicazione ASP.NET, è necessario troppo[impostare il monitoraggio di eccezione](app-insights-asp-net-exceptions.md) toosee eccezioni gestite da framework hello.)

Fare clic su un tooget eccezione una traccia dello stack. Se il codice hello dell'applicazione hello è aperto in Visual Studio, è possibile fare clic hello stack traccia toohello rilevanti riga di codice hello.

![Analisi dello stack delle eccezioni](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Visualizzare i riepiloghi di richiesta e l'eccezione nel codice hello
In hello riga Codelens sopra ogni metodo del gestore, viene visualizzato un conteggio di hello richieste e le eccezioni registrate da Application Insights in hello ultime 24 ore.

![Analisi dello stack delle eccezioni](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Codelens Mostra i dati di Application Insights solo se è necessario [configurato il portale di Application Insights app toosend telemetria toohello](app-insights-asp-net.md).
>

[Altre informazioni su Application Insights in CodeLens](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Tendenze
Tendenze è uno strumento che permette di visualizzare il comportamento dell'app nel tempo. 

Scegliere **esplorare le tendenze di telemetria** dal pulsante della barra degli strumenti di Application Insights hello o nella finestra di ricerca di Application Insights. Scegliere uno dei cinque tooget query comuni avviato. È possibile analizzare set di dati diversi in base ai tipi di dati di telemetria, agli intervalli di tempo e ad altre proprietà. 

toofind anomalie nei dati, scegliere una delle opzioni di anomalie hello in elenco a discesa "Tipo di visualizzazione" hello. opzioni di filtro nella parte inferiore di hello della finestra hello Hello rendono semplice toohone in base a subset specifici dei dati di telemetria.

![Tendenze](./media/app-insights-visual-studio/51.png)

[Altre informazioni su Tendenze](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Monitoraggio locale
(Da Visual Studio 2015 Update 2) Se non è configurato il portale di Application Insights toohello hello SDK toosend telemetria (in modo che non è presente alcuna chiave di strumentazione in Applicationinsights) finestra diagnostica hello Visualizza dati di telemetria da una sessione di debug più recenti. 

Questo è consigliabile se è già stata pubblicata una versione precedente dell'app. Per evitare che il debug di sessioni toobe dati telemetria hello confuse con dati di telemetria relativi hello hello portale Application Insights da app pubblicata hello.

È inoltre utile se si dispone di un [telemetria personalizzata](app-insights-api-custom-events-metrics.md) che si desidera toodebug prima dell'invio portale toohello telemetria.

* *Inizialmente configurato completamente portale toohello telemetria di Application Insights toosend. Ma ora telemetria hello toosee solo in Visual Studio.*
  
  * Nelle impostazioni della finestra di ricerca hello, è una diagnostica locale toosearch di opzione, anche se l'app invia portale toohello telemetria.
  * dati di telemetria toostop inviati toohello portal, impostare come commento la riga hello `<instrumentationkey>...` da Applicationinsights. Quando si passa nuovamente portale toohello di telemetria toosend pronto, rimuovere i commenti.


## <a name="next-steps"></a>Passaggi successivi
|  |  |
| --- | --- |
| **[Aggiungere altri dati](app-insights-asp-net-more.md)**<br/>Monitorare l'utilizzo, la disponibilità, le dipendenze e le eccezioni, integrare le tracce dei framework di registrazione e scrivere telemetria personalizzata. |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[Utilizzo di portale Application Insights hello](app-insights-dashboards.md)**<br/>Visualizzare i dashboard, strumenti avanzati di diagnostica e di analisi, avvisi, una mappa attiva delle dipendenze dell'applicazione e i dati di telemetria esportati. |![Visual Studio](./media/app-insights-visual-studio/62.png) |

