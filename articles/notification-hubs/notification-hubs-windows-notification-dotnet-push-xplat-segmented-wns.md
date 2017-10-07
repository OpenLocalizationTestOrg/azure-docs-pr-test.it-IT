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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Utilizzare gli hub di notifica toosend le ultime notizie
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Panoramica
In questo argomento illustra come toouse gli hub di notifica di Azure toobroadcast ultime notizie notifiche tooa Windows Store o app di Windows Phone 8.1 (non Silverlight). Se la destinazione è Windows Phone 8.1 Silverlight, vedere toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) versione. Al termine, verrà essere in grado di tooregister per l'interruzione delle categorie di notizie, che si è interessati e ricevere notifiche di push solo per quelle categorie. Questo scenario è un modello comune per molte applicazioni in cui le notifiche hanno inviato toobe toogroups di utenti che hanno dichiarato in precedenza interesse in essi, ad esempio lettore RSS, le App per fan e così via. 

Scenari di trasmissione sono abilitati per includere uno o più *tag* durante la creazione di una registrazione nell'hub di notifica hello. Quando le notifiche vengono inviate tooa tag, tutti i dispositivi che sono registrati per il tag di hello riceverà la notifica hello. Poiché i tag sono semplicemente stringhe, essi non è toobe in precedenza. Per ulteriori informazioni sui tag, vedere troppo[Routing hub di notifica ed espressioni Tag](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Progetti creati con Windows Store e Windows Phone 8.1 o versioni precedenti non sono supportati in Visual Studio 2017.  Per altre informazioni, vedere [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Prerequisiti
In questo argomento è basato sull'app hello è stato creato in [iniziare con gli hub di notifica][get-started]. Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [Introduzione ad Hub di notifica][get-started].

## <a name="add-category-selection-toohello-app"></a>Aggiungi categoria selezione toohello app
Hello primo passaggio consiste tooadd hello UI elementi tooyour esistente pagina principale che consentono di hello utente tooselect categorie tooregister. categorie di Hello selezionate da un utente vengono archiviate nel dispositivo hello. Quando viene avviata l'applicazione hello, viene creata una registrazione del dispositivo nell'hub di notifica con categorie hello selezionata sotto forma di tag.

1. Aprire il file di progetto di hello MainPage. XAML, quindi hello copia seguente di codice hello **griglia** elemento:
   
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
2. Fare clic con il pulsante destro hello **Shared** del progetto e aggiungere una nuova classe denominata **notifiche**, aggiungere hello **pubblica** toohello modificatore definizione di classe, quindi aggiungere hello seguente **utilizzando** istruzioni toohello nuovo file di codice:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. Il codice seguente di hello di copia nel nuovo hello **notifiche** classe:
   
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
   
    Questa classe utilizza hello archiviazione locale toostore hello le categorie di notizie, che in questo dispositivo è tooreceive. Si noti che, anziché chiamare hello *RegisterNativeAsync* metodo viene chiamato *RegisterTemplateAsync* tooregister per le categorie di hello mediante un modello di registrazione. 
   
    È inoltre fornire un nome per il modello di hello ("simpleWNSTemplateExample"), perché potrebbe essere opportuno tooregister più di un modello, ad esempio uno per le notifiche di tipo avviso popup e uno per i riquadri e dobbiamo tooname in ordine tooupdate in grado di toobe o eliminarli.
   
    Si noti che se si registra un dispositivo più modelli con hello stesso tag, un messaggio in arrivo di destinazione che tag comporta più notifiche recapitati dispositivo toohello (uno per ogni modello). Questo comportamento è utile quando hello stesso messaggio logico ha tooresult in più notifiche visive, ad esempio che illustra un badge sia un avviso popup in un'applicazione Windows Store.
   
    Per altre informazioni sui modelli, vedere [Modelli](notification-hubs-templates-cross-platform-push-messages.md).
