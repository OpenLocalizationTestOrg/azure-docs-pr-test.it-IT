---
title: Modelli di pagina in Gestione API di Azure | Microsoft Docs
description: Informazioni su come personalizzare il contenuto delle pagine del portale per sviluppatori usando un set di modelli in Gestione API di Azure.
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
ms.openlocfilehash: 7f9ef37a694bce786b6acaa428df83f0cb23c2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="9beab-103">Modelli di pagina in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="9beab-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="9beab-104">In Gestione API di Azure è possibile personalizzare le pagine del portale per sviluppatori usando un set di modelli che ne configurano il contenuto.</span><span class="sxs-lookup"><span data-stu-id="9beab-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="9beab-105">La sintassi [DotLiquid](http://dotliquidmarkup.org/) usata insieme all'editor di propria scelta, ad esempio [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e a un set di [risorse stringa](api-management-template-resources.md#strings) localizzate, [risorse Glifo](api-management-template-resources.md#glyphs) e [controlli di pagina](api-management-page-controls.md) offre una grande flessibilità nella configurazione personalizzata del contenuto delle pagine attraverso questi modelli.</span><span class="sxs-lookup"><span data-stu-id="9beab-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="9beab-106">I modelli in questa sezione consentono di personalizzare il contenuto delle pagine di accesso, di iscrizione e Pagina non trovata del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="9beab-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="9beab-107">Accesso</span><span class="sxs-lookup"><span data-stu-id="9beab-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="9beab-108">Iscrizione</span><span class="sxs-lookup"><span data-stu-id="9beab-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="9beab-109">Pagina non trovata</span><span class="sxs-lookup"><span data-stu-id="9beab-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="9beab-110">La documentazione seguente include alcuni modelli predefiniti di esempio. A causa dei continui miglioramenti che vengono apportati, questi modelli sono però soggetti a modifiche.</span><span class="sxs-lookup"><span data-stu-id="9beab-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="9beab-111">È possibile visualizzare i modelli predefiniti direttamente nel portale per sviluppatori accedendo ai singoli modelli desiderati.</span><span class="sxs-lookup"><span data-stu-id="9beab-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="9beab-112">Per altre informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API di Azure con i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="9beab-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="9beab-113"><a name="SignIn"></a> Accesso</span><span class="sxs-lookup"><span data-stu-id="9beab-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="9beab-114">Il modello di **accesso** consente di personalizzare la pagina di accesso del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="9beab-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="9beab-115">![Pagina di accesso](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "Modelli della pagina di accesso nel portale per sviluppatori di Gestione API")</span><span class="sxs-lookup"><span data-stu-id="9beab-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="9beab-116">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="9beab-116">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="9beab-117">Controlli</span><span class="sxs-lookup"><span data-stu-id="9beab-117">Controls</span></span>  
 <span data-ttu-id="9beab-118">Questo modello può usare i [controlli di pagina](api-management-page-controls.md) seguenti.</span><span class="sxs-lookup"><span data-stu-id="9beab-118">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="9beab-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="9beab-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="9beab-120">provider</span><span class="sxs-lookup"><span data-stu-id="9beab-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="9beab-121">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="9beab-121">Data model</span></span>  
 <span data-ttu-id="9beab-122">Entità [Accesso utente](api-management-template-data-model-reference.md#UseSignIn).</span><span class="sxs-lookup"><span data-stu-id="9beab-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="9beab-123">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="9beab-123">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="9beab-124"><a name="SignUp"></a> Iscrizione</span><span class="sxs-lookup"><span data-stu-id="9beab-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="9beab-125">Il modello di **iscrizione** consente di personalizzare la pagina di iscrizione del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="9beab-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="9beab-126">![Pagina di iscrizione](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "Modelli della pagina di iscrizione nel portale per sviluppatori di Gestione API")</span><span class="sxs-lookup"><span data-stu-id="9beab-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="9beab-127">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="9beab-127">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="9beab-128">Controlli</span><span class="sxs-lookup"><span data-stu-id="9beab-128">Controls</span></span>  
 <span data-ttu-id="9beab-129">Questo modello può usare i [controlli di pagina](api-management-page-controls.md) seguenti.</span><span class="sxs-lookup"><span data-stu-id="9beab-129">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="9beab-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="9beab-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="9beab-131">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="9beab-131">Data model</span></span>  
 <span data-ttu-id="9beab-132">Entità [Iscrizione utente](api-management-template-data-model-reference.md#UserSignUp).</span><span class="sxs-lookup"><span data-stu-id="9beab-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="9beab-133">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="9beab-133">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="9beab-134"><a name="PageNotFound"></a> Pagina non trovata</span><span class="sxs-lookup"><span data-stu-id="9beab-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="9beab-135">Il modello **Pagina non trovata** consente di personalizzare la pagina Pagina non trovata del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="9beab-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span></span>  
  
 <span data-ttu-id="9beab-136">![Pagina non trovata](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "Modelli di Pagina non trovata nel portale per sviluppatori di Gestione API")</span><span class="sxs-lookup"><span data-stu-id="9beab-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="9beab-137">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="9beab-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="9beab-138">Controlli</span><span class="sxs-lookup"><span data-stu-id="9beab-138">Controls</span></span>  
 <span data-ttu-id="9beab-139">Questo modello potrebbe non usare i [controlli di pagina](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="9beab-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="9beab-140">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="9beab-140">Data model</span></span>  
  
|<span data-ttu-id="9beab-141">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9beab-141">Property</span></span>|<span data-ttu-id="9beab-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="9beab-142">Type</span></span>|<span data-ttu-id="9beab-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9beab-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="9beab-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="9beab-144">referenceCode</span></span>|<span data-ttu-id="9beab-145">string</span><span class="sxs-lookup"><span data-stu-id="9beab-145">string</span></span>|<span data-ttu-id="9beab-146">Codice generato se questa pagina viene visualizzata in seguito a un errore interno.</span><span class="sxs-lookup"><span data-stu-id="9beab-146">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="9beab-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="9beab-147">errorCode</span></span>|<span data-ttu-id="9beab-148">string</span><span class="sxs-lookup"><span data-stu-id="9beab-148">string</span></span>|<span data-ttu-id="9beab-149">Codice generato se questa pagina viene visualizzata in seguito a un errore interno.</span><span class="sxs-lookup"><span data-stu-id="9beab-149">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="9beab-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="9beab-150">emailBody</span></span>|<span data-ttu-id="9beab-151">string</span><span class="sxs-lookup"><span data-stu-id="9beab-151">string</span></span>|<span data-ttu-id="9beab-152">Corpo del messaggio di posta elettronica generato se questa pagina viene visualizzata in seguito a un errore interno.</span><span class="sxs-lookup"><span data-stu-id="9beab-152">Email body generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="9beab-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="9beab-153">requestedUrl</span></span>|<span data-ttu-id="9beab-154">string</span><span class="sxs-lookup"><span data-stu-id="9beab-154">string</span></span>|<span data-ttu-id="9beab-155">URL richiesto quando la pagina non è stata trovata.</span><span class="sxs-lookup"><span data-stu-id="9beab-155">The URL requested when the page was not found.</span></span>|  
|<span data-ttu-id="9beab-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="9beab-156">referrerUrl</span></span>|<span data-ttu-id="9beab-157">string</span><span class="sxs-lookup"><span data-stu-id="9beab-157">string</span></span>|<span data-ttu-id="9beab-158">URL del referrer all'URL richiesto.</span><span class="sxs-lookup"><span data-stu-id="9beab-158">The referrer URL to the requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="9beab-159">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="9beab-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="9beab-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9beab-160">Next steps</span></span>
<span data-ttu-id="9beab-161">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9beab-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>