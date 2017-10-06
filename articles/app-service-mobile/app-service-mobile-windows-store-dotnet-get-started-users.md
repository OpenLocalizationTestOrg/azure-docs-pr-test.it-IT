---
title: app di Windows della piattaforma UWP (Universal) aaaAdd authentication tooyour | Documenti Microsoft
description: "Informazioni su come gli utenti tooauthenticate di App mobili di Azure App Service toouse dell'app Universal Windows Platform (UWP) utilizzando una varietà di provider di identità, tra cui: AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>Aggiungere app di Windows authentication tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

In questo argomento illustra come app per dispositivi mobili tooyour tooadd l'autenticazione basata su cloud. In questa esercitazione è aggiungere progetto di avvio rapido di autenticazione toohello piattaforma UWP (Universal Windows) per App per dispositivi mobili utilizzando un provider di identità che è supportato dal servizio App di Azure. Al termine viene autenticato e autorizzato dall'App Mobile back-end, valore di ID utente hello viene visualizzato.

Questa esercitazione è basata su hello avvio rapido di applicazioni per dispositivi mobili. È necessario completare prima esercitazione hello [introduzione App per dispositivi mobili](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Registrare l'app per l'autenticazione e configurare hello servizio App
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app

L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app. App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello. In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto. È tuttavia possibile usare QUALSIASI schema URL. Deve essere univoco tooyour applicazioni per dispositivi mobili. reindirizzamento di hello tooenable sul lato server hello:

1. In hello [portale], selezionare il servizio App.

2. Fare clic su hello **autenticazione / autorizzazione** opzione di menu.

3. In hello **consentito URL di reindirizzamento esterno**, immettere `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.  Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.  È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.

4. Fare clic su **OK**.

5. Fare clic su **Salva**.

## <a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

A questo punto, è possibile verificare che tale back-end tooyour l'accesso anonimo è stato disabilitato. I progetti di app UWP hello imposta come progetto di avvio hello, distribuire ed eseguire app di hello; Verificare che, dopo l'avvio dell'applicazione hello, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato). Ciò accade perché l'applicazione hello tenta tooaccess codice dell'App Mobile come un utente non autenticato, ma hello *TodoItem* tabella richiede ora l'autenticazione.

Successivamente, si aggiornerà gli utenti di hello app tooauthenticate prima di richiedere risorse di servizio App.

## <a name="add-authentication"></a>Aggiungere app toohello authentication
1. Nel progetto di app UWP hello file MainPage.xaml.cs e aggiungere hello frammento di codice seguente:
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    Questo codice esegue l'autenticazione utente hello con un account di accesso di Facebook. Se si utilizza un provider di identità diverso da Facebook, modificare il valore di hello di **MobileServiceAuthenticationProvider** sopra toohello valore per il provider.
2. Sostituire hello **OnNavigatedTo ()** metodo MainPage.xaml.cs. Successivamente, si aggiungerà un **Accedi** app toohello pulsante che attiva l'autenticazione.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Aggiungere hello seguente frammento di codice toohello MainPage.xaml.cs:
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Aprire il file di progetto hello MainPage. XAML, individuare l'elemento hello che definisce hello **salvare** pulsante e sostituirlo con hello seguente codice:
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. Aggiungere hello seguente frammento di codice toohello App.xaml.cs:

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Aprire il file package. appxmanifest, passare troppo**dichiarazioni**nella **dichiarazioni disponibili** elenco a discesa, seleziona **protocollo** e fare clic su **Aggiungi** pulsante. Configurare ora hello **proprietà** di hello **protocollo** dichiarazione. In **nome visualizzato**, aggiungere il nome di hello desiderato toousers toodisplay dell'applicazione. In **Nome** aggiungere il valore {url_scheme_of_your_app}.
7. Premere hello F5 toorun chiave hello app, fare clic su hello **Accedi** pulsante e sign in app hello con il provider di identità selezionato. Dopo l'accesso ha esito positivo, hello app viene eseguita senza errori e si tooquery in grado di back-end e apportare aggiornamenti toodata.

## <a name="tokens"></a>Archiviare i token di autenticazione hello client hello
Hello esempio precedente ha mostrato uno standard sign-in, che richiede hello client toocontact sia provider di identità hello e hello servizio App ogni volta che viene avviata l'applicazione hello. Non solo è inefficiente, è possibile eseguire questo metodo in utilizzo-si riferisce problemi molti clienti tentare toostart app in hello contemporaneamente. Un approccio migliore è token di autorizzazione hello toocache restituito dal servizio App e riprovare toouse questo prima di utilizzare un provider basato su Accedi.

> [!NOTE]
> È possibile memorizzare nella cache token hello rilasciati da servizi di App, indipendentemente dal fatto se si utilizza l'autenticazione gestita da client o servizio. In questa esercitazione viene usata l'autenticazione gestita dal servizio.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Passaggi successivi
Ora che è stata completata questa esercitazione l'autenticazione di base, è consigliabile continuare su tooone di hello seguenti esercitazioni:

* [Aggiungere app tooyour di notifiche push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Informazioni su come le notifiche push tooadd supportano tooyour app e configurare le notifiche di push toosend App Mobile back-end toouse gli hub di notifica di Azure.
* [Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Informazioni su come offline tooadd supportano un'applicazione con un back-end dell'App Mobile. Sincronizzazione non in linea consente agli utenti finali toointeract con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
