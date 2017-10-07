---
title: aaaAdd nuovi utenti tooAzure Active Directory | Documenti Microsoft
description: Viene illustrato come tooadd nuovi utenti in Azure Active Directory.
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
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="a51e8-103">Guida introduttiva: Aggiungere nuovi utenti tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a51e8-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="a51e8-104">Questo articolo spiega come tooadd nuovi utenti dell'organizzazione in Azure Active Directory (Azure AD) hello uno alla volta utilizzando hello portale di Azure o sincronizzando l'utente di Windows Server Active Directory locale dell'account dati.</span><span class="sxs-lookup"><span data-stu-id="a51e8-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="a51e8-105">Aggiungere gli utenti basati su cloud</span><span class="sxs-lookup"><span data-stu-id="a51e8-105">Add cloud-based users</span></span>
1. <span data-ttu-id="a51e8-106">Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="a51e8-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="a51e8-107">Selezionare **Azure Active Directory** e quindi **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a51e8-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="a51e8-108">In hello **utenti e gruppi** pannello seleziona **tutti gli utenti**, quindi selezionare **nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="a51e8-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="a51e8-109">![Comando Aggiungi hello](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="a51e8-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="a51e8-110">Immettere i dettagli per l'utente hello, ad esempio **nome** e **nome utente**.</span><span class="sxs-lookup"><span data-stu-id="a51e8-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="a51e8-111">Hello parte di nome di dominio del nome utente hello deve essere hello predefinita iniziale dominio nome "[nome dominio].onmicrosoft.com" o verificati, non federata [nome di dominio personalizzato](add-custom-domain.md) , ad esempio "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="a51e8-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="a51e8-112">Generato password utente in modo che è possibile fornirlo toohello utente al termine questo processo di copia o hello nota in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="a51e8-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="a51e8-113">Facoltativamente, è possibile aprire e compilare informazioni hello in hello **profilo** blade, hello **gruppi** pannello o hello **ruolo della Directory** pannello per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="a51e8-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="a51e8-114">Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a51e8-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="a51e8-115">In hello **utente** pannello seleziona **crea**.</span><span class="sxs-lookup"><span data-stu-id="a51e8-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="a51e8-116">Consente di distribuire in modo sicuro generato hello password toohello nuovo utente in modo che hello utente possa accedere.</span><span class="sxs-lookup"><span data-stu-id="a51e8-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="a51e8-117">È inoltre possibile sincronizzare i dati dell'account utente locale Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a51e8-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="a51e8-118">Soluzioni di gestione identità Microsoft span locale e le funzionalità basate su cloud, la creazione di una singola identità utente per l'autenticazione e autorizzazione tooall risorse, indipendentemente dalla posizione.</span><span class="sxs-lookup"><span data-stu-id="a51e8-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="a51e8-119">Tutto questo viene chiamato Identità ibrida.</span><span class="sxs-lookup"><span data-stu-id="a51e8-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="a51e8-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) può essere utilizzato toointegrate le directory locali con Azure Active Directory per gli scenari identità ibrido.</span><span class="sxs-lookup"><span data-stu-id="a51e8-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="a51e8-121">In questo modo tooprovide un'identità comune per gli utenti per le applicazioni di Office 365, Azure e SaaS integrata con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a51e8-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="a51e8-122">Eliminare gli utenti da Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a51e8-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="a51e8-123">Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="a51e8-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="a51e8-124">Selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a51e8-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="a51e8-125">In hello **utenti e gruppi** blade, toodelete utente hello selezionare dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="a51e8-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="a51e8-126">Nel Pannello di hello per l'utente selezionato hello, selezionare **Panoramica**, quindi nella barra dei comandi di hello, selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="a51e8-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="a51e8-127">![Comando Aggiungi hello](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="a51e8-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="a51e8-128">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a51e8-128">Learn more</span></span> 
* [<span data-ttu-id="a51e8-129">Aggiungere un utente esterno</span><span class="sxs-lookup"><span data-stu-id="a51e8-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="a51e8-130">Assegnare un ruolo di utente tooa in Azure AD</span><span class="sxs-lookup"><span data-stu-id="a51e8-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="a51e8-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a51e8-131">Next steps</span></span>
<span data-ttu-id="a51e8-132">In questa Guida rapida, si è appreso come tooadd nuovi utenti tooAzure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="a51e8-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="a51e8-133">È possibile utilizzare hello seguente collegamento toocreate un nuovo utente in Azure AD dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a51e8-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a51e8-134">Aggiungere gli utenti tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="a51e8-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
