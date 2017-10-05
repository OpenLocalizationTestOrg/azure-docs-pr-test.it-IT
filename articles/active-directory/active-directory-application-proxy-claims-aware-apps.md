---
title: App in grado di riconoscere attestazioni - Proxy di applicazione di Azure AD | Documentazione Microsoft
description: Come pubblicare applicazioni ASP.NET locali che accettano le attestazioni di AD FS per l'accesso remoto sicuro da parte degli utenti.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="bce0e-103">Uso di app in grado di riconoscere attestazioni nel proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="bce0e-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="bce0e-104">Le [app in grado di riconoscere attestazioni](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) eseguono un reindirizzamento al servizio token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bce0e-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="bce0e-105">Il servizio token di sicurezza richiede le credenziali all'utente in cambio di un token e quindi reindirizza l'utente all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bce0e-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="bce0e-106">È possibile consentire al proxy di applicazione di usare questi reindirizzamenti in diversi modi.</span><span class="sxs-lookup"><span data-stu-id="bce0e-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="bce0e-107">Usare questo articolo per configurare la distribuzione per app in grado di riconoscere attestazioni.</span><span class="sxs-lookup"><span data-stu-id="bce0e-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bce0e-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bce0e-108">Prerequisites</span></span>
<span data-ttu-id="bce0e-109">Assicurarsi che il servizio token di sicurezza cui viene reindirizzata l'app in grado di riconoscere attestazioni sia disponibile esternamente alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="bce0e-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="bce0e-110">Per rendere disponibile il servizio token di sicurezza, è possibile esporlo tramite un proxy o consentire le connessioni esterne.</span><span class="sxs-lookup"><span data-stu-id="bce0e-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="bce0e-111">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="bce0e-111">Publish your application</span></span>

1. <span data-ttu-id="bce0e-112">Pubblicare l'applicazione seguendo le istruzioni contenute in [Pubblicare le applicazioni con il proxy di applicazione](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bce0e-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="bce0e-113">Passare alla pagina dell'applicazione nel portale e selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bce0e-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="bce0e-114">Se si sceglie **Azure Active Directory** come **Metodo di autenticazione preliminare**, selezionare **Single Sign-On di Azure AD disabilitato** come **Metodo di autenticazione interna**.</span><span class="sxs-lookup"><span data-stu-id="bce0e-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="bce0e-115">Se si sceglie **Pass-through** come **Metodo di autenticazione preliminare**, non è necessario apportare alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="bce0e-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="bce0e-116">Configurare AD FS</span><span class="sxs-lookup"><span data-stu-id="bce0e-116">Configure ADFS</span></span>

<span data-ttu-id="bce0e-117">È possibile configurare AD FS per le app in grado di riconoscere attestazioni in due modi diversi.</span><span class="sxs-lookup"><span data-stu-id="bce0e-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="bce0e-118">Il primo consiste nell'usare domini personalizzati.</span><span class="sxs-lookup"><span data-stu-id="bce0e-118">The first is by using custom domains.</span></span> <span data-ttu-id="bce0e-119">Il secondo è con WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="bce0e-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="bce0e-120">Opzione 1: domini personalizzati</span><span class="sxs-lookup"><span data-stu-id="bce0e-120">Option 1: Custom domains</span></span>

<span data-ttu-id="bce0e-121">Se tutti gli URL interni per le applicazioni sono nomi di dominio completi (FQDN), è possibile configurare [domini personalizzati](active-directory-application-proxy-custom-domains.md) per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bce0e-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="bce0e-122">Usare i domini personalizzati per creare URL esterni identici agli URL interni.</span><span class="sxs-lookup"><span data-stu-id="bce0e-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="bce0e-123">Se gli URL esterni corrispondono agli URL interni, i reindirizzamenti del servizio token di sicurezza funzionano indipendentemente dal fatto che gli utenti siano in locale o in remoto.</span><span class="sxs-lookup"><span data-stu-id="bce0e-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="bce0e-124">Opzione 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="bce0e-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="bce0e-125">Aprire la console di gestione di AD FS.</span><span class="sxs-lookup"><span data-stu-id="bce0e-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="bce0e-126">Passare a **Attendibilità componente**, fare clic con il pulsante destro del mouse sull'app da pubblicare con il proxy dell'applicazione e quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="bce0e-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Schermata: clic con il pulsante destro del mouse sul nome dell'app in Attendibilità componente](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="bce0e-128">Nella scheda **Endpoint** selezionare **WS-Federation** in **Tipo di endpoint**.</span><span class="sxs-lookup"><span data-stu-id="bce0e-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="bce0e-129">In **URL attendibile** specificare l'URL immesso in **URL esterno** nel proxy di applicazione e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bce0e-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Schermata: aggiunta di un endpoint e impostazione del valore per URL attendibile](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="bce0e-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bce0e-131">Next steps</span></span>
* <span data-ttu-id="bce0e-132">[Abilitare Single Sign-On](application-proxy-sso-overview.md) per le applicazioni che non sono in grado di riconoscere attestazioni</span><span class="sxs-lookup"><span data-stu-id="bce0e-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="bce0e-133">Abilitare le app client native per l'interazione con applicazioni proxy</span><span class="sxs-lookup"><span data-stu-id="bce0e-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


