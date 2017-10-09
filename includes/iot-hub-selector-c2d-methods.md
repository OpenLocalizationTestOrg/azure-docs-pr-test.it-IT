> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

L'hub IoT di Azure è un servizio completamente gestito che consente comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione. Esercitazioni precedenti ([iniziare con l'IoT Hub] e [inviare messaggi da Cloud a dispositivo con l'IoT Hub]) illustrare hello da dispositivo a cloud e cloud a dispositivo messaggistica funzionalità di base di IoT Hub. IoT Hub offre inoltre i metodi non durevoli tooinvoke possibilità sui dispositivi dal cloud hello hello. Indirizzare i metodi rappresentano un'interazione richiesta-risposta con un tooan simili dispositivi HTTP chiamare in quanto essi esito positivo o negativo (dopo un timeout specificato dall'utente) utente hello toolet conoscere lo stato di hello della chiamata di hello. [Richiamare un metodo diretto su un dispositivo] [ lnk-devguide-methods] vengono descritti i metodi diretti in modo più dettagliato e offre indicazioni su quando toouse diretta metodi anziché i messaggi da cloud a dispositivo o le proprietà desiderate.

Questa esercitazione illustra come:

* Utilizzare hello toocreate portale Azure un hub IoT e creare un'identità del dispositivo nell'hub IoT.
* Creare un'applicazione di dispositivo simulato che dispone di un metodo diretto, che può essere chiamato da cloud hello.
* Creare un'applicazione console che chiama un metodo diretto in app dispositivo simulato hello tramite l'hub IoT.

> [!NOTE]
> In questo momento, metodi diretti sono solo supportata nei dispositivi che si connettono tramite Hub tooIoT hello protocollo MQTT. Consultare toohello [supporto MQTT] [ lnk-devguide-mqtt] per istruzioni su come tooconvert esistente dispositivo app toouse MQTT.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[inviare messaggi da Cloud a dispositivo con l'IoT Hub]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[iniziare con l'IoT Hub]: ../articles/iot-hub/iot-hub-node-node-getstarted.md