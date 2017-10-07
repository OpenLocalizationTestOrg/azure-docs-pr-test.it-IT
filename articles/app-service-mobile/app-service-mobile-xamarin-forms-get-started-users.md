---
title: aaaGet avviato con l'autenticazione per App per dispositivi mobili in app Xamarin Forms | Documenti Microsoft
description: "Informazioni su come gli utenti tooauthenticate di App per dispositivi mobili toouse dell'app Xamarin form tramite un'ampia varietà di provider di identità, tra cui Azure ad, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>Aggiungere app Xamarin Forms tooyour di autenticazione
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>Panoramica
In questo argomento illustra come tooauthenticate agli utenti di un'App Mobile di servizio App dall'applicazione client. In questa esercitazione, si aggiunge l'autenticazione a progetto di avvio rapido Xamarin Forms hello utilizzando un provider di identità che è supportato dal servizio App. Una volta viene correttamente autenticato e autorizzato dall'App Mobile, valore di ID utente hello viene visualizzato e sarà in grado di tooaccess limitato dati della tabella.

## <a name="prerequisites"></a>Prerequisiti
Per ottenere risultati migliori hello in questa esercitazione, è consigliabile completare prima hello [creare un'app Xamarin Forms] [ 1] esercitazione. Al termine di questa esercitazione, sarà disponibile un progetto Xamarin.Forms che corrisponde a un'app TodoList multipiattaforma.

Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere il progetto tooyour pacchetto di hello autenticazione estensione. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure][2].

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Registrare l'app per l'autenticazione e configurare i servizi app
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app

L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app. App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello. In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto. È tuttavia possibile usare QUALSIASI schema URL. Deve essere univoco tooyour applicazioni per dispositivi mobili. reindirizzamento di hello tooenable sul lato server hello:

1. In hello [portale], selezionare il servizio App.

2. Fare clic su hello **autenticazione / autorizzazione** opzione di menu.

