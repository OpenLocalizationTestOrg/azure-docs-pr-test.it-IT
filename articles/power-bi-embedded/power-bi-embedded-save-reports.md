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
# <a name="save-reports-in-power-bi-embedded"></a>Salvare i report in Power BI Embedded

Informazioni sull'incorporamento di report toosave all'interno di Power BI. Ciò richiede autorizzazioni appropriate nell'ordine toowork correttamente.

Con Power BI Embedded è possibile modificare report esistenti e salvarli, È anche possibile creare un nuovo report e salvare come un nuovo toocreate report uno.

In ordine toosave un report è necessario innanzitutto toocreate un token per il report specifico di hello con ambiti destra hello:

* è necessario tooenable Salva Report.ReadWrite ambito
* tooenable Salva come ambiti Report.Read e Workspace.Report.Copy sono necessari
* tooenable salvataggio e la Salva con nome, Report.ReadWrite e Workspace.Report.Copy requierd

Rispettivamente in hello tooenable ordine destra Salva o Salva come i pulsanti nel menu file necessario tooprovide hello destro autorizzazione nella configurazione di incorporamento hello quando si incorpora hello report:

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> Il token di accesso deve inoltre dagli ambiti appropriati hello. Per altre informazioni, vedere [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ambiti).

## <a name="embed-report-in-edit-mode"></a>Incorporare un report in modalità di modifica

Di seguito si desidera tooEmbed un report in modalità di modifica all'interno dell'app, toodo così sufficiente passare le proprietà a destra di hello nella configurazione di incorporamento chiamare powerbi.embed(). Sarà necessario toosupply autorizzazioni e un viewMode di hello toosee di ordine di salvataggio e salvare come pulsanti quando è in modalità di modifica. Per altre informazioni, vedere [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Dettagli della configurazione di incorporamento).

In JavaScript, ad esempio:

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

Un report sarà così incorporato nell'app in modalità di modifica.

## <a name="save-report"></a>Salvare il report

Dopo che i report di hello Embbeding in modalità con diritto token hello e autorizzazioni di modifica è possibile salvare report hello dal menu file hello o da javascript:

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Salva con nome

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
> Un nuovo report viene creato solo dopo l'operazione *Salva con nome*. Dopo hello salvato, area di disegno hello è ancora visualizzazione di report precedente hello modifica la modalità e non hello nuovo report. Sarà necessario tooembed hello nuovo report che è stato creato. A questo scopo è necessario un nuovo token di accesso, perché vengono creati per singolo report.

Sarà quindi necessario nuovo report hello tooload dopo un *salvare come*. Ciò è simile tooembedding qualsiasi report.

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

## <a name="see-also"></a>Vedere anche

[Esempio introduttivo](power-bi-embedded-get-started-sample.md)  
[Incorporare un report](power-bi-embedded-embed-report.md)  
[Creare un nuovo report da un set di dati](power-bi-embedded-create-report-from-dataset.md)  
[Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Esempio di incorporamento con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)

