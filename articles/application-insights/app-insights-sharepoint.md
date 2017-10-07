---
title: aaaMonitor un sito di SharePoint con Application Insights
description: Avviare il monitoraggio di una nuova applicazione con una nuova chiave di strumentazione
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Monitorare un sito di SharePoint con Application Insights
Azure Application Insights consente di monitorare la disponibilità di hello, prestazioni e utilizzo delle applicazioni. Questo articolo si apprenderà come tooset è per un sito di SharePoint.

## <a name="create-an-application-insights-resource"></a>Creare una risorsa Application Insights
In hello [portale di Azure](https://portal.azure.com), creare una nuova risorsa di Application Insights. Scegliere ASP.NET come tipo di applicazione hello.

![Fare clic su proprietà, selezionare la chiave hello e premere ctrl + C](./media/app-insights-sharepoint/01-new.png)

Pannello Hello visualizzato è il luogo di hello dove verrà visualizzato i dati di utilizzo e prestazioni sull'app. tooit indietro tooget successivo che accesso tooAzure, è necessario trovare un riquadro per tale nella schermata iniziale di hello. In alternativa fare clic su Sfoglia toofind è.

## <a name="add-our-script-tooyour-web-pages"></a>Aggiungere le pagine web tooyour di script
Durante l'avvio rapido, ottenere script hello per le pagine web:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Inserire uno script di hello prima hello &lt;/head&gt; tag di ogni pagina desiderata tootrack. Se il sito Web dispone di una pagina master, è possibile inserire script hello non esiste. Ad esempio, in un progetto ASP.NET MVC inserire lo script in View\Shared\_Layout.cshtml.

script Hello contiene una chiave di strumentazione hello che indirizza una risorsa di Application Insights tooyour telemetria hello.

### <a name="add-hello-code-tooyour-site-pages"></a>Aggiungere pagine del sito di hello codice tooyour
#### <a name="on-hello-master-page"></a>Nella pagina master hello
Se è possibile modificare una pagina master hello del sito, che fornirà il monitoraggio per ogni pagina del sito hello.

Vedere la pagina master hello e modificarlo utilizzando SharePoint Designer o un altro editor.

![](./media/app-insights-sharepoint/03-master.png)

Aggiungere codice hello prima hello </head> tag. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>oppure nelle singole pagine
toomonitor un set limitato di pagine, aggiungere uno script di hello separatamente tooeach pagina. 

Inserire una web part e incorporare il frammento di codice hello in essa contenuti.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Visualizza i dati sull'app
Ridistribuire l'app.

Pannello applicazione tooyour restituito in hello [portale di Azure](https://portal.azure.com).

gli eventi prima di Hello vengono visualizzati nella ricerca. 

![](./media/app-insights-sharepoint/09-search.png)

Se si prevedono più dati, fare clic su Aggiorna dopo pochi secondi.

Dal pannello della panoramica hello, fare clic su **analitica utilizzo** toocharts toosee di utenti, sessioni e le visualizzazioni di pagina:

![](./media/app-insights-sharepoint/06-usage.png)

Fare clic su qualsiasi toosee grafico ulteriori dettagli, ad esempio le visualizzazioni di pagina:

![](./media/app-insights-sharepoint/07-pages.png)

Oppure gli utenti:

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Acquisizione dell'ID utente
frammento di codice Hello pagina web standard non acquisisce l'id utente hello da SharePoint, ma è possibile farlo con una piccola modifica.

1. Copiare la chiave di strumentazione dell'applicazione hello Essentials elenco a discesa in Application Insights. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Sostituire con la chiave di strumentazione hello "XXXX" nel seguente frammento di hello. 
2. Incorporare script hello nell'applicazione SharePoint anziché frammento hello che si ottiene dal portale hello.

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a>Passaggi successivi
* [Test Web](app-insights-monitor-web-app-availability.md) disponibilità hello toomonitor del sito.
* [Application Insights](app-insights-overview.md) per altri tipi di app.

<!--Link references-->


