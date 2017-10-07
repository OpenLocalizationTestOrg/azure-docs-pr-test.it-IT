---
title: aaaGet avviato con l'autenticazione per App per dispositivi mobili in Android di Xamarin
description: "Informazioni su come gli utenti tooauthenticate di App per dispositivi mobili toouse dell'app Android di Xamarin attraverso una varietà di provider di identità, tra cui Azure ad, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>Aggiungere app xamarin tooyour di autenticazione
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

In questo argomento illustra come tooauthenticate agli utenti di un'App Mobile dall'applicazione client. In questa esercitazione si Aggiungi progetto di avvio rapido toohello l'autenticazione utilizzando un provider di identità supportati da app mobili di Azure. Al termine viene autenticato e autorizzato in hello App per dispositivi mobili, valore di ID utente hello viene visualizzato.

Questa esercitazione è basata su hello Guida introduttiva di App per dispositivi mobili. È necessario anche completare Esercitazione hello [creare un'app xamarin]. Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere il progetto tooyour pacchetto di hello autenticazione estensione. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register"></a>Registrare l'app per l'autenticazione e configurare i servizi app
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

In Visual Studio o Xamarin Studio, eseguire il progetto di client hello in un dispositivo o l'emulatore. Verificare che, dopo l'avvio dell'applicazione hello, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato). Ciò accade perché l'applicazione hello tenta tooaccess back-end App per dispositivi mobili come un utente non autenticato. Hello *TodoItem* tabella richiede ora l'autenticazione.

Successivamente, si aggiornerà le risorse toorequest di hello del client app dal back-end di hello App per dispositivi mobili con un utente autenticato.

## <a name="add-authentication"></a>Aggiungere app toohello authentication
app Hello è hello tootap di utenti aggiornati toorequire **Accedi** pulsante e l'autenticazione prima di visualizzazione dei dati.

1. Aggiungere i seguenti toohello codice hello **TodoActivity** classe:
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    Crea un nuovo tooauthenticate metodo un utente e un gestore per un nuovo **Accedi** pulsante. utente Hello nel codice di esempio hello precedente viene autenticato utilizzando un account di accesso di Facebook. Una finestra di dialogo è l'ID utente utilizzato toodisplay hello dopo l'autenticazione.
   
   > [!NOTE]
   > Se si utilizza un provider di identità diverso da Facebook, modificare il valore di hello passato troppo**LoginAsync** sopra tooone seguenti hello: *MicrosoftAccount*, *Twitter*, *Google*, o *WindowsAzureActiveDirectory*.
   > 
   > 
2. In hello **OnCreate** (metodo), delete o hello commento riga di codice seguente:
   
        OnRefreshItemsSelected ();
3. Nel file hello Activity_To_Do.axml aggiungere hello seguenti *LoginUser* pulsante definizione prima hello esistente *AddItem* pulsante:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Aggiungere i seguenti file di risorse Strings toohello elemento hello:
   
        <string name="login_button_text">Sign in</string>
5. Aprire il file AndroidManifest.xml hello, aggiungere seguente codice all'interno di hello `<application>` elemento XML:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. In Visual Studio o Xamarin Studio, eseguire il progetto di client hello in un emulatore o il dispositivo e accedere con il provider di identità selezionato. Quando si è connessi in correttamente, hello elenco delle attività, è possibile apportare aggiornamenti toohello dati hello app verrà visualizzato l'ID di accesso.

<!-- URLs. -->
[creare un'app xamarin]: app-service-mobile-xamarin-android-get-started.md