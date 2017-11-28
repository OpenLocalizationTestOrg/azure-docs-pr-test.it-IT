---
title: "aaaToggle tra la modalità di visualizzazione e modifica per i report in Power BI Embedded Azure | Documenti Microsoft"
description: "Informazioni su come tootoggle tra la modalità di visualizzazione e modifica per i report all'interno di Power BI Embedded."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="79261-103">Passare dalla modalità di visualizzazione alla modalità di modifica dei report e viceversa in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="79261-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="79261-104">Informazioni su come tootoggle tra la modalità di visualizzazione e modifica per i report all'interno di Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="79261-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="79261-105">Creazione di un token di accesso</span><span class="sxs-lookup"><span data-stu-id="79261-105">Creating an access token</span></span>

<span data-ttu-id="79261-106">Sarà necessario toocreate un token di accesso che consente di visualizzare di tooboth possibilità hello e modificare un report.</span><span class="sxs-lookup"><span data-stu-id="79261-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="79261-107">tooedit e salvare un report, sarà necessario hello **Report.ReadWrite** token di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="79261-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="79261-108">Per altre informazioni, vedere [Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="79261-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="79261-109">Verrà consentono tooedit e salvare le modifiche tooan report esistente.</span><span class="sxs-lookup"><span data-stu-id="79261-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="79261-110">Se si desidera anche la funzione hello di supportare **Salva con nome**, sarà necessario toosupply ulteriori autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="79261-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="79261-111">Per altre informazioni, vedere [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ambiti).</span><span class="sxs-lookup"><span data-stu-id="79261-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="79261-112">Configurazione di incorporamento</span><span class="sxs-lookup"><span data-stu-id="79261-112">Embed configuration</span></span>

<span data-ttu-id="79261-113">Sarà necessario toosupply autorizzazioni e un viewMode di hello toosee ordine Salva pulsante quando è in modalità di modifica.</span><span class="sxs-lookup"><span data-stu-id="79261-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="79261-114">Per altre informazioni, vedere [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Dettagli della configurazione di incorporamento).</span><span class="sxs-lookup"><span data-stu-id="79261-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="79261-115">In JavaScript, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="79261-115">For example in JavaScript:</span></span>

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

<span data-ttu-id="79261-116">Ciò indicherà report hello tooembed in modalità di visualizzazione in base alle **viewMode** impostato troppo**modelli. ViewMode.View**.</span><span class="sxs-lookup"><span data-stu-id="79261-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="79261-117">Modalità di visualizzazione</span><span class="sxs-lookup"><span data-stu-id="79261-117">View mode</span></span>

<span data-ttu-id="79261-118">È possibile utilizzare hello seguente tooswitch JavaScript in modalità di visualizzazione, se si è in modalità di modifica.</span><span class="sxs-lookup"><span data-stu-id="79261-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="79261-119">Modalità di modifica</span><span class="sxs-lookup"><span data-stu-id="79261-119">Edit mode</span></span>

<span data-ttu-id="79261-120">È possibile utilizzare hello seguente tooswitch JavaScript in modalità di modifica, se si è nella visualizzazione modalità.</span><span class="sxs-lookup"><span data-stu-id="79261-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="79261-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="79261-121">See also</span></span>

[<span data-ttu-id="79261-122">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="79261-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="79261-123">Incorporare un report</span><span class="sxs-lookup"><span data-stu-id="79261-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="79261-124">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="79261-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="79261-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="79261-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="79261-126">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="79261-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="79261-127">Repository Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="79261-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="79261-128">Repository Git PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="79261-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="79261-129">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="79261-129">More questions?</span></span> [<span data-ttu-id="79261-130">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="79261-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
