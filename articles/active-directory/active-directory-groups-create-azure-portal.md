---
title: un gruppo di utenti in Azure Active Directory aaaCreate | Documenti Microsoft
description: Come toocreate un gruppo in Azure Active Directory e aggiungere membri toohello gruppo
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="81ecc-103">Creare un gruppo e aggiungere membri in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81ecc-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81ecc-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="81ecc-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="81ecc-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="81ecc-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="81ecc-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81ecc-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="81ecc-107">Questo articolo viene illustrato come toocreate e popolare un nuovo gruppo in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="81ecc-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="81ecc-108">Utilizzare un'attività di gestione gruppo tooperform, ad esempio l'assegnazione di licenze o autorizzazioni tooa numero di utenti o dispositivi in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="81ecc-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="81ecc-109">Come si crea un gruppo?</span><span class="sxs-lookup"><span data-stu-id="81ecc-109">How do I create a group?</span></span>
1. <span data-ttu-id="81ecc-110">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="81ecc-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="81ecc-111">Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="81ecc-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="81ecc-113">In hello **utenti e gruppi** pannello seleziona **tutti i gruppi di**.</span><span class="sxs-lookup"><span data-stu-id="81ecc-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Pannello gruppi hello di apertura](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="81ecc-115">In hello **utenti e gruppi - tutti i gruppi di** blade, seleziona hello **Aggiungi** comando.</span><span class="sxs-lookup"><span data-stu-id="81ecc-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![Comando Aggiungi hello](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="81ecc-117">In hello **gruppo** pannello, aggiungere un nome e una descrizione per il gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="81ecc-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="81ecc-118">tooselect tooadd toohello gruppo membri, seleziona **assegnato** in hello **tipo di appartenenza** e quindi selezionare **membri**.</span><span class="sxs-lookup"><span data-stu-id="81ecc-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="81ecc-119">Per ulteriori informazioni su come toomanage hello appartenenza di un gruppo in modo dinamico, vedere [utilizzando attributi toocreate regole per l'appartenenza al gruppo avanzate](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="81ecc-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Selezione di membri tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="81ecc-121">In hello **membri** pannello, selezionare uno o più utenti o dispositivi gruppo toohello tooadd e seleziona hello **selezionare** pulsante nella parte inferiore di hello di hello pannello tooadd li toohello gruppo.</span><span class="sxs-lookup"><span data-stu-id="81ecc-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="81ecc-122">Hello **utente** filtri casella hello in base alla corrispondenza parte dell'utente tooany voce di un nome utente o un dispositivo di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="81ecc-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="81ecc-123">I caratteri jolly non sono consentiti nella casella.</span><span class="sxs-lookup"><span data-stu-id="81ecc-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="81ecc-124">Al termine dell'aggiunta di membri toohello gruppo, selezionare **crea** su hello **gruppo** blade.</span><span class="sxs-lookup"><span data-stu-id="81ecc-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Creare una conferma del gruppo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="81ecc-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81ecc-126">Next steps</span></span>
<span data-ttu-id="81ecc-127">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="81ecc-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="81ecc-128">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="81ecc-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="81ecc-129">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="81ecc-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="81ecc-130">Gestire i membri di un gruppo</span><span class="sxs-lookup"><span data-stu-id="81ecc-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="81ecc-131">Gestire le appartenenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="81ecc-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="81ecc-132">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="81ecc-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
