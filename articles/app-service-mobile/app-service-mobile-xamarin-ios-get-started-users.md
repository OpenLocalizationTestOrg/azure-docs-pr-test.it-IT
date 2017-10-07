---
title: aaaGet avviato con l'autenticazione per App per dispositivi mobili in Xamarin iOS
description: "Informazioni su come gli utenti tooauthenticate di App per dispositivi mobili toouse dell'app Xamarin iOS tramite un'ampia varietà di provider di identità, tra cui Azure ad, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a>Aggiungere app xamarin tooyour di autenticazione
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

In questo argomento illustra come tooauthenticate agli utenti di un'App Mobile di servizio App dall'applicazione client. In questa esercitazione, si aggiunge l'autenticazione toohello xamarin delle Guide rapide progetto usando un provider di identità che è supportato dal servizio App. Dopo che viene correttamente autenticato e autorizzato dall'App Mobile, valore di ID utente hello viene visualizzato e sarà in grado di tooaccess limitato dati della tabella.

È necessario completare prima esercitazione hello [creare un'app xamarin]. Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere il progetto tooyour pacchetto di hello autenticazione estensione. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Registrare l'app per l'autenticazione e configurare i servizi app
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app

L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app. App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello. In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto. È tuttavia possibile usare QUALSIASI schema URL. Deve essere univoco tooyour applicazioni per dispositivi mobili. reindirizzamento di hello tooenable sul lato server hello:

1. In hello [portale], selezionare il servizio App.

2. Fare clic su hello **autenticazione / autorizzazione** opzione di menu.

3. In hello **consentito URL di reindirizzamento esterno**, immettere `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.  Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.  È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.

4. Fare clic su **OK**.

5. Fare clic su **Salva**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Limitare le autorizzazioni tooauthenticated utenti
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. In Visual Studio o Xamarin Studio, eseguire il progetto di client hello in un dispositivo o l'emulatore. Verificare che, dopo l'avvio dell'applicazione hello, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato). Errore Hello è connesso toohello console del debugger hello. In Visual Studio, pertanto, verrà visualizzato errore hello nella finestra di output di hello.

&nbsp;&nbsp;Questo errore non autorizzato si verifica perché l'applicazione hello tenta tooaccess back-end App per dispositivi mobili come un utente non autenticato. Hello *TodoItem* tabella richiede ora l'autenticazione.

Successivamente, si aggiornerà le risorse toorequest di hello del client app dal back-end di hello App per dispositivi mobili con un utente autenticato.

## <a name="add-authentication-toohello-app"></a>Aggiungere app toohello authentication
In questa sezione si modificherà hello app toodisplay una schermata di accesso prima di visualizzare dati. Quando viene avviata l'applicazione hello, non non si connetteranno tooyour servizio App e non verrà visualizzati tutti i dati. Dopo la prima volta hello hello eseguite dall'utente hello movimenti di aggiornamento, viene visualizzata la finestra hello; Dopo che verrà visualizzato l'elenco di accesso con esito positivo hello delle attività.

1. Nel progetto client hello, aprire il file hello **QSTodoService.cs** e aggiungere hello seguente istruzione using e `MobileServiceUser` con funzione di accesso toohello QSTodoService classe:
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. Aggiungi nuovo metodo denominato **Authenticate** troppo**QSTodoService** con hello seguente definizione:

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] Se si utilizza un provider di identità diverso da un Facebook, modificare il valore di hello passato troppo**LoginAsync** sopra tooone seguenti hello: _MicrosoftAccount_, _Twitter_, _Google_, o _WindowsAzureActiveDirectory_.

3. Aprire **QSTodoListViewController.cs**. Modificare la definizione di metodo hello di **ViewDidLoad** rimozione chiamata hello troppo**RefreshAsync()** verso la fine hello:
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. Modificare il metodo hello **RefreshAsync** tooauthenticate se hello **utente** proprietà è null. Aggiungere hello codice nella parte superiore di hello hello della definizione di metodo seguenti:
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. Aprire **appdelegate. cs**, aggiungere al metodo hello:

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. Aprire **Info. plist** file, passare troppo**URL tipi** in hello **avanzate** sezione. Configurare ora hello **identificatore** hello e **schemi URL** del tipo di URL e fare clic su **Aggiungi tipo URL**. **Gli schemi URL** deve essere hello stesso come il {url_scheme_of_your_app}.
7. In Visual Studio o Xamarin Studio connessa tooyour Xamarin Host di compilazione nel Mac, eseguire il progetto di client hello destinato a un dispositivo o un emulatore. Verificare che app hello non visualizza alcun dato.
   
    Eseguire l'operazione di aggiornamento di hello trascinando verso il basso hello elenco di elementi, che provoca il tooappear schermata di accesso hello. Dopo che sono state immesse credenziali valide, hello app verrà visualizzato l'elenco hello delle attività, mentre è possibile apportare aggiornamenti toohello dati.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[creare un'app xamarin]: app-service-mobile-xamarin-ios-get-started.md