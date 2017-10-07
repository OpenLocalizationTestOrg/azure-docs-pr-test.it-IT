---
title: il dispositivo di Azure IoT aaaThe SDK per C | Documenti Microsoft
description: Iniziare con il dispositivo di Azure IoT hello SDK per C e informazioni su come le App per dispositivi toocreate che comunicano con un hub IoT.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>Azure IoT SDK per dispositivi per C

Hello **dispositivo IoT di Azure SDK** è un set di librerie progettato processo hello toosimplify di invio di messaggi tooand ricezione di messaggi da hello **IoT Hub Azure** servizio. Sono disponibili diverse varianti di hello SDK, ogni destinazione una piattaforma specifica, ma in questo articolo descrive hello **dispositivo IoT di Azure SDK per C**.

il dispositivo di Azure IoT Hello SDK per C viene scritta in ANSI C (C99) toomaximize portabilità. Questa funzionalità rende toooperate ideale di librerie hello su più piattaforme e dispositivi, in particolare quando riducendo al minimo su disco e footprint di memoria è una priorità.

Sono disponibili un'ampia gamma di piattaforme in cui hello SDK è stato testato (vedere hello [Azure Certified per catalogo dispositivo IoT](https://catalog.azureiotsuite.com/) per informazioni dettagliate). Sebbene in questo articolo include procedure dettagliate di codice di esempio in esecuzione nella piattaforma Windows hello, codice hello descritto in questo articolo è identico per intervallo hello delle piattaforme supportate.

In questo articolo viene illustrata toohello architettura del dispositivo di Azure IoT hello SDK per C. Viene illustrato come inviare dati tooIoT Hub libreria dispositivi di hello tooinitialize e ricevere messaggi da esso. informazioni di Hello in questo articolo dovrebbero essere sufficiente tooget avviato utilizzando hello SDK, ma fornisce anche informazioni tooadditional puntatori sulle librerie hello.

## <a name="sdk-architecture"></a>Architettura dell'SDK

