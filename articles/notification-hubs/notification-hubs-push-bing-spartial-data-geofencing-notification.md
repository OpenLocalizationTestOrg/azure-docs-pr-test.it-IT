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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="f4131-104">Notifiche push basate su recinto virtuale con Hub di notifica di Azure e dati spaziali di Bing</span><span class="sxs-lookup"><span data-stu-id="f4131-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="f4131-105">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="f4131-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f4131-106">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="f4131-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f4131-107">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="f4131-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="f4131-108">In questa esercitazione si apprenderà come notifiche con gli hub di notifica di Azure e i dati spaziali di Bing, sfruttate all'interno di un'applicazione UWP di push toodeliver basati sulla posizione.</span><span class="sxs-lookup"><span data-stu-id="f4131-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4131-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f4131-109">Prerequisites</span></span>
<span data-ttu-id="f4131-110">In primo luogo, è necessario che siano tutti hello software e del servizio prerequisiti toomake:</span><span class="sxs-lookup"><span data-stu-id="f4131-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="f4131-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) o versione successiva (è accettabile anche [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)).</span><span class="sxs-lookup"><span data-stu-id="f4131-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="f4131-112">La versione più recente di hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f4131-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="f4131-113">[Account Bing Maps Dev Center](https://www.bingmapsportal.com/) (è possibile crearne uno gratuitamente e associarlo all'account Microsoft).</span><span class="sxs-lookup"><span data-stu-id="f4131-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="f4131-114">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f4131-114">Getting Started</span></span>
<span data-ttu-id="f4131-115">Iniziamo creando hello progetto.</span><span class="sxs-lookup"><span data-stu-id="f4131-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="f4131-116">In Visual Studio avviare un nuovo progetto di tipo **App vuota (Windows universale)**.</span><span class="sxs-lookup"><span data-stu-id="f4131-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="f4131-117">Una volta completata la creazione del progetto hello, è necessario harness hello per hello app stessa.</span><span class="sxs-lookup"><span data-stu-id="f4131-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="f4131-118">Ora per installare tutti gli elementi per l'infrastruttura recinto hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="f4131-119">Perché è in corso toouse che servizi Bing per questo oggetto, è un endpoint pubblico di API REST che consente di elaborare i frame tooquery percorso specifico:</span><span class="sxs-lookup"><span data-stu-id="f4131-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="f4131-120">Sarà necessario toospecify hello seguenti parametri tooget lo stesso risultato:</span><span class="sxs-lookup"><span data-stu-id="f4131-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="f4131-121">**ID origine dati** e **Nome origine dati**: nell'API Bing Maps le origini dati contengono diversi metadati suddivisi in bucket, ad esempio posizioni e orario di ufficio dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="f4131-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="f4131-122">Altre informazioni sono disponibili qui.</span><span class="sxs-lookup"><span data-stu-id="f4131-122">You can read more about those here.</span></span> 
* <span data-ttu-id="f4131-123">**Nome dell'entità** : hello entità desiderata toouse come punto di riferimento per la notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="f4131-124">**Chiave API di Bing mappe** – chiave hello ottenuti in precedenza durante la creazione di account di hello Bing Dev Center.</span><span class="sxs-lookup"><span data-stu-id="f4131-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="f4131-125">Si verrà approfondita nel programma di installazione di hello per ognuno degli elementi di hello precedenti.</span><span class="sxs-lookup"><span data-stu-id="f4131-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="f4131-126">Configurazione dell'origine dati hello</span><span class="sxs-lookup"><span data-stu-id="f4131-126">Setting up hello data source</span></span>
<span data-ttu-id="f4131-127">È possibile farlo in hello Bing Maps Dev Center.</span><span class="sxs-lookup"><span data-stu-id="f4131-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="f4131-128">Fare clic sul **origini dati** in hello superiore barra di spostamento e selezionare **Gestisci origini dati**.</span><span class="sxs-lookup"><span data-stu-id="f4131-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="f4131-129">Se non si è mai lavorato con API di Bing Maps prima, probabilmente vi sarà tutte le origini dati presenti, pertanto è possibile creare solo uno nuovo facendo clic sull'origine dati di caricamento dati tooa.</span><span class="sxs-lookup"><span data-stu-id="f4131-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="f4131-130">Assicurarsi che compilare tutti i campi necessario hello:</span><span class="sxs-lookup"><span data-stu-id="f4131-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="f4131-131">È possibile chiedersi: che cos'è il file di dati hello e cosa dovrebbe si essere caricando?</span><span class="sxs-lookup"><span data-stu-id="f4131-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="f4131-132">Ai fini di hello di questo test, è possibile utilizzare solo: esempio hello basato su pipe che delimita un'area di trasmissione è disponibile San Francisco hello:</span><span class="sxs-lookup"><span data-stu-id="f4131-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="f4131-133">Hello precedente rappresenta questa entità:</span><span class="sxs-lookup"><span data-stu-id="f4131-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="f4131-134">È sufficiente copiare e incollare la stringa hello precedente in un nuovo file e salvarlo come **NotificationHubsGeofence.pipe**e caricarlo in hello Bing Dev Center.</span><span class="sxs-lookup"><span data-stu-id="f4131-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="f4131-135">Potrebbe essere richiesta toospecify una nuova chiave per hello **chiave Master** è diverso dal hello **chiave di Query**.</span><span class="sxs-lookup"><span data-stu-id="f4131-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="f4131-136">È sufficiente creare una nuova chiave tramite hello dashboard e l'aggiornamento hello caricamento pagina di origine dati.</span><span class="sxs-lookup"><span data-stu-id="f4131-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="f4131-137">Dopo aver caricato il file di dati di hello, sarà necessario assicurarsi che si pubblica l'origine dati hello toomake.</span><span class="sxs-lookup"><span data-stu-id="f4131-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="f4131-138">Andare troppo**Gestisci origini dati**, esattamente come abbiamo fatto in precedenza, trovare l'origine dati nell'elenco di hello e fare clic su **pubblica** in hello **azioni** colonna.</span><span class="sxs-lookup"><span data-stu-id="f4131-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="f4131-139">In un bit, dovrebbe essere l'origine dati in hello **origini dei dati pubblicati** scheda:</span><span class="sxs-lookup"><span data-stu-id="f4131-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="f4131-140">Se si fa clic **modifica**, si sarà in grado di toosee a colpo d'occhio le posizioni in cui è stata introdotta in essa contenuti:</span><span class="sxs-lookup"><span data-stu-id="f4131-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="f4131-141">A questo punto, il portale di hello non viene visualizzato hello limiti per geofence hello creati: è sufficiente è un messaggio di conferma che il percorso di hello specificato è nelle vicinanze destra hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="f4131-142">A questo punto si dispone di tutti i requisiti per l'origine dati hello hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="f4131-143">Fare clic su Dettagli hello tooget hello URL di richiesta per una chiamata API hello, nel centro per sviluppatori di Bing mappe, hello **origini dati** e selezionare **informazioni sull'origine dati**.</span><span class="sxs-lookup"><span data-stu-id="f4131-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="f4131-144">Hello **Query URL** è siamo dopo di essa.</span><span class="sxs-lookup"><span data-stu-id="f4131-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="f4131-145">Si tratta hello endpoint sul quale è possibile eseguire query toocheck se hello periferica è attualmente all'interno dei limiti di hello di una posizione.</span><span class="sxs-lookup"><span data-stu-id="f4131-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="f4131-146">tooperform questo controllo, è sufficiente tooexecute chiamata un'operazione GET hello URL della query, con i seguenti parametri aggiunti hello:</span><span class="sxs-lookup"><span data-stu-id="f4131-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="f4131-147">In questo modo si specifica un punto di destinazione che si ottenga da dispositivo hello e Bing Maps eseguirà automaticamente hello calcoli toosee se si trova all'interno di geofence hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="f4131-148">Quando si esegue una richiesta di hello tramite un browser (o cURL), si otterrà standard una risposta JSON:</span><span class="sxs-lookup"><span data-stu-id="f4131-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="f4131-149">Questa risposta avviene solo quando punto hello è effettivamente all'interno di hello designato limiti.</span><span class="sxs-lookup"><span data-stu-id="f4131-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="f4131-150">In caso contrario, si otterrà un bucket **results** vuoto:</span><span class="sxs-lookup"><span data-stu-id="f4131-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="f4131-151">Configurazione di un'applicazione UWP hello</span><span class="sxs-lookup"><span data-stu-id="f4131-151">Setting up hello UWP application</span></span>
<span data-ttu-id="f4131-152">Ora che è disponibile l'origine dati hello pronta, è possibile iniziare a utilizzare hello applicazione UWP che viene avviato automaticamente in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f4131-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="f4131-153">Prima di tutto è necessario abilitare i servizi di posizione per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4131-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="f4131-154">toodo, fai doppio clic sul `Package.appxmanifest` file **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="f4131-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="f4131-155">Nella scheda Proprietà pacchetto hello che appena aperta, fare clic su **funzionalità** e assicurarsi di selezionare **percorso**:</span><span class="sxs-lookup"><span data-stu-id="f4131-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="f4131-156">Come funzionalità di percorso hello è dichiarata, creare una nuova cartella nella soluzione denominata `Core`e aggiungere un nuovo file in essa contenute, chiamato `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="f4131-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="f4131-157">Hello `LocationHelper` classe è abbastanza semplice a questo punto: non è consentono di percorso di utente tooobtain hello tramite API del sistema hello:</span><span class="sxs-lookup"><span data-stu-id="f4131-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

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

