---
title: metodi di indirizzare aaaUnderstand IoT Hub di Azure | Documenti Microsoft
description: Guida per sviluppatori - utilizzare metodi diretti tooinvoke codice nei dispositivi da un'applicazione di servizio.
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="d9b77-103">Comprendere e richiamare metodi diretti dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="d9b77-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="d9b77-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d9b77-104">Overview</span></span>
<span data-ttu-id="d9b77-105">IoT Hub offre metodi diretti di possibilità tooinvoke sui dispositivi dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d9b77-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="d9b77-106">Metodi diretti rappresentano un'interazione richiesta-risposta con un tooan simili dispositivi HTTP chiamare in quanto essi esito positivo o negativo (dopo un timeout specificato dall'utente).</span><span class="sxs-lookup"><span data-stu-id="d9b77-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="d9b77-107">Ciò è utile per scenari in cui il corso hello di un'azione immediata è diverso a seconda se il dispositivo hello è stato in grado di toorespond, ad esempio l'invio di un dispositivo di riattivazione tooa SMS se un dispositivo è offline (SMS molto più costoso rispetto a una chiamata al metodo).</span><span class="sxs-lookup"><span data-stu-id="d9b77-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="d9b77-108">Ogni metodo del dispositivo è destinato a un unico dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d9b77-108">Each device method targets a single device.</span></span> <span data-ttu-id="d9b77-109">[I processi] [ lnk-devguide-jobs] forniscono un modo tooinvoke metodi diretti su più dispositivi e pianificare la chiamata di metodo per i dispositivi disconnessi.</span><span class="sxs-lookup"><span data-stu-id="d9b77-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="d9b77-110">Chiunque abbia autorizzazioni di **connessione servizio** per l'hub IoT può richiamare un metodo in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d9b77-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="d9b77-111">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="d9b77-111">When toouse</span></span>
<span data-ttu-id="d9b77-112">Metodi diretti seguono un modello di richiesta-risposta e disponibili solo per le comunicazioni che richiedono la conferma immediata dei relativi risultati, in genere interattivo il controllo di hello dispositivo, ad esempio tooturn su una ventola.</span><span class="sxs-lookup"><span data-stu-id="d9b77-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="d9b77-113">Fare riferimento troppo[indicazioni di comunicazione Cloud a dispositivo] [ lnk-c2d-guidance] in caso di dubbio tra l'utilizzo di proprietà desiderate, indirizzare i metodi o i messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d9b77-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="d9b77-114">Ciclo di vita dei metodi</span><span class="sxs-lookup"><span data-stu-id="d9b77-114">Method lifecycle</span></span>
<span data-ttu-id="d9b77-115">Metodi diretti sono implementati nel dispositivo hello e possono richiedere zero o più input in hello metodo payload toocorrectly creare un'istanza.</span><span class="sxs-lookup"><span data-stu-id="d9b77-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="d9b77-116">Per richiamare un metodo diretto è possibile usare un URI per il servizio (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="d9b77-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="d9b77-117">Il dispositivo riceve i metodi diretti tramite un argomento MQTT specifico del dispositivo (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="d9b77-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="d9b77-118">Si potrebbe supporta i metodi diretti su protocolli di rete sul lato dispositivo aggiuntivi in hello future.</span><span class="sxs-lookup"><span data-stu-id="d9b77-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="d9b77-119">Quando si richiama un metodo diretto in un dispositivo, i valori e nomi di proprietà possono contenere solo US-ASCII stampabili caratteri alfanumerici, ad eccezione di quelli hello seguente insieme: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="d9b77-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="d9b77-120">Indirizzare i metodi sono sincroni e l'esito positivo o esito negativo dopo il periodo di timeout di hello (impostazione predefinita: 30 secondi, impostabile backup too3600 secondi).</span><span class="sxs-lookup"><span data-stu-id="d9b77-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="d9b77-121">Metodi diretti sono utili negli scenari interattivi in cui si desidera tooact un dispositivo solo se il dispositivo di hello è online e riceventi comandi, ad esempio l'attivazione chiaro da un telefono.</span><span class="sxs-lookup"><span data-stu-id="d9b77-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="d9b77-122">In questi scenari, si desidera toosee un immediato esito positivo o negativo in modo servizio cloud hello può agire sul risultato di hello appena possibile.</span><span class="sxs-lookup"><span data-stu-id="d9b77-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="d9b77-123">dispositivo Hello può restituire un corpo del messaggio in seguito a metodo hello, ma non è necessario per toodo metodo hello in modo.</span><span class="sxs-lookup"><span data-stu-id="d9b77-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="d9b77-124">Nelle chiamate ai metodi non esiste alcuna garanzia di ordinamento o semantica di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="d9b77-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="d9b77-125">Metodo diretto sono solo per HTTP dal lato cloud hello e MQTT solo dal lato dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="d9b77-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="d9b77-126">il payload per il metodo richieste e risposte Hello è un documento JSON backup too8KB.</span><span class="sxs-lookup"><span data-stu-id="d9b77-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="d9b77-127">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="d9b77-127">Reference topics:</span></span>
<span data-ttu-id="d9b77-128">Hello argomenti di riferimento seguenti offrono ulteriori informazioni sull'utilizzo di metodi diretti.</span><span class="sxs-lookup"><span data-stu-id="d9b77-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="d9b77-129">Richiamare un metodo diretto da un'app back-end</span><span class="sxs-lookup"><span data-stu-id="d9b77-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="d9b77-130">Chiamata al metodo</span><span class="sxs-lookup"><span data-stu-id="d9b77-130">Method invocation</span></span>
<span data-ttu-id="d9b77-131">Le chiamate a metodi diretti in un dispositivo sono chiamate HTTP e includono:</span><span class="sxs-lookup"><span data-stu-id="d9b77-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="d9b77-132">Hello *URI* toohello specifico dispositivo (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="d9b77-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="d9b77-133">Hello POST *(metodo)*</span><span class="sxs-lookup"><span data-stu-id="d9b77-133">hello POST *method*</span></span>
* <span data-ttu-id="d9b77-134">*Intestazioni* , che contengono hello authorization, richiedere l'ID, tipo di contenuto e la codifica del contenuto</span><span class="sxs-lookup"><span data-stu-id="d9b77-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="d9b77-135">JSON trasparente *corpo* in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d9b77-135">A transparent JSON *body* in hello following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="d9b77-136">Il timeout è espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="d9b77-136">Timeout is in seconds.</span></span> <span data-ttu-id="d9b77-137">Se non è stato impostato alcun timeout, il valore predefinito too30 secondi.</span><span class="sxs-lookup"><span data-stu-id="d9b77-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="d9b77-138">Response</span><span class="sxs-lookup"><span data-stu-id="d9b77-138">Response</span></span>
<span data-ttu-id="d9b77-139">applicazione di back-end Hello riceve una risposta che comprende:</span><span class="sxs-lookup"><span data-stu-id="d9b77-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="d9b77-140">*Codice di stato HTTP*, che viene utilizzata per errori provenienti da hello IoT Hub, tra cui un errore 404 per i dispositivi non è attualmente connesso</span><span class="sxs-lookup"><span data-stu-id="d9b77-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="d9b77-141">*Intestazioni* , che contengono hello ETag, richiedere l'ID, tipo di contenuto e la codifica del contenuto</span><span class="sxs-lookup"><span data-stu-id="d9b77-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="d9b77-142">Un formato JSON *corpo* in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d9b77-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="d9b77-143">Entrambi `status` e `body` sono forniti dal dispositivo hello e usate toorespond con codice di stato del dispositivo hello e/o descrizione.</span><span class="sxs-lookup"><span data-stu-id="d9b77-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="d9b77-144">Gestire un metodo diretto in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="d9b77-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="d9b77-145">Chiamata al metodo</span><span class="sxs-lookup"><span data-stu-id="d9b77-145">Method invocation</span></span>
<span data-ttu-id="d9b77-146">I dispositivi ricevono richieste dirette del metodo su un argomento MQTT hello:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="d9b77-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="d9b77-147">corpo Hello quale dispositivo hello riceve si hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d9b77-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="d9b77-148">Le richieste di metodo sono QoS 0.</span><span class="sxs-lookup"><span data-stu-id="d9b77-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="d9b77-149">Response</span><span class="sxs-lookup"><span data-stu-id="d9b77-149">Response</span></span>
<span data-ttu-id="d9b77-150">dispositivo Hello invia risposte troppo`$iothub/methods/res/{status}/?$rid={request id}`, dove:</span><span class="sxs-lookup"><span data-stu-id="d9b77-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="d9b77-151">Hello `status` proprietà è stato fornito dal dispositivo hello di esecuzione del metodo.</span><span class="sxs-lookup"><span data-stu-id="d9b77-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="d9b77-152">Hello `$rid` proprietà è l'ID richiesta hello dalla chiamata al metodo hello ricevuta dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9b77-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="d9b77-153">corpo Hello viene impostato dal dispositivo hello e può essere qualsiasi stato.</span><span class="sxs-lookup"><span data-stu-id="d9b77-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="d9b77-154">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="d9b77-154">Additional reference material</span></span>
<span data-ttu-id="d9b77-155">Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:</span><span class="sxs-lookup"><span data-stu-id="d9b77-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="d9b77-156">[Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.</span><span class="sxs-lookup"><span data-stu-id="d9b77-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="d9b77-157">[Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello che si applicano toohello servizio IoT Hub e hello limitazione tooexpect comportamento quando si utilizza servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d9b77-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="d9b77-158">[Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9b77-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="d9b77-159">[Il linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi] [ lnk-query] descrive hello linguaggio di query IoT Hub è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.</span><span class="sxs-lookup"><span data-stu-id="d9b77-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="d9b77-160">[Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="d9b77-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9b77-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d9b77-161">Next steps</span></span>
<span data-ttu-id="d9b77-162">A questo punto si è appreso come metodi diretti toouse, potrebbe risultare interessante nel seguente argomento della Guida alla developer IoT Hub hello:</span><span class="sxs-lookup"><span data-stu-id="d9b77-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="d9b77-163">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="d9b77-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="d9b77-164">Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello segue esercitazione IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="d9b77-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="d9b77-165">[Usare metodi diretti][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="d9b77-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
