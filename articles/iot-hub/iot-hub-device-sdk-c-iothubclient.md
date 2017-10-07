---
title: il dispositivo di IoT aaaAzure SDK per C - IoTHubClient | Documenti Microsoft
description: La libreria di IoTHubClient toouse hello nel dispositivo di Azure IoT hello SDK per App per dispositivi toocreate C che comunicano con un hub IoT.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>Azure IoT SDK per dispositivi per C: altre informazioni su IoTHubClient
Hello [innanzitutto articolo](iot-hub-device-sdk-c-intro.md) in hello questa serie introdotto **dispositivo IoT di Azure SDK per C**. e spiegato che l'SDK comprende due livelli architetturali. In base hello è hello **IoTHubClient** libreria che gestisce direttamente la comunicazione con l'IoT Hub. È inoltre disponibile hello **serializzatore** libreria che compila tooprovide in cui servizi di serializzazione. In questo articolo verranno fornite ulteriori dettagli su hello **IoTHubClient** libreria.

articolo di Hello precedente come descritto hello toouse **IoTHubClient** libreria toosend eventi tooIoT Hub e ricevere messaggi. In questo articolo si estende la discussione di che spiega come gestire precisamente toomore *quando* inviare e ricevere dati, un'introduzione toohello **inferiore a livello di API**. Spiega anche come tooattach proprietà tooevents (e il recupero dei messaggi) utilizzando proprietà hello gestione delle funzionalità in hello **IoTHubClient** libreria. Infine, verranno fornite ulteriori spiegazioni di toohandle modi i messaggi ricevuti dall'IoT Hub.

Hello articolo si conclude con la copertura di un paio di vari argomenti, inclusi ulteriori informazioni sulle credenziali di dispositivo e come toochange hello comportamento di hello **IoTHubClient** tramite le opzioni di configurazione.

Si userà hello **IoTHubClient** esempi del SDK tooexplain questi argomenti. Se si desidera toofollow lungo, vedere hello **l'hub IOT\_client\_esempio\_http** e **l'hub IOT\_client\_esempio\_amqp** applicazioni presenti nel dispositivo di Azure IoT hello SDK per C. tutti gli elementi descritti in hello le sezioni seguenti è illustrato in questi esempi.

