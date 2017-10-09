---
title: aaaGet avviato con Windows Universal App Azure Mobile Engagement
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per App universali di Windows.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Introduzione a Azure Mobile Engagement per app di Windows universali
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand l'utilizzo delle app e trasmissione push agli utenti di toosegmented notifiche di un'applicazione Windows universale.
Questa esercitazione illustra hello broadcast uno scenario semplice utilizzando Mobile Engagement. Si crea un'app universale di Windows vuota che raccoglie dati di base relativi all'utilizzo dell'app e riceve notifiche push tramite Servizi notifica Push Windows (WNS).

> [!NOTE]
> servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti. Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Configurare Mobile Engagement per l'app universale di Windows
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato una "integrazione di base," hello minimo imposta dati toocollect necessarie e invia una notifica push. la documentazione completa integrazione Hello è reperibile in hello [integrazione Windows Mobile Engagement SDK universale](mobile-engagement-windows-store-sdk-overview.md).

Creare un'app di base con l'integrazione di Visual Studio toodemonstrate hello.

### <a name="create-a-windows-universal-app-project"></a>Creare un progetto di app universale di Windows
Hello passaggi seguenti si presuppongono hello utilizzo di Visual Studio 2015 se hello passaggi sono simili nelle versioni precedenti di Visual Studio.

1. Avviare Visual Studio e in hello **Home** selezionare **nuovo progetto**.
2. Nel menu a comparsa hello, selezionare **Windows** -> **Universal** -> **App vuota (Windows universale)**. Compilare app hello **nome** e **Nome soluzione**, quindi fare clic su **OK**.

    ![][1]

Ora è stata creata un progetto di App universali di Windows in cui è stato quindi integrare hello Azure Mobile Engagement SDK.

### <a name="connect-your-app-toomobile-engagement-backend"></a>La connessione back-end Engagement tooMobile app
1. Installare hello [MicrosoftAzure.MobileEngagement] pacchetto Nuget nel progetto. Se la destinazione piattaforme Windows e Windows Phone, è necessario toodo questo per entrambi i progetti. Per Windows 8. x e Windows Phone 8.1, hello stesso Nuget pacchetto posizioni hello corretto specifico della piattaforma i file binari in ogni progetto.
2. Aprire **package. appxmanifest** e verificare che tale hello funzionalità seguente viene aggiunto sono:

        Internet (Client)

    ![][2]
3. Ora di copiare una stringa di connessione hello copiato in precedenza per l'applicazione di Mobile Engagement e incollarlo in hello `Resources\EngagementConfiguration.xml` file tra hello `<connectionString>` e `</connectionString>` tag:

    ![][3]

    > [!TIP]
    > Se l'app è destinata a entrambe le piattaforme Windows e Windows Phone, è comunque preferibile creare due applicazioni Mobile Engagement, una per ogni piattaforma supportata. La presenza di due App assicura che è possibile creare corretta segmentazione dei destinatari hello e che si possono inviare le notifiche di destinazione in modo appropriato per ogni piattaforma.

    > [!IMPORTANT]
    > NuGet non copia automaticamente le risorse SDK hello nell'applicazione UWP Windows 10. È stata toodo manualmente seguendo i passaggi di hello cui visualizzati quando viene installato il pacchetto Nuget di hello (Readme. txt).  

1. In hello `App.xaml.cs` file:

    a. Aggiungere hello `using` istruzione:

            using Microsoft.Azure.Engagement;

    b. Aggiungere un metodo che inizializza hello Engagement:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Inizializzare Ciao SDK hello **OnLaunched** metodo:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Inserire il seguente hello in hello **OnActivated** (metodo) e, se non è già presente, aggiungere il metodo hello:

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Abilitare il monitoraggio in tempo reale
toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare almeno un back-end Mobile Engagement delle toohello schermata (attività).

1. In hello **MainPage.xaml.cs**, aggiungere il seguente hello `using` istruzione:

    using Microsoft.Azure.Engagement.Overlay;
