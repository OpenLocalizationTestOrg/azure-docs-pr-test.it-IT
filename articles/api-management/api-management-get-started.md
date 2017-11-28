---
title: aaaManage l'API prima in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toocreate API, operazioni di aggiunta e Introduzione a gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="8d0ac-103">Gestire la prima API in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="8d0ac-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="8d0ac-104"><a name="overview"> </a>Panoramica</span><span class="sxs-lookup"><span data-stu-id="8d0ac-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="8d0ac-105">Questa guida Mostra come tooquickly iniziare utilizzando Gestione API di Azure e rendere la prima chiamata API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="8d0ac-106"><a name="concepts"></a>Cos'è Gestione API di Azure?</span><span class="sxs-lookup"><span data-stu-id="8d0ac-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="8d0ac-107">È possibile utilizzare Gestione API di Azure tootake qualsiasi back-end e avviare un programma API flessibile basato su di esso.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="8d0ac-108">Gli scenari comuni includono:</span><span class="sxs-lookup"><span data-stu-id="8d0ac-108">Common scenarios include:</span></span>

* <span data-ttu-id="8d0ac-109">**protezione dell'infrastruttura mobile** con la delega dell'accesso con le chiavi API, la prevenzione degli attacchi DOS con la limitazione oppure l'uso di criteri di sicurezza avanzata come la convalida dei token JWT.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="8d0ac-110">**Abilitazione ecosistemi partner ISV** tramite l'offerta di caricamento rapido partner tramite developer hello portale e compila un toodecouple facciata API da implementazioni interne che non sono particolarmente adatto per l'utilizzo di partner.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="8d0ac-111">**Esegue un programma API interno** offrendo una posizione centralizzata per hello organizzazione toocommunicate sulla disponibilità di hello e più recenti modifiche apportate tooAPIs, controllo di accesso in base agli account aziendali, tutti basati su un canale protetto tra Hello gateway API e hello back-end.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="8d0ac-112">sistema Hello è costituito da hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="8d0ac-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="8d0ac-113">Hello **gateway API** hello endpoint che:</span><span class="sxs-lookup"><span data-stu-id="8d0ac-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="8d0ac-114">Accetta API chiama e li indirizza tooyour ai back-end.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="8d0ac-115">Verifica le chiavi API, i token JWT, i certificati e altre credenziali.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="8d0ac-116">Applica le quote di utilizzo e i limiti di frequenza.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="8d0ac-117">Trasforma l'API volo hello senza modifiche al codice.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="8d0ac-118">Memorizza nella cache le risposte di back-end durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="8d0ac-119">Registra i metadati della chiamata a scopi di analisi.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="8d0ac-120">Hello **portale di pubblicazione** è l'interfaccia amministrativa di hello in cui impostare il programma di API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="8d0ac-121">Può essere usato per:</span><span class="sxs-lookup"><span data-stu-id="8d0ac-121">Use it to:</span></span>
  
  * <span data-ttu-id="8d0ac-122">Definire o importare lo schema API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-122">Define or import API schema.</span></span>
  * <span data-ttu-id="8d0ac-123">Creare pacchetti di API nei prodotti.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-123">Package APIs into products.</span></span>
  * <span data-ttu-id="8d0ac-124">Impostare i criteri, ad esempio quote o di trasformazioni su hello API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="8d0ac-125">Ottenere informazioni dall'analisi.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="8d0ac-126">Gestire gli utenti.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-126">Manage users.</span></span>
