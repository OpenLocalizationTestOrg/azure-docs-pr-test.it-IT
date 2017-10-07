---
title: Rilevamento di anomalie di errore, in Application Insights - aaaSmart | Documenti Microsoft
description: "Avvisa l'utente toounusual modifiche tasso hello di richieste non riuscite tooyour web app e fornisce l'analisi diagnostica. Non è necessaria alcuna configurazione."
services: application-insights
documentationcenter: 
author: yorac
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: bwren
ms.openlocfilehash: dfd178ca9546294be91f27b0c1b846d519539b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---failure-anomalies"></a>Rilevamento intelligente - Anomalie degli errori
[Application Insights](app-insights-overview.md) invia automaticamente una notifica è quasi in tempo reale se l'app web di cui si verifichi un aumento anomalo della percentuale di hello delle richieste non riuscite. Rileva un insolito aumento della percentuale di hello di richieste HTTP o chiamate a dipendenze che vengono segnalate come non riuscita. Per quanto riguarda le richieste, quelle non riuscite hanno in genere un codice di risposta 400 o superiore. toohelp valutare e diagnosticare il problema di hello, un'analisi delle caratteristiche di hello di errori di hello e dati di telemetria correlati viene fornita nella notifica hello. Esistono anche portale Application Insights toohello di collegamenti per un'ulteriore diagnosi. Hello funzionalità non deve configurazione o la configurazione, come Usa il machine learning percentuale di errori normale di algoritmi toopredict hello.

Questa funzionalità funziona per App web Java e ASP.NET, ospitata nel cloud hello o sul server. Funziona anche per qualsiasi app che genera dati di telemetria di richiesta o di dipendenza, ad esempio, un ruolo di lavoro che chiama [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) o [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency).

Dopo l'impostazione [Application Insights per il progetto](app-insights-overview.md), e fornito l'app genera una certa quantità minima di dati di telemetria, Smart rilevamento di anomalie di errore accetta toolearn hello un comportamento normale dell'applicazione, prima che 24 ore viene attivato e che può inviare gli avvisi.

Ecco un avviso di esempio.

![Esempio di avviso di rilevamento intelligente che mostra l'analisi del cluster riguardo all'errore](./media/app-insights-proactive-failure-diagnostics/013.png)

