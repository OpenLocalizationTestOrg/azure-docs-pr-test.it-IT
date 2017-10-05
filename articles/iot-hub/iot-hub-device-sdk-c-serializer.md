---
title: Azure IoT SDK per dispositivi per C - Serializzatore | Documentazione Microsoft
description: Come usare la libreria Serializer in Azure IoT SDK per dispositivi per C per creare app per dispositivi che comunicano con un hub IoT.
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
ms.openlocfilehash: aa03c29c54d75538b1fdf987cac5f09d5d344f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="972de-103">Azure IoT SDK per dispositivi C: altre informazioni sul serializzatore</span><span class="sxs-lookup"><span data-stu-id="972de-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="972de-104">Il [primo articolo](iot-hub-device-sdk-c-intro.md) di questa serie ha introdotto **Azure IoT SDK per dispositivi per C**. L'articolo successivo fornisce una descrizione più dettagliata di [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="972de-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="972de-105">Questo articolo completa l'illustrazione dell'SDK fornendo una descrizione più dettagliata del componente restante, la libreria **serializer**.</span><span class="sxs-lookup"><span data-stu-id="972de-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="972de-106">L'articolo introduttivo ha descritto come usare la libreria **serializer** per inviare eventi e ricevere messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="972de-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="972de-107">Questo articolo estende la discussione, fornendo una spiegazione più completa della modellazione dei dati con il linguaggio macro **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="972de-108">Include anche altri dettagli su come vengono serializzati i messaggi da parte della libreria e, in alcuni casi, come è possibile controllare il comportamento della serializzazione.</span><span class="sxs-lookup"><span data-stu-id="972de-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="972de-109">Verranno descritti anche alcuni parametri modificabili che determinano le dimensioni dei modelli creati.</span><span class="sxs-lookup"><span data-stu-id="972de-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="972de-110">L'articolo si conclude rivedendo alcuni argomenti trattati negli articoli precedenti, quale la gestione dei messaggi e delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="972de-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="972de-111">Come si scoprirà, alcune funzionalità hanno lo stesso comportamento quando si usa sia la libreria **serializer** che la libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="972de-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="972de-112">Tutto ciò che viene descritto in questo articolo si basa sugli esempi dell'SDK per **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="972de-113">Se si vuole seguire la procedura, vedere le applicazioni **simplesample\_amqp** e **simplesample\_http** incluse in Azure IoT SDK per dispositivi per C.</span><span class="sxs-lookup"><span data-stu-id="972de-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="972de-114">È possibile trovare il repository GitHub di [**Azure IoT SDK per dispositivi per C**](https://github.com/Azure/azure-iot-sdk-c) e visualizzare i dettagli dell'API nelle [informazioni di riferimento per l'API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="972de-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="972de-115">Linguaggio di modellazione</span><span class="sxs-lookup"><span data-stu-id="972de-115">The modeling language</span></span>
<span data-ttu-id="972de-116">L'[articolo introduttivo](iot-hub-device-sdk-c-intro.md) di questa serie ha presentato il linguaggio di modellazione di **Azure IoT SDK per dispositivi per C** tramite l'esempio fornito nell'applicazione **simplesample\_amqp**:</span><span class="sxs-lookup"><span data-stu-id="972de-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="972de-117">Come si può notare, il linguaggio di modellazione si basa su macro C.</span><span class="sxs-lookup"><span data-stu-id="972de-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="972de-118">Si inizia sempre la definizione con **BEGIN\_NAMESPACE** e si termina sempre con **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="972de-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="972de-119">È normale denominare lo spazio dei nomi in base alla propria società o, come in questo caso, in base al progetto su cui si sta lavorando.</span><span class="sxs-lookup"><span data-stu-id="972de-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="972de-120">Nello spazio dei nomi sono incluse le definizioni dei modelli.</span><span class="sxs-lookup"><span data-stu-id="972de-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="972de-121">In questo caso è presente un singolo modello per un anemometro.</span><span class="sxs-lookup"><span data-stu-id="972de-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="972de-122">Al modello, come detto, può essere assegnato un nome qualsiasi, ma in genere si usa un nome che faccia riferimento al dispositivo o al tipo di dati che si vuole scambiare con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="972de-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="972de-123">I modelli contengono una definizione degli eventi che è possibile inserire nell'hub IoT (*dati*), oltre ai messaggi che si possono ricevere dall'hub IoT (*azioni*).</span><span class="sxs-lookup"><span data-stu-id="972de-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="972de-124">Come si può vedere dall'esempio, gli eventi hanno un tipo e un nome, mentre le azioni hanno un nome e parametri facoltativi, ognuno con un tipo.</span><span class="sxs-lookup"><span data-stu-id="972de-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="972de-125">In questo esempio non vengono illustrati i tipi di dati aggiuntivi supportati dall'SDK,</span><span class="sxs-lookup"><span data-stu-id="972de-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="972de-126">che saranno trattati in seguito.</span><span class="sxs-lookup"><span data-stu-id="972de-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="972de-127">L'hub IoT fa riferimento ai dati inviati da un dispositivo come *eventi*, mentre il linguaggio di modellazione li definisce *dati*, usando **WITH_DATA**.</span><span class="sxs-lookup"><span data-stu-id="972de-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="972de-128">In modo analogo, l'hub IoT fa riferimento ai dati inviati ai dispositivi come *messaggi*, mentre il linguaggio di modellazione li definisce *azioni*, usando **WITH_ACTION**.</span><span class="sxs-lookup"><span data-stu-id="972de-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="972de-129">Tenere presente che questi termini possono essere usati in modo intercambiabile in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="972de-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="972de-130">Tipi di dati supportati</span><span class="sxs-lookup"><span data-stu-id="972de-130">Supported data types</span></span>
<span data-ttu-id="972de-131">I tipi di dati seguenti sono supportati nei modelli creati con la libreria **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="972de-132">Tipo</span><span class="sxs-lookup"><span data-stu-id="972de-132">Type</span></span> | <span data-ttu-id="972de-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="972de-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="972de-134">double</span><span class="sxs-lookup"><span data-stu-id="972de-134">double</span></span> |<span data-ttu-id="972de-135">Numero a virgola mobile a precisione doppia</span><span class="sxs-lookup"><span data-stu-id="972de-135">double precision floating point number</span></span> |
| <span data-ttu-id="972de-136">int</span><span class="sxs-lookup"><span data-stu-id="972de-136">int</span></span> |<span data-ttu-id="972de-137">Intero a 32 bit</span><span class="sxs-lookup"><span data-stu-id="972de-137">32 bit integer</span></span> |
| <span data-ttu-id="972de-138">float</span><span class="sxs-lookup"><span data-stu-id="972de-138">float</span></span> |<span data-ttu-id="972de-139">Numero a virgola mobile a precisione singola</span><span class="sxs-lookup"><span data-stu-id="972de-139">single precision floating point number</span></span> |
| <span data-ttu-id="972de-140">long</span><span class="sxs-lookup"><span data-stu-id="972de-140">long</span></span> |<span data-ttu-id="972de-141">Intero lungo</span><span class="sxs-lookup"><span data-stu-id="972de-141">long integer</span></span> |
| <span data-ttu-id="972de-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="972de-142">int8\_t</span></span> |<span data-ttu-id="972de-143">Intero a 8 bit</span><span class="sxs-lookup"><span data-stu-id="972de-143">8 bit integer</span></span> |
| <span data-ttu-id="972de-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="972de-144">int16\_t</span></span> |<span data-ttu-id="972de-145">Intero a 16 bit</span><span class="sxs-lookup"><span data-stu-id="972de-145">16 bit integer</span></span> |
| <span data-ttu-id="972de-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="972de-146">int32\_t</span></span> |<span data-ttu-id="972de-147">Intero a 32 bit</span><span class="sxs-lookup"><span data-stu-id="972de-147">32 bit integer</span></span> |
| <span data-ttu-id="972de-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="972de-148">int64\_t</span></span> |<span data-ttu-id="972de-149">Intero a 64 bit</span><span class="sxs-lookup"><span data-stu-id="972de-149">64 bit integer</span></span> |
| <span data-ttu-id="972de-150">bool</span><span class="sxs-lookup"><span data-stu-id="972de-150">bool</span></span> |<span data-ttu-id="972de-151">boolean</span><span class="sxs-lookup"><span data-stu-id="972de-151">boolean</span></span> |
| <span data-ttu-id="972de-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="972de-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="972de-153">Stringa ASCII</span><span class="sxs-lookup"><span data-stu-id="972de-153">ASCII string</span></span> |
| <span data-ttu-id="972de-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="972de-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="972de-155">Offset data/ora</span><span class="sxs-lookup"><span data-stu-id="972de-155">date time offset</span></span> |
| <span data-ttu-id="972de-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="972de-156">EDM\_GUID</span></span> |<span data-ttu-id="972de-157">GUID</span><span class="sxs-lookup"><span data-stu-id="972de-157">GUID</span></span> |
| <span data-ttu-id="972de-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="972de-158">EDM\_BINARY</span></span> |<span data-ttu-id="972de-159">binary</span><span class="sxs-lookup"><span data-stu-id="972de-159">binary</span></span> |
| <span data-ttu-id="972de-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="972de-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="972de-161">Tipo di dati complesso</span><span class="sxs-lookup"><span data-stu-id="972de-161">complex data type</span></span> |

