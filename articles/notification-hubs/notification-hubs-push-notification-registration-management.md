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
# <a name="registration-management"></a>Gestione delle registrazioni
## <a name="overview"></a>Panoramica
In questo argomento viene illustrato come dispositivi tooregister con gli hub di notifica in ordine tooreceive notifiche push. argomento Hello descrive le registrazioni a un livello elevato, quindi introduce hello due modelli principali per la registrazione di dispositivi: la registrazione dal dispositivo hello direttamente toohello hub di notifica e la registrazione tramite un back-end dell'applicazione. 

## <a name="what-is-device-registration"></a>Che cos'è la registrazione di un dispositivo
La registrazione del dispositivo con un hub di notifica viene eseguita tramite una **registrazione** o un'**installazione**.

#### <a name="registrations"></a>Registrazioni
Una registrazione associa hello servizio notifica piattaforma (PNS) handle per un dispositivo con tag e possibilmente un modello. handle PNS Hello potrebbe essere un ChannelURI, token del dispositivo o l'id registrazione GCM. I tag vengono utilizzati tooroute notifiche toohello set corretto di handle di dispositivo. Per altre informazioni, vedere [Routing ed espressioni tag](notification-hubs-tags-segment-push-message.md). I modelli sono tooimplement utilizzati per ogni registrazione trasformazione. Per altre informazioni, vedere [Modelli](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Installazioni
Un'installazione è una registrazione avanzata che include un contenitore di proprietà correlate al push. È hello tooregistering approccio migliore e più recenti dei dispositivi. Tuttavia, non è supportato dall’SDK .NET lato client ([SDK dell’hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)), per adesso.  Ciò significa che se si sta registrando dal dispositivo client hello stesso, sarebbe necessario hello toouse [API REST degli hub di notifica](https://msdn.microsoft.com/library/mt621153.aspx) approccio toosupport installazioni. Se si utilizza un servizio back-end, dovrebbe essere in grado di toouse [SDK di Hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

di seguito Hello sono alcune installazioni toousing vantaggi chiave:

* La creazione o l'aggiornamento di un'installazione è completamente idempotente. È quindi possibile riprovare a eseguire l'operazione senza preoccuparsi di registrazioni duplicate.
* il modello di installazione di Hello rende facile toodo singoli push - destinazione dispositivo specifico. Un tag di sistema **"$InstallationId:[installationId]"** viene aggiunto automaticamente con ogni registrazione basata su un'installazione. Pertanto, è possibile chiamare tootarget di tag toothis una trasmissione un dispositivo specifico senza toodo qualsiasi codifica aggiuntiva.
* Utilizzo di installazioni consente inoltre si toodo parziale gli aggiornamenti di registrazione. Hello aggiornamento parziale di un'installazione viene richiesta con un metodo PATCH utilizzando hello [standard JSON Patch](https://tools.ietf.org/html/rfc6902). Ciò è particolarmente utile quando si desidera che il tag tooupdate registrazione hello. Non hai toopull registrazione intera hello verso il basso e quindi di inviare nuovamente tutti i tag precedente hello.

Un'installazione può contenere hello hello le proprietà seguenti. Per un elenco completo delle proprietà di installazione hello, vedere [creare o sovrascrivere un'installazione con l'API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) o [le proprietà di installazione](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) per hello.

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



È importante toonote che le registrazioni e le installazioni per impostazione predefinita non scadono.

Le registrazioni e le installazioni devono contenere un handle PNS valido per ogni dispositivo/canale. Poiché in un'app client sul dispositivo hello è possibile ottenere solo gli handle PNS, un modello è tooregister direttamente sul dispositivo con app client hello. Hello altri logica di business e considerazioni sulla sicurezza, disponibilità correlati tootags potrebbero richiedere la registrazione del dispositivo toomanage in hello app back-end. 

#### <a name="templates"></a>Modelli
Se si desidera toouse [modelli](notification-hubs-templates-cross-platform-push-messages.md), installazione dispositivo hello contenere anche tutti i modelli associati al dispositivo in un formato JSON di formato (vedere l'esempio precedente). Hello i nomi dei modelli indirizzare modelli diversi per hello stesso dispositivo.

Si noti che ogni nome di modello esegue il mapping tooa corpo del modello e un insieme facoltativo di tag. Inoltre, ogni piattaforma può avere ulteriori proprietà del modello. Per Windows Store (con WNS) e Windows Phone 8 (tramite MPNS), un altro set di intestazioni può far parte del modello di hello. Nel caso di hello di APN, è possibile impostare un'espressione di modello costante o tooa un tooeither di proprietà di scadenza. Per un elenco completo delle proprietà di installazione hello, vedere [creare o sovrascrivere un'installazione con REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) argomento.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Riquadri secondari per le app di Windows Store
Per le applicazioni client di Windows Store, l'invio di notifiche toosecondary riquadri è hello stesso come inviarli toohello primario. Questo è supportato anche nelle installazioni. Si noti che i riquadri secondari un URI di canale diversi, quali hello SDK nella tua app client gestisce in modo trasparente.

