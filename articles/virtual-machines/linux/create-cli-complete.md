---
title: Creare un ambiente Linux tramite l'interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Usare l'interfaccia della riga di comando di Azure 2.0 per creare da zero una risorsa di archiviazione, una VM di Linux, una rete virtuale con subnet, il bilanciamento del carico, una scheda NIC, un IP pubblico e un gruppo di sicurezza di rete.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: e5c4785428b2150e951923e98079e00808a82d87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="8c6b5-103">Creare una macchina virtuale Linux completa con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8c6b5-103">Create a complete Linux virtual machine with the Azure CLI</span></span>
<span data-ttu-id="8c6b5-104">Per creare rapidamente una macchina virtuale in Azure, è possibile usare un singolo comando dell'interfaccia della riga di comando di Azure che si serve dei valori predefiniti per creare tutte le risorse di supporto richieste.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-104">To quickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values to create any required supporting resources.</span></span> <span data-ttu-id="8c6b5-105">Le risorse, ad esempio una rete virtuale, l'indirizzo IP pubblico e regole del gruppo di sicurezza di rete, vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="8c6b5-106">Per un maggiore controllo dell'ambiente di produzione è possibile creare queste risorse in anticipo e quindi aggiungervi le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs to them.</span></span> <span data-ttu-id="8c6b5-107">In questo articolo descrive come creare una macchina virtuale e tutte le risorse di supporto, una alla volta.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-107">This article guides you through how to create a VM and each of the supporting resources one by one.</span></span>

