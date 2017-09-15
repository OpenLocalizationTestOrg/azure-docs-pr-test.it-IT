## <a name="virtual-network"></a><span data-ttu-id="6ab45-101">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6ab45-101">Virtual Network</span></span>
<span data-ttu-id="6ab45-102">Le reti virtuali e le risorse subnet consentono di definire un limite di sicurezza per i carichi di lavoro in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab45-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="6ab45-103">Una rete virtuale è caratterizzata da una raccolta di spazi di indirizzi, definiti come blocchi CIDR.</span><span class="sxs-lookup"><span data-stu-id="6ab45-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="6ab45-104">Gli amministratori di rete hanno familiarità con la notazione CIDR.</span><span class="sxs-lookup"><span data-stu-id="6ab45-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="6ab45-105">Se non si ha familiarità con CIDR, è possibile [ottenere maggiori informazioni](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="6ab45-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Reti virtuali con più subnet](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="6ab45-107">Le reti virtuali contengono le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="6ab45-107">VNets contain the following properties.</span></span>

| <span data-ttu-id="6ab45-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6ab45-108">Property</span></span> | <span data-ttu-id="6ab45-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ab45-109">Description</span></span> | <span data-ttu-id="6ab45-110">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="6ab45-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ab45-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="6ab45-111">**addressSpace**</span></span> |<span data-ttu-id="6ab45-112">Raccolta di prefissi di indirizzi che costituiscono la rete virtuale nella notazione CIDR</span><span class="sxs-lookup"><span data-stu-id="6ab45-112">Collection of address prefixes that make up the VNet in CIDR notation</span></span> |<span data-ttu-id="6ab45-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6ab45-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="6ab45-114">**subnet**</span><span class="sxs-lookup"><span data-stu-id="6ab45-114">**subnets**</span></span> |<span data-ttu-id="6ab45-115">Raccolta di subnet che costituiscono la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6ab45-115">Collection of subnets that make up the VNet</span></span> |<span data-ttu-id="6ab45-116">vedere [subnet](#Subnets) di seguito.</span><span class="sxs-lookup"><span data-stu-id="6ab45-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="6ab45-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="6ab45-117">**ipAddress**</span></span> |<span data-ttu-id="6ab45-118">Indirizzo IP assegnato all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="6ab45-118">IP address assigned to object.</span></span> <span data-ttu-id="6ab45-119">La proprietà è di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="6ab45-119">This is a read-only property.</span></span> |<span data-ttu-id="6ab45-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="6ab45-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="6ab45-121">Subnet</span><span class="sxs-lookup"><span data-stu-id="6ab45-121">Subnets</span></span>
<span data-ttu-id="6ab45-122">Una subnet è una risorsa figlio di una rete virtuale e consente di definire i segmenti degli spazi di indirizzi all'interno di un blocco CIDR, usando i prefissi degli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="6ab45-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="6ab45-123">Le NIC possono essere aggiunte alle subnet e connesse alle macchine virtuali, fornendo connettività per diversi carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6ab45-123">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="6ab45-124">Le subnet contengono le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="6ab45-124">Subnets contain the following properties.</span></span> 

| <span data-ttu-id="6ab45-125">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6ab45-125">Property</span></span> | <span data-ttu-id="6ab45-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ab45-126">Description</span></span> | <span data-ttu-id="6ab45-127">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="6ab45-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ab45-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="6ab45-128">**addressPrefix**</span></span> |<span data-ttu-id="6ab45-129">Singolo prefisso di indirizzo che costituisce la subnet nella notazione CIDR</span><span class="sxs-lookup"><span data-stu-id="6ab45-129">Single address prefix that make up the subnet in CIDR notation</span></span> |<span data-ttu-id="6ab45-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="6ab45-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="6ab45-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="6ab45-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="6ab45-132">NSG applicato alla subnet</span><span class="sxs-lookup"><span data-stu-id="6ab45-132">NSG applied to the subnet</span></span> |<span data-ttu-id="6ab45-133">vedere [NSG](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="6ab45-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="6ab45-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="6ab45-134">**routeTable**</span></span> |<span data-ttu-id="6ab45-135">Tabella di route applicata alla subnet</span><span class="sxs-lookup"><span data-stu-id="6ab45-135">Route table applied to the subnet</span></span> |<span data-ttu-id="6ab45-136">vedere [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="6ab45-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="6ab45-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="6ab45-137">**ipConfigurations**</span></span> |<span data-ttu-id="6ab45-138">Raccolta di oggetti di configurazione IP usati dalle schede di rete connesse alla subnet</span><span class="sxs-lookup"><span data-stu-id="6ab45-138">Collection of IP configruation objects used by NICs connected to the subnet</span></span> |<span data-ttu-id="6ab45-139">vedere [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="6ab45-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="6ab45-140">Rete virtuale di esempio in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="6ab45-140">Sample VNet in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="6ab45-141">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6ab45-141">Additional resources</span></span>
* <span data-ttu-id="6ab45-142">Altre informazioni sulle [reti virtuali](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ab45-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="6ab45-143">Leggere [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6ab45-143">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="6ab45-144">Leggere [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) per le subnet.</span><span class="sxs-lookup"><span data-stu-id="6ab45-144">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

