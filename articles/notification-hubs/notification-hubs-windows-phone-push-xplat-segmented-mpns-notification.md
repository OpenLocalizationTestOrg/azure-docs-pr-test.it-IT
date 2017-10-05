---
title: Usare Hub di notifica per inviare le ultime notizie (Windows Phone)
description: Usare Hub di notifica di Azure con i tag nelle registrazioni per inviare le ultime notizie a un'app per Windows Phone.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3a6a69bf555c7267d3fbeb03ff6c03054991960f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="c9285-103">Uso di Hub di notifica per inviare le ultime notizie</span><span class="sxs-lookup"><span data-stu-id="c9285-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="c9285-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c9285-104">Overview</span></span>
<span data-ttu-id="c9285-105">Questo argomento descrive come usare Hub di notifica di Azure per trasmettere le notifiche relative alle ultime notizie a un'app per Windows Phone 8.0/8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="c9285-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="c9285-106">Se si sviluppano app per Windows Store o Windows Phone 8.1, fare riferimento alla versione [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) .</span><span class="sxs-lookup"><span data-stu-id="c9285-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer to to the [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="c9285-107">Al termine dell'esercitazione, si sarà appreso a effettuare la registrazione alle categorie di ultime notizie desiderate e ricevere le notifiche push solo da tali categorie.</span><span class="sxs-lookup"><span data-stu-id="c9285-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="c9285-108">Questo scenario è un modello comune per molte app nelle quali le notifiche devono essere inviate a gruppi di utenti che hanno dichiarato un interesse, ad esempio lettori di feed RSS, app per fan di musica e così via.</span><span class="sxs-lookup"><span data-stu-id="c9285-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="c9285-109">È possibile abilitare gli scenari di trasmissione includendo uno o più *tag* durante la creazione di una registrazione nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="c9285-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="c9285-110">Quando le notifiche vengono inviate a un tag, tutti i dispositivi che hanno effettuato la registrazione al tag riceveranno la notifica.</span><span class="sxs-lookup"><span data-stu-id="c9285-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="c9285-111">Poiché i tag sono costituiti da stringhe, non è necessario eseguire il provisioning anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="c9285-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="c9285-112">Per ulteriori informazioni sui tag, vedere [Espressioni di routing e tag  per hub di notifica](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="c9285-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9285-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c9285-113">Prerequisites</span></span>
<span data-ttu-id="c9285-114">Questo argomento si basa sull'app creata nell'esercitazione [Introduzione ad Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="c9285-114">This topic builds on the app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="c9285-115">Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="c9285-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="c9285-116">Aggiungere la selezione delle categorie all'app</span><span class="sxs-lookup"><span data-stu-id="c9285-116">Add category selection to the app</span></span>
<span data-ttu-id="c9285-117">Il primo passaggio prevede l'aggiunta degli elementi dell'interfaccia utente alla pagina principale esistente per consentire all'utente di selezionare le categorie per le quali registrarsi.</span><span class="sxs-lookup"><span data-stu-id="c9285-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="c9285-118">Le categorie selezionate da un utente sono archiviate nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c9285-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="c9285-119">All'avvio dell'app, viene creata una registrazione nell'hub di notifica con le categorie selezionate come tag.</span><span class="sxs-lookup"><span data-stu-id="c9285-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="c9285-120">Aprire il file di progetto MainPage.xaml, quindi sostituire gli elementi **Grid** denominati `TitlePanel` e `ContentPanel` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c9285-120">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. <span data-ttu-id="c9285-121">Nel progetto creare una nuova classe denominata **Notifications**, aggiungere il modificatore **public** alla definizione della classe e quindi aggiungere le istruzioni **using** seguenti al nuovo file di codice:</span><span class="sxs-lookup"><span data-stu-id="c9285-121">In the project, create a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="c9285-122">Copiare il codice seguente nella nuova classe **Notifications** :</span><span class="sxs-lookup"><span data-stu-id="c9285-122">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task to complete registration in the ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used to receive notifications while the app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete the registrationTask here.  
            // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // The stored categories tags are passed with the template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used to receive notifications while the app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out the information that was part of the message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all the fields in the toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="c9285-123">Questa classe utilizza lo spazio di memorizzazione isolato  per archiviare le categorie di notizie che il dispositivo deve ricevere.</span><span class="sxs-lookup"><span data-stu-id="c9285-123">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="c9285-124">Contiene inoltre i metodi di registrazione per queste categorie tramite una registrazione delle notifiche [modello](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="c9285-124">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="c9285-125">Nel file di progetto App.xaml.cs aggiungere la proprietà seguente alla classe **App**.</span><span class="sxs-lookup"><span data-stu-id="c9285-125">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="c9285-126">Sostituire i segnaposto `<hub name>` e `<connection string with listen access>` con il nome dell'hub di notifica e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c9285-126">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="c9285-127">Poiché le credenziali che sono distribuite con un'app client in genere non sono sicure, distribuire solo la chiave per l'accesso Listen con l'app client.</span><span class="sxs-lookup"><span data-stu-id="c9285-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="c9285-128">L'accesso Listen consente all'app di registrarsi per le notifiche ma le registrazioni esistenti non possono essere modificate e le notifiche non possono essere inviate.</span><span class="sxs-lookup"><span data-stu-id="c9285-128">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="c9285-129">La chiave di accesso completo viene usata in un servizio back-end sicuro per l'invio delle notifiche e la modifica delle registrazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="c9285-129">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="c9285-130">In MainPage.xaml.cs aggiungere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="c9285-130">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="c9285-131">Aggiungere quindi il metodo seguente nel file di progetto MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="c9285-131">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    <span data-ttu-id="c9285-132">Questo metodo crea un elenco di categorie e utilizza la classe **Notifications** per archiviare l'elenco nell'archiviazione locale e registrare i tag corrispondenti nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="c9285-132">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="c9285-133">Se le categorie vengono modificate, la registrazione viene ricreata con le nuove categorie.</span><span class="sxs-lookup"><span data-stu-id="c9285-133">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="c9285-134">L'app può quindi archiviare un set di categorie nell'archiviazione locale del dispositivo ed effettuare la registrazione con l'hub di notifica ogni volta che l'utente modifica la selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="c9285-134">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="c9285-135">Registrazione per le notifiche</span><span class="sxs-lookup"><span data-stu-id="c9285-135">Register for notifications</span></span>
<span data-ttu-id="c9285-136">Questa procedura consente di effettuare la registrazione con l'hub di notifica all'avvio usando le categorie archiviate nella risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="c9285-136">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="c9285-137">Poiché l'URI di canale assegnato dal Servizio notifica push Microsoft può cambiare in qualsiasi momento, è necessario ripetere la registrazione per le notifiche di frequente per evitare errori di notifica.</span><span class="sxs-lookup"><span data-stu-id="c9285-137">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="c9285-138">Questo esempio esegue la registrazione per le notifiche a ogni avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="c9285-138">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="c9285-139">Per le app che vengono eseguite di frequente, oltre una volta al giorno, è possibile ignorare la registrazione per conservare la larghezza di banda qualora sia trascorso meno di un giorno dalla registrazione precedente.</span><span class="sxs-lookup"><span data-stu-id="c9285-139">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="c9285-140">Aprire il file App.xaml.cs e aggiungere il modificatore **async** al metodo **Application_Launching** e sostituire il codice di registrazione di Hub di notifica aggiunto in [Introduzione ad Hub di notifica] con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c9285-140">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="c9285-141">In questo modo, ogni volta che l'app viene avviata vengono recuperate le categorie dall'archiviazione locale e viene richiesta una registrazione per tali categorie.</span><span class="sxs-lookup"><span data-stu-id="c9285-141">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="c9285-142">Nel file di progetto MainPage.xaml.cs aggiungere il codice seguente che implementa il metodo **OnNavigatedTo** :</span><span class="sxs-lookup"><span data-stu-id="c9285-142">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    <span data-ttu-id="c9285-143">La pagina principale viene aggiornata in base allo stato delle categorie salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c9285-143">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="c9285-144">Ora l'app è completa e può quindi archiviare un set di categorie nell'archiviazione locale del dispositivo ed effettuare la registrazione con l'hub di notifica ogni volta che l'utente modifica la selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="c9285-144">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="c9285-145">Verrà ora definito un back-end per l'invio delle notifiche delle categorie all'app.</span><span class="sxs-lookup"><span data-stu-id="c9285-145">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="c9285-146">Invio di notifiche con tag</span><span class="sxs-lookup"><span data-stu-id="c9285-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="c9285-147">Eseguire l'app e generare notifiche</span><span class="sxs-lookup"><span data-stu-id="c9285-147">Run the app and generate notifications</span></span>
1. <span data-ttu-id="c9285-148">In Visual Studio premere F5 per compilare e avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="c9285-148">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="c9285-149">Si noti che l'interfaccia utente dell'app fornisce un set di interruttori che consentono di scegliere le categorie per le quali effettuare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c9285-149">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="c9285-150">Abilitare uno o più interruttori di categorie e quindi fare clic su **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="c9285-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="c9285-151">L'app converte le categorie selezionate in tag e richiede una nuova registrazione del dispositivo per i tag selezionati dall'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="c9285-151">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="c9285-152">Le categorie registrate vengono restituite e visualizzate in una finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c9285-152">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="c9285-153">Dopo aver ricevuto una conferma di completamento della sottoscrizione delle categorie, eseguire l'app console per l'invio di notifiche per ogni categoria.</span><span class="sxs-lookup"><span data-stu-id="c9285-153">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each categories.</span></span> <span data-ttu-id="c9285-154">Verificare di ricevere una notifica solo per le categorie sottoscritte.</span><span class="sxs-lookup"><span data-stu-id="c9285-154">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="c9285-155">L'argomento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="c9285-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how to broadcast breaking news by category. Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs to broadcast localized breaking news]

    Learn how to expand the breaking news app to enable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how to push notifications to specific authenticated users. This is a good solution for sending notifications only to specific users.
-->

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
<span data-ttu-id="c9285-156">[Introduzione ad Hub di notifica]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span><span class="sxs-lookup"><span data-stu-id="c9285-156">[Get started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span></span>
[Use Notification Hubs to broadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

