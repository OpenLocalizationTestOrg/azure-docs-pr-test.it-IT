---
title: Gestire i gruppi di sicurezza di rete - Azure PowerShell | Documentazione Microsoft
description: Informazioni su come gestire i gruppi di sicurezza di rete mediante PowerShell.
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
ms.openlocfilehash: ca7f4926ca4edf9d20612aca74f6ae5f0ed847b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="bd755-103">Gestire i gruppi di sicurezza di rete mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd755-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="bd755-104">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd755-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bd755-105">Questo articolo illustra l'uso del modello di distribuzione Resource Manager che Microsoft consiglia di usare invece del modello di distribuzione classica per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="bd755-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="bd755-106">Recuperare le informazioni</span><span class="sxs-lookup"><span data-stu-id="bd755-106">Retrieve Information</span></span>
<span data-ttu-id="bd755-107">È possibile visualizzare i gruppi di sicurezza di rete (NSG, Network Security Group) esistenti, recuperare le regole relative a un NSG esistente e trovare le risorse a cui un NSG è associato.</span><span class="sxs-lookup"><span data-stu-id="bd755-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="bd755-108">Visualizzare NSG esistenti</span><span class="sxs-lookup"><span data-stu-id="bd755-108">View existing NSGs</span></span>
<span data-ttu-id="bd755-109">Per visualizzare tutti gli NSG esistenti in una sottoscrizione, eseguire il cmdlet `Get-AzureRmNetworkSecurityGroup`.</span><span class="sxs-lookup"><span data-stu-id="bd755-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="bd755-110">Risultato previsto:</span><span class="sxs-lookup"><span data-stu-id="bd755-110">Expected result:</span></span>

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


<span data-ttu-id="bd755-111">Per visualizzare l'elenco di NSG in un gruppo di risorse specifico, eseguire il cmdlet `Get-AzureRmNetworkSecurityGroup`.</span><span class="sxs-lookup"><span data-stu-id="bd755-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="bd755-112">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="bd755-112">Expected output:</span></span>

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

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="bd755-113">Elencare tutte le regole per un NSG</span><span class="sxs-lookup"><span data-stu-id="bd755-113">List all rules for an NSG</span></span>
<span data-ttu-id="bd755-114">Per visualizzare le regole di un NSG denominato **NSG-FrontEnd**, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="bd755-115">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="bd755-115">Expected output:</span></span>

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
> <span data-ttu-id="bd755-116">Per elencare le regole predefinite dell'NSG **NSG-FrontEnd**, è anche possibile usare `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules`.</span><span class="sxs-lookup"><span data-stu-id="bd755-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="bd755-117">Visualizzare le associazioni di NSG</span><span class="sxs-lookup"><span data-stu-id="bd755-117">View NSGs associations</span></span>
<span data-ttu-id="bd755-118">Per visualizzare le risorse a cui l'NSG **NSG-FrontEnd** è associato, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="bd755-119">Cercare le proprietà **NetworkInterfaces** e **Subnets** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="bd755-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="bd755-120">Nell'esempio precedente, l'NSG non è associato ad alcuna interfaccia di rete (NIC), ma è associato a una subnet denominata **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="bd755-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="bd755-121">Gestire le regole</span><span class="sxs-lookup"><span data-stu-id="bd755-121">Manage rules</span></span>
<span data-ttu-id="bd755-122">È possibile aggiungere regole a un NSG esistente, modificare le regole esistenti e rimuovere regole.</span><span class="sxs-lookup"><span data-stu-id="bd755-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="bd755-123">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="bd755-123">Add a rule</span></span>
<span data-ttu-id="bd755-124">Per aggiungere una regola che consenta il traffico **in ingresso** alla porta **443** da qualsiasi computer all'NSG **NSG-FrontEnd**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd755-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="bd755-125">Eseguire il comando seguente per recuperare l'NSG esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-125">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="bd755-126">Eseguire il comando seguente per aggiungere una regola all'NSG:</span><span class="sxs-lookup"><span data-stu-id="bd755-126">Run the following command to add a rule to the NSG:</span></span>

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

3. <span data-ttu-id="bd755-127">Per salvare le modifiche apportate all'NSG, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-127">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="bd755-128">Output previsto che mostra solo le regole di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="bd755-128">Expected output showing only the security rules:</span></span>
   
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

### <a name="change-a-rule"></a><span data-ttu-id="bd755-129">Modificare una regola</span><span class="sxs-lookup"><span data-stu-id="bd755-129">Change a rule</span></span>
<span data-ttu-id="bd755-130">Per modificare la regola creata in precedenza per consentire traffico in ingresso solo da **Internet** , attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="bd755-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span></span>

1. <span data-ttu-id="bd755-131">Eseguire il comando seguente per recuperare l'NSG esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-131">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="bd755-132">Eseguire il comando seguente con le nuove impostazioni di regola:</span><span class="sxs-lookup"><span data-stu-id="bd755-132">Run the following command with the new rule settings:</span></span>

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

3. <span data-ttu-id="bd755-133">Per salvare le modifiche apportate all'NSG, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-133">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="bd755-134">Output previsto che mostra solo le regole di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="bd755-134">Expected output showing only the security rules:</span></span>
   
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

### <a name="delete-a-rule"></a><span data-ttu-id="bd755-135">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="bd755-135">Delete a rule</span></span>
1. <span data-ttu-id="bd755-136">Eseguire il comando seguente per recuperare l'NSG esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-136">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="bd755-137">Eseguire il comando seguente per rimuovere la regola dall'NSG:</span><span class="sxs-lookup"><span data-stu-id="bd755-137">Run the following command to remove the rule from the NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="bd755-138">Per salvare le modifiche apportate all'NSG, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-138">Save the changes made to the NSG, by running the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="bd755-139">Output previsto che mostra solo le regole di sicurezza. Si noti che **https-rule** non è più presente:</span><span class="sxs-lookup"><span data-stu-id="bd755-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span></span>
   
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