3. In hello **consentito URL di reindirizzamento esterno**, immettere `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.  Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.  È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.

4. Fare clic su **OK**.

5. Fare clic su **Salva**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Limitare le autorizzazioni tooauthenticated utenti
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>Aggiungi libreria di classi portabile toohello autenticazione
App per dispositivi mobili Usa hello [LoginAsync] [ 3] metodo di estensione su hello [MobileServiceClient] [ 4] toosign in un utente con il servizio App autenticazione. Questo esempio utilizza un flusso di autenticazione server gestito che consente di visualizzare hello interfaccia del provider Accedi nell'app hello. Per altre informazioni, vedere [Autenticazione gestita dal server][5]. Per offrire un'esperienza utente migliore nell'app di produzione, è consigliabile prendere invece in considerazione l'uso dell'[autenticazione gestita dal client][6].

tooauthenticate con un progetto Xamarin form, definire un **IAuthenticate** interfaccia hello libreria di classi portabile per app hello. Aggiungere quindi una **Accedi** interfaccia utente di toohello pulsante definito nella libreria di classi portabile, in cui si fa clic su hello toostart autenticazione. Al termine dell'autenticazione, i dati vengono caricati dal back-end dell'app mobile hello.

Hello implementare **IAuthenticate** interfaccia per ogni piattaforma supportata dall'app.

1. In Visual Studio o Xamarin Studio, aprire l'app. cs dal progetto di hello con **portabile** in nome hello, che è il progetto libreria di classi portabile, aggiungere il seguente hello `using` istruzione:

        using System.Threading.Tasks;
2. In App. cs, aggiungere hello seguente `IAuthenticate` interfaccia definizione immediatamente prima di hello `App` definizione di classe.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. interfaccia hello tooinitialize con un'implementazione specifica della piattaforma, aggiungere hello segue i membri statici toohello **App** classe.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. Aprire TodoList.xaml dal progetto di libreria di classi portabile hello, aggiungere il seguente hello **pulsante** elemento hello *buttonsPanel* elemento di layout, dopo pulsante esistente hello:

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    Questo pulsante attiva l'autenticazione gestita dal server con il back-end dell'app per dispositivi mobili.
5. Aprire TodoList.xaml.cs dal progetto di libreria di classi portabile hello, quindi aggiungere hello seguente campo toohello `TodoList` classe:

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Sostituire hello **OnAppearing** metodo con hello seguente codice:

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    Questo codice garantisce che i dati solo aggiornati dal servizio hello dopo l'autenticazione.
7. Aggiungere hello seguente gestore per hello **selezionato** evento toohello **TodoList** classe:

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. Salvare le modifiche e ricompilare il progetto di libreria di classi portabile hello non verifica errori.

## <a name="add-authentication-toohello-android-app"></a>Aggiungere app per Android toohello autenticazione
Questa sezione viene illustrato come hello tooimplement **IAuthenticate** interfaccia nel progetto di app Android hello. Se i dispositivi Android non sono supportati, ignorare questa sezione.

1. In Visual Studio o Xamarin Studio, fare doppio clic su hello **droid** del progetto, quindi **imposta come progetto di avvio**.
2. Hello toostart di premere F5 nel debugger hello del progetto, quindi verificare che, dopo l'avvio dell'applicazione, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato). Poiché l'accesso nel back-end hello è solo per gli utenti con restrizioni tooauthorized, viene generato codice 401 Hello.
3. Aprire Mainactivity nel progetto Android hello e aggiungere il seguente hello `using` istruzioni:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Hello aggiornamento **MainActivity** hello tooimplement classe **IAuthenticate** interfaccia, come indicato di seguito:

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. Hello aggiornamento **MainActivity** classe aggiungendo un **MobileServiceUser** campo e un **Authenticate** metodo, è necessario per hello **IAuthenticate**  interfaccia, come indicato di seguito:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider][7].

6. Aggiungere seguente codice all'interno di hello <application> nodo di AndroidManifest.xml:

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. Aggiungere i seguenti toohello codice hello **OnCreate** metodo hello **MainActivity** classe prima chiamata hello troppo`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    Questo codice garantisce l'autenticatore hello viene inizializzata prima carica app hello.
2. Ricompilare l'applicazione hello, eseguirlo, quindi eseguire l'accesso con provider di autenticazione hello selezionato e verificare che l'eventuale tooaccess in grado di dati come utente autenticato.

## <a name="add-authentication-toohello-ios-app"></a>Aggiungere app per iOS toohello autenticazione
Questa sezione viene illustrato come hello tooimplement **IAuthenticate** interfaccia nel progetto di app iOS hello. Se i dispositivi iOS non sono supportati, ignorare questa sezione.

1. In Visual Studio o Xamarin Studio, fare doppio clic su hello **iOS** del progetto, quindi **imposta come progetto di avvio**.
2. Hello toostart di premere F5 nel debugger hello del progetto, quindi verificare che viene generata un'eccezione non gestita con un codice di stato di 401 (Unauthorized) dopo l'avvio dell'applicazione hello. risposta 401 Hello viene prodotta perché l'accesso nel back-end hello è solo per gli utenti con restrizioni tooauthorized.
3. Aprire appdelegate. cs nel progetto iOS hello e aggiungere il seguente hello `using` istruzioni:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Hello aggiornamento **AppDelegate** hello tooimplement classe **IAuthenticate** interfaccia, come indicato di seguito:

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. Hello aggiornamento **AppDelegate** classe aggiungendo un **MobileServiceUser** campo e un **Authenticate** metodo, è necessario per hello **IAuthenticate**  interfaccia, come indicato di seguito:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider].

