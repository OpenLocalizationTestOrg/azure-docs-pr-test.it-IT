---
title: Gestire NSG usando il portale di Azure | Documentazione Microsoft
description: Informazioni su come gestire i gruppi di sicurezza di rete esistenti usando il portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: e9bcf8a893ff209337f6a5763b631a22f8514e20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-nsgs-using-the-portal"></a><span data-ttu-id="ff860-103">Gestire gruppi di sicurezza di rete usando il portale</span><span class="sxs-lookup"><span data-stu-id="ff860-103">Manage NSGs using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff860-104">Portale</span><span class="sxs-lookup"><span data-stu-id="ff860-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="ff860-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff860-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="ff860-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ff860-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ff860-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ff860-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ff860-108">Questo articolo illustra l'uso del modello di distribuzione Resource Manager che Microsoft consiglia di usare invece del modello di distribuzione classica per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="ff860-108">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="ff860-109">Recuperare le informazioni</span><span class="sxs-lookup"><span data-stu-id="ff860-109">Retrieve Information</span></span>
<span data-ttu-id="ff860-110">È possibile visualizzare i gruppi di sicurezza di rete (NSG, Network Security Group) esistenti, recuperare le regole relative a un NSG esistente e trovare le risorse a cui un NSG è associato.</span><span class="sxs-lookup"><span data-stu-id="ff860-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="ff860-111">Visualizzare NSG esistenti</span><span class="sxs-lookup"><span data-stu-id="ff860-111">View existing NSGs</span></span>

<span data-ttu-id="ff860-112">Per visualizzare tutti gli NSG esistenti in una sottoscrizione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-112">To view all existing NSGs in a subscription, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-113">In un browser passare a http://portal.azure.com e, se necessario, accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="ff860-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="ff860-114">Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="ff860-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="ff860-116">Controllare l'elenco di NSG nel pannello **Gruppi di sicurezza di rete** .</span><span class="sxs-lookup"><span data-stu-id="ff860-116">Check the list of NSGs in the **Network security groups** blade.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="ff860-118">Visualizzare gli NSG in un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ff860-118">View NSGs in a resource group</span></span>

