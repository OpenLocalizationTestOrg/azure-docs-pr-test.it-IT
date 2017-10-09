## <a name="create-a-device-identity"></a><span data-ttu-id="56741-101">Creare un'identità del dispositivo</span><span class="sxs-lookup"><span data-stu-id="56741-101">Create a device identity</span></span>

<span data-ttu-id="56741-102">In questa sezione, utilizzare uno strumento di Node.js denominato [l'hub IOT Esplora] [ iot-hub-explorer] toocreate un'identità del dispositivo per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="56741-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="56741-103">Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="56741-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="56741-104">Eseguire hello nell'ambiente della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="56741-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="56741-105">Eseguire quindi hello hub tooyour toologin di comando seguente.</span><span class="sxs-lookup"><span data-stu-id="56741-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="56741-106">Substitute `{iot hub connection string}` con hello stringa di connessione IoT Hub è stato copiato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="56741-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="56741-107">Infine, creare una nuova identità dispositivo chiamata `myDeviceId` con il comando hello:</span><span class="sxs-lookup"><span data-stu-id="56741-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="56741-108">Prendere nota della stringa di connessione dispositivo hello dal risultato hello.</span><span class="sxs-lookup"><span data-stu-id="56741-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="56741-109">Questa stringa di connessione del dispositivo viene utilizzata da hello dispositivo app tooconnect tooyour IoT Hub come un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="56741-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="56741-110">Fare riferimento troppo[introduzione con l'IoT Hub] [ lnk-getstarted] tooprogrammatically creare le identità del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="56741-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
