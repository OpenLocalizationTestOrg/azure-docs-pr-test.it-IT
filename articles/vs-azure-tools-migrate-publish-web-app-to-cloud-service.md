---
title: aaaHow tooMigrate e pubblicare un'applicazione Web di tooan del servizio Cloud Azure da Visual Studio | Documenti Microsoft
description: Informazioni su come toomigrate e pubblicare il tooan di applicazione web del servizio cloud di Azure tramite Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Procedura: eseguire la migrazione e pubblicare un servizio Cloud di Azure da Visual Studio di tooan applicazione Web
sfruttare tootake hello in servizi di hosting e la scalabilità di Azure, si potrebbe essere necessario toomigrate e pubblicare il servizio di cloud di Azure tooan applicazione web. È possibile eseguire un'applicazione web in Azure con l'applicazione di modifiche minime tooyour esistente.

> [!NOTE]
> In questo argomento riguarda la distribuzione di servizi toocloud, non tooweb siti. Per informazioni sulla distribuzione di siti tooweb, vedere [distribuire un'app web in Azure App Service](app-service-web/web-sites-deploy.md).
>
>

Per un elenco di modelli specifici supportati per Visual c# e Visual Basic, vedere la sezione hello **modelli di progetto supportati** più avanti in questo argomento.

È innanzitutto necessario abilitare l'applicazione Web per Azure da Visual Studio. Hello seguente illustrazione mostra hello i passaggi principali toopublish l'applicazione web esistente aggiungendo un toouse progetto Azure per la distribuzione. Questo processo aggiunge un progetto Azure con una soluzione tooyour ruolo web hello necessario. Basato sul tipo hello del progetto web che è necessario, le proprietà del progetto hello per gli assembly vengono aggiornate anche se il pacchetto del servizio hello richiede ulteriori assembly per la distribuzione.

![Pubblicare un tooMicrosoft di applicazione Web Azure](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Hello **convertire**, **convertire il progetto servizio Cloud tooAzure** comando viene visualizzato solo per il progetto web hello nella soluzione. Comando hello, ad esempio, non è disponibile per un progetto Silverlight nella soluzione.
> Quando si crea un pacchetto del servizio o si pubblica l'applicazione tooAzure, potrebbero verificarsi avvisi o errori. Questi avvisi ed errori possono aiutare a risolvere i problemi prima di distribuire tooAzure. Ad esempio, si potrebbe ricevere un avviso relativo a un assembly mancante. Per ulteriori informazioni su come tootreat gli avvisi come errori, vedere [configurare un progetto di servizio Cloud di Azure con Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Se si compila l'applicazione, eseguirla localmente utilizzando l'emulatore di calcolo hello o pubblicarla tooAzure, è possibile visualizzare il seguente errore in hello hello **elenco errori** finestra: **hello specificato percorso, il nome di file, o entrambi sono troppo lunghi** . Questo errore si verifica perché hello del nome completo del progetto Azure hello è troppo lungo. lunghezza Hello del nome di progetto hello, incluso il percorso completo di hello, non può essere superare i 146 caratteri. Ad esempio, questo è il nome di progetto completo hello incluso il percorso di file per un progetto Azure creato per un'applicazione Silverlight: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Potrebbe essere toomove tooa diverse directory della soluzione di che ha una lunghezza di hello tooreduce percorso più breve del nome completo del progetto hello.
>
>

toomigrate e pubblicare un tooAzure di applicazione web da Visual Studio, seguire questi passaggi.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Abilitare un'applicazione Web per la distribuzione tooAzure
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>un'applicazione web per la distribuzione tooAzure tooenable
1. tooenable l'applicazione web per la distribuzione tooAzure, menu di scelta rapida hello aprire un web del progetto nella soluzione e scegliere Aggiungi progetto di distribuzione di Azure.

    si verifica Hello seguenti azioni:

   * Un progetto Azure chiamato `<name of hello web project>.Azure` viene aggiunto toohello soluzione per l'applicazione.
   * Un ruolo web per il progetto web hello viene aggiunto toothis progetto Azure.
   * Hello **Copia localmente** tootrue è impostata per ogni assembly che sono necessari per MVC 2, MVC 3, MVC 4 e applicazioni aziendali di Silverlight. Consente di aggiungere questi pacchetto del servizio toohello assembly utilizzato per la distribuzione.

   > [!IMPORTANT]
   > Se si dispone di altri assembly o i file necessari per l'applicazione web, è necessario impostare manualmente le proprietà di hello per questi file. Per informazioni su come tooset queste proprietà, vedere hello sezione **i file di inclusione nel pacchetto del servizio hello** più avanti in questo articolo.
   >
   > [!NOTE]
   > Se esiste un ruolo web per un progetto web specifico in un progetto Azure nella soluzione hello, **convertire**, **convertire il progetto servizio Cloud tooAzure** non viene visualizzata nel menu di scelta rapida hello per questo progetto web .
   >
   >

   Se si dispone di più progetti web nell'applicazione web e si desidera ruoli web toocreate per ogni progetto web, è necessario eseguire passaggi di hello in questa procedura per ogni progetto web. Questo crea progetti Azure distinti per ogni ruolo Web. Ciascun progetto Web può essere pubblicato separatamente. In alternativa, è possibile aggiungere manualmente un altro progetto ruolo web tooan esistente Azure nell'applicazione web. toodo, menu di scelta rapida aprire hello hello **ruoli** cartella nel progetto Azure, scegliere **Aggiungi**, quindi **progetto ruolo Web nella soluzione**, scegliere hello progetto tooadd come web ruolo, quindi scegliere hello **OK** pulsante.

## <a name="use-an-azure-sql-database-for-your-application"></a>Usare un database SQL di Azure per l'applicazione
Se si dispone di una stringa di connessione per l'applicazione web che utilizza un database di SQL Server locale hello, è necessario modificare questo toouse di stringa di connessione un'istanza del Database SQL ospitata da Azure.

> [!IMPORTANT]
> La sottoscrizione deve consentire toouse Database SQL. Se si accede alla sottoscrizione da hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), è possibile determinare i servizi forniti la sottoscrizione. Hello istruzioni seguenti si applicano toohello rilasciato [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885). Se si utilizza hello [portale di Azure](http://portal.microsoft.com), saltare la procedura seguente toohello.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse un'istanza del Database SQL nel ruolo web per la stringa di connessione
1. un'istanza di Database SQL in hello toocreate [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), seguire i passaggi hello in hello articolo seguente: [creare un Database di SQL Server](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > Quando si impostano hello regole di firewall per l'istanza di Database SQL, è necessario selezionare hello **Consenti tooaccess altri servizi di Azure a questo server** casella di controllo.
   >
   >
2. toocreate un'istanza di Database SQL toouse per la stringa di connessione, seguire i passaggi di hello nella sezione successiva hello hello articolo seguente: [creare un Database SQL](http://go.microsoft.com/fwlink/?LinkId=225110).
3. toocopy toouse di stringa di connessione ADO.NET a hello per la stringa di connessione, eseguire i passaggi hello hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Scegliere hello **Database** pulsante e quindi aprire hello nodo per la sottoscrizione di hello utilizzato toocreate l'istanza del Database di SQL.
   2. toodisplay hello le istanze di Database SQL, scegliere hello **database SQL** nodo.
   3. proprietà hello toodisplay per database hello, scegliere database hello. Hello **proprietà** verrà aperta la vista.

      > [!NOTE]
      > Se hello **proprietà** non viene visualizzata, potrebbe essere necessario tooopen usando hello divisore.
      >
      >
   4. stringhe di connessione toodisplay hello, scegliere tooView di hello puntini di sospensione (…) pulsante Avanti.

      Hello **le stringhe di connessione** viene visualizzata la finestra di dialogo.
   5. Ciao toocopy stringa di connessione ADO.NET, evidenziare il testo hello e premere Ctrl + C hello.
   6. finestra di dialogo hello tooclose scegliere hello **Chiudi** pulsante.
4. connessione hello tooreplace stringa hello Web. config file toouse di questa istanza del Database SQL, aprire il file Web. config hello, evidenziare hello esistente stringa di connessione e quindi scegliere i tasti Ctrl + V hello. Hello stringa di connessione ADO.NET per l'istanza di hello del Database SQL sostituisce una stringa di connessione esistente hello.
5. È inoltre necessario aggiungere il parametro hello `MultipleActiveResultSets=True` toohello stringa di connessione. stringa di connessione Hello deve avere hello seguente formato:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (Facoltativo) Una stringa di connessione di un metodo alternativo toochanging hello direttamente nel file Web. config hello è tooadd una sezione in uno dei file di trasformazione Web. config hello, a seconda della configurazione della build hello utilizzare toocreate il pacchetto del servizio. Aprire file Web.Debug.Config hello o file Web.Release.Config hello. Aggiungere hello seguente sezione nel file:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Salvare il file hello che è stato modificato e ripubblicare l'applicazione.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>un'istanza del Database SQL tramite toouse hello portale di Azure classico
1. In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), selezionare il nodo di database SQL hello.

   * Se viene visualizzata l'istanza di hello del Database SQL che si desidera toouse, scegliere tooopen è.
   * In caso contrario tutte le istanze, scegliere collegamento appropriato hello e quindi creare un'istanza.
2. Dopo avere aperto o creato un'istanza del database, scegliere hello **le stringhe di connessione** collegamento.
3. Nella parte inferiore di hello della pagina hello, scegliere impostazioni del firewall tooconfigure collegamento hello e accettare i valori predefiniti di hello o configurare i valori hello che è necessario.
4. Copiare una stringa di connessione ADO.NET hello e incollarlo nel file Web. config sulla stringa di connessione per il database locale hello precedente hello tooadd assicurarsi di essere `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Pubblicare un'applicazione Web di tooAzure
### <a name="toopublish-a-web-application-tooazure"></a>toopublish un tooAzure di applicazione Web
1. un'applicazione hello tootest nell'ambiente di sviluppo locale hello utilizzando l'emulatore di calcolo di Azure hello, menu di scelta rapida aprire hello hello Azure per il ruolo web hello del progetto e scegliere **imposta come progetto di avvio**. Scegliere **Debug**, **Avvia debug** (tastiera: **F5**).

    Hello **hello Avvia ambiente di debug Azure** verrà visualizzata la finestra di dialogo e un'applicazione hello viene avviata nel browser hello. Per informazioni dettagliate su come toostart ogni tipo di applicazione web in hello emulatore di calcolo, vedere la tabella hello in questa sezione.
2. tooset i servizi di hello per le tooAzure toopublish applicazione, è necessario un account Microsoft e una sottoscrizione di Azure. Hello utilizzare i passaggi nel seguente argomento tooset dei servizi hello: [preparare toopublish oppure distribuire un'applicazione Azure da Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. toopublish tooAzure di applicazione web hello, aprire il menu di scelta rapida hello per il progetto web hello e scegliere **pubblicare tooAzure**.

    Hello **pubblica l'applicazione Azure** verrà visualizzata la finestra di dialogo e Visual Studio avvia il processo di distribuzione hello. Per ulteriori informazioni su come toopublish hello applicazione, vedere la sezione hello **pubblicare un'applicazione Azure da Visual Studio** in [pubblicazione di un servizio Cloud utilizzando strumenti di Azure hello](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > È anche possibile pubblicare un'applicazione web dal progetto Azure hello hello. toodo, aprire il menu di scelta rapida hello per hello progetto Azure e scegliere **pubblica**.
   >
   >
4. toosee hello lo stato di avanzamento della distribuzione di hello, è possibile visualizzare hello **Log attività Azure** finestra. Questo registro viene visualizzato automaticamente quando si avvia il processo di distribuzione hello. È possibile espandere una voce nel registro attività hello hello tooshow informazioni dettagliate, come illustrato nella seguente figura hello:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. Processo di distribuzione (facoltativo) toocancel hello, aprire il menu di scelta rapida hello per hello voce nel registro attività hello e scegliere **Annulla e Rimuovi**. Questo arresta il processo di distribuzione hello e si elimina l'ambiente di distribuzione hello da Azure.

   > [!NOTE]
   > tooremove questo ambiente di distribuzione dopo è stato distribuito, è necessario utilizzare hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (Facoltativo) Una volta avviate le istanze del ruolo, Visual Studio verrà visualizzato ambiente di distribuzione hello in hello **calcolo di Azure** nodo **Cloud Explorer** o **Esplora Server**. Da qui è possibile visualizzare lo stato di hello di hello singole istanze del ruolo.

    Hello illustrazione che segue le istanze del ruolo hello in **Esplora Server** mentre sono ancora in stato Initializing hello:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess l'applicazione dopo la distribuzione, scegliere la distribuzione hello sulla freccia avanti tooyour quando lo stato **completato** viene visualizzato in hello **log attività Azure**. Consente di visualizzare hello URL per l'applicazione web in Azure. Vedere la seguente tabella per informazioni dettagliate di hello su come toostart uno specifico tipo di applicazione web da Azure hello.

    Hello nella tabella seguente elenca i dettagli di hello sui come toostart applicazioni da Azure o toorun web o eseguire il debug di un'applicazione web localmente tramite hello emulatore di calcolo di Azure:

   | Tipo di applicazione Web | Hello esecuzione/Debug localmente utilizzando l'emulatore di calcolo | Esecuzione in Azure |
   | --- | --- | --- |
   | Applicazione Web ASP.NET |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |Scegliere un collegamento ipertestuale URL hello visualizzato in hello **distribuzione** scheda hello **log attività Azure** tooload hello inizio pagina hello browser. |
   | Applicazione Web ASP.NET MVC 2 |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |Scegliere un collegamento ipertestuale URL hello visualizzato in hello **distribuzione** scheda hello **log attività Azure** tooload hello inizio pagina hello browser. |
   | Applicazione Web ASP.NET MVC 3 |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |Scegliere un collegamento ipertestuale URL hello visualizzato in hello **distribuzione** scheda hello **log attività Azure** tooload hello inizio pagina hello browser. |
   | Applicazione Web ASP.NET MVC 4 |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |Scegliere un collegamento ipertestuale URL hello visualizzato in hello **distribuzione** scheda hello **log attività Azure** tooload hello inizio pagina hello browser. |
   | Applicazione Web ASP.NET vuota |È necessario aggiungere una pagina aspx nell'applicazione che imposta come pagina iniziale di hello per il progetto web. Sulla barra dei menu hello, quindi scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |Se si dispone di una pagina aspx predefinita nell'applicazione, scegliere un collegamento ipertestuale URL hello visualizzato in hello **distribuzione** scheda hello **log attività Azure** e questa pagina viene caricata nel browser hello. Se si dispone di una pagina aspx differente, è necessario toonavigate toothis pagina specifica utilizzando hello seguente formato per l'url:`<url for deployment>/<name of page>.aspx` |
   | Applicazione Silverlight |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |Pagina specifica di toonavigate toohello è necessario per l'applicazione utilizzando hello seguente formato per l'url:`<url for deployment>/<name of page>.aspx` |
   | Applicazione aziendale di Silverlight |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |Pagina specifica di toonavigate toohello è necessario per l'applicazione utilizzando hello seguente formato per l'url:`<url for deployment>/<name of page>.aspx` |
   | Applicazione di navigazione Silverlight |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |Pagina specifica di toonavigate toohello è necessario per l'applicazione utilizzando hello seguente formato per l'url:`<url for deployment>/<name of page>.aspx` |
   | Applicazione di servizio WCF |È necessario impostare i file con estensione svc hello di hello inizio pagina per il progetto di servizio WCF. Sulla barra dei menu hello, quindi scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |File con estensione svc toohello toonavigate è necessario per l'applicazione utilizzando hello seguente formato per l'url:`<url for deployment>/<name of service file>.svc` |
   | Applicazione di servizio del flusso di lavoro WCF |È necessario impostare i file con estensione svc hello di hello inizio pagina per il progetto di servizio WCF. Sulla barra dei menu hello, quindi scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |File con estensione svc toohello toonavigate è necessario per l'applicazione utilizzando hello seguente formato per l'url:`<url for deployment>/<name of service file>.svc` |
   | Entità dinamiche ASP.NET |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |È necessario aggiornare la stringa di connessione hello (vedere la sezione successiva). Pagina specifica di toonavigate toohello è inoltre necessario per l'applicazione utilizzando hello seguente formato per l'url:`<url for deployment>/<name of page>.aspx` |
   | ASP.NET dinamico dati Linq tooSQL |Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** (tastiera: scegliere hello **F5** chiave.). |È necessario eseguire passaggi di hello in questa procedura: utilizzare un database SQL Azure per l'applicazione (vedere la sezione precedente in questo argomento). Pagina specifica di toonavigate toohello è inoltre necessario per l'applicazione utilizzando hello seguente formato per l'url:`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Aggiornamento di una stringa di connessione per entità dinamiche ASP.NET
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>una stringa di connessione per entità ASP.NET Dynamic tooUpdate
1. toocreate un database di SQL Azure che può essere usato per un'applicazione web entità ASP.NET Dynamic, seguire i passaggi di hello nella procedura hello **utilizzare un database SQL Azure per l'applicazione** più indietro in questo argomento.
2. Aggiungere tabelle hello e i campi necessari per il database da hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).
3. stringa di connessione Hello per questo tipo di applicazione ha hello seguente formato nel file Web. config hello:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Hello aggiornamento *connectionString* valore con la stringa di connessione ADO.NET per database SQL Azure hello come indicato di seguito:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. file Web. config di hello toosave con modifiche hello che sono state apportate toohello stringa di connessione, sulla barra dei menu hello scegliere **File**, **salvare file Web. config**.

