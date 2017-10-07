---
title: Avvisi aaaSet in Azure Application Insights | Documenti Microsoft
description: "Ricevere notifiche su tempi di risposta più lenti, eccezioni e altre prestazioni o modifiche nell'uso delle app Web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Impostare gli avvisi in Application Insights
[Azure Application Insights] [ start] può inviare un avviso toochanges nelle metriche delle prestazioni o l'utilizzo nell'app web. 

Application Insights consente di monitorare l'app in tempo reale in un [ampia gamma di piattaforme] [ platforms] toohelp diagnosticare problemi di prestazioni e comprendere i modelli di utilizzo.

Esistono tre tipologie di avvisi:

* Gli **avvisi delle metriche** indicano quando una qualsiasi metrica supera un valore di soglia per un determinato periodo, ad esempio i tempi di risposta, il numero di eccezioni, l'uso della CPU o il numero di visualizzazioni della pagina. 
* [**Test Web** ] [ availability] indicano quando non è disponibile nel hello sito internet o risponde lentamente. [Altre informazioni][availability].
* [**La funzionalità diagnostica proattiva** ](app-insights-proactive-diagnostics.md) vengono configurate automaticamente toonotify di modelli di prestazioni insoliti.

L'articolo è incentrato sugli avvisi delle metriche.

## <a name="set-a-metric-alert"></a>Impostare un avviso metrica
Pannello regole di avviso hello aprire, quindi utilizzare hello pulsante Aggiungi. 

![Nel pannello regole di avviso hello, scegliere Aggiungi avviso. Impostare l'app come hello toomeasure risorse, fornire un nome per l'avviso hello e scegliere una metrica.](./media/app-insights-alerts/01-set-metric.png)

