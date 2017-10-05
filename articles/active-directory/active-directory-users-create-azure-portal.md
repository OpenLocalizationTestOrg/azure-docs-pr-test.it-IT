---
title: Aggiungere nuovi utenti ad Azure Active Directory | Documentazione Microsoft
description: Illustra come aggiungere nuovi utenti o modificare le informazioni sugli utenti in Azure Active Directory.
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
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="c73c4-103">Aggiungere nuovi utenti in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c73c4-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c73c4-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c73c4-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="c73c4-105">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="c73c4-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="c73c4-106">Questo articolo illustra come aggiungere nuovi utenti all'organizzazione in Azure Active Directory, ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c73c4-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="c73c4-107">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="c73c4-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c73c4-108">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="c73c4-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura del pannello Utenti e gruppi](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="c73c4-110">Nel pannello **Utenti e gruppi** selezionare **Tutti gli utenti** e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c73c4-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Selezione del comando Aggiungi](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="c73c4-112">Immettere dettagli per gli utenti, ad esempio **nome** e **nome utente**.</span><span class="sxs-lookup"><span data-stu-id="c73c4-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="c73c4-113">La parte del nome di dominio del nome utente deve essere il nome di dominio "foo.onmicrosoft.com" del nome di dominio predefinito iniziale o un nome di dominio verificato, non federato, ad esempio "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="c73c4-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="c73c4-114">Copiare o comunque annotare la password generata in modo da poterla fornire all'utente al termine del processo.</span><span class="sxs-lookup"><span data-stu-id="c73c4-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="c73c4-115">Facoltativamente, è possibile aprire e inserire le informazioni contenute nel pannello **Profilo**, **Gruppi** o **Ruolo della directory** per l'utente.</span><span class="sxs-lookup"><span data-stu-id="c73c4-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="c73c4-116">Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c73c4-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="c73c4-117">Nel pannello **Utente** selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c73c4-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="c73c4-118">Distribuire in modo sicuro la password generata al nuovo utente per consentirgli l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c73c4-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="c73c4-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c73c4-119">Next steps</span></span>
* [<span data-ttu-id="c73c4-120">Aggiungere un utente esterno</span><span class="sxs-lookup"><span data-stu-id="c73c4-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="c73c4-121">Reimpostare la password di un utente nel nuovo portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c73c4-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="c73c4-122">Modificare le informazioni di lavoro di un utente</span><span class="sxs-lookup"><span data-stu-id="c73c4-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="c73c4-123">Gestire i profili utente</span><span class="sxs-lookup"><span data-stu-id="c73c4-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="c73c4-124">Eliminare un utente in Azure AD</span><span class="sxs-lookup"><span data-stu-id="c73c4-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="c73c4-125">Assegnare un utente a un ruolo in Azure AD</span><span class="sxs-lookup"><span data-stu-id="c73c4-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
