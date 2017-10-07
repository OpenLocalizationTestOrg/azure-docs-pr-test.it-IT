---
title: un processo Web .NET in Azure App Service aaaCreate | Documenti Microsoft
description: "Informazioni sulla creazione di un app a più livelli con ASP.NET MVC e Azure. Hello front-end viene eseguito in un'app web in Azure App Service e hello back-end esegue come un processo Web. app Hello Usa Entity Framework, Database SQL e le code di archiviazione di Azure e BLOB."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Creare un processo Web .NET nel servizio app di Azure
Questa esercitazione viene illustrato come toowrite codice per una semplice applicazione ASP.NET MVC 5 multilivello che usa hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

scopo di hello Hello [WebJobs SDK](websites-webjobs-resources.md) è toosimplify hello codice scritto per attività comuni che possono eseguire un processo Web, ad esempio l'elaborazione di immagini, l'elaborazione della coda, aggregazione RSS, manutenzione di file e l'invio di messaggi di posta elettronica. Hello WebJobs SDK include funzionalità per l'utilizzo di archiviazione di Azure e Bus di servizio per la pianificazione di attività e la gestione degli errori e per molti altri scenari comuni. Inoltre, ha progettato toobe estendibile e vi è un [repository del codice sorgente aperta per le estensioni](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

applicazione di esempio Hello è un servizio BBS pubblicità. Gli utenti possono caricare le immagini per gli annunci e un processo di back-end converte toothumbnails immagini hello. pagina di elenco annuncio Hello mostrate le anteprime di hello e pagina dettagli di annuncio hello Mostra immagine ingrandita hello. Di seguito è riportata una schermata:

![Elenco di inserzioni](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Questa applicazione di esempio funziona con le [code di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) e con i [BLOB di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Hello esercitazione viene illustrato come toodeploy hello applicazione troppo[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) e [Database SQL di Azure](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Prerequisiti
Hello esercitazione si presuppone che si conosca come toowork con [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) progetti in Visual Studio.

esercitazione Hello è stato inizialmente scritto per Visual Studio 2013, ma può essere utilizzato con le versioni successive di Visual Studio. Se si utilizza Visual Studio 2015 o 2017, prendere nota prima di eseguire un'applicazione hello in locale, è necessario modificare hello `Data Source` fa parte della stringa di connessione di SQL Server LocalDB hello nei file Web. config e App. config di hello da `Data Source=(localdb)\v11.0` troppo`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>È necessario avere un toocomplete account Azure in questa esercitazione:
>
> * È possibile [aprire un account Azure, gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): si ottiene crediti che è possibile utilizzare tootry out a pagamento di servizi di Azure e anche dopo che consentono, è possibile tenere conto di hello e utilizzare servizi di Azure gratuiti, ad esempio siti Web. Carta di credito non verranno mai addebitata, a meno che non modificare le impostazioni in modo esplicito e chiedere toobe addebitati.
> * I [sottoscrittori di Visual Studio possono attivare il credito Azure mensile](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): con la sottoscrizione ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.
>
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
>
>

## <a id="learn"></a>Contenuto dell'esercitazione
Hello esercitazione vengono illustrate le modalità hello toodo seguenti attività:

* Abilitare il computer per lo sviluppo di Azure installando hello Azure SDK (solo per Visual Studio 2013 e 2015 utenti).
* Creare un progetto di applicazione Console che distribuisce automaticamente come un processo Web di Azure quando si distribuisce il progetto di web associato hello.
* Testare un back-end WebJobs SDK in locale nel computer di sviluppo hello.
* Pubblicare un'applicazione con un'app web di processi Web back-end tooa nel servizio App.
* Caricare i file e archiviarli in hello servizio Blob di Azure.
* Utilizzare hello Azure WebJobs SDK toowork con BLOB e code di archiviazione di Azure.

## <a id="contosoads"></a>Architettura dell'applicazione
applicazione di esempio Hello utilizza hello [basate su coda di lavoro modello](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carico di lavoro hello intenso della CPU di creazione di anteprime tooa back-end processo.

app Hello archivia gli annunci in un database SQL, mediante Entity Framework Code First toocreate hello le tabelle e accedere ai dati hello. Per ogni annuncio, database hello archivia due URL: uno per dimensioni effettive hello e uno per l'anteprima di hello.

![Tabella di inserzioni](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Quando un utente carica un'immagine, hello web app memorizza immagine hello in un [blob di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), e archivia le informazioni sugli annunci hello in database hello con un URL che punta toohello blob. AT hello stesso tempo, viene scritto un tooan messaggio coda di Azure. In un processo di back-end in esecuzione come un processo Web di Azure, hello WebJobs SDK esegue il polling della coda di hello per i nuovi messaggi. Quando viene visualizzato un nuovo messaggio, hello processo Web viene creata un'anteprima dell'immagine e aggiornamenti hello campo del database URL anteprima per quell'annuncio. Di seguito è riportato un diagramma che illustra l'interagiscono tra le parti di un'applicazione hello hello:

![Architettura di Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
le istruzioni dell'esercitazione Hello applicano tooAzure SDK per .NET 2.7.1 o versione successiva.

## <a id="storage"></a>Creare un account di archiviazione di Azure
Un account di archiviazione di Azure fornisce risorse per l'archiviazione dei dati di code e blob nel cloud hello. Viene utilizzato anche per dashboard hello da hello dati di registrazione toostore WebJobs SDK.

In un'applicazione effettiva si creano in genere account separati per i dati dell'applicazione rispetto ai dati di registrazione e account separati per i dati di test rispetto ai dati di produzione. In questa esercitazione sarà usato un solo account.

1. Aprire hello **Esplora Server** finestra in Visual Studio.
2. Pulsante destro del mouse hello **Azure** nodo e quindi fare clic su **connettersi tooMicrosoft sottoscrizione Azure...** .
   
   ![Connettersi tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Accedere con le credenziali di Azure.
4. Fare doppio clic su **archiviazione** in hello nodo di Azure e quindi fare clic su **crea Account di archiviazione**.
   
   ![Crea account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. In hello **crea Account di archiviazione** finestra di dialogo immettere un nome per l'account di archiviazione hello.

    nome Hello deve essere univoco (nessun altro account di archiviazione di Azure può avere hello stesso nome). Se specifica un nome hello è già in uso, si otterrà un toochange possibilità è.

    Hello tooaccess URL l'account di archiviazione sarà *{nome}*. c.
6. Set hello **regione o gruppo di affinità** riepilogo toohello area più vicina tooyou.

    Questa impostazione specifica il data center di Azure che ospiterà l'account di archiviazione. Per questa esercitazione è possibile selezionare qualsiasi area senza riscontrare differenze evidenti. Per un'app web di produzione, è tuttavia il server web e il toobe di account di archiviazione in hello stesso latenza toominimize di area e i dati in uscita addebiti. app web Hello (che verrà creato in un secondo momento) deve essere Data Center più vicino possibile toohello browser, accedere alle app web hello in latenza toominimize ordine.
7. Set hello **replica** elenco a discesa elenco troppo**ridondanza locale**.

    Quando la replica geografica è abilitata per un account di archiviazione, il contenuto di hello archiviato è posizione tooa replicati Data Center secondario tooenable failover toothat in caso di un errore grave nella posizione primaria hello. La replica geografica può comportare costi aggiuntivi. Per gli account di sviluppo e test, in genere non si desidera toopay per la replica geografica. Per altre informazioni, vedere la pagina relativa alla [creazione, gestione o eliminazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).
8. Fare clic su **Crea**.

    ![Nuovo account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Scaricare l'applicazione hello
1. Scaricare e decomprimere hello [completato soluzione](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Avviare Visual Studio.
3. Da hello **File** dal menu **aprire > progetto/soluzione**, passare toowhere soluzione hello è stato scaricato e quindi aprire il file di soluzione hello.
4. Premere soluzione hello toobuild CTRL + MAIUSC + B.

    Per impostazione predefinita, Visual Studio vengono automaticamente ripristinati contenuto del pacchetto NuGet hello, che non era incluso nel hello *zip* file. Se non ripristino i pacchetti hello, installarli manualmente, passare toohello **Gestisci pacchetti NuGet per la soluzione** finestra di dialogo e fare clic su hello **ripristinare** pulsante in alto a destra hello.
5. In **Esplora**, assicurarsi che **ContosoAdsWeb** sia selezionato come progetto di avvio hello.

## <a id="configurestorage"></a>Configurare l'account di archiviazione di hello applicazione toouse
1. Aprire l'applicazione hello *Web. config* file nel progetto ContosoAdsWeb hello.

    file Hello contiene una stringa di connessione SQL e una stringa di connessione di archiviazione di Azure per l'utilizzo di BLOB e code.

    stringa di connessione SQL Hello punta tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.

    stringa di connessione di archiviazione Hello è riportato un esempio con segnaposto per hello chiave account di archiviazione nome e l'accesso. Si sarà sostituire con una stringa di connessione con nome hello e la chiave dell'account di archiviazione.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    stringa di connessione di archiviazione Hello è denominato AzureWebJobsStorage perché è hello Nome hello che webjobs SDK viene utilizzato per impostazione predefinita. Hello stesso nome viene usato in modo da valore stringa di una sola connessione tooset hello ambiente Azure.
2. In **Esplora Server**, fare doppio clic su account di archiviazione in hello **archiviazione** nodo e quindi fare clic su **proprietà**.

    ![Fare clic su proprietà Account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. In hello **proprietà** finestra, fare clic su **chiavi dell'Account di archiviazione**, quindi fare clic sui puntini di sospensione hello.

    ![Chiavi dell'account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Hello copia **stringa di connessione**.

    ![Get the storage account keys](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Sostituire una stringa di connessione di archiviazione hello in hello *Web. config* file con stringa di connessione hello appena copiato. Assicurarsi di selezionare tutti gli elementi all'interno di virgolette hello hello virgolette prima di incollare escluso.
6. Aprire hello *app* file nel progetto ContosoAdsWebJob hello.

    Questo file ha due stringhe di connessione di archiviazione, una per i dati dell'applicazione e l'altra per la registrazione. È possibile usare account di archiviazione separati per i dati applicazione e la registrazione oppure usare [più account di archiviazione per i dati](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). In questa esercitazione viene usato un singolo account di archiviazione. le stringhe di connessione Hello dotati di segnaposto per le chiavi account di archiviazione hello.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    Per impostazione predefinita, hello WebJobs SDK esegue la ricerca di stringhe di connessione denominate AzureWebJobsStorage e AzureWebJobsDashboard. In alternativa, è possibile [archiviare la stringa di connessione hello tuttavia si desidera e passarlo in modo esplicito toohello `JobHost` oggetto](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Sostituire entrambe le stringhe di connessione di archiviazione con stringa di connessione hello copiato in precedenza.
8. Salvare le modifiche.

## <a id="run"></a>Eseguire un'applicazione hello in locale
1. front-end web di hello toostart dell'applicazione hello, premere CTRL + F5.

    browser predefinito Hello apre toohello home page. (progetto web hello viene eseguita perché sono state apportate il progetto di avvio hello.)

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. toostart hello processo Web backend dell'applicazione hello, fare doppio clic su progetto ContosoAdsWebJob hello in **Esplora**, quindi fare clic su **Debug** > **Avvia nuova istanza** .

    Una finestra dell'applicazione console aprirà e visualizzerà la registrazione messaggi che indica l'oggetto JobHost SDK processi Web hello avviata toorun.

    ![Finestra dell'applicazione console che mostra il back-end hello è in esecuzione](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. Nel browser fare clic su **Create an Ad**.
4. Immettere alcuni dati di test, selezionare tooupload un'immagine e quindi fare clic su **crea**.

    ![Pagina di creazione](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    app Hello va toohello pagina di indice, ma non è presente un'anteprima per ad nuovo hello perché tale elaborazione non si è ancora verificato.

    Nel frattempo, dopo un breve periodo di attesa registrazione nella finestra dell'applicazione hello console verrà visualizzato un messaggio che un messaggio nella coda è stato ricevuto ed elaborato.

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Dopo aver visualizzato la registrazione dei messaggi nella finestra dell'applicazione console hello hello, aggiornare hello indice toosee hello miniatura.

    ![Pagina di indice](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Fare clic su **dettagli** per le dimensioni effettive hello toosee Active Directory.

    ![Pagina dei dettagli](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Si è in esecuzione un'applicazione hello nel computer locale e utilizza un Server SQL database si trova sul computer, ma funziona con le code e BLOB hello cloud. Nella seguente sezione hello viene eseguita un'applicazione hello nel cloud hello, utilizzando un database cloud nonché cloud BLOB e code.  

## <a id="runincloud"></a>Eseguire un'applicazione hello nel cloud hello
L'utente eseguirà hello seguente un'applicazione nel cloud hello hello toorun passaggi:

* Distribuire le app tooWeb. Visual Studio creerà automaticamente una nuova app Web in servizio app e un'istanza di database SQL.
* Configurare hello web app toouse l'account di archiviazione e database SQL di Azure.

Dopo aver creato alcune annunci durante l'esecuzione nel cloud hello, verranno visualizzati hello hello toosee di WebJobs SDK dashboard rich toooffer ha funzionalità di monitoraggio.

### <a name="deploy-tooweb-apps"></a>Distribuire le app tooWeb

1. Chiudere il browser hello e finestra dell'applicazione console hello.
2. Seguire i passaggi hello hello [pubblicare tooAzure con il Database SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sezione.
3. Dopo aver completato i passaggi di hello per la distribuzione, continuare con le attività rimanenti hello in questo articolo.

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>Configurare l'account di archiviazione e database SQL di Azure di hello web app toouse
È una protezione ottimale troppo[evitare di inserire le informazioni riservate, ad esempio le stringhe di connessione nei file archiviati nel repository del codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Azure offre un modo toodo: è possibile impostare la stringa di connessione e altri valori dell'impostazione nell'ambiente Azure hello e le API di configurazione ASP.NET prelevano automaticamente questi valori quando l'applicazione hello in esecuzione in Azure. È possibile impostare questi valori in Azure utilizzando **Esplora Server**, hello portale di Azure, Windows PowerShell o hello interfaccia della riga di comando multipiattaforma. Per altre informazioni, vedere il blog sul [funzionamento delle stringhe di applicazione e di connessione](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

In questa sezione, utilizzare **Esplora Server** tooset valori di stringa di connessione in Azure.

1. In **Esplora server** fare clic con il pulsante destro del mouse sull'app Web in **Azure > Servizio app > {gruppo di risorse}**, quindi scegliere **Visualizza impostazioni**.

    Hello **App Web di Azure** verrà visualizzata la finestra su hello **configurazione** scheda.
2. Modifica nome hello del nome di toohello stringa di connessione di hello DefaultConnection scelto quando è stato configurato il database SQL hello in hello [pubblicare tooAzure con il Database SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) articolo.

    Azure viene creato automaticamente la stringa di connessione durante la creazione di app web hello con un database associato, ha già il valore di stringa di connessione corretta hello. Si desidera modificare solo toowhat nome hello che il codice sta cercando.
3. Aggiungere due nuove stringhe di connessione denominate AzureWebJobsStorage e AzureWebJobsDashboard. Impostare il tipo di database hello troppo**personalizzato**, set hello connessione stringa valore toohello stesso valore utilizzato in precedenza per hello e *Web. config* e *app* file. (Assicurarsi includere hello intera stringa di connessione, non solo chiave di accesso hello e non includere virgolette hello.)

    Queste stringhe di connessione vengono utilizzate da hello WebJobs SDK, uno per i dati dell'applicazione e uno per la registrazione. Come illustrato in precedenza, hello per i dati dell'applicazione viene usato anche dal codice di hello web front-end.
4. Fare clic su **Salva**.

    ![Stringhe di connessione nel portale di Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. In **Esplora Server**, fare doppio clic su hello web app e quindi fare clic su **arrestare**.
6. Al termine dell'app web hello, fare nuovamente doppio clic su hello web app e quindi fare clic su **avviare**.

   Hello processo Web viene avviato automaticamente quando si esegue la pubblicazione, ma arresta quando si esegue una configurazione di modifica. toorestart, è possibile riavviare l'app web hello o riavviare i processi Web hello in hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715). È in genere consigliato toorestart hello web app dopo una modifica della configurazione.
7. Aggiornare hello finestra del browser con URL dell'app web hello nella relativa barra degli indirizzi.

    verrà visualizzata la pagina home Hello.
8. Creare un annuncio, come quando si [veniva eseguita localmente di un'applicazione hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   pagina di indice Hello Mostra senza un'anteprima inizialmente.
9. Aggiornare la pagina hello dopo alcuni secondi e hello anteprima viene visualizzata.

   Se non viene visualizzata l'anteprima di hello, potrebbe essere toowait un minuto per hello processo Web toorestart. Se dopo un periodo di tempo, non viene comunque visualizzato anteprima hello quando si aggiorna la pagina di hello, hello processo Web potrebbe non avere avviato automaticamente. In tal caso, passare toohello **servizi App** pannello in hello [portale di Azure](https://portal.azure.com/), individuare l'app web e quindi fare clic su **avviare**.

### <a name="view-hello-webjobs-sdk-dashboard"></a>Hello visualizzazione dashboard WebJobs SDK
1. In hello [portale di Azure](https://portal.azure.com/)selezionare hello **pannello App servizi**, individuare l'app web e selezionare **processi Web**.
3. Seleziona hello **registri** scheda.

    ![Scheda Log](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Una nuova scheda del browser apre toohello dashboard WebJobs SDK. dashboard di Hello mostra che hello processo Web è in esecuzione e Mostra un elenco di funzioni nel codice che hello che webjobs SDK è attivato.
4. Fare clic su uno hello funzioni toosee dettagli dell'esecuzione.

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    Hello **funzione riproduzione** in questa pagina, hello WebJobs SDK framework toocall hello funzione nuovamente e consente di definire una funzione di probabilità toochange hello dati passati toohello prima.

> [!NOTE]
> Al termine di test, prendere in considerazione l'eliminazione di hello web app, l'account di archiviazione e l'istanza del Database SQL. Hello web app è gratuita, ma l'account di archiviazione SQL hello e l'istanza di database essere addebitati i costi (sebbene, minima a causa di piccole dimensioni toohello). Inoltre, se si lascia hello web app in esecuzione, tutti gli utenti che consente di trovare l'URL può creare e visualizzare annunci. 
>
>

### <a name="delete-your-web-app"></a>Eliminare l'app Web
Nel portale di hello passare toohello **servizi App** pannello, individuare e selezionare l'app web e quindi fare clic su **eliminare**. Se si desidera tootemporarily impedire ad altri utenti di accedere alle app web hello, fare clic su **arrestare** invece. In tal caso, gli addebiti continueranno tooaccrue per hello account di archiviazione e Database SQL.

### <a name="delete-your-storage-account"></a>Eliminare l'account di archiviazione
toodelete l'account di archiviazione, vedere [eliminare un account di archiviazione](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Eliminare il database
toodelete del database SQL del database, vedere hello [API REST di Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) documentazione.

## <a id="create"></a>Creare un'applicazione hello da zero
In questa sezione verranno eseguite hello quanto segue:

* Creare una soluzione Visual Studio con un progetto Web.
* Aggiungere un progetto libreria di classi per i dati di hello livello di accesso condiviso tra hello front-end e back-end.
* Aggiungere un progetto di applicazione Console per hello back-end con processi Web abilitata la distribuzione.
* Aggiungere i pacchetti NuGet.
* Impostare i riferimenti al progetto.
* Copiare il file di codice e la configurazione dell'applicazione da applicazione hello scaricato indicata nella sezione precedente di hello di esercitazione hello.
* Esaminare le parti hello del codice di hello che funzionano con code e BLOB di Azure e hello WebJobs SDK.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Creare una soluzione Visual Studio con un progetto Web e un progetto libreria di classi
1. In Visual Studio scegliere **File** > **Nuovo** > **Progetto**.
2. In hello **nuovo progetto** finestra di dialogo, scegliere **Visual c#** > **Web** > **applicazione Web ASP.NET(.NETFramework)**.
3. Nome progetto hello ContosoAdsWeb, assegnare soluzione hello ContosoAdsWebJobsSDK (modificare il nome di soluzione hello se si inseriranno in hello stessa cartella hello scaricato soluzione), quindi fare clic su **OK**.

    ![Nuovo progetto](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. In hello **nuova applicazione Web ASP.NET** finestra di dialogo, scegliere il modello MVC hello e selezionare **Modifica autenticazione**.

    ![Modifica autenticazione](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. In hello **Modifica autenticazione** finestra di dialogo, scegliere **Nessuna autenticazione**, quindi fare clic su **OK**.

    ![No Authentication](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. In hello **nuova applicazione Web ASP.NET** finestra di dialogo, fare clic su **OK**.

    Visual Studio crea una soluzione di hello e progetto web hello.
7. In **Esplora**, fare doppio clic soluzione hello (non il progetto hello) e scegliere **Aggiungi** > **nuovo progetto**.
8. In hello **Aggiungi nuovo progetto** finestra di dialogo, scegliere **Visual c#** > **Windows Desktop classico** > **libreria di classi (.NET Framework)** modello.  
9. Progetto hello nome *ContosoAdsCommon*, quindi fare clic su **OK**.

    Questo progetto conterrà il contesto di Entity Framework hello e il modello di dati di hello che hello front-end e back-end verrà utilizzata. In alternativa, è possibile definire classi correlate a EF hello nel progetto web hello e fare riferimento a tale progetto dal progetto processo Web hello. Tuttavia, quindi il progetto processo Web avrebbe un assembly tooweb di riferimento, che non sono necessarie.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Aggiungere un progetto applicazione console con la distribuzione dei processi Web abilitata.
1. Fare clic sul progetto web hello (soluzione non hello o progetto libreria di classi hello) e quindi fare clic su **Aggiungi** > **nuovo progetto processo Web di Azure**.

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. In hello **Aggiungi processo Web di Azure** finestra di dialogo immettere ContosoAdsWebJob come entrambi hello **nome progetto** hello e **nome del processo Web**. Lasciare **modalità processo Web eseguire** impostare troppo**eseguire continuamente**.
3. Fare clic su **OK**.

   Visual Studio crea un'applicazione Console che è toodeploy configurato come un processo Web ogni volta che si distribuisce il progetto di web hello. toodo, che eseguita hello seguenti attività dopo aver creato il progetto hello:

   * Aggiungere un *Settings pubblicare processo Web* file nella cartella proprietà di progetto processo Web hello.
   * Aggiungere un *processi Web list.json* file nella cartella proprietà di progetto web hello.
   * Installato hello pacchetto Microsoft.Web.WebJobs.Publish NuGet nel progetto processo Web hello.

   Per ulteriori informazioni su queste modifiche, vedere [come toodeploy processi Web usando Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>Aggiungere i pacchetti NuGet
modello di Hello nuovo progetto per un progetto processo Web viene installato automaticamente come pacchetto NuGet di processi Web SDK hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) e le relative dipendenze.

Una delle dipendenze WebJobs SDK viene installato automaticamente nel progetto processo Web hello è hello hello Azure Storage Client Library (SCL). Tuttavia, è necessario tooadd è toohello web progetto toowork con BLOB e code.

1. Aprire hello **Gestisci pacchetti NuGet** finestra di dialogo per la soluzione hello.
2. Nel riquadro sinistro hello selezionare **i pacchetti installati**.
3. Trovare hello *di archiviazione di Azure* pacchetto e quindi fare clic su **Gestisci**.
4. In hello **selezionare progetti** casella, seleziona hello **ContosoAdsWeb** casella di controllo e quindi fare clic su **OK**.

    Tutti i tre progetti utilizzano hello toowork di Entity Framework con i dati nel Database SQL.
5. Nel riquadro sinistro hello selezionare **Online**.
6. Trovare hello *EntityFramework* NuGet package e installarlo in tutti e tre i progetti.

### <a name="set-project-references"></a>Configurare le preferenze del progetto
Entrambi i progetti processi Web e i web funzionano con il database SQL di hello, pertanto sia necessario un progetto di riferimento toohello ContosoAdsCommon.

1. Nel progetto ContosoAdsWeb hello impostare un progetto di riferimento toohello ContosoAdsCommon. (Fare clic sul progetto ContosoAdsWeb hello e quindi fare clic su **Aggiungi** > **riferimento**. 
2. In hello **gestione riferimenti** nella finestra di dialogo **progetti** > **soluzione** > **ContosoAdsCommon**, quindi fare clic su **OK**.)
   
    progetto processo Web Hello necessita di riferimenti per l'utilizzo di immagini e per l'accesso alle stringhe di connessione.

4. Nel progetto ContosoAdsWebJob hello, impostare un riferimento troppo`System.Drawing` e `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Aggiungere il codice e i file di configurazione
In questa esercitazione non viene visualizzato come troppo[creare controller MVC e viste mediante scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), come troppo[scrivere codice di Entity Framework compatibile con i database di SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), o [hello concetti di base programmazione in ASP.NET 4.5 asincrona](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Pertanto, tutti i toodo rimane è copiare file di codice e la configurazione di soluzione hello scaricato in una nuova soluzione hello. Dopo che a tale scopo, hello nelle sezioni seguenti mostrano e spiegano chiave parti di codice hello.

tooadd file tooa progetto o una cartella, progetto hello pulsante destro del mouse o una cartella e fare clic su **Aggiungi** > **elemento esistente**. Hello seleziona i file desiderati e fare clic su **Aggiungi**. Se viene richiesto se si desidera che i file esistenti tooreplace, fare clic su **Sì**.

1. Nel progetto ContosoAdsCommon hello, eliminare hello *Class1.cs* aggiuntivo relativo hello sul posto i seguenti file dal progetto scaricato hello e dei file.

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. Nel progetto ContosoAdsWeb hello, aggiungere i seguenti file dal progetto scaricato hello hello.

   * *Web.config*
   * *Global.asax.cs*  
   * In hello *controller* cartella: *AdController.cs*
   * In hello *Views\Shared* cartella: *layout. cshtml* file
   * In hello *Views\Home* cartella: *cshtml*
   * In hello *Views\Ad* cartella (Crea cartella hello innanzitutto): cinque *. cshtml* file
3. Nel progetto ContosoAdsWebJob hello, aggiungere i seguenti file dal progetto scaricato hello hello.

   * *App. config* (Modifica filtro del tipo di file hello troppo**tutti i file**)
   * *Program.cs*
   * *Functions.cs*

È ora possibile compilare, eseguire e distribuire un'applicazione hello come indicato in precedenza nell'esercitazione hello. Prima di a tale scopo, tuttavia, arrestare hello processo Web che è ancora in esecuzione nell'app web prima di hello che è distribuito. In caso contrario, tale processo Web verrà elaborare messaggi della coda creati in locale o da app hello in esecuzione in una nuova app web, tutti usino hello stesso account di archiviazione.

## <a id="code"></a>Esaminare il codice dell'applicazione hello
Nelle sezioni seguenti Hello viene codice hello correlati tooworking con hello WebJobs SDK e BLOB di archiviazione di Azure e code.

> [!NOTE]
> Per hello codice toohello specifico WebJobs SDK, visitare toohello [Program.cs e Functions.cs](#programcs) sezioni.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
file Ad.cs Hello definisce un'enumerazione per le categorie di Active Directory e una classe di entità POCO per informazioni di Active Directory.

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
classe ContosoAdsContext Hello specifica classe annuncio hello viene utilizzato in una raccolta di DbSet, Entity Framework vengono archiviati in un database SQL.

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

classe Hello dispone di due costruttori. Hello innanzitutto viene utilizzato dal progetto web hello e specifica il nome di hello di una stringa di connessione che viene archiviato nel file Web. config hello o ambiente di runtime di Azure hello. costruttore secondo Hello consente toopass nella stringa di connessione hello. Poiché non dispone di un file Web. config, che è necessario dal progetto processo Web hello. Illustrato in precedenza in questa stringa di connessione è stata archiviata e verrà visualizzato in un secondo momento come codice hello recupera la stringa di connessione hello quando viene creata un'istanza di classe DbContext hello.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
Hello `BlobInformation` classe è utilizzata toostore informazioni di un blob dell'immagine in un messaggio nella coda.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Codice che viene chiamato da hello `Application_Start` metodo crea un *immagini* contenitore blob e un *immagini* coda se non sono già presenti. In questo modo si garantisce che ogni volta che si avvia con un nuovo account di archiviazione, hello necessari coda e il contenitore blob vengono creati automaticamente.

Hello account di archiviazione toohello di accesso di codice ottiene tramite la stringa di connessione di archiviazione hello da hello *Web. config* file o l'ambiente di runtime di Azure.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Quindi, ottiene un riferimento toohello *immagini* contenitore blob, crea hello contenitore se non esiste già, e imposta le autorizzazioni per il nuovo contenitore di hello di accesso. Per impostazione predefinita, i nuovi contenitori consentono solo client con BLOB tooaccess credenziali account di archiviazione. app web Hello deve hello BLOB toobe pubblico in modo da poter visualizzare immagini con URL che BLOB immagine toohello punto.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

Codice simile Ottiene un riferimento toohello *thumbnailrequest* coda e crea una nuova coda. In questo caso non sono necessarie modifiche alle autorizzazioni.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
Hello *layout. cshtml* file imposta nome di app hello nell'intestazione di hello e piè di pagina e viene creata una voce di menu "Annunci".

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hello *Views\Home\Index.cshtml* file vengono visualizzati i collegamenti di categoria nella home page di hello. collegamenti Hello passare hello integer di hello `Category` enum in una pagina di indice di annunci toohello variabile di stringa di query.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
In hello *AdController.cs* file, hello costruttore chiamate hello `InitializeStorage` gli oggetti di Azure Storage Client Library toocreate metodo che forniscono un'API per l'utilizzo di BLOB e code.

Quindi, codice hello Ottiene un riferimento toohello *immagini* blob contenitore, come illustrato in precedenza nella *Global.asax.cs*. Durante questa operazione, imposta un [criterio per l'esecuzione di nuovi tentativi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) predefinito appropriato per un'app Web. criteri di ripetizione di backoff esponenziale predefiniti Hello potrebbe bloccarsi hello web app per più di un minuto ripetuti tentativi per un errore temporaneo. criteri di ripetizione Hello specificato qui attende 3 secondi dopo ogni cercare i tentativi di toothree.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Codice simile Ottiene un riferimento toohello *immagini* coda.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

La maggior parte del codice del controller hello è tipico per l'utilizzo di un modello di dati di Entity Framework utilizzando una classe DbContext. Un'eccezione è hello HttpPost `Create` metodo, che consente di caricare un file e lo salva nell'archiviazione blob. Raccoglitore di modelli Hello offre un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello metodo dell'oggetto.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Se l'utente hello selezionato tooupload un file, codice hello Carica file hello, viene salvato in un blob e aggiorna i record di database di Active Directory hello con un URL che punta toohello blob.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Hello codice hello caricamento è in hello `UploadAndSaveBlobAsync` metodo. Crea un nome GUID per il blob hello, caricamenti e Salva il file di hello e restituisce un blob di riferimento toohello salvato.

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

Dopo aver hello HttpPost `Create` metodo carica un blob e gli aggiornamenti hello database, viene creato un processo coda messaggi tooinform hello back-end che un'immagine è pronta per l'anteprima di conversione tooa.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

codice per hello HttpPost Hello `Edit` metodo è simile, ad eccezione del fatto che se l'utente di hello seleziona un nuovo file di immagine, è necessario eliminare tutti i blob che esistono già per questo annuncio.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Ecco il codice hello che elimina BLOB quando si elimina un annuncio:

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml
Hello *cshtml* file Visualizza l'anteprima con hello altri dati di Active Directory:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

Hello *Details.cshtml* file Visualizza immagine ingrandita hello:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml ed Edit.cshtml
Hello *Create.cshtml* e *Edit.cshtml* file specificano di codifica che consente di hello hello tooget controller `HttpPostedFileBase` oggetto.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Un `<input>` elemento indica hello browser tooprovide una finestra di dialogo di selezione file.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Quando hello Avvia processo Web, hello `Main` chiamate al metodo hello WebJobs SDK `JobHost.RunAndBlock` esecuzione delle funzioni attivate sul thread corrente hello toobegin del metodo.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - Metodo GenerateThumbnail
Hello WebJobs SDK chiama questo metodo quando viene ricevuto un messaggio nella coda. metodo Hello crea un'immagine di anteprima e inserisce hello anteprima URL nel database di hello.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* Hello `QueueTrigger` attributo indirizza hello WebJobs SDK toocall questo metodo quando viene ricevuto un nuovo messaggio nella coda thumbnailrequest hello.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    Hello `BlobInformation` oggetto nel messaggio della coda hello viene automaticamente deserializzato in hello `blobInfo` parametro. Al termine del metodo hello, viene eliminato il messaggio di coda hello. Se il metodo hello non riesce prima del completamento, il messaggio di coda hello non viene eliminato; Dopo la scadenza di un lease di 10 minuti, il messaggio hello è toobe rilasciato nuovamente prelevato ed elaborato. Questa sequenza non verrà ripetuta all'infinito se un messaggio genera sempre un'eccezione. Dopo 5 non riuscito tentativi tooprocess un messaggio, messaggio hello viene spostata tooa coda denominata {queuename}-messaggi non elaborabili. Hello il numero massimo di tentativi è configurabile.
* Hello due `Blob` gli attributi forniscono gli oggetti che sono associati tooblobs: blob dell'immagine esistente toohello uno e uno tooa nuova anteprima blob creato con il metodo hello.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    I nomi di BLOB provengono dalle proprietà di hello `BlobInformation` oggetto ricevuto nel messaggio della coda hello (`BlobName` e `BlobNameWithoutExtension`). tooget hello le funzionalità complete di hello libreria Client di archiviazione, è possibile utilizzare hello `CloudBlockBlob` toowork di classe con i BLOB. Se si desidera che il codice tooreuse che è stato scritto toowork con `Stream` oggetti, è possibile utilizzare hello `Stream` classe.

Per ulteriori informazioni su come toowrite funzioni che utilizzano attributi WebJobs SDK, vedere hello seguenti risorse:

* [Coda di archiviazione con hello WebJobs SDK come toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [La modalità di archiviazione con blob di Azure toouse hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [La modalità di archiviazione con tabelle di Azure toouse hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Come toouse del Bus di servizio di Azure con hello WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Se l'app web viene eseguito su più macchine virtuali, verrà eseguito contemporaneamente più processi Web, e in alcuni scenari il possibile risultato hello stesso dati elaborati più volte. Questo non costituisce un problema se si usa coda incorporato hello, blob e trigger di Bus di servizio. Hello SDK assicura che le funzioni verranno elaborate solo una volta per ogni messaggio o di un blob.
> * Per informazioni sull'arresto normale tooimplement, vedere [spegnimento](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Hello codice hello `ConvertImageToThumbnailJPG` (metodo) (non illustrato) utilizza le classi hello `System.Drawing` dello spazio dei nomi per motivi di semplicità. Tuttavia, le classi di hello in questo spazio dei nomi sono state progettate per l'uso con Windows Form. Non sono supportate per l'uso in un servizio Windows o ASP.NET. Per altre informazioni sulle opzioni di elaborazione delle immagini, vedere [Generazione dinamica delle immagini](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Informazioni dettagliate sul ridimensionamento delle immagini](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è visto una semplice applicazione multilivello che usa WebJobs SDK hello per l'elaborazione back-end. Questa sezione offre alcuni suggerimenti per ottenere altre informazioni sulle applicazioni ASP.NET multilivello e sui processi Web.

### <a name="missing-features"></a>Funzionalità mancanti
un'applicazione Hello è semplici per un'esercitazione Guida introduttiva. In un'applicazione reale è necessario implementare [inserimento di dipendenze](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) hello e [repository e un'unità di lavoro modelli](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), utilizzare [un'interfaccia per la registrazione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), utilizzare [ Migrazioni Code First di Entity Framework](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage dati le modifiche del modello e utilizzare [resilienza delle connessioni EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage degli errori di rete temporanea.

### <a name="scaling-webjobs"></a>Scalabilità di Processi Web
Processi Web eseguito nel contesto di hello di un'app web e non sono scalabili separatamente. Ad esempio, se si dispone di un'istanza di app web Standard, si dispone solo un'istanza di esecuzione del processo in background e utilizza alcune risorse di server hello (CPU, memoria, e così via) che altrimenti sarebbero disponibili tooserve il contenuto web.

Se il traffico varia in base all'ora del giorno o giorno della settimana e back-end hello l'elaborazione è necessario toodo possono rimanere in attesa, è possibile pianificare i processi Web toorun orari di scarso traffico. Se il carico hello è ancora troppo elevato per la soluzione, è possibile eseguire back-end hello come un processo Web in un'app web separato dedicato a tale scopo. Sarà quindi possibile scalare l'app Web back-end indipendentemente dall'app Web front-end.

Per altre informazioni, vedere [Scalabilità di Processi Web](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Come evitare gli arresti per timeout delle app Web
toomake che i processi Web sono sempre in esecuzione e in esecuzione in tutte le istanze dell'app web, si dispone di hello tooenable [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) funzionalità.

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>Utilizzo di hello WebJobs SDK di fuori di processi Web
Toorun non dispone di un programma che usa WebJobs SDK hello in Azure in un processo Web. Può essere eseguito in locale e anche in altri ambienti, ad esempio un ruolo di lavoro dei servizi cloud o un servizio di Windows. Tuttavia, è possibile accedere solo hello dashboard WebJobs SDK tramite un'app web di Azure. dashboard di hello toouse tooconnect hello web app toohello account di archiviazione in uso mediante l'impostazione di stringa di connessione AzureWebJobsDashboard hello sul hello **configura** scheda del portale classico hello. Quindi, è possibile ottenere toohello Dashboard tramite hello URL seguente:

https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions

Per ulteriori informazioni, vedere [ottenere un dashboard per lo sviluppo locale con hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ma si noti che consente di visualizzare un nome di stringa di connessione precedente.

### <a name="more-webjobs-documentation"></a>Altra documentazione sui processi Web
Per altre informazioni, vedere [Risorse di documentazione di Processi Web di Azure](http://go.microsoft.com/fwlink/?LinkId=390226).
