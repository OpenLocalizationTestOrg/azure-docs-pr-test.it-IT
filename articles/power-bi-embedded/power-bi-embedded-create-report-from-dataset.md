---
title: Creare un nuovo report da un set di dati in Azure Power BI Embedded | Microsoft Docs
description: "È ora possibile creare report di Power BI Embedded da un set di dati nell'applicazione."
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
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="b1dba-103">Creare un nuovo report da un set di dati in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b1dba-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="b1dba-104">È ora possibile creare report di Power BI Embedded da un set di dati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b1dba-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="b1dba-105">Il metodo di autenticazione è simile a quello usato per l'incorporamento di report</span><span class="sxs-lookup"><span data-stu-id="b1dba-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="b1dba-106">ed è basato su token di accesso specifici di un set di dati.</span><span class="sxs-lookup"><span data-stu-id="b1dba-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="b1dba-107">I token usati per PowerBI.com vengono rilasciati da Azure Active Directory (AAD) e quelli per Power BI Embedded vengono rilasciati dal servizio dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b1dba-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="b1dba-108">Quando si crea un report incorporato, i token rilasciati riguardano un set di dati specifico.</span><span class="sxs-lookup"><span data-stu-id="b1dba-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="b1dba-109">I token dovranno essere associati all'URL di incorporamento per lo stesso elemento affinché ognuno abbia un token univoco.</span><span class="sxs-lookup"><span data-stu-id="b1dba-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="b1dba-110">Per creare un report incorporato, nel token di accesso devono essere specificati gli ambiti *Dataset.Read e Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="b1dba-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="b1dba-111">Creare il token di accesso necessario per creare un nuovo report</span><span class="sxs-lookup"><span data-stu-id="b1dba-111">Create access token needed to create new report</span></span>

