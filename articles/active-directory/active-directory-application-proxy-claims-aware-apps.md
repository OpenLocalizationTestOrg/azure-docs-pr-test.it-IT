---
title: applicazioni che supportano aaaClaims - Proxy App di Azure AD | Documenti Microsoft
description: Come toopublish locale le applicazioni ASP.NET che accetta le attestazioni ADFS per l'accesso remoto sicuro dagli utenti.
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
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="776e8-103">Uso di app in grado di riconoscere attestazioni nel proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="776e8-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="776e8-104">[Grado di riconoscere attestazioni app](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) eseguire toohello un reindirizzamento la servizio Token di sicurezza (STS).</span><span class="sxs-lookup"><span data-stu-id="776e8-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="776e8-105">servizio token di sicurezza di Hello richiede le credenziali utente hello in cambio un token e quindi reindirizza un'applicazione hello utente toohello.</span><span class="sxs-lookup"><span data-stu-id="776e8-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="776e8-106">Esistono alcuni modi tooenable Proxy dell'applicazione toowork con questi reindirizzamenti.</span><span class="sxs-lookup"><span data-stu-id="776e8-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="776e8-107">Utilizzare la distribuzione di tooconfigure questo articolo per le applicazioni in grado di riconoscere attestazioni.</span><span class="sxs-lookup"><span data-stu-id="776e8-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="776e8-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="776e8-108">Prerequisites</span></span>
<span data-ttu-id="776e8-109">Verificare che tale hello servizio token di sicurezza che hello app grado di riconoscere attestazioni reindirizza toois disponibile di fuori della rete locale.</span><span class="sxs-lookup"><span data-stu-id="776e8-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="776e8-110">Si può rendere hello servizio token di sicurezza disponibili esporlo tramite un proxy o consentendo di fuori di connessioni.</span><span class="sxs-lookup"><span data-stu-id="776e8-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="776e8-111">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="776e8-111">Publish your application</span></span>

1. <span data-ttu-id="776e8-112">Pubblicare l'applicazione in base a istruzioni toohello [pubblicare applicazioni con Proxy dell'applicazione](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="776e8-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="776e8-113">Passare toohello pagina applicazione hello portale e seleziona **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="776e8-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="776e8-114">Se si sceglie **Azure Active Directory** come **Metodo di autenticazione preliminare**, selezionare **Single Sign-On di Azure AD disabilitato** come **Metodo di autenticazione interna**.</span><span class="sxs-lookup"><span data-stu-id="776e8-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="776e8-115">Se si sceglie **pass-through** come il **metodo di preautenticazione**, non è necessario toochange nulla.</span><span class="sxs-lookup"><span data-stu-id="776e8-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="776e8-116">Configurare AD FS</span><span class="sxs-lookup"><span data-stu-id="776e8-116">Configure ADFS</span></span>

<span data-ttu-id="776e8-117">È possibile configurare AD FS per le app in grado di riconoscere attestazioni in due modi diversi.</span><span class="sxs-lookup"><span data-stu-id="776e8-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="776e8-118">Hello per primo è l'utilizzo dei domini personalizzati.</span><span class="sxs-lookup"><span data-stu-id="776e8-118">hello first is by using custom domains.</span></span> <span data-ttu-id="776e8-119">in secondo luogo, Hello è con WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="776e8-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="776e8-120">Opzione 1: domini personalizzati</span><span class="sxs-lookup"><span data-stu-id="776e8-120">Option 1: Custom domains</span></span>

<span data-ttu-id="776e8-121">Se tutti hello URL interni per le applicazioni sono complete (FQDN) dei nomi di dominio, quindi è possibile configurare [domini personalizzati](active-directory-application-proxy-custom-domains.md) per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="776e8-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="776e8-122">Utilizzare hello domini personalizzati toocreate URL esterni che sono hello stesso hello URL interno.</span><span class="sxs-lookup"><span data-stu-id="776e8-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="776e8-123">Quando l'URL esterni corrispondono gli URL interni, reindirizzamenti STS hello funzionano se gli utenti siano in locale o remoto.</span><span class="sxs-lookup"><span data-stu-id="776e8-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="776e8-124">Opzione 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="776e8-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="776e8-125">Aprire la console di gestione di AD FS.</span><span class="sxs-lookup"><span data-stu-id="776e8-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="776e8-126">Andare troppo**Relying Party Trusts**, fare clic su hello app pubblicate con Proxy dell'applicazione e scegliere **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="776e8-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Schermata: clic con il pulsante destro del mouse sul nome dell'app in Attendibilità componente](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="776e8-128">In hello **endpoint** scheda **tipo di Endpoint**selezionare **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="776e8-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="776e8-129">In **attendibili URL**, immettere l'URL hello immesso in hello Proxy dell'applicazione in **URL esterno** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="776e8-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Schermata: aggiunta di un endpoint e impostazione del valore per URL attendibile](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="776e8-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="776e8-131">Next steps</span></span>
* <span data-ttu-id="776e8-132">[Abilitare Single Sign-On](application-proxy-sso-overview.md) per le applicazioni che non sono in grado di riconoscere attestazioni</span><span class="sxs-lookup"><span data-stu-id="776e8-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="776e8-133">Abilitare toointeract di App client nativa con applicazioni di proxy</span><span class="sxs-lookup"><span data-stu-id="776e8-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


