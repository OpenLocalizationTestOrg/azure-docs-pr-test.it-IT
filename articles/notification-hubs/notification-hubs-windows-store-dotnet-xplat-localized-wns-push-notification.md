---
title: aaaNotification hub localizzata ultime notizie esercitazione
description: Informazioni su come toouse gli hub di notifica di Azure toosend localizzata notifiche sulle ultime notizie.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="fe697-103">Utilizzare gli hub di notifica toosend localizzata ultime notizie</span><span class="sxs-lookup"><span data-stu-id="fe697-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe697-104">Windows Store C#</span><span class="sxs-lookup"><span data-stu-id="fe697-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="fe697-105">iOS</span><span class="sxs-lookup"><span data-stu-id="fe697-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="fe697-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fe697-106">Overview</span></span>
<span data-ttu-id="fe697-107">In questo argomento illustra come hello toouse **modello** funzionalità di hub di notifica di Azure toobroadcast importanti notifiche di notizie che sono state localizzate per lingua e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fe697-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="fe697-108">In questa esercitazione si comincia con app di Windows Store hello creato in [toosend gli hub di notifica di utilizzare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="fe697-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="fe697-109">Al termine, che si sarà in grado di tooregister per le categorie che si è interessati, specificare una lingua in cui le notifiche hello tooreceive e ricevere notifiche di push solo per le categorie di hello selezionata in tale lingua.</span><span class="sxs-lookup"><span data-stu-id="fe697-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="fe697-110">Esistono due parti toothis scenario:</span><span class="sxs-lookup"><span data-stu-id="fe697-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="fe697-111">app di Windows Store Hello consente client dispositivi toospecify una lingua e toodifferent toosubscribe importanti categorie di notizie.</span><span class="sxs-lookup"><span data-stu-id="fe697-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="fe697-112">back-end Hello trasmette hello le notifiche, hello **tag** e **modello** funzionalità di Azure degli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="fe697-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe697-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fe697-113">Prerequisites</span></span>
<span data-ttu-id="fe697-114">È necessario aver già completato hello [toosend gli hub di notifica di utilizzare le ultime notizie] esercitazione e dispone di codice hello disponibile, poiché in questa esercitazione si basa direttamente su tale codice.</span><span class="sxs-lookup"><span data-stu-id="fe697-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="fe697-115">È inoltre necessario disporre di Visual Studio 2012 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="fe697-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="fe697-116">Concetti relativi ai modelli</span><span class="sxs-lookup"><span data-stu-id="fe697-116">Template concepts</span></span>
<span data-ttu-id="fe697-117">In [toosend gli hub di notifica di utilizzare le ultime notizie] è stata compilata un'applicazione che utilizzato **tag** toonotifications toosubscribe per le categorie di notizie diverso.</span><span class="sxs-lookup"><span data-stu-id="fe697-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="fe697-118">Molte app, tuttavia, sono destinate a più mercati ed è necessario localizzarle.</span><span class="sxs-lookup"><span data-stu-id="fe697-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="fe697-119">Ciò significa che contenuto hello di notifiche di hello stessi toobe localizzato e recapitato toohello correggere set di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="fe697-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="fe697-120">In questo argomento viene illustrato come hello toouse **modello** funzionalità degli hub di notifica tooeasily recapitare localizzata notifiche sulle ultime notizie.</span><span class="sxs-lookup"><span data-stu-id="fe697-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="fe697-121">Nota: un modo toosend localizzata notifiche è toocreate più versioni di ogni tag.</span><span class="sxs-lookup"><span data-stu-id="fe697-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="fe697-122">Ad esempio, toosupport in lingua inglese, francese e Mandarino, sarà necessaria e tre i tag diversi per notizie world: "world_en", "world_fr" e "world_ch".</span><span class="sxs-lookup"><span data-stu-id="fe697-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="fe697-123">È quindi necessario toosend una versione localizzata di hello world news tooeach dei tag.</span><span class="sxs-lookup"><span data-stu-id="fe697-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="fe697-124">In questo argomento vengono utilizzati modelli tooavoid hello aumentare del numero di tag e il requisito di hello di inviare più messaggi.</span><span class="sxs-lookup"><span data-stu-id="fe697-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="fe697-125">A un livello elevato, i modelli sono un modo toospecify come un dispositivo specifico deve ricevere una notifica.</span><span class="sxs-lookup"><span data-stu-id="fe697-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="fe697-126">modello Hello specifica il formato di payload esatta hello riferendosi tooproperties che fanno parte di messaggio hello inviato dal back-end di app.</span><span class="sxs-lookup"><span data-stu-id="fe697-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="fe697-127">In questo caso verrà inviato un messaggio indipendente dalle impostazioni locali, che contiene tutte le lingue supportate:</span><span class="sxs-lookup"><span data-stu-id="fe697-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="fe697-128">Quindi si garantisce che i dispositivi è registrato con un modello che fa riferimento la proprietà corretta toohello.</span><span class="sxs-lookup"><span data-stu-id="fe697-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="fe697-129">Ad esempio, un'applicazione Windows Store che desidera tooreceive un messaggio di avviso popup semplice verrà registrato per hello modello con i corrispondenti tag di seguito:</span><span class="sxs-lookup"><span data-stu-id="fe697-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="fe697-130">I modelli rappresentano uno strumento particolarmente efficace. Per altre informazioni, vedere l'articolo [Modelli](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="fe697-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="fe697-131">interfaccia utente di app Hello</span><span class="sxs-lookup"><span data-stu-id="fe697-131">hello app user interface</span></span>
<span data-ttu-id="fe697-132">Si modificherà ora hello delle ultime notizie app creata nell'argomento hello [toosend gli hub di notifica di utilizzare le ultime notizie] toosend localizzata aggiornate utilizzando i modelli.</span><span class="sxs-lookup"><span data-stu-id="fe697-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="fe697-133">Nell'app di Windows Store:</span><span class="sxs-lookup"><span data-stu-id="fe697-133">In your Windows Store app:</span></span>

<span data-ttu-id="fe697-134">Modificare il tooinclude MainPage. XAML, una casella combinata delle impostazioni locali:</span><span class="sxs-lookup"><span data-stu-id="fe697-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="fe697-135">Compilazione di app client di Windows Store hello</span><span class="sxs-lookup"><span data-stu-id="fe697-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="fe697-136">Nella classe notifiche, aggiungere un tooyour parametro delle impostazioni locali *StoreCategoriesAndSubscribe* e *SubscribeToCateories* metodi.</span><span class="sxs-lookup"><span data-stu-id="fe697-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="fe697-137">Si noti che, anziché chiamare hello *RegisterNativeAsync* metodo viene chiamato *RegisterTemplateAsync*: in questa fase registriamo un formato di notifica specifica in quale hello modello dipende dalle impostazioni locali di hello.</span><span class="sxs-lookup"><span data-stu-id="fe697-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="fe697-138">È inoltre fornire un nome per il modello di hello ("localizedWNSTemplateExample"), perché potrebbe essere opportuno tooregister più di un modello, ad esempio uno per le notifiche di tipo avviso popup e uno per i riquadri e dobbiamo tooname in ordine tooupdate in grado di toobe o eliminarli.</span><span class="sxs-lookup"><span data-stu-id="fe697-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="fe697-139">Si noti che se si registra un dispositivo più modelli con hello stesso tag, un messaggio in arrivo di destinazione che tag comporta più notifiche recapitati dispositivo toohello (uno per ogni modello).</span><span class="sxs-lookup"><span data-stu-id="fe697-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="fe697-140">Questo comportamento è utile quando hello stesso messaggio logico ha tooresult in più notifiche visive, ad esempio che illustra un badge sia un avviso popup in un'applicazione Windows Store.</span><span class="sxs-lookup"><span data-stu-id="fe697-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="fe697-141">Aggiungere hello delle impostazioni locali archiviate di hello tooretrieve metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="fe697-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="fe697-142">Nel file MainPage.xaml.cs, aggiornare il pulsante gestore click per il recupero hello valore corrente della casella combinata delle impostazioni locali di hello e fornendo classe notifiche toohello di toohello chiamata, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="fe697-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. <span data-ttu-id="fe697-143">Infine, assicurarsi che tooupdate nel file App.xaml.cs il `InitNotificationsAsync` tooretrieve metodo hello delle impostazioni locali e utilizzarlo per la sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="fe697-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="fe697-144">Inviare notifiche localizzate dal back-end</span><span class="sxs-lookup"><span data-stu-id="fe697-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[toosend gli hub di notifica di utilizzare le ultime notizie]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
