## <a name="how-to-create-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="c9dc6-101">Come creare una rete virtuale classica con l’Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c9dc6-101">How to create a classic VNet using Azure CLI</span></span>
<span data-ttu-id="c9dc6-102">È possibile utilizzare l'interfaccia della riga di comando (CLI) di Azure per gestire le risorse di Azure dal prompt dei comandi da qualsiasi computer con Windows, Linux o OSX.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="c9dc6-103">Per creare una rete virtuale utilizzando l'interfaccia della riga di comando di Azure seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-103">To create a VNet by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="c9dc6-104">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../articles/cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-104">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c9dc6-105">Eseguire il comando per **creare reti virtuali di Azure** per creare una rete virtuale e una subnet, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-105">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="c9dc6-106">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-106">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="c9dc6-107">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="c9dc6-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="c9dc6-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-108">**--vnet**.</span></span> <span data-ttu-id="c9dc6-109">Nome della rete virtuale da creare.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-109">Name of the VNet to be created.</span></span> <span data-ttu-id="c9dc6-110">Per questo scenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="c9dc6-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="c9dc6-111">**-e (o --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="c9dc6-112">Spazio degli indirizzi della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-112">VNet address space.</span></span> <span data-ttu-id="c9dc6-113">Per questo scenario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="c9dc6-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="c9dc6-114">**-i (o -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="c9dc6-115">Maschera di rete nel formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-115">Network mask in CIDR format.</span></span> <span data-ttu-id="c9dc6-116">Per questo scenario, *16*</span><span class="sxs-lookup"><span data-stu-id="c9dc6-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="c9dc6-117">**- n (o --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="c9dc6-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="c9dc6-118">Nome della prima subnet.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-118">Name of the first subnet.</span></span> <span data-ttu-id="c9dc6-119">Per questo scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="c9dc6-120">**-p (or --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="c9dc6-121">Indirizzo IP iniziale per la subnet o spazio di indirizzi della subnet.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="c9dc6-122">Per questo scenario, *192.168.1.0*</span><span class="sxs-lookup"><span data-stu-id="c9dc6-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="c9dc6-123">**-r (o --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="c9dc6-124">Maschera di rete nel formato CIDR per la subnet.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="c9dc6-125">Per questo scenario, *24*</span><span class="sxs-lookup"><span data-stu-id="c9dc6-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="c9dc6-126">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-126">**-l (or --location)**.</span></span> <span data-ttu-id="c9dc6-127">Area di Azure in cui verrà creata la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-127">Azure region where the VNet will be created.</span></span> <span data-ttu-id="c9dc6-128">Per questo scenario, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="c9dc6-129">Eseguire il comando per **creare la subnet della rete virtuale di Azure** per creare una subnet, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-129">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span></span> <span data-ttu-id="c9dc6-130">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-130">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="c9dc6-131">Di seguito è riportato l'output previsto per il comando precedente:</span><span class="sxs-lookup"><span data-stu-id="c9dc6-131">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="c9dc6-132">**-t (o --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="c9dc6-133">Nome della rete virtuale in cui verrà creata la subnet.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-133">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="c9dc6-134">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="c9dc6-135">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-135">**-n (or --name)**.</span></span> <span data-ttu-id="c9dc6-136">Nome della nuova subnet.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-136">Name of the new subnet.</span></span> <span data-ttu-id="c9dc6-137">Per questo scenario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="c9dc6-138">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="c9dc6-139">Blocco CIDR della subnet.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-139">Subnet CIDR block.</span></span> <span data-ttu-id="c9dc6-140">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="c9dc6-141">Eseguire il comando **azure network vnet show** per visualizzare le proprietà della nuova rete virtuale, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c9dc6-141">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="c9dc6-142">Di seguito è riportato l'output previsto per il comando precedente:</span><span class="sxs-lookup"><span data-stu-id="c9dc6-142">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