<span data-ttu-id="972de-162">Si inizierà con l'ultimo tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="972de-162">Let’s start with the last data type.</span></span> <span data-ttu-id="972de-163">**DECLARE\_STRUCT** consente di definire i tipi di dati complessi, che sono raggruppamenti degli altri tipi primitivi.</span><span class="sxs-lookup"><span data-stu-id="972de-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="972de-164">Questi raggruppamenti consentono di definire un modello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-164">These groupings allow us to define a model that looks like this:</span></span>

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

<span data-ttu-id="972de-165">Il modello contiene un singolo evento dati di tipo **TestType**.</span><span class="sxs-lookup"><span data-stu-id="972de-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="972de-166">**TestType** è un tipo complesso che include diversi membri, i quali dimostrano collettivamente i tipi primitivi supportati dal linguaggio di modellazione **serializer**.</span><span class="sxs-lookup"><span data-stu-id="972de-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="972de-167">Con un modello come questo è possibile scrivere codice per l'invio di dati all'hub IoT con l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="972de-168">Sostanzialmente, si assegna un valore a ogni membro della struttura **Test** e quindi si chiama **SendAsync** per inviare l'evento dati **Test** nel cloud.</span><span class="sxs-lookup"><span data-stu-id="972de-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="972de-169">**SendAsync** è una funzione helper che invia un singolo evento dati all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
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

