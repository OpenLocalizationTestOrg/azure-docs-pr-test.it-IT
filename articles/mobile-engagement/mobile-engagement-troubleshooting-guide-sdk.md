---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: Risoluzione dei problemi relativi all'integrazione dell'SDK in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>Guida alla risoluzione dei problemi relativi all'integrazione dell'SDK
di seguito Hello sono possibili problemi che possono verificarsi con l'integrazione di Azure Mobile Engagement nell'applicazione.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>Problemi dell'SDK rilevati da un errore in un'altra area dell'applicazione
### <a name="issue"></a>Problema
* Errore relativo alla raccolta dati dell'interfaccia utente (nelle sezioni di analisi, monitoraggio, segmentazione o dashboard).
* Errori relativi alle notifiche push (le notifiche in-app, all'esterno dell'app o entrambe non funzionano).
* Errori relativi alle funzionalità avanzate (le notifiche push di monitoraggio, georilevazione o specifiche della piattaforma non funzionano).
* Errori dell'API (spesso l'errore non genera messaggi).
* Errori di servizio (nessun servizio Azure Mobile Engagement funziona per l'applicazione).

### <a name="causes"></a>Cause
* La maggior parte dei problemi necessarie toobe risolto con hello Azure Mobile Engagement SDK verranno individuati da un errore nell'applicazione (ad esempio un errore di raccolta dati dell'interfaccia utente, errore push, errore di funzionalità avanzata, errore API, arresti anomali delle applicazioni o servizio apparente interruzione).  
* Se una particolare funzionalità di Azure Mobile Engagement non è mai lavorato nell'applicazione prima di, è necessario integrazione hello toocomplete. 
* Se una particolare funzionalità di Azure Mobile Engagement funzionava e interrotto, potrebbe essere tooupgrade toohello ultima versione con hello Azure Mobile Engagement SDK. Tenere presente che esiste una versione diversa di hello Azure Mobile Engagement SDK per ogni piattaforma supportata da Azure Mobile Engagement (Android, iOS, Windows e Windows Phone).

#### <a name="sdk-integration"></a>Integrazione dell'SDK
* Azure Mobile Engagement non integrato correttamente nell'SDK (Analytics).
* Reach non integrato correttamente nell'SDK (notifiche push in-app e all'esterno dell'app).
* Certificato scaduto o versione di produzione o sviluppo non corretta (solo per iOS).
* GCM o ADM non integrato correttamente nell'SDK (solo per Android - Notifiche push di un servizio specifico).
* Verifica non integrata correttamente nell'SDK (installazione della verifica dello store).
* Località lenta o località GPS non integrata correttamente nell'SDK (selezione destinazione in base alla georilevazione).

**Vedere anche:**

* [Documentazione SDK - Guide all'integrazione][Link 5] 
* [Guida alla risoluzione dei problemi - Push][Link 23]

#### <a name="sdk-upgrade"></a>Aggiornamento dell'SDK
* Problemi di tooresolve tooupgrade SDK con le versioni precedenti di hello SDK (spesso correlate toonewer versioni del sistema operativo del dispositivo hello) è necessario.
* Disinstallare tutte le versioni precedenti dell'app dal dispositivo e reinstallare la versione più recente di hello dell'app, hello registrare nuovamente l'ID dispositivo da hello dell'interfaccia utente di Azure Mobile Engagement tooconfirm che il dispositivo utilizza hello la versione più recente dell'app.

**Vedere anche:**

* [Documentazione SDK - Note di rilascio](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [Documentazione SDK - Guide all'aggiornamento](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>Altri problemi dell'SDK
* Gli errori nel manifesto dell'applicazione "AndroidManifest.xml" possono causare Azure Mobile Engagement non toowork (solo Android).
* Un problema comune con l'integrazione SDK e utilizzo delle API è hello tooconfuse chiave SDK e hello chiave API.

**Vedere anche:**

* [Concetti - Glossario][Link 6]

## <a name="advanced-coding-issues"></a>Problemi relativi alla codifica avanzata
### <a name="issue"></a>Problema
* Codice specifico della piattaforma non direttamente correlate tooAzure che Engagement Mobile può causare problemi in iOS, Android e Windows Phone.

### <a name="causes"></a>Cause
* Molte avanzate di codifica con Azure Mobile Engagement sono causate dalla piattaforma in modo non corretto scritta codice specifico non direttamente correlate tooAzure Mobile Engagement. Sarà necessario piattaforma toohello specifico di documentazione tooconsult che si sviluppa per inoltre la documentazione di Mobile Engagement tooAzure (Android, iOS, Web, Windows e Windows Phone).
* Configurazione non corretta "categorie", impedisce il collegamento da un percorso tooanother notifica all'interno o all'esterno di hello app (solo Android). 
* Se non viene impostata "UIKit.framework" troppo "facoltativo" nel codice iOS, visualizza un "Simbolo di errore non trovato" e/o l'arresto anomalo in dispositivi iOS meno recenti (solo iOS).
* I certificati scaduti o non correttamente utilizzando hello DEV o una versione di produzione del certificato hello, push causa problemi (solo iOS).
* Esistono alcuni piattaforma tooa inerente limitazioni che non è possibile controllare Azure Mobile Engagement (ad esempio, funzionamento per center sistema hello all'esterno dell'app inserimenti in Android e iOS).
* Azure Mobile Engagement pubblica un elenco completo dei pacchetti di hello interno utilizzato da Azure Mobile Engagement per iOS e Android per riferimento. Tenere presente che alcune funzionalità di Azure Mobile Engagement sono toohello specifico della piattaforma (Android, iOS, Web, Windows e Windows Phone).

### <a name="see-also"></a>Vedere anche
* [Guida alla risoluzione dei problemi - Push][Link 23] 
* [Documentazione SDK - Note di rilascio][Link 5]
* [Documentazione SDK - Guide all'aggiornamento][Link 5]

## <a name="application-crashes"></a>Arresti anomali dell’applicazione
### <a name="issue"></a>Problema
* L'applicazione si blocca nel dispositivo hello degli utenti finali.

### <a name="causes"></a>Cause
* Informazioni sull'arresto anomalo possono essere visualizzati in hello *dell'interfaccia utente Analitica* o hello *API Analitica*
* È possibile trovare hello ID dispositivo del dispositivo di test e richiedere hello stessa azione che ha causato il toocrash di applicazione per un utente finale di toohelp identificare causa hello dell'arresto anomalo.
* Problemi noti con hello Azure Mobile Engagement SDK che causano toocrash applicazioni talvolta risolti dall'aggiornamento toohello la versione più recente di hello SDK. Verificare che toocheck hello note sulla piattaforma durante l'esame di arresti anomali del sistema.

### <a name="see-also"></a>Vedere anche
* [Documentazione SDK - Note di rilascio][Link 5]
* [Documentazione SDK - Guide all'aggiornamento][Link 5]

## <a name="app-store-upload-failures"></a>Errori di caricamento in App Store
### <a name="issue"></a>Problema
* Errori correlati toouploading hello più recente di app tooApple, Google o archivio di App di Windows hello.

### <a name="causes"></a>Cause
* App archivia talvolta blocco app con determinate funzionalità abilitate (ad esempio hello Apple Store impedisce hello ricorso IDFV nelle app di store hello e archivio GooglePlay hello hello condivisione delle informazioni di applicazione tra App). 
* Assicurarsi di controllare le note sulla versione di hello sulla piattaforma e la versione corrente di hello SDK nel caso di difficoltà di caricamento di un archivio di app toohello.

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

