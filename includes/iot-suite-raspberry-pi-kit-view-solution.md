## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="ed678-101">Dashboard di soluzione hello View</span><span class="sxs-lookup"><span data-stu-id="ed678-101">View hello solution dashboard</span></span>

<span data-ttu-id="ed678-102">dashboard di soluzione Hello consente soluzione hello distribuito toomanage.</span><span class="sxs-lookup"><span data-stu-id="ed678-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="ed678-103">Ad esempio, è possibile visualizzare dati di telemetria, aggiungere dispositivi e richiamare metodi.</span><span class="sxs-lookup"><span data-stu-id="ed678-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="ed678-104">Quando il provisioning di hello è completato e riquadro hello per la soluzione preconfigurata indica **pronto**, scegliere **avviare** tooopen il portale soluzione di monitoraggio remoto in una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="ed678-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Avviare la soluzione hello preconfigurato][img-launch-solution]

1. <span data-ttu-id="ed678-106">Per impostazione predefinita, il portale di soluzione hello Mostra hello *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="ed678-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="ed678-107">È possibile passare tooother aree del portale di soluzione hello utilizzando il menu di hello nella parte sinistra della pagina hello hello.</span><span class="sxs-lookup"><span data-stu-id="ed678-107">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="ed678-109">Aggiungere un dispositivo</span><span class="sxs-lookup"><span data-stu-id="ed678-109">Add a device</span></span>

<span data-ttu-id="ed678-110">Per una soluzione di dispositivo tooconnect toohello preconfigurato, deve identificarsi tooIoT Hub usando credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="ed678-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="ed678-111">È possibile recuperare le credenziali di dispositivo hello dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="ed678-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="ed678-112">Includere le credenziali di dispositivo hello nell'applicazione client più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ed678-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="ed678-113">Se non già stato fatto, aggiungere una soluzione di monitoraggio remoto tooyour di dispositivo personalizzate.</span><span class="sxs-lookup"><span data-stu-id="ed678-113">If you haven't already done so, add a custom device tooyour remote monitoring solution.</span></span> <span data-ttu-id="ed678-114">Completare i passaggi nel dashboard di soluzione hello hello:</span><span class="sxs-lookup"><span data-stu-id="ed678-114">Complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="ed678-115">Hello angolo in basso a sinistra del dashboard hello, fare clic su **aggiunge un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ed678-115">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Aggiungere un dispositivo][1]

1. <span data-ttu-id="ed678-117">In hello **dispositivo personalizzato** pannello, fare clic su **Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="ed678-117">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Aggiungere un dispositivo personalizzato][2]

1. <span data-ttu-id="ed678-119">Scegliere **Let me define my own Device ID** (Desidero definire il mio ID dispositivo).</span><span class="sxs-lookup"><span data-stu-id="ed678-119">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="ed678-120">Immettere un ID dispositivo, ad esempio **rasppi**, fare clic su **ID controllo** tooverify nome hello non hai già utilizzato nella soluzione e quindi fare clic su **crea** dispositivo hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="ed678-120">Enter a Device ID such as **rasppi**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Aggiungere un ID dispositivo][3]

1. <span data-ttu-id="ed678-122">Rendere le credenziali di un dispositivo di hello nota (**ID dispositivo**, **Hostname Hub IoT**, e **chiave dispositivo**).</span><span class="sxs-lookup"><span data-stu-id="ed678-122">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="ed678-123">L'applicazione client in hello Pi Raspberry deve questi toohello tooconnect valori soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="ed678-123">Your client application on hello Raspberry Pi needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="ed678-124">Fare quindi clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="ed678-124">Then click **Done**.</span></span>

    ![Vedere le credenziali del dispositivo][4]

1. <span data-ttu-id="ed678-126">Selezionare il dispositivo nell'elenco di dispositivi hello nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="ed678-126">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="ed678-127">Quindi, nel hello **dettagli dispositivo** pannello, fare clic su **Abilita periferica**.</span><span class="sxs-lookup"><span data-stu-id="ed678-127">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="ed678-128">lo stato di Hello del dispositivo è ora **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="ed678-128">hello status of your device is now **Running**.</span></span> <span data-ttu-id="ed678-129">soluzione di monitoraggio remoto Hello possa ora ricevere i dati di telemetria dal dispositivo e richiamare metodi sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ed678-129">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png