<span data-ttu-id="972de-170">Questa funzione serializza l'evento dati specificato e lo invia all'hub IoT tramite **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="972de-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="972de-171">È lo stesso codice descritto negli articoli precedenti,**SendAsync** incapsula la logica in una funzione pratica.</span><span class="sxs-lookup"><span data-stu-id="972de-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="972de-172">Un'altra funzione helper usata nel codice precedente è **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="972de-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="972de-173">Questa funzione trasforma l'ora specificata in un valore di tipo **EDM\_DATE\_TIME\_OFFSET**:</span><span class="sxs-lookup"><span data-stu-id="972de-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="972de-174">Se si esegue questo codice, viene inviato il messaggio seguente all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="972de-175">Si noti che la serializzazione è in JSON, il formato generato dalla libreria **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="972de-176">Si noti anche che ogni membro dell'oggetto JSON serializzato corrisponde ai membri di **TestType** definiti nel modello.</span><span class="sxs-lookup"><span data-stu-id="972de-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="972de-177">Anche i valori corrispondono esattamente a quelli usati nel codice.</span><span class="sxs-lookup"><span data-stu-id="972de-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="972de-178">Notare tuttavia che i dati binari sono codificati in Base 64: "AQID" è la codifica Base 64 di {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="972de-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="972de-179">Questo esempio dimostra il vantaggio che deriva dall'uso della libreria **serializer** che abilita l'invio di codice JSON nel cloud, senza doversi occupare esplicitamente della serializzazione nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="972de-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="972de-180">Tutto ciò di cui ci si deve occupare è l'impostazione dei valori degli eventi dati nel modello e la successiva chiamata di API semplici per inviare tali eventi nel cloud.</span><span class="sxs-lookup"><span data-stu-id="972de-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="972de-181">Con queste informazioni è possibile definire modelli che includono la gamma di tipi di dati supportati, compresi i tipi complessi. Volendo, si potrebbero anche includere tipi complessi in altri tipi complessi.</span><span class="sxs-lookup"><span data-stu-id="972de-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="972de-182">Il codice JSON generato dall'esempio precedente solleva tuttavia un punto importante.</span><span class="sxs-lookup"><span data-stu-id="972de-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="972de-183">*Come* si inviano dati con la libreria **serializer** determina esattamente come viene formato JSON.</span><span class="sxs-lookup"><span data-stu-id="972de-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="972de-184">Di seguito viene trattato questo punto specifico.</span><span class="sxs-lookup"><span data-stu-id="972de-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="972de-185">Altre informazioni sulla serializzazione</span><span class="sxs-lookup"><span data-stu-id="972de-185">More about serialization</span></span>
<span data-ttu-id="972de-186">La sezione precedente evidenzia un esempio dell'output generato dalla libreria **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="972de-187">Questa sezione descrive in che modo la libreria serializza i dati e come si può controllare questo comportamento tramite le API di serializzazione.</span><span class="sxs-lookup"><span data-stu-id="972de-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="972de-188">Per procedere nella discussione sulla serializzazione, si utilizzerà un nuovo modello basato su un termostato.</span><span class="sxs-lookup"><span data-stu-id="972de-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="972de-189">Prima di tutto verrà fornito un insieme di informazioni di base sullo scenario che si proverà a usare.</span><span class="sxs-lookup"><span data-stu-id="972de-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="972de-190">Si vuole creare il modello di un termostato che misuri la temperatura e l'umidità.</span><span class="sxs-lookup"><span data-stu-id="972de-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="972de-191">I singoli dati saranno inviati all'hub IoT in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="972de-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="972de-192">Per impostazione predefinita, il termostato immette un evento temperatura ogni 2 minuti e un evento umidità ogni 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="972de-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="972de-193">Con l'evento immesso dovrà essere incluso un timestamp che indichi l'ora in cui è stata misurata la temperatura o l'umidità corrispondente.</span><span class="sxs-lookup"><span data-stu-id="972de-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="972de-194">Dato lo scenario, verranno illustrati due diversi metodi per modellare i dati e verrà spiegato l'effetto della modellazione sull'output serializzato.</span><span class="sxs-lookup"><span data-stu-id="972de-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="972de-195">Modello 1</span><span class="sxs-lookup"><span data-stu-id="972de-195">Model 1</span></span>
<span data-ttu-id="972de-196">Ecco la prima versione di un modello che supporta lo scenario precedente:</span><span class="sxs-lookup"><span data-stu-id="972de-196">Here's the first version of a model that supports the previous scenario:</span></span>

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

