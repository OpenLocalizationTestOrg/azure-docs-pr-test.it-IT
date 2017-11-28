---
title: un'app aziendale tooan utente o gruppo in Azure Active Directory aaaAssign | Documenti Microsoft
description: Come tooselect un tooassign app enterprise un utente o gruppo tooit in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="d91bc-103">Assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d91bc-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="d91bc-104">È facile tooassign un utente o un gruppo tooyour enterprise in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d91bc-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d91bc-105">È necessario hello delle autorizzazioni appropriate toomanage hello enterprise app, che è necessario essere amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="d91bc-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="d91bc-106">Come assegnare utente accesso tooan enterprise app?</span><span class="sxs-lookup"><span data-stu-id="d91bc-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="d91bc-107">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="d91bc-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="d91bc-108">Selezionare **più servizi**, immettere Azure Active Directory nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="d91bc-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="d91bc-109">In hello **Azure Active Directory - *nomedirectory***  blade (vale a dire hello Azure AD pannello per directory hello gestiti), selezionare **applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d91bc-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura di app aziendali](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="d91bc-111">In hello **applicazioni aziendali** pannello seleziona **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d91bc-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="d91bc-112">Verrà visualizzato un elenco di App hello che è possibile gestire.</span><span class="sxs-lookup"><span data-stu-id="d91bc-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="d91bc-113">In hello **applicazioni aziendali - tutte le applicazioni** pannello, selezionare un'app.</span><span class="sxs-lookup"><span data-stu-id="d91bc-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="d91bc-114">In hello ***appname*** blade (vale a dire hello pannello con il nome di hello di hello app selezionata nel titolo hello), selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d91bc-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Selezione di hello tutti i comandi di applicazioni](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="d91bc-116">In hello ***appname*** **-assegnazione al gruppo & utente** blade, seleziona hello **Aggiungi** comando.</span><span class="sxs-lookup"><span data-stu-id="d91bc-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="d91bc-117">In hello **Aggiungi** pannello seleziona **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d91bc-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Assegnare un'app toohello utente o gruppo](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="d91bc-119">In hello **utenti e gruppi** pannello, selezionare uno o più utenti o gruppi da hello elenco e quindi selezionare hello **selezionare** pulsante nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="d91bc-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="d91bc-120">In hello **Aggiungi** pannello seleziona **ruolo**.</span><span class="sxs-lookup"><span data-stu-id="d91bc-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="d91bc-121">Quindi, nella hello **selezionare il ruolo** blade, selezionare un toohello tooapply ruolo selezionato di utenti o gruppi e quindi selezionare hello **OK** pulsante nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="d91bc-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="d91bc-122">In hello **Aggiungi** blade, seleziona hello **assegnare** pulsante nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="d91bc-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="d91bc-123">Hello assegnato agli utenti o gruppi disporranno delle autorizzazioni di hello definite dal hello ruolo selezionato per questa applicazione enterprise.</span><span class="sxs-lookup"><span data-stu-id="d91bc-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d91bc-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d91bc-124">Next steps</span></span>
* [<span data-ttu-id="d91bc-125">Visualizzare tutti i gruppi personali</span><span class="sxs-lookup"><span data-stu-id="d91bc-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d91bc-126">Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="d91bc-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="d91bc-127">Disabilitare l'accesso degli utenti per un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="d91bc-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="d91bc-128">Modificare il nome di hello o logo di un'applicazione aziendale</span><span class="sxs-lookup"><span data-stu-id="d91bc-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
