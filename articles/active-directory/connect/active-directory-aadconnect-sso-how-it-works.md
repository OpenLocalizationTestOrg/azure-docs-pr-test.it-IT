---
title: 'Azure AD Connect: funzionamento dell''accesso Single Sign-On facile | Microsoft Docs'
description: In questo articolo viene descritto il funzionamento dell'accesso Single Sign-On facile di Azure Active Directory.
services: active-directory
keywords: "che cos'è Azure AD Connect, installare Active Directory, componenti richiesti per Azure AD, SSO, Single Sign-On"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: f0bcbdb03fbb70ff91ac3a56974a88eb1b26c245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="c2a1e-104">Accesso Single Sign-On facile di Azure Active Directory: approfondimento tecnico</span><span class="sxs-lookup"><span data-stu-id="c2a1e-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="c2a1e-105">Questo articolo riporta i dettagli tecnici del funzionamento dell'accesso Single Sign-On (SSO) facile di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c2a1e-106">La funzionalità Accesso Single Sign-On facile è attualmente in fase di anteprima.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-106">The Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="c2a1e-107">Come opera la SSO facille?</span><span class="sxs-lookup"><span data-stu-id="c2a1e-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="c2a1e-108">Questa sezione è composta da due parti:</span><span class="sxs-lookup"><span data-stu-id="c2a1e-108">This section has two parts to it:</span></span>
1. <span data-ttu-id="c2a1e-109">Installazione della funzionalità di accesso SSO facile.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-109">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="c2a1e-110">Funzionamento di una transazione di accesso utente singolo con SSO facile.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="c2a1e-111">Installazione</span><span class="sxs-lookup"><span data-stu-id="c2a1e-111">How does set up work?</span></span>

<span data-ttu-id="c2a1e-112">L'accesso SSO facile viene abilitato con Azure AD Connect, come illustrato [qui](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="c2a1e-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="c2a1e-113">Durante l'abilitazione della funzionalità, si verificano i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2a1e-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="c2a1e-114">Un account computer denominato `AZUREADSSOACCT`, che rappresenta Azure AD, viene creato in Active Directory (AD) locale.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="c2a1e-115">La chiave di decrittografia Kerberos dell'account computer viene condivisa in modo sicuro con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="c2a1e-116">Vengono anche creati due nomi dell'entità servizio (SPN, Service Principal Name) Kerberos per rappresentare due URL usati durante l'accesso ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-116">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="c2a1e-117">L'account computer e gli SPN Kerberos vengono creati in ogni foresta di AD che si sincronizza con Azure AD, tramite Azure AD Connect, e per i cui utenti si vuole abilitare l'accesso SSO facile.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-117">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="c2a1e-118">Spostare l'account computer `AZUREADSSOACCT` in un'unità organizzativa in cui sono archiviati altri account computer per assicurarsi che venga gestito allo stesso modo e non venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-118">Move the `AZUREADSSOACCT` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c2a1e-119">È consigliabile [rinnovare la chiave di decrittografia di Kerberos](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) dell'account computer `AZUREADSSOACCT` almeno ogni 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-119">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of the `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="c2a1e-120">Funzionamento dell'accesso SSO facile</span><span class="sxs-lookup"><span data-stu-id="c2a1e-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="c2a1e-121">Una volta completata l'installazione, l'accesso SSO facile funziona esattamente come qualsiasi altro accesso che usa l'autenticazione integrata di Windows (NTLM).</span><span class="sxs-lookup"><span data-stu-id="c2a1e-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="c2a1e-122">Il flusso è il seguente:</span><span class="sxs-lookup"><span data-stu-id="c2a1e-122">The flow is as follows:</span></span>

1. <span data-ttu-id="c2a1e-123">L'utente tenta di accedere a un'applicazione, ad esempio Outlook Web App, https://outlook.office365.com/owa/, da un dispositivo aziendale appartenente a un dominio all'interno della rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-123">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="c2a1e-124">Se l'utente non ha ancora eseguito l'accesso, viene reindirizzato alla pagina di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-124">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="c2a1e-125">Se la richiesta di accesso ad Azure AD include il parametro `domain_hint` che identifica il tenant, ad esempio contoso.onmicrosoft.com, o il parametro `login_hint` che identifica l'utente, ad esempio user@contoso.onmicrosoft.com o user@contoso.com, il passaggio 2 viene saltato.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-125">If the Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying the user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="c2a1e-126">L'utente digita il nome utente nella pagina di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-126">The user types in their user name into the Azure AD sign-in page.</span></span>
4. <span data-ttu-id="c2a1e-127">Tramite l'uso di JavaScript in background, Azure AD richiede al browser, tramite una risposta di tipo 401 Non autorizzato, di specificare un ticket Kerberos.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-127">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="c2a1e-128">Il browser, a sua volta, richiede un ticket ad Active Directory per l'account computer `AZUREADSSOACCT` che rappresenta Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-128">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="c2a1e-129">Active Directory individua l'account computer e restituisce un ticket Kerberos al browser, crittografato con il segreto dell'account computer.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-129">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="c2a1e-130">Il browser inoltra il ticket Kerberos acquisito da Active Directory ad Azure AD in uno degli [URL di Azure AD aggiunti in precedenza nelle impostazioni dell'area Intranet del browser](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature).</span><span class="sxs-lookup"><span data-stu-id="c2a1e-130">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD (on one of the [Azure AD URLs previously added to the browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="c2a1e-131">Azure AD esegue la decrittografia del ticket Kerberos, che include l'identità dell'utente connesso al dispositivo aziendale, usando la chiave già condivisa.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-131">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="c2a1e-132">Dopo la valutazione, Azure AD restituisce un token all'applicazione oppure chiede all'utente di eseguire prove aggiuntive, ad esempio l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-132">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="c2a1e-133">Se l'accesso dell'utente ha esito positivo, l'utente può accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-133">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="c2a1e-134">Il diagramma seguente illustra tutti i componenti e i passaggi interessati.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-134">The following diagram illustrates all the components and the steps involved.</span></span>

![Seamless Single Sign-On](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="c2a1e-136">L'accesso SSO facile è una funzionalità opportunistica, il che significa che, se ha esito negativo, l'esperienza di accesso dell'utente ritorna al comportamento normale, ovvero l'utente dovrà immettere la propria password per eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-136">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2a1e-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2a1e-137">Next steps</span></span>

- <span data-ttu-id="c2a1e-138">[**Guida introduttiva**](active-directory-aadconnect-sso-quick-start.md): avvio ed esecuzione di Accesso SSO facile di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="c2a1e-139">[**Domande frequenti**](active-directory-aadconnect-sso-faq.md): risposte alle domande più frequenti.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="c2a1e-140">[**Risoluzione dei problemi**](active-directory-aadconnect-troubleshoot-sso.md): informazioni su come risolvere i problemi comuni relativi a questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="c2a1e-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c2a1e-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
