## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="c5d88-101">Configura dispositivo simulato di hello Node.js</span><span class="sxs-lookup"><span data-stu-id="c5d88-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="c5d88-102">Dashboard di monitoraggio remoto di hello, fare clic su **+ Aggiungi una periferica** e quindi aggiungere un *dispositivo personalizzata*.</span><span class="sxs-lookup"><span data-stu-id="c5d88-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="c5d88-103">Nome host, l'id dispositivo e chiave del dispositivo, prendere nota di hello IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c5d88-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="c5d88-104">È necessario più avanti in questa esercitazione quando si prepara un'applicazione hello remote_monitoring.js dispositivo client.</span><span class="sxs-lookup"><span data-stu-id="c5d88-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="c5d88-105">Verificare che Node.js 0.12.x o una versione successiva sia installata sul computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="c5d88-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="c5d88-106">Eseguire `node --version` un prompt dei comandi o in una versione di hello toocheck shell.</span><span class="sxs-lookup"><span data-stu-id="c5d88-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="c5d88-107">Per informazioni sull'utilizzo di un tooinstall manager pacchetto Node.js in Linux, vedere [l'installazione di Node.js tramite Gestione pacchetti][node-linux].</span><span class="sxs-lookup"><span data-stu-id="c5d88-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="c5d88-108">Dopo aver installato Node.js, clonare hello versione hello [azure iot-sdk-nodi] [ lnk-github-repo] computer di sviluppo tooyour repository.</span><span class="sxs-lookup"><span data-stu-id="c5d88-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="c5d88-109">Utilizzare sempre hello **master** ramo per la versione più recente di hello delle librerie di hello e gli esempi.</span><span class="sxs-lookup"><span data-stu-id="c5d88-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="c5d88-110">Dalla copia locale di hello [azure iot-sdk-nodi] [ lnk-github-repo] repository, hello copia i seguenti due file dalla cartella vuota tooan cartella dispositivo/nodo/esempi di hello nel computer di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="c5d88-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="c5d88-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="c5d88-111">packages.json</span></span>
   * <span data-ttu-id="c5d88-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="c5d88-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="c5d88-113">Aprire il file remote_monitoring.js hello e cercare hello seguente definizione di variabile:</span><span class="sxs-lookup"><span data-stu-id="c5d88-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="c5d88-114">Sostituire **[stringa di connessione dispositivo Hub IoT]** con la stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c5d88-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="c5d88-115">Utilizzare i valori hello per nome host IoT Hub, id dispositivo e nella chiave del dispositivo che è annotata nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="c5d88-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="c5d88-116">Una stringa di connessione del dispositivo ha hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="c5d88-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="c5d88-117">Se il nome host di IoT Hub è **contoso** e l'id dispositivo **mydevice**, la stringa di connessione sarà simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c5d88-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Salvare il file hello. <span data-ttu-id="c5d88-119">Eseguire i seguenti comandi in una shell o un prompt dei comandi nella cartella hello che contiene questi file tooinstall hello pacchetti hello e quindi eseguire l'applicazione di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="c5d88-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="c5d88-120">Osservare la telemetria dinamica in azione</span><span class="sxs-lookup"><span data-stu-id="c5d88-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="c5d88-121">dashboard di Hello Mostra hello temperatura e umidità dati di telemetria dai dispositivi simulato esistente hello:</span><span class="sxs-lookup"><span data-stu-id="c5d88-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![dashboard predefinito Hello][image1]

<span data-ttu-id="c5d88-123">Se si seleziona il dispositivo simulato di hello Node.js che è stato eseguito nella sezione precedente di hello, vedere temperatura e umidità, dati di telemetria temperatura esterni:</span><span class="sxs-lookup"><span data-stu-id="c5d88-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Aggiungere dashboard toohello temperatura esterno][image2]

<span data-ttu-id="c5d88-125">soluzione di monitoraggio remoto Hello automaticamente rileva il tipo di dati di telemetria di hello aggiuntive temperatura esterno e lo aggiunge toohello grafico nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="c5d88-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png