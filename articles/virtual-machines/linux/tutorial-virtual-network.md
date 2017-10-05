---
title: Reti virtuali di Azure e macchine virtuali Linux | Microsoft Docs
description: 'Esercitazione: gestire reti virtuali di Azure e macchine virtuali Linux con l''interfaccia della riga di comando di Azure'
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
ms.openlocfilehash: 2366905b8160675f77cbc41ba97540af70be8c01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-the-azure-cli"></a><span data-ttu-id="dc70a-103">Gestire reti virtuali di Azure e macchine virtuali Linux con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="dc70a-103">Manage Azure Virtual Networks and Linux Virtual Machines with the Azure CLI</span></span>

<span data-ttu-id="dc70a-104">Le macchine virtuali di Azure usano la rete di Azure per la comunicazione di rete interna ed esterna.</span><span class="sxs-lookup"><span data-stu-id="dc70a-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="dc70a-105">Questa esercitazione illustra la distribuzione di due macchine virtuali e la configurazione della rete di Azure per tali VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="dc70a-106">Gli esempi in questa esercitazione presuppongono che le VM ospitino un'applicazione Web con un back-end di database, ma nell'esercitazione non viene distribuita un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dc70a-106">The examples in this tutorial assume that the VMs are hosting a web application with a database back-end, however an application is not deployed in the tutorial.</span></span> <span data-ttu-id="dc70a-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="dc70a-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc70a-108">Distribuire una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="dc70a-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="dc70a-109">Creare una subnet in una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="dc70a-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="dc70a-110">Collegare macchine virtuali a una subnet</span><span class="sxs-lookup"><span data-stu-id="dc70a-110">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="dc70a-111">Gestire gli indirizzi IP pubblici delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="dc70a-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="dc70a-112">Proteggere il traffico Internet in ingresso</span><span class="sxs-lookup"><span data-stu-id="dc70a-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="dc70a-113">Proteggere il traffico da VM a VM</span><span class="sxs-lookup"><span data-stu-id="dc70a-113">Secure VM to VM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dc70a-114">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire la versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc70a-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="dc70a-115">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="dc70a-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="dc70a-116">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dc70a-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="dc70a-117">Panoramica della rete per le VM</span><span class="sxs-lookup"><span data-stu-id="dc70a-117">VM networking overview</span></span>

<span data-ttu-id="dc70a-118">Le reti virtuali di Azure consentono connessioni di rete sicure tra macchine virtuali, Internet e altri servizi di Azure come il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc70a-118">Azure virtual networks enable secure network connections between virtual machines, the internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="dc70a-119">Le reti virtuali sono suddivise in segmenti logici denominati subnet.</span><span class="sxs-lookup"><span data-stu-id="dc70a-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="dc70a-120">Le subnet vengono usate per controllare il flusso di rete e come limite di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="dc70a-120">Subnets are used to control network flow, and as a security boundary.</span></span> <span data-ttu-id="dc70a-121">Quando si distribuisce una VM, questa include in genere un'interfaccia di rete virtuale collegata a una subnet.</span><span class="sxs-lookup"><span data-stu-id="dc70a-121">When deploying a VM, it generally includes a virtual network interface, which is attached to a subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="dc70a-122">Distribuire la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="dc70a-122">Deploy virtual network</span></span>

<span data-ttu-id="dc70a-123">Per questa esercitazione viene creata una singola rete virtuale con due subnet:</span><span class="sxs-lookup"><span data-stu-id="dc70a-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="dc70a-124">una subnet front-end per ospitare un'applicazione Web e una subnet back-end per ospitare un server di database.</span><span class="sxs-lookup"><span data-stu-id="dc70a-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="dc70a-125">Per poter creare una rete virtuale, creare prima di tutto un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="dc70a-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="dc70a-126">L'esempio seguente crea un gruppo di risorse denominato *myRGNetwork* nella località eastus.</span><span class="sxs-lookup"><span data-stu-id="dc70a-126">The following example creates a resource group named *myRGNetwork* in the eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="dc70a-127">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="dc70a-127">Create virtual network</span></span>

