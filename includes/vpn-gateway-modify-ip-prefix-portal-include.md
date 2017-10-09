### <span data-ttu-id="5e38b-101"><a name="noconnection"></a>toomodify rete locale gateway prefissi degli indirizzi IP - Nessuna connessione gateway</span><span class="sxs-lookup"><span data-stu-id="5e38b-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="tooadd-additional-address-prefixes"></a><span data-ttu-id="5e38b-102">prefissi di indirizzo aggiuntivo tooadd:</span><span class="sxs-lookup"><span data-stu-id="5e38b-102">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="5e38b-103">Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-103">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="5e38b-104">Aggiungere spazio di indirizzi IP hello in hello *Aggiungi intervallo di indirizzi* casella.</span><span class="sxs-lookup"><span data-stu-id="5e38b-104">Add hello IP address space in hello *Add additional address range* box.</span></span>
3. <span data-ttu-id="5e38b-105">Fare clic su **salvare** toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5e38b-105">Click **Save** toosave your settings.</span></span>

#### <a name="tooremove-address-prefixes"></a><span data-ttu-id="5e38b-106">prefissi di indirizzo tooremove:</span><span class="sxs-lookup"><span data-stu-id="5e38b-106">tooremove address prefixes:</span></span>

1. <span data-ttu-id="5e38b-107">Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-107">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="5e38b-108">Fare clic su hello **'...'** sulla riga hello contenente hello prefisso desiderato tooremove.</span><span class="sxs-lookup"><span data-stu-id="5e38b-108">Click hello **'...'** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="5e38b-109">Fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-109">Click **Remove**.</span></span>
4. <span data-ttu-id="5e38b-110">Fare clic su **salvare** toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5e38b-110">Click **Save** toosave your settings.</span></span>

### <span data-ttu-id="5e38b-111"><a name="withconnection"></a>toomodify rete locale gateway prefissi di indirizzi IP - connessione gateway esistente</span><span class="sxs-lookup"><span data-stu-id="5e38b-111"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="5e38b-112">Se si dispone di una connessione gateway e tooadd o rimuovere i prefissi di indirizzi IP hello contenuti nel gateway di rete locale, è necessario hello toodo alla procedura seguente, in ordine.</span><span class="sxs-lookup"><span data-stu-id="5e38b-112">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="5e38b-113">Questo comporterà periodi di inattività per la connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="5e38b-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="5e38b-114">Quando si modificano i prefissi di indirizzi IP, non è necessario gateway VPN di hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="5e38b-114">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="5e38b-115">È necessario solo connessione hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="5e38b-115">You only need tooremove hello connection.</span></span>

#### <a name="1-remove-hello-connection"></a><span data-ttu-id="5e38b-116">1. Rimuovere la connessione di hello.</span><span class="sxs-lookup"><span data-stu-id="5e38b-116">1. Remove hello connection.</span></span>

1. <span data-ttu-id="5e38b-117">Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **connessioni**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-117">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="5e38b-118">Fare clic su hello **...**  hello per ogni connessione, quindi fare clic sulla riga **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-118">Click hello **...** on hello line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="5e38b-119">Fare clic su **salvare** toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5e38b-119">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-address-prefixes"></a><span data-ttu-id="5e38b-120">2. Modificare i prefissi di indirizzo hello.</span><span class="sxs-lookup"><span data-stu-id="5e38b-120">2. Modify hello address prefixes.</span></span>

<span data-ttu-id="5e38b-121">prefissi di indirizzo aggiuntivo tooadd:</span><span class="sxs-lookup"><span data-stu-id="5e38b-121">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="5e38b-122">Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-122">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="5e38b-123">Aggiungere spazio di indirizzi IP hello.</span><span class="sxs-lookup"><span data-stu-id="5e38b-123">Add hello IP address space.</span></span>
3. <span data-ttu-id="5e38b-124">Fare clic su **salvare** toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5e38b-124">Click **Save** toosave your settings.</span></span>

<span data-ttu-id="5e38b-125">prefissi di indirizzo tooremove:</span><span class="sxs-lookup"><span data-stu-id="5e38b-125">tooremove address prefixes:</span></span>

1. <span data-ttu-id="5e38b-126">Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-126">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="5e38b-127">Fare clic su hello **...**  sulla riga hello contenente hello prefisso desiderato tooremove.</span><span class="sxs-lookup"><span data-stu-id="5e38b-127">Click hello **...** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="5e38b-128">Fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-128">Click **Remove**.</span></span>
4. <span data-ttu-id="5e38b-129">Fare clic su **salvare** toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5e38b-129">Click **Save** toosave your settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="5e38b-130">3. Ricreare la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="5e38b-130">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="5e38b-131">Passare toohello Gateway della rete virtuale per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5e38b-131">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="5e38b-132">(Non hello Gateway di rete locale.)</span><span class="sxs-lookup"><span data-stu-id="5e38b-132">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="5e38b-133">Nel Gateway di rete virtuale Ciao hello **impostazioni** fare clic su **connessioni**.</span><span class="sxs-lookup"><span data-stu-id="5e38b-133">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="5e38b-134">Fare clic su hello **+ Aggiungi** tooopen hello **Aggiungi connessione** blade.</span><span class="sxs-lookup"><span data-stu-id="5e38b-134">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="5e38b-135">Ricreare la connessione.</span><span class="sxs-lookup"><span data-stu-id="5e38b-135">Recreate your connection.</span></span>
5. <span data-ttu-id="5e38b-136">Fare clic su **OK** connessione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5e38b-136">Click **OK** toocreate hello connection.</span></span>
