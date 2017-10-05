---
title: Incorporare un report in Azure Power BI Embedded | Microsoft Docs
description: Informazioni su come incorporare nell'applicazione un report che si trova in Power BI Embedded.
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="4e844-103">Incorporare un report in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4e844-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="4e844-104">Informazioni su come incorporare nell'applicazione un report che si trova in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="4e844-104">Learn how to embed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="4e844-105">Verrà esaminato come incorporare effettivamente un report nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4e844-105">We will look at how to actually embed a report into your application.</span></span> <span data-ttu-id="4e844-106">Ciò presuppone che esista già un report in un'area di lavoro della raccolta di aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4e844-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="4e844-107">Se questo passaggio non è ancora stato completato, vedere [Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4e844-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="4e844-108">Per compilare facilmente l'applicazione con Power BI Embedded, è possibile usare l'SDK per .NET (C#) o Node.js, insieme a JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4e844-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span></span> 

## <a name="using-the-access-keys-to-use-rest-apis"></a><span data-ttu-id="4e844-109">Uso delle chiavi di accesso per API REST</span><span class="sxs-lookup"><span data-stu-id="4e844-109">Using the access keys to use REST APIs</span></span>

<span data-ttu-id="4e844-110">Per chiamare l'API REST, è possibile passare la chiave di accesso che può essere ottenuta dal portale di Azure per una determinata raccolta di aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4e844-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span></span> <span data-ttu-id="4e844-111">Per altre informazioni, vedere [Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4e844-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="4e844-112">Ottenere un ID report</span><span class="sxs-lookup"><span data-stu-id="4e844-112">Get a report id</span></span>

<span data-ttu-id="4e844-113">Ogni token di accesso è basato su un report.</span><span class="sxs-lookup"><span data-stu-id="4e844-113">Every access token is based on a report.</span></span> <span data-ttu-id="4e844-114">È necessario ottenere lo specifico ID del report che si vuole incorporare.</span><span class="sxs-lookup"><span data-stu-id="4e844-114">You will need to get the given report id for the report that you want to embed.</span></span> <span data-ttu-id="4e844-115">A questo scopo è possibile effettuare chiamate all'API REST [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx),</span><span class="sxs-lookup"><span data-stu-id="4e844-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="4e844-116">che restituirà l'ID report e l'URL di incorporamento.</span><span class="sxs-lookup"><span data-stu-id="4e844-116">This will return the report id and the embed url.</span></span> <span data-ttu-id="4e844-117">È possibile usare Power BI .NET SDK oppure chiamare direttamente l'API REST.</span><span class="sxs-lookup"><span data-stu-id="4e844-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span></span>

### <a name="using-the-power-bi-net-sdk"></a><span data-ttu-id="4e844-118">Uso di Power BI .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4e844-118">Using the Power BI .NET SDK</span></span>

<span data-ttu-id="4e844-119">Quando si usa .NET SDK, è necessario creare una credenziale token basata sulla chiave di accesso ottenuta dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e844-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span></span> <span data-ttu-id="4e844-120">Ciò richiede l'installazione del [pacchetto NuGet Power BI API](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="4e844-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="4e844-121">**Installazione del pacchetto NuGet**</span><span class="sxs-lookup"><span data-stu-id="4e844-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="4e844-122">**Codice C#**</span><span class="sxs-lookup"><span data-stu-id="4e844-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a><span data-ttu-id="4e844-123">Chiamata diretta dell'API REST</span><span class="sxs-lookup"><span data-stu-id="4e844-123">Calling the REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="4e844-124">Creare un token di accesso</span><span class="sxs-lookup"><span data-stu-id="4e844-124">Create an access token</span></span>

<span data-ttu-id="4e844-125">Power BI Embedded usa token di incorporamento, che sono token JSON Web con firma HMAC.</span><span class="sxs-lookup"><span data-stu-id="4e844-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="4e844-126">I token sono firmati con la chiave di accesso della raccolta di aree di lavoro di Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="4e844-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="4e844-127">Per impostazione predefinita, i token di incorporamento vengono usati per concedere l'accesso di sola lettura a un report da incorporare in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4e844-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="4e844-128">I token di incorporamento vengono rilasciati per un report specifico e dovranno essere associati a un URL di incorporamento.</span><span class="sxs-lookup"><span data-stu-id="4e844-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="4e844-129">I token di accesso devono essere creati nel server perché le chiavi di accesso vengono usate per firmare/crittografare i token.</span><span class="sxs-lookup"><span data-stu-id="4e844-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="4e844-130">Per informazioni sulla creazione di un token di accesso, vedere [Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="4e844-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="4e844-131">È anche possibile esaminare il metodo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="4e844-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="4e844-132">Di seguito è riportato un esempio corrispondente all'uso di .NET SDK per Power BI.</span><span class="sxs-lookup"><span data-stu-id="4e844-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="4e844-133">Verrà usato l'ID report recuperato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4e844-133">You will use the report id that you retrieved earlier.</span></span> <span data-ttu-id="4e844-134">Dopo la creazione del token di incorporamento, si userà la chiave di accesso per generare il token utilizzabile per JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4e844-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span></span> <span data-ttu-id="4e844-135">La *classe PowerBIToken* richiede l'installazione del [pacchetto NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="4e844-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="4e844-136">**Installazione del pacchetto NuGet**</span><span class="sxs-lookup"><span data-stu-id="4e844-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="4e844-137">**Codice C#**</span><span class="sxs-lookup"><span data-stu-id="4e844-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a><span data-ttu-id="4e844-138">Aggiunta degli ambiti di autorizzazione ai token di incorporamento</span><span class="sxs-lookup"><span data-stu-id="4e844-138">Adding permission scopes to embed tokens</span></span>

<span data-ttu-id="4e844-139">Quando si usano token di incorporamento, può essere opportuno limitare l'utilizzo delle risorse a cui si concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="4e844-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="4e844-140">Per questo motivo, è possibile generare un token con autorizzazioni con ambito.</span><span class="sxs-lookup"><span data-stu-id="4e844-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="4e844-141">Per altre informazioni, vedere [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ambiti).</span><span class="sxs-lookup"><span data-stu-id="4e844-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="4e844-142">Incorporare con JavaScript</span><span class="sxs-lookup"><span data-stu-id="4e844-142">Embed using JavaScript</span></span>

<span data-ttu-id="4e844-143">Dopo aver ottenuto il token di accesso e l'ID report, è possibile incorporare il report con JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4e844-143">After you have the access token and the report id, we can embed the report using JavaScript.</span></span> <span data-ttu-id="4e844-144">Ciò richiede l'installazione del [pacchetto Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="4e844-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="4e844-145">L'URL di incorporamento sarà https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="4e844-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="4e844-146">Per testare il funzionamento, è possibile usare l'[esempio dell'incorporamento di report con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/),</span><span class="sxs-lookup"><span data-stu-id="4e844-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="4e844-147">che offre anche esempi di codice per le diverse operazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="4e844-147">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="4e844-148">**Installazione del pacchetto NuGet**</span><span class="sxs-lookup"><span data-stu-id="4e844-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="4e844-149">**Codice JavaScript**</span><span class="sxs-lookup"><span data-stu-id="4e844-149">**JavaScript code**</span></span>

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-the-size-of-embedded-elements"></a><span data-ttu-id="4e844-150">Impostare le dimensioni degli elementi incorporati</span><span class="sxs-lookup"><span data-stu-id="4e844-150">Set the size of embedded elements</span></span>

<span data-ttu-id="4e844-151">Il report verrà automaticamente incorporato in base alle dimensioni del contenitore.</span><span class="sxs-lookup"><span data-stu-id="4e844-151">The report will automatically be embedded based on the size of its container.</span></span> <span data-ttu-id="4e844-152">Per eseguire l'override delle dimensioni predefinite degli incorporamenti, è sufficiente aggiungere stili in linea o un attributo di classe CSS per larghezza e altezza.</span><span class="sxs-lookup"><span data-stu-id="4e844-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="4e844-153">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="4e844-153">See also</span></span>

[<span data-ttu-id="4e844-154">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="4e844-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="4e844-155">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4e844-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="4e844-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="4e844-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="4e844-157">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="4e844-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="4e844-158">Pacchetto Power BI JavaScript</span><span class="sxs-lookup"><span data-stu-id="4e844-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="4e844-159">[Pacchetto NuGet Power BI API](https://www.nuget.org/profiles/powerbi)
[Pacchetto NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="4e844-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="4e844-160">Repository Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="4e844-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="4e844-161">Repository Git PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="4e844-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="4e844-162">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="4e844-162">More questions?</span></span> [<span data-ttu-id="4e844-163">Contattare la community di Power BI</span><span class="sxs-lookup"><span data-stu-id="4e844-163">Try the Power BI Community</span></span>](http://community.powerbi.com/)
