---
title: NSGs aaaManage utilizzando hello portale di Azure | Documenti Microsoft
description: Informazioni su come toomanage NSGs utilizzando hello portale di Azure esistente.
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
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="e29bb-103">Gestire tramite il portale di hello NSGs</span><span class="sxs-lookup"><span data-stu-id="e29bb-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e29bb-104">Portale</span><span class="sxs-lookup"><span data-stu-id="e29bb-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="e29bb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e29bb-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="e29bb-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e29bb-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="e29bb-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e29bb-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e29bb-108">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="e29bb-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="e29bb-109">Recuperare le informazioni</span><span class="sxs-lookup"><span data-stu-id="e29bb-109">Retrieve Information</span></span>
<span data-ttu-id="e29bb-110">È possibile visualizzare i gruppi di sicurezza di rete (NSG, Network Security Group) esistenti, recuperare le regole relative a un NSG esistente e trovare le risorse a cui un NSG è associato.</span><span class="sxs-lookup"><span data-stu-id="e29bb-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="e29bb-111">Visualizzare NSG esistenti</span><span class="sxs-lookup"><span data-stu-id="e29bb-111">View existing NSGs</span></span>

<span data-ttu-id="e29bb-112">tooview tutti esistente NSGs in una sottoscrizione, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-113">Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="e29bb-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="e29bb-114">Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="e29bb-116">Controllare l'elenco hello di NSGs hello **gruppi di sicurezza di rete** blade.</span><span class="sxs-lookup"><span data-stu-id="e29bb-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="e29bb-118">Visualizzare gli NSG in un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="e29bb-118">View NSGs in a resource group</span></span>

<span data-ttu-id="e29bb-119">elenco di hello tooview di NSGs in hello **RG NSG** gruppo di risorse, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-120">Fare clic su **Gruppi di risorse >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="e29bb-122">Nell'elenco di hello delle risorse, cercare gli elementi la visualizzazione dell'icona NSG hello, come illustrato nell'hello **risorse** blade riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="e29bb-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="e29bb-124">Elencare tutte le regole per un NSG</span><span class="sxs-lookup"><span data-stu-id="e29bb-124">List all rules for an NSG</span></span>

<span data-ttu-id="e29bb-125">le regole di hello tooview di un gruppo denominato **front-end di NSG**completa hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e29bb-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-126">Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="e29bb-127">In hello **impostazioni** scheda, fare clic su **sicurezza regole connessioni in entrata**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="e29bb-129">Hello **sicurezza regole connessioni in entrata** pannello viene visualizzato come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e29bb-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="e29bb-131">In hello **impostazioni** scheda, fare clic su **regole di sicurezza in uscita** toosee hello regole in uscita.</span><span class="sxs-lookup"><span data-stu-id="e29bb-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e29bb-132">tooview regole predefinite, fare clic su hello **regole predefinite** sull'icona nella parte superiore di hello del pannello hello che visualizza le regole di hello.</span><span class="sxs-lookup"><span data-stu-id="e29bb-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="e29bb-133">Visualizzare le associazioni di NSG</span><span class="sxs-lookup"><span data-stu-id="e29bb-133">View NSGs associations</span></span>

<span data-ttu-id="e29bb-134">tooview hello quali risorse **front-end di NSG** NSG è hello completo, associato alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-135">Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="e29bb-136">In hello **impostazioni** scheda, fare clic su **subnet** tooview sono le subnet associata toohello gruppo.</span><span class="sxs-lookup"><span data-stu-id="e29bb-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="e29bb-138">In hello **impostazioni** scheda, fare clic su **interfacce di rete** tooview quali schede di rete sono associate toohello gruppo.</span><span class="sxs-lookup"><span data-stu-id="e29bb-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="e29bb-139">Gestire le regole</span><span class="sxs-lookup"><span data-stu-id="e29bb-139">Manage rules</span></span>
<span data-ttu-id="e29bb-140">È possibile aggiungere regole tooan gruppo esistente, modificare le regole esistenti e rimuovere le regole.</span><span class="sxs-lookup"><span data-stu-id="e29bb-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="e29bb-141">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="e29bb-141">Add a rule</span></span>
<span data-ttu-id="e29bb-142">tooadd una regola che concede **in ingresso** traffico tooport **443** da qualsiasi toohello macchina **front-end di NSG** NSG, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-143">Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e29bb-144">In hello **impostazioni** scheda, fare clic su **sicurezza regole connessioni in entrata**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="e29bb-145">In hello **sicurezza regole connessioni in entrata** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="e29bb-146">Quindi, nel hello **Aggiungi regola di sicurezza in ingresso** pannello riempire i valori hello, come illustrato di seguito e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="e29bb-148">Dopo alcuni secondi, si noti nuova regola di hello in hello **sicurezza regole connessioni in entrata** blade.</span><span class="sxs-lookup"><span data-stu-id="e29bb-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="e29bb-150">Modificare una regola</span><span class="sxs-lookup"><span data-stu-id="e29bb-150">Change a rule</span></span>
<span data-ttu-id="e29bb-151">regola di hello toochange creato in precedenza tooallow il traffico da hello in ingresso **Internet** hello completo, solo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-152">Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e29bb-153">In hello **impostazioni** , fare clic sulla regola hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e29bb-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="e29bb-154">In hello **https consentire** blade, hello modifica **origine** proprietà come illustrato di seguito e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="e29bb-156">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="e29bb-156">Delete a rule</span></span>

