---
title: un'applicazione Azure Service Fabric con l'integrazione continua (Team Services) aaaDeploy | Documenti Microsoft
description: Informazioni su come tooset di integrazione continua e distribuzione per un'applicazione di Service Fabric con Visual Studio Team Services.  Distribuire un cluster di Service Fabric tooa di applicazione in Azure.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Distribuire un'applicazione con i cluster di Service Fabric tooa CI/CD-ROM
In questa esercitazione è parte 3 di una serie e viene descritto come tooset di integrazione continua e distribuzione per un'applicazione Azure Service Fabric con Visual Studio Team Services.  È necessaria un'applicazione di Service Fabric esistente, in cui è stato creato un'applicazione hello [compilare un'applicazione .NET](service-fabric-tutorial-create-dotnet-app.md) viene utilizzato come esempio.

Nel parte tre serie hello, si apprenderà come:

> [!div class="checklist"]
> * Aggiungi progetto di origine controllo tooyour
> * Creare una definizione di compilazione in Team Services
> * Creare una definizione di versione in Team Services
> * Distribuire automaticamente e aggiornare un'applicazione

In questa serie di esercitazioni si apprenderà come:
> [!div class="checklist"]
> * [Creare un'applicazione di Service Fabric .NET](service-fabric-tutorial-create-dotnet-app.md)
> * [Distribuire hello applicazione tooa remota del cluster](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Configurare l'integrazione continua e la distribuzione continua usando Visual Studio Team Services

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione:
- Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Installare Visual Studio 2017](https://www.visualstudio.com/) e installare hello **lo sviluppo di Azure** e **sviluppo web ASP.NET e** i carichi di lavoro.
- [Installare hello Service Fabric SDK](service-fabric-get-started.md)
- Creare un'applicazione di Service Fabric, ad esempio [eseguendo questa esercitazione](service-fabric-tutorial-create-dotnet-app.md). 
- Creare un cluster di Service Fabric per Windows in Azure, ad esempio [eseguendo questa esercitazione](service-fabric-tutorial-create-cluster-azure-ps.md)
- Creare un [account di Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Scaricare l'applicazione di esempio hello voto
Se si non compila l'applicazione di esempio hello voto [parte 1 di questa serie di esercitazioni](service-fabric-tutorial-create-dotnet-app.md), è possibile scaricarlo. In una finestra di comando, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Preparare un profilo di pubblicazione
Adesso che è stato [creato un'applicazione](service-fabric-tutorial-create-dotnet-app.md) e [distribuito tooAzure applicazione hello](service-fabric-tutorial-deploy-app-to-party-cluster.md), si è pronti tooset l'integrazione continua.  Preparare un profilo di pubblicazione all'interno dell'applicazione per l'uso dal processo di distribuzione hello eseguita all'interno di Team Services.  profilo di pubblicazione Hello deve essere configurato tootarget hello cluster creato in precedenza.  Avviare Visual Studio e aprire un progetto di applicazione di Service Fabric esistente.  In **Esplora**, fare doppio clic su un'applicazione hello e selezionare **pubblica... **.

Scegliere un profilo di destinazione all'interno del toouse di progetto di applicazione del flusso di lavoro di integrazione continua, ad esempio Cloud.  Specificare l'endpoint della connessione hello cluster.  Controllare hello **hello aggiornamento applicazione** casella di controllo in modo che l'applicazione viene aggiornata per ogni distribuzione di Team Services.  Fare clic su hello **salvare** toohello di collegamento ipertestuale toosave hello impostazioni profilo di pubblicazione e quindi fare clic su **Annulla** tooclose hello finestra di dialogo.  

![Profilo di push][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Condividere i repository Git di Team Services nuova di Visual Studio soluzione tooa
Condividere i file di origine dell'applicazione creato tooa il progetto team in Team Services, pertanto non è possibile generare.  

Creare un nuovo repository Git locale per il progetto selezionando **aggiungere tooSource controllo** -> **Git** sulla barra di stato hello in hello angolo inferiore destro di Visual Studio. 

In hello **Push** visualizzare in **Team Explorer**selezionare hello **pubblicare repository Git** pulsante sotto **Push tooVisual Studio Team Services**.

![Pubblicare il repository GIT][push-git-repo]

Controllare la posta elettronica e selezionare l'account in hello **Team servizi di dominio** elenco a discesa. Immettere il nome del repository e selezionare **Pubblica repository**.

![Pubblicare il repository GIT][publish-code]

Pubblicazione di repository hello crea un nuovo progetto team nell'account con stesso nome come repository locale hello hello. repository di hello toocreate in un progetto team esistente, fare clic su **avanzate** Avanti troppo**Repository** nome e selezionare un progetto team. È possibile visualizzare il codice del sito Web hello selezionando **visualizzato nel web hello**.

## <a name="configure-continuous-delivery-with-vsts"></a>Configurare il recapito continuo con VSTS
Una definizione di compilazione di Team Services descrive un flusso di lavoro costituito da un set di istruzioni di compilazione che vengono eseguite in sequenza. Creare una definizione di compilazione che produce un pacchetto di applicazione di Service Fabric e altri elementi, i cluster di Service Fabric tooa toodeploy. Sono disponibili maggiori informazioni sulle [definizioni di compilazione di Team Services](https://www.visualstudio.com/docs/build/define/create). 

Una definizione di versione di Team Services viene descritto un flusso di lavoro che consente di distribuire un cluster tooa pacchetto di applicazione. Se utilizzati insieme, hello definizione di compilazione e definizione di versione eseguire hello intero flusso di lavoro a partire da tooending i file di origine con un'applicazione in esecuzione nel cluster. Sono disponibili maggiori informazioni sulle [definizioni di versione](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)di Team Services.

### <a name="create-a-build-definition"></a>Creare una definizione di compilazione
Aprire un web browser e passare tooyour un nuovo progetto team in: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Seleziona hello **compilazione & versione** scheda, quindi **compilazioni**, quindi **+ nuova definizione**.  In **selezionare un modello**selezionare hello **applicazione di Azure Service Fabric** modello e fare clic su **applica**. 

![Scegliere il modello di compilazione][select-build-template] 

Hello voto applicazione contiene un progetto .NET Core, aggiungere un'attività che consente di ripristinare le dipendenze di hello. In hello **attività** visualizzazione, selezionare **+ Aggiungi attività** in basso a sinistra di hello. Ricerca basata su attività della riga di comando di "Riga di comando" toofind hello, quindi fare clic su **Aggiungi**. 

![Aggiungere un'attività][add-task] 

Nella nuova attività hello, immettere "Esegui dotnet.exe" in **nome visualizzato**, "dotnet.exe" in **strumento**e "ripristino" in **argomenti**. 

![Nuova attività][new-task] 

In hello **trigger** consente di visualizzare, fare clic su hello **attiva trigger** passare in **integrazione continua**. 

Selezionare **Salva e coda** e immettere "Ospitato VS2017" come hello **coda dell'agente**. Selezionare **coda** toomanually avviare una compilazione.  Le compilazioni vengono attivate anche al momento del push o dell'archiviazione.

toocheck lo stato di avanzamento di compilazione, switch toohello **compilazioni** scheda.  Dopo aver verificato che la compilazione hello viene eseguita correttamente, è possibile definire una definizione di versione che distribuisce il cluster tooa dell'applicazione. 

### <a name="create-a-release-definition"></a>Creare una definizione di versione  

Seleziona hello **compilazione & versione** scheda, quindi **versioni**, quindi **+ nuova definizione**.  In **Crea definizione di versione**selezionare hello **distribuzione dell'infrastruttura dei servizi Azure** modello dall'elenco hello e fare clic su **Avanti**.  Seleziona hello **compilare** del codice sorgente, controllo hello **distribuzione continua** casella e fare clic su **crea**. 

In hello **ambienti** consente di visualizzare, fare clic su **Aggiungi** toohello destra **connessione Cluster**.  Specificare un nome di connessione di "mysftestcluster", un endpoint del cluster di "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" e hello Azure Active Directory o le credenziali del certificato per il cluster hello. Per le credenziali di Azure Active Directory, definire le credenziali di hello da toouse tooconnect toohello cluster in hello **Username** e **Password** campi. Per l'autenticazione basata su certificato, definire hello Base64 codifica del file del certificato client hello in hello **certificato Client** campo.  Vedere la finestra popup della Guida hello in tale campo per informazioni su come tooget tale valore.  Se il certificato è protetto da password, è possibile definire password hello in hello **Password** campo.  Fare clic su **salvare** toosave definizione di versione di hello.

![Aggiungere la connessione cluster][add-cluster-connection] 

Fare clic su **Esegui su agente** e quindi selezionare **Hosted VS2017** per **Coda di distribuzione**. Fare clic su **salvare** toosave definizione di versione di hello.

![Esegui su agente][run-on-agent]

Selezionare **+ rilasciare** -> **creare rilasciare** -> **crea** toomanually crea una versione.  Verificare che la distribuzione di hello ha avuto esito positivo e applicazione hello è in esecuzione nel cluster hello.  Aprire un web browser e passare troppo[http://mysftestcluster.westus.cloudapp.azure.com:19080Esplora/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Si noti versione dell'applicazione hello, in questo esempio è "1.0.0.20170616.3". 

## <a name="commit-and-push-changes-trigger-a-release"></a>Eseguire commit e push delle modifiche, attivare la compilazione di una versione
archiviando alcune modifiche al codice tooTeam Services funziona tooverify che hello pipeline integrazione continua.    

Durante la scrittura del codice, le modifiche vengono rilevate automaticamente da Visual Studio. Eseguire il commit di repository Git locale di modifiche tooyour selezionando hello in sospeso (icona di modifiche![In sospeso][pending]) dalla barra di stato hello in basso a destra hello.

In hello **modifiche** visualizzare in Team Explorer e aggiungere un messaggio che descrive l'aggiornamento, eseguire il commit delle modifiche.

![Esegui commit di tutto][changes]

Icona della barra di stato modifiche non pubblicate selezionare hello (![presenti modifiche non pubblicate][unpublished-changes]) o hello vista di sincronizzazione in Team Explorer. Selezionare **Push** tooupdate il codice in Team Services/TFS.

![Effettuare il push delle modifiche][push]

Push hello modifiche tooTeam Services automaticamente trigger una compilazione.  Quando la definizione di compilazione hello è stata completata correttamente, una versione viene creata automaticamente e inizia l'aggiornamento di un'applicazione hello in cluster hello.

toocheck lo stato di avanzamento di compilazione, switch toohello **compilazioni** scheda **Team Explorer** in Visual Studio.  Dopo aver verificato che la compilazione hello viene eseguita correttamente, è possibile definire una definizione di versione che distribuisce il cluster tooa dell'applicazione.

Verificare che la distribuzione di hello ha avuto esito positivo e applicazione hello è in esecuzione nel cluster hello.  Aprire un web browser e passare troppo[http://mysftestcluster.westus.cloudapp.azure.com:19080Esplora/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Si noti versione dell'applicazione hello, in questo esempio è "1.0.0.20170815.3".

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Aggiornare un'applicazione hello
Apportare le modifiche al codice in un'applicazione hello.  Salvare ed eseguire il commit delle modifiche di hello, seguendo i passaggi precedenti hello.

Una volta hello l'aggiornamento di un'applicazione hello inizia, è possibile controllare lo stato dell'aggiornamento hello in Service Fabric Explorer:

![Service Fabric Explorer][sfx2]

aggiornamento dell'applicazione Hello potrebbe richiedere alcuni minuti. Una volta completato l'aggiornamento di hello, verrà eseguito applicazione hello prossima versione di hello.  in questo esempio la versione "1.0.0.20170815.4".

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Aggiungi progetto di origine controllo tooyour
> * Creare una definizione di compilazione
> * Creare una definizione di versione
> * Distribuire automaticamente e aggiornare un'applicazione

Ora che aver distribuito un'applicazione e configurato l'integrazione continua, provare a seguente hello:
- [Aggiornare un'app](service-fabric-application-upgrade.md)
- [Testare un'app](service-fabric-testability-overview.md) 
- [Monitorare e diagnosticare](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
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
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png