## <a name="route-tables"></a><span data-ttu-id="7bdf0-101">Tabelle di route</span><span class="sxs-lookup"><span data-stu-id="7bdf0-101">Route tables</span></span>
<span data-ttu-id="7bdf0-102">Le risorse di tabelle di route contengono le route usate per definire il flusso del traffico all'interno dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="7bdf0-103">È possibile usare le route definite dall'utente (UDR) per inviare tutto il traffico da una determinata subnet a un dispositivo virtuale, ad esempio un firewall o un sistema di rilevamento delle intrusioni (IDS).</span><span class="sxs-lookup"><span data-stu-id="7bdf0-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="7bdf0-104">È possibile associare una tabella di route alle subnet.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-104">You can associate a route table to subnets.</span></span> 

<span data-ttu-id="7bdf0-105">Le tabella di route contengono le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-105">Route tables contain the following properties.</span></span>

| <span data-ttu-id="7bdf0-106">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7bdf0-106">Property</span></span> | <span data-ttu-id="7bdf0-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7bdf0-107">Description</span></span> | <span data-ttu-id="7bdf0-108">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="7bdf0-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bdf0-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="7bdf0-109">**routes**</span></span> |<span data-ttu-id="7bdf0-110">Raccolta di route definite dall'utente nella tabella di route</span><span class="sxs-lookup"><span data-stu-id="7bdf0-110">Collection of user defined routes in the route table</span></span> |<span data-ttu-id="7bdf0-111">vedere [route definite dall'utente](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="7bdf0-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="7bdf0-112">**subnet**</span><span class="sxs-lookup"><span data-stu-id="7bdf0-112">**subnets**</span></span> |<span data-ttu-id="7bdf0-113">Raccolta di subnet a cui viene applicata la tabella di route</span><span class="sxs-lookup"><span data-stu-id="7bdf0-113">Collection of subnets the route table is applied to</span></span> |<span data-ttu-id="7bdf0-114">vedere [subnet](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="7bdf0-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="7bdf0-115">route definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="7bdf0-115">User defined routes</span></span>
<span data-ttu-id="7bdf0-116">È possibile creare route definite dall'utente per specificare dove inviare il traffico, in base al relativo indirizzo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="7bdf0-117">Una route può essere considerata come la definizione del gateway predefinito in base all'indirizzo di destinazione di un pacchetto di rete.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span></span>

<span data-ttu-id="7bdf0-118">Le route definite dall'utente contengono le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-118">UDRs contain the following properties.</span></span> 

| <span data-ttu-id="7bdf0-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7bdf0-119">Property</span></span> | <span data-ttu-id="7bdf0-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7bdf0-120">Description</span></span> | <span data-ttu-id="7bdf0-121">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="7bdf0-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bdf0-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="7bdf0-122">**addressPrefix**</span></span> |<span data-ttu-id="7bdf0-123">Prefisso dell'indirizzo o indirizzo IP completo per la destinazione</span><span class="sxs-lookup"><span data-stu-id="7bdf0-123">Address prefix, or full IP address for the destination</span></span> |<span data-ttu-id="7bdf0-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="7bdf0-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="7bdf0-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="7bdf0-125">**nextHopType**</span></span> |<span data-ttu-id="7bdf0-126">Tipo di dispositivo al quale verrà inviato il traffico.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-126">Type of device the traffic will be sent to</span></span> |<span data-ttu-id="7bdf0-127">VirtualAppliance, Gateway VPN, Internet</span><span class="sxs-lookup"><span data-stu-id="7bdf0-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="7bdf0-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="7bdf0-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="7bdf0-129">Indirizzo IP per l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="7bdf0-129">IP address for the next hop</span></span> |<span data-ttu-id="7bdf0-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="7bdf0-130">192.168.1.4</span></span> |

<span data-ttu-id="7bdf0-131">Tabella di route di esempio in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="7bdf0-131">Sample route table in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="7bdf0-132">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7bdf0-132">Additional resources</span></span>
* <span data-ttu-id="7bdf0-133">Altre informazioni sulle [route definite dall'utente](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7bdf0-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="7bdf0-134">Leggere [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) per le tabelle di route.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="7bdf0-135">Leggere [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) per le route definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="7bdf0-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

