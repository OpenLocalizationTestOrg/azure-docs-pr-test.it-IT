---
title: Come configurare una nuova applicazione multi-tenant | Microsoft Docs
description: Come configurare l'accesso Single Sign-on per un'applicazione personalizzata che si sta sviluppando e registrando con Azure AD.
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
ms.openlocfilehash: 0fdc58d82d9cd2e7edac33cc5af4b98d2fd06c56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="b5bf4-103">Come configurare una nuova applicazione multi-tenant</span><span class="sxs-lookup"><span data-stu-id="b5bf4-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="b5bf4-104">L'abilitazione dell'accesso Single Sign-on (SSO) federato nell'applicazione avviene automaticamente quando si esegue la federazione tramite Azure AD per OpenID Connect, SAML 2.0 o WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="b5bf4-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="b5bf4-105">Se gli utenti finali devono eseguire l'accesso nonostante dispongano già di una sessione esistente con Azure AD, è probabile che l'applicazione non sia configurata correttamente.</span><span class="sxs-lookup"><span data-stu-id="b5bf4-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="b5bf4-106">Se si usa ADAL/MSAL, accertarsi di avere impostato **PromptBehavior** su **Auto** anziché su **Sempre**.</span><span class="sxs-lookup"><span data-stu-id="b5bf4-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="b5bf4-107">Se si sta creando un'applicazione per dispositivi mobili, potrebbe essere necessaria della configurazione aggiuntiva per abilitare l'accesso Single Sign-On negoziato o non negoziato.</span><span class="sxs-lookup"><span data-stu-id="b5bf4-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="b5bf4-108">Per Android, vedere [Abilitare l'accesso Single Sign-On tra app in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="b5bf4-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="b5bf4-109">Per iOS, vedere [Abilitare l'accesso Single Sign-On tra app in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="b5bf4-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5bf4-110">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5bf4-110">Next steps</span></span>

[<span data-ttu-id="b5bf4-111">Accesso Single Sign-On AD Azure</span><span class="sxs-lookup"><span data-stu-id="b5bf4-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="b5bf4-112">Abilitare l'accesso Single Sign-On tra app in Android</span><span class="sxs-lookup"><span data-stu-id="b5bf4-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="b5bf4-113">Abilitare l'accesso Single Sign-On tra app in iOS</span><span class="sxs-lookup"><span data-stu-id="b5bf4-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="b5bf4-114">Integrazione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5bf4-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

<span data-ttu-id="b5bf4-115">[Consent and Permissioning for AzureAD v2.0 converged Apps](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes) (Consenso e concessione delle autorizzazioni per le app con convergenza di Azure Active Directory v2.0)</span><span class="sxs-lookup"><span data-stu-id="b5bf4-115">[Consent and Permissioning for AzureAD v2.0 converged Apps](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)</span></span><br>

[<span data-ttu-id="b5bf4-116">Azure AD in Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="b5bf4-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
