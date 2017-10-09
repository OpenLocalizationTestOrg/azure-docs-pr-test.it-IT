---
title: -i gruppi di sicurezza di rete aaaManage 1.0 CLI di Azure | Documenti Microsoft
description: Informazioni su come gruppi di sicurezza di rete toomanage utilizzando hello Azure interfaccia della riga di comando (CLI) 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="0d40b-103">Gestire gruppi di sicurezza di rete utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0d40b-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0d40b-104">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="0d40b-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="0d40b-105">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="0d40b-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="0d40b-106">[Azure CLI 1.0](#View-existing-NSGs) – la CLI per hello classic e risorse Gestione modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="0d40b-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="0d40b-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="0d40b-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="0d40b-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0d40b-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0d40b-109">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="0d40b-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="0d40b-110">Recuperare le informazioni</span><span class="sxs-lookup"><span data-stu-id="0d40b-110">Retrieve Information</span></span>
<span data-ttu-id="0d40b-111">È possibile visualizzare i gruppi di sicurezza di rete (NSG, Network Security Group) esistenti, recuperare le regole relative a un NSG esistente e trovare le risorse a cui un NSG è associato.</span><span class="sxs-lookup"><span data-stu-id="0d40b-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="0d40b-112">Visualizzare NSG esistenti</span><span class="sxs-lookup"><span data-stu-id="0d40b-112">View existing NSGs</span></span>
<span data-ttu-id="0d40b-113">elenco di hello tooview di NSGs in un gruppo di risorse specifico, eseguire hello `azure network nsg list` comando come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d40b-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="0d40b-114">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="0d40b-115">Elencare tutte le regole per un NSG</span><span class="sxs-lookup"><span data-stu-id="0d40b-115">List all rules for an NSG</span></span>
<span data-ttu-id="0d40b-116">le regole di hello tooview di un gruppo denominato **front-end di NSG**hello eseguire `azure network nsg show` comando come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d40b-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="0d40b-117">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="0d40b-118">È inoltre possibile utilizzare `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` regole hello toolist hello **front-end di NSG** gruppo.</span><span class="sxs-lookup"><span data-stu-id="0d40b-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="0d40b-119">Visualizzare le associazioni di NSG</span><span class="sxs-lookup"><span data-stu-id="0d40b-119">View NSG associations</span></span>