<span data-ttu-id="972de-197">Il modello include due eventi dati: **Temperature** e **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="972de-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="972de-198">A differenza degli esempi precedenti, il tipo di ogni evento è una struttura definita tramite **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="972de-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="972de-199">**TemperatureEvent** include una misura della temperatura e un timestamp. **HumidityEvent** contiene una misura dell'umidità e un timestamp.</span><span class="sxs-lookup"><span data-stu-id="972de-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="972de-200">Questo modello offre un modo naturale per modellare i dati per lo scenario descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="972de-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="972de-201">Quando si invia un evento nel cloud, si invia una coppia temperatura/timestamp o umidità/timestamp.</span><span class="sxs-lookup"><span data-stu-id="972de-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="972de-202">È possibile inviare un evento temperatura nel cloud usando codice come il seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-202">We can send a temperature event to the cloud using code such as the following:</span></span>

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

<span data-ttu-id="972de-203">Nel codice di esempio si useranno valori hardcoded per temperatura e umidità, ma si immagini di recuperare effettivamente questi valori mediante il campionamento dei sensori corrispondenti nel termostato.</span><span class="sxs-lookup"><span data-stu-id="972de-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="972de-204">Il codice precedente usa la funzione helper **GetDateTimeOffset** introdotta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="972de-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="972de-205">Per motivi che diventeranno più chiari in seguito, il codice separa in modo esplicito l'attività di serializzazione e di invio dell'evento.</span><span class="sxs-lookup"><span data-stu-id="972de-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="972de-206">Il codice precedente serializza l'evento temperatura in un buffer.</span><span class="sxs-lookup"><span data-stu-id="972de-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="972de-207">Quindi **sendMessage**, una funzione helper inclusa in **simplesample\_amqp**, invia l'evento all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

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

<span data-ttu-id="972de-208">Questo codice è un subset della funzione helper **SendAsync** descritta nella sezione precedente, che quindi non verrà illustrata di nuovo.</span><span class="sxs-lookup"><span data-stu-id="972de-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="972de-209">Quando si esegue il codice precedente per inviare l'evento temperatura, questo formato serializzato dell'evento viene inviato all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="972de-210">Viene inviato un evento temperatura di tipo **TemperatureEvent** la cui struttura contiene un membro **Temperature** e **Time**.</span><span class="sxs-lookup"><span data-stu-id="972de-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="972de-211">Questa condizione viene riflessa direttamente dei dati serializzati.</span><span class="sxs-lookup"><span data-stu-id="972de-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="972de-212">In modo analogo è possibile inviare un evento umidità con questo codice:</span><span class="sxs-lookup"><span data-stu-id="972de-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="972de-213">Il formato serializzato inviato all'hub IoT è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="972de-214">Anche in questo caso, è un comportamento previsto.</span><span class="sxs-lookup"><span data-stu-id="972de-214">Again, this is as expected.</span></span>

<span data-ttu-id="972de-215">Con questo modello si può immaginare come sia facile aggiungere altri eventi.</span><span class="sxs-lookup"><span data-stu-id="972de-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="972de-216">Si possono definire altre strutture con **DECLARE\_STRUCT** e includere l'evento corrispondente nel modello tramite **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="972de-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="972de-217">Ora si modificherà il modello in modo da includere gli stessi dati, ma con una struttura diversa.</span><span class="sxs-lookup"><span data-stu-id="972de-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="972de-218">Modello 2</span><span class="sxs-lookup"><span data-stu-id="972de-218">Model 2</span></span>
<span data-ttu-id="972de-219">Considerare questo modello come alternativa a quello precedente:</span><span class="sxs-lookup"><span data-stu-id="972de-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="972de-220">In questo caso sono state eliminate le macro **DECLARE\_STRUCT** e sono stati semplicemente definiti gli elementi di dati dello scenario usando tipi semplici del linguaggio di modellazione.</span><span class="sxs-lookup"><span data-stu-id="972de-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="972de-221">Per il momento si ignorerà l'evento **Time** .</span><span class="sxs-lookup"><span data-stu-id="972de-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="972de-222">Ecco quindi il codice per l'immissione dell'evento **Temperature**:</span><span class="sxs-lookup"><span data-stu-id="972de-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

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

<span data-ttu-id="972de-223">Questo codice invia l'evento serializzato seguente all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="972de-224">Il codice per inviare l'evento Humidity è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="972de-225">Questo codice invia queste informazioni all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="972de-226">Di nuovo nulla di insolito fino a questo punto.</span><span class="sxs-lookup"><span data-stu-id="972de-226">So far there are still no surprises.</span></span> <span data-ttu-id="972de-227">Si modificherà ora la modalità d'uso della macro SERIALIZE.</span><span class="sxs-lookup"><span data-stu-id="972de-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="972de-228">La macro **SERIALIZE** può accettare più eventi dati come argomenti.</span><span class="sxs-lookup"><span data-stu-id="972de-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="972de-229">In questo modo si possono serializzare insieme gli eventi **Temperature** e **Humidity** e inviarli all'hub IoT con una sola chiamata:</span><span class="sxs-lookup"><span data-stu-id="972de-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="972de-230">Si potrebbe supporre che il risultato di questo codice sia l'invio di due eventi dati all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="972de-231">[</span><span class="sxs-lookup"><span data-stu-id="972de-231">[</span></span>

<span data-ttu-id="972de-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="972de-232">{"Temperature":75},</span></span>

<span data-ttu-id="972de-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="972de-233">{"Humidity":45}</span></span>

<span data-ttu-id="972de-234">]</span><span class="sxs-lookup"><span data-stu-id="972de-234">]</span></span>

