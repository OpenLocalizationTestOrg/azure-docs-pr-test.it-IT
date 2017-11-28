---
title: aaaRegistration gestione
description: In questo argomento viene illustrato come dispositivi tooregister con gli hub di notifica in ordine tooreceive notifiche push.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a><span data-ttu-id="af2ce-103">Gestione delle registrazioni</span><span class="sxs-lookup"><span data-stu-id="af2ce-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="af2ce-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="af2ce-104">Overview</span></span>
<span data-ttu-id="af2ce-105">In questo argomento viene illustrato come dispositivi tooregister con gli hub di notifica in ordine tooreceive notifiche push.</span><span class="sxs-lookup"><span data-stu-id="af2ce-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="af2ce-106">argomento Hello descrive le registrazioni a un livello elevato, quindi introduce hello due modelli principali per la registrazione di dispositivi: la registrazione dal dispositivo hello direttamente toohello hub di notifica e la registrazione tramite un back-end dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="af2ce-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="af2ce-107">Che cos'è la registrazione di un dispositivo</span><span class="sxs-lookup"><span data-stu-id="af2ce-107">What is device registration</span></span>
<span data-ttu-id="af2ce-108">La registrazione del dispositivo con un hub di notifica viene eseguita tramite una **registrazione** o un'**installazione**.</span><span class="sxs-lookup"><span data-stu-id="af2ce-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="af2ce-109">Registrazioni</span><span class="sxs-lookup"><span data-stu-id="af2ce-109">Registrations</span></span>
<span data-ttu-id="af2ce-110">Una registrazione associa hello servizio notifica piattaforma (PNS) handle per un dispositivo con tag e possibilmente un modello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="af2ce-111">handle PNS Hello potrebbe essere un ChannelURI, token del dispositivo o l'id registrazione GCM. I tag vengono utilizzati tooroute notifiche toohello set corretto di handle di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="af2ce-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="af2ce-112">Per altre informazioni, vedere [Routing ed espressioni tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="af2ce-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="af2ce-113">I modelli sono tooimplement utilizzati per ogni registrazione trasformazione.</span><span class="sxs-lookup"><span data-stu-id="af2ce-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="af2ce-114">Per altre informazioni, vedere [Modelli](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="af2ce-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="af2ce-115">Installazioni</span><span class="sxs-lookup"><span data-stu-id="af2ce-115">Installations</span></span>
<span data-ttu-id="af2ce-116">Un'installazione è una registrazione avanzata che include un contenitore di proprietà correlate al push.</span><span class="sxs-lookup"><span data-stu-id="af2ce-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="af2ce-117">È hello tooregistering approccio migliore e più recenti dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="af2ce-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="af2ce-118">Tuttavia, non è supportato dall’SDK .NET lato client ([SDK dell’hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)), per adesso.</span><span class="sxs-lookup"><span data-stu-id="af2ce-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="af2ce-119">Ciò significa che se si sta registrando dal dispositivo client hello stesso, sarebbe necessario hello toouse [API REST degli hub di notifica](https://msdn.microsoft.com/library/mt621153.aspx) approccio toosupport installazioni.</span><span class="sxs-lookup"><span data-stu-id="af2ce-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="af2ce-120">Se si utilizza un servizio back-end, dovrebbe essere in grado di toouse [SDK di Hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="af2ce-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="af2ce-121">di seguito Hello sono alcune installazioni toousing vantaggi chiave:</span><span class="sxs-lookup"><span data-stu-id="af2ce-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="af2ce-122">La creazione o l'aggiornamento di un'installazione è completamente idempotente.</span><span class="sxs-lookup"><span data-stu-id="af2ce-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="af2ce-123">È quindi possibile riprovare a eseguire l'operazione senza preoccuparsi di registrazioni duplicate.</span><span class="sxs-lookup"><span data-stu-id="af2ce-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="af2ce-124">il modello di installazione di Hello rende facile toodo singoli push - destinazione dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="af2ce-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="af2ce-125">Un tag di sistema **"$InstallationId:[installationId]"** viene aggiunto automaticamente con ogni registrazione basata su un'installazione.</span><span class="sxs-lookup"><span data-stu-id="af2ce-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="af2ce-126">Pertanto, è possibile chiamare tootarget di tag toothis una trasmissione un dispositivo specifico senza toodo qualsiasi codifica aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="af2ce-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="af2ce-127">Utilizzo di installazioni consente inoltre si toodo parziale gli aggiornamenti di registrazione.</span><span class="sxs-lookup"><span data-stu-id="af2ce-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="af2ce-128">Hello aggiornamento parziale di un'installazione viene richiesta con un metodo PATCH utilizzando hello [standard JSON Patch](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="af2ce-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="af2ce-129">Ciò è particolarmente utile quando si desidera che il tag tooupdate registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="af2ce-130">Non hai toopull registrazione intera hello verso il basso e quindi di inviare nuovamente tutti i tag precedente hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="af2ce-131">Un'installazione può contenere hello hello le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="af2ce-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="af2ce-132">Per un elenco completo delle proprietà di installazione hello, vedere [creare o sovrascrivere un'installazione con l'API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) o [le proprietà di installazione](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) per hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="af2ce-133">È importante toonote che le registrazioni e le installazioni per impostazione predefinita non scadono.</span><span class="sxs-lookup"><span data-stu-id="af2ce-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="af2ce-134">Le registrazioni e le installazioni devono contenere un handle PNS valido per ogni dispositivo/canale.</span><span class="sxs-lookup"><span data-stu-id="af2ce-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="af2ce-135">Poiché in un'app client sul dispositivo hello è possibile ottenere solo gli handle PNS, un modello è tooregister direttamente sul dispositivo con app client hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="af2ce-136">Hello altri logica di business e considerazioni sulla sicurezza, disponibilità correlati tootags potrebbero richiedere la registrazione del dispositivo toomanage in hello app back-end.</span><span class="sxs-lookup"><span data-stu-id="af2ce-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="af2ce-137">Modelli</span><span class="sxs-lookup"><span data-stu-id="af2ce-137">Templates</span></span>
<span data-ttu-id="af2ce-138">Se si desidera toouse [modelli](notification-hubs-templates-cross-platform-push-messages.md), installazione dispositivo hello contenere anche tutti i modelli associati al dispositivo in un formato JSON di formato (vedere l'esempio precedente).</span><span class="sxs-lookup"><span data-stu-id="af2ce-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="af2ce-139">Hello i nomi dei modelli indirizzare modelli diversi per hello stesso dispositivo.</span><span class="sxs-lookup"><span data-stu-id="af2ce-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="af2ce-140">Si noti che ogni nome di modello esegue il mapping tooa corpo del modello e un insieme facoltativo di tag.</span><span class="sxs-lookup"><span data-stu-id="af2ce-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="af2ce-141">Inoltre, ogni piattaforma può avere ulteriori proprietà del modello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="af2ce-142">Per Windows Store (con WNS) e Windows Phone 8 (tramite MPNS), un altro set di intestazioni può far parte del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="af2ce-143">Nel caso di hello di APN, è possibile impostare un'espressione di modello costante o tooa un tooeither di proprietà di scadenza.</span><span class="sxs-lookup"><span data-stu-id="af2ce-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="af2ce-144">Per un elenco completo delle proprietà di installazione hello, vedere [creare o sovrascrivere un'installazione con REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="af2ce-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="af2ce-145">Riquadri secondari per le app di Windows Store</span><span class="sxs-lookup"><span data-stu-id="af2ce-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="af2ce-146">Per le applicazioni client di Windows Store, l'invio di notifiche toosecondary riquadri è hello stesso come inviarli toohello primario.</span><span class="sxs-lookup"><span data-stu-id="af2ce-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="af2ce-147">Questo è supportato anche nelle installazioni.</span><span class="sxs-lookup"><span data-stu-id="af2ce-147">This is also supported in installations.</span></span> <span data-ttu-id="af2ce-148">Si noti che i riquadri secondari un URI di canale diversi, quali hello SDK nella tua app client gestisce in modo trasparente.</span><span class="sxs-lookup"><span data-stu-id="af2ce-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="af2ce-149">Hello SecondaryTiles dizionario Usa hello stesso ID di riquadro che è usato toocreate hello SecondaryTiles oggetto nell'app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="af2ce-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="af2ce-150">Come con hello canale primario, Channeluri dei riquadri secondari è possibile modificare in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="af2ce-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="af2ce-151">Nelle installazioni di hello ordine tookeep nell'hub di notifica hello aggiornato, il dispositivo hello necessario aggiornarli con hello Channeluri correnti dei riquadri secondari hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="af2ce-152">Gestione delle registrazioni dal dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="af2ce-152">Registration management from hello device</span></span>
<span data-ttu-id="af2ce-153">Per la gestione di registrazione del dispositivo da applicazioni client, hello di back-end è responsabile per l'invio di notifiche.</span><span class="sxs-lookup"><span data-stu-id="af2ce-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="af2ce-154">Le applicazioni client mantenere i propri handle PNS backup toodate e registra i tag.</span><span class="sxs-lookup"><span data-stu-id="af2ce-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="af2ce-155">Hello seguente immagine illustra questo modello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="af2ce-156">dispositivo Hello prima recupera hello handle PNS da hello PNS, quindi Registra con hub di notifica hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="af2ce-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="af2ce-157">Dopo la registrazione di hello ha esito positivo, back-end app hello può inviare una notifica che la registrazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="af2ce-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="af2ce-158">Per ulteriori informazioni su come toosend notifiche, vedere [Routing ed espressioni Tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="af2ce-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="af2ce-159">Si noti che in questo caso, si utilizzerà restare in ascolto solo tooaccess diritti da dispositivo hello gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="af2ce-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="af2ce-160">Per altre informazioni, vedere [Sicurezza](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="af2ce-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="af2ce-161">La registrazione dal dispositivo hello è il metodo più semplice di hello, ma presenta alcuni svantaggi.</span><span class="sxs-lookup"><span data-stu-id="af2ce-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="af2ce-162">primo svantaggio Hello è che un'app client può aggiornare solo i tag quando app hello è attiva.</span><span class="sxs-lookup"><span data-stu-id="af2ce-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="af2ce-163">Ad esempio, se un utente dispone di due dispositivi che registrano i team toosport correlati di tag, al primo dispositivo hello della registrazione per un tag aggiuntivo (ad esempio, Seahawks), hello secondo dispositivo non riceverà notifiche hello su hello Seahawks fino a quando l'applicazione hello in hello secondo dispositivo viene eseguita una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="af2ce-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="af2ce-164">Più in generale, quando i tag sono interessati più dispositivi, la gestione dei tag dal back-end hello è un'opzione utile.</span><span class="sxs-lookup"><span data-stu-id="af2ce-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="af2ce-165">Hello secondo svantaggio di gestione di registrazione da app client hello al fatto che, poiché possono essere attaccate App, proteggere registrazione hello toospecific tag richiede prestare particolare attenzione, come illustrato nella sezione hello "sicurezza a livello di Tag."</span><span class="sxs-lookup"><span data-stu-id="af2ce-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="af2ce-166">Tooregister codice di esempio con un hub di notifica da un dispositivo utilizzando un'installazione</span><span class="sxs-lookup"><span data-stu-id="af2ce-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="af2ce-167">In questo momento, è supportata solo tramite hello [API REST degli hub di notifica](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="af2ce-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="af2ce-168">È inoltre possibile utilizzare il metodo di PATCH hello utilizzando hello [standard JSON Patch](https://tools.ietf.org/html/rfc6902) di aggiornamento di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="af2ce-169">Tooregister codice di esempio con un hub di notifica da un dispositivo utilizzando una registrazione</span><span class="sxs-lookup"><span data-stu-id="af2ce-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="af2ce-170">Questi metodi, creare o aggiornare una registrazione per il dispositivo hello in cui vengono chiamati.</span><span class="sxs-lookup"><span data-stu-id="af2ce-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="af2ce-171">Ciò significa che, in ordine tooupdate hello handle o hello tag, è necessario sovrascrivere registrazione intera hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="af2ce-172">Tenere presente che le registrazioni sono temporanee, pertanto è necessario disporre di un archivio affidabile con i tag correnti hello che necessita di un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="af2ce-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="af2ce-173">Gestione delle registrazioni da un back-end</span><span class="sxs-lookup"><span data-stu-id="af2ce-173">Registration management from a backend</span></span>
<span data-ttu-id="af2ce-174">La gestione delle registrazioni dal back-end hello richiede che venga scritto codice aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="af2ce-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="af2ce-175">app Hello dal dispositivo hello è necessario fornire hello back-end toohello di handle PNS aggiornati a ogni avvio applicazione hello (insieme ai tag e i modelli) e back-end hello è necessario aggiornare questo handle sull'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="af2ce-176">Hello seguente immagine illustra la progettazione.</span><span class="sxs-lookup"><span data-stu-id="af2ce-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="af2ce-177">i vantaggi di Hello della gestione delle registrazioni dal back-end hello includono hello possibilità toomodify tag tooregistrations anche quando l'applicazione corrispondente hello sul dispositivo hello è inattivo e tooauthenticate hello client app prima di aggiungere una registrazione tooits tag.</span><span class="sxs-lookup"><span data-stu-id="af2ce-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="af2ce-178">Tooregister codice di esempio con un hub di notifica da un back-end di un'installazione</span><span class="sxs-lookup"><span data-stu-id="af2ce-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="af2ce-179">dispositivo client Hello ottiene comunque il pns e le proprietà di installazione rilevanti come prima e chiama un'API personalizzata nel back-end hello che consente di eseguire la registrazione di hello e autorizzare i tag back-end hello e così via può sfruttare hello [SDK di Hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="af2ce-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="af2ce-180">È inoltre possibile utilizzare il metodo di PATCH hello utilizzando hello [standard JSON Patch](https://tools.ietf.org/html/rfc6902) di aggiornamento di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="af2ce-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="af2ce-181">Tooregister codice di esempio con un hub di notifica da un dispositivo utilizzando un id di registrazione</span><span class="sxs-lookup"><span data-stu-id="af2ce-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="af2ce-182">Dal back-end dell'app è possibile eseguire operazioni CRUD di base sulle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="af2ce-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="af2ce-183">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="af2ce-183">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="af2ce-184">back-end Hello deve gestire la concorrenza tra gli aggiornamenti di registrazione.</span><span class="sxs-lookup"><span data-stu-id="af2ce-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="af2ce-185">Il bus di servizio offre il controllo della concorrenza ottimistica per la gestione delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="af2ce-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="af2ce-186">A livello di hello HTTP, questo viene implementato utilizzando hello ETag sulle operazioni di gestione di registrazione.</span><span class="sxs-lookup"><span data-stu-id="af2ce-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="af2ce-187">Questa funzionalità viene usata in modo trasparente dagli SDK Microsoft, che generano un'eccezione se un aggiornamento viene rifiutato a causa della concorrenza.</span><span class="sxs-lookup"><span data-stu-id="af2ce-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="af2ce-188">back-end app Hello è responsabile per la gestione delle eccezioni e nuovo tentativo di aggiornamento hello se necessario.</span><span class="sxs-lookup"><span data-stu-id="af2ce-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

