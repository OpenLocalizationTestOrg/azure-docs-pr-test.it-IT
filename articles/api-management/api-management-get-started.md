---
title: Gestire la prima API in Gestione API di Azure | Microsoft Docs
description: Informazioni su come creare API, aggiungere operazioni e iniziare a usare Gestione API.
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
ms.openlocfilehash: 6e76d1ee08f804637999ef2ebf5d25becf6a0408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="0410c-103">Gestire la prima API in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="0410c-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="0410c-104"><a name="overview"> </a>Panoramica</span><span class="sxs-lookup"><span data-stu-id="0410c-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="0410c-105">Questa guida illustra le procedure per iniziare subito a usare Gestione API di Azure ed effettuare la prima chiamata API.</span><span class="sxs-lookup"><span data-stu-id="0410c-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="0410c-106"><a name="concepts"> </a>Cos'è Gestione API di Azure?</span><span class="sxs-lookup"><span data-stu-id="0410c-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="0410c-107">È possibile usare Gestione API di Azure per avviare un programma API completo basato su qualsiasi back-end.</span><span class="sxs-lookup"><span data-stu-id="0410c-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="0410c-108">Gli scenari comuni includono:</span><span class="sxs-lookup"><span data-stu-id="0410c-108">Common scenarios include:</span></span>

* <span data-ttu-id="0410c-109">**protezione dell'infrastruttura mobile** con la delega dell'accesso con le chiavi API, la prevenzione degli attacchi DOS con la limitazione oppure l'uso di criteri di sicurezza avanzata come la convalida dei token JWT.</span><span class="sxs-lookup"><span data-stu-id="0410c-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="0410c-110">**abilitazione degli ecosistemi del partner ISV** , offrendo al partner un rapido caricamento attraverso il portale degli sviluppatori e compilando un'interfaccia API per la separazione dalle implementazioni interne non pronte per l'utilizzo da parte del partner.</span><span class="sxs-lookup"><span data-stu-id="0410c-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="0410c-111">**esecuzione di un programma API interno** , offrendo all'organizzazione una posizione centralizzata per la comunicazione della disponibilità e delle ultime modifiche apportate alle API e delegando l'accesso in base agli account aziendali, tutti basati su un canale protetto tra il gateway dell'API e il back-end.</span><span class="sxs-lookup"><span data-stu-id="0410c-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span></span>

<span data-ttu-id="0410c-112">Il sistema è costituito dai componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0410c-112">The system is made up of the following components:</span></span>

* <span data-ttu-id="0410c-113">Il **gateway dell'API** è l'endpoint che:</span><span class="sxs-lookup"><span data-stu-id="0410c-113">The **API gateway** is the endpoint that:</span></span>
  
  * <span data-ttu-id="0410c-114">Accetta chiamate API e le indirizza al back-end.</span><span class="sxs-lookup"><span data-stu-id="0410c-114">Accepts API calls and routes them to your backends.</span></span>
  * <span data-ttu-id="0410c-115">Verifica le chiavi API, i token JWT, i certificati e altre credenziali.</span><span class="sxs-lookup"><span data-stu-id="0410c-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="0410c-116">Applica le quote di utilizzo e i limiti di frequenza.</span><span class="sxs-lookup"><span data-stu-id="0410c-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="0410c-117">Trasforma le API in modo immediato senza modifiche del codice.</span><span class="sxs-lookup"><span data-stu-id="0410c-117">Transforms your API on the fly without code modifications.</span></span>
  * <span data-ttu-id="0410c-118">Memorizza nella cache le risposte di back-end durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="0410c-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="0410c-119">Registra i metadati della chiamata a scopi di analisi.</span><span class="sxs-lookup"><span data-stu-id="0410c-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="0410c-120">Il **portale di pubblicazione** è l'interfaccia amministrativa in cui si configura il programma API.</span><span class="sxs-lookup"><span data-stu-id="0410c-120">The **publisher portal** is the administrative interface where you set up your API program.</span></span> <span data-ttu-id="0410c-121">Può essere usato per:</span><span class="sxs-lookup"><span data-stu-id="0410c-121">Use it to:</span></span>
  
  * <span data-ttu-id="0410c-122">Definire o importare lo schema API.</span><span class="sxs-lookup"><span data-stu-id="0410c-122">Define or import API schema.</span></span>
  * <span data-ttu-id="0410c-123">Creare pacchetti di API nei prodotti.</span><span class="sxs-lookup"><span data-stu-id="0410c-123">Package APIs into products.</span></span>
  * <span data-ttu-id="0410c-124">Configurare criteri come quote o trasformazioni sulle API.</span><span class="sxs-lookup"><span data-stu-id="0410c-124">Set up policies like quotas or transformations on the APIs.</span></span>
  * <span data-ttu-id="0410c-125">Ottenere informazioni dall'analisi.</span><span class="sxs-lookup"><span data-stu-id="0410c-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="0410c-126">Gestire gli utenti.</span><span class="sxs-lookup"><span data-stu-id="0410c-126">Manage users.</span></span>
