---
title: aaaHow tooconfigure una nuova applicazione multi-tenant | Documenti Microsoft
description: Come tooconfigure single sign-on per un'applicazione personalizzata sono lo sviluppo e la registrazione con Azure AD.
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="804d4-103">Come tooconfigure una nuova applicazione multi-tenant</span><span class="sxs-lookup"><span data-stu-id="804d4-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="804d4-104">L'abilitazione dell'accesso Single Sign-on (SSO) federato nell'applicazione avviene automaticamente quando si esegue la federazione tramite Azure AD per OpenID Connect, SAML 2.0 o WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="804d4-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="804d4-105">Se gli utenti finali hanno toosign in nonostante che dispongono già di una sessione esistente in Azure AD, è probabile che l'app sia configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="804d4-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="804d4-106">Se si usa ADAL/MSAL, accertarsi di avere **PromptBehavior** impostare troppo**Auto** anziché **sempre**.</span><span class="sxs-lookup"><span data-stu-id="804d4-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="804d4-107">Se si sta creando un'app per dispositivi mobili, potrebbe essere configurazioni aggiuntive tooenable negoziata o SSO non-negoziata.</span><span class="sxs-lookup"><span data-stu-id="804d4-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="804d4-108">Per Android, vedere [Abilitare l'accesso Single Sign-On tra app in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="804d4-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="804d4-109">Per iOS, vedere [Abilitare l'accesso Single Sign-On tra app in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="804d4-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="804d4-110">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="804d4-110">Next steps</span></span>

[<span data-ttu-id="804d4-111">Accesso Single Sign-On AD Azure</span><span class="sxs-lookup"><span data-stu-id="804d4-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="804d4-112">Abilitare l'accesso Single Sign-On tra app in Android</span><span class="sxs-lookup"><span data-stu-id="804d4-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="804d4-113">Abilitare l'accesso Single Sign-On tra app in iOS</span><span class="sxs-lookup"><span data-stu-id="804d4-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="804d4-114">L'integrazione di applicazioni tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="804d4-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

<span data-ttu-id="804d4-115">[Consent and Permissioning for AzureAD v2.0 converged Apps](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes) (Consenso e concessione delle autorizzazioni per le app con convergenza di Azure Active Directory v2.0)</span><span class="sxs-lookup"><span data-stu-id="804d4-115">[Consent and Permissioning for AzureAD v2.0 converged Apps](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)</span></span><br>

[<span data-ttu-id="804d4-116">Azure AD in Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="804d4-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
