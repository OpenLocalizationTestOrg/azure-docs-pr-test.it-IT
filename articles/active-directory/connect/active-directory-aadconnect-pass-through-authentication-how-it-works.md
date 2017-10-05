---
title: 'Azure AD Connect: funzionamento dell''autenticazione pass-through | Microsoft Docs'
description: Questo articolo descrive il funzionamento dell'autenticazione pass-through di Azure Active Directory.
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
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: d34ccd40082edbe036d963ad548bff648119bdd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="f8ef4-105">Autenticazione pass-through di Azure Active Directory: approfondimento tecnico</span><span class="sxs-lookup"><span data-stu-id="f8ef4-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="f8ef4-106">L'autenticazione pass-through di Azure AD è attualmente in fase di anteprima.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="f8ef4-107">Funzionamento dell'autenticazione pass-through di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8ef4-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="f8ef4-108">Quando un utente tenta di accedere a un'applicazione Azure Active Directory (Azure AD), se l'autenticazione pass-through è abilitata nel tenant, si verificano i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8ef4-108">When a user attempts to sign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on the tenant, the following steps occur:</span></span>

1. <span data-ttu-id="f8ef4-109">L'utente tenta di accedere a un'applicazione, ad esempio a Outlook Web App, https://outlook.office365.com/owa/.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-109">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="f8ef4-110">Se l'utente non ha ancora eseguito l'accesso, viene reindirizzato alla pagina di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-110">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>
3. <span data-ttu-id="f8ef4-111">L'utente immette il nome utente e la password nella pagina di accesso di Azure AD e fa clic sul pulsante "Accedi".</span><span class="sxs-lookup"><span data-stu-id="f8ef4-111">The user enters their username and password into the Azure AD sign-in page and clicks the "Sign in" button.</span></span>
4. <span data-ttu-id="f8ef4-112">Quando riceve la richiesta di accesso, Azure AD inserisce il nome utente e la password, crittografata con una chiave pubblica, in una coda.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-112">Azure AD, on receiving the sign-in request, places the username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="f8ef4-113">Un agente di autenticazione pass-through locale esegue una chiamata in uscita alla coda e recupera il nome utente e la password crittografata.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-113">An on-premises Pass-through Authentication agent makes an outbound call to the queue and retrieves the username and encrypted password.</span></span>
6. <span data-ttu-id="f8ef4-114">L'agente decrittografa la password tramite la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-114">The agent decrypts the password using its private key.</span></span>
7. <span data-ttu-id="f8ef4-115">L'agente convalida quindi il nome utente e la password in Active Directory usando le API Windows standard. Questo meccanismo è simile a quello usato da Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-115">The agent then validates the username and password against Active Directory using standard Windows APIs (a similar mechanism to what is used by Active Directory Federation Services).</span></span> <span data-ttu-id="f8ef4-116">Il nome utente può essere il nome utente predefinito locale (in genere `userPrincipalName`) o un altro attributo configurato in Azure AD Connect (noto come `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="f8ef4-116">The username can be either the on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="f8ef4-117">Il controller di dominio (DC, Domain Controller) di Active Directory locale valuta quindi la richiesta e restituisce all'agente la risposta appropriata che può essere esito positivo, errore, password scaduta o utente bloccato.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-117">The on-premises Active Directory Domain Controller (DC) then evaluates the request and returns the appropriate response (success, failure, password expired or user locked out) to the agent.</span></span>
9. <span data-ttu-id="f8ef4-118">L'agente, a sua volta, restituisce la risposta ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-118">The agent, in turn, returns this response back to Azure AD.</span></span>
10. <span data-ttu-id="f8ef4-119">Azure AD valuta la risposta e risponde all'utente come appropriato. Ad esempio, consente l'accesso immediato dell'utente o richiede l'autenticazione a più fattori (MFA, Multi-Factor Authentication).</span><span class="sxs-lookup"><span data-stu-id="f8ef4-119">Azure AD evaluates the response and responds to the user as appropriate - for example, it either signs the user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="f8ef4-120">Se l'accesso dell'utente ha esito positivo, l'utente può accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-120">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="f8ef4-121">Il diagramma seguente illustra tutti i componenti e i passaggi interessati.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-121">The following diagram illustrates all the components and the steps involved.</span></span>

![Autenticazione pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="f8ef4-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f8ef4-123">Next steps</span></span>
- <span data-ttu-id="f8ef4-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) (Limitazioni correnti): questa funzionalità è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="f8ef4-125">Informazioni su quali scenari sono supportati e quali non lo sono.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="f8ef4-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication (Guida introduttiva: avvio ed esecuzione dell'autenticazione pass-through di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8ef4-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="f8ef4-127">[**Domande frequenti**](active-directory-aadconnect-pass-through-authentication-faq.md): risposte alle domande più frequenti.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="f8ef4-128">[**Risoluzione dei problemi**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md): informazioni su come risolvere i problemi comuni relativi a questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="f8ef4-129">[**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="f8ef4-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f8ef4-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
