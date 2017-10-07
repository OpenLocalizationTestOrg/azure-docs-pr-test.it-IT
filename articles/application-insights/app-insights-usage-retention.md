---
title: analisi di conservazione aaaUser per le applicazioni web con Azure Application Insights | Documenti Microsoft
description: Il numero di utenti restituiti tooyour app?
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Analisi della conservazione degli utenti per applicazioni Web con Application Insights

funzionalità di memorizzazione Hello [Azure Application Insights](app-insights-overview.md) si analizza il numero di utenti consente di restituiscono tooyour app e la frequenza con cui eseguire attività specifiche o a scopi. Ad esempio, se si esegue un sito di gioco, è possibile confrontare un numero di utenti che restituiscono toohello sito dopo la perdita di un gioco con numero di hello che restituiscono dopo dominante hello. Queste informazioni consentono di migliorare sia l'esperienza per l'utente che la strategia aziendale.

## <a name="get-started"></a>Attività iniziali

Se non viene visualizzato ancora dati strumento memorizzazione hello nel portale Application Insights hello [informazioni su come tooget iniziare con strumenti di gestione di hello](app-insights-usage-overview.md).

## <a name="hello-retention-tool"></a>strumento di conservazione Hello

![Strumento Conservazione](./media/app-insights-usage-retention/retention.png)

1. barra degli strumenti Hello consente agli utenti i nuovi report conservazione toocreate, aprire i report esistenti di memorizzazione, salvare i report di memorizzazione corrente o Salva con nome, annullare le modifiche apportate toosaved report, aggiornare i dati nel report hello, condivisione di report tramite posta elettronica o un collegamento diretto e hello accesso pagina della documentazione. 
2. Per impostazione predefinita, il report di conservazione mostra tutti gli utenti che non hanno fatto alcuna operazione, poi sono tornati e non hanno fatto altro per un periodo. È possibile selezionare una diversa combinazione di eventi toonarrow hello riguardano le attività dell'utente specifico.
3. Aggiungere uno o più filtri alle proprietà. Ad esempio, è possibile concentrarsi sugli utenti di un determinato paese o area. Fare clic su **aggiornamento** dopo l'impostazione di filtri hello. 
4. Hello complessivo memorizzazione grafico mostra un riepilogo del mantenimento dei dati utente tra hello periodo di tempo selezionato. 
5. griglia Hello Mostra hello numero di utenti di conservazione generatore delle query toohello secondo in #2. Ogni riga rappresenta una coorte nel programma di utenti che hanno eseguito qualsiasi evento nel tempo hello periodo indicato. Ogni cella della riga hello viene restituito il numero di tale coorte almeno una volta in un periodo successivo. Alcuni utenti potrebbero ritornare in periodi diversi. 
6. schede di approfondimenti Hello mostrano i primi cinque eventi di origine e prime cinque restituito utenti toogive eventi una migliore comprensione del loro report di conservazione. 

![Passaggio del mouse sullo strumento Conservazione](./media/app-insights-usage-retention/hover.png)

Gli utenti è possono passare il mouse sulle celle sul pulsante di hello memorizzazione strumento tooaccess hello analitica e descrizioni comandi che spiega quali cella hello significa. pulsante Analitica Hello accetta strumento Analitica toohello di utenti con gli utenti toogenerate una query già popolati dalla cella hello. 

## <a name="use-business-events-tootrack-retention"></a>Utilizzare la memorizzazione dei tootrack gli eventi di business

tooget hello utili memorizzazione analysis, gli eventi di misure che rappresentano le attività di business significativo. 

Ad esempio, molti utenti potrebbero aprire una pagina nell'app senza hello gioco che vengono visualizzati. Rilevamento solo visualizzazioni di pagina hello fornisce pertanto una stima imprecisa di quante persone hanno restituito tooplay gioco hello dopo a sfruttare in precedenza. tooget un quadro preciso di restituzione dei lettori, l'app deve inviare un evento personalizzato quando un utente viene riprodotto.  

È buona norma toocode eventi personalizzati che rappresentano azioni aziendali principali e utilizzano per l'analisi di memorizzazione. risultato di gioco hello toocapture, è necessario toowrite una riga di codice toosend tooApplication un evento personalizzato Insights. Se si scrive il codice della pagina web hello o Node.JS, l'aspetto è simile al seguente:

```JavaScript
    appinsights.trackEvent("won game");
```

O nel codice server di ASP.NET:

```C#
   telemetry.TrackEvent("won game");
```

[Altre informazioni sulla scrittura di eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>Passaggi successivi
- utilizzo di tooenable esperienze, avviare l'invio [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se si invia già hello utilizzo strumenti toolearn di esplorare gli eventi personalizzati o le visualizzazioni di pagina, come gli utenti di usare il servizio.
    - [Utenti, sessioni ed eventi](app-insights-usage-segmentation.md)
    - [Grafici a imbuto](usage-funnels.md)
    - [Flussi degli utenti](app-insights-usage-flows.md)
    - [Cartelle di lavoro](app-insights-usage-workbooks.md)
    - [Aggiungere il contesto utente](app-insights-usage-send-user-context.md)


