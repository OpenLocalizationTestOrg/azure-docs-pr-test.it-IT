---
title: Modelli di profilo utente in Gestione API di Azure | Microsoft Docs
description: Informazioni su come personalizzare il contenuto delle pagine dei profili utente nel portale per sviluppatori in Gestione API di Azure.
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
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="dd969-103">Modelli di profilo utente in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="dd969-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="dd969-104">In Gestione API di Azure è possibile personalizzare le pagine del portale per sviluppatori usando un set di modelli che ne configurano il contenuto.</span><span class="sxs-lookup"><span data-stu-id="dd969-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="dd969-105">La sintassi [DotLiquid](http://dotliquidmarkup.org/) usata insieme a un editor di propria scelta, quale [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e a un set di [risorse stringa](api-management-template-resources.md#strings), [risorse Glifo](api-management-template-resources.md#glyphs) e [controlli di pagina](api-management-page-controls.md) offre una grande flessibilità nella configurazione personalizzata del contenuto delle pagine attraverso questi modelli.</span><span class="sxs-lookup"><span data-stu-id="dd969-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="dd969-106">I modelli in questa sezione consentono di personalizzare il contenuto delle pagine dei profili utente del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="dd969-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="dd969-107">Profilo</span><span class="sxs-lookup"><span data-stu-id="dd969-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="dd969-108">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="dd969-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="dd969-109">Applicazioni</span><span class="sxs-lookup"><span data-stu-id="dd969-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="dd969-110">Aggiornare le informazioni sull'account</span><span class="sxs-lookup"><span data-stu-id="dd969-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="dd969-111">La documentazione seguente include alcuni modelli predefiniti di esempio. A causa dei continui miglioramenti che vengono apportati, questi modelli sono però soggetti a modifiche.</span><span class="sxs-lookup"><span data-stu-id="dd969-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="dd969-112">È possibile visualizzare i modelli predefiniti direttamente nel portale per sviluppatori accedendo ai singoli modelli desiderati.</span><span class="sxs-lookup"><span data-stu-id="dd969-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="dd969-113">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="dd969-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="dd969-114"><a name="Profile"></a> Profilo</span><span class="sxs-lookup"><span data-stu-id="dd969-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="dd969-115">Il modello **Profilo** consente di personalizzare la sezione profili utente della pagina del profilo utente nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="dd969-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="dd969-116">![Pagina del profilo utente](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Pagina del profilo utente Gestione API")</span><span class="sxs-lookup"><span data-stu-id="dd969-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="dd969-117">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="dd969-117">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="dd969-118">Controlli</span><span class="sxs-lookup"><span data-stu-id="dd969-118">Controls</span></span>  
 <span data-ttu-id="dd969-119">Questo modello potrebbe non usare i [controlli di pagina](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="dd969-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="dd969-120">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="dd969-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="dd969-121">I modelli [Profilo](#Profile), [Applicazioni](#Applications) e [Sottoscrizioni](#Subscriptions) condividono lo stesso modello di dati e ricevono gli stessi dati del modello.</span><span class="sxs-lookup"><span data-stu-id="dd969-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="dd969-122">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dd969-122">Property</span></span>|<span data-ttu-id="dd969-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="dd969-123">Type</span></span>|<span data-ttu-id="dd969-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dd969-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="dd969-125">firstName</span><span class="sxs-lookup"><span data-stu-id="dd969-125">firstName</span></span>|<span data-ttu-id="dd969-126">string</span><span class="sxs-lookup"><span data-stu-id="dd969-126">string</span></span>|<span data-ttu-id="dd969-127">Nome dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-127">First name of the current user.</span></span>|  
|<span data-ttu-id="dd969-128">lastName</span><span class="sxs-lookup"><span data-stu-id="dd969-128">lastName</span></span>|<span data-ttu-id="dd969-129">string</span><span class="sxs-lookup"><span data-stu-id="dd969-129">string</span></span>|<span data-ttu-id="dd969-130">Cognome dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="dd969-131">companyName</span><span class="sxs-lookup"><span data-stu-id="dd969-131">companyName</span></span>|<span data-ttu-id="dd969-132">string</span><span class="sxs-lookup"><span data-stu-id="dd969-132">string</span></span>|<span data-ttu-id="dd969-133">Il nome della società dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="dd969-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="dd969-134">addresserEmail</span></span>|<span data-ttu-id="dd969-135">string</span><span class="sxs-lookup"><span data-stu-id="dd969-135">string</span></span>|<span data-ttu-id="dd969-136">Indirizzo di posta elettronica dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="dd969-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="dd969-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="dd969-138">string</span><span class="sxs-lookup"><span data-stu-id="dd969-138">string</span></span>|<span data-ttu-id="dd969-139">URL relativo per visualizzare l'analisi per l'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="dd969-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="dd969-140">subscriptions</span></span>|<span data-ttu-id="dd969-141">Raccolta di entità [Sottoscrizione](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="dd969-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="dd969-142">Le sottoscrizioni dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="dd969-143">scala Web</span><span class="sxs-lookup"><span data-stu-id="dd969-143">applications</span></span>|<span data-ttu-id="dd969-144">Raccolta di entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="dd969-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="dd969-145">Le applicazioni dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="dd969-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="dd969-146">changePasswordUrl</span></span>|<span data-ttu-id="dd969-147">string</span><span class="sxs-lookup"><span data-stu-id="dd969-147">string</span></span>|<span data-ttu-id="dd969-148">L'URL relativo per modificare la password dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="dd969-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="dd969-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="dd969-150">string</span><span class="sxs-lookup"><span data-stu-id="dd969-150">string</span></span>|<span data-ttu-id="dd969-151">L'URL relativo per modificare il nome e l'indirizzo di posta elettronica dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="dd969-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="dd969-152">canChangePassword</span></span>|<span data-ttu-id="dd969-153">boolean</span><span class="sxs-lookup"><span data-stu-id="dd969-153">boolean</span></span>|<span data-ttu-id="dd969-154">Indica se l'utente corrente può modificare la propria password.</span><span class="sxs-lookup"><span data-stu-id="dd969-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="dd969-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="dd969-155">isSystemUser</span></span>|<span data-ttu-id="dd969-156">boolean</span><span class="sxs-lookup"><span data-stu-id="dd969-156">boolean</span></span>|<span data-ttu-id="dd969-157">Indica se l'utente corrente è membro di uno dei [gruppi](api-management-key-concepts.md#groups) predefiniti.</span><span class="sxs-lookup"><span data-stu-id="dd969-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="dd969-158">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="dd969-158">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="dd969-159"><a name="Subscriptions"></a> Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="dd969-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="dd969-160">Il modello **Sottoscrizioni** consente di personalizzare la sezione sottoscrizioni della pagina del profilo utente nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="dd969-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="dd969-161">![Pagina di sottoscrizione utente](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Pagina di sottoscrizione utente in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="dd969-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="dd969-162">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="dd969-162">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="dd969-163">Controlli</span><span class="sxs-lookup"><span data-stu-id="dd969-163">Controls</span></span>  
 <span data-ttu-id="dd969-164">Questo modello può usare i [controlli di pagina](api-management-page-controls.md) seguenti.</span><span class="sxs-lookup"><span data-stu-id="dd969-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="dd969-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="dd969-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="dd969-166">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="dd969-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="dd969-167">I modelli [Profilo](#Profile), [Applicazioni](#Applications) e [Sottoscrizioni](#Subscriptions) condividono lo stesso modello di dati e ricevono gli stessi dati del modello.</span><span class="sxs-lookup"><span data-stu-id="dd969-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="dd969-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dd969-168">Property</span></span>|<span data-ttu-id="dd969-169">Tipo</span><span class="sxs-lookup"><span data-stu-id="dd969-169">Type</span></span>|<span data-ttu-id="dd969-170">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dd969-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="dd969-171">firstName</span><span class="sxs-lookup"><span data-stu-id="dd969-171">firstName</span></span>|<span data-ttu-id="dd969-172">string</span><span class="sxs-lookup"><span data-stu-id="dd969-172">string</span></span>|<span data-ttu-id="dd969-173">Nome dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-173">First name of the current user.</span></span>|  
|<span data-ttu-id="dd969-174">lastName</span><span class="sxs-lookup"><span data-stu-id="dd969-174">lastName</span></span>|<span data-ttu-id="dd969-175">string</span><span class="sxs-lookup"><span data-stu-id="dd969-175">string</span></span>|<span data-ttu-id="dd969-176">Cognome dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="dd969-177">companyName</span><span class="sxs-lookup"><span data-stu-id="dd969-177">companyName</span></span>|<span data-ttu-id="dd969-178">string</span><span class="sxs-lookup"><span data-stu-id="dd969-178">string</span></span>|<span data-ttu-id="dd969-179">Il nome della società dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="dd969-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="dd969-180">addresserEmail</span></span>|<span data-ttu-id="dd969-181">string</span><span class="sxs-lookup"><span data-stu-id="dd969-181">string</span></span>|<span data-ttu-id="dd969-182">Indirizzo di posta elettronica dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="dd969-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="dd969-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="dd969-184">string</span><span class="sxs-lookup"><span data-stu-id="dd969-184">string</span></span>|<span data-ttu-id="dd969-185">URL relativo per visualizzare l'analisi per l'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="dd969-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="dd969-186">subscriptions</span></span>|<span data-ttu-id="dd969-187">Raccolta di entità [Sottoscrizione](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="dd969-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="dd969-188">Le sottoscrizioni dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="dd969-189">scala Web</span><span class="sxs-lookup"><span data-stu-id="dd969-189">applications</span></span>|<span data-ttu-id="dd969-190">Raccolta di entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="dd969-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="dd969-191">Le applicazioni dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="dd969-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="dd969-192">changePasswordUrl</span></span>|<span data-ttu-id="dd969-193">string</span><span class="sxs-lookup"><span data-stu-id="dd969-193">string</span></span>|<span data-ttu-id="dd969-194">L'URL relativo per modificare la password dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="dd969-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="dd969-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="dd969-196">string</span><span class="sxs-lookup"><span data-stu-id="dd969-196">string</span></span>|<span data-ttu-id="dd969-197">L'URL relativo per modificare il nome e l'indirizzo di posta elettronica dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="dd969-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="dd969-198">canChangePassword</span></span>|<span data-ttu-id="dd969-199">boolean</span><span class="sxs-lookup"><span data-stu-id="dd969-199">boolean</span></span>|<span data-ttu-id="dd969-200">Indica se l'utente corrente può modificare la propria password.</span><span class="sxs-lookup"><span data-stu-id="dd969-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="dd969-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="dd969-201">isSystemUser</span></span>|<span data-ttu-id="dd969-202">boolean</span><span class="sxs-lookup"><span data-stu-id="dd969-202">boolean</span></span>|<span data-ttu-id="dd969-203">Indica se l'utente corrente è membro di uno dei [gruppi](api-management-key-concepts.md#groups) predefiniti.</span><span class="sxs-lookup"><span data-stu-id="dd969-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="dd969-204">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="dd969-204">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="dd969-205"><a name="Applications"></a> Applicazioni</span><span class="sxs-lookup"><span data-stu-id="dd969-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="dd969-206">Il modello **Applicazioni** consente di personalizzare la sezione applicazioni della pagina del profilo utente nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="dd969-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="dd969-207">![Pagina applicazioni account utente](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "Pagina applicazioni account utente in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="dd969-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="dd969-208">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="dd969-208">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="dd969-209">Controlli</span><span class="sxs-lookup"><span data-stu-id="dd969-209">Controls</span></span>  
 <span data-ttu-id="dd969-210">Questo modello può usare i [controlli di pagina](api-management-page-controls.md) seguenti.</span><span class="sxs-lookup"><span data-stu-id="dd969-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="dd969-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="dd969-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="dd969-212">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="dd969-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="dd969-213">I modelli [Profilo](#Profile), [Applicazioni](#Applications) e [Sottoscrizioni](#Subscriptions) condividono lo stesso modello di dati e ricevono gli stessi dati del modello.</span><span class="sxs-lookup"><span data-stu-id="dd969-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="dd969-214">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dd969-214">Property</span></span>|<span data-ttu-id="dd969-215">Tipo</span><span class="sxs-lookup"><span data-stu-id="dd969-215">Type</span></span>|<span data-ttu-id="dd969-216">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dd969-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="dd969-217">firstName</span><span class="sxs-lookup"><span data-stu-id="dd969-217">firstName</span></span>|<span data-ttu-id="dd969-218">string</span><span class="sxs-lookup"><span data-stu-id="dd969-218">string</span></span>|<span data-ttu-id="dd969-219">Nome dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-219">First name of the current user.</span></span>|  
|<span data-ttu-id="dd969-220">lastName</span><span class="sxs-lookup"><span data-stu-id="dd969-220">lastName</span></span>|<span data-ttu-id="dd969-221">string</span><span class="sxs-lookup"><span data-stu-id="dd969-221">string</span></span>|<span data-ttu-id="dd969-222">Cognome dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="dd969-223">companyName</span><span class="sxs-lookup"><span data-stu-id="dd969-223">companyName</span></span>|<span data-ttu-id="dd969-224">string</span><span class="sxs-lookup"><span data-stu-id="dd969-224">string</span></span>|<span data-ttu-id="dd969-225">Il nome della società dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="dd969-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="dd969-226">addresserEmail</span></span>|<span data-ttu-id="dd969-227">string</span><span class="sxs-lookup"><span data-stu-id="dd969-227">string</span></span>|<span data-ttu-id="dd969-228">Indirizzo di posta elettronica dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="dd969-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="dd969-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="dd969-230">string</span><span class="sxs-lookup"><span data-stu-id="dd969-230">string</span></span>|<span data-ttu-id="dd969-231">URL relativo per visualizzare l'analisi per l'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="dd969-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="dd969-232">subscriptions</span></span>|<span data-ttu-id="dd969-233">Raccolta di entità [Sottoscrizione](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="dd969-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="dd969-234">Le sottoscrizioni dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="dd969-235">scala Web</span><span class="sxs-lookup"><span data-stu-id="dd969-235">applications</span></span>|<span data-ttu-id="dd969-236">Raccolta di entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="dd969-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="dd969-237">Le applicazioni dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="dd969-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="dd969-238">changePasswordUrl</span></span>|<span data-ttu-id="dd969-239">string</span><span class="sxs-lookup"><span data-stu-id="dd969-239">string</span></span>|<span data-ttu-id="dd969-240">L'URL relativo per modificare la password dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="dd969-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="dd969-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="dd969-242">string</span><span class="sxs-lookup"><span data-stu-id="dd969-242">string</span></span>|<span data-ttu-id="dd969-243">L'URL relativo per modificare il nome e l'indirizzo di posta elettronica dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="dd969-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="dd969-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="dd969-244">canChangePassword</span></span>|<span data-ttu-id="dd969-245">boolean</span><span class="sxs-lookup"><span data-stu-id="dd969-245">boolean</span></span>|<span data-ttu-id="dd969-246">Indica se l'utente corrente può modificare la propria password.</span><span class="sxs-lookup"><span data-stu-id="dd969-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="dd969-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="dd969-247">isSystemUser</span></span>|<span data-ttu-id="dd969-248">boolean</span><span class="sxs-lookup"><span data-stu-id="dd969-248">boolean</span></span>|<span data-ttu-id="dd969-249">Indica se l'utente corrente è membro di uno dei [gruppi](api-management-key-concepts.md#groups) predefiniti.</span><span class="sxs-lookup"><span data-stu-id="dd969-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="dd969-250">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="dd969-250">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="dd969-251"><a name="UpdateAccountInfo"></a> Aggiorna info account</span><span class="sxs-lookup"><span data-stu-id="dd969-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="dd969-252">Il modello **Aggiorna info account** consente di personalizzare la pagina di **aggiornamento delle informazioni dell'account** nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="dd969-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="dd969-253">![Modelli del portale per sviluppatori, pagina di informazioni sull'account utente](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Modelli del portale per sviluppatori, pagina di informazioni sull'account utente in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="dd969-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="dd969-254">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="dd969-254">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="dd969-255">Controlli</span><span class="sxs-lookup"><span data-stu-id="dd969-255">Controls</span></span>  
 <span data-ttu-id="dd969-256">Questo modello potrebbe non usare i [controlli di pagina](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="dd969-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="dd969-257">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="dd969-257">Data model</span></span>  
 <span data-ttu-id="dd969-258">Entità [Informazioni sull'account utente](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="dd969-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="dd969-259">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="dd969-259">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="dd969-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd969-260">Next steps</span></span>
<span data-ttu-id="dd969-261">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dd969-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>