* <span data-ttu-id="8d0ac-127">Hello **portale per sviluppatori** funge da presenza di hello web principale per gli sviluppatori, in cui è possibile:</span><span class="sxs-lookup"><span data-stu-id="8d0ac-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="8d0ac-128">Leggere la documentazione relativa alle API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-128">Read API documentation.</span></span>
  * <span data-ttu-id="8d0ac-129">Provare a utilizzare un'API tramite la console interattiva hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="8d0ac-130">Creare un account e sottoscrizione chiavi tooget API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="8d0ac-131">Accedere all'analisi di utilizzo personalizzata.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="8d0ac-132"><a name="create-service-instance"></a>Creare un'istanza di Gestione API</span><span class="sxs-lookup"><span data-stu-id="8d0ac-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="8d0ac-133">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="8d0ac-134">Se non si ha un account, è possibile creare un account gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="8d0ac-135">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="8d0ac-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="8d0ac-136">Hello primo passaggio nell'utilizzo di gestione API consiste toocreate un'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="8d0ac-137">Accedi toohello [portale Azure] [ Azure Portal] e fare clic su **New**, **Web e dispositivi mobili**, **gestione API**.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![API Management new instance][api-management-create-instance-menu]

<span data-ttu-id="8d0ac-139">Per **nome**, specificare un toouse nome di dominio secondario univoco per l'URL del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="8d0ac-140">Scegliere hello desiderato **sottoscrizione**, **gruppo di risorse** e **percorso** per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="8d0ac-141">Immettere **Contoso Ltd.** per hello **nome organizzazione**e immettere l'indirizzo di posta elettronica in hello **posta elettronica amministratore** campo.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="8d0ac-142">Questo indirizzo di posta elettronica viene utilizzato per notifiche da hello sistema gestione API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="8d0ac-143">Per ulteriori informazioni, vedere [come tooconfigure notifiche e modelli in Gestione API di Azure di posta elettronica][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8d0ac-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![New API Management service][api-management-create-instance-step1]

<span data-ttu-id="8d0ac-145">Le istanze del servizio Gestione API sono disponibili in tre livelli: Developer, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="8d0ac-146">Hello livello sviluppatore è per lo sviluppo, test e i programmi API pilota in cui la disponibilità elevata non rappresenta un problema.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="8d0ac-147">In hello Standard e i livelli Premium, è possibile ridimensionare il toohandle numero di unità riservata maggiore quantità di traffico.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="8d0ac-148">livelli Standard e Premium Hello forniscono al servizio Gestione API hello la maggior parte delle capacità di elaborazione e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="8d0ac-149">È possibile completare questa esercitazione usando qualsiasi livello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="8d0ac-150">Per altre informazioni sui livelli di Gestione API, vedere [Gestione API - Prezzi][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="8d0ac-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="8d0ac-151">Fare clic su **crea** toostart provisioning all'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-151">Click **Create** toostart provisioning your service instance.</span></span>

![New API Management service][api-management-instance-created]

<span data-ttu-id="8d0ac-153">Una volta creata l'istanza del servizio hello, passaggio successivo hello toocreate o importare un'API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="8d0ac-154"><a name="create-api"></a>Importare un'API</span><span class="sxs-lookup"><span data-stu-id="8d0ac-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="8d0ac-155">Un'API rappresenta un set di operazioni che possono essere richiamate da un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="8d0ac-156">Le operazioni dell'API sono servizi web tooexisting elaborate.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="8d0ac-157">È possibile creare le API (e aggiungere operazioni) in modo manuale oppure è possibile importarle.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="8d0ac-158">In questa esercitazione, verranno importate hello API per un servizio web Calcolatrice di esempio forniti da Microsoft e ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="8d0ac-159">Per informazioni sulla creazione di un'API e l'aggiunta manuale di operazioni, vedere [come toocreate API](api-management-howto-create-apis.md) e [come tooadd operazioni tooan API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="8d0ac-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="8d0ac-160">Le API vengono configurate dal portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="8d0ac-161">tooreach, fare clic su **portale di pubblicazione** dalla barra degli strumenti del servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="8d0ac-163">Calcolatrice hello tooimport API, fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **importazione API**.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Pulsante Importa API][api-management-import-api]

<span data-ttu-id="8d0ac-165">Eseguire hello seguendo i passaggi tooconfigure hello calcolatrice API:</span><span class="sxs-lookup"><span data-stu-id="8d0ac-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="8d0ac-166">Fare clic su **From URL**, immettere **http://calcapi.cloudapp.net/calcapi.json** in hello **URL del documento di specifica** testo, quindi scegliere hello **Swagger**  pulsante di opzione.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="8d0ac-167">Tipo **calc** in hello **suffisso URL di Web API** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="8d0ac-168">Fare clic nella hello **prodotti (facoltativi)** e scegliere **Starter**.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="8d0ac-169">Fare clic su **salvare** tooimport hello API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-169">Click **Save** tooimport hello API.</span></span>

![Add new API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="8d0ac-171">**Gestione API** supporta attualmente sia la versione 1.2 che la versione 2.0 del documento Swagger per l'importazione.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="8d0ac-172">Anche se la [specifica Swagger 2.0](http://swagger.io/specification) dichiara che le proprietà `host`, `basePath` e `schemes` sono facoltative, il documento Swagger 2.0 **DEVE** contenere queste proprietà. In caso contrario, non verrà importato.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="8d0ac-173">Una volta importato, hello API hello pagina Riepilogo per l'API di hello viene visualizzato nel portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Riepilogo dell'API][api-management-imported-api-summary]

<span data-ttu-id="8d0ac-175">Hello sezione API è disponibili diverse schede.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-175">hello API section has several tabs.</span></span> <span data-ttu-id="8d0ac-176">Hello **riepilogo** scheda vengono visualizzate le metriche di base e informazioni sulle API hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="8d0ac-177">Hello [impostazioni](api-management-howto-create-apis.md#configure-api-settings) scheda è tooview e modifica hello configurazione per un'API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="8d0ac-178">Hello [operazioni](api-management-howto-add-operations.md) scheda è operazioni hello toomanage utilizzato dell'API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="8d0ac-179">Hello **sicurezza** scheda può essere utilizzato tooconfigure l'autenticazione del gateway per server back-end hello utilizzando l'autenticazione di base o [autenticazione reciproca del certificato](api-management-howto-mutual-certificates.md)e tooconfigure [ l'autorizzazione dell'utente tramite OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="8d0ac-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="8d0ac-180">Hello **problemi** scheda è tooview utilizzati problemi segnalati da sviluppatori hello che utilizzano le API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="8d0ac-181">Hello **prodotti** scheda è prodotti hello tooconfigure utilizzati che contengono questa API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="8d0ac-182">Per impostazione predefinita, con ogni istanza di Gestione API vengono forniti due prodotti di esempio:</span><span class="sxs-lookup"><span data-stu-id="8d0ac-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="8d0ac-183">**Starter**</span><span class="sxs-lookup"><span data-stu-id="8d0ac-183">**Starter**</span></span>
* <span data-ttu-id="8d0ac-184">**Illimitato**</span><span class="sxs-lookup"><span data-stu-id="8d0ac-184">**Unlimited**</span></span>

<span data-ttu-id="8d0ac-185">In questa esercitazione, hello base API Calcolatrice è stato aggiunto prodotto Starter toohello quando è stato importato hello API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="8d0ac-186">Nell'ordine toomake chiamate tooan API, gli sviluppatori devono prima sottoscrizione prodotto tooa che consenta l'accesso tooit.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="8d0ac-187">Gli sviluppatori possono eseguire la sottoscrizione nel portale per sviluppatori hello tooproducts o gli amministratori possono eseguire la sottoscrizione agli sviluppatori tooproducts nel portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="8d0ac-188">Si è un amministratore dopo la creazione istanza di gestione API hello in hello passaggi precedenti nell'esercitazione di hello, pertanto sono già sottoscritti tooevery prodotto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="8d0ac-189"><a name="call-operation"></a>Chiamare un'operazione dal portale per sviluppatori hello</span><span class="sxs-lookup"><span data-stu-id="8d0ac-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="8d0ac-190">Operazioni possono essere chiamate direttamente dal portale per sviluppatori di hello, che fornisce un modo pratico di tooview e testare il funzionamento di hello di un'API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="8d0ac-191">In questo passaggio dell'esercitazione, verrà chiamata dell'API di hello base Calcolatrice **aggiungere due numeri interi** operazione.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="8d0ac-192">Fare clic su **portale per sviluppatori** dal menu hello hello in alto a destra del portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![Portale per sviluppatori][api-management-developer-portal-menu]

<span data-ttu-id="8d0ac-194">Fare clic su **API** dal menu superiore hello e quindi fare clic su **Calcolatrice di base** toosee hello operazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![Portale per sviluppatori][api-management-developer-portal-calc-api]

<span data-ttu-id="8d0ac-196">Tenere presente le descrizioni di esempio hello e i parametri che sono stati importati insieme hello API e operazioni, fornendo la documentazione per sviluppatori di hello che utilizzerà questa operazione.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="8d0ac-197">È possibile aggiungere queste descrizioni anche quando le operazioni vengono aggiunte manualmente.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="8d0ac-198">hello toocall **aggiungere due numeri interi** operazione, fare clic su **provarla**.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Prova][api-management-developer-portal-calc-api-console]

<span data-ttu-id="8d0ac-200">È possibile immettere alcuni valori per parametri hello o mantenere i valori predefiniti di hello e quindi fare clic su **inviare**.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="8d0ac-202">Dopo un'operazione viene richiamata, il portale per sviluppatori di hello Visualizza hello **stato della risposta**, hello **le intestazioni di risposta**e di qualsiasi **contenuto della risposta**.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Response][api-management-invoke-get-response]

## <span data-ttu-id="8d0ac-204"><a name="view-analytics"></a>Visualizzare l'analisi</span><span class="sxs-lookup"><span data-stu-id="8d0ac-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="8d0ac-205">tooview analitica per Calcolatrice di base, il portale di pubblicazione toohello indietro di commutatore selezionando **Gestisci** dal menu hello hello in alto a destra del portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Gestisci][api-management-manage-menu]

<span data-ttu-id="8d0ac-207">visualizzazione predefinita per il portale di pubblicazione hello Hello è hello **Dashboard**, che fornisce una panoramica dell'istanza di gestione API.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Dashboard][api-management-dashboard]

<span data-ttu-id="8d0ac-209">Posizionare il mouse di hello su grafico hello per **Calcolatrice di base** metriche specifiche di hello toosee per l'utilizzo di hello di hello API per un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="8d0ac-210">Se tutte le righe non viene visualizzato nel grafico, passare portale per sviluppatori toohello indietro ed effettuare alcune chiamate in hello API, attendere alcuni istanti e tornare toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="8d0ac-211">Fare clic su **Visualizza dettagli** pagina di riepilogo hello tooview per hello API, inclusa una versione più grande di metriche di hello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Analytics][api-management-mouse-over]

![Riepilogo][api-management-api-summary-metrics]

<span data-ttu-id="8d0ac-214">Per le metriche dettagliate e i report, fare clic su **Analitica** da hello **gestione API** menu di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Panoramica][api-management-analytics-overview]

<span data-ttu-id="8d0ac-216">Hello **Analitica** sezione ha hello seguenti quattro schede:</span><span class="sxs-lookup"><span data-stu-id="8d0ac-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="8d0ac-217">**A colpo d'occhio** fornisce l'utilizzo complessivo e metriche sull'integrità, nonché hello sviluppatori superiore, prodotti, API superiore e operazioni superiore.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="8d0ac-218">**Utilizzo** : fornisce informazioni dettagliate sulle chiamate API e sulla larghezza di banda, inclusa una rappresentazione geografica.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="8d0ac-219">**Integrità** : è incentrata sui codici di stato, sulle percentuali di operazioni sulla cache completate, sui tempi di risposta, oltre che sui tempi di risposta di API e servizi.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="8d0ac-220">**Attività** fornisce i report drill-down attività specifiche di hello da sviluppatori, prodotto, API e operation.</span><span class="sxs-lookup"><span data-stu-id="8d0ac-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="8d0ac-221"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8d0ac-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="8d0ac-222">Informazioni su come troppo[proteggere l'API con i limiti di velocità](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="8d0ac-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
