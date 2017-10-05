---
title: Come usare Hub di notifica con PHP
description: Informazioni su come usare Hub di notifica di Azure da un back-end PHP.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: c27b6308ff528224a0398e0ff40537db05417bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-php"></a><span data-ttu-id="ccfb6-103">Come usare Hub di notifica da PHP</span><span class="sxs-lookup"><span data-stu-id="ccfb6-103">How to use Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="ccfb6-104">Per accedere a tutte le funzionalità di Hub di notifica da un back-end Java/PHP/Ruby, è possibile usare l'interfaccia REST di Hub di notifica come descritto nell'argomento [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx)di MSDN.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="ccfb6-105">In questo argomento viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="ccfb6-105">In this topic we show how to:</span></span>

* <span data-ttu-id="ccfb6-106">Compilare un client REST per le funzionalità di Hub di notifica in PHP.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="ccfb6-107">Completare l' [esercitazione introduttiva](notification-hubs-ios-apple-push-notification-apns-get-started.md) per la piattaforma mobile preferita, implementando la parte del backend in PHP.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-107">Follow the [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing the back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="ccfb6-108">Interfaccia del client</span><span class="sxs-lookup"><span data-stu-id="ccfb6-108">Client interface</span></span>
<span data-ttu-id="ccfb6-109">L'interfaccia del client principale può fornire gli stessi metodi disponibili nell'[SDK di Hub di notifica per .NET](http://msdn.microsoft.com/library/jj933431.aspx). In questo modo sarà possibile tradurre direttamente tutte le esercitazioni e gli esempi disponibili in questo sito oppure messi a disposizione dalla community in Internet.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-109">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="ccfb6-110">Tutto il codice disponibile è incluso nell' [esempio di wrapper REST PHP].</span><span class="sxs-lookup"><span data-stu-id="ccfb6-110">You can find all the code available in the [PHP REST wrapper sample].</span></span>

<span data-ttu-id="ccfb6-111">Ad esempio, per creare un client:</span><span class="sxs-lookup"><span data-stu-id="ccfb6-111">For example, to create a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="ccfb6-112">Per inviare una notifica nativa iOS:</span><span class="sxs-lookup"><span data-stu-id="ccfb6-112">To send an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="ccfb6-113">Implementazione</span><span class="sxs-lookup"><span data-stu-id="ccfb6-113">Implementation</span></span>
<span data-ttu-id="ccfb6-114">Se non è già stato fatto, seguire l' [esercitazione Introduzione ad Hub di notifica] fino all'ultima sezione in cui è necessario implementare il back-end.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-114">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>
<span data-ttu-id="ccfb6-115">Si può anche usare il codice dell'[esempio di wrapper REST PHP] e passare direttamente alla sezione [Completare l'esercitazione](#complete-tutorial).</span><span class="sxs-lookup"><span data-stu-id="ccfb6-115">Also, if you want you can use the code from the [PHP REST wrapper sample] and go directly to the [Complete the tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="ccfb6-116">Tutti i dettagli per implementare un wrapper REST completo sono disponibili in [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccfb6-116">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="ccfb6-117">In questa sezione viene illustrata l'implementazione PHP dei passaggi principali necessari per accedere agli endpoint REST di Hub di notifica:</span><span class="sxs-lookup"><span data-stu-id="ccfb6-117">In this section we will describe the PHP implementation of the main steps required to access Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="ccfb6-118">Analizzare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="ccfb6-118">Parse the connection string</span></span>
2. <span data-ttu-id="ccfb6-119">Generare il token di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="ccfb6-119">Generate the authorization token</span></span>
3. <span data-ttu-id="ccfb6-120">Eseguire la chiamata HTTP</span><span class="sxs-lookup"><span data-stu-id="ccfb6-120">Perform the HTTP call</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="ccfb6-121">Analizzare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="ccfb6-121">Parse the connection string</span></span>
<span data-ttu-id="ccfb6-122">Questa è la classe principale che implementa il client, il cui costruttore analizza la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="ccfb6-122">Here is the main class implementing the client, whose constructor that parses the connection string:</span></span>

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a><span data-ttu-id="ccfb6-123">Creare il token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="ccfb6-123">Create security token</span></span>
<span data-ttu-id="ccfb6-124">I dettagli della creazione del token di sicurezza sono disponibili [qui](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccfb6-124">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="ccfb6-125">È necessario aggiungere il metodo seguente alla classe **NotificationHub** per creare il token in base dell'URI della richiesta corrente e delle credenziali estratte dalla stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-125">The following method has to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a><span data-ttu-id="ccfb6-126">Inviare una notifica</span><span class="sxs-lookup"><span data-stu-id="ccfb6-126">Send a notification</span></span>
<span data-ttu-id="ccfb6-127">Definire innanzitutto una classe che rappresenta una notifica.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-127">First, let us define a class representing a notification.</span></span>

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

<span data-ttu-id="ccfb6-128">Questa classe è un contenitore per un corpo di notifica nativo oppure un insieme di proprietà nel caso di una notifica modello e un insieme di intestazioni che contengono il formato (modello o piattaforma nativa) e proprietà specifiche della piattaforma (come la proprietà di scadenza e le intestazioni WNS di Apple).</span><span class="sxs-lookup"><span data-stu-id="ccfb6-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="ccfb6-129">Per tutte le opzioni disponibili fare riferimento alla [documentazione delle API REST di Hub di notifica](http://msdn.microsoft.com/library/dn495827.aspx) e ai formati delle piattaforme di notifica specifiche.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-129">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="ccfb6-130">Una volta definita questa classe, è possibile scrivere i metodi di notifica all'interno della classe **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="ccfb6-130">Armed with this class, we can now write the send notification methods inside of the **NotificationHub** class.</span></span>

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send the request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

<span data-ttu-id="ccfb6-131">I metodi sopra indicati inviano una richiesta POST HTTP all'endpoint /messages dell'hub di notifica, contenenti il corpo e le intestazioni corrette per l'invio della notifica.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-131">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

## <span data-ttu-id="ccfb6-132"><a name="complete-tutorial"></a>Completare l'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ccfb6-132"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="ccfb6-133">È ora possibile completare l'esercitazione introduttiva inviando la notifica da un back-end PHP.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-133">Now you can complete the Get Started tutorial by sending the notification from a PHP back-end.</span></span>

<span data-ttu-id="ccfb6-134">Inizializzare il client di Hub di notifica, sostituendo la stringa di connessione e il nome hub come indicato nell'esercitazione [esercitazione Introduzione ad Hub di notifica]:</span><span class="sxs-lookup"><span data-stu-id="ccfb6-134">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="ccfb6-135">Aggiungere quindi il codice di invio a seconda della piattaforma mobile di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-135">Then add the send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="ccfb6-136">Windows Store e Windows Phone 8.1 (non Silverlight)</span><span class="sxs-lookup"><span data-stu-id="ccfb6-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="ccfb6-137">iOS</span><span class="sxs-lookup"><span data-stu-id="ccfb6-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="ccfb6-138">Android</span><span class="sxs-lookup"><span data-stu-id="ccfb6-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="ccfb6-139">Windows Phone 8.0 e 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="ccfb6-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a><span data-ttu-id="ccfb6-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="ccfb6-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="ccfb6-141">Eseguendo il codice PHP dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccfb6-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ccfb6-142">Next Steps</span></span>
<span data-ttu-id="ccfb6-143">In questo argomento è stato illustrato come creare un semplice client REST Java per Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-143">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="ccfb6-144">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="ccfb6-144">From here you can:</span></span>

* <span data-ttu-id="ccfb6-145">Scaricare l'intero [esempio di wrapper REST PHP], che contiene tutto il codice sopra indicato.</span><span class="sxs-lookup"><span data-stu-id="ccfb6-145">Download the full [PHP REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="ccfb6-146">Visualizzare altre informazioni sulla funzionalità di aggiunta tag di Hub di notifica nell'[esercitazione per l'invio di notizie]</span><span class="sxs-lookup"><span data-stu-id="ccfb6-146">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="ccfb6-147">Visualizzare altre informazioni sull'invio di notifiche push a singoli utenti nell'[esercitazione sull'invio di notifiche agli utenti]</span><span class="sxs-lookup"><span data-stu-id="ccfb6-147">Learn about pushing notifications to individual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="ccfb6-148">Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ccfb6-148">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="ccfb6-149">[esempio di wrapper REST PHP]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span><span class="sxs-lookup"><span data-stu-id="ccfb6-149">[PHP REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span></span>
<span data-ttu-id="ccfb6-150">[esercitazione Introduzione ad Hub di notifica]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span><span class="sxs-lookup"><span data-stu-id="ccfb6-150">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span></span>