È possibile trovare hello [ **dispositivo IoT di Azure SDK per C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repository e visualizzarne i dettagli di hello API in hello [riferimento all'API C](https://azure.github.io/azure-iot-sdk-c/index.html).

sono disponibili più recente delle librerie di hello Hello in hello **master** ramo del repository hello:

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* Hello core implementazione di hello SDK è hello **l'hub IOT\_client** cartella che contiene l'implementazione di hello del livello API minimo di hello in hello SDK: hello **IoTHubClient** libreria. Hello **IoTHubClient** libreria contiene le API di messaggistica non elaborato per l'invio di messaggi tooIoT Hub e la ricezione di messaggi dall'IoT Hub di implementazione. Quando si usa questa libreria, si dovrà implementare la serializzazione dei messaggi, mente gli altri dettagli della comunicazione con l'hub IoT vengono gestiti automaticamente.
* Hello **serializzatore** cartella contiene funzioni di supporto ed esempi che illustrano come dati tooserialize prima dell'invio tramite Hub IoT tooAzure hello libreria client. utilizzo di Hello del serializzatore hello non è obbligatorio e viene fornita per praticità. hello toouse **serializzatore** library, si definisce un modello che specifica dati toosend tooIoT Hub e hello messaggi hello previsto tooreceive da esso. Una volta definito il modello di hello, hello SDK vengono fornite con una superficie API che consente di lavoro tooeasily da dispositivo a cloud e i messaggi da cloud a dispositivo senza doversi preoccupare hello dettagli di serializzazione. libreria Hello dipende dalle altre librerie open source che implementano il trasporto utilizzando i protocolli, ad esempio MQTT e AMQP.
* Hello **IoTHubClient** libreria dipende da altre librerie open source:
  * Hello [C Azure condiviso utilità](https://github.com/Azure/azure-c-shared-utility) libreria, che fornisce funzionalità comuni per le attività di base (ad esempio stringhe, la modifica di elenco e i/o) necessaria per molti SDK C correlate ad Azure.
  * Hello [uAMQP Azure](https://github.com/Azure/azure-uamqp-c) libreria, è un'implementazione sul lato client di AMQP ottimizzate per i dispositivi di risorse sufficienti.
  * Hello [uMQTT Azure](https://github.com/Azure/azure-umqtt-c) libreria che è una raccolta generica che implementa il protocollo MQTT hello e ottimizzate per i dispositivi di risorse sufficienti.

Utilizzo di queste librerie è più facile toounderstand esaminando il codice di esempio. Hello le sezioni seguenti consentono di eseguire molte delle applicazioni di esempio hello inclusi in hello SDK. Viene fornito in questa procedura dettagliata una buona ritiene per hello varie funzionalità di livelli dell'architettura di hello di hello SDK e un hello toohow introduzione API funzionano.

## <a name="before-you-run-hello-samples"></a>Prima di eseguire gli esempi di hello

Prima di eseguire gli esempi di hello in dispositivi Azure IoT hello SDK per C, è necessario [creare un'istanza del servizio dell'IoT Hub hello](iot-hub-create-through-portal.md) nella sottoscrizione di Azure. Completare quindi hello seguenti attività:

* Preparare l'ambiente di sviluppo
* Ottenere le credenziali del dispositivo.

### <a name="prepare-your-development-environment"></a>Preparare l'ambiente di sviluppo

I pacchetti vengono forniti per le piattaforme comune (ad esempio NuGet per Windows o apt_get per Debian e Ubuntu) e gli esempi di hello utilizzano questi pacchetti, se disponibile. In alcuni casi, è necessario toocompile hello SDK per o nel dispositivo. Se è necessario toocompile hello SDK, vedere [preparare l'ambiente di sviluppo](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) nel repository GitHub hello.

codice dell'applicazione esempio hello tooobtain, scaricare una copia di hello SDK da GitHub. Ottenere la copia di origine hello da hello **master** ramo di hello [repository GitHub](https://github.com/Azure/azure-iot-sdk-c).


### <a name="obtain-hello-device-credentials"></a>Ottenere le credenziali di dispositivo hello

Ora che si dispone di codice sorgente dell'esempio hello, hello Avanti cosa toodo è tooget un insieme di credenziali di dispositivo. Per un dispositivo toobe in grado di tooaccess un hub IoT, è innanzitutto necessario aggiungere hello dispositivo toohello del Registro di sistema di IoT Hub identità. Quando si aggiunge il dispositivo, ottenere un set di credenziali per un dispositivo che è necessario per l'hub IoT di hello dispositivo toobe tooconnect in grado di toohello. applicazioni di esempio Hello descritte nella sezione successiva hello prevede che le credenziali sotto forma di hello di un **stringa di connessione dispositivo**.

Esistono diversi toohelp di strumenti Apri origine si gestione l'hub IoT.

* Un'applicazione Windows denominata [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).
* Uno strumento dell'interfaccia della riga di comando di node.js multipiattaforma denominato [iothub-explorer](https://github.com/azure/iothub-explorer).

Questa esercitazione viene utilizzato con interfaccia grafica hello *Esplora dispositivo* strumento. È inoltre possibile utilizzare hello *l'hub IOT Esplora* strumento se si preferisce uno strumento CLI toouse.

strumenti di Esplora Hello dispositivo utilizza hello Azure IoT servizio librerie tooperform varie funzioni nell'IoT Hub, inclusa l'aggiunta di dispositivi. Se si utilizza hello dispositivo Esplora strumento tooadd un dispositivo, si ottiene una stringa di connessione per il dispositivo. È necessario questo applicazioni di esempio hello toorun stringa di connessione.

Se non si ha familiarità con lo strumento Esplora dispositivo di hello, hello seguente procedura descrive come toouse è tooadd un dispositivo e ottenere una stringa di connessione del dispositivo.

strumento di explorer tooinstall hello dispositivo, vedere [come toouse hello Esplora dispositivo per i dispositivi IoT Hub](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).

Quando si esegue il programma hello, viene visualizzato di questa interfaccia:

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

Immettere il **stringa di connessione Hub IoT** in hello primo campo e fare clic su **aggiornamento**. Questo passaggio Configura strumento hello in modo che possa comunicare con l'IoT Hub.

Quando la stringa di connessione IoT Hub hello è configurato, fare clic su hello **gestione** scheda:

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

Questa scheda è possibile gestire i dispositivi hello registrati nell'hub IoT.

Per creare un dispositivo scegliere hello **crea** pulsante. Viene visualizzata una finestra di dialogo con un set di chiavi, primaria e secondaria, prepopolato. Immettere un valore in **Device ID** (ID dispositivo) e fare clic su **Create** (Crea).

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

Quando viene creato il dispositivo di hello, hello dispositivi elencare gli aggiornamenti con tutti i dispositivi hello registrato, tra cui hello che quello appena creato. Facendo clic con il pulsante destro del mouse sul nuovo dispositivo, viene visualizzato questo menu:

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

Se si sceglie **copiare la stringa di connessione per il dispositivo selezionato**, stringa di connessione del dispositivo hello è Appunti toohello copiato. Mantenere una copia della stringa di connessione dispositivo hello. È necessario durante l'esecuzione di applicazioni di esempio hello descritte in hello le sezioni seguenti.

Dopo aver completato i passaggi di hello precedenti, si è pronti toostart esegua codice. Entrambi gli esempi di avere una costante nella parte superiore di hello del file di origine principale hello che consente di tooenter una stringa di connessione. Hello, ad esempio, la riga corrispondente dalla hello **l'hub IOT\_client\_esempio\_mqtt** applicazione viene visualizzata come indicato di seguito.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Utilizzo della libreria IoTHubClient hello

All'interno di hello **l'hub IOT\_client** cartella hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, è presente un **esempi** cartella che contiene un'applicazione denominata **l'hub IOT\_client\_esempio\_mqtt**.

versione di Windows Hello di hello **l'hub IOT\_client\_esempio\_mqtt** applicazione include hello seguente soluzione di Visual Studio:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> Se si apre il progetto in Visual Studio 2017, accettare hello richieste tooretarget hello toohello ultima versione del progetto.

Questa soluzione contiene un singolo progetto. In questa soluzione sono installati quattro pacchetti NuGet:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

È sempre necessario hello **Microsoft.Azure.C.SharedUtility** pacchetto quando si lavora con hello SDK. In questo esempio Usa il protocollo MQTT hello, pertanto è necessario includere hello **Microsoft.Azure.umqtt** e **Microsoft.Azure.IoTHub.MqttTransport** pacchetti (sono presenti pacchetti equivalenti per AMQP e HTTP ). Poiché l'esempio hello utilizza hello **IoTHubClient** libreria, è necessario includere anche hello **Microsoft.Azure.IoTHub.IoTHubClient** pacchetto della soluzione.

È possibile trovare l'implementazione di hello per l'applicazione di esempio hello in hello **l'hub IOT\_client\_esempio\_mqtt.c** file di origine.

i passaggi seguenti Hello usano questo toowalk di applicazione di esempio tramite le impostazioni necessarie hello toouse **IoTHubClient** libreria.

### <a name="initialize-hello-library"></a>Inizializzare la libreria hello

> [!NOTE]
> Prima di iniziare con le librerie di hello, potrebbe essere necessario tooperform alcune operazioni di inizializzazione specifiche della piattaforma. Ad esempio, se si intende toouse AMQP Linux è necessario inizializzare libreria OpenSSL hello. Negli esempi di hello Hello [repository GitHub](https://github.com/Azure/azure-iot-sdk-c) chiamare la funzione di utilità hello **piattaforma\_init** quando hello client avvia e chiamare hello **piattaforma\_deinit**  funzione prima della chiusura. Queste funzioni vengono dichiarate nel file di intestazione platform.h hello. Esaminare le definizioni di hello di queste funzioni per la piattaforma di destinazione in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine se è necessario tooinclude qualsiasi codice di inizializzazione specifiche della piattaforma nel client.

Innanzitutto, toostart utilizzano le librerie di hello, allocare un handle di client di IoT Hub:

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

Si passa una copia della stringa di connessione hello dispositivo ottenuto da funzione toothis di hello dispositivo explorer dello strumento. È inoltre possibile designare toouse protocollo di comunicazione hello. In questo esempio si usa MQTT, ma è possibile usare anche AMQP e HTTP.

Quando si dispone di un oggetto valido **l'hub IOT\_CLIENT\_gestire**, è possibile iniziare a chiamare toosend API hello e ricevere messaggi tooand dall'IoT Hub.

### <a name="send-messages"></a>Inviare messaggi

applicazione di esempio Hello imposta un ciclo toosend messaggi tooyour l'hub IoT. Hello frammento di codice seguente:

- Crea un messaggio.
- Aggiunge un messaggio toohello di proprietà.
- Invia un messaggio.

Prima di tutto, creare un messaggio:

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

Ogni volta che si invia un messaggio, si specifica una funzione di callback tooa di riferimento che viene richiamata quando viene inviati dati hello. In questo esempio viene chiamata la funzione di callback hello **SendConfirmationCallback**. Hello frammento di codice seguente viene illustrata questa funzione di callback:

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Si noti hello chiamata toohello **IoTHubMessage\_Destroy** funzione una volta terminato con un messaggio hello. Questa funzione libera le risorse di hello allocate al momento della creazione messaggio hello.

### <a name="receive-messages"></a>Ricevere messaggi

La ricezione di un messaggio è un'operazione asincrona. È innanzitutto necessario registrare hello callback tooinvoke quando il dispositivo hello riceve un messaggio:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

Hello ultimo parametro è un puntatore void di toowhatever desiderato. Nell'esempio hello è un numero intero tooan puntatore, ma potrebbe essere un puntatore tooa struttura più complessa di dati. Questo parametro Abilita toooperate funzione di callback hello in uno stato condiviso con chiamante hello di questa funzione.

Quando il dispositivo hello riceve un messaggio, hello funzione di callback registrato viene richiamato. Questa funzione di callback recupera:

* id di messaggio Hello e id di correlazione dal messaggio hello.
* contenuto del messaggio Hello.
* Tutte le proprietà personalizzate dal messaggio hello.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Hello utilizzare **IoTHubMessage\_GetByteArray** messaggio hello tooretrieve di funzione, che in questo esempio è una stringa.

### <a name="uninitialize-hello-library"></a>Annullare l'inizializzazione della libreria hello

Quando è terminato l'invio di eventi e la ricezione dei messaggi, è possibile annullare l'inizializzazione della libreria IoT hello. toodo in tal caso, eseguire hello in seguito a chiamata di funzione:

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Questa chiamata consente di liberare risorse hello precedentemente allocate dal hello **IoTHubClient\_CreateFromConnectionString** (funzione).

Come si può notare, è facile toosend e ricevere messaggi con hello **IoTHubClient** libreria. libreria Hello gestisce i dettagli di hello di comunicare con l'IoT Hub, tra cui toouse protocollo (dal punto di vista hello dello sviluppatore di hello, si tratta di un'opzione di configurazione minima).

Hello **IoTHubClient** libreria fornisce anche un controllo preciso come dati hello tooserialize il dispositivo invia tooIoT Hub. In alcuni casi, questo livello di controllo è un vantaggio, ma in altri è un dettaglio di implementazione che non si desidera toobe riguarda. Se è questo caso di hello, è possibile utilizzare hello **serializzatore** libreria, descritto nella sezione successiva hello.

## <a name="use-hello-serializer-library"></a>Utilizzo della libreria serializzatore hello

Concettualmente hello **serializzatore** libreria si trova nella parte superiore di hello **IoTHubClient** libreria in hello SDK. Usa hello **IoTHubClient** libreria per hello sottostante la comunicazione con l'IoT Hub, ma aggiunge funzionalità di modellazione per la rimozione di carico hello per gestire la serializzazione dei messaggi da Developer Edition hello. Il funzionamento di questa libreria può essere illustrato meglio con un esempio.

Inside hello **serializzatore** cartella hello [repository di azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), è un **esempi** cartella che contiene un'applicazione denominata **simplesample \_mqtt**. versione di Windows Hello di questo esempio include hello seguente soluzione di Visual Studio:

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> Se si apre il progetto in Visual Studio 2017, accettare hello richieste tooretarget hello toohello ultima versione del progetto.

Come esempio hello precedente, questo include diversi pacchetti NuGet:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

Si è visto la maggior parte dei pacchetti nell'esempio precedente hello, ma **Microsoft.Azure.IoTHub.Serializer** è nuovo. Questo pacchetto è necessario quando si utilizza hello **serializzatore** libreria.

È possibile trovare l'implementazione di hello dell'applicazione di esempio hello in hello **simplesample\_mqtt.c** file.

Hello nelle sezioni seguenti vengono illustrati le parti principali di questo esempio hello.

### <a name="initialize-hello-library"></a>Inizializzare la libreria hello

utilizzo di hello toostart **serializzatore** libreria, l'inizializzazione di hello chiamata API:

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

Hello chiamata toohello **serializzatore\_init** funzione è una singola chiamata e inizializza hello raccolta sottostante. Chiamare quindi hello **IoTHubClient\_LL\_CreateFromConnectionString** funzione, che è hello stessa API come hello **IoTHubClient** esempio. Questa chiamata imposta la stringa di connessione del dispositivo (questa chiamata è anche in cui si sceglie di protocollo hello desiderato toouse). In questo esempio utilizza MQTT trasporto hello, ma è possibile usare AMQP o HTTP.

Chiamare infine hello **crea\_modello\_istanza** (funzione). **WeatherStation** hello uno spazio dei nomi del modello di hello e **ContosoAnemometer** hello nome del modello di hello. Una volta creata l'istanza del modello hello, è possibile utilizzare toostart inviando e ricevendo messaggi. Tuttavia, è importante toounderstand è il tipo di modello.

### <a name="define-hello-model"></a>Definire il modello di hello

Un modello in hello **serializzatore** libreria definisce messaggi hello che il dispositivo può inviare tooIoT Hub e hello i messaggi, chiamato *azioni* in hello modeling language, che può ricevere. Si definisce un modello usando un set di macro di C come hello **simplesample\_mqtt** applicazione di esempio:

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Hello **iniziare\_dello spazio dei nomi** e **fine\_dello spazio dei nomi** entrambi eseguire hello dello spazio dei nomi del modello di hello come argomento. È previsto che svolgono queste macro è definizione hello del modello o i modelli e strutture dei dati che utilizzano modelli hello hello.

In questo esempio è presente un singolo modello chiamato **ContosoAnemometer**. Questo modello definisce due tipi di dati che il dispositivo può inviare tooIoT Hub: **DeviceId** e **WindSpeed**. Definisce anche tre azioni (messaggi) che il dispositivo può ricevere, cioè **TurnFanOn**, **TurnFanOff** e **SetAirResistance**. Ogni elemento dati ha un tipo e ogni azione un nome e facoltativamente un set di parametri.

dati Hello e azioni definite nel modello hello definiscono una superficie API che è possibile utilizzare toosend messaggi tooIoT Hub e rispondere dispositivo toohello toomessages inviato. L'uso di questo modello può essere illustrato meglio con un esempio.

### <a name="send-messages"></a>Inviare messaggi

modello Hello definisce i dati di hello è possibile inviare tooIoT Hub. In questo esempio, che indica una delle hello due elementi di dati definiti tramite hello **WITH_DATA** (macro). Esistono diversi toosend necessarie di passaggi **DeviceId** e **WindSpeed** hub IoT tooan di valori. i dati di hello tooset da toosend per primo è Hello:

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

Hello modello definita in precedenza consente valori hello tooset impostando i membri di un **struct**. Quindi serializzare il messaggio hello da toosend:

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

Questo codice serializza i buffer di dispositivo a cloud tooa hello (a cui fa riferimento **destinazione**). codice Hello richiama quindi hello **sendMessage** funzione toosend hello messaggio tooIoT Hub:

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


secondo parametro toolast di Hello **IoTHubClient\_LL\_SendEventAsync** è una funzione di callback tooa di riferimento che viene chiamata quando viene ricevuti correttamente i dati hello. Di seguito è la funzione di callback hello nell'esempio hello:

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

Hello secondo parametro è un contesto di toouser puntatore. lo stesso puntatore passato troppo Hello**IoTHubClient\_LL\_SendEventAsync**. In questo caso, il contesto di hello è un contatore semplice, ma è possibile assegnare qualsiasi.

Questo è tutto è toosending i messaggi da dispositivo a cloud. Hello solo cosa toocover a sinistra è come tooreceive messaggi.

### <a name="receive-messages"></a>Ricevere messaggi

Ricezione di un messaggio in modo simile toohello funzionamento messaggi in hello **IoTHubClient** libreria. Prima di tutto occorre registrare la funzione di callback di un messaggio.

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

È quindi necessario scrivere hello di callback che viene richiamato quando viene ricevuto un messaggio:

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

Questo codice boilerplate--è hello uguali per una soluzione. Questa funzione riceve messaggi hello e si occupa di routing toohello funzione appropriata tramite chiamata hello troppo**EXECUTE\_comando**. funzione Hello chiamata a questo punto dipende dalla definizione di hello di azioni di hello nel modello.

Quando si definisce un'azione nel modello, è necessario tooimplement una funzione che viene chiamata quando il dispositivo riceve il messaggio hello corrispondente. Ad esempio, se il modello definisce questa azione:

```c
WITH_ACTION(SetAirResistance, int, Position)
```

Definire una funzione con questa firma:

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Si noti come hello nome della funzione hello hello di corrisponde azione hello nel modello hello e che hello della funzione hello corrispondano hello parametri specificati per l'azione di hello. primo parametro Hello è sempre necessario e contiene un'istanza di toohello indicatore di misura del modello.

Quando il dispositivo di hello riceve un messaggio che corrisponde alla firma, la funzione corrispondente hello viene chiamata. Pertanto, a parte con il codice di boilerplate hello tooinclude da **IoTHubMessage**, la ricezione di messaggi è sufficiente definire una funzione semplice per ogni azione definita nel modello.

### <a name="uninitialize-hello-library"></a>Annullare l'inizializzazione della libreria hello

Quando è terminato l'invio dei dati e la ricezione dei messaggi, è possibile annullare l'inizializzazione della libreria IoT hello:

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

Ognuna di queste tre funzioni in linea con hello tre funzioni inizializzazione descritte in precedenza. Chiamando questi API si assicura che siano liberate le risorse allocate in precedenza.

## <a name="next-steps"></a>Passaggi successivi

In questo articolo coperto nozioni fondamentali di hello dell'uso delle librerie di hello in hello **dispositivo IoT di Azure SDK per C**. È stata fornita toounderstand sufficienti informazioni cosa è incluso in hello SDK, architettura e come tooget ha iniziato a lavorare con hello gli esempi di Windows. articolo successivo Hello continua descrizione hello di hello SDK per spiegare in che [ulteriori informazioni sulla raccolta IoTHubClient hello](iot-hub-device-sdk-c-iothubclient.md).

toolearn più sullo sviluppo per l'IoT Hub, vedere hello [Azure IoT SDK][lnk-sdks].

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
