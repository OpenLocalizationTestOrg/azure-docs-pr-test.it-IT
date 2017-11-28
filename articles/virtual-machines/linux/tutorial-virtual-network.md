---
title: aaaAzure reti virtuali e macchine virtuali Linux | Documenti Microsoft
description: Esercitazione - gestire reti virtuali di Azure e macchine virtuali Linux con hello CLI di Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="fc6e2-103">Gestire reti virtuali di Azure e macchine virtuali Linux con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="fc6e2-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="fc6e2-104">Le macchine virtuali di Azure usano la rete di Azure per la comunicazione di rete interna ed esterna.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="fc6e2-105">Questa esercitazione illustra la distribuzione di due macchine virtuali e la configurazione della rete di Azure per tali VM.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="fc6e2-106">esempi di Hello in questa esercitazione si presuppone che le macchine virtuali hello ospitano un'applicazione web con un database back-end, ma non viene distribuita un'applicazione di esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="fc6e2-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="fc6e2-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc6e2-108">Distribuire una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6e2-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="fc6e2-109">Creare una subnet in una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6e2-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="fc6e2-110">Associare subnet tooa macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fc6e2-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="fc6e2-111">Gestire gli indirizzi IP pubblici delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fc6e2-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="fc6e2-112">Proteggere il traffico Internet in ingresso</span><span class="sxs-lookup"><span data-stu-id="fc6e2-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="fc6e2-113">Proteggere il traffico tooVM VM</span><span class="sxs-lookup"><span data-stu-id="fc6e2-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fc6e2-114">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fc6e2-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fc6e2-116">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fc6e2-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="fc6e2-117">Panoramica della rete per le VM</span><span class="sxs-lookup"><span data-stu-id="fc6e2-117">VM networking overview</span></span>

<span data-ttu-id="fc6e2-118">Reti virtuali di Azure, consentire le connessioni di rete sicura tra macchine virtuali, hello internet e altri servizi di Azure, ad esempio database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="fc6e2-119">Le reti virtuali sono suddivise in segmenti logici denominati subnet.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="fc6e2-120">Subnet di flusso di rete toocontrol e come limite di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="fc6e2-121">Quando si distribuisce una macchina virtuale, in genere include un'interfaccia di rete virtuale, che è collegato tooa subnet.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="fc6e2-122">Distribuire la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6e2-122">Deploy virtual network</span></span>

<span data-ttu-id="fc6e2-123">Per questa esercitazione viene creata una singola rete virtuale con due subnet:</span><span class="sxs-lookup"><span data-stu-id="fc6e2-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="fc6e2-124">una subnet front-end per ospitare un'applicazione Web e una subnet back-end per ospitare un server di database.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="fc6e2-125">Per poter creare una rete virtuale, creare prima di tutto un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fc6e2-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fc6e2-126">esempio Hello crea un gruppo di risorse denominato *myRGNetwork* nel percorso eastus hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="fc6e2-127">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6e2-127">Create virtual network</span></span>

<span data-ttu-id="fc6e2-128">Ci hello [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create) toocreate comando una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="fc6e2-129">In questo esempio è denominato rete hello *mvVnet* e viene assegnato un prefisso dell'indirizzo *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="fc6e2-130">Viene anche creata una subnet con nome *mySubnetFrontEnd* e prefisso *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="fc6e2-131">Più avanti in questa esercitazione una VM front-end è connesso toothis subnet.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="fc6e2-132">Creare una subnet</span><span class="sxs-lookup"><span data-stu-id="fc6e2-132">Create subnet</span></span>

