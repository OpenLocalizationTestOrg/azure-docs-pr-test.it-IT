---
title: aaaAvailability imposta esercitazione per le macchine virtuali Linux in Azure | Documenti Microsoft
description: "Informazioni sui set di disponibilità hello per le macchine virtuali Linux in Azure."
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="ff6f5-103">Il set di disponibilità di toouse</span><span class="sxs-lookup"><span data-stu-id="ff6f5-103">How toouse availability sets</span></span>


<span data-ttu-id="ff6f5-104">In questa esercitazione si apprenderà come tooincrease hello disponibilità e affidabilità delle soluzioni di macchina virtuale in Azure mediante una funzionalità denominata set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="ff6f5-105">Set di disponibilità garantiscono che hello macchine virtuali di distribuire in Azure vengono distribuite tra più cluster hardware isolato.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="ff6f5-106">Questa operazione assicura che se si verifica un errore hardware o software all'interno di Azure, solo un sottoinsieme di macchine virtuali che verrà interessato e che la soluzione complessiva rimangono disponibili e operative dal punto di vista hello dei clienti di utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="ff6f5-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="ff6f5-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ff6f5-108">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ff6f5-108">Create an availability set</span></span>
> * <span data-ttu-id="ff6f5-109">Creare una macchina virtuale in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ff6f5-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="ff6f5-110">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="ff6f5-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ff6f5-111">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ff6f5-112">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ff6f5-113">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ff6f5-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="ff6f5-114">Informazioni generali sui set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ff6f5-114">Availability set overview</span></span>

<span data-ttu-id="ff6f5-115">Un Set di disponibilità è una raggruppamento logico di funzionalità che è possibile utilizzare in Azure tooensure che le risorse VM hello posizionate all'interno di essa sono isolate tra loro quando vengono distribuiti all'interno di un Data Center Azure.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="ff6f5-116">Azure garantisce che le macchine virtuali posizionate all'interno di un Set di disponibilità esegue tra più server fisici hello, calcolo rack, unità di archiviazione e commutatori di rete.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="ff6f5-117">Ciò garantisce che nell'evento hello di un errore hardware o software di Azure, solo un subset delle macchine virtuali sarà interessato e in generale l'applicazione rimanere e continuare toobe tooyour disponibili clienti.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="ff6f5-118">Utilizzo di set di disponibilità è un tooleverage funzionalità essenziali quando si desidera che le soluzioni di cloud affidabile toobuild.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="ff6f5-119">Si consideri una soluzione tipica basata su macchine virtuali, in cui si dispone di 4 server Web front-end e vengono usate 2 macchine virtuali di back-end che ospitano un database.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="ff6f5-120">Con Azure, si toodefine due set di disponibilità prima di distribuire le macchine virtuali: set di disponibilità di uno per il livello di "web" hello e un set di disponibilità per il livello di "database" hello.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="ff6f5-121">Quando si crea una nuova macchina virtuale, è possibile specificare la disponibilità di hello imposta come comando di creazione di una macchina virtuale az toohello di parametro e di Azure automaticamente verificare che le macchine virtuali create all'interno di hello disponibile hello set vengono isolati in più risorse hardware fisiche.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="ff6f5-122">Ciò significa che se si è verificato un problema hardware fisico hello in esecuzione in uno dei Server Web o macchine virtuali del Server di Database, si conosce tale hello altre istanze del Server Web e macchine virtuali del Database rimarrà in esecuzione correttamente perché sono in un hardware diverso.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="ff6f5-123">Quando si desidera toodeploy affidabile VM soluzioni basate su all'interno di Azure, è necessario utilizzare sempre i set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="ff6f5-124">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ff6f5-124">Create an availability set</span></span>

