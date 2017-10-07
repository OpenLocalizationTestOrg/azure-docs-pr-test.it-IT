---
title: 'Azure Active Directory B2C: criteri predefiniti | Microsoft Docs'
description: Un argomento nel framework di criteri estendibile hello di Azure Active Directory B2C e su come toocreate vari tipi di criteri
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="cf2ae-103">Azure Active Directory B2C: criteri predefiniti</span><span class="sxs-lookup"><span data-stu-id="cf2ae-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="cf2ae-104">framework di criteri estendibile Hello di B2C Azure Active Directory (Azure AD) è il livello di attendibilità di hello componenti di base del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-104">hello extensible policy framework of Azure Active Directory (Azure AD) B2C is hello core strength of hello service.</span></span> <span data-ttu-id="cf2ae-105">I criteri descrivono le esperienze di identità, ad esempio iscrizione, accesso o modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="cf2ae-106">Ad esempio, un criterio per l'abbonamento consente comportamenti toocontrol configurando hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="cf2ae-106">For instance, a sign-up policy allows you toocontrol behaviors by configuring hello following settings:</span></span>

* <span data-ttu-id="cf2ae-107">Account di tipi (account di social networking, ad esempio Facebook) o locale, ad esempio indirizzi di posta elettronica che i consumer possono utilizzare toosign per un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="cf2ae-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use toosign up for hello application</span></span>
* <span data-ttu-id="cf2ae-108">Attributi (ad esempio nome, il CAP e scarpe) toobe raccolti dai consumer hello durante l'iscrizione</span><span class="sxs-lookup"><span data-stu-id="cf2ae-108">Attributes (for example, first name, postal code, and shoe size) toobe collected from hello consumer during sign-up</span></span>
* <span data-ttu-id="cf2ae-109">Uso di Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="cf2ae-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="cf2ae-110">Hello aspetto di tutte le pagine di iscrizione</span><span class="sxs-lookup"><span data-stu-id="cf2ae-110">hello look and feel of all sign-up pages</span></span>
* <span data-ttu-id="cf2ae-111">Informazioni (che si manifesta come attestazioni in un token) che l'applicazione hello riceve al termine dell'esecuzione dei criteri di hello</span><span class="sxs-lookup"><span data-stu-id="cf2ae-111">Information (which manifests as claims in a token) that hello application receives when hello policy run finishes</span></span>

<span data-ttu-id="cf2ae-112">È possibile creare più criteri di tipi diversi nel proprio tenant e usarli nelle applicazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="cf2ae-113">I criteri possono essere usati per più applicazioni.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-113">Policies can be reused across applications.</span></span> <span data-ttu-id="cf2ae-114">Questa flessibilità consente agli sviluppatori toodefine e modificare esperienze di identità consumer con una quantità minima o nessun codice tootheir le modifiche.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-114">This flexibility enables developers toodefine and modify consumer identity experiences with minimal or no changes tootheir code.</span></span>

