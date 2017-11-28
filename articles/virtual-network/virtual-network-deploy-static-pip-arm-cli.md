---
title: una macchina virtuale con un indirizzo IP pubblico statico - CLI di Azure 2.0 aaaCreate | Documenti Microsoft
description: Informazioni su come una macchina virtuale con un indirizzo pubblico IP statico usando toocreate hello Azure interfaccia della riga di comando (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="d7633-103">Creare una macchina virtuale con un indirizzo IP pubblico statico utilizzando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d7633-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7633-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d7633-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="d7633-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7633-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="d7633-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d7633-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="d7633-107">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d7633-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="d7633-108">Modello</span><span class="sxs-lookup"><span data-stu-id="d7633-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="d7633-109">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="d7633-109">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="d7633-110">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7633-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="d7633-111">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="d7633-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="d7633-112"><a name = "create"></a>Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="d7633-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="d7633-113">È possibile completare questa attività usando hello Azure CLI 2.0 (in questo articolo) o hello [CLI di Azure 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d7633-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="d7633-114">valori Hello "" per le variabili di hello nei passaggi hello che seguono creano risorse con le impostazioni da uno scenario di hello.</span><span class="sxs-lookup"><span data-stu-id="d7633-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="d7633-115">Modificare i valori hello, come appropriato, per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d7633-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="d7633-116">Installare hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) se non ne è già installata.</span><span class="sxs-lookup"><span data-stu-id="d7633-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="d7633-117">Creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux completando i passaggi hello hello [creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7633-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="d7633-118">Da una shell dei comandi, accedere con il comando hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="d7633-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="d7633-119">Creare VM hello eseguendo script hello che segue in un computer Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="d7633-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="d7633-120">Hello Azure indirizzo IP pubblico, rete virtuale, l'interfaccia di rete e risorse macchina virtuale devono esistere in hello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="d7633-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="d7633-121">Anche se le risorse di hello non hanno tooexist in hello stesso gruppo di risorse, in hello avviene script seguente.</span><span class="sxs-lookup"><span data-stu-id="d7633-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

<span data-ttu-id="d7633-122">Inoltre toocreating una macchina virtuale, lo script hello crea:</span><span class="sxs-lookup"><span data-stu-id="d7633-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="d7633-123">Un unico premio gestito disco per impostazione predefinita, ma sono disponibili altre opzioni per il tipo di disco hello che è possibile creare.</span><span class="sxs-lookup"><span data-stu-id="d7633-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="d7633-124">Hello lettura [creare una VM Linux di Azure 2.0 CLI hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="d7633-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="d7633-125">Risorse di rete virtuale, subnet, scheda di interfaccia di rete e indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="d7633-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="d7633-126">In alternativa, è possibile usare le risorse *esistenti* di rete virtuale, subnet, scheda di interfaccia di rete o indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="d7633-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="d7633-127">toolearn come toouse esistente alle risorse di rete anziché la creazione di altre risorse, immettere `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="d7633-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="d7633-128"><a name = "validate"></a>Convalidare la creazione della VM e l'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="d7633-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="d7633-129">Immettere il comando hello `az resource list --resouce-group IaaSStory --output table` toosee un elenco di risorse hello creato dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="d7633-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="d7633-130">Deve essere presente cinque risorse nell'output restituito hello: una macchina virtuale, rete virtuale, indirizzo IP pubblico, disco e interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="d7633-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="d7633-131">Immettere il comando hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="d7633-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="d7633-132">In hello restituito l'output, annotare il valore di hello del **IpAddress** e tale valore hello **PublicIpAllocationMethod** è *statico*.</span><span class="sxs-lookup"><span data-stu-id="d7633-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="d7633-133">Prima di eseguire hello comando seguente, rimuovere <> hello, sostituire *Username* con nome hello utilizzato per hello **Username** variabile script hello e sostituire *ipAddress* con hello **ipAddress** dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d7633-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="d7633-134">Comando che segue hello esecuzione tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="d7633-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="d7633-135"><a name= "clean-up"></a>Rimuovere hello macchina virtuale e le risorse associate</span><span class="sxs-lookup"><span data-stu-id="d7633-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="d7633-136">Si consiglia di eliminare le risorse di hello create in questo esercizio, se non vengono usati nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d7633-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="d7633-137">Le risorse di VM, indirizzo IP pubblico e disco comportano spese finché si esegue il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d7633-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="d7633-138">risorse di hello tooremove create durante questo esercizio, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d7633-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="d7633-139">risorse di hello tooview nel gruppo di risorse hello, eseguire hello `az resource list --resource-group IaaSStory` comando.</span><span class="sxs-lookup"><span data-stu-id="d7633-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="d7633-140">Verificare che non sono presenti risorse nel gruppo di risorse hello, diverso da risorse hello create dallo script hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d7633-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="d7633-141">tutte le risorse create in questo esercizio, eseguire hello toodelete `az group delete -n IaaSStory` comando.</span><span class="sxs-lookup"><span data-stu-id="d7633-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="d7633-142">comando Hello Elimina gruppo di risorse hello e tutte le risorse di hello che contiene.</span><span class="sxs-lookup"><span data-stu-id="d7633-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7633-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d7633-143">Next steps</span></span>

<span data-ttu-id="d7633-144">Traffico di rete può propagare tooand da hello che macchina virtuale creata in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d7633-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="d7633-145">È possibile definire regole in entrata e in uscita all'interno di un gruppo che consentono di limitare il traffico di hello che possano essere scambiate tooand dall'interfaccia di rete hello, hello subnet o entrambi.</span><span class="sxs-lookup"><span data-stu-id="d7633-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="d7633-146">ulteriori informazioni sulla NSGs, leggere hello toolearn [Panoramica gruppo](virtual-networks-nsg.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d7633-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