* Impostare altre proprietà di risorsa hello prima hello. **Scegliere la risorsa hello "(componenti)"** se si desidera tooset avvisi sulle metriche delle prestazioni o sull'utilizzo.
* nome Hello che è possibile assegnare toohello avviso deve essere univoco nel gruppo di risorse hello (non solo l'applicazione).
* Essere unità hello toonote attenzione in cui viene chiesto di valore di soglia tooenter hello.
* Se si seleziona la casella hello "... per i proprietari di posta elettronica", gli avvisi vengono inviati tramite tooeveryone di posta elettronica con gruppo di risorse toothis di accesso. tooexpand questo set di utenti, aggiungerli toohello [gruppo di risorse o sottoscrizione](app-insights-resources-roles-access-control.md) (non hello risorsa).
* Se si specifica "Ulteriori messaggi di posta elettronica", gli avvisi vengono inviati toothose persone o gruppi (se è stata selezionata hello "email proprietari..." casella). 
* Impostare un [webhook indirizzo](../monitoring-and-diagnostics/insights-webhooks-alerts.md) se è stata impostata un'app web che risponde tooalerts. Viene chiamato quando viene attivato l'avviso hello e quando viene risolto. Si noti però che attualmente i parametri di query non vengono passati come proprietà webhook.
* È possibile disabilitare o abilitare hello avviso: hello pulsanti nella parte superiore di hello del pannello hello.

*Pulsante di hello Aggiungi avviso non è presente.* 

* Si sta usando un account aziendale? È possibile impostare avvisi se si dispone di risorse di applicazione toothis accesso proprietario o collaboratore. Esaminare il pannello di controllo di accesso hello. [Informazioni sul controllo di accesso][roles].

> [!NOTE]
> Nel pannello avvisi hello, vedrai che è già presente un avviso set di: [diagnostica proattiva](app-insights-proactive-failure-diagnostics.md). Avviso automatico Hello controlla una particolare metrica, percentuale errori. A meno che non si decide di avviso proattivo di hello toodisable, non è necessario tooset avviso al tasso di errore di richiesta. 
> 
> 

## <a name="see-your-alerts"></a>Visualizzare gli avvisi
Si riceve un messaggio di posta elettronica quando lo stato dell'avviso passa da inattivo ad attivo e viceversa. 

stato corrente di Hello di ogni avviso viene visualizzato nel pannello regole di avviso hello.

È un riepilogo delle attività recenti negli avvisi hello elenco a discesa:

![Menu a discesa degli avvisi](./media/app-insights-alerts/010-alert-drop.png)

cronologia Hello modifiche di stato è hello Log attività:

![Nel pannello della panoramica hello, fare clic su impostazioni, i log di controllo](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Funzionamento degli avvisi
* Un avviso può avere tre stati: "Mai attivato", "Attivato" e "Risolto". Attivato indica hello condizione specificata è true, quando l'ultima valutazione.
* Quando lo stato di un avviso viene modificato, viene generata una notifica. (Se la condizione dell'avviso hello era già true al momento della creazione avviso hello, si potrebbe ottenere una notifica fino a quando non diventa false condizione hello.)
* Ogni notifica genera un messaggio di posta elettronica se hello messaggi di posta elettronica casella selezionata o indirizzi di posta elettronica fornito. È anche possibile esaminare hello notifiche riepilogo.
* Un avviso viene valutato ogni volta che arriva una metrica, ma non altrimenti.
* valutazione Hello aggrega metrica hello su hello precedente e confronta quindi toohello soglia toodetermine hello nuovo stato.
* Specifica il periodo di Hello prescelto intervallo hello durante il quale le metriche vengono aggregate. Non influisce sulla frequenza hello avviso valutazione: che dipende dalla frequenza di hello di arrivo delle metriche.
* Se nessun dato arriva per una determinata metrica per un certo tempo, diversi effetti sulla valutazione degli avvisi e nei grafici hello in Esplora metrica gap hello. In Esplora metrica, se non viene visualizzato alcun dato per più di intervallo di campionamento del grafico hello hello grafico mostra un valore pari a 0. Ma un avviso in base a hello stessa metrica non verranno rivalutate e hello subisce lo stato dell'avviso. 
  
    Quando si arrivano alla fine dei dati, grafico hello passa valore diverso da zero tooa indietro. avviso di Hello valuta in base ai dati hello disponibili per il periodo di hello specificato. Se il nuovo punto di dati hello hello unico disponibile nel periodo di hello, hello aggregazione si basa solo da che punto dati.
* Un avviso può spesso passare velocemente dallo stato di avviso a quello integro e viceversa, anche se si imposta un periodo prolungato. Questa situazione può verificarsi se il valore della metrica hello si aggira intorno soglia hello. Non vi è alcun isteresi nella soglia hello: hello transizione tooalert avviene a hello hello transizione toohealthy lo stesso valore.

## <a name="what-are-good-alerts-tooset"></a>Quali sono avvisi buona tooset?
Dipende dall'applicazione. toostart con, è ottimale tooset non un numero eccessivo di metriche. Tempo esaminando i grafici metrica durante l'esecuzione dell'app, tooget un'idea di come si comporta normalmente. Questo metodo consente di individuare i modi tooimprove le prestazioni. Quindi configurare avvisi tootell si quando metriche hello andare fuori zona normale hello. 

Gli avvisi più diffusi includono:

* Le [metriche del browser][client], soprattutto i **tempi di caricamento delle pagine** del browser, sono ottimali per le applicazioni Web. Se la pagina contiene molti script, è consigliabile cercare le **eccezioni del browser**. In ordine tooget queste metriche e gli avvisi, è necessario tooset [pagina monitoraggio][client].
* **Tempo di risposta server** per hello sul lato server applicazioni web. Nonché configurare gli avvisi, tenere sotto controllo la metrica toosee se eccessivamente varia con frequenza elevata di richieste: variazione potrebbe indicare che l'app sta esaurendo le risorse. 
* **Eccezioni del server** -toosee loro, si dispone di alcune toodo [impostazioni aggiuntive](app-insights-asp-net-exceptions.md).

Non dimenticare che [diagnostica Frequenza errori proattiva](app-insights-proactive-failure-diagnostics.md) automaticamente hello frequenza con cui l'app risponde toorequests con codici di errore. 

## <a name="automation"></a>Automazione
* [Utilizzare PowerShell tooautomate impostazione di avvisi](app-insights-powershell-alerts.md)
* [Usare i webhook tooautomate risponde tooalerts](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Vedere anche
* [Test Web di disponibilità](app-insights-monitor-web-app-availability.md)
* [Automatizzare la configurazione degli avvisi](app-insights-powershell-alerts.md)
* [Diagnostica proattiva](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

