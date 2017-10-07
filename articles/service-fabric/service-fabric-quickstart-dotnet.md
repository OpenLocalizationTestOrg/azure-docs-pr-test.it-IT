---
title: un'applicazione .NET Service Fabric in Azure aaaCreate | Documenti Microsoft
description: Creare un'applicazione .NET per Azure utilizzando l'esempio di Guida introduttiva di Service Fabric hello.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a>Creare un'applicazione .NET Service Fabric in Azure
Azure Service Fabric è una piattaforma di sistemi distribuiti per la distribuzione e la gestione di microservizi e contenitori scalabili e affidabili. 

Questa Guida introduttiva viene illustrato come toodeploy il primo tooService di applicazioni .NET dell'infrastruttura. Al termine, si dispone di un'applicazione voto con un front-end che salva i risultati di voto in un servizio back-end con stato cluster hello web di ASP.NET Core.

![Screenshot dell'applicazione](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

Usando questa applicazione, si apprenderà come:
> [!div class="checklist"]
> * Creare un'applicazione mediante .NET e Service Fabric
> * Usare ASP.NET Core come front-end Web
> * Archiviare i dati dell'applicazione in un servizio con stato
> * Eseguire il debug dell'applicazione in locale
> * Distribuire hello applicazione tooa cluster in Azure
> * Applicazione hello di scalabilità orizzontale in più nodi
> * Eseguire un aggiornamento in sequenza delle applicazioni

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa Guida rapida:
1. [Installare Visual Studio 2017](https://www.visualstudio.com/) con hello **lo sviluppo di Azure** e **sviluppo web ASP.NET e** i carichi di lavoro.
2. [Installare Git](https://git-scm.com/)
3. [Installare Microsoft Azure Service Fabric SDK hello](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. Eseguire hello comando tooenable Visual Studio toodeploy toohello dell'infrastruttura del servizio cluster locale seguente:
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a>Scaricare l'esempio hello
In una finestra di comando, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a>Eseguire un'applicazione hello in locale
Fare doppio clic sull'icona di Visual Studio hello in hello Menu Start e scegliere **Esegui come amministratore**. In servizi di tooyour debugger hello tooattach ordine, è necessario toorun Visual Studio come amministratore.

Aprire hello **Voting.sln** soluzione di Visual Studio dal repository hello è stato clonato.

un'applicazione hello toodeploy, premere **F5**.

> [!NOTE]
> Hello prima eseguire e distribuire un'applicazione hello, Visual Studio crea un cluster locale per il debug. Questa operazione può richiedere del tempo. lo stato di creazione di cluster Hello viene visualizzato nella finestra di output di hello Visual Studio.

Una volta completata la distribuzione di hello, avviare un browser e aprire questa pagina: `http://localhost:8080` -web hello front-end dell'applicazione hello.

![Front-end dell'applicazione](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

È ora possibile aggiungere un set di opzioni per le votazioni e iniziare a raccogliere i voti. esecuzione dell'applicazione Hello e archivia tutti i dati del cluster di Service Fabric, senza necessità di hello di un database separato.

## <a name="walk-through-hello-voting-sample-application"></a>Procedura dettagliata hello voto applicazione di esempio
Hello voto applicazione è costituita da due servizi:
- Il servizio front-end (VotingWeb) Web - An ASP.NET Core web front-end del servizio, che serve a pagina web hello ed espone web toocommunicate API con il servizio back-end hello.
- Il servizio back-end (VotingData)-servizio web di ASP.NET Core, che espone un voto di hello toostore API comporta un dizionario affidabile persistente su disco.

![Diagramma dell'applicazione](./media/service-fabric-quickstart-dotnet/application-diagram.png)

Quando voto hello applicazione hello seguenti si verificano eventi:
1. JavaScript invia API web toohello richiesta di voto hello in servizio front-end web di hello come una richiesta HTTP PUT.

2. servizio front-end web di Hello Usa un proxy toolocate e inoltrare un servizio back-end toohello di richiesta HTTP PUT.

3. servizio back-end Hello accetta la richiesta in ingresso hello e archivi hello aggiornamento risultato in un dizionario affidabile, che ottiene i nodi toomultiple replicati all'interno di cluster hello e persistente su disco. Dati dell'applicazione hello tutti archiviati in cluster hello, pertanto non è necessario alcun database.

## <a name="debug-in-visual-studio"></a>Eseguire il debug in Visual Studio
Durante il debug dell'applicazione in Visual Studio, viene usato un cluster di sviluppo locale di Service Fabric. È necessario hello opzione tooadjust lo scenario di tooyour esperienza di debug. In questa applicazione, i dati vengono archiviati nel servizio back-end tramite un oggetto Reliable Dictionary. Visual Studio rimuove un'applicazione hello per impostazione predefinita, quando si arresta il debugger hello. Rimozione di un'applicazione hello comporta hello dati back-end hello tooalso servizio da rimuovere. dati di hello toopersist tra le sessioni di debug, è possibile modificare hello **modalità di Debug dell'applicazione** come proprietà nel hello **voto** progetto in Visual Studio.

toolook cosa accade nel codice hello, hello completo alla procedura seguente:
1. Aprire hello **VotesController.cs** file e impostare un punto di interruzione dell'API web hello **inserire** (metodo) (riga 47), è possibile cercare file hello in hello Esplora soluzioni in Visual Studio.

2. Aprire hello **VoteDataController.cs** file e impostare un punto di interruzione in questa web API **inserire** (metodo) (riga 50).

3. Tornare indietro del browser toohello e fare clic su un'opzione di voto oppure aggiungere una nuova opzione di voto. È stato raggiunto punto di interruzione prima hello nel controller api hello web front-end.
    - Si tratta di dove hello JavaScript nel browser hello invia un controller di API web toohello richiesta nel servizio front-end hello.
    
    ![Aggiungere il servizio front-end di voto](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - Prima di tutto è costruire hello URL toohello ReverseProxy per il servizio back-end **(1)**.
    - Quindi inviare hello HTTP PUT richiesta toohello ReverseProxy **(2)**.
    - Infine hello restituiamo risposta hello client toohello servizio back-end di hello **(3)**.

4. Premere **F5** toocontinue
    - Sono ora al punto di interruzione hello in servizio back-end hello.
    
    ![Aggiungere il servizio back-end di voto](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - Nella prima riga di hello nel metodo hello **(1)** usiamo hello `StateManager` tooget o aggiungere un dizionario affidabile denominato `counts`.
    - Tutte le interazioni con i valori in un oggetto Reliable Dictionary richiedono una transazione, che viene creata dall'istruzione using **(2)**.
    - Transazione hello, è stato quindi aggiornare il valore di hello della chiave pertinenti di hello per hello voto opzione e commit hello operazione **(3)**. Dopo il commit di hello metodo viene restituito, hello dati viene aggiornati nel dizionario hello e replicati tooother nodi nel cluster hello. dati Hello sono ora archiviati in modo sicuro in cluster hello e servizio back-end hello failover dei nodi tooother, persistono dati hello disponibili.
5. Premere **F5** toocontinue

hello toostop debug sessione, premere **MAIUSC + F5**.

## <a name="deploy-hello-application-tooazure"></a>Distribuire tooAzure applicazione hello
toodeploy cluster tooa hello applicazione in Azure, è possibile scegliere toocreate la propria cluster, oppure utilizzare un Cluster di terze parti.

Cluster di terze parti sono i cluster di Service Fabric gratuito, periodo di tempo limitato ospitati in Azure e vengono eseguiti dal team di Service Fabric hello in tutti gli utenti possono distribuire le applicazioni e informazioni sulla piattaforma hello. tooget accesso tooa Cluster di terze parti, [istruzioni hello](http://aka.ms/tryservicefabric). 

Per informazioni sulla creazione di un cluster, vedere [Creare il primo cluster di Service Fabric di Azure](service-fabric-get-started-azure-cluster.md).

> [!Note]
> il servizio front-end web di Hello è toolisten configurato sulla porta 8080 per il traffico in ingresso. Assicurarsi che tale porta sia aperta nel cluster. Se si utilizza hello Cluster di terze parti, questa porta è aperta.
>

### <a name="deploy-hello-application-using-visual-studio"></a>Distribuire l'applicazione hello utilizzando Visual Studio
Ora che un'applicazione hello è pronta, è possibile distribuire cluster tooa direttamente da Visual Studio.

1. Fare doppio clic su **voto** in hello Esplora soluzioni e scegliere **pubblica**. finestra di dialogo pubblicazione Hello viene visualizzato.

    ![Finestra di dialogo Pubblica](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. Tipo di Endpoint della connessione hello cluster hello in hello **Endpoint della connessione** campo e fare clic su **pubblica**. Se l'iscrizione per hello Cluster di terze parti, hello Endpoint della connessione viene fornito nel browser hello. Ad esempio, `winh1x87d1d.westus.cloudapp.azure.com:19000`.

3. Aprire un browser e digitare, ad esempio, nell'indirizzo cluster hello - `http://winh1x87d1d.westus.cloudapp.azure.com`. Dovrebbe essere un'applicazione hello in esecuzione in cluster hello in Azure.

![Front-end dell'applicazione](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a>Ridimensionare applicazioni e servizi in un cluster
Servizi di Service Fabric possono essere scalati facilmente in un cluster di tooaccommodate per una modifica nel carico di hello nei servizi di hello. Scalabilità di un servizio modificando hello numero di istanze in esecuzione nel cluster hello. Sono disponibili diversi sistemi per garantire la scalabilità dei servizi: è possibile usare gli script o i comandi di PowerShell oppure l'interfaccia della riga di comando di Service Fabric (sfctl). In questo esempio verrà usato Service Fabric Explorer.

Service Fabric Explorer viene eseguito in tutti i cluster di Service Fabric e sono accessibili da un browser, esplorando la porta di Gestione cluster HTTP toohello (19080), ad esempio, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.

hello tooscale servizio front-end web, hello i passaggi seguenti:

1. Aprire Service Fabric Explorer nel cluster, ad esempio `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.
2. Fare clic su Avanti toohello di hello puntini di sospensione (tre punti) **fabric: / voto/VotingWeb** nodo in treeview hello e scegliere **servizio scala**.

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    È ora possibile scegliere numero hello tooscale istanze del servizio front-end web di hello.

3. Modificare il numero di hello troppo**2** e fare clic su **servizio scala**.
4. Fare clic su hello **fabric: / voto/VotingWeb** nodo nella visualizzazione struttura ad albero di hello ed espandere il nodo di partizione hello (rappresentato da un GUID).

    ![Ridimensionamento dei servizi in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    Si noterà ora che hello servizio dispone di due istanze, e nella visualizzazione ad albero di hello vedere quali nodi eseguire istanze hello in.

Da questa attività, gestione semplice è raddoppiato risorse hello disponibili per il carico utente tooprocess di servizio front-end. È importante toounderstand che non è necessario più istanze di un servizio di toohave eseguirlo in modo affidabile. Se non è un servizio, Service Fabric assicura che una nuova istanza del servizio viene eseguito nel cluster hello.

## <a name="perform-a-rolling-application-upgrade"></a>Eseguire un aggiornamento in sequenza delle applicazioni
Quando si distribuisce una nuova applicazione di tooyour gli aggiornamenti, Service Fabric esegue il rollup di aggiornamento hello in modo sicuro. Gli aggiornamenti in sequenza non comportano tempi di inattività durante l'aggiornamento e consentono il rollback automatico in caso di errori.

tooupgrade applicazione hello, hello seguenti:

1. Aprire hello **cshtml** file in Visual Studio, è possibile cercare file hello in hello Esplora soluzioni in Visual Studio.
2. Tramite l'aggiunta di testo, ad esempio, modificare il titolo di hello nella pagina hello.
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. Salvare il file hello.
4. Fare doppio clic su **voto** in hello Esplora soluzioni e scegliere **pubblica**. finestra di dialogo pubblicazione Hello viene visualizzato.
5. Fare clic su hello **versione manifesto** pulsante toochange hello versione servizio hello e applicazione.
6. Modifica di versione di hello di hello **codice** elemento sotto **VotingWebPkg** troppo "2.0.0", ad esempio e fare clic su **salvare**.

    ![Finestra di dialogo Modifica versione](./media/service-fabric-quickstart-dotnet/change-version.png)
7. In hello **pubblicare l'applicazione di Service Fabric** finestra di dialogo, la casella di controllo di controllo hello hello aggiornamento dell'applicazione e fare clic su **pubblica**.

    ![Impostazione di aggiornamento nella finestra di dialogo Pubblica](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. Aprire il browser e passare ad esempio l'indirizzo del cluster toohello sulla porta 19080 - `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.
9. Fare clic su hello **applicazioni** nodo nella visualizzazione ad albero di hello e quindi **gli aggiornamenti in corso** nel riquadro di destra hello. Viene visualizzato come aggiornamento hello transita attraverso domini di aggiornamento hello del cluster, assicurarsi che ogni dominio sia integro prima di procedere toohello accanto.
    ![Visualizzazione dell'aggiornamento in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)

    Service Fabric rende aggiornamenti sicuro in attesa di due minuti dopo l'aggiornamento del servizio hello in ogni nodo cluster hello. Prevedere hello intero aggiornamento tootake circa 8 minuti.

10. Durante l'aggiornamento di hello è in esecuzione, è possibile utilizzare ancora un'applicazione hello. Poiché si dispone di due istanze del servizio di hello in esecuzione nel cluster hello, alcune delle richieste può ottenere una versione aggiornata dell'applicazione hello, mentre altri potrebbero comunque essere la versione precedente di hello.

## <a name="next-steps"></a>Passaggi successivi
In questa guida introduttiva si è appreso come:

> [!div class="checklist"]
> * Creare un'applicazione mediante .NET e Service Fabric
> * Usare ASP.NET Core come front-end Web
> * Archiviare i dati dell'applicazione in un servizio con stato
> * Eseguire il debug dell'applicazione in locale
> * Distribuire hello applicazione tooa cluster in Azure
> * Applicazione hello di scalabilità orizzontale in più nodi
> * Eseguire un aggiornamento in sequenza delle applicazioni

toolearn ulteriori informazioni su Service Fabric e .NET, esaminare in questa esercitazione:
> [!div class="nextstepaction"]
> [Applicazione .NET in Service Fabric](service-fabric-tutorial-create-dotnet-app.md)