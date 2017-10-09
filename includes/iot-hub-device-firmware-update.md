## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
In questa sezione verrà illustrato come:

* Creare un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello
* Attivare un aggiornamento del firmware simulato
* Hello utilizzare segnalati proprietà tooenable doppi query tooidentify dispositivi e quando sono completato un aggiornamento del firmware

Passaggio 1: creare una cartella vuota denominata **manageddevice**.  In hello **manageddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```

Passaggio 2: al prompt dei comandi in hello **manageddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** e **mqtt azure-iot-dispositivo** dispositivo Pacchetti SDK:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Passaggio 3: Usando un editor di testo, creare un **dmpatterns_fwupdate_device.js** file hello **manageddevice** cartella.

Passaggio 4: Aggiungere seguente hello 'Richiedi' istruzioni all'inizio di hello di hello **dmpatterns_fwupdate_device.js** file:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Passaggio 5: Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza. Sostituire hello `{yourdeviceconnectionstring}` segnaposto con stringa di connessione hello effettuate in precedenza nota di sezione "Creare un'identità del dispositivo" hello in precedenza:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Passaggio 6: Aggiungere il seguente hello funzione che viene utilizzato tooupdate segnalati proprietà:
   
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

Passaggio 7: Aggiungere hello funzioni che simulano il download e l'applicazione hello firmware immagine seguenti:
   
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

Passaggio 8: Aggiungere hello dopo che gli aggiornamenti di stato di aggiornamento hello firmware tramite hello segnalate troppo proprietà funzione**in attesa**. In genere, i dispositivi vengono informati della disponibilità di un aggiornamento e definita dall'amministratore criteri provoca hello dispositivo toostart download e l'applicazione hello aggiornamento. Questa funzione in cui è hello tooenable logica che deve essere eseguita criteri. Per semplicità, esempio hello in attesa di 4 secondi prima dell'immagine di firmware hello toodownload procedere:
   
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

Passaggio 9: Aggiunta di hello dopo che gli aggiornamenti di stato di aggiornamento hello firmware tramite hello segnalate troppo proprietà funzione**download**. Hello funzione quindi simula un download firmware e infine gli aggiornamenti hello tooeither lo stato di aggiornamento del firmware **downloadFailed** o **downloadComplete**:
   
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

Passaggio 10: Aggiunta di hello dopo che gli aggiornamenti di stato di aggiornamento hello firmware tramite hello segnalate troppo proprietà funzione**applicazione**. Hello funzione quindi simula applica immagine del firmware di hello e infine gli aggiornamenti hello tooeither lo stato di aggiornamento del firmware **applyFailed** o **applyComplete**:
    
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

Passaggio 11: Aggiungere seguente hello funzione hello tale handle **firmwareUpdate** dirette del metodo e il firmware più fasi di hello Avvia processo di aggiornamento:
    
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

Passaggio 12: Infine, aggiungere hello seguente di codice che si connette l'hub IoT tooyour:
    
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
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 