---
title: 'Azure Active Directory Domain Services: Introduzione | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)
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
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="b5bc4-103">Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="b5bc4-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="b5bc4-104">Questo articolo illustra come tooenable Azure Active Directory servizi di dominio (Azure AD DS) tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="b5bc4-105">hello toolaunch **servizi di dominio Active Directory di Azure attiva** hello procedura guidata, completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b5bc4-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="b5bc4-106">Passare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5bc4-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5bc4-107">Nel riquadro di sinistra hello, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="b5bc4-108">In hello **New** blade, tipo **servizi di dominio** nella barra di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Ricerca di Domain Services](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="b5bc4-110">Fare clic su tooselect **servizi di dominio Active Directory di Azure** elenco hello dei suggerimenti di ricerca.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="b5bc4-111">In hello **servizi di dominio Active Directory di Azure** pannello, fare clic su hello **crea** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Pannello Domain Services](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="b5bc4-113">Hello **servizi di dominio Active Directory di Azure attiva** procedura guidata viene avviata.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="b5bc4-114">Attività 1: Configurare le impostazioni di base</span><span class="sxs-lookup"><span data-stu-id="b5bc4-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="b5bc4-115">In hello **nozioni di base** pagina della procedura guidata hello, è possibile specificare nome di dominio DNS hello per il dominio gestito hello.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="b5bc4-116">È anche possibile scegliere il gruppo di risorse hello e dominio gestito di Azure percorso toowhich hello deve essere distribuito.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![Configurare le informazioni di base](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="b5bc4-118">Scegliere hello **nome di dominio DNS** per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="b5bc4-119">nome di dominio Hello predefinito della directory hello (con un **. c o m** suffisso) viene specificato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="b5bc4-120">È anche possibile immettere un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="b5bc4-121">In questo esempio, è il nome di dominio personalizzato hello *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="b5bc4-122">prefisso Hello del nome del dominio specificato (ad esempio, *contoso100* in hello *contoso100.com* nome di dominio) deve contenere meno di 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="b5bc4-123">Non è possibile creare un dominio gestito con un prefisso più lungo di 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="b5bc4-124">Verificare il nome di dominio DNS hello che scelto per hello gestito dominio non esiste già nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="b5bc4-125">In particolare, verificare se:</span><span class="sxs-lookup"><span data-stu-id="b5bc4-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="b5bc4-126">Si dispone già di un dominio con hello stesso nome di dominio DNS nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="b5bc4-127">rete virtuale di Hello in cui si prevede di dominio gestiti di hello tooenable stabilita una connessione VPN alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="b5bc4-128">In questo scenario, verificare che non si dispone di un dominio con hello stesso nome di dominio DNS nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="b5bc4-129">È un servizio cloud esistente con lo stesso nome nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="b5bc4-130">Scegliere hello **tipo di rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="b5bc4-131">Per impostazione predefinita, hello **Gestione risorse** viene selezionato il tipo di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="b5bc4-132">È consigliabile usare questo tipo di rete virtuale per tutti i nuovi domini gestiti creati.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="b5bc4-133">Seleziona hello Azure **sottoscrizione** nel quale si desidera toocreate hello gestito dominio.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="b5bc4-134">Seleziona hello **gruppo di risorse** toowhich hello gestito dominio deve appartenere.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="b5bc4-135">È possibile scegliere entrambi hello **Crea nuovo** o **utilizzare esistente** gruppo di risorse hello tooselect opzioni.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="b5bc4-136">Scegliere hello Azure **percorso** in cui hello deve essere creato un dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="b5bc4-137">In hello **rete** pagina della procedura guidata hello, vedrai le reti virtuali solo appartenenti toohello percorso selezionato.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="b5bc4-138">Al termine, fare clic su **OK** toomove su toohello **rete** pagina della procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="b5bc4-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="b5bc4-139">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="b5bc4-139">Next step</span></span>
[<span data-ttu-id="b5bc4-140">Attività 2: Configurare le impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="b5bc4-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
