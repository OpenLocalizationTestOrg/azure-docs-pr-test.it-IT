---
title: controlli di pagina di gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui controlli della pagina hello disponibili per l'utilizzo nei modelli di portale per sviluppatori in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="f93a9-103">Controlli pagina in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="f93a9-103">Azure API Management page controls</span></span>
<span data-ttu-id="f93a9-104">Gestione API di Azure fornisce i seguenti controlli per l'utilizzo nei modelli del portale per sviluppatori di hello hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="f93a9-105">un controllo, toouse posizionarlo nel percorso di hello desiderato nel modello di portale per sviluppatori di hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="f93a9-106">Alcuni controlli, ad esempio hello [app azioni](#app-actions) di controllo, dispone di parametri, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="f93a9-107">valori Hello hello parametri vengono passati come parte del modello di dati hello per modello hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="f93a9-108">Nella maggior parte dei casi, è possibile semplicemente incollare hello disponibili esempio per ogni controllo toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="f93a9-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="f93a9-109">Per ulteriori informazioni sui valori dei parametri di hello, è possibile visualizzare sezione modello di dati hello per ogni modello in cui è possibile utilizzare un controllo.</span><span class="sxs-lookup"><span data-stu-id="f93a9-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="f93a9-110">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="f93a9-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="f93a9-111">Controlli pagina per i modelli nel portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="f93a9-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="f93a9-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="f93a9-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="f93a9-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="f93a9-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="f93a9-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="f93a9-115">provider</span><span class="sxs-lookup"><span data-stu-id="f93a9-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="f93a9-116">search-control</span><span class="sxs-lookup"><span data-stu-id="f93a9-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="f93a9-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="f93a9-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="f93a9-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="f93a9-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="f93a9-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="f93a9-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="f93a9-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="f93a9-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="f93a9-121">Hello `app-actions` controllo fornisce un'interfaccia utente per l'interazione con le applicazioni in una pagina del profilo utente hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="f93a9-122">![Controllo app&amp;#45;actions](./media/api-management-page-controls/APIM-app-actions-control.png "Controllo app-actions in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="f93a9-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="f93a9-123">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f93a9-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="f93a9-124">parameters</span><span class="sxs-lookup"><span data-stu-id="f93a9-124">Parameters</span></span>  
  
