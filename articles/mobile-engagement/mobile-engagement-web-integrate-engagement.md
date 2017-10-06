---
title: integrazione di Mobile Engagement Web SDK aaaAzure | Documenti Microsoft
description: "Hello procedure per hello Azure Mobile Engagement Web SDK e gli aggiornamenti più recenti"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Integrare Azure Mobile Engagement in un'applicazione Web
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

procedure Hello in questo articolo vengono descritti analitica hello più semplice modo tooactivate hello e funzioni in Azure Mobile Engagement nell'applicazione web di monitoraggio.

Seguire hello passaggi tooactivate hello report del log che sono necessari toocompute tutte le statistiche sugli utenti, sessioni, attività, arresti anomali del sistema e technicals. Per le statistiche di dipendenti dall'applicazione, ad esempio eventi, errori e i processi, è necessario attivare manualmente i report di log utilizzando l'API di Azure Mobile Engagement hello. Per ulteriori informazioni, vedere [come toouse hello avanzate tag API in un'applicazione web di Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Introduzione
[Scaricare hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).
Hello Web di Mobile Engagement SDK viene fornito come un singolo file JavaScript, azure-engagement.js, aver tooinclude in ogni pagina dell'applicazione web o del sito.

> [!IMPORTANT]
> Prima di eseguire questo script, è necessario eseguire uno script o scrivere tooconfigure Mobile Engagement per l'applicazione di frammento di codice.
> 
> 

## <a name="browser-compatibility"></a>Compatibilità dei browser
Hello Mobile Engagement Web SDK Usa JSON native di codifica e decodifica inoltre le richieste AJAX toocross dominio (basarsi sulla specifica W3C CORS hello). È compatibile con hello seguenti browser:

* Microsoft Edge 12+
* Internet Explorer 10+
* Firefox 3.5+
* Chrome 4+
* Safari 6+
* Opera 12+

## <a name="configure-mobile-engagement"></a>Configurare Mobile Engagement
Scrivere uno script che crea globale `azureEngagement` oggetto JavaScript, come in hello di esempio seguente. Poiché il sito potrebbe essere composto da più pagine, questo esempio presuppone che lo script sia incluso in ogni pagina. In questo esempio è denominato oggetto JavaScript hello `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Hello `connectionString` valore per l'applicazione viene visualizzata nel portale di Azure hello.

> [!NOTE]
> `appVersionName` e `appVersionCode` sono facoltativi. Si consiglia tuttavia di configurarli in modo che l'analisi possa elaborare le informazioni relative alla versione.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Includere script di Mobile Engagement nelle pagine
Aggiungere pagine tooyour gli script di Mobile Engagement in uno dei seguenti modi hello:

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

Oppure:

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
Dopo il caricamento di uno script di Mobile Engagement Web SDK hello crea hello **engagement** tooaccess alias hello API SDK. Non è possibile utilizzare questa configurazione di alias toodefine hello SDK. In questa documentazione l'alias viene usato come riferimento.

Si noti che se l'alias predefinito hello in conflitto con un'altra variabile globale dalla pagina, è possibile ridefinirla nella configurazione di hello come indicato di seguito prima di caricare hello Mobile Engagement Web SDK:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>Segnalazione di base
La segnalazione di base in Mobile Engagement riguarda le statistiche a livello di sessione, ad esempio le statistiche relative a utenti, sessioni, attività e arresti anomali del sistema.

### <a name="session-tracking"></a>Monitoraggio di una sessione
Una sessione di Mobile Engagement è suddivisa in una sequenza di attività identificate da un nome.

In un sito Web classico è consigliabile dichiarare un'attività diversa in ogni pagina del sito. Per una sito o applicazione web in cui hello pagina corrente non cambia mai, le attività di hello tootrack su scala ridotta, potrebbe essere, ad esempio all'interno di pagina hello.

Ovvero, toostart o modifica hello attività corrente dell'utente chiamata hello `engagement.agent.startActivity` (funzione). ad esempio:

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

server di Mobile Engagement Hello termina automaticamente una sessione aperta all'interno di tre minuti dopo la chiusura di una pagina dell'applicazione hello.

In alternativa, è possibile terminare una sessione manualmente chiamando `engagement.agent.endActivity`. Consente di impostare too'Idle attività utente corrente di hello.'  sessione Hello terminerà dopo 10 secondi, a meno che una nuova chiamata`engagement.agent.startActivity` riprende una sessione di hello.

È possibile configurare il ritardo di 10 secondi hello nell'oggetto globale engagement hello, come indicato di seguito:

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> Non è possibile utilizzare `engagement.agent.endActivity` in hello `onunload` callback perché in questa fase non è possibile apportare le chiamate AJAX.
> 
> 

## <a name="advanced-reporting"></a>Segnalazione avanzata
Facoltativamente, se si desidera processi, errori ed eventi di tooreport specifiche dell'applicazione, è necessario toouse hello API di Mobile Engagement. Si accede hello API di Mobile Engagement tramite hello `engagement.agent` oggetto.

È possibile accedere a tutti i hello avanzate funzionalità di Mobile Engagement in hello API di Mobile Engagement. API Hello è descritta in dettaglio nell'articolo hello [come toouse hello avanzate tag API in un'applicazione web di Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-hello-urls-used-for-ajax-calls"></a>Personalizzare gli URL hello utilizzati per le chiamate AJAX
È possibile personalizzare gli URL che hello che usa Web di Mobile Engagement SDK. Ad esempio, tooredefine hello log URL (hello SDK dell'endpoint per la registrazione), è possibile eseguire l'override di configurazione hello come segue:

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

Se le funzioni dell'URL restituiranno una stringa che inizia con `/`, `//`, `http://`, o `https://`, non viene utilizzato lo schema predefinito di hello. Per impostazione predefinita, hello `https://` schema viene utilizzato per tali URL. Se si desidera schema predefinito di hello toocustomize, eseguire l'override di configurazione hello, simile al seguente:

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
