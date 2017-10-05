---
title: Gestire i gruppi di sicurezza di rete - interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Informazioni su come gestire i gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11ec0d3d9e33c06d4c0a164f7fba5dd5cca73872
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="82639-103">Gestire i gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="82639-103">Manage network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="82639-104">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="82639-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="82639-105">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="82639-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="82639-106">[Interfaccia della riga di comando di Azure 1.0](virtual-network-manage-nsg-cli-nodejs.md): l'interfaccia della riga di comando per i modelli di distribuzione classici e di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="82639-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="82639-107">[Interfaccia della riga di comando di Azure 2.0](#View-existing-NSGs): interfaccia avanzata per il modello di distribuzione di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="82639-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for the resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="82639-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="82639-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="82639-109">Questo articolo illustra l'uso del modello di distribuzione Resource Manager che Microsoft consiglia di usare invece del modello di distribuzione classica per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="82639-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="82639-110">Prerequisito</span><span class="sxs-lookup"><span data-stu-id="82639-110">Prerequisite</span></span>
<span data-ttu-id="82639-111">Se questa operazione non è stata ancora eseguita, installare e configurare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account Azure usando il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="82639-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="82639-112">Visualizzare NSG esistenti</span><span class="sxs-lookup"><span data-stu-id="82639-112">View existing NSGs</span></span>
<span data-ttu-id="82639-113">Per visualizzare l'elenco di gruppi di sicurezza di rete in un gruppo di risorse specifico, eseguire il comando [az network nsg list](/cli/azure/network/nsg#list) con un formato di output `-o table`:</span><span class="sxs-lookup"><span data-stu-id="82639-113">To view the list of NSGs in a specific resource group, run the [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="82639-114">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="82639-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="82639-115">Elencare tutte le regole per un NSG</span><span class="sxs-lookup"><span data-stu-id="82639-115">List all rules for an NSG</span></span>
<span data-ttu-id="82639-116">Per visualizzare le regole di un gruppo di sicurezza di rete denominato **NSG-FrontEnd**, eseguire il comando [az network nsg show](/cli/azure/network/nsg#show) usando il [filtro di query JMESPATH](/cli/azure/query-az-cli2) e il formato di output `-o table`:</span><span class="sxs-lookup"><span data-stu-id="82639-116">To view the rules of an NSG named **NSG-FrontEnd**, run the [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and the `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="82639-117">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="82639-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs to all VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs to Internet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="82639-118">È possibile anche usare [az network nsg rule list](/cli/azure/network/nsg/rule#list) per elencare solo le regole personalizzate da un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="82639-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) to list only the custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="82639-119">Visualizzare le associazioni di NSG</span><span class="sxs-lookup"><span data-stu-id="82639-119">View NSG associations</span></span>

<span data-ttu-id="82639-120">Per visualizzare le risorse a cui l'NSG **NSG-FrontEnd** è associato, eseguire il comando `az network nsg show` come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="82639-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="82639-121">Cercare le proprietà **networkInterfaces** e **subnets** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="82639-121">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="82639-122">Nell'esempio precedente, l'NSG non è associato ad alcuna interfaccia di rete (NIC) ed è associato a una subnet denominata **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="82639-122">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="82639-123">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="82639-123">Add a rule</span></span>
<span data-ttu-id="82639-124">Per aggiungere una regola che consenta il traffico **in ingresso** alla porta **443** da qualsiasi computer all'NSG **NSG-FrontEnd**, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82639-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access to port 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="82639-125">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="82639-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access to port 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="82639-126">Modificare una regola</span><span class="sxs-lookup"><span data-stu-id="82639-126">Change a rule</span></span>
<span data-ttu-id="82639-127">Per modificare la regola creata in precedenza per consentire solo il traffico in ingresso da **Internet**, eseguire il comando [az network nsg rule update](/cli/azure/network/nsg/rule#update) come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="82639-127">To change the rule created above to allow inbound traffic from the **Internet** only, run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="82639-128">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="82639-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access to port 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="82639-129">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="82639-129">Delete a rule</span></span>
<span data-ttu-id="82639-130">Per eliminare la regola creata in precedenza, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82639-130">To delete the rule created above, run the following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="82639-131">Associare un NSG a una NIC</span><span class="sxs-lookup"><span data-stu-id="82639-131">Associate an NSG to a NIC</span></span>
<span data-ttu-id="82639-132">Per associare il gruppo di sicurezza di rete **NSG-FrontEnd** alla scheda di interfaccia di rete **TestNICWeb1**, eseguire il comando [az network nic update](/cli/azure/network/nic#update):</span><span class="sxs-lookup"><span data-stu-id="82639-132">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, use the [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="82639-133">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="82639-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="82639-134">Annullare l'associazione tra un NSG e una NIC</span><span class="sxs-lookup"><span data-stu-id="82639-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="82639-135">Per annullare l'associazione del gruppo di sicurezza di rete **NSG-FrontEnd** dalla scheda di interfaccia di rete **TestNICWeb1** eseguire di nuovo il comando [az network nsg rule update](/cli/azure/network/nsg/rule#update) ma sostituire l'argomento `--network-security-group` con una stringa vuota (`""`).</span><span class="sxs-lookup"><span data-stu-id="82639-135">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace the `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="82639-136">Nell'output la chiave `networkSecurityGroup` è impostata su null.</span><span class="sxs-lookup"><span data-stu-id="82639-136">In the output, the `networkSecurityGroup` key is set to null.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="82639-137">Annullare l'associazione tra un NSG e una subnet</span><span class="sxs-lookup"><span data-stu-id="82639-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="82639-138">Per annullare l'associazione del gruppo di sicurezza di rete **NSG-FrontEnd** dalla subnet **FrontEnd** eseguire il comando [az network nsg rule update](/cli/azure/network/nsg/rule#update), ma sostituire l'argomento `--network-security-group` con una stringa vuota (`""`).</span><span class="sxs-lookup"><span data-stu-id="82639-138">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, again run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace the `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="82639-139">Nell'output la chiave `networkSecurityGroup` è impostata su null.</span><span class="sxs-lookup"><span data-stu-id="82639-139">In the output, the `networkSecurityGroup` key is set to null.</span></span>

## <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="82639-140">Associare un gruppo di sicurezza di rete a una subnet</span><span class="sxs-lookup"><span data-stu-id="82639-140">Associate an NSG to a subnet</span></span>
<span data-ttu-id="82639-141">Per associare di nuovo il gruppo di sicurezza di rete **NSG-FrontEnd** alla subnet **FrontEnd**, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82639-141">To associate the **NSG-FrontEnd** NSG to the **FrontEnd** subnet again, run the following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="82639-142">Nell'output il valore della chiave `networkSecurityGroup` è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="82639-142">In the output, the `networkSecurityGroup` key has something similar for the value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="82639-143">Eliminare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="82639-143">Delete an NSG</span></span>
<span data-ttu-id="82639-144">È possibile eliminare un NSG solo se non è associato ad alcuna risorsa.</span><span class="sxs-lookup"><span data-stu-id="82639-144">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="82639-145">Per eliminare un NSG, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="82639-145">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="82639-146">Per controllare le risorse associate a un NSG, eseguire `azure network nsg show` come illustrato in [Visualizzare le associazioni di NSG](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="82639-146">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="82639-147">Se l'NSG è associato a una o più NIC, eseguire `azure network nic set` come illustrato in [Annullare l'associazione tra un NSG e una NIC](#Dissociate-an-NSG-from-a-NIC) per ognuna delle NIC.</span><span class="sxs-lookup"><span data-stu-id="82639-147">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="82639-148">Se l'NSG è associato a una o più subnet, eseguire `azure network vnet subnet set` come illustrato in [Annullare l'associazione tra un NSG e una subnet](#Dissociate-an-NSG-from-a-subnet) per ognuna delle subnet.</span><span class="sxs-lookup"><span data-stu-id="82639-148">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="82639-149">Per eliminare l'NSG, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82639-149">To delete the NSG, run the following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="82639-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82639-150">Next steps</span></span>
* <span data-ttu-id="82639-151">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.</span><span class="sxs-lookup"><span data-stu-id="82639-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

