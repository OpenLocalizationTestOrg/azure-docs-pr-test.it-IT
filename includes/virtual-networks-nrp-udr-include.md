## <a name="route-tables"></a><span data-ttu-id="461f4-101">Tabelle di route</span><span class="sxs-lookup"><span data-stu-id="461f4-101">Route tables</span></span>
<span data-ttu-id="461f4-102">Risorse tabella route contiene le route utilizzate toodefine come flussi di traffico all'interno dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="461f4-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="461f4-103">È possibile utilizzare toosend route (UDR) definito dall'utente tutto il traffico da un determinata subnet tooa dispositivo virtuale, ad esempio un sistema di rilevamento delle intrusioni o di firewall (ID).</span><span class="sxs-lookup"><span data-stu-id="461f4-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="461f4-104">È possibile associare un toosubnets tabella di route.</span><span class="sxs-lookup"><span data-stu-id="461f4-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="461f4-105">Tabelle di route contengono hello le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="461f4-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="461f4-106">Proprietà</span><span class="sxs-lookup"><span data-stu-id="461f4-106">Property</span></span> | <span data-ttu-id="461f4-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="461f4-107">Description</span></span> | <span data-ttu-id="461f4-108">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="461f4-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="461f4-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="461f4-109">**routes**</span></span> |<span data-ttu-id="461f4-110">Raccolta di utenti definiti route nella tabella di route hello</span><span class="sxs-lookup"><span data-stu-id="461f4-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="461f4-111">vedere [route definite dall'utente](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="461f4-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="461f4-112">**subnet**</span><span class="sxs-lookup"><span data-stu-id="461f4-112">**subnets**</span></span> |<span data-ttu-id="461f4-113">Raccolta della tabella di routing hello subnet viene applicata troppo</span><span class="sxs-lookup"><span data-stu-id="461f4-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="461f4-114">vedere [subnet](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="461f4-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="461f4-115">route definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="461f4-115">User defined routes</span></span>
<span data-ttu-id="461f4-116">È possibile creare toospecify UDRs cui traffico deve essere inviato, in base al relativo indirizzo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="461f4-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="461f4-117">È possibile considerare una route come definizione del gateway predefinito hello basate sull'indirizzo di destinazione hello di un pacchetto di rete.</span><span class="sxs-lookup"><span data-stu-id="461f4-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="461f4-118">UDRs contengono hello le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="461f4-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="461f4-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="461f4-119">Property</span></span> | <span data-ttu-id="461f4-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="461f4-120">Description</span></span> | <span data-ttu-id="461f4-121">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="461f4-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="461f4-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="461f4-122">**addressPrefix**</span></span> |<span data-ttu-id="461f4-123">Prefisso dell'indirizzo o indirizzo IP completo per la destinazione di hello</span><span class="sxs-lookup"><span data-stu-id="461f4-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="461f4-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="461f4-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="461f4-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="461f4-125">**nextHopType**</span></span> |<span data-ttu-id="461f4-126">Tipo di dispositivo hello traffico verrà inviato troppo</span><span class="sxs-lookup"><span data-stu-id="461f4-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="461f4-127">VirtualAppliance, Gateway VPN, Internet</span><span class="sxs-lookup"><span data-stu-id="461f4-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="461f4-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="461f4-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="461f4-129">Indirizzo IP dell'hop successivo hello</span><span class="sxs-lookup"><span data-stu-id="461f4-129">IP address for hello next hop</span></span> |<span data-ttu-id="461f4-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="461f4-130">192.168.1.4</span></span> |

<span data-ttu-id="461f4-131">Tabella di route di esempio in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="461f4-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="461f4-132">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="461f4-132">Additional resources</span></span>
* <span data-ttu-id="461f4-133">Altre informazioni sulle [route definite dall'utente](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="461f4-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="461f4-134">Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) per le tabelle di route.</span><span class="sxs-lookup"><span data-stu-id="461f4-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="461f4-135">Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) per l'utente definito route (UDRs).</span><span class="sxs-lookup"><span data-stu-id="461f4-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