2. Classe di base hello di **MainPage** da **pagina** troppo**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. In hello `MainPage.xaml` file:

    a. Aggiungere le dichiarazioni di spazi dei nomi tooyour:

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Sostituire hello **pagina** nei nomi di tag XML hello con **engagement: EngagementPageOverlay**

> [!IMPORTANT]
> Se la pagina esegue l'override di hello `OnNavigatedTo` metodo toocall assicurarsi di essere `base.OnNavigatedTo(e)`. In caso contrario, non viene riportata l'attività di hello `EngagementPage` chiamate `StartActivity` all'interno di relativo `OnNavigatedTo` (metodo)). Ciò è particolarmente importante in un progetto Windows Phone in cui il modello predefinito di hello ha un `OnNavigatedTo` metodo.
>
> Per **App universali di Windows 10**, utilizzare il metodo hello consigliato in hello "metodo consigliato: eseguire l'overload di classi di pagina" sezione di [avanzate Reporting con hello Windows Universal App Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md) , invece di hello uno indicato in precedenza.

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitare le notifiche push e la messaggistica in-app
Engagement mobile permette toointeract e raggiungere gli utenti con le notifiche push e nel contesto di hello delle campagne di messaggistica in-app. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Hello nelle sezioni seguenti impostarle backup tooreceive l'app.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Abilitare il tooreceive app le notifiche Push WNS
1. In hello `Package.appxmanifest` file hello **applicazione** scheda **notifiche**, impostare **popup:** troppo**Sì**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Inizializzare hello REACH SDK
In `App.xaml.cs`, chiamare **EngagementReach.Instance.Init(e);** in hello **InitEngagement** funzione subito dopo l'inizializzazione dell'agente di hello:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

Si è pronti toosend un avviso popup. Viene quindi verificato che l'integrazione di base sia stata eseguita correttamente.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>Concedere accesso tooMobile Engagement toosend notifiche
1. Aprire [Dev Center per Windows Store] nel Web browser, accedere e creare un account, se necessario.
2. Fare clic su **Dashboard** angolo hello in alto a destra e quindi fare clic su **crea una nuova app** dal menu Pannello sinistro hello.

    ![][9]
3. Creare l'app riservandone il nome.

    ![][10]
4. Dopo aver creato l'applicazione hello, passare troppo**servizi -> notifiche Push** dal menu a sinistra di hello.

    ![][11]
5. In hello Push sezione notifiche, fare clic su hello **sito Services Live** collegamento.

    ![][12]
6. Passare toohello relativa alle credenziali Push. Verificare di disporre in hello **impostazioni App** sezione e quindi copiare il **SID pacchetto** e **segreto Client**

    ![][13]
7. Passare toohello **impostazioni** del portale Mobile Engagement e fare clic su hello **Push nativo** sezione a sinistra di hello. Quindi, fare clic su hello **modifica** tooenter pulsante il **ID di pacchetto sicurezza (SID)** e **chiave privata** come illustrato:

    ![][6]
8. Verificare infine che è stato associato l'app di Visual Studio con questa app creata nell'archivio di App hello. Fare clic su **Associa applicazione a Store** in Visual Studio.

    ![][7]

## <a id="send"></a>Invia un'app tooyour notifica
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Se l'applicazione hello è in esecuzione, si noterà una notifica in-app. in caso contrario, se l'applicazione hello è chiuso, viene visualizzata una notifica di tipo avviso popup.
Se è visualizzata una notifica in-app, ma non una notifica di tipo avviso popup e si esegue l'applicazione hello in modalità di debug in Visual Studio, quindi provare a **gli eventi del ciclo di vita -> Sospendi** in hello barra degli strumenti tooensure app hello è sospeso. Se si fa clic sul pulsante Home hello durante il debug di un'applicazione hello in Visual Studio, quindi non sempre sospesi e durante la notifica hello viene visualizzato come in-app, non viene visualizzata come una notifica di tipo avviso popup.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Dev Center per Windows Store]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
