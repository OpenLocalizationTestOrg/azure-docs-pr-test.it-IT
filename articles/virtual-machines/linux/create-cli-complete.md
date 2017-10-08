---
title: un ambiente Linux con hello Azure CLI 2.0 aaaCreate | Documenti Microsoft
description: Creare archiviazione, una VM Linux, una rete virtuale e subnet, un bilanciamento del carico, una scheda di rete, un indirizzo IP pubblico e un gruppo di sicurezza di rete, tutti da hello messa a terra tramite hello CLI di Azure 2.0.
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
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="5b95f-103">Creare una macchina virtuale di Linux completezza con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="5b95f-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="5b95f-104">tooquickly creare una macchina virtuale (VM) in Azure, è possibile utilizzare un singolo comando CLI di Azure che utilizza l'impostazione predefinita i valori toocreate qualsiasi necessarie risorse di supporto.</span><span class="sxs-lookup"><span data-stu-id="5b95f-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="5b95f-105">Le risorse, ad esempio una rete virtuale, l'indirizzo IP pubblico e regole del gruppo di sicurezza di rete, vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5b95f-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="5b95f-106">Per un maggiore controllo dell'ambiente di produzione, utilizzare, è possibile creare queste risorse anticipo e quindi aggiungere toothem le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5b95f-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="5b95f-107">In questo articolo descrive come toocreate una macchina virtuale e ogni hello risorse di supporto uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="5b95f-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="5b95f-108">Assicurarsi di avere installato più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e l'account connesso tooan Azure con [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5b95f-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5b95f-109">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="5b95f-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5b95f-110">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="5b95f-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="5b95f-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5b95f-111">Create resource group</span></span>
<span data-ttu-id="5b95f-112">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="5b95f-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="5b95f-113">Il gruppo di risorse deve essere creato prima della macchina virtuale e delle risorse della rete virtuale di supporto.</span><span class="sxs-lookup"><span data-stu-id="5b95f-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="5b95f-114">Creare il gruppo di risorse hello con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5b95f-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="5b95f-115">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="5b95f-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="5b95f-116">Per impostazione predefinita, l'output di hello di comandi CLI di Azure è in JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="5b95f-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="5b95f-117">toochange hello predefinito output tooa elenco o una tabella, ad esempio, utilizzare [az configurare - output](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="5b95f-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="5b95f-118">È inoltre possibile aggiungere `--output` comando tooany per un periodo di una modifica in formato di output.</span><span class="sxs-lookup"><span data-stu-id="5b95f-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="5b95f-119">Hello esempio seguente viene illustrato l'output JSON hello da hello `az group create` comando:</span><span class="sxs-lookup"><span data-stu-id="5b95f-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="5b95f-120">Creare una rete virtuale e una subnet</span><span class="sxs-lookup"><span data-stu-id="5b95f-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="5b95f-121">Successivamente si crea una rete virtuale in Azure e una subnet in toowhich è possibile creare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5b95f-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="5b95f-122">Utilizzare [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create) toocreate una rete virtuale denominata *myVnet* con hello *192.168.0.0/16* prefisso dell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="5b95f-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="5b95f-123">È inoltre aggiungere una subnet denominata *mySubnet* con prefisso di indirizzo hello *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="5b95f-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="5b95f-124">output di Hello Mostra subnet hello come punto di vista logico creato all'interno di rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="5b95f-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="5b95f-125">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="5b95f-125">Create a public IP address</span></span>
<span data-ttu-id="5b95f-126">Creare ora un indirizzo IP pubblico con [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="5b95f-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="5b95f-127">Questo indirizzo IP pubblico consente si tooconnect tooyour macchine virtuali da hello Internet.</span><span class="sxs-lookup"><span data-stu-id="5b95f-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="5b95f-128">Poiché l'indirizzo predefinito hello è dinamica, è inoltre creare una voce DNS denominata con hello `--domain-name-label` opzione.</span><span class="sxs-lookup"><span data-stu-id="5b95f-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="5b95f-129">esempio Hello crea un indirizzo IP pubblico denominato *myPublicIP* con nome DNS hello *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="5b95f-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="5b95f-130">Poiché il nome DNS hello deve essere univoco, fornire il proprio nome DNS univoco:</span><span class="sxs-lookup"><span data-stu-id="5b95f-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="5b95f-131">Output:</span><span class="sxs-lookup"><span data-stu-id="5b95f-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="5b95f-132">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="5b95f-132">Create a network security group</span></span>
<span data-ttu-id="5b95f-133">flusso di hello toocontrol del traffico da e verso le macchine virtuali, creare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5b95f-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="5b95f-134">Un gruppo di sicurezza di rete può essere applicato tooa NIC o subnet.</span><span class="sxs-lookup"><span data-stu-id="5b95f-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="5b95f-135">Hello seguente utilizza [rete az creare](/cli/azure/network/nsg#create) toocreate un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="5b95f-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="5b95f-136">Si definiscono regole che consentono o negano il traffico specifico hello.</span><span class="sxs-lookup"><span data-stu-id="5b95f-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="5b95f-137">tooallow le connessioni in ingresso sulla porta 22 (toosupport SSH), creare una regola in ingresso per il gruppo di sicurezza di rete hello con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="5b95f-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="5b95f-138">esempio Hello crea una regola denominata *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="5b95f-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="5b95f-139">tooallow le connessioni in ingresso sulla porta 80 (il traffico web toosupport), aggiungere un'altra regola di gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5b95f-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="5b95f-140">esempio Hello crea una regola denominata *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="5b95f-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="5b95f-141">Esaminare il gruppo di sicurezza rete hello e le regole con [Mostra nsg di rete az](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="5b95f-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="5b95f-142">Output:</span><span class="sxs-lookup"><span data-stu-id="5b95f-142">Output:</span></span>

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
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
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
      "description": "Allow outbound traffic from all VMs tooInternet",
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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="5b95f-143">Creare una scheda di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="5b95f-143">Create a virtual NIC</span></span>
<span data-ttu-id="5b95f-144">Schede di interfaccia di rete virtuale (NIC) disponibili a livello di codice in quanto è possibile applicare regole tootheir utilizzare.</span><span class="sxs-lookup"><span data-stu-id="5b95f-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="5b95f-145">È inoltre possibile averne più di una.</span><span class="sxs-lookup"><span data-stu-id="5b95f-145">You can also have more than one.</span></span> <span data-ttu-id="5b95f-146">In seguito hello [az rete nic creare](/cli/azure/network/nic#create) comando, si crea una scheda di rete denominata *myNic* e associarlo a gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="5b95f-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="5b95f-147">indirizzo IP pubblico Hello *myPublicIP* è inoltre associata a una scheda di rete virtuale. hello</span><span class="sxs-lookup"><span data-stu-id="5b95f-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="5b95f-148">Output:</span><span class="sxs-lookup"><span data-stu-id="5b95f-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="5b95f-149">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="5b95f-149">Create an availability set</span></span>
<span data-ttu-id="5b95f-150">I set di disponibilità agevolano la distribuzione delle macchine virtuali nei domini di errore e nei domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="5b95f-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="5b95f-151">Anche se è solo creare una macchina virtuale al momento, si tratta di best practice toouse disponibilità set toomake è più facile tooexpand in hello future.</span><span class="sxs-lookup"><span data-stu-id="5b95f-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="5b95f-152">I domini di errore definiscono un gruppo di macchine virtuali che condividono una fonte di alimentazione e uno switch di rete comuni.</span><span class="sxs-lookup"><span data-stu-id="5b95f-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="5b95f-153">Per impostazione predefinita, hello le macchine virtuali configurate all'interno del set di disponibilità sono separate tra i domini di errore toothree.</span><span class="sxs-lookup"><span data-stu-id="5b95f-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="5b95f-154">Un problema hardware in uno di questi domini di errore non influenza tutte le macchine virtuali che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="5b95f-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="5b95f-155">Indicano i domini di aggiornamento gruppi di macchine virtuali e l'hardware fisico sottostante che può essere riavviata in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="5b95f-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="5b95f-156">Durante la manutenzione pianificata, ordine di hello in aggiornamento vengono riavviati domini potrebbe non essere sequenziale, ma riavvio del dominio di aggiornamento solo una alla volta.</span><span class="sxs-lookup"><span data-stu-id="5b95f-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="5b95f-157">Azure distribuisce automaticamente le macchine virtuali tra i domini di errore e l'aggiornamento di hello durante il posizionamento in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="5b95f-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="5b95f-158">Per ulteriori informazioni, vedere [la gestione della disponibilità di hello di macchine virtuali](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="5b95f-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="5b95f-159">Creare un set di disponibilità per la macchina virtuale con [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="5b95f-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="5b95f-160">esempio Hello crea un set denominato di disponibilità *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="5b95f-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="5b95f-161">Hello output note domini di errore e domini di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="5b95f-161">hello output notes fault domains and update domains:</span></span>

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


## <a name="create-hello-linux-vms"></a><span data-ttu-id="5b95f-162">Creare le macchine virtuali Linux hello</span><span class="sxs-lookup"><span data-stu-id="5b95f-162">Create hello Linux VMs</span></span>
<span data-ttu-id="5b95f-163">Si è creato toosupport risorse di rete hello macchine virtuali accessibile tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="5b95f-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="5b95f-164">A questo punto, creare una macchina virtuale e proteggerla con la chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="5b95f-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="5b95f-165">In questo caso, verrà toocreate una VM Ubuntu in base a hello LTS più recente.</span><span class="sxs-lookup"><span data-stu-id="5b95f-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="5b95f-166">È possibile trovare immagini aggiuntive con [az vm image list](/cli/azure/vm/image#list), come descritto nell'articolo sulla [ricerca di immagini della macchina virtuale di Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="5b95f-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="5b95f-167">È inoltre possibile specificare un toouse chiave SSH per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="5b95f-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="5b95f-168">Se non si dispone di una coppia di chiavi pubblica SSH, è possibile [crearli](mac-create-ssh-keys.md) o utilizzare hello `--generate-ssh-keys` toocreate parametro usarle per l'utente.</span><span class="sxs-lookup"><span data-stu-id="5b95f-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="5b95f-169">Se si dispone già di una coppia di chiavi, questo parametro usa le chiavi esistenti in `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="5b95f-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="5b95f-170">Creare VM hello riportando tutti i risorse e informazioni insieme hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5b95f-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="5b95f-171">esempio Hello crea una macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5b95f-171">hello following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="5b95f-172">SSH tooyour VM con hello voce DNS specificato durante la creazione di indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="5b95f-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="5b95f-173">Questo `fqdn` è illustrato nell'output di hello durante la creazione di una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="5b95f-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

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

<span data-ttu-id="5b95f-174">Output:</span><span class="sxs-lookup"><span data-stu-id="5b95f-174">Output:</span></span>

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="5b95f-175">È possibile installare NGINX e vedere hello traffico flusso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5b95f-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="5b95f-176">Installare NGINX come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b95f-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="5b95f-177">toosee sito NGINX predefinito di hello in azione, aprire il web browser e immettere il nome FQDN:</span><span class="sxs-lookup"><span data-stu-id="5b95f-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Sito NGINX predefinito nella macchina virtuale](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="5b95f-179">Esportare come modello</span><span class="sxs-lookup"><span data-stu-id="5b95f-179">Export as a template</span></span>
<span data-ttu-id="5b95f-180">È ora possibile toocreate un ambiente di sviluppo aggiuntive con hello stessi parametri o un ambiente di produzione a esso corrispondente?</span><span class="sxs-lookup"><span data-stu-id="5b95f-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="5b95f-181">Gestione risorse Usa i modelli JSON che definiscono tutti i parametri di hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="5b95f-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="5b95f-182">È possibile creare interi ambienti facendo riferimento a questo modello JSON.</span><span class="sxs-lookup"><span data-stu-id="5b95f-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="5b95f-183">È possibile [creare manualmente modelli JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o esportare un modello JSON hello di toocreate ambiente esistente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="5b95f-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="5b95f-184">Utilizzare [esportazione gruppo az](/cli/azure/group#export) tooexport la risorsa gruppo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b95f-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="5b95f-185">Questo comando Crea hello `myResourceGroup.json` file nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="5b95f-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="5b95f-186">Quando si crea un ambiente da questo modello, viene chiesto di tutti i nomi di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="5b95f-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="5b95f-187">È possibile popolare questi nomi nel file di modello aggiungendo hello `--include-parameter-default-value` parametro toohello `az group export` comando.</span><span class="sxs-lookup"><span data-stu-id="5b95f-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="5b95f-188">Modifica i nome di risorsa hello JSON modelli toospecify, o [creare un file parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) che specifica i nomi delle risorse hello.</span><span class="sxs-lookup"><span data-stu-id="5b95f-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="5b95f-189">un ambiente nel modello di utilizzo toocreate [distribuzione gruppo az creare](/cli/azure/group/deployment#create) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b95f-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="5b95f-190">Potrebbe essere necessario tooread [altre informazioni su come toodeploy dai modelli](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b95f-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5b95f-191">Informazioni su come utilizzare i file dei parametri hello tooincrementally aggiornamento ambienti e accedere ai modelli da un unico percorso di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5b95f-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b95f-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b95f-192">Next steps</span></span>
<span data-ttu-id="5b95f-193">Ora si è pronti toobegin utilizzo di più componenti di rete e le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5b95f-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="5b95f-194">È possibile utilizzare questo toobuild ambiente di esempio dell'applicazione utilizzando i componenti di base hello introdotti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="5b95f-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
