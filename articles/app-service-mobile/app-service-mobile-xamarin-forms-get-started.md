---
title: aaaGet avviato con l'App per dispositivi mobili con xamarin. Forms
description: Seguire questa esercitazione toostart tramite App per dispositivi mobili per lo sviluppo di xamarin. Forms
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Creare un'app Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come una servizio back-end basato su cloud tooa xamarin. Forms app per dispositivi mobili utilizzando tooadd hello funzionalità delle App per dispositivi mobili del servizio App di Azure come back-end hello. Vengono creati un nuovo back-end di app per dispositivi mobili e una semplice app Xamarin.Forms di tipo elenco attività che archivia dati delle app in Azure.

Il completamento di questa esercitazione è un prerequisito per tutte le altre esercitazioni relative alle app per dispositivi mobili per Xamarin.Forms.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguenti:

* Un account Azure attivo. Se non si dispone di un account, è possibile iscriversi a una versione di valutazione di Azure e iniziare a too10 libero App per dispositivi mobili che è possibile continuare a usare anche il termine di valutazione. Per altre informazioni, vedere [Versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* Visual Studio con Xamarin. Per informazioni, vedere hello [impostare backup e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) pagina.

* Un computer Mac in cui siano stati installati Xcode v7.0 o versione successiva e Xamarin Studio Community. Per informazioni, vedere [Configurare e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configurazione, installazione e verifiche per gli utenti Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-a-new-mobile-apps-back-end"></a>Creare un nuovo back-end di App per dispositivi mobili

toocreate terminare una nuova App per dispositivi mobili nuovamente, hello seguenti:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

È stato configurato un back-end di App per dispositivi mobili che può essere usato dalle applicazioni client per dispositivi mobili. Successivamente, si scarica un progetto server per un back-end di elenco semplice di attività da eseguire e quindi pubblicarlo tooAzure.

## <a name="configure-hello-server-project"></a>Configurare il progetto server di hello

tooconfigure hello server progetto toouse in hello Node.js o .NET back-end, hello seguenti:

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>Scaricare ed eseguire una soluzione xamarin. Forms hello

È possibile scaricare la soluzione hello in uno dei due modi. Scaricarlo tooa Mac e aprirlo in Xamarin Studio, o scaricarlo computer Windows tooa e aprirlo in Visual Studio tramite un Mac connesso alla rete per la compilazione di app iOS hello. Per altre informazioni, vedere [Configurare e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).

In un computer Mac o Windows hello seguenti:

1. Passare toohello [portale di Azure].

2. In hello **impostazioni** pannello per app per dispositivi mobili, in **Mobile**selezionare **iniziare** > **xamarin. Forms**. In **Passaggio 3** selezionare  **Crea una nuova app** e quindi selezionare **Scarica**.

   Questa azione consente di scaricare un progetto che contiene un'applicazione client che è connesso tooyour app per dispositivi mobili. Salvare computer locale tooyour file progetto compresso hello e prendere nota del dove salvarla.

3. Estrarre il progetto hello scaricato e aprirlo in Visual Studio (Windows) o di Xamarin Studio (Mac).

   ![Progetto estratto in Xamarin Studio][9]

   ![Progetto estratto in Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a>(Facoltativo) Eseguire il progetto di iOS hello
In questa sezione si eseguirlo hello Xamarin iOS per i dispositivi iOS. Se non si usano dispositivi iOS, è possibile ignorare questa sezione.

#### <a name="in-xamarin-studio"></a>In Xamarin Studio
1. Fare clic sul progetto iOS hello e quindi selezionare **imposta come progetto di avvio**.

2. In hello **eseguire** dal menu **Avvia debug** toobuild hello progetto e avviare hello app nell'emulatore di iPhone hello.

#### <a name="in-visual-studio"></a>In Visual Studio
1. Fare clic sul progetto iOS hello e quindi selezionare **imposta come progetto di avvio**.

2. In hello **compilare** dal menu **Configuration Manager**.

3. In hello **Configuration Manager** la finestra di dialogo, seleziona hello **compilare** e **Distribuisci** progetto iOS toohello successivo di caselle di controllo.

4. toobuild hello progetto e avviare hello app nell'emulatore iPhone hello, seleziona hello **F5** chiave.

   > [!NOTE]
   > Se si verificano problemi di compilazione progetto hello, eseguire hello manager e aggiornamento toohello ultima versione del pacchetto NuGet di pacchetti di supporto Xamarin hello. Progetti di avvio rapido potrebbero essere lento tooupdate toohello ultime versioni.    
   >
   >

5. Nell'app hello, digitare un testo significativo, ad esempio *informazioni su Xamarin*, e quindi selezionare hello sul segno più (**+**).

    ![][10]

    Questa azione Invia un toohello richiesta post che nuova App per dispositivi mobili di back-end che è ospitato in Azure. Dati richiesta hello viene inseriti nella tabella TodoItem hello. Gli elementi archiviati nella tabella hello vengono restituiti per hello terminare nuovamente App per dispositivi mobili e hello dati vengono visualizzati nell'elenco di hello.

    > [!NOTE]
    > È disponibile codice hello che accede l'App per dispositivi mobili di back-end in hello file TodoItemManager.cs c# del progetto di libreria di classi portabile hello della soluzione.
    >
    >

## <a name="optional-run-hello-android-project"></a>(Facoltativo) Esegui progetto Android hello
In questa sezione si esegue il progetto di hello Xamarin droid per Android. Se non si usano dispositivi Android, è possibile ignorare questa sezione.

#### <a name="in-xamarin-studio"></a>In Xamarin Studio

1. Fare clic sul progetto Android hello e quindi selezionare **imposta come progetto di avvio**.

2. toobuild hello progetto e avviare l'applicazione hello in un emulatore Android hello **eseguire** dal menu **Avvia debug**.

#### <a name="in-visual-studio"></a>In Visual Studio

1. Fare clic sul progetto Android (Droid) hello e quindi selezionare **imposta come progetto di avvio**.

2. In hello **compilare** dal menu **Configuration Manager**.

3. In hello **Configuration Manager** la finestra di dialogo, seleziona hello **compilare** e **Distribuisci** progetto Android toohello Avanti caselle di controllo.

4. toobuild hello progetto e avviare l'applicazione hello in un emulatore Android, seleziona hello **F5** chiave.

   > [!NOTE]
   > Se si verificano problemi di compilazione progetto hello, eseguire hello manager e aggiornamento toohello ultima versione del pacchetto NuGet di pacchetti di supporto Xamarin hello. Progetti di avvio rapido potrebbero essere lento tooupdate toohello ultime versioni.    
   >
   >

5. Nell'app hello, digitare un testo significativo, ad esempio *informazioni su Xamarin*, e quindi selezionare hello sul segno più (**+**).

    ![][11]
    
    Questa azione Invia un toohello richiesta post che nuova App per dispositivi mobili di back-end che è ospitato in Azure. Dati richiesta hello viene inseriti nella tabella TodoItem hello. Gli elementi archiviati nella tabella hello vengono restituiti per hello terminare nuovamente App per dispositivi mobili e hello dati vengono visualizzati nell'elenco di hello.
    
    > [!NOTE]
    > È disponibile codice hello che accede l'App per dispositivi mobili di back-end in hello file TodoItemManager.cs c# del progetto di libreria di classi portabile hello della soluzione.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(Facoltativo) Eseguire il progetto di Windows hello

In questa sezione si esegue hello progetto Xamarin WinApp per i dispositivi Windows. Se non si usano dispositivi Windows, è possibile ignorare questa sezione.

#### <a name="in-visual-studio"></a>In Visual Studio

1. Fare doppio clic su uno qualsiasi dei progetti di Windows hello e quindi selezionare **imposta come progetto di avvio**.

2. In hello **compilare** dal menu **Configuration Manager**.

3. In hello **Configuration Manager** la finestra di dialogo, seleziona hello **compilare** e **Distribuisci** caselle di controllo toohello Windows progetto successivo che si è scelto.

4. toobuild hello progetto e avviare l'applicazione hello in un emulatore di Windows, seleziona hello **F5** chiave.

   > [!NOTE]
   > Se si verificano problemi di compilazione progetto hello, eseguire hello manager e aggiornamento toohello ultima versione del pacchetto NuGet di pacchetti di supporto Xamarin hello. Progetti di avvio rapido potrebbero essere lento tooupdate toohello ultime versioni.    
   >
   >

5. Nell'app hello, digitare un testo significativo, ad esempio *informazioni su Xamarin*, e quindi selezionare hello sul segno più (**+**).

    Questa azione Invia un toohello richiesta post che nuova App per dispositivi mobili di back-end che è ospitato in Azure. Dati richiesta hello viene inseriti nella tabella TodoItem hello. Gli elementi archiviati nella tabella hello vengono restituiti per hello terminare nuovamente App per dispositivi mobili e hello dati vengono visualizzati nell'elenco di hello.
    
    ![][12]
    
    > [!NOTE]
    > È disponibile codice hello che accede l'App per dispositivi mobili di back-end in hello file TodoItemManager.cs c# del progetto di libreria di classi portabile hello della soluzione.
    >
    >

## <a name="next-steps"></a>Passaggi successivi

* [Aggiungere app tooyour authentication](app-service-mobile-xamarin-forms-get-started-users.md)  
  Informazioni su come gli utenti tooauthenticate dell'app con un provider di identità.

* [Aggiungere app tooyour di notifiche push](app-service-mobile-xamarin-forms-get-started-push.md)  
  Informazioni su come le notifiche push tooadd supportano tooyour app e configurare le notifiche di push di App per dispositivi mobili back-end toouse gli hub di notifica di Azure toosend hello.

* [Abilitare la sincronizzazione offline per l'app](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Informazioni su come tooadd supporto offline per l'app usando un App per dispositivi mobili back-end. La sincronizzazione offline consente di visualizzare, aggiungere o modificare i dati dell'app per dispositivi mobili, anche se non è presente alcuna connessione di rete.

* [Usare i client gestiti hello per App per dispositivi mobili](app-service-mobile-dotnet-how-to-use-client-library.md)  
  Informazioni su come toowork con hello gestita client SDK nell'app Xamarin.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portale di Azure]: https://portal.azure.com/
