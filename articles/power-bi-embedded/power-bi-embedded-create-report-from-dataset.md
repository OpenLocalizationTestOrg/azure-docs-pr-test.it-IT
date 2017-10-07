---
title: un nuovo report da un set di dati in Power BI Embedded Azure aaaCreate | Documenti Microsoft
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Creare un nuovo report da un set di dati in Power BI Embedded

È ora possibile creare report di Power BI Embedded da un set di dati nell'applicazione. 

Hello metodo di autenticazione è simile incorporare toothat del report. È basato su token di accesso che sono tooa specifico set di dati. I token usati per PowerBI.com vengono rilasciati da Azure Active Directory (AAD) e quelli per Power BI Embedded vengono rilasciati dal servizio dell'utente.

Quando hello di creazione di un report incorporato, i token rilasciati sono per un set di dati specifico. I token devono essere associati con hello incorporare URL su hello stesso elemento tooensure ogni dispone di un token univoco. In un report incorporato, ordinare toocreate *Dataset.Read e Workspace.Report.Create* gli ambiti devono essere forniti in token di accesso hello.

## <a name="create-access-token-needed-toocreate-new-report"></a>Crea nuovo report di access token toocreate necessari

Power BI Embedded usa token di incorporamento, che sono token JSON Web con firma HMAC. i token Hello sono firmati con la chiave di accesso hello dalla raccolta di area di lavoro di Azure Power BI Embedded. Incorporare i token, per impostazione predefinita, vengono utilizzati tooprovide leggere accedere solo tooa report tooembed in un'applicazione. I token di incorporamento vengono rilasciati per un report specifico e dovranno essere associati a un URL di incorporamento.

I token di accesso devono essere creati nel server di hello come chiavi di accesso hello sono utilizzati toosign o crittografare i token hello. Per informazioni su come toocreate un token di accesso, vedere [autenticazione e autorizzazione a Power BI Embedded](power-bi-embedded-app-token-flow.md). È inoltre possibile rivedere hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metodo. Di seguito è riportato un esempio di questo aspetto utilizzando hello .NET SDK per Power BI.

In questo esempio, è necessario l'id di set di dati che si desidera creare nuovi report hello di toocreat. È anche necessario ambiti hello tooadd per *Dataset.Read e Workspace.Report.Create*.

Hello *PowerBIToken classe* richiede l'installazione di hello [Power BI Core NuGut pacchetto](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Installazione del pacchetto NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Codice C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Creare un nuovo report vuoto

In ordine toocreate un nuovo report, creare hello configurazione deve essere fornita. Deve includere il token di accesso di hello, hello embedURL e datasetID hello da report hello toocreate. Ciò è necessario installare nuget hello [Power BI JavaScript pacchetto](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). embedUrl Hello sarà sufficiente https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> È possibile utilizzare hello [esempio incorporare Report di JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funzionalità. Vengono inoltre forniti esempi di codice per operazioni diverse hello disponibili.

**Installazione del pacchetto NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Codice JavaScript**

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

La chiamata *powerbi.createReport()* consente di visualizzare un canvas vuoto in modalità di modifica all'interno di hello *div* elemento.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Salvare i nuovi report

report di Hello non verrà effettivamente creato finché non si chiama hello **salvare come** operazione. A tale scopo è possibile usare il menu File o JavaScript.

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
> Un nuovo report viene creato solo dopo che è stata chiamata l'operazione **Salva con nome**. Dopo aver salvato, area di disegno hello risulterà comunque hello set di dati nel report non hello e di modalità di modifica. È necessario nuovo report di tooreload hello come se si trattasse di qualsiasi altro report.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Carico hello nuovo report

In ordine toointeract con nuovo report hello è necessario tooembed in hello allo stesso modo un'applicazione hello incorpora una relazione regolare, ovvero un nuovo token deve essere rilasciato in modo specifico per hello nuovo report e quindi chiamata hello incorporare metodo.

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Automatizzare salvataggio e caricamento di un nuovo rapporto utilizzando hello "salvato" evento

Processo dell'ordine tooautomate hello di "Salva con nome" e quindi caricare nuovo report hello è possibile rendere di hello "salvato" evento. Questo evento viene generato quando hello operazione di salvataggio è stata completata e restituisce un oggetto Json contenente valore reportId nuovo hello, nome del report, valore reportId precedente hello (se presente) e se l'operazione hello stato saveAs o salvare.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

processo hello tooAutomate può restare in ascolto sull'evento "salvato" hello, richiedere valore reportId nuovo hello, creare il nuovo token di hello e incorporare report nuovo hello con esso.

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
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

## <a name="see-also"></a>Vedere anche

[Esempio introduttivo](power-bi-embedded-get-started-sample.md)  
[Salvare i report](power-bi-embedded-save-reports.md)  
[Incorporare un report](power-bi-embedded-embed-report.md)  
[Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Esempio di incorporamento con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Pacchetto NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Pacchetto Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)