* <span data-ttu-id="0410c-127">Il **portale per sviluppatori** funge da principale presenza Web per gli sviluppatori, che potranno:</span><span class="sxs-lookup"><span data-stu-id="0410c-127">The **developer portal** serves as the main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="0410c-128">Leggere la documentazione relativa alle API.</span><span class="sxs-lookup"><span data-stu-id="0410c-128">Read API documentation.</span></span>
  * <span data-ttu-id="0410c-129">Provare un'API con la console interattiva.</span><span class="sxs-lookup"><span data-stu-id="0410c-129">Try out an API via the interactive console.</span></span>
  * <span data-ttu-id="0410c-130">Creare un account ed eseguire la sottoscrizione per ottenere le chiavi API.</span><span class="sxs-lookup"><span data-stu-id="0410c-130">Create an account and subscribe to get API keys.</span></span>
  * <span data-ttu-id="0410c-131">Accedere all'analisi di utilizzo personalizzata.</span><span class="sxs-lookup"><span data-stu-id="0410c-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="0410c-132"><a name="create-service-instance"> </a>Creare un'istanza di Gestione API</span><span class="sxs-lookup"><span data-stu-id="0410c-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="0410c-133">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="0410c-133">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="0410c-134">Se non si ha un account, è possibile creare un account gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0410c-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="0410c-135">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="0410c-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="0410c-136">Per poter usare Gestione API, occorre innanzitutto creare un'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="0410c-136">The first step in working with API Management is to create a service instance.</span></span> <span data-ttu-id="0410c-137">Accedere al [portale di Azure][Azure Portal] e fare clic su **Nuovo**, **Web e dispositivi mobili**, **Gestione API**.</span><span class="sxs-lookup"><span data-stu-id="0410c-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![API Management new instance][api-management-create-instance-menu]

<span data-ttu-id="0410c-139">In **URL**specificare un nome univoco di sottodominio da usare come URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="0410c-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span></span>

<span data-ttu-id="0410c-140">Scegliere i valori di **Sottoscrizione**, **Gruppo di risorse** e **Area** per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="0410c-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="0410c-141">Immettere **Contoso Ltd.**</span><span class="sxs-lookup"><span data-stu-id="0410c-141">Enter **Contoso Ltd.**</span></span> <span data-ttu-id="0410c-142">in **Nome organizzazione** e specificare l'indirizzo di posta elettronica nel campo **Indirizzo di posta elettronica dell'amministratore**.</span><span class="sxs-lookup"><span data-stu-id="0410c-142">for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="0410c-143">Questo indirizzo di posta elettronica viene usato per le notifiche inviate dal sistema Gestione API.</span><span class="sxs-lookup"><span data-stu-id="0410c-143">This email address is used for notifications from the API Management system.</span></span> <span data-ttu-id="0410c-144">Per altre informazioni, vedere [Come configurare notifiche e modelli di posta elettronica in Gestione API di Azure][How to configure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="0410c-144">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span></span>
> 
> 

![New API Management service][api-management-create-instance-step1]

<span data-ttu-id="0410c-146">Le istanze del servizio Gestione API sono disponibili in tre livelli: Developer, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="0410c-146">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="0410c-147">Il livello Developer è dedicato allo sviluppo, al test e alla distribuzione pilota di programmi API in cui l'elevata disponibilità non è un fattore rilevante.</span><span class="sxs-lookup"><span data-stu-id="0410c-147">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="0410c-148">Nei livelli Standard e Premium è possibile aumentare il numero di unità riservate per gestire un maggior volume di traffico.</span><span class="sxs-lookup"><span data-stu-id="0410c-148">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span></span> <span data-ttu-id="0410c-149">I livelli Standard e Premium forniscono al servizio Gestione API anche una potenza di elaborazione e prestazioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="0410c-149">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span></span> <span data-ttu-id="0410c-150">È possibile completare questa esercitazione usando qualsiasi livello.</span><span class="sxs-lookup"><span data-stu-id="0410c-150">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="0410c-151">Per altre informazioni sui livelli di Gestione API, vedere [Gestione API - Prezzi][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="0410c-151">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="0410c-152">Fare clic su **Crea** per avviare il provisioning di un'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="0410c-152">Click **Create** to start provisioning your service instance.</span></span>

