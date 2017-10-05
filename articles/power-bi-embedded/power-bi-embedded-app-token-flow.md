---
title: Autenticazione e autorizzazione con Power BI Embedded
description: Autenticazione e autorizzazione con Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="7fbf8-103">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7fbf8-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="7fbf8-104">Il servizio Power BI Embedded usa le **chiavi** e i **token dell'app** per l'autenticazione e l'autorizzazione anziché usare l'autenticazione esplicita dell'utente finale.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="7fbf8-105">In questo modello è l'applicazione a gestire l'autenticazione e l'autorizzazione degli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="7fbf8-106">Se necessario, l'app crea e invia i token dell'app al servizio Microsoft per richiedere il rendering del report richiesto.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span></span> <span data-ttu-id="7fbf8-107">Questo modello non richiede che l'applicazione usi Azure Active Directory per l'autenticazione e l'autorizzazione dell'utente, sebbene sia possibile.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-to-authenticate"></a><span data-ttu-id="7fbf8-108">Due modalità di autenticazione</span><span class="sxs-lookup"><span data-stu-id="7fbf8-108">Two ways to authenticate</span></span>

<span data-ttu-id="7fbf8-109">**Chiave** : è possibile usare le chiavi per tutte le chiamate API REST di Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="7fbf8-110">Per trovare le chiavi nel **portale di Azure**, fare clic su **Tutte le impostazioni** e quindi su **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="7fbf8-111">Occorre gestire sempre la chiave come se fosse una password.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="7fbf8-112">Queste chiavi sono autorizzate a effettuare qualsiasi chiamata API REST su una raccolta specifica di aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-112">These keys have permissions to make any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="7fbf8-113">Per usare una chiave su una chiamata REST, aggiungere l'intestazione di autorizzazione seguente:</span><span class="sxs-lookup"><span data-stu-id="7fbf8-113">To use a key on a REST call, add the following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="7fbf8-114">**Token dell'app** : i token dell'app vengono usati per tutte le richieste di incorporamento.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="7fbf8-115">Sono stati progettati per essere eseguiti sul lato client, quindi sono limitati a un singolo report ed è consigliabile impostare una scadenza.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span></span>

<span data-ttu-id="7fbf8-116">I token dell'app sono token JSON Web (JWT, JSON Web Token) firmati da una delle chiavi dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="7fbf8-117">Il token dell'app può contenere le attestazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7fbf8-117">Your app token can contain the following claims:</span></span>