<span data-ttu-id="972de-235">In altre parole, si potrebbe ritenere che questo codice corrisponda all'invio di **Temperature** e **Humidity** separatamente</span><span class="sxs-lookup"><span data-stu-id="972de-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="972de-236">e che passare entrambi gli eventi a **SERIALIZE** nella stessa chiamata sia solo questione di praticità.</span><span class="sxs-lookup"><span data-stu-id="972de-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="972de-237">Non è però così.</span><span class="sxs-lookup"><span data-stu-id="972de-237">However, that’s not the case.</span></span> <span data-ttu-id="972de-238">Al contrario, il codice precedente invia questo singolo evento dati all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="972de-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="972de-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="972de-240">Può sembrare strano perché il modello definisce **Temperature** e **Humidity** come due eventi *distinti*:</span><span class="sxs-lookup"><span data-stu-id="972de-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="972de-241">Più precisamente, questi eventi non sono stati modellati con **Temperature** e **Humidity** nella stessa struttura:</span><span class="sxs-lookup"><span data-stu-id="972de-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="972de-242">Se fosse stato usato questo modello, sarebbe stato più facile capire in che modo **Temperature** e **Humidity** sarebbero inviati nello stesso messaggio serializzato.</span><span class="sxs-lookup"><span data-stu-id="972de-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="972de-243">Potrebbe tuttavia non essere chiaro perché funziona in questo modo quando si passano entrambi gli eventi dati a **SERIALIZE** con il modello n. 2.</span><span class="sxs-lookup"><span data-stu-id="972de-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="972de-244">Questo comportamento è più facile da comprendere se si conoscono i presupposti della libreria **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="972de-245">Per chiarire questo aspetto, si riesaminerà il modello:</span><span class="sxs-lookup"><span data-stu-id="972de-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="972de-246">Pensare al modello in termini di "orientato a oggetti".</span><span class="sxs-lookup"><span data-stu-id="972de-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="972de-247">In questo caso si modella un dispositivo fisico (Thermostat), che include attributi come **Temperature** e **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="972de-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="972de-248">Si può inviare l'intero stato del modello con un codice come il seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="972de-249">Presupponendo che i valori di Temperature, Humidity e Time siano impostati, si vedrà un evento come questo inviato all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="972de-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="972de-250">A volte è consigliabile inviare solo *alcune* proprietà del modello nel cloud. Questo è vero soprattutto se il modello contiene un numero elevato di eventi dati.</span><span class="sxs-lookup"><span data-stu-id="972de-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="972de-251">È utile inviare solo un subset di eventi dati, come nell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="972de-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="972de-252">Questo genera esattamente lo stesso evento serializzato come se si fosse definito **TemperatureEvent** con un membro **Temperature** e un membro **Time**, come è stato fatto nel modello n. 1.</span><span class="sxs-lookup"><span data-stu-id="972de-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="972de-253">In questo caso è stato possibile generare esattamente lo stesso evento serializzato usando un modello diverso (modello n. 2), perché la chiamata a **SERIALIZE** è stata eseguita in un modo diverso.</span><span class="sxs-lookup"><span data-stu-id="972de-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="972de-254">Il punto importante è che se si passano più eventi dati a **SERIALIZE** , presuppone che ogni evento sia una proprietà in un singolo oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="972de-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="972de-255">L'approccio migliore dipende dall'utente e da come viene considerato il modello.</span><span class="sxs-lookup"><span data-stu-id="972de-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="972de-256">Se si inviano "eventi" nel cloud e ogni evento contiene un set di proprietà definito, è più appropriato il primo approccio.</span><span class="sxs-lookup"><span data-stu-id="972de-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="972de-257">In tal caso, usare **DECLARE\_STRUCT** per definire la struttura di ogni evento e quindi includere gli eventi nel modello usando la macro **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="972de-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="972de-258">Inviare quindi ogni evento come illustrato sopra nel primo esempio.</span><span class="sxs-lookup"><span data-stu-id="972de-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="972de-259">Con questo approccio si passerà solo un singolo evento dati a **SERIALIZER**.</span><span class="sxs-lookup"><span data-stu-id="972de-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="972de-260">Se si considera il modello come se fosse orientato a oggetti, potrebbe essere più appropriato il secondo approccio.</span><span class="sxs-lookup"><span data-stu-id="972de-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="972de-261">In questo caso, gli elementi definiti con **WITH\_DATA** diventano le "proprietà" dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="972de-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="972de-262">Si passerà il subset di eventi che si preferisce a **SERIALIZE** , a seconda del livello di stato degli "oggetti" che si vuole inviare nel cloud.</span><span class="sxs-lookup"><span data-stu-id="972de-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="972de-263">Nessun approccio è giusto o sbagliato.</span><span class="sxs-lookup"><span data-stu-id="972de-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="972de-264">Tenere solo presente il funzionamento della libreria **serializer** e scegliere l'approccio di modellazione che meglio soddisfa le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="972de-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="972de-265">Gestione dei messaggi</span><span class="sxs-lookup"><span data-stu-id="972de-265">Message handling</span></span>
<span data-ttu-id="972de-266">Fino ad ora si è discusso solo dell'invio di eventi all'hub IoT, ma non è stata considerata la ricezione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="972de-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="972de-267">Il motivo è che quello che occorre sapere sulla ricezione dei messaggi è stato ampiamente illustrato in un [articolo precedente](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="972de-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="972de-268">Tenere presente, come detto in quell'articolo, che i messaggi vengono elaborati registrando una funzione di richiamata dei messaggi:</span><span class="sxs-lookup"><span data-stu-id="972de-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="972de-269">Si scrive quindi la funzione di callback che viene richiamata alla ricezione di un messaggio:</span><span class="sxs-lookup"><span data-stu-id="972de-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="972de-270">Questa implementazione di **IoTHubMessage** chiama la funzione specifica per ogni azione del modello.</span><span class="sxs-lookup"><span data-stu-id="972de-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="972de-271">Ad esempio, se il modello definisce questa azione:</span><span class="sxs-lookup"><span data-stu-id="972de-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="972de-272">È necessario definire una funzione con questa firma.</span><span class="sxs-lookup"><span data-stu-id="972de-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="972de-273">**SetAirResistance** .</span><span class="sxs-lookup"><span data-stu-id="972de-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="972de-274">Non è stato invece ancora illustrato qual è l'aspetto della versione serializzata del messaggio.</span><span class="sxs-lookup"><span data-stu-id="972de-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="972de-275">In altre parole, se si vuole inviare un messaggio **SetAirResistance** al dispositivo, quale sarà il suo aspetto?</span><span class="sxs-lookup"><span data-stu-id="972de-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="972de-276">Se si invia un messaggio a un dispositivo, si dovrà usare Azure IoT service SDK.</span><span class="sxs-lookup"><span data-stu-id="972de-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="972de-277">È comunque necessario sapere quale stringa inviare per richiamare un'azione particolare.</span><span class="sxs-lookup"><span data-stu-id="972de-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="972de-278">Il formato generale per l'invio di un messaggio è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="972de-279">Se invia un oggetto JSON serializzato con due proprietà: **Name** è il nome dell'azione, ovvero il messaggio, e **Parameters** contiene i parametri dell'azione.</span><span class="sxs-lookup"><span data-stu-id="972de-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="972de-280">Ad esempio, per richiamare **SetAirResistance** è possibile inviare questo messaggio a un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="972de-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="972de-281">Il nome dell'azione deve corrispondere esattamente a un'azione definita nel modello.</span><span class="sxs-lookup"><span data-stu-id="972de-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="972de-282">Anche i nomi dei parametri devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="972de-282">The parameter names must match as well.</span></span> <span data-ttu-id="972de-283">Tenere presente anche la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="972de-283">Also note case sensitivity.</span></span> <span data-ttu-id="972de-284">**Name** e **Parameters** sono sempre in maiuscolo.</span><span class="sxs-lookup"><span data-stu-id="972de-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="972de-285">Assicurarsi di rispettare la corrispondenza maiuscole/minuscole per i nomi di azioni e i parametri del modello.</span><span class="sxs-lookup"><span data-stu-id="972de-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="972de-286">In questo esempio, il nome dell'azione è "SetAirResistance" e non "setairresistance".</span><span class="sxs-lookup"><span data-stu-id="972de-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="972de-287">Le altre due azioni **TurnFanOn** e **TurnFanOff** possono essere richiamate inviando i messaggi seguenti a un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="972de-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="972de-288">Questo descrive tutto ciò che è necessario sapere quando si inviano eventi e si ricevono messaggi con la libreria **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="972de-289">Prima di proseguire, si esamineranno alcuni parametri che è possibile configurare per controllare le dimensioni del modello.</span><span class="sxs-lookup"><span data-stu-id="972de-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="972de-290">Configurazione delle macro</span><span class="sxs-lookup"><span data-stu-id="972de-290">Macro configuration</span></span>
<span data-ttu-id="972de-291">Se si usa la libreria **Serializer** , una parte importante dell'SDK che è opportuno tenere presente si trova nella libreria azure-c-shared-utility.</span><span class="sxs-lookup"><span data-stu-id="972de-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="972de-292">Se è stato clonato il repository Azure-iot-sdk-c da GitHub usando l'opzione ricorsiva, la libreria delle utilità condivise è disponibile qui:</span><span class="sxs-lookup"><span data-stu-id="972de-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="972de-293">Se la libreria non è stata clonata, è possibile trovarla [qui](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="972de-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="972de-294">Nella libreria delle utilità condivise, si troverà la seguente cartella:</span><span class="sxs-lookup"><span data-stu-id="972de-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="972de-295">Questa cartella contiene una soluzione di Visual Studio chiamata **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="972de-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="972de-296">Il programma in questa soluzione genera il file **macro\_utils.h**.</span><span class="sxs-lookup"><span data-stu-id="972de-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="972de-297">L'SDK include un file macro\_utils.h predefinito.</span><span class="sxs-lookup"><span data-stu-id="972de-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="972de-298">Questa soluzione consente tuttavia di modificare alcuni parametri e quindi di ricreare il file di intestazione in base a questi parametri.</span><span class="sxs-lookup"><span data-stu-id="972de-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="972de-299">I due parametri chiave da considerare sono **nArithmetic** e **nMacroParameters**, definiti in queste due righe del file macro\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="972de-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="972de-300">Questi valori sono i parametri predefiniti inclusi nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="972de-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="972de-301">Ecco il significato di ogni parametro:</span><span class="sxs-lookup"><span data-stu-id="972de-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="972de-302">nMacroParameters: controlla la quantità di parametri che possono essere inclusi in una definizione di macro DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="972de-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="972de-303">nArithmetic: controlla il numero totale di membri consentiti in un modello.</span><span class="sxs-lookup"><span data-stu-id="972de-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="972de-304">Il motivo per cui questi parametri sono importanti è il fatto che controllano le dimensioni massime del modello.</span><span class="sxs-lookup"><span data-stu-id="972de-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="972de-305">Considerare ad esempio questa definizione di modello:</span><span class="sxs-lookup"><span data-stu-id="972de-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="972de-306">Come già accennato, **DECLARE\_MODEL** è semplicemente una macro C.</span><span class="sxs-lookup"><span data-stu-id="972de-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="972de-307">I nomi del modello e l'istruzione **WITH\_DATA** (un'altra macro) sono parametri di **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="972de-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="972de-308">**nMacroParameters** definisce il numero di parametri che può essere incluso in **DECLARE\_MODELLO**.</span><span class="sxs-lookup"><span data-stu-id="972de-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="972de-309">In realtà definisce la quantità di eventi dati e dichiarazioni di azione supportata.</span><span class="sxs-lookup"><span data-stu-id="972de-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="972de-310">Quindi, il limite predefinito di 124 significa che è possibile definire un modello con una combinazione di circa 60 azioni ed eventi dati.</span><span class="sxs-lookup"><span data-stu-id="972de-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="972de-311">Se si prova a superare questo limite, verranno visualizzati errori del compilatore simili al seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="972de-312">Il parametro **nArithmetic** riguarda più il funzionamento interno del linguaggio macro che l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="972de-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="972de-313">Controlla il numero totale dei membri che si possono usare nel modello, incluse le macro **DECLARE_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="972de-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="972de-314">Se iniziano a essere visualizzati errori del compilatore come questo, provare ad aumentare il valore di **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="972de-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="972de-315">Per modificare questi parametri, modificare i valori nel file macro\_utils.tt, ricompilare la soluzione macro\_utils\_h\_generator.sln ed eseguire il programma compilato.</span><span class="sxs-lookup"><span data-stu-id="972de-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="972de-316">In questo caso, verrà generato un nuovo file macro\_utils.h che sarà inserito nella directory .\\common\\inc.</span><span class="sxs-lookup"><span data-stu-id="972de-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="972de-317">Per usare la nuova versione di macro\_utils.h, rimuovere il pacchetto NuGet **serializer** dalla soluzione e al suo posto includere il progetto di Visual Studio **serializer**.</span><span class="sxs-lookup"><span data-stu-id="972de-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="972de-318">In questo modo si consente la compilazione del codice in base al codice sorgente della libreria serializer,</span><span class="sxs-lookup"><span data-stu-id="972de-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="972de-319">incluso il file macro\_utils.h aggiornato.</span><span class="sxs-lookup"><span data-stu-id="972de-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="972de-320">Se si vuole procedere in questo modo per **simplesample\_amqp**, iniziare rimuovendo il pacchetto NuGet della libreria serializer dalla soluzione:</span><span class="sxs-lookup"><span data-stu-id="972de-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="972de-321">Aggiungere quindi questo progetto alla soluzione Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="972de-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="972de-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="972de-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="972de-323">Al termine, la soluzione dovrebbe avere un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="972de-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="972de-324">A questo punto quando si compila la soluzione, il file macro\_utils.h aggiornato viene incluso nel file binario.</span><span class="sxs-lookup"><span data-stu-id="972de-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="972de-325">Se si aumentano molto questi valori, potrebbero essere superati i limiti del compilatore.</span><span class="sxs-lookup"><span data-stu-id="972de-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="972de-326">A questo proposito, **nMacroParameters** è il parametro principale a cui prestare attenzione.</span><span class="sxs-lookup"><span data-stu-id="972de-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="972de-327">La specifica C99 definisce che è consentito un minimo di 127 parametri in una definizione di macro.</span><span class="sxs-lookup"><span data-stu-id="972de-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="972de-328">Il compilatore Microsoft segue esattamente la specifica e ha un limite di 127, quindi non si potrà aumentare **nMacroParameters** oltre il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="972de-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="972de-329">Altri compilatori potrebbero consentirlo, ad esempio il compilatore GNU supporta un limite più alto.</span><span class="sxs-lookup"><span data-stu-id="972de-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="972de-330">A questo punto è stato discusso praticamente tutto ciò che occorre sapere sulla scrittura del codice con la libreria **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="972de-331">Prima di concludere, ecco di seguito alcuni argomenti degli articoli precedenti che potrebbero risultare interessanti.</span><span class="sxs-lookup"><span data-stu-id="972de-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="972de-332">API di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="972de-332">The lower-level APIs</span></span>
<span data-ttu-id="972de-333">L'applicazione di esempio illustrata in questo articolo è **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="972de-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="972de-334">Questo esempio usa le API di livello superiore (non "LL") per inviare eventi e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="972de-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="972de-335">Se si usano queste API, viene eseguito un thread in background che si occupa dell'invio degli eventi e della ricezione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="972de-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="972de-336">Queste API (LL) di livello inferiore possono tuttavia essere usate per eliminare il thread in background e assumere il controllo esplicito dei tempi di invio di eventi e ricezione dei messaggi dal cloud.</span><span class="sxs-lookup"><span data-stu-id="972de-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="972de-337">Come descritto in un [articolo precedente](iot-hub-device-sdk-c-iothubclient.md)è disponibile un set di funzioni costituito dalle API di livello superiore:</span><span class="sxs-lookup"><span data-stu-id="972de-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="972de-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="972de-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="972de-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="972de-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="972de-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="972de-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="972de-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="972de-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="972de-342">Queste API sono illustrate in **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="972de-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="972de-343">È disponibile anche set analogo di API di livello inferiore.</span><span class="sxs-lookup"><span data-stu-id="972de-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="972de-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="972de-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="972de-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="972de-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="972de-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="972de-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="972de-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="972de-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="972de-348">Tenere presente che le API di livello inferiore funzionano esattamente come descritto negli articoli precedenti.</span><span class="sxs-lookup"><span data-stu-id="972de-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="972de-349">È possibile usare il primo set di API se si vuole avere un thread in background che gestisce l'invio degli eventi e la ricezione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="972de-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="972de-350">Usare il secondo set di API se si vuole avere il controllo esplicito dei tempi di invio e ricezione dei dati dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="972de-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="972de-351">Entrambi i set di API funzionano correttamente con la libreria **serializer** .</span><span class="sxs-lookup"><span data-stu-id="972de-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="972de-352">Per un esempio dell'uso delle API di livello inferiore con la libreria **serializer**, vedere l'applicazione **simplesample\_http**.</span><span class="sxs-lookup"><span data-stu-id="972de-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="972de-353">Argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="972de-353">Additional topics</span></span>
<span data-ttu-id="972de-354">Alcuni altri argomenti che vale la pena citare riguardano la gestione delle proprietà, l'uso di credenziali del dispositivo alternative e le opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="972de-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="972de-355">Ecco tutti gli argomenti illustrati in un [articolo precedente](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="972de-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="972de-356">L'aspetto principale in questo caso è che tutte queste funzionalità hanno lo stesso comportamento quando si usa sia la libreria **serializer** che la libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="972de-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="972de-357">Ad esempio, per associare proprietà a un evento dal modello, usare **IoTHubMessage\_Properties** e **Map**\_**AddorUpdate** come descritto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="972de-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="972de-358">Non ha importanza se l'evento è stato generato dalla libreria **serializer** o creato manualmente con la libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="972de-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="972de-359">Per quanto riguarda le credenziali del dispositivo alternative, **IoTHubClient\_LL\_Create** funziona altrettanto bene di **IoTHubClient\_CreateFromConnectionString** per l'allocazione di un **IOTHUB\_CLIENT\_HANDLE**.</span><span class="sxs-lookup"><span data-stu-id="972de-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="972de-360">Infine, se si usa la libreria **serializer**, è possibile impostare le opzioni di configurazione con **IoTHubClient\_LL\_SetOption** esattamente come è stato fatto con la libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="972de-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="972de-361">Una funzionalità esclusiva nella libreria **serializer** riguarda le API di inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="972de-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="972de-362">Prima di iniziare a utilizzare la libreria, è necessario chiamare **serializer\_init**:</span><span class="sxs-lookup"><span data-stu-id="972de-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="972de-363">Questa operazione viene eseguita subito prima di chiamare **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="972de-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="972de-364">In modo analogo, una volta che si è terminato di utilizzare la libreria, l'ultima chiamata da eseguire sarà **serializer\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="972de-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="972de-365">Per il resto, tutte le altre funzionalità elencate sopra hanno lo stesso comportamento sia nella libreria **serializer** che nella libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="972de-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="972de-366">Per altre informazioni su uno qualsiasi di questi argomenti, vedere l' [articolo precedente](iot-hub-device-sdk-c-iothubclient.md) di questa serie.</span><span class="sxs-lookup"><span data-stu-id="972de-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="972de-367">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="972de-367">Next steps</span></span>
<span data-ttu-id="972de-368">Questo articolo descrive in dettaglio gli aspetti univoci della libreria **serializer** inclusa in **Azure IoT SDK per dispositivi per C**. Con le informazioni fornite si dovrebbe avere una buona conoscenza di come usare i modelli per inviare eventi e ricevere messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="972de-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="972de-369">Questo articolo conclude anche la serie in tre parti relativa allo sviluppo di applicazioni con **Azure IoT SDK per dispositivi per C**. Le informazioni dovrebbero essere sufficienti non solo per iniziare, ma anche per avere una conoscenza approfondita del funzionamento delle API.</span><span class="sxs-lookup"><span data-stu-id="972de-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="972de-370">Per altre informazioni, nell'SDK sono disponibili alcuni esempi non illustrati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="972de-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="972de-371">Anche la [documentazione dell'SDK](https://github.com/Azure/azure-iot-sdk-c) è una risorsa molto utile per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="972de-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="972de-372">Per altre informazioni sullo sviluppo dell'hub IoT, vedere gli [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="972de-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="972de-373">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="972de-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="972de-374">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="972de-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