![New API Management service][api-management-instance-created]

<span data-ttu-id="0410c-154">Dopo aver creato l'istanza del servizio, l'operazione successiva consiste nel creare o importare un'API.</span><span class="sxs-lookup"><span data-stu-id="0410c-154">Once the service instance is created, the next step is to create or import an API.</span></span>

## <span data-ttu-id="0410c-155"><a name="create-api"> </a>Importare un'API</span><span class="sxs-lookup"><span data-stu-id="0410c-155"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="0410c-156">Un'API rappresenta un set di operazioni che possono essere richiamate da un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="0410c-156">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="0410c-157">Le operazioni API vengono trasmesse tramite proxy ai servizi Web esistenti.</span><span class="sxs-lookup"><span data-stu-id="0410c-157">API operations are proxied to existing web services.</span></span>

<span data-ttu-id="0410c-158">È possibile creare le API (e aggiungere operazioni) in modo manuale oppure è possibile importarle.</span><span class="sxs-lookup"><span data-stu-id="0410c-158">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="0410c-159">In questa esercitazione, verrà importata l'API per un servizio Web calcolatrice di esempio fornito da Microsoft e ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="0410c-159">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="0410c-160">Per indicazioni sulla creazione di un'API e l'aggiunta manuale di operazioni, vedere [Come creare API in Gestione API di Azure](api-management-howto-create-apis.md) e [Come aggiungere operazioni a un'API in Gestione API di Azure](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="0410c-160">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="0410c-161">Le API vengono configurate dal portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="0410c-161">APIs are configured from the publisher portal.</span></span> <span data-ttu-id="0410c-162">Per accedervi, fare clic su **Publisher portal** (Portale di pubblicazione) nella barra degli strumenti del servizio.</span><span class="sxs-lookup"><span data-stu-id="0410c-162">To reach it, click **Publisher portal** from the service toolbar.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="0410c-164">Per importare l'API Calculator, fare clic su **API** nel menu **Gestione API** sulla sinistra e quindi scegliere **Importa API**.</span><span class="sxs-lookup"><span data-stu-id="0410c-164">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Pulsante Importa API][api-management-import-api]

<span data-ttu-id="0410c-166">Per configurare l'API Calcolatrice, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0410c-166">Perform the following steps to configure the calculator API:</span></span>

1. <span data-ttu-id="0410c-167">Fare clic su **Importa dall'URL**, immettere **http://calcapi.cloudapp.net/calcapi.json** nella casella di testo **Specification document URL** (URL documento specifica) e fare clic sul pulsante di opzione **Swagger**.</span><span class="sxs-lookup"><span data-stu-id="0410c-167">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="0410c-168">Digitare **calc** nella casella di testo **Web API URL suffix** (Suffisso dell'URL dell'API Web).</span><span class="sxs-lookup"><span data-stu-id="0410c-168">Type **calc** into the **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="0410c-169">Fare clic sulla casella **Products (optional)** (Prodotti - facoltativo) e scegliere **Starter**.</span><span class="sxs-lookup"><span data-stu-id="0410c-169">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="0410c-170">Fare clic su **Salva** per importare l'API.</span><span class="sxs-lookup"><span data-stu-id="0410c-170">Click **Save** to import the API.</span></span>

![Add new API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="0410c-172">**Gestione API** supporta attualmente sia la versione 1.2 che la versione 2.0 del documento Swagger per l'importazione.</span><span class="sxs-lookup"><span data-stu-id="0410c-172">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="0410c-173">Anche se la [specifica Swagger 2.0](http://swagger.io/specification) dichiara che le proprietà `host`, `basePath` e `schemes` sono facoltative, il documento Swagger 2.0 **DEVE** contenere queste proprietà. In caso contrario, non verrà importato.</span><span class="sxs-lookup"><span data-stu-id="0410c-173">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="0410c-174">Una volta importata l'API, la pagina di riepilogo dell'API viene visualizzata nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="0410c-174">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

![Riepilogo dell'API][api-management-imported-api-summary]

<span data-ttu-id="0410c-176">La sezione API comprende diverse schede.</span><span class="sxs-lookup"><span data-stu-id="0410c-176">The API section has several tabs.</span></span> <span data-ttu-id="0410c-177">Nella scheda **Riepilogo** sono visualizzate le informazioni e le metriche di base sull'API.</span><span class="sxs-lookup"><span data-stu-id="0410c-177">The **Summary** tab displays basic metrics and information about the API.</span></span> <span data-ttu-id="0410c-178">È possibile usare la scheda [Impostazioni](api-management-howto-create-apis.md#configure-api-settings) per visualizzare e modificare la configurazione di un'API.</span><span class="sxs-lookup"><span data-stu-id="0410c-178">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span></span> <span data-ttu-id="0410c-179">La scheda [Operazioni](api-management-howto-add-operations.md) consente di gestire le operazioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="0410c-179">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span></span> <span data-ttu-id="0410c-180">La scheda **Sicurezza** consente di configurare l'autenticazione del gateway per il server back-end usando l'autenticazione di base o l'[autenticazione reciproca dei certificati](api-management-howto-mutual-certificates.md) e di configurare l'[autorizzazione utente con OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="0410c-180">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="0410c-181">La scheda **Problemi** consente di visualizzare i problemi segnalati dagli sviluppatori che stanno usando le API.</span><span class="sxs-lookup"><span data-stu-id="0410c-181">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span></span> <span data-ttu-id="0410c-182">La scheda **Prodotti** viene usata per configurare i prodotti contenenti l'API.</span><span class="sxs-lookup"><span data-stu-id="0410c-182">The **Products** tab is used to configure the products that contain this API.</span></span>

<span data-ttu-id="0410c-183">Per impostazione predefinita, con ogni istanza di Gestione API vengono forniti due prodotti di esempio:</span><span class="sxs-lookup"><span data-stu-id="0410c-183">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="0410c-184">**Starter**</span><span class="sxs-lookup"><span data-stu-id="0410c-184">**Starter**</span></span>
* <span data-ttu-id="0410c-185">**Illimitato**</span><span class="sxs-lookup"><span data-stu-id="0410c-185">**Unlimited**</span></span>

<span data-ttu-id="0410c-186">In questa esercitazione, è stata aggiunta l'API Calcolatrice di base al prodotto Starter quando l'API è stata importata.</span><span class="sxs-lookup"><span data-stu-id="0410c-186">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span></span>

<span data-ttu-id="0410c-187">Per effettuare chiamate a un'API, gli sviluppatori devono prima sottoscrivere un prodotto che offre l'accesso all'API.</span><span class="sxs-lookup"><span data-stu-id="0410c-187">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span></span> <span data-ttu-id="0410c-188">La sottoscrizione dei prodotti può essere effettuata direttamente dagli sviluppatori nel portale per sviluppatori; in alternativa, gli amministratori possono sottoscrivere i prodotti per conto degli sviluppatori nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="0410c-188">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span></span> <span data-ttu-id="0410c-189">Dal momento che nei passaggi precedenti di questa esercitazione è stata creata un'istanza di Gestione API, l'utente corrente ha già effettuato la sottoscrizione a ogni prodotto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0410c-189">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span></span>

## <span data-ttu-id="0410c-190"><a name="call-operation"> </a>Chiamare un'operazione dal portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="0410c-190"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>
<span data-ttu-id="0410c-191">È possibile chiamare le operazioni direttamente dal portale per sviluppatori, che consente di visualizzare e testare le operazioni di un'API in modo pratico.</span><span class="sxs-lookup"><span data-stu-id="0410c-191">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="0410c-192">In questo passaggio dell'esercitazione verrà chiamata l'operazione **Aggiungere due integer** dell'API Calcolatrice di base.</span><span class="sxs-lookup"><span data-stu-id="0410c-192">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="0410c-193">Fare clic su **Portale per sviluppatori** nel menu in alto a destra del portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="0410c-193">Click **Developer portal** from the menu at the top right of the publisher portal.</span></span>

![Portale per sviluppatori][api-management-developer-portal-menu]

<span data-ttu-id="0410c-195">Fare clic su **API** nel menu in alto e quindi su **Basic Calculator** (Calcolatrice di base) per visualizzare le operazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="0410c-195">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span></span>

![Portale per sviluppatori][api-management-developer-portal-calc-api]

<span data-ttu-id="0410c-197">Notare le descrizioni e i parametri di esempio che sono stati importati assieme alle API e alle operazioni, che costituiscono la documentazione destinata agli sviluppatori che useranno l'operazione.</span><span class="sxs-lookup"><span data-stu-id="0410c-197">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span></span> <span data-ttu-id="0410c-198">È possibile aggiungere queste descrizioni anche quando le operazioni vengono aggiunte manualmente.</span><span class="sxs-lookup"><span data-stu-id="0410c-198">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="0410c-199">Per chiamare l'operazione di **aggiunta di due Integer**, fare clic su **Try it** (Prova).</span><span class="sxs-lookup"><span data-stu-id="0410c-199">To call the **Add two integers** operation, click **Try it**.</span></span>

![Prova][api-management-developer-portal-calc-api-console]

<span data-ttu-id="0410c-201">È possibile immettere alcuni valori per i parametri o mantenere quelli predefiniti e quindi fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="0410c-201">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="0410c-203">Dopo aver richiamato un'operazione, nel portale per sviluppatori vengono visualizzati lo **stato della risposta**, le **intestazioni della risposta** e l'eventuale **contenuto della risposta**.</span><span class="sxs-lookup"><span data-stu-id="0410c-203">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![Response][api-management-invoke-get-response]

## <span data-ttu-id="0410c-205"><a name="view-analytics"> </a>Visualizzare l'analisi</span><span class="sxs-lookup"><span data-stu-id="0410c-205"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="0410c-206">Per visualizzare l'analisi per la Calcolatrice di base, tornare al portale di pubblicazione selezionando **Gestisci** nel menu in alto a destra nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="0410c-206">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span></span>

![Gestisci][api-management-manage-menu]

<span data-ttu-id="0410c-208">La visualizzazione predefinita del portale di pubblicazione è il **dashboard**, che offre una panoramica dell'istanza di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="0410c-208">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span></span>

![dashboard][api-management-dashboard]

<span data-ttu-id="0410c-210">Passare il puntatore del mouse sul grafico della **Calcolatrice di base** per visualizzare le metriche specifiche relative all'utilizzo dell'API in un dato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="0410c-210">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="0410c-211">Se il grafico non contiene linee, tornare al portale per sviluppatori ed effettuare alcune chiamate all'API, attendere qualche secondo e quindi tornare al dashboard.</span><span class="sxs-lookup"><span data-stu-id="0410c-211">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span></span>
> 
> 

<span data-ttu-id="0410c-212">Fare clic su **Visualizza dettagli** per visualizzare la pagina di riepilogo per l'API, inclusa una versione più estesa delle metriche visualizzate.</span><span class="sxs-lookup"><span data-stu-id="0410c-212">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span></span>

![Analisi][api-management-mouse-over]

![Riepilogo][api-management-api-summary-metrics]

<span data-ttu-id="0410c-215">Per report e metriche dettagliate fare clic su **Analisi** nel menu **Gestione API** sulla sinistra.</span><span class="sxs-lookup"><span data-stu-id="0410c-215">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span></span>

![Panoramica][api-management-analytics-overview]

<span data-ttu-id="0410c-217">La sezione **Analisi** include le quattro schede seguenti:</span><span class="sxs-lookup"><span data-stu-id="0410c-217">The **Analytics** section has the following four tabs:</span></span>

* <span data-ttu-id="0410c-218">**Riepilogo** : fornisce metriche complessive sull'utilizzo e l'integrità, oltre a indicare API, operazioni e prodotti più usati e gli sviluppatori più attivi.</span><span class="sxs-lookup"><span data-stu-id="0410c-218">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="0410c-219">**Utilizzo** : fornisce informazioni dettagliate sulle chiamate API e sulla larghezza di banda, inclusa una rappresentazione geografica.</span><span class="sxs-lookup"><span data-stu-id="0410c-219">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="0410c-220">**Integrità** : è incentrata sui codici di stato, sulle percentuali di operazioni sulla cache completate, sui tempi di risposta, oltre che sui tempi di risposta di API e servizi.</span><span class="sxs-lookup"><span data-stu-id="0410c-220">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="0410c-221">**Attività** : fornisce report che illustrano in dettaglio l'attività specifica in base a sviluppatore, prodotto, API e operazione.</span><span class="sxs-lookup"><span data-stu-id="0410c-221">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="0410c-222"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0410c-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="0410c-223">Informazioni su come [proteggere le API con limiti di frequenza](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="0410c-223">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
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
