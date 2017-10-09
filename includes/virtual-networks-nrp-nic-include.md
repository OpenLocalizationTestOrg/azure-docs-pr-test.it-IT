## <a name="nic"></a><span data-ttu-id="ba36f-101">NIC</span><span class="sxs-lookup"><span data-stu-id="ba36f-101">NIC</span></span>
<span data-ttu-id="ba36f-102">Una risorsa di scheda di interfaccia rete fornisce una subnet esistente tooan connettività di rete in una risorsa di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ba36f-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="ba36f-103">Sebbene sia possibile creare una scheda di rete come oggetto autonomo, è necessario tooassociate è tooanother oggetto tooactually fornisce la connettività.</span><span class="sxs-lookup"><span data-stu-id="ba36f-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="ba36f-104">Una scheda di rete può essere utilizzato tooconnect tooa subnet VM, un indirizzo IP pubblico o un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ba36f-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="ba36f-105">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ba36f-105">Property</span></span> | <span data-ttu-id="ba36f-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ba36f-106">Description</span></span> | <span data-ttu-id="ba36f-107">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="ba36f-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba36f-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="ba36f-108">**virtualMachine**</span></span> |<span data-ttu-id="ba36f-109">Hello VM NIC è associato.</span><span class="sxs-lookup"><span data-stu-id="ba36f-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="ba36f-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="ba36f-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="ba36f-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="ba36f-111">**macAddress**</span></span> |<span data-ttu-id="ba36f-112">Indirizzo MAC per hello NIC</span><span class="sxs-lookup"><span data-stu-id="ba36f-112">MAC address for hello NIC</span></span> |<span data-ttu-id="ba36f-113">qualsiasi valore compreso tra 4 e 30.</span><span class="sxs-lookup"><span data-stu-id="ba36f-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="ba36f-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="ba36f-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="ba36f-115">Toohello associata gruppo NIC</span><span class="sxs-lookup"><span data-stu-id="ba36f-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="ba36f-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="ba36f-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="ba36f-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="ba36f-117">**dnsSettings**</span></span> |<span data-ttu-id="ba36f-118">Impostazioni DNS per hello NIC</span><span class="sxs-lookup"><span data-stu-id="ba36f-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="ba36f-119">vedere [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="ba36f-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="ba36f-120">Una scheda di interfaccia di rete o scheda di rete, rappresenta un'interfaccia di rete che può essere associati tooa virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="ba36f-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="ba36f-121">Una macchina virtuale può avere una o più schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="ba36f-121">A VM can have one or more NICs.</span></span>

![Scheda di interfaccia di rete in una macchina virtuale singola](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="ba36f-123">Configurazioni IP</span><span class="sxs-lookup"><span data-stu-id="ba36f-123">IP configurations</span></span>
<span data-ttu-id="ba36f-124">Schede di rete dispone di un oggetto figlio denominato **configurazioni IP** contenente hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba36f-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="ba36f-125">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ba36f-125">Property</span></span> | <span data-ttu-id="ba36f-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ba36f-126">Description</span></span> | <span data-ttu-id="ba36f-127">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="ba36f-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba36f-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="ba36f-128">**subnet**</span></span> |<span data-ttu-id="ba36f-129">Hello subnet scheda di rete è connessa a.</span><span class="sxs-lookup"><span data-stu-id="ba36f-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="ba36f-130">/Subscriptions/{GUID}/../microsoft.Network/virtualNetworks/myvnet1/Subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="ba36f-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="ba36f-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="ba36f-131">**privateIPAddress**</span></span> |<span data-ttu-id="ba36f-132">Indirizzo IP per subnet hello Ciao NIC</span><span class="sxs-lookup"><span data-stu-id="ba36f-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="ba36f-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="ba36f-133">10.0.0.8</span></span> |
| <span data-ttu-id="ba36f-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="ba36f-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="ba36f-135">Metodo di allocazione degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="ba36f-135">IP allocation method</span></span> |<span data-ttu-id="ba36f-136">Dinamico o statico</span><span class="sxs-lookup"><span data-stu-id="ba36f-136">Dynamic or Static</span></span> |
| <span data-ttu-id="ba36f-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="ba36f-137">**enableIPForwarding**</span></span> |<span data-ttu-id="ba36f-138">Se è possibile utilizzare per il routing hello NIC</span><span class="sxs-lookup"><span data-stu-id="ba36f-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="ba36f-139">true o false</span><span class="sxs-lookup"><span data-stu-id="ba36f-139">true or false</span></span> |
| <span data-ttu-id="ba36f-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="ba36f-140">**primary**</span></span> |<span data-ttu-id="ba36f-141">Se è hello NIC hello schede di rete primaria per hello VM</span><span class="sxs-lookup"><span data-stu-id="ba36f-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="ba36f-142">true o false</span><span class="sxs-lookup"><span data-stu-id="ba36f-142">true or false</span></span> |
| <span data-ttu-id="ba36f-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="ba36f-143">**publicIPAddress**</span></span> |<span data-ttu-id="ba36f-144">PIP associato hello NIC</span><span class="sxs-lookup"><span data-stu-id="ba36f-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="ba36f-145">vedere [Impostazioni DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="ba36f-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="ba36f-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="ba36f-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="ba36f-147">Eseguire il backup hello pool di indirizzi fine A che NIC è associata</span><span class="sxs-lookup"><span data-stu-id="ba36f-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="ba36f-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="ba36f-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="ba36f-149">Connessioni in entrata hello regole NAT bilanciamento di carico A che NIC è associata</span><span class="sxs-lookup"><span data-stu-id="ba36f-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="ba36f-150">Indirizzo IP pubblico di esempio in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="ba36f-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="ba36f-151">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ba36f-151">Additional resources</span></span>
* <span data-ttu-id="ba36f-152">Hello lettura [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) per schede di rete.</span><span class="sxs-lookup"><span data-stu-id="ba36f-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

