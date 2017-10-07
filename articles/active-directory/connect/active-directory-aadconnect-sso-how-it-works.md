---
title: 'Azure AD Connect: funzionamento dell''accesso Single Sign-On facile | Microsoft Docs'
description: "In questo articolo viene descritto il funzionamento hello Azure Active Directory trasparente funzionalità Single Sign-On."
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
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="4c174-104">Accesso Single Sign-On facile di Azure Active Directory: approfondimento tecnico</span><span class="sxs-lookup"><span data-stu-id="4c174-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="4c174-105">Questo articolo riporta i dettagli tecnici in hello Azure Active Directory trasparente Single Sign-On (SSO trasparente) funzionamento.</span><span class="sxs-lookup"><span data-stu-id="4c174-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="4c174-106">caratteristica di SSO trasparente Hello è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="4c174-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="4c174-107">Come opera la SSO facille?</span><span class="sxs-lookup"><span data-stu-id="4c174-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="4c174-108">In questa sezione presenta due parti tooit:</span><span class="sxs-lookup"><span data-stu-id="4c174-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="4c174-109">Hello il programma di installazione della funzionalità SSO trasparente hello.</span><span class="sxs-lookup"><span data-stu-id="4c174-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="4c174-110">Funzionamento di una transazione di accesso utente singolo con SSO facile.</span><span class="sxs-lookup"><span data-stu-id="4c174-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="4c174-111">Installazione</span><span class="sxs-lookup"><span data-stu-id="4c174-111">How does set up work?</span></span>

<span data-ttu-id="4c174-112">L'accesso SSO facile viene abilitato con Azure AD Connect, come illustrato [qui](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="4c174-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="4c174-113">Durante l'abilitazione di funzionalità hello, si verifica hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4c174-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="4c174-114">Un account computer denominato `AZUREADSSOACCT`, che rappresenta Azure AD, viene creato in Active Directory (AD) locale.</span><span class="sxs-lookup"><span data-stu-id="4c174-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="4c174-115">chiave di decrittografia Kerberos dell'account del computer Hello è condivisa in modo sicuro con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c174-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="4c174-116">Inoltre, due Kerberos nomi dell'entità servizio (SPN) vengono creati due URL toorepresent utilizzati durante l'accesso AD Azure.</span><span class="sxs-lookup"><span data-stu-id="4c174-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="4c174-117">vengono creati account di computer Hello e i nomi SPN Kerberos hello in ogni foresta di Active Directory si sincronizza tooAzure Active Directory (tramite Azure AD Connect) e per gli utenti di cui si desidera SSO senza problemi.</span><span class="sxs-lookup"><span data-stu-id="4c174-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="4c174-118">Spostare hello `AZUREADSSOACCT` tooan account computer unità Organizzativa in cui sono archiviate tooensure che è gestito in altri account di computer hello stesso modo e non viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="4c174-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="4c174-119">È consigliabile si [rollover chiave di decrittografia Kerberos hello](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) di hello `AZUREADSSOACCT` account computer almeno ogni 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="4c174-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="4c174-120">Funzionamento dell'accesso SSO facile</span><span class="sxs-lookup"><span data-stu-id="4c174-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="4c174-121">Una volta completata l'installazione di hello, SSO trasparente funziona hello stesso modo di qualsiasi altra Accedi che utilizza l'autenticazione integrata di Windows (IWA).</span><span class="sxs-lookup"><span data-stu-id="4c174-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="4c174-122">flusso Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="4c174-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="4c174-123">utente di Hello tenta tooaccess un'applicazione (ad esempio, hello Outlook Web App - https://outlook.office365.com/owa/) da un dispositivo azienda appartenenti a un dominio all'interno della rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="4c174-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="4c174-124">Se l'utente hello non è già effettuato l'accesso, utente hello è reindirizzato toohello Azure AD nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="4c174-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="4c174-125">Se hello Azure AD Accedi richiesta include un `domain_hint` (identificazione del tenant, ad esempio, contoso.onmicrosoft.com) o `login_hint` (identificazione utente hello - ad esempio, user@contoso.onmicrosoft.com o user@contoso.com) parametro, quindi il passaggio 2 è stata ignorata.</span><span class="sxs-lookup"><span data-stu-id="4c174-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="4c174-126">tipi di utente Hello in nome utente nella pagina di accesso hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c174-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="4c174-127">Utilizzo di JavaScript nel background hello, il Azure AD richiede browser hello, tramite una risposta 401 non autorizzato, tooprovide un ticket Kerberos.</span><span class="sxs-lookup"><span data-stu-id="4c174-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="4c174-128">browser Hello, a sua volta, richiede un ticket da Active Directory per hello `AZUREADSSOACCT` account computer (rappresentato da Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c174-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="4c174-129">Active Directory individua account computer hello e restituisce un browser toohello del ticket Kerberos crittografato con la chiave privata dell'account del computer hello.</span><span class="sxs-lookup"><span data-stu-id="4c174-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="4c174-130">browser Hello inoltra il ticket Kerberos hello acquisito da Active Directory tooAzure Active Directory (in uno dei hello [gli URL di Azure Active Directory aggiunti in precedenza le impostazioni di zona Intranet del browser toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="4c174-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="4c174-131">Azure AD esegue la decrittografia hello ticket Kerberos, che include l'identità di hello dell'utente hello effettuato l'accesso a dispositivi aziendali hello, utilizzate in precedenza hello di chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="4c174-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="4c174-132">Dopo aver valutato, Azure Active Directory restituisce una token toohello indietro di applicazione o chiede hello utente tooperform prove aggiuntive, ad esempio multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="4c174-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="4c174-133">Se hello utente Accedi ha esito positivo, l'utente hello è tooaccess in grado di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="4c174-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="4c174-134">Hello diagramma seguente illustra tutti i componenti di hello e hello passaggi della procedura.</span><span class="sxs-lookup"><span data-stu-id="4c174-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Seamless Single Sign-On](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="4c174-136">SSO trasparente è opportunistico, vale a dire in caso contrario, esperienza di accesso hello fallback comportamento normale tooits - ad esempio, hello utente deve tooenter toosign le password in.</span><span class="sxs-lookup"><span data-stu-id="4c174-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c174-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c174-137">Next steps</span></span>

- <span data-ttu-id="4c174-138">[**Guida introduttiva**](active-directory-aadconnect-sso-quick-start.md): avvio ed esecuzione di Accesso SSO facile di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c174-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="4c174-139">[**Domande frequenti su** ](active-directory-aadconnect-sso-faq.md) -risposte toofrequently domande frequenti.</span><span class="sxs-lookup"><span data-stu-id="4c174-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="4c174-140">[**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-sso.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="4c174-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="4c174-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4c174-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
