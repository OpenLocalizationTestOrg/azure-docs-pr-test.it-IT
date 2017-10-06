---
title: aaaSending le notifiche push con hub di notifica di Azure e Node.js
description: Informazioni su come toouse gli hub di notifica toosend notifiche push da un'applicazione Node.js.
keywords: notifica push,notifiche push,push node.js,push ios
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Invio di notifiche push con Hub di notifica di Azure e Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Panoramica
> [!IMPORTANT]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

Questa guida illustra come toosend notifiche con l'aiuto di hello Azure degli hub di notifica push direttamente da un'applicazione Node.js. 

scenari di Hello trattati includono l'invio di tooapplications notifiche push su hello seguenti piattaforme:

* Android
* iOS
* Windows Phone
* Piattaforma UWP (Universal Windows Platform) 

Per ulteriori informazioni sull'hub di notifica, vedere hello [passaggi successivi](#next) sezione.

## <a name="what-are-notification-hubs"></a>Informazioni su Hub di notifica
Hub di notifica di Azure forniscono un'infrastruttura di facile utilizzo, multipiattaforma e scalabile per l'invio di dispositivi toomobile le notifiche push. Per informazioni dettagliate sull'infrastruttura del servizio hello, vedere hello [gli hub di notifica di Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) pagina.

## <a name="create-a-nodejs-application"></a>Creazione di un'applicazione Node.js
passaggio prima di Hello in questa esercitazione consiste nel creare una nuova applicazione Node.js vuota. Per istruzioni sulla creazione di un'applicazione Node.js, vedere [creare e distribuire un tooAzure di applicazione del sito Web Node.js][nodejswebsite], [servizio Cloud Node.js] [ Node.js Cloud Service] tramite Windows PowerShell, o [sito Web con WebMatrix].

## <a name="configure-your-application-toouse-notification-hubs"></a>Configurare gli hub di notifica tooUse dell'applicazione
toouse gli hub di notifica di Azure, è necessario toodownload e utilizzare hello Node.js [pacchetto azure](https://www.npmjs.com/package/azure), che include un set predefinito di librerie di supporto che comunicano con servizi REST di notifica push di hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)
1. Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Linux) e passare toohello cartella in cui viene creata l'applicazione vuota .
2. Tipo **npm installare Service bus di azure** nella finestra di comando hello.
3. È possibile eseguire manualmente hello **ls** o **dir** comando tooverify che un **nodo\_moduli** cartella è stata creata. All'interno di tale cartella, trovare hello **azure** pacchetto che contiene le librerie di hello necessarie tooaccess hello Hub di notifica.

> [!NOTE]
> Maggiori informazioni sull'installazione di NPM in ufficiale hello [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>Modulo di importazione hello
Utilizzando un editor di testo aggiungere hello seguente toohello cima hello **server.js** file dell'applicazione hello:

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Configurare una connessione all'Hub di notifica di Azure
Hello **NotificationHubService** oggetto consente di collaborare con gli hub di notifica. Hello codice seguente viene creata una **NotificationHubService** oggetto per l'hub nofication hello denominato **hubname**. Aggiungerlo parte superiore di hello di hello **server.js** file, dopo il modulo di hello istruzione tooimport hello azure:

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Hello connessione **connectionstring** valore può essere ottenuto dalla hello [portale Azure] eseguendo hello alla procedura seguente:

1. Nel riquadro di spostamento a sinistra di hello, fare clic su **Sfoglia**.
2. Selezionare **gli hub di notifica**e quindi hub hello trova desiderato toouse per esempio hello. È possibile fare riferimento toohello [esercitazione Windows Store introduttiva](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) se è necessario informazioni sulla creazione di un nuovo Hub di notifica.
3. Selezionare **Impostazioni**.
4. Fare clic su **Criteri di accesso**. Verranno visualizzate la stringhe di connessione di accesso completo e condiviso.