<span data-ttu-id="8c6b5-108">Verificare di avere installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e di avere eseguito la registrazione a un account di Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-108">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="8c6b5-109">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-109">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8c6b5-110">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="8c6b5-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8c6b5-111">Create resource group</span></span>
<span data-ttu-id="8c6b5-112">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="8c6b5-113">Il gruppo di risorse deve essere creato prima della macchina virtuale e delle risorse della rete virtuale di supporto.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="8c6b5-114">Creare il gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-114">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8c6b5-115">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8c6b5-116">Per impostazione predefinita, l'output del comando dell'interfaccia della riga di comando di Azure è in formato JSON, ovvero JavaScript Object Notation.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-116">By default, the output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="8c6b5-117">Per trasformare l'output predefinito in un elenco o in una tabella, ad esempio, usare [az configure --output](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-117">To change the default output to a list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="8c6b5-118">È possibile anche aggiungere `--output` a qualsiasi comando per apportare una modifica una sola volta nel formato di output.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-118">You can also add `--output` to any command for a one time change in output format.</span></span> <span data-ttu-id="8c6b5-119">L'esempio seguente illustra l'output JSON ottenuto dal comando `az group create`:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-119">The following example shows the JSON output from the `az group create` command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="8c6b5-120">Creare una rete virtuale e una subnet</span><span class="sxs-lookup"><span data-stu-id="8c6b5-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="8c6b5-121">Dopodiché è necessario creare una rete virtuale in Azure e una subnet in cui poter creare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-121">Next you create a virtual network in Azure and a subnet in to which you can create your VMs.</span></span> <span data-ttu-id="8c6b5-122">Usare [az network vnet create](/cli/azure/network/vnet#create) per creare una rete virtuale denominata *myVnet* con il prefisso dell'indirizzo *192.168.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-122">Use [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named *myVnet* with the *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="8c6b5-123">Aggiungere anche una subnet denominata *mySubnet* con un prefisso di indirizzo di *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-123">You also add a subnet named *mySubnet* with the address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="8c6b5-124">L'output mostra la subnet creata in modo logico all'interno della rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-124">The output shows the subnet as logically created inside the virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="8c6b5-125">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="8c6b5-125">Create a public IP address</span></span>
<span data-ttu-id="8c6b5-126">Creare ora un indirizzo IP pubblico con [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="8c6b5-127">L'indirizzo IP pubblico consente di connettersi alle macchine virtuali da Internet.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-127">This public IP address enables you to connect to your VMs from the Internet.</span></span> <span data-ttu-id="8c6b5-128">Poiché l'indirizzo predefinito è dinamico, è anche necessario creare una voce DNS denominata con l'opzione `--domain-name-label`.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-128">Because the default address is dynamic, we also create a named DNS entry with the `--domain-name-label` option.</span></span> <span data-ttu-id="8c6b5-129">L'esempio seguente crea un indirizzo IP pubblico chiamato *myPublicIP* con il nome DNS *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-129">The following example creates a public IP named *myPublicIP* with the DNS name of *mypublicdns*.</span></span> <span data-ttu-id="8c6b5-130">Dal momento che il nome DNS deve essere univoco, è necessario inserire il proprio nome DNS univoco:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-130">Because the DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="8c6b5-131">Output:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-131">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a><span data-ttu-id="8c6b5-132">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="8c6b5-132">Create a network security group</span></span>
<span data-ttu-id="8c6b5-133">Per controllare il flusso del traffico in ingresso e in uscita dalle macchine virtuali creare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-133">To control the flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="8c6b5-134">Per una scheda di interfaccia di rete o una subnet è possibile usare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-134">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="8c6b5-135">L'esempio seguente usa [az network nsg create](/cli/azure/network/nsg#create) per creare un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-135">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="8c6b5-136">È necessario definire le regole che consentono o bloccano un traffico specifico.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-136">You define rules that allow or deny the specific traffic.</span></span> <span data-ttu-id="8c6b5-137">Creare una regola in ingresso per il gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create) per consentire le connessioni in ingresso sulla porta 22, per supportare SSH.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-137">To allow inbound connections on port 22 (to support SSH), create an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="8c6b5-138">L'esempio seguente crea una regola denominata *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-138">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

<span data-ttu-id="8c6b5-139">Per consentire le connessioni in ingresso sulla porta 80, per supportare il traffico Web, aggiungere un'altra regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-139">To allow inbound connections on port 80 (to support web traffic), add another network security group rule.</span></span> <span data-ttu-id="8c6b5-140">L'esempio seguente crea una regola denominata *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-140">The following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="8c6b5-141">Esaminare il gruppo di sicurezza di rete e le regole con [az network nsg show](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="8c6b5-141">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="8c6b5-142">Output:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-142">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to Internet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a><span data-ttu-id="8c6b5-143">Creare una scheda di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8c6b5-143">Create a virtual NIC</span></span>
<span data-ttu-id="8c6b5-144">Le schede di interfaccia di rete virtuale sono disponibili a livello di programmazione in quanto è possibile applicare delle regole di uso.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="8c6b5-145">È inoltre possibile averne più di una.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-145">You can also have more than one.</span></span> <span data-ttu-id="8c6b5-146">Nel comando seguente [az network nic create](/cli/azure/network/nic#create) si crea una scheda di interfaccia di rete denominata *myNic* e la si associa al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-146">In the following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with the network security group.</span></span> <span data-ttu-id="8c6b5-147">L'indirizzo IP pubblico *myPublicIP* è associato anche a una scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-147">The public IP address *myPublicIP* is also associated with the virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="8c6b5-148">Output:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-148">Output:</span></span>

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a><span data-ttu-id="8c6b5-149">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="8c6b5-149">Create an availability set</span></span>
<span data-ttu-id="8c6b5-150">I set di disponibilità agevolano la distribuzione delle macchine virtuali nei domini di errore e nei domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="8c6b5-151">Anche se si crea una sola macchina virtuale al momento, è consigliabile usare i set di disponibilità in modo da semplificarne l'espansione in futuro.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-151">Even though you only create one VM right now, it's best practice to use availability sets to make it easier to expand in the future.</span></span> 

<span data-ttu-id="8c6b5-152">I domini di errore definiscono un gruppo di macchine virtuali che condividono una fonte di alimentazione e uno switch di rete comuni.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="8c6b5-153">Per impostazione predefinita, le macchine virtuali configurate nell'ambito di un set di disponibilità vengono suddivise tra un massimo di tre domini di errore.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-153">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="8c6b5-154">Un problema hardware in uno di questi domini di errore non influenza tutte le macchine virtuali che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="8c6b5-155">I domini di aggiornamento indicano gruppi di macchine virtuali e l'hardware fisico sottostante che possono essere riavviati nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="8c6b5-156">Durante la manutenzione pianificata, i domini di aggiornamento non vengono necessariamente riavviati in ordine sequenziale, ma ne viene riavviato uno solo alla volta.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-156">During planned maintenance, the order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="8c6b5-157">Azure distribuisce automaticamente le macchine virtuali tra i domini di errore e di aggiornamento durante il posizionamento in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-157">Azure automatically distributes VMs across the fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="8c6b5-158">Per altre informazioni, vedere [Gestione della disponibilità delle macchine virtuali](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-158">For more information, see [managing the availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="8c6b5-159">Creare un set di disponibilità per la macchina virtuale con [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="8c6b5-160">L'esempio seguente crea un set di disponibilità denominato *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-160">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="8c6b5-161">L'output elenca i domini di errore e i domini di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-161">The output notes fault domains and update domains:</span></span>

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-the-linux-vms"></a><span data-ttu-id="8c6b5-162">Creare le VM di Linux</span><span class="sxs-lookup"><span data-stu-id="8c6b5-162">Create the Linux VMs</span></span>
<span data-ttu-id="8c6b5-163">Sono state create le risorse di rete per supportare le VM accessibili tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-163">You've created the network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="8c6b5-164">A questo punto, creare una macchina virtuale e proteggerla con la chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="8c6b5-165">In questo caso, si vuole creare una VM Ubuntu basata sull'LTS più recente.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-165">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="8c6b5-166">È possibile trovare immagini aggiuntive con [az vm image list](/cli/azure/vm/image#list), come descritto nell'articolo sulla [ricerca di immagini della macchina virtuale di Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="8c6b5-167">È possibile anche specificare una chiave SSH da usare per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-167">We also specify an SSH key to use for authentication.</span></span> <span data-ttu-id="8c6b5-168">Se non si dispone di una coppia di chiavi pubblica SSH, è possibile [crearla](mac-create-ssh-keys.md) o utilizzare il parametro `--generate-ssh-keys` per crearla automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use the `--generate-ssh-keys` parameter to create them for you.</span></span> <span data-ttu-id="8c6b5-169">Se si dispone già di una coppia di chiavi, questo parametro usa le chiavi esistenti in `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="8c6b5-170">Creare la macchina virtuale unendo tutte le risorse e le informazioni con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-170">Create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="8c6b5-171">L'esempio seguente crea una macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-171">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="8c6b5-172">Eseguire l'autenticazione SSH alla macchina virtuale con la voce DNS indicata al momento della creazione dell'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-172">SSH to your VM with the DNS entry you provided when you created the public IP address.</span></span> <span data-ttu-id="8c6b5-173">Questo `fqdn` viene mostrato nell'output durante la creazione della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-173">This `fqdn` is shown in the output as you create your VM:</span></span>

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="8c6b5-174">Output:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-174">Output:</span></span>

```bash
The authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="8c6b5-175">È possibile installare NGINX e vedere il flusso del traffico alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-175">You can install NGINX and see the traffic flow to the VM.</span></span> <span data-ttu-id="8c6b5-176">Installare NGINX come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="8c6b5-177">Per visualizzare il sito NGINX predefinito in azione, aprire il Web browser e immettere il nome FQDN:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-177">To see the default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Sito NGINX predefinito nella macchina virtuale](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="8c6b5-179">Esportare come modello</span><span class="sxs-lookup"><span data-stu-id="8c6b5-179">Export as a template</span></span>
<span data-ttu-id="8c6b5-180">È possibile creare ora un ambiente di sviluppo aggiuntivo usando gli stessi parametri oppure creare un ambiente di produzione compatibile?</span><span class="sxs-lookup"><span data-stu-id="8c6b5-180">What if you now want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="8c6b5-181">Azure Resource Manager utilizza i modelli JSON che definiscono tutti i parametri per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-181">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="8c6b5-182">È possibile creare interi ambienti facendo riferimento a questo modello JSON.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="8c6b5-183">È possibile [creare modelli JSON manualmente](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o esportare un ambiente esistente per creare il modello JSON desiderato.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span></span> <span data-ttu-id="8c6b5-184">Usare [az group export](/cli/azure/group#export) per esportare il gruppo di risorse come segue:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-184">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="8c6b5-185">Questo comando crea il file `myResourceGroup.json` nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-185">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="8c6b5-186">Quando si crea un ambiente da questo modello, vengono richiesti tutti i nomi delle risorse.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-186">When you create an environment from this template, you are prompted for all the resource names.</span></span> <span data-ttu-id="8c6b5-187">È possibile inserire questi nomi nel file del modello aggiungendo il parametro `--include-parameter-default-value` al comando `az group export`.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-187">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the `az group export` command.</span></span> <span data-ttu-id="8c6b5-188">Modificare il modello JSON per specificare i nomi delle risorse, o [creare un file parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nel quale vengono specificati i nomi delle risorse.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-188">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="8c6b5-189">Per creare un ambiente in base al modello, usare [az group deployment create](/cli/azure/group/deployment#create) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8c6b5-189">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="8c6b5-190">Se lo si desidera, è possibile consultare [ulteriori informazioni su come eseguire la distribuzione partendo dai modelli](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c6b5-190">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8c6b5-191">Ulteriori informazioni su come aggiornare gli ambienti in modo incrementale, utilizzare il file di parametri e accedere ai modelli da un unico percorso di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-191">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c6b5-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c6b5-192">Next steps</span></span>
<span data-ttu-id="8c6b5-193">Ora è possibile iniziare a utilizzare più componenti di rete e VM.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-193">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="8c6b5-194">È possibile utilizzare questo ambiente di esempio per compilare l'applicazione utilizzando i componenti principali presentati qui.</span><span class="sxs-lookup"><span data-stu-id="8c6b5-194">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
