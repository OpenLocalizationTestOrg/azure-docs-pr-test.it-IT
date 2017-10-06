---
title: il dispositivo di IoT aaaAzure SDK per C - serializzatore | Documenti Microsoft
description: La libreria di serializzatore hello toouse nel dispositivo di Azure IoT hello SDK per App per dispositivi toocreate C che comunicano con un hub IoT.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>Azure IoT SDK per dispositivi C: altre informazioni sul serializzatore
Hello [innanzitutto articolo](iot-hub-device-sdk-c-intro.md) in hello questa serie introdotto **dispositivo IoT di Azure SDK per C**. articolo successivo hello fornita una descrizione più dettagliata di hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). In questo articolo viene completata la copertura di hello SDK fornendo una descrizione più dettagliata di hello rimanenti componente: hello **serializzatore** libreria.

articolo introduttivo di Hello descritto come hello toouse **serializzatore** libreria toosend eventi tooand ricevere messaggi dall'IoT Hub. In questo articolo viene estesa la discussione, fornendo una spiegazione più completa della procedura toomodel i dati con hello **serializzatore** linguaggio macro. Hello sono inoltre incluse ulteriori informazioni su come libreria hello serializza i messaggi (e in alcuni casi come è possibile controllare il comportamento di serializzazione hello). Verranno inoltre descritti alcuni è possibile modificare i parametri che determinano dimensioni hello dei modelli di hello create.

Infine, articolo hello effettua nuovamente richieste alcune informazioni fornite negli articoli precedenti, ad esempio di messaggio e la gestione di proprietà. Come verrà individuato, il lavoro di tali funzionalità in hello stesso tramite hello **serializzatore** libreria come avviene con hello **IoTHubClient** libreria.

Tutti gli elementi descritti in questo articolo si basa sull'hello **serializzatore** esempi SDK. Se si desidera toofollow lungo, vedere hello **simplesample\_amqp** e **simplesample\_http** applicazioni contenute nel dispositivo di Azure IoT hello SDK per C.

