## <a name="specify-hello-behavior-of-hello-iot-device"></a><span data-ttu-id="c4b4d-101">Specificare il comportamento del dispositivo IoT hello hello</span><span class="sxs-lookup"><span data-stu-id="c4b4d-101">Specify hello behavior of hello IoT device</span></span>

<span data-ttu-id="c4b4d-102">libreria client di IoT Hub serializzatore Hello Usa il formato del modello toospecify hello scambi di hello messaggi hello dispositivo con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-102">hello IoT Hub serializer client library uses a model toospecify hello format of hello messages hello device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="c4b4d-103">Aggiungere hello dopo le dichiarazioni delle variabili dopo hello `#include` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-103">Add hello following variable declarations after hello `#include` statements.</span></span> <span data-ttu-id="c4b4d-104">Sostituire i valori segnaposto hello [Id dispositivo] e [dispositivo Key] con i valori che si è preso nota per il dispositivo in hello remoto soluzione di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-104">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="c4b4d-105">Utilizzare hello Hostname Hub IoT da hello soluzione dashboard tooreplace [hub IOT Name].</span><span class="sxs-lookup"><span data-stu-id="c4b4d-105">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="c4b4d-106">Ad esempio, se il nome host dell'hub IoT è **contoso.azure-devices.net**, sostituire [Nome IoTHub] con **contoso**:</span><span class="sxs-lookup"><span data-stu-id="c4b4d-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="c4b4d-107">Aggiungere codice toodefine hello modello che consente di hello dispositivo toocommunicate con l'IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-107">Add hello following code toodefine hello model that enables hello device toocommunicate with IoT Hub.</span></span> <span data-ttu-id="c4b4d-108">Questo modello consente di specificare che il dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="c4b4d-108">This model specifies that hello device:</span></span>

   - <span data-ttu-id="c4b4d-109">Può inviare temperatura, temperatura esterna, umidità e un ID dispositivo come dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="c4b4d-110">Può inviare i metadati relativi a hello dispositivo tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-110">Can send metadata about hello device tooIoT Hub.</span></span> <span data-ttu-id="c4b4d-111">dispositivo Hello invia i metadati di base in un **DeviceInfo** oggetto all'avvio.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-111">hello device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="c4b4d-112">Può inviare segnalate proprietà, un doppio dispositivo toohello nell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-112">Can send reported properties, toohello device twin in IoT Hub.</span></span> <span data-ttu-id="c4b4d-113">Queste proprietà segnalate sono raggruppate in proprietà di configurazione, dispositivo e di sistema.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="c4b4d-114">Può ricevere e agire su desiderato impostate in un doppio dispositivo hello nell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-114">Can receive and act on desired properties set in hello device twin in IoT Hub.</span></span>
   - <span data-ttu-id="c4b4d-115">Può rispondere toohello **riavviare** e **InitiateFirmwareUpdate** indirizzare i metodi richiamati tramite il portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-115">Can respond toohello **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through hello solution portal.</span></span> <span data-ttu-id="c4b4d-116">dispositivo Hello invia le informazioni sui metodi di hello diretto supporta l'utilizzo di proprietà restituita.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-116">hello device sends information about hello direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define hello Model
    BEGIN_NAMESPACE(Contoso);

    /* Reported properties */
    DECLARE_STRUCT(SystemProperties,
      ascii_char_ptr, Manufacturer,
      ascii_char_ptr, FirmwareVersion,
      ascii_char_ptr, InstalledRAM,
      ascii_char_ptr, ModelNumber,
      ascii_char_ptr, Platform,
      ascii_char_ptr, Processor,
      ascii_char_ptr, SerialNumber
    );

    DECLARE_STRUCT(LocationProperties,
      double, Latitude,
      double, Longitude
    );

    DECLARE_STRUCT(ReportedDeviceProperties,
      ascii_char_ptr, DeviceState,
      LocationProperties, Location
    );

    DECLARE_MODEL(ConfigProperties,
      WITH_REPORTED_PROPERTY(double, TemperatureMeanValue),
      WITH_REPORTED_PROPERTY(uint8_t, TelemetryInterval)
    );

    /* Part of DeviceInfo */
    DECLARE_STRUCT(DeviceProperties,
      ascii_char_ptr, DeviceID,
      _Bool, HubEnabledState
    );

    DECLARE_DEVICETWIN_MODEL(Thermostat,
      /* Telemetry (temperature, external temperature and humidity) */
      WITH_DATA(double, Temperature),
      WITH_DATA(double, ExternalTemperature),
      WITH_DATA(double, Humidity),
      WITH_DATA(ascii_char_ptr, DeviceId),

      /* DeviceInfo */
      WITH_DATA(ascii_char_ptr, ObjectType),
      WITH_DATA(_Bool, IsSimulatedDevice),
      WITH_DATA(ascii_char_ptr, Version),
      WITH_DATA(DeviceProperties, DeviceProperties),

      /* Device twin properties */
      WITH_REPORTED_PROPERTY(ReportedDeviceProperties, Device),
      WITH_REPORTED_PROPERTY(ConfigProperties, Config),
      WITH_REPORTED_PROPERTY(SystemProperties, System),

      WITH_DESIRED_PROPERTY(double, TemperatureMeanValue, onDesiredTemperatureMeanValue),
      WITH_DESIRED_PROPERTY(uint8_t, TelemetryInterval, onDesiredTelemetryInterval),

      /* Direct methods implemented by hello device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-hello-behavior-of-hello-device"></a><span data-ttu-id="c4b4d-117">Implementare il comportamento di hello del dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="c4b4d-117">Implement hello behavior of hello device</span></span>
<span data-ttu-id="c4b4d-118">Aggiungere codice che implementa il comportamento di hello definito nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-118">Now add code that implements hello behavior defined in hello model.</span></span>

1. <span data-ttu-id="c4b4d-119">Aggiungere hello seguente di funzioni che gestiscono le proprietà desiderata hello impostate in dashboard soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-119">Add hello following functions that handle hello desired properties set in hello solution dashboard.</span></span> <span data-ttu-id="c4b4d-120">Queste proprietà desiderate sono definite nel modello di hello:</span><span class="sxs-lookup"><span data-stu-id="c4b4d-120">These desired properties are defined in hello model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="c4b4d-121">Aggiungere hello seguente di funzioni che gestiscono i metodi di diretto hello richiamati tramite l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-121">Add hello following functions that handle hello direct methods invoked through hello IoT hub.</span></span> <span data-ttu-id="c4b4d-122">Questi metodi diretti sono definiti nel modello di hello:</span><span class="sxs-lookup"><span data-stu-id="c4b4d-122">These direct methods are defined in hello model:</span></span>

    ```c
    /* Handlers for direct methods */
    METHODRETURN_HANDLE Reboot(Thermostat* thermostat)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Rebooting\"");
      printf("Received reboot request\r\n");
      return result;
    }

    METHODRETURN_HANDLE InitiateFirmwareUpdate(Thermostat* thermostat, ascii_char_ptr FwPackageURI)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Initiating Firmware Update\"");
      printf("Recieved firmware update request. Use package at: %s\r\n", FwPackageURI);
      return result;
    }
    ```

1. <span data-ttu-id="c4b4d-123">Aggiungere hello funzione che invia una soluzione di toohello preconfigurato messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="c4b4d-123">Add hello following function that sends a message toohello preconfigured solution:</span></span>
   
    ```c
    /* Send data tooIoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable toocreate a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted hello message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="c4b4d-124">Aggiungere hello gestore di callback che viene eseguito quando il dispositivo hello ha inviato i nuovi valori di proprietà restituito toohello preconfigurato soluzione seguente:</span><span class="sxs-lookup"><span data-stu-id="c4b4d-124">Add hello following callback handler that runs when hello device has sent new reported property values toohello preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="c4b4d-125">Aggiungere i seguenti hello funzionano tooconnect soluzione toohello preconfigurato dispositivo nel cloud hello e scambiano di dati.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-125">Add hello following function tooconnect your device toohello preconfigured solution in hello cloud, and exchange data.</span></span> <span data-ttu-id="c4b4d-126">Questa funzione esegue hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c4b4d-126">This function performs hello following steps:</span></span>

    - <span data-ttu-id="c4b4d-127">Inizializza la piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-127">Initializes hello platform.</span></span>
    - <span data-ttu-id="c4b4d-128">Registra lo spazio dei nomi di hello Contoso con libreria di serializzazione hello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-128">Registers hello Contoso namespace with hello serialization library.</span></span>
    - <span data-ttu-id="c4b4d-129">Inizializza i client hello con stringa di connessione dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-129">Initializes hello client with hello device connection string.</span></span>
    - <span data-ttu-id="c4b4d-130">Creare un'istanza di hello **termostato** modello.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-130">Create an instance of hello **Thermostat** model.</span></span>
    - <span data-ttu-id="c4b4d-131">Crea e invia i valori delle proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="c4b4d-132">Invia un oggetto **DeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="c4b4d-133">Crea una telemetria toosend ciclo ogni secondo.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-133">Creates a loop toosend telemetry every second.</span></span>
    - <span data-ttu-id="c4b4d-134">Deinizializza tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c4b4d-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed tooinitialize hello platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable tooSERIALIZER_REGISTER_NAMESPACE\n");
          }
          else
          {
            IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, MQTT_Protocol);
            if (iotHubClientHandle == NULL)
            {
              printf("Failure in IoTHubClient_CreateFromConnectionString\n");
            }
            else
            {
      #ifdef MBED_BUILD_TIMESTAMP
              // For mbed add hello certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed tooset option \"TrustedCerts\"\n");
              }
      #endif // MBED_BUILD_TIMESTAMP
              Thermostat* thermostat = IoTHubDeviceTwin_CreateThermostat(iotHubClientHandle);
              if (thermostat == NULL)
              {
                printf("Failure in IoTHubDeviceTwin_CreateThermostat\n");
              }
              else
              {
                /* Set values for reported properties */
                thermostat->Config.TemperatureMeanValue = 55.5;
                thermostat->Config.TelemetryInterval = 3;
                thermostat->Device.DeviceState = "normal";
                thermostat->Device.Location.Latitude = 47.642877;
                thermostat->Device.Location.Longitude = -122.125497;
                thermostat->System.Manufacturer = "Contoso Inc.";
                thermostat->System.FirmwareVersion = "2.22";
                thermostat->System.InstalledRAM = "8 MB";
                thermostat->System.ModelNumber = "DB-14";
                thermostat->System.Platform = "Plat 9.75";
                thermostat->System.Processor = "i3-7";
                thermostat->System.SerialNumber = "SER21";
                /* Specify hello signatures of hello supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot hello device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file\"}";

                /* Send reported properties tooIoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object tooIoT Hub at startup\n");
      
                  thermostat->ObjectType = "DeviceInfo";
                  thermostat->IsSimulatedDevice = 0;
                  thermostat->Version = "1.0";
                  thermostat->DeviceProperties.HubEnabledState = 1;
                  thermostat->DeviceProperties.DeviceID = (char*)deviceId;

                  unsigned char* buffer;
                  size_t bufferSize;

                  if (SERIALIZE(&buffer, &bufferSize, thermostat->ObjectType, thermostat->Version, thermostat->IsSimulatedDevice, thermostat->DeviceProperties) != CODEFIRST_OK)
                  {
                    (void)printf("Failed serializing DeviceInfo\n");
                  }
                  else
                  {
                    sendMessage(iotHubClientHandle, buffer, bufferSize);
                  }

                  /* Send telemetry */
                  thermostat->Temperature = 50;
                  thermostat->ExternalTemperature = 55;
                  thermostat->Humidity = 50;
                  thermostat->DeviceId = (char*)deviceId;

                  while (1)
                  {
                    unsigned char*buffer;
                    size_t bufferSize;

                    (void)printf("Sending sensor value Temperature = %f, Humidity = %f\n", thermostat->Temperature, thermostat->Humidity);

                    if (SERIALIZE(&buffer, &bufferSize, thermostat->DeviceId, thermostat->Temperature, thermostat->Humidity, thermostat->ExternalTemperature) != CODEFIRST_OK)
                    {
                      (void)printf("Failed sending sensor value\r\n");
                    }
                    else
                    {
                      sendMessage(iotHubClientHandle, buffer, bufferSize);
                    }

                    ThreadAPI_Sleep(1000);
                  }

                  IoTHubDeviceTwin_DestroyThermostat(thermostat);
                }
              }
              IoTHubClient_Destroy(iotHubClientHandle);
            }
            serializer_deinit();
          }
        }
        platform_deinit();
      }
    ```
   
    <span data-ttu-id="c4b4d-135">Per riferimento, di seguito è riportato un esempio **telemetria** toohello messaggio inviato preconfigurato soluzione:</span><span class="sxs-lookup"><span data-stu-id="c4b4d-135">For reference, here is a sample **Telemetry** message sent toohello preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```