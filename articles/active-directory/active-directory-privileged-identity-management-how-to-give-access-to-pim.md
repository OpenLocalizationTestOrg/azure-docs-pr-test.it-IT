---
title: Come concedere l'accesso per la gestione di Privileged Identity Management - Azure | Documentazione Microsoft
description: Informazioni su come aggiungere ruoli agli utenti con l'estensione Azure Active Directory Privileged Identity Management per consentire la gestione di PIM.
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
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="9ab97-103">Concedere l'accesso per la gestione di Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="9ab97-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="9ab97-104">L'amministratore globale che abilita Azure AD Privileged Identity Management (PIM) per un'organizzazione ottiene automaticamente le assegnazioni di ruolo e l'accesso a PIM.</span><span class="sxs-lookup"><span data-stu-id="9ab97-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="9ab97-105">Per impostazione predefinita, nessun altro utente ottiene l'accesso in scrittura, inclusi gli altri amministratori globali.</span><span class="sxs-lookup"><span data-stu-id="9ab97-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="9ab97-106">Gli altri amministratori globali, amministratori della sicurezza e ruoli con autorizzazioni di lettura per la sicurezza hanno l'accesso in sola lettura ad Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="9ab97-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="9ab97-107">Per concedere l'accesso a PIM, il primo utente può assegnare ad altri il ruolo di **amministratore dei ruoli con privilegi** .</span><span class="sxs-lookup"><span data-stu-id="9ab97-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="9ab97-108">Questa assegnazione deve essere eseguita dall'interno PIM e non può essere modificata tramite PowerShell o altri portali.</span><span class="sxs-lookup"><span data-stu-id="9ab97-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="9ab97-109">Per la gestione di Azure AD PIM è necessario Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="9ab97-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="9ab97-110">Poiché gli account Microsoft non possono effettuare la registrazione per Azure MFA, gli utenti che eseguono l'accesso con un account Microsoft non possono accedere a Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="9ab97-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="9ab97-111">Assicurarsi che almeno due utenti abbiano sempre il ruolo di amministratore dei ruoli con privilegi, per l'eventualità in cui uno di questi venga bloccato o il suo account venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="9ab97-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="9ab97-112">Concedere a un altro utente l'accesso per la gestione di PIM</span><span class="sxs-lookup"><span data-stu-id="9ab97-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="9ab97-113">Accedere al [portale di Azure](https://portal.azure.com/) e selezionare l'app **Azure AD Privileged Identity Management** nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="9ab97-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="9ab97-114">Selezionare **Gestione dei ruoli con privilegi** > **Amministratore dei ruoli con privilegi** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9ab97-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Schermata Aggiungi amministratori dei ruoli con privilegi][1]
3. <span data-ttu-id="9ab97-116">Nel pannello Aggiungi utenti gestiti il passaggio 1 è già stato completato.</span><span class="sxs-lookup"><span data-stu-id="9ab97-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="9ab97-117">Selezionare il passaggio 2, **Seleziona utenti** e ricercare l'utente da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="9ab97-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Schermata Seleziona gli utenti][2]
4. <span data-ttu-id="9ab97-119">Selezionare l'utente nell'elenco dei risultati della ricerca e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="9ab97-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="9ab97-120">Fare clic su **OK** per salvare la selezione.</span><span class="sxs-lookup"><span data-stu-id="9ab97-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="9ab97-121">L'utente selezionato verrà visualizzato nell'elenco degli amministratori dei ruoli con privilegi.</span><span class="sxs-lookup"><span data-stu-id="9ab97-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="9ab97-122">Ogni volta che si assegna un nuovo ruolo a un utente, questo viene configurato automaticamente come idoneo per attivare il ruolo.</span><span class="sxs-lookup"><span data-stu-id="9ab97-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="9ab97-123">Se si vuole rendere l'utente permanente nel ruolo, fare clic sull'utente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="9ab97-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="9ab97-124">Scegliere **Rendi permanente** dal menu delle informazioni dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9ab97-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="9ab97-125">Inviare all'utente un collegamento a [Introduzione ad Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="9ab97-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="9ab97-126">Rimuovere i diritti di accesso di un altro utente per la gestione di PIM</span><span class="sxs-lookup"><span data-stu-id="9ab97-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="9ab97-127">Prima di rimuovere un utente dal ruolo di amministratore dei ruoli con privilegi, assicurarsi che siano sempre presenti due utenti assegnati al ruolo.</span><span class="sxs-lookup"><span data-stu-id="9ab97-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="9ab97-128">Nel dashboard di PIM fare clic sul ruolo di **amministratore dei ruoli con privilegi**.</span><span class="sxs-lookup"><span data-stu-id="9ab97-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="9ab97-129">Verrà visualizzato l'elenco degli utenti attualmente assegnati al ruolo.</span><span class="sxs-lookup"><span data-stu-id="9ab97-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="9ab97-130">Selezionare l'utente nell'elenco degli utenti.</span><span class="sxs-lookup"><span data-stu-id="9ab97-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="9ab97-131">Fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="9ab97-131">Click on **Remove**.</span></span>  <span data-ttu-id="9ab97-132">Verrà visualizzato un messaggio di richiesta di conferma.</span><span class="sxs-lookup"><span data-stu-id="9ab97-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="9ab97-133">Fare clic su **Sì** per rimuovere l'utente dal ruolo.</span><span class="sxs-lookup"><span data-stu-id="9ab97-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="9ab97-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9ab97-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