<span data-ttu-id="0d40b-120">tooview hello quali risorse **front-end di NSG** NSG è associato alla, eseguire hello `azure network nsg show` comando come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d40b-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="0d40b-121">Si noti che hello solo differenza è utilizzare hello di hello **- json** parametro.</span><span class="sxs-lookup"><span data-stu-id="0d40b-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="0d40b-122">Cercare hello **networkInterfaces** e **subnet** proprietà come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0d40b-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="0d40b-123">Nell'esempio hello sopra, hello gruppo non è associata tooany interfacce di rete (NIC) ed è associato tooa subnet denominata **front-end**.</span><span class="sxs-lookup"><span data-stu-id="0d40b-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="0d40b-124">Gestire le regole</span><span class="sxs-lookup"><span data-stu-id="0d40b-124">Manage rules</span></span>
<span data-ttu-id="0d40b-125">È possibile aggiungere regole tooan gruppo esistente, modificare le regole esistenti e rimuovere le regole.</span><span class="sxs-lookup"><span data-stu-id="0d40b-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="0d40b-126">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="0d40b-126">Add a rule</span></span>
<span data-ttu-id="0d40b-127">tooadd una regola che concede **in ingresso** traffico tooport **443** da qualsiasi toohello macchina **front-end di NSG** NSG, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d40b-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="0d40b-128">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="0d40b-129">Modificare una regola</span><span class="sxs-lookup"><span data-stu-id="0d40b-129">Change a rule</span></span>
<span data-ttu-id="0d40b-130">regola di hello toochange creato in precedenza tooallow il traffico da hello in ingresso **Internet** solo, eseguire hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="0d40b-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="0d40b-131">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="0d40b-132">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="0d40b-132">Delete a rule</span></span>
<span data-ttu-id="0d40b-133">regola di hello toodelete creato in precedenza, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d40b-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="0d40b-134">Hello `--quiet` parametro assicura che non è necessario l'eliminazione di hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="0d40b-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="0d40b-135">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="0d40b-136">Gestire le associazioni</span><span class="sxs-lookup"><span data-stu-id="0d40b-136">Manage associations</span></span>
<span data-ttu-id="0d40b-137">È possibile associare un gruppo toosubnets e schede di rete.</span><span class="sxs-lookup"><span data-stu-id="0d40b-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="0d40b-138">È anche possibile annullare l'associazione tra un NSG e qualsiasi risorsa a cui è associato.</span><span class="sxs-lookup"><span data-stu-id="0d40b-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="0d40b-139">Associare un tooa gruppo NIC</span><span class="sxs-lookup"><span data-stu-id="0d40b-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="0d40b-140">hello tooassociate **front-end di NSG** NSG toohello **TestNICWeb1** NIC, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d40b-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="0d40b-141">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="0d40b-142">Annullare l'associazione tra un NSG e una NIC</span><span class="sxs-lookup"><span data-stu-id="0d40b-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="0d40b-143">hello toodissociate **front-end di NSG** NSG da hello **TestNICWeb1** NIC, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d40b-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="0d40b-144">Hello avviso "" valore (vuoto) per hello `network-security-group-id` parametro.</span><span class="sxs-lookup"><span data-stu-id="0d40b-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="0d40b-145">Che è la modalità di rimozione di un gruppo di tooan di associazione.</span><span class="sxs-lookup"><span data-stu-id="0d40b-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="0d40b-146">Non è possibile eseguire hello stesso con hello `network-security-group-name` parametro.</span><span class="sxs-lookup"><span data-stu-id="0d40b-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="0d40b-147">Risultato previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="0d40b-148">Annullare l'associazione tra un NSG e una subnet</span><span class="sxs-lookup"><span data-stu-id="0d40b-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="0d40b-149">hello toodissociate **front-end di NSG** NSG da hello **front-end** subnet, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d40b-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="0d40b-150">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="0d40b-151">Associare una subnet tooa NSG</span><span class="sxs-lookup"><span data-stu-id="0d40b-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="0d40b-152">hello tooassociate **front-end di NSG** NSG toohello **FronEnd** subnet eseguito nuovamente, hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d40b-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="0d40b-153">Hello comando precedente funziona solo perché hello **front-end di NSG** gruppo si trova in hello stesso gruppo di risorse di rete virtuale hello **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="0d40b-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="0d40b-154">Se hello gruppo si trova in un gruppo di risorse diverso, è necessario hello toouse `--network-security-group-id` parametro invece e fornire l'id completo hello per hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="0d40b-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="0d40b-155">È possibile recuperare l'id di hello eseguendo `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` e cercando hello **id** proprietà.</span><span class="sxs-lookup"><span data-stu-id="0d40b-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="0d40b-156">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="0d40b-157">Eliminare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="0d40b-157">Delete an NSG</span></span>
<span data-ttu-id="0d40b-158">È possibile eliminare un gruppo solo se non è associata la risorsa tooany.</span><span class="sxs-lookup"><span data-stu-id="0d40b-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="0d40b-159">un gruppo, toodelete procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="0d40b-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="0d40b-160">risorse di hello toocheck associati tooan NSG, eseguire hello `azure network nsg show` come illustrato nella [NSGs visualizzazione associazioni](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="0d40b-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="0d40b-161">Se hello NSG è associato tooany schede di rete, eseguire hello `azure network nic set` come illustrato nella [annullare l'associazione di un gruppo da una scheda di rete](#Dissociate-an-NSG-from-a-NIC) per ogni scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="0d40b-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="0d40b-162">Se hello gruppo subnet tooany associate, eseguire hello `azure network vnet subnet set` come illustrato nella [annullare l'associazione di un gruppo da una subnet](#Dissociate-an-NSG-from-a-subnet) per ogni subnet.</span><span class="sxs-lookup"><span data-stu-id="0d40b-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="0d40b-163">hello toodelete NSG, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d40b-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="0d40b-164">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0d40b-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="0d40b-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d40b-165">Next steps</span></span>
* <span data-ttu-id="0d40b-166">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.</span><span class="sxs-lookup"><span data-stu-id="0d40b-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

