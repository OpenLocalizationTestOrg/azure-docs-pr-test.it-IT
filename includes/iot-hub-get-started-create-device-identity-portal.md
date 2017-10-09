## <a name="create-a-device-identity"></a><span data-ttu-id="99fe7-101">Creare un'identità del dispositivo</span><span class="sxs-lookup"><span data-stu-id="99fe7-101">Create a device identity</span></span>

<span data-ttu-id="99fe7-102">In questa sezione utilizzare hello [portale di Azure] [ lnk-azure-portal] toocreate un'identità del dispositivo nel Registro di sistema di hello identità nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="99fe7-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="99fe7-103">Un dispositivo non può connettersi tooIoT hub, a meno che non sia presente una voce nel Registro di sistema di hello identità.</span><span class="sxs-lookup"><span data-stu-id="99fe7-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="99fe7-104">Per ulteriori informazioni, vedere sezione "Registro di sistema di identità" hello hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="99fe7-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="99fe7-105">Hello **Esplora dispositivo** in hello portale consente di generare un ID univoco del dispositivo e una chiave che il dispositivo può usare tooidentify stesso quando si connette tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="99fe7-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="99fe7-106">Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="99fe7-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="99fe7-107">Assicurarsi che si è connessi toohello [portale di Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="99fe7-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="99fe7-108">In hello Jumpbar, fare clic su **tutte le risorse** e trovare la risorsa di hub IoT.</span><span class="sxs-lookup"><span data-stu-id="99fe7-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Passare l'hub Iot tooyour][img-find-iothub]

1. <span data-ttu-id="99fe7-110">Quando la risorsa di hub IoT è aperto, fare clic su hello **Esplora dispositivo** strumento e quindi fare clic su **Aggiungi** nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="99fe7-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="99fe7-111">Specificare il nome di hello per il nuovo dispositivo, ad esempio **myDeviceId**, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="99fe7-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Creare l'identità del dispositivo nel portale][img-create-device]

   <span data-ttu-id="99fe7-113">In questo modo viene creata una nuova identità del dispositivo per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="99fe7-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="99fe7-114">In hello **Esplora dispositivo**dell'elenco dei dispositivi, fare clic su dispositivo hello appena creato e prendere nota della hello **stringa di connessione---chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="99fe7-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Stringa di connessione del dispositivo][img-connection-string]

> [!NOTE]
> <span data-ttu-id="99fe7-116">Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="99fe7-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="99fe7-117">Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="99fe7-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="99fe7-118">Se l'applicazione deve toostore altri metadati specifici del dispositivo, deve utilizzare un archivio specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="99fe7-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="99fe7-119">Per altre informazioni, vedere la [Guida per gli sviluppatori dell'hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="99fe7-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

