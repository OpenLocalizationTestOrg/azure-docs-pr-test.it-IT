---
title: aaaHow toouse gli hub di notifica con PHP
description: Informazioni su come toouse gli hub di notifica di Azure da un server back-end PHP.
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
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="57d00-103">Come toouse gli hub di notifica da PHP</span><span class="sxs-lookup"><span data-stu-id="57d00-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="57d00-104">È possibile accedere a tutte le funzionalità di hub di notifica da un server back-end PHP/Java o Ruby utilizzando l'interfaccia REST di Hub di notifica di hello come descritto nell'argomento MSDN hello [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="57d00-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="57d00-105">In questo argomento viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="57d00-105">In this topic we show how to:</span></span>

* <span data-ttu-id="57d00-106">Compilare un client REST per le funzionalità di Hub di notifica in PHP.</span><span class="sxs-lookup"><span data-stu-id="57d00-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="57d00-107">Seguire hello [esercitazione introduttiva Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) per la piattaforma per dispositivi mobili scelta, l'implementazione di parte di back-end hello in PHP.</span><span class="sxs-lookup"><span data-stu-id="57d00-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="57d00-108">Interfaccia del client</span><span class="sxs-lookup"><span data-stu-id="57d00-108">Client interface</span></span>
<span data-ttu-id="57d00-109">interfaccia del client principale Hello può fornire hello stessi metodi disponibili in hello [.NET SDK hub di notifica](http://msdn.microsoft.com/library/jj933431.aspx), sarà toodirectly convertire tutte le esercitazioni hello e gli esempi disponibili in questo sito, e fornito dalla community di hello in hello internet.</span><span class="sxs-lookup"><span data-stu-id="57d00-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="57d00-110">È possibile trovare tutto il codice hello disponibile in hello [esempio wrapper PHP REST].</span><span class="sxs-lookup"><span data-stu-id="57d00-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="57d00-111">Toocreate, ad esempio, un client:</span><span class="sxs-lookup"><span data-stu-id="57d00-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="57d00-112">toosend una notifica nativa iOS:</span><span class="sxs-lookup"><span data-stu-id="57d00-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="57d00-113">Implementazione</span><span class="sxs-lookup"><span data-stu-id="57d00-113">Implementation</span></span>
<span data-ttu-id="57d00-114">Se è stato non è già fatto, seguire il nostro [esercitazione introduttiva Get] backup toohello ultima sezione in cui occorre tooimplement hello back-end.</span><span class="sxs-lookup"><span data-stu-id="57d00-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="57d00-115">Inoltre, se si desidera è possibile utilizzare codice hello hello [esempio wrapper PHP REST] e passare direttamente toohello [esercitazione hello completo](#complete-tutorial) sezione.</span><span class="sxs-lookup"><span data-stu-id="57d00-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="57d00-116">Tutti hello tooimplement dettagli sono disponibili wrapper REST completo nel [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="57d00-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="57d00-117">In questa sezione verranno descritti implementazione PHP hello di hello passaggi principali necessari tooaccess endpoint REST degli hub di notifica:</span><span class="sxs-lookup"><span data-stu-id="57d00-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="57d00-118">Analizzare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="57d00-118">Parse hello connection string</span></span>
2. <span data-ttu-id="57d00-119">Generare il token di autorizzazione hello</span><span class="sxs-lookup"><span data-stu-id="57d00-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="57d00-120">Eseguire la chiamata HTTP hello</span><span class="sxs-lookup"><span data-stu-id="57d00-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="57d00-121">Analizzare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="57d00-121">Parse hello connection string</span></span>
<span data-ttu-id="57d00-122">Ecco hello classe principale implementazione hello client, il cui costruttore che analizza la stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="57d00-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="57d00-123">Creare il token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="57d00-123">Create security token</span></span>
<span data-ttu-id="57d00-124">sono disponibili dettagli Hello di creazione dei token di sicurezza hello [qui](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="57d00-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="57d00-125">metodo seguente Hello ha aggiunto toobe toohello **hub di notifica** token hello toocreate della classe dipende dall'URI della richiesta corrente hello e le credenziali di hello estratte dalla stringa di connessione hello hello.</span><span class="sxs-lookup"><span data-stu-id="57d00-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="57d00-126">Inviare una notifica</span><span class="sxs-lookup"><span data-stu-id="57d00-126">Send a notification</span></span>
<span data-ttu-id="57d00-127">Definire innanzitutto una classe che rappresenta una notifica.</span><span class="sxs-lookup"><span data-stu-id="57d00-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="57d00-128">Questa classe è un contenitore per un corpo di notifica nativo oppure un insieme di proprietà nel caso di una notifica modello e un insieme di intestazioni che contengono il formato (modello o piattaforma nativa) e proprietà specifiche della piattaforma (come la proprietà di scadenza e le intestazioni WNS di Apple).</span><span class="sxs-lookup"><span data-stu-id="57d00-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="57d00-129">Consultare toohello [documentazione delle API REST degli hub di notifica](http://msdn.microsoft.com/library/dn495827.aspx) e hello formati delle piattaforme di notifica specifica per tutte le opzioni disponibili di hello.</span><span class="sxs-lookup"><span data-stu-id="57d00-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="57d00-130">Grazie a questa classe, è possibile ora scrivere hello trasmissione metodi di notifica all'interno di hello **hub di notifica** classe.</span><span class="sxs-lookup"><span data-stu-id="57d00-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

        // Send hello request
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

<span data-ttu-id="57d00-131">Hello sopra i metodi di inviare un endpoint di /messages toohello richiesta HTTP POST di hub di notifica, notifica hello toosend di intestazioni e corpo corretto hello.</span><span class="sxs-lookup"><span data-stu-id="57d00-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="57d00-132"><a name="complete-tutorial"></a>Esercitazione hello completo</span><span class="sxs-lookup"><span data-stu-id="57d00-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="57d00-133">Ora è possibile completare l'esercitazione Introduzione hello inviando notifiche hello da un server back-end PHP.</span><span class="sxs-lookup"><span data-stu-id="57d00-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="57d00-134">Inizializzare il client di hub di notifica (sostituire nome hub e di stringa di connessione hello come indicato nell'hello [esercitazione introduttiva Get]):</span><span class="sxs-lookup"><span data-stu-id="57d00-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="57d00-135">Aggiungere codice di trasmissione hello a seconda della piattaforma per dispositivi mobili di destinazione.</span><span class="sxs-lookup"><span data-stu-id="57d00-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="57d00-136">Windows Store e Windows Phone 8.1 (non Silverlight)</span><span class="sxs-lookup"><span data-stu-id="57d00-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="57d00-137">iOS</span><span class="sxs-lookup"><span data-stu-id="57d00-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="57d00-138">Android</span><span class="sxs-lookup"><span data-stu-id="57d00-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="57d00-139">Windows Phone 8.0 e 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="57d00-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="57d00-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="57d00-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="57d00-141">Eseguendo il codice PHP dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="57d00-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57d00-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57d00-142">Next Steps</span></span>
<span data-ttu-id="57d00-143">In questo argomento illustrato come toocreate un linguaggio semplice REST client per gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="57d00-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="57d00-144">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="57d00-144">From here you can:</span></span>

* <span data-ttu-id="57d00-145">Scaricare hello completo [esempio wrapper PHP REST], che contiene tutto il codice hello precedente.</span><span class="sxs-lookup"><span data-stu-id="57d00-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="57d00-146">Ulteriori informazioni sugli hub di notifica tag funzionalità in hello [esercitazione delle ultime notizie]</span><span class="sxs-lookup"><span data-stu-id="57d00-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="57d00-147">Informazioni su utenti tooindividual le notifiche di push in [esercitazione notificare gli utenti]</span><span class="sxs-lookup"><span data-stu-id="57d00-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="57d00-148">Per ulteriori informazioni, vedere anche hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="57d00-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[esempio wrapper PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[esercitazione introduttiva Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

