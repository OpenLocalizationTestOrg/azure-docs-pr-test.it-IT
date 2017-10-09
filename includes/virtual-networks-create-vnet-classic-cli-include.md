## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="1aa13-101">Come toocreate una rete virtuale classica mediante Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1aa13-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="1aa13-102">È possibile utilizzare hello Azure CLI toomanage le risorse di Azure dal prompt dei comandi di hello da qualsiasi computer che eseguono Windows, Linux o OSX.</span><span class="sxs-lookup"><span data-stu-id="1aa13-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="1aa13-103">una rete virtuale tramite l'interfaccia CLI di Azure, hello toocreate procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1aa13-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="1aa13-104">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../articles/cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1aa13-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="1aa13-105">Eseguire hello **creazione della rete virtuale di rete di azure** comando toocreate una rete virtuale e una subnet, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1aa13-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="1aa13-106">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="1aa13-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="1aa13-107">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="1aa13-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="1aa13-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-108">**--vnet**.</span></span> <span data-ttu-id="1aa13-109">Nome di hello toobe di rete virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="1aa13-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="1aa13-110">Per questo scenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="1aa13-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="1aa13-111">**-e (o --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="1aa13-112">Spazio degli indirizzi della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1aa13-112">VNet address space.</span></span> <span data-ttu-id="1aa13-113">Per questo scenario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="1aa13-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="1aa13-114">**-i (o -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="1aa13-115">Maschera di rete nel formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="1aa13-115">Network mask in CIDR format.</span></span> <span data-ttu-id="1aa13-116">Per questo scenario, *16*</span><span class="sxs-lookup"><span data-stu-id="1aa13-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="1aa13-117">**- n (o --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="1aa13-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="1aa13-118">Nome della subnet prima hello.</span><span class="sxs-lookup"><span data-stu-id="1aa13-118">Name of hello first subnet.</span></span> <span data-ttu-id="1aa13-119">Per questo scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="1aa13-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="1aa13-120">**-p (or --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="1aa13-121">Indirizzo IP iniziale per la subnet o spazio di indirizzi della subnet.</span><span class="sxs-lookup"><span data-stu-id="1aa13-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="1aa13-122">Per questo scenario, *192.168.1.0*</span><span class="sxs-lookup"><span data-stu-id="1aa13-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="1aa13-123">**-r (o --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="1aa13-124">Maschera di rete nel formato CIDR per la subnet.</span><span class="sxs-lookup"><span data-stu-id="1aa13-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="1aa13-125">Per questo scenario, *24*</span><span class="sxs-lookup"><span data-stu-id="1aa13-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="1aa13-126">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-126">**-l (or --location)**.</span></span> <span data-ttu-id="1aa13-127">Area di Azure in cui verrà creato hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1aa13-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="1aa13-128">Per questo scenario, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="1aa13-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="1aa13-129">Eseguire hello **subnet di rete virtuale di rete di azure creare** toocreate comando una subnet, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1aa13-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="1aa13-130">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="1aa13-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="1aa13-131">Ecco l'output di hello previsto per comando hello sopra indicato:</span><span class="sxs-lookup"><span data-stu-id="1aa13-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="1aa13-132">**-t (o --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="1aa13-133">Nome della rete virtuale in cui verrà creata la subnet hello hello.</span><span class="sxs-lookup"><span data-stu-id="1aa13-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="1aa13-134">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="1aa13-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="1aa13-135">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-135">**-n (or --name)**.</span></span> <span data-ttu-id="1aa13-136">Nome della nuova subnet hello.</span><span class="sxs-lookup"><span data-stu-id="1aa13-136">Name of hello new subnet.</span></span> <span data-ttu-id="1aa13-137">Per questo scenario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="1aa13-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="1aa13-138">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="1aa13-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="1aa13-139">Blocco CIDR della subnet.</span><span class="sxs-lookup"><span data-stu-id="1aa13-139">Subnet CIDR block.</span></span> <span data-ttu-id="1aa13-140">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="1aa13-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="1aa13-141">Eseguire hello **Mostra di rete virtuale di rete di azure** comando proprietà hello tooview di hello nuova rete virtuale, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1aa13-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="1aa13-142">Ecco l'output di hello previsto per comando hello sopra indicato:</span><span class="sxs-lookup"><span data-stu-id="1aa13-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
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

