---
title: "una macchina virtuale con più schede di rete - CLI di Azure 2.0 aaaCreate | Documenti Microsoft"
description: "Informazioni su come una macchina virtuale con più schede di rete utilizzando toocreate hello CLI di Azure 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="08767-103">Creare una macchina virtuale con più schede di rete utilizzando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="08767-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="08767-104">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="08767-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="08767-105">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="08767-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="08767-106"><a name="create"></a>Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="08767-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="08767-107">È possibile completare questa attività usando hello Azure CLI 2.0 (in questo articolo) o hello [CLI di Azure 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="08767-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="08767-108">valori Hello "" per le variabili di hello nei passaggi hello che seguono creano risorse con le impostazioni da uno scenario di hello.</span><span class="sxs-lookup"><span data-stu-id="08767-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="08767-109">Modificare i valori hello, come appropriato, per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="08767-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="08767-110">Installare hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) se non ne è già installata.</span><span class="sxs-lookup"><span data-stu-id="08767-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="08767-111">Creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux completando i passaggi hello hello [creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08767-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="08767-112">Da una shell dei comandi, accedere con il comando hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="08767-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="08767-113">Creare VM hello eseguendo script hello che segue in un computer Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="08767-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="08767-114">script di Hello crea un gruppo di risorse, una rete virtuale (VNet) con due subnet, due schede di rete e una macchina virtuale con hello due schede di rete associata tooit.</span><span class="sxs-lookup"><span data-stu-id="08767-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="08767-115">Una delle schede di rete hello subnet tooone connesso e viene assegnata un indirizzo IP pubblico e privato.</span><span class="sxs-lookup"><span data-stu-id="08767-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="08767-116">Hello altro NIC è connessa toohello altre subnet e viene assegnato un indirizzo IP privato statico e alcun indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="08767-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="08767-117">Hello scheda di rete, indirizzo IP pubblico, rete virtuale e risorse macchina virtuale devono esistere in hello stesso percorso e sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="08767-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="08767-118">Anche se le risorse di hello non hanno tooexist in hello stesso gruppo di risorse, in hello avviene script seguente.</span><span class="sxs-lookup"><span data-stu-id="08767-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

<span data-ttu-id="08767-119">Inoltre toocreating una macchina virtuale con due schede di rete, consente di creare script hello:</span><span class="sxs-lookup"><span data-stu-id="08767-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="08767-120">Un unico premio gestito disco per impostazione predefinita, ma sono disponibili altre opzioni per il tipo di disco hello che è possibile creare.</span><span class="sxs-lookup"><span data-stu-id="08767-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="08767-121">Hello lettura [creare una VM Linux di Azure 2.0 CLI hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="08767-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="08767-122">Una rete virtuale con due subnet e un singolo indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="08767-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="08767-123">In alternativa, è possibile usare le risorse *esistenti* di rete virtuale, subnet, scheda di interfaccia di rete o indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="08767-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="08767-124">toolearn come toouse esistente alle risorse di rete anziché la creazione di altre risorse, immettere `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="08767-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="08767-125"><a name = "validate"></a>Convalidare la creazione di VM e le schede di interfacce di rete</span><span class="sxs-lookup"><span data-stu-id="08767-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="08767-126">Immettere il comando hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee un elenco di risorse hello creato dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="08767-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="08767-127">Deve essere presente sei risorse nell'output restituito hello: due schede di rete, un disco, un indirizzo IP pubblico, una rete virtuale e una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="08767-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="08767-128">Immettere il comando hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="08767-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="08767-129">In hello restituito l'output, annotare il valore di hello del **IpAddress** e tale valore hello **PublicIpAllocationMethod** è *statico*.</span><span class="sxs-lookup"><span data-stu-id="08767-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="08767-130">Prima di eseguire hello comando seguente, rimuovere <> hello, sostituire *Username* con nome hello utilizzato per hello **Username** variabile script hello e sostituire *ipAddress* con hello **ipAddress** dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="08767-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="08767-131">Comando che segue hello esecuzione tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="08767-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="08767-132">Una volta connessi toohello macchina virtuale, eseguire hello `sudo ifconfig` comando toosee *eth0* e *scheda eth1* interfacce.</span><span class="sxs-lookup"><span data-stu-id="08767-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="08767-133">Ogni scheda di rete è stata assegnata hello privati indirizzi IP statici specificati nello script hello dai server DHCP di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="08767-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="08767-134">Hello indirizzi IP e MAC assegnati toohello NIC non cambiano finché hello che macchina virtuale è stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="08767-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="08767-135">È consigliabile non modificare gli indirizzi IP all'interno di un sistema operativo, come è possibile disabilitare computer toohello di connettività.</span><span class="sxs-lookup"><span data-stu-id="08767-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="08767-136">Gli indirizzi IP pubblici non sono presenti nel sistema operativo hello, come se fossero tooand convertita indirizzo di rete dall'indirizzo IP privato hello da hello dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="08767-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="08767-137"><a name= "clean-up"></a>Rimuovere hello macchina virtuale e le risorse associate</span><span class="sxs-lookup"><span data-stu-id="08767-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="08767-138">Si consiglia di eliminare le risorse di hello create in questo esercizio, se non vengono usati nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="08767-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="08767-139">Le risorse di VM, indirizzo IP pubblico e disco comportano spese finché si esegue il provisioning.</span><span class="sxs-lookup"><span data-stu-id="08767-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="08767-140">risorse di hello tooremove create durante questo esercizio, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="08767-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="08767-141">risorse di hello tooview nel gruppo di risorse hello, eseguire hello `az resource list --resource-group Multi-NIC-VM` comando.</span><span class="sxs-lookup"><span data-stu-id="08767-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="08767-142">Verificare che non sono presenti risorse nel gruppo di risorse hello, diverso da risorse hello create dallo script hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="08767-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="08767-143">tutte le risorse create in questo esercizio, eseguire hello toodelete `az group delete --name Multi-NIC-VM` comando.</span><span class="sxs-lookup"><span data-stu-id="08767-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="08767-144">comando Hello Elimina gruppo di risorse hello e tutte le risorse di hello che contiene.</span><span class="sxs-lookup"><span data-stu-id="08767-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08767-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08767-145">Next steps</span></span>

<span data-ttu-id="08767-146">Traffico di rete può propagare tooand da hello che macchina virtuale creata in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="08767-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="08767-147">È possibile definire regole in entrata e in uscita all'interno di un gruppo che consentono di limitare il traffico di hello che possano essere scambiate tooand da ogni interfaccia di rete, ogni subnet o entrambi.</span><span class="sxs-lookup"><span data-stu-id="08767-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="08767-148">ulteriori informazioni sulla NSGs, leggere hello toolearn [Panoramica gruppo](virtual-networks-nsg.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="08767-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
