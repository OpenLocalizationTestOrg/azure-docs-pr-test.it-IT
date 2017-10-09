## <a name="create-a-device-identity"></a><span data-ttu-id="d1275-101">Creare un'identità del dispositivo</span><span class="sxs-lookup"><span data-stu-id="d1275-101">Create a device identity</span></span>
<span data-ttu-id="d1275-102">In questa sezione si crea un'applicazione console .NET che crea un'identità del dispositivo nel Registro di sistema di hello identità nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d1275-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="d1275-103">Un dispositivo non può connettersi tooIoT hub, a meno che non sia presente una voce nel Registro di sistema di hello identità.</span><span class="sxs-lookup"><span data-stu-id="d1275-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="d1275-104">Per ulteriori informazioni, vedere sezione "Registro di sistema di identità" hello hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d1275-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d1275-105">Quando si esegue questa app console, viene generato un ID univoco del dispositivo e chiave che il dispositivo può usare tooidentify stesso quando vengono inviati al dispositivo a cloud messaggi tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d1275-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="d1275-106">Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="d1275-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="d1275-107">In Visual Studio, aggiungere una nuova soluzione tooa progetto Visual c# Windows Desktop classico utilizzando hello **applicazione Console (.NET Framework)** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="d1275-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d1275-108">Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d1275-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d1275-109">Progetto hello nome **CreateDeviceIdentity** e nome hello soluzione **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="d1275-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][10]
2. <span data-ttu-id="d1275-111">In Esplora soluzioni fare doppio clic su hello **CreateDeviceIdentity** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d1275-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="d1275-112">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="d1275-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="d1275-113">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="d1275-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][11]
4. <span data-ttu-id="d1275-115">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="d1275-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="d1275-116">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="d1275-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d1275-117">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="d1275-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="d1275-118">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="d1275-118">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    <span data-ttu-id="d1275-119">Questo metodo crea un'identità del dispositivo con ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="d1275-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="d1275-120">(Se tale ID dispositivo esiste già nel Registro di sistema identità hello, codice hello semplicemente recupera informazioni sul dispositivo esistente hello.) app Hello Visualizza chiave primaria di hello per tale identità.</span><span class="sxs-lookup"><span data-stu-id="d1275-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="d1275-121">Utilizzare questa chiave hello simulato dispositivo app tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d1275-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="d1275-122">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="d1275-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="d1275-123">Eseguire l'applicazione e prendere nota della chiave del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="d1275-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Chiave del dispositivo generati da un'applicazione hello][12]

> [!NOTE]
> <span data-ttu-id="d1275-125">Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="d1275-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="d1275-126">Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d1275-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="d1275-127">Se l'applicazione deve toostore altri metadati specifici del dispositivo, deve utilizzare un archivio specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d1275-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="d1275-128">Per altre informazioni, vedere la [Guida per gli sviluppatori dell'hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d1275-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
