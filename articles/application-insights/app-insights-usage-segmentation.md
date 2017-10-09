---
title: analisi aaaUser, sessione ed eventi in Application Insights di Azure | Documenti Microsoft
description: Analisi demografica degli utenti dell'app Web.
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Analisi di utenti, sessioni ed eventi in Application Insights

Scoprire quando le persone usano l'app Web, a quali pagine sono più interessati, dove si trovano, quali browser e sistemi operativi usano. Analizzare i dati di telemetria sull'utilizzo e sull'azienda con [Azure Application Insights](app-insights-overview.md).

## <a name="get-started"></a>Attività iniziali

Se non viene visualizzato ancora dati hello utenti, sessioni o blade eventi nel portale Application Insights hello [informazioni su come tooget iniziare con strumenti di gestione di hello](app-insights-usage-overview.md).

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>strumento di segmentazione Hello utenti, sessioni e gli eventi

Tre di utilizzo di hello pannelli utilizzano hello stesso strumento tooslice e il dicing dei dati di telemetria dall'app web da tre diverse prospettive. Applicazione di filtri e suddividere i dati di hello, consente di individuare informazioni dettagliate sull'utilizzo del relativo hello di pagine e funzionalità diverse.

* **Strumento Utenti**: numero di persone che hanno usato l'app e le relative funzionalità.  Gli utenti vengono conteggiati tramite ID anonimi memorizzati nei cookie del browser. Una singola persona che usa browser o computer diversi verrà conteggiata più di una volta.
* **Strumento Sessioni**: il numero di sessioni delle attività dell'utente che include determinate pagine e funzionalità dell'app. Una sessione viene conteggiata dopo mezz'ora di inattività dell'utente o in seguito a un uso continuo di 24 ore.
* **Strumento Eventi**: la frequenza con cui vengono usate alcune pagine e funzionalità dell'app. La visualizzazione di una pagina viene conteggiata quando un browser carica la pagina dell'app, purché sia stata [instrumentata](app-insights-javascript.md). 

    Un evento personalizzato rappresenta un'occorrenza di un problema verificatosi nell'app, spesso un'interazione dell'utente fare clic su un pulsante o hello completamento di alcune delle attività. Inserire codice nell'app troppo[generare eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent).

![Strumento Uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Esecuzione di query per determinati utenti 

Esplorare i diversi gruppi di utenti modificando le opzioni di query hello nella parte superiore di hello dello strumento di hello utenti: 

* Who used (Usato da): scegliere gli eventi personalizzati e le visualizzazioni di pagina. 
* Durante: scegliere un intervallo di tempo. 
* Da: Scegliere come toobucket hello dati, per un periodo di tempo o da un'altra proprietà, ad esempio browser o una città. 
* Divisione: Scegliere una proprietà per i dati di hello toosplit o segmento. 
* Aggiungere filtri: Limitare hello query toocertain utenti, sessioni o gli eventi in base alle relative proprietà, ad esempio browser o una città. 
 
## <a name="saving-and-sharing-reports"></a>Salvataggio e condivisione di report 
È possibile salvare i report agli utenti, entrambi tooyou privata solo nella sezione report personali hello o condivisi con tutti gli utenti con accesso toothis risorsa di Application Insights hello sezione report condiviso.  
 
Durante il salvataggio di un report o la modifica delle proprietà, scegliere "Intervallo di tempo relativo corrente" toosave che un report verrà continuamente l'aggiornamento dati, se si torna indietro certa quantità di tempo fisso.  
 
Scegliere "Intervallo di tempo assoluto corrente" toosave un report con un set di dati predefinito. Tenere presente che i dati in Application Insights viene archiviati solo per 90 giorni, pertanto se sono trascorsi più di 90 giorni da un report con un intervallo di tempo assoluto è stato salvato, report hello apparirà vuoto. 
 
## <a name="example-instances"></a>Istanze di esempio

sezione di esempio istanze Hello Mostra informazioni su un numero limitato di singoli utenti, sessioni o gli eventi corrispondenti a query corrente hello. Prendere in considerazione ed esplorare i comportamenti di hello dei singoli utenti, in aggiunta tooaggregates, forniscono informazioni dettagliate sul modo le persone usano effettivamente l'app. 
 
## <a name="insights"></a>Informazioni dettagliate 

intestazione laterale approfondimenti Hello Mostra cluster di grandi dimensioni di utenti che condividono le proprietà comuni. Questi cluster consentono di individuare andamenti sorprendenti sulle modalità di uso dell'app. Se ad esempio 40% di utilizzo di hello dell'app tutti provengono da utenti che utilizzano una singola funzionalità.  


## <a name="next-steps"></a>Passaggi successivi
- utilizzo di tooenable esperienze, avviare l'invio [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se si invia già hello utilizzo strumenti toolearn di esplorare gli eventi personalizzati o le visualizzazioni di pagina, come gli utenti di usare il servizio.
    - [Grafici a imbuto](usage-funnels.md)
    - [Conservazione](app-insights-usage-retention.md)
    - [Flussi degli utenti](app-insights-usage-flows.md)
    - [Cartelle di lavoro](app-insights-usage-workbooks.md)
    - [Aggiungere il contesto utente](app-insights-usage-send-user-context.md)

