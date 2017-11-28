## <a name="create-an-iot-hub"></a><span data-ttu-id="061ac-101">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="061ac-101">Create an IoT hub</span></span>

1. <span data-ttu-id="061ac-102">Nel [portale di Azure](https://portal.azure.com/) fare clic su **Nuovo** > **Internet delle cose** > **Hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="061ac-102">In the [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Creare un hub IoT nel portale di Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="061ac-104">Nel riquadro **Hub IoT** immettere le informazioni seguenti per l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="061ac-104">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

     <span data-ttu-id="061ac-105">**Nome**: immettere il nome dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="061ac-105">**Name**: Enter the name of your IoT hub.</span></span> <span data-ttu-id="061ac-106">Se il nome immesso è valido, viene visualizzato un segno di spunta verde.</span><span class="sxs-lookup"><span data-stu-id="061ac-106">If the name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="061ac-107">**Piano tariffario e livello di scalabilità**: selezionare il livello **F1 gratuito**.</span><span class="sxs-lookup"><span data-stu-id="061ac-107">**Pricing and scale tier**: Select the **F1 - Free** tier.</span></span> <span data-ttu-id="061ac-108">Questa opzione è sufficiente per questa demo.</span><span class="sxs-lookup"><span data-stu-id="061ac-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="061ac-109">Per altre informazioni, vedere [Piano tariffario e livello di scalabilità](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="061ac-109">For more information, see the [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="061ac-110">**Gruppo di risorse**: creare un gruppo di risorse per ospitare l'hub IoT o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="061ac-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="061ac-111">Per altre informazioni, vedere [Usare i gruppi di risorse per gestire le risorse di Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="061ac-111">For more information, see [Use resource groups to manage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="061ac-112">**Percorso**: selezionare la posizione più vicina all'utente in cui viene creato l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="061ac-112">**Location**: Select the closest location to you where the IoT hub is created.</span></span>

     <span data-ttu-id="061ac-113">**Aggiungi al dashboard**: selezionare questa opzione per semplificare l'accesso all'hub IoT dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="061ac-113">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Immettere le informazioni per creare l'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="061ac-115">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="061ac-115">Click **Create**.</span></span> <span data-ttu-id="061ac-116">La creazione dell'hub IoT può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="061ac-116">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="061ac-117">È possibile visualizzare lo stato di avanzamento nel riquadro **Notifiche**.</span><span class="sxs-lookup"><span data-stu-id="061ac-117">You can see progress in the **Notifications** pane.</span></span>

   ![Vedere le notifiche relative allo stato dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="061ac-119">Dopo aver creato l'hub IoT, selezionarlo nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="061ac-119">After your IoT hub is created, click it on the dashboard.</span></span> <span data-ttu-id="061ac-120">Annotare il **Nome host**, quindi fare clic su **Criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="061ac-120">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>

   ![Ottenere il nome host dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="061ac-122">Nel riquadro **Criteri di accesso condivisi** fare clic sul criterio **iothubowner**, quindi copiare e annotare la **Stringa di connessione** dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="061ac-122">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub.</span></span> <span data-ttu-id="061ac-123">Per altre informazioni, vedere [Controllare l'accesso all'hub IoT](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="061ac-123">For more information, see [Control access to IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="061ac-124">Per questa esercitazione di configurazione non è necessaria la stringa di connessione iothubowner.</span><span class="sxs-lookup"><span data-stu-id="061ac-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="061ac-125">Potrebbe essere tuttavia necessaria per alcune delle esercitazioni in altri scenari IoT, dopo aver completato questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="061ac-125">However, you may need it for some of the tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Ottenere la stringa di connessione dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a><span data-ttu-id="061ac-127">Registrare un dispositivo nell'hub IoT per il dispositivo</span><span class="sxs-lookup"><span data-stu-id="061ac-127">Register a device in the IoT hub for your device</span></span>

1. <span data-ttu-id="061ac-128">Nel [portale di Azure](https://portal.azure.com/), aprire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="061ac-128">In the [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="061ac-129">Fare clic su **Esplora dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="061ac-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="061ac-130">Nel riquadro Esplora dispositivi fare clic su **Aggiungi** per aggiungere un dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="061ac-130">In the Device Explorer pane, click **Add** to add a device to your IoT hub.</span></span> <span data-ttu-id="061ac-131">Eseguire quindi le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="061ac-131">Then do the following:</span></span>

   <span data-ttu-id="061ac-132">**ID dispositivo**: immettere l'ID del nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="061ac-132">**Device ID**: Enter the ID of the new device.</span></span> <span data-ttu-id="061ac-133">Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="061ac-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="061ac-134">**Tipo di autenticazione**: selezionare **Chiave simmetrica**.</span><span class="sxs-lookup"><span data-stu-id="061ac-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="061ac-135">**Genera chiavi automaticamente**: selezionare questa casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="061ac-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="061ac-136">**Connetti dispositivo all'hub IoT**: fare clic su **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="061ac-136">**Connect device to IoT Hub**: Click **Enable**.</span></span>

   ![Aggiungere un dispositivo a Device Explorer nell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="061ac-138">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="061ac-138">Click **Save**.</span></span>
5. <span data-ttu-id="061ac-139">Dopo la creazione del dispositivo, aprire il dispositivo nel riquadro **Esplora dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="061ac-139">After the device is created, open the device in the **Device Explorer** pane.</span></span>
6. <span data-ttu-id="061ac-140">Annotare la chiave primaria della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="061ac-140">Make a note of the primary key of the connection string.</span></span>

   ![Ottenere la stringa di connessione del dispositivo](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
