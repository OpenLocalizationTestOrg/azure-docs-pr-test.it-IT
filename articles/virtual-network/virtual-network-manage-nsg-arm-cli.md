---
title: -i gruppi di sicurezza di rete aaaManage 2.0 CLI di Azure | Documenti Microsoft
description: Informazioni su come gruppi di sicurezza di rete toomanage utilizzando hello Azure interfaccia della riga di comando (CLI) 2.0.
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
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="cc7f9-103">Gestire gruppi di sicurezza di rete utilizzando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cc7f9-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="cc7f9-104">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="cc7f9-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="cc7f9-105">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="cc7f9-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="cc7f9-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="cc7f9-107">[Azure CLI 2.0](#View-existing-NSGs) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="cc7f9-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="cc7f9-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cc7f9-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cc7f9-109">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="cc7f9-110">Prerequisito</span><span class="sxs-lookup"><span data-stu-id="cc7f9-110">Prerequisite</span></span>
<span data-ttu-id="cc7f9-111">Se non hai ancora, installare e configurare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="cc7f9-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="cc7f9-112">Visualizzare NSG esistenti</span><span class="sxs-lookup"><span data-stu-id="cc7f9-112">View existing NSGs</span></span>
<span data-ttu-id="cc7f9-113">elenco di hello tooview di NSGs in un gruppo di risorse specifico, eseguire hello [elenco gruppo di rete az](/cli/azure/network/nsg#list) comando con un `-o table` formato di output:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="cc7f9-114">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="cc7f9-115">Elencare tutte le regole per un NSG</span><span class="sxs-lookup"><span data-stu-id="cc7f9-115">List all rules for an NSG</span></span>
<span data-ttu-id="cc7f9-116">le regole di hello tooview di un gruppo denominato **front-end di NSG**hello eseguire [Mostra nsg di rete az](/cli/azure/network/nsg#show) comando mediante un [filtro query JMESPATH](/cli/azure/query-az-cli2) hello e `-o table` formato di output:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="cc7f9-117">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="cc7f9-118">È inoltre possibile utilizzare [elenco delle regole az rete nsg](/cli/azure/network/nsg/rule#list) toolist solo hello regole personalizzate di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="cc7f9-119">Visualizzare le associazioni di NSG</span><span class="sxs-lookup"><span data-stu-id="cc7f9-119">View NSG associations</span></span>

<span data-ttu-id="cc7f9-120">tooview hello quali risorse **front-end di NSG** NSG è associato alla, eseguire hello `az network nsg show` comando come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="cc7f9-121">Cercare hello **networkInterfaces** e **subnet** proprietà come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

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

<span data-ttu-id="cc7f9-122">Nell'esempio hello sopra, hello gruppo non è associata tooany interfacce di rete (NIC) ed è associato tooa subnet denominata **front-end**.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="cc7f9-123">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="cc7f9-123">Add a rule</span></span>
<span data-ttu-id="cc7f9-124">tooadd una regola che concede **in ingresso** traffico tooport **443** da qualsiasi toohello macchina **front-end di NSG** NSG, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="cc7f9-125">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
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

## <a name="change-a-rule"></a><span data-ttu-id="cc7f9-126">Modificare una regola</span><span class="sxs-lookup"><span data-stu-id="cc7f9-126">Change a rule</span></span>
<span data-ttu-id="cc7f9-127">regola di hello toochange creato in precedenza tooallow il traffico da hello in ingresso **Internet** solo eseguire hello [aggiornamento regola gruppo di rete az](/cli/azure/network/nsg/rule#update) comando:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="cc7f9-128">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
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

## <a name="delete-a-rule"></a><span data-ttu-id="cc7f9-129">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="cc7f9-129">Delete a rule</span></span>
<span data-ttu-id="cc7f9-130">regola di hello toodelete creato in precedenza, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="cc7f9-131">Associare un tooa gruppo NIC</span><span class="sxs-lookup"><span data-stu-id="cc7f9-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="cc7f9-132">hello tooassociate **front-end di NSG** NSG toohello **TestNICWeb1** NIC, utilizzare hello [aggiornamento nic di rete az](/cli/azure/network/nic#update) comando:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="cc7f9-133">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-133">Expected output:</span></span>

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

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="cc7f9-134">Annullare l'associazione tra un NSG e una NIC</span><span class="sxs-lookup"><span data-stu-id="cc7f9-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="cc7f9-135">hello toodissociate **front-end di NSG** NSG da hello **TestNICWeb1** NIC, eseguire hello [aggiornamento regola gruppo di rete az](/cli/azure/network/nsg/rule#update) comando nuovamente ma sostituire hello `--network-security-group` argomento con una stringa vuota (`""`).</span><span class="sxs-lookup"><span data-stu-id="cc7f9-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="cc7f9-136">Nell'output di hello hello `networkSecurityGroup` chiave toonull è impostata.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="cc7f9-137">Annullare l'associazione tra un NSG e una subnet</span><span class="sxs-lookup"><span data-stu-id="cc7f9-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="cc7f9-138">hello toodissociate **front-end di NSG** NSG da hello **front-end** subnet, eseguire di nuovo hello [aggiornamento regola gruppo di rete az](/cli/azure/network/nsg/rule#update) comando nuovamente ma sostituire hello `--network-security-group` argomento con una stringa vuota (`""`).</span><span class="sxs-lookup"><span data-stu-id="cc7f9-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="cc7f9-139">Nell'output di hello hello `networkSecurityGroup` chiave toonull è impostata.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="cc7f9-140">Associare una subnet tooa NSG</span><span class="sxs-lookup"><span data-stu-id="cc7f9-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="cc7f9-141">hello tooassociate **front-end di NSG** NSG toohello **front-end** subnet eseguito nuovamente, hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="cc7f9-142">Nell'output di hello hello `networkSecurityGroup` chiave ha un comportamento simile per valore hello:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

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

## <a name="delete-an-nsg"></a><span data-ttu-id="cc7f9-143">Eliminare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="cc7f9-143">Delete an NSG</span></span>
<span data-ttu-id="cc7f9-144">È possibile eliminare un gruppo solo se non è associata la risorsa tooany.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="cc7f9-145">un gruppo, toodelete procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="cc7f9-146">risorse di hello toocheck associati tooan NSG, eseguire hello `azure network nsg show` come illustrato nella [NSGs visualizzazione associazioni](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="cc7f9-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="cc7f9-147">Se hello NSG è associato tooany schede di rete, eseguire hello `azure network nic set` come illustrato nella [annullare l'associazione di un gruppo da una scheda di rete](#Dissociate-an-NSG-from-a-NIC) per ogni scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="cc7f9-148">Se hello gruppo subnet tooany associate, eseguire hello `azure network vnet subnet set` come illustrato nella [annullare l'associazione di un gruppo da una subnet](#Dissociate-an-NSG-from-a-subnet) per ogni subnet.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="cc7f9-149">hello toodelete NSG, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cc7f9-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="cc7f9-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc7f9-150">Next steps</span></span>
* <span data-ttu-id="cc7f9-151">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.</span><span class="sxs-lookup"><span data-stu-id="cc7f9-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

