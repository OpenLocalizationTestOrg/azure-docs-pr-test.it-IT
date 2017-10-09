## <a name="view-hello-telemetry"></a><span data-ttu-id="86d57-101">Visualizzazione hello telemetria</span><span class="sxs-lookup"><span data-stu-id="86d57-101">View hello telemetry</span></span>

<span data-ttu-id="86d57-102">soluzione di monitoraggio remoto di dati di telemetria toohello ora invia Hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="86d57-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="86d57-103">È possibile visualizzare i dati di telemetria hello nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="86d57-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="86d57-104">È anche possibile inviare messaggi tooyour Pi Raspberry dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="86d57-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="86d57-105">Passare il dashboard di soluzione toohello.</span><span class="sxs-lookup"><span data-stu-id="86d57-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="86d57-106">Selezionare il dispositivo in hello **tooView dispositivo** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="86d57-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="86d57-107">telemetria Hello da hello Pi Raspberry vengono visualizzati nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="86d57-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Visualizzare i dati di telemetria da hello Raspberry Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="86d57-109">Agire sul dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="86d57-109">Act on hello device</span></span>

<span data-ttu-id="86d57-110">Dal dashboard di soluzione hello, è possibile richiamare metodi sulle Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="86d57-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="86d57-111">Quando hello Pi Raspberry si connette toohello soluzione di monitoraggio remoto, invia informazioni sui metodi di hello che supporta.</span><span class="sxs-lookup"><span data-stu-id="86d57-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="86d57-112">Nel dashboard di soluzione hello, fare clic su **dispositivi** toovisit hello **dispositivi** pagina.</span><span class="sxs-lookup"><span data-stu-id="86d57-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="86d57-113">Selezionare le Pi Raspberry hello **elenco dei dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="86d57-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="86d57-114">Quindi scegliere **Metodi**:</span><span class="sxs-lookup"><span data-stu-id="86d57-114">Then choose **Methods**:</span></span>

    ![Elencare i dispositivi nel dashboard][img-list-devices]

- <span data-ttu-id="86d57-116">In hello **Richiama metodo** pagina, scegliere **LightBlink** in hello **metodo** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="86d57-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="86d57-117">Scegliere **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="86d57-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="86d57-118">simulatore Hello viene stampato un messaggio nella console di hello in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="86d57-118">hello simulator prints a message in hello console on hello Raspberry Pi.</span></span> <span data-ttu-id="86d57-119">app Hello in hello Pi Raspberry invia un dashboard di soluzione toohello indietro riconoscimento:</span><span class="sxs-lookup"><span data-stu-id="86d57-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![Visualizzare la cronologia del metodo][img-method-history]

- <span data-ttu-id="86d57-121">È possibile passare il LED di hello e disattivare utilizzando hello **ChangeLightStatus** metodo con un **LightStatusValue** impostare troppo**1** per su o **0** per disattivare.</span><span class="sxs-lookup"><span data-stu-id="86d57-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="86d57-122">Se si lascia in esecuzione nell'account di Azure di soluzione di monitoraggio remoto hello, verrà addebitato per volta hello che è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="86d57-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="86d57-123">Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="86d57-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="86d57-124">Eliminare la soluzione hello preconfigurato dall'account di Azure al termine dell'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="86d57-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md