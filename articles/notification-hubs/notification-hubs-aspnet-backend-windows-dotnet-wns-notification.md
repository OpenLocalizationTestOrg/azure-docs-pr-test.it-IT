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
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="c7515-104">Uso di Hub di notifica di Azure per inviare notifiche agli utenti con back-end.NET</span><span class="sxs-lookup"><span data-stu-id="c7515-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="c7515-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c7515-105">Overview</span></span>
<span data-ttu-id="c7515-106">Supporto di notifica push in Azure consente tooaccess un semplice utilizzo, multipiattaforma e infrastruttura push di scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per le applicazioni aziendali e per dispositivi mobili piattaforme.</span><span class="sxs-lookup"><span data-stu-id="c7515-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="c7515-107">Questa esercitazione viene illustrato come toouse gli hub di notifica di Azure toosend push utente app specifica tooa di notifiche in un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="c7515-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="c7515-108">Un back-end ASP.NET WebAPI è usato tooauthenticate client.</span><span class="sxs-lookup"><span data-stu-id="c7515-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="c7515-109">Utilizzando hello autenticato l'utente del client e tag verrà aggiunto automaticamente dalla registrazione di toonotification hello back-end.</span><span class="sxs-lookup"><span data-stu-id="c7515-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="c7515-110">Questo tag sarà toosend utilizzati dalle notifiche di toogenerate hello back-end per un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="c7515-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="c7515-111">Per ulteriori informazioni sulla registrazione per le notifiche tramite un back-end dell'app, vedere l'argomento Guida hello [registrazione dal back-end app](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7515-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="c7515-112">In questa esercitazione si basa sull'hub di notifica hello e progetto creato in hello [iniziare con gli hub di notifica] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c7515-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="c7515-113">In questa esercitazione è anche hello prerequisiti toohello [Secure Push] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c7515-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="c7515-114">Dopo aver completato i passaggi di hello in questa esercitazione, è possibile procedere toohello [Secure Push] esercitazione che illustra come hello toomodify codice in questa esercitazione toosend una notifica push in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="c7515-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c7515-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c7515-115">Before you begin</span></span>
<span data-ttu-id="c7515-116">I commenti e suggerimenti inviati seriamente verranno presi in considerazione.</span><span class="sxs-lookup"><span data-stu-id="c7515-116">We do take your feedback seriously.</span></span> <span data-ttu-id="c7515-117">Se hai difficoltà il completamento di questo argomento o indicazioni per migliorare il contenuto, Gradiremmo commenti e suggerimenti nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="c7515-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="c7515-118">codice Hello completata per questa esercitazione è disponibile su GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="c7515-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c7515-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c7515-119">Prerequisites</span></span>
<span data-ttu-id="c7515-120">Prima di iniziare questa esercitazione, è necessario aver già completato queste esercitazioni su Servizi mobili:</span><span class="sxs-lookup"><span data-stu-id="c7515-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="c7515-121">[iniziare con gli hub di notifica]</span><span class="sxs-lookup"><span data-stu-id="c7515-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="c7515-122">Creare l'hub di notifica e riserva nome applicazione hello e registrare le notifiche di tooreceive in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c7515-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="c7515-123">In questa esercitazione si presuppone che siano già stati completati questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="c7515-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="c7515-124">In caso contrario, attenersi alla procedura hello in [Introduzione agli hub di notifica (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), in particolare, hello sezioni [registrare l'app per Windows Store hello](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) e [Configura Hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="c7515-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="c7515-125">In particolare, assicurarsi di avere immesso hello **SID pacchetto** e **segreto Client** valori nel portale hello hello **configura** scheda per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="c7515-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="c7515-126">Questa procedura di configurazione è descritta nella sezione hello [configurare l'Hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="c7515-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="c7515-127">Si tratta di un passaggio importante: se credenziali hello nel portale di hello non corrispondono a quelle specificate per nome app hello scelto, notifica push di hello non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="c7515-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="c7515-128">Se si utilizza App per dispositivi mobili in Azure App Service come il servizio back-end, vedere hello [versione di App per dispositivi mobili](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c7515-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="c7515-129">Aggiornare il codice hello per il progetto client hello</span><span class="sxs-lookup"><span data-stu-id="c7515-129">Update hello code for hello client project</span></span>
<span data-ttu-id="c7515-130">In questa sezione aggiornare il codice hello nei progetti di hello siano stati completati per hello [iniziare con gli hub di notifica] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c7515-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="c7515-131">Hello deve essere già associato archivio hello e configurato per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="c7515-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="c7515-132">In questa sezione, si verrà aggiungere codice toocall hello nuovo WebAPI back-end e utilizzarlo per la registrazione e l'invio di notifiche.</span><span class="sxs-lookup"><span data-stu-id="c7515-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="c7515-133">In Visual Studio, aprire Esplora hello hello creato per hello [iniziare con gli hub di notifica] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c7515-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="c7515-134">In Esplora soluzioni fare doppio clic su hello **(Windows 8.1)** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c7515-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="c7515-135">Sul lato sinistro di hello, fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="c7515-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="c7515-136">In hello **ricerca** digitare **Http Client**.</span><span class="sxs-lookup"><span data-stu-id="c7515-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="c7515-137">Nell'elenco risultati hello, fare clic su **Microsoft HTTP Client Libraries**, quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="c7515-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="c7515-138">Completare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c7515-138">Complete hello installation.</span></span>
6. <span data-ttu-id="c7515-139">In hello NuGet **ricerca** digitare **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="c7515-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="c7515-140">Installare hello **Json.NET** pacchetto e quindi chiudere hello Gestione pacchetti NuGet finestra.</span><span class="sxs-lookup"><span data-stu-id="c7515-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="c7515-141">Ripetere i passaggi di hello sopra per hello **(Windows Phone 8.1)** hello tooinstall progetto **JSON.NET** pacchetto NuGet per il progetto Windows Phone hello.</span><span class="sxs-lookup"><span data-stu-id="c7515-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="c7515-142">In Esplora soluzioni, in hello **(Windows 8.1)** progetto, fare doppio clic su **MainPage. XAML** tooopen nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="c7515-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="c7515-143">In hello **MainPage. XAML** codice XML, sostituire hello `<Grid>` sezione con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="c7515-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="c7515-144">Questo codice aggiunge una casella di testo Nome utente e password che hello utente eseguirà l'autenticazione con.</span><span class="sxs-lookup"><span data-stu-id="c7515-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="c7515-145">Aggiunge anche nelle caselle di testo per il messaggio di notifica hello e tag username hello che devono ricevere notifica hello:</span><span class="sxs-lookup"><span data-stu-id="c7515-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
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
10. <span data-ttu-id="c7515-146">In Esplora soluzioni, in hello **(Windows Phone 8.1)** progetto, aprire **MainPage. XAML** e sostituire hello Windows Phone 8.1 `<Grid>` sezione con quel codice precedente.</span><span class="sxs-lookup"><span data-stu-id="c7515-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="c7515-147">interfaccia Hello dovrebbe essere simile toowhats illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c7515-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="c7515-148">In Esplora soluzioni, aprire hello **MainPage.xaml.cs** file per hello **(Windows 8.1)** e **(Windows Phone 8.1)** progetti.</span><span class="sxs-lookup"><span data-stu-id="c7515-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="c7515-149">Aggiungere il seguente hello `using` istruzioni nella parte superiore di hello di entrambi i file:</span><span class="sxs-lookup"><span data-stu-id="c7515-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="c7515-150">In **MainPage.xaml.cs** per hello **(Windows 8.1)** e **(Windows Phone 8.1)** progetti, aggiungere hello seguente membro toohello `MainPage` classe.</span><span class="sxs-lookup"><span data-stu-id="c7515-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="c7515-151">Tooreplace assicurarsi di essere `<Enter Your Backend Endpoint>` con hello l'endpoint di back-end effettivo ottenuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7515-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="c7515-152">ad esempio `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c7515-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="c7515-153">Aggiungere codice hello seguente classe MainPage toohello **MainPage.xaml.cs** per hello **(Windows 8.1)** e **(Windows Phone 8.1)** progetti.</span><span class="sxs-lookup"><span data-stu-id="c7515-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="c7515-154">Hello `PushClick` hello è fare clic su gestore per hello **inviare Push** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c7515-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="c7515-155">Chiama hello back-end tootrigger tooall una notifica dispositivi con un tag di nome utente corrispondente hello `to_tag` parametro.</span><span class="sxs-lookup"><span data-stu-id="c7515-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="c7515-156">messaggio di notifica Hello viene inviato come contenuto JSON nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="c7515-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="c7515-157">Hello `LoginAndRegisterClick` hello è fare clic su gestore per hello **Accedi e registrare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c7515-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="c7515-158">Hello basic archivia i token di autenticazione nel servizio di archiviazione locale (si noti che questo rappresenta un token viene utilizzato uno schema di autenticazione), quindi Usa `RegisterClient` tooregister per le notifiche tramite hello di back-end.</span><span class="sxs-lookup"><span data-stu-id="c7515-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

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



1. <span data-ttu-id="c7515-159">In Esplora soluzioni in hello **Shared** progetto, aprire hello **App.xaml.cs** file.</span><span class="sxs-lookup"><span data-stu-id="c7515-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="c7515-160">Trovare chiamata hello troppo`InitNotificationsAsync()` in hello `OnLaunched()` gestore dell'evento.</span><span class="sxs-lookup"><span data-stu-id="c7515-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="c7515-161">Impostare come commento o eliminare anche chiamata hello`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="c7515-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="c7515-162">gestore del pulsante Hello aggiunte in precedenza verrà inizializzato registrazioni di notifica.</span><span class="sxs-lookup"><span data-stu-id="c7515-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="c7515-163">In Esplora soluzioni fare doppio clic su hello **Shared** del progetto, quindi fare clic su **Aggiungi**, quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="c7515-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="c7515-164">Nome classe hello **RegisterClient.cs**, quindi fare clic su **OK** classe hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="c7515-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="c7515-165">Questa classe eseguirà il wrapping hello REST chiamate necessarie toocontact hello app back-end, in ordine tooregister per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="c7515-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="c7515-166">Archivia anche localmente hello *RegistrationId* creato da hello Hub di notifica, come descritto in dettaglio nella [registrazione dal back-end app](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7515-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="c7515-167">Si noti che usa un token di autorizzazione memorizzato nell'archiviazione locale quando si fa clic hello **Accedi e registrare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c7515-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="c7515-168">Aggiungere il seguente hello `using` istruzioni all'inizio di hello del file di RegisterClient.cs hello:</span><span class="sxs-lookup"><span data-stu-id="c7515-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="c7515-169">Aggiungere hello seguente codice all'interno di hello `RegisterClient` definizione di classe.</span><span class="sxs-lookup"><span data-stu-id="c7515-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
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
4. <span data-ttu-id="c7515-170">Salvare tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c7515-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="c7515-171">Test dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="c7515-171">Testing hello Application</span></span>
1. <span data-ttu-id="c7515-172">Avvia un'applicazione hello in Windows 8.1 e Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="c7515-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="c7515-173">Per Windows Phone 8.1 è possibile eseguire l'istanza di hello nell'emulatore Windows hello o un dispositivo reale.</span><span class="sxs-lookup"><span data-stu-id="c7515-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="c7515-174">Nell'istanza di Windows 8.1 hello di hello app, immettere un **Username** e **Password** come illustrato nella schermata di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="c7515-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="c7515-175">Deve essere diversi dal nome dell'utente hello e la password che immessi in Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="c7515-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="c7515-176">Fare clic su **Log in and register** e verificare nella relativa finestra di dialogo di avere effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c7515-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="c7515-177">In questo modo anche hello **inviare Push** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c7515-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="c7515-178">Nell'istanza di hello Windows Phone 8.1, immettere una stringa del nome utente in entrambi hello **Username** e **Password** campi quindi fare clic su **accesso e registrazione**.</span><span class="sxs-lookup"><span data-stu-id="c7515-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="c7515-179">Quindi in hello **destinatario Username Tag** immettere nome utente hello registrato in Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="c7515-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="c7515-180">Immettere un messaggio di notifica e fare clic su **Send Push**.</span><span class="sxs-lookup"><span data-stu-id="c7515-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="c7515-181">Solo i dispositivi di hello che sono registrati con il tag di nome utente corrispondente hello ricevono il messaggio di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="c7515-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="c7515-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7515-182">Next Steps</span></span>
* <span data-ttu-id="c7515-183">Se si desidera che gli utenti dai gruppi di interesse toosegment, vedere [toosend gli hub di notifica di utilizzare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="c7515-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="c7515-184">altre informazioni su come toolearn toouse gli hub di notifica, vedere [materiale sussidiario per gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="c7515-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
