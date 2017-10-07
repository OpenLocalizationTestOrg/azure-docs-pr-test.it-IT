---
title: dominio personalizzato aaaAssign utenti tooa in Azure Active Directory | Documenti Microsoft
description: Come toopopulate un dominio personalizzato in Azure Active Directory con account utente.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="af2b8-103">Assegnare gli utenti tooa personalizzato dominio</span><span class="sxs-lookup"><span data-stu-id="af2b8-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="af2b8-104">Dopo aver aggiunto il tooAzure personalizzato di dominio Active Directory, è necessario aggiungere gli account utente di hello per questo dominio, in modo da poter iniziare tuttavia l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="af2b8-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af2b8-105">Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="af2b8-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="af2b8-106">Per modalità toomanage i nomi di dominio nel centro di amministrazione di hello Azure AD, vedere [gestione dei nomi di dominio personalizzati in Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af2b8-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="af2b8-107">Utenti sincronizzati da una directory locale</span><span class="sxs-lookup"><span data-stu-id="af2b8-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="af2b8-108">Se è già stato di una connessione tra locale Active Directory e Azure Active Directory, sincronizzazione può popolare account hello.</span><span class="sxs-lookup"><span data-stu-id="af2b8-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="af2b8-109">Per ulteriori informazioni su come toosynchronize Azure Active Directory con Active Directory locale, vedere [integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="af2b8-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="af2b8-110">Gli utenti aggiunti e gestiti nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="af2b8-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="af2b8-111">dominio di hello toochange per un account utente esistente:</span><span class="sxs-lookup"><span data-stu-id="af2b8-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="af2b8-112">Hello aprirlo portale di Azure classico utilizzando un account che è un amministratore globale o un amministratore di utente.</span><span class="sxs-lookup"><span data-stu-id="af2b8-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="af2b8-113">Aprire la directory.</span><span class="sxs-lookup"><span data-stu-id="af2b8-113">Open your directory.</span></span>
3. <span data-ttu-id="af2b8-114">Seleziona hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="af2b8-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="af2b8-115">Selezionare hello utente dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="af2b8-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="af2b8-116">Modificare il dominio hello per utente hello e quindi selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="af2b8-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="af2b8-117">Questa operazione può anche essere eseguita tramite [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="af2b8-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="af2b8-118">Selezionare un dominio personalizzato durante la creazione di un nuovo utente</span><span class="sxs-lookup"><span data-stu-id="af2b8-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="af2b8-119">Hello aprirlo portale di Azure classico utilizzando un account che è un amministratore globale o un amministratore di utente.</span><span class="sxs-lookup"><span data-stu-id="af2b8-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="af2b8-120">Aprire la directory.</span><span class="sxs-lookup"><span data-stu-id="af2b8-120">Open your directory.</span></span>
3. <span data-ttu-id="af2b8-121">Seleziona hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="af2b8-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="af2b8-122">Nella barra dei comandi di hello, selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="af2b8-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="af2b8-123">Quando si aggiunge il nome di utente hello, scegliere dominio personalizzato hello dall'elenco di domini hello.</span><span class="sxs-lookup"><span data-stu-id="af2b8-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="af2b8-124">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="af2b8-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af2b8-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af2b8-125">Next steps</span></span>
* [<span data-ttu-id="af2b8-126">Utilizzo di dominio personalizzato nomi toosimplify hello esperienza di accesso per gli utenti</span><span class="sxs-lookup"><span data-stu-id="af2b8-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="af2b8-127">Gestire i nomi di dominio personalizzati</span><span class="sxs-lookup"><span data-stu-id="af2b8-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="af2b8-128">Informazioni sui concetti relativi alla gestione dei domini in Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2b8-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

