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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Utilizzare gli hub di notifica toosend le ultime notizie
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Panoramica
In questo argomento illustra come toouse gli hub di notifica di Azure toobroadcast ultime notizie notifiche tooa Windows Phone 8.0/8.1 Silverlight app. Se la destinazione è Windows Store o app di Windows Phone 8.1, consultare tootoohello [universali di Windows](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) versione. Al termine, verrà essere in grado di tooregister per l'interruzione delle categorie di notizie, che si è interessati e ricevere notifiche di push solo per quelle categorie. Questo scenario è un modello comune per molte applicazioni in cui le notifiche hanno inviato toobe toogroups di utenti che hanno dichiarato in precedenza interesse in essi, ad esempio lettore RSS, le App per ventole musica e così via.

Scenari di trasmissione sono abilitati per includere uno o più *tag* durante la creazione di una registrazione nell'hub di notifica hello. Quando le notifiche vengono inviate tooa tag, tutti i dispositivi che sono registrati per il tag di hello riceverà la notifica hello. Poiché i tag sono semplicemente stringhe, essi non è toobe in precedenza. Per ulteriori informazioni sui tag, vedere troppo[Routing hub di notifica ed espressioni Tag](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Prerequisiti
In questo argomento è basato sull'app hello è stato creato in [iniziare con gli hub di notifica]. Prima di iniziare questa esercitazione, è necessario completare le procedure illustrate in [iniziare con gli hub di notifica].

## <a name="add-category-selection-toohello-app"></a>Aggiungi categoria selezione toohello app
Hello primo passaggio consiste tooadd hello UI elementi tooyour esistente pagina principale che consentono di hello utente tooselect categorie tooregister. categorie di Hello selezionate da un utente vengono archiviate nel dispositivo hello. Quando viene avviata l'applicazione hello, viene creata una registrazione del dispositivo nell'hub di notifica con categorie hello selezionata sotto forma di tag.

1. Aprire il file di progetto di hello MainPage. XAML, quindi sostituire hello **griglia** gli elementi denominati `TitlePanel` e `ContentPanel` con hello seguente codice:
   
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
2. Nel progetto hello, creare una nuova classe denominata **notifiche**, aggiungere hello **pubblica** toohello modificatore definizione di classe, quindi aggiungere il seguente hello **utilizzando** istruzioni toohello nuovo file di codice:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. Il codice seguente di hello di copia nel nuovo hello **notifiche** classe:
   
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

    Questa classe utilizza hello isolato archiviazione toostore hello categorie delle news che il dispositivo è tooreceive. Contiene anche metodi tooregister per queste categorie utilizzando un [modello](notification-hubs-templates-cross-platform-push-messages.md) registrazione della notifica.


1. Nel file di progetto App.xaml.cs hello, aggiungere hello seguente proprietà toohello **App** classe. Sostituire hello `<hub name>` e `<connection string with listen access>` segnaposto con la notifica hub hello nome e la stringa di connessione per *DefaultListenSharedAccessSignature* ottenuti in precedenza.
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > Poiché le credenziali che vengono distribuite con un'applicazione client non sono in genere sicure, deve essere distribuito solo chiave hello per l'accesso in ascolto con l'applicazione client. Abilita accesso che tooregister l'app per le notifiche, ma le registrazioni esistenti non può essere modificato in attesa e non possono essere inviate le notifiche. chiave di accesso completo Hello viene utilizzata in un servizio back-end protetto per l'invio di notifiche e la modifica delle registrazioni esistenti.
   > 
   > 
2. Aggiungere il file MainPage.xaml.cs, hello successiva riga:
   
        using Windows.UI.Popups;
3. Nel file di progetto MainPage.xaml.cs hello, aggiungere al metodo hello:
   
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
   
    Questo metodo crea un elenco di categorie e utilizza hello **notifiche** classe elenco hello toostore nella memoria locale hello e registrare i corrispondenti tag di hello con l'hub di notifica. Quando vengono modificate le categorie, registrazione hello viene ricreata con le nuove categorie hello.

L'app è in grado di toostore un set di categorie in archiviazione locale nel dispositivo hello e registrare con hub di notifica hello ogni volta che le modifiche dell'utente hello hello selezione di categorie.

## <a name="register-for-notifications"></a>Registrazione per le notifiche
Questi passaggi registrare con l'hub di notifica hello all'avvio mediante le categorie di hello che sono state archiviate nel servizio di archiviazione locale.

> [!NOTE]
> Poiché il canale di hello URI assegnato da hello Microsoft Push Notification Service (MPNS) è possibile modificare in qualsiasi momento, è consigliabile registrare per le notifiche di frequente errori di notifica tooavoid. Questo esempio viene registrato per le notifiche ogni volta che viene avviata l'applicazione hello. Per le app che vengono eseguite frequentemente, più di una volta al giorno, è possibile probabilmente ignorare la larghezza di banda di registrazione toopreserve se meno di un giorno è trascorso registrazione precedente hello.
> 
> 

1. Aprire il file App.xaml.cs hello e aggiungere hello **async** modificatore troppo**Application_Launching** (metodo) e sostituire codice di registrazione hello hub di notifica che è stato aggiunto in [iniziare con gli hub di notifica] con hello seguente codice:
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    Ciò assicura che ogni volta che viene avviata l'applicazione hello Recupera categorie hello dall'archiviazione locale e richiede una registrazione per queste categorie.
2. Nel file di progetto MainPage.xaml.cs hello, aggiungere hello seguente di codice che implementa hello **OnNavigatedTo** metodo:
   
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
   
    ![][2]
3. Dopo aver ricevuto un messaggio di conferma che le categorie sono state sottoscrizione completata, eseguire le notifiche tramite toosend app console hello per le categorie di ogni. Verificare che si riceve solo una notifica per le categorie di hello che sottoscritti.
   
    ![][3]

L'argomento è stato completato.

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