6. Aggiornare classe AppDelegate hello aggiungendo l'overload del metodo OpenUrl (opzioni NSDictionary di app, url NSUrl, UIApplication)

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. Aggiungere hello successiva riga di codice toohello **FinishedLaunching** chiamata del metodo prima di hello troppo`LoadApplication()`:

        App.Init(this);

    Questo codice garantisce l'autenticatore hello viene inizializzata prima che venga caricata l'applicazione hello.

6. Aggiungere **{url_scheme_of_your_app}** tooURL schemi in Info. plist.

7. Ricompilare l'applicazione hello, eseguirlo, quindi eseguire l'accesso con provider di autenticazione hello selezionato e verificare che l'eventuale tooaccess in grado di dati come utente autenticato.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>Aggiungere l'autenticazione tooWindows 10 (incluso Phone) progetti di app
Questa sezione viene illustrato come hello tooimplement **IAuthenticate** interfaccia nei progetti di app di Windows 10 hello. Hello stessi passaggi sono validi per i progetti di piattaforma UWP (Universal Windows), ma utilizzando hello **UWP** progetto (con le modifiche indicate). Se i dispositivi Windows non sono supportati, ignorare questa sezione.

1. "In Visual Studio, fare doppio clic su uno hello **UWP** del progetto, quindi **imposta come progetto di avvio**.
2. Hello toostart di premere F5 nel debugger hello del progetto, quindi verificare che viene generata un'eccezione non gestita con un codice di stato di 401 (Unauthorized) dopo l'avvio dell'applicazione hello. risposta 401 Hello si verifica poiché l'accesso nel back-end hello è solo per gli utenti con restrizioni tooauthorized.
3. Apri il file MainPage.xaml.cs del progetto di app di Windows hello e aggiungere il seguente hello `using` istruzioni:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    Sostituire `<your_Portable_Class_Library_namespace>` con hello dello spazio dei nomi per la libreria di classi portabile.
4. Hello aggiornamento **MainPage** hello tooimplement classe **IAuthenticate** interfaccia, come indicato di seguito:

        public sealed partial class MainPage : IAuthenticate
5. Hello aggiornamento **MainPage** classe aggiungendo un **MobileServiceUser** campo e un **Authenticate** metodo, è necessario per hello **IAuthenticate** interfaccia, come indicato di seguito:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    Se si usa un provider di identità diverso da Facebook, scegliere un valore diverso per [MobileServiceAuthenticationProvider].

1. Aggiungere hello successiva riga di codice nel costruttore hello per hello **MainPage** classe prima chiamata hello troppo`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    Sostituire `<your_Portable_Class_Library_namespace>` con hello dello spazio dei nomi per la libreria di classi portabile.

3. Se si utilizza **UWP**, aggiungere il seguente hello **OnActivated** toohello l'override del metodo **App** classe:

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Quando l'override del metodo hello esiste già, aggiungere il codice condizionale hello da hello precedente frammento di codice.  Questo codice non è necessario per i progetti Universal Windows.

3. Aggiungere **{schema_url_app}** in Package.appxmanifest. 

4. Ricompilare l'applicazione hello, eseguirlo, quindi eseguire l'accesso con provider di autenticazione hello selezionato e verificare che l'eventuale tooaccess in grado di dati come utente autenticato.

## <a name="next-steps"></a>Passaggi successivi
Ora che è stata completata questa esercitazione l'autenticazione di base, è consigliabile continuare su tooone di hello seguenti esercitazioni:

* [Aggiungere app tooyour di notifiche push](app-service-mobile-xamarin-forms-get-started-push.md)

  Informazioni su come le notifiche push tooadd supportano tooyour app e configurare le notifiche di push toosend App Mobile back-end toouse gli hub di notifica di Azure.
* [Abilitare la sincronizzazione offline per l'app](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  Informazioni su come offline tooadd supportano un'applicazione con un back-end dell'App Mobile. Sincronizzazione non in linea consente toointeract gli utenti finali con un'app per dispositivi mobili - visualizzazione, aggiunta o modifica dei dati, anche quando è presente alcuna connessione di rete.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
