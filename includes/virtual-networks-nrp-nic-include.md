## <a name="nic"></a><span data-ttu-id="33dbb-101">NIC</span><span class="sxs-lookup"><span data-stu-id="33dbb-101">NIC</span></span>
<span data-ttu-id="33dbb-102">La scheda di interfaccia di rete (o NIC) è una risorsa che fornisce la connettività di rete a una subnet esistente in una risorsa di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="33dbb-102">A network interface card (NIC) resource provides network connectivity to an existing subnet in a VNet resource.</span></span> <span data-ttu-id="33dbb-103">Sebbene sia possibile creare una scheda di interfaccia di rete come oggetto autonomo, è necessario associarla a un altro oggetto per fornire davvero la connettività.</span><span class="sxs-lookup"><span data-stu-id="33dbb-103">Although you can create a NIC as a stand alone object, you need to associate it to another object to actually provide connectivity.</span></span> <span data-ttu-id="33dbb-104">Una scheda di interfaccia di rete può essere usata per la connessione di una macchina virtuale a una subnet, a un indirizzo IP pubblico o a un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="33dbb-104">A NIC can be used to connect a VM to a subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="33dbb-105">Proprietà</span><span class="sxs-lookup"><span data-stu-id="33dbb-105">Property</span></span> | <span data-ttu-id="33dbb-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="33dbb-106">Description</span></span> | <span data-ttu-id="33dbb-107">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="33dbb-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33dbb-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="33dbb-108">**virtualMachine**</span></span> |<span data-ttu-id="33dbb-109">VM alla quale è associata la scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="33dbb-109">VM the NIC is associated with.</span></span> |<span data-ttu-id="33dbb-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="33dbb-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="33dbb-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="33dbb-111">**macAddress**</span></span> |<span data-ttu-id="33dbb-112">Indirizzo MAC della scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="33dbb-112">MAC address for the NIC</span></span> |<span data-ttu-id="33dbb-113">qualsiasi valore compreso tra 4 e 30.</span><span class="sxs-lookup"><span data-stu-id="33dbb-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="33dbb-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="33dbb-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="33dbb-115">Gruppo di sicurezza di rete associato alla scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="33dbb-115">NSG associated to the NIC</span></span> |<span data-ttu-id="33dbb-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="33dbb-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="33dbb-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="33dbb-117">**dnsSettings**</span></span> |<span data-ttu-id="33dbb-118">Impostazioni DNS della scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="33dbb-118">DNS settings for the NIC</span></span> |<span data-ttu-id="33dbb-119">vedere [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="33dbb-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="33dbb-120">La scheda di interfaccia di rete, o NIC, rappresenta un'interfaccia di rete che è possibile associare a una macchina virtuale (VM).</span><span class="sxs-lookup"><span data-stu-id="33dbb-120">A Network Interface Card, or NIC, represents a network interface that can be associated to a virtual machine (VM).</span></span> <span data-ttu-id="33dbb-121">Una macchina virtuale può avere una o più schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="33dbb-121">A VM can have one or more NICs.</span></span>

![Scheda di interfaccia di rete in una macchina virtuale singola](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="33dbb-123">Configurazioni IP</span><span class="sxs-lookup"><span data-stu-id="33dbb-123">IP configurations</span></span>
<span data-ttu-id="33dbb-124">Le schede di interfaccia di rete dispongono di un oggetto figlio denominato **ipConfigurations** contenente le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="33dbb-124">NICs have a child object named **ipConfigurations** containing the following properties:</span></span>

| <span data-ttu-id="33dbb-125">Proprietà</span><span class="sxs-lookup"><span data-stu-id="33dbb-125">Property</span></span> | <span data-ttu-id="33dbb-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="33dbb-126">Description</span></span> | <span data-ttu-id="33dbb-127">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="33dbb-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33dbb-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="33dbb-128">**subnet**</span></span> |<span data-ttu-id="33dbb-129">Subnet alla quale è connessa la scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="33dbb-129">Subnet the NIC is onnected to.</span></span> |<span data-ttu-id="33dbb-130">/Subscriptions/{GUID}/../microsoft.Network/virtualNetworks/myvnet1/Subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="33dbb-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="33dbb-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="33dbb-131">**privateIPAddress**</span></span> |<span data-ttu-id="33dbb-132">Indirizzo IP della scheda di interfaccia di rete nella subnet</span><span class="sxs-lookup"><span data-stu-id="33dbb-132">IP address for the NIC in the subnet</span></span> |<span data-ttu-id="33dbb-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="33dbb-133">10.0.0.8</span></span> |
| <span data-ttu-id="33dbb-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="33dbb-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="33dbb-135">Metodo di allocazione degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="33dbb-135">IP allocation method</span></span> |<span data-ttu-id="33dbb-136">Dinamico o statico</span><span class="sxs-lookup"><span data-stu-id="33dbb-136">Dynamic or Static</span></span> |
| <span data-ttu-id="33dbb-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="33dbb-137">**enableIPForwarding**</span></span> |<span data-ttu-id="33dbb-138">Indica se la scheda di interfaccia di rete può essere usata per il routing</span><span class="sxs-lookup"><span data-stu-id="33dbb-138">Whether the NIC can be used for routing</span></span> |<span data-ttu-id="33dbb-139">true o false</span><span class="sxs-lookup"><span data-stu-id="33dbb-139">true or false</span></span> |
| <span data-ttu-id="33dbb-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="33dbb-140">**primary**</span></span> |<span data-ttu-id="33dbb-141">Indica se la scheda di interfaccia di rete è la scheda primaria per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="33dbb-141">Whether the NIC is the primary NIC for the VM</span></span> |<span data-ttu-id="33dbb-142">true o false</span><span class="sxs-lookup"><span data-stu-id="33dbb-142">true or false</span></span> |
| <span data-ttu-id="33dbb-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="33dbb-143">**publicIPAddress**</span></span> |<span data-ttu-id="33dbb-144">Indirizzo PIP associato alla scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="33dbb-144">PIP associated with the NIC</span></span> |<span data-ttu-id="33dbb-145">vedere [Impostazioni DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="33dbb-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="33dbb-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="33dbb-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="33dbb-147">Pool di indirizzi di back-end associati alla scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="33dbb-147">Back end address pools the NIC is associated with</span></span> | |
| <span data-ttu-id="33dbb-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="33dbb-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="33dbb-149">Regole NAT del servizio di bilanciamento del carico in ingresso associate alla scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="33dbb-149">Inbound load balancer NAT rules the NIC is associated with</span></span> | |

<span data-ttu-id="33dbb-150">Indirizzo IP pubblico di esempio in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="33dbb-150">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="33dbb-151">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="33dbb-151">Additional resources</span></span>
* <span data-ttu-id="33dbb-152">Leggere [la documentazione di riferimento API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) per schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="33dbb-152">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

