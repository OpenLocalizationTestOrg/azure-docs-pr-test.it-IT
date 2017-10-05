---
title: 'Pubblicare app client native: Azure AD | Microsoft Docs'
description: Illustra come abilitare la comunicazione tra le app client native e il connettore del proxy di applicazione di Azure AD per consentire l'accesso remoto sicuro alle app locali.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="3b264-103">Come abilitare le app client native per l'interazione con le applicazioni proxy</span><span class="sxs-lookup"><span data-stu-id="3b264-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="3b264-104">Oltre che per applicazioni Web, è possibile usare il proxy di applicazione di Azure Active Directory per pubblicare app client native.</span><span class="sxs-lookup"><span data-stu-id="3b264-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="3b264-105">Le app client native si differenziano dalle app Web perché vengono installate su un dispositivo, mentre le app Web sono accessibili tramite un browser.</span><span class="sxs-lookup"><span data-stu-id="3b264-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="3b264-106">Il proxy di applicazione supporta le app client native accettando token rilasciati da Azure AD e inviati in intestazioni HTTP Authorize standard.</span><span class="sxs-lookup"><span data-stu-id="3b264-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relazione tra utenti finali, Azure Active Directory e applicazioni pubblicate](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="3b264-108">Per pubblicare applicazioni native, usare Azure AD Authentication Library, che gestisce l'autenticazione e supporta molti ambienti client.</span><span class="sxs-lookup"><span data-stu-id="3b264-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="3b264-109">Il proxy di applicazione si integra con [lo scenario Da applicazione nativa ad API Web](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="3b264-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="3b264-110">Questo articolo illustra i quattro passaggi necessari per pubblicare un'applicazione nativa con il proxy di applicazione e Azure AD Authentication Library.</span><span class="sxs-lookup"><span data-stu-id="3b264-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="3b264-111">Passaggio 1: Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="3b264-111">Step 1: Publish your application</span></span>
<span data-ttu-id="3b264-112">Pubblicare l'applicazione proxy come qualsiasi altra applicazione e assegnare agli utenti l'accesso all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3b264-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="3b264-113">Per altre informazioni, vedere [Pubblicare applicazioni mediante il proxy di applicazione](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="3b264-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="3b264-114">Passaggio 2: Configurare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="3b264-114">Step 2: Configure your application</span></span>
<span data-ttu-id="3b264-115">Configurare l'applicazione nativa come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3b264-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="3b264-116">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b264-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3b264-117">Passare ad **Azure Active Directory** > **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="3b264-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="3b264-118">Selezionare **Registrazione nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="3b264-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="3b264-119">Specificare un nome, selezionare **Nativa** come tipo di applicazione e immettere l'URI di reindirizzamento per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3b264-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![Creare una nuova registrazione di app](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="3b264-121">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3b264-121">Select **Create**.</span></span>

<span data-ttu-id="3b264-122">Per informazioni più dettagliate sulla creazione di una nuova registrazione di app, vedere [Integrazione di applicazioni con Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="3b264-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="3b264-123">Passaggio 3: Concedi accesso ad altre applicazioni</span><span class="sxs-lookup"><span data-stu-id="3b264-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="3b264-124">Abilitare l'applicazione nativa da esporre ad altre applicazioni nella directory:</span><span class="sxs-lookup"><span data-stu-id="3b264-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="3b264-125">In **Registrazioni per l'app** selezionare la nuova applicazione nativa appena creata.</span><span class="sxs-lookup"><span data-stu-id="3b264-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="3b264-126">Selezionare **Autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="3b264-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="3b264-127">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3b264-127">Select **Add**.</span></span>
4. <span data-ttu-id="3b264-128">Aprire il primo passaggio, **Selezionare un'API**.</span><span class="sxs-lookup"><span data-stu-id="3b264-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="3b264-129">Usare la barra di ricerca per trovare l'app del proxy di applicazione pubblicata nella prima sezione.</span><span class="sxs-lookup"><span data-stu-id="3b264-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="3b264-130">Scegliere tale app e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="3b264-130">Choose that app, then click **Select**.</span></span> 

   ![Cercare l'app proxy](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="3b264-132">Aprire il secondo passaggio, **Selezionare le autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="3b264-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="3b264-133">Usare la casella di controllo per concedere all'applicazione proxy l'accesso all'applicazione nativa e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="3b264-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![Concedere l'accesso all'app proxy](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="3b264-135">Selezionare **Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="3b264-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="3b264-136">Passaggio 4: Modificare Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="3b264-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="3b264-137">Modificare il codice dell'applicazione nativa nel contesto di autenticazione di Active Directory Authentication Library (ADAL) per includere il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="3b264-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="3b264-138">Le variabili nel codice di esempio devono essere sostituite come segue:</span><span class="sxs-lookup"><span data-stu-id="3b264-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="3b264-139">Il valore di **Tenant ID** è riportato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b264-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="3b264-140">Passare ad **Azure Active Directory** > **Proprietà** e copiare l'ID directory.</span><span class="sxs-lookup"><span data-stu-id="3b264-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="3b264-141">Il valore di **External URL** è l'URL front-end immesso nell'applicazione proxy.</span><span class="sxs-lookup"><span data-stu-id="3b264-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="3b264-142">Per trovare questo valore, passare alla sezione **Proxy dell'applicazione** dell'app proxy.</span><span class="sxs-lookup"><span data-stu-id="3b264-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="3b264-143">Il valore di **App ID of the Native app** è riportato nella pagina **Proprietà** dell'applicazione nativa.</span><span class="sxs-lookup"><span data-stu-id="3b264-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="3b264-144">Il valore di **Redirect URI of the native app** è riportato nella pagina **URI di reindirizzamento** dell'applicazione nativa.</span><span class="sxs-lookup"><span data-stu-id="3b264-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="3b264-145">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3b264-145">See also</span></span>

<span data-ttu-id="3b264-146">Per altre informazioni sul flusso delle applicazioni native, vedere [Da applicazione nativa ad API Web](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="3b264-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="3b264-147">Per le notizie e gli aggiornamenti più recenti, vedere [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="3b264-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
