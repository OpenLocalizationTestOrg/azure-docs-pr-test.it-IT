---
title: aaaGet avviato con un esempio
description: Power BI incorporato, utilizzare il SDK tooadd report interattivi di Power BI in un'applicazione di business intelligence
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a>Introduzione all'esempio di Power BI Embedded

**Microsoft Power BI Embedded**consente di integrare i report di Power BI direttamente nelle applicazioni Web o per dispositivi mobili. In questo articolo verranno introdotti è toohello **Power BI Embedded** get di esempio avviata.

Prima di continuare, è opportuno hello toosave seguenti risorse. Verrà consentono per l'integrazione di report di Power BI in app di esempio hello e la propria App troppo.

* [App Web di esempio per l'area di lavoro](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Riferimento all'API di Power BI Embedded](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponibile tramite NuGet)
* [Esempio per incorporare il report di JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Prima di è possibile configurare e l'esecuzione hello ottenere Power BI Embedded avvio esempio, è necessario toocreate almeno **dell'area di lavoro raccolta** nella sottoscrizione di Azure. toolearn come toocreate un **dell'area di lavoro raccolta** nel portale di Azure hello vedere [Introduzione a Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="configure-hello-sample-app"></a>Configurare l'applicazione di esempio hello

Si analizzerà l'impostazione di Visual Studio development ambiente tooaccess hello componenti necessari toorun hello esempio app.

1. Scaricare e decomprimere hello [Power BI Embedded - integrare un report in un'app web](http://go.microsoft.com/fwlink/?LinkId=761493) sample su GitHub.
2. Aprire il file **PowerBI embedded.sln** in Visual Studio. Potrebbe essere necessario hello tooexecute **pacchetto di aggiornamento** comando hello Console di gestione pacchetti NuGET in pacchetti di hello tooupdate ordine utilizzato in questa soluzione.
3. Compilare la soluzione hello.
4. Eseguire hello **ProvisionSample** applicazione console. Nell'applicazione console di esempio hello, eseguire il provisioning di un'area di lavoro e importare un file PBIX.
5. tooprovision un nuovo **dell'area di lavoro**, selezionare l'opzione 1, **gestione raccolta**, quindi selezionare l'opzione 6, **il provisioning di una nuova area di lavoro**
6. tooimport un nuovo **Report**, selezionare l'opzione 2, **Report gestione**, quindi selezionare l'opzione 3, **file di importazione PBIX Desktop in un'area di lavoro**.

7. Immettere il **nome della raccolta di aree di lavoro** e la **chiave di accesso**. È possibile ottenere questi in hello **portale Azure**. toolearn altre informazioni su come tooget il **chiave di accesso**, vedere [Visualizza chiavi di accesso API di Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Introduzione a Microsoft Power BI Embedded.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Copiare e salvare hello appena creato **ID area di lavoro** toouse più avanti in questo articolo. Dopo aver hello **ID area di lavoro** viene creato, sarà possibile trovarlo hello **portale Azure**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. del file in un file PBIX tooimport il **dell'area di lavoro**, selezionare l'opzione **6. Import PBIX Desktop file into an existing workspace**. Se non è un file PBIX file utile, è possibile scaricare hello [PBIX di esempio di analisi delle vendite al dettaglio](http://go.microsoft.com/fwlink/?LinkID=780547).
10. Se richiesto, immettere un nome descrittivo per il **set di dati**.

Verrà visualizzata una risposta simile alla seguente:

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Se il file PBIX contiene tutte le connessioni DirectQuery, eseguire le stringhe di connessione hello opzione tooupdate 7.

A questo punto il report di Power BI in formato PBIX è stato importato nell'**area di lavoro**. A questo punto, vediamo come hello toorun **Power BI Embedded** ottenere app web di esempio avviata.

## <a name="run-hello-sample-web-app"></a>Eseguire app web di esempio hello
esempio di app web Hello è un'applicazione di esempio che il rendering dei report importati i **dell'area di lavoro**. Ecco come tooconfigure hello esempio di app web.

1. In hello **incorporato PowerBI** soluzione di Visual Studio, destro, fare clic su hello **EmbedSample** applicazione web e scegliere **imposta come progetto di avvio**.
2. In **Web. config**, in hello **EmbedSample** applicazione web, modificare hello **appSettings**: **AccessKey**,  **WorkspaceCollection** nome, e **Idareadilavoro**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Eseguire hello **EmbedSample** applicazione web.

Dopo aver eseguito hello **EmbedSample** applicazione web, il pannello di navigazione a sinistra di hello deve contenere un **report** menu. report di hello tooview è stato importato, espandere **report**, fare clic su un report. Se è stata importata hello [PBIX di esempio di analisi delle vendite al dettaglio](http://go.microsoft.com/fwlink/?LinkID=780547), app web di esempio hello è analogo al seguente:

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

Dopo aver selezionato un report, hello **EmbedSample** applicazione web dovrebbe apparire questo:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Esplorare il codice di esempio hello

Hello **Microsoft Power BI Embedded** esempio è un'app web di esempio che illustra come toointegrate **Power BI** report nell'app. Model-View-Controller (MVC) usa le procedure consigliate toodemonstrate modello di progettazione. In questa sezione evidenzia le parti del codice di esempio hello che è possibile esplorare all'interno di hello **incorporato PowerBI** soluzione dell'app web. modello Model-View-Controller (MVC) Hello separa la modellazione hello di dominio di hello, presentazione hello e azioni hello basate sull'input dell'utente in tre classi separate: modello, visualizzazione e controllo. toolearn ulteriori informazioni su MVC, vedere [informazioni su ASP.NET](http://www.asp.net/mvc).

Hello **Microsoft Power BI Embedded** codice di esempio è separato come indicato di seguito. Ogni sezione include il nome di file hello nella soluzione di Power BI embedded.sln hello in modo che è possibile trovare codice hello: esempio hello.

> [!NOTE]
> In questa sezione è riportato un riepilogo hello del codice di esempio che illustra il modo in cui è stato scritto codice di hello. hello tooview completo di esempio, caricare la soluzione hello embedded.sln di Power BI in Visual Studio.

### <a name="model"></a>Modello

esempio Hello ha un **ReportsViewModel** e **ReportViewModel**.

**ReportsViewModel.cs**: rappresenta i report di Power BI.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**: rappresenta un report di Power BI.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>Stringa di connessione

stringa di connessione Hello deve essere nel seguente formato hello:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

L'uso di attributi comuni di server e database avrà esito negativo. Ad esempio: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Visualizza

Hello **vista** gestisce visualizzazione hello di Power BI **report** di Power BI e **Report**.

**Reports.cshtml**: eseguire l'iterazione su **Model.Reports** toocreate un **ActionLink**. Hello **ActionLink** è composta da come indicato di seguito:

| Parte: | Descrizione |
| --- | --- |
| Titolo |Nome del Report hello. |
| QueryString |Toohello un collegamento ID del Report. |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

Report.cshtml: Impostare hello **Model.AccessToken**, e l'espressione Lambda per hello **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Controller

**DashboardController.cs**: crea un'istanza di PowerBIClient per il passaggio di un **token dell'applicazione**. Viene generato un JSON Web Token JWT () da hello **chiave per la firma** tooget hello **credenziali**. Hello **credenziali** è toocreate utilizzata un'istanza di **PowerBIClient**. Dopo aver creato un'istanza di **PowerBIClient**, è possibile chiamare i metodi GetReports() e GetReportsAsync().

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


Task<ActionResult> Report(string reportId)

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a>Integrare un report nell'app

Dopo aver creato un **Report**, si utilizza un **IFrame** tooembed hello Power BI **Report**. Ecco un frammento di codice da powerbi.js in hello **Microsoft Power BI Embedded** esempio.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Filtrare i report incorporati nell'applicazione

È possibile filtrare un report incorporato tramite una sintassi dell'URL. toodo, si aggiunge un **$filter** con parametro della stringa di query un **eq** operatore tooyour iFrame src url con hello filtro specificato. Di seguito è riportata la sintassi di query filtro hello:

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} non può includere spazi o caratteri speciali. Hello {fieldValue} accetta un singolo valore categorico.  

## <a name="see-also"></a>Vedere anche

[Scenari comuni di Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Incorporare un report](power-bi-embedded-embed-report.md)  
[Creare un nuovo report da un set di dati](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Esempio di incorporamento con JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)
