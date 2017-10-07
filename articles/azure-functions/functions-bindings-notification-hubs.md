---
title: associazione di Hub di notifica delle funzioni aaaAzure | Documenti Microsoft
description: Comprendere come associazione di Hub di notifica di Azure toouse nelle funzioni di Azure.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="be082-104">Associazione di output di Hub di notifica in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="be082-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="be082-105">Questo articolo viene illustrato come associazioni di Hub di notifica di Azure tooconfigure e codice nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="be082-105">This article explains how tooconfigure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="be082-106">Le funzioni possono inviare notifiche push usando un hub di notifica di Azure configurato con poche righe di codice.</span><span class="sxs-lookup"><span data-stu-id="be082-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="be082-107">Tuttavia, hello Hub di notifica di Azure deve essere configurato per la piattaforma notifiche servizi (PNS) si desidera toouse hello.</span><span class="sxs-lookup"><span data-stu-id="be082-107">However, hello Azure Notification Hub must be configured for hello Platform Notifications Services (PNS) you want toouse.</span></span> <span data-ttu-id="be082-108">Per ulteriori informazioni su come configurare un Hub di notifica di Azure e lo sviluppo di applicazioni client che registrano tooreceive notifiche, vedere [Introduzione agli hub di notifica](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) e scegliere la piattaforma di destinazione client in hello In alto.</span><span class="sxs-lookup"><span data-stu-id="be082-108">For more information on configuring an Azure Notification Hub and developing a client applications that register tooreceive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at hello top.</span></span>

