---
title: Mapping delle attestazioni utente per Collaborazione B2B in Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: 5f8559450b24effd40a38879aeae3a8dd03944a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="4eb4b-103">Mapping delle attestazioni utente per Collaborazione B2B in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4eb4b-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="4eb4b-104">Azure Active Directory (Azure AD) supporta la personalizzazione delle attestazioni rilasciate nel token SAML per gli utenti di Collaborazione B2B.</span><span class="sxs-lookup"><span data-stu-id="4eb4b-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="4eb4b-105">Quando un utente esegue l'autenticazione all'applicazione, Azure AD rilascia un token SAML all'applicazione contenente informazioni (o attestazioni) sull'utente, che lo identificano in modo univoco.</span><span class="sxs-lookup"><span data-stu-id="4eb4b-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="4eb4b-106">Per impostazione predefinita, sono inclusi il nome utente, l'indirizzo di posta elettronica, il nome e il cognome dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4eb4b-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="4eb4b-107">Le attestazioni inviate all'applicazione nel token SAML possono essere visualizzate o modificate nella scheda Attributi .</span><span class="sxs-lookup"><span data-stu-id="4eb4b-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="4eb4b-108">Due sono i possibili motivi per cui potrebbe essere necessario modificare le attestazioni rilasciate nel token SAML.</span><span class="sxs-lookup"><span data-stu-id="4eb4b-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="4eb4b-109">L'applicazione è stata scritta per richiedere un set di URI attestazione o di valori attestazione diverso</span><span class="sxs-lookup"><span data-stu-id="4eb4b-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="4eb4b-110">L'applicazione richiede che l'attestazione NameIdentifier sia diversa dal nome dell'entità utente archiviato in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4eb4b-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![Visualizzare le attestazioni nel token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="4eb4b-112">Per informazioni su come aggiungere e modificare le attestazioni, vedere l'articolo sulla personalizzazione delle attestazioni, [Personalizzazione delle attestazioni rilasciate nel token SAML per le app preintegrate in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="4eb4b-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="4eb4b-113">Per gli utenti di Collaborazione B2B, il mapping tra NameID e UPN tra tenant non è consentito per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4eb4b-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4eb4b-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4eb4b-114">Next steps</span></span>

<span data-ttu-id="4eb4b-115">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="4eb4b-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4eb4b-116">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="4eb4b-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4eb4b-117">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="4eb4b-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="4eb4b-118">Aggiunta di un utente di Collaborazione B2B a un ruolo</span><span class="sxs-lookup"><span data-stu-id="4eb4b-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="4eb4b-119">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="4eb4b-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="4eb4b-120">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="4eb4b-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="4eb4b-121">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="4eb4b-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="4eb4b-122">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="4eb4b-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="4eb4b-123">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="4eb4b-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="4eb4b-124">Token utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="4eb4b-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="4eb4b-125">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="4eb4b-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
