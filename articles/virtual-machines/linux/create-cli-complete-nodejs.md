---
title: Creare un ambiente Linux completo tramite l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Usare l'interfaccia della riga di comando 1.0 di Azure per creare da zero una risorsa di archiviazione, una VM di Linux, una rete virtuale con subnet, il bilanciamento del carico, una scheda di interfaccia di rete, un IP pubblico e un gruppo di sicurezza di rete.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 201ccd523e49d638ace50fbc0ffdceb705b35473
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="86e3a-103">Creare un ambiente Linux completo tramite l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="86e3a-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="86e3a-104">In questo articolo viene spiegato come creare una semplice rete con un servizio di bilanciamento del carico e un paio di VM utili per lo sviluppo e per calcoli semplici.</span><span class="sxs-lookup"><span data-stu-id="86e3a-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="86e3a-105">Viene presentato in dettaglio l'intero processo, comando dopo comando, fino a creare due VM Linux funzionanti e sicure a cui è possibile connettersi da qualsiasi posizione in Internet.</span><span class="sxs-lookup"><span data-stu-id="86e3a-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="86e3a-106">Si potrà quindi passare a reti e ambienti più complessi.</span><span class="sxs-lookup"><span data-stu-id="86e3a-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="86e3a-107">Durante il processo si apprenderanno informazioni sulla gerarchia delle dipendenze fornita dal modello di distribuzione di Resource Manager e sulle potenzialità che offre.</span><span class="sxs-lookup"><span data-stu-id="86e3a-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="86e3a-108">Dopo aver osservato come viene realizzato il sistema, è possibile ricrearlo molto più rapidamente utilizzando i [modelli di Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86e3a-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="86e3a-109">In più, dopo aver scoperto come interagiscono le parti dell'ambiente, diventa più facile creare modelli per automatizzarle.</span><span class="sxs-lookup"><span data-stu-id="86e3a-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="86e3a-110">Nell'ambiente sono presenti:</span><span class="sxs-lookup"><span data-stu-id="86e3a-110">The environment contains:</span></span>

* <span data-ttu-id="86e3a-111">Due VM all'interno di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="86e3a-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="86e3a-112">Un servizio di bilanciamento del carico con una regola di bilanciamento del carico sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="86e3a-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="86e3a-113">Regole del gruppo di sicurezza di rete (NSG) per proteggere la VM dal traffico indesiderato.</span><span class="sxs-lookup"><span data-stu-id="86e3a-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

