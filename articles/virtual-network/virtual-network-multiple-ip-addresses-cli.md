---
title: "Creare una VM con più indirizzi IP usando l'interfaccia della riga di comando di Azure 2.0 | Microsoft Docs"
description: "Informazioni su come assegnare più indirizzi IP a una macchina virtuale usando l'interfaccia della riga di comando di Azure 2.0 | Resource Manager."
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
ms.openlocfilehash: 0e9b2ef89ca39a7988a7b2573496a605dfc604b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-cli-20"></a><span data-ttu-id="990ff-103">Assegnare più indirizzi IP alle macchine virtuali usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="990ff-103">Assign multiple IP addresses to virtual machines using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="990ff-104">Questo articolo spiega come creare una macchina virtuale (VM) tramite il modello di distribuzione Azure Resource Manager usando l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="990ff-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 2.0.</span></span> <span data-ttu-id="990ff-105">Non è possibile a assegnare più indirizzi IP alle risorse create tramite il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="990ff-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="990ff-106">Per altre informazioni sui modelli di distribuzione di Azure, leggere l'articolo [Understand Azure deployment models](../resource-manager-deployment-model.md) (Informazioni sui modelli di distribuzione di Azure).</span><span class="sxs-lookup"><span data-stu-id="990ff-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="990ff-107"><a name = "create"></a>Creare una macchina virtuale con più indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="990ff-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="990ff-108">È possibile completare questa attività usando l'interfaccia della riga di comando di Azure 2.0 (questo articolo) o l'[interfaccia della riga di comando di Azure 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="990ff-108">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="990ff-109">Sostituire i valori in base alle esigenze specifiche dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="990ff-109">Change the values, as appropriate, for your environment.</span></span> <span data-ttu-id="990ff-110">La procedura seguente illustra come creare una macchina virtuale di esempio con più indirizzi IP, come descritto nello scenario.</span><span class="sxs-lookup"><span data-stu-id="990ff-110">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="990ff-111">Modificare i valori delle variabili e i tipi di indirizzi IP come richiesto per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="990ff-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="990ff-112">Installare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2), se non è già stata installata.</span><span class="sxs-lookup"><span data-stu-id="990ff-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="990ff-113">Creare una coppia di chiavi SSH pubblica e privata per le VM Linux completando i passaggi descritti in [Creare una coppia di chiavi SSH pubblica e privata per le VM Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="990ff-113">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="990ff-114">Da una shell dei comandi accedere con il comando `az login` e selezionare la sottoscrizione in uso.</span><span class="sxs-lookup"><span data-stu-id="990ff-114">From a command shell, login with the command `az login` and select the subscription you're using.</span></span>
4. <span data-ttu-id="990ff-115">Creare la VM eseguendo lo script seguente in un computer Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="990ff-115">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="990ff-116">Lo script crea un gruppo di risorse, una rete virtuale (VNet), una scheda di interfaccia di rete con tre configurazioni IP e una VM con due schede di interfaccia di rete collegate.</span><span class="sxs-lookup"><span data-stu-id="990ff-116">The script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="990ff-117">Le risorse di schede di interfaccia di rete, indirizzo IP pubblico, rete virtuale e VM devono essere tutte presenti nella stessa località e nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="990ff-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="990ff-118">Lo script seguente esamina un caso in cui tutte le risorse sono incluse nello stesso gruppo di risorse, anche se questo non è un requisito.</span><span class="sxs-lookup"><span data-stu-id="990ff-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using the `--allocation-method Static` option. If you
# do not specify this option, the address is allocated dynamically. The address is assigned to the resource from a pool
# of IP adresses unique to each Azure region. Download and view the file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists the ranges for each region.

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

# Create a network interface connected to the subnet and associate the public IP address to it. Azure will create the
# first IP configuration with a static private IP address and will associate the public IP address resource to it.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it to the NIC. This configuration has a
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

# Create a third IP configuration, and associate it to the NIC. This configuration has  static private IP address and   # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations
# to any NIC in a VM. To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach the NIC.

