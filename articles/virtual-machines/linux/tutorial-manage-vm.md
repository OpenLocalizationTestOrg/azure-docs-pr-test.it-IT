---
title: Creare e gestire VM Linux con l'interfaccia della riga di comando di Azure | Microsoft Docs
description: 'Esercitazione: creare e gestire VM Linux con l''interfaccia della riga di comando di Azure'
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
ms.openlocfilehash: c163c715eb1438a0d6b0ab53cbb43816ca8dbbb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-linux-vms-with-the-azure-cli"></a><span data-ttu-id="0a46f-103">Creare e gestire VM Linux con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0a46f-103">Create and Manage Linux VMs with the Azure CLI</span></span>

<span data-ttu-id="0a46f-104">Le macchine virtuali di Azure offrono un ambiente di elaborazione completamente configurabile e flessibile.</span><span class="sxs-lookup"><span data-stu-id="0a46f-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="0a46f-105">Questa esercitazione illustra gli elementi di base della distribuzione di una macchina virtuale di Azure, ad esempio la selezione delle dimensioni di una VM, la selezione dell'immagine di una VM e la distribuzione di una VM.</span><span class="sxs-lookup"><span data-stu-id="0a46f-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="0a46f-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="0a46f-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a46f-107">Creare e connettersi a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="0a46f-108">Selezionare e usare le immagini di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-108">Select and use VM images</span></span>
> * <span data-ttu-id="0a46f-109">Visualizzare e usare macchine virtuali di dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="0a46f-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="0a46f-110">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="0a46f-110">Resize a VM</span></span>
> * <span data-ttu-id="0a46f-111">Visualizzare e comprendere lo stato di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0a46f-112">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="0a46f-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0a46f-113">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="0a46f-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="0a46f-114">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0a46f-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="0a46f-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0a46f-115">Create resource group</span></span>

