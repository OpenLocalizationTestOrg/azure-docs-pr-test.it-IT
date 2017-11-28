---
title: "Esercitazione sui set di disponibilità per macchine virtuali Linux in Azure | Microsoft Docs"
description: "Informazioni sui set di disponibilità per macchine virtuali Linux in Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="ad89a-103">Come usare i set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ad89a-103">How to use availability sets</span></span>


<span data-ttu-id="ad89a-104">In questa esercitazione si apprenderà come aumentare la disponibilità e l'affidabilità delle soluzioni delle proprie macchine virtuali in Azure tramite una funzionalità denominata set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ad89a-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="ad89a-105">I set di disponibilità assicurano che le macchine virtuali distribuite in Azure vengano distribuite tra più cluster hardware isolati.</span><span class="sxs-lookup"><span data-stu-id="ad89a-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="ad89a-106">Questa operazione assicura che, se si verifica un errore hardware o software all'interno di Azure, solo un sottoinsieme delle macchine virtuali verrà interessato e la soluzione complessiva rimarrà disponibile e operativa dal punto di vista dei clienti che la usano.</span><span class="sxs-lookup"><span data-stu-id="ad89a-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span>

<span data-ttu-id="ad89a-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="ad89a-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ad89a-108">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ad89a-108">Create an availability set</span></span>
> * <span data-ttu-id="ad89a-109">Creare una macchina virtuale in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ad89a-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="ad89a-110">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="ad89a-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ad89a-111">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="ad89a-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ad89a-112">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="ad89a-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="ad89a-113">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ad89a-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="ad89a-114">Informazioni generali sui set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ad89a-114">Availability set overview</span></span>

<span data-ttu-id="ad89a-115">Un set di disponibilità è una funzionalità di raggruppamento logico che è possibile usare in Azure per garantire che le risorse delle macchine virtuali inserite dall'utente siano isolate tra loro quando vengono distribuite all'interno di un data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad89a-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="ad89a-116">Azure garantisce che le macchine virtuali inserite all'interno di un set di disponibilità vengano eseguite tra più server fisici, rack di calcolo, unità di archiviazione e commutatori di rete.</span><span class="sxs-lookup"><span data-stu-id="ad89a-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="ad89a-117">Ciò garantisce che in caso di errore hardware o software in Azure, verrà interessato solo un sottoinsieme delle macchine virtuali e l'applicazione complessiva si manterrà aggiornata e continuerà a essere disponibile per i clienti.</span><span class="sxs-lookup"><span data-stu-id="ad89a-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="ad89a-118">L'uso dei set di disponibilità è una funzionalità essenziale da sfruttare quando si desidera creare soluzioni di cloud affidabili.</span><span class="sxs-lookup"><span data-stu-id="ad89a-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="ad89a-119">Si consideri una soluzione tipica basata su macchine virtuali, in cui si dispone di 4 server Web front-end e vengono usate 2 macchine virtuali di back-end che ospitano un database.</span><span class="sxs-lookup"><span data-stu-id="ad89a-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="ad89a-120">Con Azure è possibile definire due set di disponibilità prima di distribuire le macchine virtuali: un set di disponibilità per il livello "Web" e un set di disponibilità per il livello "database".</span><span class="sxs-lookup"><span data-stu-id="ad89a-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="ad89a-121">Quando si crea una nuova macchina virtuale, è quindi possibile specificare il set di disponibilità come parametro per il comando az vm create. Azure automaticamente garantirà che le macchine virtuali create all'interno del set di disponibilità vengano isolate su più risorse hardware fisiche.</span><span class="sxs-lookup"><span data-stu-id="ad89a-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="ad89a-122">Ciò significa che, se l'hardware fisico su cui è in esecuzione una delle macchine virtuali dei server di database o dei server Web presenta un problema, le altre istanze delle macchine virtuali dei server Web e di database rimarranno in esecuzione correttamente perché si trovano su un hardware diverso.</span><span class="sxs-lookup"><span data-stu-id="ad89a-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="ad89a-123">Usare sempre i set di disponibilità quando si vuole distribuire soluzioni affidabili basate su macchine virtuali all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad89a-123">You should always use Availability Sets when you want to deploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="ad89a-124">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ad89a-124">Create an availability set</span></span>