<span data-ttu-id="dc70a-128">Usare il comando [az network vnet create](/cli/azure/network/vnet#create) per creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="dc70a-128">Us the [az network vnet create](/cli/azure/network/vnet#create) command to create a virtual network.</span></span> <span data-ttu-id="dc70a-129">In questo esempio, alla rete vengono assegnati il nome *myVnet* e il prefisso di indirizzo *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-129">In this example, the network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="dc70a-130">Viene anche creata una subnet con nome *mySubnetFrontEnd* e prefisso *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="dc70a-131">Più avanti in questa esercitazione, a questa subnet verrà connessa una VM front-end.</span><span class="sxs-lookup"><span data-stu-id="dc70a-131">Later in this tutorial a front-end VM is connected to this subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="dc70a-132">Creare una subnet</span><span class="sxs-lookup"><span data-stu-id="dc70a-132">Create subnet</span></span>

<span data-ttu-id="dc70a-133">Alla rete virtuale viene aggiunta una nuova subnet con il comando [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="dc70a-133">A new subnet is added to the virtual network using the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="dc70a-134">In questo esempio, alla subnet vengono assegnati il nome *mySubnetBackEnd* e il prefisso di indirizzo *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-134">In this example, the subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="dc70a-135">Questa subnet verrà usata con tutti i servizi back-end.</span><span class="sxs-lookup"><span data-stu-id="dc70a-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="dc70a-136">A questo punto, è stata creata una rete che è stata segmentata in due subnet, una per i servizi front-end e un'altra per i servizi back-end.</span><span class="sxs-lookup"><span data-stu-id="dc70a-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="dc70a-137">Nella sezione successiva, le macchine virtuali verranno create e connesse a queste subnet.</span><span class="sxs-lookup"><span data-stu-id="dc70a-137">In the next section, virtual machines are created and connected to these subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="dc70a-138">Informazioni sull'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="dc70a-138">Understand public IP address</span></span>

<span data-ttu-id="dc70a-139">Un indirizzo IP pubblico consente alle risorse di Azure di essere accessibili in Internet.</span><span class="sxs-lookup"><span data-stu-id="dc70a-139">A public IP address allows Azure resources to be accessible on the internet.</span></span> <span data-ttu-id="dc70a-140">In questa sezione dell'esercitazione verrà creata una VM per illustrare l'uso degli indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="dc70a-140">In this section of the tutorial, a VM is created to demonstrate how to work with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="dc70a-141">Metodo di allocazione</span><span class="sxs-lookup"><span data-stu-id="dc70a-141">Allocation method</span></span>

<span data-ttu-id="dc70a-142">Un indirizzo IP pubblico può essere allocato in modo dinamico o statico.</span><span class="sxs-lookup"><span data-stu-id="dc70a-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="dc70a-143">Per impostazione predefinita, un indirizzo IP pubblico viene allocato in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="dc70a-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="dc70a-144">Gli indirizzi IP dinamici vengono rilasciati quando una VM viene deallocata.</span><span class="sxs-lookup"><span data-stu-id="dc70a-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="dc70a-145">Questo comportamento determina la modifica dell'indirizzo IP durante qualsiasi operazione che includa la deallocazione di una VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-145">This behavior causes the IP address to change during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="dc70a-146">Il metodo di allocazione può essere impostato come statico affinché l'indirizzo IP resti assegnato a una VM anche durante uno stato di deallocazione.</span><span class="sxs-lookup"><span data-stu-id="dc70a-146">The allocation method can be set to static, which ensures that the IP address remain assigned to a VM, even during a deallocated state.</span></span> <span data-ttu-id="dc70a-147">Quando si usa un indirizzo IP con allocazione statica, l'indirizzo IP non può essere specificato</span><span class="sxs-lookup"><span data-stu-id="dc70a-147">When using a statically allocated IP address, the IP address itself cannot be specified.</span></span> <span data-ttu-id="dc70a-148">e viene invece allocato da un pool di indirizzi disponibili.</span><span class="sxs-lookup"><span data-stu-id="dc70a-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="dc70a-149">Allocazione dinamica</span><span class="sxs-lookup"><span data-stu-id="dc70a-149">Dynamic allocation</span></span>

<span data-ttu-id="dc70a-150">Quando si crea una VM con il comando [az vm create](/cli/azure/vm#create), il metodo di allocazione predefinito dell'indirizzo IP pubblico è il metodo dinamico.</span><span class="sxs-lookup"><span data-stu-id="dc70a-150">When creating a VM with the [az vm create](/cli/azure/vm#create) command, the default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="dc70a-151">Nell'esempio seguente viene creata una VM con un indirizzo IP dinamico.</span><span class="sxs-lookup"><span data-stu-id="dc70a-151">In the following example, a VM is created with a dynamic IP address.</span></span> 

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

### <a name="static-allocation"></a><span data-ttu-id="dc70a-152">Allocazione statica</span><span class="sxs-lookup"><span data-stu-id="dc70a-152">Static allocation</span></span>

<span data-ttu-id="dc70a-153">Quando si crea una macchina virtuale con il comando [az vm create](/cli/azure/vm#create), per assegnare un indirizzo IP pubblico statico includere l'argomento `--public-ip-address-allocation static`.</span><span class="sxs-lookup"><span data-stu-id="dc70a-153">When creating a virtual machine using the [az vm create](/cli/azure/vm#create) command, include the `--public-ip-address-allocation static` argument to assign a static public IP address.</span></span> <span data-ttu-id="dc70a-154">Questa operazione non viene illustrata in questa esercitazione, ma nella sezione successiva un indirizzo IP con allocazione dinamica verrà modificato in indirizzo con allocazione statica.</span><span class="sxs-lookup"><span data-stu-id="dc70a-154">This operation is not demonstrated in this tutorial, however in the next section a dynamically allocated IP address is changed to a statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="dc70a-155">Modificare il metodo di allocazione</span><span class="sxs-lookup"><span data-stu-id="dc70a-155">Change allocation method</span></span>

<span data-ttu-id="dc70a-156">Il metodo di allocazione degli indirizzi IP può essere modificato con il comando [az network public-ip update](/cli/azure/network/public-ip#update).</span><span class="sxs-lookup"><span data-stu-id="dc70a-156">The IP address allocation method can be changed using the [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="dc70a-157">In questo esempio, il metodo di allocazione dell'indirizzo IP della VM front-end viene modificato in statico.</span><span class="sxs-lookup"><span data-stu-id="dc70a-157">In this example, the IP address allocation method of the front-end VM is changed to static.</span></span>

<span data-ttu-id="dc70a-158">Per prima cosa, deallocare la VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-158">First, deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="dc70a-159">Usare il comando [az network public-ip update](/cli/azure/network/public-ip#update) per aggiornare il metodo di allocazione.</span><span class="sxs-lookup"><span data-stu-id="dc70a-159">Use the [az network public-ip update](/cli/azure/network/public-ip#update) command to update the allocation method.</span></span> <span data-ttu-id="dc70a-160">In questo caso, si imposta `--allocation-method` su *static*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-160">In this case, the `--allocation-method` is being set to *static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="dc70a-161">Avviare la VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-161">Start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="dc70a-162">Nessun indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="dc70a-162">No public IP address</span></span>

<span data-ttu-id="dc70a-163">Spesso non è necessario che una VM sia accessibile tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="dc70a-163">Often, a VM does not need to be accessible over the internet.</span></span> <span data-ttu-id="dc70a-164">Per creare una VM senza indirizzo IP pubblico, usare l'argomento `--public-ip-address ""` con due virgolette doppie vuote.</span><span class="sxs-lookup"><span data-stu-id="dc70a-164">To create a VM without a public IP address, use the `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="dc70a-165">Questa configurazione verrà illustrata più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dc70a-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="dc70a-166">Proteggere il traffico di rete</span><span class="sxs-lookup"><span data-stu-id="dc70a-166">Secure network traffic</span></span>

<span data-ttu-id="dc70a-167">Un gruppo di sicurezza di rete (NSG) contiene un elenco di regole di sicurezza che consentono o rifiutano il traffico di rete verso le risorse connesse a reti virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc70a-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to Azure Virtual Networks (VNet).</span></span> <span data-ttu-id="dc70a-168">I gruppi di sicurezza di rete possono essere associati a subnet o singole interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-168">NSGs can be associated to subnets or individual network interfaces.</span></span> <span data-ttu-id="dc70a-169">Quando un gruppo di sicurezza di rete è associato a un'interfaccia di rete, si applica solo alla VM associata.</span><span class="sxs-lookup"><span data-stu-id="dc70a-169">When an NSG is associated with a network interface, it applies only the associated VM.</span></span> <span data-ttu-id="dc70a-170">Quando un gruppo di sicurezza di rete è associato a una subnet, le regole si applicano a tutte le risorse connesse alla subnet.</span><span class="sxs-lookup"><span data-stu-id="dc70a-170">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="dc70a-171">Regole dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="dc70a-171">Network security group rules</span></span>

<span data-ttu-id="dc70a-172">Le regole dei gruppi di sicurezza di rete definiscono le porte di rete su cui il traffico viene consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="dc70a-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="dc70a-173">Le regole possono includere intervalli di indirizzi IP di origine e di destinazione in modo da controllare il traffico tra subnet o sistemi specifici.</span><span class="sxs-lookup"><span data-stu-id="dc70a-173">The rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="dc70a-174">Le regole dei gruppi di sicurezza di rete possono includere anche una priorità, compresa tra 1 e 4096.</span><span class="sxs-lookup"><span data-stu-id="dc70a-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="dc70a-175">Le regole vengono valutate in ordine di priorità.</span><span class="sxs-lookup"><span data-stu-id="dc70a-175">Rules are evaluated in the order of priority.</span></span> <span data-ttu-id="dc70a-176">Una regola con priorità 100 viene valutata prima di una con priorità 200.</span><span class="sxs-lookup"><span data-stu-id="dc70a-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="dc70a-177">Tutti i gruppi di sicurezza di rete contengono un set di regole predefinite.</span><span class="sxs-lookup"><span data-stu-id="dc70a-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="dc70a-178">Le regole predefinite non possono essere eliminate, ma poiché hanno la priorità più bassa, è possibile eseguirne l'override con le regole create dall'utente.</span><span class="sxs-lookup"><span data-stu-id="dc70a-178">The default rules cannot be deleted, but because they are assigned the lowest priority, they can be overridden by the rules that you create.</span></span>

- <span data-ttu-id="dc70a-179">**Rete virtuale**: il traffico che ha origine e termina in una rete virtuale è consentito sia in ingresso che in uscita.</span><span class="sxs-lookup"><span data-stu-id="dc70a-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="dc70a-180">**Internet**: il traffico in uscita è consentito, mentre il traffico in ingresso viene bloccato.</span><span class="sxs-lookup"><span data-stu-id="dc70a-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="dc70a-181">**Servizio di bilanciamento del carico**: viene consentito al servizio di bilanciamento del carico di Azure di verificare tramite probe l'integrità delle VM e delle istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="dc70a-181">**Load balancer** - Allow Azure’s load balancer to probe the health of your VMs and role instances.</span></span> <span data-ttu-id="dc70a-182">Se non si usa un set con bilanciamento del carico, è possibile eseguire l'override di questa regola.</span><span class="sxs-lookup"><span data-stu-id="dc70a-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="dc70a-183">Creare gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="dc70a-183">Create network security groups</span></span>

<span data-ttu-id="dc70a-184">È possibile creare un gruppo di sicurezza di rete contemporaneamente a una VM usando il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="dc70a-184">A network security group can be created at the same time as a VM using the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="dc70a-185">In questo caso, il gruppo di sicurezza di rete viene associato all'interfaccia di rete della VM e viene creata automaticamente una regola del gruppo di sicurezza di rete per consentire il traffico sulla porta *22* da qualsiasi origine.</span><span class="sxs-lookup"><span data-stu-id="dc70a-185">When doing so, the NSG is associated with the VMs network interface and an NSG rule is auto created to allow traffic on port *22* from any source.</span></span> <span data-ttu-id="dc70a-186">In precedenza in questa esercitazione è stato creato automaticamente il gruppo di sicurezza di rete front-end con la VM front-end.</span><span class="sxs-lookup"><span data-stu-id="dc70a-186">Earlier in this tutorial, the front-end NSG was auto-created with the front-end VM.</span></span> <span data-ttu-id="dc70a-187">È stata anche creata automaticamente una regola del gruppo di sicurezza di rete per la porta 22.</span><span class="sxs-lookup"><span data-stu-id="dc70a-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="dc70a-188">In alcuni casi può essere utile creare preventivamente un gruppo di sicurezza di rete, ad esempio quando non devono essere create regole SSH predefinite o quando il gruppo di sicurezza di rete deve essere collegato a una subnet.</span><span class="sxs-lookup"><span data-stu-id="dc70a-188">In some cases, it may be helpful to pre-create an NSG, such as when default SSH rules should not be created, or when the NSG should be attached to a subnet.</span></span> 

<span data-ttu-id="dc70a-189">Per creare un gruppo di sicurezza di rete, usare il comando [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="dc70a-189">Use the [az network nsg create](/cli/azure/network/nsg#create) command to create a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="dc70a-190">Il gruppo di sicurezza di rete verrà associato a una subnet, anziché a un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-190">Instead of associating the NSG to a network interface, it is associated with a subnet.</span></span> <span data-ttu-id="dc70a-191">In questa configurazione, qualsiasi VM collegata alla subnet eredita le regole del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-191">In this configuration, any VM that is attached to the subnet inherits the NSG rules.</span></span>

<span data-ttu-id="dc70a-192">Aggiornare la subnet *mySubnetBackEnd* esistente con il nuovo gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-192">Update the existing subnet named *mySubnetBackEnd* with the new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="dc70a-193">Creare quindi una macchina virtuale collegata a *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-193">Now create a virtual machine, which is attached to the *mySubnetBackEnd*.</span></span> <span data-ttu-id="dc70a-194">Si noti che l'argomento `--nsg` ha come valore virgolette doppie vuote.</span><span class="sxs-lookup"><span data-stu-id="dc70a-194">Notice that the `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="dc70a-195">Non è necessario creare un gruppo di sicurezza di rete con la VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-195">An NSG does not need to be created with the VM.</span></span> <span data-ttu-id="dc70a-196">La VM è collegata alla subnet back-end, che è protetta con il gruppo di sicurezza di rete back-end già creato.</span><span class="sxs-lookup"><span data-stu-id="dc70a-196">The VM is attached to the back-end subnet, which is protected with the pre-created back-end NSG.</span></span> <span data-ttu-id="dc70a-197">Tale gruppo di sicurezza di rete viene applicato alla VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-197">This NSG applies to the VM.</span></span> <span data-ttu-id="dc70a-198">Si noti che anche l'argomento `--public-ip-address` ha come valore virgolette doppie vuote.</span><span class="sxs-lookup"><span data-stu-id="dc70a-198">Also, notice here that the `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="dc70a-199">Questa configurazione crea una VM senza un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="dc70a-199">This configuration creates a VM without a public IP address.</span></span> 

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

### <a name="secure-incoming-traffic"></a><span data-ttu-id="dc70a-200">Proteggere il traffico in ingresso</span><span class="sxs-lookup"><span data-stu-id="dc70a-200">Secure incoming traffic</span></span>

<span data-ttu-id="dc70a-201">Quando è stata creata la VM front-end, è stata creata una regola del gruppo di sicurezza di rete per consentire il traffico in ingresso sulla porta 22.</span><span class="sxs-lookup"><span data-stu-id="dc70a-201">When the front-end VM was created, an NSG rule was created to allow incoming traffic on port 22.</span></span> <span data-ttu-id="dc70a-202">Questa regola consente le connessioni SSH alla VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-202">This rule allows SSH connections to the VM.</span></span> <span data-ttu-id="dc70a-203">Per questo esempio deve essere consentito il traffico anche sulla porta *80*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="dc70a-204">Questa configurazione consente l'accesso a un'applicazione Web nella VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-204">This configuration allows a web application to be accessed on the VM.</span></span>

<span data-ttu-id="dc70a-205">Per creare una regola per la porta *80*, usare il comando [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="dc70a-205">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port *80*.</span></span>

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

<span data-ttu-id="dc70a-206">La VM front-end è ora accessibile solo sulla porta *22* e sulla porta *80*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-206">The front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="dc70a-207">Tutto il resto del traffico in ingresso viene bloccato in corrispondenza del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-207">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="dc70a-208">Potrebbe essere utile visualizzare le configurazioni delle regole dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-208">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="dc70a-209">Il comando [az network rule list](/cli/azure/network/nsg/rule#list) restituisce la configurazione delle regole dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-209">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="dc70a-210">Output:</span><span class="sxs-lookup"><span data-stu-id="dc70a-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-to-vm-traffic"></a><span data-ttu-id="dc70a-211">Proteggere il traffico da VM a VM</span><span class="sxs-lookup"><span data-stu-id="dc70a-211">Secure VM to VM traffic</span></span>

<span data-ttu-id="dc70a-212">Le regole dei gruppi di sicurezza di rete possono essere applicate anche tra VM.</span><span class="sxs-lookup"><span data-stu-id="dc70a-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="dc70a-213">Per questo esempio, la VM front-end deve comunicare con la VM back-end sulle porte *22* e *3306*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-213">For this example, the front-end VM needs to communicate with the back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="dc70a-214">Questa configurazione consente le connessioni SSH dalla VM front-end nonché la comunicazione di un'applicazione nella VM front-end con un database MySQL back-end.</span><span class="sxs-lookup"><span data-stu-id="dc70a-214">This configuration allows SSH connections from the front-end VM, and also allow an application on the front-end VM to communicate with a back-end MySQL database.</span></span> <span data-ttu-id="dc70a-215">Tutto il resto del traffico tra le macchine virtuali front-end e back-end dovrà essere bloccato.</span><span class="sxs-lookup"><span data-stu-id="dc70a-215">All other traffic should be blocked between the front-end and back-end virtual machines.</span></span>

<span data-ttu-id="dc70a-216">Per creare una regola per la porta 22, usare il comando [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="dc70a-216">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port 22.</span></span> <span data-ttu-id="dc70a-217">Si noti che l'argomento `--source-address-prefix` specifica il valore *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-217">Notice that the `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="dc70a-218">Questa configurazione garantisce che tramite il gruppo di sicurezza di rete sia consentito solo il traffico dalla subnet front-end.</span><span class="sxs-lookup"><span data-stu-id="dc70a-218">This configuration ensures that only traffic from the front-end subnet is allowed through the NSG.</span></span>

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

<span data-ttu-id="dc70a-219">Aggiungere ora una regola per il traffico MySQL sulla porta 3306.</span><span class="sxs-lookup"><span data-stu-id="dc70a-219">Now add a rule for MySQL traffic on port 3306.</span></span>

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

<span data-ttu-id="dc70a-220">Infine, dato che i gruppi di sicurezza di rete includono una regola predefinita che consente tutto il traffico tra le VM della stessa rete virtuale, è possibile creare una regola affinché il gruppo di sicurezza di rete back-end blocchi tutto il traffico.</span><span class="sxs-lookup"><span data-stu-id="dc70a-220">Finally, because NSGs have a default rule allowing all traffic between VMs in the same VNet, a rule can be created for the back-end NSGs to block all traffic.</span></span> <span data-ttu-id="dc70a-221">Si noti che a `--priority` viene assegnato un valore di *300*, inferiore a quello delle regole MySQL e del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-221">Notice here that the `--priority` is given a value of *300*, which is lower that both the NSG and MySQL rules.</span></span> <span data-ttu-id="dc70a-222">Questa configurazione garantisce che tramite il gruppo di sicurezza di rete sia comunque consentito il traffico SSH e MySQL.</span><span class="sxs-lookup"><span data-stu-id="dc70a-222">This configuration ensures that SSH and MySQL traffic is still allowed through the NSG.</span></span>

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

<span data-ttu-id="dc70a-223">La VM back-end è ora accessibile dalla subnet front-end solo sulla porta *22* e sulla porta *3306*.</span><span class="sxs-lookup"><span data-stu-id="dc70a-223">The back-end VM is now only accessible on port *22* and port *3306* from the front-end subnet.</span></span> <span data-ttu-id="dc70a-224">Tutto il resto del traffico in ingresso viene bloccato in corrispondenza del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-224">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="dc70a-225">Potrebbe essere utile visualizzare le configurazioni delle regole dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-225">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="dc70a-226">Il comando [az network rule list](/cli/azure/network/nsg/rule#list) restituisce la configurazione delle regole dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="dc70a-226">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="dc70a-227">Output:</span><span class="sxs-lookup"><span data-stu-id="dc70a-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="dc70a-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc70a-228">Next steps</span></span>

<span data-ttu-id="dc70a-229">In questa esercitazione sono state create e protette reti di Azure in relazione a macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="dc70a-229">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> <span data-ttu-id="dc70a-230">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="dc70a-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc70a-231">Distribuire una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="dc70a-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="dc70a-232">Creare una subnet in una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="dc70a-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="dc70a-233">Collegare macchine virtuali a una subnet</span><span class="sxs-lookup"><span data-stu-id="dc70a-233">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="dc70a-234">Gestire gli indirizzi IP pubblici delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="dc70a-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="dc70a-235">Proteggere il traffico Internet in ingresso</span><span class="sxs-lookup"><span data-stu-id="dc70a-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="dc70a-236">Proteggere il traffico da VM a VM</span><span class="sxs-lookup"><span data-stu-id="dc70a-236">Secure VM to VM traffic</span></span>

<span data-ttu-id="dc70a-237">Passare all'esercitazione successiva per apprendere come proteggere i dati nelle macchine virtuali con Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc70a-237">Advance to the next tutorial to learn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc70a-238">Eseguire il backup di macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="dc70a-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
