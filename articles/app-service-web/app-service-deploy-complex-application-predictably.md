---
title: aaaProvision e distribuire microservizi in modo prevedibile in Azure
description: "Informazioni su come toodeploy un'applicazione è costituito da microservizi nel servizio App di Azure come unità singola e prevedibile utilizzando modelli di gruppo di risorse JSON e script di PowerShell."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Effettuare il provisioning di microservizi e distribuirli in modo prevedibile in Azure
Questa esercitazione viene illustrato come tooprovision e distribuire un'applicazione composta da [microservizi](https://en.wikipedia.org/wiki/Microservices) in [Azure App Service](/services/app-service/) come unità singola e prevedibile utilizzando modelli di gruppo di risorse JSON e Creazione di script di PowerShell. 

Quando il provisioning e la distribuzione di applicazioni a scalabilità elevata che sono composti di microservizi estremamente separata, ripetibilità e la prevedibilità sono toosuccess fondamentale. [Servizio App di Azure](/services/app-service/) consente microservizi toocreate che includono le app web, App mobile, App per le API e App per la logica. [Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) consente si toomanage microservizi hello tutti come un'unità, insieme alle dipendenze delle risorse, ad esempio impostazioni di controllo di origine e del database. A questo punto è possibile distribuire l'applicazione usando modelli JSON e semplici script di PowerShell. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Nell'esercitazione di hello, distribuire un'applicazione che comprende:

* Due app Web (ovvero due microservizi)
* Un database SQL di back-end
* Impostazioni dell'app, stringhe di connessione e controllo del codice sorgente
* Application Insights, avvisi, impostazioni di scalabilità automatica

## <a name="tools-you-will-use"></a>Strumenti da usare
In questa esercitazione si utilizzerà hello gli strumenti seguenti. Poiché non si tratta di informazioni complete sugli strumenti, si verrà scenario end-to-end di toostick toohello e fornirle tooeach una breve introduzione, e in cui è possibile trovare ulteriori informazioni su di esso. 

### <a name="azure-resource-manager-templates-json"></a>Modelli di Gestione risorse di Azure (JSON)
Ogni volta che si crea un'app web in Azure App Service, ad esempio, Gestione risorse di Azure Usa un gruppo JSON modello toocreate hello intera risorsa con le risorse del componente hello. Un modello complesso da hello [Azure Marketplace](/marketplace) come hello [WordPress scalabile](/marketplace/partners/wordpress/scalablewordpress/) app può includere database MySQL hello, gli account di archiviazione, hello piano di servizio App, hello web app stessa, le regole di avviso, app impostazioni, le impostazioni di scalabilità automatica e altre e tutti questi modelli sono disponibili tooyou tramite PowerShell. Per informazioni su come toodownload e utilizzare tali modelli, vedere [tramite Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

