---
title: un'applicazione ASP.NET in Azure con il Database SQL aaaBuild | Documenti Microsoft
description: Informazioni su come tooget un ASP.NET app Usa Azure, con tooa connessione Database SQL.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Creare un'app ASP.NET in Azure con un database SQL

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione. In questa esercitazione Mostra come toodeploy un ASP.NET basati sui dati web app in Azure e connetterla troppo[Database SQL di Azure](../sql-database/sql-database-technical-overview.md). Al termine, si dispone di un'applicazione ASP.NET in esecuzione in [Azure App Service](../app-service/app-service-value-prop-what-is.md) e tooSQL Database connesso.

![Applicazione ASP.NET pubblicata nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un database SQL in Azure
> * Connettersi a un tooSQL app ASP.NET Database
> * Distribuire hello app tooAzure
> * Modello di dati hello e ridistribuire l'applicazione hello
> * Registri di flusso di Azure tooyour terminal
> * Gestire app hello in hello portale di Azure

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

* Installare [Visual Studio 2017](https://www.visualstudio.com/downloads/) con hello carichi di lavoro seguente:
  - **Sviluppo Web e ASP.NET**
  - **Sviluppo di Azure**

  ![Sviluppo Web e ASP.NET e sviluppo di Azure (in Web e Cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Scaricare l'esempio hello

[Scaricare il progetto di esempio hello](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Estrarre (decomprimere) hello *master.zip dotnet-sqldb-esercitazione* file.

progetto di esempio Hello contiene un basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-lettura-aggiornamento-eliminazione) app usando [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Eseguire app hello

Aprire hello *dotnet-sqldb-esercitazione-master/DotNetAppSqlDb.sln* file in Visual Studio. 

Tipo `Ctrl+F5` toorun hello app senza debug. Hello app viene visualizzata nel browser predefinito. Seleziona hello **Crea nuovo** collegare e creare un paio *attività* elementi. 

![Finestra di dialogo Nuovo progetto ASP.NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Hello test **modifica**, **dettagli**, e **eliminare** collegamenti.

app Hello Usa un tooconnect di contesto di database con database hello. In questo esempio, il contesto di database hello utilizza una stringa di connessione denominata `MyDbConnection`. stringa di connessione Hello è impostato in hello *Web. config* file e cui viene fatto riferimento in hello *Models/MyDatabaseContext.cs* file. nome di stringa di connessione Hello viene utilizzato più avanti in hello tooconnect esercitazione hello Azure web app tooan Database SQL di Azure. 

## <a name="publish-tooazure-with-sql-database"></a>Pubblicare tooAzure con il Database SQL

In hello **Esplora**, fare doppio clic sui **DotNetAppSqlDb** del progetto e selezionare **pubblica**.

![Pubblicare da Esplora soluzioni](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

Verificare che **Servizio app di Microsoft Azure** sia selezionato e fare clic su **Pubblica**.

![Pubblicare dalla pagina di panoramica progetto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Pubblicazione apre hello **Crea servizio App** finestra di dialogo, che consente di creare tutti hello risorse di Azure è necessario toorun app web ASP.NET in Azure.

### <a name="sign-in-tooazure"></a>Accedi tooAzure

In hello **Crea servizio App** finestra di dialogo, fare clic su **aggiungere un account**, quindi accedi tooyour sottoscrizione di Azure. Se si è già connessi a un account Microsoft, verificare che l'account contenga la sottoscrizione di Azure. Se hello Microsoft account connesso non dispone di sottoscrizione di Azure, scegliere account di tooadd hello corretto.
   
![Accedi tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

Una volta effettuato l'accesso, si è pronti toocreate che tutte le risorse che necessarie per l'app web di Azure in questa finestra di dialogo di hello.

### <a name="configure-hello-web-app-name"></a>Nome dell'applicazione web hello configurare

È possibile mantenere nome dell'applicazione web hello generato o modificare il nome univoco tooanother (i caratteri validi sono `a-z`, `0-9`, e `-`). nome dell'applicazione web Hello viene utilizzata come parte dell'URL di hello predefinito per l'app (`<app_name>.azurewebsites.net`, dove `<app_name>` è il nome dell'applicazione web). nome dell'applicazione web Hello deve toobe univoco tra tutte le App in Azure. 

![Finestra di dialogo Crea servizio app](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Avanti troppo**gruppo di risorse**, fare clic su **New**.

![TooResource successivo gruppo, fare clic su nuovo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Nome gruppo di risorse hello **myResourceGroup**.

> [!NOTE]
> Non fare clic su **Crea**. È necessario innanzitutto tooset di un Database SQL in un passaggio successivo.

### <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Avanti troppo**piano di servizio App**, fare clic su **New**. 

In hello **configurare il piano di servizio App** finestra di dialogo, configurare il nuovo piano di servizio App hello con hello seguenti impostazioni:

![Creare un piano di servizio app](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Impostazione  | Valore consigliato | Per altre informazioni |
| ----------------- | ------------ | ----|
|**Piano di servizio app**| myAppServicePlan | [Piani del servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Posizione**| Europa occidentale | [Aree di Azure](https://azure.microsoft.com/regions/) |
|**Dimensione**| Free | [Piani tariffari](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>Creare un'istanza di SQL Server

Prima di creare un database è necessario un [server logico di database SQL di Azure](../sql-database/sql-database-features.md). Un server logico contiene un gruppo di database gestiti come gruppo.

Selezionare **Esplora altri servizi di Azure**.

![Configurare il nome dell'app Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

In hello **servizi** scheda, fare clic su hello  **+**  icona Avanti troppo**Database SQL**. 

![Nella scheda Servizi hello, fare clic sull'icona + hello tooSQL successivo Database.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

In hello **configurare il Database SQL** finestra di dialogo, fare clic su **New** Avanti troppo**SQL Server**. 

Viene generato un nome di server univoco. Questo nome viene utilizzato come parte dell'URL di hello predefinito per il server logico, `<server_name>.database.windows.net`. Deve essere univoco in tutte le istanze di server logico in Azure. È possibile modificare il nome di server hello, ma per questa esercitazione, mantenere il valore di hello generato.

Aggiungere un nome utente e una password di amministratore e quindi selezionare **OK**. Per i requisiti di complessità delle password, vedere [Criteri password](/sql/relational-databases/security/password-policy).

Prendere nota del nome utente e della password. Sono necessari server logico di hello toomanage istanza in un secondo momento.

![Creare un'istanza di SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>Creare un database SQL

In hello **configurare il Database SQL** finestra di dialogo: 

* Mantenere l'impostazione predefinita, hello generata **nome del Database**.
* In **Nome stringa di connessione** digitare *MyDbConnection*. Questo nome deve corrispondere una stringa di connessione hello a cui fa riferimento in *Models/MyDatabaseContext.cs*.
* Selezionare **OK**.

![Configurare il database SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Hello **Crea servizio App** finestra di dialogo Mostra risorse hello è stato creato. Fare clic su **Crea**. 

![risorse Hello che è stato creato](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Al termine della procedura guidata hello creazione hello risorse di Azure, vengono pubblicati i tooAzure app ASP.NET. Il browser predefinito viene avviato con app di hello URL toohello distribuito. 

Aggiungere alcune attività.

![Applicazione ASP.NET pubblicata nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Congratulazioni. L'applicazione ASP.NET basata sui dati è in esecuzione nel Servizio app di Azure.

## <a name="access-hello-sql-database-locally"></a>Accedere localmente hello Database SQL

Visual Studio consente di esplorare e gestire il nuovo Database SQL facilmente nel hello **Esplora oggetti di SQL Server**.

### <a name="create-a-database-connection"></a>Creare una connessione al database

Da hello **vista** dal menu **Esplora oggetti di SQL Server**.

Nella parte superiore di hello di **Esplora oggetti di SQL Server**, fare clic su hello **aggiungere SQL Server** pulsante.

### <a name="configure-hello-database-connection"></a>Configurare una connessione al database hello

In hello **Connetti** finestra di dialogo espandere hello **Azure** nodo. Vengono visualizzate tutte le istanze del database SQL di Azure.

Seleziona hello `DotNetAppSqlDb` Database SQL. connessione Hello creata in precedenza viene inserito automaticamente nella parte inferiore di hello.

Digitare hello password di amministratore di database creato in precedenza e fare clic su **Connetti**.

![Configurare la connessione al database da Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>Consentire la connessione client dal computer

Hello **creare una nuova regola firewall** è aperta una finestra di dialogo. Per impostazione predefinita, l'istanza del database SQL consente solo le connessioni da servizi di Azure, ad esempio dall'app Web di Azure. tooconnect tooyour del database, creare una regola del firewall nell'istanza di Database SQL di hello. regola del firewall Hello consente hello indirizzo IP del computer locale.

finestra di dialogo Hello è già stato compilato con indirizzo IP pubblico del computer.

Assicurarsi che l'opzione **Aggiungi IP client** sia selezionata e fare clic su **OK**. 

![Impostare il firewall per l'istanza del database SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Una volta terminato Visual Studio creazione hello impostazione del firewall per l'istanza del Database SQL, la connessione viene visualizzato nella **Esplora oggetti di SQL Server**.

In questo caso, è possibile eseguire hello più comuni operazioni di database, ad esempio le query eseguite, creano visualizzazioni e stored procedure e altro ancora. 

Fare clic su hello `Todoes` tabella e selezionare **Visualizza dati**. 

![Esplorare gli oggetti del database SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Aggiornare l'app con Migrazioni Code First

È possibile utilizzare strumenti comuni di hello in Visual Studio tooupdate l'app web e il database in Azure. In questo passaggio utilizzare migrazioni Code First in Entity Framework toomake tooyour modifica uno schema di database e pubblicarlo tooAzure.

Per altre informazioni sull'uso di Migrazioni Code First di Entity Framework, vedere [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application) (Introduzione a Code First di Entity Framework 6 con MVC 5).

### <a name="update-your-data-model"></a>Aggiornare il modello di dati

Aprire _Models\Todo.cs_ nell'editor di codice hello. Aggiungere hello seguente proprietà toohello `ToDo` classe:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Eseguire Migrazioni Code First in locale

Eseguire alcuni comandi toomake aggiornamenti tooyour database locale. 

Da hello **strumenti** menu, fare clic su **Gestione pacchetti NuGet** > **Package Manager Console**.

Nella finestra della Console di gestione pacchetti hello, abilitare le migrazioni Code First:

```PowerShell
Enable-Migrations
```

Aggiungere una migrazione:

```PowerShell
Add-Migration AddProperty
```

Aggiornamento del database locale hello:

```PowerShell
Update-Database
```

Tipo `Ctrl+F5` toorun hello app. Hello test, modificare, informazioni dettagliate, nonché creare collegamenti.

Se un'applicazione hello viene caricata senza errori, migrazioni Code First è stata completata. Tuttavia, ha un aspetto ancora la pagina hello stesso poiché la logica dell'applicazione non utilizza ancora la nuova proprietà. 

### <a name="use-hello-new-property"></a>Utilizzare hello nuova proprietà

Apportare alcune modifiche nel hello toouse codice `Done` proprietà. Per semplicità in questa esercitazione, sarà solo hello toochange `Index` e `Create` viste proprietà hello toosee nell'azione.

Aprire _Controllers\TodosController.cs_.

Trovare hello `Create()` (metodo) e aggiungere `Done` toohello elenco delle proprietà hello `Bind` attributo. Al termine, il `Create()` firma del metodo è simile a hello seguente codice:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Aprire _Views\Todos\Create.cshtml_.

Nel codice Razor hello, vedrai un `<div class="form-group">` elemento che utilizza `model.Description`e quindi un'altra `<div class="form-group">` elemento che utilizza `model.CreatedDate`. Immediatamente dopo questi due elementi, aggiungere un altro elemento `<div class="form-group">` che usa `model.Done`:

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Aprire _Views\Todos\Index.cshtml_.

Ricerca di hello vuoto `<th></th>` elemento. Sopra questo elemento, aggiungere hello codice Razor seguenti:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Trovare hello `<td>` elemento contenente hello `Html.ActionLink()` metodi di supporto. Sopra questo elemento, aggiungere hello codice Razor seguenti:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

Che sono tutte le necessarie modifiche hello toosee hello `Index` e `Create` viste. 

Tipo `Ctrl+F5` toorun hello app.

È ora possibile aggiungere un'attività e selezionare **Fine**. L'attività viene visualizzata come completata nella home page. Tenere presente che hello `Edit` visualizzazione non mostra hello `Done` campo, perché non si sono modificati hello `Edit` visualizzazione.

### <a name="enable-code-first-migrations-in-azure"></a>Abilitare Migrazioni Code First in Azure

Ora che il codice delle modifiche, inclusa la migrazione di database, si pubblicarla tooyour Azure web app e aggiorna il Database SQL con le migrazioni Code First troppo.

Fare di nuovo clic con il pulsante destro del mouse sul progetto e selezionare **Pubblica**.

Fare clic su **impostazioni** tooopen hello pubblicazione guidata.

![Aprire le impostazioni di pubblicazione](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

Nella procedura guidata hello, fare clic su **Avanti**.

Verificare che la stringa di connessione hello per il Database SQL viene popolato in **MyDatabaseContext (MyDbConnection)**. Potrebbe essere necessario hello tooselect **myToDoAppDb** database dall'elenco a discesa hello. 

Selezionare **Esegui migrazione primo codice (inizia all'avvio dell'applicazione)**, quindi fare clic su **Salva**.

![Abilitare Migrazioni Code First nell'app Web di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Pubblicare le modifiche

Dopo aver abilitato Migrazioni Code First nell'app Web di Azure pubblicare le modifiche al codice.

In hello pagina pubblica, fare clic su **pubblica**.

Provare di nuovo ad aggiungere attività e selezionare **Fine**. Le attività verranno visualizzate nella home page come completate.

![App Web di Azure dopo la migrazione Code First](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Tutte le attività esistenti rimangono visualizzate. Quando si pubblica nuovamente l'applicazione ASP.NET, i dati esistenti nel database SQL non vengono persi. Inoltre, migrazioni Code First cambia solo schema dati hello e lascia intatti i dati esistenti.


## <a name="stream-application-logs"></a>Eseguire lo streaming dei log delle applicazioni

È possibile trasmettere i messaggi di traccia direttamente il tooVisual app web di Azure Studio.

Aprire _Controllers\TodosController.cs_.

Ogni azione inizia con un metodo `Trace.WriteLine()`. Questo codice viene aggiunto tooshow è la modalità tooadd traccia dei messaggi tooyour Azure web app.

### <a name="open-server-explorer"></a>Aprire Esplora server

Da hello **vista** dal menu **Esplora Server**. È possibile configurare la registrazione per l'app Web di Azure in **Esplora server**. 

### <a name="enable-log-streaming"></a>Abilitare lo streaming dei log

In **Esplora server** espandere **Azure** > **Servizio app**.

Espandere hello **myResourceGroup** gruppo di risorse creato al momento della creazione hello Azure web app.

Fare clic con il pulsante destro del mouse sull'app Web di Azure e scegliere **Visualizza log in streaming**.

![Abilitare lo streaming dei log](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Hello registri vengono ora trasmessi in hello **Output** finestra. 

![Streaming dei log nella finestra Output](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

Tuttavia, non viene visualizzato uno dei messaggi di traccia hello ancora. Questo perché quando si seleziona prima **Visualizza log di Streaming**, l'app web di Azure consente di impostare il livello di traccia hello troppo`Error`, che registra solo gli eventi di errore (con hello `Trace.TraceError()` (metodo)).

### <a name="change-trace-levels"></a>Modificare i livelli di traccia

traccia hello toochange livelli toooutput altri messaggi di traccia, passare nuovamente troppo**Esplora Server**.

Fare di nuovo clic con il pulsante destro del mouse sull'app Web di Azure e selezionare **Impostazioni**.

In hello **registrazione delle applicazioni (File System)** elenco a discesa Seleziona **Verbose**. Fare clic su **Salva**.

![Modificare tooVerbose livello di traccia](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> È possibile sperimentare toosee livelli diversi di traccia vengono visualizzati i tipi di messaggi per ogni livello. Ad esempio, hello **informazioni** livello include tutti i log creati da `Trace.TraceInformation()`, `Trace.TraceWarning()`, e `Trace.TraceError()`, ma non i log creati da `Trace.WriteLine()`.
>
>

Nel browser, fare clic su intorno a un'applicazione elenco attività hello in Azure. i messaggi di traccia Hello ora vengono trasmessi toohello **Output** finestra in Visual Studio.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Arrestare lo streaming dei log

toostop hello servizio flusso di log, fare clic su hello **interrompere il monitoraggio** pulsante hello **Output** finestra.

![Arrestare lo streaming dei log](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Gestire l'app Web di Azure

Passare toohello [portale di Azure](https://portal.azure.com) toosee hello web app è stato creato. 



Scegliere dal menu a sinistra hello **servizio App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

Viene visualizzata la pagina dell'app Web. 

Per impostazione predefinita, il portale di hello Mostra hello **Panoramica** pagina. che offre una visualizzazione dello stato dell'app. In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare. schede di Hello sul lato sinistro di hello della pagina hello mostrano è possibile aprire le pagine di configurazione diverso hello. 

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un database SQL in Azure
> * Connettersi a un tooSQL app ASP.NET Database
> * Distribuire hello app tooAzure
> * Modello di dati hello e ridistribuire l'applicazione hello
> * Registri di flusso di Azure tooyour terminal
> * Gestire app hello in hello portale di Azure

Spostare toolearn esercitazione successiva toohello come toomap un DNS personalizzato denominati toohello web app.

> [!div class="nextstepaction"]
> [Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md)
