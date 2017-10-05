---
title: Esercitazione sull'invio di ultime notizie localizzate mediante Hub di notifica
description: Informazioni su come usare Hub di notifica di Azure per inviare notifiche relative alle ultime notizie localizzate.
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
ms.openlocfilehash: e864e832b4c50644bf4062dee29d34ff9fe2774e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news"></a><span data-ttu-id="115cc-103">Utilizzo di Hub di notifica per inviare notizie localizzate</span><span class="sxs-lookup"><span data-stu-id="115cc-103">Use Notification Hubs to send localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="115cc-104">Windows Store C#</span><span class="sxs-lookup"><span data-stu-id="115cc-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="115cc-105">iOS</span><span class="sxs-lookup"><span data-stu-id="115cc-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="115cc-106">Overview</span><span class="sxs-lookup"><span data-stu-id="115cc-106">Overview</span></span>
<span data-ttu-id="115cc-107">In questo argomento viene illustrato come utilizzare la funzionalità relativa ai **modelli** di Hub di notifica di Azure per trasmettere notifiche relative alle ultime notizie localizzate in base alla lingua e al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="115cc-107">This topic shows you how to use the **template** feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="115cc-108">In questa esercitazione verrà utilizzata l'app di Windows Store creata in [Utilizzo di Hub di notifica per inviare le ultime notizie].</span><span class="sxs-lookup"><span data-stu-id="115cc-108">In this tutorial you start with the Windows Store app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="115cc-109">Al termine, sarà possibile effettuare la registrazione per le categorie di proprio interesse, specificare la lingua in cui ricevere le notifiche e ricevere solo notifiche push per le categorie selezionate nella lingua scelta.</span><span class="sxs-lookup"><span data-stu-id="115cc-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="115cc-110">Lo scenario è composto da due parti:</span><span class="sxs-lookup"><span data-stu-id="115cc-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="115cc-111">l'app di Windows Store consente ai dispositivi client di specificare una lingua e di sottoscrivere categorie diverse di ultime notizie;</span><span class="sxs-lookup"><span data-stu-id="115cc-111">the Windows Store app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="115cc-112">il back-end trasmette le notifiche usando le funzionalità relative ai **tag** e ai **modelli** di Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="115cc-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="115cc-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="115cc-113">Prerequisites</span></span>
<span data-ttu-id="115cc-114">È necessario aver completato l'esercitazione [Utilizzo di Hub di notifica per inviare le ultime notizie] e disporre del relativo codice, in quanto questa esercitazione è basata direttamente su tale codice.</span><span class="sxs-lookup"><span data-stu-id="115cc-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="115cc-115">È inoltre necessario disporre di Visual Studio 2012 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="115cc-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="115cc-116">Concetti relativi ai modelli</span><span class="sxs-lookup"><span data-stu-id="115cc-116">Template concepts</span></span>
<span data-ttu-id="115cc-117">In [Utilizzo di Hub di notifica per inviare le ultime notizie] è stata creata un'app che utilizza i **tag** per sottoscrivere le notifiche per diverse categorie di notizie.</span><span class="sxs-lookup"><span data-stu-id="115cc-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="115cc-118">Molte app, tuttavia, sono destinate a più mercati ed è necessario localizzarle.</span><span class="sxs-lookup"><span data-stu-id="115cc-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="115cc-119">Questo significa che il contenuto delle notifiche deve essere localizzato e inviato al set di dispositivi corretto.</span><span class="sxs-lookup"><span data-stu-id="115cc-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="115cc-120">In questo argomento verrà illustrato come usare la funzionalità relativa ai **modelli** di Hub di notifica per inviare facilmente notifiche relative alle ultime notizie localizzate.</span><span class="sxs-lookup"><span data-stu-id="115cc-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="115cc-121">Nota: un possibile modo per inviare notifiche localizzate consiste nel creare più versioni di ogni tag.</span><span class="sxs-lookup"><span data-stu-id="115cc-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="115cc-122">Per supportare l'inglese, il francese e il mandarino, ad esempio, sono necessari tre tag diversi per le ultime notizie internazionali: "world_en", "world_fr" e "world_ch".</span><span class="sxs-lookup"><span data-stu-id="115cc-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="115cc-123">È quindi necessario inviare una versione localizzata delle ultime notizie internazionali a ogni tag.</span><span class="sxs-lookup"><span data-stu-id="115cc-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="115cc-124">In questo argomento verranno utilizzati i modelli per evitare la proliferazione di tag e la necessità di inviare più messaggi.</span><span class="sxs-lookup"><span data-stu-id="115cc-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="115cc-125">In linea generale, i modelli consentono di specificare in che modo uno specifico dispositivo deve ricevere una notifica.</span><span class="sxs-lookup"><span data-stu-id="115cc-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="115cc-126">Il modello definisce lo specifico formato di payload da utilizzare, facendo riferimento alle proprietà del messaggio inviato dal back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="115cc-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="115cc-127">In questo caso verrà inviato un messaggio indipendente dalle impostazioni locali, che contiene tutte le lingue supportate:</span><span class="sxs-lookup"><span data-stu-id="115cc-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="115cc-128">Si procederà quindi a verificare che i dispositivi effettuino la registrazione con un modello che faccia riferimento alla proprietà corretta.</span><span class="sxs-lookup"><span data-stu-id="115cc-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="115cc-129">Ad esempio, un'app di Windows Store che desidera ricevere un semplice avviso popup effettuerà la registrazione per il modello seguente con eventuali tag corrispondenti:</span><span class="sxs-lookup"><span data-stu-id="115cc-129">For instance, a Windows Store app that wants to receive a simple toast message will register for the following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="115cc-130">I modelli rappresentano uno strumento particolarmente efficace. Per altre informazioni, vedere l'articolo relativo ai [Modelli](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="115cc-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="the-app-user-interface"></a><span data-ttu-id="115cc-131">Interfaccia utente dell'app</span><span class="sxs-lookup"><span data-stu-id="115cc-131">The app user interface</span></span>
<span data-ttu-id="115cc-132">L'app Breaking News creata nell'argomento [Utilizzo di Hub di notifica per inviare le ultime notizie] verrà ora modificata in modo da inviare notizie localizzate mediante modelli.</span><span class="sxs-lookup"><span data-stu-id="115cc-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="115cc-133">Nell'app di Windows Store:</span><span class="sxs-lookup"><span data-stu-id="115cc-133">In your Windows Store app:</span></span>

