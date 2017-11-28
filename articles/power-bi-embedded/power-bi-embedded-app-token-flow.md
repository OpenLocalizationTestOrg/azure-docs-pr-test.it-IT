---
title: aaaAuthenticating e l'autorizzazione a Power BI Embedded
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
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="c7d61-103">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c7d61-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="c7d61-104">Usa servizio Power BI Embedded Hello **chiavi** e **App token** per l'autenticazione e autorizzazione, anziché l'autenticazione degli utenti finali esplicita.</span><span class="sxs-lookup"><span data-stu-id="c7d61-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="c7d61-105">In questo modello è l'applicazione a gestire l'autenticazione e l'autorizzazione degli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="c7d61-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="c7d61-106">Se necessario, l'app crea e invia i token App hello indicante il nostro toorender servizio hello report richiesto.</span><span class="sxs-lookup"><span data-stu-id="c7d61-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="c7d61-107">Questa soluzione non richiede il toouse app Azure Active Directory per l'autenticazione e autorizzazione, anche se è ancora possibile.</span><span class="sxs-lookup"><span data-stu-id="c7d61-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="c7d61-108">Due modi tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="c7d61-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="c7d61-109">**Chiave** : è possibile usare le chiavi per tutte le chiamate API REST di Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c7d61-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="c7d61-110">le chiavi di Hello sono reperibile in hello **portale di Azure** facendo clic su **tutte le impostazioni** e quindi **le chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="c7d61-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="c7d61-111">Occorre gestire sempre la chiave come se fosse una password.</span><span class="sxs-lookup"><span data-stu-id="c7d61-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="c7d61-112">Queste chiavi hanno autorizzazioni toomake chiamare qualsiasi API REST su un insieme specifico dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c7d61-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="c7d61-113">toouse una chiave in una chiamata REST, aggiungere hello intestazione di autorizzazione seguente:</span><span class="sxs-lookup"><span data-stu-id="c7d61-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="c7d61-114">**Token dell'app** : i token dell'app vengono usati per tutte le richieste di incorporamento.</span><span class="sxs-lookup"><span data-stu-id="c7d61-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="c7d61-115">Si toobe progettato eseguire sul lato client, in modo che siano limitati tooa singoli report e le relative procedure consigliate tooset un'ora di scadenza.</span><span class="sxs-lookup"><span data-stu-id="c7d61-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="c7d61-116">I token dell'app sono token JSON Web (JWT, JSON Web Token) firmati da una delle chiavi dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c7d61-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="c7d61-117">Il token di app può contenere hello seguenti attestazioni:</span><span class="sxs-lookup"><span data-stu-id="c7d61-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="c7d61-118">Attestazione</span><span class="sxs-lookup"><span data-stu-id="c7d61-118">Claim</span></span> | <span data-ttu-id="c7d61-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7d61-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7d61-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="c7d61-120">**ver**</span></span> |<span data-ttu-id="c7d61-121">versione di Hello del token app hello.</span><span class="sxs-lookup"><span data-stu-id="c7d61-121">hello version of hello app token.</span></span> <span data-ttu-id="c7d61-122">0.2.0 è la versione corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="c7d61-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="c7d61-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="c7d61-123">**aud**</span></span> |<span data-ttu-id="c7d61-124">Hello destinatario del token hello.</span><span class="sxs-lookup"><span data-stu-id="c7d61-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="c7d61-125">Per Power BI Embedded usare: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="c7d61-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="c7d61-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="c7d61-126">**iss**</span></span> |<span data-ttu-id="c7d61-127">Stringa che indica un'applicazione hello che ha rilasciato il token hello.</span><span class="sxs-lookup"><span data-stu-id="c7d61-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="c7d61-128">**type**</span><span class="sxs-lookup"><span data-stu-id="c7d61-128">**type**</span></span> |<span data-ttu-id="c7d61-129">tipo di Hello del token di app che viene creato.</span><span class="sxs-lookup"><span data-stu-id="c7d61-129">hello type of app token which is being created.</span></span> <span data-ttu-id="c7d61-130">Tipo di hello è supportato solo corrente è **incorporare**.</span><span class="sxs-lookup"><span data-stu-id="c7d61-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="c7d61-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="c7d61-131">**wcn**</span></span> |<span data-ttu-id="c7d61-132">Token hello del nome dell'area di lavoro insieme viene emessa per.</span><span class="sxs-lookup"><span data-stu-id="c7d61-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="c7d61-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="c7d61-133">**wid**</span></span> |<span data-ttu-id="c7d61-134">Token di hello ID area di lavoro viene emessa per.</span><span class="sxs-lookup"><span data-stu-id="c7d61-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="c7d61-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="c7d61-135">**rid**</span></span> |<span data-ttu-id="c7d61-136">Report è rilasciato per il token hello ID.</span><span class="sxs-lookup"><span data-stu-id="c7d61-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="c7d61-137">**username** (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="c7d61-137">**username** (optional)</span></span> |<span data-ttu-id="c7d61-138">Utilizzato con una riga, questa è una stringa che consenta di identificare l'utente hello quando l'applicazione delle regole di riga.</span><span class="sxs-lookup"><span data-stu-id="c7d61-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="c7d61-139">**roles** (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="c7d61-139">**roles** (optional)</span></span> |<span data-ttu-id="c7d61-140">Stringa contenente hello ruoli tooselect quando l'applicazione delle regole di sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="c7d61-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="c7d61-141">Se si passa più di un ruolo, è consigliabile passarli come matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="c7d61-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="c7d61-142">**scp** (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="c7d61-142">**scp** (optional)</span></span> |<span data-ttu-id="c7d61-143">Stringa contenente gli ambiti delle autorizzazioni hello.</span><span class="sxs-lookup"><span data-stu-id="c7d61-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="c7d61-144">Se si passa più di un ruolo, è consigliabile passarli come matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="c7d61-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="c7d61-145">**exp** (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="c7d61-145">**exp** (optional)</span></span> |<span data-ttu-id="c7d61-146">Indica il tempo di hello in cui hello token scadrà.</span><span class="sxs-lookup"><span data-stu-id="c7d61-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="c7d61-147">Questi valori devono essere passati come timestamp Unix.</span><span class="sxs-lookup"><span data-stu-id="c7d61-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="c7d61-148">**nbf** (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="c7d61-148">**nbf** (optional)</span></span> |<span data-ttu-id="c7d61-149">Indica il tempo di hello in cui hello token inizia validi.</span><span class="sxs-lookup"><span data-stu-id="c7d61-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="c7d61-150">Questi valori devono essere passati come timestamp Unix.</span><span class="sxs-lookup"><span data-stu-id="c7d61-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="c7d61-151">Un token dell'app di esempio avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="c7d61-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="c7d61-152">Quando viene decodificato, avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="c7d61-152">When decoded, it will look something like this:</span></span>

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

<span data-ttu-id="c7d61-153">Sono disponibili metodi all'interno di hello SDK che consentono di semplificare la creazione di apptokens.</span><span class="sxs-lookup"><span data-stu-id="c7d61-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="c7d61-154">Ad esempio, per .NET è possibile esaminare hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) classe e hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metodi.</span><span class="sxs-lookup"><span data-stu-id="c7d61-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="c7d61-155">Per hello .NET SDK, è possibile fare riferimento troppo[ambiti](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="c7d61-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="c7d61-156">Ambiti</span><span class="sxs-lookup"><span data-stu-id="c7d61-156">Scopes</span></span>

<span data-ttu-id="c7d61-157">Quando si utilizza il token di incorporamento, è consigliabile toorestrict utilizzo delle risorse di hello a che si concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c7d61-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="c7d61-158">Per questo motivo, è possibile generare un token con autorizzazioni con ambito.</span><span class="sxs-lookup"><span data-stu-id="c7d61-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="c7d61-159">di seguito Hello sono gli ambiti disponibili hello per Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c7d61-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="c7d61-160">Scope</span><span class="sxs-lookup"><span data-stu-id="c7d61-160">Scope</span></span>|<span data-ttu-id="c7d61-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7d61-161">Description</span></span>|
|---|---|
|<span data-ttu-id="c7d61-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="c7d61-162">Dataset.Read</span></span>|<span data-ttu-id="c7d61-163">Sono disponibili autorizzazioni hello tooread specificato set di dati.</span><span class="sxs-lookup"><span data-stu-id="c7d61-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="c7d61-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="c7d61-164">Dataset.Write</span></span>|<span data-ttu-id="c7d61-165">Fornisce l'autorizzazione toowrite toohello specificato set di dati.</span><span class="sxs-lookup"><span data-stu-id="c7d61-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="c7d61-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="c7d61-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="c7d61-167">Fornisce l'autorizzazione tooread e scrittura toohello specificato set di dati.</span><span class="sxs-lookup"><span data-stu-id="c7d61-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="c7d61-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="c7d61-168">Report.Read</span></span>|<span data-ttu-id="c7d61-169">Sono disponibili autorizzazioni hello tooview specificato report.</span><span class="sxs-lookup"><span data-stu-id="c7d61-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="c7d61-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="c7d61-170">Report.ReadWrite</span></span>|<span data-ttu-id="c7d61-171">Fornisce la modifica e dell'autorizzazione tooview hello report specificato.</span><span class="sxs-lookup"><span data-stu-id="c7d61-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="c7d61-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="c7d61-172">Workspace.Report.Create</span></span>|<span data-ttu-id="c7d61-173">Fornisce un nuovo report all'interno di hello specificato di autorizzazione toocreate dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c7d61-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="c7d61-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="c7d61-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="c7d61-175">Fornisce un report esistente all'interno di hello specificato di autorizzazione tooclone dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c7d61-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="c7d61-176">È possibile fornire più ambiti mediante uno spazio tra gli ambiti di hello hello seguente.</span><span class="sxs-lookup"><span data-stu-id="c7d61-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="c7d61-177">**Attestazioni e ambiti necessari**</span><span class="sxs-lookup"><span data-stu-id="c7d61-177">**Required claims - scopes**</span></span>

<span data-ttu-id="c7d61-178">SCP: scopesClaim {scopesClaim} può essere una stringa o una matrice di stringhe, notando hello consentito autorizzazioni risorse tooworkspace (Report, set di dati e così via)</span><span class="sxs-lookup"><span data-stu-id="c7d61-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="c7d61-179">Un token decodificato, con gli ambiti definiti, avrà un aspetto simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="c7d61-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

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

### <a name="operations-and-scopes"></a><span data-ttu-id="c7d61-180">Operazioni e ambiti</span><span class="sxs-lookup"><span data-stu-id="c7d61-180">Operations and scopes</span></span>

|<span data-ttu-id="c7d61-181">Operazione</span><span class="sxs-lookup"><span data-stu-id="c7d61-181">Operation</span></span>|<span data-ttu-id="c7d61-182">Risorsa di destinazione</span><span class="sxs-lookup"><span data-stu-id="c7d61-182">Target resource</span></span>|<span data-ttu-id="c7d61-183">Autorizzazioni del token</span><span class="sxs-lookup"><span data-stu-id="c7d61-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="c7d61-184">Creare (in memoria) un nuovo report basato su un set di dati.</span><span class="sxs-lookup"><span data-stu-id="c7d61-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="c7d61-185">Set di dati</span><span class="sxs-lookup"><span data-stu-id="c7d61-185">Dataset</span></span>|<span data-ttu-id="c7d61-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="c7d61-186">Dataset.Read</span></span>|
|<span data-ttu-id="c7d61-187">Creare un nuovo report basato su un set di dati di (in memoria) e salvare report hello.</span><span class="sxs-lookup"><span data-stu-id="c7d61-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="c7d61-188">Set di dati</span><span class="sxs-lookup"><span data-stu-id="c7d61-188">Dataset</span></span>|<span data-ttu-id="c7d61-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="c7d61-189">* Dataset.Read</span></span><br><span data-ttu-id="c7d61-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="c7d61-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="c7d61-191">Visualizzare ed esplorare/modificare (in memoria) un report esistente.</span><span class="sxs-lookup"><span data-stu-id="c7d61-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="c7d61-192">Report.Read implica Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="c7d61-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="c7d61-193">In questo modo non autorizzazioni toosave modifiche.</span><span class="sxs-lookup"><span data-stu-id="c7d61-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="c7d61-194">Report</span><span class="sxs-lookup"><span data-stu-id="c7d61-194">Report</span></span>|<span data-ttu-id="c7d61-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="c7d61-195">Report.Read</span></span>|
|<span data-ttu-id="c7d61-196">Modificare e salvare un report esistente.</span><span class="sxs-lookup"><span data-stu-id="c7d61-196">Edit and save an existing report.</span></span>|<span data-ttu-id="c7d61-197">Report</span><span class="sxs-lookup"><span data-stu-id="c7d61-197">Report</span></span>|<span data-ttu-id="c7d61-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="c7d61-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="c7d61-199">Salvare una copia di un report (Salva con nome).</span><span class="sxs-lookup"><span data-stu-id="c7d61-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="c7d61-200">Report</span><span class="sxs-lookup"><span data-stu-id="c7d61-200">Report</span></span>|<span data-ttu-id="c7d61-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="c7d61-201">* Report.Read</span></span><br><span data-ttu-id="c7d61-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="c7d61-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="c7d61-203">Ecco il funzionamento del flusso di hello</span><span class="sxs-lookup"><span data-stu-id="c7d61-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="c7d61-204">Copiare un'applicazione hello API chiavi tooyour.</span><span class="sxs-lookup"><span data-stu-id="c7d61-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="c7d61-205">È possibile ottenere le chiavi di hello in **portale Azure**.</span><span class="sxs-lookup"><span data-stu-id="c7d61-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="c7d61-206">Il token esegue l'asserzione di un'attestazione e ha una scadenza.</span><span class="sxs-lookup"><span data-stu-id="c7d61-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="c7d61-207">Con le chiavi di accesso API si accede al token.</span><span class="sxs-lookup"><span data-stu-id="c7d61-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="c7d61-208">L'utente richiede tooview un report.</span><span class="sxs-lookup"><span data-stu-id="c7d61-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="c7d61-209">Il token viene convalidato con chiavi di accesso API.</span><span class="sxs-lookup"><span data-stu-id="c7d61-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="c7d61-210">Power BI Embedded invia toouser un report.</span><span class="sxs-lookup"><span data-stu-id="c7d61-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="c7d61-211">Dopo aver **Power BI Embedded** invia un utente, toohello hello visualizzare i report di hello nell'applicazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c7d61-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="c7d61-212">Ad esempio, se è stata importata hello [esempio di analisi delle vendite dati PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), app web di esempio hello è analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="c7d61-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="c7d61-213">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7d61-213">See Also</span></span>

[<span data-ttu-id="c7d61-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="c7d61-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="c7d61-215">Introduzione all'esempio di Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c7d61-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="c7d61-216">Scenari comuni di Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c7d61-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="c7d61-217">Introduzione a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c7d61-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="c7d61-218">Repository Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="c7d61-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="c7d61-219">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="c7d61-219">More questions?</span></span> [<span data-ttu-id="c7d61-220">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="c7d61-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