<span data-ttu-id="b1dba-112">Power BI Embedded usa token di incorporamento, che sono token JSON Web con firma HMAC.</span><span class="sxs-lookup"><span data-stu-id="b1dba-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="b1dba-113">I token sono firmati con la chiave di accesso della raccolta di aree di lavoro di Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b1dba-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="b1dba-114">Per impostazione predefinita, i token di incorporamento vengono usati per concedere l'accesso di sola lettura a un report da incorporare in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b1dba-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="b1dba-115">I token di incorporamento vengono rilasciati per un report specifico e dovranno essere associati a un URL di incorporamento.</span><span class="sxs-lookup"><span data-stu-id="b1dba-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="b1dba-116">I token di accesso devono essere creati nel server perché le chiavi di accesso vengono usate per firmare/crittografare i token.</span><span class="sxs-lookup"><span data-stu-id="b1dba-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="b1dba-117">Per informazioni sulla creazione di un token di accesso, vedere [Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="b1dba-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="b1dba-118">È anche possibile esaminare il metodo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="b1dba-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="b1dba-119">Di seguito è riportato un esempio corrispondente all'uso di .NET SDK per Power BI.</span><span class="sxs-lookup"><span data-stu-id="b1dba-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="b1dba-120">In questo esempio si ha l'ID set di dati su cui si vuole creare il nuovo report.</span><span class="sxs-lookup"><span data-stu-id="b1dba-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="b1dba-121">È anche necessario aggiungere gli ambiti per *Dataset.Read e Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="b1dba-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="b1dba-122">La *classe PowerBIToken* richiede l'installazione del [pacchetto NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="b1dba-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="b1dba-123">**Installazione del pacchetto NuGet**</span><span class="sxs-lookup"><span data-stu-id="b1dba-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="b1dba-124">**Codice C#**</span><span class="sxs-lookup"><span data-stu-id="b1dba-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="b1dba-125">Creare un nuovo report vuoto</span><span class="sxs-lookup"><span data-stu-id="b1dba-125">Create a new blank report</span></span>

<span data-ttu-id="b1dba-126">Per creare un nuovo report, deve essere specificata la configurazione di creazione.</span><span class="sxs-lookup"><span data-stu-id="b1dba-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="b1dba-127">Questa dovrà includere il token di accesso, l'URL di incorporamento e l'ID set di dati per cui si vuole creare il report.</span><span class="sxs-lookup"><span data-stu-id="b1dba-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="b1dba-128">Ciò richiede l'installazione del [pacchetto Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="b1dba-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="b1dba-129">L'URL di incorporamento sarà https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="b1dba-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="b1dba-130">Per testare il funzionamento, è possibile usare l'[esempio dell'incorporamento di report con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/),</span><span class="sxs-lookup"><span data-stu-id="b1dba-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="b1dba-131">che offre anche esempi di codice per le diverse operazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="b1dba-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="b1dba-132">**Installazione del pacchetto NuGet**</span><span class="sxs-lookup"><span data-stu-id="b1dba-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="b1dba-133">**Codice JavaScript**</span><span class="sxs-lookup"><span data-stu-id="b1dba-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="b1dba-134">Chiamando *powerbi.createReport()* verrà visualizzata un'area di disegno vuota in modalità di modifica nell'elemento *div*.</span><span class="sxs-lookup"><span data-stu-id="b1dba-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="b1dba-135">Salvare i nuovi report</span><span class="sxs-lookup"><span data-stu-id="b1dba-135">Save new reports</span></span>

<span data-ttu-id="b1dba-136">Il report non verrà effettivamente creato finché non si chiama l'operazione **Salva con nome**.</span><span class="sxs-lookup"><span data-stu-id="b1dba-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="b1dba-137">A tale scopo è possibile usare il menu File o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b1dba-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="b1dba-138">Un nuovo report viene creato solo dopo che è stata chiamata l'operazione **Salva con nome**.</span><span class="sxs-lookup"><span data-stu-id="b1dba-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="b1dba-139">Dopo il salvataggio, l'area di disegno continuerà a visualizzare il set di dati in modalità di modifica e non il report.</span><span class="sxs-lookup"><span data-stu-id="b1dba-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="b1dba-140">Sarà necessario ricaricare il nuovo report nello stesso modo in cui si ricarica qualsiasi altro report.</span><span class="sxs-lookup"><span data-stu-id="b1dba-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="b1dba-141">Caricare il nuovo report</span><span class="sxs-lookup"><span data-stu-id="b1dba-141">Load the new report</span></span>

<span data-ttu-id="b1dba-142">Per interagire con il nuovo report è necessario incorporarlo così come l'applicazione incorpora un report regolare, ovvero è necessario rilasciare un nuovo token specifico per il nuovo report e quindi chiamare il metodo di incorporamento.</span><span class="sxs-lookup"><span data-stu-id="b1dba-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="b1dba-143">Automatizzare il salvataggio e il caricamento di un nuovo report con l'evento "saved"</span><span class="sxs-lookup"><span data-stu-id="b1dba-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="b1dba-144">Per automatizzare il processo di salvataggio con nome e successivo caricamento del nuovo report, è possibile usare l'evento "saved".</span><span class="sxs-lookup"><span data-stu-id="b1dba-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="b1dba-145">Questo evento viene generato al termine dell'operazione di salvataggio e restituisce un oggetto JSON che contiene il nuovo ID report, il nome del report e l'ID report precedente (se esistente) e specifica se si è trattato di un'operazione di salvataggio o di salvataggio con nome.</span><span class="sxs-lookup"><span data-stu-id="b1dba-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="b1dba-146">Per automatizzare il processo è possibile restare in ascolto dell'evento "saved", usare il nuovo ID report per creare il nuovo token e incorporare il nuovo report con tale token.</span><span class="sxs-lookup"><span data-stu-id="b1dba-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="b1dba-147">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b1dba-147">See also</span></span>

[<span data-ttu-id="b1dba-148">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="b1dba-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="b1dba-149">Salvare i report</span><span class="sxs-lookup"><span data-stu-id="b1dba-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="b1dba-150">Incorporare un report</span><span class="sxs-lookup"><span data-stu-id="b1dba-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="b1dba-151">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b1dba-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b1dba-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b1dba-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="b1dba-153">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="b1dba-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="b1dba-154">Pacchetto NuGet Power BI Core</span><span class="sxs-lookup"><span data-stu-id="b1dba-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="b1dba-155">Pacchetto Power BI JavaScript</span><span class="sxs-lookup"><span data-stu-id="b1dba-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="b1dba-156">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="b1dba-156">More questions?</span></span> [<span data-ttu-id="b1dba-157">Contattare la community di Power BI</span><span class="sxs-lookup"><span data-stu-id="b1dba-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)