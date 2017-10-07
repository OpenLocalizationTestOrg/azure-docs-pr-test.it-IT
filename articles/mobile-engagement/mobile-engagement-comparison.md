---
title: aaaComparing Azure Mobile Engagement con altri servizi Azure simili
description: 'Confronto tra Azure Mobile Engagement e altri servizi Azure simili: HockeyApp, AppInsights e Notification Hubs'
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f114775-3a9a-4dd4-8d59-b10d1da9a68b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0859ae9980d0fa96ffbc0edfbd795ccc58d2c843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-azure-mobile-engagement-with-other-similar-azure-services"></a>Confronto tra Azure Mobile Engagement e altri servizi Azure simili
elenco di Hello dei servizi offerti da Microsoft Azure è continua espansione e in alcuni casi è possibile chiedersi come Azure Mobile Engagement diverso da questo altro servizio che è stato letto o informazioni. In questo articolo tenta confusione hello tooclear e indirizza toochoose Azure Mobile Engagement quando è più appropriato per l'utilizzo. 

Azure Mobile Engagement è un servizio di destinazione in modo specifico **per gli esperti di marketing/CMOs digitale** ma potrebbe essere utilizzata da qualsiasi **proprietario di app per dispositivi mobili o server di pubblicazione** che richiede l'utilizzo di hello tooincrease, conservazione e monetizzazione delle loro App per dispositivi mobili. 

*Si tratta di una piattaforma SaaS (software-as-a-service) di engagement degli utenti che offre informazioni basate sui dati relative all'utilizzo dell'app e alla segmentazione degli utenti in tempo reale, nonché notifiche push intelligenti e contestualizzate e messaggistica in-app.* 

Suddivisione questa definizione, abbiamo hello seguenti caratteristiche principali che evidenzia inoltre la proposta di valore univoco:

1. **Notifiche push contestualizzate e messaggistica in-app**
   
   Questo è lo stato attivo principale hello del prodotto hello - eseguire le notifiche push personalizzate e di destinazione. E per questo toohappen, si raccolgono dati di analitica comportamentali rich. 
2. **Analisi dell'uso delle app in base ai dati**
   
   Offriamo multipiattaforma SDK toocollect hello comportamentali analitica sugli utenti app hello. Nota analitica comportamentali di termine hello (invece di un analitica prestazioni), poiché verrà esaminato come utenti app hello usano app hello. Verranno raccolti dati analitica delle prestazioni di base su errori, arresti anomali del sistema e così via, ma vale a dire non hello core lo stato attivo del prodotto hello. 
3. **Segmentazione degli utenti in tempo reale**
   
   Dopo aver raccolto i dati di analitica comportamento degli utenti dell'app, viene offerta toosegment i destinatari in base a diversi parametri e i dati raccolti tooenable toorun è destinata campagne push. 
4. **SaaS (Software-as-a-service):**
   
   Si dispone di un portale separato dal portale di gestione di Azure hello che è ottimizzato toointeract Visualizza analitica comportamentali avanzate relative agli utenti di app hello ed eseguire push campagne di marketing. prodotto Hello è pensati tooget usarlo in nessuna circostanza!   

Con questo set di differenziazione mano, ecco come si confrontare altri apparentemente simili offerte di Azure - nota tale articolo hello non esegue un confronto di livello di funzionalità, ma ha un più toodefine di approccio scenario basato su più adatto del prodotto:

1. [HockeyApp](https://azure.microsoft.com/services/hockeyapp/) è hello mobili DevOps soluzione Microsoft. Con, è possibile distribuire le compilazioni toobeta tester, raccogliere i dati di arresto anomalo del sistema e ottenere commenti degli utenti. Si integra con Visual Studio Team Services, semplificando la distribuzione delle compilazioni e l'integrazione degli elementi di lavoro. 
   
   lo stato attivo Hello è su DevOps e la raccolta dati sulle App per dispositivi mobili hello analitica prestazioni. Potrebbe essere necessario con l'integrazione sia HockeyApps e Mobile Engagement in app e che non è insolito perché anche se alcuni sovrapposizione nei dati raccolti hello, lo stato attivo principale hello dei prodotti hello è diverso e possono raggiungere diversi obiettivi per l'utente.  
2. [Application Insights](../application-insights/app-insights-overview.md) se app per dispositivi mobili sono sul lato server, quindi si utilizzerà lato server dell'app Application Insights toomonitor hello web ma hello client side App per dispositivi mobili, è necessario utilizzare HockeyApp. 
3. [Gli hub di notifica](https://azure.microsoft.com/services/notification-hubs/) fornisce un semplice servizio nel senso hello che non è necessario un SDK integrato nell'app per dispositivi mobili hello e si può avere il controllo completo di app per dispositivi mobili e consente l'invio di notifiche push con funzionalità di assegnazione di tag di base. Questo è molto utile per qualsiasi proprietario dell'applicazione non interessato minore sull'indirizzamento e più l'invio di comunicare informazioni immediatamente tootheir app gli utenti (popolamento di grandi dimensioni tooa broadcast). 
   
   Si noti hello lo stato attivo qui sull'invio di notifiche veloce velocissima con funzionalità di base di segmentazione. 

Seguono alcuni scenari:

1. TIM fa parte del team di marketing digitale hello all'archivio di Adventure Works che pubblica l'App per dispositivi mobili per gli utenti. Obiettivo di TIM è che gli utenti di hello che scaricano le App per dispositivi mobili continuare toouse tooensure e di frequente. Ciò aumenta non solo una marca di collegare con gli utenti dell'applicazione hello ma anche monetizzazione aumenta quando gli utenti dell'applicazione hello acquisti tramite hello app per dispositivi mobili. Per questo Tim necessario toosend destinazione notifiche toohello app gli utenti, che sono utili, tooencourage li tooopen hello app e tornare tooit spesso. In questo contesto, a Giulio servirà Mobile Engagement. 
2. Scritto JoAnn fa parte del team di sviluppo hello di hello App per dispositivi mobili Adventure Works è cercando un'arresti anomali del sistema, le eccezioni, i dettagli toolog prodotto e ottenere dati di telemetria delle prestazioni da un'app. In questo contesto, a Giovanna farà comodo HockeyApp. Scritto JoAnn Impossibile integrare entrambi HockeyApp per proprio sviluppatore con stato attivo con gli scenari e Azure Mobile Engagement per Tim hello stesso hello tooget app migliore di entrambi. 
3. Round robin fa parte del team di sviluppo hello di App per dispositivi mobili hello a rete notizie di Contoso e in tutti desiderate è toosend le ultime notizie avvisi tooall che gli utenti senza quantità segmentazione non appena viene attivato l'avviso di notizie hello. In questo caso, a Roberta serviranno gli hub di notifica. 
   In questo scenario, è possibile tuttavia che evoluzione hello app per dispositivi mobili, è un requisito toodo molto più ricche dettagli segmentazione e ottenere informazioni sul comportamento dell'utente dell'applicazione hello. In questo momento, Round Robin avrà tooevaluate Azure Mobile Engagement. 

toorecap, scopo hello di Mobile Engagement non appena toocollect analitica: non è "un altro prodotto Analitica da Microsoft". È sull'invio di notifiche push di destinazione e per questa destinazione, è raccogliere i dati di comportamento analitica, ma lo stato attivo hello rimane sull'invio di notifiche push che rendono la maggior parte degli utenti di app toohello senso hello in modo che non è come posta indesiderata. 

Per ulteriori dettagli, vedere questo [video rapido](mobile-engagement-overview.md) che sintetizza Mobile Engagement. 

