---
title: 'Azure Active Directory Domain Services: Introduzione | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services tramite il portale di Azure (anteprima)
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="ed60e-103">Abilitare Azure Active Directory Domain Services tramite il portale di Azure (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="ed60e-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>
<span data-ttu-id="ed60e-104">Questo articolo illustra come abilitare Azure Active Directory Domain Services (Azure AD DS) tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed60e-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


<span data-ttu-id="ed60e-105">Per avviare la procedura guidata **Abilita Azure AD Domain Services**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ed60e-105">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="ed60e-106">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed60e-106">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ed60e-107">Nel riquadro sinistro fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="ed60e-107">In the left pane, click on **New**.</span></span>
3. <span data-ttu-id="ed60e-108">Nel pannello **Nuovo** digitare **Domain Services** nella barra di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ed60e-108">In the **New** blade, type **Domain Services** into the search bar.</span></span>

    ![Ricerca di Domain Services](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="ed60e-110">Fare clic per selezionare **Azure AD Domain Services** dall'elenco dei suggerimenti di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ed60e-110">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="ed60e-111">Nel pannello **Azure AD Domain Services** fare clic sul pulsante **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ed60e-111">On the **Azure AD Domain Services** blade, click the **Create** button.</span></span>

    ![Pannello Domain Services](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="ed60e-113">Viene avviata la procedura guidata **Abilita Azure AD Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="ed60e-113">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="ed60e-114">Attività 1: Configurare le impostazioni di base</span><span class="sxs-lookup"><span data-stu-id="ed60e-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="ed60e-115">Nella pagina **Informazioni di base** della procedura guidata è possibile specificare il nome di dominio DNS relativo al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ed60e-115">In the **Basics** page of the wizard, you can specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="ed60e-116">È possibile anche scegliere il gruppo di risorse e la località di Azure in cui deve essere distribuito il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ed60e-116">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![Configurare le informazioni di base](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="ed60e-118">Scegliere il **Nome dominio DNS** per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ed60e-118">Choose the **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="ed60e-119">Il nome di dominio predefinito della directory (con suffisso **.onmicrosoft.com**) viene specificato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ed60e-119">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="ed60e-120">È anche possibile immettere un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="ed60e-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="ed60e-121">In questo esempio, il nome di dominio personalizzato è *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="ed60e-121">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="ed60e-122">Il prefisso del nome del dominio specificato (ad esempio, *contoso100* nel nome di dominio *contoso100.com*) può contenere massimo 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="ed60e-122">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="ed60e-123">Non è possibile creare un dominio gestito con un prefisso più lungo di 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="ed60e-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="ed60e-124">Assicurarsi che il nome di dominio DNS scelto per il dominio gestito non esista già nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed60e-124">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="ed60e-125">In particolare, verificare se:</span><span class="sxs-lookup"><span data-stu-id="ed60e-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="ed60e-126">È già presente un dominio con lo stesso nome di dominio DNS nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed60e-126">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="ed60e-127">La rete virtuale in cui si intende abilitare il dominio gestito ha una connessione VPN alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="ed60e-127">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="ed60e-128">In questo caso, verificare che non sia presente un dominio con lo stesso nome di dominio DNS nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="ed60e-128">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="ed60e-129">Esiste un servizio cloud con lo stesso nome della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed60e-129">You have an existing cloud service with that name on the virtual network.</span></span>

3. <span data-ttu-id="ed60e-130">Scegliere il **tipo di rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="ed60e-130">Choose the **type of virtual network**.</span></span> <span data-ttu-id="ed60e-131">Per impostazione predefinita, viene selezionato il tipo di rete virtuale **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="ed60e-131">By default, the **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="ed60e-132">È consigliabile usare questo tipo di rete virtuale per tutti i nuovi domini gestiti creati.</span><span class="sxs-lookup"><span data-stu-id="ed60e-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="ed60e-133">Selezionare la **Sottoscrizione** di Azure in cui si vuole creare il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ed60e-133">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

5. <span data-ttu-id="ed60e-134">Selezionare il **Gruppo di risorse** a cui deve appartenere il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ed60e-134">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="ed60e-135">Quando si seleziona il gruppo di risorse, è possibile scegliere tra le opzioni **Crea nuovo** e **Usa esistente**.</span><span class="sxs-lookup"><span data-stu-id="ed60e-135">You can choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

6. <span data-ttu-id="ed60e-136">Scegliere la **Località** di Azure in cui deve essere creato il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ed60e-136">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="ed60e-137">Nella pagina **Rete** della procedura guidata vengono visualizzate solo le reti virtuali appartenenti alla località selezionata.</span><span class="sxs-lookup"><span data-stu-id="ed60e-137">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

7. <span data-ttu-id="ed60e-138">Al termine, fare clic su **OK** per passare alla pagina **Rete** della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="ed60e-138">When you are done, click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="ed60e-139">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="ed60e-139">Next step</span></span>
[<span data-ttu-id="ed60e-140">Attività 2: Configurare le impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="ed60e-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
