---
title: assegnazione di un utente o gruppo da un'applicazione aziendale in Azure Active Directory aaaRemove | Documenti Microsoft
description: "Modalità hello tooremove assegnazione di un utente o gruppo di accesso da un'applicazione aziendale in Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="3b038-103">Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b038-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="3b038-104">È facile tooremove un utente o un gruppo viene assegnato l'accesso tooone delle applicazioni dell'organizzazione in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3b038-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3b038-105">È necessario hello delle autorizzazioni appropriate toomanage hello enterprise app, che è necessario essere amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="3b038-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="3b038-106">Come è possibile rimuovere l'assegnazione di un utente o un gruppo?</span><span class="sxs-lookup"><span data-stu-id="3b038-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="3b038-107">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="3b038-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="3b038-108">Selezionare **più servizi**, immettere **Azure Active Directory** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="3b038-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="3b038-109">In hello **Azure Active Directory - *nomedirectory***  blade (vale a dire hello Azure AD pannello per directory hello gestiti), selezionare **applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3b038-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura di app aziendali](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="3b038-111">In hello **applicazioni aziendali** pannello seleziona **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3b038-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="3b038-112">Verrà visualizzato un elenco di App hello che è possibile gestire.</span><span class="sxs-lookup"><span data-stu-id="3b038-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="3b038-113">In hello **applicazioni aziendali - tutte le applicazioni** pannello, selezionare un'app.</span><span class="sxs-lookup"><span data-stu-id="3b038-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="3b038-114">In hello ***appname*** blade (vale a dire hello pannello con il nome di hello di hello app selezionata nel titolo hello), selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3b038-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Selezione di utenti o gruppi](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="3b038-116">In hello ***appname*** **-assegnazione al gruppo & utente** pannello, selezionare uno degli altri utenti o gruppi e quindi selezionare hello **rimuovere** comando.</span><span class="sxs-lookup"><span data-stu-id="3b038-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="3b038-117">Confermare la decisione al prompt dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="3b038-117">Confirm your decision at hello prompt.</span></span>

    ![Comando Remove hello](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="3b038-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b038-119">Next steps</span></span>
* [<span data-ttu-id="3b038-120">Visualizzare tutti i gruppi personali</span><span class="sxs-lookup"><span data-stu-id="3b038-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="3b038-121">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="3b038-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="3b038-122">Disabilitare l'accesso degli utenti per un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="3b038-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="3b038-123">Modificare il nome di hello o logo di un'applicazione aziendale</span><span class="sxs-lookup"><span data-stu-id="3b038-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
