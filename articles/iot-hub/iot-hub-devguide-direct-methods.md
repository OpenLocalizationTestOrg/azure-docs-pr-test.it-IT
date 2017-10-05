---
title: Informazioni sui metodi diretti dell'hub IoT di Azure | Documentazione Microsoft
description: 'Guida per gli sviluppatori: usare metodi diretti per richiamare il codice nei dispositivi da un''app di servizio.'
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
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="c8fc5-103">Comprendere e richiamare metodi diretti dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="c8fc5-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="c8fc5-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c8fc5-104">Overview</span></span>
<span data-ttu-id="c8fc5-105">L'hub IoT offre la possibilità di richiamare metodi diretti nei dispositivi dal cloud.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="c8fc5-106">I metodi diretti rappresentano un'interazione di tipo richiesta-risposta con un dispositivo simile a una chiamata HTTP, dato che dopo il timeout specificato dall'utente l'esito positivo o negativo viene comunicato immediatamente.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="c8fc5-107">Questo risulta utile in scenari in cui l'azione immediata da intraprendere varia a seconda che il dispositivo sia riuscito o meno a rispondere. Un esempio è rappresentato dall'invio di un SMS di riattivazione a un dispositivo offline, in cui l'invio di un SMS ha un costo maggiore rispetto a una chiamata a un metodo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="c8fc5-108">Ogni metodo del dispositivo è destinato a un unico dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-108">Each device method targets a single device.</span></span> <span data-ttu-id="c8fc5-109">I [processi][lnk-devguide-jobs] permettono di richiamare i metodi diretti in più dispositivi e di pianificare la chiamata al metodo per i dispositivi disconnessi.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="c8fc5-110">Chiunque abbia autorizzazioni di **connessione servizio** per l'hub IoT può richiamare un metodo in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="c8fc5-111">Quando usare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="c8fc5-111">When to use</span></span>
<span data-ttu-id="c8fc5-112">I metodi diretti si basano su un modello di tipo richiesta- risposta e sono destinati a comunicazioni che necessitano di una conferma immediata del risultato, in genere per il controllo interattivo del dispositivo, ad esempio l'accensione di un ventilatore.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="c8fc5-113">Vedere [Cloud-to-device communication guidance][lnk-c2d-guidance] (Indicazioni sulla comunicazione da cloud a dispositivo) in caso di dubbi tra l'uso delle proprietà specifiche, dei metodi diretti o dei messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="c8fc5-114">Ciclo di vita dei metodi</span><span class="sxs-lookup"><span data-stu-id="c8fc5-114">Method lifecycle</span></span>
<span data-ttu-id="c8fc5-115">I metodi diretti vengono implementati nel dispositivo. Per creare correttamente un'istanza possono essere necessari zero o più input nel payload del metodo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="c8fc5-116">Per richiamare un metodo diretto è possibile usare un URI per il servizio (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="c8fc5-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="c8fc5-117">Il dispositivo riceve i metodi diretti tramite un argomento MQTT specifico del dispositivo (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="c8fc5-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="c8fc5-118">In futuro potranno essere supportati metodi diretti su altri protocolli di rete sul lato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="c8fc5-119">Quando si richiama un metodo diretto in un dispositivo, i valori e i nomi di proprietà possono contenere solo caratteri alfanumerici stampabili US-ASCII, ad eccezione dei seguenti: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="c8fc5-120">I metodi diretti sono sincroni e possono solo avere esito positivo o negativo dopo il periodo di timeout. Il valore predefinito è 30 secondi, ma il valore massimo impostabile è 3600 secondi.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="c8fc5-121">Risultano utili negli scenari interattivi in cui si vuole che il dispositivo agisca esclusivamente se è online e riceve comandi, ad esempio nel caso dell'accensione di una luce da un telefono.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="c8fc5-122">In questi scenari l'esito positivo o negativo deve essere immediato, in modo che il servizio cloud possa agire in base al risultato il prima possibile.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="c8fc5-123">Il dispositivo può restituire un corpo del messaggio come risultato del metodo, ma non è necessario che il metodo esegua questa operazione.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="c8fc5-124">Nelle chiamate ai metodi non esiste alcuna garanzia di ordinamento o semantica di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="c8fc5-125">I metodi diretti supportano solo HTTP lato cloud e solo MQTT lato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="c8fc5-126">Il payload per le richieste e le risposte del metodo è un documento JSON con dimensioni massime di 8 KB.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="c8fc5-127">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-127">Reference topics:</span></span>
<span data-ttu-id="c8fc5-128">Gli argomenti di riferimento seguenti offrono altre informazioni sull'uso dei metodi diretti.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="c8fc5-129">Richiamare un metodo diretto da un'app back-end</span><span class="sxs-lookup"><span data-stu-id="c8fc5-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="c8fc5-130">Chiamata al metodo</span><span class="sxs-lookup"><span data-stu-id="c8fc5-130">Method invocation</span></span>
<span data-ttu-id="c8fc5-131">Le chiamate a metodi diretti in un dispositivo sono chiamate HTTP e includono:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="c8fc5-132">*URI* specifico del dispositivo (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="c8fc5-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="c8fc5-133">*Metodo* POST</span><span class="sxs-lookup"><span data-stu-id="c8fc5-133">The POST *method*</span></span>
* <span data-ttu-id="c8fc5-134">*Intestazioni* contenenti l'autorizzazione, l'ID richiesta, il tipo di contenuto e la codifica del contenuto</span><span class="sxs-lookup"><span data-stu-id="c8fc5-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="c8fc5-135">*Corpo* JSON trasparente nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-135">A transparent JSON *body* in the following format:</span></span>

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

<span data-ttu-id="c8fc5-136">Il timeout è espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-136">Timeout is in seconds.</span></span> <span data-ttu-id="c8fc5-137">Se il timeout non è impostato, il valore predefinito è 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="c8fc5-138">Response</span><span class="sxs-lookup"><span data-stu-id="c8fc5-138">Response</span></span>
<span data-ttu-id="c8fc5-139">L'app back-end riceve una risposta che include:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="c8fc5-140">*Codice di stato HTTP*, usato per errori provenienti dall'hub IoT, incluso un errore 404 per i dispositivi attualmente non connessi</span><span class="sxs-lookup"><span data-stu-id="c8fc5-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="c8fc5-141">*Intestazioni* contenenti l'ETag, l'ID richiesta, il tipo di contenuto e la codifica del contenuto</span><span class="sxs-lookup"><span data-stu-id="c8fc5-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="c8fc5-142">*Corpo* JSON nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="c8fc5-143">Sia `status` che `body` vengono forniti dal dispositivo e usati per rispondere con la descrizione e/o il codice di stato del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="c8fc5-144">Gestire un metodo diretto in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="c8fc5-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="c8fc5-145">Chiamata al metodo</span><span class="sxs-lookup"><span data-stu-id="c8fc5-145">Method invocation</span></span>
<span data-ttu-id="c8fc5-146">I dispositivi ricevono richieste di metodi diretti nell'argomento MQTT: `$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="c8fc5-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="c8fc5-147">Il corpo ricevuto dal dispositivo è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="c8fc5-148">Le richieste di metodo sono QoS 0.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="c8fc5-149">Response</span><span class="sxs-lookup"><span data-stu-id="c8fc5-149">Response</span></span>
<span data-ttu-id="c8fc5-150">Il dispositivo invia risposte a `$iothub/methods/res/{status}/?$rid={request id}`, in cui:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="c8fc5-151">La proprietà `status` è lo stato di esecuzione del metodo fornito dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="c8fc5-152">La proprietà `$rid` è l'ID richiesta della chiamata al metodo ricevuta dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="c8fc5-153">Il corpo è impostato dal dispositivo e accetta qualsiasi stato.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="c8fc5-154">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="c8fc5-154">Additional reference material</span></span>
<span data-ttu-id="c8fc5-155">Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="c8fc5-156">[Endpoint dell'hub IoT][lnk-endpoints] illustra i diversi endpoint esposti da ogni hub IoT per operazioni della fase di esecuzione e di gestione.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="c8fc5-157">[Quote e limitazioni][lnk-quotas] descrive le quote applicabili al servizio Hub IoT e il comportamento di limitazione previsto quando si usa il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="c8fc5-158">[Azure IoT SDK per dispositivi e servizi][lnk-sdks] elenca gli SDK nei diversi linguaggi che è possibile usare quando si sviluppano app per dispositivi e servizi che interagiscono con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="c8fc5-159">[Il linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing messaggi][lnk-query] descrive il linguaggio di query dell'hub IoT che è possibile usare per recuperare informazioni dall'hub IoT sui processi e i dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="c8fc5-160">[Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt] offre altre informazioni sul supporto dell'hub IoT per il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="c8fc5-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8fc5-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8fc5-161">Next steps</span></span>
<span data-ttu-id="c8fc5-162">Ora che si è appreso come usare i metodi diretti, è possibile vedere un altro argomento di interesse reperibile nell'argomento seguente della Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="c8fc5-163">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="c8fc5-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="c8fc5-164">Per provare alcuni dei concetti descritti in questo articolo, può essere utile l'esercitazione seguente sull'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="c8fc5-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="c8fc5-165">[Usare metodi diretti][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="c8fc5-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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
