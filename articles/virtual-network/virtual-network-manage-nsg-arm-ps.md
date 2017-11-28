---
title: -i gruppi di sicurezza di rete aaaManage Azure PowerShell | Documenti Microsoft
description: Informazioni su come toomanage rete gruppi di sicurezza tramite PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="77599-103">Gestire i gruppi di sicurezza di rete mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="77599-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="77599-104">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="77599-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="77599-105">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="77599-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="77599-106">Recuperare le informazioni</span><span class="sxs-lookup"><span data-stu-id="77599-106">Retrieve Information</span></span>
<span data-ttu-id="77599-107">È possibile visualizzare i gruppi di sicurezza di rete (NSG, Network Security Group) esistenti, recuperare le regole relative a un NSG esistente e trovare le risorse a cui un NSG è associato.</span><span class="sxs-lookup"><span data-stu-id="77599-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="77599-108">Visualizzare NSG esistenti</span><span class="sxs-lookup"><span data-stu-id="77599-108">View existing NSGs</span></span>
<span data-ttu-id="77599-109">tooview tutti NSGs esistente in una sottoscrizione, eseguire hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="77599-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="77599-110">Risultato previsto:</span><span class="sxs-lookup"><span data-stu-id="77599-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="77599-111">elenco di hello tooview di NSGs in un gruppo di risorse specifico, eseguire hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="77599-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="77599-112">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="77599-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="77599-113">Elencare tutte le regole per un NSG</span><span class="sxs-lookup"><span data-stu-id="77599-113">List all rules for an NSG</span></span>
<span data-ttu-id="77599-114">le regole di hello tooview di un gruppo denominato **front-end di NSG**, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="77599-115">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="77599-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="77599-116">È inoltre possibile utilizzare `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` regole predefinite di hello toolist da hello **front-end di NSG** gruppo.</span><span class="sxs-lookup"><span data-stu-id="77599-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="77599-117">Visualizzare le associazioni di NSG</span><span class="sxs-lookup"><span data-stu-id="77599-117">View NSGs associations</span></span>
<span data-ttu-id="77599-118">tooview hello quali risorse **front-end di NSG** NSG è associato alla, hello esecuzione comando riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="77599-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="77599-119">Cercare hello **NetworkInterfaces** e **subnet** proprietà come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="77599-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="77599-120">Nell'esempio precedente hello hello gruppo non è associato tooany interfacce di rete (NIC); è associato tooa subnet denominata **front-end**.</span><span class="sxs-lookup"><span data-stu-id="77599-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="77599-121">Gestire le regole</span><span class="sxs-lookup"><span data-stu-id="77599-121">Manage rules</span></span>
<span data-ttu-id="77599-122">È possibile aggiungere regole tooan gruppo esistente, modificare le regole esistenti e rimuovere le regole.</span><span class="sxs-lookup"><span data-stu-id="77599-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="77599-123">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="77599-123">Add a rule</span></span>
<span data-ttu-id="77599-124">tooadd una regola che concede **in ingresso** traffico tooport **443** da qualsiasi toohello macchina **front-end di NSG** NSG, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="77599-125">Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="77599-126">Eseguire hello successivo comando tooadd toohello una regola gruppo:</span><span class="sxs-lookup"><span data-stu-id="77599-126">Run hello following command tooadd a rule toohello NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="77599-127">toosave hello modifiche toohello NSG, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="77599-128">Output previsto con hello solo le regole di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="77599-128">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="77599-129">Modificare una regola</span><span class="sxs-lookup"><span data-stu-id="77599-129">Change a rule</span></span>
<span data-ttu-id="77599-130">regola di hello toochange creato in precedenza tooallow il traffico da hello in ingresso **Internet** solo, seguire i passaggi di hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="77599-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="77599-131">Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="77599-132">Eseguire hello comando con le nuove impostazioni regola hello seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-132">Run hello following command with hello new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="77599-133">toosave hello modifiche toohello NSG, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="77599-134">Output previsto con hello solo le regole di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="77599-134">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="77599-135">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="77599-135">Delete a rule</span></span>
1. <span data-ttu-id="77599-136">Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="77599-137">Comando che segue di hello esecuzione regola hello tooremove da hello gruppo:</span><span class="sxs-lookup"><span data-stu-id="77599-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="77599-138">Salvare le modifiche apportate di hello toohello NSG, eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="77599-139">Output previsto con hello solo regole di sicurezza, si noti hello **regola https** non viene più elencata:</span><span class="sxs-lookup"><span data-stu-id="77599-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="77599-140">Gestire le associazioni</span><span class="sxs-lookup"><span data-stu-id="77599-140">Manage associations</span></span>
<span data-ttu-id="77599-141">È possibile associare un gruppo toosubnets e schede di rete.</span><span class="sxs-lookup"><span data-stu-id="77599-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="77599-142">È anche possibile annullare l'associazione tra un NSG e qualsiasi risorsa a cui è associato.</span><span class="sxs-lookup"><span data-stu-id="77599-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="77599-143">Associare un tooa gruppo NIC</span><span class="sxs-lookup"><span data-stu-id="77599-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="77599-144">hello tooassociate **front-end di NSG** NSG toohello **TestNICWeb1** NIC, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="77599-145">Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="77599-146">Eseguire hello successivo comando tooretrieve hello esistente NIC e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="77599-147">Set hello **sicurezza di rete** proprietà di hello **NIC** valore variabile toohello hello **NSG** variabile, immettendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="77599-148">toosave hello modifiche toohello NIC, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="77599-149">Hello solo di output previsto con **sicurezza di rete** proprietà:</span><span class="sxs-lookup"><span data-stu-id="77599-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="77599-150">Annullare l'associazione tra un NSG e una NIC</span><span class="sxs-lookup"><span data-stu-id="77599-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="77599-151">hello toodissociate **front-end di NSG** NSG da hello **TestNICWeb1** NIC, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="77599-152">Eseguire hello successivo comando tooretrieve hello esistente NIC e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="77599-153">Set hello **sicurezza di rete** proprietà di hello **NIC** variabile troppo**$null** eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="77599-154">toosave hello modifiche toohello NIC, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="77599-155">Hello solo di output previsto con **sicurezza di rete** proprietà:</span><span class="sxs-lookup"><span data-stu-id="77599-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="77599-156">Annullare l'associazione tra un NSG e una subnet</span><span class="sxs-lookup"><span data-stu-id="77599-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="77599-157">hello toodissociate **front-end di NSG** NSG da hello **front-end** subnet, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="77599-158">Eseguire hello successivo comando tooretrieve hello esistente di rete virtuale e archiviarla in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="77599-159">Esecuzione hello seguenti comando tooretrieve hello **front-end** subnet e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="77599-160">Set hello **sicurezza di rete** proprietà di hello **subnet** variabile troppo**$null** immettendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="77599-161">toosave hello modifiche toohello subnet, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="77599-162">Output previsto mostrando solo le proprietà di hello di hello **front-end** subnet.</span><span class="sxs-lookup"><span data-stu-id="77599-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="77599-163">Si noti che non esiste una proprietà per **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="77599-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="77599-164">Associare una subnet tooa NSG</span><span class="sxs-lookup"><span data-stu-id="77599-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="77599-165">hello tooassociate **front-end di NSG** NSG toohello **FronEnd** subnet nuovamente, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="77599-166">Eseguire hello successivo comando tooretrieve hello esistente di rete virtuale e archiviarla in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="77599-167">Esecuzione hello seguenti comando tooretrieve hello **front-end** subnet e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="77599-168">Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="77599-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="77599-169">Set hello **sicurezza di rete** proprietà di hello **subnet** variabile troppo**$null** eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="77599-170">toosave hello modifiche toohello subnet, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="77599-171">Hello solo di output previsto con **sicurezza di rete** proprietà di hello **front-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="77599-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="77599-172">Eliminare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="77599-172">Delete an NSG</span></span>
<span data-ttu-id="77599-173">È possibile eliminare un gruppo solo se non è associata la risorsa tooany.</span><span class="sxs-lookup"><span data-stu-id="77599-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="77599-174">un gruppo, toodelete procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="77599-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="77599-175">risorse di hello toocheck associati tooan NSG, eseguire hello `azure network nsg show` come illustrato nella [NSGs visualizzazione associazioni](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="77599-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="77599-176">Se hello NSG è associato tooany schede di rete, eseguire hello `azure network nic set` come illustrato nella [annullare l'associazione di un gruppo da una scheda di rete](#Dissociate-an-NSG-from-a-NIC) per ogni scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="77599-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="77599-177">Se hello gruppo subnet tooany associate, eseguire hello `azure network vnet subnet set` come illustrato nella [annullare l'associazione di un gruppo da una subnet](#Dissociate-an-NSG-from-a-subnet) per ogni subnet.</span><span class="sxs-lookup"><span data-stu-id="77599-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="77599-178">hello toodelete NSG, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77599-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="77599-179">Hello `-Force` parametro assicura che non è necessario l'eliminazione di hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="77599-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="77599-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77599-180">Next steps</span></span>
* <span data-ttu-id="77599-181">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.</span><span class="sxs-lookup"><span data-stu-id="77599-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

