<!--author=alkohli last changed: 9/16/15-->


#### <a name="to-cable-your-device-for-power"></a><span data-ttu-id="be133-101">Cablare il dispositivo per l'alimentazione</span><span class="sxs-lookup"><span data-stu-id="be133-101">To cable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="be133-102">Entrambi gli enclosure nel dispositivo StorSimple includono PCM ridondanti.</span><span class="sxs-lookup"><span data-stu-id="be133-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="be133-103">Per ogni enclosure entrambi i PCM devono essere installati e collegati a una fonte di alimentazione diversa per assicurare la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="be133-103">For each enclosure, the PCMs must be installed and connected to different power sources to ensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="be133-104">Assicurarsi che gli interruttori di alimentazione di tutti i moduli PCM siano in posizione OFF.</span><span class="sxs-lookup"><span data-stu-id="be133-104">Make sure that the power switches on all the PCMs are in the OFF position.</span></span>
2. <span data-ttu-id="be133-105">Nell'enclosure principale, collegare i cavi di alimentazione a entrambi i moduli PCM.</span><span class="sxs-lookup"><span data-stu-id="be133-105">On the primary enclosure, connect the power cords to both PCMs.</span></span> <span data-ttu-id="be133-106">I cavi di alimentazione sono identificati in rosso nella seguente figura del cablaggio di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="be133-106">The power cords are identified in red in the power cabling diagram, below.</span></span>
3. <span data-ttu-id="be133-107">Verificare che i due moduli PCM dell'enclosure principale usino fonti di alimentazione separate.</span><span class="sxs-lookup"><span data-stu-id="be133-107">Make sure that the two PCMs on the primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="be133-108">Collegare i cavi di alimentazione alle unità PDU (Power Distribution Unit) rack come illustrato nella seguente figura del cablaggio di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="be133-108">Attach the power cords to the power on the rack distribution units as shown in the power cabling diagram.</span></span>
5. <span data-ttu-id="be133-109">Ripetere i passaggi da 2 a 4 per l'enclosure EBOD.</span><span class="sxs-lookup"><span data-stu-id="be133-109">Repeat steps 2 through 4 for the EBOD enclosure.</span></span>
6. <span data-ttu-id="be133-110">Accendere l'enclosure EBOD girando l'interruttore di alimentazione di ciascun modulo PCM su ON.</span><span class="sxs-lookup"><span data-stu-id="be133-110">Turn on the EBOD enclosure by flipping the power switch on each PCM to the ON position.</span></span>
7. <span data-ttu-id="be133-111">Verificare che l'enclosure EBOD sia attiva assicurandosi che i LED dei controller EBOD (di colore verde sul retro dell'enclosure) siano accesi.</span><span class="sxs-lookup"><span data-stu-id="be133-111">Verify that the EBOD enclosure is turned on by checking that the green LEDs on the back of the EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="be133-112">Accendere l'enclosure principale girando l'interruttore di ciascun modulo PCM su ON.</span><span class="sxs-lookup"><span data-stu-id="be133-112">Turn on the primary enclosure by flipping each PCM switch to the ON position.</span></span>
9. <span data-ttu-id="be133-113">Verificare che il sistema sia attivo assicurandosi che i LED dei controller del dispositivo siano accesi.</span><span class="sxs-lookup"><span data-stu-id="be133-113">Verify that the system is on by ensuring the device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="be133-114">Verificare che il collegamento tra il controller EBOD e il controller del dispositivo sia attivo, assicurandosi che i quattro LED accanto alla porta SAS sul controller EBOD siano verdi.</span><span class="sxs-lookup"><span data-stu-id="be133-114">Make sure that the connection between the EBOD controller and the device controller is active by verifying that the four LEDs next to the SAS port on the EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="be133-115">Per garantire la disponibilità elevata del sistema, si consiglia vivamente di attenersi allo schema di cablaggio dell'alimentazione illustrato nella seguente figura.</span><span class="sxs-lookup"><span data-stu-id="be133-115">To ensure high availability for your system, we recommend that you strictly adhere to the power cabling scheme shown in the following diagram.</span></span>
    > 
    > 
    
    ![Cablare il dispositivo 4U per l'alimentazione](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="be133-117">**Cablaggio di alimentazione**</span><span class="sxs-lookup"><span data-stu-id="be133-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="be133-118">Etichetta</span><span class="sxs-lookup"><span data-stu-id="be133-118">Label</span></span> | <span data-ttu-id="be133-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="be133-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="be133-120">1</span><span class="sxs-lookup"><span data-stu-id="be133-120">1</span></span> |<span data-ttu-id="be133-121">Enclosure principale</span><span class="sxs-lookup"><span data-stu-id="be133-121">Primary enclosure</span></span> |
    | <span data-ttu-id="be133-122">2</span><span class="sxs-lookup"><span data-stu-id="be133-122">2</span></span> |<span data-ttu-id="be133-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="be133-123">PCM 0</span></span> |
    | <span data-ttu-id="be133-124">3</span><span class="sxs-lookup"><span data-stu-id="be133-124">3</span></span> |<span data-ttu-id="be133-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="be133-125">PCM 1</span></span> |
    | <span data-ttu-id="be133-126">4</span><span class="sxs-lookup"><span data-stu-id="be133-126">4</span></span> |<span data-ttu-id="be133-127">Controller 0</span><span class="sxs-lookup"><span data-stu-id="be133-127">Controller 0</span></span> |
    | <span data-ttu-id="be133-128">5</span><span class="sxs-lookup"><span data-stu-id="be133-128">5</span></span> |<span data-ttu-id="be133-129">Controller 1</span><span class="sxs-lookup"><span data-stu-id="be133-129">Controller 1</span></span> |
    | <span data-ttu-id="be133-130">6</span><span class="sxs-lookup"><span data-stu-id="be133-130">6</span></span> |<span data-ttu-id="be133-131">Controller 0 EBOD</span><span class="sxs-lookup"><span data-stu-id="be133-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="be133-132">7</span><span class="sxs-lookup"><span data-stu-id="be133-132">7</span></span> |<span data-ttu-id="be133-133">Controller 1 EBOD</span><span class="sxs-lookup"><span data-stu-id="be133-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="be133-134">8</span><span class="sxs-lookup"><span data-stu-id="be133-134">8</span></span> |<span data-ttu-id="be133-135">Chassis EBOD</span><span class="sxs-lookup"><span data-stu-id="be133-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="be133-136">9</span><span class="sxs-lookup"><span data-stu-id="be133-136">9</span></span> |<span data-ttu-id="be133-137">PDU</span><span class="sxs-lookup"><span data-stu-id="be133-137">PDUs</span></span> |