| <span data-ttu-id="7fbf8-118">Attestazione</span><span class="sxs-lookup"><span data-stu-id="7fbf8-118">Claim</span></span> | <span data-ttu-id="7fbf8-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7fbf8-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7fbf8-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="7fbf8-120">**ver**</span></span> |<span data-ttu-id="7fbf8-121">Versione del token dell'app.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-121">The version of the app token.</span></span> <span data-ttu-id="7fbf8-122">La versione corrente è 0.2.0.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-122">0.2.0 is the current version.</span></span> |
| <span data-ttu-id="7fbf8-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="7fbf8-123">**aud**</span></span> |<span data-ttu-id="7fbf8-124">Destinatario previsto per il token.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-124">The intended recipient of the token.</span></span> <span data-ttu-id="7fbf8-125">Per Power BI Embedded usare: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="7fbf8-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="7fbf8-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="7fbf8-126">**iss**</span></span> |<span data-ttu-id="7fbf8-127">Stringa che indica l'applicazione che ha emesso il token.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-127">A string indicating the application which issued the token.</span></span> |
| <span data-ttu-id="7fbf8-128">**type**</span><span class="sxs-lookup"><span data-stu-id="7fbf8-128">**type**</span></span> |<span data-ttu-id="7fbf8-129">Tipo di token dell'app da creare.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-129">The type of app token which is being created.</span></span> <span data-ttu-id="7fbf8-130">L'unico tipo attualmente supportato è **embed**.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-130">Current the only supported type is **embed**.</span></span> |
| <span data-ttu-id="7fbf8-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="7fbf8-131">**wcn**</span></span> |<span data-ttu-id="7fbf8-132">Nome della raccolta di aree di lavoro per cui viene emesso il token.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-132">Workspace collection name the token is being issued for.</span></span> |
| <span data-ttu-id="7fbf8-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="7fbf8-133">**wid**</span></span> |<span data-ttu-id="7fbf8-134">ID dell'area di lavoro per cui viene emesso il token.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-134">Workspace ID the token is being issued for.</span></span> |
| <span data-ttu-id="7fbf8-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="7fbf8-135">**rid**</span></span> |<span data-ttu-id="7fbf8-136">ID del report per cui viene emesso il token.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-136">Report ID the token is being issued for.</span></span> |
| <span data-ttu-id="7fbf8-137">**username** (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="7fbf8-137">**username** (optional)</span></span> |<span data-ttu-id="7fbf8-138">Usata con la sicurezza a livello di riga, questa stringa può semplificare l'identificazione dell'utente quando si applicano le regole di sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span></span> |
| <span data-ttu-id="7fbf8-139">**roles** (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="7fbf8-139">**roles** (optional)</span></span> |<span data-ttu-id="7fbf8-140">Stringa contenente i ruoli da selezionare quando si applicano le regole di sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-140">A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="7fbf8-141">Se si passa più di un ruolo, è consigliabile passarli come matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="7fbf8-142">**scp** (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="7fbf8-142">**scp** (optional)</span></span> |<span data-ttu-id="7fbf8-143">Stringa contenente gli ambiti delle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-143">A string containing the permissions scopes.</span></span> <span data-ttu-id="7fbf8-144">Se si passa più di un ruolo, è consigliabile passarli come matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="7fbf8-145">**exp** (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="7fbf8-145">**exp** (optional)</span></span> |<span data-ttu-id="7fbf8-146">Indica l'ora di scadenza del token.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-146">Indicates the time in which the token will expire.</span></span> <span data-ttu-id="7fbf8-147">Questi valori devono essere passati come timestamp Unix.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="7fbf8-148">**nbf** (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="7fbf8-148">**nbf** (optional)</span></span> |<span data-ttu-id="7fbf8-149">Indica l'ora di inizio della validità del token.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-149">Indicates the time in which the token starts being valid.</span></span> <span data-ttu-id="7fbf8-150">Questi valori devono essere passati come timestamp Unix.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="7fbf8-151">Un token dell'app di esempio avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="7fbf8-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="7fbf8-152">Quando viene decodificato, avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="7fbf8-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="7fbf8-153">All'interno di SDK sono disponibili metodi che semplificano la creazione di apptokens.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-153">There are methods available within the SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="7fbf8-154">Ad esempio, per .NET è possibile esaminare la classe [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) e i metodi [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="7fbf8-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="7fbf8-155">Per l'SDK di .NET, è possibile fare riferimento ad [Ambiti](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="7fbf8-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="7fbf8-156">Ambiti</span><span class="sxs-lookup"><span data-stu-id="7fbf8-156">Scopes</span></span>

<span data-ttu-id="7fbf8-157">Quando si usano token di incorporamento, può essere opportuno limitare l'uso delle risorse a cui si concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="7fbf8-158">Per questo motivo, è possibile generare un token con autorizzazioni con ambito.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="7fbf8-159">Di seguito sono riportati gli ambiti disponibili per Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-159">The following are the available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="7fbf8-160">Scope</span><span class="sxs-lookup"><span data-stu-id="7fbf8-160">Scope</span></span>|<span data-ttu-id="7fbf8-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7fbf8-161">Description</span></span>|
|---|---|
|<span data-ttu-id="7fbf8-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="7fbf8-162">Dataset.Read</span></span>|<span data-ttu-id="7fbf8-163">Concede l'autorizzazione per leggere il set di dati specificato.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-163">Provides permission to read the specified dataset.</span></span>|
|<span data-ttu-id="7fbf8-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="7fbf8-164">Dataset.Write</span></span>|<span data-ttu-id="7fbf8-165">Concede l'autorizzazione per scrivere il set di dati specificato.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-165">Provides permission to write to the specified dataset.</span></span>|
|<span data-ttu-id="7fbf8-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="7fbf8-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="7fbf8-167">Concede l'autorizzazione per leggere e scrivere il set di dati specificato.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-167">Provides permission to read and write to the specificed dataset.</span></span>|
|<span data-ttu-id="7fbf8-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="7fbf8-168">Report.Read</span></span>|<span data-ttu-id="7fbf8-169">Concede l'autorizzazione per visualizzare il report specificato.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-169">Provides permission to view the specified report.</span></span>|
|<span data-ttu-id="7fbf8-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="7fbf8-170">Report.ReadWrite</span></span>|<span data-ttu-id="7fbf8-171">Concede l'autorizzazione per visualizzare e modificare il report specificato.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-171">Provides permission to view and edit the specified report.</span></span>|
|<span data-ttu-id="7fbf8-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="7fbf8-172">Workspace.Report.Create</span></span>|<span data-ttu-id="7fbf8-173">Concede l'autorizzazione per creare un nuovo report nell'area di lavoro specificata.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-173">Provides permission to create a new report within the specified workspace.</span></span>|
|<span data-ttu-id="7fbf8-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="7fbf8-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="7fbf8-175">Concede l'autorizzazione per clonare un report esistente nell'area di lavoro specificata.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-175">Provides permission to clone an existing report within the specified workspace.</span></span>|

<span data-ttu-id="7fbf8-176">È possibile specificare più ambiti mediante uno spazio tra gli ambiti come nel caso seguente.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-176">You can supply multiple scopes by using a space between the scopes like the following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="7fbf8-177">**Attestazioni e ambiti necessari**</span><span class="sxs-lookup"><span data-stu-id="7fbf8-177">**Required claims - scopes**</span></span>

<span data-ttu-id="7fbf8-178">scp: {scopesClaim} scopesClaim può essere una stringa o una matrice di stringhe, che annota le autorizzazioni concesse nelle risorse dell'area di lavoro (Report, Dataset, e così via)</span><span class="sxs-lookup"><span data-stu-id="7fbf8-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="7fbf8-179">Un token decodificato, con ambiti definiti, sarebbe simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-179">A decoded token, with scopes defined, would look similar to the following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="7fbf8-180">Operazioni e ambiti</span><span class="sxs-lookup"><span data-stu-id="7fbf8-180">Operations and scopes</span></span>

|<span data-ttu-id="7fbf8-181">Operazione</span><span class="sxs-lookup"><span data-stu-id="7fbf8-181">Operation</span></span>|<span data-ttu-id="7fbf8-182">Risorsa di destinazione</span><span class="sxs-lookup"><span data-stu-id="7fbf8-182">Target resource</span></span>|<span data-ttu-id="7fbf8-183">Autorizzazioni del token</span><span class="sxs-lookup"><span data-stu-id="7fbf8-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="7fbf8-184">Creare (in memoria) un nuovo report basato su un set di dati.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="7fbf8-185">Set di dati</span><span class="sxs-lookup"><span data-stu-id="7fbf8-185">Dataset</span></span>|<span data-ttu-id="7fbf8-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="7fbf8-186">Dataset.Read</span></span>|
|<span data-ttu-id="7fbf8-187">Creare (in memoria) un nuovo report basato su un set di dati e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-187">Create (in-memory) a new report based on a dataset and save the report.</span></span>|<span data-ttu-id="7fbf8-188">Set di dati</span><span class="sxs-lookup"><span data-stu-id="7fbf8-188">Dataset</span></span>|<span data-ttu-id="7fbf8-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="7fbf8-189">* Dataset.Read</span></span><br><span data-ttu-id="7fbf8-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="7fbf8-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="7fbf8-191">Visualizzare ed esplorare/modificare (in memoria) un report esistente.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="7fbf8-192">Report.Read implica Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="7fbf8-193">In questo modo le autorizzazioni non potranno salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-193">This will not allow permissions to save edits.</span></span>|<span data-ttu-id="7fbf8-194">Report</span><span class="sxs-lookup"><span data-stu-id="7fbf8-194">Report</span></span>|<span data-ttu-id="7fbf8-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="7fbf8-195">Report.Read</span></span>|
|<span data-ttu-id="7fbf8-196">Modificare e salvare un report esistente.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-196">Edit and save an existing report.</span></span>|<span data-ttu-id="7fbf8-197">Report</span><span class="sxs-lookup"><span data-stu-id="7fbf8-197">Report</span></span>|<span data-ttu-id="7fbf8-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="7fbf8-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="7fbf8-199">Salvare una copia di un report (Salva con nome).</span><span class="sxs-lookup"><span data-stu-id="7fbf8-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="7fbf8-200">Report</span><span class="sxs-lookup"><span data-stu-id="7fbf8-200">Report</span></span>|<span data-ttu-id="7fbf8-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="7fbf8-201">* Report.Read</span></span><br><span data-ttu-id="7fbf8-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="7fbf8-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-the-flow-works"></a><span data-ttu-id="7fbf8-203">Funzionamento del flusso</span><span class="sxs-lookup"><span data-stu-id="7fbf8-203">Here's how the flow works</span></span>
1. <span data-ttu-id="7fbf8-204">È necessario copiare le chiavi API nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-204">Copy the API keys to your application.</span></span> <span data-ttu-id="7fbf8-205">È possibile ottenere le chiavi nel **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-205">You can get the keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="7fbf8-206">Il token esegue l'asserzione di un'attestazione e ha una scadenza.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="7fbf8-207">Con le chiavi di accesso API si accede al token.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="7fbf8-208">L'utente richiede di visualizzare un report.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-208">User requests to view a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="7fbf8-209">Il token viene convalidato con chiavi di accesso API.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="7fbf8-210">Power BI Embedded invia un report all'utente.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-210">Power BI Embedded sends a report to user.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="7fbf8-211">Dopo che **Power BI Embedded** invia un report all'utente, l'utente può visualizzare il report nella propria app.</span><span class="sxs-lookup"><span data-stu-id="7fbf8-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span></span> <span data-ttu-id="7fbf8-212">Ad esempio, se è stato importato l'esempio [Analyzing Sales Data PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), l'app Web di esempio sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="7fbf8-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="7fbf8-213">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7fbf8-213">See Also</span></span>

[<span data-ttu-id="7fbf8-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="7fbf8-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="7fbf8-215">Introduzione all'esempio di Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7fbf8-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="7fbf8-216">Scenari comuni di Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7fbf8-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="7fbf8-217">Introduzione a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7fbf8-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="7fbf8-218">Repository Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="7fbf8-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="7fbf8-219">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="7fbf8-219">More questions?</span></span> [<span data-ttu-id="7fbf8-220">Contattare la community di Power BI</span><span class="sxs-lookup"><span data-stu-id="7fbf8-220">Try the Power BI Community</span></span>](http://community.powerbi.com/)

