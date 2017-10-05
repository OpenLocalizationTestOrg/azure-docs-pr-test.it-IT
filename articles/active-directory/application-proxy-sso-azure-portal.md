---
title: Accedere con Single Sign-On alle app con il proxy dell'applicazione Azure AD | Microsoft Docs
description: Attivare il Single Sign-On per le applicazioni pubblicate locali con il proxy dell'applicazione Azure AD nel portale di Azure.
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
ms.openlocfilehash: 9ddc0c1bd5f2cbb24f6761cfd041b820ee6464b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="0397c-103">Insieme di credenziali delle password per l'accesso Single Sign-On con il proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="0397c-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="0397c-104">Il proxy dell'applicazione Azure Active Directory consente di migliorare la produttività pubblicando le applicazioni locali in modo che possano accedervi anche i dipendenti remoti.</span><span class="sxs-lookup"><span data-stu-id="0397c-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="0397c-105">Nel portale di Azure è inoltre possibile configurare l'accesso Single Sign-On (SSO) per queste applicazioni.</span><span class="sxs-lookup"><span data-stu-id="0397c-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="0397c-106">Gli utenti devono solo eseguire l'autenticazione con Azure AD e possono accedere all'applicazione aziendale senza dover eseguire nuovamente l'accesso.</span><span class="sxs-lookup"><span data-stu-id="0397c-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="0397c-107">Il proxy dell'applicazione supporta numerose [modalità Single Sign-On](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0397c-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="0397c-108">L'accesso basato su password è progettato per le applicazioni che usano una combinazione di nome utente/password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="0397c-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="0397c-109">Quando si configura l'accesso basato su password per l'applicazione, gli utenti devono accedere all'applicazione locale una volta.</span><span class="sxs-lookup"><span data-stu-id="0397c-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="0397c-110">Successivamente, Azure Active Directory archivia le informazioni di accesso e le fornisce automaticamente all'applicazione quando l'utente accede in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="0397c-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="0397c-111">Si presuppone che l'utente abbia già pubblicato e testato l'app con il proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0397c-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="0397c-112">In caso contrario, seguire i passaggi in [Pubblicare applicazioni tramite il proxy di applicazione AD Azure](application-proxy-publish-azure-portal.md) prima di tornare a questo punto.</span><span class="sxs-lookup"><span data-stu-id="0397c-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="0397c-113">Configurare l'insieme di credenziali delle password per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="0397c-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="0397c-114">Accedere al [portale di Azure](https://portal.azure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0397c-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="0397c-115">Selezionare **Azure Active Directory** > **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0397c-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="0397c-116">Nell'elenco a discesa selezionare l'app da configurare con la funzione SSO.</span><span class="sxs-lookup"><span data-stu-id="0397c-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="0397c-117">Selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0397c-117">Select **Single sign-on**.</span></span>

   ![Selezionare Single Sign-On](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="0397c-119">Per la modalità SSO, scegliere **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="0397c-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="0397c-120">Per l'URL di accesso, inserire l'URL della pagina in cui gli utenti immettono nome utente e password per accedere all'app fuori dalla rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="0397c-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="0397c-121">Potrebbe trattarsi dell'URL esterno creato dopo aver pubblicato l'app tramite il proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0397c-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![Scegliere l'accesso basato su password e immettere l'URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="0397c-123">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0397c-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="0397c-124">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="0397c-124">Test your app</span></span>

<span data-ttu-id="0397c-125">Passare all'URL esterno che è stato configurato per l'accesso remoto all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0397c-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="0397c-126">Accedere con le credenziali dell'app (o con le credenziali di un account di prova per cui è stato configurato l'accesso).</span><span class="sxs-lookup"><span data-stu-id="0397c-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="0397c-127">Dopo l'accesso, dovrebbe essere possibile lasciare l'app e tornare senza dover immettere nuovamente le credenziali.</span><span class="sxs-lookup"><span data-stu-id="0397c-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0397c-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0397c-128">Next steps</span></span>

- <span data-ttu-id="0397c-129">Altri modi per implementare l'accesso [Single Sign-On con il proxy di applicazione](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0397c-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="0397c-130">Informazioni sulle [Considerazioni relative alla sicurezza quando si accede alle app in remoto usando il proxy applicazione di Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="0397c-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>