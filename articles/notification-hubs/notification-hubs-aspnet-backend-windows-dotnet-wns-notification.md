---
title: aaaAzure notifica hub di notifica utenti con back-end .NET
description: Informazioni su come toosend sicuro le notifiche push in Azure. Esempi di codice scritti in c# utilizzando hello API .NET.
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Uso di Hub di notifica di Azure per inviare notifiche agli utenti con back-end.NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Panoramica
Supporto di notifica push in Azure consente tooaccess un semplice utilizzo, multipiattaforma e infrastruttura push di scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per le applicazioni aziendali e per dispositivi mobili piattaforme. Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure toosend push utente app specifica tooa di notifiche in un dispositivo specifico. Un back-end ASP.NET WebAPI è usato tooauthenticate client. Utilizzando hello autenticato l'utente del client e tag verrà aggiunto automaticamente dalla registrazione di toonotification hello back-end. Questo tag sarà toosend utilizzati dalle notifiche di toogenerate hello back-end per un utente specifico. Per ulteriori informazioni sulla registrazione per le notifiche tramite un back-end dell'app, vedere l'argomento Guida hello [registrazione dal back-end app](http://msdn.microsoft.com/library/dn743807.aspx). In questa esercitazione si basa sull'hub di notifica hello e progetto creato in hello [iniziare con gli hub di notifica] esercitazione.

In questa esercitazione è anche hello prerequisiti toohello [Secure Push] esercitazione. Dopo aver completato i passaggi di hello in questa esercitazione, è possibile procedere toohello [Secure Push] esercitazione che illustra come hello toomodify codice in questa esercitazione toosend una notifica push in modo sicuro.

## <a name="before-you-begin"></a>Prima di iniziare
I commenti e suggerimenti inviati seriamente verranno presi in considerazione. Se hai difficoltà il completamento di questo argomento o indicazioni per migliorare il contenuto, Gradiremmo commenti e suggerimenti nella parte inferiore di hello della pagina hello.

codice Hello completata per questa esercitazione è disponibile su GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario aver già completato queste esercitazioni su Servizi mobili:

* [iniziare con gli hub di notifica]<br/>Creare l'hub di notifica e riserva nome applicazione hello e registrare le notifiche di tooreceive in questa esercitazione. In questa esercitazione si presuppone che siano già stati completati questi passaggi. In caso contrario, attenersi alla procedura hello in [Introduzione agli hub di notifica (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), in particolare, hello sezioni [registrare l'app per Windows Store hello](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) e [Configura Hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). In particolare, assicurarsi di avere immesso hello **SID pacchetto** e **segreto Client** valori nel portale hello hello **configura** scheda per l'hub di notifica. Questa procedura di configurazione è descritta nella sezione hello [configurare l'Hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Si tratta di un passaggio importante: se credenziali hello nel portale di hello non corrispondono a quelle specificate per nome app hello scelto, notifica push di hello non riuscirà.

> [!NOTE]
> Se si utilizza App per dispositivi mobili in Azure App Service come il servizio back-end, vedere hello [versione di App per dispositivi mobili](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) di questa esercitazione.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Aggiornare il codice hello per il progetto client hello
In questa sezione aggiornare il codice hello nei progetti di hello siano stati completati per hello [iniziare con gli hub di notifica] esercitazione. Hello deve essere già associato archivio hello e configurato per l'hub di notifica. In questa sezione, si verrà aggiungere codice toocall hello nuovo WebAPI back-end e utilizzarlo per la registrazione e l'invio di notifiche.

1. In Visual Studio, aprire Esplora hello hello creato per hello [iniziare con gli hub di notifica] esercitazione.
2. In Esplora soluzioni fare doppio clic su hello **(Windows 8.1)** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.
3. Sul lato sinistro di hello, fare clic su **Online**.
4. In hello **ricerca** digitare **Http Client**.
5. Nell'elenco risultati hello, fare clic su **Microsoft HTTP Client Libraries**, quindi fare clic su **installare**. Completare l'installazione di hello.
6. In hello NuGet **ricerca** digitare **Json.net**. Installare hello **Json.NET** pacchetto e quindi chiudere hello Gestione pacchetti NuGet finestra.
7. Ripetere i passaggi di hello sopra per hello **(Windows Phone 8.1)** hello tooinstall progetto **JSON.NET** pacchetto NuGet per il progetto Windows Phone hello.
8. In Esplora soluzioni, in hello **(Windows 8.1)** progetto, fare doppio clic su **MainPage. XAML** tooopen nell'editor di Visual Studio hello.
9. In hello **MainPage. XAML** codice XML, sostituire hello `<Grid>` sezione con hello seguente codice. Questo codice aggiunge una casella di testo Nome utente e password che hello utente eseguirà l'autenticazione con. Aggiunge anche nelle caselle di testo per il messaggio di notifica hello e tag username hello che devono ricevere notifica hello:
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. In Esplora soluzioni, in hello **(Windows Phone 8.1)** progetto, aprire **MainPage. XAML** e sostituire hello Windows Phone 8.1 `<Grid>` sezione con quel codice precedente. interfaccia Hello dovrebbe essere simile toowhats illustrato di seguito.
    
    ![][13]