<span data-ttu-id="f4131-158">Per ulteriori informazioni su come ottenere la posizione dell'utente nelle App UWP ufficiale hello di hello [documento MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4131-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="f4131-159">toocheck che acquisizione percorso hello sia effettivamente in esecuzione, aprire hello codice sul lato della pagina principale (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="f4131-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="f4131-160">Creare un nuovo gestore eventi per hello `Loaded` evento in hello `MainPage` costruttore:</span><span class="sxs-lookup"><span data-stu-id="f4131-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="f4131-161">implementazione di Hello del gestore eventi hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="f4131-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="f4131-162">Si noti che è dichiarato come gestore hello come asincrono perché `GetCurrentLocation` è awaitable e pertanto richiede toobe eseguita in un contesto asincrono.</span><span class="sxs-lookup"><span data-stu-id="f4131-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="f4131-163">Inoltre, poiché in determinate circostanze è possibile finire con un percorso null (ad esempio servizi di posizione hello sono disabilitati o un'applicazione hello negata percorso tooaccess autorizzazioni), è necessario assicurarsi che sia gestito correttamente con un controllo null toomake.</span><span class="sxs-lookup"><span data-stu-id="f4131-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="f4131-164">Eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-164">Run hello application.</span></span> <span data-ttu-id="f4131-165">Accertarsi di consentire l'accesso alla posizione:</span><span class="sxs-lookup"><span data-stu-id="f4131-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="f4131-166">Una volta hello Avvia applicazione, dovrebbe essere in grado di toosee hello coordinate hello **Output** finestra:</span><span class="sxs-lookup"><span data-stu-id="f4131-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="f4131-167">Questo punto è chiaro che works acquisizione percorso – ritiene gestore dell'evento tooremove libero hello test caricato perché è non essere utilizzata da più.</span><span class="sxs-lookup"><span data-stu-id="f4131-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="f4131-168">passaggio successivo Hello è toocapture posizione cambia.</span><span class="sxs-lookup"><span data-stu-id="f4131-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="f4131-169">A tale scopo, necessario tornare indietro toohello `LocationHelper` classe e aggiungere il gestore eventi hello per `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="f4131-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="f4131-170">implementazione di Hello verrà visualizzate solo le coordinate di posizione hello hello **Output** finestra:</span><span class="sxs-lookup"><span data-stu-id="f4131-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="f4131-171">Impostazione di back-end hello</span><span class="sxs-lookup"><span data-stu-id="f4131-171">Setting up hello backend</span></span>
<span data-ttu-id="f4131-172">Scaricare hello [esempio back-end .NET da GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="f4131-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="f4131-173">Una volta completato il download di hello, aprire hello `NotifyUsers` cartella e, successivamente: hello `NotifyUsers.sln` file.</span><span class="sxs-lookup"><span data-stu-id="f4131-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="f4131-174">Set hello `AppBackend` progetto come hello **progetto di avvio** e avviarlo.</span><span class="sxs-lookup"><span data-stu-id="f4131-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="f4131-175">Hello progetto è già configurato toosend push notifiche tootarget per i dispositivi, quindi sarà necessario toodo solo due cose: swapping di stringa di connessione corretta hello hub di notifica hello e aggiungere limite identificazione toosend hello notifica solo quando hello utente è all'interno di geofence hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="f4131-176">stringa di connessione hello tooconfigure, in hello `Models` cartella aperta `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="f4131-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="f4131-177">Hello `NotificationHubClient.CreateClientFromConnectionString` la funzione deve contenere informazioni hello sull'hub di notifica che è possibile ottenere in hello [portale Azure](https://portal.azure.com) (cercare all'interno di hello **criteri di accesso** pannello in  **Impostazioni**).</span><span class="sxs-lookup"><span data-stu-id="f4131-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="f4131-178">Salvare il file di configurazione aggiornato hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="f4131-179">A questo punto è necessario toocreate un modello per hello risultato API di Bing mappe.</span><span class="sxs-lookup"><span data-stu-id="f4131-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="f4131-180">Hello toodo modo più semplice che è destro del mouse sul hello `Models` cartella **Aggiungi** > **classe**.</span><span class="sxs-lookup"><span data-stu-id="f4131-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="f4131-181">Denominarlo `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="f4131-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="f4131-182">Al termine, copiare hello JSON dalla risposta hello API cui abbiamo discusso nella sezione prima di hello e in uso di Visual Studio **modifica** > **Incolla speciale** > **Incolla JSON come classi**.</span><span class="sxs-lookup"><span data-stu-id="f4131-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="f4131-183">In questo modo per garantire l'oggetto hello verrà deserializzato esattamente nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="f4131-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="f4131-184">Il set di classi risultante sarà analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="f4131-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="f4131-185">Aprire quindi `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="f4131-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="f4131-186">È necessario tootweak hello Post chiamata tooaccount di latitudine e longitudine destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="f4131-187">A tale scopo, aggiungere semplicemente due stringhe toohello la firma della funzione: `latitude` e `longitude`.</span><span class="sxs-lookup"><span data-stu-id="f4131-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="f4131-188">Creare una nuova classe all'interno di hello progetto denominato `ApiHelper.cs` -verrà usato intersezioni di tooconnect tooBing toocheck punto limite.</span><span class="sxs-lookup"><span data-stu-id="f4131-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="f4131-189">Implementare una funzione `IsPointWithinBounds` simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="f4131-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="f4131-190">Assicurarsi che endpoint hello API toosubstitute hello query URL ottenuti in precedenza da hello Bing Dev Center (vale chiave toohello API).</span><span class="sxs-lookup"><span data-stu-id="f4131-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="f4131-191">Se sono presenti query toohello risultati, ciò significa che hello punto specificato è all'interno dei limiti di hello di hello geofence, in modo restituiamo `true`.</span><span class="sxs-lookup"><span data-stu-id="f4131-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="f4131-192">Se non sono presenti risultati, Bing è rivelano che punto hello rientra hello ricerca frame, in modo restituiamo `false`.</span><span class="sxs-lookup"><span data-stu-id="f4131-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="f4131-193">In `NotificationsController.cs`, creare un controllo prima istruzione switch hello:</span><span class="sxs-lookup"><span data-stu-id="f4131-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

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

