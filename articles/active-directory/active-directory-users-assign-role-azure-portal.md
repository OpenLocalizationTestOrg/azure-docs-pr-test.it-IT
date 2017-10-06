---
title: un utente aaaAssign tooadministrator ruoli in Azure Active Directory | Documenti Microsoft
description: Viene illustrato come le informazioni amministrative toochange utente in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: 8bb6711c2570843962fe075b6026542a4bca525f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-tooadministrator-roles-in-azure-active-directory"></a><span data-ttu-id="65cf8-103">Assegnare un utente tooadministrator ruoli in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65cf8-103">Assign a user tooadministrator roles in Azure Active Directory</span></span>
<span data-ttu-id="65cf8-104">Questo articolo viene illustrato come tooassign un utente tooa ruolo amministrativo in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65cf8-104">This article explains how tooassign an administrative role tooa user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="65cf8-105">Per informazioni sull'aggiunta di nuovi utenti nell'organizzazione, vedere [aggiungere nuovi utenti tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="65cf8-105">For information about adding new users in your organization, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="65cf8-106">Gli utenti aggiunti non dispongono delle autorizzazioni di amministratore per impostazione predefinita, ma è possibile assegnare ruoli toothem in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="65cf8-106">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="65cf8-107">Assegnare un utente tooa ruolo</span><span class="sxs-lookup"><span data-stu-id="65cf8-107">Assign a role tooa user</span></span>
1. <span data-ttu-id="65cf8-108">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="65cf8-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="65cf8-109">Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="65cf8-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="65cf8-111">In hello **utenti e gruppi** pannello seleziona **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="65cf8-111">On hello **Users and groups** blade, select **All users**.</span></span>

   ![Apertura hello blade di tutti gli utenti](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="65cf8-113">In hello **utenti e gruppi - tutti gli utenti** pannello, selezionare un utente dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="65cf8-113">On hello **Users and groups - All users** blade, select a user from hello list.</span></span>
5. <span data-ttu-id="65cf8-114">Nel Pannello di hello per l'utente selezionato hello, selezionare **ruolo della Directory**, quindi assegnare ruoli di hello utente tooa da hello **ruolo della Directory** elenco.</span><span class="sxs-lookup"><span data-stu-id="65cf8-114">On hello blade for hello selected user, select **Directory role**, and then assign hello user tooa role from hello **Directory role** list.</span></span> <span data-ttu-id="65cf8-115">Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="65cf8-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Assegnazione di un ruolo di utente tooa](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="65cf8-117">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="65cf8-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65cf8-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65cf8-118">Next steps</span></span>
* [<span data-ttu-id="65cf8-119">Aggiungere un utente</span><span class="sxs-lookup"><span data-stu-id="65cf8-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="65cf8-120">Reimpostare la password dell'utente nel nuovo portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="65cf8-120">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="65cf8-121">Modificare le informazioni di lavoro di un utente</span><span class="sxs-lookup"><span data-stu-id="65cf8-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="65cf8-122">Gestire i profili utente</span><span class="sxs-lookup"><span data-stu-id="65cf8-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="65cf8-123">Eliminare un utente in Azure AD</span><span class="sxs-lookup"><span data-stu-id="65cf8-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
