## <a name="create-a-device-identity"></a><span data-ttu-id="36ee0-101">Creare un'identità del dispositivo</span><span class="sxs-lookup"><span data-stu-id="36ee0-101">Create a device identity</span></span>
<span data-ttu-id="36ee0-102">In questa sezione si scriverà un'app console .NET che crea un'identità del dispositivo nel registro delle identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36ee0-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="36ee0-103">Un dispositivo non può connettersi all'hub IoT a meno che non abbia una voce nel registro di identità.</span><span class="sxs-lookup"><span data-stu-id="36ee0-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="36ee0-104">Per altre informazioni, vedere la sezione "Registro di identità" della [Guida per gli sviluppatori dell'hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="36ee0-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="36ee0-105">Quando si esegue questa app console vengono generati un ID dispositivo univoco e una chiave con cui il dispositivo può identificarsi quando invia messaggi da dispositivo a cloud all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36ee0-105">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="36ee0-106">Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="36ee0-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="36ee0-107">In Visual Studio aggiungere un progetto desktop classico di Windows Visual C# a una nuova soluzione usando il modello di progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="36ee0-107">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="36ee0-108">Verificare che la versione di .NET Framework sia 4.5.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="36ee0-108">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="36ee0-109">Denominare il progetto **CreateDeviceIdentity** e denominare la soluzione **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="36ee0-109">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][10]
2. <span data-ttu-id="36ee0-111">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **CreateDeviceIdentity** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="36ee0-111">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="36ee0-112">Nella finestra **Gestione pacchetti NuGet** selezionare **Esplora**, cercare **microsoft.azure.devices**, selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="36ee0-112">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="36ee0-113">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="36ee0-113">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][11]
4. <span data-ttu-id="36ee0-115">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="36ee0-115">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="36ee0-116">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="36ee0-116">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="36ee0-117">Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="36ee0-117">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="36ee0-118">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="36ee0-118">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="36ee0-119">Questo metodo crea un'identità del dispositivo con ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="36ee0-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="36ee0-120">Se questo ID dispositivo è già disponibile nel registro delle identità, il codice recupera semplicemente le informazioni sul dispositivo esistenti. L'app visualizzerà quindi la chiave primaria per l'identità.</span><span class="sxs-lookup"><span data-stu-id="36ee0-120">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="36ee0-121">Questa chiave verrà usata dall'app per dispositivo simulato per connettersi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36ee0-121">You use this key in the simulated device app to connect to your IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="36ee0-122">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="36ee0-122">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="36ee0-123">Eseguire l'applicazione e prendere nota della chiave del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ee0-123">Run this application, and make a note of the device key.</span></span>
   
    ![Chiave del dispositivo generata dall'applicazione][12]

> [!NOTE]
> <span data-ttu-id="36ee0-125">Il registro di identità dell'hub IoT archivia solo le identità del dispositivo per abilitare l'accesso sicuro all'hub.</span><span class="sxs-lookup"><span data-stu-id="36ee0-125">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="36ee0-126">Archivia gli ID dispositivo e le chiavi da usare come credenziali di sicurezza e un flag di attivazione/disattivazione che consente di disabilitare l'accesso per un singolo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ee0-126">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="36ee0-127">Se l'applicazione deve archiviare altri metadati specifici del dispositivo, dovrà usare un archivio specifico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36ee0-127">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="36ee0-128">Per altre informazioni, vedere la [Guida per gli sviluppatori dell'hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="36ee0-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
