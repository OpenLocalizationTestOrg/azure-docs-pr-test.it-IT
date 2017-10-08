---
title: aaaCreate e gestire le macchine virtuali Linux con hello CLI di Azure | Documenti Microsoft
description: 'Esercitazione: creare e gestire le macchine virtuali Linux con hello CLI di Azure'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="6b5c4-103">Creare e gestire le macchine virtuali Linux con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="6b5c4-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="6b5c4-104">Le macchine virtuali di Azure offrono un ambiente di elaborazione completamente configurabile e flessibile.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="6b5c4-105">Questa esercitazione illustra gli elementi di base della distribuzione di una macchina virtuale di Azure, ad esempio la selezione delle dimensioni di una VM, la selezione dell'immagine di una VM e la distribuzione di una VM.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="6b5c4-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="6b5c4-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b5c4-107">Creare e connettersi tooa VM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="6b5c4-108">Selezionare e usare le immagini di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b5c4-108">Select and use VM images</span></span>
> * <span data-ttu-id="6b5c4-109">Visualizzare e usare macchine virtuali di dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="6b5c4-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="6b5c4-110">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-110">Resize a VM</span></span>
> * <span data-ttu-id="6b5c4-111">Visualizzare e comprendere lo stato di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b5c4-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6b5c4-112">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6b5c4-113">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6b5c4-114">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b5c4-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="6b5c4-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="6b5c4-115">Create resource group</span></span>

