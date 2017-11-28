## <a name="network-security-group"></a><span data-ttu-id="67e05-101">Gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="67e05-101">Network Security Group</span></span>
<span data-ttu-id="67e05-102">Una risorsa del gruppo di sicurezza di rete consente di creare un limite di sicurezza per i carichi di lavoro, implementando le regole di accesso consentito e negato.</span><span class="sxs-lookup"><span data-stu-id="67e05-102">An NSG resource enables the creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="67e05-103">Tali regole possono essere applicate a una macchina virtuale, una scheda di rete o una subnet.</span><span class="sxs-lookup"><span data-stu-id="67e05-103">Such rules can be applied to a VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="67e05-104">Proprietà</span><span class="sxs-lookup"><span data-stu-id="67e05-104">Property</span></span> | <span data-ttu-id="67e05-105">Descrizione</span><span class="sxs-lookup"><span data-stu-id="67e05-105">Description</span></span> | <span data-ttu-id="67e05-106">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="67e05-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67e05-107">**subnet**</span><span class="sxs-lookup"><span data-stu-id="67e05-107">**subnets**</span></span> |<span data-ttu-id="67e05-108">Elenco di ID subnet a cui è collegato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="67e05-108">List of subnet ids the NSG is applied to.</span></span> |<span data-ttu-id="67e05-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="67e05-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="67e05-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="67e05-110">**securityRules**</span></span> |<span data-ttu-id="67e05-111">Elenco di regole di sicurezza che costituiscono il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="67e05-111">List of security rules that make up the NSG</span></span> |<span data-ttu-id="67e05-112">Vedere [Regola di sicurezza](#Security-rule) di seguito</span><span class="sxs-lookup"><span data-stu-id="67e05-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="67e05-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="67e05-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="67e05-114">Elenco delle regole di sicurezza predefinite presenti in ogni gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="67e05-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="67e05-115">Vedere [Regole di sicurezza predefinite](#Default-security-rules) di seguito</span><span class="sxs-lookup"><span data-stu-id="67e05-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="67e05-116">**Regola di sicurezza** : in un gruppo di sicurezza di rete possono essere definite più regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="67e05-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="67e05-117">Ogni regola può consentire o negare diversi tipi di traffico.</span><span class="sxs-lookup"><span data-stu-id="67e05-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="67e05-118">Regola di sicurezza</span><span class="sxs-lookup"><span data-stu-id="67e05-118">Security rule</span></span>
<span data-ttu-id="67e05-119">Una regola di sicurezza è una risorsa figlio di un gruppo di sicurezza di rete contenente le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="67e05-119">A security rule is a child resource of an NSG containing the properties below.</span></span>

