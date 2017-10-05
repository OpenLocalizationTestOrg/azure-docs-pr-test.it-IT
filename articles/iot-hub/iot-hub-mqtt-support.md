---
title: Informazioni sul supporto MQTT dell'hub IoT di Azure | Documentazione Microsoft
description: Guida per sviluppatori - Supporto per dispositivi che si connettono a un endpoint che usa dispositivi dell'hub IoT con il protocollo MQTT. Sono incluse informazioni sul supporto MQTT integrato in Azure IoT SDK per dispositivi.
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eab70c1aa9c49a137c2ac1012449d57915fb0d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a><span data-ttu-id="6cd4a-104">Comunicare con l'hub IoT tramite il protocollo MQTT</span><span class="sxs-lookup"><span data-stu-id="6cd4a-104">Communicate with your IoT hub using the MQTT protocol</span></span>

<span data-ttu-id="6cd4a-105">L'hub IoT consente ai dispositivi di comunicare con gli endpoint dei dispositivi dell'hub IoT usando il protocollo [MQTT v3.1.1][lnk-mqtt-org] sulla porta 8883 o MQTT v3.1.1 con protocollo WebSocket sulla porta 443.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="6cd4a-106">L'hub IoT richiede che tutte le comunicazioni del dispositivo siano protette tramite TLS/SSL (pertanto l'hub IoT non supporta connessioni non protette sulla porta 1883).</span><span class="sxs-lookup"><span data-stu-id="6cd4a-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-to-iot-hub"></a><span data-ttu-id="6cd4a-107">Connessione all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="6cd4a-107">Connecting to IoT Hub</span></span>

<span data-ttu-id="6cd4a-108">Un dispositivo può usare il protocollo MQTT per connettersi a un hub IoT usando le librerie disponibili negli [Azure IoT SDK][lnk-device-sdks] o direttamente con il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span></span>

## <a name="using-the-device-sdks"></a><span data-ttu-id="6cd4a-109">Uso degli SDK per dispositivi</span><span class="sxs-lookup"><span data-stu-id="6cd4a-109">Using the device SDKs</span></span>

<span data-ttu-id="6cd4a-110">Gli [SDK per dispositivi][lnk-device-sdks] che supportano il protocollo MQTT sono disponibili per Java, Node.js, C, C# e Python.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="6cd4a-111">Gli SDK per dispositivi usano la stringa di connessione dell'hub IoT standard per stabilire una connessione a un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span></span> <span data-ttu-id="6cd4a-112">Per usare il protocollo MQTT, il parametro del protocollo del client deve essere impostato su **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span></span> <span data-ttu-id="6cd4a-113">Per impostazione predefinita, gli SDK per dispositivi si connettono a un hub IoT con il flag **CleanSession** impostato su **0** e usano **QoS 1** per lo scambio di messaggi con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span></span>

<span data-ttu-id="6cd4a-114">Quando un dispositivo è connesso a un hub IoT, gli SDK per dispositivi forniscono i metodi che consentono al dispositivo di inviare messaggi a un hub IoT e di riceverne.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span></span>

<span data-ttu-id="6cd4a-115">La tabella seguente include i collegamenti a esempi di codice per ogni linguaggio supportato e specifica il parametro da usare per stabilire una connessione all'hub IoT con il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span></span>

| <span data-ttu-id="6cd4a-116">Linguaggio</span><span class="sxs-lookup"><span data-stu-id="6cd4a-116">Language</span></span> | <span data-ttu-id="6cd4a-117">Parametro del protocollo</span><span class="sxs-lookup"><span data-stu-id="6cd4a-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="6cd4a-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="6cd4a-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="6cd4a-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="6cd4a-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="6cd4a-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="6cd4a-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="6cd4a-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="6cd4a-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="6cd4a-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="6cd4a-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="6cd4a-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="6cd4a-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="6cd4a-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="6cd4a-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="6cd4a-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a><span data-ttu-id="6cd4a-128">Migrazione di un'app per dispositivo da AMQP a MQTT</span><span class="sxs-lookup"><span data-stu-id="6cd4a-128">Migrating a device app from AMQP to MQTT</span></span>