<span data-ttu-id="be082-109">inviare le notifiche di Hello possono essere notifiche native o notifiche di modello.</span><span class="sxs-lookup"><span data-stu-id="be082-109">hello notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="be082-110">Notifiche native una piattaforma notifica specifica come configurato nella hello `platform` proprietà di hello associazione di output.</span><span class="sxs-lookup"><span data-stu-id="be082-110">Native notifications target a specific notification platform as configured in hello `platform` property of hello output binding.</span></span> <span data-ttu-id="be082-111">Una notifica modello può essere utilizzato tootarget più piattaforme.</span><span class="sxs-lookup"><span data-stu-id="be082-111">A template notification can be used tootarget multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="be082-112">Associazione delle proprietà di uscita dell'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="be082-112">Notification hub output binding properties</span></span>
<span data-ttu-id="be082-113">file function.json Hello fornisce hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="be082-113">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="be082-114">`name`: Nome variabile utilizzato nel codice di funzione per il messaggio hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="be082-114">`name` : Variable name used in function code for hello notification hub message.</span></span>
* <span data-ttu-id="be082-115">`type`: deve essere impostato troppo*"hub di notifica"*.</span><span class="sxs-lookup"><span data-stu-id="be082-115">`type` : must be set too*"notificationHub"*.</span></span>
* <span data-ttu-id="be082-116">`tagExpression`: Espressioni tag consentono di toospecify che tooa set di dispositivi che hanno registrato notifiche tooreceive che corrispondano all'espressione tag hello recapitare le notifiche.</span><span class="sxs-lookup"><span data-stu-id="be082-116">`tagExpression` : Tag expressions allow you toospecify that notifications be delivered tooa set of devices who have registered tooreceive notifications that match hello tag expression.</span></span>  <span data-ttu-id="be082-117">Per altre informazioni, vedere [Routing ed espressioni tag](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="be082-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="be082-118">`hubName`: Nome della risorsa di hub di notifica di hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be082-118">`hubName` : Name of hello notification hub resource in hello Azure portal.</span></span>
* <span data-ttu-id="be082-119">`connection`: La stringa di connessione deve essere un **impostazione dell'applicazione** stringa di connessione impostata toohello *DefaultFullSharedAccessSignature* valore per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="be082-119">`connection` : This connection string must be an **Application Setting** connection string set toohello *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="be082-120">`direction`: deve essere impostato troppo*"out"*.</span><span class="sxs-lookup"><span data-stu-id="be082-120">`direction` : must be set too*"out"*.</span></span> 
* <span data-ttu-id="be082-121">`platform`: proprietà piattaforma hello indica piattaforma notifica hello destinazione della notifica.</span><span class="sxs-lookup"><span data-stu-id="be082-121">`platform` : hello platform property indicates hello notification platform your notification targets.</span></span> <span data-ttu-id="be082-122">Deve essere uno dei seguenti valori hello:</span><span class="sxs-lookup"><span data-stu-id="be082-122">Must be one of hello following values:</span></span>
  * <span data-ttu-id="be082-123">Per impostazione predefinita, se proprietà piattaforma hello viene omessa dall'output di hello associazione, le notifiche di modello possono essere utilizzato tootarget qualsiasi piattaforma configurata nel hello Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="be082-123">By default, if hello platform property is omitted from hello output binding, template notifications can be used tootarget any platform configured on hello Azure Notification Hub.</span></span> <span data-ttu-id="be082-124">Per ulteriori informazioni sull'utilizzo dei modelli in generale toosend cross platform notifiche con un Hub di notifica di Azure, vedere [modelli](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="be082-124">For more information on using templates in general toosend cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="be082-125">`apns` : Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="be082-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="be082-126">Per ulteriori informazioni sulla configurazione di hub di notifica hello per servizio APN e la ricezione di notifica hello in un'app client, vedere [tooiOS le notifiche push di invio con gli hub di notifica di Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="be082-126">For more information on configuring hello notification hub for APNS and receiving hello notification in a client app, see [Sending push notifications tooiOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="be082-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="be082-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="be082-128">Per ulteriori informazioni sulla configurazione dell'hub di notifica hello ADM e la ricezione di notifica hello in un'app Kindle, vedere [Introduzione agli hub di notifica per le app Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="be082-128">For more information on configuring hello notification hub for ADM and receiving hello notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="be082-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="be082-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="be082-130">Firebase Cloud Messaging è hello nuova versione di GCM, è anche supportato.</span><span class="sxs-lookup"><span data-stu-id="be082-130">Firebase Cloud Messaging, which is hello new version of GCM, is also supported.</span></span> <span data-ttu-id="be082-131">Per ulteriori informazioni sulla configurazione di hub di notifica hello per GCM/FCM e la ricezione di notifica hello in un'applicazione client per Android, vedere [tooAndroid le notifiche push di invio con gli hub di notifica di Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="be082-131">For more information on configuring hello notification hub for GCM/FCM and receiving hello notification in an Android client app, see [Sending push notifications tooAndroid with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="be082-132">`wns` : [Servizio notifica Push Windows (WPNS)](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) indirizzato a piattaforme Windows.</span><span class="sxs-lookup"><span data-stu-id="be082-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="be082-133">Anche Windows Phone 8.1 e versioni successive sono supportati da WNS.</span><span class="sxs-lookup"><span data-stu-id="be082-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="be082-134">Per ulteriori informazioni sulla configurazione di hub di notifica hello per WNS e la ricezione di notifica hello in un'app della piattaforma UWP (Universal Windows), vedere [introduzione notifica hub per App universali di Windows Platform](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="be082-134">For more information on configuring hello notification hub for WNS and receiving hello notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="be082-135">`mpns` : [Servizio di notifica push Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="be082-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="be082-136">Questa piattaforma supporta piattaforme Windows Phone 8 e precedenti di Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="be082-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="be082-137">Per ulteriori informazioni sulla configurazione di hub di notifica hello per MPNS e notifica hello in un'app di Windows Phone, vedere [invio di notifiche push con hub di notifica di Azure in Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="be082-137">For more information on configuring hello notification hub for MPNS and receiving hello notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="be082-138">Function.json di esempio:</span><span class="sxs-lookup"><span data-stu-id="be082-138">Example function.json:</span></span>

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="be082-139">Configurazione della stringa di connessione dell'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="be082-139">Notification hub connection string setup</span></span>
<span data-ttu-id="be082-140">associazione di output toouse un hub di notifica, è necessario configurare la stringa di connessione hello per l'hub di hello.</span><span class="sxs-lookup"><span data-stu-id="be082-140">toouse a Notification hub output binding, you must configure hello connection string for hello hub.</span></span> <span data-ttu-id="be082-141">Questa operazione può essere eseguita su hello *integrazione* scheda selezionando l'hub di notifica o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="be082-141">This can be done on hello *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="be082-142">È inoltre possibile aggiungere manualmente una stringa di connessione per un hub esistente mediante l'aggiunta di una stringa di connessione per hello *DefaultFullSharedAccessSignature* tooyour hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="be082-142">You can also manually add a connection string for an existing hub by adding a connection string for hello *DefaultFullSharedAccessSignature* tooyour notification hub.</span></span> <span data-ttu-id="be082-143">La stringa di connessione fornisce l'accesso alle funzioni i messaggi di notifica toosend di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="be082-143">This connection string provides your function access permission toosend notification messages.</span></span> <span data-ttu-id="be082-144">Hello *DefaultFullSharedAccessSignature* valore stringa di connessione è possibile accedere da hello **chiavi** pulsante nel pannello principale di hello della risorsa hub di notifica in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be082-144">hello *DefaultFullSharedAccessSignature* connection string value can be accessed from hello **keys** button in hello main blade of your notification hub resource in hello Azure portal.</span></span> <span data-ttu-id="be082-145">toomanually aggiungere una stringa di connessione per l'hub, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="be082-145">toomanually add a connection string for your hub, use hello following steps:</span></span> 

1. <span data-ttu-id="be082-146">In hello **funzione app** blade di hello portale di Azure, fare clic su **funzione App Impostazioni > passare le impostazioni del servizio tooApp**.</span><span class="sxs-lookup"><span data-stu-id="be082-146">On hello **Function app** blade of hello Azure portal, click **Function App Settings > Go tooApp Service settings**.</span></span>
2. <span data-ttu-id="be082-147">In hello **impostazioni** pannello, fare clic su **le impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="be082-147">In hello **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="be082-148">Scorrere verso il basso toohello **impostazioni App** sezione e aggiungere una voce denominata per *DefaultFullSharedAccessSignature* valore per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="be082-148">Scroll down toohello **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="be082-149">Fare riferimento l'App nel nome della stringa hello associazioni di output.</span><span class="sxs-lookup"><span data-stu-id="be082-149">Reference your App setting string name in hello output bindings.</span></span> <span data-ttu-id="be082-150">Simile troppo**MyHubConnectionString** utilizzato nell'esempio hello precedente.</span><span class="sxs-lookup"><span data-stu-id="be082-150">Similar too**MyHubConnectionString** used in hello example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="be082-151">Notifiche native APNS con trigger in coda C#</span><span class="sxs-lookup"><span data-stu-id="be082-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="be082-152">Questo esempio viene illustrato come tipi toouse definite in hello [libreria hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend una notifica APNS nativa.</span><span class="sxs-lookup"><span data-stu-id="be082-152">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="be082-153">Notifiche native GCM con trigger in coda C#</span><span class="sxs-lookup"><span data-stu-id="be082-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="be082-154">Questo esempio viene illustrato come tipi toouse definite in hello [libreria hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend una notifica GCM nativa.</span><span class="sxs-lookup"><span data-stu-id="be082-154">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="be082-155">Notifiche native WNS con trigger in coda C#</span><span class="sxs-lookup"><span data-stu-id="be082-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="be082-156">Questo esempio viene illustrato come tipi toouse definite in hello [libreria hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend un WNS native di tipo avviso popup notifica.</span><span class="sxs-lookup"><span data-stu-id="be082-156">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="be082-157">Esempio di modello per i trigger timer Node.js</span><span class="sxs-lookup"><span data-stu-id="be082-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="be082-158">Questo esempio invia una notifica per la [registrazione di un modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenente `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="be082-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="be082-159">Esempio di modello per i trigger timer F#</span><span class="sxs-lookup"><span data-stu-id="be082-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="be082-160">Questo esempio invia una notifica per la [registrazione di un modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenente `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="be082-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="be082-161">Esempio di modello che utilizza un parametro di uscita</span><span class="sxs-lookup"><span data-stu-id="be082-161">Template example using an out parameter</span></span>
<span data-ttu-id="be082-162">In questo esempio invia una notifica un [registrazione modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) che contiene un `message` segnaposto nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="be082-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template.</span></span>

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="be082-163">Esempio di modello con funzione asincrona</span><span class="sxs-lookup"><span data-stu-id="be082-163">Template example with asynchronous function</span></span>
<span data-ttu-id="be082-164">I parametri di uscita non sono consentiti se si utilizza codice asincrono.</span><span class="sxs-lookup"><span data-stu-id="be082-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="be082-165">In questo caso utilizzare `IAsyncCollector` tooreturn la notifica di modello.</span><span class="sxs-lookup"><span data-stu-id="be082-165">In this case use `IAsyncCollector` tooreturn your template notification.</span></span> <span data-ttu-id="be082-166">Hello codice seguente è un esempio di codice hello precedente asincrono.</span><span class="sxs-lookup"><span data-stu-id="be082-166">hello following code is an asynchronous example of hello code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="be082-167">Esempio di modello che utilizza JSON</span><span class="sxs-lookup"><span data-stu-id="be082-167">Template example using JSON</span></span>
<span data-ttu-id="be082-168">In questo esempio invia una notifica un [registrazione modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) che contiene un `message` segnaposto nel modello di hello utilizzando una stringa JSON valida.</span><span class="sxs-lookup"><span data-stu-id="be082-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="be082-169">Esempio di modello utilizzando i tipi di librerie degli hub di notifica</span><span class="sxs-lookup"><span data-stu-id="be082-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="be082-170">Questo esempio viene illustrato come tipi toouse definite in hello [libreria hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="be082-170">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a><span data-ttu-id="be082-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be082-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