<span data-ttu-id="0a46f-116">Creare un gruppo di risorse con il comando [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0a46f-116">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="0a46f-117">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="0a46f-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="0a46f-118">Il gruppo di risorse deve essere creato prima della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="0a46f-119">In questo esempio viene creato un gruppo di risorse denominato *myResourceGroupVM* nell'area *eastus*.</span><span class="sxs-lookup"><span data-stu-id="0a46f-119">In this example, a resource group named *myResourceGroupVM* is created in the *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="0a46f-120">Il gruppo di risorse viene specificato quando si crea o si modifica una VM, come viene illustrato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0a46f-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="0a46f-121">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-121">Create virtual machine</span></span>

<span data-ttu-id="0a46f-122">Crea una macchina virtuale usando il comando [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0a46f-122">Create a virtual machine with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="0a46f-123">Per la creazione di una macchina virtuale sono disponibili diverse opzioni, ad esempio l'immagine del sistema operativo, il ridimensionamento del disco e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="0a46f-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="0a46f-124">In questo esempio viene creata una macchina virtuale denominata *myVM* che esegue Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="0a46f-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="0a46f-125">Dopo la creazione della macchina virtuale, l'interfaccia della riga di comando di Azure restituisce informazioni sulla VM.</span><span class="sxs-lookup"><span data-stu-id="0a46f-125">Once the VM has been created, the Azure CLI outputs information about the VM.</span></span> <span data-ttu-id="0a46f-126">Prendere nota dell'indirizzo `publicIpAddress`, che può essere usato per accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-126">Take note of the `publicIpAddress`, this address can be used to access the virtual machine..</span></span> 

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

## <a name="connect-to-vm"></a><span data-ttu-id="0a46f-127">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-127">Connect to VM</span></span>

<span data-ttu-id="0a46f-128">È ora possibile connettersi alla VM usando SSH.</span><span class="sxs-lookup"><span data-stu-id="0a46f-128">You can now connect to the VM using SSH.</span></span> <span data-ttu-id="0a46f-129">Sostituire l'indirizzo IP di esempio con l'indirizzo `publicIpAddress` annotato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="0a46f-129">Replace the example IP address with the `publicIpAddress` noted in the previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="0a46f-130">Al termine, chiudere la sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="0a46f-130">Once finished with the VM, close the SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="0a46f-131">Informazioni sulle immagini delle VM</span><span class="sxs-lookup"><span data-stu-id="0a46f-131">Understand VM images</span></span>

<span data-ttu-id="0a46f-132">Azure Marketplace include diverse immagini che possono essere usate per creare VM.</span><span class="sxs-lookup"><span data-stu-id="0a46f-132">The Azure marketplace includes many images that can be used to create VMs.</span></span> <span data-ttu-id="0a46f-133">Nei passaggi precedenti è stata creata una macchina virtuale usando un'immagine Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0a46f-133">In the previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="0a46f-134">In questo passaggio l'interfaccia della riga di comando di Azure viene usata per cercare nel marketplace un'immagine CentOS, che viene quindi usata per distribuire una seconda macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-134">In this step, the Azure CLI is used to search the marketplace for a CentOS image, which is then used to deploy a second virtual machine.</span></span>  

<span data-ttu-id="0a46f-135">Per visualizzare un elenco delle immagini più usate, eseguire il comando [az vm image list](/cli/azure/vm/image#list).</span><span class="sxs-lookup"><span data-stu-id="0a46f-135">To see a list of the most commonly used images, use the [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="0a46f-136">L'output del comando restituisce le immagini di macchina virtuale più popolari in Azure.</span><span class="sxs-lookup"><span data-stu-id="0a46f-136">The command output returns the most popular VM images on Azure.</span></span>

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

<span data-ttu-id="0a46f-137">Per visualizzare l'elenco completo, aggiungere l'argomento `--all`.</span><span class="sxs-lookup"><span data-stu-id="0a46f-137">A full list can be seen by adding the `--all` argument.</span></span> <span data-ttu-id="0a46f-138">L'elenco di immagini può anche essere filtrato per `--publisher` o `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="0a46f-138">The image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="0a46f-139">In questo esempio l'elenco viene filtrato per cercare tutte le immagini con un'offerta corrispondente a *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="0a46f-139">In this example, the list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="0a46f-140">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="0a46f-140">Partial output:</span></span>

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

<span data-ttu-id="0a46f-141">Per distribuire una VM usando un'immagine specifica, prendere nota del valore nella colonna *Urn*.</span><span class="sxs-lookup"><span data-stu-id="0a46f-141">To deploy a VM using a specific image, take note of the value in the *Urn* column.</span></span> <span data-ttu-id="0a46f-142">Quando si specifica l'immagine, il numero di versione dell'immagine può essere sostituito con "latest", che seleziona la versione più recente della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0a46f-142">When specifying the image, the image version number can be replaced with “latest”, which selects the latest version of the distribution.</span></span> <span data-ttu-id="0a46f-143">In questo esempio viene usato l'argomento `--image` per specificare la versione più recente di un'immagine CentOS 6.5.</span><span class="sxs-lookup"><span data-stu-id="0a46f-143">In this example, the `--image` argument is used to specify the latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="0a46f-144">Informazioni sulle dimensioni delle VM</span><span class="sxs-lookup"><span data-stu-id="0a46f-144">Understand VM sizes</span></span>

<span data-ttu-id="0a46f-145">La dimensioni di una macchina virtuale determinano la quantità di risorse di calcolo, ad esempio CPU, GPU e memoria, disponibili per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-145">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="0a46f-146">È necessario ridimensionare le macchine virtuali in modo appropriato per il carico di lavoro previsto.</span><span class="sxs-lookup"><span data-stu-id="0a46f-146">Virtual machines need to be sized appropriately for the expected work load.</span></span> <span data-ttu-id="0a46f-147">Se aumenta il carico di lavoro, è possibile ridimensionare una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="0a46f-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="0a46f-148">Dimensioni delle VM</span><span class="sxs-lookup"><span data-stu-id="0a46f-148">VM Sizes</span></span>

<span data-ttu-id="0a46f-149">La tabella seguente classifica le dimensioni a seconda dei casi d'uso.</span><span class="sxs-lookup"><span data-stu-id="0a46f-149">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="0a46f-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="0a46f-150">Type</span></span>                     | <span data-ttu-id="0a46f-151">Dimensioni</span><span class="sxs-lookup"><span data-stu-id="0a46f-151">Sizes</span></span>           |    <span data-ttu-id="0a46f-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0a46f-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="0a46f-153">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="0a46f-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="0a46f-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="0a46f-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="0a46f-155">Rapporto equilibrato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="0a46f-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="0a46f-156">Soluzione ideale per sviluppo/test e soluzioni di dati e applicazioni medio-piccole.</span><span class="sxs-lookup"><span data-stu-id="0a46f-156">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| [<span data-ttu-id="0a46f-157">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="0a46f-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="0a46f-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="0a46f-158">Fs, F</span></span>             | <span data-ttu-id="0a46f-159">Rapporto elevato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="0a46f-159">High CPU-to-memory.</span></span> <span data-ttu-id="0a46f-160">Soluzione idonea per applicazioni con livelli medi di traffico, dispositivi di rete e processi batch.</span><span class="sxs-lookup"><span data-stu-id="0a46f-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="0a46f-161">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="0a46f-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="0a46f-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="0a46f-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="0a46f-163">Rapporto elevato tra memoria e core.</span><span class="sxs-lookup"><span data-stu-id="0a46f-163">High memory-to-core.</span></span> <span data-ttu-id="0a46f-164">Soluzione ideale per database relazionali, cache medio-grandi e analisi in memoria.</span><span class="sxs-lookup"><span data-stu-id="0a46f-164">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="0a46f-165">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="0a46f-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="0a46f-166">Ls</span><span class="sxs-lookup"><span data-stu-id="0a46f-166">Ls</span></span>                | <span data-ttu-id="0a46f-167">I/O e velocità effettiva del disco elevati.</span><span class="sxs-lookup"><span data-stu-id="0a46f-167">High disk throughput and IO.</span></span> <span data-ttu-id="0a46f-168">Ideale per Big Data, database SQL e NoSQL.</span><span class="sxs-lookup"><span data-stu-id="0a46f-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="0a46f-169">GPU</span><span class="sxs-lookup"><span data-stu-id="0a46f-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="0a46f-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="0a46f-170">NV, NC</span></span>            | <span data-ttu-id="0a46f-171">VM specializzate ottimizzate per livelli intensivi di rendering della grafica e modifica di video.</span><span class="sxs-lookup"><span data-stu-id="0a46f-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="0a46f-172">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="0a46f-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="0a46f-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="0a46f-173">H, A8-11</span></span>          | <span data-ttu-id="0a46f-174">Le VM con CPU più potenti, con interfacce di rete ad alta velocità effettiva opzionali (RDMA).</span><span class="sxs-lookup"><span data-stu-id="0a46f-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="0a46f-175">Trovare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="0a46f-175">Find available VM sizes</span></span>

<span data-ttu-id="0a46f-176">Per visualizzare un elenco delle dimensioni delle VM disponibili in una determinata area, usare il comando [az vm list-sizes](/cli/azure/vm#list-sizes).</span><span class="sxs-lookup"><span data-stu-id="0a46f-176">To see a list of VM sizes available in a particular region, use the [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="0a46f-177">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="0a46f-177">Partial output:</span></span>

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

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="0a46f-178">Creare una macchina virtuale con dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="0a46f-178">Create VM with specific size</span></span>

<span data-ttu-id="0a46f-179">Nell'esempio precedente di creazione di una VM, non essendo state specificate le dimensioni, sono state usate le dimensioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="0a46f-179">In the previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="0a46f-180">Le dimensioni di una VM possono essere selezionate in fase di creazione usando [az vm create](/cli/azure/vm#create) e l'argomento `--size`.</span><span class="sxs-lookup"><span data-stu-id="0a46f-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and the `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="0a46f-181">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="0a46f-181">Resize a VM</span></span>

<span data-ttu-id="0a46f-182">Dopo la distribuzione di una VM, è possibile ridimensionarla per aumentare o ridurre l'allocazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="0a46f-182">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="0a46f-183">Prima di ridimensionare una macchina virtuale, verificare se le dimensioni desiderate sono disponibili nel cluster di Azure corrente.</span><span class="sxs-lookup"><span data-stu-id="0a46f-183">Before resizing a VM, check if the desired size is available on the current Azure cluster.</span></span> <span data-ttu-id="0a46f-184">Il comando [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) restituisce l'elenco di dimensioni.</span><span class="sxs-lookup"><span data-stu-id="0a46f-184">The [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns the list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="0a46f-185">Se le dimensioni desiderate sono disponibili, la VM può essere ridimensionata mentre è accesa, ma durante l'operazione viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="0a46f-185">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span> <span data-ttu-id="0a46f-186">Usare il comando [az vm resize]( /cli/azure/vm#resize) per eseguire il ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="0a46f-186">Use the [az vm resize]( /cli/azure/vm#resize) command to perform the resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="0a46f-187">Se nel cluster corrente non sono disponibili le dimensioni desiderate, è necessario deallocare la VM prima di poter eseguire l'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="0a46f-187">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="0a46f-188">Usare il comando [az vm deallocate]( /cli/azure/vm#deallocate) per arrestare e deallocare la VM.</span><span class="sxs-lookup"><span data-stu-id="0a46f-188">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span> <span data-ttu-id="0a46f-189">Tenere presente che, quando la VM viene riaccesa, i dati sul disco temporaneo potrebbero essere rimossi.</span><span class="sxs-lookup"><span data-stu-id="0a46f-189">Note, when the VM is powered back on, any data on the temp disk may be removed.</span></span> <span data-ttu-id="0a46f-190">Anche l'indirizzo IP pubblico viene modificato a meno che non venga usato un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="0a46f-190">The public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="0a46f-191">Dopo la deallocazione, è possibile eseguire il ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="0a46f-191">Once deallocated, the resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="0a46f-192">Dopo il ridimensionamento, la VM può essere avviata.</span><span class="sxs-lookup"><span data-stu-id="0a46f-192">After the resize, the VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="0a46f-193">Stati di alimentazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-193">VM power states</span></span>

<span data-ttu-id="0a46f-194">Una macchina virtuale di Azure può avere uno dei diversi stati di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="0a46f-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="0a46f-195">Questo stato rappresenta lo stato corrente della VM dal punto di vista dell'hypervisor.</span><span class="sxs-lookup"><span data-stu-id="0a46f-195">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="0a46f-196">Stati di alimentazione</span><span class="sxs-lookup"><span data-stu-id="0a46f-196">Power states</span></span>

| <span data-ttu-id="0a46f-197">Stato di alimentazione</span><span class="sxs-lookup"><span data-stu-id="0a46f-197">Power State</span></span> | <span data-ttu-id="0a46f-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0a46f-198">Description</span></span>
|----|----|
| <span data-ttu-id="0a46f-199">Avvio in corso</span><span class="sxs-lookup"><span data-stu-id="0a46f-199">Starting</span></span> | <span data-ttu-id="0a46f-200">Indica che è in corso l'avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-200">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="0a46f-201">In esecuzione</span><span class="sxs-lookup"><span data-stu-id="0a46f-201">Running</span></span> | <span data-ttu-id="0a46f-202">Indica che la macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0a46f-202">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="0a46f-203">Arresto in corso</span><span class="sxs-lookup"><span data-stu-id="0a46f-203">Stopping</span></span> | <span data-ttu-id="0a46f-204">Indica che è in corso l'arresto della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-204">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="0a46f-205">Arrestato</span><span class="sxs-lookup"><span data-stu-id="0a46f-205">Stopped</span></span> | <span data-ttu-id="0a46f-206">Indica che la macchina virtuale è stata arrestata.</span><span class="sxs-lookup"><span data-stu-id="0a46f-206">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="0a46f-207">Alle macchine virtuali con stato arrestato continuano a essere addebitati i costi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="0a46f-207">Virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="0a46f-208">Deallocazione</span><span class="sxs-lookup"><span data-stu-id="0a46f-208">Deallocating</span></span> | <span data-ttu-id="0a46f-209">Indica che è in corso la deallocazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-209">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="0a46f-210">Deallocato</span><span class="sxs-lookup"><span data-stu-id="0a46f-210">Deallocated</span></span> | <span data-ttu-id="0a46f-211">Indica che la macchina virtuale è stata rimossa dall'hypervisor, ma è ancora disponibile nel piano di controllo.</span><span class="sxs-lookup"><span data-stu-id="0a46f-211">Indicates that the virtual machine is removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="0a46f-212">Alle macchine virtuali con stato deallocato non vengono addebitati i costi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="0a46f-212">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="0a46f-213">Indica che lo stato di alimentazione della macchina virtuale è sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="0a46f-213">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="0a46f-214">Trovare lo stato di alimentazione</span><span class="sxs-lookup"><span data-stu-id="0a46f-214">Find power state</span></span>

<span data-ttu-id="0a46f-215">Per recuperare lo stato di una determinata VM, usare il comando [az vm get instance-view](/cli/azure/vm#get-instance-view).</span><span class="sxs-lookup"><span data-stu-id="0a46f-215">To retrieve the state of a particular VM, use the [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="0a46f-216">Assicurarsi di specificare un nome valido per una macchina virtuale e un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0a46f-216">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="0a46f-217">Output:</span><span class="sxs-lookup"><span data-stu-id="0a46f-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="0a46f-218">Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="0a46f-218">Management tasks</span></span>

<span data-ttu-id="0a46f-219">Durante il ciclo di vita di una macchina virtuale si eseguono attività di gestione come l'avvio, l'arresto o l'eliminazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-219">During the life-cycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="0a46f-220">È consigliabile creare script per automatizzare le attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="0a46f-220">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="0a46f-221">Usando l'interfaccia della riga di comando di Azure è possibile eseguire molte attività di gestione comuni dalla riga di comando o tramite script.</span><span class="sxs-lookup"><span data-stu-id="0a46f-221">Using the Azure CLI, many common management tasks can be run from the command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="0a46f-222">Ottenere l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="0a46f-222">Get IP address</span></span>

<span data-ttu-id="0a46f-223">Questo comando restituisce gli indirizzi IP pubblici e privati di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0a46f-223">This command returns the private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="0a46f-224">Arrestare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="0a46f-225">Avviare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="0a46f-226">Eliminare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0a46f-226">Delete resource group</span></span>

<span data-ttu-id="0a46f-227">Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="0a46f-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="0a46f-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a46f-228">Next steps</span></span>

<span data-ttu-id="0a46f-229">In questa esercitazione sono illustrate la creazione e la gestione di VM di base, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0a46f-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a46f-230">Creare e connettersi a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-230">Create and connect to a VM</span></span>
> * <span data-ttu-id="0a46f-231">Selezionare e usare le immagini di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-231">Select and use VM images</span></span>
> * <span data-ttu-id="0a46f-232">Visualizzare e usare macchine virtuali di dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="0a46f-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="0a46f-233">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="0a46f-233">Resize a VM</span></span>
> * <span data-ttu-id="0a46f-234">Visualizzare e comprendere lo stato di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0a46f-234">View and understand VM state</span></span>

<span data-ttu-id="0a46f-235">Passare all'esercitazione successiva per informazioni sui dischi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0a46f-235">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a46f-236">Creare e gestire dischi di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="0a46f-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
