## <a name="create-an-iot-hub"></a><span data-ttu-id="f1bab-101">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="f1bab-101">Create an IoT hub</span></span>

1. <span data-ttu-id="f1bab-102">In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **Internet of Things** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="f1bab-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Creare un hub IoT in hello portale di Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="f1bab-104">In hello **hub IoT** riquadro, immettere le seguenti informazioni per l'hub IoT hello:</span><span class="sxs-lookup"><span data-stu-id="f1bab-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="f1bab-105">**Nome**: immettere il nome di hello dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f1bab-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="f1bab-106">Se specifica un nome hello è valido, viene visualizzato un segno di spunta verde.</span><span class="sxs-lookup"><span data-stu-id="f1bab-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="f1bab-107">**Livello di prezzi e scalabilità**: hello seleziona **F1 - libero** livello.</span><span class="sxs-lookup"><span data-stu-id="f1bab-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="f1bab-108">Questa opzione è sufficiente per questa demo.</span><span class="sxs-lookup"><span data-stu-id="f1bab-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="f1bab-109">Per ulteriori informazioni, vedere hello [prezzi e livello di scalabilità](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="f1bab-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="f1bab-110">**Gruppo di risorse**: creazione di un hub IoT di hello toohost di gruppo di risorse o utilizzarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="f1bab-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="f1bab-111">Per ulteriori informazioni, vedere [gruppi di risorse di utilizzare toomanage le risorse di Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f1bab-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="f1bab-112">**Percorso**: selezionare hello più vicino tooyou percorso in cui è stato creato l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="f1bab-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="f1bab-113">**PIN toodashboard**: selezionare questa opzione per l'hub IoT tooyour di facile accesso dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="f1bab-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Immettere informazioni toocreate l'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="f1bab-115">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f1bab-115">Click **Create**.</span></span> <span data-ttu-id="f1bab-116">L'hub IoT potrebbe richiedere alcuni minuti toocreate.</span><span class="sxs-lookup"><span data-stu-id="f1bab-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="f1bab-117">È possibile visualizzare lo stato di avanzamento in hello **notifiche** riquadro.</span><span class="sxs-lookup"><span data-stu-id="f1bab-117">You can see progress in hello **Notifications** pane.</span></span>

   ![Vedere le notifiche relative allo stato dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="f1bab-119">Dopo aver creato l'hub IoT, selezionarla nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="f1bab-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="f1bab-120">Prendere nota di hello **Hostname**, quindi fare clic su **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="f1bab-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![Ottieni nome host hello dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="f1bab-122">In hello **criteri di accesso condiviso** riquadro, fare clic su hello **iothubowner** criteri, quindi copia e prendere nota del hello **stringa di connessione** dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f1bab-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="f1bab-123">Per ulteriori informazioni, vedere [tooIoT accesso controllo Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="f1bab-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="f1bab-124">Per questa esercitazione di configurazione non è necessaria la stringa di connessione iothubowner.</span><span class="sxs-lookup"><span data-stu-id="f1bab-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="f1bab-125">Tuttavia, potrebbe essere necessario per alcune delle esercitazioni di hello in diversi scenari IoT dopo aver completato l'installazione.</span><span class="sxs-lookup"><span data-stu-id="f1bab-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Ottenere la stringa di connessione dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="f1bab-127">Registrare un dispositivo nell'hub IoT hello per il dispositivo</span><span class="sxs-lookup"><span data-stu-id="f1bab-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="f1bab-128">In hello [portale di Azure](https://portal.azure.com/), aprire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f1bab-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="f1bab-129">Fare clic su **Esplora dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="f1bab-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="f1bab-130">Nel riquadro di esplorazione di dispositivo hello, fare clic su **Aggiungi** tooadd un hub IoT tooyour di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f1bab-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="f1bab-131">Quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f1bab-131">Then do hello following:</span></span>

   <span data-ttu-id="f1bab-132">**ID dispositivo**: immettere l'ID hello del nuovo dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="f1bab-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="f1bab-133">Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="f1bab-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="f1bab-134">**Tipo di autenticazione**: selezionare **Chiave simmetrica**.</span><span class="sxs-lookup"><span data-stu-id="f1bab-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="f1bab-135">**Genera chiavi automaticamente**: selezionare questa casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="f1bab-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="f1bab-136">**Connessione dispositivo tooIoT Hub**: fare clic su **abilitare**.</span><span class="sxs-lookup"><span data-stu-id="f1bab-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Aggiungere un dispositivo in hello Esplora dispositivo dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="f1bab-138">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f1bab-138">Click **Save**.</span></span>
5. <span data-ttu-id="f1bab-139">Dopo aver creato il dispositivo di hello, aprire la periferica hello in hello **Esplora dispositivo** riquadro.</span><span class="sxs-lookup"><span data-stu-id="f1bab-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="f1bab-140">Prendere nota della chiave primaria di hello hello della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="f1bab-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Ottenere la stringa di connessione dispositivo hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