È possibile trovare hello [ **dispositivo IoT di Azure SDK per C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repository e visualizzarne i dettagli di hello API in hello [riferimento all'API C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-modeling-language"></a>linguaggio di modellazione Hello
Hello [articolo introduttivo](iot-hub-device-sdk-c-intro.md) in hello questa serie introdotto **dispositivo IoT di Azure SDK per C** modeling language tramite l'esempio hello disponibile in hello **simplesample\_amqp**  applicazione:

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Come si può notare, hello linguaggio di modellazione è basato sulle macro di C. Si inizia sempre la definizione con **BEGIN\_NAMESPACE** e si termina sempre con **END\_NAMESPACE**. È comune tooname hello dello spazio dei nomi per la società o, come nel seguente esempio, il progetto hello che si sta lavorando.

Cosa deve essere posizionato all'interno dello spazio dei nomi hello sono definizioni di modello. In questo caso è presente un singolo modello per un anemometro. In questo caso, modello hello può essere modificato, ma in genere denominata per il dispositivo hello o un tipo di dati si desidera tooexchange con l'IoT Hub.  

I modelli contengono una definizione di eventi hello è possibile in ingresso tooIoT Hub (hello *dati*) nonché messaggi hello è possibile ricevere dall'IoT Hub (hello *azioni*). Come si vede dall'esempio hello, gli eventi hanno un tipo e un nome. le azioni hanno un nome e i parametri facoltativi (ognuno con un tipo).

Cosa non viene dimostrata in questo esempio sono tipi di dati aggiuntivi che sono supportati da hello SDK. che saranno trattati in seguito.

> [!NOTE]
> IoT Hub fa riferimento a un dispositivo invia tooit come dati di toohello *eventi*, mentre il linguaggio di modellazione hello fa riferimento tooit come *dati* (definito tramite **WITH_DATA**). Analogamente, l'IoT Hub fa riferimento a dati toohello inviati toodevices come *messaggi*, mentre il linguaggio di modellazione hello fa riferimento tooit come *azioni* (definito tramite **WITH_ACTION**). Tenere presente che questi termini possono essere usati in modo intercambiabile in questo articolo.
> 
> 

### <a name="supported-data-types"></a>Tipi di dati supportati
Hello seguenti tipi di dati è supportato nei modelli creati con hello **serializzatore** libreria:

| Tipo | Descrizione |
| --- | --- |
| double |Numero a virgola mobile a precisione doppia |
| int |Intero a 32 bit |
| float |Numero a virgola mobile a precisione singola |
| long |Intero lungo |
| int8\_t |Intero a 8 bit |
| int16\_t |Intero a 16 bit |
| int32\_t |Intero a 32 bit |
| int64\_t |Intero a 64 bit |
| bool |boolean |
| ascii\_char\_ptr |Stringa ASCII |
| EDM\_DATE\_TIME\_OFFSET |Offset data/ora |
| EDM\_GUID |GUID |
| EDM\_BINARY |binary |
| DECLARE\_STRUCT |Tipo di dati complesso |

Iniziamo con hello ultimo tipo di dati. Hello **DECLARE\_STRUCT** consente tipi di dati complessi toodefine, ovvero raggruppamenti di hello ad altri tipi primitivi. Questi raggruppamenti consentono toodefine un modello simile al seguente:

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

Il modello contiene un singolo evento dati di tipo **TestType**. **TestType** è un tipo complesso che include molti membri, quali collettivamente vengono illustrati i tipi di primitivi hello supportati dal hello **serializzatore** linguaggio di modellazione.

Con un modello simile al seguente, è possibile scrivere codice toosend dati tooIoT Hub che viene visualizzato come segue:

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

In pratica, assegniamo membro tooevery valore hello **Test** struttura e chiamando quindi **SendAsync** toosend hello **Test** dati nel cloud toohello evento. **SendAsync** è una funzione di supporto che invia un tooIoT di dati singolo evento Hub:

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

Questa funzione serializza hello dato dati evento e lo invia tooIoT Hub utilizzando **IoTHubClient\_SendEventAsync**. Si tratta di hello stesso codice descritto negli articoli precedenti (**SendAsync** incapsula la logica di hello in una comoda funzione).

È un altra funzione di supporto utilizzata nel codice precedente hello **GetDateTimeOffset**. Questa funzione Trasforma hello momento in un valore di tipo **EDM\_data\_ora\_OFFSET**:

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

Se si esegue questo codice, hello seguente messaggio viene inviato tooIoT Hub:

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Si noti che la serializzazione di hello è JSON, è formato hello generato da hello **serializzatore** libreria. Si noti che ogni membro di hello serializzato l'oggetto JSON corrisponde anche i membri di hello di hello **TestType** definiti nel modello in esame. i valori Hello anche corrispondere esattamente a quelli usati nel codice hello. Tuttavia, si noti che i dati binari hello sono con codifica base64: "AQID" è hello codifica base64 del {0x01, 0x02, 0x03}.

In questo esempio viene hello vantaggio offerto dall'utilizzo hello **serializzatore** libreria - offre il cloud di toohello toosend JSON, senza dovere tooexplicitly di gestire la serializzazione dell'applicazione. Tutto tooworry su è l'impostazione valori hello di hello eventi dati il nostro modello e quindi chiamare toosend API semplice tali cloud toohello eventi.

Con queste informazioni, è possibile definire i modelli che includono l'intervallo di hello dei tipi di dati supportati, inclusi i tipi complessi (è possibile includere anche i tipi complessi all'interno di altri tipi complessi). Tuttavia, ha serializzato JSON generato da hello esempio precedente consente di visualizzare un punto importante. *Come* inviare dati con hello **serializzatore** libreria determina esattamente come è formata hello JSON. Di seguito viene trattato questo punto specifico.

## <a name="more-about-serialization"></a>Altre informazioni sulla serializzazione
la sezione precedente di Hello evidenzia un esempio di output di hello generati da hello **serializzatore** libreria. In questa sezione verrà illustrato come libreria hello serializza i dati e come sia possibile controllare questo comportamento utilizzando dalle API di serializzazione hello.

In ordine tooadvance hello discussione sulla serializzazione si utilizzerà un nuovo modello basato su un termostato. In primo luogo, consente di fornire alcune informazioni generali sullo scenario hello stiamo cercando tooaddress.

È necessario un termostato che misura la temperatura e umidità toomodel. Ogni blocco di dati verrà toobe inviati tooIoT Hub in modo diverso. Per impostazione predefinita, hello ingresses termostato un evento di temperatura una volta ogni 2 minuti. un evento umidità è ingressed una volta ogni 15 minuti. Quando degli eventi è ingressed, deve includere un timestamp che indica il tempo di hello tale temperatura corrispondente hello o umidità è stata misurata.

Dato questo scenario, verrà illustrata in dati di due modi diversi toomodel hello e spiega effetto hello che modellazione è su hello serializzato output.

### <a name="model-1"></a>Modello 1
Ecco hello prima versione di un modello che supporta hello scenario precedente:

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

Si noti che modello hello include due eventi di dati: **temperatura** e **umidità**. A differenza degli esempi precedenti, il tipo di hello di ogni evento è una struttura definita utilizzando **DECLARE\_STRUCT**. **TemperatureEvent** include una misura della temperatura e un timestamp. **HumidityEvent** contiene una misura dell'umidità e un timestamp. Questo modello offre dati di hello toomodel un modo semplice per uno scenario di hello descritto in precedenza. Quando si invia un cloud toohello evento, ti invieremo sia un temperatura, timestamp o una coppia di umidità o timestamp.

È possibile inviare un cloud di toohello evento temperatura utilizzando codice simile hello seguente:

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Verranno utilizzati valori hardcoded per temperatura e umidità nel codice di esempio hello, ma si supponga che vengono effettivamente recuperate questi valori eseguendo il campionamento dei sensori corrispondente hello in termostato hello.

codice Hello precedente utilizza hello **GetDateTimeOffset** helper che è stata introdotta in precedenza. Per motivi che diventeranno deselezionare successive, questo codice consente di separare in modo esplicito attività hello di serializzazione e di invio evento hello. codice precedente Hello serializza evento temperatura hello in un buffer. Quindi, **sendMessage** è una funzione di supporto (incluso in **simplesample\_amqp**) che invia hello tooIoT evento Hub:

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

Questo codice è un subset di hello **SendAsync** helper descritte nella sezione precedente hello, pertanto non verranno esaminate su di essa nuovamente qui.

Quando si esegue hello codice toosend hello temperatura dall'evento precedente, questa forma serializzata dell'evento hello viene inviata tooIoT Hub:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Viene inviato un evento temperatura di tipo **TemperatureEvent** la cui struttura contiene un membro **Temperature** e **Time**. Ciò si riflette direttamente nei dati serializzato hello.

In modo analogo è possibile inviare un evento umidità con questo codice:

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

form serializzato Hello che ha inviato tooIoT Hub visualizzato come segue:

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Anche in questo caso, è un comportamento previsto.

Con questo modello si può immaginare come sia facile aggiungere altri eventi. Si definiscono più strutture utilizzando **DECLARE\_STRUCT**e includere l'evento corrispondente hello in hello modello utilizzando **WITH\_dati**.

A questo punto, in modo che includa hello è opportuno modificare il modello di hello stessi dati ma con una struttura diversa.

### <a name="model-2"></a>Modello 2
Si consideri questo toohello modello alternativo uno sopra:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

In questo caso è stato eliminato hello **DECLARE\_STRUCT** macro e sono semplicemente la definizione di elementi di dati hello da questo scenario utilizzando i tipi semplici di hello linguaggio di modellazione.

Solo per il momento di hello si ignora hello **ora** evento. Con tale aside, ecco tooingress codice hello **temperatura**:

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Questo codice invia seguente hello serializzato tooIoT evento Hub:

```
{"Temperature":75}
```

E codice hello per l'invio di eventi umidità hello viene visualizzato come segue:

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Questo codice invia questo tooIoT Hub:

```
{"Humidity":45}
```

Di nuovo nulla di insolito fino a questo punto. A questo punto è necessario modificare come utilizziamo macro SERIALIZE hello.

Hello **SERIALIZE** (macro) può richiedere più eventi di dati come argomenti. In questo modo ci hello tooserialize **temperatura** e **umidità** insieme a eventi e li inviano tooIoT Hub in un'unica chiamata:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Si può immaginare che il risultato di hello di questo codice è che gli eventi di due dati vengono inviati tooIoT Hub:

[

{"Temperature":75},

{"Humidity":45}

]

In altre parole, è prevedibile che questo codice è hello stesso come l'invio di **temperatura** e **umidità** separatamente. È semplicemente un toopass praticità entrambi gli eventi troppo**SERIALIZE** in hello stessa chiamata. Tuttavia, non è hello caso. Al contrario, codice hello precedente invia questo tooIoT di dati singolo evento Hub:

{"Temperature":75, "Humidity":45}

Può sembrare strano perché il modello definisce **Temperature** e **Humidity** come due eventi *distinti*:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Ulteriori toohello punto, è non modello questi eventi in cui **temperatura** e **umidità** in hello stessa struttura:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

Se è stato usato questo modello, sarebbe più facile toounderstand come **temperatura** e **umidità** verrebbe inviato in hello stesso il messaggio serializzato. Tuttavia potrebbe non essere chiaro perché funziona in questo modo, quando si passano entrambi gli eventi di dati troppo**SERIALIZE** utilizzando il modello 2.

Questo comportamento è toounderstand più semplice se si conoscono l'ipotesi di hello che hello **serializzatore** effettua libreria. senso toomake di questo è necessario tornare indietro tooour modello:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Pensare al modello in termini di "orientato a oggetti". In questo caso si modella un dispositivo fisico (Thermostat), che include attributi come **Temperature** e **Humidity**.

È possibile inviare hello stato completo nello stato del modello con codice simile hello seguente:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Supponendo che i valori hello di temperatura e umidità ora vengono impostati, si vedrà un evento, ad esempio, questo tooIoT inviato Hub:

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

A volte può essere solo toosend *alcuni* proprietà di hello modello toohello cloud (Ciò vale soprattutto se il modello contiene un numero elevato di eventi di dati). È utile toosend solo un subset di eventi di dati, come nell'esempio precedente:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Questa operazione genera esattamente hello dell'evento stesso serializzato come se fosse stata definita una **TemperatureEvent** con un **temperatura** e **ora** membro, come se si con modello di 1. In questo caso è stato in grado di toogenerate esattamente hello stesso dell'evento serializzato utilizzando un diverso modello (modello di 2) perché è stato chiamato **SERIALIZE** in modo diverso.

Hello punto importante è che se si passano più eventi di dati troppo**SERIALIZE,** quindi si presuppone che ogni evento è una proprietà in un singolo oggetto JSON.

approccio migliore Hello varia a seconda di come si pensa di modello. Se si sta inviando il messaggio "eventi" toohello cloud e ogni evento contiene un set definito di proprietà, quindi primo approccio hello molto più utile. In questo caso si utilizzerebbe **DECLARE\_STRUCT** toodefine hello struttura di ogni evento e quindi includerli nel modello con hello **WITH\_dati** (macro). Quindi inviare ogni evento come in hello primo esempio. In questo approccio solo passare un singolo evento troppo**SERIALIZZATORE**.

Se si pensa al modello in modo orientato, secondo approccio hello può soddisfare è. In questo caso, hello elementi definiti mediante **WITH\_dati** hello "proprietà" dell'oggetto. Passare a qualsiasi subset di eventi troppo**SERIALIZE** che si desidera che, a seconda della quantità di stato "dell'oggetto" si desidera toosend toohello cloud.

Nessun approccio è giusto o sbagliato. Solo essere a conoscenza di come hello **serializzatore** funzionamento libreria e approccio di modellazione hello di selezione che meglio si adatta alle esigenze.

## <a name="message-handling"></a>Gestione dei messaggi
In questo articolo finora è descritto solo l'invio degli eventi tooIoT Hub e non è stata indirizzata la ricezione di messaggi. Hello motivo è che è necessario tooknow sulla ricezione dei messaggi in gran parte interessato un [precedentemente articolo](iot-hub-device-sdk-c-intro.md). Tenere presente, come detto in quell'articolo, che i messaggi vengono elaborati registrando una funzione di richiamata dei messaggi:

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

È quindi possibile scrivere hello di callback che viene richiamato quando viene ricevuto un messaggio:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
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

Questa implementazione di **IoTHubMessage** hello di chiamate di funzione specifica per ogni azione nel modello. Ad esempio, se il modello definisce questa azione:

```
WITH_ACTION(SetAirResistance, int, Position)
```

È necessario definire una funzione con questa firma.

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** viene quindi chiamato quando il messaggio viene inviato tooyour dispositivo.

Cosa spiegare non è ancora la versione di hello serializzato del messaggio ha un aspetto simile. In altre parole, se si desidera toosend un **SetAirResistance** dispositivo tooyour messaggio, cosa che hanno l'aspetto come?

Se si invia un dispositivo tooa messaggio, si imposterebbe tramite il servizio di Azure IoT hello SDK. È comunque necessario tooknow stringa toosend tooinvoke una determinata azione. formato generale di Hello per l'invio di un messaggio viene visualizzato come segue:

```
{"Name" : "", "Parameters" : "" }
```

Si sta inviando un oggetto serializzato JSON con due proprietà: **nome** hello nome dell'azione hello (messaggio) e **parametri** contiene parametri hello dell'azione.

Ad esempio, tooinvoke **SetAirResistance** è possibile inviare questo dispositivo tooa messaggio:

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

nome dell'azione Hello deve corrispondere esattamente a un'azione definita nel modello. i nomi di parametro Hello devono corrispondere. Tenere presente anche la distinzione tra maiuscole e minuscole. **Name** e **Parameters** sono sempre in maiuscolo. Verificare che toomatch hello casi il nome dell'azione e i parametri nel modello. In questo esempio, il nome dell'azione hello è "SetAirResistance" e non "setairresistance".

due altre azioni Hello **TurnFanOn** e **TurnFanOff** può essere richiamato mediante l'invio di questi dispositivi tooa messaggi:

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

Questa sezione viene descritto tutto ciò che occorre tooknow quando l'invio di eventi e la ricezione di messaggi con hello **serializzatore** libreria. Prima di proseguire, si esamineranno alcuni parametri che è possibile configurare per controllare le dimensioni del modello.

## <a name="macro-configuration"></a>Configurazione delle macro
Se si usa hello **serializzatore** libreria una parte importante di hello SDK toobe comunicata viene trovata nella libreria di azure-c-condivisi-utilità hello.
Se sono stati clonati repository hello Azure-iot-sdk-c da GitHub utilizzando hello ricorsiva - opzione, sarà possibile reperire la raccolta di utilità condivisi qui:

```
.\\c-utility
```

Se non sono stati clonati libreria hello, sarà possibile trovarlo [qui](https://github.com/Azure/azure-c-shared-utility).

Nella raccolta di utilità condivisi hello, sarà possibile reperire hello seguente cartella:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Questa cartella contiene una soluzione di Visual Studio chiamata **macro\_utils\_h\_generator.sln**:

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

il programma di Hello in questa soluzione genera hello **macro\_utils.h** file. È una macro predefinita\_file utils.h incluso con hello SDK. Questa soluzione consente toomodify alcuni parametri e quindi creare nuovamente il file di intestazione in base a questi parametri di hello.

Hello due parametri chiave toobe riguarda sono **nArithmetic** e **nMacroParameters** che sono definite in queste due righe trovate nella macro\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Questi valori sono i parametri predefiniti hello inclusi hello SDK. Ogni parametro ha hello seguente significato:

* nMacroParameters: controlla la quantità di parametri che possono essere inclusi in una definizione di macro DECLARE\_MODEL.
* nArithmetic: numero totale di controlli hello dei membri è consentito in un modello.

motivo di Hello che questi parametri sono importanti è quanto controllano il modello può essere. Considerare ad esempio questa definizione di modello:

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Come già accennato, **DECLARE\_MODEL** è semplicemente una macro C. i nomi del modello di hello e hello Hello **WITH\_dati** istruzione (ancora un'altra macro) è parametri di **DECLARE\_modello**. **nMacroParameters** definisce il numero di parametri che può essere incluso in **DECLARE\_MODELLO**. In realtà definisce la quantità di eventi dati e dichiarazioni di azione supportata. Di conseguenza, hello predefinito Limit 124 ciò significa che è possibile definire un modello con una combinazione di azioni di circa 60 e gli eventi di dati. Se si tenta di tooexceed questo limite, si riceveranno errori del compilatore che la ricerca di toothis simile:

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Hello **nArithmetic** parametro è di più sui meccanismi interni di hello del linguaggio macro hello di applicazione.  Controlla numero totale di hello di membri è consentito nel modello, tra cui **DECLARE_STRUCT** macro. Se iniziano a essere visualizzati errori del compilatore come questo, provare ad aumentare il valore di **nArithmetic**:

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Se si desidera toochange questi parametri, modificare i valori hello nella macro hello\_utils.tt file, la macro hello recompile\_utils\_h\_generator.sln soluzione e programma compilato hello esecuzione. A tale scopo, una nuova macro\_utils.h file viene generato e posizionato in hello.\\ comuni\\directory inc.

In ordine toouse hello nuova versione di una macro\_utils.h, Rimuovi hello **serializzatore** pacchetto NuGet dalla soluzione e al suo posto includono hello **serializzatore** progetto di Visual Studio. In questo modo il toocompile codice rispetto al codice sorgente hello della libreria di serializzatore hello. Ciò include la macro di hello aggiornato\_utils.h. Se si desidera toodo per **simplesample\_amqp**, iniziare a rimuovere il pacchetto NuGet hello per la libreria serializzatore hello dalla soluzione hello:

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

Aggiungere quindi questa tooyour di progetto, soluzione di Visual Studio:

> .\\c\\serializer\\build\\windows\\serializer.vcxproj
> 
> 

Al termine, la soluzione dovrebbe avere un aspetto analogo al seguente:

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Ora quando si compila la soluzione, hello aggiornato macro\_utils.h è incluso nel file binario.

Se si aumentano molto questi valori, potrebbero essere superati i limiti del compilatore. toothis punto, hello **nMacroParameters** hello parametro principale con cui toobe in questione. Specifica C99 Hello specifica che un minimo di 127 parametri siano consentiti in una definizione di macro. Hello compilatore Microsoft segue spec hello esattamente (e ha un limite di 127), in modo non sarà in grado di tooincrease **nMacroParameters** oltre predefinito hello. Altri compilatori possono consentire di toodo così (ad esempio, il compilatore di GNU hello supporta un limite maggiore).

Finora abbiamo trattato quasi tutto ciò che occorre tooknow sulla modalità in codice con hello toowrite **serializzatore** libreria. Prima di concludere, ecco di seguito alcuni argomenti degli articoli precedenti che potrebbero risultare interessanti.

## <a name="hello-lower-level-apis"></a>Hello API di livello inferiore
applicazione di esempio Hello in cui è attivo in questo articolo è **simplesample\_amqp**. In questo esempio utilizza hello (hello non-"LL") API toosend eventi di livello superiore e ricevere messaggi. Se si usano queste API, viene eseguito un thread in background che si occupa dell'invio degli eventi e della ricezione dei messaggi. Tuttavia, è possibile utilizzare tooeliminate (ova) le API di livello inferiore hello questo thread in background e assumere il controllo esplicito quando si inviano eventi o ricevere messaggi da cloud hello.

Come descritto in un [articolo precedente](iot-hub-device-sdk-c-iothubclient.md), vi è un set di funzioni che è costituito da hello API di livello superiore:

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_Destroy

Queste API sono illustrate in **simplesample\_amqp**.

È disponibile anche set analogo di API di livello inferiore.

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Si noti che operazioni API di livello inferiore hello hello esattamente come descritto negli articoli precedente hello. È possibile utilizzare primo set di API di hello se si desidera un toohandle di background thread eventi inviando e ricevendo messaggi. Utilizzare secondo set di API di hello se si desidera il controllo esplicito quando si inviare e ricevere i dati dall'IoT Hub. Uno dei due set di API lavoro altrettanto bene con hello **serializzatore** libreria.

Per un esempio di come hello livello inferiore vengono utilizzate le API con hello **serializzatore** libreria, vedere hello **simplesample\_http** dell'applicazione.

## <a name="additional-topics"></a>Argomenti aggiuntivi
Alcuni altri argomenti che vale la pena citare riguardano la gestione delle proprietà, l'uso di credenziali del dispositivo alternative e le opzioni di configurazione. Ecco tutti gli argomenti illustrati in un [articolo precedente](iot-hub-device-sdk-c-iothubclient.md). Hello punto principale è che tutte queste funzionalità funzionano in hello stesso modo con hello **serializzatore** libreria come avviene con hello **IoTHubClient** libreria. Ad esempio, se si desidera evento tooan di tooattach proprietà dal modello, utilizzare **IoTHubMessage\_proprietà** e **mappa**\_**AddorUpdate**, hello come descritto in precedenza:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Se evento hello è stato generato da hello **serializzatore** libreria o creato manualmente tramite hello **IoTHubClient** libreria non è rilevante.

Per hello alternare le credenziali di dispositivo, utilizzando **IoTHubClient\_LL\_crea** funziona così come **IoTHubClient\_CreateFromConnectionString** per allocare un **l'hub IOT\_CLIENT\_gestire**.

Infine, se si usa hello **serializzatore** libreria, è possibile impostare le opzioni di configurazione con **IoTHubClient\_LL\_SetOption** esattamente come è stato fatto quando si utilizza hello **IoTHubClient** libreria.

Una funzionalità che è univoco toohello **serializzatore** libreria sono inizializzazione hello API. Prima di iniziare a lavorare con libreria hello, è necessario chiamare **serializzatore\_init**:

```
serializer_init(NULL);
```

Questa operazione viene eseguita subito prima di chiamare **IoTHubClient\_CreateFromConnectionString**.

Analogamente, quando si completa l'utilizzo di libreria hello, hello dall'ultima chiamata ti è troppo**serializzatore\_deinit**:

```
serializer_deinit();
```

In caso contrario, tutti hello altre funzionalità elencate in precedenza lavoro stesso hello in hello **serializzatore** libreria come in hello **IoTHubClient** libreria. Per ulteriori informazioni su questi argomenti, vedere hello [articolo precedente](iot-hub-device-sdk-c-iothubclient.md) di questa serie.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo descrive in dettaglio hello univoco aspetti hello **serializzatore** libreria contenute in hello **dispositivo IoT di Azure SDK per C**. Con le informazioni di hello fornite si deve avere una buona conoscenza dei modelli di eventi toosend come toouse e ricevere messaggi dall'IoT Hub.

Questo conclude anche serie hello tre parti come applicazioni toodevelop con hello **dispositivo IoT di Azure SDK per C**. Questo deve essere sufficiente get solo toonot informazioni che è stata avviata ma offrono una conoscenza approfondita del funzionamento di hello API. Per ulteriori informazioni, in sono disponibili alcuni esempi hello che SDK non contenute in questo articolo. In caso contrario, hello [documentazione SDK](https://github.com/Azure/azure-iot-sdk-c) è un'ottima risorsa per altre informazioni.

toolearn più sullo sviluppo per l'IoT Hub, vedere hello [Azure IoT SDK][lnk-sdks].

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
