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
# <a name="azure-functions-notification-hub-output-binding"></a>Associazione di output di Hub di notifica in Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo viene illustrato come associazioni di Hub di notifica di Azure tooconfigure e codice nelle funzioni di Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Le funzioni possono inviare notifiche push usando un hub di notifica di Azure configurato con poche righe di codice. Tuttavia, hello Hub di notifica di Azure deve essere configurato per la piattaforma notifiche servizi (PNS) si desidera toouse hello. Per ulteriori informazioni su come configurare un Hub di notifica di Azure e lo sviluppo di applicazioni client che registrano tooreceive notifiche, vedere [Introduzione agli hub di notifica](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) e scegliere la piattaforma di destinazione client in hello In alto.

inviare le notifiche di Hello possono essere notifiche native o notifiche di modello. Notifiche native una piattaforma notifica specifica come configurato nella hello `platform` proprietà di hello associazione di output. Una notifica modello può essere utilizzato tootarget più piattaforme.   

## <a name="notification-hub-output-binding-properties"></a>Associazione delle proprietà di uscita dell'hub di notifica
file function.json Hello fornisce hello le proprietà seguenti:

* `name`: Nome variabile utilizzato nel codice di funzione per il messaggio hub di notifica hello.
* `type`: deve essere impostato troppo*"hub di notifica"*.
* `tagExpression`: Espressioni tag consentono di toospecify che tooa set di dispositivi che hanno registrato notifiche tooreceive che corrispondano all'espressione tag hello recapitare le notifiche.  Per altre informazioni, vedere [Routing ed espressioni tag](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Nome della risorsa di hub di notifica di hello in hello portale di Azure.
* `connection`: La stringa di connessione deve essere un **impostazione dell'applicazione** stringa di connessione impostata toohello *DefaultFullSharedAccessSignature* valore per l'hub di notifica.
* `direction`: deve essere impostato troppo*"out"*. 
* `platform`: proprietà piattaforma hello indica piattaforma notifica hello destinazione della notifica. Deve essere uno dei seguenti valori hello:
  * Per impostazione predefinita, se proprietà piattaforma hello viene omessa dall'output di hello associazione, le notifiche di modello possono essere utilizzato tootarget qualsiasi piattaforma configurata nel hello Hub di notifica di Azure. Per ulteriori informazioni sull'utilizzo dei modelli in generale toosend cross platform notifiche con un Hub di notifica di Azure, vedere [modelli](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns` : Apple Push Notification Service. Per ulteriori informazioni sulla configurazione di hub di notifica hello per servizio APN e la ricezione di notifica hello in un'app client, vedere [tooiOS le notifiche push di invio con gli hub di notifica di Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging). Per ulteriori informazioni sulla configurazione dell'hub di notifica hello ADM e la ricezione di notifica hello in un'app Kindle, vedere [Introduzione agli hub di notifica per le app Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/). Firebase Cloud Messaging è hello nuova versione di GCM, è anche supportato. Per ulteriori informazioni sulla configurazione di hub di notifica hello per GCM/FCM e la ricezione di notifica hello in un'applicazione client per Android, vedere [tooAndroid le notifiche push di invio con gli hub di notifica di Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns` : [Servizio notifica Push Windows (WPNS)](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) indirizzato a piattaforme Windows. Anche Windows Phone 8.1 e versioni successive sono supportati da WNS. Per ulteriori informazioni sulla configurazione di hub di notifica hello per WNS e la ricezione di notifica hello in un'app della piattaforma UWP (Universal Windows), vedere [introduzione notifica hub per App universali di Windows Platform](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns` : [Servizio di notifica push Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx). Questa piattaforma supporta piattaforme Windows Phone 8 e precedenti di Windows Phone. Per ulteriori informazioni sulla configurazione di hub di notifica hello per MPNS e notifica hello in un'app di Windows Phone, vedere [invio di notifiche push con hub di notifica di Azure in Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

Function.json di esempio:

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

## <a name="notification-hub-connection-string-setup"></a>Configurazione della stringa di connessione dell'hub di notifica
associazione di output toouse un hub di notifica, è necessario configurare la stringa di connessione hello per l'hub di hello. Questa operazione può essere eseguita su hello *integrazione* scheda selezionando l'hub di notifica o crearne uno nuovo. 

È inoltre possibile aggiungere manualmente una stringa di connessione per un hub esistente mediante l'aggiunta di una stringa di connessione per hello *DefaultFullSharedAccessSignature* tooyour hub di notifica. La stringa di connessione fornisce l'accesso alle funzioni i messaggi di notifica toosend di autorizzazione. Hello *DefaultFullSharedAccessSignature* valore stringa di connessione è possibile accedere da hello **chiavi** pulsante nel pannello principale di hello della risorsa hub di notifica in hello portale di Azure. toomanually aggiungere una stringa di connessione per l'hub, utilizzare hello alla procedura seguente: 

1. In hello **funzione app** blade di hello portale di Azure, fare clic su **funzione App Impostazioni > passare le impostazioni del servizio tooApp**.
2. In hello **impostazioni** pannello, fare clic su **le impostazioni dell'applicazione**.
3. Scorrere verso il basso toohello **impostazioni App** sezione e aggiungere una voce denominata per *DefaultFullSharedAccessSignature* valore per l'hub di notifica.
4. Fare riferimento l'App nel nome della stringa hello associazioni di output. Simile troppo**MyHubConnectionString** utilizzato nell'esempio hello precedente.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>Notifiche native APNS con trigger in coda C#
Questo esempio viene illustrato come tipi toouse definite in hello [libreria hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend una notifica APNS nativa. 

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

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>Notifiche native GCM con trigger in coda C#
Questo esempio viene illustrato come tipi toouse definite in hello [libreria hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend una notifica GCM nativa. 

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

## <a name="wns-native-notifications-with-c-queue-triggers"></a>Notifiche native WNS con trigger in coda C#
Questo esempio viene illustrato come tipi toouse definite in hello [libreria hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend un WNS native di tipo avviso popup notifica. 

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

## <a name="template-example-for-nodejs-timer-triggers"></a>Esempio di modello per i trigger timer Node.js
Questo esempio invia una notifica per la [registrazione di un modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenente `location` e `message`.

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

## <a name="template-example-for-f-timer-triggers"></a>Esempio di modello per i trigger timer F#
Questo esempio invia una notifica per la [registrazione di un modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenente `location` e `message`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>Esempio di modello che utilizza un parametro di uscita
In questo esempio invia una notifica un [registrazione modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) che contiene un `message` segnaposto nel modello di hello.

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

## <a name="template-example-with-asynchronous-function"></a>Esempio di modello con funzione asincrona
I parametri di uscita non sono consentiti se si utilizza codice asincrono. In questo caso utilizzare `IAsyncCollector` tooreturn la notifica di modello. Hello codice seguente è un esempio di codice hello precedente asincrono. 

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

## <a name="template-example-using-json"></a>Esempio di modello che utilizza JSON
In questo esempio invia una notifica un [registrazione modello](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) che contiene un `message` segnaposto nel modello di hello utilizzando una stringa JSON valida.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Esempio di modello utilizzando i tipi di librerie degli hub di notifica
Questo esempio viene illustrato come tipi toouse definite in hello [libreria hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

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

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

