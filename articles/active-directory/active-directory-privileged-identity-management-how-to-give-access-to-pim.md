---
title: aaaHow toogive accesso tooPrivileged Identity Management - Azure | Documenti Microsoft
description: Informazioni su come tooadd ruoli toousers con hello estensione di Azure Active Directory Privileged Identity Management in modo che possano gestire PIM.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="a43a8-103">Dando accesso toomanage Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="a43a8-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="a43a8-104">amministratore globale di Hello che abilita automaticamente Azure AD Privileged Identity Management (PIM) per un'organizzazione di ottenere le assegnazioni di ruolo e accedere tooPIM.</span><span class="sxs-lookup"><span data-stu-id="a43a8-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="a43a8-105">Per impostazione predefinita, nessun altro utente ottiene l'accesso in scrittura, inclusi gli altri amministratori globali.</span><span class="sxs-lookup"><span data-stu-id="a43a8-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="a43a8-106">Dispongono di accesso in sola lettura tooAzure PIM AD altri amministratori globali, amministratori della sicurezza e i lettori di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a43a8-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="a43a8-107">toogive tooPIM di accesso, utente prima di hello può assegnare ad altri utenti toohello **amministratore del ruolo con privilegi** ruolo.</span><span class="sxs-lookup"><span data-stu-id="a43a8-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="a43a8-108">Questa assegnazione deve essere eseguita dall'interno PIM e non può essere modificata tramite PowerShell o altri portali.</span><span class="sxs-lookup"><span data-stu-id="a43a8-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="a43a8-109">Per la gestione di Azure AD PIM è necessario Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="a43a8-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="a43a8-110">Poiché gli account Microsoft non possono effettuare la registrazione per Azure MFA, gli utenti che eseguono l'accesso con un account Microsoft non possono accedere a Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="a43a8-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="a43a8-111">Assicurarsi che almeno due utenti abbiano sempre il ruolo di amministratore dei ruoli con privilegi, per l'eventualità in cui uno di questi venga bloccato o il suo account venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="a43a8-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="a43a8-112">Assegnare un altro utente accesso toomanage PIM</span><span class="sxs-lookup"><span data-stu-id="a43a8-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="a43a8-113">Accedi toohello [portale di Azure](https://portal.azure.com/) e seleziona hello **Azure AD Privileged Identity Management** app dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="a43a8-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="a43a8-114">Selezionare **Gestione dei ruoli con privilegi** > **Amministratore dei ruoli con privilegi** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a43a8-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Schermata Aggiungi amministratori dei ruoli con privilegi][1]
3. <span data-ttu-id="a43a8-116">Nel Pannello di utenti gestiti Aggiungi hello, passaggio 1 è già stato completato.</span><span class="sxs-lookup"><span data-stu-id="a43a8-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="a43a8-117">Il passaggio 2, seleziona **selezionare utenti** e la ricerca per utente hello desiderato tooadd.</span><span class="sxs-lookup"><span data-stu-id="a43a8-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![Schermata Seleziona gli utenti][2]
4. <span data-ttu-id="a43a8-119">Selezionare l'utente hello dai risultati della ricerca hello e fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="a43a8-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="a43a8-120">Fare clic su **OK** toosave la selezione.</span><span class="sxs-lookup"><span data-stu-id="a43a8-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="a43a8-121">Hello l'utente selezionato verrà visualizzata nell'elenco di hello degli amministratori con privilegi di ruolo.</span><span class="sxs-lookup"><span data-stu-id="a43a8-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="a43a8-122">Ogni volta che si assegna un nuovo toosomeone ruolo, vengono automaticamente configurati come ruolo hello tooactivate idoneo.</span><span class="sxs-lookup"><span data-stu-id="a43a8-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="a43a8-123">Se si desidera toomake permanenti nel ruolo di hello, fare clic su utente hello nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="a43a8-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="a43a8-124">Selezionare **rendere autorizzazioni** nel menu di informazioni utente hello.</span><span class="sxs-lookup"><span data-stu-id="a43a8-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="a43a8-125">Invia hello un collegamento all'utente troppo[Introduzione a Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a43a8-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="a43a8-126">Rimuovere i diritti di accesso di un altro utente per la gestione di PIM</span><span class="sxs-lookup"><span data-stu-id="a43a8-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="a43a8-127">Prima di rimuovere un utente dal ruolo di amministratore con privilegi di ruolo hello, assicurarsi sempre che sarà ancora presente due utenti assegnati tooit.</span><span class="sxs-lookup"><span data-stu-id="a43a8-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="a43a8-128">Nel dashboard PIM hello, fare clic sul ruolo hello **amministratore del ruolo con privilegi**.</span><span class="sxs-lookup"><span data-stu-id="a43a8-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="a43a8-129">verrà visualizzato l'elenco di Hello di utenti attualmente in tale ruolo.</span><span class="sxs-lookup"><span data-stu-id="a43a8-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="a43a8-130">Fare clic sull'utente hello nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a43a8-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="a43a8-131">Fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="a43a8-131">Click on **Remove**.</span></span>  <span data-ttu-id="a43a8-132">Verrà visualizzato un messaggio di richiesta di conferma.</span><span class="sxs-lookup"><span data-stu-id="a43a8-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="a43a8-133">Fare clic su **Sì** utente hello tooremove dal ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="a43a8-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="a43a8-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a43a8-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
