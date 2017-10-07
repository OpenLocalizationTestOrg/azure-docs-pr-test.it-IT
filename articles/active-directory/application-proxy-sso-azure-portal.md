---
title: aaaSingle sign-on tooapps con Proxy dell'applicazione Azure AD | Documenti Microsoft
description: Attivare single sign-on per le applicazioni pubblicate on-premise con Proxy dell'applicazione AD Azure nel portale di Azure hello.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="d38a9-103">Insieme di credenziali delle password per l'accesso Single Sign-On con il proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d38a9-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="d38a9-104">Il proxy dell'applicazione Azure Active Directory consente di migliorare la produttività pubblicando le applicazioni locali in modo che possano accedervi anche i dipendenti remoti.</span><span class="sxs-lookup"><span data-stu-id="d38a9-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="d38a9-105">Nel portale di Azure hello, è possibile impostare single sign-on (SSO) toothese app.</span><span class="sxs-lookup"><span data-stu-id="d38a9-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="d38a9-106">Gli utenti devono solo tooauthenticate con Azure AD, e possa accedere all'applicazione enterprise senza toosign in.</span><span class="sxs-lookup"><span data-stu-id="d38a9-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="d38a9-107">Il proxy dell'applicazione supporta numerose [modalità Single Sign-On](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d38a9-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="d38a9-108">L'accesso basato su password è progettato per le applicazioni che usano una combinazione di nome utente/password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d38a9-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="d38a9-109">Quando si configura basato su password sign-on per l'applicazione, gli utenti devono toosign in toohello nell'applicazione locale una volta.</span><span class="sxs-lookup"><span data-stu-id="d38a9-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="d38a9-110">Successivamente, Azure Active Directory archivia le informazioni di accesso hello e automaticamente fornisce toohello applicazione quando gli utenti accedono in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="d38a9-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="d38a9-111">Si presuppone che l'utente abbia già pubblicato e testato l'app con il proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d38a9-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="d38a9-112">In caso contrario, seguire i passaggi di hello in [pubblicare applicazioni mediante il Proxy di applicazione AD Azure](application-proxy-publish-azure-portal.md) e tornare indietro di seguito.</span><span class="sxs-lookup"><span data-stu-id="d38a9-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="d38a9-113">Configurare l'insieme di credenziali delle password per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="d38a9-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="d38a9-114">Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d38a9-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="d38a9-115">Selezionare **Azure Active Directory** > **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d38a9-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="d38a9-116">Dall'elenco a hello, selezionare l'applicazione hello che si desidera tooset backup con SSO.</span><span class="sxs-lookup"><span data-stu-id="d38a9-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="d38a9-117">Selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d38a9-117">Select **Single sign-on**.</span></span>

   ![Selezionare Single Sign-On](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="d38a9-119">Per la modalità SSO hello, scegliere **basato su Password Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d38a9-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="d38a9-120">Per hello Sign-on URL, immettere hello pagina hello in cui gli utenti immettono toosign loro nome utente e password in app tooyour all'esterno delle rete aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="d38a9-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="d38a9-121">Può trattarsi di un URL esterno che è stato creato quando si pubblica l'applicazione hello mediante il Proxy applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d38a9-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![Scegliere l'accesso basato su password e immettere l'URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="d38a9-123">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d38a9-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="d38a9-124">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="d38a9-124">Test your app</span></span>

<span data-ttu-id="d38a9-125">Vai a URL tooexternal configurato per l'applicazione tooyour di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="d38a9-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="d38a9-126">Accedere con le credenziali per l'app (o le credenziali di hello per un account di prova configurata con accesso).</span><span class="sxs-lookup"><span data-stu-id="d38a9-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="d38a9-127">Dopo l'accesso, deve essere in grado di tooleave hello app e tornare senza dover immettere nuovamente le credenziali.</span><span class="sxs-lookup"><span data-stu-id="d38a9-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d38a9-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d38a9-128">Next steps</span></span>

- <span data-ttu-id="d38a9-129">Informazioni su altri modi tooimplement [Single sign-on con Proxy dell'applicazione](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d38a9-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="d38a9-130">Informazioni sulle [Considerazioni relative alla sicurezza quando si accede alle app in remoto usando il proxy applicazione di Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="d38a9-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>