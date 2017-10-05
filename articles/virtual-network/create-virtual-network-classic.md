---
title: "Creare una rete virtuale (classica) di Azure con più subnet | Microsoft Docs"
description: "Informazioni su come creare una rete virtuale (classica) con più subnet in Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 95c2f4fe40590a8d809f634fb5b2c92d07421bb0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="90dac-103">Creare una rete virtuale (classica) con più subnet</span><span class="sxs-lookup"><span data-stu-id="90dac-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90dac-104">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="90dac-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="90dac-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="90dac-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="90dac-106">Microsoft consiglia di creare la maggior parte di nuove reti virtuali tramite il modello di distribuzione [Resource Manager](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="90dac-106">Microsoft recommends creating most new virtual networks through the [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="90dac-107">Questa esercitazione spiega come creare una rete virtuale (classica) di Azure di base con subnet pubblica e privata separate.</span><span class="sxs-lookup"><span data-stu-id="90dac-107">In this tutorial, learn how to create a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="90dac-108">È possibile creare risorse di Azure, ad esempio macchine virtuali e servizi cloud in una subnet.</span><span class="sxs-lookup"><span data-stu-id="90dac-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="90dac-109">Le risorse create nelle reti virtuali (classica) possono comunicare tra loro e con le risorse di altre reti connesse a una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="90dac-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected to a virtual network.</span></span>

<span data-ttu-id="90dac-110">Altre informazioni su tutte le impostazioni relative alla [rete virtuale](virtual-network-manage-network.md) e alla [subnet](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="90dac-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="90dac-111">Le reti virtuali (classica) vengono eliminate immediatamente da Azure quando una [sottoscrizione viene disabilitata](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="90dac-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="90dac-112">Le reti virtuali (classica) vengono eliminate indipendentemente dall'esistenza di risorse nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="90dac-112">Virtual networks (classic) are deleted regardless of whether resources exist in the virtual network.</span></span> <span data-ttu-id="90dac-113">Se si abilita di nuovo la sottoscrizione in un secondo momento, è necessario ricreare le risorse che erano presenti nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="90dac-113">If you later re-enable the subscription, resources that existed in the virtual network must be recreated.</span></span>

<span data-ttu-id="90dac-114">Si crea una rete virtuale (classica) usando il [portale di Azure](#portal), l'[interfaccia della riga di comando di Azure 1.0 ](#azure-cli) o [Azure PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="90dac-114">You can create a virtual network (classic) by using the [Azure portal](#portal), the [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="90dac-115">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="90dac-115">Portal</span></span>

1. <span data-ttu-id="90dac-116">In un browser Internet passare al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90dac-116">In an Internet browser, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="90dac-117">Accedere usando l'[account Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="90dac-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="90dac-118">Se non si ha un account Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="90dac-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="90dac-119">Fare clic su **+Nuovo** nel portale.</span><span class="sxs-lookup"><span data-stu-id="90dac-119">Click **+New** in the portal.</span></span>
3. <span data-ttu-id="90dac-120">Immettere *Rete virtuale* nella casella **Cerca nel Marketplace** nella parte superiore del pannello **Nuovo** visualizzato.</span><span class="sxs-lookup"><span data-stu-id="90dac-120">Enter *Virtual network* in the **Search the Marketplace** box at the top of the **New** blade that appears.</span></span>  <span data-ttu-id="90dac-121">Fare clic su **Rete virtuale** quando viene visualizzato nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="90dac-121">Click **Virtual network** when it appears in the search results.</span></span>
4. <span data-ttu-id="90dac-122">Nel pannello **Rete virtuale** visualizzato selezionare **Classico** nella casella **Selezionare un modello di distribuzione** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="90dac-122">Select **Classic** in the **Select a deployment model** box in the **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="90dac-123">Nel pannello **Crea rete virtuale (classica)** immettere i valori seguenti e quindi fare clic su **Crea**:</span><span class="sxs-lookup"><span data-stu-id="90dac-123">Enter the following values on the **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="90dac-124">Impostazione</span><span class="sxs-lookup"><span data-stu-id="90dac-124">Setting</span></span>|<span data-ttu-id="90dac-125">Valore</span><span class="sxs-lookup"><span data-stu-id="90dac-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="90dac-126">Nome</span><span class="sxs-lookup"><span data-stu-id="90dac-126">Name</span></span>|<span data-ttu-id="90dac-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="90dac-127">myVnet</span></span>|
    |<span data-ttu-id="90dac-128">Spazio degli indirizzi</span><span class="sxs-lookup"><span data-stu-id="90dac-128">Address space</span></span>|<span data-ttu-id="90dac-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="90dac-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="90dac-130">Nome della subnet</span><span class="sxs-lookup"><span data-stu-id="90dac-130">Subnet name</span></span>|<span data-ttu-id="90dac-131">Pubblico</span><span class="sxs-lookup"><span data-stu-id="90dac-131">Public</span></span>|
    |<span data-ttu-id="90dac-132">Intervallo di indirizzi subnet</span><span class="sxs-lookup"><span data-stu-id="90dac-132">Subnet address range</span></span>|<span data-ttu-id="90dac-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="90dac-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="90dac-134">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="90dac-134">Resource group</span></span>|<span data-ttu-id="90dac-135">Lasciare selezionata l'opzione **Crea nuovo** e quindi immettere **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="90dac-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="90dac-136">Sottoscrizione e località</span><span class="sxs-lookup"><span data-stu-id="90dac-136">Subscription and location</span></span>|<span data-ttu-id="90dac-137">Selezionare la sottoscrizione e la posizione.</span><span class="sxs-lookup"><span data-stu-id="90dac-137">Select your subscription and location.</span></span>

    <span data-ttu-id="90dac-138">Se non si ha familiarità con Azure, acquisire altre informazioni su [gruppi di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [sottoscrizioni](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) e [località](https://azure.microsoft.com/regions), dette anche *aree*.</span><span class="sxs-lookup"><span data-stu-id="90dac-138">If you're new to Azure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred to as *regions*).</span></span>
4. <span data-ttu-id="90dac-139">Quando si crea una rete virtuale nel portale, è possibile creare una sola subnet.</span><span class="sxs-lookup"><span data-stu-id="90dac-139">In the portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="90dac-140">In questa esercitazione verrà creata una seconda subnet dopo la creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="90dac-140">In this tutorial, you create a second subnet after you create the virtual network.</span></span> <span data-ttu-id="90dac-141">In seguito sarà quindi possibile creare risorse accessibili da Internet nella subnet **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="90dac-141">You might later create Internet-accessible resources in the **Public** subnet.</span></span> <span data-ttu-id="90dac-142">Sarà anche possibile creare risorse non accessibili da Internet in una subnet **privata**.</span><span class="sxs-lookup"><span data-stu-id="90dac-142">You also might create resources that aren't accessible from the Internet in the **Private** subnet.</span></span> <span data-ttu-id="90dac-143">Per creare la seconda subnet immettere **myVnet** nella casella **Cerca risorse** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="90dac-143">To create the second subnet, enter **myVnet** in the **Search resources** box at the top of the page.</span></span> <span data-ttu-id="90dac-144">Fare clic su **myVnet** quando questo elemento viene visualizzato nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="90dac-144">Click **myVnet** when it appears in the search results.</span></span>
5. <span data-ttu-id="90dac-145">Fare clic su **Subnet** nella sezione **IMPOSTAZIONI** del pannello **Crea rete virtuale (classica)** visualizzato.</span><span class="sxs-lookup"><span data-stu-id="90dac-145">Click **Subnets** (in the **SETTINGS** section) on the **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="90dac-146">Fare clic su **+ Aggiungi** nel pannello **myVnet - subnet** visualizzato.</span><span class="sxs-lookup"><span data-stu-id="90dac-146">Click **+Add** on the **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="90dac-147">Immettere **Privata** per **Nome** nel pannello **Aggiungi subnet**.</span><span class="sxs-lookup"><span data-stu-id="90dac-147">Enter **Private** for **Name** on the **Add subnet** blade.</span></span> <span data-ttu-id="90dac-148">Immettere **10.0.1.0/24** per **Intervallo indirizzi**.</span><span class="sxs-lookup"><span data-stu-id="90dac-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="90dac-149">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90dac-149">Click **OK**.</span></span>
8. <span data-ttu-id="90dac-150">Nel pannello **myVnet - subnet** è possibile visualizzare le subnet **pubblica** e **privata** create.</span><span class="sxs-lookup"><span data-stu-id="90dac-150">On the **myVnet - Subnets** blade, you can see the **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="90dac-151">**Facoltativo**: al termine di questa esercitazione è possibile eliminare le risorse create per non incorrere in costi di utilizzo:</span><span class="sxs-lookup"><span data-stu-id="90dac-151">**Optional**: When you finish this tutorial, you might want to delete the resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="90dac-152">Fare clic su **Panoramica** nel pannello **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="90dac-152">Click **Overview** on the **myVnet** blade.</span></span>
    - <span data-ttu-id="90dac-153">Fare clic sull'icona **Elimina** nel pannello **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="90dac-153">Click the **Delete** icon on the **myVnet** blade.</span></span>
    - <span data-ttu-id="90dac-154">Per confermare l'eliminazione, nella casella **Elimina rete virtuale** fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="90dac-154">To confirm the deletion, click **Yes** in the **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="90dac-155">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="90dac-155">Azure CLI</span></span>

1. <span data-ttu-id="90dac-156">È possibile [installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) oppure usare l'interfaccia della riga di comando all'interno di Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="90dac-156">You can either [install and configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use the CLI within the Azure Cloud Shell.</span></span> <span data-ttu-id="90dac-157">Azure Cloud Shell è una shell Bash gratuita che può essere eseguita direttamente nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90dac-157">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="90dac-158">Include l'interfaccia della riga di comando di Azure preinstallata e configurata per l'uso con l'account.</span><span class="sxs-lookup"><span data-stu-id="90dac-158">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="90dac-159">Per informazioni sui comandi dell'interfaccia della riga di comando, digitare `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="90dac-159">To get help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="90dac-160">In una sessione dell'interfaccia della riga di comando accedere a Azure con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="90dac-160">In a CLI session, log in to Azure with the command that follows.</span></span> <span data-ttu-id="90dac-161">Se si fa clic **Prova** nella casella sottostante, viene aperto il servizio Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="90dac-161">If you click **Try it** in the box below, a Cloud Shell opens.</span></span> <span data-ttu-id="90dac-162">È possibile accedere alla sottoscrizione di Azure senza immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="90dac-162">You can log in to your Azure subscription, without entering the following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="90dac-163">Per garantire che l'interfaccia della riga di comando si trovi in modalità Gestione dei servizi, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="90dac-163">To ensure the CLI is in Service Management mode, enter the following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="90dac-164">Creare una rete virtuale con una subnet privata:</span><span class="sxs-lookup"><span data-stu-id="90dac-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="90dac-165">Creare una subnet pubblica all'interno della rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="90dac-165">Create a public subnet within the virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="90dac-166">Rivedere la rete virtuale e le subnet:</span><span class="sxs-lookup"><span data-stu-id="90dac-166">Review the virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="90dac-167">**Facoltativo**: al termine di questa esercitazione è possibile eliminare le risorse create per non incorrere in costi di utilizzo:</span><span class="sxs-lookup"><span data-stu-id="90dac-167">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="90dac-168">Anche se non è possibile specificare un gruppo di risorse per creare una rete virtuale (classica) usando l'interfaccia della riga di comando, Azure crea la rete virtuale in un gruppo di risorse denominato *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="90dac-168">Though you can't specify a resource group to create a virtual network (classic) in using the CLI, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="90dac-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90dac-169">PowerShell</span></span>

1. <span data-ttu-id="90dac-170">Installare la versione più recente del modulo [Azure](https://www.powershellgallery.com/packages/Azure) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90dac-170">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="90dac-171">Se non si ha familiarità con Azure PowerShell, vedere [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) (Panoramica di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="90dac-171">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="90dac-172">Avviare una sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90dac-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="90dac-173">In PowerShell accedere ad Azure immettendo il comando `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="90dac-173">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="90dac-174">Modificare il percorso e il nome file seguenti in base alle esigenze, quindi esportare il file di configurazione di rete esistente:</span><span class="sxs-lookup"><span data-stu-id="90dac-174">Change the following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="90dac-175">Per creare una rete virtuale con subnet pubblica e privata, usare un editor di testo per aggiungere l'elemento **VirtualNetworkSite** seguente al file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="90dac-175">To create a virtual network with public and private subnets, use any text editor to add the **VirtualNetworkSite** element that follows to the network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="90dac-176">Rivedere la versione completa dello [schema di file di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="90dac-176">Review the full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="90dac-177">Importare il file di configurazione di rete:</span><span class="sxs-lookup"><span data-stu-id="90dac-177">Import the network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="90dac-178">L'importazione di un file di configurazione di rete modificato può modificare le reti virtuali esistenti create con la distribuzione classica nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="90dac-178">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="90dac-179">Assicurarsi di aggiungere solo la rete virtuale precedente e di non modificare o rimuovere le reti virtuali esistenti dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="90dac-179">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="90dac-180">Rivedere la rete virtuale e le subnet:</span><span class="sxs-lookup"><span data-stu-id="90dac-180">Review the virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="90dac-181">**Facoltativo**: al termine di questa esercitazione è possibile eliminare le risorse create per non incorrere in costi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="90dac-181">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="90dac-182">Per eliminare la rete virtuale, completare i passaggi 4-6, questa volta rimuovendo l'elemento **VirtualNetworkSite** nel passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="90dac-182">To delete the virtual network, complete steps 4-6 again, this time removing the **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="90dac-183">Anche se non è possibile specificare un gruppo di risorse per creare una rete virtuale (classica) usando PowerShell, Azure crea la rete virtuale in un gruppo di risorse denominato *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="90dac-183">Though you can't specify a resource group to create a virtual network (classic) in using PowerShell, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="90dac-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90dac-184">Next steps</span></span>

- <span data-ttu-id="90dac-185">Per informazioni sulle impostazioni delle reti virtuali e delle subnet, vedere [Gestire le reti virtuali](virtual-network-manage-network.md) e [Gestire le subnet di rete virtuali](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="90dac-185">To learn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="90dac-186">In un ambiente di produzione sono disponibili varie opzioni per l'uso di reti virtuali e subnet per soddisfare requisiti diversi.</span><span class="sxs-lookup"><span data-stu-id="90dac-186">You have various options for using virtual networks and subnets in a production environment to meet different requirements.</span></span>
- <span data-ttu-id="90dac-187">Per filtrare il traffico delle subnet in ingresso e in uscita, creare e applicare [gruppi di sicurezza di rete](virtual-networks-nsg.md) alle subnet.</span><span class="sxs-lookup"><span data-stu-id="90dac-187">To filter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) to subnets.</span></span>
- <span data-ttu-id="90dac-188">Creare una macchina virtuale [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e quindi connetterla a una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="90dac-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it to an existing virtual network.</span></span>
- <span data-ttu-id="90dac-189">Per connettere due reti virtuali nella stessa località di Azure, creare un [peering reti virtuali](create-peering-different-deployment-models.md) tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="90dac-189">To connect two virtual networks in the same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between the virtual networks.</span></span> <span data-ttu-id="90dac-190">È possibile connettere una rete virtuale (Gestione risorse) a una rete virtuale (classica), ma non è possibile creare un peering tra due reti virtuali (classica).</span><span class="sxs-lookup"><span data-stu-id="90dac-190">You can peer a virtual network (Resource Manager) to a virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="90dac-191">Connettere la rete virtuale a una rete locale tramite un [Gateway VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o un circuito [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="90dac-191">Connect the virtual network to an on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
