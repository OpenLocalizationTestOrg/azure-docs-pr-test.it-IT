---
title: aaaUse gli hub di notifica toosend le ultime notizie (universale di Windows)
description: Usare gli hub di notifica di Azure con i tag in hello registrazione toosend ultime notizie tooa applicazioni universali di Windows.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="16688-103">Utilizzare gli hub di notifica toosend le ultime notizie</span><span class="sxs-lookup"><span data-stu-id="16688-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="16688-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="16688-104">Overview</span></span>
<span data-ttu-id="16688-105">In questo argomento illustra come toouse gli hub di notifica di Azure toobroadcast ultime notizie notifiche tooa Windows Store o app di Windows Phone 8.1 (non Silverlight).</span><span class="sxs-lookup"><span data-stu-id="16688-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="16688-106">Se la destinazione è Windows Phone 8.1 Silverlight, vedere toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) versione.</span><span class="sxs-lookup"><span data-stu-id="16688-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="16688-107">Al termine, verrà essere in grado di tooregister per l'interruzione delle categorie di notizie, che si è interessati e ricevere notifiche di push solo per quelle categorie.</span><span class="sxs-lookup"><span data-stu-id="16688-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="16688-108">Questo scenario è un modello comune per molte applicazioni in cui le notifiche hanno inviato toobe toogroups di utenti che hanno dichiarato in precedenza interesse in essi, ad esempio lettore RSS, le App per fan e così via.</span><span class="sxs-lookup"><span data-stu-id="16688-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="16688-109">Scenari di trasmissione sono abilitati per includere uno o più *tag* durante la creazione di una registrazione nell'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="16688-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="16688-110">Quando le notifiche vengono inviate tooa tag, tutti i dispositivi che sono registrati per il tag di hello riceverà la notifica hello.</span><span class="sxs-lookup"><span data-stu-id="16688-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="16688-111">Poiché i tag sono semplicemente stringhe, essi non è toobe in precedenza.</span><span class="sxs-lookup"><span data-stu-id="16688-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="16688-112">Per ulteriori informazioni sui tag, vedere troppo[Routing hub di notifica ed espressioni Tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="16688-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="16688-113">Progetti creati con Windows Store e Windows Phone 8.1 o versioni precedenti non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="16688-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="16688-114">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="16688-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="16688-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="16688-115">Prerequisites</span></span>
<span data-ttu-id="16688-116">In questo argomento è basato sull'app hello è stato creato in [iniziare con gli hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="16688-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="16688-117">Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="16688-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="16688-118">Aggiungi categoria selezione toohello app</span><span class="sxs-lookup"><span data-stu-id="16688-118">Add category selection toohello app</span></span>
<span data-ttu-id="16688-119">Hello primo passaggio consiste tooadd hello UI elementi tooyour esistente pagina principale che consentono di hello utente tooselect categorie tooregister.</span><span class="sxs-lookup"><span data-stu-id="16688-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="16688-120">categorie di Hello selezionate da un utente vengono archiviate nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="16688-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="16688-121">Quando viene avviata l'applicazione hello, viene creata una registrazione del dispositivo nell'hub di notifica con categorie hello selezionata sotto forma di tag.</span><span class="sxs-lookup"><span data-stu-id="16688-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="16688-122">Aprire il file di progetto di hello MainPage. XAML, quindi hello copia seguente di codice hello **griglia** elemento:</span><span class="sxs-lookup"><span data-stu-id="16688-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. <span data-ttu-id="16688-123">Fare clic con il pulsante destro hello **Shared** del progetto e aggiungere una nuova classe denominata **notifiche**, aggiungere hello **pubblica** toohello modificatore definizione di classe, quindi aggiungere hello seguente **utilizzando** istruzioni toohello nuovo file di codice:</span><span class="sxs-lookup"><span data-stu-id="16688-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="16688-124">Il codice seguente di hello di copia nel nuovo hello **notifiche** classe:</span><span class="sxs-lookup"><span data-stu-id="16688-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="16688-125">Questa classe utilizza hello archiviazione locale toostore hello le categorie di notizie, che in questo dispositivo è tooreceive.</span><span class="sxs-lookup"><span data-stu-id="16688-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="16688-126">Si noti che, anziché chiamare hello *RegisterNativeAsync* metodo viene chiamato *RegisterTemplateAsync* tooregister per le categorie di hello mediante un modello di registrazione.</span><span class="sxs-lookup"><span data-stu-id="16688-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="16688-127">È inoltre fornire un nome per il modello di hello ("simpleWNSTemplateExample"), perché potrebbe essere opportuno tooregister più di un modello, ad esempio uno per le notifiche di tipo avviso popup e uno per i riquadri e dobbiamo tooname in ordine tooupdate in grado di toobe o eliminarli.</span><span class="sxs-lookup"><span data-stu-id="16688-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="16688-128">Si noti che se si registra un dispositivo più modelli con hello stesso tag, un messaggio in arrivo di destinazione che tag comporta più notifiche recapitati dispositivo toohello (uno per ogni modello).</span><span class="sxs-lookup"><span data-stu-id="16688-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="16688-129">Questo comportamento è utile quando hello stesso messaggio logico ha tooresult in più notifiche visive, ad esempio che illustra un badge sia un avviso popup in un'applicazione Windows Store.</span><span class="sxs-lookup"><span data-stu-id="16688-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="16688-130">Per altre informazioni sui modelli, vedere [Modelli](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="16688-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="16688-131">Nel file di progetto App.xaml.cs hello, aggiungere hello seguente proprietà toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="16688-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="16688-132">Questa proprietà è utilizzata toocreate e accesso un **notifiche** istanza.</span><span class="sxs-lookup"><span data-stu-id="16688-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="16688-133">In hello di sopra di codice, sostituire hello `<hub name>` e `<connection string with listen access>` segnaposto con la notifica hub hello nome e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="16688-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="16688-134">Poiché le credenziali che vengono distribuite con un'applicazione client non sono in genere sicure, deve essere distribuito solo chiave hello per l'accesso in ascolto con l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="16688-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="16688-135">Abilita accesso che tooregister l'app per le notifiche, ma le registrazioni esistenti non può essere modificato in attesa e non possono essere inviate le notifiche.</span><span class="sxs-lookup"><span data-stu-id="16688-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="16688-136">chiave di accesso completo Hello viene utilizzata in un servizio back-end protetto per l'invio di notifiche e la modifica delle registrazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="16688-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="16688-137">Aggiungere il file MainPage.xaml.cs, hello successiva riga:</span><span class="sxs-lookup"><span data-stu-id="16688-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="16688-138">Nel file di progetto MainPage.xaml.cs hello, aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="16688-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    <span data-ttu-id="16688-139">Questo metodo crea un elenco di categorie e utilizza hello **notifiche** classe elenco hello toostore nella memoria locale hello e registrare i corrispondenti tag di hello con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="16688-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="16688-140">Quando vengono modificate le categorie, registrazione hello viene ricreata con le nuove categorie hello.</span><span class="sxs-lookup"><span data-stu-id="16688-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="16688-141">L'app è in grado di toostore un set di categorie in archiviazione locale nel dispositivo hello e registrare con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="16688-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="16688-142">Registrazione per le notifiche</span><span class="sxs-lookup"><span data-stu-id="16688-142">Register for notifications</span></span>
<span data-ttu-id="16688-143">Questi passaggi registrare con l'hub di notifica hello all'avvio mediante le categorie di hello che sono state archiviate nel servizio di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="16688-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="16688-144">Poiché il canale di hello URI assegnato dal servizio di notifica di Windows (WNS) hello può cambiare in qualsiasi momento, è consigliabile registrare per le notifiche di frequente errori di notifica tooavoid.</span><span class="sxs-lookup"><span data-stu-id="16688-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="16688-145">Questo esempio viene registrato per notifica ogni volta che viene avviata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="16688-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="16688-146">Per le app che vengono eseguite frequentemente, più di una volta al giorno, è possibile probabilmente ignorare la larghezza di banda di registrazione toopreserve se meno di un giorno è trascorso registrazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="16688-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="16688-147">Hello di file e aggiornamento App.xaml.cs hello aprire **InitNotificationsAsync** hello toouse metodo `notifications` classe toosubscribe in base alle categorie.</span><span class="sxs-lookup"><span data-stu-id="16688-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="16688-148">Ciò assicura che ogni volta che viene avviata l'applicazione hello Recupera categorie hello dall'archiviazione locale e richiede una registrazione per queste categorie.</span><span class="sxs-lookup"><span data-stu-id="16688-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="16688-149">Hello **InitNotificationsAsync** metodo è stato creato come parte di hello [iniziare con gli hub di notifica] [ get-started] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="16688-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="16688-150">Nel file di progetto MainPage.xaml.cs hello, aggiungere hello seguente codice toohello *OnNavigatedTo* metodo:</span><span class="sxs-lookup"><span data-stu-id="16688-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
        }
   
    <span data-ttu-id="16688-151">Questa pagina principale di hello gli aggiornamenti in base allo stato di hello di precedentemente salvato categorie.</span><span class="sxs-lookup"><span data-stu-id="16688-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="16688-152">app Hello è completo ed è possibile archiviare un set di categorie in hello dispositivo archiviazione locale utilizzato tooregister con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="16688-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="16688-153">Successivamente, verrà definito un back-end che può inviare categoria notifiche toothis app.</span><span class="sxs-lookup"><span data-stu-id="16688-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="16688-154">Invio di notifiche con tag</span><span class="sxs-lookup"><span data-stu-id="16688-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="16688-155">Eseguire app hello e generare le notifiche</span><span class="sxs-lookup"><span data-stu-id="16688-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="16688-156">In Visual Studio, premere F5 toocompile e avviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="16688-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="16688-157">Si noti che app hello di che dell'interfaccia utente fornisce un set attiva o disattiva che consente di scegliere toosubscribe categorie hello per.</span><span class="sxs-lookup"><span data-stu-id="16688-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="16688-158">Abilitare uno o più interruttori di categorie e quindi fare clic su **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="16688-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="16688-159">applicazione Hello converte le categorie selezionata hello in tag e richiede una nuova registrazione di dispositivi per i tag hello selezionato dall'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="16688-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="16688-160">Hello categorie registrate vengono restituite e visualizzate in una finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="16688-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="16688-161">Inviare una notifica dal back-end hello in uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="16688-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="16688-162">**Applicazione console:** avviare app console hello.</span><span class="sxs-lookup"><span data-stu-id="16688-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="16688-163">**Java/PHP** : eseguire l'app o lo script.</span><span class="sxs-lookup"><span data-stu-id="16688-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="16688-164">Le notifiche per le categorie di hello selezionato vengono visualizzati come le notifiche di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="16688-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="16688-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16688-165">Next steps</span></span>
<span data-ttu-id="16688-166">In questa esercitazione è stato appreso come toobroadcast le ultime notizie per categoria.</span><span class="sxs-lookup"><span data-stu-id="16688-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="16688-167">Provare a eseguire una delle seguenti esercitazioni che evidenziano altri scenari avanzati di hub di notifica hello:</span><span class="sxs-lookup"><span data-stu-id="16688-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="16688-168">[Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]</span><span class="sxs-lookup"><span data-stu-id="16688-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="16688-169">Informazioni su come hello tooexpand interrompere l'invio di notizie app tooenable localizzata notifiche.</span><span class="sxs-lookup"><span data-stu-id="16688-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
