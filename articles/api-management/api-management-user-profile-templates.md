---
title: aaa "modelli di profilo utente in Gestione API di Azure | Documenti di Microsoft"
description: Informazioni su come le pagine contenuto hello toocustomize di hello profilo utente nel portale per sviluppatori hello in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: c8f153b310221164809acf58e4af236928ceb41d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="952f9-103">Modelli di profilo utente in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="952f9-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="952f9-104">Gestione API di Azure fornisce che si hello contenuto hello toocustomize di possibilità di pagine del portale per sviluppatori tramite un set di modelli che consentono di configurare i propri contenuti.</span><span class="sxs-lookup"><span data-stu-id="952f9-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="952f9-105">Utilizzando [DotLiquid](http://dotliquidmarkup.org/) sintassi e hello editor di propria scelta, ad esempio [DotLiquid per i progettisti](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e un set specificato di localizzato [risorse di stringa](api-management-template-resources.md#strings), [ Risorse glifo](api-management-template-resources.md#glyphs), e [pagina controlli](api-management-page-controls.md), una grande flessibilità tooconfigure hello alcuni contenuti sono di pagine hello secondo necessità utilizzando questi modelli.</span><span class="sxs-lookup"><span data-stu-id="952f9-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="952f9-106">i modelli di Hello in questa sezione consentono di contenuto hello toocustomize hello utente delle pagine di profilo nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-106">hello templates in this section allow you toocustomize hello content of hello User profile pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="952f9-107">Profilo</span><span class="sxs-lookup"><span data-stu-id="952f9-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="952f9-108">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="952f9-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="952f9-109">Applicazioni</span><span class="sxs-lookup"><span data-stu-id="952f9-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="952f9-110">Aggiornare le informazioni sull'account</span><span class="sxs-lookup"><span data-stu-id="952f9-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="952f9-111">Modelli predefiniti di esempio sono inclusi in hello seguente documentazione, ma sono soggetto toochange scadenza toocontinuous miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="952f9-111">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="952f9-112">È possibile visualizzare i modelli predefiniti in tempo reale di hello nel portale per sviluppatori di hello passando singoli modelli toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="952f9-112">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="952f9-113">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="952f9-113">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="952f9-114"><a name="Profile"></a> Profilo</span><span class="sxs-lookup"><span data-stu-id="952f9-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="952f9-115">Hello **profilo** modello consente toocustomize sezione profilo utente di hello di pagina del profilo utente hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-115">hello **profile** template allows you toocustomize hello user profile section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="952f9-116">![Pagina del profilo utente](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Pagina del profilo utente Gestione API")</span><span class="sxs-lookup"><span data-stu-id="952f9-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="952f9-117">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="952f9-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="952f9-118">Controlli</span><span class="sxs-lookup"><span data-stu-id="952f9-118">Controls</span></span>  
 <span data-ttu-id="952f9-119">Questo modello potrebbe non usare i [controlli di pagina](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="952f9-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="952f9-120">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="952f9-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="952f9-121">Hello [profilo](#Profile), [applicazioni](#Applications), e [sottoscrizioni](#Subscriptions) hello stessi dati del modello e di ricezione hello di condividere modelli di dati del modello stesso.</span><span class="sxs-lookup"><span data-stu-id="952f9-121">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="952f9-122">Proprietà</span><span class="sxs-lookup"><span data-stu-id="952f9-122">Property</span></span>|<span data-ttu-id="952f9-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="952f9-123">Type</span></span>|<span data-ttu-id="952f9-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="952f9-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="952f9-125">firstName</span><span class="sxs-lookup"><span data-stu-id="952f9-125">firstName</span></span>|<span data-ttu-id="952f9-126">string</span><span class="sxs-lookup"><span data-stu-id="952f9-126">string</span></span>|<span data-ttu-id="952f9-127">Nome dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-127">First name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-128">lastName</span><span class="sxs-lookup"><span data-stu-id="952f9-128">lastName</span></span>|<span data-ttu-id="952f9-129">string</span><span class="sxs-lookup"><span data-stu-id="952f9-129">string</span></span>|<span data-ttu-id="952f9-130">Cognome dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-130">Last name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-131">companyName</span><span class="sxs-lookup"><span data-stu-id="952f9-131">companyName</span></span>|<span data-ttu-id="952f9-132">string</span><span class="sxs-lookup"><span data-stu-id="952f9-132">string</span></span>|<span data-ttu-id="952f9-133">nome della società Hello dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-133">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="952f9-134">addresserEmail</span></span>|<span data-ttu-id="952f9-135">string</span><span class="sxs-lookup"><span data-stu-id="952f9-135">string</span></span>|<span data-ttu-id="952f9-136">Indirizzo di posta elettronica dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-136">Email address of hello current user.</span></span>|  
|<span data-ttu-id="952f9-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="952f9-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="952f9-138">string</span><span class="sxs-lookup"><span data-stu-id="952f9-138">string</span></span>|<span data-ttu-id="952f9-139">Analitica tooview URL relativo per l'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-139">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="952f9-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="952f9-140">subscriptions</span></span>|<span data-ttu-id="952f9-141">Raccolta di entità [Sottoscrizione](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="952f9-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="952f9-142">sottoscrizioni di Hello per l'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-142">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="952f9-143">scala Web</span><span class="sxs-lookup"><span data-stu-id="952f9-143">applications</span></span>|<span data-ttu-id="952f9-144">Raccolta di entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="952f9-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="952f9-145">applicazioni dell'utente corrente hello Hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-145">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="952f9-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="952f9-146">changePasswordUrl</span></span>|<span data-ttu-id="952f9-147">string</span><span class="sxs-lookup"><span data-stu-id="952f9-147">string</span></span>|<span data-ttu-id="952f9-148">password Hello relativo URL toochange hello dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="952f9-148">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="952f9-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="952f9-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="952f9-150">string</span><span class="sxs-lookup"><span data-stu-id="952f9-150">string</span></span>|<span data-ttu-id="952f9-151">Hello posta elettronica per l'utente corrente hello e nome del relativo URL toochange hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-151">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="952f9-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="952f9-152">canChangePassword</span></span>|<span data-ttu-id="952f9-153">boolean</span><span class="sxs-lookup"><span data-stu-id="952f9-153">boolean</span></span>|<span data-ttu-id="952f9-154">Utente corrente hello se è possibile modificare la password.</span><span class="sxs-lookup"><span data-stu-id="952f9-154">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="952f9-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="952f9-155">isSystemUser</span></span>|<span data-ttu-id="952f9-156">boolean</span><span class="sxs-lookup"><span data-stu-id="952f9-156">boolean</span></span>|<span data-ttu-id="952f9-157">Hello corrente sia un membro di uno dei predefiniti hello [gruppi](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="952f9-157">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="952f9-158">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="952f9-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="952f9-159"><a name="Subscriptions"></a> Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="952f9-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="952f9-160">Hello **sottoscrizioni** modello consente toocustomize hello sottoscrizioni sezione pagina hello del profilo utente nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-160">hello **Subscriptions** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="952f9-161">![Pagina di sottoscrizione utente](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Pagina di sottoscrizione utente in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="952f9-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="952f9-162">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="952f9-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="952f9-163">Controlli</span><span class="sxs-lookup"><span data-stu-id="952f9-163">Controls</span></span>  
 <span data-ttu-id="952f9-164">Questo modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="952f9-164">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="952f9-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="952f9-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="952f9-166">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="952f9-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="952f9-167">Hello [profilo](#Profile), [applicazioni](#Applications), e [sottoscrizioni](#Subscriptions) hello stessi dati del modello e di ricezione hello di condividere modelli di dati del modello stesso.</span><span class="sxs-lookup"><span data-stu-id="952f9-167">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="952f9-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="952f9-168">Property</span></span>|<span data-ttu-id="952f9-169">Tipo</span><span class="sxs-lookup"><span data-stu-id="952f9-169">Type</span></span>|<span data-ttu-id="952f9-170">Descrizione</span><span class="sxs-lookup"><span data-stu-id="952f9-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="952f9-171">firstName</span><span class="sxs-lookup"><span data-stu-id="952f9-171">firstName</span></span>|<span data-ttu-id="952f9-172">string</span><span class="sxs-lookup"><span data-stu-id="952f9-172">string</span></span>|<span data-ttu-id="952f9-173">Nome dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-173">First name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-174">lastName</span><span class="sxs-lookup"><span data-stu-id="952f9-174">lastName</span></span>|<span data-ttu-id="952f9-175">string</span><span class="sxs-lookup"><span data-stu-id="952f9-175">string</span></span>|<span data-ttu-id="952f9-176">Cognome dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-176">Last name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-177">companyName</span><span class="sxs-lookup"><span data-stu-id="952f9-177">companyName</span></span>|<span data-ttu-id="952f9-178">string</span><span class="sxs-lookup"><span data-stu-id="952f9-178">string</span></span>|<span data-ttu-id="952f9-179">nome della società Hello dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-179">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="952f9-180">addresserEmail</span></span>|<span data-ttu-id="952f9-181">string</span><span class="sxs-lookup"><span data-stu-id="952f9-181">string</span></span>|<span data-ttu-id="952f9-182">Indirizzo di posta elettronica dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-182">Email address of hello current user.</span></span>|  
|<span data-ttu-id="952f9-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="952f9-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="952f9-184">string</span><span class="sxs-lookup"><span data-stu-id="952f9-184">string</span></span>|<span data-ttu-id="952f9-185">Analitica tooview URL relativo per l'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-185">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="952f9-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="952f9-186">subscriptions</span></span>|<span data-ttu-id="952f9-187">Raccolta di entità [Sottoscrizione](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="952f9-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="952f9-188">sottoscrizioni di Hello per l'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-188">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="952f9-189">scala Web</span><span class="sxs-lookup"><span data-stu-id="952f9-189">applications</span></span>|<span data-ttu-id="952f9-190">Raccolta di entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="952f9-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="952f9-191">applicazioni dell'utente corrente hello Hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-191">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="952f9-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="952f9-192">changePasswordUrl</span></span>|<span data-ttu-id="952f9-193">string</span><span class="sxs-lookup"><span data-stu-id="952f9-193">string</span></span>|<span data-ttu-id="952f9-194">password Hello relativo URL toochange hello dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="952f9-194">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="952f9-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="952f9-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="952f9-196">string</span><span class="sxs-lookup"><span data-stu-id="952f9-196">string</span></span>|<span data-ttu-id="952f9-197">Hello posta elettronica per l'utente corrente hello e nome del relativo URL toochange hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-197">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="952f9-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="952f9-198">canChangePassword</span></span>|<span data-ttu-id="952f9-199">boolean</span><span class="sxs-lookup"><span data-stu-id="952f9-199">boolean</span></span>|<span data-ttu-id="952f9-200">Utente corrente hello se è possibile modificare la password.</span><span class="sxs-lookup"><span data-stu-id="952f9-200">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="952f9-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="952f9-201">isSystemUser</span></span>|<span data-ttu-id="952f9-202">boolean</span><span class="sxs-lookup"><span data-stu-id="952f9-202">boolean</span></span>|<span data-ttu-id="952f9-203">Hello corrente sia un membro di uno dei predefiniti hello [gruppi](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="952f9-203">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="952f9-204">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="952f9-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="952f9-205"><a name="Applications"></a> Applicazioni</span><span class="sxs-lookup"><span data-stu-id="952f9-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="952f9-206">Hello **applicazioni** modello consente toocustomize hello sottoscrizioni sezione pagina hello del profilo utente nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-206">hello **Applications** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="952f9-207">![Pagina applicazioni account utente](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "Pagina applicazioni account utente in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="952f9-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="952f9-208">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="952f9-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="952f9-209">Controlli</span><span class="sxs-lookup"><span data-stu-id="952f9-209">Controls</span></span>  
 <span data-ttu-id="952f9-210">Questo modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="952f9-210">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="952f9-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="952f9-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="952f9-212">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="952f9-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="952f9-213">Hello [profilo](#Profile), [applicazioni](#Applications), e [sottoscrizioni](#Subscriptions) hello stessi dati del modello e di ricezione hello di condividere modelli di dati del modello stesso.</span><span class="sxs-lookup"><span data-stu-id="952f9-213">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="952f9-214">Proprietà</span><span class="sxs-lookup"><span data-stu-id="952f9-214">Property</span></span>|<span data-ttu-id="952f9-215">Tipo</span><span class="sxs-lookup"><span data-stu-id="952f9-215">Type</span></span>|<span data-ttu-id="952f9-216">Descrizione</span><span class="sxs-lookup"><span data-stu-id="952f9-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="952f9-217">firstName</span><span class="sxs-lookup"><span data-stu-id="952f9-217">firstName</span></span>|<span data-ttu-id="952f9-218">string</span><span class="sxs-lookup"><span data-stu-id="952f9-218">string</span></span>|<span data-ttu-id="952f9-219">Nome dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-219">First name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-220">lastName</span><span class="sxs-lookup"><span data-stu-id="952f9-220">lastName</span></span>|<span data-ttu-id="952f9-221">string</span><span class="sxs-lookup"><span data-stu-id="952f9-221">string</span></span>|<span data-ttu-id="952f9-222">Cognome dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-222">Last name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-223">companyName</span><span class="sxs-lookup"><span data-stu-id="952f9-223">companyName</span></span>|<span data-ttu-id="952f9-224">string</span><span class="sxs-lookup"><span data-stu-id="952f9-224">string</span></span>|<span data-ttu-id="952f9-225">nome della società Hello dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-225">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="952f9-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="952f9-226">addresserEmail</span></span>|<span data-ttu-id="952f9-227">string</span><span class="sxs-lookup"><span data-stu-id="952f9-227">string</span></span>|<span data-ttu-id="952f9-228">Indirizzo di posta elettronica dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-228">Email address of hello current user.</span></span>|  
|<span data-ttu-id="952f9-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="952f9-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="952f9-230">string</span><span class="sxs-lookup"><span data-stu-id="952f9-230">string</span></span>|<span data-ttu-id="952f9-231">Analitica tooview URL relativo per l'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-231">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="952f9-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="952f9-232">subscriptions</span></span>|<span data-ttu-id="952f9-233">Raccolta di entità [Sottoscrizione](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="952f9-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="952f9-234">sottoscrizioni di Hello per l'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-234">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="952f9-235">scala Web</span><span class="sxs-lookup"><span data-stu-id="952f9-235">applications</span></span>|<span data-ttu-id="952f9-236">Raccolta di entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="952f9-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="952f9-237">applicazioni dell'utente corrente hello Hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-237">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="952f9-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="952f9-238">changePasswordUrl</span></span>|<span data-ttu-id="952f9-239">string</span><span class="sxs-lookup"><span data-stu-id="952f9-239">string</span></span>|<span data-ttu-id="952f9-240">password Hello relativo URL toochange hello dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="952f9-240">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="952f9-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="952f9-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="952f9-242">string</span><span class="sxs-lookup"><span data-stu-id="952f9-242">string</span></span>|<span data-ttu-id="952f9-243">Hello posta elettronica per l'utente corrente hello e nome del relativo URL toochange hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-243">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="952f9-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="952f9-244">canChangePassword</span></span>|<span data-ttu-id="952f9-245">boolean</span><span class="sxs-lookup"><span data-stu-id="952f9-245">boolean</span></span>|<span data-ttu-id="952f9-246">Utente corrente hello se è possibile modificare la password.</span><span class="sxs-lookup"><span data-stu-id="952f9-246">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="952f9-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="952f9-247">isSystemUser</span></span>|<span data-ttu-id="952f9-248">boolean</span><span class="sxs-lookup"><span data-stu-id="952f9-248">boolean</span></span>|<span data-ttu-id="952f9-249">Hello corrente sia un membro di uno dei predefiniti hello [gruppi](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="952f9-249">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="952f9-250">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="952f9-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="952f9-251"><a name="UpdateAccountInfo"></a> Aggiorna info account</span><span class="sxs-lookup"><span data-stu-id="952f9-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="952f9-252">Hello **info del tuo account Uodate** modello consente hello toocustomize **aggiornare informazioni sull'account** pagina nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="952f9-252">hello **Uodate account info** template allows you toocustomize hello **Update account information** page in hello developer portal.</span></span>  
  
 <span data-ttu-id="952f9-253">![Modelli del portale per sviluppatori, pagina di informazioni sull'account utente](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Modelli del portale per sviluppatori, pagina di informazioni sull'account utente in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="952f9-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="952f9-254">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="952f9-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="952f9-255">Controlli</span><span class="sxs-lookup"><span data-stu-id="952f9-255">Controls</span></span>  
 <span data-ttu-id="952f9-256">Questo modello potrebbe non usare i [controlli di pagina](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="952f9-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="952f9-257">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="952f9-257">Data model</span></span>  
 <span data-ttu-id="952f9-258">Entità [Informazioni sull'account utente](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="952f9-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="952f9-259">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="952f9-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="952f9-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="952f9-260">Next steps</span></span>
<span data-ttu-id="952f9-261">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="952f9-261">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
