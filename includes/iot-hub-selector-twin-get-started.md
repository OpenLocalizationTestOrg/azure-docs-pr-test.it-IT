> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

I dispositivi gemelli sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni). IoT Hub persiste doppi un dispositivo per ogni dispositivo che si connette tooit.

Usare i dispositivi gemelli per:

* Archiviare i metadati dei dispositivi dal back-end della soluzione.
* Report informazioni sullo stato corrente, ad esempio le funzionalità disponibili e le condizioni (ad esempio, la connettività metodo hello usato) dall'app del dispositivo.
* Sincronizzazione dello stato di hello dei flussi di lavoro di lunga durata (ad esempio aggiornamenti firmware e la configurazione) tra un'app del dispositivo e un'applicazione back-end.
* Eseguire query sui metadati, la configurazione o lo stato dei dispositivi.

> [!NOTE]
> I dispositivi gemelli sono progettati per la sincronizzazione e per l'esecuzione di query sulle configurazioni e le condizioni dei dispositivi. Ulteriori informazioni sulle quando gemelli dispositivo toouse sono reperibile [comprendere gemelli dispositivo][lnk-twins].

I dispositivi gemelli vengono archiviati in un hub IoT e contengono gli elementi seguenti.

* *tag*, accessibili solo dal back-end soluzione hello; metadati del dispositivo
* *le proprietà desiderate*, oggetti JSON modificabili dalla soluzione hello indietro end e observable tramite app per dispositivi hello; e
* *proprietà segnalati*, oggetti JSON modificabili per app per dispositivi hello e leggibili dal back-end di hello soluzione. I tag e le proprietà non possono contenere matrici, ma gli oggetti possono essere annidati.

![][img-twin]

Inoltre, è possibile eseguire hello soluzione back-end query gemelli di dispositivo in base a tutti hello di sopra dei dati.
Fare riferimento troppo[comprendere gemelli dispositivo] [ lnk-twins] per ulteriori informazioni su gemelli di dispositivo e toohello [il linguaggio di query di IoT Hub] [ lnk-query] riferimento Per eseguire una query.

> [!NOTE]
> A questo punto, sono accessibili solo da dispositivi che si connettono tooIoT Hub gemelli di dispositivo utilizzando il protocollo MQTT hello. Consultare toohello [supporto MQTT] [ lnk-devguide-mqtt] per istruzioni su come tooconvert esistente dispositivo app toouse MQTT.

Questa esercitazione illustra come:

* Creare un'applicazione back-end che aggiunge *tag* tooa gemelli di dispositivo e un'app per dispositivo simulato che segnala la connettività del canale come un *segnalati proprietà* in un doppio dispositivo hello.
* Eseguire una query dispositivi dall'app back-end utilizzando i filtri tag hello e proprietà creata in precedenza.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md