|<span data-ttu-id="f93a9-125">Parametro</span><span class="sxs-lookup"><span data-stu-id="f93a9-125">Parameter</span></span>|<span data-ttu-id="f93a9-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f93a9-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="f93a9-127">appId</span><span class="sxs-lookup"><span data-stu-id="f93a9-127">appId</span></span>|<span data-ttu-id="f93a9-128">id di Hello dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="f93a9-129">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-129">Developer portal templates</span></span>  
 <span data-ttu-id="f93a9-130">Hello `app-actions` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="f93a9-131">Applicazioni</span><span class="sxs-lookup"><span data-stu-id="f93a9-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="f93a9-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="f93a9-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="f93a9-133">Hello `basic-signin` controllo fornisce un controllo per la raccolta di accesso degli utenti nelle informazioni di hello Accedi pagina nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="f93a9-134">![Controllo basic&#45;signin](./media/api-management-page-controls/APIM-basic-signin-control.png "Controllo basic-signin in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="f93a9-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="f93a9-135">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f93a9-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="f93a9-136">parameters</span><span class="sxs-lookup"><span data-stu-id="f93a9-136">Parameters</span></span>  
 <span data-ttu-id="f93a9-137">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="f93a9-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="f93a9-138">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-138">Developer portal templates</span></span>  
 <span data-ttu-id="f93a9-139">Hello `basic-signin` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="f93a9-140">Accesso</span><span class="sxs-lookup"><span data-stu-id="f93a9-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="f93a9-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="f93a9-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="f93a9-142">Hello `paging-control` offre funzionalità di paging in developer pagine del portale che consentono di visualizzare un elenco di elementi.</span><span class="sxs-lookup"><span data-stu-id="f93a9-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="f93a9-143">![paging-control](./media/api-management-page-controls/APIM-paging-control.png "paging-control in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="f93a9-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="f93a9-144">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f93a9-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="f93a9-145">parameters</span><span class="sxs-lookup"><span data-stu-id="f93a9-145">Parameters</span></span>  
 <span data-ttu-id="f93a9-146">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="f93a9-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="f93a9-147">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-147">Developer portal templates</span></span>  
 <span data-ttu-id="f93a9-148">Hello `paging-control` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="f93a9-149">Elenco API</span><span class="sxs-lookup"><span data-stu-id="f93a9-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="f93a9-150">Elenco di problemi</span><span class="sxs-lookup"><span data-stu-id="f93a9-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="f93a9-151">Elenco dei prodotti</span><span class="sxs-lookup"><span data-stu-id="f93a9-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="f93a9-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="f93a9-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="f93a9-153">Hello `providers` controllo fornisce un controllo per la selezione dei provider di autenticazione in una pagina nel portale per sviluppatori hello hello accesso.</span><span class="sxs-lookup"><span data-stu-id="f93a9-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="f93a9-154">![Controllo providers](./media/api-management-page-controls/APIM-providers-control.png "Controllo providers in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="f93a9-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="f93a9-155">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f93a9-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="f93a9-156">parameters</span><span class="sxs-lookup"><span data-stu-id="f93a9-156">Parameters</span></span>  
 <span data-ttu-id="f93a9-157">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="f93a9-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="f93a9-158">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-158">Developer portal templates</span></span>  
 <span data-ttu-id="f93a9-159">Hello `providers` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="f93a9-160">Accesso</span><span class="sxs-lookup"><span data-stu-id="f93a9-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="f93a9-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="f93a9-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="f93a9-162">Hello `search-control` offre funzionalità di ricerca in developer pagine del portale che consentono di visualizzare un elenco di elementi.</span><span class="sxs-lookup"><span data-stu-id="f93a9-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="f93a9-163">![search- control](./media/api-management-page-controls/APIM-search-control.png "search-control in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="f93a9-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="f93a9-164">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f93a9-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="f93a9-165">parameters</span><span class="sxs-lookup"><span data-stu-id="f93a9-165">Parameters</span></span>  
 <span data-ttu-id="f93a9-166">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="f93a9-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="f93a9-167">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-167">Developer portal templates</span></span>  
 <span data-ttu-id="f93a9-168">Hello `search-control` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="f93a9-169">Elenco API</span><span class="sxs-lookup"><span data-stu-id="f93a9-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="f93a9-170">Elenco dei prodotti</span><span class="sxs-lookup"><span data-stu-id="f93a9-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="f93a9-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="f93a9-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="f93a9-172">Hello `sign-up` controllo offre un controllo per la raccolta di informazioni sul profilo utente nella pagina nel portale per sviluppatori hello di iscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="f93a9-173">![Controllo sign&amp;#45;up](./media/api-management-page-controls/APIM-sign-up-control.png "Controllo sign-up in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="f93a9-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="f93a9-174">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f93a9-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="f93a9-175">parameters</span><span class="sxs-lookup"><span data-stu-id="f93a9-175">Parameters</span></span>  
 <span data-ttu-id="f93a9-176">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="f93a9-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="f93a9-177">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-177">Developer portal templates</span></span>  
 <span data-ttu-id="f93a9-178">Hello `sign-up` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="f93a9-179">Iscrizione</span><span class="sxs-lookup"><span data-stu-id="f93a9-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="f93a9-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="f93a9-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="f93a9-181">Hello `subscribe-button` fornisce un controllo per la sottoscrizione di un prodotto tooa utente.</span><span class="sxs-lookup"><span data-stu-id="f93a9-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="f93a9-182">![Controllo subscribe&amp;#45;button](./media/api-management-page-controls/APIM-subscribe-button-control.png "Controllo subscribe-button in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="f93a9-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="f93a9-183">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f93a9-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="f93a9-184">parameters</span><span class="sxs-lookup"><span data-stu-id="f93a9-184">Parameters</span></span>  
 <span data-ttu-id="f93a9-185">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="f93a9-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="f93a9-186">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-186">Developer portal templates</span></span>  
 <span data-ttu-id="f93a9-187">Hello `subscribe-button` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="f93a9-188">Prodotto</span><span class="sxs-lookup"><span data-stu-id="f93a9-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="f93a9-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="f93a9-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="f93a9-190">Hello `subscription-cancel` controllo fornisce un controllo per l'annullamento di un prodotto tooa sottoscrizione nella pagina del profilo utente hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="f93a9-191">![Controllo subscription&amp;#45;cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Controllo subscription-cancel in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="f93a9-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="f93a9-192">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f93a9-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="f93a9-193">parameters</span><span class="sxs-lookup"><span data-stu-id="f93a9-193">Parameters</span></span>  
  
|<span data-ttu-id="f93a9-194">Parametro</span><span class="sxs-lookup"><span data-stu-id="f93a9-194">Parameter</span></span>|<span data-ttu-id="f93a9-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f93a9-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="f93a9-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="f93a9-196">subscriptionId</span></span>|<span data-ttu-id="f93a9-197">id di Hello di hello toocancel di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f93a9-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="f93a9-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="f93a9-198">cancelUrl</span></span>|<span data-ttu-id="f93a9-199">sottoscrizione Hello annullare URL.</span><span class="sxs-lookup"><span data-stu-id="f93a9-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="f93a9-200">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="f93a9-200">Developer portal templates</span></span>  
 <span data-ttu-id="f93a9-201">Hello `subscription-cancel` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f93a9-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="f93a9-202">Prodotto</span><span class="sxs-lookup"><span data-stu-id="f93a9-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="f93a9-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f93a9-203">Next steps</span></span>
<span data-ttu-id="f93a9-204">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f93a9-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
