---
title: aaaGet avviato con Azure Mobile Engagement per le app Web | Documenti Microsoft
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per le applicazioni Web.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Introduzione ad Azure Mobile Engagement per app Web
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle App Web.

> [!NOTE]
> servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti. Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Questa esercitazione richiede il seguente hello:

* Visual Studio 2015 o un altro editor di propria scelta
* [Web SDK](http://aka.ms/P7b453)

Questo SDK Web è disponibile in anteprima solo supporta Analitica un determinato momento hello e non supporta ancora l'invio delle notifiche push browser o nell'applicazione. 

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>Configurare Mobile Engagement per l'app Web
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato una "integrazione di base," hello set minimo richiesto toocollect dati.

Verrà creata un'app web di base con l'integrazione di Visual Studio toodemonstrate hello anche se è possibile seguire i passaggi di hello con qualsiasi applicazione web creata anche all'esterno di Visual Studio. 

### <a name="create-a-new-web-app"></a>Creare una nuova app Web
Hello passaggi seguenti si presuppongono hello utilizzo di Visual Studio 2015 se hello passaggi sono simili nelle versioni precedenti di Visual Studio. 

1. Avviare Visual Studio e in hello **Home** selezionare **nuovo progetto**.
2. Nel menu a comparsa hello, selezionare **Web** -> **applicazione Web ASP.Net**. Compilare app hello **nome**, **percorso** e **Nome soluzione**, quindi fare clic su **OK**.
3. In hello **selezionare un modello** popup, selezionare **vuoto** in **ASP.Net 4.5 modelli** e fare clic su **OK**. 

Ora è stata creata un nuovo progetto di App Web vuoto in cui integrare hello Azure Mobile Engagement Web SDK.

### <a name="connect-your-app-toomobile-engagement-backend"></a>La connessione back-end Engagement tooMobile app
1. Creare una nuova cartella denominata **javascript** nella soluzione e aggiungere il file Web SDK JS hello **azure engagement.js** al suo interno. 
2. Aggiungere un nuovo file denominato **main.js** in questa cartella di javascript con hello seguente codice. Verificare che stringa di connessione di tooupdate hello. Questo `azureEngagement` oggetto sarà utilizzato tooaccess metodi Web SDK. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio con file JS][1]

## <a name="enable-real-time-monitoring"></a>Abilitare il monitoraggio in tempo reale
In ordine toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare back-end di almeno una attività toohello Mobile Engagement. Un'attività nel contesto di hello di un'app web è una pagina web. 

1. Creare una nuova pagina denominata **home.html** nel soluzione e impostare come avvio hello pagina per l'app web. 
2. Includere JavaScript di due hello che abbiamo aggiunto in precedenza in questa pagina aggiungendo hello seguente all'interno di tag body hello. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Aggiornare hello corpo tag toocall EngagementAgent `startActivity` (metodo)
   
        <body onload="engagement.agent.startActivity('Home')">
4. Ecco come appare il file **home.html** .
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>Estendere l'analisi
Di seguito sono attualmente disponibili con SDK Web che è possibile utilizzare per analitica tutti i metodi di hello:

1. Attività/Pagine Web:
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. Events
   
        engagement.agent.sendEvent(name, extras);
3. Errori
   
        engagement.agent.sendError(name, extras);
4. Processi
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

