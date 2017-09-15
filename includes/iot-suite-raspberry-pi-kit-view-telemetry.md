## <a name="view-the-telemetry"></a><span data-ttu-id="0c0e4-101">Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="0c0e4-101">View the telemetry</span></span>

<span data-ttu-id="0c0e4-102">Raspberry Pi ora invia i dati di telemetria alla soluzione di monitoraggio remota.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="0c0e4-103">È possibile visualizzare i dati di telemetria nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="0c0e4-104">È anche possibile inviare messaggi a Raspberry Pi dal dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="0c0e4-105">Passare al dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="0c0e4-106">Selezionare il dispositivo nell'elenco a discesa **Dispositivo da visualizzare**.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="0c0e4-107">I dati di telemetria da Raspberry Pi vengono visualizzati nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Visualizzare i dati di telemetria da Raspberry Pi][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="0c0e4-109">Agire sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="0c0e4-109">Act on the device</span></span>

<span data-ttu-id="0c0e4-110">Dal dashboard della soluzione è possibile richiamare i metodi in Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="0c0e4-111">Quando Raspberry Pi si connette alla soluzione di monitoraggio remoto, invia le informazioni sui metodi supportati.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="0c0e4-112">Nel dashboard della soluzione fare clic su **Dispositivi** per passare alla pagina **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="0c0e4-113">Selezionare Raspberry Pi in **Elenco dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="0c0e4-114">Quindi scegliere **Metodi**:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-114">Then choose **Methods**:</span></span>

    ![Elencare i dispositivi nel dashboard][img-list-devices]

- <span data-ttu-id="0c0e4-116">Nella pagina **Richiama metodo** scegliere **LightBlink** nell'elenco a discesa **Metodo**.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="0c0e4-117">Scegliere **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="0c0e4-118">Il LED connesso a Raspberry Pi lampeggia più volte.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-118">The LED connected to the Raspberry Pi flashes several times.</span></span> <span data-ttu-id="0c0e4-119">L'app in Raspberry Pi invia un acknowledgment al dashboard della soluzione:</span><span class="sxs-lookup"><span data-stu-id="0c0e4-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![Visualizzare la cronologia del metodo][img-method-history]

- <span data-ttu-id="0c0e4-121">È possibile accendere e spegnere il LED usando il metodo **ChangeLightStatus**, con **LightStatusValue** impostato su **1** l'accensione o su **0** per lo spegnimento.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="0c0e4-122">Se si lascia la soluzione di monitoraggio remoto in esecuzione nell'account Azure, verrà addebitato il tempo dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="0c0e4-123">Per altre informazioni sulla riduzione del consumo durante l'esecuzione della soluzione di monitoraggio remoto, vedere [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configurazione di soluzioni preconfigurate di Azure IoT Suite per scopi dimostrativi).</span><span class="sxs-lookup"><span data-stu-id="0c0e4-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="0c0e4-124">Al termine, eliminare la soluzione preconfigurata dall'account Azure.</span><span class="sxs-lookup"><span data-stu-id="0c0e4-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md