## <a name="manage-associations"></a><span data-ttu-id="bd755-140">Gestire le associazioni</span><span class="sxs-lookup"><span data-stu-id="bd755-140">Manage associations</span></span>
<span data-ttu-id="bd755-141">È possibile associare un NSG a subnet e schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="bd755-141">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="bd755-142">È anche possibile annullare l'associazione tra un NSG e qualsiasi risorsa a cui è associato.</span><span class="sxs-lookup"><span data-stu-id="bd755-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="bd755-143">Associare un NSG a una NIC</span><span class="sxs-lookup"><span data-stu-id="bd755-143">Associate an NSG to a NIC</span></span>
<span data-ttu-id="bd755-144">Per associare l'NSG **NSG-FrontEnd** alla NIC **TestNICWeb1**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd755-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="bd755-145">Eseguire il comando seguente per recuperare l'NSG esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-145">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="bd755-146">Eseguire il comando seguente per recuperare la NIC esistente e archiviarla in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-146">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="bd755-147">Impostare la proprietà **NetworkSecurityGroup** della variabile **NIC** sul valore della variabile **NSG** immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="bd755-148">Per salvare le modifiche apportate alla NIC, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-148">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="bd755-149">Output previsto che mostra solo la proprietà **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="bd755-149">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="bd755-150">Annullare l'associazione tra un NSG e una NIC</span><span class="sxs-lookup"><span data-stu-id="bd755-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="bd755-151">Per annullare l'associazione tra l'NSG **NSG-FrontEnd** e la NIC **TestNICWeb1**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd755-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="bd755-152">Eseguire il comando seguente per recuperare la NIC esistente e archiviarla in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-152">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="bd755-153">Impostare la proprietà **NetworkSecurityGroup** della variabile **NIC** su **$null** eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="bd755-154">Per salvare le modifiche apportate alla NIC, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-154">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="bd755-155">Output previsto che mostra solo la proprietà **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="bd755-155">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="bd755-156">Annullare l'associazione tra un NSG e una subnet</span><span class="sxs-lookup"><span data-stu-id="bd755-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="bd755-157">Per annullare l'associazione tra l'NSG **NSG-FrontEnd** e la subnet **FrontEnd**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd755-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="bd755-158">Eseguire il comando seguente per recuperare la rete virtuale esistente e archiviarla in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-158">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="bd755-159">Eseguire il comando seguente per recuperare la subnet **FrontEnd** e archiviarla in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="bd755-160">Impostare la proprietà **NetworkSecurityGroup** della variabile **subnet** su **$null** immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="bd755-161">Per salvare le modifiche apportate alla subnet, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-161">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="bd755-162">Output previsto che mostra solo le proprietà della subnet **FrontEnd** .</span><span class="sxs-lookup"><span data-stu-id="bd755-162">Expected output showing only the properties of the **FrontEnd** subnet.</span></span> <span data-ttu-id="bd755-163">Si noti che non esiste una proprietà per **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="bd755-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
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

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="bd755-164">Associare un gruppo di sicurezza di rete a una subnet</span><span class="sxs-lookup"><span data-stu-id="bd755-164">Associate an NSG to a subnet</span></span>
<span data-ttu-id="bd755-165">Per associare di nuovo l'NSG **NSG-FrontEnd** alla subnet **FronEnd**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd755-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="bd755-166">Eseguire il comando seguente per recuperare la rete virtuale esistente e archiviarla in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-166">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="bd755-167">Eseguire il comando seguente per recuperare la subnet **FrontEnd** e archiviarla in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="bd755-168">Eseguire il comando seguente per recuperare l'NSG esistente e archiviarlo in una variabile:</span><span class="sxs-lookup"><span data-stu-id="bd755-168">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="bd755-169">Impostare la proprietà **NetworkSecurityGroup** della variabile **subnet** su **$null** eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="bd755-170">Per salvare le modifiche apportate alla subnet, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-170">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="bd755-171">Output previsto che mostra solo la proprietà **NetworkSecurityGroup** della subnet **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="bd755-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="bd755-172">Eliminare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="bd755-172">Delete an NSG</span></span>
<span data-ttu-id="bd755-173">È possibile eliminare un NSG solo se non è associato ad alcuna risorsa.</span><span class="sxs-lookup"><span data-stu-id="bd755-173">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="bd755-174">Per eliminare un NSG, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="bd755-174">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="bd755-175">Per controllare le risorse associate a un NSG, eseguire `azure network nsg show` come illustrato in [Visualizzare le associazioni di NSG](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="bd755-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="bd755-176">Se l'NSG è associato a una o più NIC, eseguire `azure network nic set` come illustrato in [Annullare l'associazione tra un NSG e una NIC](#Dissociate-an-NSG-from-a-NIC) per ognuna delle NIC.</span><span class="sxs-lookup"><span data-stu-id="bd755-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="bd755-177">Se l'NSG è associato a una o più subnet, eseguire `azure network vnet subnet set` come illustrato in [Annullare l'associazione tra un NSG e una subnet](#Dissociate-an-NSG-from-a-subnet) per ognuna delle subnet.</span><span class="sxs-lookup"><span data-stu-id="bd755-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="bd755-178">Per eliminare l'NSG, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bd755-178">To delete the NSG, run the following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="bd755-179">Il parametro `-Force` fa in modo che non sia necessario confermare l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="bd755-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="bd755-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd755-180">Next steps</span></span>
* <span data-ttu-id="bd755-181">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.</span><span class="sxs-lookup"><span data-stu-id="bd755-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

