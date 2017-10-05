---
title: 'Azure IoT SDK per dispositivi per C: IoTHubClient | Documentazione Microsoft'
description: Come usare la libreria IoTHubClient in Azure IoT SDK per dispositivi per C per creare app per dispositivi che comunicano con un hub IoT.
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
ms.openlocfilehash: 422d89014511f0d08ba57a893570ff7b253b7bc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="cc609-103">Azure IoT SDK per dispositivi per C: altre informazioni su IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="cc609-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="cc609-104">Il [primo articolo](iot-hub-device-sdk-c-intro.md) di questa serie ha introdotto **Azure IoT SDK per dispositivi per C**. e spiegato che l'SDK comprende due livelli architetturali.</span><span class="sxs-lookup"><span data-stu-id="cc609-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="cc609-105">Al livello di base è presente la libreria **IoTHubClient** che gestisce direttamente la comunicazione con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="cc609-106">È inclusa anche libreria **serializer**, che si basa sulla libreria IoTHubClient per fornire i servizi di serializzazione.</span><span class="sxs-lookup"><span data-stu-id="cc609-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="cc609-107">In questo articolo sono forniti dettagli aggiuntivi sulla libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="cc609-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="cc609-108">L'articolo precedente descrive come usare la libreria **IoTHubClient** per inviare eventi all'hub IoT e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="cc609-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="cc609-109">Questo articolo estende la discussione, spiegando come gestire con più precisione *quando* inviare e ricevere dati, introducendo le **API di livello inferiore**.</span><span class="sxs-lookup"><span data-stu-id="cc609-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="cc609-110">Viene illustrato anche come associare le proprietà agli eventi, e recuperarle dai messaggi, usando le funzionalità di gestione delle proprietà nella libreria **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="cc609-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="cc609-111">Saranno infine descritti diversi metodi aggiuntivi per gestire i messaggi ricevuti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="cc609-112">Questo articolo si conclude con il riepilogo di un paio di vari argomenti, incluse altre informazioni sulle credenziali del dispositivo e come gestire il comportamento della libreria **IoTHubClient** tramite le opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cc609-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="cc609-113">Per illustrare questi argomenti, si useranno esempi dell'SDK relativi a **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="cc609-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="cc609-114">Se si vuole seguire la procedura, vedere le applicazioni **iothub\_client\_sample\_http** e **iothub\_client\_sample\_amqp** incluse in Azure IoT SDK per dispositivi per C. Tutto ciò che viene descritto nelle sezioni seguenti è illustrato in questi esempi.</span><span class="sxs-lookup"><span data-stu-id="cc609-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="cc609-115">È possibile trovare il repository GitHub di [**Azure IoT SDK per dispositivi per C**](https://github.com/Azure/azure-iot-sdk-c) e visualizzare i dettagli dell'API nelle [informazioni di riferimento per l'API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="cc609-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="cc609-116">API di livello inferiore</span><span class="sxs-lookup"><span data-stu-id="cc609-116">The lower-level APIs</span></span>
<span data-ttu-id="cc609-117">Nell'articolo precedente è descritto il funzionamento di base di **IotHubClient** nel contesto dell'applicazione **iothub\_client\_sample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="cc609-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="cc609-118">Spiega ad esempio come inizializzare la libreria con questo codice.</span><span class="sxs-lookup"><span data-stu-id="cc609-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="cc609-119">Spiega anche come inviare eventi con questa chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="cc609-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="cc609-120">Viene anche descritto come ricevere messaggi registrando una funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="cc609-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="cc609-121">L'articolo illustra anche come liberare risorse con codice simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="cc609-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="cc609-122">Ci sono tuttavia funzioni complementari per ognuna di queste API:</span><span class="sxs-lookup"><span data-stu-id="cc609-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="cc609-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="cc609-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="cc609-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="cc609-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="cc609-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="cc609-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="cc609-126">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="cc609-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="cc609-127">Il nome dell'API per tutte queste funzioni include "LL".</span><span class="sxs-lookup"><span data-stu-id="cc609-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="cc609-128">I parametri di ognuna di queste funzioni sono inoltre identici ai rispettivi elementi analoghi non LL.</span><span class="sxs-lookup"><span data-stu-id="cc609-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="cc609-129">Il comportamento di queste funzioni è tuttavia diverso per un aspetto importante.</span><span class="sxs-lookup"><span data-stu-id="cc609-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="cc609-130">Quando si chiama **IoTHubClient\_CreateFromConnectionString**, le librerie sottostanti creano un nuovo thread che viene eseguito in background.</span><span class="sxs-lookup"><span data-stu-id="cc609-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="cc609-131">Questo thread invia eventi all'hub IoT e ne riceve i messaggi.</span><span class="sxs-lookup"><span data-stu-id="cc609-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="cc609-132">Questi thread non vengono creati quando si utilizzano le API "LL".</span><span class="sxs-lookup"><span data-stu-id="cc609-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="cc609-133">La creazione del thread in background è un aspetto pratico per lo sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="cc609-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="cc609-134">Non occorre preoccuparsi in modo esplicito dell'invio di eventi e della ricezione di messaggi dall'hub IoT, perché tutto avviene automaticamente in background.</span><span class="sxs-lookup"><span data-stu-id="cc609-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="cc609-135">Al contrario, le API "LL" forniscono il controllo esplicito sulla comunicazione con l'hub IoT, se necessario.</span><span class="sxs-lookup"><span data-stu-id="cc609-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="cc609-136">Per comprendere meglio questo aspetto, si esaminerà un esempio:</span><span class="sxs-lookup"><span data-stu-id="cc609-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="cc609-137">Quando si chiama **IoTHubClient\_SendEventAsync**, si inserisce effettivamente l'evento in un buffer.</span><span class="sxs-lookup"><span data-stu-id="cc609-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="cc609-138">Il thread in background creato quando si chiama **IoTHubClient\_CreateFromConnectionString** monitora continuamente questo buffer e invia tutti i dati che contiene all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="cc609-139">Ciò avviene in background contemporaneamente all'esecuzione di altre attività da parte del thread principale.</span><span class="sxs-lookup"><span data-stu-id="cc609-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="cc609-140">In modo analogo, quando si registra una funzione di callback per i messaggi tramite **IoTHubClient\_SetMessageCallback**, si indica all'SDK di fare in modo che il thread in background richiami la funzione di callback quando si riceve un messaggio, indipendentemente dal thread principale.</span><span class="sxs-lookup"><span data-stu-id="cc609-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="cc609-141">Le API "LL" non creano un thread in background.</span><span class="sxs-lookup"><span data-stu-id="cc609-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="cc609-142">È necessario invece chiamare una nuova API per inviare e ricevere esplicitamente i dati dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="cc609-143">Questo approccio è illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="cc609-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="cc609-144">L'applicazione **iothub\_client\_sample\_http** inclusa nell'SDK fornisce una dimostrazione delle API di livello inferiore.</span><span class="sxs-lookup"><span data-stu-id="cc609-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="cc609-145">In questo esempio, si inviano eventi all'hub IoT con codice simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cc609-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="cc609-146">Le prime tre righe creano il messaggio e l'ultima riga invia l'evento.</span><span class="sxs-lookup"><span data-stu-id="cc609-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="cc609-147">Tuttavia, come detto in precedenza, "inviare" l'evento significa che i dati vengono semplicemente inseriti in un buffer.</span><span class="sxs-lookup"><span data-stu-id="cc609-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="cc609-148">Quando si chiama **IoTHubClient\_LL\_SendEventAsync**, non viene trasmesso nulla in rete.</span><span class="sxs-lookup"><span data-stu-id="cc609-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="cc609-149">Per inserire effettivamente i dati nell'hub IoT, è necessario chiamare **IoTHubClient\_LL\_DoWork** come in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="cc609-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="cc609-150">Questo codice dall'applicazione **iothub\_client\_sample\_http** chiama ripetutamente **IoTHubClient\_LL\_DoWork**.</span><span class="sxs-lookup"><span data-stu-id="cc609-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="cc609-151">Ogni volta che viene chiamato, **IoTHubClient\_LL\_DoWork** invia alcuni eventi dal buffer all'hub IoT e recupera un messaggio in coda inviato al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc609-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="cc609-152">In quest'ultimo caso, se è stata registrata una funzione di callback per i messaggi, verrà richiamato il callback, presupponendo la presenza di messaggi nella coda.</span><span class="sxs-lookup"><span data-stu-id="cc609-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="cc609-153">Questa funzione di callback sarà stata registrata con codice simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cc609-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="cc609-154">Il motivo per cui si chiama spesso **IoTHubClient\_LL\_DoWork** in un ciclo è dovuto al fatto che a ogni chiamata vengono inviati *alcuni* eventi memorizzati nel buffer all'hub IoT e viene recuperato *il successivo* messaggio in coda per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc609-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="cc609-155">Non è garantito che a ogni chiamata siano inviati tutti gli eventi nel buffer o siano recuperati tutti i messaggi in coda.</span><span class="sxs-lookup"><span data-stu-id="cc609-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="cc609-156">Se si vuole inviare tutti gli eventi nel buffer e quindi continuare con altre attività di elaborazione, è possibile sostituire questo ciclo con codice simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cc609-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="cc609-157">Questo codice chiama **IoTHubClient\_LL\_DoWork** finché tutti gli eventi non saranno stati inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="cc609-158">Non significa però che si siano ricevuti anche tutti i messaggi in coda.</span><span class="sxs-lookup"><span data-stu-id="cc609-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="cc609-159">Questo comportamento è dovuto in parte al fatto che la verifica di "tutti" i messaggi non è un'azione deterministica.</span><span class="sxs-lookup"><span data-stu-id="cc609-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="cc609-160">Cosa accadrebbe che si recuperassero "tutti" i messaggi, ma subito dopo ne venisse inviato un altro al dispositivo?</span><span class="sxs-lookup"><span data-stu-id="cc609-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="cc609-161">Un modo migliore per gestire questo meccanismo consiste nell'usare un timeout programmato.</span><span class="sxs-lookup"><span data-stu-id="cc609-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="cc609-162">Ad esempio, la funzione di callback dei messaggi potrebbe reimpostare un timer ogni volta che viene richiamata.</span><span class="sxs-lookup"><span data-stu-id="cc609-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="cc609-163">Si può quindi scrivere la logica per continuare l'elaborazione, ad esempio, non sono stati ricevuti messaggi negli ultimi *X* secondi.</span><span class="sxs-lookup"><span data-stu-id="cc609-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="cc609-164">Una volta completato l'inserimento degli eventi e la ricezione dei messaggi, accertarsi di chiamare la funzione corrispondente per pulire le risorse.</span><span class="sxs-lookup"><span data-stu-id="cc609-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="cc609-165">Sostanzialmente è disponibile un solo set di API per inviare e ricevere dati con un thread in background e un altro set di API che esegue la stessa operazione senza il thread in background.</span><span class="sxs-lookup"><span data-stu-id="cc609-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="cc609-166">Molti sviluppatori potrebbero preferire le API non LL, ma le API di livello inferiore sono utili quando lo sviluppatore vuole avere il controllo esplicito delle trasmissioni in rete.</span><span class="sxs-lookup"><span data-stu-id="cc609-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="cc609-167">Ad esempio, alcuni dispositivi raccolgono dati nel tempo e solo eventi in ingresso a intervalli specificati, come una volta all'ora o una volta al giorno.</span><span class="sxs-lookup"><span data-stu-id="cc609-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="cc609-168">Le API di livello inferiore consentono di controllare in modo esplicito quando inviare e ricevere dati dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="cc609-169">Altri preferiscono la semplicità offerta dalle API di livello inferiore.</span><span class="sxs-lookup"><span data-stu-id="cc609-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="cc609-170">Tutto avviene nel thread principale, invece di eseguire una parte delle operazioni in background.</span><span class="sxs-lookup"><span data-stu-id="cc609-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="cc609-171">Qualunque sia il modello scelto, assicurarsi di usare le API in modo coerente.</span><span class="sxs-lookup"><span data-stu-id="cc609-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="cc609-172">Se si inizia a chiamare **IoTHubClient\_LL\_CreateFromConnectionString**, assicurarsi di usare solo le API di livello inferiore corrispondenti per tutte le attività successive:</span><span class="sxs-lookup"><span data-stu-id="cc609-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="cc609-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="cc609-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="cc609-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="cc609-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="cc609-175">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="cc609-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="cc609-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="cc609-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="cc609-177">È vero comunque anche il contrario.</span><span class="sxs-lookup"><span data-stu-id="cc609-177">The opposite is true as well.</span></span> <span data-ttu-id="cc609-178">Se si inizia con **IoTHubClient\_CreateFromConnectionString**, continuare a usare le API non LL per tutte le altre attività di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="cc609-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="cc609-179">Per un esempio completo delle API di livello inferiore, vedere l'applicazione **iothub\_client\_sample\_http** in Azure IoT SDK per dispositivi per C.</span><span class="sxs-lookup"><span data-stu-id="cc609-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="cc609-180">Si può fare riferimento all'applicazione **iothub\_client\_sample\_amqp** per un esempio completo delle API non LL.</span><span class="sxs-lookup"><span data-stu-id="cc609-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="cc609-181">Gestione delle proprietà</span><span class="sxs-lookup"><span data-stu-id="cc609-181">Property handling</span></span>
<span data-ttu-id="cc609-182">Fino a questo punto, nel descrivere l'invio di dati si è fatto riferimento al corpo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="cc609-183">Si consideri ad esempio questo codice:</span><span class="sxs-lookup"><span data-stu-id="cc609-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="cc609-184">Questo esempio invia l'evento all'hub IoT con il testo "Hello World".</span><span class="sxs-lookup"><span data-stu-id="cc609-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="cc609-185">L'hub IoT consente tuttavia di associare proprietà a ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="cc609-186">Le proprietà sono coppie nome/valore che possono essere associate al messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="cc609-187">Ad esempio, è possibile modificare il codice precedente per associare una proprietà al messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="cc609-188">Per iniziare, chiamare **IoTHubMessage\_Properties** e passare l'handle del messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="cc609-189">Verrà restituito un riferimento a **MAP\_HANDLE** che consente di iniziare ad aggiungere proprietà.</span><span class="sxs-lookup"><span data-stu-id="cc609-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="cc609-190">Quest'ultima operazione si esegue chiamando **Map\_AddOrUpdate**, che riceve un riferimento a MAP\_HANDLE, il nome della proprietà e il valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="cc609-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="cc609-191">Con questa API è possibile aggiungere tutte le proprietà necessarie.</span><span class="sxs-lookup"><span data-stu-id="cc609-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="cc609-192">Quando l'evento viene letto da **Hub eventi**, il ricevitore può enumerare le proprietà e recuperare i valori corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="cc609-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="cc609-193">Ad esempio, in .NET questa operazione verrebbe eseguita con l'accesso alla [raccolta delle proprietà nell'oggetto EventData](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc609-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="cc609-194">Nell'esempio precedente le proprietà vengono associate a un evento inviato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="cc609-195">Le proprietà possono anche essere associate ai messaggi ricevuti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="cc609-196">Per recuperare le proprietà da un messaggio, è possibile usare codice come il seguente nella funzione di callback del messaggio:</span><span class="sxs-lookup"><span data-stu-id="cc609-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
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

<span data-ttu-id="cc609-197">La chiamata a **IoTHubMessage\_Properties** restituisce il riferimento a **MAP\_HANDLE**.</span><span class="sxs-lookup"><span data-stu-id="cc609-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="cc609-198">Il riferimento viene quindi passato a **Map\_GetInternals** per ottenere un riferimento a una matrice di coppie nome/valore, oltre a un conteggio delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="cc609-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="cc609-199">A questo punto, si tratta semplicemente di enumerare le proprietà per ottenere i valori necessari.</span><span class="sxs-lookup"><span data-stu-id="cc609-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="cc609-200">Non si devono usare proprietà nell'applicazione,</span><span class="sxs-lookup"><span data-stu-id="cc609-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="cc609-201">ma se è necessario impostarle negli eventi o recuperarle dai messaggi, la libreria **IoTHubClient** facilita l'operazione.</span><span class="sxs-lookup"><span data-stu-id="cc609-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="cc609-202">Gestione dei messaggi</span><span class="sxs-lookup"><span data-stu-id="cc609-202">Message handling</span></span>
<span data-ttu-id="cc609-203">Come spiegato in precedenza, quando arriva un messaggio dall'hub IoT, la libreria **IoTHubClient** risponde richiamando una funzione di callback registrata.</span><span class="sxs-lookup"><span data-stu-id="cc609-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="cc609-204">Un parametro restituito da questa funzione merita tuttavia qualche spiegazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="cc609-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="cc609-205">Ecco un estratto della funzione di callback nell'applicazione di esempio **iothub\_client\_sample\_http**:</span><span class="sxs-lookup"><span data-stu-id="cc609-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="cc609-206">Il tipo restituito è **IOTHUBMESSAGE\_DISPOSITION\_RESULT** e in questo caso specifico verrà restituito **IOTHUBMESSAGE\_ACCEPTED**.</span><span class="sxs-lookup"><span data-stu-id="cc609-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="cc609-207">Sono presenti altri valori che possono essere restituiti da questa funzione e che modificano il modo in cui la libreria **IoTHubClient** risponde al callback del messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="cc609-208">Ecco le opzioni.</span><span class="sxs-lookup"><span data-stu-id="cc609-208">Here are the options.</span></span>

* <span data-ttu-id="cc609-209">**IOTHUBMESSAGE\_ACCEPTED**: il messaggio è stato elaborato correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc609-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="cc609-210">La libreria **IoTHubClient** non richiamerà di nuovo la funzione di callback con lo stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="cc609-211">**IOTHUBMESSAGE\_REJECTED**: il messaggio non è stato elaborato e non si prevede di farlo in futuro.</span><span class="sxs-lookup"><span data-stu-id="cc609-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="cc609-212">La libreria **IoTHubClient** non dovrà richiamare di nuovo la funzione di callback con lo stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="cc609-213">**IOTHUBMESSAGE\_ABANDONED**: il messaggio non è stato elaborato, ma la libreria **IoTHubClient** dovrà richiamare di nuovo la funzione di callback con lo stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="cc609-214">Per i primo due codici restituiti la libreria **IoTHubClient** invia un messaggio all'hub IoT indicando che il messaggio dovrà essere eliminato dalla coda del dispositivo e non essere recapitato di nuovo.</span><span class="sxs-lookup"><span data-stu-id="cc609-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="cc609-215">L'effetto in definitiva è lo stesso, ovvero il messaggio viene eliminato dalla coda del dispositivo, ma rimane ancora la registrazione se il messaggio è stato accettato o rifiutato.</span><span class="sxs-lookup"><span data-stu-id="cc609-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="cc609-216">La registrazione di questa distinzione è utile per i mittenti del messaggio, che possono rimanere in ascolto dei commenti e scoprire se un dispositivo ha accettato o rifiutato un messaggio specifico.</span><span class="sxs-lookup"><span data-stu-id="cc609-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="cc609-217">Nell'ultimo caso, viene inviato un messaggio anche all'hub IoT, ma con l'indicazione che il messaggio dovrà essere recapitato di nuovo.</span><span class="sxs-lookup"><span data-stu-id="cc609-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="cc609-218">In genere, un messaggio viene abbandonato se si verifica un errore, ma si vuole provare a elaborarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="cc609-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="cc609-219">Al contrario, è opportuno rifiutare un messaggio quando si verifica un errore irreversibile o si decide semplicemente che non si vuole elaborare il messaggio.</span><span class="sxs-lookup"><span data-stu-id="cc609-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="cc609-220">In ogni caso, è sufficiente conoscere i diversi codici restituiti per poter dedurre il comportamento che si vuole ottenere dalla libreria **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="cc609-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="cc609-221">Credenziali del dispositivo alternative</span><span class="sxs-lookup"><span data-stu-id="cc609-221">Alternate device credentials</span></span>
<span data-ttu-id="cc609-222">Come spiegato in precedenza, la prima cosa da fare quando si usa la libreria **IoTHubClient** è ottenere un **IOTHUB\_CLIENT\_HANDLE** con una chiamata come la seguente:</span><span class="sxs-lookup"><span data-stu-id="cc609-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="cc609-223">Gli argomenti di **IoTHubClient\_CreateFromConnectionString** sono la stringa di connessione del dispositivo e un parametro che indica il protocollo da usare per comunicare con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="cc609-224">La stringa di connessione del dispositivo ha un formato simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cc609-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="cc609-225">Questa stringa contiene quattro informazioni: nome dell'hub IoT, suffisso dell'hub IoT, ID dispositivo e chiave di accesso condivisa.</span><span class="sxs-lookup"><span data-stu-id="cc609-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="cc609-226">Si ottiene il nome di dominio completo (FQDN) di un hub IoT quando si crea l'istanza dell'hub IoT nel portale di Azure. Si avrà così il nome dell'hub IoT (la prima parte dell'FQDN) e il suffisso dell'hub IoT (il resto dell'FQDN).</span><span class="sxs-lookup"><span data-stu-id="cc609-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="cc609-227">L'ID dispositivo e la chiave di accesso condiviso si ottengono al momento della registrazione del dispositivo con l'hub IoT, come descritto nell'[articolo precedente](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="cc609-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="cc609-228">**IoTHubClient\_CreateFromConnectionString** offre un modo per inizializzare la libreria.</span><span class="sxs-lookup"><span data-stu-id="cc609-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="cc609-229">Se si preferisce, è possibile creare un nuovo **IOTHUB\_CLIENT\_HANDLE** usando i singoli parametri invece della stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc609-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="cc609-230">Questo risultato si ottiene con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="cc609-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="cc609-231">Si ottiene lo stesso risultato di **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="cc609-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="cc609-232">Può sembrare ovvio che si preferisca usare **IoTHubClient\_CreateFromConnectionString** invece di questo metodo di inizializzazione più dettagliato.</span><span class="sxs-lookup"><span data-stu-id="cc609-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="cc609-233">Tenere però presente che quando si registra un dispositivo nell'hub IoT, si ottiene un ID dispositivo e una chiave del dispositivo, non una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="cc609-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="cc609-234">Lo strumento SDK per l'*esplorazione dei dispositivi* introdotto nell'[articolo precedente](iot-hub-device-sdk-c-intro.md) usa le librerie di **Azure IoT SDK per servizi** per creare la stringa di connessione del dispositivo da ID dispositivo, chiave del dispositivo e nome host dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="cc609-235">Può quindi essere preferibile chiamare **IoTHubClient\_LL\_Create**, perché evita di dover generare una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="cc609-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="cc609-236">Usare il metodo più pratico.</span><span class="sxs-lookup"><span data-stu-id="cc609-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="cc609-237">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="cc609-237">Configuration options</span></span>
<span data-ttu-id="cc609-238">Fino a questo punto, tutto ciò che è stato illustrato sul funzionamento della libreria **IoTHubClient** riflette il relativo comportamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="cc609-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="cc609-239">Sono tuttavia disponibili alcune opzioni che si possono impostare per modificare il funzionamento della libreria.</span><span class="sxs-lookup"><span data-stu-id="cc609-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="cc609-240">Questa operazione viene eseguita sfruttando l'API **IoTHubClient\_LL\_SetOption**.</span><span class="sxs-lookup"><span data-stu-id="cc609-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="cc609-241">Considerare questo esempio:</span><span class="sxs-lookup"><span data-stu-id="cc609-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="cc609-242">Ci sono un paio di opzioni usate comunemente:</span><span class="sxs-lookup"><span data-stu-id="cc609-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="cc609-243">**SetBatching** (bool): se **true**, i dati destinati all'hub IoT vengono inviati in batch.</span><span class="sxs-lookup"><span data-stu-id="cc609-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="cc609-244">Se **false**, i messaggi vengono inviati singolarmente.</span><span class="sxs-lookup"><span data-stu-id="cc609-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="cc609-245">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="cc609-245">The default is **false**.</span></span> <span data-ttu-id="cc609-246">Si noti che l'opzione **SetBatching** si applica solo al protocollo HTTP e non ai protocolli MQTT o AMQP.</span><span class="sxs-lookup"><span data-stu-id="cc609-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="cc609-247">**Timeout** (unsigned int): questo valore è rappresentato in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="cc609-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="cc609-248">Se l'invio di una richiesta HTTP o la ricezione di una risposta richiede più tempo di questo intervallo, si verifica il timeout della connessione.</span><span class="sxs-lookup"><span data-stu-id="cc609-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="cc609-249">L'opzione di invio in batch è importante.</span><span class="sxs-lookup"><span data-stu-id="cc609-249">The batching option is important.</span></span> <span data-ttu-id="cc609-250">Per impostazione predefinita, la libreria accetta eventi in ingresso singolarmente. Un singolo evento è qualsiasi elemento passato a **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="cc609-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="cc609-251">Se l'opzione di invio in batch è **true**, la libreria raccoglie dal buffer quanti più eventi possibile, fino alle dimensioni massime dei messaggi accettate dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cc609-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="cc609-252">Il batch di eventi viene inviato all'hub IoT in una singola chiamata HTTP. I singoli elementi vengono aggregati in una matrice JSON.</span><span class="sxs-lookup"><span data-stu-id="cc609-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="cc609-253">In genere l'abilitazione dell'invio in batch consente di ottenere un miglioramento significativo delle prestazioni, perché si riducono le sequenze di andata e ritorno in rete.</span><span class="sxs-lookup"><span data-stu-id="cc609-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="cc609-254">Si riduce in modo significativo anche la larghezza di banda, perché si invia un unico set di intestazioni HTTP con un batch di eventi, invece di un set di intestazioni per ogni singolo evento.</span><span class="sxs-lookup"><span data-stu-id="cc609-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="cc609-255">A meno di avere un motivo specifico per agire diversamente, è consigliabile abilitare l'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="cc609-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc609-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc609-256">Next steps</span></span>
<span data-ttu-id="cc609-257">In questo articolo viene descritto in dettaglio il comportamento della libreria **IoTHubClient** inclusa in **Azure IoT SDK per dispositivi per C**. Grazie a queste informazioni si dovrebbe avere acquisito una buona conoscenza delle funzionalità della libreria **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="cc609-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="cc609-258">L' [articolo successivo](iot-hub-device-sdk-c-serializer.md) fornisce dettagli simili sulla libreria **serializer** .</span><span class="sxs-lookup"><span data-stu-id="cc609-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="cc609-259">Per altre informazioni sullo sviluppo dell'hub IoT, vedere gli [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="cc609-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="cc609-260">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="cc609-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="cc609-261">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="cc609-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
