---
title: supporto di Azure IoT Hub MQTT aaaUnderstand | Documenti Microsoft
description: Sviluppatore Guida - supporto per i dispositivi si connettono a endpoint che utilizzano il dispositivo di IoT Hub utilizzando tooan hello protocollo MQTT. Include informazioni sul supporto MQTT integrato in hello Azure IoT dispositivo SDK.
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
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="ca664-104">Comunicare con l'hub IoT protocollo MQTT hello</span><span class="sxs-lookup"><span data-stu-id="ca664-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="ca664-105">IoT Hub consente toocommunicate dispositivi con hello Hub IoT dispositivo endpoint che utilizzano hello [MQTT v3.1.1] [ lnk-mqtt-org] protocollo sulla porta 8883 o v3.1.1 MQTT attraverso il protocollo WebSocket sulla porta 443.</span><span class="sxs-lookup"><span data-stu-id="ca664-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="ca664-106">IoT Hub richiede tutti toobe di comunicazione dispositivo protetta tramite TLS/SSL (di conseguenza, IoT Hub non supporta le connessioni non sicure attraverso la porta 1883).</span><span class="sxs-lookup"><span data-stu-id="ca664-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="ca664-107">Connessione tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="ca664-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="ca664-108">Un dispositivo può usare hub IoT di hello MQTT protocollo tooconnect tooan tramite l'utilizzo delle librerie di hello in hello [Azure IoT SDK] [ lnk-device-sdks] o utilizzando il protocollo MQTT hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="ca664-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="ca664-109">Utilizzo di hello dispositivo SDK</span><span class="sxs-lookup"><span data-stu-id="ca664-109">Using hello device SDKs</span></span>