4. Nel file di progetto App.xaml.cs hello, aggiungere hello seguente proprietà toohello **App** classe:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Questa proprietà è utilizzata toocreate e accesso un **notifiche** istanza.
   
    In hello di sopra di codice, sostituire hello `<hub name>` e `<connection string with listen access>` segnaposto con la notifica hub hello nome e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuti in precedenza.
   
   > [!NOTE]
   > Poiché le credenziali che vengono distribuite con un'applicazione client non sono in genere sicure, deve essere distribuito solo chiave hello per l'accesso in ascolto con l'applicazione client. Abilita accesso che tooregister l'app per le notifiche, ma le registrazioni esistenti non può essere modificato in attesa e non possono essere inviate le notifiche. chiave di accesso completo Hello viene utilizzata in un servizio back-end protetto per l'invio di notifiche e la modifica delle registrazioni esistenti.
   > 
   > 
5. Aggiungere il file MainPage.xaml.cs, hello successiva riga:
   
        using Windows.UI.Popups;
6. Nel file di progetto MainPage.xaml.cs hello, aggiungere al metodo hello:
   
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
   
    Questo metodo crea un elenco di categorie e utilizza hello **notifiche** classe elenco hello toostore nella memoria locale hello e registrare i corrispondenti tag di hello con l'hub di notifica. Quando vengono modificate le categorie, registrazione hello viene ricreata con le nuove categorie hello.

L'app è in grado di toostore un set di categorie in archiviazione locale nel dispositivo hello e registrare con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie.

## <a name="register-for-notifications"></a>Registrazione per le notifiche
Questi passaggi registrare con l'hub di notifica hello all'avvio mediante le categorie di hello che sono state archiviate nel servizio di archiviazione locale.

> [!NOTE]
> Poiché il canale di hello URI assegnato dal servizio di notifica di Windows (WNS) hello può cambiare in qualsiasi momento, è consigliabile registrare per le notifiche di frequente errori di notifica tooavoid. Questo esempio viene registrato per notifica ogni volta che viene avviata l'applicazione hello. Per le app che vengono eseguite frequentemente, più di una volta al giorno, è possibile probabilmente ignorare la larghezza di banda di registrazione toopreserve se meno di un giorno è trascorso registrazione precedente hello.
> 
> 

1. Hello di file e aggiornamento App.xaml.cs hello aprire **InitNotificationsAsync** hello toouse metodo `notifications` classe toosubscribe in base alle categorie.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Ciò assicura che ogni volta che viene avviata l'applicazione hello Recupera categorie hello dall'archiviazione locale e richiede una registrazione per queste categorie. Hello **InitNotificationsAsync** metodo è stato creato come parte di hello [iniziare con gli hub di notifica] [ get-started] esercitazione.
2. Nel file di progetto MainPage.xaml.cs hello, aggiungere hello seguente codice toohello *OnNavigatedTo* metodo:
   
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
   
    Questa pagina principale di hello gli aggiornamenti in base allo stato di hello di precedentemente salvato categorie.

app Hello è completo ed è possibile archiviare un set di categorie in hello dispositivo archiviazione locale utilizzato tooregister con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie. Successivamente, verrà definito un back-end che può inviare categoria notifiche toothis app.

## <a name="sending-tagged-notifications"></a>Invio di notifiche con tag
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Eseguire app hello e generare le notifiche
1. In Visual Studio, premere F5 toocompile e avviare l'applicazione hello.
   
    ![][1]
   
    Si noti che app hello di che dell'interfaccia utente fornisce un set attiva o disattiva che consente di scegliere toosubscribe categorie hello per.
2. Abilitare uno o più interruttori di categorie e quindi fare clic su **Subscribe**.
   
    applicazione Hello converte le categorie selezionata hello in tag e richiede una nuova registrazione di dispositivi per i tag hello selezionato dall'hub di notifica hello. Hello categorie registrate vengono restituite e visualizzate in una finestra di dialogo.
   
    ![][19]
3. Inviare una notifica dal back-end hello in uno dei seguenti modi hello:
   
   * **Applicazione console:** avviare app console hello.
   * **Java/PHP** : eseguire l'app o lo script.
     
     Le notifiche per le categorie di hello selezionato vengono visualizzati come le notifiche di tipo avviso popup.
     
     ![][14]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato appreso come toobroadcast le ultime notizie per categoria. Provare a eseguire una delle seguenti esercitazioni che evidenziano altri scenari avanzati di hub di notifica hello:

* [Utilizzare gli hub di notifica toobroadcast localizzata ultime notizie]
  
    Informazioni su come hello tooexpand interrompere l'invio di notizie app tooenable localizzata notifiche.

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
