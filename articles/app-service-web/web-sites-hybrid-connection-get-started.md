---
title: aaaAccess risorse locali mediante connessioni ibride in Azure App Service
description: Creare una connessione tra un'app Web nel servizio app di Azure e una risorsa locale che usa una porta TCP statica
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Accesso alle risorse locali usando connessioni ibride nel servizio app di Azure
È possibile connettersi a una risorsa servizio App di Azure app tooany locale che utilizza una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP e la maggior parte dei servizi Web personalizzati. In questo articolo illustra come toocreate una connessione ibrida tra servizio App e un database di SQL Server locale.

> [!NOTE]
> parte di App Web Hello della funzionalità di connessioni ibride hello è disponibile solo in hello [portale Azure](https://portal.azure.com). toocreate una connessione in servizi di BizTalk, vedere [connessioni ibride](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Questo contenuto si applica anche tooMobile App in Azure App Service. 
> 
> 

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Per una sottoscrizione gratuita, vedere [Versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
* toouse un SQL Server locale o un database di SQL Server Express con una connessione ibrida, TCP/IP deve toobe abilitata su una porta statica. È consigliabile usare un'istanza predefinita di on SQL Server, perché usa la porta statica 1433. Per informazioni sull'installazione e configurazione di SQL Server Express per l'utilizzo con le connessioni ibride, vedere [tooan connessione SQL Server locale da un sito web di Azure mediante connessioni ibride](http://go.microsoft.com/fwlink/?LinkID=397979).
* computer Hello in cui si installa agente di gestione connessione ibrida locale hello descritto più avanti in questo articolo:
  
  * Deve essere in grado di tooconnect tooAzure attraverso la porta 5671
  * Deve essere in grado di tooreach hello *hostname*:*NumeroPorta* della risorsa locale. 

> [!NOTE]
> passaggi di Hello in questo articolo si presuppongono che si sta utilizzando un browser hello dal computer hello che ospiterà l'agente di connessione ibrida locale hello.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Creare un'app web nel portale di Azure hello
> [!NOTE]
> Se è già stato creato un'app web o App per dispositivi mobili di back-end in hello portale di Azure che si desidera toouse per questa esercitazione, è possibile andare troppo[creare una connessione ibrida e un BizTalk Service](#CreateHC) e iniziare da qui.
> 
> 

1. In hello nell'angolo superiore sinistro di hello [portale Azure](https://portal.azure.com), fare clic su **New** > **Web e dispositivi mobili** > **App Web**.
   
    ![Nuova applicazione web][NewWebsite]
2. In hello **app Web** pannello, specificare un URL e fare clic su **crea**. 
   
    ![Website name][WebsiteCreationBlade]
3. Dopo alcuni istanti, viene creato l'app web hello e viene visualizzato il pannello app web. Pannello Hello è un dashboard scorrevole verticalmente che consente di gestire il sito.
   
    ![Website running][WebSiteRunningBlade]
4. sito hello tooverify è attivo, è possibile scegliere hello **Sfoglia** pagina predefinita di icona toodisplay hello.
   
    ![Fare clic su Sfoglia toosee app web][Browse]
   
    ![Pagina di applicazione web predefinita][DefaultWebSitePage]

Successivamente, si creerà una connessione ibrida e un servizio BizTalk per l'app web hello.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Creare una connessione ibrida e servizi BizTalk
1. Nel pannello dell'app Web fare clic su **Tutte le impostazioni** > **Rete** > **Configurare gli endpoint della connessione ibrida**.
   
    ![Connessioni ibride][CreateHCHCIcon]
2. Nel Pannello di connessioni ibride hello, fare clic su **Aggiungi**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. Hello **aggiungere una connessione ibrida** apre blade.  Poiché questa è la prima connessione ibrida, hello **nuova connessione ibrida** opzione è preselezionato e hello **creare la connessione ibrida** pannello verrà visualizzata.
   
    ![Creare una connessione ibrida][TwinCreateHCBlades]
   
    In hello **blade di connessione ibrida crea**:
   
   * Per **nome**, specificare un nome per la connessione hello.
   * Per **Hostname**, immettere il nome di hello del computer locale hello che ospita la risorsa.
   * Per **porta**, immettere il numero di porta hello che la risorsa locale utilizza (1433 per un'istanza predefinita di SQL Server).
   * Fare clic su **Servizio BizTalk**
4. Hello **Crea servizio BizTalk** apre blade. Immettere un nome per il servizio BizTalk hello e quindi fare clic su **OK**.
   
    ![Crea servizio BizTalk][CreateHCCreateBTS]
   
    Hello **Crea servizio BizTalk** pannello chiude e si ritorna toohello **creare la connessione ibrida** blade.
5. Nel Pannello di connessione ibrida crea hello, fare clic su **OK**. 
   
    ![Fare clic su OK.][CreateBTScomplete]
6. Al termine del processo di hello, area di notifica hello in hello portale indica che la connessione hello è stata creata correttamente.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. Nel pannello dell'app web hello, hello **connessioni ibride** icona Mostra che è stata creata la connessione ibrida 1 ora.
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

A questo punto, è stata completata una parte importante dell'infrastruttura di connessione di hello cloud ibrido. Nel passaggio successivo verrà creato un elemento locale corrispondente.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Installare connessione hello toocomplete di hello locale di Hybrid Connection Manager
1. Nel pannello dell'app web hello, fare clic su **tutte le impostazioni** > **rete** > **configurare gli endpoint della connessione ibrida**. 
   
    ![Hybrid connections icon][HCIcon]
2. In hello **connessioni ibride** blade, hello **stato** colonna per hello aggiunti di recente endpoint Mostra **non connesso**. Fare clic su tooconfigure connessione hello è.
   
    ![Non connesso][NotConnected]
   
    verrà visualizzata la finestra di blade di connessione ibrida Hello.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. Nel Pannello di hello, fare clic su **Listener installazione**.
   
    ![Click Listener Setup][ClickListenerSetup]
4. Hello **le proprietà di connessione ibrida** apre blade. In **locale di Hybrid Connection Manager**, scegliere **fare clic qui tooinstall**.
   
    ![Fare clic qui tooinstall][ClickToInstallHCM]
5. In hello applicazione eseguita avviso di sicurezza, scegliere **eseguire** toocontinue.
   
    ![Scegliere Esegui toocontinue][ApplicationRunWarning]
6. In hello **controllo dell'Account utente** finestra di dialogo, scegliere **Sì**.
   
   ![Choose Yes][UAC]
7. Hello Hybrid Connection Manager viene scaricato e installato automaticamente. 
   
    ![Installazione][HCMInstalling]
8. Al termine dell'installazione di hello, fare clic su **Chiudi**.
   
    ![Fare clic su Chiudi][HCMInstallComplete]
   
    In hello **connessioni ibride** blade, hello **stato** colonna Mostra ora **connesso**. 
   
    ![Stato connesso][HCStatusConnected]

Ora che infrastruttura di connessione ibrida hello è stata completata, è possibile creare un'applicazione ibrida che lo utilizza. 

> [!NOTE]
> Hello nelle sezioni seguenti illustrano come toouse una connessione ibrida con un progetto di back-end App Mobile.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Configurare il database di SQL Server di hello .NET App Mobile back-end progetto tooconnect toohello
In Servizio app, un progetto di back-end .NET per App per dispositivi mobili è semplicemente un'app Web ASP.NET dotata di un SDK per App per dispositivi mobili installato e inizializzato. toouse l'app web come un back-end dell'App per dispositivi mobili, è necessario [download e l'inizializzazione di back-end .NET le app mobili hello SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Per App per dispositivi mobili, è anche necessario toodefine una stringa di connessione per il database locale hello e modificare hello back-end toouse questa connessione. 

1. In Esplora soluzioni in Visual Studio, il file Web. config hello open per il back-end Mobile App .NET, individuare hello **connectionStrings** sezione, aggiungere una nuova voce di SqlClient seguente hello, quali toohello punti SQL locale Database del server:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Ricordare tooreplace `<**secure_password**>` in questa stringa con password hello creata per *HybridConnectionLogin*.
2. Fare clic su **salvare** nel file Web. config hello toosave di Visual Studio.
   
   > [!NOTE]
   > Questa impostazione di connessione viene utilizzata durante l'esecuzione nel computer locale hello. Durante l'esecuzione in Azure, questa impostazione è sottoposta a override dall'impostazione di connessione hello definito nel portale di hello.
   > 
   > 
3. Espandere hello **modelli** cartelle e file del modello dati aprire hello, che termina *Context.cs*.
4. Modificare hello **DbContext** toopass costruttore di istanza hello valore `OnPremisesDBConnection` toohello base **DbContext** costruttore, simile toohello frammento di codice seguente:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    servizio Hello utilizzeranno hello nuovo connessione toohello database SQL Server.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Aggiornare la stringa di connessione di hello App Mobile back-end toouse hello locale
Successivamente, è necessario tooadd un'impostazione app per la nuova stringa di connessione in modo che può essere utilizzato da Azure.  

1. In hello [portale di Azure](https://portal.azure.com) hello codice app web back-end per l'App Mobile, fare clic su **tutte le impostazioni**, quindi **le impostazioni dell'applicazione**.
2. In hello **impostazioni app Web** pannello, scorrere verso il basso troppo**le stringhe di connessione** e aggiungere un nuovo **SQL Server** stringa di connessione denominata `OnPremisesDBConnection` con un valore come `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Sostituire `<**secure_password**>` con password sicura di hello per il database locale.
   
    ![Stringa di connessione del database locale](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Premere **salvare** stringa di connessione e la connessione ibrida hello toosave appena creato.

A questo punto è possibile ripubblicare il progetto server di hello e provare di hello nuova connessione con il client App per dispositivi mobili esistenti. Dati verranno leggere e scritti database locale toohello utilizzando la connessione ibrida hello.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni sulla creazione di un'applicazione web ASP.NET che usa una connessione ibrida, vedere [tooan connessione SQL Server locale da un sito web di Azure mediante connessioni ibride](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Risorse aggiuntive
[Panoramica delle connessioni ibride](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist presenta le connessioni ibride (video Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Sito Web delle connessioni ibride](https://azure.microsoft.com/services/biztalk-services/)

[Servizi BizTalk: schede Dashboard, Monitor, Scala, Configura e Connessione ibrida](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Creazione di un cloud ibrido reale con portabilità continua delle applicazioni (video Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Connettersi tooan on-premise a SQL Server da servizi mobili di Azure mediante connessioni ibride (video di Channel 9)](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
