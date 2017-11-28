---
title: API REST di gestione aaaResource | Documenti Microsoft
description: Cenni preliminari hello autenticazione API REST di gestione risorse ed esempi di utilizzo
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="45a61-103">API REST di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45a61-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45a61-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="45a61-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="45a61-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="45a61-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="45a61-106">Portale</span><span class="sxs-lookup"><span data-stu-id="45a61-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="45a61-107">API REST</span><span class="sxs-lookup"><span data-stu-id="45a61-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="45a61-108">Dietro tooAzure ogni chiamata di gestione risorse, associate a ogni modello distribuito, dietro ogni account di archiviazione configurato non esistono API REST di uno o più chiamate toohello Azure del gestore delle risorse.</span><span class="sxs-lookup"><span data-stu-id="45a61-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="45a61-109">In questo argomento è dedicato toothose API e come è possibile chiamare senza usare affatto qualsiasi SDK.</span><span class="sxs-lookup"><span data-stu-id="45a61-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="45a61-110">Questo approccio è utile se si desidera il controllo completo di richieste tooAzure o se hello SDK per la lingua preferita non è disponibile o non supporta le operazioni di hello che è necessario.</span><span class="sxs-lookup"><span data-stu-id="45a61-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="45a61-111">In questo articolo non passa attraverso tutte le API viene esposta in Azure, ma alcune operazioni utilizzano come esempi delle modalità di connessione toothem.</span><span class="sxs-lookup"><span data-stu-id="45a61-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="45a61-112">Dopo aver compreso i concetti di base hello, è possibile leggere hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind informazioni dettagliate su come toouse hello restanti hello API.</span><span class="sxs-lookup"><span data-stu-id="45a61-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="45a61-113">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="45a61-113">Authentication</span></span>
<span data-ttu-id="45a61-114">L'autenticazione per Resource Manager viene gestita da Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="45a61-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="45a61-115">tooconnect tooany API, è necessario innanzitutto tooauthenticate con Azure AD tooreceive un token di autenticazione che è possibile passare a tooevery richiesta.</span><span class="sxs-lookup"><span data-stu-id="45a61-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="45a61-116">Come ci stiamo che descrive una chiamata pura direttamente toohello API REST, si presuppone che non si desidera tooauthenticate da viene richiesto un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="45a61-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="45a61-117">Si suppone inoltre che l'utente non usi i meccanismi di autenticazione a due fattori.</span><span class="sxs-lookup"><span data-stu-id="45a61-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="45a61-118">Pertanto, si costituiscono un'applicazione Azure AD e un'entità servizio che vengono utilizzati toolog in.</span><span class="sxs-lookup"><span data-stu-id="45a61-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="45a61-119">Ma si tenga presente che Azure AD supporta diverse procedure di autenticazione e tutti gli elementi può essere utilizzato tooretrieve tale token di autenticazione necessarie per le successive richieste API.</span><span class="sxs-lookup"><span data-stu-id="45a61-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="45a61-120">Per istruzioni dettagliate, vedere [Creare un'applicazione e un'entità servizio di Azure AD](resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="45a61-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="45a61-121">Generazione di un token di accesso</span><span class="sxs-lookup"><span data-stu-id="45a61-121">Generating an Access Token</span></span>
<span data-ttu-id="45a61-122">L'autenticazione con Azure AD viene eseguita da una chiamata in uscita tooAzure AD, disponibile all'indirizzo login.microsoftonline.com. tooauthenticate, è necessario hello toohave le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="45a61-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="45a61-123">ID del Tenant Azure Active Directory (nome ad Azure AD si utilizza toolog in hello, spesso hello come la società ma non necessaria)</span><span class="sxs-lookup"><span data-stu-id="45a61-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="45a61-124">ID dell'applicazione (prese durante il passaggio della creazione dell'applicazione hello Azure AD)</span><span class="sxs-lookup"><span data-stu-id="45a61-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="45a61-125">Password (che è stata selezionata durante la creazione di hello applicazione Azure AD)</span><span class="sxs-lookup"><span data-stu-id="45a61-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="45a61-126">In hello seguente richiesta HTTP, assicurarsi che tooreplace "ID Tenant di Azure AD," "ID applicazione" e "Password" con i valori corretti di hello.</span><span class="sxs-lookup"><span data-stu-id="45a61-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="45a61-127">**Richiesta HTTP generica:**</span><span class="sxs-lookup"><span data-stu-id="45a61-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="45a61-128">... verrà (se l'autenticazione ha esito positivo) produce una toohello simile di risposta seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="45a61-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
<span data-ttu-id="45a61-129">(access_token hello in hello risposta precedente sono stati tooincrease abbreviato leggibilità)</span><span class="sxs-lookup"><span data-stu-id="45a61-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="45a61-130">**Generazione del token di accesso con Bash:**</span><span class="sxs-lookup"><span data-stu-id="45a61-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="45a61-131">**Generazione del token di accesso con Powershell:**</span><span class="sxs-lookup"><span data-stu-id="45a61-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="45a61-132">risposta Hello contiene un token di accesso, informazioni sulla durata token è valido e informazioni su quali risorse è possibile usare tale token per.</span><span class="sxs-lookup"><span data-stu-id="45a61-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="45a61-133">token di accesso Hello ricevuti nella chiamata HTTP precedente hello devono essere passati per toohello richiesta tutte le API di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="45a61-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="45a61-134">Viene passato come un valore di intestazione denominato "Authorization" con valore hello "Portatore YOUR_ACCESS_TOKEN".</span><span class="sxs-lookup"><span data-stu-id="45a61-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="45a61-135">Si noti lo spazio di hello tra "Bearer" e il token di accesso.</span><span class="sxs-lookup"><span data-stu-id="45a61-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="45a61-136">Come si può vedere dal hello sopra i risultati di HTTP, hello token è valido per un determinato periodo di tempo durante i quali è necessario memorizzare nella cache e riutilizzare i token stesso.</span><span class="sxs-lookup"><span data-stu-id="45a61-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="45a61-137">Anche se è possibile tooauthenticate con Azure AD per ogni chiamata API, sarebbe particolarmente inefficiente.</span><span class="sxs-lookup"><span data-stu-id="45a61-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="45a61-138">Chiamata alle API REST di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="45a61-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="45a61-139">In questo argomento Usa solo alcune API tooexplain hello l'utilizzo di base di operazioni REST hello.</span><span class="sxs-lookup"><span data-stu-id="45a61-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="45a61-140">Per informazioni su tutte le operazioni di hello, vedere [le API REST di gestione risorse di Azure](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="45a61-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="45a61-141">Elenco di tutte le sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="45a61-141">List all subscriptions</span></span>
<span data-ttu-id="45a61-142">Una delle operazioni di hello più semplice che è possibile eseguire è toolist hello sottoscrizioni disponibili che è possibile accedere.</span><span class="sxs-lookup"><span data-stu-id="45a61-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="45a61-143">Hello seguito richiesta, è visualizzato come token di accesso hello viene passato come un'intestazione di:</span><span class="sxs-lookup"><span data-stu-id="45a61-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="45a61-144">Sostituire YOUR_ACCESS_TOKEN con il token di accesso vero e proprio.</span><span class="sxs-lookup"><span data-stu-id="45a61-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="45a61-145">... e di conseguenza, si visualizza un elenco di sottoscrizioni che tooaccess è consentita da questa entità servizio</span><span class="sxs-lookup"><span data-stu-id="45a61-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="45a61-146">(Gli ID sottoscrizione seguenti sono stati abbreviati per renderli più leggibili)</span><span class="sxs-lookup"><span data-stu-id="45a61-146">(Subscription IDs have been shortened for readability)</span></span>

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="45a61-147">Elencare tutti i gruppi di risorse in una sottoscrizione specifica</span><span class="sxs-lookup"><span data-stu-id="45a61-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="45a61-148">Tutte le risorse disponibili con le API di gestione risorse di hello sono annidate all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="45a61-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="45a61-149">È possibile eseguire query di gestione risorse di gruppi di risorse esistente nella sottoscrizione tramite hello seguente richiesta HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="45a61-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="45a61-150">Si noti come ID di sottoscrizione hello viene passato come parte dell'URL hello questo momento.</span><span class="sxs-lookup"><span data-stu-id="45a61-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="45a61-151">(Sostituire YOUR_ACCESS_TOKEN e SUBSCRIPTION_ID con il token di accesso e l'ID sottoscrizione effettivi)</span><span class="sxs-lookup"><span data-stu-id="45a61-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="45a61-152">Hello risposta ottenuta varia a seconda se si dispone di gruppi di risorse definiti e in tal caso, il numero.</span><span class="sxs-lookup"><span data-stu-id="45a61-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="45a61-153">(Gli ID sottoscrizione seguenti sono stati abbreviati per renderli più leggibili)</span><span class="sxs-lookup"><span data-stu-id="45a61-153">(Subscription IDs have been shortened for readability)</span></span>

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="45a61-154">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="45a61-154">Create a resource group</span></span>
<span data-ttu-id="45a61-155">Finora è stato solo stato query hello le API di gestione risorse per informazioni.</span><span class="sxs-lookup"><span data-stu-id="45a61-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="45a61-156">È ora è creare alcune risorse e per iniziare, hello più semplice di visualizzarli tutti, un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="45a61-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="45a61-157">Hello richiesta HTTP seguente crea un gruppo di risorse in una regione di propria scelta e aggiunge tooit un tag.</span><span class="sxs-lookup"><span data-stu-id="45a61-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="45a61-158">(Sostituire YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME con l'effettivo Token di accesso, ID sottoscrizione e nome del gruppo di risorse da toocreate hello)</span><span class="sxs-lookup"><span data-stu-id="45a61-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

<span data-ttu-id="45a61-159">Se ha esito positivo, si otterrà una risposta simile toohello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="45a61-159">If successful, you get a response that is similar toohello following response:</span></span>

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="45a61-160">È stato creato un gruppo di risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="45a61-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="45a61-161">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="45a61-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="45a61-162">Distribuire un gruppo di risorse tooa di risorse mediante un modello di gestione risorse</span><span class="sxs-lookup"><span data-stu-id="45a61-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="45a61-163">Con Gestione risorse, è possibile distribuire le risorse usando i modelli.</span><span class="sxs-lookup"><span data-stu-id="45a61-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="45a61-164">Un modello definisce diverse risorse e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="45a61-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="45a61-165">In questa sezione si presuppone che si ha familiarità con i modelli di gestione risorse e solo illustrare come API hello toomake chiama toostart distribuzione.</span><span class="sxs-lookup"><span data-stu-id="45a61-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="45a61-166">Per altre informazioni sulla creazione dei modelli, vedere [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md) (Creazione di modelli di Gestione risorse).</span><span class="sxs-lookup"><span data-stu-id="45a61-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="45a61-167">Distribuzione di un modello non differiscono molto toohow è chiamare altre API.</span><span class="sxs-lookup"><span data-stu-id="45a61-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="45a61-168">Un aspetto importante è che la distribuzione di un modello può richiedere molto tempo.</span><span class="sxs-lookup"><span data-stu-id="45a61-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="45a61-169">Restituisce solo una chiamata API Hello ed è attivo tooyou come tooquery developer per lo stato di hello distribuzione toofind out quando hello distribuzione viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="45a61-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="45a61-170">Per ulteriori informazioni, vedere [Track asynchronous Azure operations](resource-manager-async-operations.md) (Tenere traccia delle operazioni asincrone di Azure).</span><span class="sxs-lookup"><span data-stu-id="45a61-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="45a61-171">Per questo esempio, verrà usato un modello esposto pubblicamente disponibile su [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="45a61-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="45a61-172">modello Hello che utilizziamo consente di distribuire un'area di Stati Uniti occidentali toohello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="45a61-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="45a61-173">Anche se viene utilizzato un modello disponibile in un archivio pubblico come GitHub, è invece possibile passare modello completo hello come parte della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="45a61-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="45a61-174">Si noti che vengono forniti i valori di parametro nella richiesta di hello utilizzati all'interno di hello distribuzione modello.</span><span class="sxs-lookup"><span data-stu-id="45a61-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="45a61-175">(Sostituire SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD e DNS_NAME_FOR_PUBLIC_IP toovalues appropriato per la richiesta)</span><span class="sxs-lookup"><span data-stu-id="45a61-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

<span data-ttu-id="45a61-176">risposta JSON lunghi Hello per questa richiesta è stato omesso tooimprove leggibilità di questa documentazione.</span><span class="sxs-lookup"><span data-stu-id="45a61-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="45a61-177">risposta Hello contiene informazioni sulla distribuzione basata su modelli hello creato.</span><span class="sxs-lookup"><span data-stu-id="45a61-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45a61-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45a61-178">Next steps</span></span>

- <span data-ttu-id="45a61-179">toolearn sulla gestione di operazioni asincrone di REST, vedere [tenere traccia delle operazioni asincrone di Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="45a61-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
