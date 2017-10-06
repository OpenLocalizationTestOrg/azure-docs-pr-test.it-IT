---
title: aaaHow toouse gli hub di notifica con Python
description: Informazioni su come toouse gli hub di notifica di Azure da un server back-end di Python.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a>Come toouse gli hub di notifica da Python
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

È possibile accedere a tutte le funzionalità di hub di notifica da un server back-end utilizzabile come Java, PHP, Python o Ruby utilizzando l'interfaccia REST di Hub di notifica di hello come descritto nell'argomento MSDN hello [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx).

> [!NOTE]
> Questo è un esempio di implementazione di riferimento per l'implementazione invia notifica hello in Python e non hello ufficialmente supportata SDK Python Hub di notifiche.
> 
> L'esempio è scritto in Python 3.4.
> 
> 

Questo argomento illustra come:

* Compilare un client REST per le funzionalità di Hub di notifica in Python.
* Inviare notifiche tramite hello Python interfaccia toohello le API REST di Hub di notifica. 
* Ottenere un dump di richiesta/risposta HTTP REST hello a scopo didattico/debug. 

È possibile seguire hello [esercitazione introduttiva Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) per la piattaforma per dispositivi mobili scelta, l'implementazione di parte di back-end hello in Python.

> [!NOTE]
> ambito Hello dell'esempio hello è solo le notifiche toosend limitato e non è una gestione di registrazione.
> 
> 

