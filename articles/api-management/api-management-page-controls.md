---
title: Controlli pagina in Gestione API di Azure | Microsoft Docs
description: Informazioni sui controlli pagina disponibili per l'uso nei modelli del portale per sviluppatori in Gestione API di Azure.
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
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="78dff-103">Controlli pagina in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="78dff-103">Azure API Management page controls</span></span>
<span data-ttu-id="78dff-104">Gestione API di Azure mette a disposizione i seguenti controlli per l'uso nei modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="78dff-105">Per usare un controllo, inserirlo nella posizione desiderata nel modello del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="78dff-106">Alcuni controlli, ad esempio [app-actions](#app-actions), dispongono di parametri, come mostrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="78dff-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="78dff-107">I valori per i parametri vengono passati come parte del modello di dati per il modello.</span><span class="sxs-lookup"><span data-stu-id="78dff-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="78dff-108">Nella maggior parte dei casi, basta incollare ciascun controllo nell'esempio fornito e funzionerà correttamente.</span><span class="sxs-lookup"><span data-stu-id="78dff-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="78dff-109">Per ulteriori informazioni sui valori di parametro, è possibile vedere la sezione sul modello dei dati per ciascun modello in cui potrebbe essere usato un controllo.</span><span class="sxs-lookup"><span data-stu-id="78dff-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="78dff-110">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="78dff-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="78dff-111">Controlli pagina per i modelli nel portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="78dff-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="78dff-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="78dff-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="78dff-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="78dff-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="78dff-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="78dff-115">provider</span><span class="sxs-lookup"><span data-stu-id="78dff-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="78dff-116">search-control</span><span class="sxs-lookup"><span data-stu-id="78dff-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="78dff-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="78dff-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="78dff-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="78dff-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="78dff-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="78dff-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="78dff-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="78dff-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="78dff-121">Il controllo `app-actions` offre un'interfaccia utente per interagire con le applicazioni nella pagina del profilo utente nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="78dff-122">![Controllo app&#45;actions](./media/api-management-page-controls/APIM-app-actions-control.png "Controllo app-actions in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="78dff-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="78dff-123">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="78dff-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="78dff-124">parameters</span><span class="sxs-lookup"><span data-stu-id="78dff-124">Parameters</span></span>  
  
