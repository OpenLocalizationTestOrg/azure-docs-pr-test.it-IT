---
title: Aggiungere nuovi utenti ad Azure Active Directory | Documentazione Microsoft
description: Viene illustrato come aggiungere nuovi utenti in Azure Active Directory.
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="2286e-103">Guida introduttiva: Aggiungere nuovi utenti ad anteprima di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2286e-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="2286e-104">In questo articolo viene illustrato come aggiungere nuovi utenti dell'organizzazione in Azure Active Directory (Azure AD) uno per volta, utilizzando il portale di Azure o sincronizzando i dati dell'account utente Windows Server Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="2286e-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="2286e-105">Aggiungere gli utenti basati su cloud</span><span class="sxs-lookup"><span data-stu-id="2286e-105">Add cloud-based users</span></span>
1. <span data-ttu-id="2286e-106">Accedere all'[interfaccia di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account di amministratore globale per la directory del tenant.</span><span class="sxs-lookup"><span data-stu-id="2286e-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="2286e-107">Selezionare **Azure Active Directory** e quindi **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2286e-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="2286e-108">Nel pannello **Utenti e gruppi** selezionare **Tutti gli utenti** e quindi selezionare **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="2286e-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="2286e-109">![Selezione del comando Aggiungi](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="2286e-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="2286e-110">Immettere dettagli per gli utenti, ad esempio **nome** e **nome utente**.</span><span class="sxs-lookup"><span data-stu-id="2286e-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="2286e-111">La parte del nome di dominio del nome utente deve essere il nome di dominio "[nome dominio]" del nome di dominio predefinito iniziale o un nome di dominio verificato, non federato, [personalizzato, ](add-custom-domain.md)ad esempio "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="2286e-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="2286e-112">Copiare o comunque annotare la password generata in modo da poterla fornire all'utente al termine del processo.</span><span class="sxs-lookup"><span data-stu-id="2286e-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="2286e-113">Facoltativamente, è possibile aprire e inserire le informazioni contenute nel pannello **Profilo**, **Gruppi** o **Ruolo della directory** per l'utente.</span><span class="sxs-lookup"><span data-stu-id="2286e-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="2286e-114">Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2286e-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="2286e-115">Nel pannello **Utente** selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2286e-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="2286e-116">Distribuire in modo sicuro la password generata al nuovo utente per consentirgli l'accesso.</span><span class="sxs-lookup"><span data-stu-id="2286e-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="2286e-117">È inoltre possibile sincronizzare i dati dell'account utente locale Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2286e-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="2286e-118">Le soluzioni di gestione delle identità di Microsoft abbracciano funzionalità locali e basate sul cloud, creando una singola identità utente per l’autenticazione e l’autorizzazione per tutte le risorse, indipendentemente dalla loro ubicazione.</span><span class="sxs-lookup"><span data-stu-id="2286e-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="2286e-119">Tutto questo viene chiamato Identità ibrida.</span><span class="sxs-lookup"><span data-stu-id="2286e-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="2286e-120">È possibile utilizzare [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)per integrare le directory locali con Azure Active Directory per gli scenari con identità ibrida.</span><span class="sxs-lookup"><span data-stu-id="2286e-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="2286e-121">Consente quindi di fornire agli utenti un'identità comune per le applicazioni di Office 365, Azure e SaaS integrate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2286e-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="2286e-122">Eliminare gli utenti da Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2286e-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="2286e-123">Accedere all'[interfaccia di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account di amministratore globale per la directory del tenant.</span><span class="sxs-lookup"><span data-stu-id="2286e-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="2286e-124">Selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2286e-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="2286e-125">Nel pannello **Utenti e gruppi**, selezionare l'utente da eliminare dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="2286e-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="2286e-126">Nel pannello dell'utente selezionare **Panoramica**, quindi nella barra dei comandi selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="2286e-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="2286e-127">![Selezione del comando Aggiungi](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="2286e-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="2286e-128">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="2286e-128">Learn more</span></span> 
* [<span data-ttu-id="2286e-129">Aggiungere un utente esterno</span><span class="sxs-lookup"><span data-stu-id="2286e-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="2286e-130">Assegnare un utente a un ruolo in Azure AD</span><span class="sxs-lookup"><span data-stu-id="2286e-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="2286e-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2286e-131">Next steps</span></span>
<span data-ttu-id="2286e-132">In questa guida introduttiva si è appreso come aggiungere nuovi utenti ad Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="2286e-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="2286e-133">È possibile usare il collegamento seguente per creare un nuovo utente in Azure AD dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2286e-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2286e-134">Aggiungere utenti ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="2286e-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 