---
title: Notifiche push basate su recinto virtuale con Hub di notifica di Azure e dati spaziali di Bing | Documentazione Microsoft
description: "In questa esercitazione si apprenderà come recapitare le notifiche push in base alla posizione con Hub di notifica di Azure e i dati spaziali di Bing."
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
ms.openlocfilehash: b2a84e0479aac9ded08bb64e1ea20ddee6636cce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="14e10-104">Notifiche push basate su recinto virtuale con Hub di notifica di Azure e dati spaziali di Bing</span><span class="sxs-lookup"><span data-stu-id="14e10-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="14e10-105">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="14e10-105">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="14e10-106">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="14e10-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="14e10-107">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="14e10-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="14e10-108">In questa esercitazione si apprenderà come recapitare le notifiche push in base alla posizione con Hub di notifica di Azure e i dati spaziali di Bing, sfruttando un'applicazione della piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="14e10-108">In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14e10-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="14e10-109">Prerequisites</span></span>
<span data-ttu-id="14e10-110">Prima di tutto è necessario assicurarsi di avere tutti i prerequisiti software e relativi ai servizi:</span><span class="sxs-lookup"><span data-stu-id="14e10-110">First and foremost, you need to make sure that you have all the software and service pre-requisites:</span></span>

* <span data-ttu-id="14e10-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) o versione successiva (è accettabile anche [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)).</span><span class="sxs-lookup"><span data-stu-id="14e10-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="14e10-112">Versione più recente di [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="14e10-112">Latest version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="14e10-113">[Account Bing Maps Dev Center](https://www.bingmapsportal.com/) (è possibile crearne uno gratuitamente e associarlo all'account Microsoft).</span><span class="sxs-lookup"><span data-stu-id="14e10-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="14e10-114">Introduzione</span><span class="sxs-lookup"><span data-stu-id="14e10-114">Getting Started</span></span>
<span data-ttu-id="14e10-115">Si potrà quindi iniziare con la creazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="14e10-115">Let’s start by creating the project.</span></span> <span data-ttu-id="14e10-116">In Visual Studio avviare un nuovo progetto di tipo **App vuota (Windows universale)**.</span><span class="sxs-lookup"><span data-stu-id="14e10-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="14e10-117">Una volta completata la creazione del progetto, saranno disponibili tutte le potenzialità per l'app stessa.</span><span class="sxs-lookup"><span data-stu-id="14e10-117">Once the project creation is complete, you should have the harness for the app itself.</span></span> <span data-ttu-id="14e10-118">Ora si procederà alla configurazione dell'intera struttura del recinto virtuale.</span><span class="sxs-lookup"><span data-stu-id="14e10-118">Now let’s set up everything for the geo-fencing infrastructure.</span></span> <span data-ttu-id="14e10-119">Poiché a questo scopo si vogliono usare i servizi di Bing, è disponibile un endpoint API REST pubblico che consente di eseguire query su frame di posizione specifici:</span><span class="sxs-lookup"><span data-stu-id="14e10-119">Because we are going to use Bing services for this, there is a public REST API endpoint that allows us to query specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="14e10-120">Per renderlo funzionante, è necessario specificare i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="14e10-120">You will need to specify the following parameters to get it working:</span></span>

* <span data-ttu-id="14e10-121">**ID origine dati** e **Nome origine dati**: nell'API Bing Maps le origini dati contengono diversi metadati suddivisi in bucket, ad esempio posizioni e orario di ufficio dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="14e10-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="14e10-122">Altre informazioni sono disponibili qui.</span><span class="sxs-lookup"><span data-stu-id="14e10-122">You can read more about those here.</span></span> 
* <span data-ttu-id="14e10-123">**Nome entità** : l'entità che si vuole usare come punto di riferimento per la notifica.</span><span class="sxs-lookup"><span data-stu-id="14e10-123">**Entity Name** – the entity you want to use as a reference point for the notification.</span></span> 
* <span data-ttu-id="14e10-124">**Chiave API di Bing Maps** : questa è la chiave ottenuta in precedenza durante la creazione dell'account Bing Dev Center.</span><span class="sxs-lookup"><span data-stu-id="14e10-124">**Bing Maps API Key** – this is the key that you obtained earlier when you created the Bing Dev Center account.</span></span>

<span data-ttu-id="14e10-125">Di seguito si esaminerà in dettaglio la configurazione per ognuno degli elementi precedenti.</span><span class="sxs-lookup"><span data-stu-id="14e10-125">Let’s do a deep-dive on the setup for each of the elements above.</span></span>

## <a name="setting-up-the-data-source"></a><span data-ttu-id="14e10-126">Configurazione dell'origine dati</span><span class="sxs-lookup"><span data-stu-id="14e10-126">Setting up the data source</span></span>
<span data-ttu-id="14e10-127">È possibile eseguire questa operazione in Bing Maps Dev Center.</span><span class="sxs-lookup"><span data-stu-id="14e10-127">You can do it in the Bing Maps Dev Center.</span></span> <span data-ttu-id="14e10-128">È sufficiente fare clic su **Data sources** (Origini dati) sulla barra di spostamento in alto e selezionare **Manage Data Sources** (Gestisci origini dati).</span><span class="sxs-lookup"><span data-stu-id="14e10-128">Simply click on **Data sources** in the top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="14e10-129">Se l'API Bing Maps non è mai stata usata prima, molto probabilmente non saranno presenti origini dati, quindi è possibile crearne una nuova facendo clic su Upload data source.</span><span class="sxs-lookup"><span data-stu-id="14e10-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data to a data source.</span></span> <span data-ttu-id="14e10-130">Assicurarsi di compilare tutti i campi obbligatori:</span><span class="sxs-lookup"><span data-stu-id="14e10-130">Make sure you fill out all the required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="14e10-131">Ci si potrebbe chiedere che cos'è il file di dati e cosa si deve caricare.</span><span class="sxs-lookup"><span data-stu-id="14e10-131">You might be wondering – what is the data file and what should you be uploading?</span></span> <span data-ttu-id="14e10-132">Ai fini di questo test, è possibile usare semplicemente l'esempio basato su pipe che delimita un'area del porto di San Francisco:</span><span class="sxs-lookup"><span data-stu-id="14e10-132">For the purposes of this test, we can just use the sample pipe-based that frames an area of the San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="14e10-133">Il codice precedente rappresenta questa entità:</span><span class="sxs-lookup"><span data-stu-id="14e10-133">The above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="14e10-134">Basta copiare e incollare la stringa sopra in un nuovo file e salvarlo come **NotificationHubsGeofence.pipe**, quindi caricarlo in Bing Dev Center.</span><span class="sxs-lookup"><span data-stu-id="14e10-134">Simply copy and paste the string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in the Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="14e10-135">È possibile che venga richiesto di specificare una nuova chiave per **Master Key** (Chiave master) diversa da **Query Key** (Chiave di query).</span><span class="sxs-lookup"><span data-stu-id="14e10-135">You might be prompted to specify a new key for the **Master Key** that is different from the **Query Key**.</span></span> <span data-ttu-id="14e10-136">Creare semplicemente una nuova chiave tramite il dashboard e aggiornare la pagina di caricamento dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="14e10-136">Simply create a new key through the dashboard and refresh the data source upload page.</span></span>
> 
> 

<span data-ttu-id="14e10-137">Dopo aver caricato il file di dati, è necessario assicurarsi di pubblicare l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="14e10-137">Once you upload the data file, you will need to make sure that you publish the data source.</span></span> 

<span data-ttu-id="14e10-138">Passare a **Manage Data Sources** (Gestisci origini dati), come fatto in precedenza, trovare l'origine dati nell'elenco e fare clic su **Publish** (Pubblica) nella colonna **Actions** (Azioni).</span><span class="sxs-lookup"><span data-stu-id="14e10-138">Go to **Manage Data Sources**, just like we did above, find your data source in the list and click on **Publish** in the **Actions** column.</span></span> <span data-ttu-id="14e10-139">Dopo un attimo l'origine dati verrà visualizzata nella scheda **Published Data Sources** :</span><span class="sxs-lookup"><span data-stu-id="14e10-139">In a bit, you should see your data source in the **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="14e10-140">Se si fa clic su **Edit**, si potrà vedere un riepilogo delle posizioni inserite:</span><span class="sxs-lookup"><span data-stu-id="14e10-140">If you click **Edit**, you will be able to see at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="14e10-141">A questo punto, il portale non visualizza i limiti del recinto virtuale creato. Tutto ciò che serve è avere una conferma che la posizione specificata è in prossimità del punto corretto.</span><span class="sxs-lookup"><span data-stu-id="14e10-141">At this point, the portal does not show you the boundaries for the geofence that we created – all we need is a confirmation that the location specified is in the right vicinity.</span></span>

<span data-ttu-id="14e10-142">Ora sono disponibili tutti i requisiti per l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="14e10-142">Now you have all the requirements for the data source.</span></span> <span data-ttu-id="14e10-143">Per altre informazioni sull'URL della richiesta per la chiamata API, in Bing Maps Dev Center fare clic su **Data sources** (Origini dati) e selezionare **Data Source Information** (Informazioni origine dati).</span><span class="sxs-lookup"><span data-stu-id="14e10-143">To get the details on the request URL for the API call, in the Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="14e10-144">L'opzione da esaminare è **Query URL** .</span><span class="sxs-lookup"><span data-stu-id="14e10-144">The **Query URL** is what we’re after here.</span></span> <span data-ttu-id="14e10-145">Si tratta dell'endpoint su cui è possibile eseguire query per verificare se il dispositivo si trova o meno entro i limiti di una posizione.</span><span class="sxs-lookup"><span data-stu-id="14e10-145">This is the endpoint against which we can execute queries to check whether the device is currently within the boundaries of a location or not.</span></span> <span data-ttu-id="14e10-146">Per eseguire questa verifica, è sufficiente eseguire una chiamata GET con l'URL della query, aggiungendo i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="14e10-146">To perform this check, we simply need to execute a GET call against the query URL, with the following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="14e10-147">In questo modo si specifica un punto di destinazione ottenuto dal dispositivo e Bing Maps esegue automaticamente i calcoli per vedere se si trova all'interno del recinto virtuale.</span><span class="sxs-lookup"><span data-stu-id="14e10-147">That way you're specifying a target point that we obtain from the device and Bing Maps will automatically perform the calculations to see whether it is within the geofence.</span></span> <span data-ttu-id="14e10-148">Dopo l'esecuzione della richiesta tramite un browser (o cURL), si otterrà una risposta JSON standard:</span><span class="sxs-lookup"><span data-stu-id="14e10-148">Once you execute the request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="14e10-149">Questa risposta viene restituita solo quando il punto è effettivamente entro i limiti designati.</span><span class="sxs-lookup"><span data-stu-id="14e10-149">This response only happens when the point is actually within the designated boundaries.</span></span> <span data-ttu-id="14e10-150">In caso contrario, si otterrà un bucket **results** vuoto:</span><span class="sxs-lookup"><span data-stu-id="14e10-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-the-uwp-application"></a><span data-ttu-id="14e10-151">Configurazione dell'applicazione UWP</span><span class="sxs-lookup"><span data-stu-id="14e10-151">Setting up the UWP application</span></span>
<span data-ttu-id="14e10-152">Ora che l'origine dati è pronta, è possibile iniziare a utilizzare l'applicazione UWP avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="14e10-152">Now that we have the data source ready, we can start working on the UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="14e10-153">Prima di tutto è necessario abilitare i servizi di posizione per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="14e10-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="14e10-154">A questo scopo, fare doppio clic sul file `Package.appxmanifest` in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="14e10-154">To do this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="14e10-155">Nella scheda delle proprietà del pacchetto aperta fare clic su **Funzionalità** e assicurarsi di selezionare **Posizione**:</span><span class="sxs-lookup"><span data-stu-id="14e10-155">In the package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="14e10-156">Dopo aver dichiarato la funzionalità Posizione, creare una nuova cartella denominata `Core` nella soluzione e aggiungervi un nuovo file denominato `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="14e10-156">As the location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="14e10-157">La classe `LocationHelper` stessa a questo punto è abbastanza semplice: consente solo di ottenere la posizione dell'utente tramite l'API di sistema:</span><span class="sxs-lookup"><span data-stu-id="14e10-157">The `LocationHelper` class itself is fairly basic at this point – all it does is allow us to obtain the user location through the system API:</span></span>

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

<span data-ttu-id="14e10-158">Per altre informazioni su come ottenere la posizione dell'utente nelle app UWP, vedere il [documento ufficiale su MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="14e10-158">You can read more about getting the user’s location in UWP apps in the official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="14e10-159">Per verificare che l'acquisizione della posizione funzioni effettivamente, aprire il lato del codice della pagina principale (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="14e10-159">To check that the location acquisition is actually working, open the code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="14e10-160">Creare un nuovo gestore eventi per l'evento `Loaded` nel costruttore `MainPage`:</span><span class="sxs-lookup"><span data-stu-id="14e10-160">Create a new event handler for the `Loaded` event in the `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="14e10-161">Ecco l'implementazione del gestore eventi:</span><span class="sxs-lookup"><span data-stu-id="14e10-161">The implementation of the event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="14e10-162">Si noti che il gestore è dichiarato come async, perché `GetCurrentLocation` è di tipo awaitable e quindi richiede l'esecuzione in un contesto asincrono.</span><span class="sxs-lookup"><span data-stu-id="14e10-162">Notice that we declared the handler as async because `GetCurrentLocation` is awaitable, and therefore requires to be executed in an async context.</span></span> <span data-ttu-id="14e10-163">Poiché in alcuni casi è possibile che venga restituita una posizione Null, ad esempio i servizi di posizione sono disabilitati o all'applicazione sono state negate le autorizzazioni per l'accesso alla posizione, è necessario assicurarsi che sia gestito correttamente con un controllo Null.</span><span class="sxs-lookup"><span data-stu-id="14e10-163">Also, because under certain circumstances we might end up with a null location (e.g. the location services are disabled or the application was denied permissions to access location), we need to make sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="14e10-164">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="14e10-164">Run the application.</span></span> <span data-ttu-id="14e10-165">Accertarsi di consentire l'accesso alla posizione:</span><span class="sxs-lookup"><span data-stu-id="14e10-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="14e10-166">Una volta avviata l'applicazione, sarà possibile visualizzare le coordinate nella finestra **Output** :</span><span class="sxs-lookup"><span data-stu-id="14e10-166">Once the application launches, you should be able to see the coordinates in the **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="14e10-167">Dopo aver stabilito che l'acquisizione della posizione funziona, è possibile rimuovere il gestore dell'evento test per Loaded, perché non verrà più usato.</span><span class="sxs-lookup"><span data-stu-id="14e10-167">Now you know that location acquisition works – feel free to remove the test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="14e10-168">Il passaggio successivo consiste nell'acquisire le modifiche della posizione.</span><span class="sxs-lookup"><span data-stu-id="14e10-168">The next step is to capture location changes.</span></span> <span data-ttu-id="14e10-169">A questo scopo, tornare alla classe `LocationHelper` e aggiungere il gestore eventi per `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="14e10-169">For that, let’s go back to the `LocationHelper` class and add the event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="14e10-170">L'implementazione mostrerà le coordinate della posizione nella finestra **Output** :</span><span class="sxs-lookup"><span data-stu-id="14e10-170">The implementation will show the location coordinates in the **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-the-backend"></a><span data-ttu-id="14e10-171">Configurazione del back-end</span><span class="sxs-lookup"><span data-stu-id="14e10-171">Setting up the backend</span></span>
<span data-ttu-id="14e10-172">Scaricare l' [esempio di back-end .NET da GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="14e10-172">Download the [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="14e10-173">Al termine del download, aprire la cartella `NotifyUsers` e successivamente il file `NotifyUsers.sln`.</span><span class="sxs-lookup"><span data-stu-id="14e10-173">Once the download completes, open the `NotifyUsers` folder, and subsequently – the `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="14e10-174">Impostare il progetto `AppBackend` come **Progetto di avvio** e avviarlo.</span><span class="sxs-lookup"><span data-stu-id="14e10-174">Set the `AppBackend` project as the **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="14e10-175">Il progetto è già configurato per l'invio di notifiche push ai dispositivi di destinazione, quindi sarà necessario eseguire solo due operazioni, ovvero sostituire la stringa di connessione con quella corretta per l'hub di notifica e aggiungere l'identificazione del limite per inviare la notifica solo quando l'utente si trova all'interno del recinto virtuale.</span><span class="sxs-lookup"><span data-stu-id="14e10-175">The project is already configured to send push notifications to target devices, so we’ll need to do only two things – swap out the right connection string for the notification hub and add boundary identification to send the notification only when the user is within the geofence.</span></span>

<span data-ttu-id="14e10-176">Per configurare la stringa di connessione, nella cartella `Models` aprire `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="14e10-176">To configure the connection string, in the `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="14e10-177">La funzione `NotificationHubClient.CreateClientFromConnectionString` deve contenere le informazioni sull'hub di notifica che è possibile ottenere dal [portale di Azure](https://portal.azure.com), ovvero in **Impostazioni** nel pannello **Criteri di accesso**.</span><span class="sxs-lookup"><span data-stu-id="14e10-177">The `NotificationHubClient.CreateClientFromConnectionString` function should contain the information about your notification hub that you can get in the [Azure Portal](https://portal.azure.com) (look inside the **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="14e10-178">Salvare il file di configurazione aggiornato.</span><span class="sxs-lookup"><span data-stu-id="14e10-178">Save the updated configuration file.</span></span>

<span data-ttu-id="14e10-179">A questo punto è necessario creare un modello per il risultato dell'API Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="14e10-179">Now we need to create a model for the Bing Maps API result.</span></span> <span data-ttu-id="14e10-180">Il modo più semplice è fare clic con il pulsante destro del mouse sulla cartella `Models`, **Aggiungi** > **Classe**.</span><span class="sxs-lookup"><span data-stu-id="14e10-180">The easiest way to do that is right-click on the `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="14e10-181">Denominarlo `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="14e10-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="14e10-182">Al termine, copiare il codice JSON dalla risposta dell'API descritta nella prima sezione e in Visual Studio usare **Modifica** > **Incolla speciale** > **Incolla JSON come classi**.</span><span class="sxs-lookup"><span data-stu-id="14e10-182">Once done, copy the JSON from the API response that we discussed in the first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="14e10-183">In questo modo si assicura che l'oggetto verrà deserializzato esattamente nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="14e10-183">That way we ensure that the object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="14e10-184">Il set di classi risultante sarà analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="14e10-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="14e10-185">Aprire quindi `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="14e10-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="14e10-186">È necessario modificare la chiamata Post per tenere conto della longitudine e latitudine della destinazione.</span><span class="sxs-lookup"><span data-stu-id="14e10-186">We need to tweak the Post call to account for the target longitude and latitude.</span></span> <span data-ttu-id="14e10-187">A questo scopo, è sufficiente aggiungere due stringhe alla firma della funzione: `latitude` e `longitude`.</span><span class="sxs-lookup"><span data-stu-id="14e10-187">For that, simply add two strings to the function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="14e10-188">Creare una nuova classe all'interno del progetto chiamata `ApiHelper.cs`. Verrà usata per connettersi a Bing per controllare le intersezioni dei limiti del punto.</span><span class="sxs-lookup"><span data-stu-id="14e10-188">Create a new class within the project called `ApiHelper.cs` – we’ll use it to connect to Bing to check point boundary intersections.</span></span> <span data-ttu-id="14e10-189">Implementare una funzione `IsPointWithinBounds` simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="14e10-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="14e10-190">Assicurarsi di sostituire l'endpoint API con l'URL della query ottenuto in precedenza da Bing Dev Center (lo stesso vale per la chiave API).</span><span class="sxs-lookup"><span data-stu-id="14e10-190">Make sure to substitute the API endpoint with the query URL that you obtained earlier from the Bing Dev Center (same applies to the API key).</span></span> 
> 
> 

<span data-ttu-id="14e10-191">Se sono presenti risultati per la query, significa che il punto specificato si trova entro i limiti del recinto virtuale, quindi viene restituito `true`.</span><span class="sxs-lookup"><span data-stu-id="14e10-191">If there are results to the query, that means that the specified point is within the boundaries of the geofence, so we return `true`.</span></span> <span data-ttu-id="14e10-192">Se non sono presenti risultati, significa che il punto è all'esterno del frame di ricerca, quindi viene restituito `false`.</span><span class="sxs-lookup"><span data-stu-id="14e10-192">If there are no results, Bing is telling us that the point is outside the lookup frame, so we return `false`.</span></span>

<span data-ttu-id="14e10-193">Tornare a `NotificationsController.cs`e creare un controllo prima dell'istruzione switch:</span><span class="sxs-lookup"><span data-stu-id="14e10-193">Back in `NotificationsController.cs`, create a check right before the switch statement:</span></span>

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

<span data-ttu-id="14e10-194">In questo modo la notifica viene inviata solo se il punto si trova entro i limiti.</span><span class="sxs-lookup"><span data-stu-id="14e10-194">That way, the notification is only sent when the point is within the boundaries.</span></span>

## <a name="testing-push-notifications-in-the-uwp-app"></a><span data-ttu-id="14e10-195">Test delle notifiche push nell'app UWP</span><span class="sxs-lookup"><span data-stu-id="14e10-195">Testing push notifications in the UWP app</span></span>
<span data-ttu-id="14e10-196">Tornando all'app UWP si sarà in grado di testare le notifiche.</span><span class="sxs-lookup"><span data-stu-id="14e10-196">Going back to the UWP app, we should now be able to test notifications.</span></span> <span data-ttu-id="14e10-197">Nella classe `LocationHelper` creare una nuova funzione `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="14e10-197">Within the `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="14e10-198">Scambiare `POST_URL` con il percorso dell'applicazione Web distribuita creata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="14e10-198">Swap the `POST_URL` to the location of your deployed web application that we created in the previous section.</span></span> <span data-ttu-id="14e10-199">Per ora è possibile eseguirla in locale, ma quando si lavora alla distribuzione di una versione pubblica, sarà necessario ospitarla presso un provider esterno.</span><span class="sxs-lookup"><span data-stu-id="14e10-199">For now, it’s OK to run it locally, but as you work on deploying a public version, you will need to host it with an external provider.</span></span>
> 
> 

<span data-ttu-id="14e10-200">È importante, a questo punto, accertarsi di registrare l'app UWP per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="14e10-200">Let’s now make sure that we register the UWP app for push notifications.</span></span> <span data-ttu-id="14e10-201">In Visual Studio fare clic su **Progetto** > **Store** > **Associa applicazione a Store**.</span><span class="sxs-lookup"><span data-stu-id="14e10-201">In Visual Studio, click on **Project** > **Store** > **Associate app with the store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="14e10-202">Dopo l'accesso con l'account per sviluppatore, assicurarsi di selezionare un'app esistente o crearne una nuova a cui si deve associare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="14e10-202">Once you sign in to your developer account, make sure you select an existing app or create a new one and associate the package with it.</span></span> 

<span data-ttu-id="14e10-203">Usare Dev Center e aprire l'app appena creata.</span><span class="sxs-lookup"><span data-stu-id="14e10-203">Go to the Dev Center and open the app that you just created.</span></span> <span data-ttu-id="14e10-204">Fare clic su **Servizi** > **Notifiche push** > **Sito dei servizi Live**.</span><span class="sxs-lookup"><span data-stu-id="14e10-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="14e10-205">Nel sito prendere nota del **segreto dell'applicazione** e del **SID del pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="14e10-205">On the site, take note of the **Application Secret** and the **Package SID**.</span></span> <span data-ttu-id="14e10-206">Saranno necessari entrambi nel portale di Azure. Aprire l'hub di notifica, fare clic su **Impostazioni** > **Servizi di notifica** > **Windows (WNS)** e immettere le informazioni nei campi obbligatori.</span><span class="sxs-lookup"><span data-stu-id="14e10-206">You will need both in the Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter the information in the required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="14e10-207">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="14e10-207">Click on **Save**.</span></span>

<span data-ttu-id="14e10-208">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="14e10-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="14e10-209">Sarà necessario aggiungere un riferimento alla **libreria gestita del bus di servizio di Microsoft Azure**. Cercare semplicemente `WindowsAzure.Messaging.Managed` e aggiungerlo al progetto.</span><span class="sxs-lookup"><span data-stu-id="14e10-209">We will need to add a reference to the **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it to your project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="14e10-210">A scopo di test, è possibile creare di nuovo il gestore eventi `MainPage_Loaded` e aggiungervi questo frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="14e10-210">For testing purposes, we can create the `MainPage_Loaded` event handler once again, and add this code snippet to it:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays the registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="14e10-211">Il codice precedente registra l'app con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="14e10-211">The above registers the app with the notification hub.</span></span> <span data-ttu-id="14e10-212">Ora si è pronti per iniziare.</span><span class="sxs-lookup"><span data-stu-id="14e10-212">You are ready to go!</span></span> 

<span data-ttu-id="14e10-213">In `LocationHelper`, all'interno del gestore `Geolocator_PositionChanged`, è possibile aggiungere un frammento di codice di test che inserirà la posizione all'interno del recinto virtuale in modo forzato:</span><span class="sxs-lookup"><span data-stu-id="14e10-213">In `LocationHelper`, inside the `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put the location inside the geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="14e10-214">Poiché non vengono passate le coordinate reali (è possibile che al momento non ci si trovi entro i limiti) e si usano valori di test predefiniti, al momento dell'aggiornamento verrà visualizzata una notifica:</span><span class="sxs-lookup"><span data-stu-id="14e10-214">Because we are not passing the real coordinates (which might not be within the boundaries at the moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="14e10-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14e10-215">What’s next?</span></span>
<span data-ttu-id="14e10-216">È possibile eseguire un paio di passaggi oltre a quelli descritti per assicurarsi che la soluzione sia pronta per la produzione.</span><span class="sxs-lookup"><span data-stu-id="14e10-216">There are a couple of steps that you might need to follow in addition to the above to make sure that the solution is production-ready.</span></span>

<span data-ttu-id="14e10-217">Prima di tutto è necessario assicurarsi che i recinti virtuali siano dinamici.</span><span class="sxs-lookup"><span data-stu-id="14e10-217">First and foremost, you might need to ensure that geofences are dynamic.</span></span> <span data-ttu-id="14e10-218">A questo scopo è necessario eseguire altre operazioni con l'API Bing per poter caricare nuovi limiti nell'origine dati esistente.</span><span class="sxs-lookup"><span data-stu-id="14e10-218">This will require some extra work with the Bing API in order to be able to upload new boundaries within the existing data source.</span></span> <span data-ttu-id="14e10-219">Per altre informazioni sull'argomento, vedere la [documentazione dell'API dei servizi dati spaziali di Bing](https://msdn.microsoft.com/library/ff701734.aspx) .</span><span class="sxs-lookup"><span data-stu-id="14e10-219">Consult the [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on the subject.</span></span>

<span data-ttu-id="14e10-220">Dato che lo scopo è assicurarsi che le notifiche siano recapitate ai partecipanti corretti, è consigliabile usare l' [assegnazione di tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="14e10-220">Second, as you are working to ensure that the delivery is done to the right participants, you might want to target them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="14e10-221">La soluzione illustrata sopra descrive uno scenario in cui è possibile avere un'ampia gamma di piattaforme di destinazione, quindi il recinto virtuale non è stato limitato alle funzionalità specifiche del sistema.</span><span class="sxs-lookup"><span data-stu-id="14e10-221">The solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit the geofencing to system-specific capabilities.</span></span> <span data-ttu-id="14e10-222">Ciò premesso, la piattaforma UWP (Universal Windows Platform) offre funzionalità per [rilevare automaticamente i recinti virtuali](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="14e10-222">That said, the Universal Windows Platform offers capabilities to [detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="14e10-223">Per altri dettagli relativi alle funzionalità di Hub di notifica, vedere il [portale di documentazione](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="14e10-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

