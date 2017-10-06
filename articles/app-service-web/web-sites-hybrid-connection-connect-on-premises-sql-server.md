---
title: aaaConnect tooon locale di SQL Server da un'app web nel servizio App di Azure mediante connessioni ibride
description: Crea un'app web in Microsoft Azure e connetterla tooan database di SQL Server locale
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Connettersi a SQL Server locale tooon da un'app web nel servizio App di Azure mediante connessioni ibride
Le connessioni ibride [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) risorse tooon locale di App Web che utilizzano una porta TCP statica. Le risorse supportate includono Microsoft SQL Server, MySQL, HTTP API Web, servizio app e la maggior parte dei servizi Web personalizzati.

In questa esercitazione si apprenderà come toocreate un servizio App web app in hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715), connettersi utilizzando la nuova connessione ibrida funzionalità di hello hello web app tooyour locale SQL Server database, creare un semplice ASP.NET applicazione che utilizzerà la connessione ibrida hello e distribuire toohello applicazione hello App del servizio web app. Hello completato web app in Azure archivia le credenziali dell'utente in un database di appartenenza che si trova in locale. esercitazione Hello non presuppone alcun esperienze precedenti usando Azure o ASP.NET.

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> parte di App Web Hello della funzionalità di connessioni ibride hello è disponibile solo in hello [portale Azure](https://portal.azure.com). toocreate una connessione in servizi di BizTalk, vedere [connessioni ibride](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello i seguenti prodotti. Sono tutti disponibili in versioni gratuite, quindi è possibile avviare le attività di sviluppo per Azure in modo completamente gratuito.

* **Sottoscrizione di Azure** : per una sottoscrizione gratuita, vedere [Versione di valutazione gratuita di Azure](/pricing/free-trial/).
* **Visual Studio 2013** -toodownload una versione di valutazione gratuita di Visual Studio 2013, vedere [download di Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs). Installare questo prodotto prima di continuare.
* **Microsoft .NET Framework 3.5 Service Pack 1**: se si usa il sistema operativo Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 o Windows Server 2008 R2, è possibile abilitare questo service pack in Pannello di controllo > Programmi e funzionalità > Attivazione o disattivazione delle funzionalità Windows. In caso contrario, è possibile scaricarlo da hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express with Tools** -scaricare Microsoft SQL Server Express gratuita all'hello [pagina Database di piattaforma Web Microsoft](http://www.microsoft.com/web/platform/database.aspx). Scegliere hello **Express** (non LocalDB) versione. Hello **Express with Tools** versione include SQL Server Management Studio, che verrà utilizzato in questa esercitazione.
* **SQL Server Management Studio Express** : questo è incluso in SQL Server 2014 Express hello con download di strumenti indicato in precedenza, ma se è necessario tooinstall è separatamente, è possibile scaricare e installarlo da hello [SQL Server Express pagina di download](http://www.microsoft.com/web/platform/database.aspx).

esercitazione Hello presuppone che si disponga di una sottoscrizione di Azure, di avere installato Visual Studio 2013 e di aver installato o abilitato .NET Framework 3.5. Hello esercitazione viene illustrato come tooinstall SQL Server 2014 Express in una configurazione che funziona bene con le connessioni ibride di hello Azure funzionalità (un'istanza predefinita con una porta TCP statica). Prima di iniziare l'esercitazione hello, scaricare SQL Server 2014 Express with Tools dal percorso di hello indicato sopra, se non è installato SQL Server.

### <a name="notes"></a>Note
toouse un SQL Server locale o un database di SQL Server Express con una connessione ibrida, TCP/IP deve toobe abilitata su una porta statica. A differenza delle istanze denominate, le istanze predefinite di SQL Server usano la porta statica 1433.

computer Hello in cui si installa l'agente di gestione connessione ibrida locale hello:

* Deve disporre di connettività in uscita tooAzure su:

| Porta | Motivo |
| --- | --- |
| 80 |**Obbligatorio** per la porta HTTP per la convalida del certificato e, facoltativamente, per la connettività dati. |
| 443 |**Facoltativo** per la connettività dei dati. Se non è disponibile la connettività in uscita too443, viene utilizzata la porta TCP 80. |
| 5671 e 9352 |**Consigliato** ma facoltativo per la connettività dei dati. Notare che questa modalità normalmente genera una maggiore velocità effettiva. Se le porte toothese di connettività in uscita non è disponibile, viene utilizzata la porta TCP 443. |

* Deve essere in grado di tooreach hello *hostname*:*NumeroPorta* della risorsa locale.

passaggi di Hello in questo articolo si presuppongono che si sta utilizzando un browser hello dal computer hello che ospiterà l'agente di connessione ibrida locale hello.

Se si dispone già di SQL Server installata in una configurazione e in un ambiente che soddisfa le condizioni di hello descritte in precedenza, è possibile ignorare e avviare con [creare un database di SQL Server on-premise](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>R. Installare SQL Server Express, abilitare TCP/IP e creare un database SQL Server locale
In questa sezione mostra come abilitare TCP/IP, SQL Server Express, tooinstall e creare un database in modo che l'applicazione web funzionerà con hello portale di Azure.

### <a name="install-sql-server-express"></a>Installare SQL Server Express
1. SQL Server Express, eseguire hello tooinstall **SQLEXPRWT_x64_ENU.exe** o **SQLEXPR_x86_ENU.exe** file scaricato. verrà visualizzata Hello guidata di Centro installazione SQL Server.
   
    ![Installare SQL Server][SQLServerInstall]
2. Scegliere **nuova installazione SQL Server autonomo o aggiungere funzionalità tooan esistente installazione**. Seguire le istruzioni di hello, accettando i valori predefiniti hello e le impostazioni, fino a ottenere toohello **configurazione istanza** pagina.
3. In hello **configurazione istanza** pagina, scegliere **istanza predefinita**.
   
    ![Scegliere Istanza predefinita][ChooseDefaultInstance]
   
    Per impostazione predefinita, hello predefinito istanza di SQL Server è in ascolto delle richieste dai client di SQL Server sulla porta statica 1433, ovvero quali hello connessioni ibride funzionalità richiede. Le istanze denominate usano le porte dinamiche e UDP, che non sono supportate da Connessioni ibride.
4. Accettare i valori predefiniti hello hello **configurazione Server** pagina.
5. In hello **configurazione motore di Database** pagina **modalità di autenticazione**, scegliere **modalità mista (autenticazione di SQL Server e l'autenticazione di Windows)**e fornire una password.
   
    ![Scegliere Modalità mista][ChooseMixedMode]
   
    In questa esercitazione l'utente userà l'autenticazione SQL Server. Essere password hello tooremember assicurarsi che forniscono, poiché sarà necessario in un secondo momento.
6. Scorrere il resto di hello dell'installazione guidata del hello toocomplete hello.

### <a name="enable-tcpip"></a>Abilitare TCP/IP
tooenable TCP/IP, utilizzare Gestione configurazione di SQL Server, che è stato installato durante l'installazione di SQL Server Express. Seguire i passaggi di hello in [Abilita protocollo di rete TCP/IP per SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) prima di continuare.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Creare un database SQL Server locale
L'applicazione Web Visual Studio richiede un database di appartenenza al quale Azure può effettuare l'accesso. Ciò richiede un database di SQL Server o SQL Server Express (non hello LocalDB database hello Usa modello MVC per impostazione predefinita), pertanto si creeranno database delle appartenenze hello successivamente.

1. In SQL Server Management Studio connettersi toohello SQL Server appena installato. (Se hello **connettersi tooServer** finestra di dialogo non viene visualizzata automaticamente, passare troppo**Esplora oggetti** nel riquadro di sinistra hello, fare clic su **Connetti**, quindi fare clic su **Motore di database**.) ![Connettersi tooServer][SSMSConnectToServer]
   
    In **Tipo server** scegliere **Motore di database**. Per **nome Server**, è possibile utilizzare **localhost** o nome hello del computer di hello che si sta utilizzando. Scegliere **l'autenticazione di SQL Server**e quindi accedere con nome utente dell'amministratore di sistema di hello e una password hello creato in precedenza.
2. toocreate un nuovo database utilizzando SQL Server Management Studio, fare doppio clic su **database** in Esplora oggetti e quindi fare clic su **Nuovo Database**.
   
    ![Creare il nuovo database][SSMScreateNewDB]
3. In hello **Nuovo Database** finestra di dialogo immettere MembershipDB per nome del database hello e quindi fare clic su **OK**.
   
    ![Provide database name][SSMSprovideDBname]
   
    Si noti che non si apportano qualsiasi database toohello modifiche a questo punto. informazioni sull'appartenenza Hello verranno aggiunto automaticamente in un secondo momento dall'applicazione web al momento dell'esecuzione.
4. In Esplora oggetti, se si espande **database**, si noterà che è stato creato il database delle appartenenze hello.
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Creare un'app web nel portale di Azure hello
> [!NOTE]
> Se un'app web è già stato creato in hello portale di Azure che si desidera toouse per questa esercitazione, è possibile andare troppo[creare una connessione ibrida e un BizTalk Service](#CreateHC) e continua da tale posizione.
> 
> 

1. In hello [portale Azure](https://portal.azure.com), fare clic su **New** > **Web e dispositivi mobili** > **app Web**.
   
    ![New button][New]
2. Configurare l'applicazione web e quindi fare clic su **Crea**.
   
    ![Website name][WebsiteCreationBlade]
3. Dopo alcuni istanti, viene creato l'app web hello e viene visualizzato il pannello app web. Pannello Hello è un dashboard scorrevole verticalmente che consente di gestire l'app web.
   
    ![Website running][WebSiteRunningBlade]
   
    tooverify hello web app è in tempo reale, è possibile fare clic su hello **Sfoglia** pagina predefinita di icona toodisplay hello.

Successivamente, si creerà una connessione ibrida e un servizio BizTalk per l'app web hello.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Creare una connessione ibrida e servizi BizTalk
1. Indietro nel portale di hello, toosettings, fare clic su **rete** > **configurare gli endpoint della connessione ibrida**.
   
    ![Connessioni ibride][CreateHCHCIcon]
2. Nel Pannello di connessioni ibride hello, fare clic su **Aggiungi** > **nuova connessione ibrida**.
3. In hello **creare la connessione ibrida** pannello:
   
   * Per **nome**, specificare un nome per la connessione hello.
   * Per **Hostname**, immettere il nome di computer hello del computer host SQL Server.
   * Per **porta**, immettere 1433 (porta hello predefinita per SQL Server).
   * Fare clic su **BizTalk Service** > **nuovo servizio BizTalk** e immettere un nome per il servizio BizTalk hello.
     
     ![Creare una connessione ibrida][TwinCreateHCBlades]
4. Fare clic su **OK** due volte.
   
    Quando il processo di hello viene completata, hello **notifiche** area farà lampeggiare una verde **successo** hello e **connessione ibrida** pannello mostrerà hello nuova connessione ibrida lo stato di Hello **non connesso**.
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

A questo punto, è stata completata una parte importante dell'infrastruttura di connessione di hello cloud ibrido. Nel passaggio successivo verrà creato un elemento locale corrispondente.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Installare connessione hello toocomplete di hello locale di Hybrid Connection Manager
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Ora che infrastruttura di connessione ibrida hello è stata completata, si creerà un'applicazione web che lo utilizza.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. Creare un progetto web ASP.NET base, modificare una stringa di connessione database hello ed eseguire progetto hello in locale
### <a name="create-a-basic-aspnet-project"></a>Create a basic ASP.NET project
1. In Visual Studio, su hello **File** menu, creare un nuovo progetto:
   
    ![New Visual Studio project][HCVSNewProject]
2. In hello **modelli** sezione di hello **nuovo progetto** finestra di dialogo Seleziona **Web** e scegliere **applicazione Web ASP.NET**, quindi fare clic su  **OK**.
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. In hello **nuovo progetto ASP.NET** finestra di dialogo, scegliere **MVC**, quindi fare clic su **OK**.
   
    ![Choose MVC][HCVSChooseMVC]
4. Dopo aver creato il progetto di hello, verrà visualizzata la pagina file Leggimi di applicazione hello. Non eseguire ancora il progetto web hello.
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Modificare hello stringa di connessione di database per un'applicazione hello
In questo passaggio, si modifica stringa di connessione hello che indica l'applicazione in cui toofind locale SQL Server Express database. stringa di connessione Hello è il file Web. config dell'applicazione hello, che contiene informazioni di configurazione per un'applicazione hello.

> [!NOTE]
> tooensure che l'applicazione utilizza database hello creati in SQL Server Express e non i hello uno in LocalDB predefinito di Visual Studio, è importante completare questo passaggio prima di eseguire il progetto.
> 
> 

1. In Esplora soluzioni fare doppio clic sul file Web. config hello.
   
    ![Web.config][HCVSChooseWebConfig]
2. Modifica hello **connectionStrings** database di SQL Server toohello toopoint sezione sul computer locale, la seguente sintassi hello in hello di esempio seguente:
   
    ![Stringa di connessione][HCVSConnectionString]
   
    Quando la composizione di stringa di connessione hello, tenere seguente hello presente:
   
   * Se ci si connette tooa denominato istanza anziché un'istanza predefinita (ad esempio, YourServer\SQLEXPRESS), è necessario configurare le porte statiche toouse di SQL Server. Per informazioni sulla configurazione delle porte statiche, vedere [come tooconfigure toolisten di SQL Server su una porta specifica](http://support.microsoft.com/kb/823938). Per impostazione predefinita le istanze denominate usano UDP e le porte dinamiche, che non sono supportate dalle connessioni ibride.
   * È consigliabile specificare hello porta (1433 per impostazione predefinita, come illustrato nell'esempio hello) nella stringa di connessione hello in modo che è necessario che SQL Server locale è abilitato TCP e utilizza la porta corretta hello.
   * Tenere presente che toouse tooconnect di autenticazione di SQL Server, specificare ID utente hello e una password nella stringa di connessione.
3. Fare clic su **salvare** nel file Web. config hello toosave di Visual Studio.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Eseguire il progetto hello in locale e registrare un nuovo utente
1. A questo punto, eseguire il nuovo progetto web in locale fare clic sul pulsante Sfoglia hello in Debug. In questo esempio viene usato Internet Explorer.
   
    ![Run project][HCVSRunProject]
2. Scegliere hello angolo superiore destro della pagina web predefinita di hello, **registrare** tooregister un nuovo account:
   
    ![Register a new account][HCVSRegisterLocally]
3. Immettere un nome utente e una password:
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    Verrà creato automaticamente un database in SQL Server locale che contiene informazioni sull'appartenenza hello per l'applicazione. Una delle tabelle di hello (**dbo. AspNetUsers**) contiene le credenziali utente di app come quelle appena immesso hello di web. Questa tabella verrà visualizzato in un secondo momento nell'esercitazione di hello.
4. Chiudere una finestra del browser hello della pagina web predefinita di hello. Questo arresta un'applicazione hello in Visual Studio.

Ora pronti per la successiva hello, ovvero toopublish hello applicazione tooAzure ed eseguirne il test.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. Pubblicare hello web applicazione tooAzure ed eseguirne il test
A questo punto, si sarà pubblicare il tooyour applicazione App del servizio web app e come testarlo toosee come la connessione ibrida hello configurati in precedenza è viene utilizzato tooconnect database toohello app web nel computer locale.

### <a name="publish-hello-web-application"></a>Pubblicare un'applicazione web hello
1. È possibile scaricare il profilo di pubblicazione per app di servizio App web nel portale di Azure hello hello. Nel Pannello di hello per le app web, fare clic su **profilo di pubblicazione Get**e quindi salvare computer tooyour di file hello.
   
    ![Scarica profilo di pubblicazione][PortalDownloadPublishProfile]
   
    Quindi il file verrà importato nell'applicazione Web di Visual Studio.
2. In Visual Studio, nome del progetto hello in Esplora soluzioni e scegliere **pubblica**.
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. In hello **pubblica sul Web** della finestra di dialogo hello **profilo** scegliere **importazione**.
   
    ![Importa][HCVSPublishWebDialogImport]
4. Sfoglia tooyour scaricato il profilo di pubblicazione, selezionarlo e quindi fare clic su **OK**.
   
    ![Sfoglia tooprofile][HCVSBrowseToImportPubProfile]
5. Le informazioni di pubblicazione viene importate e lo visualizza in hello **connessione** scheda della finestra di dialogo hello.
   
    ![Click Publish][HCVSClickPublish]
   
    Fare clic su **Pubblica**.
   
    Al termine del processo di pubblicazione, il browser verrà avviare e Mostra l'applicazione ASP.NET ormai, ad eccezione del fatto che ora è in tempo reale nel cloud di Azure hello!

Successivamente, si utilizzerà il toosee di applicazione web in tempo reale la connessione ibrida in azione.

### <a name="test-hello-completed-web-application-on-azure"></a>Hello test completa l'applicazione web in Azure
1. In primo piano hello destra della pagina web in Azure, scegliere **Accedi**.
   
    ![Test log in][HCTestLogIn]
2. Il servizio App di app web è ora connesso database delle appartenenze dell'applicazione web tooyour sul computer locale. tooverify, accedere con hello stesse credenziali immesse hello locale del database in precedenza.
   
    ![Hello greeting][HCTestHelloContoso]
3. toofurther testare la nuova connessione ibrida, esegue la disconnessione dell'applicazione web di Azure e registrare come altro utente. Specificare un nuovo nome utente e password, quindi fare clic su **Registra**.
   
    ![Test register another user][HCTestRegisterRelecloud]
4. tooverify che hello credenziali del nuovo utente sono state archiviate nel database locale tramite la connessione ibrida, aprire SQL Management Studio nel computer locale. In Esplora oggetti espandere hello **MembershipDB** database e quindi espandere **tabelle**. Pulsante destro del mouse hello **dbo. AspNetUsers** l'appartenenza di tabella e scegliere **seleziona le prime 1000 righe** risultati hello tooview.
   
    ![Visualizzare i risultati di hello][HCTestSSMSTree]
5. La tabella di appartenenza locale verranno visualizzati entrambi gli account - hello uno creato in locale e hello uno creato in hello cloud di Azure. Hello creata nel cloud hello è stato salvato il database locale tooyour tramite funzionalità di connessione ibrida di Azure.
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

A questo punto, aver creato e distribuito un'applicazione web ASP.NET che usa una connessione ibrida tra un'app web nel cloud di Azure hello e un database di SQL Server locale. Congratulazioni.

## <a name="see-also"></a>Vedere anche
[Panoramica delle connessioni ibride](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist presenta le connessioni ibride (video Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Panoramica delle connessioni ibride](/services/biztalk-services/)

[Servizi BizTalk: schede Dashboard, Monitor, Scala, Configura e Connessione ibrida](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Creazione di un cloud ibrido reale con portabilità continua delle applicazioni (video Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Accesso alle risorse locali usando connessioni ibride nel Servizio app di Azure](web-sites-hybrid-connection-get-started.md)

[Panoramica dell'identità ASP.NET](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