> [!NOTE]
> Per impostazione predefinita, si riceve un messaggio di posta elettronica più breve rispetto a quello dell’esempio. Ma è possibile [formato dettagliato di commutatore toothis](#configure-alerts).
>
>

Le informazioni fornite includono:

* percentuale di errori di Hello confrontati toonormal un comportamento dell'app.
* Il numero di utenti è interessato-per sapere quanto tooworry.
* Un modello di caratteristica associato a errori di hello. In questo esempio sono presenti un codice di risposta, un nome di richiesta (operazione) e una versione dell’applicazione specifici. Che indica immediatamente in toostart ricerca nel codice. In alternativa si può usare un browser o un sistema operativo client specifico.
* eccezione Hello, tracce di log ed errori di dipendenza (database o altri componenti esterni) che vengono visualizzati toobe associato hello caratterizzati errori.
* Collega direttamente toorelevant ricerche sui dati di telemetria hello in Application Insights.

## <a name="benefits-of-smart-detection"></a>Vantaggi del rilevamento intelligente
I normali [avvisi relativi alla metrica](app-insights-alerts.md) indicano che potrebbe essersi verificato un problema. Ma hello diagnostica operazioni, eseguire un numero elevato di analisi di hello in caso contrario si sarebbe necessario toodo avvio del rilevamento intelligente. Si ottengono hello risultati ben distinto, consentendo di tooget rapidamente toohello radice del problema hello.

## <a name="how-it-works"></a>Funzionamento
Rilevamento intelligente monitora telemetria hello ricevuto dall'app e i tassi di errore specifico hello. Questa regola calcola il numero di hello di richieste per i quali hello `Successful request` proprietà è false e chiama il numero di hello di dipendenza per cui hello `Successful call` proprietà è false. Per le richieste, per impostazione predefinita, `Successful request == (resultCode < 400)` (a meno che non è stato scritto codice personalizzato troppo[filtro](app-insights-api-filtering-sampling.md#filtering) o generare la propria [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest) chiamate). 

Le prestazioni dell'applicazione hanno un modello di comportamento tipico. Alcune richieste o chiamate a dipendenze saranno più inclini toofailure rispetto ad altri; e hello percentuale di errori globale può salire man mano che aumenta di carico. Rilevamento intelligente utilizza di machine learning toofind queste anomalie.

Come dati di telemetria provengono in Application Insights da app web, comportamento corrente hello rilevamento Smart confronta con i modelli di hello rilevati in hello alcuni giorni. Se viene osservato un incremento anomalo della frequenza degli errori rispetto alle prestazioni precedenti, viene attivata un’analisi.

Quando viene attivata un'analisi, il servizio di hello esegue un'analisi di cluster su hello richieste non riuscite, tootry tooidentify una serie di valori che caratterizzano gli errori di hello. Nell'esempio hello sopra, analisi hello ha individuato che la maggior parte degli errori sono su un codice risultato specifico, nome richiesta, l'host dell'URL di Server e istanza del ruolo. Al contrario, l'analisi di hello ha individuato che proprietà del sistema operativo client hello viene distribuito in più valori, e pertanto non è elencato.

Quando il servizio è stato instrumentato con queste chiamate di telemetria, l'analizzatore hello cerca un'eccezione e un errore di dipendenza che sono associate alle richieste in cluster hello che è identificato, insieme a un esempio di tutti i log di traccia associati a tali richieste.

risultati dell'analisi di Hello viene inviato tooyou come avviso, a meno che non è stato configurato non a.

Ad esempio hello [avvisi si imposta manualmente](app-insights-alerts.md), è possibile controllare lo stato di hello di avviso hello e configurarlo nel Pannello di avvisi hello della risorsa di Application Insights. Ma a differenza di altri avvisi, non necessario tooset backup o configurazione del rilevamento intelligente. Se necessario, è possibile disabilitarlo o modificare gli indirizzi di posta elettronica di destinazione.

## <a name="configure-alerts"></a>Configurare gli avvisi
Disabilitare il rilevamento intelligente, modificare i destinatari di posta elettronica hello, creare un webhook o partecipare toomore dettagliate i messaggi di avviso.

Aprire una pagina avvisi hello. Errore anomalie è incluso insieme a eventuali avvisi che è stata impostata manualmente e si può verificare se è attualmente in stato di avviso hello.

![Nella pagina di panoramica hello, fare clic sul riquadro avvisi. In alternativa, in qualsiasi pagina di Metrica fare clic su pulsante Avvisi.](./media/app-insights-proactive-failure-diagnostics/021.png)

Fare clic su tooconfigure avviso hello è.

![Configurazione](./media/app-insights-proactive-failure-diagnostics/032.png)

Si noti che è possibile disabilitare l'avviso di rilevamento intelligente, ma non eliminarlo (o crearne un altro).

#### <a name="detailed-alerts"></a>Avvisi dettagliati
Se si seleziona "Ottenere diagnostica più dettagliata" posta elettronica hello conterrà informazioni di diagnostica. In alcuni casi sarà in grado di toodiagnose problema di hello solo dai dati hello nel messaggio di posta elettronica hello.

È un rischio per piccole che hello avviso più dettagliata potrebbe contenere informazioni riservate, perché include i messaggi di eccezione e traccia. Ciò si verifica tuttavia soltanto se il codice permette l'inserimento di informazioni riservate in tali messaggi.

## <a name="triaging-and-diagnosing-an-alert"></a>Valutazione e diagnosi di un avviso
Un avviso indica che è stato rilevato un aumento anomalo della percentuale di richieste non riuscite hello. È probabile che si sia verificato un problema con l'app o il relativo ambiente.

Base percentuale hello di richieste e numero di utenti interessati, sarà possibile decidere il livello di priorità problema hello è. Nell'esempio hello sopra, percentuale di errori di hello % 22.5 confronta con la velocità normale di % 1, indica che un'operazione non valida in corso. In hello invece, gli utenti solo 11 sono stati interessati. Se si trattasse di app, sarà in grado di tooassess la gravità di.

In molti casi, sarà in grado di toodiagnose hello problema rapidamente nome richiesta hello, eccezione, i dati di traccia e di errore di dipendenza forniti.

Esistono alcune altre indicazioni. Percentuale di errori di dipendenza hello in questo esempio è ad esempio, hello uguali a quelli hello frequenza eccezione (% 89.3). Ne consegue che eccezione hello deriva direttamente dall'errore di dipendenza hello - offrendo un'idea chiara dove toostart ricerca nel codice.

tooinvestigate ulteriormente, hello collegamenti in ogni sezione consentono di passare retta tooa [pagina ricerca](app-insights-diagnostic-search.md) filtrata toohello rilevanti richieste, eccezioni, dipendenze o tracce. È possibile aprire hello [portale di Azure](https://portal.azure.com), passare toohello risorsa di Application Insights per l'applicazione e aprire il pannello di errori hello.

In questo esempio, facendo clic su hello ' dipendenza errori collegamento Visualizza dettagli' apre il pannello di ricerca di Application Insights hello. Mostra istruzione SQL hello che contiene un esempio di causa principale di hello: i valori null sono stati forniti i campi obbligatori e non ha superato la convalida durante hello operazione di salvataggio.

![Ricerca diagnostica](./media/app-insights-proactive-failure-diagnostics/051.png)

## <a name="review-recent-alerts"></a>Esaminare gli avvisi recenti

Fare clic su **rilevamento Smart** tooget toohello più recente avviso:

![Riepilogo degli avvisi](./media/app-insights-proactive-failure-diagnostics/070.png)


## <a name="whats-hello-difference-"></a>Che cos'è la differenza hello...
Il rilevamento intelligente delle anomalie degli errori integra altre funzionalità simili ma distinte di Application Insights.

* Gli [avvisi metrica](app-insights-alerts.md) vengono impostati dall'utente e possono monitorare un'ampia gamma di metriche, ad esempio utilizzo della CPU, frequenza delle richieste, tempi di caricamento delle pagine e così via. È possibile usarli toowarn è, ad esempio, se è necessario tooadd più risorse. Al contrario, Smart rilevamento di anomalie di errore copre toonotify un intervallo ridotto di metriche più importanti (attualmente solo richieste non riuscite frequenza), progettato in quasi in tempo reale modo una volta aumenta la frequenza di richieste non riuscite dell'app web in modo significativo rispetto tooweb dell'app comportamento normale.

    Rilevamento intelligente regola automaticamente la soglia nelle condizioni tooprevailing di risposta.

    Avvio del rilevamento smart hello diagnostica accettabile.
* [Rilevamento di anomalie smart](app-insights-proactive-performance-diagnostics.md) inoltre utilizza computer intelligence toodiscover insolito criteri le metriche ed è richiesta alcuna configurazione da parte dell'utente. Ma a differenza di Smart rilevamento di anomalie di errore, scopo hello Smart il rilevamento di anomalie toofind segmenti del collettore utilizzo resi potrebbe essere errato, ad esempio da pagine specifiche in un tipo specifico del browser. Hello l'analisi viene eseguita ogni giorno e se viene trovato alcun risultato, è probabile che toobe molto meno urgenti rispetto a un avviso. Al contrario, analisi hello per le anomalie di errore viene eseguita in modo continuo sui dati di telemetria in ingresso e riceverà una notifica in pochi minuti se le tariffe di errore di server sono maggiori del previsto.

## <a name="if-you-receive-a-smart-detection-alert"></a>Se si riceve un avviso di rilevamento intelligente
*Perché ho ricevuto questo avviso?*

* È stato rilevato un aumento anomalo della richieste non riuscite velocità rispetto toohello normale di base di hello precedente. Dopo l'analisi di errori di hello e telemetria associato, si ritiene che si verifichi un problema che è consigliabile esaminare.

*Notifica hello significa che il problema è stato definitivamente?*

* Si tenta di tooalert in app interruzione o la riduzione, ma solo è possibile comprendere appieno la semantica di hello hello impatto e sulle app hello o utenti.

*Il servizio implica l'accesso manuale ai dati da parte di Microsoft?*

* No. servizio Hello è completamente automatico. Solo ricevere le notifiche di hello. ma i dati restano [privati](app-insights-data-retention-privacy.md).

*È necessario toosubscribe toothis avviso?*

* No. Ogni applicazione che invia richiesta di dati di telemetria ha una regola di avviso di rilevamento intelligente hello.

*È possibile annullare la sottoscrizione o ricevere le notifiche di hello invece inviate toomy colleghi?*

* Sì, le regole di avviso, fare clic su tooconfigure regola di rilevamento intelligente hello è. È possibile disabilitare l'avviso hello o modificare i destinatari dell'avviso hello.

*Ho perso la posta elettronica hello. Dove trovare le notifiche di hello nel portale di hello?*

* Nel log attività hello. In Azure, aprire la risorsa di Application Insights hello per l'app, quindi selezionare i log di attività.

*Alcuni degli avvisi di hello circa alcuni problemi noti e non si desidera che tooreceive li.*

* Nel backlog è disponibile una funzionalità per eliminare gli avvisi.

## <a name="next-steps"></a>Passaggi successivi
Questi strumenti di diagnostica consentono di controllare la telemetria hello dall'app:

* [Esplora metriche](app-insights-metrics-explorer.md)
* [Esplora ricerche](app-insights-diagnostic-search.md)
* [Linguaggio avanzato di query di Analisi](app-insights-analytics-tour.md)

Gli avvisi di rilevamento intelligente sono completamente automatici, Ma forse si vogliono tooset di alcune ulteriori avvisi?

* [Configurare manualmente gli avvisi relativi alle metriche](app-insights-alerts.md)
* [Test Web di disponibilità](app-insights-monitor-web-app-availability.md)