<span data-ttu-id="ff860-119">Per visualizzare l'elenco di NSG nel gruppo di risorse **RG-NSG** , seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-120">Fare clic su **Gruppi di risorse >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="ff860-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="ff860-122">Nell'elenco di risorse, cercare gli elementi che visualizzano l'icona NSG, come illustrato nel pannello **Risorse** riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ff860-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span></span>

    ![Portale di Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="ff860-124">Elencare tutte le regole per un NSG</span><span class="sxs-lookup"><span data-stu-id="ff860-124">List all rules for an NSG</span></span>

<span data-ttu-id="ff860-125">Per visualizzare le regole di un NSG denominato **NSG-FrontEnd**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-126">Nel pannello **Gruppi di sicurezza di rete** o nel pannello **Risorse** illustrato in precedenza fare clic su **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ff860-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="ff860-127">Nella scheda **Impostazioni** fare clic su **Regole di sicurezza in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="ff860-127">In the **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="ff860-129">Il pannello **Regole di sicurezza in ingresso** è visualizzato come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ff860-129">The **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="ff860-131">Nella scheda **Impostazioni** fare clic su **Regole di sicurezza in uscita** per visualizzare le regole in uscita.</span><span class="sxs-lookup"><span data-stu-id="ff860-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff860-132">Per visualizzare le regole predefinite, fare clic sull'icona **Regole predefinite** nella parte superiore del pannello in cui sono visualizzate le regole.</span><span class="sxs-lookup"><span data-stu-id="ff860-132">To view default rules, click the **Default rules** icon at the top of the blade that displays the rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="ff860-133">Visualizzare le associazioni di NSG</span><span class="sxs-lookup"><span data-stu-id="ff860-133">View NSGs associations</span></span>

<span data-ttu-id="ff860-134">Per visualizzare le risorse a cui l'NSG **NSG-FrontEnd** è associato, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-135">Nel pannello **Gruppi di sicurezza di rete** o nel pannello **Risorse** illustrato in precedenza fare clic su **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ff860-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="ff860-136">Nella scheda **Impostazioni** fare clic su **Subnet** per visualizzare le subnet associate all'NSG.</span><span class="sxs-lookup"><span data-stu-id="ff860-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="ff860-138">Nella scheda **Impostazioni** fare clic su **Interfacce di rete** per visualizzare le NIC associate all'NSG.</span><span class="sxs-lookup"><span data-stu-id="ff860-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="ff860-139">Gestire le regole</span><span class="sxs-lookup"><span data-stu-id="ff860-139">Manage rules</span></span>
<span data-ttu-id="ff860-140">È possibile aggiungere regole a un NSG esistente, modificare le regole esistenti e rimuovere regole.</span><span class="sxs-lookup"><span data-stu-id="ff860-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="ff860-141">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="ff860-141">Add a rule</span></span>
<span data-ttu-id="ff860-142">Per aggiungere una regola che consenta il traffico **in ingresso** alla porta **443** da qualsiasi computer all'NSG **NSG-FrontEnd**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-143">Nel pannello **Gruppi di sicurezza di rete** o nel pannello **Risorse** illustrato in precedenza fare clic su **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ff860-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="ff860-144">Nella scheda **Impostazioni** fare clic su **Regole di sicurezza in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="ff860-144">In the **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="ff860-145">Nel pannello **Regole di sicurezza in ingresso** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ff860-145">In the **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="ff860-146">Quindi, nel pannello **Aggiungi regola di sicurezza in ingresso**, inserire i valori come illustrato di seguito e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ff860-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="ff860-148">Dopo alcuni secondi, si noti la nuova regola nel pannello **Regole di sicurezza in ingresso** .</span><span class="sxs-lookup"><span data-stu-id="ff860-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span></span>

    ![Portale di Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="ff860-150">Modificare una regola</span><span class="sxs-lookup"><span data-stu-id="ff860-150">Change a rule</span></span>
<span data-ttu-id="ff860-151">Per modificare la regola creata in precedenza in modo da consentire traffico in ingresso solo da **Internet**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-152">Nel pannello **Gruppi di sicurezza di rete** o nel pannello **Risorse** illustrato in precedenza fare clic su **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ff860-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="ff860-153">Nella scheda **Impostazioni** fare clic sulla regola creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff860-153">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="ff860-154">Nel pannello **allow-https** modificare la proprietà di **origine** come illustrato di seguito e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ff860-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="ff860-156">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="ff860-156">Delete a rule</span></span>

<span data-ttu-id="ff860-157">Per eliminare la regola creata in precedenza, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-157">To delete the rule created above, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-158">Nel pannello **Gruppi di sicurezza di rete** o nel pannello **Risorse** illustrato in precedenza fare clic su **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ff860-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="ff860-159">Nella scheda **Impostazioni** fare clic sulla regola creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff860-159">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="ff860-160">Nel pannello **allow-https** fare clic su **Elimina** e quindi fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="ff860-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="ff860-162">Gestire le associazioni</span><span class="sxs-lookup"><span data-stu-id="ff860-162">Manage associations</span></span>
<span data-ttu-id="ff860-163">È possibile associare un NSG a subnet e schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="ff860-163">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="ff860-164">È anche possibile annullare l'associazione tra un NSG e qualsiasi risorsa a cui è associato.</span><span class="sxs-lookup"><span data-stu-id="ff860-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="ff860-165">Associare un NSG a una NIC</span><span class="sxs-lookup"><span data-stu-id="ff860-165">Associate an NSG to a NIC</span></span>
<span data-ttu-id="ff860-166">Per associare l'NSG **NSG-FrontEnd** alla NIC **TestNICWeb1**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-167">Nel pannello **Gruppi di sicurezza di rete** o nel pannello **Risorse** illustrato in precedenza fare clic su **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ff860-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="ff860-168">Nella scheda **Impostazioni** fare clic su **Interfacce di rete** > **Associa** > **interfacesAssociateTestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="ff860-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="ff860-170">Annullare l'associazione tra un NSG e una NIC</span><span class="sxs-lookup"><span data-stu-id="ff860-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="ff860-171">Per annullare l'associazione tra l'NSG **NSG-FrontEnd** e la NIC **TestNICWeb1**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-172">Nel portale di Azure fare clic su **Gruppi di risorse >** > **RG-NSG** > **...** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="ff860-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="ff860-173">Nel pannello **TestNICWeb1** fare clic su **Modifica sicurezza...** > **Nessuna**.</span><span class="sxs-lookup"><span data-stu-id="ff860-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="ff860-175">È inoltre possibile usare questo pannello per associare la NIC a qualsiasi NSG esistente.</span><span class="sxs-lookup"><span data-stu-id="ff860-175">You can also use this blade to associate the NIC to any existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="ff860-176">Annullare l'associazione tra un NSG e una subnet</span><span class="sxs-lookup"><span data-stu-id="ff860-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="ff860-177">Per annullare l'associazione tra l'NSG **NSG-FrontEnd** e la subnet **FrontEnd**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-178">Nel portale di Azure fare clic su **Gruppi di risorse >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="ff860-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="ff860-179">Nel pannello **Impostazioni** fare clic su **Subnet** > **FrontEnd** > **Gruppo di sicurezza di rete** > **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="ff860-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="ff860-181">Nel pannello **FrontEnd** fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ff860-181">In the **FrontEnd** blade, click **Save**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="ff860-183">Associare un gruppo di sicurezza di rete a una subnet</span><span class="sxs-lookup"><span data-stu-id="ff860-183">Associate an NSG to a subnet</span></span>

<span data-ttu-id="ff860-184">Per associare di nuovo l'NSG **NSG-FrontEnd** alla subnet **FronEnd**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="ff860-185">Nel portale di Azure fare clic su **Gruppi di risorse >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="ff860-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="ff860-186">Nel pannello **Impostazioni** fare clic su **Subnet** > **FrontEnd** > **Gruppo di sicurezza di rete** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ff860-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="ff860-187">Nel pannello **FrontEnd** fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ff860-187">In the **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="ff860-188">Per associare un NSG a una subnet è anche possibile usare il pannello **Impostazioni** dell'NSG.</span><span class="sxs-lookup"><span data-stu-id="ff860-188">You can also associate an NSG to a subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="ff860-189">Eliminare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="ff860-189">Delete an NSG</span></span>
<span data-ttu-id="ff860-190">È possibile eliminare un NSG solo se non è associato ad alcuna risorsa.</span><span class="sxs-lookup"><span data-stu-id="ff860-190">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="ff860-191">Per eliminare un NSG, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff860-191">To delete an NSG, complete the following steps:.</span></span>

1. <span data-ttu-id="ff860-192">Nel portale di Azure fare clic su **Gruppi di risorse >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ff860-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="ff860-193">Nel pannello **Impostazioni** fare clic su **Interfacce di rete**.</span><span class="sxs-lookup"><span data-stu-id="ff860-193">In the **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="ff860-194">Se sono elencate NIC, scegliere la NIC ed eseguire il passaggio 2 in [Annullare l'associazione tra un NSG e una NIC](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="ff860-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="ff860-195">Ripetere il passaggio 3 per ogni NIC.</span><span class="sxs-lookup"><span data-stu-id="ff860-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="ff860-196">Nel pannello **Impostazioni** fare clic su **Subnet**.</span><span class="sxs-lookup"><span data-stu-id="ff860-196">In the **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="ff860-197">Se sono elencate subnet, scegliere la subnet ed eseguire i passaggi 2 e 3 in [Annullare l'associazione tra un NSG e una subnet](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="ff860-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="ff860-198">Scorrere a sinistra fino al pannello**NSG-FrontEnd**, quindi fare clic su **Elimina** > **Sì**.</span><span class="sxs-lookup"><span data-stu-id="ff860-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="ff860-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff860-200">Next steps</span></span>
* <span data-ttu-id="ff860-201">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.</span><span class="sxs-lookup"><span data-stu-id="ff860-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
