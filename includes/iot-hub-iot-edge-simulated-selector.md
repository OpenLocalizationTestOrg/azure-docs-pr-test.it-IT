> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

Questa procedura dettagliata di hello [simulato dispositivo Cloud caricare esempio] illustra come toouse [Azure IoT Edge] [ lnk-sdk] toosend tooIoT di telemetria da dispositivo a cloud Hub da simulata dispositivi.

In questa procedura dettagliata verranno trattati i seguenti argomenti:

* **Architettura**: architettura informazioni hello [simulato dispositivo Cloud caricare esempio].
* **Compilare ed eseguire**: esempio di esecuzione hello e toobuild necessari passaggi di hello.

## <a name="architecture"></a>Architettura

Hello [simulato dispositivo Cloud caricare esempio] viene illustrato come un gateway che invia dati di telemetria da toocreate simulato hub IoT tooan di dispositivi. Un dispositivo potrebbe non essere in grado di tooconnect direttamente tooIoT Hub perché il dispositivo hello:

* Non usa un protocollo di comunicazione riconosciuto dall'hub IoT.
* Non è abbastanza tooremember hello identità assegnato tooit dall'IoT Hub.

Un gateway esterno IoT può risolvere questi problemi in hello seguenti modi:

* gateway Hello riconosce protocollo hello usato dal dispositivo hello, riceve i dati di telemetria da dispositivo a cloud dal dispositivo hello e inoltra tali tooIoT messaggi Hub utilizzando un protocollo riconosciuto dall'hub IoT hello.

* gateway Hello esegue il mapping toodevices identità IoT Hub e funge da proxy quando un dispositivo invia messaggi tooIoT Hub.

Hello seguente diagramma mostra hello componenti principali dell'esempio hello, tra cui hello moduli IoT Edge:

![][1]

i moduli di Hello non passano i messaggi direttamente tooeach altri. i moduli di Hello pubblicano messaggi tooan interno broker che recapita toohello messaggi hello altri moduli utilizzando un meccanismo di sottoscrizione. Per altre informazioni, vedere [Get started with Azure IoT Edge][lnk-gw-getstarted] (Introduzione ad Azure IoT Edge).

### <a name="protocol-ingestion-module"></a>Modulo di inserimento del protocollo

Questo modulo è hello punto di partenza per la ricezione di dati dai dispositivi, tramite il gateway hello e nel cloud hello. Nell'esempio hello modulo hello:

1. Crea dati di temperatura simulati. Se si usano dispositivi fisici, modulo hello legge i dati da tali dispositivi fisici.
1. Crea un messaggio.
1. Inserisce dati di temperatura hello simulato il contenuto del messaggio hello.
1. Aggiunge una proprietà con un messaggio di toohello indirizzo MAC FALSO.
1. Rende modulo successivo disponibile toohello di messaggio hello nella catena di hello.

modulo Hello denominato **inserimento X protocollo** in hello diagramma precedente viene chiamato **dispositivo simulato** nel codice sorgente hello.

### <a name="mac-lt-gt-iot-hub-id-module"></a>Modulo ID MAC &lt;-&gt; IoT Hub

Questo modulo esegue l'analisi dei messaggi che includono una proprietà dell'indirizzo Mac. Nell'esempio hello, modulo di hello del protocollo di inserimento aggiunge proprietà dell'indirizzo MAC hello. Se il modulo hello rileva tale proprietà, viene aggiunta un'altra proprietà con un messaggio di chiave toohello dispositivo IoT Hub. modulo Hello rende quindi modulo successivo disponibile toohello di messaggio hello nella catena di hello.

sviluppatore Hello imposta un mapping tra gli indirizzi MAC e IoT Hub identità tooassociate hello simulato i dispositivi con le identità del dispositivo IoT Hub. sviluppatore Hello aggiunge mapping hello manualmente come parte della configurazione del modulo hello.

> [!NOTE]
> Questo esempio usa un indirizzo MAC come identificatore univoco del dispositivo e lo associa a un'identità dei dispositivi di un hub IoT. Tuttavia, è possibile scrivere un modulo personalizzato che usa un identificatore univoco diverso. Ad esempio, i dispositivi siano univoci i numeri di serie o dati di telemetria hello possono includere un nome univoco del dispositivo incorporato.

### <a name="iot-hub-communication-module"></a>Modulo di comunicazione dell'hub IoT

Questo modulo accetta i messaggi con un IoT Hub proprietà chiave dispositivo assegnato dal modulo precedente hello. modulo Hello Invia messaggio hello tooIoT contenuto Hub mediante hello protocollo HTTP. HTTP è uno dei hello tre protocolli riconosciuti dall'IoT Hub.

Anziché aprendo una connessione per ogni dispositivo simulato, questo modulo viene visualizzata una singola connessione HTTP dall'hub IoT toohello di hello gateway. modulo Hello demultiplexing quindi le connessioni da tutti i dispositivi di hello simulato tramite tale connessione. Questo approccio consente tooconnect un singolo gateway molti più dispositivi.

## <a name="before-you-get-started"></a>Prima di iniziare

Prima di iniziare:

* [Creazione di un hub IoT] [ lnk-create-hub] nella sottoscrizione di Azure, è necessario il nome di hello di toocomplete l'hub in questa procedura dettagliata. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* Aggiungere due dispositivi tooyour IoT hub e prendere nota dei relativi ID e le chiavi di dispositivo. È possibile utilizzare hello [Esplora dispositivo] [ lnk-device-explorer] o [l'hub IOT Esplora] [ lnk-iothub-explorer] strumento tooadd l'hub IoT toohello di dispositivi creata nel hello precedente passaggio e recuperare le relative chiavi.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[simulato dispositivo Cloud caricare esempio]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md