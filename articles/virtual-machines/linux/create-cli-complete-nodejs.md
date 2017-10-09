---
title: un ambiente completo di Linux con hello Azure CLI 1.0 aaaCreate | Documenti Microsoft
description: Creare archiviazione, una VM Linux, una rete virtuale e subnet, un bilanciamento del carico, una scheda di rete, un indirizzo IP pubblico e un gruppo di sicurezza di rete, tutti da hello messa a terra tramite hello Azure CLI 1.0.
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
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a><span data-ttu-id="3978a-103">Creare un ambiente completo di Linux con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3978a-103">Create a complete Linux environment with hello Azure CLI 1.0</span></span>
<span data-ttu-id="3978a-104">In questo articolo viene spiegato come creare una semplice rete con un servizio di bilanciamento del carico e un paio di VM utili per lo sviluppo e per calcoli semplici.</span><span class="sxs-lookup"><span data-stu-id="3978a-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="3978a-105">Esaminare il processo di hello dal comando, fino a quando non si dispone di due funzionante, proteggere le macchine virtuali Linux toowhich che è possibile connettersi da un punto qualsiasi in hello Internet.</span><span class="sxs-lookup"><span data-stu-id="3978a-105">We walk through hello process command by command, until you have two working, secure Linux VMs toowhich you can connect from anywhere on hello Internet.</span></span> <span data-ttu-id="3978a-106">È quindi possibile spostare su ambienti e reti complesse toomore.</span><span class="sxs-lookup"><span data-stu-id="3978a-106">Then you can move on toomore complex networks and environments.</span></span>

