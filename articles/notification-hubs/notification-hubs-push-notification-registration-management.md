---
title: Gestione delle registrazioni
description: In questo argomento viene illustrato come registrare i dispositivi con gli hub di notifica al fine di ricevere notifiche push.
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
ms.openlocfilehash: a1a349150ef4c7837932706f0c4fcc8d022ec7ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="registration-management"></a><span data-ttu-id="fa11d-103">Gestione delle registrazioni</span><span class="sxs-lookup"><span data-stu-id="fa11d-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="fa11d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fa11d-104">Overview</span></span>
<span data-ttu-id="fa11d-105">In questo argomento viene illustrato come registrare i dispositivi con gli hub di notifica al fine di ricevere notifiche push.</span><span class="sxs-lookup"><span data-stu-id="fa11d-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="fa11d-106">Vengono descritte le registrazioni a livello generale, quindi sono presentati i due modelli principali per la registrazione dei dispositivi: la registrazione dal dispositivo direttamente nell'hub di notifica e la registrazione tramite un back-end dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="fa11d-107">Che cos'è la registrazione di un dispositivo</span><span class="sxs-lookup"><span data-stu-id="fa11d-107">What is device registration</span></span>
<span data-ttu-id="fa11d-108">La registrazione del dispositivo con un hub di notifica viene eseguita tramite una **registrazione** o un'**installazione**.</span><span class="sxs-lookup"><span data-stu-id="fa11d-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="fa11d-109">Registrazioni</span><span class="sxs-lookup"><span data-stu-id="fa11d-109">Registrations</span></span>
<span data-ttu-id="fa11d-110">La registrazione associa l'handle del servizio di notifica della piattaforma (PNS) per un dispositivo con tag ed eventualmente un modello.</span><span class="sxs-lookup"><span data-stu-id="fa11d-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="fa11d-111">L'handle PNS può essere un valore di ChannelURI, un token di dispositivo o un ID di registrazione GCM.</span><span class="sxs-lookup"><span data-stu-id="fa11d-111">The PNS handle could be a ChannelURI, device token, or GCM registration id.</span></span> <span data-ttu-id="fa11d-112">I tag vengono usati per instradare le notifiche al set corretto di handle di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fa11d-112">Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="fa11d-113">Per altre informazioni, vedere [Routing ed espressioni tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="fa11d-113">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="fa11d-114">I modelli vengono usati per implementare una trasformazione a livello di singola registrazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-114">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="fa11d-115">Per altre informazioni, vedere [Modelli](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="fa11d-115">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="fa11d-116">Installazioni</span><span class="sxs-lookup"><span data-stu-id="fa11d-116">Installations</span></span>
<span data-ttu-id="fa11d-117">Un'installazione è una registrazione avanzata che include un contenitore di proprietà correlate al push.</span><span class="sxs-lookup"><span data-stu-id="fa11d-117">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="fa11d-118">È comunque l'approccio migliore e più recente alla registrazione dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="fa11d-118">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="fa11d-119">Tuttavia, non è supportato dall’SDK .NET lato client ([SDK dell’hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)), per adesso.</span><span class="sxs-lookup"><span data-stu-id="fa11d-119">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="fa11d-120">Questo significa che in caso di registrazione dal dispositivo client stesso, è necessario utilizzare l’approccio [API REST hub di notifica](https://msdn.microsoft.com/library/mt621153.aspx) per supportare le installazioni.</span><span class="sxs-lookup"><span data-stu-id="fa11d-120">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="fa11d-121">Se si utilizza un servizio di back-end, è possibile utilizzare l’ [SDK dell’hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="fa11d-121">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="fa11d-122">Ecco alcuni vantaggi chiave dell'uso delle installazioni:</span><span class="sxs-lookup"><span data-stu-id="fa11d-122">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="fa11d-123">La creazione o l'aggiornamento di un'installazione è completamente idempotente.</span><span class="sxs-lookup"><span data-stu-id="fa11d-123">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="fa11d-124">È quindi possibile riprovare a eseguire l'operazione senza preoccuparsi di registrazioni duplicate.</span><span class="sxs-lookup"><span data-stu-id="fa11d-124">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="fa11d-125">Il modello di installazione semplifica l'esecuzione di singoli push destinati a un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="fa11d-125">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="fa11d-126">Un tag di sistema **"$InstallationId:[installationId]"** viene aggiunto automaticamente con ogni registrazione basata su un'installazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-126">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="fa11d-127">È quindi possibile chiamare un'operazione di invio a questo tag per fare riferimento a un dispositivo specifico senza dover scrivere codice aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="fa11d-127">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="fa11d-128">L'uso delle installazioni consente inoltre di eseguire aggiornamenti parziali delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="fa11d-128">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="fa11d-129">L'aggiornamento parziale di un'installazione è richiesto con un metodo PATCH che usa lo [standard JSON-Patch](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="fa11d-129">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="fa11d-130">Questo è particolarmente utile quando si desidera aggiornare i tag nella registrazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-130">This is particularly useful when you want to update tags on the registration.</span></span> <span data-ttu-id="fa11d-131">Non è necessario disattivare l'intera registrazione e quindi inviare di nuovo tutti i tag precedenti.</span><span class="sxs-lookup"><span data-stu-id="fa11d-131">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="fa11d-132">Un'installazione può contenere le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="fa11d-132">An installation can contain the the following properties.</span></span> <span data-ttu-id="fa11d-133">Per un elenco completo delle proprietà di installazione, vedere [Creare o sovrascrivere un'installazione con API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) o [Proprietà Installation](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa11d-133">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for the .</span></span>

    // Example installation format to show some supported properties
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



<span data-ttu-id="fa11d-134">È importante notare che le registrazioni e le installazioni non scadono più per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fa11d-134">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="fa11d-135">Le registrazioni e le installazioni devono contenere un handle PNS valido per ogni dispositivo/canale.</span><span class="sxs-lookup"><span data-stu-id="fa11d-135">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="fa11d-136">Poiché gli handle PNS possono essere ottenuti solo in un'app client sul dispositivo, un modello consiste nell'eseguire la registrazione direttamente sul dispositivo con l'app client.</span><span class="sxs-lookup"><span data-stu-id="fa11d-136">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="fa11d-137">D'altra parte, le considerazioni sulla sicurezza e la logica di business relativa ai tag potrebbero richiedere di gestire la registrazione del dispositivo nel back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="fa11d-137">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="fa11d-138">Modelli</span><span class="sxs-lookup"><span data-stu-id="fa11d-138">Templates</span></span>
<span data-ttu-id="fa11d-139">Se si desidera usare [modelli](notification-hubs-templates-cross-platform-push-messages.md), l'installazione del dispositivo contiene anche tutti i modelli associati al dispositivo in un formato JSON (vedere l'esempio precedente).</span><span class="sxs-lookup"><span data-stu-id="fa11d-139">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="fa11d-140">I nomi dei modelli consentono di usare diversi modelli per lo stesso dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fa11d-140">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="fa11d-141">Si noti che il nome di ogni modello è associato al corpo di un modello e a un set di tag facoltativo.</span><span class="sxs-lookup"><span data-stu-id="fa11d-141">Note that each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="fa11d-142">Inoltre, ogni piattaforma può avere ulteriori proprietà del modello.</span><span class="sxs-lookup"><span data-stu-id="fa11d-142">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="fa11d-143">Per Windows Store (che usa WNS) e Windows Phone 8 (che usa MPNS), un set di intestazioni aggiuntivo può far parte del modello.</span><span class="sxs-lookup"><span data-stu-id="fa11d-143">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="fa11d-144">Nel caso degli APN, è possibile impostare una proprietà di scadenza su una costante o un'espressione del modello.</span><span class="sxs-lookup"><span data-stu-id="fa11d-144">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="fa11d-145">Per un elenco completo delle proprietà di installazione, vedere l'argomento [Creare o sovrascrivere un'installazione con REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fa11d-145">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="fa11d-146">Riquadri secondari per le app di Windows Store</span><span class="sxs-lookup"><span data-stu-id="fa11d-146">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="fa11d-147">Per le applicazioni client di Windows Store, inviare notifiche ai riquadri secondari equivale a inviarle a quello primario.</span><span class="sxs-lookup"><span data-stu-id="fa11d-147">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="fa11d-148">Questo è supportato anche nelle installazioni.</span><span class="sxs-lookup"><span data-stu-id="fa11d-148">This is also supported in installations.</span></span> <span data-ttu-id="fa11d-149">Si noti che i riquadri secondari hanno un diverso ChannelUri, che viene gestito in modo trasparente dall'SDK nell'app client.</span><span class="sxs-lookup"><span data-stu-id="fa11d-149">Note that secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="fa11d-150">Il dizionario SecondaryTiles usa lo stesso TileId che viene usato per creare l'oggetto SecondaryTiles nell'app di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="fa11d-150">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="fa11d-151">Come nel caso del valore ChannelUri primario, i valori ChannelUri dei riquadri secondari possono cambiare in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="fa11d-151">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="fa11d-152">Per mantenere aggiornate le installazioni nell'hub di notifica, il dispositivo deve aggiornarle con i valori ChannelUri correnti dei riquadri secondari.</span><span class="sxs-lookup"><span data-stu-id="fa11d-152">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="fa11d-153">Gestione delle registrazioni dal dispositivo</span><span class="sxs-lookup"><span data-stu-id="fa11d-153">Registration management from the device</span></span>
<span data-ttu-id="fa11d-154">Quando si gestisce la registrazione del dispositivo dalle app client, il back-end è responsabile solo dell'invio delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="fa11d-154">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="fa11d-155">Le app client mantengono aggiornati gli handle PNS e registrano i tag.</span><span class="sxs-lookup"><span data-stu-id="fa11d-155">Client apps keep PNS handles up to date, and register tags.</span></span> <span data-ttu-id="fa11d-156">Questo modello è illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="fa11d-156">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="fa11d-157">Il dispositivo recupera l'handle PNS dal PNS, quindi esegue la registrazione direttamente con l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="fa11d-157">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="fa11d-158">Una volta che la registrazione ha esito positivo, il back-end dell'app può inviare una notifica relativa alla registrazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-158">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="fa11d-159">Per altre informazioni su come inviare le notifiche, vedere [Routing ed espressioni tag](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="fa11d-159">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="fa11d-160">Si noti che in questo caso si useranno solo i diritti Listen per accedere agli hub di notifica dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fa11d-160">Note that in this case, you will use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="fa11d-161">Per altre informazioni, vedere [Sicurezza](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="fa11d-161">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="fa11d-162">La registrazione dal dispositivo è il metodo più semplice, ma presenta alcuni svantaggi.</span><span class="sxs-lookup"><span data-stu-id="fa11d-162">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="fa11d-163">Il primo svantaggio è che un'app client può aggiornare solo i propri tag quando l'app è attiva.</span><span class="sxs-lookup"><span data-stu-id="fa11d-163">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="fa11d-164">Ad esempio, se un utente dispone di due dispositivi che registrano tag relativi a squadre sportive, quando il primo dispositivo esegue la registrazione per un ulteriore tag (ad esempio, i Seahawk), il secondo dispositivo non riceverà le notifiche relative ai Seahawk finché l'app nel secondo dispositivo non viene eseguita una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="fa11d-164">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="fa11d-165">Più in generale, quando i tag interessano più dispositivi, la gestione dei tag dal back-end rappresenta una soluzione migliore.</span><span class="sxs-lookup"><span data-stu-id="fa11d-165">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="fa11d-166">Il secondo svantaggio della gestione delle registrazioni dall'app client è che, poiché le applicazioni possono essere oggetto di un attacco, proteggere la registrazione tramite tag specifici richiede particolare attenzione, come illustrato nella sezione "Sicurezza a livello di tag".</span><span class="sxs-lookup"><span data-stu-id="fa11d-166">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="fa11d-167">Codice di esempio per la registrazione con un hub di notifica da un dispositivo tramite un'installazione</span><span class="sxs-lookup"><span data-stu-id="fa11d-167">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="fa11d-168">Al momento, questa operazione è supportata solo tramite l' [API REST degli hub di notifica](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa11d-168">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="fa11d-169">È inoltre possibile usare il metodo PATCH tramite lo [standard JSON-Patch](https://tools.ietf.org/html/rfc6902) per l'aggiornamento dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-169">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

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

        // Determine the targetUri that we will sign
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



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="fa11d-170">Codice di esempio per la registrazione con un hub di notifica da un dispositivo tramite una registrazione</span><span class="sxs-lookup"><span data-stu-id="fa11d-170">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="fa11d-171">Questi metodi creano o aggiornano una registrazione per il dispositivo in cui vengono chiamati.</span><span class="sxs-lookup"><span data-stu-id="fa11d-171">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="fa11d-172">Ciò significa che, per aggiornare l'handle o i tag, è necessario sovrascrivere l'intera registrazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-172">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="fa11d-173">Tenere presente che le registrazioni sono temporanee, quindi è necessario disporre sempre di un archivio affidabile con i tag correnti necessari per il dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="fa11d-173">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="fa11d-174">Gestione delle registrazioni da un back-end</span><span class="sxs-lookup"><span data-stu-id="fa11d-174">Registration management from a backend</span></span>
<span data-ttu-id="fa11d-175">La gestione delle registrazioni dal back-end richiede la scrittura di codice aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="fa11d-175">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="fa11d-176">L'app dal dispositivo deve fornire l'handle PNS aggiornato al back-end a ogni avvio dell'app (insieme ai tag e ai modelli) e il back-end deve aggiornare tale handle nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="fa11d-176">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="fa11d-177">Questa progettazione è illustrata nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="fa11d-177">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="fa11d-178">I vantaggi della gestione delle registrazioni dal back-end includono la possibilità di modificare i tag delle registrazioni anche quando l'app corrispondente nel dispositivo è inattiva e di autenticare l'app client prima di aggiungere un tag alla relativa registrazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-178">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="fa11d-179">Codice di esempio per la registrazione con un hub di notifica da un back-end tramite un'installazione</span><span class="sxs-lookup"><span data-stu-id="fa11d-179">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="fa11d-180">Il dispositivo client ottiene ancora il relativo handle PNS e le proprietà di installazione rilevanti come prima e chiama un'API personalizzata nel back-end che può eseguire la registrazione, autorizzare i tag e così via. Il back-end può sfruttare l'[SDK degli hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="fa11d-180">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="fa11d-181">È inoltre possibile usare il metodo PATCH tramite lo [standard JSON-Patch](https://tools.ietf.org/html/rfc6902) per l'aggiornamento dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="fa11d-181">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
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


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="fa11d-182">Codice di esempio per la registrazione con un hub di notifica da un dispositivo tramite un ID di registrazione</span><span class="sxs-lookup"><span data-stu-id="fa11d-182">Example code to register with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="fa11d-183">Dal back-end dell'app è possibile eseguire operazioni CRUD di base sulle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="fa11d-183">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="fa11d-184">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fa11d-184">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
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


<span data-ttu-id="fa11d-185">Il back-end deve gestire la concorrenza tra gli aggiornamenti delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="fa11d-185">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="fa11d-186">Il bus di servizio offre il controllo della concorrenza ottimistica per la gestione delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="fa11d-186">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="fa11d-187">A livello HTTP, questo viene implementato attraverso l'uso di ETag sulle operazioni di gestione delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="fa11d-187">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="fa11d-188">Questa funzionalità viene usata in modo trasparente dagli SDK Microsoft, che generano un'eccezione se un aggiornamento viene rifiutato a causa della concorrenza.</span><span class="sxs-lookup"><span data-stu-id="fa11d-188">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="fa11d-189">Il backend dell'app è responsabile della gestione di queste eccezioni e dei nuovi tentativi di aggiornamento, se necessario.</span><span class="sxs-lookup"><span data-stu-id="fa11d-189">The app backend is responsible for handling these exceptions and retrying the update if required.</span></span>

