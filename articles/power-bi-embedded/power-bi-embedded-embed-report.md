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
# <a name="embed-a-report-in-power-bi-embedded"></a>Incorporare un report in Power BI Embedded

Informazioni su come tooembed un report in Power BI incorporato nell'applicazione.

Verranno esaminati come tooactually incorporare un report nell'applicazione. Ciò presuppone che esista già un report in un'area di lavoro della raccolta di aree di lavoro. Se questo passaggio non è ancora stato completato, vedere [Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md).

È possibile usare .NET hello (c#) o Node.js SDK, insieme a JavaScript, tooeasily compilare l'applicazione con Power BI Embedded. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>Utilizzo di hello accesso chiavi toouse API REST

In hello toocall ordine API REST, è possibile passare hello tasto di scelta che è possibile ottenere da hello portale di Azure per una raccolta di area di lavoro specificato. Per altre informazioni, vedere [Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Ottenere un ID report

Ogni token di accesso è basato su un report. Sarà necessario hello tooget per report hello che si desidera tooembed l'id di report specificato. Questa operazione può essere eseguita in base alle chiamate toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) API REST. Report hello id e hello incorporare url verrà restituito. Questa operazione può essere eseguita utilizzando hello SDK .NET di Power BI o chiamare direttamente l'API REST hello.

### <a name="using-hello-power-bi-net-sdk"></a>Utilizzo di hello SDK .NET di Power BI

Quando si utilizza hello .NET SDK, sarà necessario toocreate una credenziale del token di cui è basata sulla chiave di accesso hello che si ottiene da hello portale di Azure. Ciò è necessario installare hello [pacchetto NuGet dell'API Power BI](https://www.nuget.org/profiles/powerbi).

**Installazione del pacchetto NuGet**

```
Install-Package Microsoft.PowerBI.Api
```

**Codice C#**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>Hello chiamata API REST direttamente

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

## <a name="create-an-access-token"></a>Creare un token di accesso

Power BI Embedded usa token di incorporamento, che sono token JSON Web con firma HMAC. i token Hello sono firmati con la chiave di accesso hello dalla raccolta di area di lavoro di Azure Power BI Embedded. Incorporare i token, per impostazione predefinita, vengono utilizzati tooprovide leggere accedere solo tooa report tooembed in un'applicazione. I token di incorporamento vengono rilasciati per un report specifico e dovranno essere associati a un URL di incorporamento.

I token di accesso devono essere creati nel server di hello come chiavi di accesso hello sono utilizzati toosign o crittografare i token hello. Per informazioni su come toocreate un token di accesso, vedere [autenticazione e autorizzazione a Power BI Embedded](power-bi-embedded-app-token-flow.md). È inoltre possibile rivedere hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metodo. Di seguito è riportato un esempio di questo aspetto utilizzando hello .NET SDK per Power BI.

Si utilizzerà l'id di report hello recuperato in precedenza. Una volta hello incorporare token viene creato, si utilizzerà quindi hello accesso toogenerate chiave hello token utilizzabili dalla prospettiva di hello javascript. Hello *PowerBIToken classe* richiede l'installazione di hello [Power BI Core NuGut pacchetto](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Installazione del pacchetto NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Codice C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>Aggiunta di token tooembed gli ambiti di autorizzazione

Quando si utilizza il token di incorporamento, è consigliabile toorestrict utilizzo delle risorse di hello a che si concede l'accesso. Per questo motivo, è possibile generare un token con autorizzazioni con ambito. Per altre informazioni, vedere [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ambiti).

## <a name="embed-using-javascript"></a>Incorporare con JavaScript

Dopo aver ottenuto il token di accesso di hello e id report hello, è possibile incorporare report hello utilizzando JavaScript. Ciò è necessario installare nuget hello [Power BI JavaScript pacchetto](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). embedUrl Hello sarà sufficiente https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> È possibile utilizzare hello [esempio incorporare Report di JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funzionalità. Vengono inoltre forniti esempi di codice per operazioni diverse hello disponibili.

**Installazione del pacchetto NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Codice JavaScript**

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

### <a name="set-hello-size-of-embedded-elements"></a>Impostare le dimensioni di hello elementi incorporati

report Hello verranno incorporati automaticamente in base alle dimensioni di hello del relativo contenitore. dimensioni predefinite di hello toooverride di hello incorpora semplicemente aggiungere una classe attributo o inline gli stili CSS per larghezza e altezza.

## <a name="see-also"></a>Vedere anche

[Esempio introduttivo](power-bi-embedded-get-started-sample.md)  
[Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Esempio di incorporamento con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Pacchetto Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Pacchetto NuGet Power BI API](https://www.nuget.org/profiles/powerbi)
[Pacchetto NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Repository Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Repository Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)
