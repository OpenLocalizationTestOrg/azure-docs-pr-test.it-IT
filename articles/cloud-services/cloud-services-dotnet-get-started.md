---
title: aaaGet avviato con servizi Cloud di Azure e ASP.NET | Documenti Microsoft
description: Informazioni su come toocreate un'applicazione multilivello con ASP.NET MVC e Azure. app Hello viene eseguito in un servizio cloud, con ruolo web e il ruolo di lavoro. Usa Entity Framework, il database SQL e le code e i BLOB di archiviazione di Azure.
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Introduzione a Servizi cloud di Azure e ASP.NET

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come un'applicazione .NET a più livelli con un front-end, ASP.NET MVC toocreate e distribuirlo tooan [servizio cloud di Azure](cloud-services-choose-me.md). Hello applicazione utilizza [Database SQL di Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [servizio Blob di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), hello e [servizio di Accodamento Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). È possibile [scaricare il progetto di Visual Studio hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) da hello MSDN Code Gallery.

Hello esercitazione viene illustrato come toobuild ed eseguire un'applicazione hello in locale, come toodeploy, tooAzure e hello esecuzione nel cloud e come toobuild da zero. È possibile avviare una compilazione da zero e quindi hello test e distribuire i passaggi in un secondo momento se si preferisce.

## <a name="contoso-ads-application"></a>Applicazione Contoso Ads
un'applicazione Hello è un servizio BBS pubblicità. Gli utenti creano un'inserzione tramite l'immissione di testo e il caricamento di un'immagine. È possibile visualizzare un elenco di annunci con immagini di anteprima, e possono essere visualizzate immagine ingrandita hello quando selezionano un' dettagli hello toosee di Active Directory.

![Elenco di inserzioni](./media/cloud-services-dotnet-get-started/list.png)

un'applicazione Hello utilizza hello [basate su coda di lavoro modello](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carico di lavoro hello intenso della CPU di creazione di processo di back-end tooa anteprime.

## <a name="alternative-architecture-websites-and-webjobs"></a>Architettura alternativa: siti Web e processi Web
Questa esercitazione viene illustrato come toorun sia front-end e back-end in un Azure cloud service. In alternativa, è hello toorun front-end in un [sito Web di Azure](/services/web-sites/) e utilizzare hello [processi Web](http://go.microsoft.com/fwlink/?LinkId=390226) funzionalità (attualmente in anteprima) per hello back-end. Per un'esercitazione che utilizza i processi Web, vedere [introduzione hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md). Per informazioni su come toochoose hello servizi che meglio si adatta lo scenario, vedere [confronto siti Web di Azure, servizi Cloud e macchine virtuali](../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>Contenuto dell'esercitazione
* Come tooenable il computer per lo sviluppo di Azure installando hello Azure SDK.
* Toocreate Visual Studio cloud come progetto di servizio con un ruolo web ASP.NET MVC e un ruolo di lavoro.
* Tootest hello come progetto di servizio cloud localmente, utilizzando l'emulatore di archiviazione Azure hello.
* La modalità toopublish hello cloud progetto tooan Azure servizio cloud e di test utilizzando un account di archiviazione di Azure.
* Come tooupload file e archiviarli nel servizio Blob di Azure hello.
* Toouse hello come servizio di Accodamento di Azure per la comunicazione tra i livelli.

## <a name="prerequisites"></a>Prerequisiti
Hello esercitazione presuppone la conoscenza [concetti di base su Azure cloud services](cloud-services-choose-me.md) , ad esempio *ruolo web* e *ruolo di lavoro* terminologia.  Si presuppone inoltre che si conosca come toowork con [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) o [Web Form](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) progetti in Visual Studio. applicazione di esempio Hello Usa MVC, ma la maggior parte dell'esercitazione hello si applica anche tooWeb form.

È possibile eseguire l'applicazione hello in locale senza una sottoscrizione di Azure, ma è necessario un cloud di toohello dall'applicazione hello toodeploy. Se non si dispone di un account, è possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) oppure [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).

le istruzioni dell'esercitazione Hello usare uno dei seguenti prodotti hello:

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Se non si dispone di uno di questi, Visual Studio siano installato automaticamente quando si installa hello Azure SDK.

## <a name="application-architecture"></a>Architettura dell'applicazione
app Hello archivia gli annunci in un database SQL, mediante Entity Framework Code First toocreate hello le tabelle e accedere ai dati hello. Per ogni annuncio, hello database archivia due URL, uno per hello dimensioni effettive e uno per l'anteprima di hello.

![Tabella di inserzioni](./media/cloud-services-dotnet-get-started/adtable.png)

Quando un utente carica un'immagine, hello front-end in esecuzione in un ruolo web archivia l'immagine di hello in un [blob di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), e archivia le informazioni sugli annunci hello in database hello con un URL che punta toohello blob. AT hello stesso tempo, viene scritto un tooan messaggio coda di Azure. Un processo di back-end in esecuzione in un ruolo di lavoro periodicamente esegue il polling della coda di hello per i nuovi messaggi. Quando viene visualizzato un nuovo messaggio, il ruolo di lavoro hello viene creata un'anteprima dell'immagine e aggiornamenti hello campo del database URL anteprima per quell'annuncio. Hello diagramma seguente viene illustrato come le parti di un'applicazione hello hello interagiscono.