<span data-ttu-id="86e3a-114">Per creare questo ambiente personalizzato, è necessario aver installato l'[interfaccia della riga di comando di Azure 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in modalità Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="86e3a-114">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="86e3a-115">È inoltre necessario uno strumento di analisi JSON.</span><span class="sxs-lookup"><span data-stu-id="86e3a-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="86e3a-116">In questo esempio viene utilizzato [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="86e3a-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="86e3a-117">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="86e3a-117">CLI versions to complete the task</span></span>
<span data-ttu-id="86e3a-118">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="86e3a-118">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="86e3a-119">[Interfaccia della riga di comando di Azure 1.0](#quick-commands): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="86e3a-119">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="86e3a-120">[Interfaccia della riga di comando di Azure 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="86e3a-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="86e3a-121">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="86e3a-121">Quick commands</span></span>
<span data-ttu-id="86e3a-122">Se si vuole eseguire rapidamente l'attività, la sezione seguente indica in dettaglio i comandi base per caricare una VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="86e3a-122">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="86e3a-123">Altre informazioni dettagliate e il contesto per ogni passaggio sono disponibili nelle sezioni successive del documento, a partire da [qui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="86e3a-123">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="86e3a-124">Controllare di aver effettuato l'accesso tramite l'[interfaccia della riga di comando di Azure 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e di usare la modalità Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="86e3a-124">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="86e3a-125">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="86e3a-125">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="86e3a-126">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="86e3a-127">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="86e3a-127">Create the resource group.</span></span> <span data-ttu-id="86e3a-128">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella località `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-128">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="86e3a-129">Verificare il gruppo di risorse utilizzando il parser JSON:</span><span class="sxs-lookup"><span data-stu-id="86e3a-129">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="86e3a-130">Creare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="86e3a-130">Create the storage account.</span></span> <span data-ttu-id="86e3a-131">Nell'esempio seguente viene creato un nuovo account di archiviazione denominato `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-131">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="86e3a-132">Il nome dell'account di archiviazione deve essere univoco; assegnare quindi all'account il proprio nome.</span><span class="sxs-lookup"><span data-stu-id="86e3a-132">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="86e3a-133">Verificare l'account di archiviazione utilizzando il parser JSON:</span><span class="sxs-lookup"><span data-stu-id="86e3a-133">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="86e3a-134">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="86e3a-134">Create the virtual network.</span></span> <span data-ttu-id="86e3a-135">Nell'esempio seguente viene creata una rete virtuale chiamata `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-135">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="86e3a-136">Creare una subnet.</span><span class="sxs-lookup"><span data-stu-id="86e3a-136">Create a subnet.</span></span> <span data-ttu-id="86e3a-137">Nell'esempio seguente viene creata una subnet denominata `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-137">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="86e3a-138">Verificare la rete virtuale e la subnet utilizzando il parser JSON:</span><span class="sxs-lookup"><span data-stu-id="86e3a-138">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="86e3a-139">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-139">Create a public IP.</span></span> <span data-ttu-id="86e3a-140">Nell'esempio seguente viene aggiunto un indirizzo IP pubblico chiamato `myPublicIP` con il nome DNS `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-140">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="86e3a-141">Il nome DNS deve essere univoco, quindi specificare il proprio nome DNS.</span><span class="sxs-lookup"><span data-stu-id="86e3a-141">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="86e3a-142">Creare il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-142">Create the load balancer.</span></span> <span data-ttu-id="86e3a-143">Nell'esempio seguente viene creato un servizio di bilanciamento del carico chiamato `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-143">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="86e3a-144">Creare un pool di indirizzi IP front-end per il servizio di bilanciamento del carico e associare l'IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-144">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="86e3a-145">Nell'esempio seguente viene creato un pool di indirizzi IP front-end chiamato `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-145">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="86e3a-146">Creare un pool di indirizzi IP back-end per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-146">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="86e3a-147">Nell'esempio seguente viene creato un pool di indirizzi IP back-end chiamato `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-147">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="86e3a-148">Creare regole Network Address Translation (NAT) in ingresso SSH per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-148">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="86e3a-149">Nell'esempio seguente vengono create due regole per il servizio di bilanciamento del carico chiamate `myLoadBalancerRuleSSH1` e `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-149">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="86e3a-150">Creare le regole NAT in ingresso Web per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-150">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="86e3a-151">Nell'esempio seguente viene creata una regola per il servizio di bilanciamento del carico denominata `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-151">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="86e3a-152">Creare il probe di integrità per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-152">Create the load balancer health probe.</span></span> <span data-ttu-id="86e3a-153">Nell'esempio seguente viene creato un probe TCP chiamato `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-153">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="86e3a-154">Verificare il servizio di bilanciamento del carico, il pool di indirizzi IP e le regole NAT utilizzando il parser JSON:</span><span class="sxs-lookup"><span data-stu-id="86e3a-154">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="86e3a-155">Creare la prima scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="86e3a-155">Create the first network interface card (NIC).</span></span> <span data-ttu-id="86e3a-156">Sostituire le sezioni `#####-###-###` con il proprio ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="86e3a-156">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="86e3a-157">L'ID sottoscrizione è indicato nell'output di **jq** quando si esaminano le risorse che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="86e3a-157">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="86e3a-158">È anche possibile visualizzare l'ID sottoscrizione con `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="86e3a-159">Nell'esempio seguente viene creata una scheda di interfaccia di rete chiamata `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-159">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="86e3a-160">Creare la seconda scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="86e3a-160">Create the second NIC.</span></span> <span data-ttu-id="86e3a-161">Nell'esempio seguente viene creata una scheda di interfaccia di rete chiamata `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-161">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="86e3a-162">Verificare le due schede di interfaccia di rete usando il parser JSON:</span><span class="sxs-lookup"><span data-stu-id="86e3a-162">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="86e3a-163">Creare il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="86e3a-163">Create the network security group.</span></span> <span data-ttu-id="86e3a-164">Nell'esempio seguente viene creato un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-164">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="86e3a-165">Aggiungere due regole in ingresso per il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="86e3a-165">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="86e3a-166">Nell'esempio seguente vengono create due regole chiamate `myNetworkSecurityGroupRuleSSH` e `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-166">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="86e3a-167">Verificare il gruppo di sicurezza di rete e le regole in ingresso usando il parser JSON:</span><span class="sxs-lookup"><span data-stu-id="86e3a-167">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="86e3a-168">Associare il gruppo di sicurezza di rete alle due schede di interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="86e3a-168">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="86e3a-169">Creare il set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="86e3a-169">Create the availability set.</span></span> <span data-ttu-id="86e3a-170">Nell'esempio seguente viene creato un set di disponibilità chiamato `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-170">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="86e3a-171">Creare la prima VM Linux.</span><span class="sxs-lookup"><span data-stu-id="86e3a-171">Create the first Linux VM.</span></span> <span data-ttu-id="86e3a-172">Nell'esempio seguente viene creata una VM chiamata `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-172">The following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="86e3a-173">Creare la seconda VM Linux.</span><span class="sxs-lookup"><span data-stu-id="86e3a-173">Create the second Linux VM.</span></span> <span data-ttu-id="86e3a-174">Nell'esempio seguente viene creata una VM chiamata `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-174">The following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="86e3a-175">Utilizzare il parser JSON per verificare tutto ciò che è stato creato:</span><span class="sxs-lookup"><span data-stu-id="86e3a-175">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="86e3a-176">Esportare il nuovo ambiente in un modello per ricreare rapidamente nuove istanze:</span><span class="sxs-lookup"><span data-stu-id="86e3a-176">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="86e3a-177">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="86e3a-177">Detailed walkthrough</span></span>
<span data-ttu-id="86e3a-178">La procedura dettagliata seguente illustra il funzionamento di ciascun comando durante la creazione dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-178">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="86e3a-179">Questi concetti torneranno utili in fase di creazione degli ambienti personalizzati per lo sviluppo o per la produzione.</span><span class="sxs-lookup"><span data-stu-id="86e3a-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="86e3a-180">Controllare di aver effettuato l'accesso tramite l'[interfaccia della riga di comando di Azure 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e di usare la modalità Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="86e3a-180">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="86e3a-181">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="86e3a-181">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="86e3a-182">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="86e3a-183">Creare i gruppi di risorse e scegliere i percorsi di distribuzione</span><span class="sxs-lookup"><span data-stu-id="86e3a-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="86e3a-184">I gruppi di risorse di Azure sono entità di distribuzione logiche che contengono informazioni di configurazione e altri metadati per abilitare la gestione logica delle distribuzioni di risorse.</span><span class="sxs-lookup"><span data-stu-id="86e3a-184">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="86e3a-185">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella località `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-185">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="86e3a-186">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="86e3a-187">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="86e3a-187">Create a storage account</span></span>
<span data-ttu-id="86e3a-188">Sono necessari account di archiviazione per i dischi della macchina virtuale e per eventuali altri dischi dati che si desidera aggiungere.</span><span class="sxs-lookup"><span data-stu-id="86e3a-188">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="86e3a-189">Si creano account di archiviazione quasi subito dopo la creazione di gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="86e3a-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="86e3a-190">Viene usato il comando `azure storage account create` , passando il percorso dell'account, il gruppo di risorse che lo controlla e il tipo di supporto di archiviazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="86e3a-190">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="86e3a-191">Nell'esempio seguente viene creato un nuovo account di archiviazione denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-191">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="86e3a-192">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="86e3a-193">Per esaminare il gruppo di risorse con il comando `azure group show`, usare lo strumento [jq](https://stedolan.github.io/jq/) insieme all'opzione `--json` dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="86e3a-193">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="86e3a-194">È possibile utilizzare **jsawk** o qualsiasi altra libreria di linguaggio per l'analisi del JSON.</span><span class="sxs-lookup"><span data-stu-id="86e3a-194">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="86e3a-195">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="86e3a-196">Per esaminare l'account di archiviazione usando l'interfaccia della riga di comando, è necessario innanzitutto impostare le chiavi e i nomi dell'account.</span><span class="sxs-lookup"><span data-stu-id="86e3a-196">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="86e3a-197">Sostituire il nome dell'account di archiviazione nell'esempio seguente con un nome a scelta:</span><span class="sxs-lookup"><span data-stu-id="86e3a-197">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="86e3a-198">Dopodiché è possibile visualizzare facilmente le informazioni di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="86e3a-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="86e3a-199">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="86e3a-200">Creare una rete virtuale e una subnet</span><span class="sxs-lookup"><span data-stu-id="86e3a-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="86e3a-201">Dopodiché è necessario creare una rete virtuale che funziona in Azure e una subnet in cui poter creare le VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-201">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="86e3a-202">Nell'esempio seguente viene creata una rete virtuale chiamata `myVnet` con il prefisso dell'indirizzo `192.168.0.0/16`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-202">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="86e3a-203">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="86e3a-204">Anche in questo caso osservare come vengono realizzate le risorse mediante l'opzione --json di `azure group show` e `jq`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-204">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="86e3a-205">Ora sono disponibili una risorsa `storageAccounts` e una risorsa `virtualNetworks`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="86e3a-206">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="86e3a-207">Viene quindi creata una subnet all'interno della rete virtuale `myVnet` in cui vengono distribuite le VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-207">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="86e3a-208">Usare il comando `azure network vnet subnet create` insieme alle risorse create in precedenza: il gruppo di risorse `myResourceGroup` e la rete virtuale `myVnet`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-208">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="86e3a-209">Nell'esempio seguente viene aggiunta una subnet chiamata `mySubnet` con il prefisso dell'indirizzo della subnet `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-209">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="86e3a-210">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="86e3a-211">Dato che la subnet è logicamente all'interno della rete virtuale, le informazioni relative alla subnet vengono cercate con un comando leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="86e3a-211">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="86e3a-212">Il comando usato è `azure network vnet show`, ma si continua a esaminare l'output JSON mediante lo strumento `jq`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-212">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="86e3a-213">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="86e3a-214">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="86e3a-214">Create a public IP address</span></span>
<span data-ttu-id="86e3a-215">A questo punto, creare l'indirizzo IP pubblico (PIP) che viene assegnato al bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-215">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="86e3a-216">Consente di connettersi alle VM da Internet tramite il comando `azure network public-ip create` .</span><span class="sxs-lookup"><span data-stu-id="86e3a-216">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="86e3a-217">Dato che l'indirizzo predefinito è dinamico, si crea una voce DNS nel dominio **cloudapp.azure.com** usando l'opzione `--domain-name-label`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-217">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="86e3a-218">Nell'esempio seguente viene aggiunto un indirizzo IP pubblico chiamato `myPublicIP` con il nome DNS `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-218">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="86e3a-219">Il nome DNS deve essere univoco, quindi specificare il proprio nome DNS.</span><span class="sxs-lookup"><span data-stu-id="86e3a-219">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="86e3a-220">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="86e3a-221">Anche l'indirizzo IP pubblico è una risorsa di primo livello che può essere visualizzata con `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-221">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="86e3a-222">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="86e3a-223">È possibile esaminare altri dettagli relativi alla risorsa, incluso il nome di dominio completo (FQDN) del sottodominio, usando il comando `azure network public-ip show` completo.</span><span class="sxs-lookup"><span data-stu-id="86e3a-223">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="86e3a-224">La risorsa indirizzo IP pubblico è stata allocata in modo logico, ma non è ancora stato assegnato un indirizzo specifico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-224">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="86e3a-225">Per ottenere un indirizzo IP, sarà necessario un servizio di bilanciamento del carico, che non è ancora stato creato.</span><span class="sxs-lookup"><span data-stu-id="86e3a-225">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="86e3a-226">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="86e3a-227">Creare un servizio di bilanciamento del carico e i pool di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="86e3a-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="86e3a-228">Quando si crea un bilanciamento del carico, questo consente di distribuire il traffico tra più VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-228">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="86e3a-229">Fornisce anche ridondanza all'applicazione grazie all'esecuzione di più VM che rispondono alle richieste degli utenti in caso di manutenzione o carichi elevati.</span><span class="sxs-lookup"><span data-stu-id="86e3a-229">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="86e3a-230">Nell'esempio seguente viene creato un servizio di bilanciamento del carico chiamato `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-230">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="86e3a-231">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="86e3a-232">Il servizio di bilanciamento del carico è piuttosto vuoto, per cui si creeranno alcuni pool di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="86e3a-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="86e3a-233">Si creeranno due pool di indirizzi IP per il servizio di bilanciamento del carico, uno per il front-end e uno per il back-end.</span><span class="sxs-lookup"><span data-stu-id="86e3a-233">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="86e3a-234">Il pool di IP front-end è visibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-234">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="86e3a-235">Rappresenta anche il percorso a cui si assegnano i PIP creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="86e3a-235">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="86e3a-236">Dopodiché, si usa il pool di back-end come un percorso per le VM a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="86e3a-236">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="86e3a-237">In questo modo, il traffico può fluire attraverso il bilanciamento del carico verso le VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-237">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="86e3a-238">Prima di tutto si creerà il pool di indirizzi IP front-end.</span><span class="sxs-lookup"><span data-stu-id="86e3a-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="86e3a-239">Nell'esempio seguente viene creato un pool di indirizzi IP front-end chiamato `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-239">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="86e3a-240">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="86e3a-241">Si noti che è stata usata l'opzione `--public-ip-name` per passare il valore `myPublicIP` creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="86e3a-241">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="86e3a-242">L'assegnazione dell'indirizzo IP pubblico al servizio di bilanciamento del carico consente di raggiungere le VM su Internet.</span><span class="sxs-lookup"><span data-stu-id="86e3a-242">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="86e3a-243">Quindi si creerà il secondo pool di indirizzi IP, questa volta per il traffico back-end.</span><span class="sxs-lookup"><span data-stu-id="86e3a-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="86e3a-244">Nell'esempio seguente viene creato un pool di indirizzi IP back-end chiamato `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-244">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="86e3a-245">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="86e3a-246">Per vedere il servizio di bilanciamento del carico è possibile usare `azure network lb show` ed esaminare l'output JSON:</span><span class="sxs-lookup"><span data-stu-id="86e3a-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="86e3a-247">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="86e3a-248">Creare le regole NAT per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="86e3a-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="86e3a-249">Affinché il traffico attraversi il servizio di bilanciamento del carico, è necessario creare le regole Network Address Translation (NAT) che specificano le azioni in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="86e3a-249">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="86e3a-250">È possibile specificare il protocollo da usare, quindi eseguire il mapping delle porte esterne alle porte interne desiderate.</span><span class="sxs-lookup"><span data-stu-id="86e3a-250">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="86e3a-251">Per questo ambiente si creeranno alcune regole che consentono il passaggio di SSH attraverso il servizio di bilanciamento del carico fino alle VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-251">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="86e3a-252">Le porte TCP 4222 e 4223 vengono configurate in modo da puntare alla porta TCP 22 nelle VM, che vengono create successivamente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-252">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="86e3a-253">Nell'esempio seguente viene creata una regola chiamata `myLoadBalancerRuleSSH1` per eseguire il mapping della porta TCP 4222 sulla porta 22:</span><span class="sxs-lookup"><span data-stu-id="86e3a-253">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="86e3a-254">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="86e3a-255">Ripetere la procedura per la seconda regola NAT per SSH.</span><span class="sxs-lookup"><span data-stu-id="86e3a-255">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="86e3a-256">Nell'esempio seguente viene creata una regola chiamata `myLoadBalancerRuleSSH2` per eseguire il mapping della porta TCP 4223 sulla porta 22:</span><span class="sxs-lookup"><span data-stu-id="86e3a-256">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="86e3a-257">Verrà anche creata una regola NAT per la porta TCP 80 per il traffico Web, collegando la regola ai pool di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="86e3a-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="86e3a-258">Se la regola viene associata a un pool IP, anziché essere associata singolarmente alle VM, è possibile aggiungere o rimuovere le VM dal pool di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="86e3a-258">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="86e3a-259">Il servizio di bilanciamento del carico regola automaticamente il flusso del traffico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-259">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="86e3a-260">Nell'esempio seguente viene creata una regola chiamata `myLoadBalancerRuleWeb` per eseguire il mapping della porta TCP 80 sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="86e3a-260">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="86e3a-261">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="86e3a-262">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="86e3a-262">Create a load balancer health probe</span></span>
<span data-ttu-id="86e3a-263">Un probe di integrità verifica periodicamente le VM che si trovano dietro il servizio di bilanciamento del carico per assicurarsi che siano operative e che rispondano alle richieste, come specificato.</span><span class="sxs-lookup"><span data-stu-id="86e3a-263">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="86e3a-264">In caso contrario ne viene disabilitata l'operatività per fare in modo che gli utenti non vengano indirizzati a esse.</span><span class="sxs-lookup"><span data-stu-id="86e3a-264">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="86e3a-265">È possibile definire controlli personalizzati per il probe di integrità, nonché gli intervalli e i valori di timeout.</span><span class="sxs-lookup"><span data-stu-id="86e3a-265">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="86e3a-266">Per altre informazioni sui probe di integrità, vedere [Probe di integrità del servizio di bilanciamento del carico](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86e3a-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="86e3a-267">Nell'esempio seguente viene creato un probe di integrità TCP chiamato `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-267">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="86e3a-268">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="86e3a-269">In questo caso è stato specificato un intervallo di 15 secondi per i controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="86e3a-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="86e3a-270">È consentito un massimo di quattro probe mancati (un minuto) prima che il bilanciamento del carico consideri l'host come non più funzionante.</span><span class="sxs-lookup"><span data-stu-id="86e3a-270">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="86e3a-271">Verificare il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="86e3a-271">Verify the load balancer</span></span>
<span data-ttu-id="86e3a-272">La configurazione del bilanciamento del carico è completa.</span><span class="sxs-lookup"><span data-stu-id="86e3a-272">Now the load balancer configuration is done.</span></span> <span data-ttu-id="86e3a-273">Ecco i passaggi effettuati:</span><span class="sxs-lookup"><span data-stu-id="86e3a-273">Here are the steps you took:</span></span>

1. <span data-ttu-id="86e3a-274">È stato creato un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-274">You created a load balancer.</span></span>
2. <span data-ttu-id="86e3a-275">È stato creato un pool di indirizzi IP front-end a cui è stato assegnato un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-275">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="86e3a-276">È stato creato un pool IP back-end a cui possono connettersi le VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="86e3a-277">Sono state create le regole NAT che consentono alle macchine virtuali di usare il protocollo SSH per la gestione, oltre a una regola che consente all'app Web di usare la porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="86e3a-277">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="86e3a-278">È stato aggiunto un probe di integrità per verificare periodicamente lo stato delle VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-278">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="86e3a-279">Questo probe di integrità garantisce agli utenti di accedere solo alle VM non più funzionanti o con contenuti non più disponibili.</span><span class="sxs-lookup"><span data-stu-id="86e3a-279">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="86e3a-280">Ecco il bilanciamento del carico risultante:</span><span class="sxs-lookup"><span data-stu-id="86e3a-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="86e3a-281">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="86e3a-282">Creare una scheda di interfaccia di rete da usare con la VM di Linux</span><span class="sxs-lookup"><span data-stu-id="86e3a-282">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="86e3a-283">Le schede di interfaccia di rete sono disponibili a livello di programmazione in quanto è possibile applicare delle regole di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="86e3a-283">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="86e3a-284">È inoltre possibile averne più di una.</span><span class="sxs-lookup"><span data-stu-id="86e3a-284">You can also have more than one.</span></span> <span data-ttu-id="86e3a-285">Nel comando `azure network nic create` seguente la scheda di interfaccia di rete viene associata al pool di indirizzi IP back-end del carico e alla regola NAT per consentire il traffico SSH.</span><span class="sxs-lookup"><span data-stu-id="86e3a-285">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="86e3a-286">Sostituire le sezioni `#####-###-###` con il proprio ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="86e3a-286">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="86e3a-287">L'ID sottoscrizione è indicato nell'output di `jq` quando si esaminano le risorse che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="86e3a-287">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="86e3a-288">È anche possibile visualizzare l'ID sottoscrizione con `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="86e3a-289">Nell'esempio seguente viene creata una scheda di interfaccia di rete chiamata `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-289">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="86e3a-290">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="86e3a-291">È possibile visualizzare i dettagli esaminando la risorsa direttamente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-291">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="86e3a-292">La risorsa viene esaminata con il comando `azure network nic show` :</span><span class="sxs-lookup"><span data-stu-id="86e3a-292">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="86e3a-293">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="86e3a-294">Ora è possibile creare la seconda scheda di interfaccia di rete, collegandola di nuovo al pool IP back-end.</span><span class="sxs-lookup"><span data-stu-id="86e3a-294">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="86e3a-295">Questa volta la seconda regola NAT consente il traffico SSH.</span><span class="sxs-lookup"><span data-stu-id="86e3a-295">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="86e3a-296">Nell'esempio seguente viene creata una scheda di interfaccia di rete chiamata `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-296">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="86e3a-297">Creare un gruppo di sicurezza di rete e le regole corrispondenti</span><span class="sxs-lookup"><span data-stu-id="86e3a-297">Create a network security group and rules</span></span>
<span data-ttu-id="86e3a-298">Vengono ora creati il gruppo di sicurezza di rete e le regole in ingresso che regolano l'accesso alla scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="86e3a-298">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="86e3a-299">Per una scheda di interfaccia di rete o una subnet è possibile usare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="86e3a-299">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="86e3a-300">Si definiscono regole per controllare il flusso del traffico da e verso le VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-300">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="86e3a-301">Nell'esempio seguente viene creato un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-301">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="86e3a-302">Si aggiungerà la regola in ingresso per il gruppo di sicurezza di rete per consentire le connessioni in ingresso sulla porta 22 (per supportare SSH).</span><span class="sxs-lookup"><span data-stu-id="86e3a-302">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="86e3a-303">Nell'esempio seguente viene creata una regola denominata `myNetworkSecurityGroupRuleSSH` per consentire il traffico TCP sulla porta 22:</span><span class="sxs-lookup"><span data-stu-id="86e3a-303">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="86e3a-304">Si aggiungerà la regola in ingresso per il gruppo di sicurezza di rete per consentire le connessioni in ingresso sulla porta 80 (per supportare il traffico Web).</span><span class="sxs-lookup"><span data-stu-id="86e3a-304">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="86e3a-305">Nell'esempio seguente viene creata una regola denominata `myNetworkSecurityGroupRuleHTTP` per consentire il traffico TCP sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="86e3a-305">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="86e3a-306">La regola in ingresso è un filtro per le connessioni di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="86e3a-306">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="86e3a-307">In questo esempio il gruppo di sicurezza di rete viene associato alla scheda di rete virtuale delle VM, di conseguenza qualsiasi richiesta per la porta 22 viene passata alla scheda di rete nella VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-307">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="86e3a-308">Questa regola è relativa alla connessione di rete anziché all'endpoint, come invece sarebbe nelle distribuzioni classiche.</span><span class="sxs-lookup"><span data-stu-id="86e3a-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="86e3a-309">Per aprire una porta, è necessario lasciare `--source-port-range` impostato su '\*' (valore predefinito) per accettare le richieste in ingresso da **qualsiasi** porta richiedente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-309">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="86e3a-310">Le porte sono solitamente dinamiche.</span><span class="sxs-lookup"><span data-stu-id="86e3a-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="86e3a-311">Associare alla scheda di rete</span><span class="sxs-lookup"><span data-stu-id="86e3a-311">Bind to the NIC</span></span>
<span data-ttu-id="86e3a-312">Associare il gruppo di sicurezza di rete alle schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="86e3a-312">Bind the NSG to the NICs.</span></span> <span data-ttu-id="86e3a-313">È necessario connettere le schede di interfaccia di rete al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="86e3a-313">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="86e3a-314">Eseguire entrambi i comandi per collegare entrambe le schede di interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="86e3a-314">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="86e3a-315">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="86e3a-315">Create an availability set</span></span>
<span data-ttu-id="86e3a-316">I set di disponibilità agevolano la distribuzione delle VM nei domini di errore e domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="86e3a-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="86e3a-317">Si creerà un set di disponibilità per le VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="86e3a-318">Nell'esempio seguente viene creato un set di disponibilità chiamato `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="86e3a-318">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="86e3a-319">I domini di errore definiscono un gruppo di macchine virtuali che condividono una fonte di alimentazione e uno switch di rete comuni.</span><span class="sxs-lookup"><span data-stu-id="86e3a-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="86e3a-320">Per impostazione predefinita, le macchine virtuali configurate nell'ambito di un set di disponibilità vengono suddivise tra un massimo di tre domini di errore.</span><span class="sxs-lookup"><span data-stu-id="86e3a-320">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="86e3a-321">L'idea è che un problema hardware in uno di questi domini di errore non abbia effetto su tutte le VM che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="86e3a-321">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="86e3a-322">Azure distribuisce automaticamente le VM tra i domini di errore durante il posizionamento in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="86e3a-322">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="86e3a-323">I domini di aggiornamento indicano gruppi di macchine virtuali e l'hardware fisico sottostante che possono essere riavviati nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="86e3a-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="86e3a-324">I domini di aggiornamento non vengono necessariamente riavviati in ordine sequenziale durante la manutenzione pianificata, ma ne viene riavviato uno solo alla volta.</span><span class="sxs-lookup"><span data-stu-id="86e3a-324">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="86e3a-325">D nuovo, Azure distribuisce automaticamente le VM tra i domini di aggiornamento durante il posizionamento in un sito di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="86e3a-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="86e3a-326">Per altre informazioni, leggere l'articolo relativo alla [gestione della disponibilità delle VM](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86e3a-326">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="86e3a-327">Creare le VM di Linux</span><span class="sxs-lookup"><span data-stu-id="86e3a-327">Create the Linux VMs</span></span>
<span data-ttu-id="86e3a-328">Sono state create le risorse di archiviazione e di rete per supportare le VM accessibili tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="86e3a-328">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="86e3a-329">Ora è possibile creare quelle VM e proteggerle con una chiave SSH priva di password.</span><span class="sxs-lookup"><span data-stu-id="86e3a-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="86e3a-330">In questo caso, si vuole creare una VM Ubuntu basata sull'LTS più recente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-330">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="86e3a-331">Per trovare le informazioni sull'immagine si usa `azure vm image list`, come descritto nell'articolo relativo alla [ricerca di immagini di VM di Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86e3a-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="86e3a-332">È stata selezionata un'immagine utilizzando il comando `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-332">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="86e3a-333">In questo caso, si usa `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="86e3a-334">Per l'ultimo campo si passa a `latest` così che in futuro si ottenga sempre la build più recente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-334">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="86e3a-335">La stringa usata è `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="86e3a-335">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="86e3a-336">Il passaggio successivo è già noto a chiunque abbia già creato una coppia di chiavi ssh-rsa pubblica e privata in Linux o Mac usando **ssh-keygen -t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="86e3a-336">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="86e3a-337">Se non si dispone di alcuna coppia di chiavi del certificato nella directory `~/.ssh` , è possibile crearle:</span><span class="sxs-lookup"><span data-stu-id="86e3a-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="86e3a-338">Automaticamente, utilizzando l'opzione `azure vm create --generate-ssh-keys` .</span><span class="sxs-lookup"><span data-stu-id="86e3a-338">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="86e3a-339">Manualmente, usando [le istruzioni per crearle autonomamente](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86e3a-339">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="86e3a-340">In alternativa, è possibile usare il metodo `--admin-password` per autenticare le connessioni SSH dopo aver creato la VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-340">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="86e3a-341">Di solito, questo metodo risulta essere meno sicuro.</span><span class="sxs-lookup"><span data-stu-id="86e3a-341">This method is typically less secure.</span></span>

<span data-ttu-id="86e3a-342">Per creare la VM si dovranno unire tutte le risorse e le informazioni con il comando `azure vm create` :</span><span class="sxs-lookup"><span data-stu-id="86e3a-342">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="86e3a-343">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="86e3a-344">È possibile connettersi immediatamente alla VM usando le chiavi SSH predefinite.</span><span class="sxs-lookup"><span data-stu-id="86e3a-344">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="86e3a-345">Assicurarsi di specificare la porta appropriata poiché si passa tramite il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="86e3a-345">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="86e3a-346">Per la prima VM impostare la regola NAT per l'inoltro della porta 4222 alla VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-346">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="86e3a-347">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-347">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="86e3a-348">Proseguire e creare la seconda VM nello stesso modo:</span><span class="sxs-lookup"><span data-stu-id="86e3a-348">Go ahead and create your second VM in the same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="86e3a-349">Ora è possibile usare il comando `azure vm show myResourceGroup myVM1` per esaminare ciò che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="86e3a-349">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="86e3a-350">A questo punto le VM Ubuntu sono in esecuzione dietro al bilanciamento del carico in Azure a cui è possibile accedere solo con la coppia di chiavi SSH, dal momento che le password sono disabilitate.</span><span class="sxs-lookup"><span data-stu-id="86e3a-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="86e3a-351">È possibile installare nginx o httpd, distribuire un'app Web e vedere il traffico passare attraverso il servizio di bilanciamento del carico e dirigersi a entrambe le VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-351">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="86e3a-352">Output:</span><span class="sxs-lookup"><span data-stu-id="86e3a-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="86e3a-353">Esportare l'ambiente come modello</span><span class="sxs-lookup"><span data-stu-id="86e3a-353">Export the environment as a template</span></span>
<span data-ttu-id="86e3a-354">Dopo aver creato questo ambiente, è possibile creare un ambiente di sviluppo aggiuntivo utilizzando gli stessi parametri oppure creare un ambiente di produzione compatibile?</span><span class="sxs-lookup"><span data-stu-id="86e3a-354">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="86e3a-355">Azure Resource Manager utilizza i modelli JSON che definiscono tutti i parametri per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-355">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="86e3a-356">È possibile creare interi ambienti facendo riferimento a questo modello JSON.</span><span class="sxs-lookup"><span data-stu-id="86e3a-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="86e3a-357">È possibile [creare modelli JSON manualmente](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o esportare un ambiente esistente per creare il modello JSON desiderato:</span><span class="sxs-lookup"><span data-stu-id="86e3a-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="86e3a-358">Questo comando crea il file `myResourceGroup.json` nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="86e3a-358">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="86e3a-359">Quando si crea un ambiente da questo modello, vengono richiesti i nomi di tutte le risorse, tra cui quelli del servizio di bilanciamento del carico, delle interfacce di rete o delle VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-359">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="86e3a-360">È possibile popolare questi nomi nel file del modello aggiungendo i parametri `-p` o `--includeParameterDefaultValue` al comando `azure group export` descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="86e3a-360">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="86e3a-361">Modificare il modello JSON per specificare i nomi delle risorse, o [creare un file parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nel quale vengono specificati i nomi delle risorse.</span><span class="sxs-lookup"><span data-stu-id="86e3a-361">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="86e3a-362">Per creare un ambiente in base al modello:</span><span class="sxs-lookup"><span data-stu-id="86e3a-362">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="86e3a-363">Se lo si desidera, è possibile consultare [ulteriori informazioni su come eseguire la distribuzione partendo dai modelli](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86e3a-363">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="86e3a-364">Ulteriori informazioni su come aggiornare gli ambienti in modo incrementale, utilizzare il file di parametri e accedere ai modelli da un unico percorso di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="86e3a-364">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86e3a-365">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86e3a-365">Next steps</span></span>
<span data-ttu-id="86e3a-366">Ora è possibile iniziare a utilizzare più componenti di rete e VM.</span><span class="sxs-lookup"><span data-stu-id="86e3a-366">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="86e3a-367">È possibile utilizzare questo ambiente di esempio per compilare l'applicazione utilizzando i componenti principali presentati qui.</span><span class="sxs-lookup"><span data-stu-id="86e3a-367">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
