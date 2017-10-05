---
title: Gestire i gruppi appartenenti a un gruppo in Azure Active Directory | Microsoft Docs
description: I gruppi possono contenere altri gruppi in Azure Active Directory. Di seguito viene illustrato come gestire queste appartenenze.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="860a5-104">Gestire i gruppi a cui appartiene il proprio gruppo nel tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="860a5-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="860a5-105">I gruppi possono contenere altri gruppi in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="860a5-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="860a5-106">Di seguito viene illustrato come gestire queste appartenenze.</span><span class="sxs-lookup"><span data-stu-id="860a5-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="860a5-107">Come è possibile trovare i gruppi di cui il gruppo dell'utente è un membro?</span><span class="sxs-lookup"><span data-stu-id="860a5-107">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="860a5-108">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="860a5-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="860a5-109">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="860a5-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="860a5-111">Nel pannello **Utenti e gruppi** selezionare **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="860a5-111">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Apertura del pannello Gruppi](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="860a5-113">Nel pannello **Utenti e gruppi - Tutti i gruppi** selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="860a5-113">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="860a5-114">Nel pannello **Gruppo - *nomegruppo*** selezionare **Appartenenza a gruppi**.</span><span class="sxs-lookup"><span data-stu-id="860a5-114">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Apertura del pannello Appartenenza ai gruppi](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="860a5-116">Per aggiungere il gruppo come membro di un altro gruppo, nel pannello **Gruppo - Appartenenza ai gruppi** selezionare il comando **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="860a5-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="860a5-117">Selezionare un gruppo nel pannello **Seleziona gruppo** e quindi fare clic sul pulsante **Seleziona** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="860a5-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="860a5-118">È possibile aggiungere il gruppo a un solo gruppo alla volta.</span><span class="sxs-lookup"><span data-stu-id="860a5-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="860a5-119">La visualizzazione nella casella **Utente** viene filtrata in base alla corrispondenza con l'immissione di una parte di un nome utente o di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="860a5-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="860a5-120">I caratteri jolly non sono consentiti nella casella.</span><span class="sxs-lookup"><span data-stu-id="860a5-120">No wildcard characters are accepted in that box.</span></span>

   ![Aggiungere l'appartenenza a un gruppo](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="860a5-122">Per rimuovere il proprio gruppo come membro di un altro gruppo, nel pannello **Gruppo - Appartenenza ai gruppi** selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="860a5-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="860a5-123">Nel pannello ***nomegruppo*** selezionare il comando **Rimuovi** e confermare la scelta quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="860a5-123">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Comando Rimuovi appartenenza](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="860a5-125">Al termine della modifica delle appartenenze dei gruppi per il proprio gruppo, selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="860a5-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="860a5-126">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="860a5-126">Additional information</span></span>
<span data-ttu-id="860a5-127">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="860a5-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="860a5-128">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="860a5-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="860a5-129">Creare un nuovo gruppo e aggiunta di membri</span><span class="sxs-lookup"><span data-stu-id="860a5-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="860a5-130">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="860a5-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="860a5-131">Gestire i membri di un gruppo</span><span class="sxs-lookup"><span data-stu-id="860a5-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="860a5-132">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="860a5-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
