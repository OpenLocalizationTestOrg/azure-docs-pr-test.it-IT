---
title: notifiche push delimitati aaaGeo con gli hub di notifica di Azure e i dati spaziali Bing | Documenti Microsoft
description: "In questa esercitazione si apprenderà come notifiche con gli hub di notifica di Azure e i dati spaziali Bing di push toodeliver basati sulla posizione."
services: notification-hubs
documentationcenter: windows
keywords: notifica push, inviare notifiche push
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Notifiche push basate su recinto virtuale con Hub di notifica di Azure e dati spaziali di Bing
> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).
> 
> 

In questa esercitazione si apprenderà come notifiche con gli hub di notifica di Azure e i dati spaziali di Bing, sfruttate all'interno di un'applicazione UWP di push toodeliver basati sulla posizione.

## <a name="prerequisites"></a>Prerequisiti
In primo luogo, è necessario che siano tutti hello software e del servizio prerequisiti toomake:

* [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) o versione successiva (è accettabile anche [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)). 
* La versione più recente di hello [Azure SDK](https://azure.microsoft.com/downloads/). 
* [Account Bing Maps Dev Center](https://www.bingmapsportal.com/) (è possibile crearne uno gratuitamente e associarlo all'account Microsoft). 

## <a name="getting-started"></a>Introduzione
Iniziamo creando hello progetto. In Visual Studio avviare un nuovo progetto di tipo **App vuota (Windows universale)**.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Una volta completata la creazione del progetto hello, è necessario harness hello per hello app stessa. Ora per installare tutti gli elementi per l'infrastruttura recinto hello. Perché è in corso toouse che servizi Bing per questo oggetto, è un endpoint pubblico di API REST che consente di elaborare i frame tooquery percorso specifico:

    http://spatial.virtualearth.net/REST/v1/data/

Sarà necessario toospecify hello seguenti parametri tooget lo stesso risultato:

* **ID origine dati** e **Nome origine dati**: nell'API Bing Maps le origini dati contengono diversi metadati suddivisi in bucket, ad esempio posizioni e orario di ufficio dell'operazione. Altre informazioni sono disponibili qui. 
* **Nome dell'entità** : hello entità desiderata toouse come punto di riferimento per la notifica di hello. 
* **Chiave API di Bing mappe** – chiave hello ottenuti in precedenza durante la creazione di account di hello Bing Dev Center.

Si verrà approfondita nel programma di installazione di hello per ognuno degli elementi di hello precedenti.

## <a name="setting-up-hello-data-source"></a>Configurazione dell'origine dati hello
È possibile farlo in hello Bing Maps Dev Center. Fare clic sul **origini dati** in hello superiore barra di spostamento e selezionare **Gestisci origini dati**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Se non si è mai lavorato con API di Bing Maps prima, probabilmente vi sarà tutte le origini dati presenti, pertanto è possibile creare solo uno nuovo facendo clic sull'origine dati di caricamento dati tooa. Assicurarsi che compilare tutti i campi necessario hello:

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

È possibile chiedersi: che cos'è il file di dati hello e cosa dovrebbe si essere caricando? Ai fini di hello di questo test, è possibile utilizzare solo: esempio hello basato su pipe che delimita un'area di trasmissione è disponibile San Francisco hello:

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Hello precedente rappresenta questa entità:

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

È sufficiente copiare e incollare la stringa hello precedente in un nuovo file e salvarlo come **NotificationHubsGeofence.pipe**e caricarlo in hello Bing Dev Center.

> [!NOTE]
> Potrebbe essere richiesta toospecify una nuova chiave per hello **chiave Master** è diverso dal hello **chiave di Query**. È sufficiente creare una nuova chiave tramite hello dashboard e l'aggiornamento hello caricamento pagina di origine dati.
> 
> 

Dopo aver caricato il file di dati di hello, sarà necessario assicurarsi che si pubblica l'origine dati hello toomake. 

Andare troppo**Gestisci origini dati**, esattamente come abbiamo fatto in precedenza, trovare l'origine dati nell'elenco di hello e fare clic su **pubblica** in hello **azioni** colonna. In un bit, dovrebbe essere l'origine dati in hello **origini dei dati pubblicati** scheda:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

Se si fa clic **modifica**, si sarà in grado di toosee a colpo d'occhio le posizioni in cui è stata introdotta in essa contenuti:

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

A questo punto, il portale di hello non viene visualizzato hello limiti per geofence hello creati: è sufficiente è un messaggio di conferma che il percorso di hello specificato è nelle vicinanze destra hello.

A questo punto si dispone di tutti i requisiti per l'origine dati hello hello. Fare clic su Dettagli hello tooget hello URL di richiesta per una chiamata API hello, nel centro per sviluppatori di Bing mappe, hello **origini dati** e selezionare **informazioni sull'origine dati**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Hello **Query URL** è siamo dopo di essa. Si tratta hello endpoint sul quale è possibile eseguire query toocheck se hello periferica è attualmente all'interno dei limiti di hello di una posizione. tooperform questo controllo, è sufficiente tooexecute chiamata un'operazione GET hello URL della query, con i seguenti parametri aggiunti hello:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

In questo modo si specifica un punto di destinazione che si ottenga da dispositivo hello e Bing Maps eseguirà automaticamente hello calcoli toosee se si trova all'interno di geofence hello. Quando si esegue una richiesta di hello tramite un browser (o cURL), si otterrà standard una risposta JSON:

![](./media/notification-hubs-geofence/bing-maps-json.png)

Questa risposta avviene solo quando punto hello è effettivamente all'interno di hello designato limiti. In caso contrario, si otterrà un bucket **results** vuoto:

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Configurazione di un'applicazione UWP hello
Ora che è disponibile l'origine dati hello pronta, è possibile iniziare a utilizzare hello applicazione UWP che viene avviato automaticamente in precedenza.

Prima di tutto è necessario abilitare i servizi di posizione per l'applicazione. toodo, fai doppio clic sul `Package.appxmanifest` file **Esplora**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

Nella scheda Proprietà pacchetto hello che appena aperta, fare clic su **funzionalità** e assicurarsi di selezionare **percorso**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Come funzionalità di percorso hello è dichiarata, creare una nuova cartella nella soluzione denominata `Core`e aggiungere un nuovo file in essa contenute, chiamato `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Hello `LocationHelper` classe è abbastanza semplice a questo punto: non è consentono di percorso di utente tooobtain hello tramite API del sistema hello:

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

Per ulteriori informazioni su come ottenere la posizione dell'utente nelle App UWP ufficiale hello di hello [documento MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

toocheck che acquisizione percorso hello sia effettivamente in esecuzione, aprire hello codice sul lato della pagina principale (`MainPage.xaml.cs`). Creare un nuovo gestore eventi per hello `Loaded` evento in hello `MainPage` costruttore:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

implementazione di Hello del gestore eventi hello è come segue:

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Si noti che è dichiarato come gestore hello come asincrono perché `GetCurrentLocation` è awaitable e pertanto richiede toobe eseguita in un contesto asincrono. Inoltre, poiché in determinate circostanze è possibile finire con un percorso null (ad esempio servizi di posizione hello sono disabilitati o un'applicazione hello negata percorso tooaccess autorizzazioni), è necessario assicurarsi che sia gestito correttamente con un controllo null toomake.

Eseguire un'applicazione hello. Accertarsi di consentire l'accesso alla posizione:

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Una volta hello Avvia applicazione, dovrebbe essere in grado di toosee hello coordinate hello **Output** finestra:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Questo punto è chiaro che works acquisizione percorso – ritiene gestore dell'evento tooremove libero hello test caricato perché è non essere utilizzata da più.

passaggio successivo Hello è toocapture posizione cambia. A tale scopo, necessario tornare indietro toohello `LocationHelper` classe e aggiungere il gestore eventi hello per `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

implementazione di Hello verrà visualizzate solo le coordinate di posizione hello hello **Output** finestra:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Impostazione di back-end hello
Scaricare hello [esempio back-end .NET da GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). Una volta completato il download di hello, aprire hello `NotifyUsers` cartella e, successivamente: hello `NotifyUsers.sln` file.

Set hello `AppBackend` progetto come hello **progetto di avvio** e avviarlo.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Hello progetto è già configurato toosend push notifiche tootarget per i dispositivi, quindi sarà necessario toodo solo due cose: swapping di stringa di connessione corretta hello hub di notifica hello e aggiungere limite identificazione toosend hello notifica solo quando hello utente è all'interno di geofence hello.

stringa di connessione hello tooconfigure, in hello `Models` cartella aperta `Notifications.cs`. Hello `NotificationHubClient.CreateClientFromConnectionString` la funzione deve contenere informazioni hello sull'hub di notifica che è possibile ottenere in hello [portale Azure](https://portal.azure.com) (cercare all'interno di hello **criteri di accesso** pannello in  **Impostazioni**). Salvare il file di configurazione aggiornato hello.

A questo punto è necessario toocreate un modello per hello risultato API di Bing mappe. Hello toodo modo più semplice che è destro del mouse sul hello `Models` cartella **Aggiungi** > **classe**. Denominarlo `GeofenceBoundary.cs`. Al termine, copiare hello JSON dalla risposta hello API cui abbiamo discusso nella sezione prima di hello e in uso di Visual Studio **modifica** > **Incolla speciale** > **Incolla JSON come classi**. 

In questo modo per garantire l'oggetto hello verrà deserializzato esattamente nel modo previsto. Il set di classi risultante sarà analogo al seguente:

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

Aprire quindi `Controllers` > `NotificationsController.cs`. È necessario tootweak hello Post chiamata tooaccount di latitudine e longitudine destinazione hello. A tale scopo, aggiungere semplicemente due stringhe toohello la firma della funzione: `latitude` e `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Creare una nuova classe all'interno di hello progetto denominato `ApiHelper.cs` -verrà usato intersezioni di tooconnect tooBing toocheck punto limite. Implementare una funzione `IsPointWithinBounds` simile alla seguente:

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> Assicurarsi che endpoint hello API toosubstitute hello query URL ottenuti in precedenza da hello Bing Dev Center (vale chiave toohello API). 
> 
> 

Se sono presenti query toohello risultati, ciò significa che hello punto specificato è all'interno dei limiti di hello di hello geofence, in modo restituiamo `true`. Se non sono presenti risultati, Bing è rivelano che punto hello rientra hello ricerca frame, in modo restituiamo `false`.

In `NotificationsController.cs`, creare un controllo prima istruzione switch hello:

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

In questo modo, hello notifica viene inviata solo quando il punto di hello è all'interno dei limiti di hello.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Test di notifiche push in app UWP hello
Tornando app UWP toohello, si dovrebbe essere tootest in grado di notifiche. All'interno di hello `LocationHelper` di classi, creare una nuova funzione – `SendLocationToBackend`:

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> Scambia hello `POST_URL` toohello percorso dell'applicazione web distribuita creata nella sezione precedente hello. Per il momento, è OK toorun localmente, ma quando si lavora sulla distribuzione di una versione pubblica, sarà necessario toohost con un provider esterno.
> 
> 

Ora Verifichiamo che tu sia che si registra app UWP hello per le notifiche push. In Visual Studio, fare clic su **progetto** > **archiviare** > **Associa applicazione hello archivio**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Una volta effettuato l'accesso account sviluppatore tooyour, assicurarsi che si seleziona un'app esistente o crearne uno nuovo e associa il pacchetto di hello. 

Passare toohello Dev Center e app hello aprire appena creato. Fare clic su **Servizi** > **Notifiche push** > **Sito dei servizi Live**.

![](./media/notification-hubs-geofence/ms-live-services.png)

Nel sito di hello, prendere nota di hello **segreto dell'applicazione** hello e **SID pacchetto**. È necessario sia nel portale di Azure: hello aprire l'hub di notifica, fare clic su **impostazioni** > **Notification Services** > **Windows (WNS)**e immettere le informazioni di hello nei campi hello necessario.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

Fare clic su **Save**.

In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**. È necessario un riferimento di toohello tooadd **libreria gestita di Microsoft Azure Service Bus** : basta cercare `WindowsAzure.Messaging.Managed` e aggiungerlo tooyour progetto.

![](./media/notification-hubs-geofence/vs-nuget.png)

A scopo di test, è possibile creare hello `MainPage_Loaded` ancora una volta, gestore e aggiungere questo tooit frammento di codice:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Hello precedente registra app hello con hub di notifica hello. Si è pronto toogo! 

In `LocationHelper`, all'interno di hello `Geolocator_PositionChanged` gestore, è possibile aggiungere un frammento di codice di test che verrà inseriti in modo forzato percorso hello geofence hello:

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Poiché è hello reale coordinate (potrebbero non essere all'interno dei limiti di hello un determinato momento hello) non sono stati superati e utilizza i valori di test predefinite, si vedrà una notifica visualizzati nell'aggiornamento:

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>Passaggi successivi
Esistono un paio di passaggi che potrebbe essere necessario toofollow in toohello aggiunta in precedenza toomake assicurarsi che la soluzione hello sia in ambienti di produzione.

Prima di tutto, potrebbe essere necessario tooensure che geofences sono dinamici. Questo richiederà un lavoro aggiuntivo con hello API di Bing in ordine toobe tooupload in grado di nuovi limiti all'interno di origine dati esistente hello. Consultare hello [documentazione API dei servizi di dati spaziali Bing](https://msdn.microsoft.com/library/ff701734.aspx) per ulteriori informazioni sul soggetto hello.

In secondo luogo, come tooensure di lavoro che non viene eseguito recapito hello toohello destra partecipanti, potrebbe essere necessario tootarget loro tramite [tag](notification-hubs-tags-segment-push-message.md).

soluzione di Hello illustrato in precedenza descrive uno scenario in cui un'ampia gamma di piattaforme di destinazione, potrebbe essere in modo che non si limitare hello geofencing toosystem funzionalità. Ciò premesso, hello Universal Windows Platform offre funzionalità troppo[rilevare geofences destra out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Per altri dettagli relativi alle funzionalità di Hub di notifica, vedere il [portale di documentazione](https://azure.microsoft.com/documentation/services/notification-hubs/).

