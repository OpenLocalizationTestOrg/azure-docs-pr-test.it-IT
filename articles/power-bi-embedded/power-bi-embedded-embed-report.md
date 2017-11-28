---
title: un report in Power BI Embedded Azure aaaEmbed | Documenti Microsoft
description: Informazioni su come tooembed un report in Power BI incorporato nell'applicazione.
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="40f15-103">Incorporare un report in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="40f15-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="40f15-104">Informazioni su come tooembed un report in Power BI incorporato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40f15-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="40f15-105">Verranno esaminati come tooactually incorporare un report nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40f15-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="40f15-106">Ciò presuppone che esista già un report in un'area di lavoro della raccolta di aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="40f15-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="40f15-107">Se questo passaggio non è ancora stato completato, vedere [Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="40f15-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="40f15-108">È possibile usare .NET hello (c#) o Node.js SDK, insieme a JavaScript, tooeasily compilare l'applicazione con Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="40f15-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="40f15-109">Utilizzo di hello accesso chiavi toouse API REST</span><span class="sxs-lookup"><span data-stu-id="40f15-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="40f15-110">In hello toocall ordine API REST, è possibile passare hello tasto di scelta che è possibile ottenere da hello portale di Azure per una raccolta di area di lavoro specificato.</span><span class="sxs-lookup"><span data-stu-id="40f15-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="40f15-111">Per altre informazioni, vedere [Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="40f15-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="40f15-112">Ottenere un ID report</span><span class="sxs-lookup"><span data-stu-id="40f15-112">Get a report id</span></span>

<span data-ttu-id="40f15-113">Ogni token di accesso è basato su un report.</span><span class="sxs-lookup"><span data-stu-id="40f15-113">Every access token is based on a report.</span></span> <span data-ttu-id="40f15-114">Sarà necessario hello tooget per report hello che si desidera tooembed l'id di report specificato.</span><span class="sxs-lookup"><span data-stu-id="40f15-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="40f15-115">Questa operazione può essere eseguita in base alle chiamate toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) API REST.</span><span class="sxs-lookup"><span data-stu-id="40f15-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="40f15-116">Report hello id e hello incorporare url verrà restituito.</span><span class="sxs-lookup"><span data-stu-id="40f15-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="40f15-117">Questa operazione può essere eseguita utilizzando hello SDK .NET di Power BI o chiamare direttamente l'API REST hello.</span><span class="sxs-lookup"><span data-stu-id="40f15-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="40f15-118">Utilizzo di hello SDK .NET di Power BI</span><span class="sxs-lookup"><span data-stu-id="40f15-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="40f15-119">Quando si utilizza hello .NET SDK, sarà necessario toocreate una credenziale del token di cui è basata sulla chiave di accesso hello che si ottiene da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40f15-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="40f15-120">Ciò è necessario installare hello [pacchetto NuGet dell'API Power BI](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="40f15-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="40f15-121">**Installazione del pacchetto NuGet**</span><span class="sxs-lookup"><span data-stu-id="40f15-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="40f15-122">**Codice C#**</span><span class="sxs-lookup"><span data-stu-id="40f15-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="40f15-123">Hello chiamata API REST direttamente</span><span class="sxs-lookup"><span data-stu-id="40f15-123">Calling hello REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="40f15-124">Creare un token di accesso</span><span class="sxs-lookup"><span data-stu-id="40f15-124">Create an access token</span></span>

<span data-ttu-id="40f15-125">Power BI Embedded usa token di incorporamento, che sono token JSON Web con firma HMAC.</span><span class="sxs-lookup"><span data-stu-id="40f15-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="40f15-126">i token Hello sono firmati con la chiave di accesso hello dalla raccolta di area di lavoro di Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="40f15-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="40f15-127">Incorporare i token, per impostazione predefinita, vengono utilizzati tooprovide leggere accedere solo tooa report tooembed in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40f15-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="40f15-128">I token di incorporamento vengono rilasciati per un report specifico e dovranno essere associati a un URL di incorporamento.</span><span class="sxs-lookup"><span data-stu-id="40f15-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="40f15-129">I token di accesso devono essere creati nel server di hello come chiavi di accesso hello sono utilizzati toosign o crittografare i token hello.</span><span class="sxs-lookup"><span data-stu-id="40f15-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="40f15-130">Per informazioni su come toocreate un token di accesso, vedere [autenticazione e autorizzazione a Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="40f15-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="40f15-131">È inoltre possibile rivedere hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metodo.</span><span class="sxs-lookup"><span data-stu-id="40f15-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="40f15-132">Di seguito è riportato un esempio di questo aspetto utilizzando hello .NET SDK per Power BI.</span><span class="sxs-lookup"><span data-stu-id="40f15-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="40f15-133">Si utilizzerà l'id di report hello recuperato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="40f15-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="40f15-134">Una volta hello incorporare token viene creato, si utilizzerà quindi hello accesso toogenerate chiave hello token utilizzabili dalla prospettiva di hello javascript.</span><span class="sxs-lookup"><span data-stu-id="40f15-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="40f15-135">Hello *PowerBIToken classe* richiede l'installazione di hello [Power BI Core NuGut pacchetto](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="40f15-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="40f15-136">**Installazione del pacchetto NuGet**</span><span class="sxs-lookup"><span data-stu-id="40f15-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="40f15-137">**Codice C#**</span><span class="sxs-lookup"><span data-stu-id="40f15-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="40f15-138">Aggiunta di token tooembed gli ambiti di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="40f15-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="40f15-139">Quando si utilizza il token di incorporamento, è consigliabile toorestrict utilizzo delle risorse di hello a che si concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="40f15-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="40f15-140">Per questo motivo, è possibile generare un token con autorizzazioni con ambito.</span><span class="sxs-lookup"><span data-stu-id="40f15-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="40f15-141">Per altre informazioni, vedere [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ambiti).</span><span class="sxs-lookup"><span data-stu-id="40f15-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="40f15-142">Incorporare con JavaScript</span><span class="sxs-lookup"><span data-stu-id="40f15-142">Embed using JavaScript</span></span>

<span data-ttu-id="40f15-143">Dopo aver ottenuto il token di accesso di hello e id report hello, è possibile incorporare report hello utilizzando JavaScript.</span><span class="sxs-lookup"><span data-stu-id="40f15-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="40f15-144">Ciò è necessario installare nuget hello [Power BI JavaScript pacchetto](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="40f15-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="40f15-145">embedUrl Hello sarà sufficiente https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="40f15-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="40f15-146">È possibile utilizzare hello [esempio incorporare Report di JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funzionalità.</span><span class="sxs-lookup"><span data-stu-id="40f15-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="40f15-147">Vengono inoltre forniti esempi di codice per operazioni diverse hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="40f15-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="40f15-148">**Installazione del pacchetto NuGet**</span><span class="sxs-lookup"><span data-stu-id="40f15-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="40f15-149">**Codice JavaScript**</span><span class="sxs-lookup"><span data-stu-id="40f15-149">**JavaScript code**</span></span>

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

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="40f15-150">Impostare le dimensioni di hello elementi incorporati</span><span class="sxs-lookup"><span data-stu-id="40f15-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="40f15-151">report Hello verranno incorporati automaticamente in base alle dimensioni di hello del relativo contenitore.</span><span class="sxs-lookup"><span data-stu-id="40f15-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="40f15-152">dimensioni predefinite di hello toooverride di hello incorpora semplicemente aggiungere una classe attributo o inline gli stili CSS per larghezza e altezza.</span><span class="sxs-lookup"><span data-stu-id="40f15-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="40f15-153">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="40f15-153">See also</span></span>

[<span data-ttu-id="40f15-154">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="40f15-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="40f15-155">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="40f15-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="40f15-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="40f15-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="40f15-157">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="40f15-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="40f15-158">Pacchetto Power BI JavaScript</span><span class="sxs-lookup"><span data-stu-id="40f15-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="40f15-159">[Pacchetto NuGet Power BI API](https://www.nuget.org/profiles/powerbi)
[Pacchetto NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="40f15-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="40f15-160">Repository Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="40f15-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="40f15-161">Repository Git PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="40f15-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="40f15-162">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="40f15-162">More questions?</span></span> [<span data-ttu-id="40f15-163">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="40f15-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
