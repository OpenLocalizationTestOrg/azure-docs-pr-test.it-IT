---
title: distribuzione aaaFlighting (beta test), in Azure App Service
description: "Informazioni su come tooflight nuove funzionalità nell'applicazione o beta testare gli aggiornamenti in questa esercitazione end-to-end. Questa soluzione combina le funzionalità del servizio app, come pubblicazione continua, slot, routing del traffico e l'integrazione di Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Distribuzione di versioni di anteprima (test beta) nel servizio app di Azure
In questa esercitazione illustra come toodo *anteprima distribuzioni* integrando hello varie funzionalità di [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) e [Azure Application Insights](/services/application-insights/).

*distribuzione di versioni di anteprima* è un processo che convalida una nuova funzionalità o una modifica con un numero limitato di clienti reali ed è un test importante in uno scenario di produzione. Si tratta di analogia toobeta test e viene talvolta definito come "test controllato volo". Molte aziende di grandi dimensioni con una presenza Web usano questo approccio per ottenere la convalida preventiva degli aggiornamenti di app nella proprià attività di [sviluppo Agile](https://en.wikipedia.org/wiki/Agile_software_development). Servizio App di Azure permette toointegrate test nell'ambiente di produzione con la pubblicazione continua e Application Insights tooimplement hello stesso scenario DevOps. I vantaggi di questo approccio includono:

* **Ottenere commenti e suggerimenti reale *prima* gli aggiornamenti sono rilasciati tooproduction** -hello solo vantaggio ottenere commenti e suggerimenti, non appena si rilascia sta per essere commenti e suggerimenti prima di rilasciare. È possibile testare gli aggiornamenti con traffico utente reale e i comportamenti anticipata desiderate per il ciclo di vita di hello prodotto.
* **Migliorare lo [sviluppo continuo basato su test (CTDD, Continuous test-driven development)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**: grazie all'integrazione di test nell'ambiente di produzione con l'integrazione continua e la strumentazione con Application Insights, la convalida dell'utente avviene tempestivamente e automaticamente nel ciclo di vita del prodotto. Questo approccio consente di ridurre gli investimenti in termini di tempo per l'esecuzione di test manuali.
* **Ottimizzazione del flusso di lavoro di test** -tramite l'automazione dei test nell'ambiente di produzione con la strumentazione di monitoraggio continuata, è possibile potenzialmente realizzare obiettivi hello di vari tipi di test in un unico processo, ad esempio [integrazione](https://en.wikipedia.org/wiki/Integration_testing), [regressione](https://en.wikipedia.org/wiki/Regression_testing), [usabilità](https://en.wikipedia.org/wiki/Usability_testing), accessibilità, localizzazione, [prestazioni](https://en.wikipedia.org/wiki/Software_performance_testing), [sicurezza](https://en.wikipedia.org/wiki/Security_testing), e [ accettazione](https://en.wikipedia.org/wiki/Acceptance_testing).

Una distribuzione di versioni di anteprima non riguarda semplicemente il routing del traffico live. In questo tipo di distribuzione desiderato toogain una visione più rapidamente possibile, sia che si tratti di un errore imprevisto, un calo delle prestazioni, problemi relativi all'esperienza utente. Tenere presente che si sta trattando con clienti reali. In questo caso toodo, a destra, è necessario assicurarsi che impostati il flighting toogather distribuzione tutti i dati di hello è necessario toomake una decisione consapevole per consentire il passaggio successivo. Questa esercitazione viene illustrato come dati toocollect con Application Insights, ma è possono usare New Relic o altre tecnologie che si adatta al proprio scenario.

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
In questa esercitazione si apprenderà come toobring hello seguenti tootest insieme di scenari, l'applicazione di servizio App nell'ambiente di produzione:

* [Instradare il traffico di produzione](app-service-web-test-in-production-get-start.md) tooyour beta app
* [Instrumentare l'app](../application-insights/app-insights-web-track-usage.md) tooobtain utile metriche
* Distribuire continuamente l'app beta e tenere traccia della metrica dell'app attiva
* Le metriche di confronto tra app di produzione hello e hello beta app toosee come codice cambia traducono tooresults

## <a name="what-you-will-need"></a>Prerequisiti
* Un account Azure
* Un account [GitHub](https://github.com/)
* Visual Studio 2015 - è possibile scaricare hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* GIT Shell (installato con [GitHub per Windows](https://windows.github.com/))-in questo modo si toorun entrambi i comandi Git e PowerShell di hello in hello stessa sessione
* Ultimi bit di [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi)
* Conoscenza di base seguenti hello:
  * Distribuzione di modelli di [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md); vedere [Distribuire un'applicazione complessa in modo prevedibile in Azure](app-service-deploy-complex-application-predictably.md)
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> È necessario un account di Azure di toocomplete questa esercitazione:
>
> * È possibile [aprire un account Azure, gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -si ottiene crediti è possibile utilizzare tootry out a pagamento di servizi di Azure e anche dopo che consentono è possibile tenere conto di hello e libero di utilizzare servizi di Azure, ad esempio le applicazioni Web.
> * È possibile [attivare i benefici della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): con la sottoscrizione Visual Studio ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.
>
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
>
>

## <a name="set-up-your-production-web-app"></a>Configurare l'app Web di produzione
> [!NOTE]
> script Hello utilizzato in questa esercitazione verranno configurate automaticamente la pubblicazione continua dall'archivio GitHub. È necessario che le credenziali per GitHub già archiviate in Azure, in caso contrario la distribuzione di hello inserito nello script non riuscirà quando si tenta di impostazioni di controllo tooconfigure origine per le app web hello.
>
> toostore il GitHub credenziali in Azure, creare un'app web in hello [portale Azure](https://portal.azure.com/) e [configurare la distribuzione di GitHub](app-service-continuous-deployment.md). È necessario solo toodo questo volta.
>
>

In uno scenario tipico DevOps, si dispone di un'applicazione che è in esecuzione in tempo reale in Azure e si desidera toomake modifiche tooit tramite la pubblicazione continua. In questo scenario, si distribuirà tooproduction un modello che sono stati sviluppati e testati.

1. Creare il propria fork di hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository. Per informazioni sulla creazione della biforcazione, vedere la pagina relativa alla [biforcazione di un repository](https://help.github.com/articles/fork-a-repo/). Una volta creata la biforcazione, è possibile visualizzarla nel browser.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Aprire una sessione di Git Shell. Se non si ha ancora Git Shell, installare [GitHub per Windows](https://windows.github.com/) .
3. Creare un clone locale nel fork eseguendo hello comando seguente:

     git clone https://github.com/<fork>/ToDoApp.git
4. Dopo aver creato il clone locale, passare troppo*&lt;repository_root >*\ARMTemplates e hello esecuzione deploy.ps1 script con un suffisso univoco, come mostrato di seguito:

     .\deploy.ps1 –RepoUrl https://github.com/<fork>/todoapp.git -ResourceGroupSuffix <suffisso_personalizzato>
5. Quando richiesto, digitare nome utente hello desiderato e la password per l'accesso al database. Memorizza le credenziali del database poiché è necessario toospecify usarle nuovamente quando l'aggiornamento hello gruppo di risorse.

   Dovrebbe essere hello provisioning lo stato di avanzamento delle varie risorse di Azure. Al termine del processo di distribuzione, script hello avviare un'applicazione hello nel browser hello e offrono un segnale acustico descrittivo.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Tornare alla sessione di Git Shell ed eseguire:

     .\swap –Name ToDoApp<suffisso_personalizzato>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Al termine dell'esecuzione dello script hello, tornare indietro indirizzo del toobrowse toohello server front-end (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee un'applicazione hello in esecuzione nell'ambiente di produzione.
8. Accedere al hello [portale Azure](https://portal.azure.com/) e diamo un'occhiata a ciò che viene creato.

   Dovrebbe essere in grado di toosee due web App in hello stesso gruppo di risorse, uno con hello `Api` suffisso nel nome hello. Se si osserva visualizzazione gruppo risorse di hello, si verifica anche hello Database SQL e server, hello piano di servizio App e slot di gestione temporanea hello per le app web hello. Esplorare le diverse risorse hello e confrontarle con  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json modo in cui sono configurati nel modello di hello.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Impostare hello dell'applicazione di produzione.  A questo punto, si supponga di ricevere commenti e suggerimenti che non sono soddisfacenti per app hello usabilità. Pertanto, si decide di tooinvestigate. Si userà tooinstrument toogive l'app è commenti e suggerimenti.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Procedere all'approfondimento: instrumentare l'app client per il monitoraggio e la metrica
1. Aprire *&lt;radice_repository >*\src\MultiChannelToDo.sln in Visual Studio.
2. Ripristinare tutti i pacchetti Nuget facendo clic con il pulsante destro del mouse sulla soluzione > **Gestisci pacchetti NuGet per la soluzione** > **Ripristina**.
3. Fare doppio clic su **MultiChannelToDo.Web** > **Aggiungi Application Insights Telemetry** > **Configura impostazioni** > Modifica gruppo di risorse tooToDoApp*&lt;your_suffix >* > **Aggiungi Application Insights tooProject**.
4. Nel portale di Azure hello, aprire Pannello hello hello **MultiChannelToDo.Web** risorsa di Application Insights. Quindi in hello **integrità applicazione** parte, fare clic su **informazioni su come caricare i dati toocollect pagina nel browser** > Copia codice.
5. Aggiungere hello copiata il codice strumentazione JS troppo*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, appena prima della chiusura hello `<heading>` tag. Deve contenere una chiave di strumentazione univoco hello della risorsa di Application Insights.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Invia eventi personalizzati tooApplication informazioni dettagliate per i clic del mouse aggiungendo hello inferiore toohello codice del corpo seguente:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Questo frammento di codice JavaScript invia tooApplication un evento personalizzato Insights ogni volta che un utente fa clic in un punto qualsiasi nell'app web hello.
7. Nella Shell di Git, eseguire il commit e push nel fork tooyour modifiche in GitHub. Attendere quindi browser toorefresh client.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Scambiare hello distribuito app modifiche tooproduction:

     .\swap –Name ToDoApp<suffisso_personalizzato>
9. Sfoglia risorsa di Application Insights toohello configurato. Fare clic su Eventi personalizzati.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Se non viene visualizzata la metrica per gli eventi personalizzati, attendere alcuni minuti e fare clic su **Aggiorna**.

Si supponga di visualizzare un grafico come il seguente:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

E griglia di eventi hello sotto di essa:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

In base tooyour ToDoApp codice dell'applicazione, hello **pulsante** evento corrisponde pulsante Invia toohello e hello **INPUT** evento corrisponde toohello casella di testo. Fino a questo punto, è tutto chiaro. Tuttavia, sembra che è una discreta quantità di clic e pochi clic sugli elementi di attività da eseguire hello (hello **LI** eventi).

Basato su, questo modulo è l'ipotesi che alcuni utenti sono confusi quale parte della hello dell'interfaccia utente è selezionabili ed è perché cursore hello è concepito per la selezione di testo quando viene posizionato in voci di elenco hello e le icone.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Potrebbe trattarsi di un esempio improbabile. Tuttavia, è corso toomake un'app tooyour analisi utilizzo software e quindi eseguire un commenti e suggerimenti di flighting distribuzione tooget usabilità dei clienti in tempo reale.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Instrumentare l'app server per il monitoraggio e la metrica
Si tratta di una tangente poiché scenario hello illustrato in questa esercitazione sono disponibili solo app client hello. Tuttavia, per motivi di completezza imposterà hello sul lato server app.

1. Fare doppio clic su **MultiChannelToDo** > **Aggiungi Application Insights Telemetry** > **Configura impostazioni** > Modifica gruppo di risorse tooToDoApp*&lt;your_suffix >* > **Aggiungi Application Insights tooProject**.
2. Nella Shell di Git, eseguire il commit e push nel fork tooyour modifiche in GitHub. Attendere quindi browser toorefresh client.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Scambiare hello distribuito app modifiche tooproduction:

     .\swap –Name ToDoApp<suffisso_personalizzato>

L'operazione è terminata.

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Provare a utilizzare: Aggiungere metriche di app client tooyour tag specifici dello slot
In questa sezione, si configurerà hello distribuzione diversi slot toosend specifici dello slot telemetria toohello stessa risorsa di Application Insights. In questo modo, è possibile confrontare dati di telemetria dei dati tra il traffico proveniente da tooeasily slot diversi (ambienti di distribuzione), vedere effetto hello delle modifiche alle app. AT hello stesso tempo, è possibile separare il traffico di produzione di hello dal resto hello in modo è possibile continuare toomonitor l'app di produzione in base alle esigenze.

Poiché si sta la raccolta dei dati sul comportamento del client, avrà [un tooyour inizializzatore telemetria codice JavaScript aggiungere](../application-insights/app-insights-api-filtering-sampling.md) in cshtml. Se si desidera tootest prestazioni sul lato server, ad esempio, è possibile anche eseguire in modo analogo nel codice server (vedere [Application Insights API per gli eventi personalizzati e le metriche](../application-insights/app-insights-api-custom-events-metrics.md).

1. Aggiungere innanzitutto hello bewteen tramite codice hello due `//` commenti sotto blocco JavaScript hello aggiunto toohello `<heading>` tag in precedenza.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Questo codice inizializzatore causa hello `appInsights` tooadd oggetto hello una proprietà personalizzata denominata `Environment` tooevery pezzo di dati di telemetria Invia.
2. Aggiungere quindi questa proprietà personalizzata come [impostazione dello slot](web-sites-staged-publishing.md#AboutConfiguration) per l'app Web in Azure. toodo, hello esecuzione seguendo i comandi nella sessione della Shell di Git.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Hello Web. config nel progetto definisce già hello `environment` impostazione dell'app. Con questa impostazione, durante il test in locale, l'applicazione hello le metriche verranno contrassegnate con `VS Debugger`. Tuttavia, quando si esegue il push tooAzure le modifiche, Azure verrà trovare e utilizzare hello `environment` verranno contrassegnato con l'impostazione nella configurazione dell'applicazione web hello invece app e le metriche `Production`.
3. Eseguire il commit e push nel fork tooyour modifiche di codice su GitHub e quindi attendere che gli utenti toouse hello nuova app (necessità toorefresh hello browser). Occupa circa 15 minuti per hello nuova proprietà tooshow nell'Application Insights `MultiChannelToDo.Web` risorse.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. A questo punto, passare toohello **eventi personalizzati** pannello nuovamente e filtro hello metriche in `Environment=Production`. Dovrebbe ora essere in grado di toosee tutti hello nuovo gli eventi personalizzati nell'ambiente di produzione hello slot con questo filtro.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Fare clic su hello **Preferiti** come pulsante toosave hello corrente Esplora metriche impostazioni toosomething **eventi personalizzati: produzione**. È possibile passare facilmente tra questa visualizzazione e una visualizzazione dello slot di distribuzione in un secondo momento.

   > [!TIP]
   > Per analisi ancora più avanzate, prendere in considerazione l' [l'integrazione della risorsa di Application Insights con Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Aggiungere tag specifici dello slot tooyour server app metriche
Nuovamente, per motivi di completezza si imposterà hello sul lato server app. A differenza di app client hello è instrumentato in JavaScript, il tag di slot specifici per l'app server hello è instrumentato con codice .NET.

1. Aprire *&lt;radice_repository >*\src\MultiChannelToDo\Global.asax.cs. Aggiungere hello un blocco di codice seguente, appena prima hello dello spazio dei nomi tra parentesi graffe.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Correggere gli errori di risoluzione nome hello aggiungendo hello `using` istruzioni sotto toohello inizio del file hello:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Aggiungere codice hello sotto toohello inizio hello `Application_Start()` metodo:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Eseguire il commit e push nel fork tooyour modifiche di codice su GitHub e quindi attendere che gli utenti toouse hello nuova app (necessità toorefresh hello browser). Occupa circa 15 minuti per hello nuova proprietà tooshow nell'Application Insights `MultiChannelToDo` risorse.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Procedere all'aggiornamento: configurare il ramo beta
1. Aprire  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json e individuare hello `appsettings` risorse (cercare `"name": "appsettings"`). Ne sono disponibili 4, una per ogni slot.
2. Per ogni `appsettings` risorse, aggiungere un `"environment": "[parameters('slotName')]"` app impostazione toohello fine hello `properties` matrice. Non dimenticare di riga precedente di hello tooend con una virgola.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Si è appena aggiunto hello `environment` app impostazione tooall slot hello nel modello di hello.
3. In hello stesso file, trovare hello `slotconfignames` risorse (cercare `"name": "slotconfignames"`). Ne sono disponibili 2, una per ogni app.
4. Per ogni `slotconfignames` risorse, aggiungere `"environment"` toohello fine hello `appSettingNames` matrice. Non dimenticare di riga precedente di hello tooend con una virgola.

    Sono state apportate hello `environment` app impostazione stick tooits rispettivi slot di distribuzione per entrambe le app.  
5. Nella sessione di Git Shell hello eseguire comandi che seguono con hello stesso suffisso di gruppo di risorse usato in precedenza.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Quando richiesto, specificare hello stesse credenziali di database SQL come prima. Quindi, quando richiesto tooupdate hello gruppo di risorse tipo `Y`, quindi `ENTER`.

    Una volta al termine dello script hello, tutte le risorse nel gruppo di risorse hello originale vengono mantenute, ma un nuovo slot denominato "beta" è stato creato con hello stesso configurazione come slot di "Gestione temporanea" hello creato in inizio hello.

   > [!NOTE]
   > Questo metodo di creazione di diversi ambienti di distribuzione è diverso dal metodo hello in [sviluppo Agile di software con il servizio App di Azure](app-service-agile-software-development.md). Con questo metodo si creano ambienti di distribuzione con slot di distribuzione, mentre con l'altro si creano ambienti di distribuzione con gruppi di risorse. La gestione di ambienti di distribuzione con gruppi di risorse consente toodevelopers ambiente di produzione hello tookeep off-limits, ma non è facile toodo test nell'ambiente di produzione, è possibile eseguire facilmente con gli slot.
   >
   >

Se necessario, è anche possibile creare un'app alfa con il codice seguente

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Per questa esercitazione si continuerà a usare l'app beta.

## <a name="update-push-your-updates-toohello-beta-app"></a>Aggiornamento: Push app aggiornamenti toohello beta
Eseguire il backup tooyour app che si desidera tooimprove.

1. Verificare di trovarsi nel ramo beta

        git checkout beta
2. In  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, hello trova `<li>` tag e aggiungere hello `style="cursor:pointer"` attributo, come illustrato di seguito.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. eseguire il commit e push tooAzure.
4. Verificare che la modifica hello viene ora rispecchiata nello slot beta hello passando toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Se non viene visualizzato hello modificare ancora, aggiornare il codice di javascript nuovo browser tooget hello.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Dopo aver creato la modifica in esecuzione nello slot di hello beta, si è pronti tooperform una distribuzione flighting.

## <a name="validate-route-traffic-toohello-beta-app"></a>Convalida: Route traffico toohello app beta
In questa sezione, si indirizza il traffico toohello beta app. Ai fini del, semplicità della dimostrazione, si userà una parte significativa dei hello utente traffico tooit tooroute. In realtà, hello quantità di traffico che si desidera tooroute dipenderanno dalla situazione specifica. Ad esempio, se il sito è su larga scala hello Microsoft.com, si potrebbe essere minore di 1% del traffico totale in dati utili toogain di ordine.

1. Nella sessione della Git Shell, eseguire hello seguenti comandi tooroute metà dello slot di hello produzione traffico toohello beta:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Hello `ReroutePercentage=50` proprietà specifica che 50% di traffico di produzione hello sarà l'URL dell'app toohello indirizzato beta (specificato da hello `ActionHostName` proprietà).
2. Passare ora toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50% di traffico hello dovrebbe ora essere slot beta toohello reindirizzato.
3. Nella risorsa di Application Insights, filtrare le metriche hello dall'ambiente = "beta".

   > [!NOTE]
   > Se si salva questa visualizzazione filtrata come preferito di un'altra, è possibile scorrere facilmente viste di Esplora metriche hello tra produzione e le viste beta.
   >
   >

Si supponga che in Application Insights viene visualizzato un codice simile toohello seguenti:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Non solo è questa visualizzazione sono presenti molti più clic su hello `<li>` tag, ma ci toobe un aumento del mouse su `<li>` tag. È quindi possibile concludere che gli utenti sono individuati hello nuovo `<li>` i tag sono selezionabili e sta ora cancellando tutte le attività già completati nell'app hello.

In base ai dati di hello della distribuzione flighting, si può decidere che la nuova interfaccia utente è pronto per la produzione.

## <a name="go-live-move-your-new-code-into-production"></a>Passare alla fase operativa: spostare di nuovo codice nell'ambiente di produzione
Si è ora pronto toomove tooproduction l'aggiornamento. Che cos'è ideale è che ora si è certi che l'aggiornamento è già stato convalidato *prima* esso viene inserito tooproduction. A questo punto è possibile distribuirlo. Poiché è stata effettuata un'app client di aggiornamento toohello AngularJS, codice lato client hello convalidati solo. Se si toomake modifiche toohello back-end Web app per le API, è possibile convalidare le modifiche allo stesso modo semplice e rapido.

1. Nella Shell di Git, rimuovere regola di routing del traffico hello eseguendo hello comando seguente:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Eseguire i comandi Git hello:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Attendere alcuni minuti per hello nuovo codice toohello toobe distribuito nello slot di gestione temporanea, quindi avviare http://ToDoApp*&lt;your_suffix >*-tooverify staging.azurewebsites.net che hello nuovo aggiornamento è stato riscaldato in gestione temporanea hello slot. Tenere presente che hello ramo master di divisione è collegato a gestione temporanea toohello slot dell'app.
4. Ora, scambio hello slot di gestione temporanea nell'ambiente di produzione

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Riepilogo
Servizio App di Azure semplifica per le aziende toomedium-piccola tootest delle App per i clienti nell'ambiente di produzione, che in genere eseguito in grandi aziende. Probabilmente questa esercitazione è state ricevute hello conoscenze necessarie toobring insieme Application Insights e servizio App toomake possibili anteprima scenari di distribuzione e anche altri test in produzione, il mondo DevOps.

## <a name="more-resources"></a>Altre risorse
* [Agile Software Development con il servizio app di Azure](app-service-agile-software-development.md)
* [Configurare ambienti di staging per le app Web nel servizio app di Azure](web-sites-staged-publishing.md)
* [Distribuire un'applicazione complessa in modo prevedibile in Azure](app-service-deploy-complex-application-predictably.md)
* [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello Validator JSON](http://jsonlint.com/)
* [Diramazione Git - Diramazione e unione di base](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Wiki del progetto Kudu](https://github.com/projectkudu/kudu/wiki)
