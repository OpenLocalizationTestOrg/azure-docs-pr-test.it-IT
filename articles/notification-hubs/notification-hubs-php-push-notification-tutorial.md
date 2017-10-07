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
# <a name="how-toouse-notification-hubs-from-php"></a>Come toouse gli hub di notifica da PHP
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

È possibile accedere a tutte le funzionalità di hub di notifica da un server back-end PHP/Java o Ruby utilizzando l'interfaccia REST di Hub di notifica di hello come descritto nell'argomento MSDN hello [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx).

In questo argomento viene illustrato come:

* Compilare un client REST per le funzionalità di Hub di notifica in PHP.
* Seguire hello [esercitazione introduttiva Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) per la piattaforma per dispositivi mobili scelta, l'implementazione di parte di back-end hello in PHP.

## <a name="client-interface"></a>Interfaccia del client
interfaccia del client principale Hello può fornire hello stessi metodi disponibili in hello [.NET SDK hub di notifica](http://msdn.microsoft.com/library/jj933431.aspx), sarà toodirectly convertire tutte le esercitazioni hello e gli esempi disponibili in questo sito, e fornito dalla community di hello in hello internet.

È possibile trovare tutto il codice hello disponibile in hello [esempio wrapper PHP REST].

Toocreate, ad esempio, un client:

    $hub = new NotificationHub("connection string", "hubname");    

toosend una notifica nativa iOS:

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>Implementazione
Se è stato non è già fatto, seguire il nostro [esercitazione introduttiva Get] backup toohello ultima sezione in cui occorre tooimplement hello back-end.
Inoltre, se si desidera è possibile utilizzare codice hello hello [esempio wrapper PHP REST] e passare direttamente toohello [esercitazione hello completo](#complete-tutorial) sezione.

Tutti hello tooimplement dettagli sono disponibili wrapper REST completo nel [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). In questa sezione verranno descritti implementazione PHP hello di hello passaggi principali necessari tooaccess endpoint REST degli hub di notifica:

1. Analizzare la stringa di connessione hello
2. Generare il token di autorizzazione hello
3. Eseguire la chiamata HTTP hello

### <a name="parse-hello-connection-string"></a>Analizzare la stringa di connessione hello
Ecco hello classe principale implementazione hello client, il cui costruttore che analizza la stringa di connessione hello:

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


### <a name="create-security-token"></a>Creare il token di sicurezza
sono disponibili dettagli Hello di creazione dei token di sicurezza hello [qui](http://msdn.microsoft.com/library/dn495627.aspx).
metodo seguente Hello ha aggiunto toobe toohello **hub di notifica** token hello toocreate della classe dipende dall'URI della richiesta corrente hello e le credenziali di hello estratte dalla stringa di connessione hello hello.

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

### <a name="send-a-notification"></a>Inviare una notifica
Definire innanzitutto una classe che rappresenta una notifica.

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

Questa classe è un contenitore per un corpo di notifica nativo oppure un insieme di proprietà nel caso di una notifica modello e un insieme di intestazioni che contengono il formato (modello o piattaforma nativa) e proprietà specifiche della piattaforma (come la proprietà di scadenza e le intestazioni WNS di Apple).

Consultare toohello [documentazione delle API REST degli hub di notifica](http://msdn.microsoft.com/library/dn495827.aspx) e hello formati delle piattaforme di notifica specifica per tutte le opzioni disponibili di hello.

Grazie a questa classe, è possibile ora scrivere hello trasmissione metodi di notifica all'interno di hello **hub di notifica** classe.

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

Hello sopra i metodi di inviare un endpoint di /messages toohello richiesta HTTP POST di hub di notifica, notifica hello toosend di intestazioni e corpo corretto hello.

## <a name="complete-tutorial"></a>Esercitazione hello completo
Ora è possibile completare l'esercitazione Introduzione hello inviando notifiche hello da un server back-end PHP.

Inizializzare il client di hub di notifica (sostituire nome hub e di stringa di connessione hello come indicato nell'hello [esercitazione introduttiva Get]):

    $hub = new NotificationHub("connection string", "hubname");    

Aggiungere codice di trasmissione hello a seconda della piattaforma per dispositivi mobili di destinazione.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows Store e Windows Phone 8.1 (non Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 e 8.1 Silverlight
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


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

Eseguendo il codice PHP dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.

## <a name="next-steps"></a>Passaggi successivi
In questo argomento illustrato come toocreate un linguaggio semplice REST client per gli hub di notifica. A questo punto è possibile:

* Scaricare hello completo [esempio wrapper PHP REST], che contiene tutto il codice hello precedente.
* Ulteriori informazioni sugli hub di notifica tag funzionalità in hello [esercitazione delle ultime notizie]
* Informazioni su utenti tooindividual le notifiche di push in [esercitazione notificare gli utenti]

Per ulteriori informazioni, vedere anche hello [Centro sviluppatori PHP](/develop/php/).

[esempio wrapper PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[esercitazione introduttiva Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