Hello SecondaryTiles dizionario Usa hello stesso ID di riquadro che è usato toocreate hello SecondaryTiles oggetto nell'app di Windows Store.
Come con hello canale primario, Channeluri dei riquadri secondari è possibile modificare in qualsiasi momento. Nelle installazioni di hello ordine tookeep nell'hub di notifica hello aggiornato, il dispositivo hello necessario aggiornarli con hello Channeluri correnti dei riquadri secondari hello.

## <a name="registration-management-from-hello-device"></a>Gestione delle registrazioni dal dispositivo hello
Per la gestione di registrazione del dispositivo da applicazioni client, hello di back-end è responsabile per l'invio di notifiche. Le applicazioni client mantenere i propri handle PNS backup toodate e registra i tag. Hello seguente immagine illustra questo modello.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

dispositivo Hello prima recupera hello handle PNS da hello PNS, quindi Registra con hub di notifica hello direttamente. Dopo la registrazione di hello ha esito positivo, back-end app hello può inviare una notifica che la registrazione di destinazione. Per ulteriori informazioni su come toosend notifiche, vedere [Routing ed espressioni Tag](notification-hubs-tags-segment-push-message.md).
Si noti che in questo caso, si utilizzerà restare in ascolto solo tooaccess diritti da dispositivo hello gli hub di notifica. Per altre informazioni, vedere [Sicurezza](notification-hubs-push-notification-security.md).

La registrazione dal dispositivo hello è il metodo più semplice di hello, ma presenta alcuni svantaggi.
primo svantaggio Hello è che un'app client può aggiornare solo i tag quando app hello è attiva. Ad esempio, se un utente dispone di due dispositivi che registrano i team toosport correlati di tag, al primo dispositivo hello della registrazione per un tag aggiuntivo (ad esempio, Seahawks), hello secondo dispositivo non riceverà notifiche hello su hello Seahawks fino a quando l'applicazione hello in hello secondo dispositivo viene eseguita una seconda volta. Più in generale, quando i tag sono interessati più dispositivi, la gestione dei tag dal back-end hello è un'opzione utile.
Hello secondo svantaggio di gestione di registrazione da app client hello al fatto che, poiché possono essere attaccate App, proteggere registrazione hello toospecific tag richiede prestare particolare attenzione, come illustrato nella sezione hello "sicurezza a livello di Tag."

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Tooregister codice di esempio con un hub di notifica da un dispositivo utilizzando un'installazione
In questo momento, è supportata solo tramite hello [API REST degli hub di notifica](https://msdn.microsoft.com/library/mt621153.aspx).

È inoltre possibile utilizzare il metodo di PATCH hello utilizzando hello [standard JSON Patch](https://tools.ietf.org/html/rfc6902) di aggiornamento di installazione di hello.

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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Tooregister codice di esempio con un hub di notifica da un dispositivo utilizzando una registrazione
Questi metodi, creare o aggiornare una registrazione per il dispositivo hello in cui vengono chiamati. Ciò significa che, in ordine tooupdate hello handle o hello tag, è necessario sovrascrivere registrazione intera hello. Tenere presente che le registrazioni sono temporanee, pertanto è necessario disporre di un archivio affidabile con i tag correnti hello che necessita di un dispositivo specifico.

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


## <a name="registration-management-from-a-backend"></a>Gestione delle registrazioni da un back-end
La gestione delle registrazioni dal back-end hello richiede che venga scritto codice aggiuntivo. app Hello dal dispositivo hello è necessario fornire hello back-end toohello di handle PNS aggiornati a ogni avvio applicazione hello (insieme ai tag e i modelli) e back-end hello è necessario aggiornare questo handle sull'hub di notifica hello. Hello seguente immagine illustra la progettazione.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

i vantaggi di Hello della gestione delle registrazioni dal back-end hello includono hello possibilità toomodify tag tooregistrations anche quando l'applicazione corrispondente hello sul dispositivo hello è inattivo e tooauthenticate hello client app prima di aggiungere una registrazione tooits tag.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Tooregister codice di esempio con un hub di notifica da un back-end di un'installazione
dispositivo client Hello ottiene comunque il pns e le proprietà di installazione rilevanti come prima e chiama un'API personalizzata nel back-end hello che consente di eseguire la registrazione di hello e autorizzare i tag back-end hello e così via può sfruttare hello [SDK di Hub di notifica per le operazioni di back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

È inoltre possibile utilizzare il metodo di PATCH hello utilizzando hello [standard JSON Patch](https://tools.ietf.org/html/rfc6902) di aggiornamento di installazione di hello.

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


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Tooregister codice di esempio con un hub di notifica da un dispositivo utilizzando un id di registrazione
Dal back-end dell'app è possibile eseguire operazioni CRUD di base sulle registrazioni. ad esempio:

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


back-end Hello deve gestire la concorrenza tra gli aggiornamenti di registrazione. Il bus di servizio offre il controllo della concorrenza ottimistica per la gestione delle registrazioni. A livello di hello HTTP, questo viene implementato utilizzando hello ETag sulle operazioni di gestione di registrazione. Questa funzionalità viene usata in modo trasparente dagli SDK Microsoft, che generano un'eccezione se un aggiornamento viene rifiutato a causa della concorrenza. back-end app Hello è responsabile per la gestione delle eccezioni e nuovo tentativo di aggiornamento hello se necessario.

