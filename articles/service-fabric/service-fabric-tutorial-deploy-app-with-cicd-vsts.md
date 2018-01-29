---
title: Distribuire un'applicazione di Azure Service Fabric con integrazione continua (Team Services) | Microsoft Docs
description: Informazioni su come configurare l'integrazione e la distribuzione continue per un'applicazione di Service Fabric tramite Visual Studio Team Services.  Distribuire un'applicazione in un cluster di Service Fabric in Azure.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/13/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2fb7ab906208a58c0b5cd3af8b53188fbab94029
ms.sourcegitcommit: 3fca41d1c978d4b9165666bb2a9a1fe2a13aabb6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2017
---
# <a name="deploy-an-application-with-cicd-to-a-service-fabric-cluster"></a>Distribuire un'applicazione con integrazione continua/distribuzione continua in un cluster di Service Fabric
Questa esercitazione è la terza di una serie e illustra come configurare l'integrazione continua e la distribuzione continua per un'applicazione di Azure Service Fabric tramite Visual Studio Team Services.  È necessaria un'applicazione di Service Fabric esistente. Viene usata come esempio l'applicazione creata in [Compilare un'applicazione .NET](service-fabric-tutorial-create-dotnet-app.md).

Nella terza parte della serie si apprenderà come:

> [!div class="checklist"]
> * Aggiungere il controllo del codice sorgente al progetto
> * Creare una definizione di compilazione in Team Services
> * Creare una definizione di versione in Team Services
> * Distribuire automaticamente e aggiornare un'applicazione

In questa serie di esercitazioni si apprenderà come:
> [!div class="checklist"]
> * [Creare un'applicazione di Service Fabric .NET](service-fabric-tutorial-create-dotnet-app.md)
> * [Distribuire l'applicazione in un cluster remoto](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Configurare l'integrazione continua e la distribuzione continua usando Visual Studio Team Services
> * [Configurare il monitoraggio e la diagnostica per l'applicazione](service-fabric-tutorial-monitoring-aspnet.md)

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione:
- Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Installare Visual Studio 2017](https://www.visualstudio.com/) e installare i carichi di lavoro **Sviluppo di Azure** e **Sviluppo ASP.NET e Web**.
- [Installare Service Fabric SDK](service-fabric-get-started.md)
- Creare un cluster di Service Fabric per Windows in Azure, ad esempio [eseguendo questa esercitazione](service-fabric-tutorial-create-vnet-and-windows-cluster.md)
- Creare un [account di Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-the-voting-sample-application"></a>Scaricare l'applicazione di voto di esempio
Se l'applicazione di voto di esempio non è stata compilata nella [parte 1 di questa serie di esercitazioni](service-fabric-tutorial-create-dotnet-app.md), è possibile scaricarla. In una finestra di comando eseguire il comando seguente per clonare il repository dell'app di esempio nel computer locale.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Preparare un profilo di pubblicazione
Dopo aver [creato un'applicazione](service-fabric-tutorial-create-dotnet-app.md) e [distribuito l'applicazione in Azure](service-fabric-tutorial-deploy-app-to-party-cluster.md), si è pronti per configurare l'integrazione continua.  Prima di tutto, preparare un profilo di pubblicazione all'interno dell'applicazione destinato all'uso da parte del processo di distribuzione eseguito in Team Services.  Il profilo di pubblicazione deve essere configurato impostando il cluster preparato in precedenza come destinazione.  Avviare Visual Studio e aprire un progetto di applicazione di Service Fabric esistente.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sull'applicazione e scegliere **Pubblica**.

Scegliere un profilo di destinazione all'interno del progetto di applicazione da usare per il flusso di lavoro di integrazione continua, ad esempio Cloud.  Specificare l'endpoint di connessione del cluster.  Selezionare la casella di controllo **Aggiorna l'applicazione** in modo che l'applicazione venga aggiornata per ogni distribuzione in Team Services.  Fare clic sul collegamento ipertestuale **Salva** per salvare le impostazioni per il profilo di pubblicazione e quindi fare clic su **Annulla** per chiudere la finestra di dialogo.  

![Profilo di push][publish-app-profile]

## <a name="share-your-visual-studio-solution-to-a-new-team-services-git-repo"></a>Condividere la soluzione di Visual Studio in un nuovo repository GIT di Team Services
È possibile condividere i file di origine dell'applicazione in un progetto team in Team Services, in modo da poter generare le compilazioni.  

Creare un nuovo repository Git locale per il progetto selezionando **Aggiungi al controllo del codice sorgente** -> **Git** sulla barra di stato nell'angolo inferiore destro di Visual Studio. 

Nella visualizzazione **Push** in **Team Explorer**, selezionare il pulsante **Pubblica repository GIT** nella sezione **Effettua il push in Visual Studio Team Services**.

![Pubblicare il repository GIT][push-git-repo]

Controllare la posta elettronica e selezionare il proprio account nell'elenco a discesa **Dominio Team Services**. Immettere il nome del repository e selezionare **Pubblica repository**.

![Pubblicare il repository GIT][publish-code]

Con la pubblicazione del repository viene creato un nuovo progetto team nell'account con lo stesso nome del repository locale. Per creare il repository in un progetto team esistente, fare clic su **Avanzate** accanto al nome del **Repository** e selezionare un progetto team. È possibile visualizzare il codice sul Web selezionando **Visualizza nel Web**.

## <a name="configure-continuous-delivery-with-vsts"></a>Configurare il recapito continuo con VSTS
Una definizione di compilazione di Team Services descrive un flusso di lavoro costituito da un set di istruzioni di compilazione che vengono eseguite in sequenza. Creare una definizione di compilazione che produce un pacchetto di applicazione di Service Fabric e altri elementi, per la distribuzione in un cluster di Service Fabric. Sono disponibili maggiori informazioni sulle [definizioni di compilazione di Team Services](https://www.visualstudio.com/docs/build/define/create). 

Una definizione di versione di Team Services descrive un flusso di lavoro che distribuisce un pacchetto di applicazione in un cluster. Se usate insieme, la definizione di compilazione e la definizione di versione eseguono l'intero flusso di lavoro a partire dai file di origine fino alla creazione di un'applicazione funzionante nel cluster. Sono disponibili maggiori informazioni sulle [definizioni di versione](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)di Team Services.

### <a name="create-a-build-definition"></a>Creare una definizione di compilazione
Aprire un web browser e passare al nuovo progetto team in: [https://&lt;myaccount&gt;.visualstudio.com/Voting/Voting%20Team/_git/Voting](https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting). 

Selezionare la scheda **Compilazione e versione**, **Compilazioni** e quindi **+ Nuova definizione**.  In **Seleziona un modello** selezionare il modello **Applicazione Azure Service Fabric** e quindi fare clic su **Applica**. 

![Scegliere il modello di compilazione][select-build-template] 

In **attività**, immettere "Ospitato VS2017" come il **coda dell'agente**. 

![Selezionare le attività][save-and-queue]

In **trigger**, abilitare l'integrazione continua impostando **attivare lo stato**.  Selezionare **salvare e coda** per avviare manualmente una compilazione.  

![Selezionare i trigger][save-and-queue2]

Si basa inoltre trigger push o check-in. Per controllare lo stato di avanzamento della compilazione, passare alla scheda **Compilazioni**.  Dopo aver verificato che la compilazione viene eseguita correttamente, definire una definizione di versione per la distribuzione dell'applicazione in un cluster. 

### <a name="create-a-release-definition"></a>Creare una definizione di versione  

Selezionare la scheda **Compilazione e versione**, **Versioni** e quindi **+ Nuova definizione**.  In **selezionare un modello**, selezionare il **distribuzione dell'infrastruttura dei servizi Azure** modello dall'elenco e quindi **applica**.  

![Scegliere il modello di versione][select-release-template]

Selezionare **attività**->**1 ambiente** e quindi **+ nuovo** per aggiungere una nuova connessione di cluster.

![Aggiungere la connessione cluster][add-cluster-connection]

Nel **Aggiungi nuova connessione al servizio Fabric** visualizzare selezionare **basata su certificati** o **Azure Active Directory** l'autenticazione.  Specificare un nome di connessione di "mysftestcluster" e un endpoint del cluster di "tcp://mysftestcluster.southcentralus.cloudapp.azure.com:19000" (o l'endpoint del cluster che a cui si sta distribuendo). 

Per l'autenticazione basata su certificato, aggiungere il **identificazione personale del certificato Server** del certificato del server utilizzato per creare il cluster.  In **certificato Client**, aggiungere la codifica base 64 del file del certificato client. In tale campo per informazioni su come ottenere tale rappresentazione con codifica base 64 del certificato, vedere il finestra popup della Guida. Aggiungere anche il **Password** per il certificato.  È possibile utilizzare il certificato del server o del cluster se non si dispone di un certificato client separato. 

Per le credenziali di Azure Active Directory, aggiungere il **identificazione personale del certificato Server** del certificato del server utilizzato per creare il cluster e le credenziali da utilizzare per connettersi al cluster in cui si desidera il **Username** e **Password** campi. 

Fare clic su **Aggiungi** per salvare la connessione del cluster.

Successivamente, aggiungere un artefatto di compilazione alla pipeline, pertanto la definizione di versione è possibile trovare l'output di compilazione. Selezionare **Pipeline** e **elementi**->**+ Aggiungi**.  In **origine (definizione di compilazione)**, selezionare la definizione di compilazione creata in precedenza.  Fare clic su **Aggiungi** per salvare l'artefatto di compilazione.

![Aggiungere l'elemento][add-artifact]

Abilitare un trigger di distribuzione continua in modo che una versione viene creata automaticamente al termine della compilazione. Fare clic sull'icona a forma di fulmine nell'elemento, abilitare il trigger e fare clic su **salvare** per salvare la definizione di versione.

![Abilitare i trigger][enable-trigger]

Selezionare **+Release** -> **Crea versione** -> **Crea** per creare manualmente una versione.  Verificare che la distribuzione venga completata correttamente e che l'applicazione sia in esecuzione nel cluster.  Aprire un web browser e passare a [http://mysftestcluster.southcentralus.cloudapp.azure.com:19080Esplora/](http://mysftestcluster.southcentralus.cloudapp.azure.com:19080/Explorer/).  Si noti la versione dell'applicazione, in questo esempio è "1.0.0.20170616.3". 

## <a name="commit-and-push-changes-trigger-a-release"></a>Eseguire commit e push delle modifiche, attivare la compilazione di una versione
Per verificare che la pipeline di integrazione continua funzioni correttamente, è possibile archiviare alcune modifiche al codice in Team Services.    

Durante la scrittura del codice, le modifiche vengono rilevate automaticamente da Visual Studio. Per eseguire il commit delle modifiche nel repository GIT locale, selezionare l'icona di modifiche in sospeso (![In sospeso][pending]) sulla barra di stato in basso a destra.

Nella visualizzazione **Modifiche** in Team Explorer aggiungere un messaggio che descrive l'aggiornamento ed eseguire il commit delle modifiche.

![Esegui commit di tutto][changes]

Selezionare l'icona della barra di stato delle modifiche non pubblicate (![Modifiche non pubblicate][unpublished-changes]) oppure la visualizzazione Sincronizza in Team Explorer. Selezionare **Push** per aggiornare il codice in Team Services/TFS.

![Effettuare il push delle modifiche][push]

Il push delle modifiche in Team Services attiva automaticamente una compilazione.  Quando la definizione di compilazione viene completata correttamente, viene creata automaticamente una versione con avvio dell'aggiornamento dell'applicazione nel cluster.

Per controllare lo stato di avanzamento della compilazione, passare alla scheda **Compilazioni** in **Team Explorer** in Visual Studio.  Dopo aver verificato che la compilazione viene eseguita correttamente, definire una definizione di versione per la distribuzione dell'applicazione in un cluster.

Verificare che la distribuzione venga completata correttamente e che l'applicazione sia in esecuzione nel cluster.  Aprire un web browser e passare a [http://mysftestcluster.southcentralus.cloudapp.azure.com:19080Esplora/](http://mysftestcluster.southcentralus.cloudapp.azure.com:19080/Explorer/).  Prendere nota della versione dell'applicazione, che in questo esempio è "1.0.0.20170815.3".

![Service Fabric Explorer][sfx1]

## <a name="update-the-application"></a>Aggiornare l'applicazione
Apportare modifiche al codice nell'applicazione.  Salvare le modifiche ed eseguirne il commit, come descritto nei passaggi precedenti.

Dopo l'avvio dell'aggiornamento dell'applicazione, è possibile controllare lo stato di aggiornamento in Service Fabric Explorer:

![Service Fabric Explorer][sfx2]

L'aggiornamento dell'applicazione potrebbe richiedere alcuni minuti. Una volta completato l'aggiornamento, l'applicazione eseguirà la versione successiva,  in questo esempio la versione "1.0.0.20170815.4".

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Passaggi successivi
Questa esercitazione illustra come:

> [!div class="checklist"]
> * Aggiungere il controllo del codice sorgente al progetto
> * Creare una definizione di compilazione
> * Creare una definizione di versione
> * Distribuire automaticamente e aggiornare un'applicazione

Passare all'esercitazione successiva:
> [!div class="nextstepaction"]
> [Configurare il monitoraggio e la diagnostica per l'applicazione](service-fabric-tutorial-monitoring-aspnet.md) 


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[save-and-queue]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SaveAndQueue.png
[save-and-queue2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SaveAndQueue2.png
[select-release-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectReleaseTemplate.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[add-artifact]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddArtifact.png
[enable-trigger]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/EnableTrigger.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
