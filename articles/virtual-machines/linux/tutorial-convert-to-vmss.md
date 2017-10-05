---
title: "Convertire una macchina virtuale di Azure in un set di scalabilità | Microsoft Docs"
description: "Creare e distribuire un set di scalabilità di macchine virtuali Linux tramite l'interfaccia della riga di comando di Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: 8d3376d2791b1349298db618d475ce5573083702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="convert-an-existing-azure-virtual-machine-to-a-scale-set"></a><span data-ttu-id="b42b5-103">Convertire una macchina virtuale di Azure esistente in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="b42b5-103">Convert an existing Azure virtual machine to a scale set</span></span>

<span data-ttu-id="b42b5-104">In questa esercitazione viene illustrato come usare l'interfaccia della riga di comando di Azure 2.0 per convertire una macchina virtuale in un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b42b5-104">This tutorial shows you how to use Azure CLI 2.0 to convert a virtual machine to a virtual machine scale set.</span></span> <span data-ttu-id="b42b5-105">È inclusa anche la procedura per automatizzare la configurazione delle macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b42b5-105">You also learn how to automate the configuration of the virtual machines in the scale set.</span></span> <span data-ttu-id="b42b5-106">Per altre informazioni su come installare l'interfaccia della riga di comando di Azure 2.0, vedere [Introduzione all'interfaccia della riga di comando di Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b42b5-106">For more information on how to install Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="b42b5-107">Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b42b5-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-the-vm"></a><span data-ttu-id="b42b5-108">Passaggio 1: eseguire il deprovisioning della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b42b5-108">Step 1 - Deprovision the VM</span></span>

<span data-ttu-id="b42b5-109">Usare SSH per connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b42b5-109">Use SSH to connect to the VM.</span></span>

<span data-ttu-id="b42b5-110">Eseguire il deprovisioning della macchina virtuale usando l'agente della macchina virtuale di Azure per eliminare file e dati.</span><span class="sxs-lookup"><span data-stu-id="b42b5-110">Deprovision the VM using the Azure VM agent to delete files and data.</span></span> <span data-ttu-id="b42b5-111">Per una panoramica dettagliata sul deprovisioning, vedere [Come generalizzare e acquisire una macchina virtuale Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="b42b5-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-the-vm"></a><span data-ttu-id="b42b5-112">Passaggio 2: acquisire un'immagine di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b42b5-112">Step 2 - Capture an image of the VM</span></span>

<span data-ttu-id="b42b5-113">Per una panoramica dettagliata sull'acquisizione, vedere [Come generalizzare e acquisire una macchina virtuale Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="b42b5-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="b42b5-114">Deallocare la macchina virtuale con [az vm deallocate](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="b42b5-114">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="b42b5-115">Generalizzare la macchina virtuale con [az vm generalize](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="b42b5-115">Generalize the VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="b42b5-116">Creare un'immagine dalla risorsa macchina virtuale con [az image create](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="b42b5-116">Create an image from the VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-the-scale-set"></a><span data-ttu-id="b42b5-117">Passaggio 3: creare il set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="b42b5-117">Step 3 - Create the scale set</span></span>

<span data-ttu-id="b42b5-118">Ottenere l'**ID** dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b42b5-118">Get the **id** of the image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="b42b5-119">Creare una macchina virtuale dalla risorsa di immagine con [az vm create](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="b42b5-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="b42b5-120">Questo comando associa anche un disco dati di 10 GB.</span><span class="sxs-lookup"><span data-stu-id="b42b5-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="b42b5-121">Tenere presente che, a seconda delle dimensioni della macchina virtuale definite (è stata usata l'opzione **Standard_DS1_v2**), il numero di dischi dati consentito è diverso.</span><span class="sxs-lookup"><span data-stu-id="b42b5-121">Keep in mind that depending on the VM size chosen (we used **Standard_DS1_v2**), the number of data disks allowed is different.</span></span> <span data-ttu-id="b42b5-122">Per altre informazioni, rivedere le [dimensioni della macchina virtuale](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="b42b5-122">For more information, review the [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="b42b5-123">Al termine, connettersi al set di scalabilità definito.</span><span class="sxs-lookup"><span data-stu-id="b42b5-123">Once the scale set finishes, connect to it.</span></span> <span data-ttu-id="b42b5-124">Ottenere un elenco di indirizzi IP per le istanze di SSH con [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="b42b5-124">Get a list of IP addresses for the instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="b42b5-125">A questo punto è possibile connettersi all'istanza della macchina virtuale per inizializzare il disco dati</span><span class="sxs-lookup"><span data-stu-id="b42b5-125">Now you can connect to the virtual machine instance to initialize the data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-the-data-disk"></a><span data-ttu-id="b42b5-126">Passaggio 4: inizializzare il disco dati</span><span class="sxs-lookup"><span data-stu-id="b42b5-126">Step 4 - Initialize the data disk</span></span>

<span data-ttu-id="b42b5-127">Quando si è connessi alla macchina virtuale, eseguire la partizione del disco con `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="b42b5-127">While connected to the virtual machine, partition the disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="b42b5-128">Scrivere un file system nella partizione con il comando `mkfs`:</span><span class="sxs-lookup"><span data-stu-id="b42b5-128">Write a file system to the partition with the `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="b42b5-129">Montare il nuovo disco in modo che sia accessibile nel sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="b42b5-129">Mount the new disk so that it is accessible in the operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="b42b5-130">È possibile ora accedere al disco tramite il punto di montaggio dell'unità dati, che può essere verificato con `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="b42b5-130">The disk can now be accesses through the datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="b42b5-131">Chiudere la sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="b42b5-131">End the SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="b42b5-132">Passaggio 5: configurare il firewall</span><span class="sxs-lookup"><span data-stu-id="b42b5-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="b42b5-133">Aprire una porta nel firewall per il server Web ospitato dal set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b42b5-133">Punch a hole through the firewall to the webserver hosted by the scale set.</span></span> <span data-ttu-id="b42b5-134">Quando è stato creato il set di scalabilità, è stato anche creato un bilanciamento del carico ed è stato usato **SSH** per le singole macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b42b5-134">When the scale set was created, a load balancer was also created, and you used it **SSH** to the individual virtual machines.</span></span> <span data-ttu-id="b42b5-135">Per aprire una porta, sono necessarie due informazioni, che possono essere ottenute tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="b42b5-135">To open a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="b42b5-136">**Pool di indirizzi IP front-end**</span><span class="sxs-lookup"><span data-stu-id="b42b5-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="b42b5-137">**Pool di indirizzi IP back-end**</span><span class="sxs-lookup"><span data-stu-id="b42b5-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="b42b5-138">Con questi due nomi, è possibile aprire la porta **80**.</span><span class="sxs-lookup"><span data-stu-id="b42b5-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="b42b5-139">Passaggio 6: automatizzare la configurazione</span><span class="sxs-lookup"><span data-stu-id="b42b5-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="b42b5-140">Il disco dati deve essere configurato in ogni istanza di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b42b5-140">The data disk needs to be configured on each virtual machine instance.</span></span> <span data-ttu-id="b42b5-141">È possibile automatizzare la configurazione della macchina virtuale con l'estensione **CustomScript**.</span><span class="sxs-lookup"><span data-stu-id="b42b5-141">We can automate the configuration of the virtual machine with the **CustomScript** extension.</span></span>

<span data-ttu-id="b42b5-142">Creare prima uno script *sh* che includa i comandi di formato disco.</span><span class="sxs-lookup"><span data-stu-id="b42b5-142">First, create a *.sh* script that includes the disk format commands.</span></span>

```sh
#!/bin/bash

# Setup the data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="b42b5-143">Caricare quindi il file script a cui può accedere l'estensione **CustomScript**.</span><span class="sxs-lookup"><span data-stu-id="b42b5-143">Next, upload that script file to where the **CustomScript** extension can access it.</span></span> <span data-ttu-id="b42b5-144">Una copia è disponibile [qui](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="b42b5-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="b42b5-145">Creare un file locale denominato **settings.json** e inserirvi il seguente blocco JSON.</span><span class="sxs-lookup"><span data-stu-id="b42b5-145">Create a local file named **settings.json** and put the following JSON block in it.</span></span> <span data-ttu-id="b42b5-146">La proprietà `flieUris` deve essere impostata sul percorso in cui è stato caricato il file script.</span><span class="sxs-lookup"><span data-stu-id="b42b5-146">The `flieUris` property should be set to where your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="b42b5-147">Distribuire questo comando al set di scalabilità con l'estensione **CustomScript**, che fa riferimento al file **settings.json** appena creato.</span><span class="sxs-lookup"><span data-stu-id="b42b5-147">Deploy this command to your scale set with the **CustomScript** extension, referencing the **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="b42b5-148">Questa estensione viene eseguita automaticamente in tutte le istanze correnti e in tutte le istanze create successivamente tramite scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b42b5-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="b42b5-149">Passaggio 7: configurare le regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="b42b5-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="b42b5-150">Attualmente non è possibile impostare le regole di scalabilità automatica nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="b42b5-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="b42b5-151">Usare il [Portale di Azure](https://portal.azure.com) per configurare la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="b42b5-151">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="b42b5-152">Passaggio 8: attività di gestione</span><span class="sxs-lookup"><span data-stu-id="b42b5-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="b42b5-153">Nel ciclo di vita del set di scalabilità, potrebbe essere necessario eseguire una o più attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="b42b5-153">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="b42b5-154">Se si vuole anche creare script che consentano di automatizzare diverse attività del ciclo di vita, l'interfaccia della riga di comando di Azure offre un modo rapido per eseguire tali operazioni.</span><span class="sxs-lookup"><span data-stu-id="b42b5-154">Additionally, you may want to create scripts that automate various lifecycle-tasks, and the Azure CLI provides a quick way to do those tasks.</span></span> <span data-ttu-id="b42b5-155">Di seguito vengono illustrate alcune attività comuni.</span><span class="sxs-lookup"><span data-stu-id="b42b5-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="b42b5-156">Ottenere informazioni sulla connessione</span><span class="sxs-lookup"><span data-stu-id="b42b5-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="b42b5-157">Impostare il conteggio delle istanze (scalabilità manuale)</span><span class="sxs-lookup"><span data-stu-id="b42b5-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="b42b5-158">Eliminare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="b42b5-158">Delete resource group</span></span>

<span data-ttu-id="b42b5-159">Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="b42b5-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b42b5-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b42b5-160">Next steps</span></span>
<span data-ttu-id="b42b5-161">Per altre informazioni su alcune funzionalità del set di scalabilità di macchine virtuali illustrate in questa esercitazione, vedere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b42b5-161">To learn more about some of the virtual machine scale set features introduced in this tutorial, see the following information:</span></span>

- [<span data-ttu-id="b42b5-162">Informazioni sui set di scalabilità di macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="b42b5-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="b42b5-163">Panoramica di Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="b42b5-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="b42b5-164">Controllare il flusso del traffico di rete con i gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="b42b5-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)