---
title: Usare Hub di notifica per inviare le ultime notizie (Windows Universal)
description: Usare Hub di notifica di Azure con i tag nella registrazione per inviare le ultime notizie a un'app Windows universale.
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
ms.openlocfilehash: 0e945b5626a08fcb428131f2abb465c2c141011a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="27acd-103">Uso di Hub di notifica per inviare le ultime notizie</span><span class="sxs-lookup"><span data-stu-id="27acd-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="27acd-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="27acd-104">Overview</span></span>
<span data-ttu-id="27acd-105">Questo argomento descrive come usare Hub di notifica di Azure per trasmettere le notifiche relative alle ultime notizie a un'app di Windows Store o Windows Phone 8.1 (non Silverlight).</span><span class="sxs-lookup"><span data-stu-id="27acd-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="27acd-106">Se si sviluppano app per Windows Phone 8.1 Silverlight, fare riferimento alla versione [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="27acd-106">If you are targeting Windows Phone 8.1 Silverlight, please refer to the [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="27acd-107">Al termine dell'esercitazione, si sarà appreso a effettuare la registrazione alle categorie di ultime notizie desiderate e ricevere le notifiche push solo da tali categorie.</span><span class="sxs-lookup"><span data-stu-id="27acd-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="27acd-108">Questo scenario è un modello comune per molte app che prevedono l'invio di notifiche a gruppi di utenti che hanno in precedenza manifestato il proprio interesse verso tali app, ad esempio lettori di feed RSS, app per fan di musica e così via.</span><span class="sxs-lookup"><span data-stu-id="27acd-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="27acd-109">È possibile abilitare gli scenari di trasmissione includendo uno o più *tag* durante la creazione di una registrazione nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="27acd-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="27acd-110">Quando le notifiche vengono inviate a un tag, tutti i dispositivi che hanno effettuato la registrazione al tag riceveranno la notifica.</span><span class="sxs-lookup"><span data-stu-id="27acd-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="27acd-111">Poiché i tag sono costituiti da stringhe, non è necessario eseguire il provisioning anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="27acd-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="27acd-112">Per ulteriori informazioni sui tag, vedere [Espressioni di routing e tag  per hub di notifica](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="27acd-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="27acd-113">Progetti creati con Windows Store e Windows Phone 8.1 o versioni precedenti non sono supportati in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="27acd-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="27acd-114">Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="27acd-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="27acd-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="27acd-115">Prerequisites</span></span>
<span data-ttu-id="27acd-116">Questo argomento si basa sull'app creata nell'esercitazione [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="27acd-116">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="27acd-117">Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="27acd-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="27acd-118">Aggiungere la selezione delle categorie all'app</span><span class="sxs-lookup"><span data-stu-id="27acd-118">Add category selection to the app</span></span>
<span data-ttu-id="27acd-119">Il primo passaggio prevede l'aggiunta degli elementi dell'interfaccia utente alla pagina principale esistente per consentire all'utente di selezionare le categorie per le quali registrarsi.</span><span class="sxs-lookup"><span data-stu-id="27acd-119">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="27acd-120">Le categorie selezionate da un utente sono archiviate nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27acd-120">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="27acd-121">All'avvio dell'app, viene creata una registrazione nell'hub di notifica con le categorie selezionate come tag.</span><span class="sxs-lookup"><span data-stu-id="27acd-121">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="27acd-122">Aprire il file di progetto MainPage.xaml, quindi copiare il codice seguente nell'elemento **Grid** :</span><span class="sxs-lookup"><span data-stu-id="27acd-122">Open the MainPage.xaml project file, then copy the following code in the **Grid** element:</span></span>
   
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
2. <span data-ttu-id="27acd-123">Fare clic con il pulsante destro del mouse sul progetto **Shared** e aggiungere una nuova classe denominata **Notifications**, aggiungere il modificatore **public** alla definizione della classe, quindi aggiungere le istruzioni **using** seguenti al nuovo file di codice:</span><span class="sxs-lookup"><span data-stu-id="27acd-123">Right click the **Shared** project and add a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="27acd-124">Copiare il codice seguente nella nuova classe **Notifications** :</span><span class="sxs-lookup"><span data-stu-id="27acd-124">Copy the following code into the new **Notifications** class:</span></span>
   
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
   
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="27acd-125">Questa classe utilizza l'archiviazione locale per archiviare le categorie di notizie che il dispositivo deve ricevere.</span><span class="sxs-lookup"><span data-stu-id="27acd-125">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="27acd-126">Anziché chiamare il metodo *RegisterNativeAsync*, chiamare *RegisterTemplateAsync* per la registrazione delle categorie usando una registrazione di modello.</span><span class="sxs-lookup"><span data-stu-id="27acd-126">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync* to register for the categories using a template registration.</span></span> 
   
    <span data-ttu-id="27acd-127">Verrà inoltre fornito un nome per il modello ("simpleWNSTemplateExample") in quanto può essere necessario registrare più modelli, ad esempio uno per le notifiche di tipo avviso popup e uno per le notifiche di tipo riquadro. In questo caso, per avere la possibilità di aggiornare o eliminare i modelli è necessario assegnare loro un nome.</span><span class="sxs-lookup"><span data-stu-id="27acd-127">We also provide a name for the template ("simpleWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="27acd-128">Si noti che, se un dispositivo registra più modelli con lo stesso tag, un messaggio in arrivo destinato a tale tag ha come esito il recapito al dispositivo di più notifiche, una per ogni modello.</span><span class="sxs-lookup"><span data-stu-id="27acd-128">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="27acd-129">Questo comportamento risulta utile quando lo stesso messaggio logico deve avere produrre più notifiche visive, ad esempio visualizzare sia una notifica badge che una notifica di tipo avviso popup in un'app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="27acd-129">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="27acd-130">Per altre informazioni sui modelli, vedere [Modelli](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="27acd-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="27acd-131">Nel file di progetto App.xaml.cs aggiungere la proprietà seguente alla classe **App** :</span><span class="sxs-lookup"><span data-stu-id="27acd-131">In the App.xaml.cs project file, add the following property to the **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="27acd-132">Questa proprietà viene utilizzata per creare un'istanza **Notifications** e accedervi.</span><span class="sxs-lookup"><span data-stu-id="27acd-132">This property is used to create and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="27acd-133">Nel codice precedente sostituire i segnaposto `<hub name>` e `<connection string with listen access>` con il nome dell'hub di notifica e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="27acd-133">In the above code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27acd-134">Poiché le credenziali che sono distribuite con un'app client in genere non sono sicure, distribuire solo la chiave per l'accesso Listen con l'app client.</span><span class="sxs-lookup"><span data-stu-id="27acd-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="27acd-135">L'accesso Listen consente all'app di registrarsi per le notifiche ma le registrazioni esistenti non possono essere modificate e le notifiche non possono essere inviate.</span><span class="sxs-lookup"><span data-stu-id="27acd-135">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="27acd-136">La chiave di accesso completo viene usata in un servizio back-end sicuro per l'invio delle notifiche e la modifica delle registrazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="27acd-136">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="27acd-137">In MainPage.xaml.cs aggiungere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="27acd-137">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="27acd-138">Aggiungere quindi il metodo seguente nel file di progetto MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="27acd-138">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="27acd-139">Questo metodo crea un elenco di categorie e utilizza la classe **Notifications** per archiviare l'elenco nell'archiviazione locale e registrare i tag corrispondenti nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="27acd-139">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="27acd-140">Se le categorie vengono modificate, la registrazione viene ricreata con le nuove categorie.</span><span class="sxs-lookup"><span data-stu-id="27acd-140">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="27acd-141">L'app può quindi archiviare un set di categorie nell'archiviazione locale del dispositivo ed effettuare la registrazione con l'hub di notifica ogni volta che l'utente modifica la selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="27acd-141">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="27acd-142">Registrazione per le notifiche</span><span class="sxs-lookup"><span data-stu-id="27acd-142">Register for notifications</span></span>
<span data-ttu-id="27acd-143">Questa procedura consente di effettuare la registrazione con l'hub di notifica all'avvio usando le categorie archiviate nella risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="27acd-143">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="27acd-144">Poiché l'URI di canale assegnato dal servizio di notifica Windows può cambiare in qualsiasi momento, è necessario ripetere di frequente la registrazione per le notifiche per evitare errori di notifica.</span><span class="sxs-lookup"><span data-stu-id="27acd-144">Because the channel URI assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="27acd-145">In questo esempio viene effettuata la registrazione per le notifiche a ogni avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="27acd-145">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="27acd-146">Per le app che vengono eseguite di frequente, oltre una volta al giorno, è possibile ignorare la registrazione per conservare la larghezza di banda qualora sia trascorso meno di un giorno dalla registrazione precedente.</span><span class="sxs-lookup"><span data-stu-id="27acd-146">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="27acd-147">Aprire il file App.xaml.cs e aggiornare il metodo **InitNotificationsAsync** per usare la classe `notifications` per la sottoscrizione in base alle categorie.</span><span class="sxs-lookup"><span data-stu-id="27acd-147">Open the App.xaml.cs file and update the **InitNotificationsAsync** method to use the `notifications` class to subscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="27acd-148">In questo modo, ogni volta che l'app viene avviata vengono recuperate le categorie dall'archiviazione locale e viene richiesta una registrazione per queste categorie.</span><span class="sxs-lookup"><span data-stu-id="27acd-148">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="27acd-149">Il metodo **InitNotificationsAsync** è stato creato nell'ambito dell'esercitazione [Introduzione ad Hub di notifica][get-started].</span><span class="sxs-lookup"><span data-stu-id="27acd-149">The **InitNotificationsAsync** method was created as part of the [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="27acd-150">Nel file di progetto MainPage.xaml.cs aggiungere il codice seguente nel metodo *OnNavigatedTo* :</span><span class="sxs-lookup"><span data-stu-id="27acd-150">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="27acd-151">La pagina principale viene aggiornata in base allo stato delle categorie salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="27acd-151">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="27acd-152">Ora l'app è completa e può quindi archiviare un set di categorie nell'archiviazione locale del dispositivo ed effettuare la registrazione con l'hub di notifica ogni volta che l'utente modifica la selezione di categorie.</span><span class="sxs-lookup"><span data-stu-id="27acd-152">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="27acd-153">Verrà ora definito un back-end per l'invio delle notifiche delle categorie all'app.</span><span class="sxs-lookup"><span data-stu-id="27acd-153">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="27acd-154">Invio di notifiche con tag</span><span class="sxs-lookup"><span data-stu-id="27acd-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="27acd-155">Eseguire l'app e generare notifiche</span><span class="sxs-lookup"><span data-stu-id="27acd-155">Run the app and generate notifications</span></span>
1. <span data-ttu-id="27acd-156">In Visual Studio premere F5 per compilare e avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="27acd-156">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="27acd-157">Si noti che l'interfaccia utente dell'app fornisce un set di interruttori che consentono di scegliere le categorie per le quali effettuare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="27acd-157">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="27acd-158">Abilitare uno o più interruttori di categorie e quindi fare clic su **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="27acd-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="27acd-159">L'app converte le categorie selezionate in tag e richiede una nuova registrazione del dispositivo per i tag selezionati dall'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="27acd-159">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="27acd-160">Le categorie registrate vengono restituite e visualizzate in una finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="27acd-160">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="27acd-161">Inviare una nuova notifica dal back-end in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="27acd-161">Send a new notification from the backend in one of the following ways:</span></span>
   
   * <span data-ttu-id="27acd-162">**App console:** avviare l'app console.</span><span class="sxs-lookup"><span data-stu-id="27acd-162">**Console app:** start the console app.</span></span>
   * <span data-ttu-id="27acd-163">**Java/PHP** : eseguire l'app o lo script.</span><span class="sxs-lookup"><span data-stu-id="27acd-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="27acd-164">Le notifiche per le categorie selezionate vengono visualizzate come notifiche di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="27acd-164">Notifications for the selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="27acd-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27acd-165">Next steps</span></span>
<span data-ttu-id="27acd-166">In questa esercitazione si è appreso a trasmettere le ultime novità per categoria.</span><span class="sxs-lookup"><span data-stu-id="27acd-166">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="27acd-167">Per informazioni su altri scenari avanzati di Hub di notifica, provare a completare le seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="27acd-167">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="27acd-168">[Usare Hub di notifica per la trasmissione di notizie localizzate]</span><span class="sxs-lookup"><span data-stu-id="27acd-168">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="27acd-169">Informazioni su come espandere l'app relativa alle ultime novità per abilitare l'invio di notifiche localizzate.</span><span class="sxs-lookup"><span data-stu-id="27acd-169">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
<span data-ttu-id="27acd-170">[Usare Hub di notifica per la trasmissione di notizie localizzate]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="27acd-170">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