<span data-ttu-id="ff6f5-125">È possibile creare un set di disponibilità usando il comando [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="ff6f5-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="ff6f5-126">In questo esempio, è impostato sia il numero di domini di aggiornamento e di errore hello *2* per la disponibilità di hello set denominata *myAvailabilitySet* in hello *myResourceGroupAvailability*gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="ff6f5-127">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-127">Create a resource group.</span></span>

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

<span data-ttu-id="ff6f5-128">Set di disponibilità consentono tooisolate risorse tra "domini di errore di" e "domini di aggiornamento".</span><span class="sxs-lookup"><span data-stu-id="ff6f5-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="ff6f5-129">Un **dominio di errore** rappresenta una raccolta isolata di server + rete + risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="ff6f5-130">Hello sopra riportato, si indica che la disponibilità impostare toobe distribuiti in almeno due domini di errore quando vengono distribuite i macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="ff6f5-131">Viene anche indicato che si desidera distribuire il set di disponibilità su due **domini di aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="ff6f5-132">Assicurarsi di due domini di aggiornamento quando Azure esegue gli aggiornamenti software sono isolate, impedendo a tutti i software hello in esecuzione sotto la macchina virtuale da cui viene aggiornata in hello le risorse della macchina virtuale contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="ff6f5-133">Configurare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="ff6f5-133">Configure virtual network</span></span>
<span data-ttu-id="ff6f5-134">Prima di distribuire alcune macchine virtuali e possibile eseguire il servizio di bilanciamento del test, creare hello che supporta le risorse di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="ff6f5-135">Per ulteriori informazioni sulle reti virtuali, vedere hello [gestire reti virtuali di Azure](tutorial-virtual-network.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="ff6f5-136">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="ff6f5-136">Create network resources</span></span>
<span data-ttu-id="ff6f5-137">Creare una rete virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="ff6f5-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="ff6f5-138">esempio Hello crea una rete virtuale denominata *myVnet* con una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="ff6f5-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="ff6f5-139">Le schede di interfaccia di rete virtuale vengono create con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="ff6f5-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="ff6f5-140">Hello esempio crea tre schede di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="ff6f5-141">(Una scheda di rete virtuale per ogni macchina virtuale viene creato per l'app in hello seguendo i passaggi).</span><span class="sxs-lookup"><span data-stu-id="ff6f5-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="ff6f5-142">È possibile creare macchine virtuali e schede di rete virtuali aggiuntive in qualsiasi momento e aggiungerli toohello servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="ff6f5-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="ff6f5-143">Creare macchine virtuali in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ff6f5-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="ff6f5-144">Macchine virtuali devono essere create all'interno di hello toomake set di disponibilità che vengono distribuite correttamente su hardware hello.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="ff6f5-145">È possibile aggiungere un gruppo di disponibilità tooan VM impostato dopo la sua creazione.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="ff6f5-146">Quando si crea una macchina virtuale mediante [creare vm az](/cli/azure/vm#create) specificare hello set di disponibilità usando hello `--availability-set` nome del parametro toospecify hello hello del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

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

<span data-ttu-id="ff6f5-147">Sono ora disponibili due macchine virtuali all'interno del set di disponibilità appena creato.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="ff6f5-148">Poiché sono presenti in hello stesso set di disponibilità, Azure garantisce che le macchine virtuali hello e tutte le risorse (inclusi i dischi di dati) vengono distribuite tra isolato hardware fisico.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="ff6f5-149">Questa distribuzione consente di garantire una disponibilità molto maggiore della soluzione complessiva delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="ff6f5-150">Una cosa che potrebbero verificarsi quando si aggiungono macchine virtuali è che una determinata dimensione di macchina virtuale non è più disponibile toouse all'interno del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="ff6f5-151">Questo problema può verificarsi se non è più sufficiente tooadd capacità mantenendo i set di disponibilità di hello isolamento regole hello applica.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="ff6f5-152">È possibile controllare le dimensioni delle macchine Virtuali sono disponibili toouse all'interno di un gruppo di disponibilità impostati utilizzando hello toosee `--availability-set list-sizes` parametro.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="ff6f5-153">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="ff6f5-153">Check for available VM sizes</span></span> 

<span data-ttu-id="ff6f5-154">È possibile aggiungere ulteriori disponibilità toohello di macchine virtuali in un momento successivo, ma è necessario tooknow le dimensioni delle macchine Virtuali sono disponibili su hardware hello.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="ff6f5-155">Utilizzare [az set di disponibilità elenco-dimensioni delle macchine virtuali](/cli/azure/availability-set#list-sizes) toolist tutte le dimensioni disponibili hello hardware hello del cluster per il set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="ff6f5-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff6f5-156">Next steps</span></span>

<span data-ttu-id="ff6f5-157">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="ff6f5-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ff6f5-158">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ff6f5-158">Create an availability set</span></span>
> * <span data-ttu-id="ff6f5-159">Creare una macchina virtuale in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ff6f5-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="ff6f5-160">Controllare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="ff6f5-160">Check available VM sizes</span></span>

<span data-ttu-id="ff6f5-161">Spostare toohello toolearn esercitazione successiva sui set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ff6f5-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff6f5-162">Creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ff6f5-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

