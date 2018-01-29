---
title: Introduzione a Servizi cloud di Azure e ASP.NET | Documentazione Microsoft
description: "Informazioni sulla creazione di un app a più livelli con ASP.NET MVC e Azure. L'app viene eseguita in un servizio cloud, con un ruolo Web e un ruolo di lavoro. Usa Entity Framework, il database SQL e le code e i BLOB di archiviazione di Azure."
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
ms.openlocfilehash: f0cdafdb88604b8874a245751246d219e8df3813
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/16/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Introduzione a Servizi cloud di Azure e ASP.NET

## <a name="overview"></a>Panoramica
Questa esercitazione illustra come creare un'applicazione .NET multilivello con un front-end MVC ASP.NET e come distribuirla in un [servizio cloud di Azure](cloud-services-choose-me.md). L'applicazione usa il [database SQL di Azure](http://msdn.microsoft.com/library/azure/ee336279), il [servizio BLOB di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage) e il [Servizio di accodamento di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). È possibile [scaricare il progetto di Visual Studio](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) da MSDN Code Gallery.

Questa esercitazione illustra come compilare ed eseguire localmente l'applicazione, come distribuirla in Azure ed eseguirla nel cloud e come creare un'applicazione completamente nuova. È possibile iniziare creando un'applicazione completamente nuova, quindi eseguire i passaggi relativi a test e distribuzione in un secondo momento, se si preferisce.

## <a name="contoso-ads-application"></a>Applicazione Contoso Ads
Questa applicazione è un BBS pubblicitario. Gli utenti creano un'inserzione tramite l'immissione di testo e il caricamento di un'immagine. Possono visualizzare un elenco di annunci con immagini di anteprima e visualizzare l'immagine con le dimensioni originali quando selezionano un annuncio per vederne i dettagli.

![Elenco di inserzioni](./media/cloud-services-dotnet-get-started/list.png)

L'applicazione usa il [modello di lavoro incentrato sulle code](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) per delegare a un processo back-end il lavoro di creazione delle anteprime, che comporta un utilizzo elevato della CPU.

## <a name="alternative-architecture-websites-and-webjobs"></a>Architettura alternativa: siti Web e processi Web
Questa esercitazione mostra come eseguire front-end e back-end in un servizio cloud di Azure. In alternativa, si può eseguire il front-end in un [sito Web di Azure](/services/web-sites/) e si può usare la funzionalità [Processi Web](http://go.microsoft.com/fwlink/?LinkId=390226), attualmente disponibile in anteprima, per il back-end. Per un'esercitazione che usa Processi Web, vedere [Introduzione all'uso dell'SDK di Processi Web di Azure](https://github.com/Azure/azure-webjobs-sdk/wiki). Per informazioni su come scegliere i servizi ideali per lo scenario specifico, vedere [Confronto tra Siti Web, Servizi cloud e Macchine virtuali di Azure](../app-service/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>Contenuto dell'esercitazione
* Abilitare il sistema per lo sviluppo in Azure installando Azure SDK.
* Creare un progetto di servizio cloud di Visual Studio con un ruolo Web MVC ASP.NET e un ruolo di lavoro.
* Testare il progetto di servizio cloud localmente, tramite l'emulatore di archiviazione di Azure.
* Pubblicare il progetto cloud in un servizio cloud di Azure e testarlo tramite un account di archiviazione di Azure.
* Caricare file e archiviarli nel servizio BLOB di Azure.
* Usare il servizio di accodamento di Azure per la comunicazione tra livelli.

## <a name="prerequisites"></a>Prerequisiti
Nell'esercitazione si presuppone che l'utente abbia familiarità con i [concetti di base relativi ai servizi cloud di Azure](cloud-services-choose-me.md), ad esempio con la terminologia *ruolo Web* e *ruolo di lavoro*.  Si presuppone anche che si sia in grado di usare progetti [MVC ASP.NET](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) o [Web Form](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) in Visual Studio. L'applicazione di esempio usa MVC, ma la maggior parte dell'esercitazione è applicabile anche a Web Form.

È possibile eseguire l'app localmente senza sottoscrizione di Azure, ma sarà necessaria una sottoscrizione per distribuire l'applicazione nel cloud. Se non si dispone di un account, è possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) oppure [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).

Le istruzioni dell'esercitazione sono applicabili ai prodotti seguenti:

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Se uno di questi prodotti non è disponibile, Visual Studio potrà essere installato automaticamente quando si installa Azure SDK.

## <a name="application-architecture"></a>Architettura dell'applicazione
L'app archivia inserzioni pubblicitarie in un database SQL usando Code First di Entity Framework per creare le tabelle e accedere ai dati. Il database archivia due URL per ogni annuncio, uno per l'immagine con dimensioni normali e uno per l'anteprima.

![Tabella di inserzioni](./media/cloud-services-dotnet-get-started/adtable.png)

Quando un utente carica un'immagine, il front-end in esecuzione in un ruolo Web archivia l'immagine in un [BLOB di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), quindi archivia le informazioni sulle inserzioni nel database con un URL che fa riferimento al BLOB. e, al tempo stesso, scrive un messaggio in una coda di Azure. Un processo back-end in esecuzione in un ruolo di lavoro esegue periodicamente il polling della coda alla ricerca di nuovi messaggi. Quando compare un nuovo messaggio, il ruolo di lavoro crea un'anteprima per quell'immagine e aggiorna il campo di database relativo all'URL dell'anteprima per quell'inserzione. Il diagramma seguente mostra l'interazione tra le parti dell'applicazione.

![Architettura di Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-the-completed-solution"></a>Download ed esecuzione della soluzione completata
1. Scaricare e decomprimere la [soluzione completata](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Avviare Visual Studio.
3. Scegliere **Apri progetto** dal menu **File**, passare alla cartella in cui è stata scaricata la soluzione, quindi aprire il file di soluzione.
4. Premere CTRL+MAIUSC+B per compilare la soluzione.

    Per impostazione predefinita, Visual Studio ripristina automaticamente il contenuto del pacchetto NuGet, che non era incluso nel file con estensione *zip* . In caso di mancato ripristino dei pacchetti, installarli manualmente passando alla finestra di dialogo **Gestisci pacchetti NuGet per la soluzione**, quindi facendo clic sul pulsante **Ripristina** in alto a destra.
5. In **Esplora soluzioni** verificare che come progetto di avvio sia selezionato **ContosoAdsCloudService**.
6. Se si usa Visual Studio 2015 o versione successiva, modificare la stringa di connessione di SQL Server nel file *Web.config* dell'applicazione per il progetto ContosoAdsWeb e nel file *ServiceConfiguration.Local.cscfg* per il progetto ContosoAdsCloudService. In ogni caso, cambiare "(localdb)\v11.0" in "(localdb)\MSSQLLocalDB".
7. Premere CTRL+F5 per eseguire l'applicazione.

    Quando si esegue localmente un progetto di servizio cloud, Visual Studio richiama automaticamente l'*emulatore di calcolo* di Azure e l'*emulatore di archiviazione* di Azure. L'emulatore di calcolo usa le risorse del computer per simulare gli ambienti del ruolo Web e del ruolo di lavoro. L'emulatore di archiviazione usa un database [LocalDB di SQL Server Express](http://msdn.microsoft.com/library/hh510202.aspx) per simulare la risorsa di archiviazione cloud di Azure.

    Alla prima esecuzione di un progetto di servizio cloud, per l'avvio degli emulatori sarà necessario circa un minuto. Dopo l'avvio dell'emulatore, nel browser predefinito verrà visualizzata la home page dell'applicazione.

    ![Architettura di Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. Fare clic su **Create an Ad**.
9. Immettere alcuni dati di test e selezionare un'immagine *jpg* da caricare, quindi fare clic su **Create**.

    ![Pagina di creazione](./media/cloud-services-dotnet-get-started/create.png)

    L'app passa alla pagina di indice, ma non mostra alcuna anteprima per la nuova inserzione, poiché l'elaborazione non è stata ancora eseguita.
10. Attendere un attimo, quindi aggiornare la pagina di indice per visualizzare l'anteprima.

     ![Pagina di indice](./media/cloud-services-dotnet-get-started/list.png)
11. Fare clic su **Details** per visualizzare l'immagine con dimensioni normali per l'inserzione.

     ![Pagina dei dettagli](./media/cloud-services-dotnet-get-started/details.png)

L'applicazione è stata eseguita interamente nel computer locale, senza connessione al cloud. L'emulatore di archiviazione archivia i dati di coda e BLOB in un database LocalDB di SQL Server Express e l'applicazione archivia i dati relativi alle inserzioni in un altro database LocalDB. Code First di Entity Framework ha creato automaticamente il database delle inserzioni al primo tentativo di accesso da parte dell'app Web.

Nella sezione seguente la soluzione sarà configurata per usare le risorse cloud di Azure per code, BLOB e per il database dell'applicazione in caso di esecuzione nel cloud. Se si vuole, è possibile continuare l'esecuzione locale usando tuttavia le risorse di archiviazione e database del cloud. È sufficiente impostare le stringhe di connessione, come sarà illustrato in seguito.

## <a name="deploy-the-application-to-azure"></a>Distribuire l'applicazione in Azure
Per eseguire l'applicazione nel cloud, eseguire i passaggi seguenti:

* Creare un servizio cloud di Azure.
* Creare un database SQL di Azure.
* Creare un account di archiviazione di Azure
* Configurare la soluzione per l'uso del database SQL di Azure in caso di esecuzione in Azure.
* Configurare la soluzione per l'uso dell'account di archiviazione di Azure in caso di esecuzione in Azure.
* Distribuire il progetto nel servizio cloud di Azure.

### <a name="create-an-azure-cloud-service"></a>Creazione di un servizio cloud di Azure
Un servizio cloud in Azure è l'ambiente in cui sarà eseguita l'applicazione.

1. Accedere al [portale di Azure](https://portal.azure.com) nel browser.
2. Fare clic su **Nuovo > Calcolo > Servizio cloud**.

3. Nella casella di input Nome DNS immettere un prefisso URL per il servizio cloud.

    L'URL deve essere univoco.  Se il prefisso scelto è già in uso, verrà visualizzato un messaggio di errore.
4. Specificare un nuovo gruppo di risorse per il servizio. Fare clic su **Crea nuovo** e quindi digitare un nome nella casella di input Gruppo di risorse, ad esempio CS_contososadsRG.

5. Scegliere l'area geografica in cui si vuole distribuire l'applicazione.

    Questo campo specifica in quale data center viene ospitato il servizio cloud. Per un'applicazione di produzione, scegliere l'area più vicina ai clienti. Per questa esercitazione, scegliere l'area geografica più vicina alla propria ubicazione.
5. Fare clic su **Crea**.

    L'immagine seguente illustra la creazione di un servizio cloud il cui URL è CSvccontosoads.cloudapp.net.

    ![Nuovo servizio cloud](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Creare un database SQL di Azure
Quando l'app è in esecuzione nel cloud, userà un database basato sul cloud.

1. Nel [portale di Azure](https://portal.azure.com) fare clic su **Nuovo > Database > Database SQL**.
2. Nella casella **Nome database** immettere *contosoads*.
3. In **Gruppo di risorse** fare clic su **Usa esistente** e selezionare il gruppo di risorse usato per il servizio cloud.
4. Nella schermata illustrata di seguito fare clic su **Server - Configurare le impostazioni necessarie** e **Creare un nuovo server**.

    ![Tunnel al server di database](./media/cloud-services-dotnet-get-started/newdb.png)

    In alternativa, se la sottoscrizione è già associata a un server, sarà possibile selezionare quel server dall'elenco a discesa.
5. Nella casella **Nome server** immettere *csvccontosodbserver*.

6. Immettere un **Nome di accesso** e una **Password** per l'amministratore.

    Se si seleziona **Creare un nuovo server** non si immetteranno un nome e una password esistenti in questa casella, ma un nuovo nome e una nuova password definiti in questo momento e da usare in seguito per l'accesso al database. Se è stato selezionato un server creato in precedenza, sarà richiesta la password dell'account utente di amministrazione già creato.
7. Scegliere la stessa **località** selezionata per il servizio cloud.

    Quando il servizio cloud e il database si trovano in data center diversi (aree diverse), la latenza aumenterà e sarà addebitato il costo relativo alla larghezza di banda esterna al data center. La larghezza di banda nell'ambito di un data center è gratuita.
8. Selezionare **Consenti ai servizi di Azure di accedere al server**.
9. Fare clic su **Seleziona** per il nuovo server.

    ![Nuovo server di database SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. Fare clic su **Crea**.

### <a name="create-an-azure-storage-account"></a>Creare un account di archiviazione di Azure
Un account di archiviazione di Azure offre risorse per l'archiviazione di dati di code e BLOB nel cloud.

In un'applicazione effettiva si creano in genere account separati per i dati dell'applicazione rispetto ai dati di registrazione e account separati per i dati di test rispetto ai dati di produzione. In questa esercitazione sarà usato un solo account.

1. Nel [portale di Azure](https://portal.azure.com) fare clic su **Nuovo > Archiviazione > Account di archiviazione: BLOB, File, Tabelle, Code**.
2. Nella casella **Nome** immettere un prefisso URL.

    La combinazione di questo prefisso e del testo visualizzato sotto la casella corrisponderà all'URL univoco dell'account di archiviazione. Se il prefisso immesso è già stato usato, sarà necessario scegliere un prefisso diverso.
3. Impostare **Modello di distribuzione** su *Classica*.

4. Nell'elenco a discesa **Replica** scegliere **Archiviazione con ridondanza locale**.

    Quando per un account di archiviazione è abilitata la replica geografica, il contenuto archiviato viene replicato in un data center secondario per permettere il failover in caso di emergenza grave nella posizione primaria. La replica geografica può comportare costi aggiuntivi. Per gli account di test e di sviluppo si preferisce in genere non pagare per la replica geografica. Per altre informazioni, vedere la pagina relativa alla [creazione, gestione o eliminazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).

5. In **Gruppo di risorse** fare clic su **Usa esistente** e selezionare il gruppo di risorse usato per il servizio cloud.
6. Scegliere dall'elenco a discesa **Località** la stessa area geografica selezionata per il servizio cloud.

    Quando il servizio cloud e l'account di archiviazione si trovano in data center diversi (aree diverse), la latenza aumenterà e verrà addebitato il costo relativo alla larghezza di banda esterna al data center. La larghezza di banda nell'ambito di un data center è gratuita.

    I gruppi di affinità di Azure offrono un meccanismo per ridurre la distanza tra le risorse in un data center e di conseguenza la latenza. In questa esercitazione non vengono utilizzati gruppi di affinità. Per altre informazioni, vedere [Come creare un gruppo di affinità in Azure](http://msdn.microsoft.com/library/jj156209.aspx).
7. Fare clic su **Crea**.

    ![Nuovo account di archiviazione](./media/cloud-services-dotnet-get-started/newstorage.png)

    La seguente figura illustra la creazione di un account di archiviazione con l'URL `csvccontosoads.core.windows.net`.

### <a name="configure-the-solution-to-use-your-azure-sql-database-when-it-runs-in-azure"></a>Configurare la soluzione per l'uso del database SQL di Azure in caso di esecuzione in Azure
Il progetto Web e il progetto ruolo di lavoro dispongono di una stringa di connessione di database specifica e quando l'app è in esecuzione in Azure ogni progetto deve fare riferimento al database SQL di Azure.

Sarà necessario usare una [trasformazione Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) per il ruolo Web e un'impostazione dell'ambiente del servizio cloud per il ruolo di lavoro.

> [!NOTE]
> In questa sezione e nella sezione successiva, le credenziali vengono archiviate in file di progetto. [Non archiviare dati sensibili in archivi pubblici di codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).
>
>

1. Nel progetto ContosoAdsWeb aprire il file di trasformazione *Web.Release.config* per il file *Web.config* dell'applicazione, eliminare il blocco di commento che include un elemento `<connectionStrings>` e sostituirlo incollando il codice seguente.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Lasciare aperto il file per la modifica.
2. Nel [portale di Azure](https://portal.azure.com) fare clic su **Database SQL** nel riquadro sinistro, selezionare il database creato per l'esercitazione, quindi fare clic su **Mostra stringhe di connessione**.

    ![Mostra stringhe di connessione](./media/cloud-services-dotnet-get-started/showcs.png)

    Il portale visualizza le stringhe di connessione, con un segnaposto per la password.

    ![Stringhe di connessione](./media/cloud-services-dotnet-get-started/connstrings.png)
3. Nel file di trasformazione *Web.Release.config* eliminare `{connectionstring}` e incollare al suo posto la stringa di connessione ADO.NET dal portale di Azure.
4. Nella stringa di connessione incollata nel file di trasformazione *Web.Release.config* sostituire `{your_password_here}` con la password creata per il nuovo database SQL.
5. Salvare il file.  
6. Selezionare e copiare la stringa di connessione, senza le virgolette tra cui è racchiusa, per usarla nei passaggi seguenti per la configurazione del progetto di ruolo di lavoro.
7. In **Esplora soluzioni**, in **Ruoli** nel progetto di servizio cloud fare clic con il pulsante destro del mouse su **ContosoAdsWorker**, quindi scegliere **Proprietà**.

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Fare clic sulla scheda **Impostazioni** .
9. Impostare **Configurazione servizio** su **Cloud**.
10. Selezionare il campo **Valore** per l'impostazione `ContosoAdsDbConnectionString` e quindi incollare la stringa di connessione copiata dalla sezione precedente dell'esercitazione.

     ![Stringa di connessione del database per il ruolo di lavoro](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Salvare le modifiche.  

### <a name="configure-the-solution-to-use-your-azure-storage-account-when-it-runs-in-azure"></a>Configurare la soluzione per l'uso dell'account di archiviazione di Azure in caso di esecuzione in Azure
Le stringhe di connessione per l'account di archiviazione di Azure per il progetto ruolo Web e il progetto ruolo di lavoro sono archiviate nelle impostazioni di ambiente nel progetto di servizio cloud. Per ogni progetto è disponibile un insieme di impostazioni distinto da usare quando l'applicazione viene eseguita localmente e nel cloud. Saranno aggiornate le impostazioni di ambiente cloud per i progetti di ruolo Web e di ruolo di lavoro.

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **ContosoAdsWeb** nella sezione **Ruoli** del progetto **ContosoAdsCloudService**, quindi scegliere **Proprietà**.

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Fare clic sulla scheda **Impostazioni** . Nella casella di riepilogo **Configurazione servizio** selezionare **Cloud**.

    ![Configurazione del cloud](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Se si seleziona la voce **StorageConnectionString**, verrà visualizzato un pulsante con puntini di sospensione (**...**) all'estremità destra della riga. Fare clic su tale pulsante per aprire la finestra di dialogo **Crea Stringa di connessione all'account di archiviazione** .

    ![Casella di creazione della stringa di connessione](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. Nella finestra di dialogo **Crea stringa di connessione a risorsa di archiviazione** fare clic su **Sottoscrizione** scegliere l'account di archiviazione creato in precedenza, quindi fare clic su **OK**. Se non è già stato effettuato l'accesso, saranno richieste le credenziali dell'account di Azure.

    ![Crea Stringa di connessione di archiviazione](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Salvare le modifiche.
6. Eseguire la stessa procedura usata per la stringa di connessione `StorageConnectionString` per impostare la stringa di connessione `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString`.

    Questa stringa di connessione è usata per la registrazione.
7. Eseguire la stessa procedura usata per il ruolo **ContosoAdsWeb** per impostare entrambe le stringhe di connessione per il ruolo **ContosoAdsWorker**. Ricordarsi di impostare **Configurazione servizio** su **Cloud**.

Le impostazioni dell'ambiente di ruolo configurate tramite l'interfaccia utente di Visual Studio sono archiviate nei seguenti file del progetto ContosoAdsCloudService:

* *ServiceDefinition.csdef* : definisce i nomi delle impostazioni.
* *ServiceConfiguration.Cloud.cscfg* : fornisce valori per l'esecuzione dell'app nel cloud.
* *ServiceConfiguration.Local.cscfg* : fornisce valori per l'esecuzione locale dell'app.

Il file ServiceDefinition.csdef include ad esempio le definizioni seguenti:

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

E il file *ServiceConfiguration.Cloud.cscfg* include i valori immessi per queste impostazioni in Visual Studio.

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

L'impostazione `<Instances>` specifica il numero di macchine virtuali in cui Azure eseguirà il codice del ruolo di lavoro. La sezione [Passaggi successivi](#next-steps) include collegamenti ad altre informazioni sulla scalabilità orizzontale di un servizio cloud,

### <a name="deploy-the-project-to-azure"></a>Distribuire il progetto in Azure
1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto cloud **ContosoAdsCloudService**, quindi scegliere **Pubblica**.

   ![Menu Pubblica](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. Nel passaggio **Accedi** della procedura guidata **Pubblica applicazione Azure** fare clic su **Avanti**.

    ![Passaggio Accedi](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. Nel passaggio **Impostazioni** della procedura guidata, fare clic su **Avanti**.

    ![Passaggio Impostazioni](./media/cloud-services-dotnet-get-started/pubsettings.png)

    Le impostazioni predefinite della scheda **Advanced** sono corrette per questa esercitazione. Per informazioni sulla scheda Avanzate, vedere [Procedura guidata Pubblica l'applicazione Azure](http://msdn.microsoft.com/library/hh535756.aspx).
4. Nel passaggio **Riepilogo** fare clic su **Pubblica**.

    ![Passaggio Riepilogo](./media/cloud-services-dotnet-get-started/pubsummary.png)

   La finestra **Log attività di Azure** sarà aperta in Visual Studio.
5. Fare clic sull'icona della freccia verso destra per espandere i dettagli della distribuzione.

    Il completamento della distribuzione richiede fino a 5 minuti.

    ![Finestra Log attività di Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. Quando lo stato della distribuzione è completato, fare clic sull' **URL dell'app Web** per avviare l'applicazione.
7. È ora possibile testare l'applicazione creando, visualizzando e modificando alcune inserzioni, esattamente come durante l'esecuzione locale dell'applicazione.

> [!NOTE]
> Al termine dei test, eliminare o arrestare il servizio cloud. Anche se non lo si usa, il servizio cloud accumulerà addebiti, poiché le risorse delle macchine virtuali sono riservate per il servizio. Se lo si lascia in esecuzione, chiunque individui l'URL potrà creare e visualizzare inserzioni. Nel [portale di Azure](https://portal.azure.com) passare alla scheda **Panoramica** per il servizio cloud, quindi fare clic sul pulsante **Elimina** nella parte superiore della pagina. Se si vuole semplicemente impedire ad altri utenti di accedere al sito, fare invece clic su **Arresta** . In questo caso, continueranno a essere generati addebiti. È possibile eseguire una procedura analoga per eliminare il database SQL e l'account di archiviazione quando non sono più necessari.
>
>

## <a name="create-the-application-from-scratch"></a>Creazione di un'applicazione completamente nuova
Se non è stata ancora scaricata l' [applicazione completa](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), scaricarla ora. I file del progetto scaricato saranno copiati nel nuovo progetto.

Per creare l'applicazione Contoso Ads sono necessari i passaggi seguenti:

* Creare una soluzione servizio cloud di Visual Studio.
* Aggiornare e aggiungere pacchetti NuGet.
* Impostare i riferimenti al progetto.
* Configurare le stringhe di connessione.
* Aggiungere file di codice.

Dopo la creazione della soluzione, esaminare il codice univoco per i progetti di servizio cloud e per i BLOB e le code di Azure.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Creare una soluzione servizio cloud di Visual Studio
1. In Visual Studio scegliere **Nuovo progetto** from the **File** .
2. Nel riquadro sinistro della finestra di dialogo **Nuovo progetto** espandere **Visual C#**, scegliere i modelli **Cloud**, quindi selezionare il modello **Servizio cloud di Azure**.
3. Assegnare al progetto e alla soluzione il nome ContosoAdsCloudService, quindi fare clic su **OK**.

    ![Nuovo progetto](./media/cloud-services-dotnet-get-started/newproject.png)
4. Nella finestra di dialogo **Nuovo servizio cloud Azure** aggiungere un ruolo Web e un ruolo di lavoro. Assegnare il nome ContosoAdsWeb al ruolo Web e il nome ContosoAdsWorker al ruolo di lavoro. Usare l'icona a forma di matita nel riquadro di destra per modificare i nomi predefiniti dei ruoli.

    ![Nuovo progetto di servizio cloud](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Quando appare la finestra di dialogo **Nuovo progetto ASP.NET** per il ruolo Web, scegliere il modello MVC, quindi fare clic su **Modifica autenticazione**.

    ![Modifica autenticazione](./media/cloud-services-dotnet-get-started/chgauth.png)
6. Nella finestra di dialogo **Modifica autenticazione** fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**.

    ![No Authentication](./media/cloud-services-dotnet-get-started/noauth.png)
7. Nella finestra di dialogo **Nuovo progetto ASP.NET** fare clic su **OK**.
8. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla soluzione, non su uno dei progetti, quindi scegliere **Aggiungi - Nuovo progetto**.
9. Nella finestra di dialogo **Aggiungi nuovo progetto** scegliere **Windows** in **Visual C#** nel riquadro sinistro e quindi fare clic sul modello **Libreria di classi**.  
10. Assegnare il nome *ContosoAdsCommon*al progetto, quindi fare clic su **OK**.

    È necessario che i progetti di ruolo Web e di ruolo di lavoro facciano riferimento al contesto e al modello di dati di Entity Framework. In alternativa, è possibile definire le classi correlate a Entity Framework nel progetto di ruolo Web e fare riferimento a tale progetto dal progetto di ruolo di lavoro. Nell'approccio alternativo, tuttavia, il progetto di ruolo di lavoro includerebbe un riferimento ad assembly Web non necessari.

### <a name="update-and-add-nuget-packages"></a>Aggiornare e aggiungere pacchetti NuGet
1. Aprire la finestra di dialogo **Gestisci pacchetti NuGet** per la soluzione.
2. Nella parte superiore della finestra selezionare **Aggiornamenti**.
3. Cercare il pacchetto *WindowsAzure.Storage*. Se è incluso nell'elenco, selezionarlo e selezionare i progetti Web e di lavoro in cui aggiornarlo e quindi fare clic su **Aggiorna**.

    La libreria del client di archiviazione viene aggiornata con frequenza maggiore rispetto ai modelli di progetto di Visual Studio. È quindi possibile che la versione disponibile in un progetto appena creato debba essere aggiornata.
4. Nella parte superiore della finestra selezionare **Sfoglia**.
5. Individuare il pacchetto NuGet *EntityFramework* e installarlo nei tre progetti.
6. Trovare il pacchetto NuGet *Microsoft.WindowsAzure.ConfigurationManager* e installarlo nel progetto del ruolo di lavoro.

### <a name="set-project-references"></a>Configurare le preferenze del progetto
1. Nel progetto ContosoAdsWeb configurare un riferimento al progetto ContosoAdsCommon. Fare clic con il pulsante destro del mouse sul progetto ContosoAdsWeb, quindi scegliere **Riferimenti** - **Aggiungi riferimenti**. Nella finestra di dialogo **Gestione riferimenti** selezionare **Soluzione - Progetti** nel riquadro di sinistra, selezionare **ContosoAdsCommon**, quindi fare clic su **OK**.
2. Nel progetto ContosoAdsWorker configurare un riferimento al progetto ContosoAdsCommon.

    ContosoAdsCommon includerà il modello di dati e la classe contesto di Entity Framework, che saranno usati dal front-end e dal back-end.
3. Nel progetto ContosoAdsWorker configurare un riferimento a `System.Drawing`.

    Questo assembly è usato dal back-end per convertire le immagini in anteprime.

### <a name="configure-connection-strings"></a>Configurare le stringhe di connessione
In questa sezione verranno configurate le stringhe di connessione di Archiviazione di Azure e SQL per il test in locale. Le istruzioni di distribuzione disponibili in precedenza in questa esercitazione illustrano come configurare le stringhe di connessione per l'esecuzione dell'app nel cloud.

1. Nel progetto ContosoAdsWeb aprire il file Web.config dell'applicazione e inserire il seguente elemento `connectionStrings` dopo l'elemento `configSections`.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Se si usa Visual Studio 2015 o versione successiva, sostituire "v11.0" con "MSSQLLocalDB".
2. Salvare le modifiche.
3. Nel progetto ContosoAdsCloudService fare clic con il pulsante destro del mouse su ContosoAdsWeb in **Ruoli**, quindi scegliere **Proprietà**.

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. Nella finestra delle proprietà di **ContosAdsWeb [Role]** fare clic sulla scheda **Impostazioni**, quindi su **Aggiungi impostazione**.

    Lasciare l'opzione **Configurazione servizio** impostata su **Tutte le configurazioni**.
5. Aggiungere un'impostazione denominata *StorageConnectionString*. Impostare il **Tipo** su *ConnectionString*, quindi impostare il **Valore** su *UseDevelopmentStorage=true*.

    ![Nuova stringa di connessione](./media/cloud-services-dotnet-get-started/scall.png)
6. Salvare le modifiche.
7. Eseguire la stessa procedura per aggiungere una stringa di connessione di archiviazione nelle proprietà del ruolo ContosoAdsWorker.
8. Nella finestra delle proprietà di **ContosoAdsWorker [Ruolo]** aggiungere un'altra stringa di connessione:

   * Nome: ContosoAdsDbConnectionString
   * Tipo: String
   * Valore: incollare la stessa stringa di connessione usata per il progetto di ruolo Web. L'esempio seguente si riferisce a Visual Studio 2013, quindi se si copia questo esempio e si usa Visual Studio 2015 o versione successiva è necessario modificare l'origine dati.

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Aggiungere file di codice
In questa sezione, i file di codice saranno copiati dalla soluzione scaricata alla nuova soluzione. Le sezioni seguenti illustrano e spiegano parti chiave del codice.

Per aggiungere file a un progetto o a una cartella, fare clic con il pulsante destro del mouse sul progetto o sulla cartella, quindi scegliere **Aggiungi** - **Elemento esistente**. Selezionare i file da aggiungere, quindi fare clic su **Aggiungi**. Se viene richiesto di confermare che si vogliono sostituire i file esistenti, fare clic su **Sì**.

1. Nel progetto ContosoAdsCommon eliminare il file *Class1.cs* e sostituirlo con i file *Ad.cs* e *ContosoAdscontext.cs* dal progetto scaricato.
2. Nel progetto ContosoAdsWeb aggiungere i file seguenti dal progetto scaricato.

   * *Global.asax.cs*.  
   * Nella cartella *Views\Shared*: *\_Layout.cshtml*.
   * Nella cartella *Views\Home*: *Index.cshtml*.
   * Nella cartella *Controllers*: *AdController.cs*.
   * Nella cartella *Views\Ad* (creare prima di tutto la cartella): cinque file *.cshtml*.
3. Nel progetto ContosoAdsWorker aggiungere il file *WorkerRole.cs* dal progetto scaricato.

È ora possibile compilare ed eseguire l'applicazione come indicato in precedenza nell'organizzazione e l'app userà le risorse locali del database e dell'emulatore di archiviazione.

Le sezioni seguenti illustrano il codice correlato all'uso dell'ambiente, dei BLOB e delle code di Azure. Questa esercitazione non spiega come creare controlli e visualizzazioni MVC usando lo scaffolding, come scrivere codice di Entity Framework da usare con database SQL Server oppure le nozioni di base della programmazione asincrona in ASP.NET 4.5. Per informazioni su questi argomenti, vedere le risorse seguenti:

* [Introduzione a MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Introduzione a EF 6 e MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Introduzione alla programmazione asincrona in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
Il file Ad.cs definisce un'enumerazione per le categorie di inserzione e una classe di entità POCO per le informazioni sulle inserzioni.

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
La classe ContosoAdsContext specifica che la classe Ad è usata in una raccolta DbSet, che sarà archiviata da Entity Framework in un database SQL.

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

La classe ha due costruttori. Il primo è usato dal progetto Web e specifica il nome di una stringa di connessione archiviata nel file Web.config. Il secondo costruttore permette di passare la stringa di connessione effettiva usata dal progetto di ruolo di lavoro, non avendo questo un file Web.config. In precedenza è stato indicato il percorso di archiviazione di questa stringa di connessione e più avanti sarà illustrato il modo in cui il codice recupera la stringa di connessione durante la creazione di istanze della classe DbContext.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Il codice chiamato dal metodo `Application_Start` crea un contenitore BLOB *images* e una coda *images*, se non esistono già. In questo modo, ogni volta che si inizia a usare un nuovo account di archiviazione o a usare l'emulatore di archiviazione in un nuovo computer, il contenitore BLOB e la coda necessari saranno creati automaticamente.

Il codice ottiene l'accesso all'account di archiviazione tramite la stringa di connessione del file *.cscfg* .

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

Ottiene quindi un riferimento al contenitore BLOB *images* , crea il contenitore se non esiste già e configura le autorizzazioni di accesso nel nuovo contenitore. Per impostazione predefinita, i nuovi contenitori permettono l'accesso ai BLOB solo ai client con credenziali dell'account di archiviazione. Per il sito Web è necessario che i BLOB siano pubblici, in modo che sia possibile visualizzare immagini usando gli URL che fanno riferimento ai BLOB delle immagini.

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

Tramite codice analogo si ottiene un riferimento alla coda *images* e si crea una nuova coda. In questo caso non sono necessarie modifiche alle autorizzazioni.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - \_Layout.cshtml
Il file *_Layout.cshtml* imposta il nome dell'app nell'intestazione e nel piè di pagina e crea una voce di menu "Ads" (Annunci).

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Il file *Views\Home\Index.cshtml* visualizza i collegamenti di categoria nella home page. I collegamenti passano il valore Integer dell'enumerazione `Category` in una variabile querystring alla pagina Ads Index.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Nel file *AdController.cs* il costruttore chiama il metodo `InitializeStorage` per creare oggetti della libreria del client di Archiviazione di Azure che forniscono un'API per l'uso di BLOB e code.

Il codice ottiene quindi un riferimento al contenitore BLOB *images*, come illustrato in precedenza in *Global.asax.cs*. Durante questa operazione, imposta un [criterio per l'esecuzione di nuovi tentativi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) predefinito appropriato per un'app Web. Il criterio per l'esecuzione di nuovi tentativi predefinito per il backoff esponenziale potrebbe sospendere l'app Web per più di un minuto in caso di nuovi tentativi ripetuti per un errore temporaneo. Il criterio di ripetizione dei tentativi specificato qui attende tre secondi dopo ogni tentativo, fino a un massimo di tre tentativi.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Tramite codice analogo si ottiene un riferimento alla coda *images* .

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

La maggior parte del codice del controller è tipica per l'uso di un modello di dati Entity Framework con una classe DbContext. Un'eccezione è costituita dal metodo `Create` HttpPost che carica un file e lo salva nell'archiviazione BLOB. Lo strumento di associazione di modelli fornisce un oggetto [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) al metodo.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Se l'utente ha selezionato un file da caricare, il codice carica il file, lo salva in un BLOB e aggiorna il record del database Ad con un URL che fa riferimento al BLOB.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Il codice che esegue il caricamento si trova nel metodo `UploadAndSaveBlobAsync` . Crea un nome GUID per il BLOB, aggiorna e salva il file, quindi restituisce un riferimento al BLOB salvato.

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

Dopo aver caricato un BLOB e aggiornato il database, il metodo `Create` HttpPost crea un messaggio di coda per segnalare al processo back-end che un'immagine è pronta per la conversione in anteprima.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

Il codice per il metodo `Edit` HttpPost è simile, con la differenza che se l'utente seleziona un nuovo file immagine, sarà necessario eliminare eventuali BLOB già esistenti.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

L’esempio successivo riporta il codice per l'eliminazione dei BLOB in caso di eliminazione di un'inserzione.

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
Il file *Index.cshtml* mostra le anteprime insieme agli altri dati delle inserzioni.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Il file *Details.cshtml* mostra l'immagine con dimensioni normali.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml ed Edit.cshtml
I file *Create.cshtml* e *Edit.cshtml* specificano la codifica di moduli che permette al controller di ottenere l'oggetto `HttpPostedFileBase`.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

Un elemento `<input>` segnala al browser che è necessario fornire una finestra di selezione del file.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - Metodo OnStart
L'ambiente del ruolo di lavoro di Azure chiama il metodo `OnStart` nella classe `WorkerRole` durante la fase di avvio del ruolo di lavoro e chiama il metodo `Run` al termine dell'esecuzione del metodo `OnStart`.

Il metodo `OnStart` ottiene la stringa di connessione del database dal file con estensione *cscfg* e la passa alla classe DbContext di Entity Framework. Per impostazione predefinita, sarà usato il provider SQLClient. Non è quindi necessario specificare alcun provider.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

In seguito, il metodo ottiene un riferimento all'account di archiviazione e crea il contenitore BLOB e la coda, se non esistono già. Il codice da usare è simile a quello già usato per il metodo `Application_Start` del ruolo Web.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Metodo Run
Il metodo `Run` è chiamato al termine del processo di inizializzazione del metodo `OnStart`. Il metodo esegue un ciclo infinito che cerca nuovi messaggi di coda e li elabora quando arrivano.

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

Dopo ogni iterazione del ciclo, se non sono stati trovati messaggi di coda, il programma rimane inattivo per un secondo. Ciò impedisce al ruolo di lavoro di generare costi eccessivi relativi al tempo della CPU e alle transazioni di archiviazione. Come ricordato da Microsoft Customer Advisory Team, uno sviluppatore aveva scordato di includere questo dettaglio, aveva eseguito la distribuzione in produzione ed era partito per le ferie. Al ritorno, si era reso conto che la dimenticanza era costata più cara delle ferie.

A volte il contenuto di un messaggio di coda provoca un errore di elaborazione. Questo messaggio è definito un *messaggio non elaborabile*. Se è stato appena registrato un errore e il ciclo è stato riavviato, è possibile che si tenti di elaborare questo messaggio all'infinito.  Il blocco CATCH include quindi un'istruzione IF che verifica il numero di volte in cui l'app ha tentato di elaborare il messaggio corrente. Se il numero è superiore a 5, il messaggio sarà eliminato dalla coda.

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

Questo codice legge il database per ottenere l'URL dell'immagine. converte l'immagine in un'anteprima, salva l'anteprima in un BLOB, aggiorna il database con l'URL del BLOB dell'anteprima ed elimina il messaggio in coda.

> [!NOTE]
> Il codice nel metodo `ConvertImageToThumbnailJPG` usa le classi disponibili nello spazio dei nomi System.Drawing per maggiore semplicità. Le classi in questo spazio dei nomi, tuttavia, sono state progettate per l'uso con Windows Form. Non sono supportate per l'uso in un servizio Windows o ASP.NET. Per altre informazioni sulle opzioni di elaborazione delle immagini, vedere [Generazione dinamica delle immagini](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Informazioni dettagliate sul ridimensionamento delle immagini](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="troubleshooting"></a>Risoluzione dei problemi
In caso di problemi durante l'esecuzione delle istruzioni di questa esercitazione, di seguito sono indicati alcuni errori comuni e le relative soluzioni.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
L'oggetto `RoleEnvironment` è fornito da Azure quando si esegue un'applicazione in Azure o in caso di esecuzione in modalità locale tramite l'emulatore di calcolo di Azure.  Se questo errore è visualizzato durante l'esecuzione locale, assicurarsi di avere impostato il progetto ContosoAdsCloudService come progetto di avvio. In questo modo, il progetto sarà configurato per l'esecuzione con l'emulatore di calcolo di Azure.

L'applicazione usa RoleEnvironment di Azure anche per ottenere i valori delle stringhe di connessione archiviati nei file con estensione *cscfg*. È quindi possibile che questa eccezione sia generata da una stringa di connessione mancante. Assicurarsi di avere creato l'impostazione StorageConnectionString per entrambe le configurazioni, cloud e locale, nel progetto ContosoAdsWeb e di avere creato entrambe le stringhe di connessione per entrambe le configurazioni nel progetto ContosoAdsWorker. Se si esegue una ricerca di tipo **Trova tutto** per StorageConnectionString nell'intera soluzione, dovrebbero essere rilevate 9 occorrenze in 6 file.

### <a name="cannot-override-to-port-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Non è possibile eseguire l'override sulla porta xxx. Nuova porta con valore inferiore al minimo consentito 8080 per HTTP protocollo
Provare a cambiare il numero di porta usato dal progetto Web. Fare clic con il pulsante destro del mouse sul progetto ContosoAdsWeb, quindi scegliere **Proprietà**. Fare clic sulla scheda **Web**, quindi cambiare il numero di porta nell'impostazione **URL progetto**.

Per un'altra soluzione alternativa che potrebbe risolvere il problema, vedere la sezione successiva.

### <a name="other-errors-when-running-locally"></a>Altri errori durante l'esecuzione locale
Per impostazione predefinita, i nuovi progetti di servizio cloud usano l'emulatore di calcolo rapido di Azure per simulare l'ambiente di Azure. Si tratta di una versione semplificata dell'emulatore di calcolo e in alcuni casi l'emulatore di calcolo completo funzionerà mentre la versione rapida non funzionerà.  

Per modificare il progetto in modo che usi l'emulatore completo, fare clic con il pulsante destro del mouse sul progetto ContosoAdsCloudService, quindi scegliere **Proprietà**. Nella finestra **Proprietà** fare clic sulla scheda **Web**, quindi selezionare il pulsante di opzione **Usa emulatore completo**.

Per eseguire l'applicazione con l'emulatore completo, sarà necessario aprire Visual Studio con privilegi di amministratore.

## <a name="next-steps"></a>Passaggi successivi
L'applicazione Contoso Ads è intenzionalmente semplice, in modo da essere idonea per un'esercitazione introduttiva. Ad esempio, non implementa l'[inserimento di dipendenze](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) o i [modelli di archivio e unità di lavoro](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), non usa un'[interfaccia per l'elaborazione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), non usa [migrazioni Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) per gestire le modifiche ai modelli di dati o la [resilienza di connessione EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) per gestire gli errori di rete temporanei e così via.

Di seguito sono indicate alcune applicazioni di esempio per servizi cloud che illustrano procedure di codifica più simili a quelle del mondo reale, elencate in ordine di complessità crescente:

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Concettualmente simile a Contoso Ads, implementa però più funzionalità e procedure più simili a quelle del mondo reale.
* [Applicazione multilivello di Servizi cloud di Azure con tabelle, code e BLOB](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36). Introduce le tabelle di archiviazione di Azure, nonché i BLOB e le code. Basata su una versione precedente di Azure SDK per .NET, richiederà alcune modifiche per funzionare con la versione corrente.
* [Nozioni fondamentali su Servizi cloud in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Un esempio completo che illustra una vasta gamma di procedure consigliate, creato dal gruppo Microsoft Patterns and Practices.

Per informazioni generali sullo sviluppo per il cloud, vedere l'articolo relativo alla [creazione di applicazioni cloud funzionanti con Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Per un video introduttivo relativo alle procedure consigliate e ai modelli per Archiviazione di Azure, vedere il video relativo a [novità, procedure consigliate e modelli per Archiviazione di Microsoft Azure](http://channel9.msdn.com/Events/Build/2014/3-628).

Per altre informazioni, vedere le seguenti risorse:

* [Servizi cloud di Azure - Parte 1: Introduzione](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Come gestire i servizi cloud](cloud-services-how-to-manage-portal.md)
* [Archiviazione di Azure](/documentation/services/storage/)
* [Come scegliere un provider di servizi cloud](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
