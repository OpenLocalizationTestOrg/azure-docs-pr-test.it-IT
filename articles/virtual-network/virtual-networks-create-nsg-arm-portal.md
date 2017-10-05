---
title: Gestire i gruppi di sicurezza di rete - Portale di Azure | Documentazione Microsoft
description: Informazioni su come gestire i gruppi di sicurezza di rete mediante il portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ecb4fb4608628f5a1bd54fac6af19fecfa4508f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="33868-103">Gestire i gruppi di sicurezza di rete mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="33868-103">Manage network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="33868-104">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="33868-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="33868-105">È anche possibile creare gruppi di sicurezza di rete con il [modello di distribuzione classica](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="33868-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="33868-106">I comandi di esempio PowerShell riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="33868-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="33868-107">Se si desidera eseguire i comandi così come sono visualizzati in questo documento, creare innanzitutto l'ambiente di test distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), fare clic su **Distribuisci in Azure**, sostituire i valori di parametro predefiniti, se necessario e seguire le istruzioni nel portale.</span><span class="sxs-lookup"><span data-stu-id="33868-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="33868-108">La procedura seguente usa **RG-NSG** come nome del gruppo di risorse in cui è stato distribuito il modello.</span><span class="sxs-lookup"><span data-stu-id="33868-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="33868-109">Creare il gruppo di sicurezza di rete NSG-FrontEnd</span><span class="sxs-lookup"><span data-stu-id="33868-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="33868-110">Per creare il gruppo di sicurezza di rete (NSG, Network Security Group) **NSG-FrontEnd** come illustrato nello scenario precedente, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="33868-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="33868-111">In un browser passare a http://portal.azure.com e, se necessario, accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="33868-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="33868-112">Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="33868-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="33868-114">Nel pannello **Gruppi di sicurezza di rete** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="33868-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="33868-116">Nel pannello **Crea gruppo di sicurezza di rete** creare un gruppo denominato *NSG-FrontEnd* nel gruppo di risorse *RG-NSG*, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="33868-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="33868-118">Creare regole in un gruppo di sicurezza di rete esistente</span><span class="sxs-lookup"><span data-stu-id="33868-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="33868-119">Per creare regole in un gruppo di sicurezza di rete esistente dal portale di Azure, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="33868-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="33868-120">Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="33868-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="33868-121">Nell'elenco dei gruppi di sicurezza di rete, fare clic su **NSG-FrontEnd** > **Regole di sicurezza in ingresso**</span><span class="sxs-lookup"><span data-stu-id="33868-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portale di Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="33868-123">Nell'elenco delle **Regole di sicurezza in ingresso**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="33868-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portale di Azure - Aggiungi regola](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="33868-125">Nel pannello **Aggiungi regola di sicurezza in ingresso** creare una regola denominata *web-rule* con priorità *200* che consente l'accesso tramite *TCP* alla porta *80* a qualsiasi VM da qualsiasi origine, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="33868-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="33868-126">Notare che la maggior parte di queste impostazioni ha già i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="33868-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portale di Azure - Impostazioni delle regole](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="33868-128">La nuova regola del gruppo di sicurezza di rete verrà visualizzata dopo pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="33868-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Portale di Azure - Nuova regola](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="33868-130">Ripetere i passaggi fino al 6 per creare una regola in entrata denominata *rdp-rule* con priorità *250*, che consente l'accesso tramite *TCP* alla porta *3389* per qualsiasi VM da qualsiasi origine.</span><span class="sxs-lookup"><span data-stu-id="33868-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="33868-131">Associare il gruppo di sicurezza di rete alla subnet FrontEnd</span><span class="sxs-lookup"><span data-stu-id="33868-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="33868-132">Fare clic su **Sfoglia >** > **Gruppi di risorse** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="33868-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="33868-133">Nel pannello **RG-NSG** fare clic su **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="33868-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portale di Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="33868-135">Nel pannello **Impostazioni** fare clic su **Subnet** > **FrontEnd** > **Gruppo di sicurezza di rete** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="33868-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portale di Azure - Impostazioni della subnet](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="33868-137">Nel pannello **FrontEnd** fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="33868-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portale di Azure - Impostazioni della subnet](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="33868-139">Creare il gruppo di sicurezza di rete NSG-BackEnd</span><span class="sxs-lookup"><span data-stu-id="33868-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="33868-140">Per creare il gruppo di sicurezza di rete **NSG-BackEnd** e associarlo alla subnet **BackEnd**, seguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="33868-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="33868-141">Ripetere la procedura illustrata in [Creare il gruppo di sicurezza di rete NSG-FrontEnd](#Create-the-NSG-FrontEnd-NSG) per creare un NSG denominato *NSG-BackEnd*</span><span class="sxs-lookup"><span data-stu-id="33868-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="33868-142">Ripetere la procedura illustrata [Creare regole in un gruppo di sicurezza di rete esistente](#Create-rules-in-an-existing-NSG) per creare le regole **in entrata** nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="33868-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="33868-143">Regola in entrata</span><span class="sxs-lookup"><span data-stu-id="33868-143">Inbound rule</span></span> | <span data-ttu-id="33868-144">Regola in uscita</span><span class="sxs-lookup"><span data-stu-id="33868-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portale di Azure - Regola in entrata](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portale di Azure - Regola in uscita](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="33868-147">Ripetere la procedura illustrata in [Associare il gruppo di sicurezza di rete alla subnet FrontEnd](#Associate-the-NSG-to-the-FrontEnd-subnet) per associare il gruppo di sicurezza di rete **NSG-Backend** alla subnet **BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="33868-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33868-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33868-148">Next Steps</span></span>
* <span data-ttu-id="33868-149">Informazioni su come [gestire i gruppi di sicurezza esistenti](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="33868-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="33868-150">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="33868-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