È possibile trovare hello [ **dispositivo IoT di Azure SDK per C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repository e visualizzarne i dettagli di hello API in hello [riferimento all'API C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Hello API di livello inferiore
Hello precedente articolo viene descritto il funzionamento di base di hello hello **IotHubClient** contesto hello di hello **l'hub IOT\_client\_esempio\_amqp** applicazione. Ad esempio, è spiegato come tooinitialize hello libreria con questo codice.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Inoltre descritto come eventi toosend usando questa chiamata di funzione.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

Hello viene inoltre descritto come tooreceive messaggi tramite la registrazione di una funzione di callback.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

articolo Hello è stato anche illustrato come risorse toofree tramite codice come illustrato di seguito hello.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

Esistono tuttavia tooeach funzioni complementare di queste API:

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Tutte queste funzioni includono "LL" nel nome API hello. Diverso da quello, parametri di hello di ognuna di queste funzioni sono relative controparti non LL tootheir identici. Tuttavia, il comportamento di hello di queste funzioni è diverso per un aspetto importante.

Quando si chiama **IoTHubClient\_CreateFromConnectionString**, librerie sottostante hello creano un nuovo thread che viene eseguito in background hello. Questo thread invia eventi all'hub IoT e ne riceve i messaggi. Nessun thread di questo tipo viene creato quando si lavora con hello "LL" API. creazione di Hello di thread in background hello è uno sviluppatore toohello praticità. Non è necessario tooworry sull'invio di eventi in modo esplicito e la ricezione di messaggi dall'IoT Hub - avviene automaticamente in background hello. Al contrario, hello "LL" API consentono di controllare esplicitamente la comunicazione con l'IoT Hub, se è necessario.

toounderstand questa soluzione migliore, esaminiamo un esempio:

Quando si chiama **IoTHubClient\_SendEventAsync**, ciò che si sta effettivamente eseguendo è l'inserimento di eventi di hello in un buffer. thread in background creato quando si chiama Hello **IoTHubClient\_CreateFromConnectionString** monitora questo buffer e i dati vengono inviati continuamente che contenga tooIoT Hub. Ciò si verifica in background hello hello la stessa ora che hello thread principale sta eseguendo altre operazioni.

Analogamente, quando si registra una funzione di callback per i messaggi utilizzando **IoTHubClient\_SetMessageCallback**, si sta per indicare in background di hello hello SDK toohave thread richiamare la funzione di callback hello quando un messaggio ricevuto, indipendentemente dal thread principale di hello.

Hello "LL" API di non creare un thread in background. Al contrario, una nuova API deve essere chiamato tooexplicitly inviare e ricevere dati da IoT Hub. Come illustrato nell'esempio seguente hello.

Hello **l'hub IOT\_client\_esempio\_http** applicazione che è incluso nel SDK illustra hello hello le API di livello inferiore. In questo esempio, si invia eventi tooIoT Hub con il codice come illustrato di seguito hello:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

prime tre righe Hello creano messaggio hello e ultima riga hello invia evento hello. Tuttavia, come indicato in precedenza, "invio" evento hello significa che i dati hello semplicemente si trova in un buffer. Non vengono trasmesse nella rete hello quando si chiama **IoTHubClient\_LL\_SendEventAsync**. In ordine tooactually in ingresso hello dati tooIoT Hub, è necessario chiamare **IoTHubClient\_LL\_DoWork**, come nel seguente esempio:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Questo codice (da hello **l'hub IOT\_client\_esempio\_http** applicazione) chiama ripetutamente **IoTHubClient\_LL\_DoWork** . Ogni volta che **IoTHubClient\_LL\_DoWork** viene chiamato, invia alcuni eventi dal buffer di hello tooIoT Hub e viene recuperato un messaggio in coda inviato toohello dispositivo. quest'ultimo caso Hello significa che se è stata registrata una funzione di callback per i messaggi, quindi viene richiamato il callback di hello (presupponendo che tutti i messaggi vengono accodati fino). È una funzione di callback verrebbe registrato con codice simile hello seguente:

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

motivo Hello **IoTHubClient\_LL\_DoWork** viene spesso chiamato in un ciclo è che ogni volta che viene chiamato, invia *alcuni* memorizzato nel buffer gli eventi tooIoT Hub e recupera *hello successivamente* messaggio messo in coda per il dispositivo hello. Ogni chiamata non è garantito che gli eventi toosend tutti memorizzato nel buffer o in coda tooretrieve tutti i messaggi. Se si desidera toosend tutti gli eventi di hello nel buffer e quindi continueranno con altre attività di elaborazione è possibile sostituire questo ciclo con codice simile hello seguente:

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Questo codice chiama **IoTHubClient\_LL\_DoWork** fino a quando tutti gli eventi nel buffer hello sono stati inviati tooIoT Hub. Non significa però che si siano ricevuti anche tutti i messaggi in coda. Parte del motivo hello è che il controllo dei messaggi "tutto" non è deterministica come un'azione. Cosa succede se si recuperano "tutti" messaggi hello, ma ne verrà quindi inviati toohello dispositivo subito dopo? Un migliore toodeal modo con cui è con un timeout programmato. Ad esempio, funzione di callback messaggio hello è stato possibile reimpostare un timer ogni volta che viene richiamato. È quindi possibile scrivere l'elaborazione di toocontinue logica Se, ad esempio, non sono stati ricevuti messaggi in hello ultima *X* secondi.

Quando è finito ingressing eventi e la ricezione di messaggi, che toocall hello corrispondente funzione tooclean delle risorse.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Si tratta in sostanza di un solo set di API toosend e ricevere dati con un thread in background e un altro set di API che hello stessa operazione senza thread in background hello. Molti sviluppatori preferibile hello LL API non ma hello le API di livello inferiore sono utili quando per sviluppatori di hello richiede un controllo esplicito le trasmissioni in rete. Ad esempio, alcuni dispositivi raccolgono dati nel tempo e solo eventi in ingresso a intervalli specificati, come una volta all'ora o una volta al giorno. Hello offrono le API di livello inferiore hello controllo tooexplicitly possibilità quando si inviano e ricevono dati dall'IoT Hub. Altri semplicemente preferiranno semplicità hello che hello che forniscono le API di livello inferiore. Tutto ciò che viene eseguita nel thread principale di hello anziché alcuni eventualità di lavoro in background hello.

Indipendentemente dal modello scelto, è possibile che toobe coerente nelle quali API utilizzare. Se si avvia chiamando **IoTHubClient\_LL\_CreateFromConnectionString**, assicurarsi di utilizzare solo hello corrispondente API di livello inferiore per tutte le operazioni di completamento:

* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy
* IoTHubClient\_LL\_DoWork

anche Hello opposto è true. Se si inizia con **IoTHubClient\_CreateFromConnectionString**, quindi utilizzare hello LL API non per tutte le altre elaborazioni.

Nel dispositivo di Azure IoT di hello SDK per C, vedere hello **l'hub IOT\_client\_esempio\_http** inferiore a livello di applicazione per un esempio completo di hello API. Hello **l'hub IOT\_client\_esempio\_amqp** applicazione è possibile fare riferimento per un esempio completo di hello LL API non.

## <a name="property-handling"></a>Gestione delle proprietà
Finora quando abbiamo descritto l'invio dei dati, è stata stato fa riferimento toohello corpo del messaggio hello. Si consideri ad esempio questo codice:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Questo esempio viene inviato un messaggio tooIoT Hub, con testo hello "Hello World". Tuttavia, IoT Hub consente inoltre di messaggio associata tooeach toobe di proprietà. Le proprietà sono coppie nome/valore che possono essere collegato toohello messaggio. Ad esempio, che potremo modificare hello tooattach di codice precedente la proprietà toohello message:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Viene avviata chiamando **IoTHubMessage\_proprietà** e passando l'handle di hello dei messaggi. Cosa viene visualizzato nuovamente un **mappa\_gestire** riferimento che consente di toostart aggiunta di proprietà. Hello quest'ultimo viene eseguito chiamando **mappa\_AddOrUpdate**, che accetta un tooa riferimento mappa\_HANDLE, il nome di proprietà hello e valore della proprietà hello. Con questa API è possibile aggiungere tutte le proprietà necessarie.

Quando evento hello viene letto dal **hub eventi**, ricevitore hello di enumerare le proprietà di hello e recuperarne i valori corrispondenti. Ad esempio, in .NET questa verrebbe eseguita accedendo hello [raccolta di proprietà nell'oggetto EventData hello](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

Nell'esempio precedente hello si assocerà evento tooan proprietà che vengono inviate tooIoT Hub. Le proprietà possono essere collegati toomessages ricevuto dall'IoT Hub. Se si desidera che la proprietà tooretrieve da un messaggio, è possibile utilizzare codice come illustrato di seguito hello nella funzione callback messaggio:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

Hello chiamata troppo**IoTHubMessage\_proprietà** hello restituisce **mappa\_gestire** riferimento. È quindi passare il riferimento troppo**mappa\_GetInternals** tooobtain una matrice di tooan di riferimento di nome/valore hello coppie (oltre a un numero di proprietà hello). A questo punto è sufficiente enumerazione dei valori di hello proprietà tooget toohello desiderato.

Non si dispone di proprietà toouse nell'applicazione. Tuttavia, se è necessario tooset usarle in eventi o recuperarli da messaggi hello **IoTHubClient** libreria rende più semplice.

## <a name="message-handling"></a>Gestione dei messaggi
Come indicato in precedenza, quando i messaggi provenienti da hello IoT Hub **IoTHubClient** libreria risponde richiamando una funzione di callback registrato. Un parametro restituito da questa funzione merita tuttavia qualche spiegazione aggiuntiva. Di seguito viene riportato un frammento della funzione di callback hello in hello **l'hub IOT\_client\_esempio\_http** applicazione di esempio:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Si noti che il tipo restituito di hello è **IOTHUBMESSAGE\_DISPOSITION\_risultato** e in questo caso restituiamo **IOTHUBMESSAGE\_accettato**. Esistono altri valori di questa funzione è possibile tornare che modifica la modalità hello **IoTHubClient** libreria reagisce callback messaggio toohello. Ecco le opzioni di hello.

* **IOTHUBMESSAGE\_accettato** : messaggio hello è stata elaborata correttamente. Hello **IoTHubClient** libreria non richiama la funzione di callback hello con hello stesso messaggio.
* **IOTHUBMESSAGE\_RIFIUTATO** : Impossibile elaborare il messaggio hello e vi è alcun toodo desiderio non hello così in futuro. Hello **IoTHubClient** libreria non deve richiamare la funzione di callback hello con hello stesso messaggio.
* **IOTHUBMESSAGE\_ABBANDONATO** : messaggio hello non è stata elaborata correttamente, ma hello **IoTHubClient** libreria deve richiamare una funzione di callback hello con hello stesso messaggio.

Per hello innanzitutto due codici restituiti, hello **IoTHubClient** libreria invia un messaggio tooIoT Hub che indica il messaggio hello deve essere eliminato dalla coda dispositivo hello e non recapitato nuovamente. effetto Hello è hello stesso (messaggio hello viene eliminato dalla coda dispositivo hello), ma se il messaggio hello è stato accettato o rifiutato è ancora registrato.  La registrazione di questa distinzione è utile toosenders del messaggio hello in grado di restare in attesa per commenti e suggerimenti e scoprire se un dispositivo ha accettato o rifiutato un messaggio specifico.

Nell'ultimo caso hello viene inviato un messaggio anche tooIoT Hub, ma significa che deve essere recapitato nuovamente il messaggio hello. In genere si sarà abbandona un messaggio se si verifica un errore ma si desidera tootry tooprocess hello messaggio nuovo. Al contrario, un messaggio di rifiuto è appropriato quando si verifica un errore irreversibile (o se si decide semplicemente che non si desidera messaggio hello tooprocess).

In ogni caso, tenere hello diversi codici in modo che è possibile dedurre il comportamento di hello desiderato hello **IoTHubClient** libreria.

## <a name="alternate-device-credentials"></a>Credenziali del dispositivo alternative
Come illustrato in precedenza, hello in primo luogo toodo quando si lavora con hello **IoTHubClient** libreria è tooobtain un **l'hub IOT\_CLIENT\_gestire** con una chiamata ad esempio hello seguenti:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Hello argomenti troppo**IoTHubClient\_CreateFromConnectionString** sono stringa di connessione del dispositivo hello e un parametro che indica il protocollo di hello utilizziamo toocommunicate con l'IoT Hub. stringa di connessione del dispositivo Hello presenta un formato che viene visualizzato come segue:

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

Questa stringa contiene quattro informazioni: nome dell'hub IoT, suffisso dell'hub IoT, ID dispositivo e chiave di accesso condivisa. Ottenere il nome di dominio completo hello (FQDN) di un hub IoT quando si crea l'istanza dell'hub IoT in hello portale di Azure, in questo modo è il nome dell'hub IoT hello (hello prima parte di hello FQDN) e il suffisso di hub IoT hello (rimanente hello hello FQDN). Ottenere ID dispositivo hello e la chiave di accesso condiviso hello quando si registra il dispositivo con l'IoT Hub (come descritto in hello [articolo precedente](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** offre libreria hello tooinitialize unidirezionale. Se si preferisce, è possibile creare un nuovo **l'hub IOT\_CLIENT\_gestire** utilizzando questi singoli parametri anziché di stringa di connessione del dispositivo hello. Questo risultato viene ottenuto con hello seguente codice:

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

Ciò consente di realizzare hello equivale al **IoTHubClient\_CreateFromConnectionString**.

Potrebbe sembrare ovvio che desideri toouse **IoTHubClient\_CreateFromConnectionString** invece di questo metodo di inizializzazione più dettagliato. Tenere però presente che quando si registra un dispositivo nell'hub IoT, si ottiene un ID dispositivo e una chiave del dispositivo, non una stringa di connessione. Hello *Esplora dispositivo* strumento SDK introdotto in hello [articolo precedente](iot-hub-device-sdk-c-intro.md) Usa librerie di hello **SDK di servizi di Azure IoT** toocreate hello dispositivo stringa di connessione ID dispositivo Hello chiave del dispositivo e nome host dell'IoT Hub. Pertanto la chiamata di **IoTHubClient\_LL\_crea** potrebbe essere preferibile perché si salva il passaggio di hello della generazione di una stringa di connessione. Usare il metodo più pratico.

## <a name="configuration-options"></a>Opzioni di configurazione
Fino a questo punto tutti gli elementi descritti su hello modo hello **IoTHubClient** works libreria riflette il comportamento predefinito. Tuttavia, esistono alcune opzioni che è possibile impostare toochange funzionamento libreria hello. Questa operazione viene eseguita sfruttando hello **IoTHubClient\_LL\_SetOption** API. Considerare questo esempio:

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Ci sono un paio di opzioni usate comunemente:

* **SetBatching** (bool) – se **true**, i dati inviati tooIoT Hub verranno inviate in batch. Se **false**, i messaggi vengono inviati singolarmente. valore predefinito di Hello è **false**. Si noti che hello **SetBatching** opzione si applica solo il protocollo HTTP toohello e non toohello MQTT o AMQP protocolli.
* **Timeout** (unsigned int): questo valore è rappresentato in millisecondi. Se l'invio di una richiesta HTTP o la ricezione di una risposta richiede più tempo rispetto a questo momento, quindi hello timeout della connessione.

opzione di invio in batch Hello è importante. Per impostazione predefinita, hello eventi ingresses libreria singolarmente (un singolo evento è qualsiasi elemento passato troppo**IoTHubClient\_LL\_SendEventAsync**). Se l'invio in batch opzione hello **true**, libreria hello raccoglie tutti gli eventi, nonché dal buffer di hello (backup toohello dimensione massima dei messaggi che accetterà IoT Hub).  Hello evento batch viene inviato tooIoT Hub in una singola chiamata HTTP (singoli eventi hello sono inclusi in una matrice JSON). In genere l'abilitazione dell'invio in batch consente di ottenere un miglioramento significativo delle prestazioni, perché si riducono le sequenze di andata e ritorno in rete. Si riduce in modo significativo anche la larghezza di banda, perché si invia un unico set di intestazioni HTTP con un batch di eventi, invece di un set di intestazioni per ogni singolo evento. A meno che non si dispone di un toodo motivo specifico, in caso contrario, in genere è opportuno tooenable l'invio in batch.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo viene descritto il comportamento hello dettaglio di hello **IoTHubClient** libreria trovata nel hello **dispositivo IoT di Azure SDK per C**. Con queste informazioni, è necessario avere una buona conoscenza delle funzionalità di hello di hello **IoTHubClient** libreria. Hello [articolo successivo](iot-hub-device-sdk-c-serializer.md) fornisce informazioni simili sulle hello **serializzatore** libreria.

toolearn più sullo sviluppo per l'IoT Hub, vedere hello [Azure IoT SDK][lnk-sdks].

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
