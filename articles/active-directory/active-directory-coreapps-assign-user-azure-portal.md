---
title: Assegnare un utente o un gruppo a un'app aziendale in Azure Active Directory | Microsoft Docs
description: Come selezionare un'app aziendale a cui assegnare un utente o gruppo in anteprima di Azure Active Directory
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
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="4cd72-103">Assegnare un utente o un gruppo a un'app aziendale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4cd72-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="4cd72-104">Assegnare un utente o un gruppo alle applicazioni aziendali in Azure Active Directory (Azure AD) è un'operazione facile.</span><span class="sxs-lookup"><span data-stu-id="4cd72-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="4cd72-105">È necessario disporre delle autorizzazioni appropriate per gestire l'app aziendale ed essere amministratore globale della directory.</span><span class="sxs-lookup"><span data-stu-id="4cd72-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="4cd72-106">Come si assegna l'accesso utente a un'app aziendale?</span><span class="sxs-lookup"><span data-stu-id="4cd72-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="4cd72-107">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="4cd72-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="4cd72-108">Selezionare **Altri servizi**, immettere Azure Active Directory nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="4cd72-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="4cd72-109">Nel pannello **Azure Active Directory - *nomedirectory*** vale a dire il pannello Azure AD per la directory che si sta gestendo, selezionare **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4cd72-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura di app aziendali](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="4cd72-111">Nel pannello **Applicazioni aziendali** selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4cd72-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="4cd72-112">Verrà visualizzato un elenco di app che è possibile gestire.</span><span class="sxs-lookup"><span data-stu-id="4cd72-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="4cd72-113">Nel pannello **Applicazioni aziendali - All applications** (Tutte le applicazioni) selezionare un'app.</span><span class="sxs-lookup"><span data-stu-id="4cd72-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="4cd72-114">Nel pannello ***nome app***, ovvero il pannello con il nome dell'app selezionata nel titolo, selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4cd72-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Selezione del comando All applications (Tutte le applicazioni)](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="4cd72-116">Nel pannello ***nome app*** **- Assegnazione di utenti e gruppi** selezionare il comando **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4cd72-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="4cd72-117">Nel pannello **Aggiungi assegnazione** selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4cd72-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Assegnare un utente o gruppo all'app](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="4cd72-119">Nel pannello **Utenti e gruppi** selezionare uno o più utenti o gruppi dall'elenco e fare clic sul pulsante **Seleziona** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="4cd72-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="4cd72-120">Nel pannello **Aggiungi assegnazione** selezionare **Ruolo**.</span><span class="sxs-lookup"><span data-stu-id="4cd72-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="4cd72-121">Nel pannello **Selezionare un ruolo** scegliere il ruolo da applicare ai gruppi o utenti selezionati, quindi fare clic su **OK** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="4cd72-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="4cd72-122">Nella parte inferiore del pannello **Aggiungi assegnazione** fare clic sul pulsante **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="4cd72-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="4cd72-123">Gli utenti o i gruppi assegnati avranno le autorizzazioni definite dal ruolo selezionato per questa app aziendale.</span><span class="sxs-lookup"><span data-stu-id="4cd72-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cd72-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4cd72-124">Next steps</span></span>
* [<span data-ttu-id="4cd72-125">Visualizzare tutti i gruppi personali</span><span class="sxs-lookup"><span data-stu-id="4cd72-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="4cd72-126">Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="4cd72-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="4cd72-127">Disabilitare l'accesso degli utenti per un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="4cd72-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="4cd72-128">Modificare il nome o il logo di un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="4cd72-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
