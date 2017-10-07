---
title: 'Azure AD Connect: Autenticazione pass-through - Limitazioni correnti | Microsoft Docs'
description: Questo articolo descrive le limitazioni correnti hello di autenticazione pass-through di Azure Active Directory (Azure AD).
services: active-directory
keywords: Autenticazione pass-through di Azure AD Connect, installare Active Directory, componenti necessari per Azure AD, SSO, Single Sign-On
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="2f0e6-104">Autenticazione pass-through di Azure Active Directory - Limitazioni correnti</span><span class="sxs-lookup"><span data-stu-id="2f0e6-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="2f0e6-105">L'autenticazione pass-through di Azure AD è attualmente in fase di anteprima.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="2f0e6-106">È una funzionalità disponibile gratuitamente e non è necessario qualsiasi edizione a pagamento di Azure AD toouse è.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-106">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="2f0e6-107">L'autenticazione pass-through è disponibile solo in hello world wide istanza Azure Active Directory e non su [Microsoft Cloud Germania](http://www.microsoft.de/cloud-deutschland) e [Cloud di Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="2f0e6-107">Pass-through Authentication is only available in hello world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="2f0e6-108">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="2f0e6-108">Supported scenarios</span></span>

<span data-ttu-id="2f0e6-109">Hello seguenti scenari è completamente supportato durante l'anteprima:</span><span class="sxs-lookup"><span data-stu-id="2f0e6-109">hello following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="2f0e6-110">L'utente accede a tutte le applicazioni basate su Web browser.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="2f0e6-111">L'utente accede ad applicazioni client di Office 365 che supportano l'[autenticazione moderna](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="2f0e6-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="2f0e6-112">Aggiunta ad Azure AD per dispositivi Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="2f0e6-113">Supporto di Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="2f0e6-114">Scenari non supportati</span><span class="sxs-lookup"><span data-stu-id="2f0e6-114">Unsupported scenarios</span></span>

<span data-ttu-id="2f0e6-115">Hello negli scenari seguenti vengono _non_ supportata durante l'anteprima:</span><span class="sxs-lookup"><span data-stu-id="2f0e6-115">hello following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="2f0e6-116">Accesso degli utenti ad applicazioni client legacy di Office (Office 2013 o versioni precedenti).</span><span class="sxs-lookup"><span data-stu-id="2f0e6-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="2f0e6-117">Le organizzazioni sono invitati tooswitch toomodern autenticazione, se possibile.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-117">Organizations are encouraged tooswitch toomodern authentication, if possible.</span></span> <span data-ttu-id="2f0e6-118">L'autenticazione moderna permette di supportare l'autenticazione pass-through e contribuisce anche a proteggere gli account utente tramite le funzionalità di [accesso condizionale](../active-directory-conditional-access.md), come l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="2f0e6-119">Accesso degli utenti ad applicazioni client Skype for Business, incluso Skype for Business 2016.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="2f0e6-120">L'utente accede a PowerShell v 1.0.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="2f0e6-121">È consigliabile tuttavia usare PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2f0e6-122">Come soluzione alternativa per scenari non supportati, attivare la sincronizzazione dell'Hash Password hello [funzionalità facoltative](active-directory-aadconnect-get-started-custom.md#optional-features) pagina nella procedura guidata Connetti hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on hello [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in hello Azure AD Connect wizard.</span></span> <span data-ttu-id="2f0e6-123">Sincronizzazione dell'Hash password agisce come fallback per hello precedenti scenari _solo_ (e _non_ come un generico tooPass-tramite l'autenticazione di fallback).</span><span class="sxs-lookup"><span data-stu-id="2f0e6-123">Password Hash Synchronization acts as a fallback for hello preceding scenarios _only_ (and _not_ as a generic fallback tooPass-through Authentication).</span></span> <span data-ttu-id="2f0e6-124">Se questi scenari non sono necessari, disabilitare la sincronizzazione dell'hash della password.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f0e6-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f0e6-125">Next steps</span></span>
- <span data-ttu-id="2f0e6-126">[**Guida introduttiva**](active-directory-aadconnect-pass-through-authentication-quick-start.md): avvio ed esecuzione dell'autenticazione pass-through di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="2f0e6-127">[**Approfondimento tecnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): informazioni sul funzionamento di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="2f0e6-128">[**Domande frequenti su** ](active-directory-aadconnect-pass-through-authentication-faq.md) -risposte toofrequently domande frequenti.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="2f0e6-129">[**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="2f0e6-130">[**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="2f0e6-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2f0e6-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
