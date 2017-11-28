---
title: "una rete virtuale di Azure (classica) con più subnet aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una rete virtuale (classica) con più subnet in Azure."
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
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="10935-103">Creare una rete virtuale (classica) con più subnet</span><span class="sxs-lookup"><span data-stu-id="10935-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10935-104">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10935-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="10935-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="10935-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="10935-106">Microsoft consiglia di creare la maggior parte delle nuove reti virtuali tramite hello [Gestione risorse](virtual-networks-create-vnet-arm-pportal.md) modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="10935-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="10935-107">In questa esercitazione, informazioni su come toocreate una base rete virtuale di Azure (versione classica) con separati subnet pubblica e privata.</span><span class="sxs-lookup"><span data-stu-id="10935-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="10935-108">È possibile creare risorse di Azure, ad esempio macchine virtuali e servizi cloud in una subnet.</span><span class="sxs-lookup"><span data-stu-id="10935-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="10935-109">Le risorse create in reti virtuali (classico) possono comunicare tra loro e con le risorse di rete virtuale di tooa connesso altre reti.</span><span class="sxs-lookup"><span data-stu-id="10935-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="10935-110">Altre informazioni su tutte le impostazioni relative alla [rete virtuale](virtual-network-manage-network.md) e alla [subnet](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="10935-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="10935-111">Le reti virtuali (classica) vengono eliminate immediatamente da Azure quando una [sottoscrizione viene disabilitata](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="10935-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="10935-112">Reti virtuali (classiche) vengono eliminate indipendentemente dall'esistono di risorse nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="10935-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="10935-113">Se si abilita di nuovo sottoscrizione hello in un secondo momento, è necessario ricreare le risorse presenti nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="10935-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="10935-114">È possibile creare una rete virtuale (versione classica) con hello [portale di Azure](#portal), hello [Azure interfaccia della riga di comando (CLI) 1.0](#azure-cli), o [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="10935-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="10935-115">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="10935-115">Portal</span></span>

1. <span data-ttu-id="10935-116">In un browser Internet, visitare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="10935-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="10935-117">Accedere usando l'[account Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="10935-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="10935-118">Se non si ha un account Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="10935-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="10935-119">Fare clic su **+ nuovo** nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="10935-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="10935-120">Immettere *rete virtuale* in hello **hello ricerca Marketplace** casella nella parte superiore di hello di hello **New** pannello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="10935-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="10935-121">Fare clic su **rete virtuale** quando viene visualizzato nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="10935-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="10935-122">Selezionare **classico** in hello **selezionare un modello di distribuzione** casella hello **rete virtuale** pannello visualizzato, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="10935-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="10935-123">Immettere hello seguendo i valori hello **crea rete virtuale (classico)** blade e quindi fare clic su **crea**:</span><span class="sxs-lookup"><span data-stu-id="10935-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="10935-124">Impostazione</span><span class="sxs-lookup"><span data-stu-id="10935-124">Setting</span></span>|<span data-ttu-id="10935-125">Valore</span><span class="sxs-lookup"><span data-stu-id="10935-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="10935-126">Nome</span><span class="sxs-lookup"><span data-stu-id="10935-126">Name</span></span>|<span data-ttu-id="10935-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="10935-127">myVnet</span></span>|
    |<span data-ttu-id="10935-128">Spazio degli indirizzi</span><span class="sxs-lookup"><span data-stu-id="10935-128">Address space</span></span>|<span data-ttu-id="10935-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="10935-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="10935-130">Nome della subnet</span><span class="sxs-lookup"><span data-stu-id="10935-130">Subnet name</span></span>|<span data-ttu-id="10935-131">Pubblico</span><span class="sxs-lookup"><span data-stu-id="10935-131">Public</span></span>|
    |<span data-ttu-id="10935-132">Intervallo di indirizzi subnet</span><span class="sxs-lookup"><span data-stu-id="10935-132">Subnet address range</span></span>|<span data-ttu-id="10935-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="10935-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="10935-134">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="10935-134">Resource group</span></span>|<span data-ttu-id="10935-135">Lasciare selezionata l'opzione **Crea nuovo** e quindi immettere **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="10935-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="10935-136">Sottoscrizione e località</span><span class="sxs-lookup"><span data-stu-id="10935-136">Subscription and location</span></span>|<span data-ttu-id="10935-137">Selezionare la sottoscrizione e la posizione.</span><span class="sxs-lookup"><span data-stu-id="10935-137">Select your subscription and location.</span></span>

    <span data-ttu-id="10935-138">Se si tooAzure nuovo, altre informazioni, vedere [gruppi di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [sottoscrizioni](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [percorsi](https://azure.microsoft.com/regions) (definita anche tooas *aree*).</span><span class="sxs-lookup"><span data-stu-id="10935-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="10935-139">Nel portale di hello, è possibile creare una sola subnet quando si crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="10935-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="10935-140">In questa esercitazione, creare una subnet secondo dopo aver creato la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="10935-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="10935-141">In un secondo momento, è possibile creare le risorse accessibili da Internet in hello **pubblica** subnet.</span><span class="sxs-lookup"><span data-stu-id="10935-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="10935-142">È anche possibile creare le risorse che non sono accessibili da Internet Ciao hello **privata** subnet.</span><span class="sxs-lookup"><span data-stu-id="10935-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="10935-143">toocreate hello secondo subnet, immettere **myVnet** in hello **individuare risorse** casella nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="10935-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="10935-144">Fare clic su **myVnet** quando viene visualizzato nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="10935-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="10935-145">Fare clic su **subnet** (in hello **impostazioni** sezione) su hello **crea rete virtuale (classico)** pannello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="10935-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="10935-146">Fare clic su **+ Aggiungi** su hello **myVnet - subnet** pannello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="10935-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="10935-147">Immettere **privata** per **nome** su hello **aggiungere subnet** blade.</span><span class="sxs-lookup"><span data-stu-id="10935-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="10935-148">Immettere **10.0.1.0/24** per **Intervallo indirizzi**.</span><span class="sxs-lookup"><span data-stu-id="10935-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="10935-149">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10935-149">Click **OK**.</span></span>
8. <span data-ttu-id="10935-150">In hello **myVnet - subnet** pannello, è possibile visualizzare hello **pubblica** e **privata** subnet a cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="10935-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="10935-151">**Parametro facoltativo**: al termine di questa esercitazione, è possibile risorse hello toodelete creato, in modo che non si incorrere in costi di utilizzo:</span><span class="sxs-lookup"><span data-stu-id="10935-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="10935-152">Fare clic su **Panoramica** su hello **myVnet** blade.</span><span class="sxs-lookup"><span data-stu-id="10935-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="10935-153">Fare clic su hello **eliminare** icona su hello **myVnet** blade.</span><span class="sxs-lookup"><span data-stu-id="10935-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="10935-154">l'eliminazione di hello tooconfirm, fare clic su **Sì** in hello **rete virtuale Delete** casella.</span><span class="sxs-lookup"><span data-stu-id="10935-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="10935-155">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="10935-155">Azure CLI</span></span>

1. <span data-ttu-id="10935-156">È possibile [installare e configurare hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), oppure utilizzare hello CLI all'interno di hello Shell di Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="10935-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="10935-157">Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="10935-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="10935-158">Ha hello CLI di Azure preinstallato e configurato toouse con l'account.</span><span class="sxs-lookup"><span data-stu-id="10935-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="10935-159">Guida di tooget per i comandi CLI, digitare `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="10935-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="10935-160">In una sessione CLI, accedi tooAzure con il comando che segue hello.</span><span class="sxs-lookup"><span data-stu-id="10935-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="10935-161">Se si fa clic **provarla** nella casella hello sottostante, consente di aprire una Shell di Cloud.</span><span class="sxs-lookup"><span data-stu-id="10935-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="10935-162">Tooyour sottoscrizione di Azure, è possibile accedere senza dover immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="10935-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="10935-163">hello tooensure CLI è in modalità di gestione dei servizi, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="10935-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="10935-164">Creare una rete virtuale con una subnet privata:</span><span class="sxs-lookup"><span data-stu-id="10935-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="10935-165">Creare una subnet pubblica all'interno di rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="10935-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="10935-166">Esaminare la rete virtuale hello e subnet:</span><span class="sxs-lookup"><span data-stu-id="10935-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="10935-167">**Parametro facoltativo**: È possibile che le risorse di hello toodelete creato al termine di questa esercitazione, in modo che non si incorrere in costi di utilizzo:</span><span class="sxs-lookup"><span data-stu-id="10935-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="10935-168">Se non è possibile specificare un toocreate gruppo di risorse una rete virtuale (classica) utilizzando hello CLI, Azure crea rete virtuale hello in un gruppo di risorse denominato *predefinito rete*.</span><span class="sxs-lookup"><span data-stu-id="10935-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="10935-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="10935-169">PowerShell</span></span>

1. <span data-ttu-id="10935-170">Installare hello l'ultima versione di hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) modulo.</span><span class="sxs-lookup"><span data-stu-id="10935-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="10935-171">Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10935-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="10935-172">Avviare una sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10935-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="10935-173">In PowerShell, accedere tooAzure immettendo hello `Add-AzureAccount` comando.</span><span class="sxs-lookup"><span data-stu-id="10935-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="10935-174">Modificare l'esempio hello percorso e nome file, come appropriato, quindi esportare il file di configurazione di rete esistente:</span><span class="sxs-lookup"><span data-stu-id="10935-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="10935-175">toocreate una rete virtuale con subnet pubbliche e private, utilizzare qualsiasi hello tooadd editor di testo **VirtualNetworkSite** elemento che segue toohello file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="10935-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

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

    <span data-ttu-id="10935-176">Hello revisione completa [schema di file di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="10935-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="10935-177">Importare i file di configurazione di rete hello:</span><span class="sxs-lookup"><span data-stu-id="10935-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="10935-178">L'importazione di un file di configurazione di rete modificato può causare modifiche tooexisting reti virtuali (classiche) nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="10935-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="10935-179">Assicurarsi di aggiungere solo reti virtuali precedente hello e di non modificare o rimuovere qualsiasi rete virtuale esistente dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="10935-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="10935-180">Esaminare la rete virtuale hello e subnet:</span><span class="sxs-lookup"><span data-stu-id="10935-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="10935-181">**Parametro facoltativo**: È possibile che le risorse di hello toodelete creato al termine di questa esercitazione, in modo che non si incorrere in costi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="10935-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="10935-182">toodelete hello rete virtuale completezza i passaggi da 4 a 6 nuovamente questo hello rimozione ora **VirtualNetworkSite** elemento aggiunto nel passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="10935-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="10935-183">Se non è possibile specificare un toocreate gruppo di risorse una rete virtuale (classica) nell'utilizzo di PowerShell, Azure crea rete virtuale hello in un gruppo di risorse denominato *predefinito rete*.</span><span class="sxs-lookup"><span data-stu-id="10935-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="10935-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10935-184">Next steps</span></span>

- <span data-ttu-id="10935-185">toolearn su tutte le reti virtuali e le impostazioni di subnet, vedere [gestire reti virtuali](virtual-network-manage-network.md) e [gestire subnet della rete virtuale](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="10935-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="10935-186">Si sono disponibili varie opzioni per l'utilizzo di reti virtuali e le subnet in una diversi requisiti toomeet ambiente produzione.</span><span class="sxs-lookup"><span data-stu-id="10935-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="10935-187">toofilter in ingresso e in uscita traffico della subnet, creare e applicare [gruppi di sicurezza di rete](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="10935-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="10935-188">Creare un [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) macchina virtuale, quindi connetterla tooan una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="10935-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="10935-189">reti virtuali tooconnect due in hello nello stesso percorso di Azure, creare un [peering reti virtuali](create-peering-different-deployment-models.md) tra reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="10935-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="10935-190">È possibile connettersi a una rete virtuale (classico) tooa di rete virtuale, Gestione risorse (), ma non è possibile creare un peering tra due reti virtuali (classico).</span><span class="sxs-lookup"><span data-stu-id="10935-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="10935-191">Connessione rete locale tooan di rete virtuale hello utilizzando un [Gateway VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.</span><span class="sxs-lookup"><span data-stu-id="10935-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