<span data-ttu-id="115cc-134">Modificare il file MainPage.xaml in modo da includere una casella combinata per le impostazioni locali:</span><span class="sxs-lookup"><span data-stu-id="115cc-134">Change your MainPage.xaml to include a locale combobox:</span></span>

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

## <a name="building-the-windows-store-client-app"></a><span data-ttu-id="115cc-135">Compilazione dell'app client di Windows Store</span><span class="sxs-lookup"><span data-stu-id="115cc-135">Building the Windows Store client app</span></span>
1. <span data-ttu-id="115cc-136">Nella classe Notifications aggiungere un parametro "locale" ai metodi *StoreCategoriesAndSubscribe* e *SubscribeToCategories*.</span><span class="sxs-lookup"><span data-stu-id="115cc-136">In your Notifications class, add a locale parameter to your  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
            // Using the localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="115cc-137">Tenere presente che anziché chiamare il metodo *RegisterNativeAsync* viene chiamato *RegisterTemplateAsync*: si registra un formato di notifica specifico, in cui il modello dipende dalle impostazioni locali.</span><span class="sxs-lookup"><span data-stu-id="115cc-137">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which the template depends on the locale.</span></span> <span data-ttu-id="115cc-138">Verrà inoltre fornito un nome per il modello ("localizedWNSTemplateExample") in quanto può essere necessario registrare più modelli, ad esempio uno per le notifiche di tipo avviso popup e uno per le notifiche di tipo riquadro. In questo caso, per avere la possibilità di aggiornare o eliminare i modelli è necessario assegnare loro un nome.</span><span class="sxs-lookup"><span data-stu-id="115cc-138">We also provide a name for the template ("localizedWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="115cc-139">Si noti che, se un dispositivo registra più modelli con lo stesso tag, un messaggio in arrivo destinato a tale tag ha come esito il recapito al dispositivo di più notifiche, una per ogni modello.</span><span class="sxs-lookup"><span data-stu-id="115cc-139">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="115cc-140">Questo comportamento risulta utile quando lo stesso messaggio logico deve avere produrre più notifiche visive, ad esempio visualizzare sia una notifica badge che una notifica di tipo avviso popup in un'app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="115cc-140">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="115cc-141">Aggiungere il metodo seguente per recuperare le impostazioni locali archiviate:</span><span class="sxs-lookup"><span data-stu-id="115cc-141">Add the following method to retrieve the stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="115cc-142">In MainPage.xaml.cs aggiornare il gestore degli eventi clic del pulsante recuperando il valore corrente della casella combinata Locale e fornendolo alla chiamata alla classe Notifications, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="115cc-142">In your MainPage.xaml.cs, update your button click handler by retrieving the current value of the Locale combo box and providing it to the call to the Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="115cc-143">Infine, nel file App.xaml.cs, assicurarsi di aggiornare il metodo `InitNotificationsAsync` per recuperare le impostazioni locali e utilizzarle per la sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="115cc-143">Finally, in your App.xaml.cs file, make sure to update your `InitNotificationsAsync` method to retrieve the locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="115cc-144">Inviare notifiche localizzate dal back-end</span><span class="sxs-lookup"><span data-stu-id="115cc-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[The app user interface]: #ui
[Building the Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
<span data-ttu-id="115cc-145">[Utilizzo di Hub di notifica per inviare le ultime notizie]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="115cc-145">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
