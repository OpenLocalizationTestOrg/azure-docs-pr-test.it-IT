---
title: le applicazioni client native aaaPublish - Azure AD | Documenti Microsoft
description: Descrive come toocommunicate di App client nativa tooenable con Azure Active Directory Application Proxy Connector tooprovide accesso remoto sicuro tooyour locale delle app.
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
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="53c6e-103">Come toointeract di App client nativa tooenable con proxy applicazioni</span><span class="sxs-lookup"><span data-stu-id="53c6e-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="53c6e-104">Nelle applicazioni tooweb aggiunta, il Proxy di applicazione Azure Active Directory può essere anche le applicazioni client native toopublish utilizzato.</span><span class="sxs-lookup"><span data-stu-id="53c6e-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="53c6e-105">Le app client native si differenziano dalle app Web perché vengono installate su un dispositivo, mentre le app Web sono accessibili tramite un browser.</span><span class="sxs-lookup"><span data-stu-id="53c6e-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="53c6e-106">Il proxy di applicazione supporta le app client native accettando token rilasciati da Azure AD e inviati in intestazioni HTTP Authorize standard.</span><span class="sxs-lookup"><span data-stu-id="53c6e-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relazione tra utenti finali, Azure Active Directory e applicazioni pubblicate](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="53c6e-108">Usare Azure AD Authentication Library, che si occupa di autenticazione e supporta molti ambienti client, le applicazioni native toopublish hello.</span><span class="sxs-lookup"><span data-stu-id="53c6e-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="53c6e-109">Proxy dell'applicazione si integra con hello [uno scenario di applicazione nativa tooWeb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="53c6e-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="53c6e-110">In questo articolo illustra hello quattro passaggi toopublish un'applicazione nativa con Proxy dell'applicazione e hello Azure AD Authentication Library.</span><span class="sxs-lookup"><span data-stu-id="53c6e-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="53c6e-111">Passaggio 1: Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="53c6e-111">Step 1: Publish your application</span></span>
<span data-ttu-id="53c6e-112">Pubblicare l'applicazione proxy come qualsiasi altra applicazione e assegnare gli utenti tooaccess l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="53c6e-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="53c6e-113">Per altre informazioni, vedere [Pubblicare applicazioni mediante il proxy di applicazione](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="53c6e-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="53c6e-114">Passaggio 2: Configurare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="53c6e-114">Step 2: Configure your application</span></span>
<span data-ttu-id="53c6e-115">Configurare l'applicazione nativa come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="53c6e-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="53c6e-116">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="53c6e-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="53c6e-117">Passare troppo**Azure Active Directory** > **registrazioni di App**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="53c6e-118">Selezionare **Registrazione nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="53c6e-119">Specificare un nome per l'applicazione, seleziona **nativo** come tipo di applicazione, hello e fornire hello URI di reindirizzamento per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="53c6e-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![Creare una nuova registrazione di app](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="53c6e-121">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-121">Select **Create**.</span></span>

<span data-ttu-id="53c6e-122">Per informazioni più dettagliate sulla creazione di una nuova registrazione di app, vedere [Integrazione di applicazioni con Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="53c6e-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="53c6e-123">Passaggio 3: Applicazioni concedere accesso tooother</span><span class="sxs-lookup"><span data-stu-id="53c6e-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="53c6e-124">Abilitare hello applicazione nativa toobe esposti tooother applicazioni nella directory:</span><span class="sxs-lookup"><span data-stu-id="53c6e-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="53c6e-125">Ancora in **registrazioni di App**, selezionare hello nuova applicazione nativa appena creato.</span><span class="sxs-lookup"><span data-stu-id="53c6e-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="53c6e-126">Selezionare **Autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="53c6e-127">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-127">Select **Add**.</span></span>
4. <span data-ttu-id="53c6e-128">Innanzitutto aprire hello **selezionare un'API**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="53c6e-129">Usare hello ricerca barra toofind hello Proxy di applicazione app pubblicata nella prima sezione hello.</span><span class="sxs-lookup"><span data-stu-id="53c6e-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="53c6e-130">Scegliere tale app e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-130">Choose that app, then click **Select**.</span></span> 

   ![Cercare hello proxy app](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="53c6e-132">Aprire hello secondo passaggio, ovvero **selezionare autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="53c6e-133">Utilizzare hello casella di controllo toogrant applicazione applicazione nativa access tooyour proxy, quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![Concedere accesso tooproxy app](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="53c6e-135">Selezionare **Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="53c6e-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="53c6e-136">Passaggio 4: Modificare hello Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="53c6e-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="53c6e-137">Modificare il codice di applicazione nativa hello in contesto di autenticazione hello di hello tooinclude di Active Directory Authentication Library (ADAL) hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="53c6e-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="53c6e-138">le variabili di Hello nel codice di esempio hello devono essere sostituite come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="53c6e-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="53c6e-139">**ID tenant** è reperibile nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="53c6e-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="53c6e-140">Passare troppo**Azure Active Directory** > **proprietà** e hello copia ID di Directory.</span><span class="sxs-lookup"><span data-stu-id="53c6e-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="53c6e-141">**URL esterno** URL front-end di hello immesso nel Proxy applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="53c6e-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="53c6e-142">toofind questo valore, passare toohello **proxy dell'applicazione** sezione hello proxy app.</span><span class="sxs-lookup"><span data-stu-id="53c6e-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="53c6e-143">**ID dell'app** di hello app nativa è reperibile in hello **proprietà** pagina dell'applicazione nativa hello.</span><span class="sxs-lookup"><span data-stu-id="53c6e-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="53c6e-144">**URI di reindirizzamento dell'app nativa hello** possono trovarsi in hello **Redirect URIs** pagina dell'applicazione nativa hello.</span><span class="sxs-lookup"><span data-stu-id="53c6e-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="53c6e-145">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="53c6e-145">See also</span></span>

<span data-ttu-id="53c6e-146">Per ulteriori informazioni sul flusso di hello applicazione nativa, vedere [tooweb applicazione nativa API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="53c6e-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="53c6e-147">Per informazioni più recenti hello e gli aggiornamenti, consultare hello [blog del Proxy dell'applicazione](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="53c6e-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