| <span data-ttu-id="67e05-120">Proprietà</span><span class="sxs-lookup"><span data-stu-id="67e05-120">Property</span></span> | <span data-ttu-id="67e05-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="67e05-121">Description</span></span> | <span data-ttu-id="67e05-122">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="67e05-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67e05-123">**description**</span><span class="sxs-lookup"><span data-stu-id="67e05-123">**description**</span></span> |<span data-ttu-id="67e05-124">Descrizione della regola</span><span class="sxs-lookup"><span data-stu-id="67e05-124">Description for the rule</span></span> |<span data-ttu-id="67e05-125">Consentire il traffico in ingresso per tutte le macchine virtuali nella subnet X</span><span class="sxs-lookup"><span data-stu-id="67e05-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="67e05-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="67e05-126">**protocol**</span></span> |<span data-ttu-id="67e05-127">Protocollo per la regola</span><span class="sxs-lookup"><span data-stu-id="67e05-127">Protocol to match for the rule</span></span> |<span data-ttu-id="67e05-128">TCP, UDP o *</span><span class="sxs-lookup"><span data-stu-id="67e05-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="67e05-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="67e05-129">**sourcePortRange**</span></span> |<span data-ttu-id="67e05-130">Intervallo di porte di origine per la regola</span><span class="sxs-lookup"><span data-stu-id="67e05-130">Source port range to match for the rule</span></span> |<span data-ttu-id="67e05-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="67e05-131">80, 100-200, *</span></span> |
| <span data-ttu-id="67e05-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="67e05-132">**destinationPortRange**</span></span> |<span data-ttu-id="67e05-133">Intervallo di porte di destinazione per la regola</span><span class="sxs-lookup"><span data-stu-id="67e05-133">Destination port range to match for the rule</span></span> |<span data-ttu-id="67e05-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="67e05-134">80, 100-200, *</span></span> |
| <span data-ttu-id="67e05-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="67e05-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="67e05-136">Prefisso dell'indirizzo di origine per la regola</span><span class="sxs-lookup"><span data-stu-id="67e05-136">Source address prefix to match for the rule</span></span> |<span data-ttu-id="67e05-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="67e05-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="67e05-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="67e05-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="67e05-139">Prefisso dell'indirizzo di destinazione per la regola</span><span class="sxs-lookup"><span data-stu-id="67e05-139">Destination address prefix to match for the rule</span></span> |<span data-ttu-id="67e05-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="67e05-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="67e05-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="67e05-141">**direction**</span></span> |<span data-ttu-id="67e05-142">Direzione del traffico per la regola</span><span class="sxs-lookup"><span data-stu-id="67e05-142">Direction of traffic to match for the rule</span></span> |<span data-ttu-id="67e05-143">in ingresso o in uscita</span><span class="sxs-lookup"><span data-stu-id="67e05-143">inbound or outbound</span></span> |
| <span data-ttu-id="67e05-144">**priority**</span><span class="sxs-lookup"><span data-stu-id="67e05-144">**priority**</span></span> |<span data-ttu-id="67e05-145">Priorità per la regola.</span><span class="sxs-lookup"><span data-stu-id="67e05-145">Priority for the rule.</span></span> <span data-ttu-id="67e05-146">Le regole vengono controllate nell'ordine di priorità. Una volta che viene applicata una regola, non viene verificata la corrispondenza di altre regole.</span><span class="sxs-lookup"><span data-stu-id="67e05-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="67e05-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="67e05-147">10, 100, 65000</span></span> |
| <span data-ttu-id="67e05-148">**access**</span><span class="sxs-lookup"><span data-stu-id="67e05-148">**access**</span></span> |<span data-ttu-id="67e05-149">Tipo di accesso da applicare se la regola corrisponde</span><span class="sxs-lookup"><span data-stu-id="67e05-149">Type of access to apply if the rule matches</span></span> |<span data-ttu-id="67e05-150">consentire o negare</span><span class="sxs-lookup"><span data-stu-id="67e05-150">allow or deny</span></span> |

<span data-ttu-id="67e05-151">Gruppo di sicurezza di rete di esempio in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="67e05-151">Sample NSG in JSON format:</span></span>

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

### <a name="default-security-rules"></a><span data-ttu-id="67e05-152">Regole di sicurezza predefinite</span><span class="sxs-lookup"><span data-stu-id="67e05-152">Default security rules</span></span>

<span data-ttu-id="67e05-153">Le regole di sicurezza predefinite hanno le stesse proprietà disponibili nelle regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="67e05-153">Default security rules have the same properties available in security rules.</span></span> <span data-ttu-id="67e05-154">Esistono per fornire la connettività di base tra le risorse a cui sono applicati gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="67e05-154">They exist to provide basic connectivity between resources that have NSGs applied to them.</span></span> <span data-ttu-id="67e05-155">Assicurarsi di conoscere le [regole di sicurezza predefinite](../articles/virtual-network/virtual-networks-nsg.md#default-rules) esistenti.</span><span class="sxs-lookup"><span data-stu-id="67e05-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="67e05-156">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="67e05-156">Additional resources</span></span>
* <span data-ttu-id="67e05-157">Altre informazioni sui [gruppi di sicurezza di rete](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="67e05-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="67e05-158">Leggere [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) per i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="67e05-158">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="67e05-159">Leggere [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) per le regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="67e05-159">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
