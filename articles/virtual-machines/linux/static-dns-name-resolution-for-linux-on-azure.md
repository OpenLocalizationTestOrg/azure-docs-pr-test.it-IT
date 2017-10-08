---
title: aaaUse DNS interno per la macchina virtuale la risoluzione dei nomi con hello Azure CLI 2.0 | Documenti Microsoft
description: Come la rete virtuale toocreate schede di interfaccia e utilizzare DNS interno per la risoluzione dei nomi di macchina virtuale in Azure con hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="05c22-103">Creare schede di interfaccia di rete virtuale e usare DNS interni per la risoluzione dei nomi di VM in Azure</span><span class="sxs-lookup"><span data-stu-id="05c22-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="05c22-104">Questo articolo illustra come tooset statici nomi DNS interni per le macchine virtuali Linux mediante rete schede di interfaccia (vNics) e i nomi DNS con etichetta con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="05c22-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="05c22-105">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05c22-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="05c22-106">Si ricorre ai nomi DNS statici per i servizi di infrastruttura permanenti, ad esempio per un server di compilazione Jenkins, usato per questo documento, o un server Git.</span><span class="sxs-lookup"><span data-stu-id="05c22-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="05c22-107">requisiti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="05c22-107">hello requirements are:</span></span>

* [<span data-ttu-id="05c22-108">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="05c22-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="05c22-109">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="05c22-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="05c22-110">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="05c22-110">Quick commands</span></span>
<span data-ttu-id="05c22-111">Se è necessario tooquickly attività hello, hello successiva sezione Dettagli comandi hello necessari.</span><span class="sxs-lookup"><span data-stu-id="05c22-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="05c22-112">Ulteriori informazioni e il contesto per ogni passaggio è reperibile nel resto di hello del documento hello, [avvio qui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="05c22-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="05c22-113">tooperform questi passaggi, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="05c22-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="05c22-114">Pre-requisiti: gruppo di risorse, rete virtuale e subnet, gruppo di sicurezza di rete con SSH in ingresso.</span><span class="sxs-lookup"><span data-stu-id="05c22-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="05c22-115">Creare una scheda di interfaccia di rete virtuale con un nome DNS interno statico</span><span class="sxs-lookup"><span data-stu-id="05c22-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="05c22-116">Creare una scheda di rete virtuale hello con [az rete nic creare](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="05c22-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="05c22-117">Hello `--internal-dns-name` flag CLI è per l'etichetta DNS di impostazione hello, che fornisce nome DNS statico hello per scheda di interfaccia di rete virtuale hello (vNic).</span><span class="sxs-lookup"><span data-stu-id="05c22-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="05c22-118">esempio Hello crea una scheda di rete virtuale denominata `myNic`, connetterla toohello `myVnet` rete virtuale e viene creato un record di nome DNS interno denominato `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="05c22-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="05c22-119">Distribuire una macchina virtuale e connettersi hello vNic</span><span class="sxs-lookup"><span data-stu-id="05c22-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="05c22-120">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="05c22-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="05c22-121">Hello `--nics` flag si connette hello vNic toohello VM durante hello tooAzure di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="05c22-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="05c22-122">esempio Hello crea una macchina virtuale denominata `myVM` con i dischi di Azure gestita e collega hello vNic denominato `myNic` da hello passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="05c22-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="05c22-123">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="05c22-123">Detailed walkthrough</span></span>

<span data-ttu-id="05c22-124">Un'integrazione completa continua e distribuzione continua (CiCd) infrastruttura di Azure richiede alcuni server server toobe statico o di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="05c22-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="05c22-125">È consigliabile che le risorse di Azure come hello reti virtuali e i gruppi di sicurezza di rete sono statiche e le risorse distribuite raramente di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="05c22-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="05c22-126">Dopo la distribuzione di una rete virtuale, può essere riutilizzato per nuove distribuzioni senza alcuna infrastruttura toohello effetto negativo.</span><span class="sxs-lookup"><span data-stu-id="05c22-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="05c22-127">È quindi possibile aggiungere un server di repository Git o un server di automazione di Jenkins recapita CiCd toothis di rete virtuale per gli ambienti di sviluppo o test.</span><span class="sxs-lookup"><span data-stu-id="05c22-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="05c22-128">I nomi DNS interni sono risolvibili solo all'interno di una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="05c22-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="05c22-129">I nomi DNS hello sono interni, pertanto non sono toohello risolvibile all'esterno di internet, offre un'infrastruttura toohello aggiuntiva di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="05c22-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="05c22-130">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="05c22-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="05c22-131">I nomi dei parametri di esempio includono `myResourceGroup`, `myNic` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="05c22-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="05c22-132">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="05c22-132">Create hello resource group</span></span>
<span data-ttu-id="05c22-133">Innanzitutto, creare il gruppo di risorse hello con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="05c22-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="05c22-134">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westus` percorso:</span><span class="sxs-lookup"><span data-stu-id="05c22-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="05c22-135">Creare una rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="05c22-135">Create hello virtual network</span></span>

<span data-ttu-id="05c22-136">passaggio successivo Hello è toobuild toolaunch una rete virtuale hello macchine virtuali in.</span><span class="sxs-lookup"><span data-stu-id="05c22-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="05c22-137">rete virtuale Hello contiene una subnet per questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="05c22-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="05c22-138">Per ulteriori informazioni su reti virtuali di Azure, vedere [creare una rete virtuale mediante Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05c22-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="05c22-139">Creare una rete virtuale di hello con [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="05c22-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="05c22-140">esempio Hello crea una rete virtuale denominata `myVnet` e subnet denominata `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="05c22-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="05c22-141">Creare il gruppo di sicurezza di rete hello</span><span class="sxs-lookup"><span data-stu-id="05c22-141">Create hello Network Security Group</span></span>
<span data-ttu-id="05c22-142">Azure i gruppi di sicurezza di rete sono equivalenti tooa firewall a livello di rete hello.</span><span class="sxs-lookup"><span data-stu-id="05c22-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="05c22-143">Per ulteriori informazioni sui gruppi di sicurezza di rete, vedere [come NSGs toocreate in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05c22-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="05c22-144">Creare un gruppo di sicurezza di rete hello con [rete az creare](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="05c22-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="05c22-145">esempio Hello crea un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="05c22-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="05c22-146">Aggiungere un tooallow regola in entrata SSH</span><span class="sxs-lookup"><span data-stu-id="05c22-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="05c22-147">Aggiungere una regola in ingresso per il gruppo di sicurezza di rete hello con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="05c22-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="05c22-148">esempio Hello crea una regola denominata `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="05c22-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="05c22-149">Associare subnet hello hello il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="05c22-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="05c22-150">subnet hello tooassociate hello gruppo di sicurezza di rete, utilizzare [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="05c22-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="05c22-151">esempio Hello associa il nome di subnet hello `mySubnet` con il gruppo di sicurezza di rete denominata hello `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="05c22-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="05c22-152">Creare una scheda di interfaccia di rete virtuale hello e i nomi DNS statici</span><span class="sxs-lookup"><span data-stu-id="05c22-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="05c22-153">Azure è molto flessibile, ma toouse i nomi DNS per la risoluzione dei nomi di macchina virtuale, è necessario toocreate virtuale schede di rete (vNics) che includono un'etichetta DNS.</span><span class="sxs-lookup"><span data-stu-id="05c22-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="05c22-154">vNics sono importanti per poterli usare di nuovo connettendo le macchine virtuali toodifferent sul ciclo di vita di hello infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="05c22-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="05c22-155">Questo approccio consente di mantenere hello vNic come una risorsa statica durante hello macchine virtuali può essere temporaneo.</span><span class="sxs-lookup"><span data-stu-id="05c22-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="05c22-156">Tramite l'assegnazione di etichette su NIC virtuale hello DNS, siamo tooenable in grado di risoluzione dei nomi semplici da altre macchine virtuali nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="05c22-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="05c22-157">Utilizzo dei nomi di risolvibili consente altri server di automazione hello tooaccess macchine virtuali in base al nome DNS hello `Jenkins` o di server di Git hello `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="05c22-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="05c22-158">Creare una scheda di rete virtuale hello con [az rete nic creare](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="05c22-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="05c22-159">esempio Hello crea una scheda di rete virtuale denominata `myNic`, connetterla toohello `myVnet` rete virtuale denominata `myVnet`e viene creato un record di nome DNS interno denominato `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="05c22-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="05c22-160">Distribuire hello VM nell'infrastruttura di rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="05c22-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="05c22-161">È ora disponibile una rete virtuale e una subnet, un gruppo di sicurezza di rete che agisce come un tooprotect firewall la subnet bloccare tutto il traffico in ingresso, ad eccezione di porta 22 per SSH e una scheda di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="05c22-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="05c22-162">Ora è possibile distribuire una VM all'interno di questa infrastruttura di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="05c22-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="05c22-163">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="05c22-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="05c22-164">esempio Hello crea una macchina virtuale denominata `myVM` con i dischi di Azure gestita e collega hello vNic denominato `myNic` da hello passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="05c22-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="05c22-165">Utilizzando hello CLI flag toocall risorse esistente, è indicare hello toodeploy Azure VM all'interno di una rete esistente hello.</span><span class="sxs-lookup"><span data-stu-id="05c22-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="05c22-166">tooreiterate, dopo una rete virtuale e subnet sono stati distribuiti, essi possono essere lasciati come statiche o permanente di risorse all'interno di propria area di Azure.</span><span class="sxs-lookup"><span data-stu-id="05c22-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="05c22-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05c22-167">Next steps</span></span>
* [<span data-ttu-id="05c22-168">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="05c22-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="05c22-169">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="05c22-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