## <a name="client-interface"></a>Interfaccia del client
interfaccia del client principale Hello può fornire hello stessi metodi disponibili in hello [.NET SDK hub di notifica](http://msdn.microsoft.com/library/jj933431.aspx). In questo modo si toodirectly fornito dalla community di hello in hello e convertire tutte le esercitazioni di hello e gli esempi disponibili sul sito internet.

È possibile trovare tutto il codice hello disponibile in hello [esempio wrapper Python REST].

Toocreate, ad esempio, un client:

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

toosend Windows di tipo avviso popup notifica:

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>Implementazione
Se è stato non è già fatto, seguire il nostro [esercitazione introduttiva Get] backup toohello ultima sezione in cui occorre tooimplement hello back-end.

Tutti hello tooimplement dettagli sono disponibili wrapper REST completo nel [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). In questa sezione descrive l'implementazione di Python hello di hello passaggi principali necessari tooaccess endpoint REST degli hub di notifica e inviare notifiche

1. Analizzare la stringa di connessione hello
2. Generare il token di autorizzazione hello
3. Inviare una notifica tramite l'API REST HTTP

### <a name="parse-hello-connection-string"></a>Analizzare la stringa di connessione hello
Di seguito è l'implementazione hello client, il cui costruttore analizza la stringa di connessione hello la classe principale hello:

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a>Creare il token di sicurezza
sono disponibili dettagli Hello di creazione dei token di sicurezza hello [qui](http://msdn.microsoft.com/library/dn495627.aspx).
i metodi seguenti Hello avere toobe aggiunto toohello **hub di notifica** token hello toocreate della classe dipende dall'URI della richiesta corrente hello e le credenziali di hello estratte dalla stringa di connessione hello hello.

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a>Inviare una notifica tramite l'API REST HTTP
Definire innanzitutto una classe che rappresenta la notifica.

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

Questa classe è un contenitore per un corpo di notifica nativo oppure un set di proprietà nel caso di una notifica modello e un set di intestazioni che contengono il formato (modello o piattaforma nativa) e proprietà specifiche della piattaforma (come la proprietà di scadenza e le intestazioni WNS di Apple).

Consultare toohello [documentazione delle API REST degli hub di notifica](http://msdn.microsoft.com/library/dn495827.aspx) e hello formati delle piattaforme di notifica specifica per tutte le opzioni disponibili di hello.

Ora a questa classe, è possibile scrivere hello trasmissione metodi di notifica all'interno di hello **hub di notifica** classe.

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

Hello sopra i metodi di inviare un endpoint di /messages toohello richiesta HTTP POST di hub di notifica, notifica hello toosend di intestazioni e corpo corretto hello.

### <a name="using-debug-property-tooenable-detailed-logging"></a>Tooenable di proprietà di debug mediante la registrazione dettagliata
L'abilitazione di proprietà di debug durante l'inizializzazione di hello Hub di notifica verranno scritte le informazioni di registrazione dettagliate su hello HTTP richiesta e dump di risposta, nonché il messaggio di notifica dettagliato Invia risultato. Abbiamo aggiunto di recente questa proprietà chiamata [TestSend gli hub di notifica proprietà](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) che restituisce informazioni dettagliate sul risultato di trasmissione di hello notifica. toouse, inizializzare con hello seguenti:

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

richiesta di invio di Hub di notifica Hello URL HTTP viene aggiunto con il parametro querystring "test" di conseguenza. 

## <a name="complete-tutorial"></a>Esercitazione hello completo
Ora è possibile completare l'esercitazione Introduzione hello inviando notifiche hello da un server back-end di Python.

Inizializzare il client di hub di notifica (sostituire nome hub e di stringa di connessione hello come indicato nell'hello [esercitazione introduttiva Get]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

Aggiungere codice di trasmissione hello a seconda della piattaforma per dispositivi mobili di destinazione. In questo esempio aggiunge anche tooenable di metodi a livello superiore l'invio di notifiche in base alla piattaforma hello, ad esempio send_windows_notification per windows. send_apple_notification (per apple) e così via. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows Store e Windows Phone 8.1 (non Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 e 8.1 Silverlight
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

Eseguendo il codice Python dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.

## <a name="examples"></a>Esempi:
### <a name="enabling-debug-property"></a>Abilitazione della proprietà di debug
Quando si abilita il flag di debug durante l'inizializzazione di hello hub di notifica viene visualizzata dettagliate dump di richiesta e risposta HTTP, nonché NotificationOutcome seguente hello in cui è possibile comprendere quali HTTP e le intestazioni HTTP vengono passate nella richiesta di hello risposta ricevuta dal hello Hub di notifica:![][1]

verrà visualizzato il risultato dettagliato di Hub di notifica, ad esempio: 

* Quando il messaggio hello viene correttamente inviato toohello Push Notification Service. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* Se si sono verificati Nessuna destinazione trovata per le notifiche push, probabilmente sarà toosee seguente di hello in risposta hello (che indica che non vi sono Nessuna registrazione trovata notifica hello toodeliver probabilmente perché le registrazioni hello presenti alcuni tag non corrispondenti)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>Trasmissione tooWindows notifica di tipo avviso popup
Si noti intestazioni hello ottengano inviate quando si invia un client di tooWindows notifica di tipo avviso popup broadcast. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>Inviare la notifica specificando un tag (o un'espressione tag)
Intestazione di tag HTTP hello si noti che viene aggiunto toohello HTTP richiesta (nell'esempio hello seguente, viene inviato hello tooregistrations solo di notifica con payload 'sportivi')

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>Inviare la notifica specificando più tag
Si noti come intestazione HTTP tag hello cambia quando vengono inviati più tag. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>Notifica basata su modelli
Si noti che hello formato HTTP modifiche di intestazione e corpo payload hello viene inviato come parte del corpo della richiesta HTTP hello:

**Lato client - modello registrato**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**Sul lato server - invio di payload hello**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>Passaggi successivi
In questo argomento illustrato come toocreate un semplice Python REST client per gli hub di notifica. A questo punto è possibile:

* Scaricare hello completo [esempio wrapper Python REST], che contiene tutto il codice hello precedente.
* Ulteriori informazioni sugli hub di notifica tag funzionalità in hello [esercitazione delle ultime notizie]
* Ulteriori informazioni sulla funzionalità di modelli di hub di notifica in hello [esercitazione notizie di localizzazione]

<!-- URLs -->
[esempio wrapper Python REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[esercitazione introduttiva Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[esercitazione delle ultime notizie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[esercitazione notizie di localizzazione]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

