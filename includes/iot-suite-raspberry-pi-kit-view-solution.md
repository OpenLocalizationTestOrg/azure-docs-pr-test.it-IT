## <a name="view-the-solution-dashboard"></a><span data-ttu-id="fef76-101">Visualizzare il dashboard della soluzione</span><span class="sxs-lookup"><span data-stu-id="fef76-101">View the solution dashboard</span></span>

<span data-ttu-id="fef76-102">Il dashboard della soluzione consente di gestire la soluzione distribuita.</span><span class="sxs-lookup"><span data-stu-id="fef76-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="fef76-103">Ad esempio, è possibile visualizzare dati di telemetria, aggiungere dispositivi e richiamare metodi.</span><span class="sxs-lookup"><span data-stu-id="fef76-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="fef76-104">Al termine del provisioning, quando il riquadro della soluzione preconfigurata indica **Pronto**, scegliere **Avvia** per aprire il portale della soluzione di monitoraggio remoto in una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="fef76-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Avviare la soluzione preconfigurata][img-launch-solution]

1. <span data-ttu-id="fef76-106">Per impostazione predefinita, il portale della soluzione visualizza il *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="fef76-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="fef76-107">È possibile passare ad altre aree del portale della soluzione usando il menu sul lato sinistro della pagina.</span><span class="sxs-lookup"><span data-stu-id="fef76-107">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="fef76-109">Aggiungere un dispositivo</span><span class="sxs-lookup"><span data-stu-id="fef76-109">Add a device</span></span>

<span data-ttu-id="fef76-110">Per connettere un dispositivo alla soluzione preconfigurata, è necessario che identifichi se stesso nell'hub IoT mediante delle credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="fef76-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="fef76-111">È possibile recuperare le credenziali del dispositivo dal dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fef76-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="fef76-112">Le istruzioni per includere le credenziali del dispositivo nell'applicazione client sono illustrate più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fef76-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="fef76-113">Se non è già stato fatto, aggiungere un dispositivo personalizzato alla soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="fef76-113">If you haven't already done so, add a custom device to your remote monitoring solution.</span></span> <span data-ttu-id="fef76-114">Completare questa procedura nel dashboard della soluzione:</span><span class="sxs-lookup"><span data-stu-id="fef76-114">Complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="fef76-115">Nell'angolo inferiore sinistro del dashboard fare clic su **Aggiungi un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="fef76-115">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![Aggiungere un dispositivo][1]

1. <span data-ttu-id="fef76-117">Nel pannello **Dispositivo personalizzato** fare clic su **Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="fef76-117">In the **Custom Device** panel, click **Add new**.</span></span>

   ![Aggiungere un dispositivo personalizzato][2]

1. <span data-ttu-id="fef76-119">Scegliere **Let me define my own Device ID** (Desidero definire il mio ID dispositivo).</span><span class="sxs-lookup"><span data-stu-id="fef76-119">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="fef76-120">Immettere un ID dispositivo, ad esempio **rasppi**, fare clic su **Controlla ID** per verificare di non avere già usato il nome nella soluzione e quindi fare clic su **Crea** per effettuare il provisioning del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fef76-120">Enter a Device ID such as **rasppi**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![Aggiungere un ID dispositivo][3]

1. <span data-ttu-id="fef76-122">Annotare le credenziali del dispositivo (**ID dispositivo**, **Nome host hub IoT** e **Chiave dispositivo**).</span><span class="sxs-lookup"><span data-stu-id="fef76-122">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="fef76-123">Questi valori sono necessari per consentire all'applicazione client in Raspberry Pi di connettersi alla soluzione per il monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="fef76-123">Your client application on the Raspberry Pi needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="fef76-124">Fare quindi clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="fef76-124">Then click **Done**.</span></span>

    ![Vedere le credenziali del dispositivo][4]

1. <span data-ttu-id="fef76-126">Selezionare il dispositivo nell'elenco dei dispositivi nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fef76-126">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="fef76-127">Nel pannello **Dettagli dispositivo** fare clic su **Attiva dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="fef76-127">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="fef76-128">Lo stato del dispositivo è ora **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="fef76-128">The status of your device is now **Running**.</span></span> <span data-ttu-id="fef76-129">La soluzione per il monitoraggio remoto può ora ricevere i dati di telemetria dal dispositivo e richiamare i metodi sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fef76-129">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png