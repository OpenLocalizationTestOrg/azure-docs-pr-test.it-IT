---
title: Assegnare un utente ai ruoli di amministratore in Azure Active Directory | Microsoft Docs
description: Illustra come cambiare le informazioni amministrative in Azure Active Directory
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
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="e3acf-103">Assegnare un utente ai ruoli di amministratore in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3acf-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="e3acf-104">Questo articolo descrive come assegnare un ruolo di amministratore a un utente in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3acf-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e3acf-105">Per informazioni sull'aggiunta di nuovi utenti nell'organizzazione, vedere [Aggiungere nuovi utenti ad Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e3acf-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="e3acf-106">Gli utenti aggiunti non hanno autorizzazioni di amministratore per impostazione predefinita, ma è possibile assegnare loro dei ruoli in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="e3acf-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="e3acf-107">Assegnare un ruolo a un utente</span><span class="sxs-lookup"><span data-stu-id="e3acf-107">Assign a role to a user</span></span>
1. <span data-ttu-id="e3acf-108">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="e3acf-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="e3acf-109">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="e3acf-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="e3acf-111">Nel pannello **Utenti e gruppi** selezionare **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e3acf-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![Apertura del pannello Tutti gli utenti](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="e3acf-113">Nel pannello **Utenti e gruppi - Tutti gli utenti** selezionare un utente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="e3acf-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="e3acf-114">Nel pannello per l'utente prescelto selezionare **Ruolo della directory** e quindi assegnare l'utente a un ruolo nell'elenco **Ruolo della directory**.</span><span class="sxs-lookup"><span data-stu-id="e3acf-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="e3acf-115">Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e3acf-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Assegnazione di un utente a un ruolo](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="e3acf-117">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e3acf-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3acf-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3acf-118">Next steps</span></span>
* [<span data-ttu-id="e3acf-119">Aggiungere un utente</span><span class="sxs-lookup"><span data-stu-id="e3acf-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="e3acf-120">Reimpostare la password di un utente nel nuovo portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e3acf-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="e3acf-121">Modificare le informazioni di lavoro di un utente</span><span class="sxs-lookup"><span data-stu-id="e3acf-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="e3acf-122">Gestire i profili utente</span><span class="sxs-lookup"><span data-stu-id="e3acf-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="e3acf-123">Eliminare un utente in Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3acf-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