VmName="myVm"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. The script fails if the VM size
# is not supported in the location you select. Run the `azure vm sizes --location estcentralus` command to get a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace the value for the OsImage variable value with a value for *urn* from the utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file. If you're creating a Windows VM, remove the following
# line and you'll be prompted for the password you want to configure for the VM.

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

<span data-ttu-id="990ff-119">Oltre a creare una VM con una scheda di interfaccia di rete con 3 configurazioni IP, lo script crea:</span><span class="sxs-lookup"><span data-stu-id="990ff-119">In addition to creating a VM with a NIC with 3 IP configurations, the script creates:</span></span>

- <span data-ttu-id="990ff-120">Un unico disco gestito Premium per impostazione predefinita, ma sono disponibili altre opzioni per il tipo di disco che è possibile creare.</span><span class="sxs-lookup"><span data-stu-id="990ff-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="990ff-121">Leggere [Creare una VM Linux usando l'interfaccia della riga di comando di Azure 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="990ff-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="990ff-122">Una rete virtuale con una subnet e due indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="990ff-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="990ff-123">In alternativa, è possibile usare le risorse *esistenti* di rete virtuale, subnet, scheda di interfaccia di rete o indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="990ff-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="990ff-124">Per informazioni su come usare le risorse di rete esistenti anziché creare risorse aggiuntive, immettere `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="990ff-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="990ff-125">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="990ff-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="990ff-126">Per altre informazioni sui prezzi degli indirizzi IP, vedere la pagina [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="990ff-126">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="990ff-127">È previsto un limite per il numero di indirizzi IP pubblici che possono essere usati in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="990ff-127">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="990ff-128">Per altre informazioni sui limiti, vedere l'articolo [Limiti di Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="990ff-128">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="990ff-129">Dopo avere creato la VM, immettere il comando `az network nic show --name MyNic1 --resource-group myResourceGroup` per visualizzare la configurazione della scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="990ff-129">After the VM is created, enter the `az network nic show --name MyNic1 --resource-group myResourceGroup` command to view the NIC configuration.</span></span> <span data-ttu-id="990ff-130">Immettere `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` per visualizzare un elenco di configurazioni IP associate alla scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="990ff-130">Enter the `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` to view a list of the IP configurations associated to the NIC.</span></span>

<span data-ttu-id="990ff-131">Aggiungere gli indirizzi IP privati al sistema operativo della macchina virtuale seguendo la procedura per il proprio sistema operativo riportata nella sezione [Aggiungere indirizzi IP a una macchina virtuale](#os-config) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="990ff-131">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="990ff-132"><a name="add"></a>Aggiungere indirizzi IP a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="990ff-132"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="990ff-133">È possibile aggiungere indirizzi IP privati e pubblici a una scheda di interfaccia di rete esistente completando la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="990ff-133">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="990ff-134">Gli esempi si basano sullo [scenario](#Scenario) descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="990ff-134">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="990ff-135">Aprire una shell dei comandi e completare i passaggi rimanenti in questa sezione all'interno di una singola sessione.</span><span class="sxs-lookup"><span data-stu-id="990ff-135">Open a command shell and complete the remaining steps in this section within a single session.</span></span> <span data-ttu-id="990ff-136">Se l'interfaccia della riga di comando di Azure non è installata e configurata, completare la procedura riportata nell'articolo [Installazione dell'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) e accedere all'account Azure con il comando `az-login`.</span><span class="sxs-lookup"><span data-stu-id="990ff-136">If you don't already have Azure CLI installed and configured, complete the steps in the [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login to your Azure account with the `az-login` command.</span></span>

2. <span data-ttu-id="990ff-137">Completare i passaggi in una delle sezioni seguenti, a seconda delle esigenze:</span><span class="sxs-lookup"><span data-stu-id="990ff-137">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="990ff-138">**Aggiungere un indirizzo IP privato**</span><span class="sxs-lookup"><span data-stu-id="990ff-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="990ff-139">Per aggiungere un indirizzo IP privato a una scheda di interfaccia di rete, è necessario creare una configurazione IP usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="990ff-139">To add a private IP address to a NIC, you must create an IP configuration using the command that follows.</span></span> <span data-ttu-id="990ff-140">L'indirizzo IP statico deve essere un indirizzo non usato per la subnet.</span><span class="sxs-lookup"><span data-stu-id="990ff-140">The static IP address must be an unused address for the subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="990ff-141">Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).</span><span class="sxs-lookup"><span data-stu-id="990ff-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="990ff-142">**Aggiungere un indirizzo IP pubblico**</span><span class="sxs-lookup"><span data-stu-id="990ff-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="990ff-143">L'indirizzo IP pubblico viene aggiunto associandolo a una nuova configurazione IP o a una configurazione IP esistente.</span><span class="sxs-lookup"><span data-stu-id="990ff-143">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="990ff-144">Completare i passaggi in una delle sezioni che seguono, a seconda del caso.</span><span class="sxs-lookup"><span data-stu-id="990ff-144">Complete the steps in one of the sections that follow, as you require.</span></span>

    <span data-ttu-id="990ff-145">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="990ff-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="990ff-146">Per altre informazioni sui prezzi degli indirizzi IP, vedere la pagina [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="990ff-146">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="990ff-147">È previsto un limite per il numero di indirizzi IP pubblici che possono essere usati in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="990ff-147">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="990ff-148">Per altre informazioni sui limiti, vedere l'articolo [Limiti di Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="990ff-148">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="990ff-149">**Associare la risorsa a una nuova configurazione IP**</span><span class="sxs-lookup"><span data-stu-id="990ff-149">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="990ff-150">Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="990ff-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="990ff-151">È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="990ff-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="990ff-152">Per crearne una nuova, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="990ff-152">To create a new one, enter the following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="990ff-153">Per creare una nuova configurazione IP con un indirizzo IP privato statico e la risorsa indirizzo IP pubblico *myPublicIP3* associata, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="990ff-153">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="990ff-154">**Associare la risorsa a una configurazione IP esistente** una risorsa di indirizzi IP pubblica può essere associata solo a una configurazione IP che non ha ancora associata.</span><span class="sxs-lookup"><span data-stu-id="990ff-154">**Associate the resource to an existing IP configuration** A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="990ff-155">È possibile stabilire se una configurazione IP dispone di un indirizzo IP pubblico associato immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="990ff-155">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="990ff-156">Output restituito:</span><span class="sxs-lookup"><span data-stu-id="990ff-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="990ff-157">Poiché l'output della colonna **PublicIpAddressId** per *IpConfig-3* è vuoto, nessuna risorsa di indirizzo IP pubblico è attualmente associata.</span><span class="sxs-lookup"><span data-stu-id="990ff-157">Since the **PublicIpAddressId** column for *IpConfig-3* is blank in the output, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="990ff-158">È possibile aggiungere una risorsa indirizzo IP pubblico esistente a IpConfig-3 o immettere il comando seguente per crearne una:</span><span class="sxs-lookup"><span data-stu-id="990ff-158">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="990ff-159">Immettere il comando seguente per associare la risorsa indirizzo IP pubblico alla configurazione IP esistente denominata *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="990ff-159">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="990ff-160">Visualizzare gli ID di risorse indirizzo IP privato e indirizzo IP pubblico assegnati alla scheda di interfaccia di rete immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="990ff-160">View the private IP addresses and the public IP address resource Ids assigned to the NIC by entering the following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="990ff-161">Output restituito:</span><span class="sxs-lookup"><span data-stu-id="990ff-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="990ff-162">Aggiungere al sistema operativo della macchina virtuale gli indirizzi IP privati aggiunti alla scheda di interfaccia di rete seguendo le istruzioni disponibili nella sezione [Aggiungere indirizzi IP a una macchina virtuale](#os-config) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="990ff-162">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="990ff-163">Non aggiungere gli indirizzi IP pubblici al sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="990ff-163">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
