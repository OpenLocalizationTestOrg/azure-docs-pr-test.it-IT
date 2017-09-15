> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbc67-101">C su Windows</span><span class="sxs-lookup"><span data-stu-id="fbc67-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="fbc67-102">C su Linux</span><span class="sxs-lookup"><span data-stu-id="fbc67-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="fbc67-103">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fbc67-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="fbc67-104">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="fbc67-104">Scenario overview</span></span>
<span data-ttu-id="fbc67-105">In questo scenario, viene creato un dispositivo che invia la seguente telemetria alla [soluzione preconfigurata][lnk-what-are-preconfig-solutions] per il monitoraggio remoto:</span><span class="sxs-lookup"><span data-stu-id="fbc67-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="fbc67-106">Temperatura esterna</span><span class="sxs-lookup"><span data-stu-id="fbc67-106">External temperature</span></span>
* <span data-ttu-id="fbc67-107">Temperatura interna</span><span class="sxs-lookup"><span data-stu-id="fbc67-107">Internal temperature</span></span>
* <span data-ttu-id="fbc67-108">Umidità</span><span class="sxs-lookup"><span data-stu-id="fbc67-108">Humidity</span></span>

<span data-ttu-id="fbc67-109">Per semplicità, il codice nel dispositivo genera valori di esempio, ma si consiglia di estendere l'esempio connettendo i sensori reali al dispositivo e inviando i dati di telemetria reali.</span><span class="sxs-lookup"><span data-stu-id="fbc67-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="fbc67-110">Inoltre, il dispositivo è in grado di rispondere ai metodi richiamati dal dashboard di soluzione e ai valori di proprietà desiderati impostati nel dashboard di soluzione.</span><span class="sxs-lookup"><span data-stu-id="fbc67-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="fbc67-111">Per completare l'esercitazione, è necessario un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="fbc67-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="fbc67-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="fbc67-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fbc67-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="fbc67-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="fbc67-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="fbc67-114">Before you start</span></span>
<span data-ttu-id="fbc67-115">Prima di scrivere un codice per il dispositivo, occorre eseguire la soluzione preconfigurata di monitoraggio remoto e poi effettuare il provisioning di un nuovo dispositivo personalizzato all'interno della soluzione in questione.</span><span class="sxs-lookup"><span data-stu-id="fbc67-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="fbc67-116">Eseguire il provisioning della soluzione preconfigurata per il monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="fbc67-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="fbc67-117">Il dispositivo creato in questa esercitazione invia dati a un'istanza della soluzione preconfigurata per il [monitoraggio remoto][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="fbc67-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="fbc67-118">Se nel proprio account Azure non è già stato eseguito il provisioning della soluzione preconfigurata per il monitoraggio remoto, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fbc67-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="fbc67-119">Nella pagina <https://www.azureiotsuite.com/> fare clic su **+** per creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="fbc67-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="fbc67-120">Fare clic su **Seleziona** nel pannello **Remote monitoring** (Monitoraggio remoto) per creare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="fbc67-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="fbc67-121">Nella pagina per la **creazione della soluzione di monitoraggio remoto** immettere il nome desiderato in **Nome soluzione** e selezionare l'**area** in cui eseguire la distribuzione e quindi la sottoscrizione di Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="fbc67-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="fbc67-122">Fare clic su **Crea soluzione**.</span><span class="sxs-lookup"><span data-stu-id="fbc67-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="fbc67-123">Attendere finché non viene completato il processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="fbc67-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="fbc67-124">Le soluzioni preconfigurate usano servizi di Azure fatturabili.</span><span class="sxs-lookup"><span data-stu-id="fbc67-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="fbc67-125">Al termine, assicurarsi di rimuovere la soluzione preconfigurata dalla sottoscrizione per evitare eventuali addebiti non necessari.</span><span class="sxs-lookup"><span data-stu-id="fbc67-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="fbc67-126">Per rimuovere completamente una soluzione preconfigurata dalla sottoscrizione, visitare la pagina <https://www.azureiotsuite.com/>.</span><span class="sxs-lookup"><span data-stu-id="fbc67-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="fbc67-127">Al termine del processo di provisioning della soluzione di monitoraggio remoto, fare clic su **Avvia** per aprire il dashboard della soluzione nel browser.</span><span class="sxs-lookup"><span data-stu-id="fbc67-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Dashboard della soluzione][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="fbc67-129">Effettuare il provisioning del dispositivo nella soluzione di monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="fbc67-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="fbc67-130">Se è già stato eseguito il provisioning di un dispositivo nella soluzione, è possibile saltare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="fbc67-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="fbc67-131">È necessario conoscere le credenziali del dispositivo quando si crea l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="fbc67-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="fbc67-132">Per connettere un dispositivo alla soluzione preconfigurata, è necessario che identifichi se stesso nell'hub IoT mediante delle credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="fbc67-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="fbc67-133">È possibile recuperare le credenziali del dispositivo dal dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fbc67-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="fbc67-134">Le istruzioni per includere le credenziali del dispositivo nell'applicazione client sono illustrate più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fbc67-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="fbc67-135">Per aggiungere un dispositivo alla soluzione per il monitoraggio remoto, completare i passaggi seguenti nel dashboard della soluzione:</span><span class="sxs-lookup"><span data-stu-id="fbc67-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="fbc67-136">Nell'angolo inferiore sinistro del dashboard fare clic su **Aggiungi un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="fbc67-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Aggiungere un dispositivo][1]
2. <span data-ttu-id="fbc67-138">Nel pannello **Dispositivo personalizzato** fare clic su **Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="fbc67-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Aggiungere un dispositivo personalizzato][2]
3. <span data-ttu-id="fbc67-140">Scegliere **Let me define my own Device ID** (Desidero definire il mio ID dispositivo).</span><span class="sxs-lookup"><span data-stu-id="fbc67-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="fbc67-141">Immettere un ID dispositivo, ad esempio **mydevice**, fare clic su **Controlla ID** per verificare che tale nome non sia già in uso e quindi fare clic su **Crea** per effettuare il provisioning del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fbc67-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Aggiungere un ID dispositivo][3]
4. <span data-ttu-id="fbc67-143">Annotare le credenziali del dispositivo (ID dispositivo, nome host dell'hub IoT e chiave dispositivo).</span><span class="sxs-lookup"><span data-stu-id="fbc67-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="fbc67-144">Questi valori sono necessari per consentire all'applicazione client di connettersi alla soluzione per il monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="fbc67-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="fbc67-145">Fare quindi clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="fbc67-145">Then click **Done**.</span></span>
   
    ![Vedere le credenziali del dispositivo][4]
5. <span data-ttu-id="fbc67-147">Selezionare il dispositivo nell'elenco dei dispositivi nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="fbc67-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="fbc67-148">Nel pannello **Dettagli dispositivo** fare clic su **Attiva dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="fbc67-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="fbc67-149">Lo stato del dispositivo è ora **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="fbc67-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="fbc67-150">La soluzione per il monitoraggio remoto può ora ricevere i dati di telemetria dal dispositivo e richiamare i metodi sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fbc67-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/