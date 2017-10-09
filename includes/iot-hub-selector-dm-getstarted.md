> [!div class="op_single_selector"]
> * [Dispositivo: Node.js Service: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Dispositivo: Node.js Service: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Dispositivo: Java Service: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Applicazioni back-end è possono utilizzare le primitive di IoT Hub di Azure, ad esempio [doppi dispositivo] [ lnk-devtwin] e [diretta metodi][lnk-c2dmethod], tooremotely avviare e monitorare azioni di gestione dispositivo nei dispositivi. In questa esercitazione Mostra come un'applicazione back-end e un'app per dispositivi possono collaborare tooinitiate e monitorare un IoT Hub utilizzando il riavvio del dispositivo remoto.

Usare le azioni di gestione dispositivo tooinitiate un metodo diretto (ad esempio il riavvio, impostazioni di fabbrica e aggiornamento del firmware) da un'applicazione back-end in cloud hello. dispositivo Hello è responsabile per:

* Gestione della richiesta del metodo hello inviata dall'IoT Hub.
* Avvio di azione specifici del dispositivo corrispondente hello sul dispositivo hello.
* Fornire gli aggiornamenti di stato tramite *segnalati proprietà* tooIoT Hub.

È possibile utilizzare un'applicazione back-end in hello cloud toorun dispositivo doppi query tooreport sullo stato di avanzamento hello delle azioni di gestione del dispositivo.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
