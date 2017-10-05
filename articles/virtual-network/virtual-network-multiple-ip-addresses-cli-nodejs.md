---
title: "Creare una VM con più indirizzi IP usando l'interfaccia della riga di comando 1.0 di Azure | Microsoft Docs"
description: "Informazioni su come assegnare più indirizzi IP a una macchina virtuale usando l'interfaccia della riga di comando 1.0 di Azure | Resource Manager."
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
ms.openlocfilehash: 9f085dfa1fe4db36d58cb976bb550a46bf241ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-azure-cli-10"></a><span data-ttu-id="b8710-103">Assegnare più indirizzi IP alle macchine virtuali usando l'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="b8710-103">Assign multiple IP addresses to virtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="b8710-104">Questo articolo spiega come creare una macchina virtuale (VM) tramite il modello di distribuzione Azure Resource Manager usando l'interfaccia della riga di comando 1.0 di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8710-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 1.0.</span></span> <span data-ttu-id="b8710-105">Non è possibile a assegnare più indirizzi IP alle risorse create tramite il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="b8710-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="b8710-106">Per altre informazioni sui modelli di distribuzione di Azure, leggere l'articolo [Understand Azure deployment models](../resource-manager-deployment-model.md) (Informazioni sui modelli di distribuzione di Azure).</span><span class="sxs-lookup"><span data-stu-id="b8710-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="b8710-107"><a name = "create"></a>Creare una macchina virtuale con più indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="b8710-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="b8710-108">È possibile completare questa attività usando l'interfaccia della riga di comando di Azure 1.0 (questo articolo) o l'[interfaccia della riga di comando di Azure 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b8710-108">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="b8710-109">La procedura seguente illustra come creare una macchina virtuale di esempio con più indirizzi IP, come descritto nello scenario.</span><span class="sxs-lookup"><span data-stu-id="b8710-109">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="b8710-110">Modificare i nomi delle variabili e i tipi di indirizzi IP come richiesto per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="b8710-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="b8710-111">Per installare e configurare l'interfaccia della riga di comando di Azure 1.0, seguire la procedura riportata nell'articolo [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e accedere all'account Azure con il comando `azure-login`.</span><span class="sxs-lookup"><span data-stu-id="b8710-111">Install and configure the Azure CLI 1.0 by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with the `azure-login` command.</span></span>