<span data-ttu-id="fc6e2-133">Una nuova subnet viene aggiunto hello tramite la rete virtuale toohello [creare subnet della rete virtuale rete az](/cli/azure/network/vnet/subnet#create) comando.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="fc6e2-134">In questo esempio è denominato subnet hello *mySubnetBackEnd* e viene assegnato un prefisso dell'indirizzo *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="fc6e2-135">Questa subnet verrà usata con tutti i servizi back-end.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="fc6e2-136">A questo punto, è stata creata una rete che è stata segmentata in due subnet, una per i servizi front-end e un'altra per i servizi back-end.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="fc6e2-137">Nella sezione successiva hello, macchine virtuali vengono create e subnet toothese collegate.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="fc6e2-138">Informazioni sull'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="fc6e2-138">Understand public IP address</span></span>

<span data-ttu-id="fc6e2-139">Un indirizzo IP pubblico consente toobe risorse di Azure accessibili su internet di hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="fc6e2-140">In questa sezione dell'esercitazione hello toodemonstrate come gli indirizzi toowork con indirizzo IP pubblico viene creata una VM.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="fc6e2-141">Metodo di allocazione</span><span class="sxs-lookup"><span data-stu-id="fc6e2-141">Allocation method</span></span>

<span data-ttu-id="fc6e2-142">Un indirizzo IP pubblico può essere allocato in modo dinamico o statico.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="fc6e2-143">Per impostazione predefinita, un indirizzo IP pubblico viene allocato in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="fc6e2-144">Gli indirizzi IP dinamici vengono rilasciati quando una VM viene deallocata.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="fc6e2-145">Questo comportamento provoca toochange indirizzo IP di hello durante qualsiasi operazione che include la deallocazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="fc6e2-146">metodo di allocazione Hello può essere impostato toostatic, che assicura che l'indirizzo IP hello rimangono assegnati tooa macchina virtuale, anche durante uno stato deallocato.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="fc6e2-147">Quando si utilizza un indirizzo IP allocato in modo statico, non è specificato l'indirizzo IP hello stesso.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="fc6e2-148">e viene invece allocato da un pool di indirizzi disponibili.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="fc6e2-149">Allocazione dinamica</span><span class="sxs-lookup"><span data-stu-id="fc6e2-149">Dynamic allocation</span></span>

<span data-ttu-id="fc6e2-150">Quando si crea una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando hello predefinito pubblico IP indirizzo metodo di allocazione è dinamico.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="fc6e2-151">Nell'esempio seguente di hello, una macchina virtuale viene creata con un indirizzo IP dinamico.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="fc6e2-152">Allocazione statica</span><span class="sxs-lookup"><span data-stu-id="fc6e2-152">Static allocation</span></span>

<span data-ttu-id="fc6e2-153">Quando si crea una macchina virtuale utilizzando hello [creare vm az](/cli/azure/vm#create) comando, includere hello `--public-ip-address-allocation static` tooassign argomento un indirizzo IP pubblico statico.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="fc6e2-154">Questa operazione non viene dimostrata in questa esercitazione, tuttavia nella sezione successiva hello un indirizzo IP allocato in modo dinamico è tooa modificato in modo statico indirizzo allocato.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="fc6e2-155">Modificare il metodo di allocazione</span><span class="sxs-lookup"><span data-stu-id="fc6e2-155">Change allocation method</span></span>

<span data-ttu-id="fc6e2-156">metodo di allocazione degli indirizzi IP Hello può essere modificato utilizzando hello [aggiornamento public-ip di rete az](/cli/azure/network/public-ip#update) comando.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="fc6e2-157">In questo esempio hello metodo di allocazione degli indirizzi IP della VM front-end viene modificato hello toostatic.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="fc6e2-158">In primo luogo, deallocare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="fc6e2-159">Hello utilizzare [aggiornamento public-ip di rete az](/cli/azure/network/public-ip#update) metodo di allocazione hello tooupdate di comando.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="fc6e2-160">In questo caso, hello `--allocation-method` viene impostato troppo*statico*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="fc6e2-161">Avviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="fc6e2-162">Nessun indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="fc6e2-162">No public IP address</span></span>

<span data-ttu-id="fc6e2-163">Spesso, una macchina virtuale non è necessario toobe accessibile tramite internet hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="fc6e2-164">una macchina virtuale senza un indirizzo IP pubblico, utilizzare hello toocreate `--public-ip-address ""` argomento con un set vuoto di virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="fc6e2-165">Questa configurazione verrà illustrata più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="fc6e2-166">Proteggono il traffico di rete</span><span class="sxs-lookup"><span data-stu-id="fc6e2-166">Secure network traffic</span></span>

<span data-ttu-id="fc6e2-167">Un rete gruppo di sicurezza () contiene un elenco di regole di sicurezza che consentono o negano tooresources il traffico di rete connessa tooAzure reti virtuali (VNet).</span><span class="sxs-lookup"><span data-stu-id="fc6e2-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="fc6e2-168">È possibile NSGs toosubnets associato o interfacce di rete singoli.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="fc6e2-169">Quando un gruppo è associata a un'interfaccia di rete, viene applicato solo hello associata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="fc6e2-170">Quando un gruppo è subnet tooa associato, hello regole tooall risorse toohello connesso subnet.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="fc6e2-171">Regole dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="fc6e2-171">Network security group rules</span></span>

<span data-ttu-id="fc6e2-172">Le regole dei gruppi di sicurezza di rete definiscono le porte di rete su cui il traffico viene consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="fc6e2-173">le regole di Hello possono includere intervalli di indirizzi IP di origine e di destinazione in modo che viene controllato il traffico tra sistemi specifici o subnet.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="fc6e2-174">Le regole dei gruppi di sicurezza di rete possono includere anche una priorità, compresa tra 1 e 4096.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="fc6e2-175">Le regole vengono valutate in ordine di hello di priorità.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="fc6e2-176">Una regola con priorità 100 viene valutata prima di una con priorità 200.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="fc6e2-177">Tutti i gruppi di sicurezza di rete contengono un set di regole predefinite.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="fc6e2-178">le regole predefinite di Hello non possono essere eliminate, ma poiché vengono assegnati priorità più bassa hello, possono essere sostituite dalle regole di hello creati.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="fc6e2-179">**Rete virtuale**: il traffico che ha origine e termina in una rete virtuale è consentito sia in ingresso che in uscita.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="fc6e2-180">**Internet**: il traffico in uscita è consentito, mentre il traffico in ingresso viene bloccato.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="fc6e2-181">**Bilanciamento del carico** -integrità hello tooprobe di Azure consente carico bilanciamento del carico delle macchine virtuali e istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="fc6e2-182">Se non si usa un set con bilanciamento del carico, è possibile eseguire l'override di questa regola.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="fc6e2-183">Creare gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="fc6e2-183">Create network security groups</span></span>

<span data-ttu-id="fc6e2-184">Un gruppo di sicurezza di rete può essere creato in hello stesso tempo come una macchina virtuale tramite hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="fc6e2-185">In tal caso, hello NSG è associata a interfaccia di rete di macchine virtuali hello e una regola di gruppo viene creato automaticamente tooallow traffico sulla porta *22* da qualsiasi origine.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="fc6e2-186">In precedenza in questa esercitazione, hello NSG front-end è stato creato automaticamente con hello VM front-end.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="fc6e2-187">È stata anche creata automaticamente una regola del gruppo di sicurezza di rete per la porta 22.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="fc6e2-188">In alcuni casi, potrebbe essere utile toopre-creare un gruppo, ad esempio quando le regole SSH predefinite non possono essere create o quando hello gruppo deve essere collegato tooa subnet.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="fc6e2-189">Hello utilizzare [rete az creare](/cli/azure/network/nsg#create) comando toocreate un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="fc6e2-190">Invece di associazione di interfaccia di rete tooa NSG hello è associata a una subnet.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="fc6e2-191">In questa configurazione, tutte le VM che è collegato toohello subnet eredita le regole NSG hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="fc6e2-192">Aggiornare una subnet esistente di hello denominata *mySubnetBackEnd* con hello nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="fc6e2-193">Creare una macchina virtuale, che è collegato toohello *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="fc6e2-194">Si noti che hello `--nsg` argomento ha un valore di virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="fc6e2-195">Un gruppo non è necessario toobe creato con hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="fc6e2-196">Hello VM è subnet back-end toohello collegati, che è protetta con hello back-end gruppo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="fc6e2-197">Questo gruppo si applica toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="fc6e2-198">Inoltre, noterete che hello `--public-ip-address` argomento ha un valore di virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="fc6e2-199">Questa configurazione crea una VM senza un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="fc6e2-200">Proteggere il traffico in ingresso</span><span class="sxs-lookup"><span data-stu-id="fc6e2-200">Secure incoming traffic</span></span>

<span data-ttu-id="fc6e2-201">Quando hello VM front-end è stato creato, è stata creata una regola di NSG tooallow il traffico in entrata sulla porta 22.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="fc6e2-202">Questa regola consente toohello connessioni SSH macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="fc6e2-203">Per questo esempio deve essere consentito il traffico anche sulla porta *80*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="fc6e2-204">Questa configurazione consente una toobe di applicazione web accede hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="fc6e2-205">Hello utilizzare [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) toocreate comando una regola per la porta *80*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="fc6e2-206">Hello VM front-end è ora accessibile solo sulla porta *22* e la porta *80*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="fc6e2-207">Tutto il traffico in ingresso viene bloccato nel gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="fc6e2-208">Potrebbe essere utile toovisualize configurazioni delle regole di hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="fc6e2-209">Configurazione delle regole di NSG hello restituito con hello [elenco regole di rete az](/cli/azure/network/nsg/rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="fc6e2-210">Output:</span><span class="sxs-lookup"><span data-stu-id="fc6e2-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="fc6e2-211">Proteggere il traffico tooVM VM</span><span class="sxs-lookup"><span data-stu-id="fc6e2-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="fc6e2-212">Le regole dei gruppi di sicurezza di rete possono essere applicate anche tra VM.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="fc6e2-213">In questo esempio hello VM front-end deve toocommunicate con hello VM back-end sulla porta *22* e *3306*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="fc6e2-214">Questa configurazione consente le connessioni SSH da hello VM front-end e inoltre consentire un'applicazione hello toocommunicate VM front-end con un database MySQL di back-end.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="fc6e2-215">Bloccare tutto il traffico tra le macchine virtuali front-end e back-end hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="fc6e2-216">Hello utilizzare [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) toocreate comando una regola per la porta 22.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="fc6e2-217">Si noti che hello `--source-address-prefix` argomento specifica un valore di *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="fc6e2-218">Questa configurazione assicura che solo il traffico dalla subnet front-end hello è consentito attraverso hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="fc6e2-219">Aggiungere ora una regola per il traffico MySQL sulla porta 3306.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="fc6e2-220">Infine, perché NSGs dispone di una regola predefinita che consente tutto il traffico tra macchine virtuali in hello stessa rete virtuale, creare una regola può essere per hello back-end NSGs tooblock tutto il traffico.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="fc6e2-221">Noterete che hello `--priority` viene assegnato un valore di *300*, che è inferiore che entrambi hello MySQL e gruppo di regole.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="fc6e2-222">Questa configurazione assicura che il traffico SSH e MySQL è ancora consentito attraverso hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="fc6e2-223">Hello VM back-end è ora accessibile solo sulla porta *22* e la porta *3306* dalla subnet front-end hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="fc6e2-224">Tutto il traffico in ingresso viene bloccato nel gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="fc6e2-225">Potrebbe essere utile toovisualize configurazioni delle regole di hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="fc6e2-226">Configurazione delle regole di NSG hello restituito con hello [elenco regole di rete az](/cli/azure/network/nsg/rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="fc6e2-227">Output:</span><span class="sxs-lookup"><span data-stu-id="fc6e2-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="fc6e2-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc6e2-228">Next steps</span></span>

<span data-ttu-id="fc6e2-229">In questa esercitazione è creato e protetto reti di Azure come macchine toovirtual correlati.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="fc6e2-230">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="fc6e2-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc6e2-231">Distribuire una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6e2-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="fc6e2-232">Creare una subnet in una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6e2-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="fc6e2-233">Associare subnet tooa macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fc6e2-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="fc6e2-234">Gestire gli indirizzi IP pubblici delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fc6e2-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="fc6e2-235">Proteggere il traffico Internet in ingresso</span><span class="sxs-lookup"><span data-stu-id="fc6e2-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="fc6e2-236">Proteggere il traffico tooVM VM</span><span class="sxs-lookup"><span data-stu-id="fc6e2-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="fc6e2-237">Spostare toohello toolearn esercitazione successiva sulla protezione dei dati su macchine virtuali tramite backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc6e2-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc6e2-238">Eseguire il backup di macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="fc6e2-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
