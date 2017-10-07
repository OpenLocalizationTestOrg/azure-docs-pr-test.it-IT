---
title: modelli aaaPage in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toocustomize hello contenuto di pagine del portale per sviluppatori tramite un set di modelli in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="e7997-103">Modelli di pagina in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="e7997-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="e7997-104">Gestione API di Azure fornisce che si hello contenuto hello toocustomize di possibilità di pagine del portale per sviluppatori tramite un set di modelli che consentono di configurare i propri contenuti.</span><span class="sxs-lookup"><span data-stu-id="e7997-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="e7997-105">Utilizzando [DotLiquid](http://dotliquidmarkup.org/) sintassi e hello editor di propria scelta, ad esempio [DotLiquid per i progettisti](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e un set specificato di localizzato [risorse di stringa](api-management-template-resources.md#strings), [ Risorse glifo](api-management-template-resources.md#glyphs), e [pagina controlli](api-management-page-controls.md), una grande flessibilità tooconfigure hello alcuni contenuti sono di pagine hello secondo necessità utilizzando questi modelli.</span><span class="sxs-lookup"><span data-stu-id="e7997-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="e7997-106">Hello i modelli in questa sezione consentono di contenuto di hello toocustomize di hello Accedi, sign backup e pagine di pagina non trovata nel portale per sviluppatori di hello.</span><span class="sxs-lookup"><span data-stu-id="e7997-106">hello templates in this section allow you toocustomize hello content of hello sign in, sign up, and page not found pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="e7997-107">Accesso</span><span class="sxs-lookup"><span data-stu-id="e7997-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="e7997-108">Iscrizione</span><span class="sxs-lookup"><span data-stu-id="e7997-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="e7997-109">Pagina non trovata</span><span class="sxs-lookup"><span data-stu-id="e7997-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="e7997-110">Modelli predefiniti di esempio sono inclusi in hello seguente documentazione, ma sono soggetto toochange scadenza toocontinuous miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="e7997-110">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="e7997-111">È possibile visualizzare i modelli predefiniti in tempo reale di hello nel portale per sviluppatori di hello passando singoli modelli toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="e7997-111">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="e7997-112">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="e7997-112">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="e7997-113"><a name="SignIn"></a> Accesso</span><span class="sxs-lookup"><span data-stu-id="e7997-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="e7997-114">Hello **Accedi** modello consente accesso hello toocustomize nella pagina nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="e7997-114">hello **sign in** template allows you toocustomize hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="e7997-115">![Pagina di accesso](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "Modelli della pagina di accesso nel portale per sviluppatori di Gestione API")</span><span class="sxs-lookup"><span data-stu-id="e7997-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="e7997-116">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="e7997-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="e7997-117">Controlli</span><span class="sxs-lookup"><span data-stu-id="e7997-117">Controls</span></span>  
 <span data-ttu-id="e7997-118">Questo modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="e7997-118">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="e7997-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="e7997-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="e7997-120">provider</span><span class="sxs-lookup"><span data-stu-id="e7997-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="e7997-121">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="e7997-121">Data model</span></span>  
 <span data-ttu-id="e7997-122">Entità [Accesso utente](api-management-template-data-model-reference.md#UseSignIn).</span><span class="sxs-lookup"><span data-stu-id="e7997-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="e7997-123">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="e7997-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <span data-ttu-id="e7997-124"><a name="SignUp"></a> Iscrizione</span><span class="sxs-lookup"><span data-stu-id="e7997-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="e7997-125">Hello **iscriversi** modello consente toocustomize hello pagina di iscrizione nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="e7997-125">hello **sign up** template allows you toocustomize hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="e7997-126">![Pagina di iscrizione](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "Modelli della pagina di iscrizione nel portale per sviluppatori di Gestione API")</span><span class="sxs-lookup"><span data-stu-id="e7997-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="e7997-127">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="e7997-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="e7997-128">Controlli</span><span class="sxs-lookup"><span data-stu-id="e7997-128">Controls</span></span>  
 <span data-ttu-id="e7997-129">Questo modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="e7997-129">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="e7997-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="e7997-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="e7997-131">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="e7997-131">Data model</span></span>  
 <span data-ttu-id="e7997-132">Entità [Iscrizione utente](api-management-template-data-model-reference.md#UserSignUp).</span><span class="sxs-lookup"><span data-stu-id="e7997-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="e7997-133">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="e7997-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <span data-ttu-id="e7997-134"><a name="PageNotFound"></a> Pagina non trovata</span><span class="sxs-lookup"><span data-stu-id="e7997-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="e7997-135">Hello **pagina non trovata** modello consente di toocustomize hello pagina non trovata pagina nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="e7997-135">hello **page not found** template allows you toocustomize hello page not found page in hello developer portal.</span></span>  
  
 <span data-ttu-id="e7997-136">![Pagina non trovata](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "Modelli di Pagina non trovata nel portale per sviluppatori di Gestione API")</span><span class="sxs-lookup"><span data-stu-id="e7997-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="e7997-137">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="e7997-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="e7997-138">Controlli</span><span class="sxs-lookup"><span data-stu-id="e7997-138">Controls</span></span>  
 <span data-ttu-id="e7997-139">Questo modello potrebbe non usare i [controlli di pagina](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="e7997-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="e7997-140">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="e7997-140">Data model</span></span>  
  
|<span data-ttu-id="e7997-141">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e7997-141">Property</span></span>|<span data-ttu-id="e7997-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="e7997-142">Type</span></span>|<span data-ttu-id="e7997-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e7997-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="e7997-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="e7997-144">referenceCode</span></span>|<span data-ttu-id="e7997-145">string</span><span class="sxs-lookup"><span data-stu-id="e7997-145">string</span></span>|<span data-ttu-id="e7997-146">Codice generato come risultato di hello di un errore interno è stato visualizzato in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="e7997-146">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="e7997-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="e7997-147">errorCode</span></span>|<span data-ttu-id="e7997-148">string</span><span class="sxs-lookup"><span data-stu-id="e7997-148">string</span></span>|<span data-ttu-id="e7997-149">Codice generato come risultato di hello di un errore interno è stato visualizzato in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="e7997-149">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="e7997-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="e7997-150">emailBody</span></span>|<span data-ttu-id="e7997-151">string</span><span class="sxs-lookup"><span data-stu-id="e7997-151">string</span></span>|<span data-ttu-id="e7997-152">Se questa pagina è stata visualizzata come risultato di hello di un errore interno generato corpo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="e7997-152">Email body generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="e7997-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="e7997-153">requestedUrl</span></span>|<span data-ttu-id="e7997-154">string</span><span class="sxs-lookup"><span data-stu-id="e7997-154">string</span></span>|<span data-ttu-id="e7997-155">URL di Hello richiesto quando hello pagina non trovata.</span><span class="sxs-lookup"><span data-stu-id="e7997-155">hello URL requested when hello page was not found.</span></span>|  
|<span data-ttu-id="e7997-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="e7997-156">referrerUrl</span></span>|<span data-ttu-id="e7997-157">string</span><span class="sxs-lookup"><span data-stu-id="e7997-157">string</span></span>|<span data-ttu-id="e7997-158">Hello referrer URL toohello richiesta URL.</span><span class="sxs-lookup"><span data-stu-id="e7997-158">hello referrer URL toohello requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="e7997-159">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="e7997-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="e7997-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e7997-160">Next steps</span></span>
<span data-ttu-id="e7997-161">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e7997-161">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