<span data-ttu-id="3978a-107">Lungo il percorso di hello, conoscere gerarchia delle dipendenze hello che offre modello di distribuzione di gestione risorse di hello e su quanta capacità fornisce.</span><span class="sxs-lookup"><span data-stu-id="3978a-107">Along hello way, you learn about hello dependency hierarchy that hello Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="3978a-108">Dopo aver visualizzato la modalità di compilazione sistema hello, è possibile ricompilare molto più rapidamente utilizzando [modelli di Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3978a-108">After you see how hello system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3978a-109">Inoltre, dopo aver appreso come hello parti dell'ambiente montate, creazione di modelli tooautomate li diventa più facile.</span><span class="sxs-lookup"><span data-stu-id="3978a-109">Also, after you learn how hello parts of your environment fit together, creating templates tooautomate them becomes easier.</span></span>

<span data-ttu-id="3978a-110">ambiente di Hello contiene:</span><span class="sxs-lookup"><span data-stu-id="3978a-110">hello environment contains:</span></span>

* <span data-ttu-id="3978a-111">Due VM all'interno di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="3978a-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="3978a-112">Un servizio di bilanciamento del carico con una regola di bilanciamento del carico sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="3978a-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="3978a-113">Rete gruppo di sicurezza (), le regole per la macchina virtuale dal traffico indesiderato tooprotect.</span><span class="sxs-lookup"><span data-stu-id="3978a-113">Network security group (NSG) rules tooprotect your VM from unwanted traffic.</span></span>

<span data-ttu-id="3978a-114">toocreate questo ambiente personalizzato, è necessario più recente hello [CLI di Azure 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in modalità di gestione risorse (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="3978a-114">toocreate this custom environment, you need hello latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="3978a-115">È inoltre necessario uno strumento di analisi JSON.</span><span class="sxs-lookup"><span data-stu-id="3978a-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="3978a-116">In questo esempio viene utilizzato [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="3978a-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3978a-117">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="3978a-117">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="3978a-118">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-118">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="3978a-119">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="3978a-119">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3978a-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="3978a-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="3978a-121">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="3978a-121">Quick commands</span></span>
<span data-ttu-id="3978a-122">Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base tooupload comandi tooAzure una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3978a-122">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="3978a-123">Ulteriori informazioni e il contesto per ogni passaggio è reperibile nel resto di hello del documento hello, a partire [qui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="3978a-123">More detailed information and context for each step can be found in hello rest of hello document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="3978a-124">Assicurarsi di aver [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:</span><span class="sxs-lookup"><span data-stu-id="3978a-124">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3978a-125">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="3978a-125">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3978a-126">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="3978a-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="3978a-127">Creare il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-127">Create hello resource group.</span></span> <span data-ttu-id="3978a-128">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` percorso:</span><span class="sxs-lookup"><span data-stu-id="3978a-128">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="3978a-129">Verificare che il gruppo di risorse hello utilizzando parser JSON hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-129">Verify hello resource group by using hello JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="3978a-130">Creare account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-130">Create hello storage account.</span></span> <span data-ttu-id="3978a-131">esempio Hello crea un account di archiviazione denominato `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="3978a-131">hello following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="3978a-132">(nome di account di archiviazione hello deve essere univoco, quindi fornire il proprio nome univoco.)</span><span class="sxs-lookup"><span data-stu-id="3978a-132">(hello storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="3978a-133">Verificare l'account di archiviazione hello utilizzando parser JSON hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-133">Verify hello storage account by using hello JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="3978a-134">Creare la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-134">Create hello virtual network.</span></span> <span data-ttu-id="3978a-135">esempio Hello crea una rete virtuale denominata `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="3978a-135">hello following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="3978a-136">Creare una subnet.</span><span class="sxs-lookup"><span data-stu-id="3978a-136">Create a subnet.</span></span> <span data-ttu-id="3978a-137">esempio Hello crea una subnet denominata `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="3978a-137">hello following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="3978a-138">Verificare la rete virtuale hello e subnet utilizzando parser JSON hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-138">Verify hello virtual network and subnet by using hello JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="3978a-139">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3978a-139">Create a public IP.</span></span> <span data-ttu-id="3978a-140">esempio Hello crea un indirizzo IP pubblico denominato `myPublicIP` con nome DNS hello `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="3978a-140">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="3978a-141">(nome DNS hello deve essere univoco, quindi fornire il proprio nome univoco.)</span><span class="sxs-lookup"><span data-stu-id="3978a-141">(hello DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="3978a-142">Creazione di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-142">Create hello load balancer.</span></span> <span data-ttu-id="3978a-143">esempio Hello crea un bilanciamento del carico denominato `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="3978a-143">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="3978a-144">Creare un pool IP front-end di bilanciamento del carico hello e associare l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-144">Create a front-end IP pool for hello load balancer, and associate hello public IP.</span></span> <span data-ttu-id="3978a-145">esempio Hello crea un pool IP front-end denominato `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="3978a-145">hello following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="3978a-146">Creare pool IP hello back-end di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-146">Create hello back-end IP pool for hello load balancer.</span></span> <span data-ttu-id="3978a-147">esempio Hello crea un pool IP back-end denominato `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="3978a-147">hello following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="3978a-148">Creare la rete in ingresso SSH regole translation (NAT) indirizzo di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-148">Create SSH inbound network address translation (NAT) rules for hello load balancer.</span></span> <span data-ttu-id="3978a-149">esempio Hello crea due regole di bilanciamento del carico, `myLoadBalancerRuleSSH1` e `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="3978a-149">hello following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="3978a-150">Creare web hello regole NAT in ingresso per hello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="3978a-150">Create hello web inbound NAT rules for hello load balancer.</span></span> <span data-ttu-id="3978a-151">esempio Hello crea una regola di bilanciamento del carico denominata `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="3978a-151">hello following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="3978a-152">Creare i probe di integrità bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-152">Create hello load balancer health probe.</span></span> <span data-ttu-id="3978a-153">esempio Hello crea un probe TCP denominato `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="3978a-153">hello following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="3978a-154">Verificare le regole NAT bilanciamento del carico hello e pool IP utilizzando parser JSON hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-154">Verify hello load balancer, IP pools, and NAT rules by using hello JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="3978a-155">Creare hello prima scheda di rete (NIC).</span><span class="sxs-lookup"><span data-stu-id="3978a-155">Create hello first network interface card (NIC).</span></span> <span data-ttu-id="3978a-156">Sostituire hello `#####-###-###` sezioni con il proprio ID sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="3978a-156">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="3978a-157">La sottoscrizione con ID è riportato un output di hello **jq** quando si esaminano le risorse di hello si sta creando.</span><span class="sxs-lookup"><span data-stu-id="3978a-157">Your subscription ID is noted in hello output of **jq** when you examine hello resources you are creating.</span></span> <span data-ttu-id="3978a-158">È anche possibile visualizzare l'ID sottoscrizione con `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="3978a-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="3978a-159">esempio Hello crea una scheda di rete denominata `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="3978a-159">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="3978a-160">Creare hello seconda scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="3978a-160">Create hello second NIC.</span></span> <span data-ttu-id="3978a-161">esempio Hello crea una scheda di rete denominata `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="3978a-161">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="3978a-162">Verificare hello due schede di rete utilizzando il parser JSON hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-162">Verify hello two NICs by using hello JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="3978a-163">Creare un gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-163">Create hello network security group.</span></span> <span data-ttu-id="3978a-164">esempio Hello crea un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="3978a-164">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="3978a-165">Aggiungere due regole in entrata per il gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-165">Add two inbound rules for hello network security group.</span></span> <span data-ttu-id="3978a-166">esempio Hello crea due regole, `myNetworkSecurityGroupRuleSSH` e `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="3978a-166">hello following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="3978a-167">Verificare le regole in entrata e gruppo di sicurezza di rete hello utilizzando parser JSON hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-167">Verify hello network security group and inbound rules by using hello JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="3978a-168">Associazione di sicurezza di rete hello toohello due schede di rete di gruppo:</span><span class="sxs-lookup"><span data-stu-id="3978a-168">Bind hello network security group toohello two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="3978a-169">Creare set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-169">Create hello availability set.</span></span> <span data-ttu-id="3978a-170">esempio Hello crea un set denominato di disponibilità `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="3978a-170">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="3978a-171">Creare hello prima VM Linux.</span><span class="sxs-lookup"><span data-stu-id="3978a-171">Create hello first Linux VM.</span></span> <span data-ttu-id="3978a-172">esempio Hello crea una macchina virtuale denominata `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="3978a-172">hello following example creates a VM named `myVM1`:</span></span>

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

<span data-ttu-id="3978a-173">Creare hello secondo VM Linux.</span><span class="sxs-lookup"><span data-stu-id="3978a-173">Create hello second Linux VM.</span></span> <span data-ttu-id="3978a-174">esempio Hello crea una macchina virtuale denominata `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="3978a-174">hello following example creates a VM named `myVM2`:</span></span>

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

<span data-ttu-id="3978a-175">Utilizzare hello JSON parser tooverify che tutto ciò che è stato compilato:</span><span class="sxs-lookup"><span data-stu-id="3978a-175">Use hello JSON parser tooverify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="3978a-176">Esportare il nuovo ambiente tooa tooquickly ricreare nuove istanze di modello:</span><span class="sxs-lookup"><span data-stu-id="3978a-176">Export your new environment tooa template tooquickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="3978a-177">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="3978a-177">Detailed walkthrough</span></span>
<span data-ttu-id="3978a-178">Hello dettagliati passaggi che seguono illustrano ogni comando operazioni eseguite durante la compilazione orizzontale dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="3978a-178">hello detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="3978a-179">Questi concetti torneranno utili in fase di creazione degli ambienti personalizzati per lo sviluppo o per la produzione.</span><span class="sxs-lookup"><span data-stu-id="3978a-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="3978a-180">Assicurarsi di aver [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:</span><span class="sxs-lookup"><span data-stu-id="3978a-180">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3978a-181">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="3978a-181">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3978a-182">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="3978a-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="3978a-183">Creare i gruppi di risorse e scegliere i percorsi di distribuzione</span><span class="sxs-lookup"><span data-stu-id="3978a-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="3978a-184">I gruppi di risorse di Azure sono entità logica di distribuzione che contengono informazioni e i metadati tooenable hello logica gestione della configurazione di distribuzioni di risorse.</span><span class="sxs-lookup"><span data-stu-id="3978a-184">Azure resource groups are logical deployment entities that contain configuration information and metadata tooenable hello logical management of resource deployments.</span></span> <span data-ttu-id="3978a-185">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` percorso:</span><span class="sxs-lookup"><span data-stu-id="3978a-185">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="3978a-186">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-186">Output:</span></span>

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

## <a name="create-a-storage-account"></a><span data-ttu-id="3978a-187">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3978a-187">Create a storage account</span></span>
<span data-ttu-id="3978a-188">È necessario l'account di archiviazione per i dischi di macchina virtuale e per qualsiasi disco dati aggiuntivo che si desidera tooadd.</span><span class="sxs-lookup"><span data-stu-id="3978a-188">You need storage accounts for your VM disks and for any additional data disks that you want tooadd.</span></span> <span data-ttu-id="3978a-189">Si creano account di archiviazione quasi subito dopo la creazione di gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="3978a-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="3978a-190">In questo caso si usa hello `azure storage account create` comando, passando il percorso di hello dell'account di hello, gruppo di risorse hello che controlla e tipo hello di supporto di archiviazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="3978a-190">Here we use hello `azure storage account create` command, passing hello location of hello account, hello resource group that controls it, and hello type of storage support you want.</span></span> <span data-ttu-id="3978a-191">esempio Hello crea un account di archiviazione denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="3978a-191">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="3978a-192">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="3978a-193">la risorsa gruppo mediante hello tooexamine `azure group show` comando, è possibile utilizzare hello [jq](https://stedolan.github.io/jq/) strumento insieme hello `--json` opzione CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="3978a-193">tooexamine our resource group by using hello `azure group show` command, let's use hello [jq](https://stedolan.github.io/jq/) tool along with hello `--json` Azure CLI option.</span></span> <span data-ttu-id="3978a-194">(È possibile utilizzare **jsawk** o qualsiasi libreria linguaggio si preferisce tooparse hello JSON.)</span><span class="sxs-lookup"><span data-stu-id="3978a-194">(You can use **jsawk** or any language library you prefer tooparse hello JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="3978a-195">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-195">Output:</span></span>

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

<span data-ttu-id="3978a-196">account di archiviazione tooinvestigate hello utilizzando hello CLI, è necessario innanzitutto le chiavi e nomi di account tooset hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-196">tooinvestigate hello storage account by using hello CLI, you first need tooset hello account names and keys.</span></span> <span data-ttu-id="3978a-197">Sostituire il nome di hello hello dell'account di archiviazione nel seguente esempio con un nome che si sceglie di hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-197">Replace hello name of hello storage account in hello following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="3978a-198">Dopodiché è possibile visualizzare facilmente le informazioni di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="3978a-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="3978a-199">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="3978a-200">Creare una rete virtuale e una subnet</span><span class="sxs-lookup"><span data-stu-id="3978a-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="3978a-201">Successivamente sarà tooneed toocreate una rete virtuale in esecuzione in Azure e una subnet in cui è possibile creare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3978a-201">Next you're going tooneed toocreate a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="3978a-202">esempio Hello crea una rete virtuale denominata `myVnet` con hello `192.168.0.0/16` prefisso dell'indirizzo:</span><span class="sxs-lookup"><span data-stu-id="3978a-202">hello following example creates a virtual network named `myVnet` with hello `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="3978a-203">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-203">Output:</span></span>

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

<span data-ttu-id="3978a-204">Nuovamente, consente di usare il possibilità - json hello di `azure group show` e `jq` toosee come svilupperemo le risorse.</span><span class="sxs-lookup"><span data-stu-id="3978a-204">Again, let's use hello --json option of `azure group show` and `jq` toosee how we're building our resources.</span></span> <span data-ttu-id="3978a-205">Ora sono disponibili una risorsa `storageAccounts` e una risorsa `virtualNetworks`.</span><span class="sxs-lookup"><span data-stu-id="3978a-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="3978a-206">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-206">Output:</span></span>

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

<span data-ttu-id="3978a-207">Ora è possibile crearne una subnet in hello `myVnet` rete virtuale in cui hello sono distribuite macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3978a-207">Now let's create a subnet in hello `myVnet` virtual network into which hello VMs are deployed.</span></span> <span data-ttu-id="3978a-208">Utilizziamo hello `azure network vnet subnet create` comando, insieme a risorse hello abbiamo creato: hello `myResourceGroup` gruppo di risorse e hello `myVnet` rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3978a-208">We use hello `azure network vnet subnet create` command, along with hello resources we've already created: hello `myResourceGroup` resource group and hello `myVnet` virtual network.</span></span> <span data-ttu-id="3978a-209">Nell'esempio seguente di hello, aggiungiamo subnet hello denominata `mySubnet` con prefisso dell'indirizzo di subnet hello `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="3978a-209">In hello following example, we add hello subnet named `mySubnet` with hello subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="3978a-210">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="3978a-211">Poiché subnet hello è logicamente all'interno di rete virtuale hello, cercare informazioni sulla subnet hello con un comando leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="3978a-211">Because hello subnet is logically inside hello virtual network, we look for hello subnet information with a slightly different command.</span></span> <span data-ttu-id="3978a-212">comando Hello utilizziamo `azure network vnet show`, ma si continua l'output JSON hello tooexamine utilizzando `jq`.</span><span class="sxs-lookup"><span data-stu-id="3978a-212">hello command we use is `azure network vnet show`, but we continue tooexamine hello JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="3978a-213">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-213">Output:</span></span>

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

## <a name="create-a-public-ip-address"></a><span data-ttu-id="3978a-214">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="3978a-214">Create a public IP address</span></span>
<span data-ttu-id="3978a-215">Ora è possibile crearne hello indirizzo IP pubblico (PIP) che vengono assegnati tooyour servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="3978a-215">Now let's create hello public IP address (PIP) that we assign tooyour load balancer.</span></span> <span data-ttu-id="3978a-216">La procedura permette tooconnect tooyour, le macchine virtuali da Internet hello utilizzando hello `azure network public-ip create` comando.</span><span class="sxs-lookup"><span data-stu-id="3978a-216">It enables you tooconnect tooyour VMs from hello Internet by using hello `azure network public-ip create` command.</span></span> <span data-ttu-id="3978a-217">Poiché l'indirizzo predefinito hello è dinamico, non è creare una voce DNS denominata in hello **cloudapp.azure.com** dominio utilizzando hello `--domain-name-label` opzione.</span><span class="sxs-lookup"><span data-stu-id="3978a-217">Because hello default address is dynamic, we create a named DNS entry in hello **cloudapp.azure.com** domain by using hello `--domain-name-label` option.</span></span> <span data-ttu-id="3978a-218">esempio Hello crea un indirizzo IP pubblico denominato `myPublicIP` con nome DNS hello `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="3978a-218">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="3978a-219">Poiché il nome DNS hello deve essere univoco, è fornire il proprio nome DNS univoco:</span><span class="sxs-lookup"><span data-stu-id="3978a-219">Because hello DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="3978a-220">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
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

<span data-ttu-id="3978a-221">Hello indirizzo IP pubblico è anche una risorsa di primo livello, in modo da visualizzare con `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="3978a-221">hello public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="3978a-222">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-222">Output:</span></span>

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

<span data-ttu-id="3978a-223">È possibile esaminare ulteriori dettagli di risorse, inclusi il nome di dominio completo hello (FQDN) del sottodominio hello, utilizzando hello completo `azure network public-ip show` comando.</span><span class="sxs-lookup"><span data-stu-id="3978a-223">You can investigate more resource details, including hello fully qualified domain name (FQDN) of hello subdomain, by using hello complete `azure network public-ip show` command.</span></span> <span data-ttu-id="3978a-224">risorsa di indirizzo IP pubblica Hello è stata allocata in modo logico, ma non è ancora stato assegnato un indirizzo specifico.</span><span class="sxs-lookup"><span data-stu-id="3978a-224">hello public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="3978a-225">tooobtain un indirizzo IP, sarà tooneed un bilanciamento del carico, non è stato ancora creato.</span><span class="sxs-lookup"><span data-stu-id="3978a-225">tooobtain an IP address, you're going tooneed a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="3978a-226">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-226">Output:</span></span>

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

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="3978a-227">Creare un servizio di bilanciamento del carico e i pool di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="3978a-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="3978a-228">Quando si crea un bilanciamento del carico, consente il traffico toodistribute tra più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3978a-228">When you create a load balancer, it enables you toodistribute traffic across multiple VMs.</span></span> <span data-ttu-id="3978a-229">Fornisce inoltre l'applicazione tooyour ridondanza tramite l'esecuzione di più macchine virtuali che rispondono a richieste toouser nell'evento di hello di manutenzione o di notevoli carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3978a-229">It also provides redundancy tooyour application by running multiple VMs that respond toouser requests in hello event of maintenance or heavy loads.</span></span> <span data-ttu-id="3978a-230">esempio Hello crea un bilanciamento del carico denominato `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="3978a-230">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="3978a-231">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="3978a-232">Il servizio di bilanciamento del carico è piuttosto vuoto, per cui si creeranno alcuni pool di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="3978a-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="3978a-233">Vogliamo toocreate due pool IP per il bilanciamento del carico, una per i componenti front-end hello e uno per back-end hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-233">We want toocreate two IP pools for our load balancer, one for hello front end and one for hello back end.</span></span> <span data-ttu-id="3978a-234">il pool IP front-end di Hello è visibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="3978a-234">hello front-end IP pool is publicly visible.</span></span> <span data-ttu-id="3978a-235">È inoltre toowhich percorso hello che assegniamo hello PIP creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3978a-235">It's also hello location toowhich we assign hello PIP that we created earlier.</span></span> <span data-ttu-id="3978a-236">Quindi utilizziamo pool back-end hello come un percorso per il nostro tooconnect macchine virtuali per.</span><span class="sxs-lookup"><span data-stu-id="3978a-236">Then we use hello back-end pool as a location for our VMs tooconnect to.</span></span> <span data-ttu-id="3978a-237">In questo modo, hello il traffico tramite toohello di bilanciamento carico di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3978a-237">That way, hello traffic can flow through hello load balancer toohello VMs.</span></span>

<span data-ttu-id="3978a-238">Prima di tutto si creerà il pool di indirizzi IP front-end.</span><span class="sxs-lookup"><span data-stu-id="3978a-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="3978a-239">esempio Hello crea un pool di server front-end denominato `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="3978a-239">hello following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="3978a-240">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="3978a-241">Si noti come è possibile usare hello `--public-ip-name` attivare toopass hello `myPublicIP` creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3978a-241">Note how we used hello `--public-ip-name` switch toopass in hello `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="3978a-242">Assegnazione indirizzo IP pubblico hello servizio di bilanciamento del carico indirizzo toohello consente tooreach le macchine virtuali tra hello Internet.</span><span class="sxs-lookup"><span data-stu-id="3978a-242">Assigning hello public IP address toohello load balancer allows you tooreach your VMs across hello Internet.</span></span>

<span data-ttu-id="3978a-243">Quindi si creerà il secondo pool di indirizzi IP, questa volta per il traffico back-end.</span><span class="sxs-lookup"><span data-stu-id="3978a-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="3978a-244">esempio Hello crea un pool back-end denominato `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="3978a-244">hello following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="3978a-245">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="3978a-246">È possibile osservare come il bilanciamento del carico procede esaminando con `azure network lb show` ed esaminando l'output JSON hello:</span><span class="sxs-lookup"><span data-stu-id="3978a-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining hello JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="3978a-247">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-247">Output:</span></span>

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

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="3978a-248">Creare le regole NAT per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="3978a-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="3978a-249">traffico tooget che passano attraverso il servizio di bilanciamento del carico, è necessario la regole toocreate network address translation (NAT) che specificano le azioni in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="3978a-249">tooget traffic flowing through our load balancer, we need toocreate network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="3978a-250">È possibile specificare hello protocollo toouse, quindi eseguire il mapping di porte toointernal porte esterne come desiderato.</span><span class="sxs-lookup"><span data-stu-id="3978a-250">You can specify hello protocol toouse, then map external ports toointernal ports as desired.</span></span> <span data-ttu-id="3978a-251">Per l'ambiente, creare alcune regole che consentono di SSH tramite il nostro tooour del servizio di bilanciamento carico di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3978a-251">For our environment, let's create some rules that allow SSH through our load balancer tooour VMs.</span></span> <span data-ttu-id="3978a-252">È necessario impostare la porta TCP porte 4222 e 4223 toodirect tooTCP 22 nel nostro macchine virtuali (che si creano più avanti).</span><span class="sxs-lookup"><span data-stu-id="3978a-252">We set up TCP ports 4222 and 4223 toodirect tooTCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="3978a-253">esempio Hello crea una regola denominata `myLoadBalancerRuleSSH1` toomap TCP porta 4222 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="3978a-253">hello following example creates a rule named `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="3978a-254">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
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

<span data-ttu-id="3978a-255">Ripetere la procedura hello per la seconda regola NAT per SSH.</span><span class="sxs-lookup"><span data-stu-id="3978a-255">Repeat hello procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="3978a-256">esempio Hello crea una regola denominata `myLoadBalancerRuleSSH2` toomap TCP porta 4223 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="3978a-256">hello following example creates a rule named `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="3978a-257">Verrà inoltre proseguo e creare una regola NAT per la porta TCP 80 per il traffico web, l'associazione di pool IP tooour regola hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking hello rule up tooour IP pools.</span></span> <span data-ttu-id="3978a-258">Se è collegare hello regola tooan pool IP, anziché l'associazione di hello regola tooour macchine virtuali singolarmente, è possibile aggiungere o rimuovere le macchine virtuali dal pool IP hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-258">If we hook up hello rule tooan IP pool, instead of hooking up hello rule tooour VMs individually, we can add or remove VMs from hello IP pool.</span></span> <span data-ttu-id="3978a-259">servizio di bilanciamento del carico Hello regola automaticamente il flusso di hello del traffico.</span><span class="sxs-lookup"><span data-stu-id="3978a-259">hello load balancer automatically adjusts hello flow of traffic.</span></span> <span data-ttu-id="3978a-260">esempio Hello crea una regola denominata `myLoadBalancerRuleWeb` toomap TCP porta 80 tooport 80:</span><span class="sxs-lookup"><span data-stu-id="3978a-260">hello following example creates a rule named `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="3978a-261">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
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

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="3978a-262">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="3978a-262">Create a load balancer health probe</span></span>
<span data-ttu-id="3978a-263">Integrità di probe periodicamente controlli sulle macchine virtuali che si trovano dietro il nostro toomake bilanciamento di carico che è operativo e risponde toorequests come definito hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-263">A health probe periodically checks on hello VMs that are behind our load balancer toomake sure they're operating and responding toorequests as defined.</span></span> <span data-ttu-id="3978a-264">Se non vengono rimossi dal tooensure operazione che gli utenti non vengono indirizzate toothem.</span><span class="sxs-lookup"><span data-stu-id="3978a-264">If not, they're removed from operation tooensure that users aren't being directed toothem.</span></span> <span data-ttu-id="3978a-265">È possibile definire controlli personalizzati per il probe di integrità hello, insieme a intervalli e i valori di timeout.</span><span class="sxs-lookup"><span data-stu-id="3978a-265">You can define custom checks for hello health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="3978a-266">Per altre informazioni sui probe di integrità, vedere [Probe di integrità del servizio di bilanciamento del carico](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3978a-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3978a-267">esempio Hello crea un TCP integrità sondati denominata `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="3978a-267">hello following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="3978a-268">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="3978a-269">In questo caso è stato specificato un intervallo di 15 secondi per i controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="3978a-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="3978a-270">È possibile perdere un massimo di quattro probe (un minuto) prima di bilanciamento del carico hello considera che ospitano hello non funziona più.</span><span class="sxs-lookup"><span data-stu-id="3978a-270">We can miss a maximum of four probes (one minute) before hello load balancer considers that hello host is no longer functioning.</span></span>

## <a name="verify-hello-load-balancer"></a><span data-ttu-id="3978a-271">Verificare di bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="3978a-271">Verify hello load balancer</span></span>
<span data-ttu-id="3978a-272">Dopo l'operazione di configurazione di bilanciamento del carico hello viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="3978a-272">Now hello load balancer configuration is done.</span></span> <span data-ttu-id="3978a-273">Di seguito sono hello passaggi:</span><span class="sxs-lookup"><span data-stu-id="3978a-273">Here are hello steps you took:</span></span>

1. <span data-ttu-id="3978a-274">È stato creato un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="3978a-274">You created a load balancer.</span></span>
2. <span data-ttu-id="3978a-275">È stato creato un pool IP front-end e un tooit IP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="3978a-275">You created a front-end IP pool and assigned a public IP tooit.</span></span>
3. <span data-ttu-id="3978a-276">È stato creato un pool IP back-end a cui possono connettersi le VM.</span><span class="sxs-lookup"><span data-stu-id="3978a-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="3978a-277">Le regole NAT che consentono di macchine virtuali toohello SSH per la gestione, insieme a una regola che consenta la porta TCP 80 per l'app web creata.</span><span class="sxs-lookup"><span data-stu-id="3978a-277">You created NAT rules that allow SSH toohello VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="3978a-278">È stato aggiunto un hello di integrità probe tooperiodically controllo macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3978a-278">You added a health probe tooperiodically check hello VMs.</span></span> <span data-ttu-id="3978a-279">Questo probe di integrità garantisce che gli utenti non tentano tooaccess una macchina virtuale che non è più funzionante o del contenuto.</span><span class="sxs-lookup"><span data-stu-id="3978a-279">This health probe ensures that users don't try tooaccess a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="3978a-280">Ecco il bilanciamento del carico risultante:</span><span class="sxs-lookup"><span data-stu-id="3978a-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="3978a-281">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-281">Output:</span></span>

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

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a><span data-ttu-id="3978a-282">Creare un toouse NIC con hello VM Linux</span><span class="sxs-lookup"><span data-stu-id="3978a-282">Create an NIC toouse with hello Linux VM</span></span>
<span data-ttu-id="3978a-283">Schede di rete disponibili a livello di codice in quanto è possibile applicare regole tootheir utilizzare.</span><span class="sxs-lookup"><span data-stu-id="3978a-283">NICs are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="3978a-284">È inoltre possibile averne più di una.</span><span class="sxs-lookup"><span data-stu-id="3978a-284">You can also have more than one.</span></span> <span data-ttu-id="3978a-285">In seguito hello `azure network nic create` dei comandi, si agganciare i pool IP hello NIC toohello carico back-end e associarlo a hello traffico SSH toopermit di regole NAT.</span><span class="sxs-lookup"><span data-stu-id="3978a-285">In hello following `azure network nic create` command, you hook up hello NIC toohello load back-end IP pool and associate it with hello NAT rule toopermit SSH traffic.</span></span>

<span data-ttu-id="3978a-286">Sostituire hello `#####-###-###` sezioni con il proprio ID sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="3978a-286">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="3978a-287">La sottoscrizione con ID è riportato un output di hello `jq` quando si esaminano le risorse di hello si sta creando.</span><span class="sxs-lookup"><span data-stu-id="3978a-287">Your subscription ID is noted in hello output of `jq` when you examine hello resources you are creating.</span></span> <span data-ttu-id="3978a-288">È anche possibile visualizzare l'ID sottoscrizione con `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="3978a-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="3978a-289">esempio Hello crea una scheda di rete denominata `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="3978a-289">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="3978a-290">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
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

<span data-ttu-id="3978a-291">È possibile visualizzare i dettagli di hello esaminando risorse hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="3978a-291">You can see hello details by examining hello resource directly.</span></span> <span data-ttu-id="3978a-292">Si esamina la risorsa hello utilizzando hello `azure network nic show` comando:</span><span class="sxs-lookup"><span data-stu-id="3978a-292">You examine hello resource by using hello `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="3978a-293">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-293">Output:</span></span>

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

<span data-ttu-id="3978a-294">Ora è creare hello seconda scheda di rete, collegare nuovamente nel pool IP tooour back-end.</span><span class="sxs-lookup"><span data-stu-id="3978a-294">Now we create hello second NIC, hooking in tooour back-end IP pool again.</span></span> <span data-ttu-id="3978a-295">Questa regola NAT secondo tempo hello consenta il traffico SSH.</span><span class="sxs-lookup"><span data-stu-id="3978a-295">This time hello second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="3978a-296">esempio Hello crea una scheda di rete denominata `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="3978a-296">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="3978a-297">Creare un gruppo di sicurezza di rete e le regole corrispondenti</span><span class="sxs-lookup"><span data-stu-id="3978a-297">Create a network security group and rules</span></span>
<span data-ttu-id="3978a-298">Ora verrà creato un gruppo di sicurezza di rete e hello per le regole in entrata che regolano l'accesso toohello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="3978a-298">Now we create a network security group and hello inbound rules that govern access toohello NIC.</span></span> <span data-ttu-id="3978a-299">Un gruppo di sicurezza di rete può essere applicato tooa NIC o subnet.</span><span class="sxs-lookup"><span data-stu-id="3978a-299">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="3978a-300">Definire un flusso di hello toocontrol regole del traffico da e verso le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3978a-300">You define rules toocontrol hello flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="3978a-301">esempio Hello crea un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="3978a-301">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="3978a-302">Aggiungere la regola in ingresso di hello per hello NSG tooallow connessioni sulla porta 22 (toosupport SSH) in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3978a-302">Let's add hello inbound rule for hello NSG tooallow inbound connections on port 22 (toosupport SSH).</span></span> <span data-ttu-id="3978a-303">esempio Hello crea una regola denominata `myNetworkSecurityGroupRuleSSH` tooallow TCP sulla porta 22:</span><span class="sxs-lookup"><span data-stu-id="3978a-303">hello following example creates a rule named `myNetworkSecurityGroupRuleSSH` tooallow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="3978a-304">A questo punto aggiungere la regola in ingresso di hello per hello NSG tooallow connessioni sulla porta 80 (traffico web toosupport) in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3978a-304">Now let's add hello inbound rule for hello NSG tooallow inbound connections on port 80 (toosupport web traffic).</span></span> <span data-ttu-id="3978a-305">esempio Hello crea una regola denominata `myNetworkSecurityGroupRuleHTTP` tooallow TCP sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="3978a-305">hello following example creates a rule named `myNetworkSecurityGroupRuleHTTP` tooallow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="3978a-306">regola connessioni in entrata Hello è un filtro per le connessioni di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3978a-306">hello inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="3978a-307">In questo esempio viene eseguita l'associazione hello NSG toohello NIC virtuale le macchine virtuali, il che significa che qualsiasi tooport richiesta 22 è passato toohello NIC la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3978a-307">In this example, we bind hello NSG toohello VMs virtual NIC, which means that any request tooport 22 is passed through toohello NIC on our VM.</span></span> <span data-ttu-id="3978a-308">Questa regola è relativa alla connessione di rete anziché all'endpoint, come invece sarebbe nelle distribuzioni classiche.</span><span class="sxs-lookup"><span data-stu-id="3978a-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="3978a-309">tooopen una porta, è necessario lasciare hello `--source-port-range` impostare troppo '\*' tooaccept (valore predefinito di hello) in entrata delle richieste da **qualsiasi** porta richiesta.</span><span class="sxs-lookup"><span data-stu-id="3978a-309">tooopen a port, you must leave hello `--source-port-range` set too'\*' (hello default value) tooaccept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="3978a-310">Le porte sono solitamente dinamiche.</span><span class="sxs-lookup"><span data-stu-id="3978a-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-toohello-nic"></a><span data-ttu-id="3978a-311">Associare toohello NIC</span><span class="sxs-lookup"><span data-stu-id="3978a-311">Bind toohello NIC</span></span>
<span data-ttu-id="3978a-312">Associare hello toohello di gruppo NIC.</span><span class="sxs-lookup"><span data-stu-id="3978a-312">Bind hello NSG toohello NICs.</span></span> <span data-ttu-id="3978a-313">È necessario tooconnect nostri NIC con il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="3978a-313">We need tooconnect our NICs with our network security group.</span></span> <span data-ttu-id="3978a-314">Eseguire entrambi i comandi, toohook di entrambi i nostri schede di rete:</span><span class="sxs-lookup"><span data-stu-id="3978a-314">Run both commands, toohook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="3978a-315">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="3978a-315">Create an availability set</span></span>
<span data-ttu-id="3978a-316">I set di disponibilità agevolano la distribuzione delle VM nei domini di errore e domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3978a-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="3978a-317">Si creerà un set di disponibilità per le VM.</span><span class="sxs-lookup"><span data-stu-id="3978a-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="3978a-318">esempio Hello crea un set denominato di disponibilità `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="3978a-318">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="3978a-319">I domini di errore definiscono un gruppo di macchine virtuali che condividono una fonte di alimentazione e uno switch di rete comuni.</span><span class="sxs-lookup"><span data-stu-id="3978a-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="3978a-320">Per impostazione predefinita, hello le macchine virtuali configurate all'interno del set di disponibilità sono separate tra i domini di errore toothree.</span><span class="sxs-lookup"><span data-stu-id="3978a-320">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="3978a-321">l'idea Hello è un problema hardware in uno di questi domini di errore non influisce sulla ogni macchina virtuale che esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="3978a-321">hello idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="3978a-322">Durante il posizionamento in un set di disponibilità, Azure distribuisce automaticamente le macchine virtuali in domini di errore hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-322">Azure automatically distributes VMs across hello fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="3978a-323">Indicano i domini di aggiornamento gruppi di macchine virtuali e l'hardware fisico sottostante che può essere riavviata in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="3978a-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="3978a-324">ordine di Hello in cui vengono riavviati i domini di aggiornamento potrebbe non essere sequenziale durante la manutenzione pianificata, ma solo un aggiornamento è stato riavviato alla volta.</span><span class="sxs-lookup"><span data-stu-id="3978a-324">hello order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="3978a-325">D nuovo, Azure distribuisce automaticamente le VM tra i domini di aggiornamento durante il posizionamento in un sito di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="3978a-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="3978a-326">Altre informazioni sui [la gestione della disponibilità di hello di macchine virtuali](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3978a-326">Read more about [managing hello availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-hello-linux-vms"></a><span data-ttu-id="3978a-327">Creare le macchine virtuali Linux hello</span><span class="sxs-lookup"><span data-stu-id="3978a-327">Create hello Linux VMs</span></span>
<span data-ttu-id="3978a-328">Risorse di archiviazione e rete hello aver creato le macchine virtuali toosupport accessibile tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="3978a-328">You've created hello storage and network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="3978a-329">Ora è possibile creare quelle VM e proteggerle con una chiave SSH priva di password.</span><span class="sxs-lookup"><span data-stu-id="3978a-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="3978a-330">In questo caso, verrà toocreate una VM Ubuntu in base a hello LTS più recente.</span><span class="sxs-lookup"><span data-stu-id="3978a-330">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="3978a-331">Per trovare le informazioni sull'immagine si usa `azure vm image list`, come descritto nell'articolo relativo alla [ricerca di immagini di VM di Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3978a-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3978a-332">È stata selezionata un'immagine utilizzando il comando hello `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="3978a-332">We selected an image by using hello command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="3978a-333">In questo caso, si usa `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="3978a-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="3978a-334">Ultimo campo hello, passiamo `latest` in modo che in futuro hello è ottenere sempre la compilazione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-334">For hello last field, we pass `latest` so that in hello future we always get hello most recent build.</span></span> <span data-ttu-id="3978a-335">(stringa hello utilizziamo `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="3978a-335">(hello string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="3978a-336">Il passaggio successivo è familiare tooanyone che ha già creato un ssh chiave pubblica e privata rsa associare in Linux o Mac usando **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="3978a-336">This next step is familiar tooanyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="3978a-337">Se non si dispone di alcuna coppia di chiavi del certificato nella directory `~/.ssh` , è possibile crearle:</span><span class="sxs-lookup"><span data-stu-id="3978a-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="3978a-338">Automaticamente, tramite hello `azure vm create --generate-ssh-keys` opzione.</span><span class="sxs-lookup"><span data-stu-id="3978a-338">Automatically, by using hello `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="3978a-339">Manualmente, utilizzando [toocreate istruzioni hello li manualmente](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3978a-339">Manually, by using [hello instructions toocreate them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3978a-340">In alternativa, è possibile utilizzare hello `--admin-password` metodo tooauthenticate le connessioni SSH dopo hello macchina virtuale viene creato.</span><span class="sxs-lookup"><span data-stu-id="3978a-340">Alternatively, you can use hello `--admin-password` method tooauthenticate your SSH connections after hello VM is created.</span></span> <span data-ttu-id="3978a-341">Di solito, questo metodo risulta essere meno sicuro.</span><span class="sxs-lookup"><span data-stu-id="3978a-341">This method is typically less secure.</span></span>

<span data-ttu-id="3978a-342">Creiamo hello VM riportando tutti i risorse e informazioni insieme hello `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="3978a-342">We create hello VM by bringing all our resources and information together with hello `azure vm create` command:</span></span>

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

<span data-ttu-id="3978a-343">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="3978a-344">È possibile connettersi immediatamente tooyour VM utilizzando le chiavi SSH predefinito.</span><span class="sxs-lookup"><span data-stu-id="3978a-344">You can connect tooyour VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="3978a-345">Assicurarsi di specificare la porta appropriata hello poiché passaggio tramite bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-345">Make sure that you specify hello appropriate port since we're passing through hello load balancer.</span></span> <span data-ttu-id="3978a-346">(Per la prima macchina virtuale, è necessario impostare hello NAT regola tooforward porta 4222 tooour VM.)</span><span class="sxs-lookup"><span data-stu-id="3978a-346">(For our first VM, we set up hello NAT rule tooforward port 4222 tooour VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="3978a-347">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-347">Output:</span></span>

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="3978a-348">Vado avanti e creare la seconda macchina virtuale in hello allo stesso modo:</span><span class="sxs-lookup"><span data-stu-id="3978a-348">Go ahead and create your second VM in hello same manner:</span></span>

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

<span data-ttu-id="3978a-349">Ed è ora possibile usare hello `azure vm show myResourceGroup myVM1` comando tooexamine è stato creato.</span><span class="sxs-lookup"><span data-stu-id="3978a-349">And you can now use hello `azure vm show myResourceGroup myVM1` command tooexamine what you've created.</span></span> <span data-ttu-id="3978a-350">A questo punto le VM Ubuntu sono in esecuzione dietro al bilanciamento del carico in Azure a cui è possibile accedere solo con la coppia di chiavi SSH, dal momento che le password sono disabilitate.</span><span class="sxs-lookup"><span data-stu-id="3978a-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="3978a-351">È possibile installare nginx o httpd, distribuire un'app web e visualizzare il traffico hello scorrono tooboth del servizio di bilanciamento carico di hello di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-351">You can install nginx or httpd, deploy a web app, and see hello traffic flow through hello load balancer tooboth of hello VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="3978a-352">Output:</span><span class="sxs-lookup"><span data-stu-id="3978a-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
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


## <a name="export-hello-environment-as-a-template"></a><span data-ttu-id="3978a-353">Esportazione hello ambiente come modello</span><span class="sxs-lookup"><span data-stu-id="3978a-353">Export hello environment as a template</span></span>
<span data-ttu-id="3978a-354">Dopo aver creato questo ambiente, cosa accade se si desidera toocreate un ambiente di sviluppo aggiuntive con hello stessi parametri o un ambiente di produzione a esso corrispondente?</span><span class="sxs-lookup"><span data-stu-id="3978a-354">Now that you have built out this environment, what if you want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="3978a-355">Gestione risorse Usa i modelli JSON che definiscono tutti i parametri di hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="3978a-355">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="3978a-356">È possibile creare interi ambienti facendo riferimento a questo modello JSON.</span><span class="sxs-lookup"><span data-stu-id="3978a-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="3978a-357">È possibile [creare manualmente modelli JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o esportare un modello JSON hello di toocreate ambiente esistente per l'utente:</span><span class="sxs-lookup"><span data-stu-id="3978a-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="3978a-358">Questo comando Crea hello `myResourceGroup.json` file nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="3978a-358">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="3978a-359">Quando si crea un ambiente da questo modello, viene chiesto di tutti i nomi risorsa hello, inclusi i nomi di hello per le macchine virtuali, le interfacce di rete o bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-359">When you create an environment from this template, you are prompted for all hello resource names, including hello names for hello load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="3978a-360">È possibile popolare questi nomi nel file di modello aggiungendo hello `-p` o `--includeParameterDefaultValue` parametro toohello `azure group export` comando illustrata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3978a-360">You can populate these names in your template file by adding hello `-p` or `--includeParameterDefaultValue` parameter toohello `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="3978a-361">Modifica i nome di risorsa hello JSON modelli toospecify, o [creare un file parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) che specifica i nomi delle risorse hello.</span><span class="sxs-lookup"><span data-stu-id="3978a-361">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="3978a-362">toocreate un ambiente in base al modello:</span><span class="sxs-lookup"><span data-stu-id="3978a-362">toocreate an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="3978a-363">Potrebbe essere necessario tooread [altre informazioni su come toodeploy dai modelli](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3978a-363">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3978a-364">Informazioni su come utilizzare i file dei parametri hello tooincrementally aggiornamento ambienti e accedere ai modelli da un unico percorso di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3978a-364">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3978a-365">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3978a-365">Next steps</span></span>
<span data-ttu-id="3978a-366">Ora si è pronti toobegin utilizzo di più componenti di rete e le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3978a-366">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="3978a-367">È possibile utilizzare questo toobuild ambiente di esempio dell'applicazione utilizzando i componenti di base hello introdotti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="3978a-367">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
