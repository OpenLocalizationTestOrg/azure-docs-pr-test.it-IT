## <a name="create-a-device-identity"></a>Creare un'identità del dispositivo
In questa sezione si crea un'applicazione console .NET che crea un'identità del dispositivo nel Registro di sistema di hello identità nell'hub IoT. Un dispositivo non può connettersi tooIoT hub, a meno che non sia presente una voce nel Registro di sistema di hello identità. Per ulteriori informazioni, vedere sezione "Registro di sistema di identità" hello hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity]. Quando si esegue questa app console, viene generato un ID univoco del dispositivo e chiave che il dispositivo può usare tooidentify stesso quando vengono inviati al dispositivo a cloud messaggi tooIoT Hub. Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.

1. In Visual Studio, aggiungere una nuova soluzione tooa progetto Visual c# Windows Desktop classico utilizzando hello **applicazione Console (.NET Framework)** modello di progetto. Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive. Progetto hello nome **CreateDeviceIdentity** e nome hello soluzione **IoTHubGetStarted**.
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][10]
2. In Esplora soluzioni fare doppio clic su hello **CreateDeviceIdentity** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.
3. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.
   
    ![Finestra Gestione pacchetti NuGet][11]
4. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Aggiungere hello seguente metodo toohello **programma** classe:
   
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
   
    Questo metodo crea un'identità del dispositivo con ID **myFirstDevice**. (Se tale ID dispositivo esiste già nel Registro di sistema identità hello, codice hello semplicemente recupera informazioni sul dispositivo esistente hello.) app Hello Visualizza chiave primaria di hello per tale identità. Utilizzare questa chiave hello simulato dispositivo app tooconnect tooyour IoT hub.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Eseguire l'applicazione e prendere nota della chiave del dispositivo hello.
   
    ![Chiave del dispositivo generati da un'applicazione hello][12]

> [!NOTE]
> Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso. Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo. Se l'applicazione deve toostore altri metadati specifici del dispositivo, deve utilizzare un archivio specifici dell'applicazione. Per altre informazioni, vedere la [Guida per gli sviluppatori dell'hub IoT][lnk-devguide-identity].
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
