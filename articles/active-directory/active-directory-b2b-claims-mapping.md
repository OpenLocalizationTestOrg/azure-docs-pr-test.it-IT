---
title: mapping in Azure Active Directory di attestazioni utente collaborazione aaaB2B | Documenti Microsoft
description: Informazioni sul mapping delle attestazioni per Collaborazione B2B in Azure Active Directory
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="98180-103">Mapping delle attestazioni utente per Collaborazione B2B in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98180-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="98180-104">Azure Active Directory (Azure AD) supporta la personalizzazione di attestazioni di hello rilasciate nel token SAML hello per gli utenti di collaborazione B2B.</span><span class="sxs-lookup"><span data-stu-id="98180-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="98180-105">Quando un utente esegue l'autenticazione dell'applicazione toohello, Azure AD rilascia una app toohello token SAML che contiene informazioni (o attestazioni) sull'utente hello che li identifica in modo univoco.</span><span class="sxs-lookup"><span data-stu-id="98180-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="98180-106">Per impostazione predefinita, sono inclusi il nome utente dell'utente hello, indirizzo di posta elettronica, nome e cognome.</span><span class="sxs-lookup"><span data-stu-id="98180-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="98180-107">È possibile visualizzare o modificare attestazioni hello inviate in hello applicazione toohello token SAML nella scheda attributi hello.</span><span class="sxs-lookup"><span data-stu-id="98180-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="98180-108">Esistono due possibili motivi per cui potrebbe essere necessario attestazioni di hello tooedit rilasciate nel token SAML hello.</span><span class="sxs-lookup"><span data-stu-id="98180-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="98180-109">è stato scritto toorequire un diverso set di URI di attestazione o i valori di attestazione a un'applicazione Hello</span><span class="sxs-lookup"><span data-stu-id="98180-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="98180-110">L'applicazione richiede toobe di attestazione NameIdentifier hello diverso dal nome dell'entità utente hello archiviati in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="98180-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![Visualizzare le attestazioni nel token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="98180-112">Per informazioni su come tooadd e modifica attestazioni, vedere l'articolo specificato di personalizzazione di attestazioni, [personalizzazione di attestazioni rilasciate nel token SAML hello per le app preintegrate in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="98180-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="98180-113">Per gli utenti di Collaborazione B2B, il mapping tra NameID e UPN tra tenant non è consentito per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="98180-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="98180-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98180-114">Next steps</span></span>

<span data-ttu-id="98180-115">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="98180-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="98180-116">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="98180-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="98180-117">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="98180-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="98180-118">Aggiunta di un ruolo di tooa utente collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="98180-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="98180-119">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="98180-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="98180-120">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="98180-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="98180-121">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="98180-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="98180-122">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="98180-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="98180-123">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="98180-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="98180-124">Token utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="98180-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="98180-125">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="98180-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
