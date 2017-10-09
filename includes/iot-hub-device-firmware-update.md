## <a name="create-a-simulated-device-app"></a><span data-ttu-id="f5f42-101">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="f5f42-101">Create a simulated device app</span></span>
<span data-ttu-id="f5f42-102">In questa sezione verrà illustrato come:</span><span class="sxs-lookup"><span data-stu-id="f5f42-102">In this section, you:</span></span>

* <span data-ttu-id="f5f42-103">Creare un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello</span><span class="sxs-lookup"><span data-stu-id="f5f42-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="f5f42-104">Attivare un aggiornamento del firmware simulato</span><span class="sxs-lookup"><span data-stu-id="f5f42-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="f5f42-105">Hello utilizzare segnalati proprietà tooenable doppi query tooidentify dispositivi e quando sono completato un aggiornamento del firmware</span><span class="sxs-lookup"><span data-stu-id="f5f42-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="f5f42-106">Passaggio 1: creare una cartella vuota denominata **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="f5f42-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="f5f42-107">In hello **manageddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="f5f42-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f5f42-108">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="f5f42-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="f5f42-109">Passaggio 2: al prompt dei comandi in hello **manageddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** e **mqtt azure-iot-dispositivo** dispositivo Pacchetti SDK:</span><span class="sxs-lookup"><span data-stu-id="f5f42-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="f5f42-110">Passaggio 3: Usando un editor di testo, creare un **dmpatterns_fwupdate_device.js** file hello **manageddevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="f5f42-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="f5f42-111">Passaggio 4: Aggiungere seguente hello 'Richiedi' istruzioni all'inizio di hello di hello **dmpatterns_fwupdate_device.js** file:</span><span class="sxs-lookup"><span data-stu-id="f5f42-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="f5f42-112">Passaggio 5: Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.</span><span class="sxs-lookup"><span data-stu-id="f5f42-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="f5f42-113">Sostituire hello `{yourdeviceconnectionstring}` segnaposto con stringa di connessione hello effettuate in precedenza nota di sezione "Creare un'identità del dispositivo" hello in precedenza:</span><span class="sxs-lookup"><span data-stu-id="f5f42-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="f5f42-114">Passaggio 6: Aggiungere il seguente hello funzione che viene utilizzato tooupdate segnalati proprietà:</span><span class="sxs-lookup"><span data-stu-id="f5f42-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
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

<span data-ttu-id="f5f42-115">Passaggio 7: Aggiungere hello funzioni che simulano il download e l'applicazione hello firmware immagine seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5f42-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
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

<span data-ttu-id="f5f42-116">Passaggio 8: Aggiungere hello dopo che gli aggiornamenti di stato di aggiornamento hello firmware tramite hello segnalate troppo proprietà funzione**in attesa**.</span><span class="sxs-lookup"><span data-stu-id="f5f42-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="f5f42-117">In genere, i dispositivi vengono informati della disponibilità di un aggiornamento e definita dall'amministratore criteri provoca hello dispositivo toostart download e l'applicazione hello aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="f5f42-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="f5f42-118">Questa funzione in cui è hello tooenable logica che deve essere eseguita criteri.</span><span class="sxs-lookup"><span data-stu-id="f5f42-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="f5f42-119">Per semplicità, esempio hello in attesa di 4 secondi prima dell'immagine di firmware hello toodownload procedere:</span><span class="sxs-lookup"><span data-stu-id="f5f42-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
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

<span data-ttu-id="f5f42-120">Passaggio 9: Aggiunta di hello dopo che gli aggiornamenti di stato di aggiornamento hello firmware tramite hello segnalate troppo proprietà funzione**download**.</span><span class="sxs-lookup"><span data-stu-id="f5f42-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="f5f42-121">Hello funzione quindi simula un download firmware e infine gli aggiornamenti hello tooeither lo stato di aggiornamento del firmware **downloadFailed** o **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="f5f42-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="f5f42-122">Passaggio 10: Aggiunta di hello dopo che gli aggiornamenti di stato di aggiornamento hello firmware tramite hello segnalate troppo proprietà funzione**applicazione**.</span><span class="sxs-lookup"><span data-stu-id="f5f42-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="f5f42-123">Hello funzione quindi simula applica immagine del firmware di hello e infine gli aggiornamenti hello tooeither lo stato di aggiornamento del firmware **applyFailed** o **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="f5f42-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="f5f42-124">Passaggio 11: Aggiungere seguente hello funzione hello tale handle **firmwareUpdate** dirette del metodo e il firmware più fasi di hello Avvia processo di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="f5f42-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

<span data-ttu-id="f5f42-125">Passaggio 12: Infine, aggiungere hello seguente di codice che si connette l'hub IoT tooyour:</span><span class="sxs-lookup"><span data-stu-id="f5f42-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> <span data-ttu-id="f5f42-126">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="f5f42-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f5f42-127">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5f42-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 