<span data-ttu-id="e29bb-157">toodelete hello regola creata in precedenza, completo hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-158">Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e29bb-159">In hello **impostazioni** , fare clic sulla regola hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e29bb-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="e29bb-160">In hello **https consentire** pannello, fare clic su **eliminare**, quindi fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="e29bb-162">Gestire le associazioni</span><span class="sxs-lookup"><span data-stu-id="e29bb-162">Manage associations</span></span>
<span data-ttu-id="e29bb-163">È possibile associare un gruppo toosubnets e schede di rete.</span><span class="sxs-lookup"><span data-stu-id="e29bb-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="e29bb-164">È anche possibile annullare l'associazione tra un NSG e qualsiasi risorsa a cui è associato.</span><span class="sxs-lookup"><span data-stu-id="e29bb-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="e29bb-165">Associare un tooa gruppo NIC</span><span class="sxs-lookup"><span data-stu-id="e29bb-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="e29bb-166">hello tooassociate **front-end di NSG** NSG toohello **TestNICWeb1** NIC, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-167">Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e29bb-168">In hello **impostazioni** scheda, fare clic su **interfacce di rete** > **associare** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="e29bb-170">Annullare l'associazione tra un NSG e una NIC</span><span class="sxs-lookup"><span data-stu-id="e29bb-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="e29bb-171">hello toodissociate **front-end di NSG** NSG da hello **TestNICWeb1** NIC, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-172">Dal portale di Azure hello, fare clic su **gruppi di risorse >** > **RG NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="e29bb-173">In hello **TestNICWeb1** pannello, fare clic su **modificare la sicurezza...**   >  **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="e29bb-175">Inoltre, è possibile utilizzare questo tooany NIC di blade tooassociate hello gruppo esistente.</span><span class="sxs-lookup"><span data-stu-id="e29bb-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="e29bb-176">Annullare l'associazione tra un NSG e una subnet</span><span class="sxs-lookup"><span data-stu-id="e29bb-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="e29bb-177">hello toodissociate **front-end di NSG** NSG da hello **front-end** subnet, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-178">Dal portale di Azure hello, fare clic su **gruppi di risorse >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="e29bb-179">In hello **impostazioni** pannello, fare clic su **subnet** > **front-end** > **il gruppo di sicurezza di rete**  >  **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="e29bb-181">In hello **front-end** pannello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="e29bb-183">Associare una subnet tooa NSG</span><span class="sxs-lookup"><span data-stu-id="e29bb-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="e29bb-184">hello tooassociate **front-end di NSG** NSG toohello **FronEnd** subnet nuovamente, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e29bb-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="e29bb-185">Dal portale di Azure hello, fare clic su **gruppi di risorse >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="e29bb-186">In hello **impostazioni** pannello, fare clic su **subnet** > **front-end** > **il gruppo di sicurezza di rete**  >  **Front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="e29bb-187">In hello **front-end** pannello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="e29bb-188">È inoltre possibile associare una subnet tooa NSG da thh NSG **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="e29bb-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="e29bb-189">Eliminare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e29bb-189">Delete an NSG</span></span>
<span data-ttu-id="e29bb-190">È possibile eliminare un gruppo solo se non è associata la risorsa tooany.</span><span class="sxs-lookup"><span data-stu-id="e29bb-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="e29bb-191">toodelete un gruppo, hello completo alla procedura seguente:.</span><span class="sxs-lookup"><span data-stu-id="e29bb-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="e29bb-192">Dal portale di Azure hello, fare clic su **gruppi di risorse >** > **RG NSG** > **...**   >  **Front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e29bb-193">In hello **impostazioni** pannello, fare clic su **interfacce di rete**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="e29bb-194">Se sono presenti eventuali schede di rete elencate, fare clic su hello NIC e seguire i passaggi 2 nel [annullare l'associazione di un gruppo da una scheda di rete](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="e29bb-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="e29bb-195">Ripetere il passaggio 3 per ogni NIC.</span><span class="sxs-lookup"><span data-stu-id="e29bb-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="e29bb-196">In hello **impostazioni** pannello, fare clic su **subnet**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="e29bb-197">Se sono presenti subnet elencati, fare clic su subnet hello e seguire i passaggi 2 e 3 in [annullare l'associazione di un gruppo da una subnet](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="e29bb-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="e29bb-198">Scorre verso sinistra toohello **front-end di NSG** pannello, quindi fare clic su **eliminare** > **Sì**.</span><span class="sxs-lookup"><span data-stu-id="e29bb-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="e29bb-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e29bb-200">Next steps</span></span>
* <span data-ttu-id="e29bb-201">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.</span><span class="sxs-lookup"><span data-stu-id="e29bb-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