<span data-ttu-id="6b5c4-116">Creare un gruppo di risorse con hello [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="6b5c4-117">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="6b5c4-118">Il gruppo di risorse deve essere creato prima della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="6b5c4-119">In questo esempio, un gruppo di risorse denominato *myResourceGroupVM* viene creato in hello *eastus* area.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="6b5c4-120">gruppo di risorse Hello viene specificato durante la creazione o modifica di una macchina virtuale, che può essere visualizzata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="6b5c4-121">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b5c4-121">Create virtual machine</span></span>

<span data-ttu-id="6b5c4-122">Creare una macchina virtuale con hello [creare vm az](https://docs.microsoft.com/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="6b5c4-123">Per la creazione di una macchina virtuale sono disponibili diverse opzioni, ad esempio l'immagine del sistema operativo, il ridimensionamento del disco e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="6b5c4-124">In questo esempio viene creata una macchina virtuale denominata *myVM* che esegue Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="6b5c4-125">Una volta hello che macchina virtuale è stata creata, hello CLI di Azure genera informazioni hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="6b5c4-126">Prendere nota di hello `publicIpAddress`, questo indirizzo può essere una macchina virtuale di tooaccess utilizzati hello...</span><span class="sxs-lookup"><span data-stu-id="6b5c4-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a><span data-ttu-id="6b5c4-127">Connettersi tooVM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-127">Connect tooVM</span></span>

<span data-ttu-id="6b5c4-128">È ora possibile connettersi toohello VM tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="6b5c4-129">Sostituire l'indirizzo IP di esempio hello con hello `publicIpAddress` annotate nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="6b5c4-130">Una volta terminato con hello VM, chiudere una sessione SSH hello.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="6b5c4-131">Informazioni sulle immagini delle VM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-131">Understand VM images</span></span>

<span data-ttu-id="6b5c4-132">Hello Azure marketplace include molte immagini che possono essere macchine virtuali toocreate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="6b5c4-133">Nei passaggi precedenti hello, una macchina virtuale è stata creata usando un'immagine Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="6b5c4-134">In questo passaggio, hello che CLI di Azure è marketplace hello toosearch utilizzato per un'immagine CentOS, che viene quindi utilizzato toodeploy una seconda macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="6b5c4-135">un elenco di hello toosee utilizzato più di frequente immagini, utilizzare hello [elenco di immagini di macchina virtuale az](/cli/azure/vm/image#list) comando.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="6b5c4-136">output del comando Hello restituisce le immagini di macchina virtuale più diffusi hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-136">hello command output returns hello most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="6b5c4-137">Un elenco completo può essere visualizzato mediante l'aggiunta di hello `--all` argomento.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="6b5c4-138">è inoltre possibile filtrare l'elenco di immagini Hello da `--publisher` o `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="6b5c4-139">In questo esempio hello viene filtrato per tutte le immagini con un'offerta corrispondente *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="6b5c4-140">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="6b5c4-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="6b5c4-141">toodeploy una macchina virtuale usando un'immagine specifica, prendere nota del valore di hello in hello *Urn* colonna.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="6b5c4-142">Quando si specifica l'immagine di hello, numero di versione di hello immagine può essere sostituito con "più recente", che consente di selezionare più recente della distribuzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="6b5c4-143">In questo esempio hello `--image` argomento è una versione più recente di hello toospecify utilizzati di un'immagine CentOS 6.5.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="6b5c4-144">Informazioni sulle dimensioni delle VM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-144">Understand VM sizes</span></span>

<span data-ttu-id="6b5c4-145">Una dimensione di macchina virtuale determina la quantità hello delle risorse di calcolo, ad esempio memoria, CPU e GPU che vengono apportate una macchina virtuale disponibile toohello.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="6b5c4-146">Macchine virtuali devono toobe una dimensione appropriata per il carico di lavoro hello previsto.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="6b5c4-147">Se aumenta il carico di lavoro, è possibile ridimensionare una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="6b5c4-148">Dimensioni delle VM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-148">VM Sizes</span></span>

<span data-ttu-id="6b5c4-149">Hello nella tabella seguente classifica le dimensioni in casi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="6b5c4-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="6b5c4-150">Type</span></span>                     | <span data-ttu-id="6b5c4-151">Dimensioni</span><span class="sxs-lookup"><span data-stu-id="6b5c4-151">Sizes</span></span>           |    <span data-ttu-id="6b5c4-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="6b5c4-153">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="6b5c4-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="6b5c4-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="6b5c4-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="6b5c4-155">Rapporto equilibrato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="6b5c4-156">La soluzione ideale per sviluppo / test e le soluzioni di applicazioni e dati toomedium di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="6b5c4-157">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="6b5c4-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="6b5c4-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="6b5c4-158">Fs, F</span></span>             | <span data-ttu-id="6b5c4-159">Rapporto elevato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-159">High CPU-to-memory.</span></span> <span data-ttu-id="6b5c4-160">Soluzione idonea per applicazioni con livelli medi di traffico, dispositivi di rete e processi batch.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="6b5c4-161">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="6b5c4-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="6b5c4-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="6b5c4-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="6b5c4-163">Rapporto elevato tra memoria e core.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-163">High memory-to-core.</span></span> <span data-ttu-id="6b5c4-164">Ideale per i database relazionali, cache toolarge medium e analitica in memoria.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="6b5c4-165">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="6b5c4-166">Ls</span><span class="sxs-lookup"><span data-stu-id="6b5c4-166">Ls</span></span>                | <span data-ttu-id="6b5c4-167">I/O e velocità effettiva del disco elevati.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-167">High disk throughput and IO.</span></span> <span data-ttu-id="6b5c4-168">Ideale per Big Data, database SQL e NoSQL.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="6b5c4-169">GPU</span><span class="sxs-lookup"><span data-stu-id="6b5c4-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="6b5c4-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="6b5c4-170">NV, NC</span></span>            | <span data-ttu-id="6b5c4-171">VM specializzate ottimizzate per livelli intensivi di rendering della grafica e modifica di video.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="6b5c4-172">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="6b5c4-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6b5c4-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="6b5c4-173">H, A8-11</span></span>          | <span data-ttu-id="6b5c4-174">Le VM con CPU più potenti, con interfacce di rete ad alta velocità effettiva opzionali (RDMA).</span><span class="sxs-lookup"><span data-stu-id="6b5c4-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="6b5c4-175">Trovare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="6b5c4-175">Find available VM sizes</span></span>

<span data-ttu-id="6b5c4-176">toosee un elenco di macchine Virtuali di dimensioni disponibili in una determinata area, usare hello [elenco-dimensioni delle macchine virtuali az](/cli/azure/vm#list-sizes) comando.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="6b5c4-177">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="6b5c4-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="6b5c4-178">Creare una macchina virtuale con dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="6b5c4-178">Create VM with specific size</span></span>

<span data-ttu-id="6b5c4-179">Nell'esempio di creazione macchina virtuale precedente hello, una dimensione non è stato specificato, in base alla quale le dimensioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="6b5c4-180">È possibile selezionare una dimensione di macchina virtuale al momento della creazione utilizzando [creare vm az](/cli/azure/vm#create) e hello `--size` argomento.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="6b5c4-181">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-181">Resize a VM</span></span>

<span data-ttu-id="6b5c4-182">Dopo la distribuzione di una macchina virtuale, può essere ridimensionato tooincrease o ridurre l'allocazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="6b5c4-183">Prima di ridimensionamento di una macchina virtuale, controllare se hello dimensione desiderata è disponibile nel cluster di Azure corrente hello.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="6b5c4-184">Hello [az vm elenco-vm--opzioni di ridimensionamento](/cli/azure/vm#list-vm-resize-options) restituisce hello elenco delle dimensioni di comando.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="6b5c4-185">Se lo si desidera hello dimensione è disponibile, hello VM può essere ridimensionata da uno stato acceso, ma che è stato riavviato durante l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="6b5c4-186">Hello utilizzare [az vm ridimensionare]( /cli/azure/vm#resize) comando tooperform hello ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="6b5c4-187">Se hello dimensioni desiderate non è in cluster corrente hello, hello VM esigenze toobe deallocato prima operazione di ridimensionamento hello può verificarsi.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="6b5c4-188">Hello utilizzare [az vm deallocare]( /cli/azure/vm#deallocate) comando toostop e deallocare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="6b5c4-189">Si noti che quando hello VM viene acceso nuovamente, potrebbero venire rimosso tutti i dati su disco temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="6b5c4-190">indirizzo IP pubblico Hello viene modificato anche se non viene utilizzato un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="6b5c4-191">Una volta deallocato, può verificarsi hello ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="6b5c4-192">Dopo hello ridimensionare, hello VM può essere avviata.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="6b5c4-193">Stati di alimentazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b5c4-193">VM power states</span></span>

<span data-ttu-id="6b5c4-194">Una macchina virtuale di Azure può avere uno dei diversi stati di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="6b5c4-195">Questo stato rappresenta lo stato corrente di hello di hello VM dal punto di vista hello di hello hypervisor.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="6b5c4-196">Stati di alimentazione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-196">Power states</span></span>

| <span data-ttu-id="6b5c4-197">Stato di alimentazione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-197">Power State</span></span> | <span data-ttu-id="6b5c4-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-198">Description</span></span>
|----|----|
| <span data-ttu-id="6b5c4-199">Avvio in corso</span><span class="sxs-lookup"><span data-stu-id="6b5c4-199">Starting</span></span> | <span data-ttu-id="6b5c4-200">Indica la macchina virtuale hello viene avviata.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="6b5c4-201">In esecuzione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-201">Running</span></span> | <span data-ttu-id="6b5c4-202">Indica che la macchina virtuale hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="6b5c4-203">Arresto in corso</span><span class="sxs-lookup"><span data-stu-id="6b5c4-203">Stopping</span></span> | <span data-ttu-id="6b5c4-204">Indica che la macchina virtuale hello è stata arrestata.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="6b5c4-205">Arrestato</span><span class="sxs-lookup"><span data-stu-id="6b5c4-205">Stopped</span></span> | <span data-ttu-id="6b5c4-206">Indica che la macchina virtuale hello è stata arrestata.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="6b5c4-207">Macchine virtuali in stato arrestato hello continuerà a essere addebitati.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="6b5c4-208">Deallocazione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-208">Deallocating</span></span> | <span data-ttu-id="6b5c4-209">Indica che la macchina virtuale hello è in corso deallocazione.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="6b5c4-210">Deallocato</span><span class="sxs-lookup"><span data-stu-id="6b5c4-210">Deallocated</span></span> | <span data-ttu-id="6b5c4-211">Indica che la macchina virtuale hello è rimosso dall'hypervisor hello ma ancora disponibili nel piano di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="6b5c4-212">Macchine virtuali in stato deallocato hello non essere addebitati.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="6b5c4-213">Indica che lo stato di alimentazione hello della macchina virtuale hello è sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="6b5c4-214">Trovare lo stato di alimentazione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-214">Find power state</span></span>

<span data-ttu-id="6b5c4-215">stato di hello tooretrieve di una determinata macchina virtuale, utilizzare hello [az vm ottenere Vista istanza](/cli/azure/vm#get-instance-view) comando.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="6b5c4-216">Essere toospecify che un nome valido per una macchina virtuale e un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="6b5c4-217">Output:</span><span class="sxs-lookup"><span data-stu-id="6b5c4-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="6b5c4-218">Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="6b5c4-218">Management tasks</span></span>

<span data-ttu-id="6b5c4-219">Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="6b5c4-220">Inoltre, è consigliabile toocreate script tooautomate attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="6b5c4-221">Utilizza hello CLI di Azure, molte attività comuni di gestione può essere eseguita dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="6b5c4-222">Ottenere l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="6b5c4-222">Get IP address</span></span>

<span data-ttu-id="6b5c4-223">Questo comando restituisce gli indirizzi IP pubblici e privati di hello di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="6b5c4-224">Arrestare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b5c4-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="6b5c4-225">Avviare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b5c4-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="6b5c4-226">Eliminare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="6b5c4-226">Delete resource group</span></span>

<span data-ttu-id="6b5c4-227">Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="6b5c4-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b5c4-228">Next steps</span></span>

<span data-ttu-id="6b5c4-229">In questa esercitazione sono illustrate la creazione e la gestione di VM di base, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6b5c4-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b5c4-230">Creare e connettersi tooa VM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="6b5c4-231">Selezionare e usare le immagini di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b5c4-231">Select and use VM images</span></span>
> * <span data-ttu-id="6b5c4-232">Visualizzare e usare macchine virtuali di dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="6b5c4-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="6b5c4-233">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="6b5c4-233">Resize a VM</span></span>
> * <span data-ttu-id="6b5c4-234">Visualizzare e comprendere lo stato di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b5c4-234">View and understand VM state</span></span>

<span data-ttu-id="6b5c4-235">Spostare toohello toolearn esercitazione successiva su dischi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b5c4-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b5c4-236">Creare e gestire dischi di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="6b5c4-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
