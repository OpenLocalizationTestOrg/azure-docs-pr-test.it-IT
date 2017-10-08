---
title: "aaaVM con più indirizzi IP mediante Azure CLI 1.0 hello | Documenti Microsoft"
description: "Informazioni su come tooassign più gli indirizzi IP tooa macchina virtuale utilizzando hello Azure CLI 1.0 | Gestore delle risorse."
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
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="6b133-103">Assegnare più indirizzi IP macchine toovirtual mediante Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6b133-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="6b133-104">In questo articolo viene illustrato come una macchina virtuale (VM) tramite il modello di distribuzione Azure Resource Manager hello utilizzando toocreate hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="6b133-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="6b133-105">Impossibile assegnare più indirizzi IP tooresources creato tramite il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="6b133-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="6b133-106">ulteriori informazioni sui modelli di distribuzione di Azure, leggere hello toolearn [comprendere i modelli di distribuzione](../resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="6b133-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="6b133-107"><a name = "create"></a>Creare una macchina virtuale con più indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="6b133-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="6b133-108">È possibile completare questa attività usando hello Azure CLI 1.0 (in questo articolo) o hello [CLI di Azure 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6b133-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="6b133-109">passaggi di Hello che seguono viene illustrato come toocreate un esempio di macchina virtuale con più IP risolve, come descritto nello scenario di hello.</span><span class="sxs-lookup"><span data-stu-id="6b133-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="6b133-110">Modificare i nomi delle variabili e i tipi di indirizzi IP come richiesto per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="6b133-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="6b133-111">Installare e configurare Azure CLI 1.0 da hello seguente passaggi hello in hello [installare e configurare hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo e accedere al proprio account Azure con hello `azure-login` comando.</span><span class="sxs-lookup"><span data-stu-id="6b133-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="6b133-112">Creare un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="6b133-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="6b133-113">Creare una rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="6b133-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="6b133-114">Creare una subnet nella rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="6b133-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="6b133-115">Creare un account di archiviazione per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b133-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="6b133-116">Prima di eseguire hello seguente comando, sostituire *mystorageaccount* con un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="6b133-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="6b133-117">nome Hello deve essere univoco in Azure:</span><span class="sxs-lookup"><span data-stu-id="6b133-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="6b133-118">Creare hello le configurazioni IP, una scheda di rete e assegnare hello IP configurazioni toohello scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="6b133-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="6b133-119">È possibile aggiungere, rimuovere o modificare le configurazioni di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="6b133-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="6b133-120">Hello le configurazioni seguenti è descritti nello scenario hello:</span><span class="sxs-lookup"><span data-stu-id="6b133-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="6b133-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="6b133-121">**IPConfig-1**</span></span>

    <span data-ttu-id="6b133-122">Immettere i comandi che seguono toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="6b133-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="6b133-123">Una risorsa indirizzo IP pubblico con un indirizzo IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="6b133-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="6b133-124">Una scheda di rete, assegnazione di indirizzo IP pubblico hello e una tooit di indirizzo IP privato statico.</span><span class="sxs-lookup"><span data-stu-id="6b133-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="6b133-125">Sostituire *mypublicdns* con un nome univoco all'interno di hello località di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b133-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="6b133-126">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="6b133-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="6b133-127">ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="6b133-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="6b133-128">È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6b133-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="6b133-129">informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.</span><span class="sxs-lookup"><span data-stu-id="6b133-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="6b133-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="6b133-130">**IPConfig-2**</span></span>

     <span data-ttu-id="6b133-131">Immettere i seguenti comandi toocreate hello una nuova risorsa di indirizzo IP pubblica e una nuova configurazione IP con un indirizzo IP pubblico statico e un indirizzo IP privato statico:</span><span class="sxs-lookup"><span data-stu-id="6b133-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="6b133-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="6b133-132">**IPConfig-3**</span></span>

    <span data-ttu-id="6b133-133">Immettere i seguenti comandi toocreate una configurazione IP con un indirizzo IP privato statico e alcun indirizzo IP pubblico hello:</span><span class="sxs-lookup"><span data-stu-id="6b133-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="6b133-134">Anche se in questo articolo assegna tutti tooa di configurazioni IP singola scheda di rete, è inoltre possibile assegnare più tooany di configurazioni IP NIC in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b133-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="6b133-135">la modalità di lettura di una macchina virtuale con più schede di rete, toocreate toolearn hello crea una macchina virtuale con più schede di rete articolo.</span><span class="sxs-lookup"><span data-stu-id="6b133-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="6b133-136">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="6b133-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="6b133-137">toochange hello v2 tooStandard DS2 dimensioni di macchina virtuale, ad esempio, aggiungere semplicemente hello seguente proprietà `--vm-size Standard_DS3_v2` toohello `azure vm create` comando nel passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="6b133-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="6b133-138">Immettere hello successivo comando tooview hello NIC e hello configurazioni IP associate:</span><span class="sxs-lookup"><span data-stu-id="6b133-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="6b133-139">Toohello macchina virtuale del sistema operativo di indirizzi IP privati di Aggiungi hello completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6b133-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="6b133-140"><a name="add"></a>Aggiungere tooa di indirizzi IP VM</span><span class="sxs-lookup"><span data-stu-id="6b133-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="6b133-141">È possibile aggiungere ulteriori pubbliche e private IP indirizzi tooan esistente NIC completando i passaggi di hello che seguono.</span><span class="sxs-lookup"><span data-stu-id="6b133-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="6b133-142">esempi di Hello si basano su hello [scenario](#Scenario) descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6b133-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="6b133-143">Aprire CLI di Azure e completa hello rimanenti passaggi in questa sezione all'interno di una singola sessione CLI.</span><span class="sxs-lookup"><span data-stu-id="6b133-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="6b133-144">Se si dispone già di Azure CLI installato e configurato, hello completato i passaggi in hello [installare e configurare hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo e accedere al proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="6b133-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="6b133-145">Completare i passaggi di hello in uno di hello le sezioni, in base ai requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b133-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="6b133-146">**Aggiungere un indirizzo IP privato**</span><span class="sxs-lookup"><span data-stu-id="6b133-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="6b133-147">tooadd un tooa di indirizzo IP privato NIC, è necessario creare una configurazione IP utilizzando hello comando riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6b133-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="6b133-148">indirizzo statico Hello deve essere un indirizzo per subnet hello inutilizzato.</span><span class="sxs-lookup"><span data-stu-id="6b133-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="6b133-149">Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).</span><span class="sxs-lookup"><span data-stu-id="6b133-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="6b133-150">**Aggiungere un indirizzo IP pubblico**</span><span class="sxs-lookup"><span data-stu-id="6b133-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="6b133-151">Viene aggiunto un indirizzo IP pubblico associandolo tooeither una nuova configurazione IP o una configurazione IP esistente.</span><span class="sxs-lookup"><span data-stu-id="6b133-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="6b133-152">Completare i passaggi di hello nelle sezioni che seguono, hello necessari.</span><span class="sxs-lookup"><span data-stu-id="6b133-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="6b133-153">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="6b133-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="6b133-154">ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="6b133-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="6b133-155">È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6b133-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="6b133-156">informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.</span><span class="sxs-lookup"><span data-stu-id="6b133-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="6b133-157">**Associare hello risorsa tooa nuova configurazione IP**</span><span class="sxs-lookup"><span data-stu-id="6b133-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="6b133-158">Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="6b133-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="6b133-159">È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="6b133-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="6b133-160">toocreate uno nuovo, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b133-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="6b133-161">una nuova configurazione IP con un indirizzo IP privato statico e hello associata toocreate *myPublicIP3* indirizzo IP pubblico risorsa degli indirizzi, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b133-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="6b133-162">**Associare risorse hello tooan esistente configurazione IP**</span><span class="sxs-lookup"><span data-stu-id="6b133-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="6b133-163">Una risorsa di indirizzo IP pubblica può essere solo la configurazione IP tooan associato che non ha ancora associata.</span><span class="sxs-lookup"><span data-stu-id="6b133-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="6b133-164">È possibile determinare se una configurazione IP è un indirizzo IP pubblico associato immettendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b133-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="6b133-165">Cerca un toohello simile di riga che segue per IPConfig-3 nell'output restituito hello:</span><span class="sxs-lookup"><span data-stu-id="6b133-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="6b133-166">Poiché hello **indirizzo IP pubblico** colonna per *IpConfig 3* è vuoto, nessuna risorsa dell'indirizzo IP pubblica è tooit attualmente associato.</span><span class="sxs-lookup"><span data-stu-id="6b133-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="6b133-167">È possibile aggiungere un esistente pubblica IP indirizzo risorsa tooIpConfig-3 o immettere hello toocreate comando uno di seguito:</span><span class="sxs-lookup"><span data-stu-id="6b133-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="6b133-168">Immettere hello comando risorsa toohello configurazione IP esistente denominato di indirizzo IP pubblico di tooassociate hello seguente *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="6b133-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="6b133-169">Visualizzare gli indirizzi IP privati hello e hello pubblica IP indirizzo risorse assegnato toohello NIC immettendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b133-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="6b133-170">Hello ha restituito l'output è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b133-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="6b133-171">Aggiungere indirizzi IP privati hello è stato aggiunto il sistema operativo VM di toohello NIC toohello seguendo le istruzioni hello hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6b133-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="6b133-172">Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="6b133-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
