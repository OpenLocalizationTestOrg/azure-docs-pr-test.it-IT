## <a name="create-a-simulated-device-app"></a><span data-ttu-id="4e317-101">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="4e317-101">Create a simulated device app</span></span>
<span data-ttu-id="4e317-102">In questa sezione verrà illustrato come:</span><span class="sxs-lookup"><span data-stu-id="4e317-102">In this section, you:</span></span>

* <span data-ttu-id="4e317-103">Creare un'app console Node.js che risponde a un metodo diretto chiamato dal cloud</span><span class="sxs-lookup"><span data-stu-id="4e317-103">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="4e317-104">Attivare un aggiornamento del firmware simulato</span><span class="sxs-lookup"><span data-stu-id="4e317-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="4e317-105">Usare le proprietà segnalate per abilitare le query nei dispositivi gemelli in modo da identificare i dispositivi e l'ora dell'ultimo completamento di un aggiornamento del firmware</span><span class="sxs-lookup"><span data-stu-id="4e317-105">Use the reported properties to enable device twin queries to identify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="4e317-106">Passaggio 1: creare una cartella vuota denominata **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="4e317-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="4e317-107">Nella cartella **manageddevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4e317-107">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="4e317-108">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="4e317-108">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="4e317-109">Passaggio 2: eseguire questo comando al prompt dei comandi nella cartella **manageddevice** per installare i pacchetti SDK per dispositivi **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="4e317-109">Step 2: At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="4e317-110">Passaggio 3: con un editor di testo creare un file **dmpatterns_fwupdate_device.js** nella cartella **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="4e317-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in the **manageddevice** folder.</span></span>

<span data-ttu-id="4e317-111">Passaggio 4: aggiungere le istruzioni "require" seguenti all'inizio del file **dmpatterns_fwupdate_device.js**:</span><span class="sxs-lookup"><span data-stu-id="4e317-111">Step 4: Add the following 'require' statements at the start of the **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="4e317-112">Passaggio 5: aggiungere una variabile **connectionString** e usarla per creare un'istanza **Client**.</span><span class="sxs-lookup"><span data-stu-id="4e317-112">Step 5: Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="4e317-113">Sostituire il segnaposto `{yourdeviceconnectionstring}` con la stringa di connessione di cui si è preso nota prima nella sezione "Create a device identity" (Creare un'identità del dispositivo):</span><span class="sxs-lookup"><span data-stu-id="4e317-113">Replace the `{yourdeviceconnectionstring}` placeholder with the connection string you previously made a note of in the "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="4e317-114">Passaggio 6: aggiungere la funzione seguente che viene usata per aggiornare le proprietà segnalate:</span><span class="sxs-lookup"><span data-stu-id="4e317-114">Step 6: Add the following function that is used to update reported properties:</span></span>
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

<span data-ttu-id="4e317-115">Passaggio 7: aggiungere le funzioni seguenti che simulano il download e l'applicazione dell'immagine del firmware:</span><span class="sxs-lookup"><span data-stu-id="4e317-115">Step 7: Add the following functions that simulate downloading and applying the firmware image:</span></span>
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

<span data-ttu-id="4e317-116">Passaggio 8: aggiungere la funzione seguente che imposta lo stato di aggiornamento del firmware tramite le proprietà segnalate su **waiting**.</span><span class="sxs-lookup"><span data-stu-id="4e317-116">Step 8: Add the following function that updates the firmware update status through the reported properties to **waiting**.</span></span> <span data-ttu-id="4e317-117">In genere i dispositivi vengono informati che è disponibile un aggiornamento e i criteri definiti dall'amministratore fanno in modo che il dispositivo avvii il download e applichi l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4e317-117">Typically, devices are informed of an available update and an administrator defined policy causes the device to start downloading and applying the update.</span></span> <span data-ttu-id="4e317-118">In questa funzione viene eseguita la logica per abilitare tali criteri.</span><span class="sxs-lookup"><span data-stu-id="4e317-118">This function is where the logic to enable that policy should run.</span></span> <span data-ttu-id="4e317-119">Per semplicità, l'esempio attende quattro secondi prima di procedere al download dell'immagine del firmware:</span><span class="sxs-lookup"><span data-stu-id="4e317-119">For simplicity, the sample waits for four seconds before proceeding to download the firmware image:</span></span>
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

<span data-ttu-id="4e317-120">Passaggio 9: aggiungere la funzione seguente che imposta lo stato di aggiornamento del firmware tramite le proprietà segnalate su **downloading**.</span><span class="sxs-lookup"><span data-stu-id="4e317-120">Step 9: Add the following function that updates the firmware update status through the reported properties to **downloading**.</span></span> <span data-ttu-id="4e317-121">La funzione simula quindi un download del firmware e infine imposta lo stato di aggiornamento del firmware su **downloadFailed** o su **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="4e317-121">The function then simulates a firmware download and finally updates the firmware update status to either **downloadFailed** or **downloadComplete**:</span></span>
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

<span data-ttu-id="4e317-122">Passaggio 10: aggiungere la funzione seguente che imposta lo stato di aggiornamento del firmware tramite le proprietà segnalate su **applying**.</span><span class="sxs-lookup"><span data-stu-id="4e317-122">Step 10: Add the following function that updates the firmware update status through the reported properties to **applying**.</span></span> <span data-ttu-id="4e317-123">La funzione simula quindi l'applicazione dell'immagine del firmware e infine imposta lo stato di aggiornamento del firmware su **applyFailed** o su **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="4e317-123">The function then simulates applying the firmware image and finally updates the firmware update status to either **applyFailed** or **applyComplete**:</span></span>
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

<span data-ttu-id="4e317-124">Passaggio 11: aggiungere la funzione seguente che gestisce il metodo diretto **firmwareUpdate** e avvia il processo di aggiornamento del firmware in più fasi:</span><span class="sxs-lookup"><span data-stu-id="4e317-124">Step 11: Add the following function that handles the **firmwareUpdate** direct method and initiates the multi-stage firmware update process:</span></span>
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond the cloud app for the direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response to method \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get the parameter from the body of the method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain the device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start the multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

<span data-ttu-id="4e317-125">Passaggio 12: aggiungere infine il codice seguente che effettua la connessione all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="4e317-125">Step 12: Finally, add the following code that connects to your IoT hub:</span></span>
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect to IotHub client');
      }  else {
        console.log('Client connected to IoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> <span data-ttu-id="4e317-126">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="4e317-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4e317-127">Nel codice di produzione è consigliabile implementare criteri per i tentativi, ad esempio un backoff esponenziale, come illustrato nell'articolo di MSDN [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx) (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="4e317-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 