<span data-ttu-id="f4131-194">In questo modo, hello notifica viene inviata solo quando il punto di hello è all'interno dei limiti di hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="f4131-195">Test di notifiche push in app UWP hello</span><span class="sxs-lookup"><span data-stu-id="f4131-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="f4131-196">Tornando app UWP toohello, si dovrebbe essere tootest in grado di notifiche.</span><span class="sxs-lookup"><span data-stu-id="f4131-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="f4131-197">All'interno di hello `LocationHelper` di classi, creare una nuova funzione – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="f4131-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="f4131-198">Scambia hello `POST_URL` toohello percorso dell'applicazione web distribuita creata nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="f4131-199">Per il momento, è OK toorun localmente, ma quando si lavora sulla distribuzione di una versione pubblica, sarà necessario toohost con un provider esterno.</span><span class="sxs-lookup"><span data-stu-id="f4131-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="f4131-200">Ora Verifichiamo che tu sia che si registra app UWP hello per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="f4131-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="f4131-201">In Visual Studio, fare clic su **progetto** > **archiviare** > **Associa applicazione hello archivio**.</span><span class="sxs-lookup"><span data-stu-id="f4131-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="f4131-202">Una volta effettuato l'accesso account sviluppatore tooyour, assicurarsi che si seleziona un'app esistente o crearne uno nuovo e associa il pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="f4131-203">Passare toohello Dev Center e app hello aprire appena creato.</span><span class="sxs-lookup"><span data-stu-id="f4131-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="f4131-204">Fare clic su **Servizi** > **Notifiche push** > **Sito dei servizi Live**.</span><span class="sxs-lookup"><span data-stu-id="f4131-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="f4131-205">Nel sito di hello, prendere nota di hello **segreto dell'applicazione** hello e **SID pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="f4131-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="f4131-206">È necessario sia nel portale di Azure: hello aprire l'hub di notifica, fare clic su **impostazioni** > **Notification Services** > **Windows (WNS)**e immettere le informazioni di hello nei campi hello necessario.</span><span class="sxs-lookup"><span data-stu-id="f4131-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="f4131-207">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4131-207">Click on **Save**.</span></span>