<span data-ttu-id="ad89a-125">È possibile creare un set di disponibilità usando il comando [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="ad89a-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="ad89a-126">In questo esempio sia il numero di domini di aggiornamento che quello di domini di errore viene impostato a *2* per il set di disponibilità denominato *myAvailabilitySet* nel gruppo di risorse *myResourceGroupAvailability*.</span><span class="sxs-lookup"><span data-stu-id="ad89a-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="ad89a-127">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ad89a-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="ad89a-128">I set di disponibilità consentono di isolare le risorse su "domini di errore" e "domini di aggiornamento".</span><span class="sxs-lookup"><span data-stu-id="ad89a-128">Availability Sets allow you to isolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="ad89a-129">Un **dominio di errore** rappresenta una raccolta isolata di server + rete + risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ad89a-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="ad89a-130">Nell'esempio precedente viene indicato che si desidera distribuire il set di disponibilità su almeno due domini di errore quando vengono distribuite le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ad89a-130">In the preceding example, we indicate that we want our availability set to be distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="ad89a-131">Viene anche indicato che si desidera distribuire il set di disponibilità su due **domini di aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="ad89a-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="ad89a-132">Due domini di aggiornamento assicurano che, quando Azure esegue gli aggiornamenti software, le risorse delle macchine virtuali siano isolate, impedendo che tutto il software in esecuzione nelle macchine virtuali venga aggiornato contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ad89a-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all the software running underneath our VM from being updated at the same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="ad89a-133">Configurare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="ad89a-133">Configure virtual network</span></span>
<span data-ttu-id="ad89a-134">Prima di distribuire alcune macchine virtuali e testare il servizio di bilanciamento, creare le risorse di rete virtuale di supporto.</span><span class="sxs-lookup"><span data-stu-id="ad89a-134">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="ad89a-135">Per altre informazioni sulle reti virtuali, vedere l'esercitazione [Gestire le reti virtuali di Azure](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="ad89a-135">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="ad89a-136">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="ad89a-136">Create network resources</span></span>
<span data-ttu-id="ad89a-137">Creare una rete virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="ad89a-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="ad89a-138">L'esempio seguente crea una rete virtuale denominata *myVnet* con una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="ad89a-138">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="ad89a-139">Le schede di interfaccia di rete virtuale vengono create con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="ad89a-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="ad89a-140">L'esempio seguente crea tre schede di interfaccia di rete virtuali,</span><span class="sxs-lookup"><span data-stu-id="ad89a-140">The following example creates three virtual NICs.</span></span> <span data-ttu-id="ad89a-141">Una scheda di interfaccia di rete virtuale per ogni VM creata per l'app nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="ad89a-141">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="ad89a-142">È possibile creare altre schede di interfaccia di rete virtuale e macchine virtuali in qualsiasi momento e aggiungerle al bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="ad89a-142">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="ad89a-143">Creare macchine virtuali in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ad89a-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="ad89a-144">Per garantire la corretta distribuzione delle macchine virtuali in tutto l'hardware, le VM devono essere create all'interno del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ad89a-144">VMs must be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="ad89a-145">Non è possibile aggiungere una macchina virtuale esistente a un set di disponibilità dopo la sua creazione.</span><span class="sxs-lookup"><span data-stu-id="ad89a-145">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="ad89a-146">Quando si crea una macchina virtuale usando il comando [az vm create](/cli/azure/vm#create) si specifica il set di disponibilità usando il parametro `--availability-set` per indicare il nome del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ad89a-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify the availability set using the `--availability-set` parameter to specify the name of the availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="ad89a-147">Sono ora disponibili due macchine virtuali all'interno del set di disponibilità appena creato.</span><span class="sxs-lookup"><span data-stu-id="ad89a-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="ad89a-148">Poiché sono nello stesso set di disponibilità, Azure assicura che le macchine virtuali e tutte le relative risorse (inclusi i dischi di dati) siano distribuite su un hardware fisico isolato.</span><span class="sxs-lookup"><span data-stu-id="ad89a-148">Because they are in the same availability set, Azure will ensure that the VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="ad89a-149">Questa distribuzione consente di garantire una disponibilità molto maggiore della soluzione complessiva delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ad89a-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="ad89a-150">Quando si aggiungono macchine virtuali, potrebbe verificarsi che una determinata dimensione di macchina virtuale non sia più disponibile per l'uso all'interno del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ad89a-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available to use within your availability set.</span></span> <span data-ttu-id="ad89a-151">Questo problema può verificarsi se non è più disponibile una capacità sufficiente per aggiungerla, mentre vengono mantenute le regole di isolamento che il set di disponibilità applica.</span><span class="sxs-lookup"><span data-stu-id="ad89a-151">This issue can happen if there is no longer enough capacity to add it while preserving the isolation rules the availability set enforces.</span></span> <span data-ttu-id="ad89a-152">È possibile verificare quali dimensioni di macchina virtuale sono disponibili per l'uso all'interno di un set di disponibilità esistente tramite il parametro `--availability-set list-sizes`.</span><span class="sxs-lookup"><span data-stu-id="ad89a-152">You can check to see what VM sizes are available to use within an existing availability set using the `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="ad89a-153">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="ad89a-153">Check for available VM sizes</span></span> 

<span data-ttu-id="ad89a-154">È possibile aggiungere più macchine virtuali al set di disponibilità in un secondo momento, ma è necessario conoscere le dimensioni delle macchine virtuali disponibili nell'hardware.</span><span class="sxs-lookup"><span data-stu-id="ad89a-154">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="ad89a-155">Usare il comando [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) per elencare tutte le dimensioni disponibili nel cluster hardware per il set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ad89a-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="ad89a-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad89a-156">Next steps</span></span>

<span data-ttu-id="ad89a-157">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="ad89a-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ad89a-158">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ad89a-158">Create an availability set</span></span>
> * <span data-ttu-id="ad89a-159">Creare una macchina virtuale in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ad89a-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="ad89a-160">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="ad89a-160">Check available VM sizes</span></span>

<span data-ttu-id="ad89a-161">Passare all'esercitazione successiva per informazioni sui set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ad89a-161">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad89a-162">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ad89a-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