<span data-ttu-id="ca664-110">[Dispositivo SDK] [ lnk-device-sdks] tale hello supporto protocollo MQTT sono disponibili per Java, Node.js, C, c# e Python.</span><span class="sxs-lookup"><span data-stu-id="ca664-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="ca664-111">uso del dispositivo di Hello SDK hello standard IoT Hub connessione stringa tooestablish un hub IoT tooan di connessione.</span><span class="sxs-lookup"><span data-stu-id="ca664-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="ca664-112">protocollo MQTT toouse hello, hello client protocollo parametro deve essere impostato troppo**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="ca664-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="ca664-113">Per impostazione predefinita, il dispositivo di hello SDK connettersi tooan IoT Hub con hello **CleanSession** flag impostato troppo**0** e utilizzare **1 QoS** per scambio di messaggi con l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="ca664-114">Quando un dispositivo è connesso tooan hub IoT, dispositivo hello SDK forniscono metodi che consentono di messaggi di toosend dispositivo hello tooand ricevere messaggi da un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ca664-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="ca664-115">Hello nella tabella seguente sono contenuti collegamenti toocode esempi per ogni lingua supportata e specifica hello parametro toouse tooestablish tooIoT una connessione Hub utilizzando il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="ca664-116">Lingua</span><span class="sxs-lookup"><span data-stu-id="ca664-116">Language</span></span> | <span data-ttu-id="ca664-117">Parametro del protocollo</span><span class="sxs-lookup"><span data-stu-id="ca664-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="ca664-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="ca664-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="ca664-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="ca664-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="ca664-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="ca664-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="ca664-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="ca664-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="ca664-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="ca664-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="ca664-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="ca664-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="ca664-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="ca664-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="ca664-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="ca664-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="ca664-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="ca664-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="ca664-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="ca664-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="ca664-128">Migrazione di un'app di dispositivo da tooMQTT AMQP</span><span class="sxs-lookup"><span data-stu-id="ca664-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="ca664-129">Se si utilizza hello [dispositivo SDK][lnk-device-sdks], il passaggio da Usa AMQP tooMQTT, è necessario modificare il parametro di protocollo hello nell'inizializzazione del client hello come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ca664-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="ca664-130">In tal caso, verificare che hello toocheck seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ca664-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="ca664-131">AMQP restituisce gli errori per diverse condizioni, mentre MQTT termina la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="ca664-132">Di conseguenza, la logica di gestione delle eccezioni potrebbe richiedere alcune modifiche.</span><span class="sxs-lookup"><span data-stu-id="ca664-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="ca664-133">Non supporta hello MQTT *rifiutare* operazioni durante la ricezione [messaggi da cloud a dispositivo][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="ca664-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="ca664-134">Se l'app back-end deve tooreceive una risposta da app per dispositivi hello, è consigliabile utilizzare [diretta metodi][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="ca664-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="ca664-135">Protocollo hello MQTT direttamente</span><span class="sxs-lookup"><span data-stu-id="ca664-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="ca664-136">Se un dispositivo non è possibile usare il dispositivo di hello SDK, è possibile connettersi ancora gli endpoint pubblici dispositivo toohello protocollo MQTT hello sulla porta 8883.</span><span class="sxs-lookup"><span data-stu-id="ca664-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="ca664-137">In hello **CONNETTI** dispositivo hello pacchetto deve utilizzare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="ca664-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="ca664-138">Per hello **ClientId** campo, utilizzare hello **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="ca664-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="ca664-139">Per hello **Username** campo, utilizzare `{iothubhostname}/{device_id}/api-version=2016-11-14`, dove {iothubhostname} è hello CName completo dell'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="ca664-140">Ad esempio, se hello nome dell'hub IoT è **contoso.azure devices.net** e nome hello del dispositivo è **MyDevice01**, hello completo **Username** campo deve contenere `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="ca664-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="ca664-141">Per hello **Password** campo, utilizzare un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="ca664-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="ca664-142">formato Hello del token di firma di accesso condiviso è hello hello stesso per entrambi hello HTTP e protocolli AMQP:</span><span class="sxs-lookup"><span data-stu-id="ca664-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="ca664-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="ca664-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="ca664-144">Per ulteriori informazioni su come toogenerate i token di firma di accesso condiviso, vedere la sezione di dispositivo di hello della [i token di sicurezza tramite l'IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="ca664-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="ca664-145">Durante il test, è inoltre possibile utilizzare hello [Esplora dispositivo] [ lnk-device-explorer] tooquickly strumento generare un token di firma di accesso condiviso che è possibile copiare e incollare nel codice:</span><span class="sxs-lookup"><span data-stu-id="ca664-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="ca664-146">Passare toohello **Management** scheda **Esplora dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ca664-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="ca664-147">Fare clic su **SAS Token** in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="ca664-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="ca664-148">In **SASTokenForm**, selezionare il dispositivo in hello **DeviceID** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="ca664-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="ca664-149">Impostare il valore **TTL**.</span><span class="sxs-lookup"><span data-stu-id="ca664-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="ca664-150">Fare clic su **genera** toocreate il token.</span><span class="sxs-lookup"><span data-stu-id="ca664-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="ca664-151">token di firma di accesso condiviso generata Hello ha questa struttura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="ca664-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="ca664-152">parte di questo token toouse come hello Hello **Password** è tooconnect campo utilizzando MQTT: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="ca664-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="ca664-153">Per MQTT connettere e disconnettere i pacchetti, IoT Hub genera un evento su hello **operazioni di monitoraggio** canale con informazioni aggiuntive che consentono di problemi di connettività tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="ca664-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="ca664-154">Invio di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="ca664-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="ca664-155">Dopo aver apportato una connessione ha esito positivo, un dispositivo può inviare messaggi tooIoT Hub utilizzando `devices/{device_id}/messages/events/` o `devices/{device_id}/messages/events/{property_bag}` come un **il nome dell'argomento**.</span><span class="sxs-lookup"><span data-stu-id="ca664-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="ca664-156">Hello `{property_bag}` elemento consente i messaggi di hello dispositivo toosend con proprietà aggiuntive in un formato con codifica url.</span><span class="sxs-lookup"><span data-stu-id="ca664-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="ca664-157">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ca664-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="ca664-158">Questo `{property_bag}` elemento Usa hello stessa codifica per le stringhe di query nel protocollo hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="ca664-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="ca664-159">app per dispositivi Hello inoltre è possibile utilizzare `devices/{device_id}/messages/events/{property_bag}` come hello **il nome dell'argomento verrà** toodefine *i messaggi di* toobe inoltrati come un messaggio di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="ca664-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="ca664-160">L'hub IoT non supporta i messaggi di QoS 2.</span><span class="sxs-lookup"><span data-stu-id="ca664-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="ca664-161">Se un'app dispositivo pubblica un messaggio con **QoS 2**, IoT Hub chiude la connessione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="ca664-162">L'hub IoT non rende persistenti i messaggi di mantenimento.</span><span class="sxs-lookup"><span data-stu-id="ca664-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="ca664-163">Se un dispositivo invia un messaggio con hello **MANTIENI** too1 impostato, l'IoT Hub aggiunge hello **x-opt-conserva** messaggio toohello di proprietà dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca664-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="ca664-164">In questo caso, anziché salvare in modo permanente hello mantenere messaggio, l'IoT Hub passa toohello back-end app.</span><span class="sxs-lookup"><span data-stu-id="ca664-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="ca664-165">L'hub IoT supporta solo una connessione MQTT attiva per ogni dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ca664-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="ca664-166">Qualsiasi nuova connessione MQTT per conto di hello lo stesso ID dispositivo provoca l'IoT Hub toodrop hello esistente.</span><span class="sxs-lookup"><span data-stu-id="ca664-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="ca664-167">Per altre informazioni, vedere [Guida per gli sviluppatori sulla messaggistica][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="ca664-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="ca664-168">Ricezione di messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="ca664-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="ca664-169">i messaggi tooreceive dall'IoT Hub, un dispositivo deve eseguire la sottoscrizione con `devices/{device_id}/messages/devicebound/#` come un **filtro argomento**.</span><span class="sxs-lookup"><span data-stu-id="ca664-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="ca664-170">carattere jolly a più livelli di Hello  **#**  in hello argomento filtro viene utilizzato solo tooallow hello proprietà aggiuntive del dispositivo tooreceive nel nome di argomento hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="ca664-171">IoT Hub non consente l'utilizzo di hello di hello  **#**  o **?**</span><span class="sxs-lookup"><span data-stu-id="ca664-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="ca664-172">per il filtro di argomenti secondari.</span><span class="sxs-lookup"><span data-stu-id="ca664-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="ca664-173">Poiché l'IoT Hub non è un broker di messaggistica di pubblicazione-sottoscrizione generale, supporta solo nomi di argomento hello documentato e filtri di argomento.</span><span class="sxs-lookup"><span data-stu-id="ca664-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="ca664-174">Hello dispositivo non ricevere messaggi dall'IoT Hub, fino a quando non completata che ha sottoscritto endpoint specifico del dispositivo tooits, rappresentato da hello `devices/{device_id}/messages/devicebound/#` filtro argomento.</span><span class="sxs-lookup"><span data-stu-id="ca664-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="ca664-175">Dopo aver stabilito sottoscrizione ha esito positivo, il dispositivo di hello avvia la ricezione dei messaggi solo cloud a dispositivo che sono stati inviati tooit volta hello di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="ca664-176">Se si connette il dispositivo hello con **CleanSession** flag impostato troppo**0**, sottoscrizione hello viene mantenuto tra sessioni diverse.</span><span class="sxs-lookup"><span data-stu-id="ca664-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="ca664-177">In questo caso, hello alla successiva connessione con **CleanSession 0** dispositivo hello riceve messaggi in sospeso che sono stati inviati tooit mentre è stato disconnesso.</span><span class="sxs-lookup"><span data-stu-id="ca664-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="ca664-178">Se il dispositivo hello Usa **CleanSession** flag impostato troppo**1** , tuttavia, non riceve i messaggi dall'IoT Hub fino a quando non sottoscrive tooits dispositivo endpoint.</span><span class="sxs-lookup"><span data-stu-id="ca664-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="ca664-179">IoT Hub recapita i messaggi con hello **il nome dell'argomento** `devices/{device_id}/messages/devicebound/`, o `devices/{device_id}/messages/devicebound/{property_bag}` se sono presenti eventuali proprietà di messaggio.</span><span class="sxs-lookup"><span data-stu-id="ca664-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="ca664-180">`{property_bag}` contiene coppie chiave/valore con codifica URL di proprietà dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="ca664-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="ca664-181">Solo le proprietà dell'applicazione e le proprietà di sistema definibile dall'utente (ad esempio **messageId** o **correlationId**) sono inclusi nel contenitore delle proprietà di hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="ca664-182">I nomi di proprietà di sistema hanno prefisso hello  **$** , le proprietà dell'applicazione utilizzano hello nome della proprietà originale senza il prefisso.</span><span class="sxs-lookup"><span data-stu-id="ca664-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="ca664-183">Quando un'app dispositivo sottoscrive argomento tooa con **QoS 2**, IoT Hub concede massima QoS livello 1 in hello **SUBACK** pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ca664-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="ca664-184">Successivamente, l'IoT Hub recapita dispositivo toohello messaggi con QoS 1.</span><span class="sxs-lookup"><span data-stu-id="ca664-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="ca664-185">Recupero delle proprietà dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="ca664-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="ca664-186">Innanzitutto, un dispositivo sottoscrive troppo`$iothub/twin/res/#`, le risposte dell'operazione di tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="ca664-187">Quindi, invia un messaggio vuoto di tootopic `$iothub/twin/GET/?$rid={request id}`, con un valore popolato per **id richiesta**. servizio hello invia un messaggio di risposta contenente i dati di un doppio dispositivo hello in argomento `$iothub/twin/res/{status}/?$rid={request id}`, utilizzando hello stesso  **id richiesta** come richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="ca664-188">L'ID richiesta può essere qualsiasi valore valido per la proprietà di un messaggio, come descritto nella [Guida per gli sviluppatori sulla messaggistica dell'hub IoT][lnk-messaging], e lo stato viene convalidato come valore intero.</span><span class="sxs-lookup"><span data-stu-id="ca664-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="ca664-189">corpo della risposta Hello contiene sezione proprietà hello doppi dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="ca664-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="ca664-190">corpo Hello della voce del Registro di sistema di identità hello limitata membro "proprietà" toohello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ca664-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

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

