---
title: Associazione di Hub di notifica in Funzioni di Azure | Documentazione Microsoft
description: Informazioni su come usare l'associazione di Hub di notifica di Azure in Funzioni di Azure.
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
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="b21ba-104">Associazione di output di Hub di notifica in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b21ba-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b21ba-105">Questo articolo illustra come configurare e scrivere il codice di associazioni di Hub di notifica in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b21ba-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="b21ba-106">Le funzioni possono inviare notifiche push usando un hub di notifica di Azure configurato con poche righe di codice.</span><span class="sxs-lookup"><span data-stu-id="b21ba-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="b21ba-107">L'hub di notifica di Azure tuttavia deve essere configurato per i servizi di notifiche della piattaforma (PNS) che si intende usare.</span><span class="sxs-lookup"><span data-stu-id="b21ba-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="b21ba-108">Per altre informazioni sulla configurazione di un hub di notifica di Azure e sullo sviluppo di applicazioni client che eseguono la registrazione per ricevere notifiche, vedere [Introduzione ad Hub di notifica per le app della piattaforma UWP (Universal Windows Platform)](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) e fare clic sulla piattaforma client di destinazione nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="b21ba-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="b21ba-109">Le notifiche inviate possono essere native o modello.</span><span class="sxs-lookup"><span data-stu-id="b21ba-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="b21ba-110">Le notifiche native sono indirizzate a una piattaforma di notifica specifica, come configurato nella `platform` proprietà dell'associazione di uscita.</span><span class="sxs-lookup"><span data-stu-id="b21ba-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="b21ba-111">È possibile utilizzare una notifica modello per indirizzare più piattaforme.</span><span class="sxs-lookup"><span data-stu-id="b21ba-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="b21ba-112">Associazione delle proprietà di uscita dell'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="b21ba-112">Notification hub output binding properties</span></span>
<span data-ttu-id="b21ba-113">Il file function.json specifica le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="b21ba-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="b21ba-114">`name` : nome della variabile usato nel codice della funzione per il messaggio dell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="b21ba-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="b21ba-115">`type` : deve essere impostato su *"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="b21ba-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="b21ba-116">`tagExpression` : le espressioni tag consentono di specificare che le notifiche devono essere recapitate a un set di dispositivi che hanno eseguito la registrazione per ricevere le notifiche corrispondenti all'espressione tag.</span><span class="sxs-lookup"><span data-stu-id="b21ba-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="b21ba-117">Per altre informazioni, vedere [Routing ed espressioni tag](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="b21ba-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="b21ba-118">`hubName` : nome della risorsa dell'hub di notifica nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b21ba-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="b21ba-119">`connection` : questa stringa di connessione deve essere una stringa di connessione dell' **impostazione dell'applicazione** configurata sul valore *DefaultFullSharedAccessSignature* per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="b21ba-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="b21ba-120">`direction` : deve essere impostato su *"out"*.</span><span class="sxs-lookup"><span data-stu-id="b21ba-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="b21ba-121">`platform` : la piattaforma delle proprietà indica la piattaforma di notifica a cui è indirizzata la notifica.</span><span class="sxs-lookup"><span data-stu-id="b21ba-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="b21ba-122">Deve essere uno dei valori seguenti: </span><span class="sxs-lookup"><span data-stu-id="b21ba-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="b21ba-123">Per impostazione predefinita, se la proprietà della piattaforma viene omessa dall'associazione di output, possono essere usate le notifiche del modello per indirizzarsi a qualsiasi piattaforma configurata nell'hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="b21ba-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="b21ba-124">Per ulteriori informazioni sull'utilizzo dei modelli in generale per inviare notifiche tra piattaforme con un hub di notifica di Azure, vedere [Modelli](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="b21ba-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="b21ba-125">`apns` : Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="b21ba-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="b21ba-126">Per ulteriori informazioni su come configurare l'hub di notifica per APN e ricevere la notifica in un'applicazione client, vedere [Invio di notifiche push a iOS con hub di notifica di Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="b21ba-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="b21ba-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="b21ba-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="b21ba-128">Per ulteriori informazioni su come configurare l'hub di notifica per ADM e ricevere la notifica in un'applicazione Kindle, vedere [Introduzione agli hub di notifica per le applicazioni Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="b21ba-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="b21ba-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="b21ba-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="b21ba-130">È supportato anche Firebase Cloud Messaging, la nuova versione di GCM.</span><span class="sxs-lookup"><span data-stu-id="b21ba-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="b21ba-131">Per ulteriori informazioni su come configurare l'hub di notifica per GCM/FCM e ricevere la notifica in un'applicazione client Android, vedere [Invio di notifiche push ad Android con hub di notifica di Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="b21ba-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="b21ba-132">`wns` : [Servizio notifica Push Windows (WPNS)](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) indirizzato a piattaforme Windows.</span><span class="sxs-lookup"><span data-stu-id="b21ba-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="b21ba-133">Anche Windows Phone 8.1 e versioni successive sono supportati da WNS.</span><span class="sxs-lookup"><span data-stu-id="b21ba-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="b21ba-134">Per ulteriori informazioni su come configurare l'hub di notifica per WNS e ricevere la notifica in un'applicazione Universal Windows Platform (UWP), vedere [Introduzione agli hub di notifica per le applicazioni Universal Windows Platform](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="b21ba-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="b21ba-135">`mpns` : [Servizio di notifica push Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="b21ba-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="b21ba-136">Questa piattaforma supporta piattaforme Windows Phone 8 e precedenti di Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b21ba-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="b21ba-137">Per ulteriori informazioni su come configurare l'hub di notifica per APN e ricevere la notifica in un'applicazione Windows Phone, vedere [Invio di notifiche push con hub di notifica di Azure su Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="b21ba-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="b21ba-138">Function.json di esempio:</span><span class="sxs-lookup"><span data-stu-id="b21ba-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="b21ba-139">Configurazione della stringa di connessione dell'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="b21ba-139">Notification hub connection string setup</span></span>
<span data-ttu-id="b21ba-140">Per usare un'associazione di output dell'hub di notifica, è necessario configurare la stringa di connessione per l'hub.</span><span class="sxs-lookup"><span data-stu-id="b21ba-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="b21ba-141">Nella scheda *Integra* è possibile selezionare quindi l'hub di notifica o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="b21ba-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="b21ba-142">È anche possibile aggiungere manualmente una stringa di connessione per un hub esistente aggiungendo una stringa di connessione per *DefaultFullSharedAccessSignature* all'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="b21ba-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="b21ba-143">Questa stringa di connessione fornisce l'autorizzazione di accesso alla funzione per inviare messaggi di notifica.</span><span class="sxs-lookup"><span data-stu-id="b21ba-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="b21ba-144">È possibile accedere al valore della stringa di connessione *DefaultFullSharedAccessSignature* dal pulsante **chiavi** nel pannello principale della risorsa dell'hub di notifica nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b21ba-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="b21ba-145">Per aggiungere manualmente una stringa di connessione per l'hub, usare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b21ba-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="b21ba-146">Nel pannello **App per le funzioni** del portale di Azure fare clic su **Impostazioni dell'app per le funzioni > Passa a Impostazioni del servizio app**.</span><span class="sxs-lookup"><span data-stu-id="b21ba-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="b21ba-147">Nel pannello **Impostazioni** fare clic su **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="b21ba-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="b21ba-148">Scorrere verso il basso fino alla sezione **Impostazioni app** e aggiungere una voce denominata per il valore *DefaultFullSharedAccessSignature* per l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="b21ba-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="b21ba-149">Fare riferimento al nome della stringa di impostazione app nelle associazioni di output.</span><span class="sxs-lookup"><span data-stu-id="b21ba-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="b21ba-150">È simile a **MyHubConnectionString** usato nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="b21ba-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="b21ba-151">Notifiche native APNS con trigger in coda C#</span><span class="sxs-lookup"><span data-stu-id="b21ba-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="b21ba-152">Questo esempio illustra come usare i tipi definiti nella [libreria di Hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) per inviare una notifica APNS nativa.</span><span class="sxs-lookup"><span data-stu-id="b21ba-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="b21ba-153">Notifiche native GCM con trigger in coda C#</span><span class="sxs-lookup"><span data-stu-id="b21ba-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="b21ba-154">Questo esempio illustra come usare i tipi definiti nella [libreria di Hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) per inviare una notifica GCM nativa.</span><span class="sxs-lookup"><span data-stu-id="b21ba-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="b21ba-155">Notifiche native WNS con trigger in coda C#</span><span class="sxs-lookup"><span data-stu-id="b21ba-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="b21ba-156">Questo esempio illustra come usare i tipi definiti nella [libreria di Hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) per inviare una notifica WNS popup nativa.</span><span class="sxs-lookup"><span data-stu-id="b21ba-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
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
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="b21ba-157">Esempio di modello per i trigger timer Node.js</span><span class="sxs-lookup"><span data-stu-id="b21ba-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="b21ba-158">Questo esempio invia una notifica per la [registrazione di un modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenente `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="b21ba-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="b21ba-159">Esempio di modello per i trigger timer F#</span><span class="sxs-lookup"><span data-stu-id="b21ba-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="b21ba-160">Questo esempio invia una notifica per la [registrazione di un modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenente `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="b21ba-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="b21ba-161">Esempio di modello che utilizza un parametro di uscita</span><span class="sxs-lookup"><span data-stu-id="b21ba-161">Template example using an out parameter</span></span>
<span data-ttu-id="b21ba-162">Questo esempio invia una notifica per la [registrazione di un modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenente `message` un segnaposto nel modello.</span><span class="sxs-lookup"><span data-stu-id="b21ba-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="b21ba-163">Esempio di modello con funzione asincrona</span><span class="sxs-lookup"><span data-stu-id="b21ba-163">Template example with asynchronous function</span></span>
<span data-ttu-id="b21ba-164">I parametri di uscita non sono consentiti se si utilizza codice asincrono.</span><span class="sxs-lookup"><span data-stu-id="b21ba-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="b21ba-165">In questo caso utilizzare `IAsyncCollector` per tornare alla notifica modello.</span><span class="sxs-lookup"><span data-stu-id="b21ba-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="b21ba-166">Il codice seguente è un esempio asincrono del codice precedente.</span><span class="sxs-lookup"><span data-stu-id="b21ba-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="b21ba-167">Esempio di modello che utilizza JSON</span><span class="sxs-lookup"><span data-stu-id="b21ba-167">Template example using JSON</span></span>
<span data-ttu-id="b21ba-168">Questo esempio invia una notifica per la [registrazione di un modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenente `message` un segnaposto nel modello tramite una stringa JSON valida.</span><span class="sxs-lookup"><span data-stu-id="b21ba-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="b21ba-169">Esempio di modello utilizzando i tipi di librerie degli hub di notifica</span><span class="sxs-lookup"><span data-stu-id="b21ba-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="b21ba-170">Questo esempio illustra come usare i tipi definiti nella [libreria di Hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="b21ba-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="b21ba-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b21ba-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