## <a name="supported-project-templates"></a>Modelli di progetto supportati
toopublish un tooAzure di applicazione web, un'applicazione hello deve utilizzare uno dei modelli di progetto hello per c# o Visual Basic elencato nella seguente tabella hello.

| Gruppo modelli di progetto | Modello di progetto |
| --- | --- |
| Web |Applicazione Web ASP.NET |
| Web |Applicazione Web ASP.NET MVC 2 |
| Web |Applicazione Web ASP.NET MVC 3 |
| Web |Applicazione Web ASP.NET MVC4 |
| Web |Applicazione Web ASP.NET vuota |
| Web |Applicazione Web vuota ASP.NET MVC 2 |
| Web |Applicazione Web entità ASP.NET Dynamic Data |
| Web |ASP.NET dinamico dati Linq tooSQL applicazione Web |
| Silverlight |Applicazione Silverlight |
| Silverlight |Applicazione aziendale di Silverlight |
| Silverlight |Applicazione di navigazione Silverlight |
| WCF |Applicazione di servizio WCF |
| WCF |Applicazione di servizio del flusso di lavoro WCF |
| Flusso di lavoro |Applicazione di servizio del flusso di lavoro WCF |

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla pubblicazione, vedere [preparare tooPublish oppure distribuire un'applicazione Azure da Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Vedere anche [Configurazione delle credenziali per l'autenticazione denominate](vs-azure-tools-setting-up-named-authentication-credentials.md)