<span data-ttu-id="f4131-208">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f4131-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="f4131-209">È necessario un riferimento di toohello tooadd **libreria gestita di Microsoft Azure Service Bus** : basta cercare `WindowsAzure.Messaging.Managed` e aggiungerlo tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="f4131-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="f4131-210">A scopo di test, è possibile creare hello `MainPage_Loaded` ancora una volta, gestore e aggiungere questo tooit frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="f4131-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="f4131-211">Hello precedente registra app hello con hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="f4131-212">Si è pronto toogo!</span><span class="sxs-lookup"><span data-stu-id="f4131-212">You are ready toogo!</span></span> 

<span data-ttu-id="f4131-213">In `LocationHelper`, all'interno di hello `Geolocator_PositionChanged` gestore, è possibile aggiungere un frammento di codice di test che verrà inseriti in modo forzato percorso hello geofence hello:</span><span class="sxs-lookup"><span data-stu-id="f4131-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="f4131-214">Poiché è hello reale coordinate (potrebbero non essere all'interno dei limiti di hello un determinato momento hello) non sono stati superati e utilizza i valori di test predefinite, si vedrà una notifica visualizzati nell'aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="f4131-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="f4131-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4131-215">What’s next?</span></span>
<span data-ttu-id="f4131-216">Esistono un paio di passaggi che potrebbe essere necessario toofollow in toohello aggiunta in precedenza toomake assicurarsi che la soluzione hello sia in ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="f4131-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="f4131-217">Prima di tutto, potrebbe essere necessario tooensure che geofences sono dinamici.</span><span class="sxs-lookup"><span data-stu-id="f4131-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="f4131-218">Questo richiederà un lavoro aggiuntivo con hello API di Bing in ordine toobe tooupload in grado di nuovi limiti all'interno di origine dati esistente hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="f4131-219">Consultare hello [documentazione API dei servizi di dati spaziali Bing](https://msdn.microsoft.com/library/ff701734.aspx) per ulteriori informazioni sul soggetto hello.</span><span class="sxs-lookup"><span data-stu-id="f4131-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="f4131-220">In secondo luogo, come tooensure di lavoro che non viene eseguito recapito hello toohello destra partecipanti, potrebbe essere necessario tootarget loro tramite [tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="f4131-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="f4131-221">soluzione di Hello illustrato in precedenza descrive uno scenario in cui un'ampia gamma di piattaforme di destinazione, potrebbe essere in modo che non si limitare hello geofencing toosystem funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f4131-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="f4131-222">Ciò premesso, hello Universal Windows Platform offre funzionalità troppo[rilevare geofences destra out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="f4131-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="f4131-223">Per altri dettagli relativi alle funzionalità di Hub di notifica, vedere il [portale di documentazione](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="f4131-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

