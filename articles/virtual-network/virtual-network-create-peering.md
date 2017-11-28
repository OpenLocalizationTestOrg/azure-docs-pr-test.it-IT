---
title: aaaCreate un peering di rete virtuale di Azure - Gestione risorse - stessa sottoscrizione | Documenti Microsoft
description: Informazioni su come toocreate un peering di rete virtuale tra reti virtuali create tramite Gestione risorse presenti in hello stessa sottoscrizione di Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="6944a-103">Creare un peering di rete virtuale - Resource Manager, stessa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6944a-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="6944a-104">In questa esercitazione viene illustrato toocreate peering tra reti virtuali create tramite Gestione risorse di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6944a-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="6944a-105">Entrambe le reti virtuali presenti in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6944a-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="6944a-106">Peering due risorse di consente di reti virtuali in reti virtuali diverse toocommunicate reciprocamente con hello stessa larghezza di banda e latenza, come se fosse di risorse hello in hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6944a-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="6944a-107">Altre informazioni sul [Peering di rete virtuale](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6944a-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="6944a-108">Hello passaggi toocreate un peering di reti virtuali sono diversi, a seconda che le reti virtuali hello siano hello uguale o diverso, sottoscrizioni e che [modello di distribuzione Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) vengono create le reti virtuali hello tramite.</span><span class="sxs-lookup"><span data-stu-id="6944a-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="6944a-109">Informazioni su come toocreate un virtuale rete peering in altri scenari, fare clic su uno scenario di hello di hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="6944a-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="6944a-110">Modello di distribuzione di Azure</span><span class="sxs-lookup"><span data-stu-id="6944a-110">Azure deployment model</span></span>  | <span data-ttu-id="6944a-111">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="6944a-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="6944a-112">Entrambi con Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6944a-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="6944a-113">Diversa</span><span class="sxs-lookup"><span data-stu-id="6944a-113">Different</span></span>|
|[<span data-ttu-id="6944a-114">Uno con Resource Manager, uno con una distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="6944a-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="6944a-115">Uguale</span><span class="sxs-lookup"><span data-stu-id="6944a-115">Same</span></span>|
|[<span data-ttu-id="6944a-116">Uno con Resource Manager, uno con una distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="6944a-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="6944a-117">Diversa</span><span class="sxs-lookup"><span data-stu-id="6944a-117">Different</span></span>|

<span data-ttu-id="6944a-118">Impossibile creare una rete virtuale peering tra due reti virtuali distribuite tramite il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="6944a-119">Un peering di reti virtuali può essere creato solo tra due reti virtuali presenti in hello stessa regione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6944a-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="6944a-120">Se è necessario tooconnect reti virtuali che sono stati creati tramite il modello di distribuzione classica hello o che esistono in diverse aree di Azure, è possibile utilizzare un Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6944a-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="6944a-121">È possibile utilizzare hello [portale di Azure](#portal), hello Azure [interfaccia della riga di comando](#cli) (CLI), Azure [PowerShell](#powershell), o un [modellodigestionerisorsediAzure](#template) toocreate un peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6944a-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="6944a-122">Fare clic su uno qualsiasi dei hello precedente dello strumento collegamenti toogo direttamente toohello i passaggi per la creazione di una rete virtuale peering utilizzando lo strumento di scelta.</span><span class="sxs-lookup"><span data-stu-id="6944a-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="6944a-123"><a name="portal"></a>Creare un peering - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6944a-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="6944a-124">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6944a-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6944a-125">account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6944a-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="6944a-126">Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="6944a-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="6944a-127">Fare clic su **+ Nuovo**, **Rete** e quindi **Rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="6944a-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="6944a-128">In hello **crea rete virtuale** pannello, immettere o selezionare i valori per hello seguenti impostazioni, quindi fare clic su **crea**:</span><span class="sxs-lookup"><span data-stu-id="6944a-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="6944a-129">**Nome**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="6944a-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="6944a-130">**Spazio indirizzi**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="6944a-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="6944a-131">**Nome subnet**: *predefinito*</span><span class="sxs-lookup"><span data-stu-id="6944a-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="6944a-132">**Intervallo di indirizzi subnet**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="6944a-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="6944a-133">**Sottoscrizione**: selezionare la propria sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6944a-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="6944a-134">**Gruppo di risorse**: selezionare **Crea nuovo** e immettere *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="6944a-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="6944a-135">**Località**: *Stati Uniti orientali*</span><span class="sxs-lookup"><span data-stu-id="6944a-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="6944a-136">Completare i passaggi da 2-3 nuovamente specificando hello seguenti valori nel passaggio 3:</span><span class="sxs-lookup"><span data-stu-id="6944a-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="6944a-137">**Nome**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="6944a-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="6944a-138">**Spazio indirizzi**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="6944a-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="6944a-139">**Nome subnet**: *predefinito*</span><span class="sxs-lookup"><span data-stu-id="6944a-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="6944a-140">**Intervallo di indirizzi subnet**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="6944a-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="6944a-141">**Sottoscrizione**: selezionare la propria sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6944a-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="6944a-142">**Gruppo di risorse**: selezionare **Usa esistente** e quindi *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="6944a-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="6944a-143">**Località**: *Stati Uniti orientali*</span><span class="sxs-lookup"><span data-stu-id="6944a-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="6944a-144">In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="6944a-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="6944a-145">Fare clic su **myResourceGroup** quando viene visualizzato nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="6944a-146">Viene visualizzato un pannello per hello **myresourcegroup** gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6944a-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="6944a-147">gruppo di risorse Hello contiene hello due reti virtuali create nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="6944a-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="6944a-148">Fare clic su **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="6944a-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="6944a-149">In hello **myVnet1** pannello visualizzato, fare clic su **peering** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="6944a-150">In hello **myVnet1 - peering** blade che venivano visualizzate, fare clic su **+ Aggiungi**</span><span class="sxs-lookup"><span data-stu-id="6944a-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="6944a-151">In hello **Aggiungi peering** blade che viene visualizzata, immettere o selezionare hello le opzioni seguenti, quindi fare clic su **OK**:</span><span class="sxs-lookup"><span data-stu-id="6944a-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="6944a-152">**Nome**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="6944a-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="6944a-153">**Modello di distribuzione della rete virtuale**: selezionare **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="6944a-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="6944a-154">**Sottoscrizione**: selezionare la propria sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6944a-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="6944a-155">**Rete virtuale**: fare clic su **Scegliere una rete virtuale** e quindi scegliere **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="6944a-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="6944a-156">**Consenti accesso alla rete virtuale:** assicurarsi che sia selezionato **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="6944a-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="6944a-157">Questa esercitazione non prevede l'uso di altre impostazioni.</span><span class="sxs-lookup"><span data-stu-id="6944a-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="6944a-158">lettura toolearn su tutte le impostazioni peer, [gestire peering di reti virtuali](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="6944a-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="6944a-159">Dopo aver fatto clic **OK** nel passaggio precedente hello, hello **Aggiungi peering** pannello chiude e viene visualizzato hello **myVnet1 - peering** pannello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="6944a-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="6944a-160">Dopo alcuni secondi, hello peering creato viene visualizzato nel pannello hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="6944a-161">**Avviato** è elencato nella hello **stato PEERING** colonna per hello **myVnet1ToMyVnet2** peering è creato.</span><span class="sxs-lookup"><span data-stu-id="6944a-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="6944a-162">Si è stato effettuato il peering tooVnet2 Vnet1, ma ora è necessario connettersi myVnet2 toomyVnet1.</span><span class="sxs-lookup"><span data-stu-id="6944a-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="6944a-163">peering Hello è necessario creare in entrambe le direzioni risorse tooenable hello toocommunicate di reti virtuali tra loro.</span><span class="sxs-lookup"><span data-stu-id="6944a-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="6944a-164">Completare di nuovo i passaggi da 5 a 10 per myVnet2.</span><span class="sxs-lookup"><span data-stu-id="6944a-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="6944a-165">Nome hello peering *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="6944a-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="6944a-166">Pochi secondi dopo aver fatto clic **OK** toocreate hello peering per MyVnet2, hello **myVnet2ToMyVnet1** peering appena creato viene elencato con **connesso** in hello  **Lo stato di PEERING** colonna.</span><span class="sxs-lookup"><span data-stu-id="6944a-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="6944a-167">Completare di nuovo i passaggi da 5 a 7 per MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="6944a-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="6944a-168">Hello **stato PEERING** per hello **myVnet1ToVNet2** peering fa ora parte anche **connesso**.</span><span class="sxs-lookup"><span data-stu-id="6944a-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="6944a-169">peering Hello è stata stabilita correttamente dopo aver visualizzato **connesso** in hello **stato PEERING** colonna per entrambe le reti virtuali nel peering hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="6944a-170">**Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.</span><span class="sxs-lookup"><span data-stu-id="6944a-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="6944a-171">**Facoltativo**: le risorse di hello toodelete creati in questa esercitazione, hello completo di passaggi di hello [eliminare risorse](#delete-portal) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6944a-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="6944a-172">Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="6944a-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="6944a-173">Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="6944a-174">Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS.</span><span class="sxs-lookup"><span data-stu-id="6944a-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="6944a-175">Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="6944a-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="6944a-176"><a name="cli"></a>Creare un peering - Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6944a-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="6944a-177">Hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="6944a-177">hello following script:</span></span>

- <span data-ttu-id="6944a-178">Richiede hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="6944a-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6944a-179">versione di hello toofind, eseguire hello `az --version` comando.</span><span class="sxs-lookup"><span data-stu-id="6944a-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="6944a-180">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6944a-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="6944a-181">Funziona in una shell Bash.</span><span class="sxs-lookup"><span data-stu-id="6944a-181">Works in a Bash shell.</span></span> <span data-ttu-id="6944a-182">Per opzioni all'esecuzione di script CLI di Azure su client Windows, vedere [in esecuzione hello CLI di Azure in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6944a-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="6944a-183">Anziché installare hello CLI e le relative dipendenze, è possibile utilizzare hello Shell di Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="6944a-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="6944a-184">Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6944a-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="6944a-185">Ha hello CLI di Azure preinstallato e configurato toouse con l'account.</span><span class="sxs-lookup"><span data-stu-id="6944a-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="6944a-186">Fare clic su hello **provarla** pulsante nello script hello tooyour accedere indicato di seguito, che richiama una Shell di Cloud che consente l'accesso con account di Azure.</span><span class="sxs-lookup"><span data-stu-id="6944a-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="6944a-187">tooexecute hello script, fare clic su hello **copia** pulsante e incollare il contenuto di hello nella Shell Cloud.</span><span class="sxs-lookup"><span data-stu-id="6944a-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="6944a-188">Creare un gruppo di risorse e due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6944a-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="6944a-189">Creare una rete virtuale peering tra due reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="6944a-190">Dopo l'esecuzione di script hello esaminare hello peering per ogni rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6944a-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="6944a-191">Rieseguire hello precedente comando, sostituendo *myVnet1* con *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="6944a-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="6944a-192">Mostra i comandi di output di Hello di entrambi **connesso** in hello **PeeringState** colonna.</span><span class="sxs-lookup"><span data-stu-id="6944a-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="6944a-193">Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="6944a-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="6944a-194">Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="6944a-195">Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS.</span><span class="sxs-lookup"><span data-stu-id="6944a-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="6944a-196">Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="6944a-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="6944a-197">**Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.</span><span class="sxs-lookup"><span data-stu-id="6944a-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="6944a-198">**Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-cli) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6944a-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="6944a-199"><a name="powershell"></a>Creare un peering - PowerShell</span><span class="sxs-lookup"><span data-stu-id="6944a-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="6944a-200">Installare hello l'ultima versione di hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo.</span><span class="sxs-lookup"><span data-stu-id="6944a-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="6944a-201">Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6944a-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="6944a-202">toostart una sessione di PowerShell, andare troppo**avviare**, immettere **powershell**, quindi fare clic su **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6944a-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="6944a-203">In PowerShell, accedere tooAzure immettendo hello `login-azurermaccount` comando.</span><span class="sxs-lookup"><span data-stu-id="6944a-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="6944a-204">account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6944a-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="6944a-205">Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="6944a-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="6944a-206">Creare un gruppo di risorse e due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6944a-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="6944a-207">script hello tooexecute seguente hello copia dello script, incollarlo in PowerShell e quindi premere `Enter` dopo l'ultima riga hello viene visualizzata nella schermata di hello:</span><span class="sxs-lookup"><span data-stu-id="6944a-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="6944a-208">Creare una rete virtuale peering tra due reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="6944a-209">Esempio hello copia dello script, incollare in tooPowerShell e quindi premere `Enter` dopo l'ultima riga hello viene visualizzata nella schermata di hello:</span><span class="sxs-lookup"><span data-stu-id="6944a-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="6944a-210">tooreview hello subnet per la rete virtuale hello, seguente hello copia comando, incollare in tooPowerShell e quindi premere `Enter`:</span><span class="sxs-lookup"><span data-stu-id="6944a-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="6944a-211">Rieseguire hello precedente comando, sostituendo *myVnet1* con *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="6944a-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="6944a-212">Mostra i comandi di output di Hello di entrambi **connesso** in hello **PeeringState** colonna.</span><span class="sxs-lookup"><span data-stu-id="6944a-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="6944a-213">**Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.</span><span class="sxs-lookup"><span data-stu-id="6944a-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="6944a-214">**Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-powershell) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6944a-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="6944a-215">Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="6944a-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="6944a-216">Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="6944a-217">Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS.</span><span class="sxs-lookup"><span data-stu-id="6944a-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="6944a-218">Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="6944a-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="6944a-219"><a name="template"></a>Creare un peering - Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6944a-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="6944a-220">Fare riferimento al modello di Resource Manager per [creare un peering di rete virtuale](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering).</span><span class="sxs-lookup"><span data-stu-id="6944a-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="6944a-221">Le istruzioni vengono forniti con il modello di hello per la distribuzione modello hello utilizzando hello hello Azure CLI, PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6944a-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="6944a-222">Log nello strumento toowhichever scelto toodeploy hello modello con un account che dispone hello toocreate delle autorizzazioni necessarie a una rete virtuale peering.</span><span class="sxs-lookup"><span data-stu-id="6944a-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="6944a-223">Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="6944a-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="6944a-224">**Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.</span><span class="sxs-lookup"><span data-stu-id="6944a-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="6944a-225">**Facoltativo**: le risorse di hello toodelete creati in questa esercitazione, hello completo di passaggi di hello [eliminare risorse](#delete) sezione di questo articolo, utilizzando hello hello Azure CLI, PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6944a-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="6944a-226"><a name="permissions"></a>Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="6944a-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="6944a-227">Hello che è utilizzare una rete virtuale peering toocreate devono disporre hello necessarie ruolo o autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="6944a-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="6944a-228">Ad esempio, se si sono stati peering due reti virtuali denominate VNet1 e VNet2, all'account deve essere assegnato hello seguente ruolo minimo o autorizzazioni per ogni rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="6944a-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="6944a-229">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6944a-229">Virtual network</span></span>|<span data-ttu-id="6944a-230">Ruolo</span><span class="sxs-lookup"><span data-stu-id="6944a-230">Role</span></span>|<span data-ttu-id="6944a-231">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="6944a-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="6944a-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="6944a-232">VNet1</span></span>|[<span data-ttu-id="6944a-233">Collaboratore di rete</span><span class="sxs-lookup"><span data-stu-id="6944a-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="6944a-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="6944a-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="6944a-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="6944a-235">VNet2</span></span>|[<span data-ttu-id="6944a-236">Collaboratore di rete</span><span class="sxs-lookup"><span data-stu-id="6944a-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="6944a-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="6944a-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="6944a-238">Altre informazioni, vedere [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e l'assegnazione di autorizzazioni specifiche troppo[ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Gestione risorse (solo).</span><span class="sxs-lookup"><span data-stu-id="6944a-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="6944a-239"><a name="delete"></a>Eliminare risorse</span><span class="sxs-lookup"><span data-stu-id="6944a-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="6944a-240">Al termine di questa esercitazione, è possibile risorse hello toodelete creato nell'esercitazione di hello, in modo non si incorrere in costi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="6944a-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="6944a-241">Un gruppo di risorse anche se si elimina tutte le risorse che si trovano nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="6944a-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="6944a-242"><a name="delete-portal"></a>Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6944a-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="6944a-243">Nella casella di ricerca portale hello, immettere **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6944a-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="6944a-244">Nei risultati della ricerca hello, fare clic su **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6944a-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="6944a-245">In hello **myResourceGroup** pannello, fare clic su hello **eliminare** icona.</span><span class="sxs-lookup"><span data-stu-id="6944a-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="6944a-246">l'eliminazione di hello tooconfirm, in hello **hello di tipo nome gruppo di risorse** immettere **myResourceGroup**, quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="6944a-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="6944a-247"><a name="delete-cli"></a></span><span class="sxs-lookup"><span data-stu-id="6944a-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="6944a-248">Immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6944a-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="6944a-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="6944a-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="6944a-250">Immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6944a-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="6944a-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6944a-251">Next steps</span></span>

- <span data-ttu-id="6944a-252">Acquisire familiarità con importanti [vincoli e comportamenti del peering di rete virtuale](virtual-network-manage-peering.md#requirements-and-constraints) prima di creare un peering di rete virtuale per l'uso in produzione.</span><span class="sxs-lookup"><span data-stu-id="6944a-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="6944a-253">Acquisire informazioni più dettagliate su tutte le [impostazioni per il peering di rete virtuale](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="6944a-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="6944a-254">Informazioni su come troppo[creare un hub e spoke topologia di rete](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6944a-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
