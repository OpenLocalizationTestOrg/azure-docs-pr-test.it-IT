---
title: "aaaVM con più indirizzi IP mediante Azure CLI 2.0 hello | Documenti Microsoft"
description: "Informazioni su come tooassign più gli indirizzi IP tooa macchina virtuale utilizzando hello Azure CLI 2.0 | Gestore delle risorse."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a><span data-ttu-id="a249d-103">Assegnare più indirizzi IP macchine toovirtual utilizzando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a249d-103">Assign multiple IP addresses toovirtual machines using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="a249d-104">In questo articolo viene illustrato come una macchina virtuale (VM) tramite il modello di distribuzione Azure Resource Manager hello utilizzando toocreate hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="a249d-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 2.0.</span></span> <span data-ttu-id="a249d-105">Impossibile assegnare più indirizzi IP tooresources creato tramite il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="a249d-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="a249d-106">ulteriori informazioni sui modelli di distribuzione di Azure, leggere hello toolearn [comprendere i modelli di distribuzione](../resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="a249d-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="a249d-107"><a name = "create"></a>Creare una macchina virtuale con più indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="a249d-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="a249d-108">È possibile completare questa attività usando hello Azure CLI 2.0 (in questo articolo) o hello [CLI di Azure 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a249d-108">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="a249d-109">Modificare i valori hello, come appropriato, per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a249d-109">Change hello values, as appropriate, for your environment.</span></span> <span data-ttu-id="a249d-110">passaggi di Hello che seguono viene illustrato come toocreate un esempio di macchina virtuale con più IP risolve, come descritto nello scenario di hello.</span><span class="sxs-lookup"><span data-stu-id="a249d-110">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="a249d-111">Modificare i valori delle variabili e i tipi di indirizzi IP come richiesto per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="a249d-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="a249d-112">Installare hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) se non ne è già installata.</span><span class="sxs-lookup"><span data-stu-id="a249d-112">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="a249d-113">Creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux completando i passaggi hello hello [creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a249d-113">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="a249d-114">Da una shell dei comandi, accedere con il comando hello `az login` selezionare hello sottoscrizione in uso.</span><span class="sxs-lookup"><span data-stu-id="a249d-114">From a command shell, login with hello command `az login` and select hello subscription you're using.</span></span>
4. <span data-ttu-id="a249d-115">Creare VM hello eseguendo script hello che segue in un computer Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="a249d-115">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="a249d-116">script Hello crea un gruppo di risorse, una rete virtuale (VNet), una scheda di rete con tre configurazioni IP e una macchina virtuale con tooit di hello due schede di rete associate.</span><span class="sxs-lookup"><span data-stu-id="a249d-116">hello script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="a249d-117">Hello scheda di rete, indirizzo IP pubblico, rete virtuale e risorse macchina virtuale devono esistere in hello stesso percorso e sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a249d-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="a249d-118">Anche se le risorse di hello non hanno tooexist in hello stesso gruppo di risorse, in hello avviene script seguente.</span><span class="sxs-lookup"><span data-stu-id="a249d-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

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
```

<span data-ttu-id="a249d-119">Una macchina virtuale con una scheda NIC con 3 configurazioni IP toocreating, script hello crea inoltre:</span><span class="sxs-lookup"><span data-stu-id="a249d-119">In addition toocreating a VM with a NIC with 3 IP configurations, hello script creates:</span></span>

- <span data-ttu-id="a249d-120">Un unico premio gestito disco per impostazione predefinita, ma sono disponibili altre opzioni per il tipo di disco hello che è possibile creare.</span><span class="sxs-lookup"><span data-stu-id="a249d-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="a249d-121">Hello lettura [creare una VM Linux di Azure 2.0 CLI hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="a249d-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="a249d-122">Una rete virtuale con una subnet e due indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="a249d-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="a249d-123">In alternativa, è possibile usare le risorse *esistenti* di rete virtuale, subnet, scheda di interfaccia di rete o indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="a249d-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="a249d-124">toolearn come toouse esistente alle risorse di rete anziché la creazione di altre risorse, immettere `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="a249d-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="a249d-125">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="a249d-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="a249d-126">ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="a249d-126">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="a249d-127">È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a249d-127">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="a249d-128">informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.</span><span class="sxs-lookup"><span data-stu-id="a249d-128">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="a249d-129">Dopo la creazione di VM hello immettere hello `az network nic show --name MyNic1 --resource-group myResourceGroup` configurazione NIC hello tooview del comando.</span><span class="sxs-lookup"><span data-stu-id="a249d-129">After hello VM is created, enter hello `az network nic show --name MyNic1 --resource-group myResourceGroup` command tooview hello NIC configuration.</span></span> <span data-ttu-id="a249d-130">Immettere hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview un elenco di configurazioni IP hello associata toohello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="a249d-130">Enter hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview a list of hello IP configurations associated toohello NIC.</span></span>

<span data-ttu-id="a249d-131">Toohello macchina virtuale del sistema operativo di indirizzi IP privati di Aggiungi hello completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a249d-131">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="a249d-132"><a name="add"></a>Aggiungere tooa di indirizzi IP VM</span><span class="sxs-lookup"><span data-stu-id="a249d-132"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="a249d-133">È possibile aggiungere ulteriori pubbliche e private IP indirizzi tooan esistente NIC completando i passaggi di hello che seguono.</span><span class="sxs-lookup"><span data-stu-id="a249d-133">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="a249d-134">esempi di Hello si basano su hello [scenario](#Scenario) descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a249d-134">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="a249d-135">Aprire una shell dei comandi e completa hello rimanenti passaggi in questa sezione all'interno di una singola sessione.</span><span class="sxs-lookup"><span data-stu-id="a249d-135">Open a command shell and complete hello remaining steps in this section within a single session.</span></span> <span data-ttu-id="a249d-136">Se si dispone già di Azure CLI installato e configurato, hello completato i passaggi in hello [CLI di Azure 2.0 installazione](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour articolo e account di accesso account Azure con hello `az-login` comando.</span><span class="sxs-lookup"><span data-stu-id="a249d-136">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login tooyour Azure account with hello `az-login` command.</span></span>

2. <span data-ttu-id="a249d-137">Completare i passaggi di hello in uno di hello le sezioni, in base ai requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a249d-137">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="a249d-138">**Aggiungere un indirizzo IP privato**</span><span class="sxs-lookup"><span data-stu-id="a249d-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="a249d-139">tooadd un tooa di indirizzo IP privato NIC, è necessario creare una configurazione IP hello comando che segue.</span><span class="sxs-lookup"><span data-stu-id="a249d-139">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command that follows.</span></span> <span data-ttu-id="a249d-140">indirizzo IP statico Hello deve essere un indirizzo per subnet hello inutilizzato.</span><span class="sxs-lookup"><span data-stu-id="a249d-140">hello static IP address must be an unused address for hello subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="a249d-141">Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).</span><span class="sxs-lookup"><span data-stu-id="a249d-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="a249d-142">**Aggiungere un indirizzo IP pubblico**</span><span class="sxs-lookup"><span data-stu-id="a249d-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="a249d-143">Viene aggiunto un indirizzo IP pubblico associandolo tooeither una nuova configurazione IP o una configurazione IP esistente.</span><span class="sxs-lookup"><span data-stu-id="a249d-143">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="a249d-144">Completare i passaggi di hello nelle sezioni che seguono, hello necessari.</span><span class="sxs-lookup"><span data-stu-id="a249d-144">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    <span data-ttu-id="a249d-145">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="a249d-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="a249d-146">ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="a249d-146">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="a249d-147">È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a249d-147">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="a249d-148">informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.</span><span class="sxs-lookup"><span data-stu-id="a249d-148">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="a249d-149">**Associare hello risorsa tooa nuova configurazione IP**</span><span class="sxs-lookup"><span data-stu-id="a249d-149">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="a249d-150">Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="a249d-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="a249d-151">È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="a249d-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="a249d-152">toocreate uno nuovo, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a249d-152">toocreate a new one, enter hello following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="a249d-153">una nuova configurazione IP con un indirizzo IP privato statico e hello associata toocreate *myPublicIP3* indirizzo IP pubblico risorsa degli indirizzi, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a249d-153">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="a249d-154">**Configurazione IP esistente di hello associare risorse tooan** una risorsa di indirizzo IP pubblica può essere solo la configurazione IP tooan associato che non ha ancora associata.</span><span class="sxs-lookup"><span data-stu-id="a249d-154">**Associate hello resource tooan existing IP configuration** A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="a249d-155">È possibile determinare se una configurazione IP è un indirizzo IP pubblico associato immettendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a249d-155">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="a249d-156">Output restituito:</span><span class="sxs-lookup"><span data-stu-id="a249d-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="a249d-157">Poiché hello **PublicIpAddressId** colonna per *IpConfig 3* è vuoto in hello output, alcuna risorsa di indirizzo IP pubblica non è tooit attualmente associato.</span><span class="sxs-lookup"><span data-stu-id="a249d-157">Since hello **PublicIpAddressId** column for *IpConfig-3* is blank in hello output, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="a249d-158">È possibile aggiungere un esistente pubblica IP indirizzo risorsa tooIpConfig-3 o immettere hello toocreate comando uno di seguito:</span><span class="sxs-lookup"><span data-stu-id="a249d-158">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="a249d-159">Immettere hello comando risorsa toohello configurazione IP esistente denominato di indirizzo IP pubblico di tooassociate hello seguente *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="a249d-159">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="a249d-160">Gli indirizzi IP privati di visualizzazione hello e hello pubblica di indirizzi IP assegnati toohello NIC immettendo hello comando seguente ID di risorsa:</span><span class="sxs-lookup"><span data-stu-id="a249d-160">View hello private IP addresses and hello public IP address resource Ids assigned toohello NIC by entering hello following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="a249d-161">Output restituito:</span><span class="sxs-lookup"><span data-stu-id="a249d-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="a249d-162">Aggiungere indirizzi IP privati hello è stato aggiunto il sistema operativo VM di toohello NIC toohello seguendo le istruzioni hello hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a249d-162">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="a249d-163">Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a249d-163">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