![Portale di Azure - Hub di notifica](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> È inoltre possibile recuperare stringa di connessione di hello utilizzando hello **Get-AzureSbNamespace** cmdlet forniti da [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello **Mostra lo spazio dei nomi Service bus di azure** con Hello [interfaccia della riga di comando di Azure (Azure CLI)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Architettura generale
Hello **NotificationHubService** oggetto espone hello istanze dell'oggetto per l'invio di dispositivi toospecific di notifiche push e le applicazioni seguenti:

* **Android** -utilizzare hello **GcmService** oggetto, che è disponibile all'indirizzo **notificationHubService.gcm**
* **iOS** -utilizzare hello **ApnsService** oggetto, che è possibile accedere al **notificationHubService.apns**
* **Windows Phone** -utilizzare hello **MpnsService** oggetto, che è disponibile all'indirizzo **notificationHubService.mpns**
* **Piattaforma UWP** -utilizzare hello **WnsService** oggetto, che è disponibile all'indirizzo **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Procedura: inviare le applicazioni di tooAndroid di notifiche push
Hello **GcmService** oggetto fornisce un **inviare** metodo che può essere utilizzati toosend push notifiche tooAndroid applicazioni. Hello **inviare** accetta hello seguenti parametri:

* **Tag** -hello identificatore tag. Se non viene specificato alcun tag, verrà inviata notifica hello client tooall.
* **Payload** -hello JSON del messaggio o il payload di stringa non elaborata.
* **Callback** -hello funzione di callback.

Per ulteriori informazioni sul formato di payload hello, vedere hello **Payload** sezione di hello [implementazione Server GCM](http://developer.android.com/google/gcm/server.html#payload) documento.

Hello codice seguente viene utilizzato hello **GcmService** istanza esposto da hello **NotificationHubService** toosend un tooall di notifica push registrato i client.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Procedura: inviare le applicazioni di tooiOS di notifiche push
Stesso come descritta in precedenza, le applicazioni Android hello **ApnsService** oggetto fornisce un **inviare** metodo che può essere utilizzati toosend push notifiche tooiOS applicazioni. Hello **inviare** accetta hello seguenti parametri:

* **Tag** -hello identificatore tag. Se non viene specificato alcun tag, verrà inviata notifica hello client tooall.
* **Payload** : hello JSON del messaggio o stringa payload.
* **Callback** -hello funzione di callback.

Per il formato di payload hello ulteriori informazioni, vedere hello **Payload di notifica** sezione di hello [locali e Guida per programmatori notifica Push](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) documento.

Hello codice seguente viene utilizzato hello **ApnsService** istanza esposto da hello **NotificationHubService** toosend un avviso messaggio tooall client:

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Procedura: inviare le applicazioni di Phone tooWindows di notifiche push
Hello **MpnsService** oggetto fornisce un **inviare** metodo che può essere utilizzato toosend push notifiche tooWindows applicazioni Phone. Hello **inviare** accetta hello seguenti parametri:

* **Tag** -hello identificatore tag. Se non viene specificato alcun tag, verrà inviata notifica hello client tooall.
* **Payload** -hello payload XML del messaggio.
* **TargetName** - `toast` per le notifiche di tipo avviso popup. `token` per le notifiche di tipo riquadro.
* **Classe di notifica** -hello priorità della notifica hello. Vedere hello **gli elementi dell'intestazione HTTP** sezione di hello [notifiche Push da un server](http://msdn.microsoft.com/library/hh221551.aspx) documento per i valori validi.
* **Options** : intestazioni delle richieste facoltative.
* **Callback** -hello funzione di callback.

Per un elenco di valido **TargetName**, **della classe di notifica** e opzioni di intestazione, estrarre hello [notifiche Push da un server](http://msdn.microsoft.com/library/hh221551.aspx) pagina.

Hello seguente codice di esempio utilizza hello **MpnsService** istanza esposto da hello **NotificationHubService** toosend una notifica push di tipo avviso popup:

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Procedura: inviare le applicazioni di Windows Platform (UWP) tooUniversal di notifiche push
Hello **WnsService** oggetto fornisce un **inviare** metodo che può essere utilizzati toosend push notifiche tooUniversal piattaforma Windows applicazioni.  Hello **inviare** accetta hello seguenti parametri:

* **Tag** -hello identificatore tag. Se non viene specificato alcun tag, verrà inviata notifica hello client tooall registrato.
* **Payload** -payload del messaggio hello XML.
* **Tipo** -hello tipo di notifica.
* **Options** : intestazioni delle richieste facoltative.
* **Callback** -hello funzione di callback.

Per un elenco dei valori validi per i tipi e le intestazioni delle richieste, vedere [Intestazioni delle richieste e delle risposte per il servizio di notifica push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Hello codice seguente viene utilizzato hello **WnsService** istanza esposto da hello **NotificationHubService** toosend un'app UWP tooa di tipo avviso popup push notifica:

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Passaggi successivi
frammenti di esempio Hello precedenti consentono si tooeasily compilazione servizio infrastruttura toodeliver push notifiche tooa vasta gamma di dispositivi. Ora che si sono appreso nozioni fondamentali di hello dell'utilizzo degli hub di notifica con node.js, seguire questi toolearn collegamenti con informazioni su come è possibile estendere ulteriormente queste funzionalità.

* Vedere hello riferimento MSDN per [gli hub di notifica di Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Visitare hello [Azure SDK per nodo] repository in GitHub per ulteriori esempi e i dettagli di implementazione.

[Azure SDK per nodo]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[sito Web con WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[portale Azure]: https://portal.azure.com