<span data-ttu-id="cf2ae-115">Per usare i criteri, è disponibile una semplice interfaccia per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="cf2ae-116">L'applicazione può attivare un criterio tramite una richiesta di autenticazione HTTP standard (passando un parametro di criteri nella richiesta di hello) e riceve un token personalizzato come risposta.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in hello request) and receives a customized token as response.</span></span> <span data-ttu-id="cf2ae-117">Ad esempio, hello l'unica differenza tra le richieste che richiamano un criterio di iscrizione e richiamare un criterio di accesso è nome criterio hello utilizzato nel parametro di stringa di query hello "p":</span><span class="sxs-lookup"><span data-stu-id="cf2ae-117">For example, hello only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is hello policy name that's used in hello "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="cf2ae-118">Per ulteriori informazioni su hello criteri framework, vedere [questo post di blog sul Blog di sicurezza e Azure Active Directory B2C su Enterprise Mobility hello](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf2ae-118">For more information about hello policy framework, see [this blog post about Azure AD B2C on hello Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="cf2ae-119">Creare un criterio di iscrizione o accesso</span><span class="sxs-lookup"><span data-stu-id="cf2ae-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="cf2ae-120">Questo criterio consente di gestire le esperienze di iscrizione e accesso dei consumatori tramite una singola configurazione.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="cf2ae-121">I consumer sono dirette verso il basso hello percorso verso destra (iscrizione o accesso) a seconda del contesto di hello.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-121">Consumers are led down hello right path (sign-up or sign-in) depending on hello context.</span></span> <span data-ttu-id="cf2ae-122">Vengono inoltre descritte contenuto hello di token che un'applicazione hello riceverà iscrizioni ha esito positivo o accessi.  È un esempio di codice per il criterio di iscrizione o accesso hello [disponibile qui](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="cf2ae-122">It also describes hello contents of tokens that hello application will receive upon successful sign-ups or sign-ins.  A code sample for hello sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="cf2ae-123">È consigliabile usare questo criterio invece di criteri di iscrizione e di accesso.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="cf2ae-124">Creare un criterio di iscrizione</span><span class="sxs-lookup"><span data-stu-id="cf2ae-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="cf2ae-125">Creare un criterio di accesso</span><span class="sxs-lookup"><span data-stu-id="cf2ae-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="cf2ae-126">Creare i criteri di modifica del profilo</span><span class="sxs-lookup"><span data-stu-id="cf2ae-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="cf2ae-127">Creare i criteri di reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="cf2ae-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="cf2ae-128">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="cf2ae-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="cf2ae-129">Come si collegano i criteri di iscrizione o accesso ai criteri di reimpostazione delle password?</span><span class="sxs-lookup"><span data-stu-id="cf2ae-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="cf2ae-130">Quando si crea un criterio di iscrizione o accesso (con gli account locali), viene visualizzato un **password dimenticata?** collegamento hello prima pagina dell'esperienza di hello.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on hello first page of hello experience.</span></span> <span data-ttu-id="cf2ae-131">Se si fa clic su questo collegamento non si attivano automaticamente i criteri di reimpostazione delle password.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="cf2ae-132">Hello, invece, il codice di errore  **`AADB2C90118`**  viene restituito tooyour app.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-132">Instead, hello error code **`AADB2C90118`** is returned tooyour app.</span></span> <span data-ttu-id="cf2ae-133">L'app deve toohandle questo codice di errore tramite la chiamata di un criterio di reimpostazione password specifica.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-133">Your app needs toohandle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="cf2ae-134">Per ulteriori informazioni, vedere una [esempio che illustra l'approccio di hello del collegamento dei criteri di](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="cf2ae-134">For more information, see a [sample that demonstrates hello approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="cf2ae-135">È consigliabile usare criteri di iscrizione o accesso o criteri di iscrizione e criteri di accesso?</span><span class="sxs-lookup"><span data-stu-id="cf2ae-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="cf2ae-136">È consigliabile usare criteri di iscrizione o accesso al posto di criteri di iscrizione e criteri di accesso.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="cf2ae-137">criteri di iscrizione o accesso Hello offre maggiori funzionalità rispetto a criterio di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-137">hello sign-up or sign-in policy has more capabilities than hello sign-in policy.</span></span> <span data-ttu-id="cf2ae-138">Inoltre, consente la personalizzazione dell'interfaccia utente di pagina toouse e ha un supporto migliore per la localizzazione.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-138">It also enables you toouse page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="cf2ae-139">criteri di accesso Hello sono consigliato se non è necessario toolocalize i criteri, solo necessario funzionalità di personalizzazione secondaria per la personalizzazione e la password reset incorporato.</span><span class="sxs-lookup"><span data-stu-id="cf2ae-139">hello sign-in policy is recommended if you don't need toolocalize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf2ae-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cf2ae-140">Next steps</span></span>
* [<span data-ttu-id="cf2ae-141">Configurazione di token, sessione e accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cf2ae-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="cf2ae-142">Disabilitare la verifica della posta elettronica durante l'iscrizione dell'utente</span><span class="sxs-lookup"><span data-stu-id="cf2ae-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

