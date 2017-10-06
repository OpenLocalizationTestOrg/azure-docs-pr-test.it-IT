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
# <a name="how-toouse-notification-hubs-from-python"></a><span data-ttu-id="314ae-103">Come toouse gli hub di notifica da Python</span><span class="sxs-lookup"><span data-stu-id="314ae-103">How toouse Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="314ae-104">È possibile accedere a tutte le funzionalità di hub di notifica da un server back-end utilizzabile come Java, PHP, Python o Ruby utilizzando l'interfaccia REST di Hub di notifica di hello come descritto nell'argomento MSDN hello [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="314ae-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="314ae-105">Questo è un esempio di implementazione di riferimento per l'implementazione invia notifica hello in Python e non hello ufficialmente supportata SDK Python Hub di notifiche.</span><span class="sxs-lookup"><span data-stu-id="314ae-105">This is a sample reference implementation for implementing hello notification sends in Python and is not hello officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="314ae-106">L'esempio è scritto in Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="314ae-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="314ae-107">Questo argomento illustra come:</span><span class="sxs-lookup"><span data-stu-id="314ae-107">In this topic we show how to:</span></span>

* <span data-ttu-id="314ae-108">Compilare un client REST per le funzionalità di Hub di notifica in Python.</span><span class="sxs-lookup"><span data-stu-id="314ae-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="314ae-109">Inviare notifiche tramite hello Python interfaccia toohello le API REST di Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="314ae-109">Send notifications using hello Python interface toohello Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="314ae-110">Ottenere un dump di richiesta/risposta HTTP REST hello a scopo didattico/debug.</span><span class="sxs-lookup"><span data-stu-id="314ae-110">Get a dump of hello HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="314ae-111">È possibile seguire hello [esercitazione introduttiva Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) per la piattaforma per dispositivi mobili scelta, l'implementazione di parte di back-end hello in Python.</span><span class="sxs-lookup"><span data-stu-id="314ae-111">You can follow hello [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing hello back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="314ae-112">ambito Hello dell'esempio hello è solo le notifiche toosend limitato e non è una gestione di registrazione.</span><span class="sxs-lookup"><span data-stu-id="314ae-112">hello scope of hello sample is only limited toosend notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="314ae-113">Interfaccia del client</span><span class="sxs-lookup"><span data-stu-id="314ae-113">Client interface</span></span>
<span data-ttu-id="314ae-114">interfaccia del client principale Hello può fornire hello stessi metodi disponibili in hello [.NET SDK hub di notifica](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="314ae-114">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="314ae-115">In questo modo si toodirectly fornito dalla community di hello in hello e convertire tutte le esercitazioni di hello e gli esempi disponibili sul sito internet.</span><span class="sxs-lookup"><span data-stu-id="314ae-115">This will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="314ae-116">È possibile trovare tutto il codice hello disponibile in hello [esempio wrapper Python REST].</span><span class="sxs-lookup"><span data-stu-id="314ae-116">You can find all hello code available in hello [Python REST wrapper sample].</span></span>

<span data-ttu-id="314ae-117">Toocreate, ad esempio, un client:</span><span class="sxs-lookup"><span data-stu-id="314ae-117">For example, toocreate a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="314ae-118">toosend Windows di tipo avviso popup notifica:</span><span class="sxs-lookup"><span data-stu-id="314ae-118">toosend a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="314ae-119">Implementazione</span><span class="sxs-lookup"><span data-stu-id="314ae-119">Implementation</span></span>
<span data-ttu-id="314ae-120">Se è stato non è già fatto, seguire il nostro [esercitazione introduttiva Get] backup toohello ultima sezione in cui occorre tooimplement hello back-end.</span><span class="sxs-lookup"><span data-stu-id="314ae-120">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>

<span data-ttu-id="314ae-121">Tutti hello tooimplement dettagli sono disponibili wrapper REST completo nel [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="314ae-121">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="314ae-122">In questa sezione descrive l'implementazione di Python hello di hello passaggi principali necessari tooaccess endpoint REST degli hub di notifica e inviare notifiche</span><span class="sxs-lookup"><span data-stu-id="314ae-122">In this section we will describe hello Python implementation of hello main steps required tooaccess Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="314ae-123">Analizzare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="314ae-123">Parse hello connection string</span></span>
2. <span data-ttu-id="314ae-124">Generare il token di autorizzazione hello</span><span class="sxs-lookup"><span data-stu-id="314ae-124">Generate hello authorization token</span></span>
3. <span data-ttu-id="314ae-125">Inviare una notifica tramite l'API REST HTTP</span><span class="sxs-lookup"><span data-stu-id="314ae-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="314ae-126">Analizzare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="314ae-126">Parse hello connection string</span></span>
<span data-ttu-id="314ae-127">Di seguito è l'implementazione hello client, il cui costruttore analizza la stringa di connessione hello la classe principale hello:</span><span class="sxs-lookup"><span data-stu-id="314ae-127">Here is hello main class implementing hello client, whose constructor parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="314ae-128">Creare il token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="314ae-128">Create security token</span></span>
<span data-ttu-id="314ae-129">sono disponibili dettagli Hello di creazione dei token di sicurezza hello [qui](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="314ae-129">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="314ae-130">i metodi seguenti Hello avere toobe aggiunto toohello **hub di notifica** token hello toocreate della classe dipende dall'URI della richiesta corrente hello e le credenziali di hello estratte dalla stringa di connessione hello hello.</span><span class="sxs-lookup"><span data-stu-id="314ae-130">hello following methods have toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="314ae-131">Inviare una notifica tramite l'API REST HTTP</span><span class="sxs-lookup"><span data-stu-id="314ae-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="314ae-132">Definire innanzitutto una classe che rappresenta la notifica.</span><span class="sxs-lookup"><span data-stu-id="314ae-132">First, let use define a class representing a notification.</span></span>

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

<span data-ttu-id="314ae-133">Questa classe è un contenitore per un corpo di notifica nativo oppure un set di proprietà nel caso di una notifica modello e un set di intestazioni che contengono il formato (modello o piattaforma nativa) e proprietà specifiche della piattaforma (come la proprietà di scadenza e le intestazioni WNS di Apple).</span><span class="sxs-lookup"><span data-stu-id="314ae-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="314ae-134">Consultare toohello [documentazione delle API REST degli hub di notifica](http://msdn.microsoft.com/library/dn495827.aspx) e hello formati delle piattaforme di notifica specifica per tutte le opzioni disponibili di hello.</span><span class="sxs-lookup"><span data-stu-id="314ae-134">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="314ae-135">Ora a questa classe, è possibile scrivere hello trasmissione metodi di notifica all'interno di hello **hub di notifica** classe.</span><span class="sxs-lookup"><span data-stu-id="314ae-135">Now with this class, we can write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="314ae-136">Hello sopra i metodi di inviare un endpoint di /messages toohello richiesta HTTP POST di hub di notifica, notifica hello toosend di intestazioni e corpo corretto hello.</span><span class="sxs-lookup"><span data-stu-id="314ae-136">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

### <a name="using-debug-property-tooenable-detailed-logging"></a><span data-ttu-id="314ae-137">Tooenable di proprietà di debug mediante la registrazione dettagliata</span><span class="sxs-lookup"><span data-stu-id="314ae-137">Using debug property tooenable detailed logging</span></span>
<span data-ttu-id="314ae-138">L'abilitazione di proprietà di debug durante l'inizializzazione di hello Hub di notifica verranno scritte le informazioni di registrazione dettagliate su hello HTTP richiesta e dump di risposta, nonché il messaggio di notifica dettagliato Invia risultato.</span><span class="sxs-lookup"><span data-stu-id="314ae-138">Enabling debug property while initializing hello Notification Hub will write out detailed logging information about hello HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="314ae-139">Abbiamo aggiunto di recente questa proprietà chiamata [TestSend gli hub di notifica proprietà](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) che restituisce informazioni dettagliate sul risultato di trasmissione di hello notifica.</span><span class="sxs-lookup"><span data-stu-id="314ae-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about hello notification send outcome.</span></span> <span data-ttu-id="314ae-140">toouse, inizializzare con hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="314ae-140">toouse it - initialize using hello following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="314ae-141">richiesta di invio di Hub di notifica Hello URL HTTP viene aggiunto con il parametro querystring "test" di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="314ae-141">hello Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="314ae-142"><a name="complete-tutorial"></a>Esercitazione hello completo</span><span class="sxs-lookup"><span data-stu-id="314ae-142"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="314ae-143">Ora è possibile completare l'esercitazione Introduzione hello inviando notifiche hello da un server back-end di Python.</span><span class="sxs-lookup"><span data-stu-id="314ae-143">Now you can complete hello Get Started tutorial by sending hello notification from a Python back-end.</span></span>

<span data-ttu-id="314ae-144">Inizializzare il client di hub di notifica (sostituire nome hub e di stringa di connessione hello come indicato nell'hello [esercitazione introduttiva Get]):</span><span class="sxs-lookup"><span data-stu-id="314ae-144">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="314ae-145">Aggiungere codice di trasmissione hello a seconda della piattaforma per dispositivi mobili di destinazione.</span><span class="sxs-lookup"><span data-stu-id="314ae-145">Then add hello send code depending on your target mobile platform.</span></span> <span data-ttu-id="314ae-146">In questo esempio aggiunge anche tooenable di metodi a livello superiore l'invio di notifiche in base alla piattaforma hello, ad esempio send_windows_notification per windows. send_apple_notification (per apple) e così via.</span><span class="sxs-lookup"><span data-stu-id="314ae-146">This sample also adds higher level methods tooenable sending notifications based on hello platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="314ae-147">Windows Store e Windows Phone 8.1 (non Silverlight)</span><span class="sxs-lookup"><span data-stu-id="314ae-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="314ae-148">Windows Phone 8.0 e 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="314ae-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="314ae-149">iOS</span><span class="sxs-lookup"><span data-stu-id="314ae-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="314ae-150">Android</span><span class="sxs-lookup"><span data-stu-id="314ae-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="314ae-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="314ae-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="314ae-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="314ae-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="314ae-153">Eseguendo il codice Python dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="314ae-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="314ae-154">Esempi:</span><span class="sxs-lookup"><span data-stu-id="314ae-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="314ae-155">Abilitazione della proprietà di debug</span><span class="sxs-lookup"><span data-stu-id="314ae-155">Enabling debug property</span></span>
<span data-ttu-id="314ae-156">Quando si abilita il flag di debug durante l'inizializzazione di hello hub di notifica viene visualizzata dettagliate dump di richiesta e risposta HTTP, nonché NotificationOutcome seguente hello in cui è possibile comprendere quali HTTP e le intestazioni HTTP vengono passate nella richiesta di hello risposta ricevuta dal hello Hub di notifica:![][1]</span><span class="sxs-lookup"><span data-stu-id="314ae-156">When you enable debug flag while initializing hello NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like hello following where you can understand what HTTP headers are passed in hello request and what HTTP response was received from hello Notification Hub: ![][1]</span></span>

<span data-ttu-id="314ae-157">verrà visualizzato il risultato dettagliato di Hub di notifica, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="314ae-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="314ae-158">Quando il messaggio hello viene correttamente inviato toohello Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="314ae-158">when hello message is successfully sent toohello Push Notification Service.</span></span> 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* <span data-ttu-id="314ae-159">Se si sono verificati Nessuna destinazione trovata per le notifiche push, probabilmente sarà toosee seguente di hello in risposta hello (che indica che non vi sono Nessuna registrazione trovata notifica hello toodeliver probabilmente perché le registrazioni hello presenti alcuni tag non corrispondenti)</span><span class="sxs-lookup"><span data-stu-id="314ae-159">If there were no targets found for any push notification then you are likely going toosee hello following in hello response (which indicates that there were no registrations found toodeliver hello notification probably because hello registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a><span data-ttu-id="314ae-160">Trasmissione tooWindows notifica di tipo avviso popup</span><span class="sxs-lookup"><span data-stu-id="314ae-160">Broadcast toast notification tooWindows</span></span>
<span data-ttu-id="314ae-161">Si noti intestazioni hello ottengano inviate quando si invia un client di tooWindows notifica di tipo avviso popup broadcast.</span><span class="sxs-lookup"><span data-stu-id="314ae-161">Notice hello headers that get sent out when you are sending a broadcast toast notification tooWindows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="314ae-162">Inviare la notifica specificando un tag (o un'espressione tag)</span><span class="sxs-lookup"><span data-stu-id="314ae-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="314ae-163">Intestazione di tag HTTP hello si noti che viene aggiunto toohello HTTP richiesta (nell'esempio hello seguente, viene inviato hello tooregistrations solo di notifica con payload 'sportivi')</span><span class="sxs-lookup"><span data-stu-id="314ae-163">Notice hello Tags HTTP header which gets added toohello HTTP request (in hello example below, we are sending hello notification only tooregistrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="314ae-164">Inviare la notifica specificando più tag</span><span class="sxs-lookup"><span data-stu-id="314ae-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="314ae-165">Si noti come intestazione HTTP tag hello cambia quando vengono inviati più tag.</span><span class="sxs-lookup"><span data-stu-id="314ae-165">Notice how hello Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="314ae-166">Notifica basata su modelli</span><span class="sxs-lookup"><span data-stu-id="314ae-166">Templated notification</span></span>
<span data-ttu-id="314ae-167">Si noti che hello formato HTTP modifiche di intestazione e corpo payload hello viene inviato come parte del corpo della richiesta HTTP hello:</span><span class="sxs-lookup"><span data-stu-id="314ae-167">Notice that hello Format HTTP header changes and hello payload body is sent as part of hello HTTP request body:</span></span>

<span data-ttu-id="314ae-168">**Lato client - modello registrato**</span><span class="sxs-lookup"><span data-stu-id="314ae-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="314ae-169">**Sul lato server - invio di payload hello**</span><span class="sxs-lookup"><span data-stu-id="314ae-169">**Server side - sending hello payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="314ae-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="314ae-170">Next Steps</span></span>
<span data-ttu-id="314ae-171">In questo argomento illustrato come toocreate un semplice Python REST client per gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="314ae-171">In this topic we showed how toocreate a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="314ae-172">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="314ae-172">From here you can:</span></span>

* <span data-ttu-id="314ae-173">Scaricare hello completo [esempio wrapper Python REST], che contiene tutto il codice hello precedente.</span><span class="sxs-lookup"><span data-stu-id="314ae-173">Download hello full [Python REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="314ae-174">Ulteriori informazioni sugli hub di notifica tag funzionalità in hello [esercitazione delle ultime notizie]</span><span class="sxs-lookup"><span data-stu-id="314ae-174">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="314ae-175">Ulteriori informazioni sulla funzionalità di modelli di hub di notifica in hello [esercitazione notizie di localizzazione]</span><span class="sxs-lookup"><span data-stu-id="314ae-175">Continue learning about Notification Hubs Templates feature in hello [Localizing News tutorial]</span></span>

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

