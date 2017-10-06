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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="61fe3-103">Azure IoT SDK per dispositivi C: altre informazioni sul serializzatore</span><span class="sxs-lookup"><span data-stu-id="61fe3-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="61fe3-104">Hello [innanzitutto articolo](iot-hub-device-sdk-c-intro.md) in hello questa serie introdotto **dispositivo IoT di Azure SDK per C**. articolo successivo hello fornita una descrizione più dettagliata di hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="61fe3-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="61fe3-105">In questo articolo viene completata la copertura di hello SDK fornendo una descrizione più dettagliata di hello rimanenti componente: hello **serializzatore** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="61fe3-106">articolo introduttivo di Hello descritto come hello toouse **serializzatore** libreria toosend eventi tooand ricevere messaggi dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61fe3-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="61fe3-107">In questo articolo viene estesa la discussione, fornendo una spiegazione più completa della procedura toomodel i dati con hello **serializzatore** linguaggio macro.</span><span class="sxs-lookup"><span data-stu-id="61fe3-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="61fe3-108">Hello sono inoltre incluse ulteriori informazioni su come libreria hello serializza i messaggi (e in alcuni casi come è possibile controllare il comportamento di serializzazione hello).</span><span class="sxs-lookup"><span data-stu-id="61fe3-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="61fe3-109">Verranno inoltre descritti alcuni è possibile modificare i parametri che determinano dimensioni hello dei modelli di hello create.</span><span class="sxs-lookup"><span data-stu-id="61fe3-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="61fe3-110">Infine, articolo hello effettua nuovamente richieste alcune informazioni fornite negli articoli precedenti, ad esempio di messaggio e la gestione di proprietà.</span><span class="sxs-lookup"><span data-stu-id="61fe3-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="61fe3-111">Come verrà individuato, il lavoro di tali funzionalità in hello stesso tramite hello **serializzatore** libreria come avviene con hello **IoTHubClient** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="61fe3-112">Tutti gli elementi descritti in questo articolo si basa sull'hello **serializzatore** esempi SDK.</span><span class="sxs-lookup"><span data-stu-id="61fe3-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="61fe3-113">Se si desidera toofollow lungo, vedere hello **simplesample\_amqp** e **simplesample\_http** applicazioni contenute nel dispositivo di Azure IoT hello SDK per C.</span><span class="sxs-lookup"><span data-stu-id="61fe3-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="61fe3-114">È possibile trovare hello [ **dispositivo IoT di Azure SDK per C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repository e visualizzarne i dettagli di hello API in hello [riferimento all'API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="61fe3-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="61fe3-115">linguaggio di modellazione Hello</span><span class="sxs-lookup"><span data-stu-id="61fe3-115">hello modeling language</span></span>
<span data-ttu-id="61fe3-116">Hello [articolo introduttivo](iot-hub-device-sdk-c-intro.md) in hello questa serie introdotto **dispositivo IoT di Azure SDK per C** modeling language tramite l'esempio hello disponibile in hello **simplesample\_amqp**  applicazione:</span><span class="sxs-lookup"><span data-stu-id="61fe3-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="61fe3-117">Come si può notare, hello linguaggio di modellazione è basato sulle macro di C.</span><span class="sxs-lookup"><span data-stu-id="61fe3-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="61fe3-118">Si inizia sempre la definizione con **BEGIN\_NAMESPACE** e si termina sempre con **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="61fe3-119">È comune tooname hello dello spazio dei nomi per la società o, come nel seguente esempio, il progetto hello che si sta lavorando.</span><span class="sxs-lookup"><span data-stu-id="61fe3-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="61fe3-120">Cosa deve essere posizionato all'interno dello spazio dei nomi hello sono definizioni di modello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="61fe3-121">In questo caso è presente un singolo modello per un anemometro.</span><span class="sxs-lookup"><span data-stu-id="61fe3-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="61fe3-122">In questo caso, modello hello può essere modificato, ma in genere denominata per il dispositivo hello o un tipo di dati si desidera tooexchange con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61fe3-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="61fe3-123">I modelli contengono una definizione di eventi hello è possibile in ingresso tooIoT Hub (hello *dati*) nonché messaggi hello è possibile ricevere dall'IoT Hub (hello *azioni*).</span><span class="sxs-lookup"><span data-stu-id="61fe3-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="61fe3-124">Come si vede dall'esempio hello, gli eventi hanno un tipo e un nome. le azioni hanno un nome e i parametri facoltativi (ognuno con un tipo).</span><span class="sxs-lookup"><span data-stu-id="61fe3-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="61fe3-125">Cosa non viene dimostrata in questo esempio sono tipi di dati aggiuntivi che sono supportati da hello SDK.</span><span class="sxs-lookup"><span data-stu-id="61fe3-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="61fe3-126">che saranno trattati in seguito.</span><span class="sxs-lookup"><span data-stu-id="61fe3-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="61fe3-127">IoT Hub fa riferimento a un dispositivo invia tooit come dati di toohello *eventi*, mentre il linguaggio di modellazione hello fa riferimento tooit come *dati* (definito tramite **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="61fe3-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="61fe3-128">Analogamente, l'IoT Hub fa riferimento a dati toohello inviati toodevices come *messaggi*, mentre il linguaggio di modellazione hello fa riferimento tooit come *azioni* (definito tramite **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="61fe3-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="61fe3-129">Tenere presente che questi termini possono essere usati in modo intercambiabile in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="61fe3-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="61fe3-130">Tipi di dati supportati</span><span class="sxs-lookup"><span data-stu-id="61fe3-130">Supported data types</span></span>
<span data-ttu-id="61fe3-131">Hello seguenti tipi di dati è supportato nei modelli creati con hello **serializzatore** libreria:</span><span class="sxs-lookup"><span data-stu-id="61fe3-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="61fe3-132">Tipo</span><span class="sxs-lookup"><span data-stu-id="61fe3-132">Type</span></span> | <span data-ttu-id="61fe3-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="61fe3-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61fe3-134">double</span><span class="sxs-lookup"><span data-stu-id="61fe3-134">double</span></span> |<span data-ttu-id="61fe3-135">Numero a virgola mobile a precisione doppia</span><span class="sxs-lookup"><span data-stu-id="61fe3-135">double precision floating point number</span></span> |
| <span data-ttu-id="61fe3-136">int</span><span class="sxs-lookup"><span data-stu-id="61fe3-136">int</span></span> |<span data-ttu-id="61fe3-137">Intero a 32 bit</span><span class="sxs-lookup"><span data-stu-id="61fe3-137">32 bit integer</span></span> |
| <span data-ttu-id="61fe3-138">float</span><span class="sxs-lookup"><span data-stu-id="61fe3-138">float</span></span> |<span data-ttu-id="61fe3-139">Numero a virgola mobile a precisione singola</span><span class="sxs-lookup"><span data-stu-id="61fe3-139">single precision floating point number</span></span> |
| <span data-ttu-id="61fe3-140">long</span><span class="sxs-lookup"><span data-stu-id="61fe3-140">long</span></span> |<span data-ttu-id="61fe3-141">Intero lungo</span><span class="sxs-lookup"><span data-stu-id="61fe3-141">long integer</span></span> |
| <span data-ttu-id="61fe3-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="61fe3-142">int8\_t</span></span> |<span data-ttu-id="61fe3-143">Intero a 8 bit</span><span class="sxs-lookup"><span data-stu-id="61fe3-143">8 bit integer</span></span> |
| <span data-ttu-id="61fe3-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="61fe3-144">int16\_t</span></span> |<span data-ttu-id="61fe3-145">Intero a 16 bit</span><span class="sxs-lookup"><span data-stu-id="61fe3-145">16 bit integer</span></span> |
| <span data-ttu-id="61fe3-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="61fe3-146">int32\_t</span></span> |<span data-ttu-id="61fe3-147">Intero a 32 bit</span><span class="sxs-lookup"><span data-stu-id="61fe3-147">32 bit integer</span></span> |
| <span data-ttu-id="61fe3-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="61fe3-148">int64\_t</span></span> |<span data-ttu-id="61fe3-149">Intero a 64 bit</span><span class="sxs-lookup"><span data-stu-id="61fe3-149">64 bit integer</span></span> |
| <span data-ttu-id="61fe3-150">bool</span><span class="sxs-lookup"><span data-stu-id="61fe3-150">bool</span></span> |<span data-ttu-id="61fe3-151">boolean</span><span class="sxs-lookup"><span data-stu-id="61fe3-151">boolean</span></span> |
| <span data-ttu-id="61fe3-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="61fe3-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="61fe3-153">Stringa ASCII</span><span class="sxs-lookup"><span data-stu-id="61fe3-153">ASCII string</span></span> |
| <span data-ttu-id="61fe3-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="61fe3-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="61fe3-155">Offset data/ora</span><span class="sxs-lookup"><span data-stu-id="61fe3-155">date time offset</span></span> |
| <span data-ttu-id="61fe3-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="61fe3-156">EDM\_GUID</span></span> |<span data-ttu-id="61fe3-157">GUID</span><span class="sxs-lookup"><span data-stu-id="61fe3-157">GUID</span></span> |
| <span data-ttu-id="61fe3-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="61fe3-158">EDM\_BINARY</span></span> |<span data-ttu-id="61fe3-159">binary</span><span class="sxs-lookup"><span data-stu-id="61fe3-159">binary</span></span> |
| <span data-ttu-id="61fe3-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="61fe3-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="61fe3-161">Tipo di dati complesso</span><span class="sxs-lookup"><span data-stu-id="61fe3-161">complex data type</span></span> |

<span data-ttu-id="61fe3-162">Iniziamo con hello ultimo tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="61fe3-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="61fe3-163">Hello **DECLARE\_STRUCT** consente tipi di dati complessi toodefine, ovvero raggruppamenti di hello ad altri tipi primitivi.</span><span class="sxs-lookup"><span data-stu-id="61fe3-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="61fe3-164">Questi raggruppamenti consentono toodefine un modello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="61fe3-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="61fe3-165">Il modello contiene un singolo evento dati di tipo **TestType**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="61fe3-166">**TestType** è un tipo complesso che include molti membri, quali collettivamente vengono illustrati i tipi di primitivi hello supportati dal hello **serializzatore** linguaggio di modellazione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="61fe3-167">Con un modello simile al seguente, è possibile scrivere codice toosend dati tooIoT Hub che viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="61fe3-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="61fe3-168">In pratica, assegniamo membro tooevery valore hello **Test** struttura e chiamando quindi **SendAsync** toosend hello **Test** dati nel cloud toohello evento.</span><span class="sxs-lookup"><span data-stu-id="61fe3-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="61fe3-169">**SendAsync** è una funzione di supporto che invia un tooIoT di dati singolo evento Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

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

<span data-ttu-id="61fe3-170">Questa funzione serializza hello dato dati evento e lo invia tooIoT Hub utilizzando **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="61fe3-171">Si tratta di hello stesso codice descritto negli articoli precedenti (**SendAsync** incapsula la logica di hello in una comoda funzione).</span><span class="sxs-lookup"><span data-stu-id="61fe3-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="61fe3-172">È un altra funzione di supporto utilizzata nel codice precedente hello **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="61fe3-173">Questa funzione Trasforma hello momento in un valore di tipo **EDM\_data\_ora\_OFFSET**:</span><span class="sxs-lookup"><span data-stu-id="61fe3-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="61fe3-174">Se si esegue questo codice, hello seguente messaggio viene inviato tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="61fe3-175">Si noti che la serializzazione di hello è JSON, è formato hello generato da hello **serializzatore** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="61fe3-176">Si noti che ogni membro di hello serializzato l'oggetto JSON corrisponde anche i membri di hello di hello **TestType** definiti nel modello in esame.</span><span class="sxs-lookup"><span data-stu-id="61fe3-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="61fe3-177">i valori Hello anche corrispondere esattamente a quelli usati nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="61fe3-178">Tuttavia, si noti che i dati binari hello sono con codifica base64: "AQID" è hello codifica base64 del {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="61fe3-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="61fe3-179">In questo esempio viene hello vantaggio offerto dall'utilizzo hello **serializzatore** libreria - offre il cloud di toohello toosend JSON, senza dovere tooexplicitly di gestire la serializzazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="61fe3-180">Tutto tooworry su è l'impostazione valori hello di hello eventi dati il nostro modello e quindi chiamare toosend API semplice tali cloud toohello eventi.</span><span class="sxs-lookup"><span data-stu-id="61fe3-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="61fe3-181">Con queste informazioni, è possibile definire i modelli che includono l'intervallo di hello dei tipi di dati supportati, inclusi i tipi complessi (è possibile includere anche i tipi complessi all'interno di altri tipi complessi).</span><span class="sxs-lookup"><span data-stu-id="61fe3-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="61fe3-182">Tuttavia, ha serializzato JSON generato da hello esempio precedente consente di visualizzare un punto importante.</span><span class="sxs-lookup"><span data-stu-id="61fe3-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="61fe3-183">*Come* inviare dati con hello **serializzatore** libreria determina esattamente come è formata hello JSON.</span><span class="sxs-lookup"><span data-stu-id="61fe3-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="61fe3-184">Di seguito viene trattato questo punto specifico.</span><span class="sxs-lookup"><span data-stu-id="61fe3-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="61fe3-185">Altre informazioni sulla serializzazione</span><span class="sxs-lookup"><span data-stu-id="61fe3-185">More about serialization</span></span>
<span data-ttu-id="61fe3-186">la sezione precedente di Hello evidenzia un esempio di output di hello generati da hello **serializzatore** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="61fe3-187">In questa sezione verrà illustrato come libreria hello serializza i dati e come sia possibile controllare questo comportamento utilizzando dalle API di serializzazione hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="61fe3-188">In ordine tooadvance hello discussione sulla serializzazione si utilizzerà un nuovo modello basato su un termostato.</span><span class="sxs-lookup"><span data-stu-id="61fe3-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="61fe3-189">In primo luogo, consente di fornire alcune informazioni generali sullo scenario hello stiamo cercando tooaddress.</span><span class="sxs-lookup"><span data-stu-id="61fe3-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="61fe3-190">È necessario un termostato che misura la temperatura e umidità toomodel.</span><span class="sxs-lookup"><span data-stu-id="61fe3-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="61fe3-191">Ogni blocco di dati verrà toobe inviati tooIoT Hub in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="61fe3-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="61fe3-192">Per impostazione predefinita, hello ingresses termostato un evento di temperatura una volta ogni 2 minuti. un evento umidità è ingressed una volta ogni 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="61fe3-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="61fe3-193">Quando degli eventi è ingressed, deve includere un timestamp che indica il tempo di hello tale temperatura corrispondente hello o umidità è stata misurata.</span><span class="sxs-lookup"><span data-stu-id="61fe3-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="61fe3-194">Dato questo scenario, verrà illustrata in dati di due modi diversi toomodel hello e spiega effetto hello che modellazione è su hello serializzato output.</span><span class="sxs-lookup"><span data-stu-id="61fe3-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="61fe3-195">Modello 1</span><span class="sxs-lookup"><span data-stu-id="61fe3-195">Model 1</span></span>
<span data-ttu-id="61fe3-196">Ecco hello prima versione di un modello che supporta hello scenario precedente:</span><span class="sxs-lookup"><span data-stu-id="61fe3-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="61fe3-197">Si noti che modello hello include due eventi di dati: **temperatura** e **umidità**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="61fe3-198">A differenza degli esempi precedenti, il tipo di hello di ogni evento è una struttura definita utilizzando **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="61fe3-199">**TemperatureEvent** include una misura della temperatura e un timestamp. **HumidityEvent** contiene una misura dell'umidità e un timestamp.</span><span class="sxs-lookup"><span data-stu-id="61fe3-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="61fe3-200">Questo modello offre dati di hello toomodel un modo semplice per uno scenario di hello descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="61fe3-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="61fe3-201">Quando si invia un cloud toohello evento, ti invieremo sia un temperatura, timestamp o una coppia di umidità o timestamp.</span><span class="sxs-lookup"><span data-stu-id="61fe3-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="61fe3-202">È possibile inviare un cloud di toohello evento temperatura utilizzando codice simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="61fe3-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="61fe3-203">Verranno utilizzati valori hardcoded per temperatura e umidità nel codice di esempio hello, ma si supponga che vengono effettivamente recuperate questi valori eseguendo il campionamento dei sensori corrispondente hello in termostato hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="61fe3-204">codice Hello precedente utilizza hello **GetDateTimeOffset** helper che è stata introdotta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="61fe3-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="61fe3-205">Per motivi che diventeranno deselezionare successive, questo codice consente di separare in modo esplicito attività hello di serializzazione e di invio evento hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="61fe3-206">codice precedente Hello serializza evento temperatura hello in un buffer.</span><span class="sxs-lookup"><span data-stu-id="61fe3-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="61fe3-207">Quindi, **sendMessage** è una funzione di supporto (incluso in **simplesample\_amqp**) che invia hello tooIoT evento Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="61fe3-208">Questo codice è un subset di hello **SendAsync** helper descritte nella sezione precedente hello, pertanto non verranno esaminate su di essa nuovamente qui.</span><span class="sxs-lookup"><span data-stu-id="61fe3-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="61fe3-209">Quando si esegue hello codice toosend hello temperatura dall'evento precedente, questa forma serializzata dell'evento hello viene inviata tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="61fe3-210">Viene inviato un evento temperatura di tipo **TemperatureEvent** la cui struttura contiene un membro **Temperature** e **Time**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="61fe3-211">Ciò si riflette direttamente nei dati serializzato hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="61fe3-212">In modo analogo è possibile inviare un evento umidità con questo codice:</span><span class="sxs-lookup"><span data-stu-id="61fe3-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="61fe3-213">form serializzato Hello che ha inviato tooIoT Hub visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="61fe3-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="61fe3-214">Anche in questo caso, è un comportamento previsto.</span><span class="sxs-lookup"><span data-stu-id="61fe3-214">Again, this is as expected.</span></span>

<span data-ttu-id="61fe3-215">Con questo modello si può immaginare come sia facile aggiungere altri eventi.</span><span class="sxs-lookup"><span data-stu-id="61fe3-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="61fe3-216">Si definiscono più strutture utilizzando **DECLARE\_STRUCT**e includere l'evento corrispondente hello in hello modello utilizzando **WITH\_dati**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="61fe3-217">A questo punto, in modo che includa hello è opportuno modificare il modello di hello stessi dati ma con una struttura diversa.</span><span class="sxs-lookup"><span data-stu-id="61fe3-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="61fe3-218">Modello 2</span><span class="sxs-lookup"><span data-stu-id="61fe3-218">Model 2</span></span>
<span data-ttu-id="61fe3-219">Si consideri questo toohello modello alternativo uno sopra:</span><span class="sxs-lookup"><span data-stu-id="61fe3-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="61fe3-220">In questo caso è stato eliminato hello **DECLARE\_STRUCT** macro e sono semplicemente la definizione di elementi di dati hello da questo scenario utilizzando i tipi semplici di hello linguaggio di modellazione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="61fe3-221">Solo per il momento di hello si ignora hello **ora** evento.</span><span class="sxs-lookup"><span data-stu-id="61fe3-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="61fe3-222">Con tale aside, ecco tooingress codice hello **temperatura**:</span><span class="sxs-lookup"><span data-stu-id="61fe3-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="61fe3-223">Questo codice invia seguente hello serializzato tooIoT evento Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="61fe3-224">E codice hello per l'invio di eventi umidità hello viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="61fe3-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="61fe3-225">Questo codice invia questo tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="61fe3-226">Di nuovo nulla di insolito fino a questo punto.</span><span class="sxs-lookup"><span data-stu-id="61fe3-226">So far there are still no surprises.</span></span> <span data-ttu-id="61fe3-227">A questo punto è necessario modificare come utilizziamo macro SERIALIZE hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="61fe3-228">Hello **SERIALIZE** (macro) può richiedere più eventi di dati come argomenti.</span><span class="sxs-lookup"><span data-stu-id="61fe3-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="61fe3-229">In questo modo ci hello tooserialize **temperatura** e **umidità** insieme a eventi e li inviano tooIoT Hub in un'unica chiamata:</span><span class="sxs-lookup"><span data-stu-id="61fe3-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="61fe3-230">Si può immaginare che il risultato di hello di questo codice è che gli eventi di due dati vengono inviati tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="61fe3-231">[</span><span class="sxs-lookup"><span data-stu-id="61fe3-231">[</span></span>

<span data-ttu-id="61fe3-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="61fe3-232">{"Temperature":75},</span></span>

<span data-ttu-id="61fe3-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="61fe3-233">{"Humidity":45}</span></span>

<span data-ttu-id="61fe3-234">]</span><span class="sxs-lookup"><span data-stu-id="61fe3-234">]</span></span>

<span data-ttu-id="61fe3-235">In altre parole, è prevedibile che questo codice è hello stesso come l'invio di **temperatura** e **umidità** separatamente.</span><span class="sxs-lookup"><span data-stu-id="61fe3-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="61fe3-236">È semplicemente un toopass praticità entrambi gli eventi troppo**SERIALIZE** in hello stessa chiamata.</span><span class="sxs-lookup"><span data-stu-id="61fe3-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="61fe3-237">Tuttavia, non è hello caso.</span><span class="sxs-lookup"><span data-stu-id="61fe3-237">However, that’s not hello case.</span></span> <span data-ttu-id="61fe3-238">Al contrario, codice hello precedente invia questo tooIoT di dati singolo evento Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="61fe3-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="61fe3-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="61fe3-240">Può sembrare strano perché il modello definisce **Temperature** e **Humidity** come due eventi *distinti*:</span><span class="sxs-lookup"><span data-stu-id="61fe3-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="61fe3-241">Ulteriori toohello punto, è non modello questi eventi in cui **temperatura** e **umidità** in hello stessa struttura:</span><span class="sxs-lookup"><span data-stu-id="61fe3-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="61fe3-242">Se è stato usato questo modello, sarebbe più facile toounderstand come **temperatura** e **umidità** verrebbe inviato in hello stesso il messaggio serializzato.</span><span class="sxs-lookup"><span data-stu-id="61fe3-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="61fe3-243">Tuttavia potrebbe non essere chiaro perché funziona in questo modo, quando si passano entrambi gli eventi di dati troppo**SERIALIZE** utilizzando il modello 2.</span><span class="sxs-lookup"><span data-stu-id="61fe3-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="61fe3-244">Questo comportamento è toounderstand più semplice se si conoscono l'ipotesi di hello che hello **serializzatore** effettua libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="61fe3-245">senso toomake di questo è necessario tornare indietro tooour modello:</span><span class="sxs-lookup"><span data-stu-id="61fe3-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="61fe3-246">Pensare al modello in termini di "orientato a oggetti".</span><span class="sxs-lookup"><span data-stu-id="61fe3-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="61fe3-247">In questo caso si modella un dispositivo fisico (Thermostat), che include attributi come **Temperature** e **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="61fe3-248">È possibile inviare hello stato completo nello stato del modello con codice simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="61fe3-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="61fe3-249">Supponendo che i valori hello di temperatura e umidità ora vengono impostati, si vedrà un evento, ad esempio, questo tooIoT inviato Hub:</span><span class="sxs-lookup"><span data-stu-id="61fe3-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="61fe3-250">A volte può essere solo toosend *alcuni* proprietà di hello modello toohello cloud (Ciò vale soprattutto se il modello contiene un numero elevato di eventi di dati).</span><span class="sxs-lookup"><span data-stu-id="61fe3-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="61fe3-251">È utile toosend solo un subset di eventi di dati, come nell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="61fe3-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="61fe3-252">Questa operazione genera esattamente hello dell'evento stesso serializzato come se fosse stata definita una **TemperatureEvent** con un **temperatura** e **ora** membro, come se si con modello di 1.</span><span class="sxs-lookup"><span data-stu-id="61fe3-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="61fe3-253">In questo caso è stato in grado di toogenerate esattamente hello stesso dell'evento serializzato utilizzando un diverso modello (modello di 2) perché è stato chiamato **SERIALIZE** in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="61fe3-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="61fe3-254">Hello punto importante è che se si passano più eventi di dati troppo**SERIALIZE,** quindi si presuppone che ogni evento è una proprietà in un singolo oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="61fe3-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="61fe3-255">approccio migliore Hello varia a seconda di come si pensa di modello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="61fe3-256">Se si sta inviando il messaggio "eventi" toohello cloud e ogni evento contiene un set definito di proprietà, quindi primo approccio hello molto più utile.</span><span class="sxs-lookup"><span data-stu-id="61fe3-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="61fe3-257">In questo caso si utilizzerebbe **DECLARE\_STRUCT** toodefine hello struttura di ogni evento e quindi includerli nel modello con hello **WITH\_dati** (macro).</span><span class="sxs-lookup"><span data-stu-id="61fe3-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="61fe3-258">Quindi inviare ogni evento come in hello primo esempio.</span><span class="sxs-lookup"><span data-stu-id="61fe3-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="61fe3-259">In questo approccio solo passare un singolo evento troppo**SERIALIZZATORE**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="61fe3-260">Se si pensa al modello in modo orientato, secondo approccio hello può soddisfare è.</span><span class="sxs-lookup"><span data-stu-id="61fe3-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="61fe3-261">In questo caso, hello elementi definiti mediante **WITH\_dati** hello "proprietà" dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="61fe3-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="61fe3-262">Passare a qualsiasi subset di eventi troppo**SERIALIZE** che si desidera che, a seconda della quantità di stato "dell'oggetto" si desidera toosend toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="61fe3-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="61fe3-263">Nessun approccio è giusto o sbagliato.</span><span class="sxs-lookup"><span data-stu-id="61fe3-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="61fe3-264">Solo essere a conoscenza di come hello **serializzatore** funzionamento libreria e approccio di modellazione hello di selezione che meglio si adatta alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="61fe3-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="61fe3-265">Gestione dei messaggi</span><span class="sxs-lookup"><span data-stu-id="61fe3-265">Message handling</span></span>
<span data-ttu-id="61fe3-266">In questo articolo finora è descritto solo l'invio degli eventi tooIoT Hub e non è stata indirizzata la ricezione di messaggi.</span><span class="sxs-lookup"><span data-stu-id="61fe3-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="61fe3-267">Hello motivo è che è necessario tooknow sulla ricezione dei messaggi in gran parte interessato un [precedentemente articolo](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="61fe3-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="61fe3-268">Tenere presente, come detto in quell'articolo, che i messaggi vengono elaborati registrando una funzione di richiamata dei messaggi:</span><span class="sxs-lookup"><span data-stu-id="61fe3-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="61fe3-269">È quindi possibile scrivere hello di callback che viene richiamato quando viene ricevuto un messaggio:</span><span class="sxs-lookup"><span data-stu-id="61fe3-269">You then write hello callback function that’s invoked when a message is received:</span></span>

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

<span data-ttu-id="61fe3-270">Questa implementazione di **IoTHubMessage** hello di chiamate di funzione specifica per ogni azione nel modello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="61fe3-271">Ad esempio, se il modello definisce questa azione:</span><span class="sxs-lookup"><span data-stu-id="61fe3-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="61fe3-272">È necessario definire una funzione con questa firma.</span><span class="sxs-lookup"><span data-stu-id="61fe3-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="61fe3-273">**SetAirResistance** viene quindi chiamato quando il messaggio viene inviato tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="61fe3-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="61fe3-274">Cosa spiegare non è ancora la versione di hello serializzato del messaggio ha un aspetto simile.</span><span class="sxs-lookup"><span data-stu-id="61fe3-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="61fe3-275">In altre parole, se si desidera toosend un **SetAirResistance** dispositivo tooyour messaggio, cosa che hanno l'aspetto come?</span><span class="sxs-lookup"><span data-stu-id="61fe3-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="61fe3-276">Se si invia un dispositivo tooa messaggio, si imposterebbe tramite il servizio di Azure IoT hello SDK.</span><span class="sxs-lookup"><span data-stu-id="61fe3-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="61fe3-277">È comunque necessario tooknow stringa toosend tooinvoke una determinata azione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="61fe3-278">formato generale di Hello per l'invio di un messaggio viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="61fe3-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="61fe3-279">Si sta inviando un oggetto serializzato JSON con due proprietà: **nome** hello nome dell'azione hello (messaggio) e **parametri** contiene parametri hello dell'azione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="61fe3-280">Ad esempio, tooinvoke **SetAirResistance** è possibile inviare questo dispositivo tooa messaggio:</span><span class="sxs-lookup"><span data-stu-id="61fe3-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="61fe3-281">nome dell'azione Hello deve corrispondere esattamente a un'azione definita nel modello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="61fe3-282">i nomi di parametro Hello devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="61fe3-282">hello parameter names must match as well.</span></span> <span data-ttu-id="61fe3-283">Tenere presente anche la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="61fe3-283">Also note case sensitivity.</span></span> <span data-ttu-id="61fe3-284">**Name** e **Parameters** sono sempre in maiuscolo.</span><span class="sxs-lookup"><span data-stu-id="61fe3-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="61fe3-285">Verificare che toomatch hello casi il nome dell'azione e i parametri nel modello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="61fe3-286">In questo esempio, il nome dell'azione hello è "SetAirResistance" e non "setairresistance".</span><span class="sxs-lookup"><span data-stu-id="61fe3-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="61fe3-287">due altre azioni Hello **TurnFanOn** e **TurnFanOff** può essere richiamato mediante l'invio di questi dispositivi tooa messaggi:</span><span class="sxs-lookup"><span data-stu-id="61fe3-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="61fe3-288">Questa sezione viene descritto tutto ciò che occorre tooknow quando l'invio di eventi e la ricezione di messaggi con hello **serializzatore** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="61fe3-289">Prima di proseguire, si esamineranno alcuni parametri che è possibile configurare per controllare le dimensioni del modello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="61fe3-290">Configurazione delle macro</span><span class="sxs-lookup"><span data-stu-id="61fe3-290">Macro configuration</span></span>
<span data-ttu-id="61fe3-291">Se si usa hello **serializzatore** libreria una parte importante di hello SDK toobe comunicata viene trovata nella libreria di azure-c-condivisi-utilità hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="61fe3-292">Se sono stati clonati repository hello Azure-iot-sdk-c da GitHub utilizzando hello ricorsiva - opzione, sarà possibile reperire la raccolta di utilità condivisi qui:</span><span class="sxs-lookup"><span data-stu-id="61fe3-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="61fe3-293">Se non sono stati clonati libreria hello, sarà possibile trovarlo [qui](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="61fe3-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="61fe3-294">Nella raccolta di utilità condivisi hello, sarà possibile reperire hello seguente cartella:</span><span class="sxs-lookup"><span data-stu-id="61fe3-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="61fe3-295">Questa cartella contiene una soluzione di Visual Studio chiamata **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="61fe3-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="61fe3-296">il programma di Hello in questa soluzione genera hello **macro\_utils.h** file.</span><span class="sxs-lookup"><span data-stu-id="61fe3-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="61fe3-297">È una macro predefinita\_file utils.h incluso con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="61fe3-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="61fe3-298">Questa soluzione consente toomodify alcuni parametri e quindi creare nuovamente il file di intestazione in base a questi parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="61fe3-299">Hello due parametri chiave toobe riguarda sono **nArithmetic** e **nMacroParameters** che sono definite in queste due righe trovate nella macro\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="61fe3-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="61fe3-300">Questi valori sono i parametri predefiniti hello inclusi hello SDK.</span><span class="sxs-lookup"><span data-stu-id="61fe3-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="61fe3-301">Ogni parametro ha hello seguente significato:</span><span class="sxs-lookup"><span data-stu-id="61fe3-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="61fe3-302">nMacroParameters: controlla la quantità di parametri che possono essere inclusi in una definizione di macro DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="61fe3-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="61fe3-303">nArithmetic: numero totale di controlli hello dei membri è consentito in un modello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="61fe3-304">motivo di Hello che questi parametri sono importanti è quanto controllano il modello può essere.</span><span class="sxs-lookup"><span data-stu-id="61fe3-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="61fe3-305">Considerare ad esempio questa definizione di modello:</span><span class="sxs-lookup"><span data-stu-id="61fe3-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="61fe3-306">Come già accennato, **DECLARE\_MODEL** è semplicemente una macro C.</span><span class="sxs-lookup"><span data-stu-id="61fe3-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="61fe3-307">i nomi del modello di hello e hello Hello **WITH\_dati** istruzione (ancora un'altra macro) è parametri di **DECLARE\_modello**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="61fe3-308">**nMacroParameters** definisce il numero di parametri che può essere incluso in **DECLARE\_MODELLO**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="61fe3-309">In realtà definisce la quantità di eventi dati e dichiarazioni di azione supportata.</span><span class="sxs-lookup"><span data-stu-id="61fe3-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="61fe3-310">Di conseguenza, hello predefinito Limit 124 ciò significa che è possibile definire un modello con una combinazione di azioni di circa 60 e gli eventi di dati.</span><span class="sxs-lookup"><span data-stu-id="61fe3-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="61fe3-311">Se si tenta di tooexceed questo limite, si riceveranno errori del compilatore che la ricerca di toothis simile:</span><span class="sxs-lookup"><span data-stu-id="61fe3-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="61fe3-312">Hello **nArithmetic** parametro è di più sui meccanismi interni di hello del linguaggio macro hello di applicazione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="61fe3-313">Controlla numero totale di hello di membri è consentito nel modello, tra cui **DECLARE_STRUCT** macro.</span><span class="sxs-lookup"><span data-stu-id="61fe3-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="61fe3-314">Se iniziano a essere visualizzati errori del compilatore come questo, provare ad aumentare il valore di **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="61fe3-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="61fe3-315">Se si desidera toochange questi parametri, modificare i valori hello nella macro hello\_utils.tt file, la macro hello recompile\_utils\_h\_generator.sln soluzione e programma compilato hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="61fe3-316">A tale scopo, una nuova macro\_utils.h file viene generato e posizionato in hello.\\ comuni\\directory inc.</span><span class="sxs-lookup"><span data-stu-id="61fe3-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="61fe3-317">In ordine toouse hello nuova versione di una macro\_utils.h, Rimuovi hello **serializzatore** pacchetto NuGet dalla soluzione e al suo posto includono hello **serializzatore** progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61fe3-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="61fe3-318">In questo modo il toocompile codice rispetto al codice sorgente hello della libreria di serializzatore hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="61fe3-319">Ciò include la macro di hello aggiornato\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="61fe3-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="61fe3-320">Se si desidera toodo per **simplesample\_amqp**, iniziare a rimuovere il pacchetto NuGet hello per la libreria serializzatore hello dalla soluzione hello:</span><span class="sxs-lookup"><span data-stu-id="61fe3-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="61fe3-321">Aggiungere quindi questa tooyour di progetto, soluzione di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="61fe3-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="61fe3-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="61fe3-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="61fe3-323">Al termine, la soluzione dovrebbe avere un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="61fe3-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="61fe3-324">Ora quando si compila la soluzione, hello aggiornato macro\_utils.h è incluso nel file binario.</span><span class="sxs-lookup"><span data-stu-id="61fe3-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="61fe3-325">Se si aumentano molto questi valori, potrebbero essere superati i limiti del compilatore.</span><span class="sxs-lookup"><span data-stu-id="61fe3-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="61fe3-326">toothis punto, hello **nMacroParameters** hello parametro principale con cui toobe in questione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="61fe3-327">Specifica C99 Hello specifica che un minimo di 127 parametri siano consentiti in una definizione di macro.</span><span class="sxs-lookup"><span data-stu-id="61fe3-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="61fe3-328">Hello compilatore Microsoft segue spec hello esattamente (e ha un limite di 127), in modo non sarà in grado di tooincrease **nMacroParameters** oltre predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="61fe3-329">Altri compilatori possono consentire di toodo così (ad esempio, il compilatore di GNU hello supporta un limite maggiore).</span><span class="sxs-lookup"><span data-stu-id="61fe3-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="61fe3-330">Finora abbiamo trattato quasi tutto ciò che occorre tooknow sulla modalità in codice con hello toowrite **serializzatore** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="61fe3-331">Prima di concludere, ecco di seguito alcuni argomenti degli articoli precedenti che potrebbero risultare interessanti.</span><span class="sxs-lookup"><span data-stu-id="61fe3-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="61fe3-332">Hello API di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="61fe3-332">hello lower-level APIs</span></span>
<span data-ttu-id="61fe3-333">applicazione di esempio Hello in cui è attivo in questo articolo è **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="61fe3-334">In questo esempio utilizza hello (hello non-"LL") API toosend eventi di livello superiore e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="61fe3-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="61fe3-335">Se si usano queste API, viene eseguito un thread in background che si occupa dell'invio degli eventi e della ricezione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="61fe3-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="61fe3-336">Tuttavia, è possibile utilizzare tooeliminate (ova) le API di livello inferiore hello questo thread in background e assumere il controllo esplicito quando si inviano eventi o ricevere messaggi da cloud hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="61fe3-337">Come descritto in un [articolo precedente](iot-hub-device-sdk-c-iothubclient.md), vi è un set di funzioni che è costituito da hello API di livello superiore:</span><span class="sxs-lookup"><span data-stu-id="61fe3-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="61fe3-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="61fe3-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="61fe3-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="61fe3-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="61fe3-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="61fe3-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="61fe3-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="61fe3-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="61fe3-342">Queste API sono illustrate in **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="61fe3-343">È disponibile anche set analogo di API di livello inferiore.</span><span class="sxs-lookup"><span data-stu-id="61fe3-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="61fe3-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="61fe3-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="61fe3-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="61fe3-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="61fe3-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="61fe3-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="61fe3-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="61fe3-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="61fe3-348">Si noti che operazioni API di livello inferiore hello hello esattamente come descritto negli articoli precedente hello.</span><span class="sxs-lookup"><span data-stu-id="61fe3-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="61fe3-349">È possibile utilizzare primo set di API di hello se si desidera un toohandle di background thread eventi inviando e ricevendo messaggi.</span><span class="sxs-lookup"><span data-stu-id="61fe3-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="61fe3-350">Utilizzare secondo set di API di hello se si desidera il controllo esplicito quando si inviare e ricevere i dati dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61fe3-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="61fe3-351">Uno dei due set di API lavoro altrettanto bene con hello **serializzatore** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="61fe3-352">Per un esempio di come hello livello inferiore vengono utilizzate le API con hello **serializzatore** libreria, vedere hello **simplesample\_http** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="61fe3-353">Argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="61fe3-353">Additional topics</span></span>
<span data-ttu-id="61fe3-354">Alcuni altri argomenti che vale la pena citare riguardano la gestione delle proprietà, l'uso di credenziali del dispositivo alternative e le opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="61fe3-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="61fe3-355">Ecco tutti gli argomenti illustrati in un [articolo precedente](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="61fe3-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="61fe3-356">Hello punto principale è che tutte queste funzionalità funzionano in hello stesso modo con hello **serializzatore** libreria come avviene con hello **IoTHubClient** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="61fe3-357">Ad esempio, se si desidera evento tooan di tooattach proprietà dal modello, utilizzare **IoTHubMessage\_proprietà** e **mappa**\_**AddorUpdate**, hello come descritto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="61fe3-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="61fe3-358">Se evento hello è stato generato da hello **serializzatore** libreria o creato manualmente tramite hello **IoTHubClient** libreria non è rilevante.</span><span class="sxs-lookup"><span data-stu-id="61fe3-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="61fe3-359">Per hello alternare le credenziali di dispositivo, utilizzando **IoTHubClient\_LL\_crea** funziona così come **IoTHubClient\_CreateFromConnectionString** per allocare un **l'hub IOT\_CLIENT\_gestire**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="61fe3-360">Infine, se si usa hello **serializzatore** libreria, è possibile impostare le opzioni di configurazione con **IoTHubClient\_LL\_SetOption** esattamente come è stato fatto quando si utilizza hello **IoTHubClient** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="61fe3-361">Una funzionalità che è univoco toohello **serializzatore** libreria sono inizializzazione hello API.</span><span class="sxs-lookup"><span data-stu-id="61fe3-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="61fe3-362">Prima di iniziare a lavorare con libreria hello, è necessario chiamare **serializzatore\_init**:</span><span class="sxs-lookup"><span data-stu-id="61fe3-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="61fe3-363">Questa operazione viene eseguita subito prima di chiamare **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="61fe3-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="61fe3-364">Analogamente, quando si completa l'utilizzo di libreria hello, hello dall'ultima chiamata ti è troppo**serializzatore\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="61fe3-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="61fe3-365">In caso contrario, tutti hello altre funzionalità elencate in precedenza lavoro stesso hello in hello **serializzatore** libreria come in hello **IoTHubClient** libreria.</span><span class="sxs-lookup"><span data-stu-id="61fe3-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="61fe3-366">Per ulteriori informazioni su questi argomenti, vedere hello [articolo precedente](iot-hub-device-sdk-c-iothubclient.md) di questa serie.</span><span class="sxs-lookup"><span data-stu-id="61fe3-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61fe3-367">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61fe3-367">Next steps</span></span>
<span data-ttu-id="61fe3-368">In questo articolo descrive in dettaglio hello univoco aspetti hello **serializzatore** libreria contenute in hello **dispositivo IoT di Azure SDK per C**. Con le informazioni di hello fornite si deve avere una buona conoscenza dei modelli di eventi toosend come toouse e ricevere messaggi dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61fe3-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="61fe3-369">Questo conclude anche serie hello tre parti come applicazioni toodevelop con hello **dispositivo IoT di Azure SDK per C**. Questo deve essere sufficiente get solo toonot informazioni che è stata avviata ma offrono una conoscenza approfondita del funzionamento di hello API.</span><span class="sxs-lookup"><span data-stu-id="61fe3-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="61fe3-370">Per ulteriori informazioni, in sono disponibili alcuni esempi hello che SDK non contenute in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="61fe3-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="61fe3-371">In caso contrario, hello [documentazione SDK](https://github.com/Azure/azure-iot-sdk-c) è un'ottima risorsa per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="61fe3-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="61fe3-372">toolearn più sullo sviluppo per l'IoT Hub, vedere hello [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="61fe3-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="61fe3-373">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="61fe3-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="61fe3-374">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="61fe3-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
