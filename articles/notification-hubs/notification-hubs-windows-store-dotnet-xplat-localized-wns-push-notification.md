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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>Utilizzare gli hub di notifica toosend localizzata ultime notizie
> [!div class="op_single_selector"]
> * [Windows Store C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Panoramica
In questo argomento illustra come hello toouse **modello** funzionalità di hub di notifica di Azure toobroadcast importanti notifiche di notizie che sono state localizzate per lingua e dispositivo. In questa esercitazione si comincia con app di Windows Store hello creato in [toosend gli hub di notifica di utilizzare le ultime notizie]. Al termine, che si sarà in grado di tooregister per le categorie che si è interessati, specificare una lingua in cui le notifiche hello tooreceive e ricevere notifiche di push solo per le categorie di hello selezionata in tale lingua.

Esistono due parti toothis scenario:

* app di Windows Store Hello consente client dispositivi toospecify una lingua e toodifferent toosubscribe importanti categorie di notizie.
* back-end Hello trasmette hello le notifiche, hello **tag** e **modello** funzionalità di Azure degli hub di notifica.

## <a name="prerequisites"></a>Prerequisiti
È necessario aver già completato hello [toosend gli hub di notifica di utilizzare le ultime notizie] esercitazione e dispone di codice hello disponibile, poiché in questa esercitazione si basa direttamente su tale codice.

È inoltre necessario disporre di Visual Studio 2012 o versione successiva.

## <a name="template-concepts"></a>Concetti relativi ai modelli
In [toosend gli hub di notifica di utilizzare le ultime notizie] è stata compilata un'applicazione che utilizzato **tag** toonotifications toosubscribe per le categorie di notizie diverso.
Molte app, tuttavia, sono destinate a più mercati ed è necessario localizzarle. Ciò significa che contenuto hello di notifiche di hello stessi toobe localizzato e recapitato toohello correggere set di dispositivi.
In questo argomento viene illustrato come hello toouse **modello** funzionalità degli hub di notifica tooeasily recapitare localizzata notifiche sulle ultime notizie.

Nota: un modo toosend localizzata notifiche è toocreate più versioni di ogni tag. Ad esempio, toosupport in lingua inglese, francese e Mandarino, sarà necessaria e tre i tag diversi per notizie world: "world_en", "world_fr" e "world_ch". È quindi necessario toosend una versione localizzata di hello world news tooeach dei tag. In questo argomento vengono utilizzati modelli tooavoid hello aumentare del numero di tag e il requisito di hello di inviare più messaggi.

A un livello elevato, i modelli sono un modo toospecify come un dispositivo specifico deve ricevere una notifica. modello Hello specifica il formato di payload esatta hello riferendosi tooproperties che fanno parte di messaggio hello inviato dal back-end di app. In questo caso verrà inviato un messaggio indipendente dalle impostazioni locali, che contiene tutte le lingue supportate:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Quindi si garantisce che i dispositivi è registrato con un modello che fa riferimento la proprietà corretta toohello. Ad esempio, un'applicazione Windows Store che desidera tooreceive un messaggio di avviso popup semplice verrà registrato per hello modello con i corrispondenti tag di seguito:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



I modelli rappresentano uno strumento particolarmente efficace. Per altre informazioni, vedere l'articolo [Modelli](notification-hubs-templates-cross-platform-push-messages.md). 

## <a name="hello-app-user-interface"></a>interfaccia utente di app Hello
Si modificherà ora hello delle ultime notizie app creata nell'argomento hello [toosend gli hub di notifica di utilizzare le ultime notizie] toosend localizzata aggiornate utilizzando i modelli.

Nell'app di Windows Store:

Modificare il tooinclude MainPage. XAML, una casella combinata delle impostazioni locali:

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

## <a name="building-hello-windows-store-client-app"></a>Compilazione di app client di Windows Store hello
1. Nella classe notifiche, aggiungere un tooyour parametro delle impostazioni locali *StoreCategoriesAndSubscribe* e *SubscribeToCateories* metodi.
   
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
   
    Si noti che, anziché chiamare hello *RegisterNativeAsync* metodo viene chiamato *RegisterTemplateAsync*: in questa fase registriamo un formato di notifica specifica in quale hello modello dipende dalle impostazioni locali di hello. È inoltre fornire un nome per il modello di hello ("localizedWNSTemplateExample"), perché potrebbe essere opportuno tooregister più di un modello, ad esempio uno per le notifiche di tipo avviso popup e uno per i riquadri e dobbiamo tooname in ordine tooupdate in grado di toobe o eliminarli.
   
    Si noti che se si registra un dispositivo più modelli con hello stesso tag, un messaggio in arrivo di destinazione che tag comporta più notifiche recapitati dispositivo toohello (uno per ogni modello). Questo comportamento è utile quando hello stesso messaggio logico ha tooresult in più notifiche visive, ad esempio che illustra un badge sia un avviso popup in un'applicazione Windows Store.
2. Aggiungere hello delle impostazioni locali archiviate di hello tooretrieve metodo seguente:
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. Nel file MainPage.xaml.cs, aggiornare il pulsante gestore click per il recupero hello valore corrente della casella combinata delle impostazioni locali di hello e fornendo classe notifiche toohello di toohello chiamata, come illustrato:
   
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
4. Infine, assicurarsi che tooupdate nel file App.xaml.cs il `InitNotificationsAsync` tooretrieve metodo hello delle impostazioni locali e utilizzarlo per la sottoscrizione:
   
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

## <a name="send-localized-notifications-from-your-back-end"></a>Inviare notifiche localizzate dal back-end
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