<span data-ttu-id="ca664-191">Hello codici di stato possibili sono:</span><span class="sxs-lookup"><span data-stu-id="ca664-191">hello possible status codes are:</span></span>

|<span data-ttu-id="ca664-192">Stato</span><span class="sxs-lookup"><span data-stu-id="ca664-192">Status</span></span> | <span data-ttu-id="ca664-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ca664-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="ca664-194">200</span><span class="sxs-lookup"><span data-stu-id="ca664-194">200</span></span> | <span data-ttu-id="ca664-195">Success</span><span class="sxs-lookup"><span data-stu-id="ca664-195">Success</span></span> |
| <span data-ttu-id="ca664-196">429</span><span class="sxs-lookup"><span data-stu-id="ca664-196">429</span></span> | <span data-ttu-id="ca664-197">Numero eccessivo di richieste (limitazione), come descritto in [Limitazione dell'hub IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="ca664-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="ca664-198">5**</span><span class="sxs-lookup"><span data-stu-id="ca664-198">5**</span></span> | <span data-ttu-id="ca664-199">Errori server</span><span class="sxs-lookup"><span data-stu-id="ca664-199">Server errors</span></span> |

<span data-ttu-id="ca664-200">Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ca664-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="ca664-201">Aggiornare le proprietà segnalate di un dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="ca664-201">Update device twin's reported properties</span></span>

<span data-ttu-id="ca664-202">Hello sequenza seguente descrive la modalità di aggiornamento hello in un dispositivo di proprietà in un doppio dispositivo hello nell'IoT Hub segnalato:</span><span class="sxs-lookup"><span data-stu-id="ca664-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="ca664-203">Un dispositivo deve prima sottoscrizione toohello `$iothub/twin/res/#` le risposte dell'operazione di argomento tooreceive hello dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ca664-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="ca664-204">Un dispositivo invia un messaggio che contiene hello dispositivo un doppio update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` argomento.</span><span class="sxs-lookup"><span data-stu-id="ca664-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="ca664-205">Questo messaggio include un valore **request id**.</span><span class="sxs-lookup"><span data-stu-id="ca664-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="ca664-206">Hello servizio, quindi invia un messaggio di risposta contenente hello nuovo valore ETag per la raccolta di proprietà riportato su un argomento di hello `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="ca664-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="ca664-207">Questo messaggio di risposta utilizza hello stesso **id richiesta** come richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="ca664-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="ca664-208">corpo del messaggio Hello richiesta contiene un documento JSON, che fornisce nuovi valori per le proprietà segnalate (nessuna altra proprietà o metadati possono essere modificato).</span><span class="sxs-lookup"><span data-stu-id="ca664-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="ca664-209">Ogni membro nel documento JSON hello aggiorna o aggiunta un membro corrispondente hello documento del hello dispositivo disponibilità di una copia.</span><span class="sxs-lookup"><span data-stu-id="ca664-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="ca664-210">Un membro è stato impostato troppo`null`, eliminazioni hello hello contenente l'oggetto membro.</span><span class="sxs-lookup"><span data-stu-id="ca664-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="ca664-211">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ca664-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="ca664-212">Hello codici di stato possibili sono:</span><span class="sxs-lookup"><span data-stu-id="ca664-212">hello possible status codes are:</span></span>

|<span data-ttu-id="ca664-213">Stato</span><span class="sxs-lookup"><span data-stu-id="ca664-213">Status</span></span> | <span data-ttu-id="ca664-214">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ca664-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="ca664-215">200</span><span class="sxs-lookup"><span data-stu-id="ca664-215">200</span></span> | <span data-ttu-id="ca664-216">Success</span><span class="sxs-lookup"><span data-stu-id="ca664-216">Success</span></span> |
| <span data-ttu-id="ca664-217">400</span><span class="sxs-lookup"><span data-stu-id="ca664-217">400</span></span> | <span data-ttu-id="ca664-218">Richiesta non valida.</span><span class="sxs-lookup"><span data-stu-id="ca664-218">Bad Request.</span></span> <span data-ttu-id="ca664-219">JSON non valido</span><span class="sxs-lookup"><span data-stu-id="ca664-219">Malformed JSON</span></span> |
| <span data-ttu-id="ca664-220">429</span><span class="sxs-lookup"><span data-stu-id="ca664-220">429</span></span> | <span data-ttu-id="ca664-221">Numero eccessivo di richieste (limitazione), come descritto in [Limitazione dell'hub IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="ca664-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="ca664-222">5**</span><span class="sxs-lookup"><span data-stu-id="ca664-222">5**</span></span> | <span data-ttu-id="ca664-223">Errori server</span><span class="sxs-lookup"><span data-stu-id="ca664-223">Server errors</span></span> |

<span data-ttu-id="ca664-224">Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ca664-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="ca664-225">Ricezione delle notifiche di aggiornamento delle proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="ca664-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="ca664-226">Quando è connesso un dispositivo, l'IoT Hub invia argomento toohello notifiche `$iothub/twin/PATCH/properties/desired/?$version={new version}`, che includono il contenuto di hello di hello aggiornamento eseguita dal back-end di hello soluzione.</span><span class="sxs-lookup"><span data-stu-id="ca664-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="ca664-227">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ca664-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="ca664-228">Come per gli aggiornamenti delle proprietà, `null` indica i valori che hello JSON dell'oggetto membro eliminato.</span><span class="sxs-lookup"><span data-stu-id="ca664-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="ca664-229">L'hub IoT genera notifiche di modifica solo quando i dispositivi sono connessi.</span><span class="sxs-lookup"><span data-stu-id="ca664-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="ca664-230">Verificare che hello tooimplement [flusso riconnessione dispositivo] [ lnk-devguide-twin-reconnection] tookeep hello desiderato la sincronizzazione tra l'IoT Hub e hello app per dispositivi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="ca664-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="ca664-231">Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ca664-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="ca664-232">Rispondere tooa dirette del metodo</span><span class="sxs-lookup"><span data-stu-id="ca664-232">Respond tooa direct method</span></span>

<span data-ttu-id="ca664-233">Innanzitutto, un dispositivo ha toosubscribe troppo`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="ca664-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="ca664-234">IoT Hub invia l'argomento del metodo richieste toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, con un corpo vuoto o un JSON valido.</span><span class="sxs-lookup"><span data-stu-id="ca664-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="ca664-235">toorespond, dispositivo hello invia un messaggio con un JSON valido o di un corpo vuoto toohello argomento `$iothub/methods/res/{status}/?$rid={request id}`, dove **id richiesta** è toomatch hello uno nel messaggio di richiesta, hello e **stato** ha toobe un numero intero .</span><span class="sxs-lookup"><span data-stu-id="ca664-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="ca664-236">Per altre informazioni, vedere la [Guida per gli sviluppatori sui metodi diretti][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="ca664-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="ca664-237">Considerazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ca664-237">Additional considerations</span></span>

<span data-ttu-id="ca664-238">In considerazione finale, se è necessario comportamento del protocollo MQTT hello toocustomize sul lato cloud hello, è necessario rivedere hello [gateway del protocollo Azure IoT] [ lnk-azure-protocol-gateway] che consente ad alte prestazioni toodeploy gateway di protocollo personalizzato che interagisce direttamente con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ca664-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="ca664-239">gateway del protocollo Hello Azure IoT consente di toocustomize hello dispositivo protocollo tooaccommodate brownfield MQTT le distribuzioni o altri protocolli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="ca664-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="ca664-240">Questo approccio richiede tuttavia l'esecuzione e la gestione di un gateway di protocollo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="ca664-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca664-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ca664-241">Next steps</span></span>

<span data-ttu-id="ca664-242">toolearn ulteriori informazioni su protocollo MQTT hello, vedere hello [documentazione MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="ca664-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="ca664-243">toolearn ulteriori informazioni sulla pianificazione della distribuzione di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="ca664-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="ca664-244">[Catalogo dei dispositivi Azure Certified per IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="ca664-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="ca664-245">[Supportare protocolli aggiuntivi][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="ca664-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="ca664-246">[Eseguire il confronto con Hub eventi][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="ca664-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="ca664-247">[Scalabilità, disponibilità elevata e ripristino di emergenza][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="ca664-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="ca664-248">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="ca664-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ca664-249">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="ca664-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="ca664-250">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ca664-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
