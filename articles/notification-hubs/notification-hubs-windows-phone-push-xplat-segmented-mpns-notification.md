---
title: aaaUse gli hub di notifica toosend le ultime notizie (Windows Phone)
description: Utilizzare tag toouse gli hub di notifica di Azure in toosend registrazioni app di Windows Phone tooa notizie di rilievo.
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
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="9352b-103">Utilizzare gli hub di notifica toosend le ultime notizie</span><span class="sxs-lookup"><span data-stu-id="9352b-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="9352b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9352b-104">Overview</span></span>
<span data-ttu-id="9352b-105">In questo argomento illustra come toouse gli hub di notifica di Azure toobroadcast ultime notizie notifiche tooa Windows Phone 8.0/8.1 Silverlight app.</span><span class="sxs-lookup"><span data-stu-id="9352b-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="9352b-106">Se la destinazione è Windows Store o app di Windows Phone 8.1, consultare tootoohello [universali di Windows](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) versione.</span><span class="sxs-lookup"><span data-stu-id="9352b-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="9352b-107">Al termine, verrà essere in grado di tooregister per l'interruzione delle categorie di notizie, che si è interessati e ricevere notifiche di push solo per quelle categorie.</span><span class="sxs-lookup"><span data-stu-id="9352b-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="9352b-108">Questo scenario è un modello comune per molte applicazioni in cui le notifiche hanno inviato toobe toogroups di utenti che hanno dichiarato in precedenza interesse in essi, ad esempio lettore RSS, le App per ventole musica e così via.</span><span class="sxs-lookup"><span data-stu-id="9352b-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="9352b-109">Scenari di trasmissione sono abilitati per includere uno o più *tag* durante la creazione di una registrazione nell'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="9352b-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="9352b-110">Quando le notifiche vengono inviate tooa tag, tutti i dispositivi che sono registrati per il tag di hello riceverà la notifica hello.</span><span class="sxs-lookup"><span data-stu-id="9352b-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="9352b-111">Poiché i tag sono semplicemente stringhe, essi non è toobe in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9352b-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="9352b-112">Per ulteriori informazioni sui tag, vedere troppo[Routing hub di notifica ed espressioni Tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="9352b-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9352b-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9352b-113">Prerequisites</span></span>
<span data-ttu-id="9352b-114">In questo argomento è basato sull'app hello è stato creato in [iniziare con gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="9352b-114">This topic builds on hello app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="9352b-115">Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [iniziare con gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="9352b-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="9352b-116">Aggiungi categoria selezione toohello app</span><span class="sxs-lookup"><span data-stu-id="9352b-116">Add category selection toohello app</span></span>
<span data-ttu-id="9352b-117">Hello primo passaggio consiste tooadd hello UI elementi tooyour esistente pagina principale che consentono di hello utente tooselect categorie tooregister.</span><span class="sxs-lookup"><span data-stu-id="9352b-117">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="9352b-118">categorie di Hello selezionate da un utente vengono archiviate nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9352b-118">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="9352b-119">Quando viene avviata l'applicazione hello, viene creata una registrazione del dispositivo nell'hub di notifica con categorie hello selezionata sotto forma di tag.</span><span class="sxs-lookup"><span data-stu-id="9352b-119">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="9352b-120">Aprire il file di progetto di hello MainPage. XAML, quindi sostituire hello **griglia** gli elementi denominati `TitlePanel` e `ContentPanel` con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="9352b-120">Open hello MainPage.xaml project file, then replace hello **Grid** elements named `TitlePanel` and `ContentPanel` with hello following code:</span></span>
   
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
2. <span data-ttu-id="9352b-121">Nel progetto hello, creare una nuova classe denominata **notifiche**, aggiungere hello **pubblica** toohello modificatore definizione di classe, quindi aggiungere il seguente hello **utilizzando** istruzioni toohello nuovo file di codice:</span><span class="sxs-lookup"><span data-stu-id="9352b-121">In hello project, create a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="9352b-122">Il codice seguente di hello di copia nel nuovo hello **notifiche** classe:</span><span class="sxs-lookup"><span data-stu-id="9352b-122">Copy hello following code into hello new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
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
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
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
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
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
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="9352b-123">Questa classe utilizza hello isolato archiviazione toostore hello categorie delle news che il dispositivo è tooreceive.</span><span class="sxs-lookup"><span data-stu-id="9352b-123">This class uses hello isolated storage toostore hello categories of news that this device is tooreceive.</span></span> <span data-ttu-id="9352b-124">Contiene anche metodi tooregister per queste categorie utilizzando un [modello](notification-hubs-templates-cross-platform-push-messages.md) registrazione della notifica.</span><span class="sxs-lookup"><span data-stu-id="9352b-124">It also contains methods tooregister for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="9352b-125">Nel file di progetto App.xaml.cs hello, aggiungere hello seguente proprietà toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="9352b-125">In hello App.xaml.cs project file, add hello following property toohello **App** class.</span></span> <span data-ttu-id="9352b-126">Sostituire hello `<hub name>` e `<connection string with listen access>` segnaposto con la notifica hub hello nome e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9352b-126">Replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="9352b-127">Poiché le credenziali che vengono distribuite con un'applicazione client non sono in genere sicure, deve essere distribuito solo chiave hello per l'accesso in ascolto con l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="9352b-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="9352b-128">Abilita accesso che tooregister l'app per le notifiche, ma le registrazioni esistenti non può essere modificato in attesa e non possono essere inviate le notifiche.</span><span class="sxs-lookup"><span data-stu-id="9352b-128">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="9352b-129">chiave di accesso completo Hello viene utilizzata in un servizio back-end protetto per l'invio di notifiche e la modifica delle registrazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="9352b-129">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="9352b-130">Aggiungere il file MainPage.xaml.cs, hello successiva riga:</span><span class="sxs-lookup"><span data-stu-id="9352b-130">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="9352b-131">Nel file di progetto MainPage.xaml.cs hello, aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="9352b-131">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="9352b-132">Questo metodo crea un elenco di categorie e utilizza hello **notifiche** classe elenco hello toostore nella memoria locale hello e registrare i corrispondenti tag di hello con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="9352b-132">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="9352b-133">Quando vengono modificate le categorie, registrazione hello viene ricreata con le nuove categorie hello.</span><span class="sxs-lookup"><span data-stu-id="9352b-133">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="9352b-134">L'app è in grado di toostore un set di categorie in archiviazione locale nel dispositivo hello e registrare con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="9352b-134">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="9352b-135">Registrazione per le notifiche</span><span class="sxs-lookup"><span data-stu-id="9352b-135">Register for notifications</span></span>
<span data-ttu-id="9352b-136">Questi passaggi registrare con l'hub di notifica hello all'avvio mediante le categorie di hello che sono state archiviate nel servizio di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="9352b-136">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="9352b-137">Poiché il canale di hello URI assegnato da hello Microsoft Push Notification Service (MPNS) è possibile modificare in qualsiasi momento, è consigliabile registrare per le notifiche di frequente errori di notifica tooavoid.</span><span class="sxs-lookup"><span data-stu-id="9352b-137">Because hello channel URI assigned by hello Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="9352b-138">Questo esempio viene registrato per le notifiche ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9352b-138">This example registers for notifications every time that hello app starts.</span></span> <span data-ttu-id="9352b-139">Per le app che vengono eseguite frequentemente, più di una volta al giorno, è possibile probabilmente ignorare la larghezza di banda di registrazione toopreserve se meno di un giorno è trascorso registrazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="9352b-139">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="9352b-140">Aprire il file App.xaml.cs hello e aggiungere hello **async** modificatore troppo**Application_Launching** (metodo) e sostituire codice di registrazione hello hub di notifica che è stato aggiunto in [iniziare con gli hub di notifica] con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="9352b-140">Open hello App.xaml.cs file and add hello **async** modifier too**Application_Launching** method and replace hello Notification Hubs registration code that you added in [Get started with Notification Hubs] with hello following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="9352b-141">Ciò assicura che ogni volta che viene avviata l'applicazione hello Recupera categorie hello dall'archiviazione locale e richiede una registrazione per queste categorie.</span><span class="sxs-lookup"><span data-stu-id="9352b-141">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="9352b-142">Nel file di progetto MainPage.xaml.cs hello, aggiungere hello seguente di codice che implementa hello **OnNavigatedTo** metodo:</span><span class="sxs-lookup"><span data-stu-id="9352b-142">In hello MainPage.xaml.cs project file, add hello following code that implements hello **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="9352b-143">Questa pagina principale di hello gli aggiornamenti in base allo stato di hello di precedentemente salvato categorie.</span><span class="sxs-lookup"><span data-stu-id="9352b-143">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="9352b-144">app Hello è completo ed è possibile archiviare un set di categorie in hello dispositivo archiviazione locale utilizzato tooregister con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="9352b-144">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="9352b-145">Successivamente, verrà definito un back-end che può inviare categoria notifiche toothis app.</span><span class="sxs-lookup"><span data-stu-id="9352b-145">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="9352b-146">Invio di notifiche con tag</span><span class="sxs-lookup"><span data-stu-id="9352b-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="9352b-147">Eseguire app hello e generare le notifiche</span><span class="sxs-lookup"><span data-stu-id="9352b-147">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="9352b-148">In Visual Studio, premere F5 toocompile e avviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9352b-148">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="9352b-149">Si noti che app hello di che dell'interfaccia utente fornisce un set attiva o disattiva che consente di scegliere toosubscribe categorie hello per.</span><span class="sxs-lookup"><span data-stu-id="9352b-149">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="9352b-150">Abilitare uno o più interruttori di categorie e quindi fare clic su **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="9352b-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="9352b-151">applicazione Hello converte le categorie selezionata hello in tag e richiede una nuova registrazione di dispositivi per i tag hello selezionato dall'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="9352b-151">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="9352b-152">Hello categorie registrate vengono restituite e visualizzate in una finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9352b-152">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="9352b-153">Dopo aver ricevuto un messaggio di conferma che le categorie sono state sottoscrizione completata, eseguire le notifiche tramite toosend app console hello per le categorie di ogni.</span><span class="sxs-lookup"><span data-stu-id="9352b-153">After receiving a confirmation that your categories were subscription completed, run hello console app toosend notifications for each categories.</span></span> <span data-ttu-id="9352b-154">Verificare che si riceve solo una notifica per le categorie di hello che sottoscritti.</span><span class="sxs-lookup"><span data-stu-id="9352b-154">Verify you only receive a notification for hello categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="9352b-155">L'argomento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9352b-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[iniziare con gli hub di notifica]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

