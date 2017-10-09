## <a name="create-an-iot-hub"></a><span data-ttu-id="317b4-101">Creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="317b4-101">Create an IoT hub</span></span>
<span data-ttu-id="317b4-102">Creare un hub IoT per tooconnect di app del dispositivo simulato per.</span><span class="sxs-lookup"><span data-stu-id="317b4-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="317b4-103">Hello passaggi seguenti viene illustrato come toocomplete questa attività dal utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="317b4-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="317b4-104">Accedi toohello [portale di Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="317b4-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="317b4-105">In hello Jumpbar, fare clic su **New** > **Internet of Things** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="317b4-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Indice del portale di Azure][1]
1. <span data-ttu-id="317b4-107">In hello **hub IoT** pannello, scegliere configurazione hello per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="317b4-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![Pannello Hub IoT][2]
   
   1. <span data-ttu-id="317b4-109">In hello **nome** , immettere un nome per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="317b4-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="317b4-110">Se hello **nome** è valido e disponibile, viene visualizzato un segno di spunta verde in hello **nome** casella.</span><span class="sxs-lookup"><span data-stu-id="317b4-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="317b4-111">Selezionare un [piano tariffario e un livello di scalabilità][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="317b4-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="317b4-112">Per questa esercitazione non è necessario un livello specifico.</span><span class="sxs-lookup"><span data-stu-id="317b4-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="317b4-113">Per questa esercitazione, usare il livello F1 gratuito di hello.</span><span class="sxs-lookup"><span data-stu-id="317b4-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="317b4-114">In **Gruppo di risorse** creare un gruppo di risorse o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="317b4-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="317b4-115">Per ulteriori informazioni, vedere [utilizzando risorse gruppi di risorse di Azure toomanage][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="317b4-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="317b4-116">In **percorso**, selezionare hello percorso toohost l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="317b4-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="317b4-117">Per questa esercitazione, scegliere la località più vicina.</span><span class="sxs-lookup"><span data-stu-id="317b4-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="317b4-118">Dopo aver scelto le opzioni di configurazione dell'hub IoT, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="317b4-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="317b4-119">Può richiedere alcuni minuti per Azure toocreate l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="317b4-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="317b4-120">stato hello toocheck, è possibile monitorare lo stato di avanzamento hello hello schermata iniziale o nel Pannello di notifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="317b4-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Stato del nuovo hub IoT][3]
1. <span data-ttu-id="317b4-122">Hub IoT hello è stata creata, fare clic su nuovo riquadro di hello per l'hub IoT nel Pannello di hello hello tooopen portale Azure per l'hub IoT nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="317b4-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="317b4-123">Prendere nota di hello **Hostname**, quindi fare clic su **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="317b4-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Pannello del nuovo hub IoT][4]
1. <span data-ttu-id="317b4-125">In hello **criteri di accesso condiviso** pannello, fare clic su hello **iothubowner** criteri, quindi copiare e prendere nota della stringa di connessione IoT Hub hello in hello **iothubowner** blade.</span><span class="sxs-lookup"><span data-stu-id="317b4-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="317b4-126">Per ulteriori informazioni, vedere [il controllo degli accessi] [ lnk-access-control] in hello "Guida per sviluppatori di IoT Hub".</span><span class="sxs-lookup"><span data-stu-id="317b4-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
    ![Pannello Criteri di accesso condivisi][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