11. In Esplora soluzioni, aprire hello **MainPage.xaml.cs** file per hello **(Windows 8.1)** e **(Windows Phone 8.1)** progetti. Aggiungere il seguente hello `using` istruzioni nella parte superiore di hello di entrambi i file:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. In **MainPage.xaml.cs** per hello **(Windows 8.1)** e **(Windows Phone 8.1)** progetti, aggiungere hello seguente membro toohello `MainPage` classe. Tooreplace assicurarsi di essere `<Enter Your Backend Endpoint>` con hello l'endpoint di back-end effettivo ottenuto in precedenza. ad esempio `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Aggiungere codice hello seguente classe MainPage toohello **MainPage.xaml.cs** per hello **(Windows 8.1)** e **(Windows Phone 8.1)** progetti.
    
    Hello `PushClick` hello è fare clic su gestore per hello **inviare Push** pulsante. Chiama hello back-end tootrigger tooall una notifica dispositivi con un tag di nome utente corrispondente hello `to_tag` parametro. messaggio di notifica Hello viene inviato come contenuto JSON nel corpo della richiesta hello.
    
    Hello `LoginAndRegisterClick` hello è fare clic su gestore per hello **Accedi e registrare** pulsante. Hello basic archivia i token di autenticazione nel servizio di archiviazione locale (si noti che questo rappresenta un token viene utilizzato uno schema di autenticazione), quindi Usa `RegisterClient` tooregister per le notifiche tramite hello di back-end.

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. In Esplora soluzioni in hello **Shared** progetto, aprire hello **App.xaml.cs** file. Trovare chiamata hello troppo`InitNotificationsAsync()` in hello `OnLaunched()` gestore dell'evento. Impostare come commento o eliminare anche chiamata hello`InitNotificationsAsync()`. gestore del pulsante Hello aggiunte in precedenza verrà inizializzato registrazioni di notifica.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. In Esplora soluzioni fare doppio clic su hello **Shared** del progetto, quindi fare clic su **Aggiungi**, quindi fare clic su **classe**. Nome classe hello **RegisterClient.cs**, quindi fare clic su **OK** classe hello toogenerate.
   
   Questa classe eseguirà il wrapping hello REST chiamate necessarie toocontact hello app back-end, in ordine tooregister per le notifiche push. Archivia anche localmente hello *RegistrationId* creato da hello Hub di notifica, come descritto in dettaglio nella [registrazione dal back-end app](http://msdn.microsoft.com/library/dn743807.aspx). Si noti che usa un token di autorizzazione memorizzato nell'archiviazione locale quando si fa clic hello **Accedi e registrare** pulsante.
2. Aggiungere il seguente hello `using` istruzioni all'inizio di hello del file di RegisterClient.cs hello:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Aggiungere hello seguente codice all'interno di hello `RegisterClient` definizione di classe.
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. Salvare tutte le modifiche.

## <a name="testing-hello-application"></a>Test dell'applicazione hello
1. Avvia un'applicazione hello in Windows 8.1 e Windows Phone 8.1. Per Windows Phone 8.1 è possibile eseguire l'istanza di hello nell'emulatore Windows hello o un dispositivo reale.
2. Nell'istanza di Windows 8.1 hello di hello app, immettere un **Username** e **Password** come illustrato nella schermata di hello riportata di seguito. Deve essere diversi dal nome dell'utente hello e la password che immessi in Windows Phone.
3. Fare clic su **Log in and register** e verificare nella relativa finestra di dialogo di avere effettuato l'accesso. In questo modo anche hello **inviare Push** pulsante.
   
    ![][14]
4. Nell'istanza di hello Windows Phone 8.1, immettere una stringa del nome utente in entrambi hello **Username** e **Password** campi quindi fare clic su **accesso e registrazione**.
5. Quindi in hello **destinatario Username Tag** immettere nome utente hello registrato in Windows 8.1. Immettere un messaggio di notifica e fare clic su **Send Push**.
   
    ![][16]
6. Solo i dispositivi di hello che sono registrati con il tag di nome utente corrispondente hello ricevono il messaggio di notifica hello.
   
    ![][15]

## <a name="next-steps"></a>Passaggi successivi
* Se si desidera che gli utenti dai gruppi di interesse toosegment, vedere [toosend gli hub di notifica di utilizzare le ultime notizie].
* altre informazioni su come toolearn toouse gli hub di notifica, vedere [materiale sussidiario per gli hub di notifica].

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[iniziare con gli hub di notifica]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend gli hub di notifica di utilizzare le ultime notizie]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[materiale sussidiario per gli hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx
