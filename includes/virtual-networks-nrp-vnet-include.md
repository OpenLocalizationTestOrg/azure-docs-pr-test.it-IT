## <a name="virtual-network"></a><span data-ttu-id="d6b89-101">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d6b89-101">Virtual Network</span></span>
<span data-ttu-id="d6b89-102">Le reti virtuali e le risorse subnet consentono di definire un limite di sicurezza per i carichi di lavoro in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="d6b89-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="d6b89-103">Una rete virtuale è caratterizzata da una raccolta di spazi di indirizzi, definiti come blocchi CIDR.</span><span class="sxs-lookup"><span data-stu-id="d6b89-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="d6b89-104">Gli amministratori di rete hanno familiarità con la notazione CIDR.</span><span class="sxs-lookup"><span data-stu-id="d6b89-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="d6b89-105">Se non si ha familiarità con CIDR, è possibile [ottenere maggiori informazioni](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="d6b89-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Reti virtuali con più subnet](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="d6b89-107">Le reti virtuali contengono hello le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="d6b89-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="d6b89-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d6b89-108">Property</span></span> | <span data-ttu-id="d6b89-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6b89-109">Description</span></span> | <span data-ttu-id="d6b89-110">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="d6b89-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6b89-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="d6b89-111">**addressSpace**</span></span> |<span data-ttu-id="d6b89-112">Raccolta di prefissi di indirizzo che costituiscono hello rete virtuale nella notazione CIDR</span><span class="sxs-lookup"><span data-stu-id="d6b89-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="d6b89-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d6b89-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="d6b89-114">**subnet**</span><span class="sxs-lookup"><span data-stu-id="d6b89-114">**subnets**</span></span> |<span data-ttu-id="d6b89-115">Raccolta di subnet che costituiscono hello rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d6b89-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="d6b89-116">vedere [subnet](#Subnets) di seguito.</span><span class="sxs-lookup"><span data-stu-id="d6b89-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="d6b89-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="d6b89-117">**ipAddress**</span></span> |<span data-ttu-id="d6b89-118">Indirizzo IP assegnato tooobject.</span><span class="sxs-lookup"><span data-stu-id="d6b89-118">IP address assigned tooobject.</span></span> <span data-ttu-id="d6b89-119">La proprietà è di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="d6b89-119">This is a read-only property.</span></span> |<span data-ttu-id="d6b89-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="d6b89-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="d6b89-121">Subnet</span><span class="sxs-lookup"><span data-stu-id="d6b89-121">Subnets</span></span>
<span data-ttu-id="d6b89-122">Una subnet è una risorsa figlio di una rete virtuale e consente di definire i segmenti degli spazi di indirizzi all'interno di un blocco CIDR, usando i prefissi degli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="d6b89-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="d6b89-123">Schede di rete possono essere aggiunte toosubnets e tooVMs connesso, fornisce la connettività per diversi carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d6b89-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="d6b89-124">Subnet contengono hello le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="d6b89-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="d6b89-125">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d6b89-125">Property</span></span> | <span data-ttu-id="d6b89-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6b89-126">Description</span></span> | <span data-ttu-id="d6b89-127">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="d6b89-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6b89-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="d6b89-128">**addressPrefix**</span></span> |<span data-ttu-id="d6b89-129">Singolo prefisso di indirizzo di subnet hello in notazione CIDR</span><span class="sxs-lookup"><span data-stu-id="d6b89-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="d6b89-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="d6b89-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="d6b89-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="d6b89-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="d6b89-132">Subnet toohello NSG applicato</span><span class="sxs-lookup"><span data-stu-id="d6b89-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="d6b89-133">vedere [NSG](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="d6b89-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="d6b89-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="d6b89-134">**routeTable**</span></span> |<span data-ttu-id="d6b89-135">Tabella di route applicato toohello subnet</span><span class="sxs-lookup"><span data-stu-id="d6b89-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="d6b89-136">vedere [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="d6b89-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="d6b89-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="d6b89-137">**ipConfigurations**</span></span> |<span data-ttu-id="d6b89-138">Raccolta di oggetti di configurazione IP usati da schede di rete connessa toohello subnet</span><span class="sxs-lookup"><span data-stu-id="d6b89-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="d6b89-139">vedere [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="d6b89-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="d6b89-140">Rete virtuale di esempio in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="d6b89-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="d6b89-141">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d6b89-141">Additional resources</span></span>
* <span data-ttu-id="d6b89-142">Altre informazioni sulle [reti virtuali](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6b89-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="d6b89-143">Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="d6b89-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="d6b89-144">Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) per subnet.</span><span class="sxs-lookup"><span data-stu-id="d6b89-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

