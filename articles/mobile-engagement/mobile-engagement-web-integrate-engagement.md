---
title: Integrazione di Azure Mobile Engagement SDK per Web | Microsoft Azure
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Web
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
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Integrare Azure Mobile Engagement in un'applicazione Web
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Le procedure contenute in questo articolo descrivono il modo più semplice per attivare le funzioni di analisi e monitoraggio di Azure Mobile Engagement in un'applicazione Web.

I passaggi seguenti sono utili per attivare la segnalazione dei log necessari per calcolare tutte le statistiche relative a utenti, sessioni, attività, arresti anomali del sistema e dati tecnici. Per le statistiche dipendenti dall'applicazione, ad esempio eventi, errori e processi, è necessario attivare manualmente la segnalazione dei log tramite l'API di Azure Mobile Engagement. Per altre informazioni, leggere [Come usare l'API di Engagement in un'applicazione Web](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Introduzione
[Scaricare Azure Mobile Engagement SDK per Web](http://aka.ms/P7b453).
Il Mobile Engagement SDK per Web viene fornito come un singolo file JavaScript denominato azure-engagement.js, che deve essere incluso in ogni pagina del sito o dell'applicazione Web.

> [!IMPORTANT]
> Prima di eseguire questo script, è necessario eseguire uno script o un frammento di codice, scritto per configurare Mobile Engagement per l'applicazione.
> 
> 

## <a name="browser-compatibility"></a>Compatibilità dei browser
Il Mobile Engagement SDK per Web usa la codifica/decodifica JSON nativa e le richieste AJAX tra domini (basandosi sulla specifica W3C CORS). È compatibile con i seguenti browser:

* Microsoft Edge 12+
* Internet Explorer 10+
* Firefox 3.5+
* Chrome 4+
* Safari 6+
* Opera 12+

## <a name="configure-mobile-engagement"></a>Configurare Mobile Engagement
Scrivere uno script per creare un oggetto JavaScript `azureEngagement` globale simile al seguente. Poiché il sito potrebbe essere composto da più pagine, questo esempio presuppone che lo script sia incluso in ogni pagina. In questo esempio, l'oggetto JavaScript viene denominato `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Il valore `connectionString` per l'applicazione viene visualizzato nel portale di Azure.

> [!NOTE]
> `appVersionName` e `appVersionCode` sono facoltativi. Si consiglia tuttavia di configurarli in modo che l'analisi possa elaborare le informazioni relative alla versione.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Includere script di Mobile Engagement nelle pagine
Aggiungere gli script di Mobile Engagement alle pagine in uno dei modi seguenti:

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
Dopo aver caricato lo script di Mobile Engagement SDK per Web, viene creato l'alias **engagement** per accedere alle API dell'SDK. Non è possibile usare l'alias per definire la configurazione dell'SDK. In questa documentazione l'alias viene usato come riferimento.

Si noti che se l'alias predefinito è in conflitto con un'altra variabile globale della pagina, sarà possibile ridefinirlo nella configurazione prima di caricare il Mobile Engagement SDK per Web nel modo seguente:

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

In un sito Web classico è consigliabile dichiarare un'attività diversa in ogni pagina del sito. Per una sito o un'applicazione Web in cui la pagina corrente non cambia mai, si desidera monitorare le attività su scala ridotta, ad esempio all'interno della pagina.

In entrambi i casi, per avviare o modificare l'attività utente corrente, chiamare la funzione `engagement.agent.startActivity` . Ad esempio: 

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

Il server di Mobile Engagement termina automaticamente una sessione aperta entro 3 minuti dalla chiusura della pagina dell'applicazione.

In alternativa, è possibile terminare una sessione manualmente chiamando `engagement.agent.endActivity`. Ciò consente di impostare l'attività dell'utente corrente su "Idle".  La sessione terminerà dopo 10 secondi fino a quando una nuova chiamata a `engagement.agent.startActivity` riprenda la sessione.

È possibile configurare il ritardo di 10 secondi nell'oggetto engagement globale, come segue:

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> Non è possibile usare `engagement.agent.endActivity` nel callback `onunload` perché non è possibile eseguire chiamate AJAX in questa fase.
> 
> 

## <a name="advanced-reporting"></a>Segnalazione avanzata
Facoltativamente, per segnalare eventi, errori e processi specifici dell'applicazione, è necessario usare l'API di Mobile Engagement. È possibile accedere alle API di Mobile Engagement tramite l'oggetto `engagement.agent` .

È possibile accedere a tutte le funzionalità avanzate di Mobile Engagement nell'API di Mobile Engagement. Per altre informazioni sull'API, leggere [Come usare l'API di Engagement in un'applicazione Web](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-the-urls-used-for-ajax-calls"></a>Personalizzare gli URL usati per le chiamate AJAX
È possibile personalizzare gli URL usati dal Mobile Engagement SDK per Web. Ad esempio, per ridefinire l'URL di accesso (l'endpoint SDK per l'accesso), è possibile eseguire l'override della configurazione in modo simile al seguente:

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

Se le funzioni URL restituiscono una stringa che inizia con `/`, `//`, `http://` o `https://`, lo schema predefinito non è usato. Per impostazione predefinita, per tali URL viene usato lo schema `https://` . Se si desidera personalizzare lo schema predefinito, eseguire l'override della configurazione in modo simile al seguente:

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
