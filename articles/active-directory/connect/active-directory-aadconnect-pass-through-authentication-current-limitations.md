---
title: 'Azure AD Connect: Autenticazione pass-through - Limitazioni correnti | Microsoft Docs'
description: Questo articolo descrive le limitazioni correnti dell'autenticazione pass-through di Azure Active Directory (Azure AD).
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
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="1f400-104">Autenticazione pass-through di Azure Active Directory - Limitazioni correnti</span><span class="sxs-lookup"><span data-stu-id="1f400-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="1f400-105">L'autenticazione pass-through di Azure AD è attualmente in fase di anteprima.</span><span class="sxs-lookup"><span data-stu-id="1f400-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="1f400-106">È una funzionalità gratuita e non serve alcuna delle edizioni a pagamento di Azure AD per utilizzarla.</span><span class="sxs-lookup"><span data-stu-id="1f400-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="1f400-107">L'autenticazione pass-through è disponibile solo nell'istanza di Azure AD a livello mondiale, non in [Microsoft Cloud per la Germania](http://www.microsoft.de/cloud-deutschland) o nel [cloud di Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="1f400-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="1f400-108">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="1f400-108">Supported scenarios</span></span>

<span data-ttu-id="1f400-109">Gli scenari seguenti sono completamente supportati in fase di anteprima:</span><span class="sxs-lookup"><span data-stu-id="1f400-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="1f400-110">L'utente accede a tutte le applicazioni basate su Web browser.</span><span class="sxs-lookup"><span data-stu-id="1f400-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="1f400-111">L'utente accede ad applicazioni client di Office 365 che supportano l'[autenticazione moderna](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="1f400-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="1f400-112">Aggiunta ad Azure AD per dispositivi Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1f400-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="1f400-113">Supporto di Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="1f400-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="1f400-114">Scenari non supportati</span><span class="sxs-lookup"><span data-stu-id="1f400-114">Unsupported scenarios</span></span>

<span data-ttu-id="1f400-115">Gli scenari seguenti _non_ sono supportati in fase di anteprima:</span><span class="sxs-lookup"><span data-stu-id="1f400-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="1f400-116">Accesso degli utenti ad applicazioni client legacy di Office (Office 2013 o versioni precedenti).</span><span class="sxs-lookup"><span data-stu-id="1f400-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="1f400-117">Le organizzazioni sono incoraggiate a passare all'autenticazione moderna, se possibile.</span><span class="sxs-lookup"><span data-stu-id="1f400-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="1f400-118">L'autenticazione moderna permette di supportare l'autenticazione pass-through e contribuisce anche a proteggere gli account utente tramite le funzionalità di [accesso condizionale](../active-directory-conditional-access.md), come l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="1f400-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="1f400-119">Accesso degli utenti ad applicazioni client Skype for Business, incluso Skype for Business 2016.</span><span class="sxs-lookup"><span data-stu-id="1f400-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="1f400-120">L'utente accede a PowerShell v 1.0.</span><span class="sxs-lookup"><span data-stu-id="1f400-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="1f400-121">È consigliabile tuttavia usare PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="1f400-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1f400-122">Come soluzione alternativa per gli scenari non supportati, abilitare la sincronizzazione dell'hash della password nella pagina [Funzionalità facoltative](active-directory-aadconnect-get-started-custom.md#optional-features) della procedura guidata di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1f400-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="1f400-123">La sincronizzazione dell'hash della password funziona come fallback _solo_ per gli scenari precedenti (e _non_ come fallback generico per l'autenticazione pass-through).</span><span class="sxs-lookup"><span data-stu-id="1f400-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="1f400-124">Se questi scenari non sono necessari, disabilitare la sincronizzazione dell'hash della password.</span><span class="sxs-lookup"><span data-stu-id="1f400-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f400-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1f400-125">Next steps</span></span>
- <span data-ttu-id="1f400-126">[**Guida introduttiva**](active-directory-aadconnect-pass-through-authentication-quick-start.md): avvio ed esecuzione dell'autenticazione pass-through di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f400-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="1f400-127">[**Approfondimento tecnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): informazioni sul funzionamento di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1f400-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="1f400-128">[**Domande frequenti**](active-directory-aadconnect-pass-through-authentication-faq.md): risposte alle domande più frequenti.</span><span class="sxs-lookup"><span data-stu-id="1f400-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="1f400-129">[**Risoluzione dei problemi**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md): informazioni su come risolvere i problemi comuni relativi a questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1f400-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="1f400-130">[**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.</span><span class="sxs-lookup"><span data-stu-id="1f400-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="1f400-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1f400-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