Per ulteriori informazioni sui modelli di hello Azure Resource Manager, vedere [la creazione di modelli di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>Azure SDK 2.6 per Visual Studio
Hello SDK più recenti contiene miglioramenti toohello il supporto del modello di gestione delle risorse nell'editor di JSON hello. È possibile utilizzare questo tooquickly creare un modello di gruppo di risorse da zero o aprire un modello JSON esistente (ad esempio, un modello di raccolta scaricato) per la modifica, compilare i file dei parametri hello e distribuire anche il gruppo di risorse hello direttamente da di Azure Soluzione di gruppo di risorse.

Per altre informazioni, vedere [Azure SDK 2.6 per Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).

### <a name="azure-powershell-080-or-later"></a>Azure PowerShell 0.8.0 o versione successiva
A partire dalla versione 0.8.0, hello Azure PowerShell installazione include il modulo di gestione risorse di Azure hello in aggiunta toohello modulo di Azure. Questo nuovo modulo consente la distribuzione di hello tooscript di gruppi di risorse.

Per altre informazioni, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Esplora risorse di Azure
Questo [strumento anteprima](https://resources.azure.com) consente le definizioni di tooexplore hello JSON di tutti i gruppi di risorse hello le singole risorse hello e di sottoscrizione. Nello strumento di hello, è possibile modificare le definizioni di hello JSON di una risorsa, eliminare un'intera gerarchia di risorse e creare nuove risorse.  informazioni di Hello immediatamente disponibili in questo strumento sono molto utile per la creazione di un modello quanto mostra ciò che occorre tooset per un particolare tipo di risorsa, hello proprietà correggere i valori e così via. È anche possibile creare il gruppo di risorse in hello [portale Azure](https://portal.azure.com/), quindi controllare le relative definizioni JSON in hello Esplora strumento toohelp creare un template da gruppo di risorse hello.

### <a name="deploy-tooazure-button"></a>Pulsante tooAzure di distribuzione
Se si utilizzano GitHub per controllo del codice sorgente, è possibile inserire un [pulsante tooAzure Distribuisci](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) nel file Leggimi. MD, che consente un tooAzure dell'interfaccia utente di distribuzione di chiavi in mano. Mentre è possibile farlo per qualsiasi applicazione web semplice, è possibile estendere questo tooenable la distribuzione di un intero gruppo di risorse mediante l'inserimento di un file azuredeploy.json nella radice del repository hello. Questo file JSON, che contiene il modello di gruppo di hello risorse, verrà utilizzato dal gruppo di risorse di hello Distribuisci tooAzure pulsante toocreate hello. Per un esempio, vedere hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) esempio, che verrà utilizzato in questa esercitazione.

## <a name="get-hello-sample-resource-group-template"></a>Modello di gruppo di risorse di esempio hello ottenere
Ora entriamo tooit destra.

1. Passare toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) esempio di servizio App.
2. Nel file readme.md, fare clic su **distribuire tooAzure**.
3. Si è eseguito toohello [distribuire in azure](https://deploy.azure.com) del sito e i parametri della distribuzione tooinput frequenti. Si noti che la maggior parte dei campi hello sono popolata con il nome di repository hello e alcune stringhe casuali. Se si desidera, ma ciò hello è tooenter accesso amministrativo di SQL Server hello e una password di hello, quindi fare clic su, è possibile modificare tutti i campi di hello **Avanti**.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. Successivamente, fare clic su **Distribuisci** toostart processo di distribuzione hello. Dopo l'esecuzione del processo di hello toocompletion, fare clic su hello http://todoapp*XXXX*. hello toobrowse di collegamento azurewebsites.net applicazione distribuita. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   Hello dell'interfaccia utente potrebbe essere leggermente più lenta quando si Sfoglia innanzitutto tooit hello App appena avvio, poiché convincere manualmente che si tratta di un'applicazione completamente funzionale.
5. Nella pagina distribuzione hello, fare clic su hello **Gestisci** collegare la nuova applicazione hello toosee nel portale di Azure hello.
6. In hello **Essentials** elenco a discesa, fare clic sul collegamento di gruppo di risorse hello. Si noti inoltre che app web hello è già connesso repository GitHub toohello in **progetto esterno**. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. Nel Pannello di gruppo di risorse hello, si noti che esistono già due App web e un Database SQL nel gruppo di risorse hello.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

Tutto ciò che si è visto solo in pochi minuti breve è un'applicazione di due-microservizio completamente distribuito, con tutti i componenti di hello, dipendenze, le impostazioni, database e la pubblicazione continua, impostare da un'orchestrazione automatizzata in Gestione risorse di Azure. Tutte le operazioni sono state eseguite da due elementi:

* pulsante di Hello Distribuisci tooAzure
* azuredeploy.JSON nella radice del repository hello

È possibile distribuire l'applicazione stessa decine, centinaia o migliaia di volte e hello utilizzare la stessa configurazione ogni volta. la prevedibilità ripetibilità e hello Hello di questo approccio consente applicazioni a scalabilità elevata toodeploy con maggiore facilità e affidabilità.

## <a name="examine-or-edit-azuredeployjson"></a>Esaminare (o modificare) AZUREDEPLOY.JSON
Ora esaminiamo come repository di GitHub hello è stato impostato. Si utilizzerà editor JSON hello in hello Azure .NET SDK, pertanto se è stato ancora installato [Azure .NET SDK 2.6](/downloads/), farlo ora.

1. Hello clone [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository utilizzando lo strumento preferito git. Nella schermata di hello riportata di seguito, questa scelta in Team Explorer in Visual Studio 2013 hello.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. Dalla radice del repository hello, aprire azuredeploy.json in Visual Studio. Se non viene visualizzato il riquadro di struttura JSON hello, è necessario tooinstall Azure .NET SDK.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

È consapevole di non passare toodescribe ogni dettaglio del formato JSON hello ma hello [più risorse](#resources) sezione vengono forniti i collegamenti per l'apprendimento di linguaggio del modello gruppo di risorse hello. In questo caso, faccio clic tooshow hello interessanti funzionalità che consentono di iniziare a rendere il proprio modello personalizzato per la distribuzione di app.

### <a name="parameters"></a>parameters
Esaminiamo hello parametri sezione toosee che molti di questi parametri sono quali hello **distribuire tooAzure** pulsante richiede tooinput. sito Hello dietro hello **distribuire tooAzure** pulsante Popola hello input dell'interfaccia utente utilizzando i parametri di hello definiti nel azuredeploy.json. Questi parametri sono utilizzati in definizioni di risorse hello, ad esempio i nomi delle risorse, i valori delle proprietà e così via.

### <a name="resources"></a>Risorse
Nel nodo risorse hello, si noterà che le risorse di primo livello 4 vengono definite, tra cui un'istanza di SQL Server, un piano di servizio App e due le app web. 

#### <a name="app-service-plan"></a>Piano di servizio app
Iniziamo con una risorsa a livello di radice semplice in hello JSON. Selezionare il piano di servizio App hello denominato hello struttura JSON, **[hostingPlanName]** toohighlight hello codice JSON corrispondente. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

Si noti che hello `type` elemento specifica la stringa hello per un piano di servizio App (è stata chiamata una server farm fa volta long, long) e altri elementi e le proprietà vengono compilate utilizzando parametri hello definiti nel file JSON hello e non dispone di questa risorsa le risorse annidate.

> [!NOTE]
> Si noti inoltre il valore di hello di `apiVersion` indica quale versione di definizione di risorsa JSON per la hello toouse hello API REST con e può influire sulle modalità di formattazione all'interno di hello risorse hello Azure `{}`. 
> 
> 

#### <a name="sql-server"></a>SQL Server
Successivamente, fare clic sulla risorsa di SQL Server hello denominata **SQLServer** in hello struttura JSON.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

Hello nota seguente su hello evidenziato codice JSON:

* utilizzo di Hello dei parametri assicura che siano denominate risorse hello creato e configurate in modo che li rende più coerenti tra loro.
* Hello risorse di SQL Server ha due risorse annidate, ognuno ha un valore diverso per `type`.
* Hello annidati risorse all'interno di `“resources”: […]`, in cui sono definite database hello e regole del firewall hello, hanno un `dependsOn` elemento che specifica l'ID della risorsa di SQL Server a livello di radice di hello risorsa hello. In questo modo Azure Resource Manager, "prima di creare la risorsa, che deve essere già presente un'altra risorsa; e, se tale altra risorsa è definita nel modello di hello, quindi creare che uno prima di tutto".
  
  > [!NOTE]
  > Per informazioni dettagliate su come hello toouse `resourceId()` funzione, vedere [funzioni di modello di gestione risorse di Azure](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).
  > 
  > 
* effetto di hello Hello `dependsOn` elemento è di che Gestione risorse di Azure può sapere quali risorse possono essere create in parallelo e quali risorse devono essere create in sequenza. 

#### <a name="web-app"></a>App Web
A questo punto, passiamo toohello effettivo App web, che sono più complesse. Fare clic su app web hello [variables('apiSiteName')] in hello struttura JSON toohighlight il codice JSON. Come si noterà, diventa tutto molto più interessante. A tale scopo, parlerò funzionalità hello uno alla volta:

##### <a name="root-resource"></a>Risorsa radice
app web Hello dipende da due diverse risorse. Ciò significa che Gestione risorse di Azure consente di creare app web hello solo dopo che entrambi hello piano di servizio App e hello istanza di SQL Server vengono creati.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>Impostazioni app
le impostazioni dell'app Hello sono anche definite come una risorsa annidata.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

In hello `properties` elemento per `config/appsettings`, si dispone di due impostazioni di app in formato hello `“<name>” : “<value>”`.

* `PROJECT`è un [impostazione KUDU](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) distribuzione di Azure che indica quale toouse progetto in una soluzione di Visual Studio multiprogetto. Visualizzerà in un secondo momento come controllo del codice sorgente è configurato, ma poiché hello ToDoApp codice si trova in una soluzione di Visual Studio più progetti, è necessario che questa impostazione.
* `clientUrl`è semplicemente un'app di cui l'impostazione di tale codice dell'applicazione hello Usa.

##### <a name="connection-strings"></a>Stringhe di connessione
le stringhe di connessione Hello sono anche definite come una risorsa annidata.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

In hello `properties` elemento per `config/connectionstrings`, ogni stringa di connessione è definita come una coppia nome-valore, con formato specifico di hello di `“<name>” : {“value”: “…”, “type”: “…”}`. Per hello `type` elemento, i valori possibili sono `MySql`, `SQLServer`, `SQLAzure`, e `Custom`.

> [!TIP]
> Per un elenco dei tipi di stringa di connessione hello definitivo, eseguire hello comando in Azure PowerShell seguente: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>Controllo del codice sorgente
le impostazioni di codice sorgente Hello sono anche definite come una risorsa annidata. Gestione risorse di Azure Usa questa risorsa tooconfigure continua la pubblicazione (vedere però `IsManualIntegration` in un secondo momento) e anche tookick la distribuzione di hello del codice dell'applicazione automaticamente durante l'elaborazione di hello del file JSON hello.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`e `branch` deve essere molto intuitivo e deve puntare toohello Git repository e hello il nome di hello ramo toopublish da. Anche in questo caso, sono definite dai parametri di input. 

Nota in hello `dependsOn` elemento che, in aggiunta toohello web risorsa app stessa, `sourcecontrols/web` dipende anche dalla `config/appsettings` e `config/connectionstrings`. Infatti, una volta `sourcecontrols/web` è configurato, il processo di distribuzione di Azure hello tenterà automaticamente toodeploy, compilare e avviare il codice dell'applicazione hello. Pertanto, inserimento consente questa dipendenza è assicurarsi che tale applicazione hello con accesso toohello necessarie app impostazioni e le stringhe di connessione prima di eseguita il codice dell'applicazione hello. 

> [!NOTE]
> Si noti inoltre che `IsManualIntegration` è troppo`true`. Questa proprietà è necessaria in questa esercitazione perché non sono effettivamente proprietari repository GitHub hello e pertanto non è effettivamente concedere autorizzazioni tooAzure tooconfigure la pubblicazione continua da [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (ad esempio push automatico repository aggiornato tooAzure). È possibile utilizzare il valore di predefinito hello `false` per il repository specificato di hello solo se è stato configurato credenziali per GitHub del proprietario hello hello [portale di Azure](https://portal.azure.com/) prima. In altre parole, se è stata impostata una origine controllo tooGitHub o BitBucket per qualsiasi app in hello [portale Azure](https://portal.azure.com/) in precedenza, l'utente con credenziali, Azure verrà Memorizza credenziali hello e usarli ogni volta che si distribuisce un'app dello GitHub o BitBucket in hello future. Tuttavia, se questo non già, la distribuzione del modello JSON hello avrà esito negativo quando Gestione risorse di Azure tenta le impostazioni di codice sorgente dell'app di tooconfigure hello web perché Impossibile accedere a GitHub o BitBucket con credenziali del proprietario del repository hello.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>Confrontare il modello JSON hello con gruppo di risorse distribuite
In questo caso, è possibile passare attraverso pannelli tutti hello dell'app web in hello [portale Azure](https://portal.azure.com/), ma non esiste un altro strumento che come utile, se non è più. Passare toohello [Esplora inventario risorse di Azure](https://resources.azure.com) strumento di anteprima, che offre una rappresentazione JSON di tutti i gruppi di risorse hello le sottoscrizioni, in cui si trovano in realtà in hello Azure back-end. È possibile anche informazioni sulla gerarchia JSON del gruppo di risorse hello in Azure con gerarchia hello nel file di modello hello utilizzati toocreate.

Ad esempio, quando passa toohello [Esplora inventario risorse di Azure](https://resources.azure.com) strumento ed espandere i nodi di hello in Esplora hello, è possibile visualizzare il gruppo di risorse di hello e le risorse a livello di radice hello che vengono raccolti con i relativi tipi di risorse corrispondente.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

Se il drill-down tooa web app, dovrebbe essere in grado di toosee web app configurazione dettagli simili toohello seguente schermata:

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

Nuovamente, hello risorse annidate devono avere un toothose molto simili gerarchia nel file di modello JSON e dovrebbe essere impostazioni app hello, le stringhe di connessione e così via, adeguatamente riflesso nel riquadro di hello JSON. Hello l'assenza di impostazioni può indicare un problema con il file JSON e può consentire di risolvere il file di modello JSON.

## <a name="deploy-hello-resource-group-template-yourself"></a>Distribuire modello gruppo di risorse hello manualmente
Hello **distribuire tooAzure** pulsante è molto utile, ma consente modello gruppo di risorse hello toodeploy in azuredeploy.json solo se si dispone già inserito azuredeploy.json tooGitHub. Hello Azure .NET SDK fornisce inoltre strumenti hello per si toodeploy qualsiasi file di modello JSON direttamente dal computer locale. toodo, questa procedura hello seguire seguente:

1. In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.
2. Fare clic su **Visual C#** > **Cloud** > **Gruppo di risorse di Azure**, quindi su **OK**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. In **Seleziona modello di Azure** selezionare **Modello vuoto** e fare clic su **OK**.
4. Trascinare azuredeploy.json in hello **modello** cartella del nuovo progetto.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. In Esplora soluzioni, aprire azuredeploy.json hello copiato.
6. Solo per i migliori risultati hello di dimostrazione hello, aggiungere alcuni standard Application Insights tooour JSON file di risorse, fare clic su **Aggiungi risorsa**. Se si è interessati solo nella distribuzione di file JSON hello, ignorare i passaggi di distribuzione toohello.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. Selezionare **Application Insights per app Web**, assicurarsi che siano selezionati un piano di servizio app esistente e un'app Web e quindi fare clic su **Aggiungi**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   Sarà ora essere in grado di toosee diverse nuove risorse che, a seconda della risorsa hello e funzionalità, presentano dipendenze entrambi hello app web del piano o hello servizio App. Queste risorse non sono abilitate per la definizione esistente e sarà toochange che.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. Nella struttura JSON hello, fare clic su **appInsights scalabilità automatica** toohighlight il codice JSON. Si tratta di hello scalabilità impostazione per il piano di servizio App.
9. Nel codice evidenziato di JSON hello, individuare hello `location` e `enabled` proprietà e impostarli come illustrato di seguito.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. Nella struttura JSON hello, fare clic su **CPUHigh appInsights** toohighlight il codice JSON. Si tratta di un avviso.
11. Individuare hello `location` e `isEnabled` proprietà e impostarli come illustrato di seguito. Hello stesso per hello altri tre avvisi (lampadine viola).
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. A questo punto si toodeploy pronto. Fare clic sul progetto hello e selezionare **Distribuisci** > **nuova distribuzione**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. Accedere al proprio account Azure, se non si è già connessi.
14. Selezionare un gruppo di risorse esistente nella sottoscrizione o creare un nuovo gruppo, selezionare **azuredeploy.json**, quindi fare clic su **Modifica parametri**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    Sarà ora in grado di tooedit tutti i parametri di hello è definiti nel file di modello hello in una tabella nice. I parametri che definiscono i valori predefiniti avranno già i relativi valori predefiniti e i parametri che definiscono un elenco di valori consentiti saranno visualizzati come elenchi a discesa.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. Compilare tutti i parametri vuoto hello e utilizzare hello [indirizzo repository GitHub per ToDoApp](https://github.com/azure-appservice-samples/ToDoApp.git) in **URL repository**. Fare quindi clic su **Salva**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > La scalabilità automatica è una funzionalità disponibile in **Standard** livello o superiore, a livello di piano e gli avvisi sono funzionalità offerte da **base** livello o superiore, è necessario hello tooset **sku** parametro troppo**Standard** o **Premium** in ordine toosee tutte le nuove App Insights risorse chiara backup.
    > 
    > 
16. Fare clic su **Distribuisci**. Se si seleziona **salvare le password**, hello password verrà salvata nel file di parametro hello **in testo normale**. In caso contrario, verrà chiesto password del database hello tooinput durante il processo di distribuzione hello.

La procedura è terminata. Ora è sufficiente toogo toohello [portale Azure](https://portal.azure.com/) hello e [Esplora inventario risorse di Azure](https://resources.azure.com) toosee strumento hello nuovi avvisi e impostazioni di scalabilità automatica aggiunto tooyour JSON applicazione distribuita.

I passaggi in questa sezione viene eseguita principalmente seguente hello:

1. File di modello hello preparata
2. Creare un toogo di file di parametro con file di modello hello
3. File di modello hello distribuito con il file di parametro hello

ultimo passaggio Hello avviene facilmente da un cmdlet di PowerShell. toosee cosa ha Visual Studio quando distribuito il AzureResourceGroup.ps1 dell'applicazione, aprire Scripts\Deploy. È una grande quantità di codice non esiste, ma aggiungo toohighlight tutto il codice pertinente hello toodeploy hello modello file con file di parametro hello è necessario.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

Hello ultimo cmdlet, `New-AzureResourceGroup`, è hello che effettivamente esegue hello azione. Tutte queste deve dimostrare che, con l'aiuto di hello di strumenti, è relativamente semplice toodeploy tooyou l'applicazione del cloud in modo prevedibile. Ogni volta che si esegue il cmdlet di hello in hello stesso modello con hello stesso file di parametro, si userà tooget hello stesso risultato.

## <a name="summary"></a>Riepilogo
DevOps, ripetibilità e la prevedibilità di distribuzione tooany le chiavi di un'applicazione a scalabilità elevata composta da microservizi. In questa esercitazione è stato distribuito un tooAzure applicazione due microservizio come un singolo gruppo di risorse utilizzando il modello di gestione risorse di Azure hello. Probabilmente, riceve hello Knowledge Base, è necessario in ordine toostart conversione dell'applicazione in Azure in un modello e può eseguire il provisioning e distribuirlo in modo prevedibile. 

## <a name="next-steps"></a>Passaggi successivi
Scoprire come troppo[si applicano le metodologie agile e pubblicare l'applicazione di microservizi con facilità](app-service-agile-software-development.md) e tecniche di distribuzione come avanzate [anteprima distribuzione](app-service-web-test-in-production-controlled-test-flight.md) facilmente.

<a name="resources"></a>

## <a name="more-resources"></a>Altre risorse
* [Linguaggio del modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Funzioni del modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-template-functions.md)
* [Distribuire un'applicazione con un modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-template-deploy.md)
* [Uso di Azure PowerShell con Gestione risorse di Azure](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Risoluzione dei problemi relativi alle distribuzioni di gruppi di risorse in Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md)

