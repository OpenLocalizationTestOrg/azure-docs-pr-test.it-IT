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
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="a5ab7-105">Autenticazione pass-through di Azure Active Directory: approfondimento tecnico</span><span class="sxs-lookup"><span data-stu-id="a5ab7-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="a5ab7-106">L'autenticazione pass-through di Azure AD è attualmente in fase di anteprima.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="a5ab7-107">Funzionamento dell'autenticazione pass-through di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5ab7-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="a5ab7-108">Quando un utente tenta di toosign in un'applicazione protetta da Azure Active Directory (Azure AD) e se l'autenticazione pass-through è abilitato nel tenant di hello, hello si verificano i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a5ab7-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="a5ab7-109">utente di Hello tenta tooaccess un'applicazione (ad esempio, hello Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="a5ab7-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="a5ab7-110">Se l'utente hello non è già effettuato l'accesso, utente hello è reindirizzato toohello Azure AD nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="a5ab7-111">Hello immesso nome utente e password nella pagina di accesso AD Azure hello e fa clic sul pulsante "Accedi" hello.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="a5ab7-112">Azure AD, alla ricezione di hello richiesta di accesso, posiziona hello username e password (crittografata utilizzando una chiave pubblica) in una coda.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="a5ab7-113">Un agente autenticazione pass-through locali rende una coda toohello chiamata in uscita e recupera hello username e password crittografata.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="a5ab7-114">agente Hello decrittografa password hello utilizzando la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="a5ab7-115">agente Hello viene quindi convalidato hello username e password in Active Directory utilizzando le API Windows standard (un toowhat meccanismo simili è utilizzato da Active Directory Federation Services).</span><span class="sxs-lookup"><span data-stu-id="a5ab7-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="a5ab7-116">Hello nome utente può essere un nome utente predefinito di hello locale (in genere `userPrincipalName`) o un altro attributo configurata in Azure AD Connect (noto come `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="a5ab7-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="a5ab7-117">Controller di dominio Active Directory (DC) locale Hello quindi valuta hello richiesta e restituisce hello risposta appropriata (esito positivo, l'errore, password scaduta o utente bloccato) toohello agente.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="a5ab7-118">agente Hello, a sua volta, restituisce questo tooAzure indietro risposta annuncio.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="a5ab7-119">Azure AD restituisce una risposta hello e risponde toohello utente come appropriato: ad esempio, effettua l'accesso utente hello immediatamente o richieste per multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="a5ab7-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="a5ab7-120">Se hello utente Accedi ha esito positivo, l'utente hello è tooaccess in grado di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="a5ab7-121">Hello diagramma seguente illustra tutti i componenti di hello e hello passaggi della procedura.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Autenticazione pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="a5ab7-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5ab7-123">Next steps</span></span>
- <span data-ttu-id="a5ab7-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) (Limitazioni correnti): questa funzionalità è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="a5ab7-125">Informazioni su quali scenari sono supportati e quali non lo sono.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="a5ab7-126">[**Guida introduttiva**](active-directory-aadconnect-pass-through-authentication-quick-start.md): avvio ed esecuzione dell'autenticazione pass-through di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="a5ab7-127">[**Domande frequenti su** ](active-directory-aadconnect-pass-through-authentication-faq.md) -risposte toofrequently domande frequenti.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="a5ab7-128">[**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="a5ab7-129">[**Seamless Single Sign-On di Azure AD**](active-directory-aadconnect-sso.md): altre informazioni su questa funzionalità complementare.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="a5ab7-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a5ab7-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
