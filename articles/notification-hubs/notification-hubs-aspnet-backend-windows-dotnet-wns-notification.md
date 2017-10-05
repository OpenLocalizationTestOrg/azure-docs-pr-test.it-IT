---
title: Uso di Hub di notifica di Azure per inviare notifiche agli utenti con back-end.NET
description: Informazioni su come inviare notifiche push sicure in Azure. Gli esempi di codice sono scritti in C# mediante l'API .NET.
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
ms.openlocfilehash: c0b963ef661612b1a176dd8e5f01d56e61eb5acb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="5479b-104">Uso di Hub di notifica di Azure per inviare notifiche agli utenti con back-end.NET</span><span class="sxs-lookup"><span data-stu-id="5479b-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="5479b-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5479b-105">Overview</span></span>
<span data-ttu-id="5479b-106">Il supporto per le notifiche push in Azure consente di accedere a un'infrastruttura push facile da usare, multipiattaforma e con scalabilità orizzontale, che semplifica considerevolmente l'implementazione delle notifiche push sia per le applicazioni consumer sia per quelle aziendali per piattaforme mobili.</span><span class="sxs-lookup"><span data-stu-id="5479b-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="5479b-107">In questa esercitazione viene illustrato come usare Hub di notifica di Azure per inviare notifiche push a un utente specifico dell'app su un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="5479b-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="5479b-108">Un back-end WebAPI ASP.NET viene usato per autenticare i client.</span><span class="sxs-lookup"><span data-stu-id="5479b-108">An ASP.NET WebAPI backend is used to authenticate clients.</span></span> <span data-ttu-id="5479b-109">Usando l’utente client autenticato, un tag viene aggiunto automaticamente dal back-end per la registrazione delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="5479b-109">Using the authenticated client user, and tag will be automatically added by the backend to notification registration.</span></span> <span data-ttu-id="5479b-110">Questo tag viene usato per l’invio tramite il back-end per generare notifiche per un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="5479b-110">This tag will be used to send by the backend to generate notifications for a specific user.</span></span> <span data-ttu-id="5479b-111">Per altre informazioni sulla registrazione per le notifiche tramite il back-end di un'app, vedere l'argomento della guida [Registrazione dal back-end dell'app](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="5479b-111">For more information on registering for notifications using an app backend, see the guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="5479b-112">Questa esercitazione si basa sull'hub di notifica e sul progetto creato nell'esercitazione [Introduzione ad Hub di notifica] .</span><span class="sxs-lookup"><span data-stu-id="5479b-112">This tutorial builds on the notification hub and project that you created in the [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="5479b-113">È inoltre propedeutica all'esercitazione [Push sicuro] .</span><span class="sxs-lookup"><span data-stu-id="5479b-113">This tutorial is also the prerequisite to the [Secure Push] tutorial.</span></span> <span data-ttu-id="5479b-114">Dopo avere eseguito i passaggi indicati in questa esercitazione, è possibile passare all'esercitazione [Push sicuro] , che illustra come modificare il codice in questa esercitazione per inviare una notifica push in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="5479b-114">After you have completed the steps in this tutorial, you can proceed to the [Secure Push] tutorial, which shows how to modify the code in this tutorial to send a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5479b-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5479b-115">Before you begin</span></span>
<span data-ttu-id="5479b-116">I commenti e suggerimenti inviati seriamente verranno presi in considerazione.</span><span class="sxs-lookup"><span data-stu-id="5479b-116">We do take your feedback seriously.</span></span> <span data-ttu-id="5479b-117">Se si riscontrano difficoltà nel completare questo argomento o si hanno suggerimenti per migliorarne il contenuto, è possibile lasciare un commento nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="5479b-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span>

<span data-ttu-id="5479b-118">Il codice completo per questa esercitazione è disponibile su GitHub [qui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="5479b-118">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5479b-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5479b-119">Prerequisites</span></span>
<span data-ttu-id="5479b-120">Prima di iniziare questa esercitazione, è necessario aver già completato queste esercitazioni su Servizi mobili:</span><span class="sxs-lookup"><span data-stu-id="5479b-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="5479b-121">[Introduzione ad Hub di notifica]</span><span class="sxs-lookup"><span data-stu-id="5479b-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="5479b-122">Creare il proprio hub di notifica, riservare il nome dell'app e registrarsi per ricevere le notifiche in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5479b-122">You create your notification hub and reserve the app name and register to receive notifications in this tutorial.</span></span> <span data-ttu-id="5479b-123">In questa esercitazione si presuppone che siano già stati completati questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="5479b-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="5479b-124">In caso contrario, attenersi alla procedura riportata in [Introduzione ad Hub di notifica (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), con particolare riferimento alle sezioni [Registrare l'app di Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) e [Configurare l'hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="5479b-124">If not, please follow the steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, the sections [Register your app for the Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="5479b-125">In particolare, assicurarsi di avere immesso i valori **SID pacchetto** e **Chiave privata client** nel portale, nella scheda **Configura** per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="5479b-125">In particular, make sure that you have entered the **Package SID** and **Client Secret** values in the portal, in the **Configure** tab for your notification hub.</span></span> <span data-ttu-id="5479b-126">Questa procedura di configurazione è descritta nella sezione [Configurazione dell'hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="5479b-126">This configuration procedure is described in the section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="5479b-127">Questo passaggio è importante: se le credenziali sul portale non corrispondono a quelle specificate per il nome di app scelto, la notifica push non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="5479b-127">This is an important step: if the credentials on the portal do not match those specified for the app name you choose, the push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="5479b-128">Se si usano app per dispositivi mobili nel servizio app di Azure, vedere la [versione per App per dispositivi mobili](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5479b-128">If you are using Mobile Apps in Azure App Service as your backend service, see the [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-the-code-for-the-client-project"></a><span data-ttu-id="5479b-129">Aggiornare il codice per il progetto client</span><span class="sxs-lookup"><span data-stu-id="5479b-129">Update the code for the client project</span></span>
<span data-ttu-id="5479b-130">In questa sezione viene aggiornato il codice nel progetto completato per l’esercitazione [Introduzione ad Hub di notifica] .</span><span class="sxs-lookup"><span data-stu-id="5479b-130">In this section, you update the code in the project you completed for the [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="5479b-131">Il codice dovrebbe essere già associato allo store e configurato per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="5479b-131">The should already be associated with the store and configured for your notification hub.</span></span> <span data-ttu-id="5479b-132">In questa sezione si aggiungerà il codice per chiamare il nuovo back-end WebAPI e si userà tale codice per la registrazione e l'invio di notifiche.</span><span class="sxs-lookup"><span data-stu-id="5479b-132">In this section, you will add code to call the new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="5479b-133">In Visual Studio, aprire la soluzione creata per l’esercitazione [Introduzione ad Hub di notifica] .</span><span class="sxs-lookup"><span data-stu-id="5479b-133">In Visual Studio, open the the solution you created for the [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="5479b-134">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **(Windows 8.1)**, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5479b-134">In Solution Explorer, right-click the **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="5479b-135">Sul lato sinistro fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="5479b-135">On the left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="5479b-136">Nella **casella di ricerca** digitare **Client Http**.</span><span class="sxs-lookup"><span data-stu-id="5479b-136">In the **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="5479b-137">Nell'elenco dei risultati fare clic su **Librerie client HTTP Microsoft** e quindi su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="5479b-137">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="5479b-138">Completare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="5479b-138">Complete the installation.</span></span>
6. <span data-ttu-id="5479b-139">Di nuovo nella **casella di ricerca** di NuGet digitare **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="5479b-139">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="5479b-140">Installare il pacchetto **Json.NET** , quindi chiudere la finestra di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="5479b-140">Install the **Json.NET** package, and then close the NuGet Package Manager window.</span></span>
7. <span data-ttu-id="5479b-141">Ripetere i passaggi precedenti per il progetto **(Windows Phone 8.1)** al fine di installare il pacchetto NuGet **JSON.NET** per il progetto Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="5479b-141">Repeat the steps above for the **(Windows Phone 8.1)** project to install the **JSON.NET** NuGet package for the Windows Phone project.</span></span>
8. <span data-ttu-id="5479b-142">In Esplora soluzioni, nel progetto **(Windows 8.1)**, fare doppio clic su **MainPage.xaml** per aprirlo nell'editor di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5479b-142">In Solution Explorer, in the **(Windows 8.1)** project, double-click **MainPage.xaml** to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="5479b-143">Nel codice XML **MainPage.xaml** sostituire la sezione `<Grid>` con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="5479b-143">In the **MainPage.xaml** XML code, replace the `<Grid>` section with the following code.</span></span> <span data-ttu-id="5479b-144">Questo codice consente di aggiungere una casella di testo con nome utente e password con cui l'utente eseguirà l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="5479b-144">This code adds a username and password textbox that the user will authenticate with.</span></span> <span data-ttu-id="5479b-145">Consente inoltre di aggiungere caselle di testo per il messaggio di notifica e il tag del nome utente che deve ricevere la notifica:</span><span class="sxs-lookup"><span data-stu-id="5479b-145">It also adds textboxes for the notification message and the username tag that should receive the notification:</span></span>
   
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
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag To Send To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="5479b-146">In Esplora soluzioni, nel progetto **(Windows Phone 8.1)**, aprire **MainPage.xaml** e sostituire la sezione `<Grid>` di Windows Phone 8.1 con lo stesso codice riportato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5479b-146">In Solution Explorer, in the **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace the Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="5479b-147">L’interfaccia dovrebbe essere simile a quanto illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="5479b-147">The interface should look similar to whats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="5479b-148">In Esplora soluzioni aprire il file **MainPage.xaml.cs** per i progetti **(Windows 8.1)** e **(Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="5479b-148">In Solution Explorer, open the **MainPage.xaml.cs** file for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="5479b-149">Aggiungere le istruzioni `using` seguenti all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="5479b-149">Add the following `using` statements at the top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="5479b-150">In **MainPage.xaml.cs**, per i progetti **(Windows 8.1)** e **(Windows Phone 8.1)**, aggiungere il seguente membro alla classe `MainPage`.</span><span class="sxs-lookup"><span data-stu-id="5479b-150">In **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add the following member to the `MainPage` class.</span></span> <span data-ttu-id="5479b-151">Assicurarsi di sostituire `<Enter Your Backend Endpoint>` con l'endpoint back-end effettivo ottenuto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="5479b-151">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="5479b-152">ad esempio `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5479b-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="5479b-153">Aggiungere il codice seguente alla classe MainPage in **MainPage.xaml.cs** per i progetti **(Windows 8.1)** e **(Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="5479b-153">Add the code below to the MainPage class in **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="5479b-154">Il metodo `PushClick` è il gestore di clic per il pulsante **Send Push** .</span><span class="sxs-lookup"><span data-stu-id="5479b-154">The `PushClick` method is the click handler for the **Send Push** button.</span></span> <span data-ttu-id="5479b-155">Chiama il back-end per attivare una notifica a tutti i dispositivi con un tag di nome utente corrispondente al parametro `to_tag` .</span><span class="sxs-lookup"><span data-stu-id="5479b-155">It calls the backend to trigger a notification to all devices with a username tag that matches the `to_tag` parameter.</span></span> <span data-ttu-id="5479b-156">Il messaggio di notifica viene inviato come contenuto JSON nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5479b-156">The notification message is sent as JSON content in the request body.</span></span>
    
    <span data-ttu-id="5479b-157">Il metodo `LoginAndRegisterClick` è il gestore di clic per il pulsante **Log in and register** .</span><span class="sxs-lookup"><span data-stu-id="5479b-157">The `LoginAndRegisterClick` method is the click handler for the **Log in and register** button.</span></span> <span data-ttu-id="5479b-158">Tale metodo memorizza il token di autenticazione di base nell'archivio locale (si noti che rappresenta qualsiasi token usato dallo schema di autenticazione), quindi usa `RegisterClient` per la registrazione per le notifiche tramite il back-end.</span><span class="sxs-lookup"><span data-stu-id="5479b-158">It stores the basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` to register for notifications using the backend.</span></span>

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
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed to send " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // The "username:<user name>" tag gets automatically added by the message handler in the backend.
            // The tag passed here can be whatever other tags you may want to use.
            try
            {
                // The device handle used will be different depending on the device and PNS. 
                // Windows devices use the channel uri as the PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed to register with RegisterClient");
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



1. <span data-ttu-id="5479b-159">In Esplora soluzioni, nel progetto **Condiviso**, aprire il file **App.xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="5479b-159">In Solution Explorer, under the **Shared** project, open the **App.xaml.cs** file.</span></span> <span data-ttu-id="5479b-160">Individuare la chiamata a `InitNotificationsAsync()` in the `OnLaunched()` .</span><span class="sxs-lookup"><span data-stu-id="5479b-160">Find the call to `InitNotificationsAsync()` in the `OnLaunched()` event handler.</span></span> <span data-ttu-id="5479b-161">Impostare come commento o eliminare la chiamata a `InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="5479b-161">Comment out or delete the call to `InitNotificationsAsync()`.</span></span> <span data-ttu-id="5479b-162">Il gestore del pulsante aggiunto in precedenza inizializzerà le registrazioni delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="5479b-162">The button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="5479b-163">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **Condiviso**, quindi scegliere **Aggiungi** e infine **Classe**.</span><span class="sxs-lookup"><span data-stu-id="5479b-163">In Solution Explorer, right-click the **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="5479b-164">Assegnare alla classe il nome **RegisterClient.cs**, quindi fare clic su **OK** per generare la classe.</span><span class="sxs-lookup"><span data-stu-id="5479b-164">Name the class **RegisterClient.cs**, then click **OK** to generate the class.</span></span>
   
   <span data-ttu-id="5479b-165">Questa classe conclude le chiamate REST necessarie per contattare il back-end dell'app allo scopo di effettuare la registrazione per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="5479b-165">This class will wrap the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="5479b-166">Archivia inoltre in locale i *registrationId* creati dall'hub di notifica, come illustrato in [Registrazione dal back-end dell'app](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="5479b-166">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="5479b-167">Si noti che usa un token di autorizzazione memorizzato nell'archivio locale quando si fa clic sul pulsante **Esegui accesso e registrazione** .</span><span class="sxs-lookup"><span data-stu-id="5479b-167">Note that it uses an authorization token stored in local storage when you click the **Log in and register** button.</span></span>
2. <span data-ttu-id="5479b-168">Aggiungere le seguenti istruzioni `using` all'inizio del file RegisterClient.cs:</span><span class="sxs-lookup"><span data-stu-id="5479b-168">Add the following `using` statements at the top of the RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="5479b-169">Aggiungere il codice seguente all'interno della definizione di classe `RegisterClient` .</span><span class="sxs-lookup"><span data-stu-id="5479b-169">Add the following code inside the `RegisterClient` class definition.</span></span>
   
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
4. <span data-ttu-id="5479b-170">Salvare tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="5479b-170">Save all your changes.</span></span>

## <a name="testing-the-application"></a><span data-ttu-id="5479b-171">Test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5479b-171">Testing the Application</span></span>
1. <span data-ttu-id="5479b-172">Avviare l'applicazione in Windows 8.1 e Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="5479b-172">Launch the application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="5479b-173">Per Windows Phone 8.1 è possibile eseguire l'istanza nell'emulatore o in un dispositivo reale.</span><span class="sxs-lookup"><span data-stu-id="5479b-173">For Windows Phone 8.1 you can run the instance in the emulator or an actual device.</span></span>
2. <span data-ttu-id="5479b-174">Nell'istanza di Windows 8.1 dell'app immettere un **Nome utente** e una **Password** come illustrato nella schermata riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="5479b-174">In the Windows 8.1 instance of the app, enter a **Username** and **Password** as shown in the screen below.</span></span> <span data-ttu-id="5479b-175">È consigliabile immettere un nome utente e una password diversi dal nome utente e dalla password immessi in Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="5479b-175">It should differ from the user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="5479b-176">Fare clic su **Log in and register** e verificare nella relativa finestra di dialogo di avere effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="5479b-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="5479b-177">In questo modo anche il pulsante **Send Push** verrà abilitato.</span><span class="sxs-lookup"><span data-stu-id="5479b-177">This will also enable the **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="5479b-178">Nell'istanza di Windows Phone 8.1 immettere la stringa di un nome utente nei campi **Nome utente** e **Password** quini fare clic su **Log in and register**.</span><span class="sxs-lookup"><span data-stu-id="5479b-178">On the Windows Phone 8.1 instance, enter a user name string in both the **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="5479b-179">Quindi nel campo relativo al **tag del nome utente del destinatario** immettere il nome utente registrato in Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="5479b-179">Then in the **Recipient Username Tag** field, enter the user name registered on Windows 8.1.</span></span> <span data-ttu-id="5479b-180">Immettere un messaggio di notifica e fare clic su **Send Push**.</span><span class="sxs-lookup"><span data-stu-id="5479b-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="5479b-181">Solo i dispositivi registrati con il tag del nome utente del destinatario riceveranno il messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="5479b-181">Only the devices that have registered with the matching username tag receive the notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="5479b-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5479b-182">Next Steps</span></span>
* <span data-ttu-id="5479b-183">Se si desidera segmentare gli utenti per gruppi di interesse, vedere [Utilizzo di Hub di notifica per inviare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="5479b-183">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span>
* <span data-ttu-id="5479b-184">Per ulteriori informazioni sull'uso di Hub di notifica, vedere la pagina delle [linee guida su Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="5479b-184">To learn more about how to use Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
<span data-ttu-id="5479b-185">[Introduzione ad Hub di notifica]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="5479b-185">[Get started with Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="5479b-186">[Push sicuro]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="5479b-186">[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span></span>
<span data-ttu-id="5479b-187">[Utilizzo di Hub di notifica per inviare le ultime notizie]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="5479b-187">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
<span data-ttu-id="5479b-188">[linee guida su Hub di notifica]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="5479b-188">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
