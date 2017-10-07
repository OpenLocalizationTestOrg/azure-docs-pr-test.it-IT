---
title: aaaAzure Mobile Engagement Troubleshooting Guide - API
description: Guide alla risoluzione dei problemi di Azure Mobile Engagement - API
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a>Guida alla risoluzione dei problemi relativi all’API
di seguito Hello sono possibili problemi che possono verificarsi come amministratori interagiscono con Azure Mobile Engagement tramite hello API.

## <a name="syntax-issues"></a>Problemi di sintassi
### <a name="issue"></a>Problema
* Errori di sintassi utilizzando API hello (o un comportamento imprevisto).

### <a name="causes"></a>Cause
* Problemi di sintassi:
  * Verificare che toocheck hello sintassi dell'API di hello specifico si utilizza tooconfirm che hello opzione è disponibile.
  * Un problema comune di utilizzo delle API è l'API di Reach tooconfuse hello e hello API Push (la maggior parte delle attività deve essere eseguita con hello API Reach anziché hello API Push). 
  * Un altro problema comune con l'integrazione SDK e utilizzo delle API è hello tooconfuse chiave SDK e hello chiave API.
  * Gli script che si connettono toohello API necessario toosend dati almeno ogni 10 minuti o connessione hello scadrà (soprattutto negli script di monitoraggio API in attesa di dati). timeout tooprevent, disporre di un ping a XMPP ogni sessione hello tookeep 10 minuti con server hello trasmissione script.

### <a name="see-also"></a>Vedere anche
* [Documentazione dell'API][Link 4]
* [Informazioni sul protocollo XMPP](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a>Non è possibile toouse hello API tooperform hello stessa azione disponibile in hello dell'interfaccia utente di Azure Mobile Engagement
### <a name="issue"></a>Problema
* Un'azione che funziona da interfaccia utente di Azure Mobile Engagement non funziona da hello hello relative API di Azure Mobile Engagement.

### <a name="causes"></a>Cause
* Conferma che è possibile eseguire l'azione stessa dall'interfaccia utente di Azure Mobile Engagement hello mostra che è stato integrato correttamente questa funzionalità di Azure Mobile Engagement con hello hello SDK.

### <a name="see-also"></a>Vedere anche
* [Documentazione dell'interfaccia utente][Link 1]

## <a name="error-messages"></a>Messaggi di errore
### <a name="issue"></a>Problema
* Codici di errore utilizzando API hello visualizzato in fase di esecuzione o nei registri.

### <a name="causes"></a>Cause
* Di seguito, è riportato un elenco completo di codici di stato API comuni da usare come riferimento e per risolvere i problemi preliminari:
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a>Vedere anche
* [Documentazione dell'API - Errori dettagliati su ogni API specifica][Link 4]

## <a name="silent-failures"></a>Errori invisibili all'utente
### <a name="issue"></a>Problema
* Non è possibile eseguire l'azione API e non vengono visualizzati messaggi di errore nel runtime o nei registri.

### <a name="causes"></a>Cause
* Numero di elementi verrà disabilitata nell'interfaccia utente di Azure Mobile Engagement se non è integrate correttamente, ma non verranno eseguite automaticamente da hello API, pertanto tenere presente hello tootest hello funzionalità hello UI toosee se risulta appropriato.
* Azure Mobile Engagement e molte funzionalità avanzate di Azure Mobile Engagement si sta tentando di toouse, toobe necessità singolarmente integrato nell'app con hello SDK in due fasi distinte, prima di poter utilizzare.

### <a name="see-also"></a>Vedere anche
* [Guida alla risoluzione dei problemi - SDK][Link 25]

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
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

