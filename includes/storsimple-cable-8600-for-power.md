<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a><span data-ttu-id="c98e5-101">toocable il dispositivo per l'alimentazione</span><span class="sxs-lookup"><span data-stu-id="c98e5-101">toocable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="c98e5-102">Entrambi gli enclosure nel dispositivo StorSimple includono PCM ridondanti.</span><span class="sxs-lookup"><span data-stu-id="c98e5-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="c98e5-103">Per ogni enclosure, hello PCM deve essere installato e connesso toodifferent power origini tooensure la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="c98e5-103">For each enclosure, hello PCMs must be installed and connected toodifferent power sources tooensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="c98e5-104">Assicurarsi che tutti i moduli PCM hello interruttori di alimentazione hello siano in posizione OFF hello.</span><span class="sxs-lookup"><span data-stu-id="c98e5-104">Make sure that hello power switches on all hello PCMs are in hello OFF position.</span></span>
2. <span data-ttu-id="c98e5-105">Sull'enclosure principale hello, connettersi tooboth cavi di alimentazione hello PCM.</span><span class="sxs-lookup"><span data-stu-id="c98e5-105">On hello primary enclosure, connect hello power cords tooboth PCMs.</span></span> <span data-ttu-id="c98e5-106">Hello cavi di alimentazione sono identificati in rosso in power hello cablaggio diagramma, di seguito.</span><span class="sxs-lookup"><span data-stu-id="c98e5-106">hello power cords are identified in red in hello power cabling diagram, below.</span></span>
3. <span data-ttu-id="c98e5-107">Assicurarsi che hello due moduli PCM hello enclosure principale usino separato fonti di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="c98e5-107">Make sure that hello two PCMs on hello primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="c98e5-108">Collegare hello power cavi toohello accensione unità di distribuzione di hello rack come illustrato nel diagramma di cablaggio di alimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="c98e5-108">Attach hello power cords toohello power on hello rack distribution units as shown in hello power cabling diagram.</span></span>
5. <span data-ttu-id="c98e5-109">Ripetere i passaggi da 2 a 4 per hello enclosure EBOD.</span><span class="sxs-lookup"><span data-stu-id="c98e5-109">Repeat steps 2 through 4 for hello EBOD enclosure.</span></span>
6. <span data-ttu-id="c98e5-110">Accendere l'enclosure EBOD hello girando l'interruttore di alimentazione hello in posizione on toohello ogni PCM.</span><span class="sxs-lookup"><span data-stu-id="c98e5-110">Turn on hello EBOD enclosure by flipping hello power switch on each PCM toohello ON position.</span></span>
7. <span data-ttu-id="c98e5-111">Verificare che hello enclosure EBOD sia attiva assicurandosi che il LED verde hello su hello parte posteriore di controller EBOD hello è accesi.</span><span class="sxs-lookup"><span data-stu-id="c98e5-111">Verify that hello EBOD enclosure is turned on by checking that hello green LEDs on hello back of hello EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="c98e5-112">Accendere l'enclosure principale hello girando toohello in posizione on commutatore ogni PCM.</span><span class="sxs-lookup"><span data-stu-id="c98e5-112">Turn on hello primary enclosure by flipping each PCM switch toohello ON position.</span></span>
9. <span data-ttu-id="c98e5-113">Verificare che il sistema hello sia nel assicurandosi che i controller di dispositivo hello che LED siano accesi.</span><span class="sxs-lookup"><span data-stu-id="c98e5-113">Verify that hello system is on by ensuring hello device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="c98e5-114">Assicurarsi che la connessione hello tra controller EBOD hello e controller del dispositivo hello sia attiva verificando che siano di colore verde hello quattro LED Avanti toohello porta SAS sul controller EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="c98e5-114">Make sure that hello connection between hello EBOD controller and hello device controller is active by verifying that hello four LEDs next toohello SAS port on hello EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="c98e5-115">tooensure la disponibilità elevata per il sistema, si consiglia di attenersi schema illustrato nel seguente diagramma hello di cablaggio di alimentazione di toohello.</span><span class="sxs-lookup"><span data-stu-id="c98e5-115">tooensure high availability for your system, we recommend that you strictly adhere toohello power cabling scheme shown in hello following diagram.</span></span>
    > 
    > 
    
    ![Cablare il dispositivo 4U per l'alimentazione](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="c98e5-117">**Cablaggio di alimentazione**</span><span class="sxs-lookup"><span data-stu-id="c98e5-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="c98e5-118">Etichetta</span><span class="sxs-lookup"><span data-stu-id="c98e5-118">Label</span></span> | <span data-ttu-id="c98e5-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c98e5-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c98e5-120">1</span><span class="sxs-lookup"><span data-stu-id="c98e5-120">1</span></span> |<span data-ttu-id="c98e5-121">Enclosure principale</span><span class="sxs-lookup"><span data-stu-id="c98e5-121">Primary enclosure</span></span> |
    | <span data-ttu-id="c98e5-122">2</span><span class="sxs-lookup"><span data-stu-id="c98e5-122">2</span></span> |<span data-ttu-id="c98e5-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="c98e5-123">PCM 0</span></span> |
    | <span data-ttu-id="c98e5-124">3</span><span class="sxs-lookup"><span data-stu-id="c98e5-124">3</span></span> |<span data-ttu-id="c98e5-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="c98e5-125">PCM 1</span></span> |
    | <span data-ttu-id="c98e5-126">4</span><span class="sxs-lookup"><span data-stu-id="c98e5-126">4</span></span> |<span data-ttu-id="c98e5-127">Controller 0</span><span class="sxs-lookup"><span data-stu-id="c98e5-127">Controller 0</span></span> |
    | <span data-ttu-id="c98e5-128">5</span><span class="sxs-lookup"><span data-stu-id="c98e5-128">5</span></span> |<span data-ttu-id="c98e5-129">Controller 1</span><span class="sxs-lookup"><span data-stu-id="c98e5-129">Controller 1</span></span> |
    | <span data-ttu-id="c98e5-130">6</span><span class="sxs-lookup"><span data-stu-id="c98e5-130">6</span></span> |<span data-ttu-id="c98e5-131">Controller 0 EBOD</span><span class="sxs-lookup"><span data-stu-id="c98e5-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="c98e5-132">7</span><span class="sxs-lookup"><span data-stu-id="c98e5-132">7</span></span> |<span data-ttu-id="c98e5-133">Controller 1 EBOD</span><span class="sxs-lookup"><span data-stu-id="c98e5-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="c98e5-134">8</span><span class="sxs-lookup"><span data-stu-id="c98e5-134">8</span></span> |<span data-ttu-id="c98e5-135">Chassis EBOD</span><span class="sxs-lookup"><span data-stu-id="c98e5-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="c98e5-136">9</span><span class="sxs-lookup"><span data-stu-id="c98e5-136">9</span></span> |<span data-ttu-id="c98e5-137">PDU</span><span class="sxs-lookup"><span data-stu-id="c98e5-137">PDUs</span></span> |

