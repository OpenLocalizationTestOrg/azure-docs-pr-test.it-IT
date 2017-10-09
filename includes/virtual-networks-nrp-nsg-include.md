## <a name="network-security-group"></a><span data-ttu-id="68b79-101">Gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="68b79-101">Network Security Group</span></span>
<span data-ttu-id="68b79-102">Una risorsa di gruppo consente la creazione di hello del limite di sicurezza per i carichi di lavoro, implementando consentire e le regole di negazione.</span><span class="sxs-lookup"><span data-stu-id="68b79-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="68b79-103">Tali regole possono essere applicati tooa macchina virtuale, una scheda di rete o subnet.</span><span class="sxs-lookup"><span data-stu-id="68b79-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="68b79-104">Proprietà</span><span class="sxs-lookup"><span data-stu-id="68b79-104">Property</span></span> | <span data-ttu-id="68b79-105">Descrizione</span><span class="sxs-lookup"><span data-stu-id="68b79-105">Description</span></span> | <span data-ttu-id="68b79-106">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="68b79-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="68b79-107">**subnet**</span><span class="sxs-lookup"><span data-stu-id="68b79-107">**subnets**</span></span> |<span data-ttu-id="68b79-108">Elenco di ID di subnet hello gruppo viene applicato a.</span><span class="sxs-lookup"><span data-stu-id="68b79-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="68b79-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="68b79-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="68b79-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="68b79-110">**securityRules**</span></span> |<span data-ttu-id="68b79-111">Elenco di regole di sicurezza che costituiscono hello NSG</span><span class="sxs-lookup"><span data-stu-id="68b79-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="68b79-112">Vedere [Regola di sicurezza](#Security-rule) di seguito</span><span class="sxs-lookup"><span data-stu-id="68b79-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="68b79-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="68b79-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="68b79-114">Elenco delle regole di sicurezza predefinite presenti in ogni gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="68b79-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="68b79-115">Vedere [Regole di sicurezza predefinite](#Default-security-rules) di seguito</span><span class="sxs-lookup"><span data-stu-id="68b79-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="68b79-116">**Regola di sicurezza** : in un gruppo di sicurezza di rete possono essere definite più regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="68b79-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="68b79-117">Ogni regola può consentire o negare diversi tipi di traffico.</span><span class="sxs-lookup"><span data-stu-id="68b79-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="68b79-118">Regola di sicurezza</span><span class="sxs-lookup"><span data-stu-id="68b79-118">Security rule</span></span>
<span data-ttu-id="68b79-119">Una regola di sicurezza è una risorsa figlio di un gruppo che contiene proprietà hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="68b79-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="68b79-120">Proprietà</span><span class="sxs-lookup"><span data-stu-id="68b79-120">Property</span></span> | <span data-ttu-id="68b79-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="68b79-121">Description</span></span> | <span data-ttu-id="68b79-122">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="68b79-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="68b79-123">**description**</span><span class="sxs-lookup"><span data-stu-id="68b79-123">**description**</span></span> |<span data-ttu-id="68b79-124">Descrizione della regola hello</span><span class="sxs-lookup"><span data-stu-id="68b79-124">Description for hello rule</span></span> |<span data-ttu-id="68b79-125">Consentire il traffico in ingresso per tutte le macchine virtuali nella subnet X</span><span class="sxs-lookup"><span data-stu-id="68b79-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="68b79-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="68b79-126">**protocol**</span></span> |<span data-ttu-id="68b79-127">Protocollo toomatch per regola hello</span><span class="sxs-lookup"><span data-stu-id="68b79-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="68b79-128">TCP, UDP o *</span><span class="sxs-lookup"><span data-stu-id="68b79-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="68b79-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="68b79-129">**sourcePortRange**</span></span> |<span data-ttu-id="68b79-130">Toomatch intervallo porte di origine per la regola hello</span><span class="sxs-lookup"><span data-stu-id="68b79-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="68b79-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="68b79-131">80, 100-200, *</span></span> |
| <span data-ttu-id="68b79-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="68b79-132">**destinationPortRange**</span></span> |<span data-ttu-id="68b79-133">Toomatch intervallo porte di destinazione per la regola hello</span><span class="sxs-lookup"><span data-stu-id="68b79-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="68b79-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="68b79-134">80, 100-200, *</span></span> |
| <span data-ttu-id="68b79-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="68b79-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="68b79-136">Toomatch di prefisso di indirizzo di origine per la regola hello</span><span class="sxs-lookup"><span data-stu-id="68b79-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="68b79-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="68b79-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="68b79-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="68b79-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="68b79-139">Toomatch di prefisso di indirizzo di destinazione per la regola hello</span><span class="sxs-lookup"><span data-stu-id="68b79-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="68b79-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="68b79-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="68b79-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="68b79-141">**direction**</span></span> |<span data-ttu-id="68b79-142">Direzione del traffico toomatch per regola hello</span><span class="sxs-lookup"><span data-stu-id="68b79-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="68b79-143">in ingresso o in uscita</span><span class="sxs-lookup"><span data-stu-id="68b79-143">inbound or outbound</span></span> |
| <span data-ttu-id="68b79-144">**priority**</span><span class="sxs-lookup"><span data-stu-id="68b79-144">**priority**</span></span> |<span data-ttu-id="68b79-145">Priorità per la regola di hello.</span><span class="sxs-lookup"><span data-stu-id="68b79-145">Priority for hello rule.</span></span> <span data-ttu-id="68b79-146">Le regole vengono controllate nell'ordine di priorità. Una volta che viene applicata una regola, non viene verificata la corrispondenza di altre regole.</span><span class="sxs-lookup"><span data-stu-id="68b79-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="68b79-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="68b79-147">10, 100, 65000</span></span> |
| <span data-ttu-id="68b79-148">**access**</span><span class="sxs-lookup"><span data-stu-id="68b79-148">**access**</span></span> |<span data-ttu-id="68b79-149">Tipo di accesso tooapply se hello regola corrispondente</span><span class="sxs-lookup"><span data-stu-id="68b79-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="68b79-150">consentire o negare</span><span class="sxs-lookup"><span data-stu-id="68b79-150">allow or deny</span></span> |

<span data-ttu-id="68b79-151">Gruppo di sicurezza di rete di esempio in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="68b79-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="68b79-152">Regole di sicurezza predefinite</span><span class="sxs-lookup"><span data-stu-id="68b79-152">Default security rules</span></span>

<span data-ttu-id="68b79-153">Regole di sicurezza predefinite sono hello stesse proprietà disponibili nelle regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="68b79-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="68b79-154">Connettività di base tra le risorse che hanno applicato NSGs toothem tooprovide esistenti.</span><span class="sxs-lookup"><span data-stu-id="68b79-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="68b79-155">Assicurarsi di conoscere le [regole di sicurezza predefinite](../articles/virtual-network/virtual-networks-nsg.md#default-rules) esistenti.</span><span class="sxs-lookup"><span data-stu-id="68b79-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="68b79-156">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="68b79-156">Additional resources</span></span>
* <span data-ttu-id="68b79-157">Altre informazioni sui [gruppi di sicurezza di rete](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="68b79-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="68b79-158">Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) per NSGs.</span><span class="sxs-lookup"><span data-stu-id="68b79-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="68b79-159">Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) per le regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="68b79-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
