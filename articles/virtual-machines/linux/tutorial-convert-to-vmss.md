---
title: imposta una scala di macchina virtuale di Azure tooa aaaConvert | Documenti Microsoft
description: "Creare e distribuire un scalabilità della macchina virtuale Linux Azure impostato con hello CLI di Azure."
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
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="622c8-103">Convertire un set di scalabilità tooa macchina virtuale di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="622c8-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="622c8-104">Questa esercitazione viene illustrato come tooconvert toouse CLI di Azure 2.0 scalabilità della macchina virtuale una macchina virtuale tooa impostare.</span><span class="sxs-lookup"><span data-stu-id="622c8-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="622c8-105">Verrà inoltre descritto come set di configurazione di hello tooautomate delle macchine virtuali hello in scala di hello.</span><span class="sxs-lookup"><span data-stu-id="622c8-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="622c8-106">Per ulteriori informazioni su come tooinstall CLI di Azure 2.0, vedere [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="622c8-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="622c8-107">Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="622c8-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="622c8-108">Passaggio 1: eseguire il deprovisioning hello VM</span><span class="sxs-lookup"><span data-stu-id="622c8-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="622c8-109">Usare SSH tooconnect toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="622c8-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="622c8-110">Hello deprovisioning VM utilizzando hello Azure VM agente toodelete file e i dati.</span><span class="sxs-lookup"><span data-stu-id="622c8-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="622c8-111">Per una panoramica dettagliata sul deprovisioning, vedere [Come generalizzare e acquisire una macchina virtuale Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="622c8-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="622c8-112">Passaggio 2: acquisire un'immagine di hello VM</span><span class="sxs-lookup"><span data-stu-id="622c8-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="622c8-113">Per una panoramica dettagliata sull'acquisizione, vedere [Come generalizzare e acquisire una macchina virtuale Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="622c8-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="622c8-114">Deallocare hello macchina virtuale con [az vm deallocare](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="622c8-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="622c8-115">Generalizzare hello macchina virtuale con [generalizzare la macchina virtuale az](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="622c8-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="622c8-116">Creare un'immagine dalla risorsa di macchina virtuale hello con [immagine az creare](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="622c8-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="622c8-117">Passaggio 3: creare set di scalabilità hello</span><span class="sxs-lookup"><span data-stu-id="622c8-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="622c8-118">Ottenere hello **id** dell'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="622c8-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="622c8-119">Creare una macchina virtuale dalla risorsa di immagine con [az vm create](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="622c8-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="622c8-120">Questo comando associa anche un disco dati di 10 GB.</span><span class="sxs-lookup"><span data-stu-id="622c8-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="622c8-121">Tenere presente che, a seconda di hello VM dimensioni definite (utilizzassimo **Standard_DS1_v2**), hello numero di dischi dati è diverso.</span><span class="sxs-lookup"><span data-stu-id="622c8-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="622c8-122">Per ulteriori informazioni, esaminare hello [dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="622c8-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="622c8-123">Una volta al termine di set di scalabilità di hello, connettersi tooit.</span><span class="sxs-lookup"><span data-stu-id="622c8-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="622c8-124">Ottenere un elenco di indirizzi IP per le istanze di hello per SSH con [az vmss elenco--connessione-informazioni sull'istanza](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="622c8-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="622c8-125">Ora è possibile connettersi disco della macchina virtuale istanza tooinitialize hello dati toohello</span><span class="sxs-lookup"><span data-stu-id="622c8-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="622c8-126">Passaggio 4: disco dati di inizializzazione hello</span><span class="sxs-lookup"><span data-stu-id="622c8-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="622c8-127">Durante la macchina virtuale connessa toohello, partizione disco hello con `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="622c8-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="622c8-128">Scrittura di una partizione toohello con hello `mkfs` comando:</span><span class="sxs-lookup"><span data-stu-id="622c8-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="622c8-129">Montare il disco nuovo hello in modo che siano accessibile nel sistema operativo hello:</span><span class="sxs-lookup"><span data-stu-id="622c8-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="622c8-130">disco Hello è ora possibile accede tramite hello datadrive puntoMontaggio, che può essere verificato con `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="622c8-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="622c8-131">Terminare la sessione SSH hello.</span><span class="sxs-lookup"><span data-stu-id="622c8-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="622c8-132">Passaggio 5: configurare il firewall</span><span class="sxs-lookup"><span data-stu-id="622c8-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="622c8-133">Punto di entrata breccia hello firewall toohello webserver ospitato dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="622c8-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="622c8-134">Quando è stato creato il set di scalabilità di hello ed è stato creato anche un servizio di bilanciamento del carico è stato utilizzato **SSH** toohello singole macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="622c8-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="622c8-135">tooopen una porta, è necessario che due tipi di informazioni, che è possibile ottenere mediante Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="622c8-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="622c8-136">**Pool di indirizzi IP front-end**</span><span class="sxs-lookup"><span data-stu-id="622c8-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="622c8-137">**Pool di indirizzi IP back-end**</span><span class="sxs-lookup"><span data-stu-id="622c8-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="622c8-138">Con questi due nomi, è possibile aprire la porta **80**.</span><span class="sxs-lookup"><span data-stu-id="622c8-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="622c8-139">Passaggio 6: automatizzare la configurazione</span><span class="sxs-lookup"><span data-stu-id="622c8-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="622c8-140">disco dati Hello deve toobe configurato in ogni istanza di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="622c8-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="622c8-141">È possibile automatizzare la configurazione di hello della macchina virtuale hello con hello **CustomScript** estensione.</span><span class="sxs-lookup"><span data-stu-id="622c8-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="622c8-142">Creare innanzitutto un *sh* script che include comandi di formato di disco hello.</span><span class="sxs-lookup"><span data-stu-id="622c8-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="622c8-143">Successivamente, caricare tale hello toowhere file di script **CustomScript** estensione può accedervi.</span><span class="sxs-lookup"><span data-stu-id="622c8-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="622c8-144">Una copia è disponibile [qui](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="622c8-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="622c8-145">Creare un file locale denominato **Settings** e put hello in seguito il blocco JSON in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="622c8-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="622c8-146">Hello `flieUris` proprietà deve essere impostata toowhere caricato il file di script.</span><span class="sxs-lookup"><span data-stu-id="622c8-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="622c8-147">Distribuire questo comando tooyour set di scalabilità con hello **CustomScript** estensione, che fanno riferimento a hello **Settings** file appena creato.</span><span class="sxs-lookup"><span data-stu-id="622c8-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="622c8-148">Questa estensione viene eseguita automaticamente in tutte le istanze correnti e in tutte le istanze create successivamente tramite scalabilità.</span><span class="sxs-lookup"><span data-stu-id="622c8-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="622c8-149">Passaggio 7: configurare le regole di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="622c8-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="622c8-150">Attualmente non è possibile impostare le regole di scalabilità automatica nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="622c8-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="622c8-151">Hello utilizzare [portale di Azure](https://portal.azure.com) scalabilità automatica tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="622c8-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="622c8-152">Passaggio 8: attività di gestione</span><span class="sxs-lookup"><span data-stu-id="622c8-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="622c8-153">Nel ciclo di vita hello del set di scalabilità di hello, potrebbe essere necessario toorun uno o più attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="622c8-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="622c8-154">Inoltre, è opportuno toocreate script che automatizzano le varie attività di ciclo di vita e hello CLI di Azure fornisce un toodo rapidamente le attività.</span><span class="sxs-lookup"><span data-stu-id="622c8-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="622c8-155">Di seguito vengono illustrate alcune attività comuni.</span><span class="sxs-lookup"><span data-stu-id="622c8-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="622c8-156">Ottenere informazioni sulla connessione</span><span class="sxs-lookup"><span data-stu-id="622c8-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="622c8-157">Impostare il conteggio delle istanze (scalabilità manuale)</span><span class="sxs-lookup"><span data-stu-id="622c8-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="622c8-158">Eliminare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="622c8-158">Delete resource group</span></span>

<span data-ttu-id="622c8-159">Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="622c8-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="622c8-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="622c8-160">Next steps</span></span>
<span data-ttu-id="622c8-161">toolearn ulteriori informazioni su alcune delle scalabilità della macchina virtuale hello impostare funzionalità introdotte in questa esercitazione, vedere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="622c8-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="622c8-162">Informazioni sui set di scalabilità di macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="622c8-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="622c8-163">Panoramica di Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="622c8-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="622c8-164">Controllare il flusso del traffico di rete con i gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="622c8-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)