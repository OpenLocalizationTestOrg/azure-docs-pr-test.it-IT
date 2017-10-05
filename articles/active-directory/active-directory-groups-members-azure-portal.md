---
title: Gestire i membri per un gruppo in Azure Active Directory | Microsoft Docs
description: 'Procedura: Aggiungere o rimuovere gli utenti e i dispositivi da un gruppo in Azure Active Directory'
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="bf541-103">Gestire l'appartenenza al gruppo per gli utenti nel tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf541-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="bf541-104">Questo articolo descrive come gestire i membri di un gruppo in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf541-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="bf541-105">Come è possibile trovare i membri e gestirli?</span><span class="sxs-lookup"><span data-stu-id="bf541-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="bf541-106">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="bf541-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="bf541-107">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="bf541-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="bf541-109">Nel pannello **Utenti e gruppi** selezionare **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bf541-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Apertura del pannello Gruppi](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="bf541-111">Nel pannello **Utenti e gruppi - Tutti i gruppi** selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="bf541-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="bf541-112">Nel pannello **Gruppo - *nomegruppo*** selezionare **Membri**.</span><span class="sxs-lookup"><span data-stu-id="bf541-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Apertura del pannello Membri](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="bf541-114">Per aggiungere membri al gruppo, nel pannello **Gruppo - Membri** selezionare **Aggiungi membri**.</span><span class="sxs-lookup"><span data-stu-id="bf541-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Comando Aggiungi membri](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="bf541-116">Nel pannello **Membri** selezionare uno o più utenti o dispositivi da aggiungere al gruppo e fare clic sul pulsante **Seleziona** nella parte inferiore del pannello per aggiungerli al gruppo.</span><span class="sxs-lookup"><span data-stu-id="bf541-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="bf541-117">La visualizzazione nella casella **Utente** viene filtrata in base alla corrispondenza con l'immissione di una parte di un nome utente o di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bf541-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="bf541-118">I caratteri jolly non sono consentiti nella casella.</span><span class="sxs-lookup"><span data-stu-id="bf541-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="bf541-119">Per rimuovere membri dal gruppo, nel pannello **Gruppo - Membri** selezionare un membro.</span><span class="sxs-lookup"><span data-stu-id="bf541-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="bf541-120">Nel pannello ***nome membro*** selezionare il comando **Rimuovi** e confermare la scelta quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="bf541-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Comando Rimuovi membri](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="bf541-122">Al termine della modifica dei membri per il gruppo, selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bf541-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="bf541-123">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bf541-123">Additional information</span></span>
<span data-ttu-id="bf541-124">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf541-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="bf541-125">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="bf541-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="bf541-126">Creare un nuovo gruppo e aggiunta di membri</span><span class="sxs-lookup"><span data-stu-id="bf541-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="bf541-127">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="bf541-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="bf541-128">Gestire le appartenenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="bf541-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="bf541-129">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="bf541-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