|<span data-ttu-id="78dff-125">Parametro</span><span class="sxs-lookup"><span data-stu-id="78dff-125">Parameter</span></span>|<span data-ttu-id="78dff-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="78dff-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="78dff-127">appId</span><span class="sxs-lookup"><span data-stu-id="78dff-127">appId</span></span>|<span data-ttu-id="78dff-128">L'ID dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="78dff-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="78dff-129">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-129">Developer portal templates</span></span>  
 <span data-ttu-id="78dff-130">È possibile usare il controllo `app-actions` nei seguenti modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="78dff-131">Applicazioni</span><span class="sxs-lookup"><span data-stu-id="78dff-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="78dff-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="78dff-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="78dff-133">Il controllo `basic-signin` permette di raccogliere le informazioni di accesso degli utenti nella pagina di accesso del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="78dff-134">![Controllo basic&#45;signin](./media/api-management-page-controls/APIM-basic-signin-control.png "Controllo basic-signin in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="78dff-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="78dff-135">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="78dff-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="78dff-136">parameters</span><span class="sxs-lookup"><span data-stu-id="78dff-136">Parameters</span></span>  
 <span data-ttu-id="78dff-137">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="78dff-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="78dff-138">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-138">Developer portal templates</span></span>  
 <span data-ttu-id="78dff-139">È possibile usare il controllo `basic-signin` nei seguenti modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="78dff-140">Accesso</span><span class="sxs-lookup"><span data-stu-id="78dff-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="78dff-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="78dff-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="78dff-142">Il controllo `paging-control` offre funzionalità di paging nelle pagine del portale per sviluppatore che presentano un elenco di elementi.</span><span class="sxs-lookup"><span data-stu-id="78dff-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="78dff-143">![paging-control](./media/api-management-page-controls/APIM-paging-control.png "paging-control in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="78dff-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="78dff-144">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="78dff-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="78dff-145">parameters</span><span class="sxs-lookup"><span data-stu-id="78dff-145">Parameters</span></span>  
 <span data-ttu-id="78dff-146">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="78dff-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="78dff-147">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-147">Developer portal templates</span></span>  
 <span data-ttu-id="78dff-148">È possibile usare il controllo `paging-control` nei seguenti modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="78dff-149">Elenco API</span><span class="sxs-lookup"><span data-stu-id="78dff-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="78dff-150">Elenco di problemi</span><span class="sxs-lookup"><span data-stu-id="78dff-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="78dff-151">Elenco dei prodotti</span><span class="sxs-lookup"><span data-stu-id="78dff-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="78dff-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="78dff-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="78dff-153">Il controllo `providers` permette di selezionare i provider di autenticazione nella pagina di accesso del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="78dff-154">![Controllo providers](./media/api-management-page-controls/APIM-providers-control.png "Controllo providers in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="78dff-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="78dff-155">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="78dff-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="78dff-156">parameters</span><span class="sxs-lookup"><span data-stu-id="78dff-156">Parameters</span></span>  
 <span data-ttu-id="78dff-157">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="78dff-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="78dff-158">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-158">Developer portal templates</span></span>  
 <span data-ttu-id="78dff-159">È possibile usare il controllo `providers` nei seguenti modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="78dff-160">Accesso</span><span class="sxs-lookup"><span data-stu-id="78dff-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="78dff-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="78dff-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="78dff-162">Il controllo `search-control` offre funzionalità di ricerca nelle pagine del portale per sviluppatore che presentano un elenco di elementi.</span><span class="sxs-lookup"><span data-stu-id="78dff-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="78dff-163">![search- control](./media/api-management-page-controls/APIM-search-control.png "search-control in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="78dff-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="78dff-164">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="78dff-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="78dff-165">parameters</span><span class="sxs-lookup"><span data-stu-id="78dff-165">Parameters</span></span>  
 <span data-ttu-id="78dff-166">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="78dff-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="78dff-167">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-167">Developer portal templates</span></span>  
 <span data-ttu-id="78dff-168">È possibile usare il controllo `search-control` nei seguenti modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="78dff-169">Elenco API</span><span class="sxs-lookup"><span data-stu-id="78dff-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="78dff-170">Elenco dei prodotti</span><span class="sxs-lookup"><span data-stu-id="78dff-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="78dff-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="78dff-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="78dff-172">Il controllo `sign-up` permette di raccogliere le informazioni di profilo degli utenti nella pagina di iscrizione del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="78dff-173">![Controllo sign&#45;up](./media/api-management-page-controls/APIM-sign-up-control.png "Controllo sign-up in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="78dff-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="78dff-174">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="78dff-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="78dff-175">parameters</span><span class="sxs-lookup"><span data-stu-id="78dff-175">Parameters</span></span>  
 <span data-ttu-id="78dff-176">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="78dff-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="78dff-177">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-177">Developer portal templates</span></span>  
 <span data-ttu-id="78dff-178">È possibile usare il controllo `sign-up` nei seguenti modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="78dff-179">Iscrizione</span><span class="sxs-lookup"><span data-stu-id="78dff-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="78dff-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="78dff-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="78dff-181">Il controllo `subscribe-button` consente di sottoscrivere un utente a un prodotto.</span><span class="sxs-lookup"><span data-stu-id="78dff-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="78dff-182">![Controllo subscribe&#45;button](./media/api-management-page-controls/APIM-subscribe-button-control.png "Controllo subscribe-button in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="78dff-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="78dff-183">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="78dff-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="78dff-184">parameters</span><span class="sxs-lookup"><span data-stu-id="78dff-184">Parameters</span></span>  
 <span data-ttu-id="78dff-185">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="78dff-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="78dff-186">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-186">Developer portal templates</span></span>  
 <span data-ttu-id="78dff-187">È possibile usare il controllo `subscribe-button` nei seguenti modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="78dff-188">Prodotto</span><span class="sxs-lookup"><span data-stu-id="78dff-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="78dff-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="78dff-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="78dff-190">Il controllo `subscription-cancel` consente di annullare la sottoscrizione a un prodotto nella pagina di profilo dell'utente nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="78dff-191">![Controllo subscription&#45;cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Controllo subscription-cancel in Gestione API di Azure")</span><span class="sxs-lookup"><span data-stu-id="78dff-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="78dff-192">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="78dff-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="78dff-193">parameters</span><span class="sxs-lookup"><span data-stu-id="78dff-193">Parameters</span></span>  
  
|<span data-ttu-id="78dff-194">Parametro</span><span class="sxs-lookup"><span data-stu-id="78dff-194">Parameter</span></span>|<span data-ttu-id="78dff-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="78dff-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="78dff-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="78dff-196">subscriptionId</span></span>|<span data-ttu-id="78dff-197">L'ID della sottoscrizione da annullare.</span><span class="sxs-lookup"><span data-stu-id="78dff-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="78dff-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="78dff-198">cancelUrl</span></span>|<span data-ttu-id="78dff-199">L'URL di annullamento della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="78dff-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="78dff-200">Modelli del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="78dff-200">Developer portal templates</span></span>  
 <span data-ttu-id="78dff-201">È possibile usare il controllo `subscription-cancel` nei seguenti modelli del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="78dff-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="78dff-202">Prodotto</span><span class="sxs-lookup"><span data-stu-id="78dff-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="78dff-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78dff-203">Next steps</span></span>
<span data-ttu-id="78dff-204">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="78dff-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>