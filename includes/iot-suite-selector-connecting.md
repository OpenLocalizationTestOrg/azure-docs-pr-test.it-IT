> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a4c3-101">C su Windows</span><span class="sxs-lookup"><span data-stu-id="2a4c3-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="2a4c3-102">C su Linux</span><span class="sxs-lookup"><span data-stu-id="2a4c3-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="2a4c3-103">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2a4c3-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="2a4c3-104">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="2a4c3-104">Scenario overview</span></span>
<span data-ttu-id="2a4c3-105">In questo scenario, si crea un dispositivo che invia hello seguendo il monitoraggio remoto di dati di telemetria toohello [preconfigurato soluzione][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="2a4c3-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="2a4c3-106">Temperatura esterna</span><span class="sxs-lookup"><span data-stu-id="2a4c3-106">External temperature</span></span>
* <span data-ttu-id="2a4c3-107">Temperatura interna</span><span class="sxs-lookup"><span data-stu-id="2a4c3-107">Internal temperature</span></span>
* <span data-ttu-id="2a4c3-108">Umidità</span><span class="sxs-lookup"><span data-stu-id="2a4c3-108">Humidity</span></span>

<span data-ttu-id="2a4c3-109">Per semplicità, codice hello sul dispositivo hello genera valori di esempio, ma che incoraggia la collaborazione è tooextend: esempio hello connettendosi dispositivo tooyour sensori reale e l'invio di dati di telemetria reale.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="2a4c3-110">dispositivo Hello è anche toomethods toorespond in grado di richiamata dal dashboard di soluzione hello e valori di proprietà impostati in dashboard soluzione hello desiderati.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="2a4c3-111">toocomplete questa esercitazione, è necessario un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="2a4c3-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2a4c3-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="2a4c3-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2a4c3-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2a4c3-114">Before you start</span></span>
<span data-ttu-id="2a4c3-115">Prima di scrivere un codice per il dispositivo, occorre eseguire la soluzione preconfigurata di monitoraggio remoto e poi effettuare il provisioning di un nuovo dispositivo personalizzato all'interno della soluzione in questione.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="2a4c3-116">Eseguire il provisioning della soluzione preconfigurata per il monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="2a4c3-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="2a4c3-117">dispositivo Hello si creerà in questa esercitazione invia istanza tooan dati hello [monitoraggio remoto] [ lnk-remote-monitoring] preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="2a4c3-118">Se non hai già effettuato il provisioning hello soluzione preconfigurata nell'account di Azure di monitoraggio remoto, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2a4c3-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="2a4c3-119">In hello <https://www.azureiotsuite.com/> pagina, fare clic su  **+**  toocreate una soluzione.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="2a4c3-120">Fare clic su **selezionare** su hello **monitoraggio remoto** pannello toocreate la soluzione.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="2a4c3-121">In hello **creare il monitoraggio remoto soluzione** pagina, immettere un **Nome soluzione** di propria scelta, selezionare hello **area** toodeploy per desiderati e selezionare hello Azure toouse toowant di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="2a4c3-122">Fare clic su **Crea soluzione**.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="2a4c3-123">Attendere il completamento di hello processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="2a4c3-124">le soluzioni di Hello preconfigurato utilizzano fatturabili servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="2a4c3-125">Verificare tooremove hello soluzione preconfigurata dalla sottoscrizione di una volta con esso tooavoid eventuali addebiti non necessari.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="2a4c3-126">È possibile rimuovere completamente una soluzione preconfigurata dalla sottoscrizione, visitare hello <https://www.azureiotsuite.com/> pagina.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="2a4c3-127">Termine del processo per la soluzione di monitoraggio remoto hello di provisioning hello, fare clic su **avviare** dashboard di soluzione hello tooopen nel browser.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Dashboard della soluzione][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="2a4c3-129">Eseguire il provisioning del dispositivo nella soluzione di monitoraggio remoto hello</span><span class="sxs-lookup"><span data-stu-id="2a4c3-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="2a4c3-130">Se è già stato eseguito il provisioning di un dispositivo nella soluzione, è possibile saltare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="2a4c3-131">Quando si crea un'applicazione client hello, sono necessarie le credenziali di dispositivo di tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="2a4c3-132">Per una soluzione di dispositivo tooconnect toohello preconfigurato, deve identificarsi tooIoT Hub usando credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="2a4c3-133">È possibile recuperare le credenziali di dispositivo hello dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="2a4c3-134">Includere le credenziali di dispositivo hello nell'applicazione client più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="2a4c3-135">tooadd una soluzione di monitoraggio remoto tooyour di dispositivo, hello completo seguendo i passaggi nel dashboard di soluzione hello:</span><span class="sxs-lookup"><span data-stu-id="2a4c3-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="2a4c3-136">Hello angolo in basso a sinistra del dashboard hello, fare clic su **aggiunge un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Aggiungere un dispositivo][1]
2. <span data-ttu-id="2a4c3-138">In hello **dispositivo personalizzato** pannello, fare clic su **Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Aggiungere un dispositivo personalizzato][2]
3. <span data-ttu-id="2a4c3-140">Scegliere **Let me define my own Device ID** (Desidero definire il mio ID dispositivo).</span><span class="sxs-lookup"><span data-stu-id="2a4c3-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="2a4c3-141">Immettere un ID dispositivo, ad esempio **mydevice**, fare clic su **ID controllo** tooverify tale nome è già in uso e quindi fare clic su **crea** dispositivo hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Aggiungere un ID dispositivo][3]
4. <span data-ttu-id="2a4c3-143">Rendere un dispositivo di hello nota le credenziali (ID dispositivo, nome host di Hub IoT e chiave del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="2a4c3-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="2a4c3-144">L'applicazione client deve questi toohello tooconnect valori soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="2a4c3-145">Fare quindi clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-145">Then click **Done**.</span></span>
   
    ![Vedere le credenziali del dispositivo][4]
5. <span data-ttu-id="2a4c3-147">Selezionare il dispositivo nell'elenco di dispositivi hello nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="2a4c3-148">Quindi, nel hello **dettagli dispositivo** pannello, fare clic su **Abilita periferica**.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="2a4c3-149">lo stato di Hello del dispositivo è ora **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="2a4c3-150">soluzione di monitoraggio remoto Hello possa ora ricevere i dati di telemetria dal dispositivo e richiamare metodi sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="2a4c3-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/