2. <span data-ttu-id="b8710-112">Creare un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="b8710-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="b8710-113">Creare una rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="b8710-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="b8710-114">Creare una subnet nella rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="b8710-114">Create a subnet in the virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="b8710-115">Creare un account di archiviazione per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b8710-115">Create  a storage account for the VM.</span></span> <span data-ttu-id="b8710-116">Prima di eseguire il comando seguente, sostituire *mystorageaccount* con un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="b8710-116">Before running the following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="b8710-117">Il nome deve essere univoco in Azure:</span><span class="sxs-lookup"><span data-stu-id="b8710-117">The name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="b8710-118">Creare le configurazioni IP, una scheda di interfaccia di rete e assegnare le configurazioni IP alla scheda creata.</span><span class="sxs-lookup"><span data-stu-id="b8710-118">Create the IP configurations, a NIC, and assign the IP configurations to the NIC.</span></span> <span data-ttu-id="b8710-119">È possibile aggiungere, rimuovere o modificare le configurazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="b8710-119">You can add, remove, or change the configurations as necessary.</span></span> <span data-ttu-id="b8710-120">Nello scenario vengono descritte le configurazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b8710-120">The following configurations are described in the scenario:</span></span>

    <span data-ttu-id="b8710-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="b8710-121">**IPConfig-1**</span></span>

    <span data-ttu-id="b8710-122">Immettere i comandi seguenti per creare:</span><span class="sxs-lookup"><span data-stu-id="b8710-122">Enter the commands that follow to create:</span></span>

    - <span data-ttu-id="b8710-123">Una risorsa indirizzo IP pubblico con un indirizzo IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="b8710-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="b8710-124">Una scheda di interfaccia di rete alla quale assegnare l'indirizzo IP pubblico e un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="b8710-124">A NIC, assigning the public IP address and a static private IP address to it.</span></span>
    
    <span data-ttu-id="b8710-125">Sostituire *mypublicdns* con un nome che sia univoco nella località di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8710-125">Replace *mypublicdns* with a name that is unique within the Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="b8710-126">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="b8710-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="b8710-127">Per altre informazioni sui prezzi degli indirizzi IP, vedere la pagina [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="b8710-127">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="b8710-128">È previsto un limite per il numero di indirizzi IP pubblici che possono essere usati in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b8710-128">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="b8710-129">Per altre informazioni sui limiti, vedere l'articolo [Limiti di Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="b8710-129">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="b8710-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="b8710-130">**IPConfig-2**</span></span>

     <span data-ttu-id="b8710-131">Immettere i comandi seguenti per creare una nuova risorsa indirizzo IP pubblico e una nuova configurazione IP con un indirizzo IP pubblico e un indirizzo IP privato statico:</span><span class="sxs-lookup"><span data-stu-id="b8710-131">Enter the following commands to create a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="b8710-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="b8710-132">**IPConfig-3**</span></span>

    <span data-ttu-id="b8710-133">Immettere i comandi seguenti per creare una configurazione IP con un indirizzo IP privato statico e nessun indirizzo IP pubblico:</span><span class="sxs-lookup"><span data-stu-id="b8710-133">Enter the following commands to create an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="b8710-134">Sebbene questo articolo assegna tutte le configurazioni IP a una singola scheda di interfaccia di rete, è possibile anche assegnare più configurazioni IP a qualsiasi scheda di interfaccia di rete in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b8710-134">Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations to any NIC in a VM.</span></span> <span data-ttu-id="b8710-135">Per informazioni su come creare una VM con più interfacce di rete, leggere l'articolo Creare una macchina virtuale con più schede di interfaccia di rete usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8710-135">To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="b8710-136">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="b8710-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="b8710-137">Per modificare le dimensioni della macchina virtuale alla versione 2 DS2 Standard, ad esempio, è sufficiente aggiungere la seguente proprietà `--vm-size Standard_DS3_v2` al comando `azure vm create` nel passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="b8710-137">To change the VM size to Standard DS2 v2, for example, simply add the following property `--vm-size Standard_DS3_v2` to the `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="b8710-138">Immettere il comando seguente per visualizzare la scheda di interfaccia di rete e le configurazioni IP associate:</span><span class="sxs-lookup"><span data-stu-id="b8710-138">Enter the following command to view the NIC and the associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="b8710-139">Aggiungere gli indirizzi IP privati al sistema operativo della macchina virtuale seguendo la procedura per il proprio sistema operativo riportata nella sezione [Aggiungere indirizzi IP a una macchina virtuale](#os-config) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b8710-139">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="b8710-140"><a name="add"></a>Aggiungere indirizzi IP a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b8710-140"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="b8710-141">È possibile aggiungere indirizzi IP privati e pubblici a una scheda di interfaccia di rete esistente completando la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="b8710-141">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="b8710-142">Gli esempi si basano sullo [scenario](#Scenario) descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b8710-142">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="b8710-143">Aprire l'interfaccia della riga di comando di Azure e completare i passaggi rimanenti in questa sezione all'interno di una singola sessione dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b8710-143">Open Azure CLI and complete the remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="b8710-144">Se l'interfaccia della riga di comando di Azure non è installata e configurata, completare la procedura riportata nell'articolo [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="b8710-144">If you don't already have Azure CLI installed and configured, complete the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="b8710-145">Completare i passaggi in una delle sezioni seguenti, a seconda delle esigenze:</span><span class="sxs-lookup"><span data-stu-id="b8710-145">Complete the steps in one of the following sections, based on your requirements:</span></span>

    - <span data-ttu-id="b8710-146">**Aggiungere un indirizzo IP privato**</span><span class="sxs-lookup"><span data-stu-id="b8710-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="b8710-147">Per aggiungere un indirizzo IP privato a una scheda di interfaccia di rete, è necessario creare una configurazione IP tramite il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="b8710-147">To add a private IP address to a NIC, you must create an IP configuration using the command below.</span></span> <span data-ttu-id="b8710-148">L'indirizzo statico deve essere un indirizzo non usato per la subnet.</span><span class="sxs-lookup"><span data-stu-id="b8710-148">The static address must be an unused address for the subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="b8710-149">Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).</span><span class="sxs-lookup"><span data-stu-id="b8710-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="b8710-150">**Aggiungere un indirizzo IP pubblico**</span><span class="sxs-lookup"><span data-stu-id="b8710-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="b8710-151">L'indirizzo IP pubblico viene aggiunto associandolo a una nuova configurazione IP o a una configurazione IP esistente.</span><span class="sxs-lookup"><span data-stu-id="b8710-151">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="b8710-152">Completare i passaggi in una delle sezioni che seguono, a seconda del caso.</span><span class="sxs-lookup"><span data-stu-id="b8710-152">Complete the steps in one of the sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="b8710-153">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="b8710-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="b8710-154">Per altre informazioni sui prezzi degli indirizzi IP, vedere la pagina [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="b8710-154">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="b8710-155">È previsto un limite per il numero di indirizzi IP pubblici che possono essere usati in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b8710-155">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="b8710-156">Per altre informazioni sui limiti, vedere l'articolo [Limiti di Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="b8710-156">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="b8710-157">**Associare la risorsa a una nuova configurazione IP**</span><span class="sxs-lookup"><span data-stu-id="b8710-157">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="b8710-158">Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="b8710-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="b8710-159">È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="b8710-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="b8710-160">Per crearne una nuova, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b8710-160">To create a new one, enter the following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="b8710-161">Per creare una nuova configurazione IP con un indirizzo IP privato statico e la risorsa indirizzo IP pubblico *myPublicIP3* associata, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b8710-161">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="b8710-162">**Associare la risorsa a una nuova configurazione IP**</span><span class="sxs-lookup"><span data-stu-id="b8710-162">**Associate the resource to an existing IP configuration**</span></span>

        <span data-ttu-id="b8710-163">Una risorsa indirizzo IP pubblico può essere associata a una configurazione IP cui non ne sia associata alcuna.</span><span class="sxs-lookup"><span data-stu-id="b8710-163">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="b8710-164">È possibile stabilire se una configurazione IP dispone di un indirizzo IP pubblico associato immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b8710-164">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="b8710-165">Cercare una riga simile a quella che segue per IPConfig-3 nell'output restituito:</span><span class="sxs-lookup"><span data-stu-id="b8710-165">Look for a line similar to the one that follows for IPConfig-3 in the returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="b8710-166">Poiché la colonna **IP pubblico** per *IpConfig-3* è vuota, nessuna risorsa di indirizzo IP pubblico è attualmente associata.</span><span class="sxs-lookup"><span data-stu-id="b8710-166">Since the **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="b8710-167">È possibile aggiungere una risorsa indirizzo IP pubblico esistente a IpConfig-3 o immettere il comando seguente per crearne una:</span><span class="sxs-lookup"><span data-stu-id="b8710-167">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="b8710-168">Immettere il comando seguente per associare la risorsa indirizzo IP pubblico alla configurazione IP esistente denominata *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="b8710-168">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="b8710-169">Visualizzare le risorse indirizzo IP privato e indirizzo IP pubblico assegnate alla scheda di interfaccia di rete immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b8710-169">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="b8710-170">L'output restituito è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b8710-170">The returned output is similar to the following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="b8710-171">Aggiungere al sistema operativo della macchina virtuale gli indirizzi IP privati aggiunti alla scheda di interfaccia di rete seguendo le istruzioni disponibili nella sezione [Aggiungere indirizzi IP a una macchina virtuale](#os-config) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b8710-171">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="b8710-172">Non aggiungere gli indirizzi IP pubblici al sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b8710-172">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
