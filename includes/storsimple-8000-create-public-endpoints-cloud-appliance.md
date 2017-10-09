#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="56e83-101">endpoint pubblici toocreate nel dispositivo cloud hello</span><span class="sxs-lookup"><span data-stu-id="56e83-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="56e83-102">Accedi toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56e83-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="56e83-103">Andare troppo**macchine virtuali**, quindi selezionare e fare clic sulla macchina virtuale hello che viene usato come dispositivo di cloud.</span><span class="sxs-lookup"><span data-stu-id="56e83-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="56e83-104">È necessario toocreate rete sicurezza gruppo () regola toocontrol hello flusso di traffico da e verso la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="56e83-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="56e83-105">Eseguire hello seguendo i passaggi toocreate una regola di gruppo.</span><span class="sxs-lookup"><span data-stu-id="56e83-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="56e83-106">Selezionare **Gruppo di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="56e83-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="56e83-107">Fare clic su hello predefinito rete gruppo di sicurezza viene presentato.</span><span class="sxs-lookup"><span data-stu-id="56e83-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="56e83-108">Selezionare **Regole di sicurezza in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="56e83-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="56e83-109">Fare clic su **+ Aggiungi** toocreate una regola di sicurezza in ingresso.</span><span class="sxs-lookup"><span data-stu-id="56e83-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="56e83-110">Nel pannello regole di sicurezza in ingresso Aggiungi di hello:</span><span class="sxs-lookup"><span data-stu-id="56e83-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="56e83-111">Per hello **nome**, digitare quanto segue di hello assegnare un nome per l'endpoint di hello: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="56e83-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="56e83-112">Per hello **priorità**, selezionare un numero minore di 1000 (priorità hello per regola predefinita hello).</span><span class="sxs-lookup"><span data-stu-id="56e83-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="56e83-113">Valore più alto hello, una priorità inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="56e83-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="56e83-114">Set hello **origine** troppo**qualsiasi**.</span><span class="sxs-lookup"><span data-stu-id="56e83-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="56e83-115">Per hello **servizio**selezionare **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="56e83-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="56e83-116">Hello **protocollo** viene impostata automaticamente troppo**TCP** hello e **intervallo di porte** è troppo**5986**.</span><span class="sxs-lookup"><span data-stu-id="56e83-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="56e83-117">Fare clic su **OK** regola hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="56e83-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="56e83-118">Il passaggio finale consiste tooassociate la sicurezza della rete di gruppo con una subnet o un'interfaccia di rete specifici.</span><span class="sxs-lookup"><span data-stu-id="56e83-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="56e83-119">Eseguire hello seguendo i passaggi tooassociate il gruppo di sicurezza di rete con una subnet.</span><span class="sxs-lookup"><span data-stu-id="56e83-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="56e83-120">Andare troppo**subnet**.</span><span class="sxs-lookup"><span data-stu-id="56e83-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="56e83-121">Fare clic su **+ Associa**.</span><span class="sxs-lookup"><span data-stu-id="56e83-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="56e83-122">Selezionare la rete virtuale e quindi selezionare la subnet appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="56e83-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="56e83-123">Fare clic su **OK** regola hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="56e83-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="56e83-124">Dopo aver creata la regola hello, è possibile visualizzare il relativo indirizzo IP virtuale pubblico (VIP) di dettagli toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="56e83-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="56e83-125">Registrare tale indirizzo.</span><span class="sxs-lookup"><span data-stu-id="56e83-125">Record this address.</span></span>


