---
title: gruppi di sicurezza di rete aaaManage - portale di Azure | Documenti Microsoft
description: Informazioni su come gruppi di sicurezza di rete toomanage utilizzando hello portale di Azure.
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
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="3e7e3-103">Gestire i gruppi di sicurezza di rete usando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3e7e3-103">Manage network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3e7e3-104">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="3e7e3-105">È anche possibile [creare NSGs nel modello di distribuzione classica hello](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3e7e3-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="3e7e3-106">esempio Hello PowerShell comandi riportati di seguito prevedono un ambiente semplice già creato in base hello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="3e7e3-107">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare innanzitutto ambiente di test di hello distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), fare clic su **distribuire tooAzure**, sostituire i valori dei parametri predefiniti hello Se necessario e seguire le istruzioni di hello in hello portale.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="3e7e3-108">Hello passaggi sottostanti utilizzano **RG NSG** come nome hello del modello di hello gruppo di risorse hello è stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="3e7e3-109">Creare hello NSG front-end di NSG</span><span class="sxs-lookup"><span data-stu-id="3e7e3-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="3e7e3-110">hello toocreate **front-end di NSG** gruppo come illustrato nell'esempio hello di cui sopra, procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="3e7e3-111">Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3e7e3-112">Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="3e7e3-114">In hello **gruppi di sicurezza di rete** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="3e7e3-116">In hello **Crea gruppo di sicurezza di rete** pannello, creare un gruppo denominato *front-end di NSG* in hello *RG NSG* gruppo di risorse e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="3e7e3-118">Creare regole in un gruppo di sicurezza di rete esistente</span><span class="sxs-lookup"><span data-stu-id="3e7e3-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="3e7e3-119">le regole di toocreate in un gruppo esistente dal portale di Azure hello procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="3e7e3-120">Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="3e7e3-121">Selezionare nell'elenco hello di NSGs **front-end di NSG** > **regole di sicurezza in ingresso**</span><span class="sxs-lookup"><span data-stu-id="3e7e3-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portale di Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="3e7e3-123">Nell'elenco di hello di **sicurezza regole connessioni in entrata**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portale di Azure - Aggiungi regola](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="3e7e3-125">In hello **Aggiungi regola di sicurezza in ingresso** pannello, creare una regola denominata *regola web* con priorità di *200* che consente l'accesso tramite *TCP* tooport *80* tooany macchina virtuale da qualsiasi origine e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="3e7e3-126">Notare che la maggior parte di queste impostazioni ha già i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portale di Azure - Impostazioni delle regole](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="3e7e3-128">Regola di nuovo hello in hello gruppo sarà presente dopo alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Portale di Azure - Nuova regola](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="3e7e3-130">Ripetere i passaggi too6 toocreate una regola in ingresso denominata *rdp regola* con una priorità di *250* che consente l'accesso tramite *TCP* tooport *3389* tooany macchina virtuale da qualsiasi origine.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="3e7e3-131">Associare subnet front-end di hello NSG toohello</span><span class="sxs-lookup"><span data-stu-id="3e7e3-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="3e7e3-132">Fare clic su **Sfoglia >** > **Gruppi di risorse** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="3e7e3-133">In hello **RG NSG** pannello, fare clic su **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portale di Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="3e7e3-135">In hello **impostazioni** pannello, fare clic su **subnet** > **front-end** > **il gruppo di sicurezza di rete**  >  **Front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portale di Azure - Impostazioni della subnet](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="3e7e3-137">In hello **front-end** pannello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portale di Azure - Impostazioni della subnet](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="3e7e3-139">Creare hello NSG back-end di NSG</span><span class="sxs-lookup"><span data-stu-id="3e7e3-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="3e7e3-140">hello toocreate **back-end di NSG** NSG e associarlo toohello **back-end** subnet, seguire hello passaggi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="3e7e3-141">Passaggi di ripetizione hello [hello Crea gruppo di front-end di NSG](#Create-the-NSG-FrontEnd-NSG) toocreate un gruppo denominato *back-end di gruppo*</span><span class="sxs-lookup"><span data-stu-id="3e7e3-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="3e7e3-142">Passaggi di ripetizione hello [creare regole in un gruppo esistente](#Create-rules-in-an-existing-NSG) toocreate hello **in ingresso** regole riportate nella tabella hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="3e7e3-143">Regola in entrata</span><span class="sxs-lookup"><span data-stu-id="3e7e3-143">Inbound rule</span></span> | <span data-ttu-id="3e7e3-144">Regola in uscita</span><span class="sxs-lookup"><span data-stu-id="3e7e3-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portale di Azure - Regola in entrata](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portale di Azure - Regola in uscita](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="3e7e3-147">Hello ripetere i passaggi [associare subnet front-end di hello NSG toohello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **back-end di NSG** NSG toohello **back-end** subnet.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e7e3-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e7e3-148">Next Steps</span></span>
* <span data-ttu-id="3e7e3-149">Informazioni su come troppo[gestire NSGs esistente](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="3e7e3-150">[Abilitare la registrazione](virtual-network-nsg-manage-log.md) per i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

