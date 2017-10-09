## <a name="create-a-device-identity"></a>Creare un'identità del dispositivo

In questa sezione, utilizzare uno strumento di Node.js denominato [l'hub IOT Esplora] [ iot-hub-explorer] toocreate un'identità del dispositivo per questa esercitazione. Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.

1. Eseguire hello nell'ambiente della riga di comando:

    `npm install -g iothub-explorer@latest`

1. Eseguire quindi hello hub tooyour toologin di comando seguente. Substitute `{iot hub connection string}` con hello stringa di connessione IoT Hub è stato copiato in precedenza:

    `iothub-explorer login "{iot hub connection string}"`

1. Infine, creare una nuova identità dispositivo chiamata `myDeviceId` con il comando hello:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Prendere nota della stringa di connessione dispositivo hello dal risultato hello. Questa stringa di connessione del dispositivo viene utilizzata da hello dispositivo app tooconnect tooyour IoT Hub come un dispositivo.

![][img-identity]

Fare riferimento troppo[introduzione con l'IoT Hub] [ lnk-getstarted] tooprogrammatically creare le identità del dispositivo.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
