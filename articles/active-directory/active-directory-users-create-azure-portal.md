---
title: aaaAdd nuovi utenti tooAzure Active Directory | Documenti Microsoft
description: Viene illustrato come tooadd nuovi utenti o modificare le informazioni utente in Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: c4a156ea31b81202bb0d0ac224afbfc3f1785532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-tooazure-active-directory"></a><span data-ttu-id="d9256-103">Aggiungere nuovi utenti tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9256-103">Add new users tooAzure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9256-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d9256-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="d9256-105">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="d9256-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="d9256-106">Questo articolo spiega come tooadd nuovi utenti dell'organizzazione in hello Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9256-106">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="d9256-107">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="d9256-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="d9256-108">Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="d9256-108">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura del pannello Utenti e gruppi](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="d9256-110">In hello **utenti e gruppi** pannello seleziona **tutti gli utenti**, quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d9256-110">On hello **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Comando Aggiungi hello](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="d9256-112">Immettere i dettagli per l'utente hello, ad esempio **nome** e **nome utente**.</span><span class="sxs-lookup"><span data-stu-id="d9256-112">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="d9256-113">parte di nome di dominio di Hello del nome utente hello deve essere il nome di dominio "foo.onmicrosoft.com" hello predefinita iniziale dominio nome o un nome di dominio verificato, non federati, ad esempio "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="d9256-113">hello domain name portion of hello user name must either be hello initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="d9256-114">Generato password utente in modo che è possibile fornirlo toohello utente al termine questo processo di copia o hello nota in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="d9256-114">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="d9256-115">Facoltativamente, è possibile aprire e compilare informazioni hello in hello **profilo** blade, hello **gruppi** pannello o hello **ruolo della Directory** pannello per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="d9256-115">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="d9256-116">Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d9256-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="d9256-117">In hello **utente** pannello seleziona **crea**.</span><span class="sxs-lookup"><span data-stu-id="d9256-117">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="d9256-118">Consente di distribuire in modo sicuro generato hello password toohello nuovo utente in modo che hello utente possa accedere.</span><span class="sxs-lookup"><span data-stu-id="d9256-118">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="d9256-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d9256-119">Next steps</span></span>
* [<span data-ttu-id="d9256-120">Aggiungere un utente esterno</span><span class="sxs-lookup"><span data-stu-id="d9256-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="d9256-121">Reimpostare la password dell'utente nel nuovo portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="d9256-121">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="d9256-122">Modificare le informazioni di lavoro di un utente</span><span class="sxs-lookup"><span data-stu-id="d9256-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="d9256-123">Gestire i profili utente</span><span class="sxs-lookup"><span data-stu-id="d9256-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="d9256-124">Eliminare un utente in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9256-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="d9256-125">Assegnare un ruolo di utente tooa in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9256-125">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
