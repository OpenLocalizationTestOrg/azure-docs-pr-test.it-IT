---
title: gruppi di hello aaaManage il gruppo appartiene tooin Azure Active Directory | Documenti Microsoft
description: I gruppi possono contenere altri gruppi in Azure Active Directory. Ecco come toomanage tali appartenenze.
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
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="6b2fc-104">Gestire i gruppi di toowhich che appartiene un gruppo nel tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b2fc-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="6b2fc-105">I gruppi possono contenere altri gruppi in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="6b2fc-106">Ecco come toomanage tali appartenenze.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="6b2fc-107">Ricerca di gruppi di hello di che al gruppo dell'utente è membro</span><span class="sxs-lookup"><span data-stu-id="6b2fc-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="6b2fc-108">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="6b2fc-109">Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="6b2fc-111">In hello **utenti e gruppi** pannello seleziona **tutti i gruppi di**.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Pannello gruppi hello di apertura](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="6b2fc-113">In hello **utenti e gruppi - tutti i gruppi** pannello, selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="6b2fc-114">In hello **gruppo - *groupname***  pannello seleziona **appartenenze**.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Pannello di appartenenza al gruppo di apertura hello](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="6b2fc-116">tooadd il gruppo come membro del gruppo di un altro, in hello **gruppo - appartenenze** blade, seleziona hello **Aggiungi** comando.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="6b2fc-117">Selezionare un gruppo hello **Seleziona gruppo** blade e quindi seleziona hello **selezionare** pulsante nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="6b2fc-118">È possibile aggiungere il gruppo tooonly uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="6b2fc-119">Hello **utente** filtri casella hello in base alla corrispondenza parte dell'utente tooany voce di un nome utente o un dispositivo di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="6b2fc-120">I caratteri jolly non sono consentiti nella casella.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-120">No wildcard characters are accepted in that box.</span></span>

   ![Aggiungere l'appartenenza a un gruppo](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="6b2fc-122">tooremove il gruppo come membro del gruppo di un altro, in hello **gruppo - appartenenze** pannello, selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="6b2fc-123">In hello ***groupname*** blade, seleziona hello **rimuovere** comandi e confermare la scelta al prompt dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Comando Rimuovi appartenenza](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="6b2fc-125">Al termine della modifica delle appartenenze dei gruppi per il proprio gruppo, selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="6b2fc-126">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6b2fc-126">Additional information</span></span>
<span data-ttu-id="6b2fc-127">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b2fc-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="6b2fc-128">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="6b2fc-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="6b2fc-129">Creare un nuovo gruppo e aggiunta di membri</span><span class="sxs-lookup"><span data-stu-id="6b2fc-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="6b2fc-130">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="6b2fc-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="6b2fc-131">Gestire i membri di un gruppo</span><span class="sxs-lookup"><span data-stu-id="6b2fc-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="6b2fc-132">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="6b2fc-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
