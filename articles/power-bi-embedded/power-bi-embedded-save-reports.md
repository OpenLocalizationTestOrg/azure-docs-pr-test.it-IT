---
title: aaaSave report in Power BI Embedded Azure | Documenti Microsoft
description: "Informazioni sull'incorporamento di report toosave all'interno di Power BI. Ciò richiede autorizzazioni appropriate nell'ordine toowork correttamente."
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="d426d-104">Salvare i report in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d426d-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="d426d-105">Informazioni sull'incorporamento di report toosave all'interno di Power BI.</span><span class="sxs-lookup"><span data-stu-id="d426d-105">Learn how toosave reports within Power BI embedded.</span></span> <span data-ttu-id="d426d-106">Ciò richiede autorizzazioni appropriate nell'ordine toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="d426d-106">This requires proper permissions in order toowork successfully.</span></span>

<span data-ttu-id="d426d-107">Con Power BI Embedded è possibile modificare report esistenti e salvarli,</span><span class="sxs-lookup"><span data-stu-id="d426d-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="d426d-108">È anche possibile creare un nuovo report e salvare come un nuovo toocreate report uno.</span><span class="sxs-lookup"><span data-stu-id="d426d-108">You can also create a new report and save as a new report toocreate one.</span></span>

<span data-ttu-id="d426d-109">In ordine toosave un report è necessario innanzitutto toocreate un token per il report specifico di hello con ambiti destra hello:</span><span class="sxs-lookup"><span data-stu-id="d426d-109">In order toosave a report you first need toocreate a token for hello specific report with hello right scopes:</span></span>

* <span data-ttu-id="d426d-110">è necessario tooenable Salva Report.ReadWrite ambito</span><span class="sxs-lookup"><span data-stu-id="d426d-110">tooenable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="d426d-111">tooenable Salva come ambiti Report.Read e Workspace.Report.Copy sono necessari</span><span class="sxs-lookup"><span data-stu-id="d426d-111">tooenable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="d426d-112">tooenable salvataggio e la Salva con nome, Report.ReadWrite e Workspace.Report.Copy requierd</span><span class="sxs-lookup"><span data-stu-id="d426d-112">tooenable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="d426d-113">Rispettivamente in hello tooenable ordine destra Salva o Salva come i pulsanti nel menu file necessario tooprovide hello destro autorizzazione nella configurazione di incorporamento hello quando si incorpora hello report:</span><span class="sxs-lookup"><span data-stu-id="d426d-113">Respectively in order tooenable hello right save/save as buttons in file menu you need tooprovide hello right permission in hello Embed configuration when you Embed hello report:</span></span>

* <span data-ttu-id="d426d-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="d426d-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="d426d-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="d426d-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="d426d-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="d426d-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="d426d-117">Il token di accesso deve inoltre dagli ambiti appropriati hello.</span><span class="sxs-lookup"><span data-stu-id="d426d-117">Your access token also needs hello appropriate scopes.</span></span> <span data-ttu-id="d426d-118">Per altre informazioni, vedere [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ambiti).</span><span class="sxs-lookup"><span data-stu-id="d426d-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="d426d-119">Incorporare un report in modalità di modifica</span><span class="sxs-lookup"><span data-stu-id="d426d-119">Embed report in edit mode</span></span>

<span data-ttu-id="d426d-120">Di seguito si desidera tooEmbed un report in modalità di modifica all'interno dell'app, toodo così sufficiente passare le proprietà a destra di hello nella configurazione di incorporamento chiamare powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="d426d-120">Let's say you want tooEmbed a report in edit mode inside your app, toodo so just pass hello right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="d426d-121">Sarà necessario toosupply autorizzazioni e un viewMode di hello toosee di ordine di salvataggio e salvare come pulsanti quando è in modalità di modifica.</span><span class="sxs-lookup"><span data-stu-id="d426d-121">You will need toosupply permissions and a viewMode in order toosee hello save and save as buttons when in edit mode.</span></span> <span data-ttu-id="d426d-122">Per altre informazioni, vedere [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Dettagli della configurazione di incorporamento).</span><span class="sxs-lookup"><span data-stu-id="d426d-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="d426d-123">In JavaScript, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d426d-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="d426d-124">Un report sarà così incorporato nell'app in modalità di modifica.</span><span class="sxs-lookup"><span data-stu-id="d426d-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="d426d-125">Salvare il report</span><span class="sxs-lookup"><span data-stu-id="d426d-125">Save report</span></span>

<span data-ttu-id="d426d-126">Dopo che i report di hello Embbeding in modalità con diritto token hello e autorizzazioni di modifica è possibile salvare report hello dal menu file hello o da javascript:</span><span class="sxs-lookup"><span data-stu-id="d426d-126">After Embbeding hello report in edit mode with hello right token and permissions you can save hello report from hello file menu or from javascript:</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="d426d-127">Salva con nome</span><span class="sxs-lookup"><span data-stu-id="d426d-127">Save as</span></span>

```
// Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="d426d-128">Un nuovo report viene creato solo dopo l'operazione *Salva con nome*.</span><span class="sxs-lookup"><span data-stu-id="d426d-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="d426d-129">Dopo hello salvato, area di disegno hello è ancora visualizzazione di report precedente hello modifica la modalità e non hello nuovo report.</span><span class="sxs-lookup"><span data-stu-id="d426d-129">After hello save, hello canvas is still showing hello old report in edit mode and not hello new report.</span></span> <span data-ttu-id="d426d-130">Sarà necessario tooembed hello nuovo report che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="d426d-130">You will need tooembed hello new report that was created.</span></span> <span data-ttu-id="d426d-131">A questo scopo è necessario un nuovo token di accesso, perché vengono creati per singolo report.</span><span class="sxs-lookup"><span data-stu-id="d426d-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="d426d-132">Sarà quindi necessario nuovo report hello tooload dopo un *salvare come*.</span><span class="sxs-lookup"><span data-stu-id="d426d-132">You will then need tooload hello new report after a *save as*.</span></span> <span data-ttu-id="d426d-133">Ciò è simile tooembedding qualsiasi report.</span><span class="sxs-lookup"><span data-stu-id="d426d-133">This is similar tooembedding any report.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a><span data-ttu-id="d426d-134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d426d-134">See also</span></span>

[<span data-ttu-id="d426d-135">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="d426d-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="d426d-136">Incorporare un report</span><span class="sxs-lookup"><span data-stu-id="d426d-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="d426d-137">Creare un nuovo report da un set di dati</span><span class="sxs-lookup"><span data-stu-id="d426d-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="d426d-138">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d426d-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="d426d-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d426d-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="d426d-140">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="d426d-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="d426d-141">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="d426d-141">More questions?</span></span> [<span data-ttu-id="d426d-142">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="d426d-142">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