<span data-ttu-id="6cd4a-129">Se si usano gli [SDK per dispositivi][lnk-device-sdks], per passare da AMQP a MQTT è necessario modificare il parametro del protocollo nell'inizializzazione client come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated previously.</span></span>

<span data-ttu-id="6cd4a-130">Quando si esegue questa operazione, controllare gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-130">When doing so, make sure to check the following items:</span></span>

* <span data-ttu-id="6cd4a-131">AMQP restituisce errori per diverse condizioni, mentre MQTT termina la connessione.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span></span> <span data-ttu-id="6cd4a-132">Di conseguenza, la logica di gestione delle eccezioni potrebbe richiedere alcune modifiche.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="6cd4a-133">MQTT non supporta le operazioni di *rifiuto* quando si ricevono [messaggi da cloud a dispositivo][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="6cd4a-134">Se l'app back-end deve ricevere una risposta dall'app per dispositivo, considerare la possibilità di usare [metodi diretti][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-the-mqtt-protocol-directly"></a><span data-ttu-id="6cd4a-135">Uso del protocollo MQTT direttamente</span><span class="sxs-lookup"><span data-stu-id="6cd4a-135">Using the MQTT protocol directly</span></span>
<span data-ttu-id="6cd4a-136">Se un dispositivo non può usare gli SDK per dispositivi, può comunque connettersi agli endpoint pubblici del dispositivo tramite il protocollo MQTT sulla porta 8883.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol on port 8883.</span></span> <span data-ttu-id="6cd4a-137">Nel pacchetto **CONNECT** il dispositivo deve usare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-137">In the **CONNECT** packet the device should use the following values:</span></span>

* <span data-ttu-id="6cd4a-138">Per il campo **ClientId** usare **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-138">For the **ClientId** field, use the **deviceId**.</span></span>
* <span data-ttu-id="6cd4a-139">Per il campo **Username** usare `{iothubhostname}/{device_id}/api-version=2016-11-14`, dove {iothubhostname} rappresenta il record CName completo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span></span>

    <span data-ttu-id="6cd4a-140">Ad esempio, se il nome dell'hub IoT è **contoso.azure-devices.net** e il nome del dispositivo è **MyDevice01**, il campo **Username** completo deve contenere `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="6cd4a-141">Per il campo **Password** usare un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-141">For the **Password** field, use a SAS token.</span></span> <span data-ttu-id="6cd4a-142">Il formato del token di firma di accesso condiviso è identico a quello per i protocolli HTTP e AMQP:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="6cd4a-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="6cd4a-144">Per altre informazioni su come generare i token di firma di accesso condiviso, vedere la sezione sui dispositivi nell'articolo [Uso dei token di sicurezza dell'hub IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="6cd4a-145">Durante il test è anche possibile usare lo strumento [Device Explorer][lnk-device-explorer] per generare rapidamente un token di firma di accesso condiviso da copiare e incollare nel codice:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="6cd4a-146">Andare alla scheda **Management** (Gestione) di **Device Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-146">Go to the **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="6cd4a-147">Fare clic su **SAS Token** in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="6cd4a-148">In **SASTokenForm** selezionare il dispositivo nell'elenco a discesa **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span></span> <span data-ttu-id="6cd4a-149">Impostare il valore **TTL**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="6cd4a-150">Fare clic su **Generate** per creare il token.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-150">Click **Generate** to create your token.</span></span>

     <span data-ttu-id="6cd4a-151">Il token di firma di accesso condiviso generato ha questa struttura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="6cd4a-152">La porzione di questo token da usare come campo **Password** per connettersi usando MQTT è: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="6cd4a-153">Per i pacchetti di connessione e disconnessione di MQTT l'hub IoT genera un evento nel canale **Monitoraggio operazioni** con ulteriori informazioni in grado di contribuire a risolvere i problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="6cd4a-154">Invio di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="6cd4a-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="6cd4a-155">Dopo avere stabilito una connessione, un dispositivo può inviare messaggi all'hub IoT usando `devices/{device_id}/messages/events/` o `devices/{device_id}/messages/events/{property_bag}` come **nome di argomento**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="6cd4a-156">L'elemento `{property_bag}` consente al dispositivo di inviare messaggi con proprietà aggiuntive in un formato con codifica URL.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="6cd4a-157">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="6cd4a-158">Questo elemento `{property_bag}`usa la stessa codifica delle stringhe di query nel protocollo HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span></span>
>
>

<span data-ttu-id="6cd4a-159">L'app per dispositivo può usare anche `devices/{device_id}/messages/events/{property_bag}` come **nome argomento Will** per definire *messaggi Will* da inoltrare come messaggio di telemetria.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span></span>

- <span data-ttu-id="6cd4a-160">L'hub IoT non supporta i messaggi di QoS 2.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="6cd4a-161">Quando un'app per dispositivo pubblica un messaggio con **QoS 2**, l'hub IoT chiude la connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span></span>
- <span data-ttu-id="6cd4a-162">L'hub IoT non rende persistenti i messaggi di mantenimento.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="6cd4a-163">Se un dispositivo invia un messaggio con il flag **RETAIN** impostato su 1, l'hub IoT aggiunge al messaggio la proprietà dell'applicazione **x-opt-retain**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span></span> <span data-ttu-id="6cd4a-164">In tal caso, anziché rendere persistente il messaggio di mantenimento, l'hub IoT passa invece all'app back-end.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span></span>
- <span data-ttu-id="6cd4a-165">L'hub IoT supporta solo una connessione MQTT attiva per ogni dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="6cd4a-166">Qualsiasi nuova connessione MQTT per conto dello stesso ID di dispositivo causa la perdita della connessione esistente da parte dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span></span>

<span data-ttu-id="6cd4a-167">Per altre informazioni, vedere [Guida per gli sviluppatori sulla messaggistica][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="6cd4a-168">Ricezione di messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="6cd4a-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="6cd4a-169">Per ricevere messaggi dall'hub IoT, un dispositivo deve eseguire la sottoscrizione con `devices/{device_id}/messages/devicebound/#` come **filtro di argomento**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="6cd4a-170">Il carattere jolly a più livelli **#** nel filtro argomento viene utilizzato solo per consentire al dispositivo di ricevere proprietà aggiuntive nel nome dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span></span> <span data-ttu-id="6cd4a-171">L'hub IoT on consente l'utilizzo di caratteri jolly **#** o **?**</span><span class="sxs-lookup"><span data-stu-id="6cd4a-171">IoT Hub does not allow the usage of the **#** or **?**</span></span> <span data-ttu-id="6cd4a-172">per il filtro di argomenti secondari.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="6cd4a-173">Poiché l'hub IoT non è un broker di messaggistica di pubblicazione e sottoscrizione generico, supporta solo i nomi di argomento e i filtri di argomento documentati .</span><span class="sxs-lookup"><span data-stu-id="6cd4a-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span></span>

<span data-ttu-id="6cd4a-174">Il dispositivo non riceverà i messaggi dall'hub IoT prima di aver effettuato la sottoscrizione all'endpoint del dispositivo specifico, rappresentato dal filtro argomento `devices/{device_id}/messages/devicebound/#`.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-174">The device does not receive any messages from IoT Hub, until it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="6cd4a-175">Dopo aver stabilito la sottoscrizione correttamente, il dispositivo inizierà a ricevere solo messaggi da cloud a dispositivo che gli sono stati inviati dopo la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-175">After successful subscription has been established, the device starts receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span></span> <span data-ttu-id="6cd4a-176">Se il dispositivo si connette con il flag **CleanSession** impostato su **0**, la sottoscrizione sarà mantenuta tra sessioni diverse.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-176">If the device connects with **CleanSession** flag set to **0**, the subscription is persisted across different sessions.</span></span> <span data-ttu-id="6cd4a-177">In questo caso, alla connessione successiva con **CleanSession 0** il dispositivo riceverà i messaggi in sospeso che gli sono stati inviati mentre era disconnesso.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-177">In this case, the next time it connects with **CleanSession 0** the device receives outstanding messages that have been sent to it while it was disconnected.</span></span> <span data-ttu-id="6cd4a-178">Se il dispositivo usa il flag **CleanSession** impostato su **1** tuttavia, non riceverà i messaggi dall'hub IoT fino a quando non si registra presso l'endpoint del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-178">If the device uses **CleanSession** flag set to **1** though, it does not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span></span>

<span data-ttu-id="6cd4a-179">L'hub IoT recapita i messaggi con il **nome di argomento** `devices/{device_id}/messages/devicebound/` o `devices/{device_id}/messages/devicebound/{property_bag}` se sono presenti proprietà dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="6cd4a-180">`{property_bag}` contiene coppie chiave/valore con codifica URL di proprietà dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="6cd4a-181">Solo le proprietà dell'applicazione e le proprietà di sistema configurabili dall'utente, ad esempio **messageId** o **correlationId**, sono incluse nel contenitore delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span></span> <span data-ttu-id="6cd4a-182">I nomi delle proprietà di sistema hanno il prefisso **$**. Le proprietà dell'applicazione usano il nome della proprietà originale senza il prefisso.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span></span>

<span data-ttu-id="6cd4a-183">Quando un'app del dispositivo esegue una sottoscrizione a un argomento con **QoS 2**, l'hub IoT concede il livello QoS 1 massimo nel pacchetto **SUBACK**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span></span> <span data-ttu-id="6cd4a-184">Successivamente, l'hub IoT invierà i messaggi al dispositivo tramite QoS 1.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-184">After that, IoT Hub delivers messages to the device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="6cd4a-185">Recupero delle proprietà dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="6cd4a-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="6cd4a-186">Un dispositivo effettua la sottoscrizione a `$iothub/twin/res/#` per ricevere le risposte dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span></span> <span data-ttu-id="6cd4a-187">Invia quindi un messaggio vuoto all'argomento `$iothub/twin/GET/?$rid={request id}`, con un valore popolato per **request id**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**.</span></span> <span data-ttu-id="6cd4a-188">Il servizio invierà quindi un messaggio di risposta con i dati del dispositivo gemello nell'argomento `$iothub/twin/res/{status}/?$rid={request id}`, usando lo stesso **ID richiesta** della richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-188">The service then sends a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span></span>

<span data-ttu-id="6cd4a-189">L'ID richiesta può essere qualsiasi valore valido per la proprietà di un messaggio, come descritto nella [Guida per gli sviluppatori sulla messaggistica dell'hub IoT][lnk-messaging], e lo stato viene convalidato come valore intero.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-189">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="6cd4a-190">Il corpo della risposta contiene la sezione delle proprietà del dispositivo gemello:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-190">The response body contains the properties section of the device twin:</span></span>

<span data-ttu-id="6cd4a-191">Il corpo della voce del registro delle identità sarà limitato al membro "properties", ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-191">The body of the identity registry entry limited to the “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="6cd4a-192">I possibili codici di stato sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-192">The possible status codes are:</span></span>

|<span data-ttu-id="6cd4a-193">Stato</span><span class="sxs-lookup"><span data-stu-id="6cd4a-193">Status</span></span> | <span data-ttu-id="6cd4a-194">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cd4a-194">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6cd4a-195">200</span><span class="sxs-lookup"><span data-stu-id="6cd4a-195">200</span></span> | <span data-ttu-id="6cd4a-196">Success</span><span class="sxs-lookup"><span data-stu-id="6cd4a-196">Success</span></span> |
| <span data-ttu-id="6cd4a-197">429</span><span class="sxs-lookup"><span data-stu-id="6cd4a-197">429</span></span> | <span data-ttu-id="6cd4a-198">Numero eccessivo di richieste (limitazione), come descritto in [Limitazione dell'hub IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-198">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="6cd4a-199">5**</span><span class="sxs-lookup"><span data-stu-id="6cd4a-199">5**</span></span> | <span data-ttu-id="6cd4a-200">Errori server</span><span class="sxs-lookup"><span data-stu-id="6cd4a-200">Server errors</span></span> |

<span data-ttu-id="6cd4a-201">Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-201">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="6cd4a-202">Aggiornare le proprietà segnalate di un dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6cd4a-202">Update device twin's reported properties</span></span>

<span data-ttu-id="6cd4a-203">La sequenza seguente descrive in che modo un dispositivo aggiorna le proprietà dichiarate in un dispositivo gemello nell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-203">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span></span>

1. <span data-ttu-id="6cd4a-204">Un dispositivo deve prima sottoscrivere l'argomento `$iothub/twin/res/#` per ricevere le risposte dell'operazione dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-204">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="6cd4a-205">Un dispositivo invia un messaggio che contiene l'aggiornamento di un dispositivo gemello per l'argomento `$iothub/twin/PATCH/properties/reported/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-205">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="6cd4a-206">Questo messaggio include un valore **request id**.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-206">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="6cd4a-207">Il servizio invia un messaggio di risposta che contiene il nuovo valore ETag per la raccolta di proprietà dichiarate sull'argomento `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-207">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="6cd4a-208">Questo messaggio di risposta usa lo stesso valore **request id** della richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-208">This response message uses the same **request id** as the request.</span></span>

<span data-ttu-id="6cd4a-209">Il corpo del messaggio di richiesta contiene un documento JSON che specifica nuovi valori per le proprietà segnalate. Non è possibile modificare altre proprietà o altri metadati.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-209">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="6cd4a-210">Ogni membro nel documento JSON aggiorna o aggiunge il membro corrispondente nel documento del dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-210">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span></span> <span data-ttu-id="6cd4a-211">Un membro impostato su `null` elimina il membro dall'oggetto contenitore.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-211">A member set to `null`, deletes the member from the containing object.</span></span> <span data-ttu-id="6cd4a-212">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-212">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="6cd4a-213">I possibili codici di stato sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-213">The possible status codes are:</span></span>

|<span data-ttu-id="6cd4a-214">Stato</span><span class="sxs-lookup"><span data-stu-id="6cd4a-214">Status</span></span> | <span data-ttu-id="6cd4a-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cd4a-215">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6cd4a-216">200</span><span class="sxs-lookup"><span data-stu-id="6cd4a-216">200</span></span> | <span data-ttu-id="6cd4a-217">Success</span><span class="sxs-lookup"><span data-stu-id="6cd4a-217">Success</span></span> |
| <span data-ttu-id="6cd4a-218">400</span><span class="sxs-lookup"><span data-stu-id="6cd4a-218">400</span></span> | <span data-ttu-id="6cd4a-219">Richiesta non valida.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-219">Bad Request.</span></span> <span data-ttu-id="6cd4a-220">JSON non valido</span><span class="sxs-lookup"><span data-stu-id="6cd4a-220">Malformed JSON</span></span> |
| <span data-ttu-id="6cd4a-221">429</span><span class="sxs-lookup"><span data-stu-id="6cd4a-221">429</span></span> | <span data-ttu-id="6cd4a-222">Numero eccessivo di richieste (limitazione), come descritto in [Limitazione dell'hub IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-222">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="6cd4a-223">5**</span><span class="sxs-lookup"><span data-stu-id="6cd4a-223">5**</span></span> | <span data-ttu-id="6cd4a-224">Errori server</span><span class="sxs-lookup"><span data-stu-id="6cd4a-224">Server errors</span></span> |

<span data-ttu-id="6cd4a-225">Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-225">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="6cd4a-226">Ricezione delle notifiche di aggiornamento delle proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="6cd4a-226">Receiving desired properties update notifications</span></span>

<span data-ttu-id="6cd4a-227">Quando un dispositivo è connesso, l'hub IoT invia notifiche all'argomento `$iothub/twin/PATCH/properties/desired/?$version={new version}`, con il contenuto dell'aggiornamento eseguito dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-227">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span></span> <span data-ttu-id="6cd4a-228">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-228">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="6cd4a-229">Come per gli aggiornamenti delle proprietà, i valori `null` indicano l'eliminazione del membro dell'oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-229">As for property updates, `null` values means that the JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="6cd4a-230">L'hub IoT genera notifiche di modifica solo quando i dispositivi sono connessi.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-230">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="6cd4a-231">Assicurarsi di implementare il [flusso di riconnessione del dispositivo][lnk-devguide-twin-reconnection] per mantenere la sincronizzazione delle proprietà desiderate tra l'hub IoT e l'app per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-231">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span></span>

<span data-ttu-id="6cd4a-232">Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-232">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-to-a-direct-method"></a><span data-ttu-id="6cd4a-233">Rispondere a un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="6cd4a-233">Respond to a direct method</span></span>

<span data-ttu-id="6cd4a-234">Un dispositivo deve effettuare la sottoscrizione a `$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-234">First, a device has to subscribe to `$iothub/methods/POST/#`.</span></span> <span data-ttu-id="6cd4a-235">L'hub IoT invia le richieste di metodo all'argomento `$iothub/methods/POST/{method name}/?$rid={request id}` con un codice JSON valido o un corpo vuoto.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-235">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="6cd4a-236">Per rispondere, il dispositivo invia all'argomento `$iothub/methods/res/{status}/?$rid={request id}` un messaggio con un codice JSON valido o un corpo vuoto, dove l'**ID della richiesta** deve corrispondere al valore presente nel messaggio della richiesta e lo **stato** deve essere un numero intero.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-236">To respond, the device sends a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span></span>

<span data-ttu-id="6cd4a-237">Per altre informazioni, vedere la [Guida per gli sviluppatori sui metodi diretti][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-237">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="6cd4a-238">Ulteriori considerazioni</span><span class="sxs-lookup"><span data-stu-id="6cd4a-238">Additional considerations</span></span>

<span data-ttu-id="6cd4a-239">Se è necessario personalizzare il comportamento del protocollo MQTT sul lato cloud, è infine consigliabile vedere [Gateway del protocollo IoT Azure][lnk-azure-protocol-gateway], che descrive come distribuire un gateway del protocollo personalizzato con prestazioni elevate che si interfaccia direttamente con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-239">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="6cd4a-240">Il gateway del protocollo IoT Azure consente di personalizzare il protocollo del dispositivo per supportare le distribuzioni di MQTT cosiddette "brownfield" o altri protocolli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-240">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="6cd4a-241">Questo approccio richiede tuttavia l'esecuzione e la gestione di un gateway di protocollo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="6cd4a-241">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cd4a-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cd4a-242">Next steps</span></span>

<span data-ttu-id="6cd4a-243">Per altre informazioni sul protocollo MQTT, vedere la [documentazione di MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="6cd4a-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="6cd4a-244">Per altre informazioni sulla pianificazione della distribuzione dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-244">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="6cd4a-245">[Catalogo dei dispositivi Azure Certified per IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-245">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="6cd4a-246">[Supportare protocolli aggiuntivi][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-246">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="6cd4a-247">[Eseguire il confronto con Hub eventi][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-247">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="6cd4a-248">[Scalabilità, disponibilità elevata e ripristino di emergenza][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-248">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="6cd4a-249">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="6cd4a-249">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6cd4a-250">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-250">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="6cd4a-251">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6cd4a-251">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
