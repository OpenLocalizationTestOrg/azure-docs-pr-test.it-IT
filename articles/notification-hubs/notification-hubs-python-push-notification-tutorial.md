---
title: Come usare Hub di notifica con Python
description: Informazioni su come usare Hub di notifica di Azure da un back-end Python.
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
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="56dea-103">Come usare Hub di notifica da Python</span><span class="sxs-lookup"><span data-stu-id="56dea-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="56dea-104">Per accedere a tutte le funzionalità di Hub di notifica da un back-end Java/PHP/Ruby, è possibile usare l'interfaccia REST di Hub di notifica come descritto nell'argomento [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx)in MSDN.</span><span class="sxs-lookup"><span data-stu-id="56dea-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="56dea-105">Di seguito è riportato un esempio di riferimento per l'implementazione degli invii di notifiche in Python. Non si tratta dell'SDK Python di Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="56dea-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="56dea-106">L'esempio è scritto in Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="56dea-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="56dea-107">Questo argomento illustra come:</span><span class="sxs-lookup"><span data-stu-id="56dea-107">In this topic we show how to:</span></span>

* <span data-ttu-id="56dea-108">Compilare un client REST per le funzionalità di Hub di notifica in Python.</span><span class="sxs-lookup"><span data-stu-id="56dea-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="56dea-109">Inviare notifiche tramite l'interfaccia di Python alle API REST di Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="56dea-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="56dea-110">Eseguire un dump della richiesta/risposta HTTP REST a scopo didattico/di debug.</span><span class="sxs-lookup"><span data-stu-id="56dea-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="56dea-111">Completare l' [esercitazione introduttiva](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) per la piattaforma mobile preferita, implementando la parte del back-end in Python.</span><span class="sxs-lookup"><span data-stu-id="56dea-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="56dea-112">L'ambito dell'esempio è limitato all'invio di notifiche. Non viene eseguita alcuna gestione delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="56dea-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="56dea-113">Interfaccia del client</span><span class="sxs-lookup"><span data-stu-id="56dea-113">Client interface</span></span>
<span data-ttu-id="56dea-114">L'interfaccia principale del client può fornire gli stessi metodi disponibili nell' [SDK di Hub di notifica per .NET](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="56dea-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="56dea-115">Questo consentirà di convertire direttamente tutte le esercitazioni e gli esempi disponibili in questo sito e a cui hanno contribuito i membri della community su Internet.</span><span class="sxs-lookup"><span data-stu-id="56dea-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="56dea-116">Tutto il codice disponibile è incluso nell' [esempio di wrapper REST Python].</span><span class="sxs-lookup"><span data-stu-id="56dea-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="56dea-117">Ad esempio, per creare un client:</span><span class="sxs-lookup"><span data-stu-id="56dea-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="56dea-118">Per inviare una notifica di tipo avviso popup di Windows:</span><span class="sxs-lookup"><span data-stu-id="56dea-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="56dea-119">Implementazione</span><span class="sxs-lookup"><span data-stu-id="56dea-119">Implementation</span></span>
<span data-ttu-id="56dea-120">Se non è già stato fatto, seguire l' [esercitazione introduttiva] fino all'ultima sezione in cui è necessario implementare il back-end.</span><span class="sxs-lookup"><span data-stu-id="56dea-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="56dea-121">Tutti i dettagli per implementare un wrapper REST completo sono disponibili in [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="56dea-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="56dea-122">In questa sezione viene illustrata l'implementazione Python dei passaggi principali necessari per accedere agli endpoint REST di Hub di notifica e inviare notifiche:</span><span class="sxs-lookup"><span data-stu-id="56dea-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="56dea-123">Analizzare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="56dea-123">Parse the connection string</span></span>
2. <span data-ttu-id="56dea-124">Generare il token di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="56dea-124">Generate the authorization token</span></span>
3. <span data-ttu-id="56dea-125">Inviare una notifica tramite l'API REST HTTP</span><span class="sxs-lookup"><span data-stu-id="56dea-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="56dea-126">Analizzare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="56dea-126">Parse the connection string</span></span>
<span data-ttu-id="56dea-127">Questa è la classe principale che implementa il client, il cui costruttore analizza la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="56dea-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="56dea-128">Creare il token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="56dea-128">Create security token</span></span>
<span data-ttu-id="56dea-129">I dettagli della creazione del token di sicurezza sono disponibili [qui](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="56dea-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="56dea-130">È necessario aggiungere i metodi seguenti alla classe **NotificationHub** per creare il token in base all'URI della richiesta corrente e delle credenziali estratte dalla stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="56dea-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="56dea-131">Inviare una notifica tramite l'API REST HTTP</span><span class="sxs-lookup"><span data-stu-id="56dea-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="56dea-132">Definire innanzitutto una classe che rappresenta la notifica.</span><span class="sxs-lookup"><span data-stu-id="56dea-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="56dea-133">Questa classe è un contenitore per un corpo di notifica nativo oppure un set di proprietà nel caso di una notifica modello e un set di intestazioni che contengono il formato (modello o piattaforma nativa) e proprietà specifiche della piattaforma (come la proprietà di scadenza e le intestazioni WNS di Apple).</span><span class="sxs-lookup"><span data-stu-id="56dea-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="56dea-134">Per tutte le opzioni disponibili fare riferimento alla [documentazione delle API REST di Hub di notifica](http://msdn.microsoft.com/library/dn495827.aspx) e ai formati delle piattaforme di notifica specifiche.</span><span class="sxs-lookup"><span data-stu-id="56dea-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="56dea-135">Una volta definita questa classe, è possibile scrivere i metodi di notifica all'interno della classe **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="56dea-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
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

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
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

<span data-ttu-id="56dea-136">I metodi sopra indicati inviano una richiesta POST HTTP all'endpoint /messages dell'hub di notifica, contenenti il corpo e le intestazioni corrette per l'invio della notifica.</span><span class="sxs-lookup"><span data-stu-id="56dea-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="56dea-137">Uso di proprietà di debug per abilitare la registrazione dettagliata</span><span class="sxs-lookup"><span data-stu-id="56dea-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="56dea-138">L'abilitazione della proprietà di debug durante l'inizializzazione di Hub di notifica consente la scrittura di informazioni di registrazione dettagliate sulla richiesta HTTP e sul dump di risposta, nonché del risultato dettagliato dell'invio del messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="56dea-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="56dea-139">È stata recentemente aggiunta la [proprietà Notification Hubs TestSend](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) che restituisce informazioni dettagliate sul risultato dell'invio della notifica.</span><span class="sxs-lookup"><span data-stu-id="56dea-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="56dea-140">Per usarle, inizializzarle con le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="56dea-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="56dea-141">L'URL HTTP della richiesta di invio a Hub di notifica viene aggiunto con una querystring "test" come risultato.</span><span class="sxs-lookup"><span data-stu-id="56dea-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="56dea-142"><a name="complete-tutorial"></a>Completare l'esercitazione</span><span class="sxs-lookup"><span data-stu-id="56dea-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="56dea-143">È ora possibile completare l'esercitazione introduttiva inviando la notifica da un back-end Python.</span><span class="sxs-lookup"><span data-stu-id="56dea-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="56dea-144">Inizializzare il client di Hub di notifica, sostituendo la stringa di connessione e il nome hub come indicato nell'esercitazione [esercitazione introduttiva]:</span><span class="sxs-lookup"><span data-stu-id="56dea-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="56dea-145">Aggiungere quindi il codice di invio a seconda della piattaforma mobile di destinazione.</span><span class="sxs-lookup"><span data-stu-id="56dea-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="56dea-146">In questo esempio vengono aggiunti anche metodi di livello più elevato per abilitare l'invio di notifiche in base alla piattaforma, ad esempio send_windows_notification per Windows o send_apple_notification per Apple e così via.</span><span class="sxs-lookup"><span data-stu-id="56dea-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="56dea-147">Windows Store e Windows Phone 8.1 (non Silverlight)</span><span class="sxs-lookup"><span data-stu-id="56dea-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="56dea-148">Windows Phone 8.0 e 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="56dea-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="56dea-149">iOS</span><span class="sxs-lookup"><span data-stu-id="56dea-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="56dea-150">Android</span><span class="sxs-lookup"><span data-stu-id="56dea-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="56dea-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="56dea-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="56dea-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="56dea-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="56dea-153">Eseguendo il codice Python dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="56dea-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="56dea-154">Esempi:</span><span class="sxs-lookup"><span data-stu-id="56dea-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="56dea-155">Abilitazione della proprietà di debug</span><span class="sxs-lookup"><span data-stu-id="56dea-155">Enabling debug property</span></span>
<span data-ttu-id="56dea-156">Quando si abilita il flag di debug durante l'inizializzazione di Hub di notifica, verranno visualizzati una richiesta HTTP dettagliata e un dump di risposta, nonché un risultato di notifica simile a quello riportato di seguito, dove è possibile comprendere quali intestazioni HTTP vengono passate e quale risposta HTTP è stata ricevuta da Hub di notifica: ![][1]</span><span class="sxs-lookup"><span data-stu-id="56dea-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="56dea-157">verrà visualizzato il risultato dettagliato di Hub di notifica, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="56dea-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="56dea-158">quando il messaggio viene inviato correttamente al servizio di notifica push.</span><span class="sxs-lookup"><span data-stu-id="56dea-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="56dea-159">Se non fosse possibile trovare destinazioni per qualsiasi notifica push, probabilmente nella risposta verrà visualizzato quanto segue, dove viene indicato che non è stata trovata alcuna registrazione per recapitare la notifica perché nelle registrazioni erano presenti alcuni tag non corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="56dea-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="56dea-160">Trasmettere notifiche di tipo avviso popup a Windows</span><span class="sxs-lookup"><span data-stu-id="56dea-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="56dea-161">Notare le intestazioni che vengono inviate quando si inoltra una notifica di tipo popup al client Windows.</span><span class="sxs-lookup"><span data-stu-id="56dea-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="56dea-162">Inviare la notifica specificando un tag (o un'espressione tag)</span><span class="sxs-lookup"><span data-stu-id="56dea-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="56dea-163">Si noti l'intestazione HTTP Tags che viene aggiunta alla richiesta HTTP (nell'esempio seguente viene inviata la notifica solo alle registrazioni con payload 'sports')</span><span class="sxs-lookup"><span data-stu-id="56dea-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="56dea-164">Inviare la notifica specificando più tag</span><span class="sxs-lookup"><span data-stu-id="56dea-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="56dea-165">Si noti come l'intestazione HTTP Tags cambia quando vengono inviati più tag.</span><span class="sxs-lookup"><span data-stu-id="56dea-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="56dea-166">Notifica basata su modelli</span><span class="sxs-lookup"><span data-stu-id="56dea-166">Templated notification</span></span>
<span data-ttu-id="56dea-167">Si noti che l'intestazione HTTP Format cambia e che il corpo del payload viene inviato come parte del corpo della richiesta HTTP:</span><span class="sxs-lookup"><span data-stu-id="56dea-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="56dea-168">**Lato client - modello registrato**</span><span class="sxs-lookup"><span data-stu-id="56dea-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="56dea-169">**Lato server - invio del payload**</span><span class="sxs-lookup"><span data-stu-id="56dea-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="56dea-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56dea-170">Next Steps</span></span>
<span data-ttu-id="56dea-171">Questo argomento ha illustrato come creare un semplice client REST Python per Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="56dea-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="56dea-172">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="56dea-172">From here you can:</span></span>

* <span data-ttu-id="56dea-173">Scaricare l'intero [esempio di wrapper REST Python], che contiene tutto il codice sopra indicato.</span><span class="sxs-lookup"><span data-stu-id="56dea-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="56dea-174">Visualizzare altre informazioni sulla funzionalità di aggiunta tag di Hub di notifica nell' [esercitazione sull'invio delle ultime notizie]</span><span class="sxs-lookup"><span data-stu-id="56dea-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="56dea-175">Per altre informazioni sulla funzionalità relativa ai modelli di Hub di notifica, vedere l' [esercitazione sull'invio di notizie localizzate]</span><span class="sxs-lookup"><span data-stu-id="56dea-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="56dea-176">[esempio di wrapper REST Python]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="56dea-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="56dea-177">[esercitazione introduttiva]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="56dea-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="56dea-178">[esercitazione sull'invio delle ultime notizie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="56dea-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="56dea-179">[esercitazione sull'invio di notizie localizzate]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="56dea-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

