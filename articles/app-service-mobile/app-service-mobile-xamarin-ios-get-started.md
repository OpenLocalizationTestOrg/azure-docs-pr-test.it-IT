---
title: aaaGet avviato con App Mobile di servizio App di Azure per le app xamarin | Documenti Microsoft
description: Seguire questa esercitazione tooget introduttive sull'utilizzo di App per dispositivi mobili per lo sviluppo di xamarin. IOS.
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Creare un'app per Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come tooadd un back-end basato su cloud service tooa xamarin app per dispositivi mobili utilizzando un back-end dell'app per dispositivi mobili di Azure.  Verranno creati un nuovo back-end di app per dispositivi mobili e una semplice app Xamarin.iOS *Todo list* che archivia i dati delle app in Azure.

Completato questa esercitazione è un prerequisito per tutte le altre esercitazioni di xamarin sulla funzionalità delle App per dispositivi mobili hello in Azure App Service.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:

* Un account Azure attivo. Se non si dispone di un account, iscriversi a una versione di valutazione di Azure e iniziare a too10 libero App per dispositivi mobili che è possibile continuare a usare anche il termine di valutazione. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio con Xamarin. Per le istruzioni vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .
* Un computer Mac in cui siano stati installati Xcode v7.0 o versione successiva e Xamarin Studio Community. Vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configurazione, installazione e verifiche per gli utenti Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Creare un back-end dell'app per dispositivi mobili di Azure
Seguire questi toocreate passaggi un back-end dell'App Mobile.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Configurare il progetto server di hello
È stato eseguito il provisioning di un back-end dell'app per dispositivi mobili di Azure che può essere usato dalle applicazioni client per dispositivi mobili. Successivamente, scaricare un progetto server di un semplice "elenco di attività" back-end e pubblicarlo tooAzure.

Seguire i seguenti passaggi tooconfigure hello server progetto toouse hello back-end entrambi hello, Node.js o .NET.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Scaricare ed eseguire app xamarin hello
1. Aprire hello [portale di Azure] in una finestra del browser.
2. Nel Pannello di hello impostazioni per l'App Mobile, fare clic su **iniziare** > **xamarin**. Al passaggio 3 fare clic su **Crea una nuova app** , se l'opzione non è già selezionata.  Fare clic su hello **scaricare** pulsante.

      Un'applicazione client che si connette back-end mobile tooyour viene scaricata. Salvare il file di progetto in formato compresso hello nel computer locale e prendere nota del dove salvarla.
3. Estrarre il progetto hello scaricato e aprirlo in Xamarin Studio (o Visual Studio).

    ![][9]

    ![][8]
4. Premere progetto hello toobuild chiave F5 di hello e avviare l'applicazione hello nell'emulatore iPhone hello.
5. Nell'app hello, digitare un testo significativo, ad esempio *informazioni su Xamarin*, quindi fare clic su hello  **+**  pulsante.

    ![][10]

    Dati richiesta hello viene inseriti nella tabella TodoItem hello. Vengono restituiti gli elementi archiviati nella tabella hello dal back-end di hello app per dispositivi mobili e i dati vengono visualizzati nell'elenco di hello.

> [!NOTE]
> È possibile esaminare il codice hello che accede a tooquery di back-end le app per dispositivi mobili e inserire i dati nel file c# QSTodoService.cs hello.
>
>

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere app tooyour sincronizzazione Offline](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Aggiungere app tooyour authentication](app-service-mobile-xamarin-ios-get-started-users.md)
* [Aggiungere app xamarin tooyour di notifiche push](app-service-mobile-xamarin-ios-get-started-push.md)
* [Modalità di gestione client per App mobili di Azure hello toouse](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[portale di Azure]: https://portal.azure.com/