![Architettura di Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>Scaricare ed eseguire la soluzione hello completata
1. Scaricare e decomprimere hello [completato soluzione](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Avviare Visual Studio.
3. Da hello **File** dal menu **Apri progetto**, passare toowhere soluzione hello è stato scaricato e quindi aprire il file di soluzione hello.
4. Premere soluzione hello toobuild CTRL + MAIUSC + B.

    Per impostazione predefinita, Visual Studio vengono automaticamente ripristinati contenuto del pacchetto NuGet hello, che non era incluso nel hello *zip* file. Se non ripristino i pacchetti hello, installarli manualmente, passare toohello **Gestisci pacchetti NuGet per la soluzione** la finestra di dialogo e fare clic su hello **ripristinare** pulsante in alto a destra hello.
5. In **Esplora**, assicurarsi che **ContosoAdsCloudService** sia selezionato come progetto di avvio hello.
6. Se si utilizza Visual Studio 2015 o versione successiva, modificare la stringa di connessione di hello in un'applicazione hello *Web. config* file di progetto ContosoAdsWeb hello in hello *ServiceConfiguration.Local.* file di progetto ContosoAdsCloudService hello. In ogni caso, modificare "(localdb) \v11.0" troppo "(localdb) \MSSQLLocalDB".
7. Premere CTRL + F5 toorun un'applicazione hello.

    Quando si esegue un progetto servizio cloud in locale, Visual Studio richiama automaticamente hello Azure *emulatore di calcolo* e Azure *emulatore di archiviazione*. Usa emulatore di calcolo Hello il ruolo del computer risorse toosimulate hello web e ambienti di ruolo di lavoro. Usa emulatore di archiviazione Hello un [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) archiviazione cloud di Azure toosimulate nel database.

    Hello prima esecuzione di un progetto di servizio cloud, accetta un minuto dell'hello emulatori toostart backup. Al termine dell'avvio dell'emulatore, browser predefinito hello verrà visualizzata la home page dell'applicazione toohello.

    ![Architettura di Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. Fare clic su **Create an Ad**.
9. Immettere alcuni dati di test e selezionare un *jpg* immagine tooupload e quindi fare clic su **crea**.

    ![Pagina di creazione](./media/cloud-services-dotnet-get-started/create.png)

    app Hello va toohello pagina di indice, ma non è presente un'anteprima per ad nuovo hello perché tale elaborazione non si è ancora verificato.
10. Attendere qualche istante, quindi aggiornare hello indice toosee hello miniatura.

     ![Pagina di indice](./media/cloud-services-dotnet-get-started/list.png)
11. Fare clic su **dettagli** per le dimensioni effettive hello toosee Active Directory.

     ![Pagina dei dettagli](./media/cloud-services-dotnet-get-started/details.png)

Si è in esecuzione un'applicazione hello interamente nel computer locale, senza cloud toohello di connessione. emulatore di archiviazione Hello archivia coda hello e dati blob in un database di SQL Server Express LocalDB e un'applicazione hello archivia i dati di Active Directory hello in un altro database di LocalDB. Database di Entity Framework Code First hello creati automaticamente ad hello prima volta tooaccess ha tentato di app web hello.

Nella seguente sezione hello si configurerà hello soluzione toouse cloud di Azure le risorse per le code, BLOB e database dell'applicazione hello quando viene eseguito nel cloud hello. Se si desidera toocontinue toorun localmente ma si utilizzano le risorse di archiviazione e database cloud, è possibile farlo. È sufficiente impostare le stringhe di connessione, si noterà come toodo.

## <a name="deploy-hello-application-tooazure"></a>Distribuire tooAzure applicazione hello
L'utente eseguirà hello seguente un'applicazione nel cloud hello hello toorun passaggi:

* Creare un servizio cloud di Azure.
* Creare un database SQL di Azure.
* Creare un account di archiviazione di Azure
* Configurare hello soluzione toouse il database SQL di Azure quando è in esecuzione in Azure.
* Configurare hello soluzione toouse l'account di archiviazione di Azure quando è in esecuzione in Azure.
* Distribuire il servizio cloud di Azure di hello progetto tooyour.

### <a name="create-an-azure-cloud-service"></a>Creazione di un servizio cloud di Azure
Un servizio cloud di Azure è un'applicazione hello hello ambiente verrà eseguita in.

1. Nel browser aprire hello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo > Calcolo > Servizio cloud**.

3. Nella casella input nome DNS hello, immettere un prefisso di URL per il servizio cloud hello.

    Questo URL è toobe univoco.  Se il prefisso hello che scelto è già in uso, si otterrà un messaggio di errore.
4. Specificare un nuovo gruppo di risorse per il servizio di hello. Fare clic su **Crea nuovo** e quindi digitare un nome in hello risorse input casella di gruppo, ad esempio CS_contososadsRG.

5. Scegliere hello area in cui un'applicazione hello toodeploy.

    Questo campo specifica in quale data center viene ospitato il servizio cloud. Per un'applicazione di produzione, scegliere i clienti tooyour di hello area più vicini. Per questa esercitazione, scegliere tooyou di hello area più vicina.
5. Fare clic su **Crea**.

    In hello seguente immagine, viene creato un servizio cloud con hello CSvccontosoads.cloudapp.net URL.

    ![Nuovo servizio cloud](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Creare un database SQL di Azure
Quando l'applicazione hello viene eseguito nel cloud hello, utilizza un database basato su cloud.

1. In hello [portale di Azure](https://portal.azure.com), fare clic su **nuovo > database > Database SQL**.
2. In hello **nome del Database** immettere *contosoads*.
3. In hello **gruppo di risorse**, fare clic su **utilizzare esistente** e gruppo di risorse selezionare hello utilizzato per il servizio cloud hello.
4. In hello seguente immagine, fare clic su **Server - Configurare le impostazioni necessarie** e **creare un nuovo server**.

    ![Server toodatabase tunnel](./media/cloud-services-dotnet-get-started/newdb.png)

    In alternativa, se la sottoscrizione contiene già un server, è possibile selezionare il server dall'elenco a discesa hello.
5. In hello **nome Server** immettere *csvccontosodbserver*.

6. Immettere un **Nome di accesso** e una **Password** per l'amministratore.

    Se si seleziona **Creare un nuovo server** non si immetteranno un nome e una password esistenti in questa casella, Si sta immettendo un nuovo nome e una password che si definiscono toouse ora in un secondo momento quando si accede a database hello. Se si seleziona un server in cui è stato creato in precedenza, verrà chiesto di account utente con privilegi amministrativi toohello password hello già stato creato.
7. Scegliere hello stesso **percorso** scelto per il servizio cloud hello.

    Quando il servizio di cloud hello e database sono in diversi Data Center (diverse aree geografiche), latenza aumenta e verrà addebitato della larghezza di banda fuori hello data center. La larghezza di banda nell'ambito di un data center è gratuita.
8. Controllare **server tooaccess di servizi di azure Consenti**.
9. Fare clic su **selezionare** per nuovo server hello.

    ![Nuovo server di database SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. Fare clic su **Crea**.

### <a name="create-an-azure-storage-account"></a>Creare un account di archiviazione di Azure
Un account di archiviazione di Azure fornisce risorse per l'archiviazione dei dati di code e blob nel cloud hello.

In un'applicazione effettiva si creano in genere account separati per i dati dell'applicazione rispetto ai dati di registrazione e account separati per i dati di test rispetto ai dati di produzione. In questa esercitazione sarà usato un solo account.

1. In hello [portale di Azure](https://portal.azure.com), fare clic su **nuovo > archiviazione > - account di archiviazione blob, file, tabella e coda**.
2. In hello **nome** , immettere un prefisso di URL.

    Questo testo prefisso e hello che viene visualizzato nella casella hello sarà account archiviazione tooyour hello univoco URL. Se il prefisso hello che immesso è già stato utilizzato da un altro utente, sarà necessario toochoose un prefisso diverso.
3. Set hello **modello di distribuzione** troppo*classico*.

4. Set hello **replica** elenco a discesa elenco troppo**archiviazione localmente ridondante**.

    Quando la replica geografica è abilitata per un account di archiviazione, il contenuto di hello archiviato è replicata tooa Data Center secondario tooenable failover se si verifica un errore grave nella posizione primaria hello. La replica geografica può comportare costi aggiuntivi. Per gli account di sviluppo e test, in genere non si desidera toopay per la replica geografica. Per altre informazioni, vedere la pagina relativa alla [creazione, gestione o eliminazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).

5. In hello **gruppo di risorse**, fare clic su **utilizzare esistente** e gruppo di risorse selezionare hello utilizzato per il servizio cloud hello.
6. Set hello **percorso** toohello riepilogo stessa area scelto per il servizio cloud hello.

    Quando si trovano in Data Center diversi account di servizio e l'archiviazione cloud hello (diverse aree geografiche), latenza aumenta e verrà addebitato della larghezza di banda fuori hello data center. La larghezza di banda nell'ambito di un data center è gratuita.

    Gruppi di affinità di Azure forniscono una distanza di hello meccanismo toominimize tra le risorse in un data center, che è possibile ridurre la latenza. In questa esercitazione non vengono utilizzati gruppi di affinità. Per ulteriori informazioni, vedere [come tooCreate un'affinità di gruppo in Azure](http://msdn.microsoft.com/library/jj156209.aspx).
7. Fare clic su **Crea**.

    ![Nuovo account di archiviazione](./media/cloud-services-dotnet-get-started/newstorage.png)

    Nell'immagine di hello, viene creato un account di archiviazione con URL hello `csvccontosoads.core.windows.net`.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Configurare il database SQL di Azure hello soluzione toouse durante l'esecuzione in Azure
Hello progetto web e progetto ruolo di lavoro ogni hello la propria stringa di connessione database e ogni database SQL di Azure di toopoint toohello è necessario quando l'applicazione hello in esecuzione in Azure.

Si userà un [trasformazione Web. config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) per ruolo web hello e un'impostazione di ambiente del servizio cloud per il ruolo di lavoro hello.

> [!NOTE]
> In questa sezione e la sezione successiva di hello, archiviare le credenziali nei file di progetto. [Non archiviare dati sensibili in archivi pubblici di codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).
>
>

1. Nel progetto ContosoAdsWeb hello aprire hello *Web.Release.config* file di trasformazione per un'applicazione hello *Web. config* file, eliminare il blocco di commento hello che contiene un `<connectionStrings>` elemento e incollare Hello seguente codice al suo posto.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Lasciare aperta per la modifica di file hello.
2. In hello [portale di Azure](https://portal.azure.com), fare clic su **database SQL** nel riquadro di sinistra hello, fare clic su database hello creato per questa esercitazione e quindi fare clic su **Mostra stringhe di connessione**.

    ![Mostra stringhe di connessione](./media/cloud-services-dotnet-get-started/showcs.png)

    portale Hello consente di visualizzare le stringhe di connessione, con un segnaposto per la password di hello.

    ![Stringhe di connessione](./media/cloud-services-dotnet-get-started/connstrings.png)
3. In hello *Web.Release.config* trasformare il file, eliminare `{connectionstring}` e incollare nel relativo hello sul posto, la stringa di connessione ADO.NET da hello portale di Azure.
4. Nella stringa di connessione hello incollata nel hello *Web.Release.config* file di trasformazione, sostituire `{your_password_here}` con password hello creata per il nuovo database di SQL hello.
5. Salvare il file hello.  
6. Selezionare e copiare la stringa di connessione hello (senza hello che racchiudono le virgolette) per l'utilizzo in hello alla procedura seguente per la configurazione di progetto di ruolo di lavoro hello.
7. In **Esplora**in **ruoli** nel progetto servizio cloud hello destro **ContosoAdsWorker** e quindi fare clic su **proprietà**.

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Fare clic su hello **impostazioni** scheda.
9. Modifica **configurazione del servizio** troppo**Cloud**.
10. Seleziona hello **valore** field per hello `ContosoAdsDbConnectionString` impostazione e quindi incollare stringa di connessione hello copiato dalla sezione precedente di hello di esercitazione hello.

     ![Stringa di connessione del database per il ruolo di lavoro](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Salvare le modifiche.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Configurare l'account di archiviazione di Azure hello soluzione toouse durante l'esecuzione in Azure
Stringhe di connessione di account di archiviazione di Azure per il progetto di ruolo web hello e progetto di ruolo di lavoro hello vengono archiviate nelle impostazioni di ambiente nel progetto di servizio cloud hello. Per ogni progetto, è presente un set separato di impostazioni toobe utilizzata quando un'applicazione hello in esecuzione in locale e al momento dell'esecuzione nel cloud hello. Si aggiornerà le impostazioni di ambiente cloud hello per i progetti di ruolo web e di lavoro.

1. In **Esplora**, fare doppio clic su **ContosoAdsWeb** in **ruoli** in hello **ContosoAdsCloudService** del progetto e quindi fare clic su **Proprietà**.

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Fare clic su hello **impostazioni** scheda. In hello **configurazione del servizio** elenco a discesa scegliere **Cloud**.

    ![Configurazione del cloud](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Seleziona hello **StorageConnectionString** voce, è possibile notare i puntini di sospensione (**...** ) ubicato a destra hello della riga hello. Fare clic su hello tooopen pulsante puntini di sospensione di hello **crea stringa di connessione Account di archiviazione** la finestra di dialogo.

    ![Casella di creazione della stringa di connessione](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. In hello **crea stringa di connessione di archiviazione** la finestra di dialogo, fare clic su **sottoscrizione**, scegliere account di archiviazione hello creato in precedenza e quindi fare clic su **OK**. Se non è già stato effettuato l'accesso, saranno richieste le credenziali dell'account di Azure.

    ![Crea Stringa di connessione di archiviazione](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Salvare le modifiche.
6. Seguire hello stessa procedura utilizzata per hello `StorageConnectionString` hello tooset stringa di connessione `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` stringa di connessione.

    Questa stringa di connessione è usata per la registrazione.
7. Seguire hello stessa procedura utilizzata per hello **ContosoAdsWeb** tooset ruolo entrambe le stringhe di connessione per hello **ContosoAdsWorker** ruolo. Non dimenticare tooset **configurazione del servizio** troppo**Cloud**.

impostazioni di ambiente ruolo Hello che sia stato configurato utilizzando hello dell'interfaccia utente di Visual Studio vengono archiviate nel seguente file di progetto ContosoAdsCloudService hello hello:

* *Servicedefinition. Csdef* -definisce i nomi delle impostazioni di hello.
* *ServiceConfiguration* -fornisce valori per l'esecuzione dell'applicazione hello nel cloud hello.
* *Local. cscfg* -fornisce valori per l'esecuzione dell'applicazione hello in locale.

Ad esempio, hello Servicedefinition include hello seguenti definizioni:

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

Hello e *ServiceConfiguration* file include i valori hello immessi per tali impostazioni in Visual Studio.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

Hello `<Instances>` impostazione specifica il numero di hello di macchine virtuali che Azure verrà eseguito il lavoro hello codice del ruolo in. Hello [passaggi successivi](#next-steps) sono incluse informazioni toomore collegamenti sulla scalabilità orizzontale di un servizio cloud,

### <a name="deploy-hello-project-tooazure"></a>Distribuire hello progetto tooAzure
1. In **Esplora**, hello rapida **ContosoAdsCloudService** cloud progetto e quindi selezionare **pubblica**.

   ![Menu Pubblica](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. In hello **Accedi** passaggio di hello **pubblica l'applicazione Azure** procedura guidata, fare clic su **Avanti**.

    ![Passaggio Accedi](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. In hello **impostazioni** passaggio della procedura guidata hello, fare clic su **Avanti**.

    ![Passaggio Impostazioni](./media/cloud-services-dotnet-get-started/pubsettings.png)

    le impostazioni predefinite in hello Hello **avanzate** scheda sono supportate per questa esercitazione. Per informazioni sulla scheda Avanzate hello, vedere [pubblicazione guidata applicazione Azure](http://msdn.microsoft.com/library/hh535756.aspx).
4. In hello **riepilogo** passaggio, fare clic su **pubblica**.

    ![Passaggio Riepilogo](./media/cloud-services-dotnet-get-started/pubsummary.png)

   Hello **Log attività Azure** finestra verrà aperta in Visual Studio.
5. Fare clic su dettagli relativi alla distribuzione hello tooexpand icona freccia destra hello.

    distribuzione di Hello può richiedere fino a too5 minuti o più toocomplete.

    ![Finestra Log attività di Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. Quando lo stato di distribuzione hello è stato completato, fare clic su hello **URL app Web** toostart un'applicazione hello.
7. È ora possibile testare l'applicazione hello creando, visualizzazione e modifica alcuni annunci, quando è stata eseguita un'applicazione hello in locale.

> [!NOTE]
> Quando si sta Termina test, eliminazione o l'arresto del servizio cloud di hello. Anche se non si utilizza servizio cloud hello, spettante addebiti perché sono riservate risorse della macchina virtuale. Se lo si lascia in esecuzione, chiunque individui l'URL potrà creare e visualizzare inserzioni. In hello [portale di Azure](https://portal.azure.com), visitare toohello **Panoramica** scheda per il servizio cloud e quindi fare clic su hello **eliminare** pulsante nella parte superiore di hello della pagina hello. Se si desidera tootemporarily impedire ad altri utenti di accedere a hello sito, fare clic su **arrestare** invece. In tal caso, gli addebiti continueranno tooaccrue. Quando non è più necessario, è possibile seguire un simile hello di toodelete procedure account di archiviazione e database SQL.
>
>

## <a name="create-hello-application-from-scratch"></a>Creare un'applicazione hello da zero
Se è stato già scaricato [applicazione hello completato](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), procedere ora. Si saranno copiare i file dal progetto scaricato hello in nuovo progetto di hello.

La creazione di un'applicazione Contoso annunci hello prevede hello alla procedura seguente:

* Creare una soluzione servizio cloud di Visual Studio.
* Aggiornare e aggiungere pacchetti NuGet.
* Impostare i riferimenti al progetto.
* Configurare le stringhe di connessione.
* Aggiungere file di codice.

Dopo la creazione di soluzioni di hello, si verrà esaminato il codice hello in progetti di servizio univoco toocloud e BLOB di Azure e code.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Creare una soluzione servizio cloud di Visual Studio
1. In Visual Studio, scegliere **nuovo progetto** da hello **File** menu.
2. Nel riquadro di sinistra hello di hello **nuovo progetto** finestra di dialogo espandere **Visual c#** e scegliere **Cloud** modelli, quindi scegliere hello **servizioClouddiAzure** modello.
3. Nome progetto hello e soluzione ContosoAdsCloudService e quindi fare clic su **OK**.

    ![Nuovo progetto](./media/cloud-services-dotnet-get-started/newproject.png)
4. In hello **nuovo servizio Cloud Azure** finestra di dialogo, aggiungere un ruolo web e un ruolo di lavoro. Nome di ruolo web hello ContosoAdsWeb e assegnare il ruolo di lavoro hello ContosoAdsWorker. (Utilizzare l'icona della matita hello in nomi predefiniti dei ruoli hello hello riquadro di destra toochange hello).

    ![Nuovo progetto di servizio cloud](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Quando viene visualizzato hello **nuovo progetto ASP.NET** la finestra di dialogo per il ruolo web hello, scegliere il modello MVC hello e quindi fare clic su **Modifica autenticazione**.

    ![Modifica autenticazione](./media/cloud-services-dotnet-get-started/chgauth.png)
6. In hello **Modifica autenticazione** finestra di dialogo scegliere **Nessuna autenticazione**, quindi fare clic su **OK**.

    ![No Authentication](./media/cloud-services-dotnet-get-started/noauth.png)
7. In hello **nuovo progetto ASP.NET** finestra di dialogo, fare clic su **OK**.
8. In **Esplora**, fare doppio clic soluzione hello (non uno dei progetti hello) e scegliere **Add - nuovo progetto**.
9. In hello **Aggiungi nuovo progetto** finestra di dialogo scegliere **Windows** in **Visual c#** in hello riquadro sinistro e quindi fare clic su hello **libreria di classi** modello.  
10. Progetto hello nome *ContosoAdsCommon*, quindi fare clic su **OK**.

    È necessario tooreference hello hello e contesto dati modello di Entity Framework da progetti di ruolo web e di lavoro. In alternativa, è possibile definire classi correlate a EF hello nel progetto di ruolo web hello e fare riferimento a tale progetto dal progetto di ruolo di lavoro hello. Ma in alternativa hello, il progetto di ruolo di lavoro sarebbe necessario un assembly di riferimento tooweb che non sono necessarie.

### <a name="update-and-add-nuget-packages"></a>Aggiornare e aggiungere pacchetti NuGet
1. Aprire hello **Gestisci pacchetti NuGet** la finestra di dialogo per la soluzione hello.
2. Nella parte superiore di hello della finestra hello, selezionare **aggiornamenti**.
3. Cercare hello *Windowsazure* del pacchetto e, se è nell'elenco di hello, selezionarlo e selezionare tooupdate di progetti web e di lavoro hello in e quindi fare clic su **aggiornamento**.

    libreria client di archiviazione Hello viene aggiornata più frequentemente di modelli di progetto di Visual Studio, pertanto tale versione di hello sono spesso disponibili in un toobe esigenze di un nuovo progetto aggiornato.
4. Nella parte superiore di hello della finestra hello, selezionare **Sfoglia**.
5. Trovare hello *EntityFramework* NuGet package e installarlo in tutti e tre i progetti.
6. Trovare hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package e installarlo nel progetto di ruolo di lavoro hello.

### <a name="set-project-references"></a>Configurare le preferenze del progetto
1. Nel progetto ContosoAdsWeb hello impostare un progetto di riferimento toohello ContosoAdsCommon. Fare clic sul progetto ContosoAdsWeb hello e quindi fare clic su **riferimenti** - **Aggiungi riferimenti**. In hello **gestione riferimenti** nella finestra di dialogo **soluzione progetti** nel riquadro di sinistra hello, selezionare **ContosoAdsCommon**, quindi fare clic su **OK**.
2. Nel progetto ContosoAdsWorker hello impostare un progetto di riferimento toohello ContosAdsCommon.

    ContosoAdsCommon conterrà hello Entity Framework dati del modello e il contesto di classe, che verrà usato da entrambi hello front-end e back-end.
3. Nel progetto ContosoAdsWorker hello, impostare un riferimento troppo`System.Drawing`.

    L'assembly è usato da toothumbnails immagini di hello tooconvert back-end.

### <a name="configure-connection-strings"></a>Configurare le stringhe di connessione
In questa sezione verranno configurate le stringhe di connessione di Archiviazione di Azure e SQL per il test in locale. istruzioni di distribuzione Hello in precedenza nell'esercitazione hello spiegano come le stringhe di tooset connessione hello per quando hello app in esecuzione nel cloud hello.

1. Nel progetto ContosoAdsWeb hello, Web. config dell'applicazione hello aperto, seguente hello insert `connectionStrings` elemento dopo hello `configSections` elemento.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Se si usa Visual Studio 2015 o versione successiva, sostituire "v11.0" con "MSSQLLocalDB".
2. Salvare le modifiche.
3. Nel progetto ContosoAdsCloudService hello, fare doppio clic su ContosoAdsWeb in **ruoli**, quindi fare clic su **proprietà**.

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. In hello **ContosAdsWeb [ruolo]** finestra Proprietà, fare clic su hello **impostazioni** scheda e quindi fare clic su **Aggiungi impostazione**.

    Lasciare **configurazione del servizio** impostare troppo**tutte le configurazioni**.
5. Aggiungere un'impostazione denominata *StorageConnectionString*. Impostare **tipo** troppo*ConnectionString*e impostare **valore** troppo*UseDevelopmentStorage = true*.

    ![Nuova stringa di connessione](./media/cloud-services-dotnet-get-started/scall.png)
6. Salvare le modifiche.
7. Seguire hello tooadd procedura stessa stringa di connessione di archiviazione nelle proprietà del ruolo ContosoAdsWorker hello.
8. Ancora in hello **ContosoAdsWorker [ruolo]** finestra Proprietà, aggiungere un'altra stringa di connessione:

   * Nome: ContosoAdsDbConnectionString
   * Tipo: String
   * Valore: Incolla hello stessa stringa di connessione è utilizzata per il progetto di ruolo web hello. (per Visual Studio 2013 è hello di esempio seguente. Non dimenticare hello toochange origine dati se si copia in questo esempio e si utilizza Visual Studio 2015 o versione successiva.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Aggiungere file di codice
In questa sezione si copiano i file di codice da soluzione hello scaricato in una nuova soluzione hello. Hello nelle sezioni seguenti verrà Mostra e illustrano i componenti chiave di questo codice.

tooadd file tooa progetto o una cartella, progetto hello pulsante destro del mouse o una cartella e fare clic su **Aggiungi** - **elemento esistente**. Selezionare file hello desiderati e quindi fare clic su **Aggiungi**. Se viene richiesto se si desidera che i file esistenti tooreplace, fare clic su **Sì**.

1. Nel progetto ContosoAdsCommon hello, eliminare hello *Class1.cs* file e aggiungere il relativo hello sul posto *Ad.cs* e *ContosoAdscontext.cs* progetto scaricare i file da hello.
2. Nel progetto ContosoAdsWeb hello, aggiungere i seguenti file dal progetto scaricato hello hello.

   * *Global.asax.cs*.  
   * In hello *Views\Shared* cartella:  *\_cshtml*.
   * In hello *Views\Home* cartella: *cshtml*.
   * In hello *controller* cartella: *AdController.cs*.
   * In hello *Views\Ad* cartella (Crea cartella hello innanzitutto): cinque *. cshtml* file.
3. Nel progetto ContosoAdsWorker hello aggiungere *WorkerRole.cs* da hello scaricato il progetto.

È possibile compilare ed eseguire un'applicazione hello come indicato in precedenza nell'esercitazione hello e app hello utilizzerà le risorse dell'emulatore di archiviazione e un database locale.

Nelle sezioni seguenti Hello viene codice hello tooworking correlati con hello ambiente Azure, BLOB e code. In questa esercitazione viene illustrato come controller MVC toocreate e utilizzare lo scaffolding di visualizzazioni, come toowrite codice di Entity Framework che funziona con i database di SQL Server, o elementi fondamentali di hello della programmazione asincrona in ASP.NET 4.5. Per informazioni su questi argomenti, vedere hello seguenti risorse:

* [Introduzione a MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Introduzione a EF 6 e MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Programmazione tooasynchronous introduzione in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
file Ad.cs Hello definisce un'enumerazione per le categorie di Active Directory e una classe di entità POCO per informazioni di Active Directory.

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
classe ContosoAdsContext Hello specifica classe annuncio hello viene utilizzato in una raccolta di DbSet, Entity Framework verranno archiviati in un database SQL.

```csharp
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
```

classe Hello dispone di due costruttori. Hello primo di essi viene utilizzato dal progetto web hello e specifica il nome di hello di una stringa di connessione che viene archiviato nel file Web. config hello. costruttore secondo Hello consente toopass nella stringa di connessione effettiva hello utilizzato dal progetto di ruolo di lavoro hello, poiché non dispone di un file Web. config. Illustrato in precedenza in questa stringa di connessione è stata archiviata e verrà visualizzato in un secondo momento come codice hello recupera la stringa di connessione hello quando viene creata un'istanza di classe DbContext hello.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Codice che viene chiamato da hello `Application_Start` metodo crea un *immagini* contenitore blob e un *immagini* coda se non sono già presenti. In questo modo si garantisce che ogni volta che si inizi con un nuovo account di archiviazione, o utilizzando l'emulatore di archiviazione hello in un nuovo computer, coda e il contenitore blob necessari hello verrà creati automaticamente.

Hello account di archiviazione toohello di accesso di codice ottiene tramite la stringa di connessione di archiviazione hello da hello *cscfg* file.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

Viene quindi ottenuto un riferimento toohello *immagini* contenitore blob, crea hello contenitore se non esiste già, e imposta le autorizzazioni per il nuovo contenitore di hello di accesso. Per impostazione predefinita, nuovi contenitori consentono solo client con account di archiviazione BLOB tooaccess credenziali. sito Web di Hello deve hello BLOB toobe pubblico in modo da poter visualizzare immagini con URL che BLOB immagine toohello punto.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

Codice simile Ottiene un riferimento toohello *immagini* coda e crea una nuova coda. In questo caso non sono necessarie modifiche alle autorizzazioni.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - \_Layout.cshtml
Hello *layout. cshtml* file imposta nome di app hello nell'intestazione di hello e piè di pagina e viene creata una voce di menu "Annunci".

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hello *Views\Home\Index.cshtml* file vengono visualizzati i collegamenti di categoria nella home page di hello. collegamenti Hello passare hello integer di hello `Category` enum in una pagina di indice di annunci toohello variabile di stringa di query.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
In hello *AdController.cs* file, hello costruttore chiamate hello `InitializeStorage` gli oggetti di Azure Storage Client Library toocreate metodo che forniscono un'API per l'utilizzo di BLOB e code.

Quindi codice hello Ottiene un riferimento toohello *immagini* blob contenitore, come illustrato in precedenza nella *Global.asax.cs*. Durante questa operazione, imposta un [criterio per l'esecuzione di nuovi tentativi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) predefinito appropriato per un'app Web. criteri di ripetizione di backoff esponenziale predefiniti Hello potrebbe bloccarsi hello web app per più di un minuto ripetuti tentativi per un errore temporaneo. criteri di ripetizione Hello specificato qui attende 3 secondi dopo ogni cercare i tentativi di toothree.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Codice simile Ottiene un riferimento toohello *immagini* coda.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

La maggior parte del codice del controller hello è tipico per l'utilizzo di un modello di dati di Entity Framework utilizzando una classe DbContext. Un'eccezione è hello HttpPost `Create` metodo, che consente di caricare un file e lo salva nell'archiviazione blob. Raccoglitore di modelli Hello offre un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello metodo dell'oggetto.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Se l'utente hello selezionato tooupload un file, codice hello Carica file hello, viene salvato in un blob e aggiorna i record di database di Active Directory hello con un URL che punta toohello blob.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Hello codice hello caricamento è in hello `UploadAndSaveBlobAsync` metodo. Crea un nome GUID per il blob hello, caricamenti e Salva il file di hello e restituisce un blob di riferimento toohello salvato.

```csharp
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
```

Dopo aver hello HttpPost `Create` metodo carica un blob e aggiornamenti hello database, viene creato un tooinform messaggio della coda il processo di back-end che un'immagine è pronta per l'anteprima tooa di conversione.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

codice per hello HttpPost Hello `Edit` metodo è simile ad eccezione del fatto che se l'utente di hello seleziona un nuovo file di immagine è necessario eliminare tutti i blob che esistono già.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

Hello esempio successivo Mostra codice hello che elimina BLOB quando si elimina un annuncio.

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml
Hello *cshtml* file Visualizza l'anteprima con hello altri dati di Active Directory.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Hello *Details.cshtml* file Visualizza immagine ingrandita hello.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml ed Edit.cshtml
Hello *Create.cshtml* e *Edit.cshtml* file specificano di codifica che consente di hello hello tooget controller `HttpPostedFileBase` oggetto.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

Un `<input>` elemento indica hello browser tooprovide una finestra di dialogo di selezione file.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - Metodo OnStart
ambiente di ruolo di lavoro di Azure Hello chiama hello `OnStart` metodo hello `WorkerRole` classe quando il ruolo di lavoro hello introduzione e chiama hello `Run` metodo quando hello `OnStart` al termine di metodo.

Hello `OnStart` metodo ottiene una stringa di connessione database hello da hello *cscfg* file e lo passa a classe Entity Framework DbContext toohello. provider SQLClient Hello viene utilizzato per impostazione predefinita, in modo che il provider di hello non toobe specificato.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

Successivamente, il metodo hello Ottiene un account di archiviazione toohello di riferimento e Crea coda contenitore blob hello se non sono presenti. codice Hello che è simile toowhat già visto nel ruolo web hello `Application_Start` metodo.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Metodo Run
Hello `Run` metodo viene chiamato quando hello `OnStart` metodo completa le operazioni di inizializzazione. metodo Hello esegue un ciclo infinito che verifica la presenza di nuovi messaggi in coda e li elabora quando vengono ricevuti.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

Dopo ogni iterazione del ciclo di hello, se è stato trovato alcun messaggio di coda, il programma hello rimane inattivo per un secondo. Ciò impedisce che il ruolo di lavoro hello costi eccessivo della CPU tempo e l'archiviazione delle transazioni. Hello Team di consulenza clienti di Microsoft indica una storia su uno sviluppatore che ha dimenticato tooinclude, distribuito tooproduction e sinistra per ferie. Quando si è ottenuto il suo supervisione costano più ferie hello.

Talvolta il contenuto di hello di un messaggio nella coda causa un errore durante l'elaborazione. Si tratta di un *messaggio non elaborabile*, e se appena registrato un errore e riavviare il ciclo di hello, tooprocess è possibile provare all'infinito che il messaggio.  Blocco catch hello include pertanto un se istruzione che controlla toosee quante volte app hello ha tentato tooprocess hello messaggio corrente e se sono trascorsi più di 5 volte, il messaggio hello viene eliminato dalla coda di hello.

`ProcessQueueMessage` è chiamato quando viene trovato un messaggio della coda.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

Questo codice legge l'URL dell'immagine di hello database tooget hello, converte tooa anteprima dell'immagine di hello, Salva anteprima hello in un blob, Aggiorna database hello con URL blob anteprima hello ed elimina il messaggio di coda hello.

> [!NOTE]
> Hello codice hello `ConvertImageToThumbnailJPG` metodo utilizza le classi nello spazio dei nomi System. Drawing hello per motivi di semplicità. Tuttavia, le classi di hello in questo spazio dei nomi sono state progettate per l'uso con Windows Form. Non sono supportate per l'uso in un servizio Windows o ASP.NET. Per altre informazioni sulle opzioni di elaborazione delle immagini, vedere [Generazione dinamica delle immagini](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Informazioni dettagliate sul ridimensionamento delle immagini](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="troubleshooting"></a>Risoluzione dei problemi
Nel caso in cui qualcosa non funziona mentre si stiano seguendo le istruzioni di hello in questa esercitazione, ecco alcuni errori comuni e come tooresolve li.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
Hello `RoleEnvironment` oggetto viene fornito da Azure quando si esegue un'applicazione in Azure o quando si esegue in locale utilizzando l'emulatore di calcolo di Azure hello.  Se questo errore si verifica quando si esegue in locale, assicurarsi di aver impostato come progetto di avvio hello progetto ContosoAdsCloudService hello. Questo imposta hello progetto toorun utilizzando l'emulatore di calcolo di Azure hello.

Una delle operazioni di hello utilizzi dell'applicazione hello hello Azure RoleEnvironment per è tooget hello valori stringa di connessione archiviate in hello *cscfg* file, in modo da un'altra causa dell'eccezione corrente è una stringa di connessione mancante. Verificare che creato impostazione StorageConnectionString hello per i Cloud e locali configurazioni nel progetto ContosoAdsWeb hello e creato entrambe le stringhe di connessione per entrambe le configurazioni nel progetto ContosoAdsWorker hello. Se esegue un **Trova tutti** ricerca per StorageConnectionString nell'intera soluzione hello, si devono visualizzarlo 9 volte nei file di 6.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Impossibile eseguire l'override tooport xxx. Nuova porta con valore inferiore al minimo consentito 8080 per HTTP protocollo
Provare a modificare il numero di porta hello utilizzato dal progetto web hello. Fare clic sul progetto ContosoAdsWeb hello e quindi fare clic su **proprietà**. Fare clic su hello **Web** scheda e quindi modificare il numero di porta hello in hello **Url progetto** impostazione.

Per un'altra alternativa che è possibile risolvere il problema di hello, vedere hello seguente sezione.

### <a name="other-errors-when-running-locally"></a>Altri errori durante l'esecuzione locale
Dal cloud di nuova impostazione predefinita i progetti di servizio utilizzano hello toosimulate express di hello Azure compute emulator ambiente Azure. Si tratta di una versione leggera di emulatore di calcolo completo hello e in alcuni hello condizioni emulatore completo funzionerà versione express hello non.  

toochange hello progetto toouse hello completa dell'emulatore, fare clic sul progetto ContosoAdsCloudService hello e quindi fare clic su **proprietà**. In hello **proprietà** finestra fare clic su hello **Web** scheda e quindi fare clic su hello **emulatore completo utilizzare** pulsante di opzione.

In ordine toorun un'applicazione hello con l'emulatore completo hello, è necessario tooopen Visual Studio con privilegi di amministratore.

## <a name="next-steps"></a>Passaggi successivi
applicazione Contoso annunci Hello è intenzionalmente semplici per un'esercitazione Guida introduttiva. Ad esempio, non implementa [inserimento di dipendenze](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) o hello [repository e un'unità di lavoro modelli](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), non [utilizzare un'interfaccia per la registrazione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), non utilizza [ Migrazioni Code First di Entity Framework](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage dati le modifiche del modello o [resilienza delle connessioni EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) temporaneo toomanage errori di rete e così via.

Ecco alcune applicazioni di esempio di servizio cloud in cui vengono illustrate altre procedure di codifica del mondo reale, elencati dal meno complesso toomore complessi:

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Concettualmente simili tooContoso annunci ma implementa più funzionalità e altre procedure di codifica del mondo reale.
* [Applicazione multilivello di Servizi cloud di Azure con tabelle, code e BLOB](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36). Introduce le tabelle di archiviazione di Azure, nonché i BLOB e le code. Basato su una versione precedente di hello Azure SDK per .NET, richiederà alcuni toowork modifiche con la versione corrente di hello.
* [Nozioni fondamentali su Servizi cloud in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Un esempio completo che illustra una vasta gamma di procedure consigliate, prodotta dal gruppo di Microsoft Patterns and Practices hello.

Per informazioni generali sullo sviluppo per il cloud hello, vedere [creazione di App per Cloud del mondo reale con Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Per un tooAzure video di introduzione archiviazione procedure consigliate e modelli, vedere [archiviazione di Microsoft Azure-novità, le procedure consigliate e modelli](http://channel9.msdn.com/Events/Build/2014/3-628).

Per ulteriori informazioni, vedere hello seguenti risorse:

* [Servizi cloud di Azure - Parte 1: Introduzione](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Come toomanage dei servizi Cloud](cloud-services-how-to-manage.md)
* [Archiviazione di Azure](/documentation/services/storage/)
* [Il provider del servizio toochoose un cloud](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
