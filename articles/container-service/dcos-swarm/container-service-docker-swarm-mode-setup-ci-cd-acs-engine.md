---
title: "aaaCI/CD con motore del servizio contenitore di Azure e la modalità Swarm | Documenti Microsoft"
description: "Utilizzare il motore del servizio contenitore di Azure con Docker Swarm modalità, un registro di sistema contenitore di Azure e Visual Studio Team Services toodeliver continuamente un'applicazione .NET Core multi-contenitore"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: Docker, contenitori, microservizi, Swarm, Azure, Visual Studio Team Services, DevOps, motore del servizio contenitore di Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>CI/CD completo della pipeline toodeploy un'applicazione multi-contenitore nel servizio contenitore di Azure con il motore di ACS e Docker Swarm modalità utilizzando Visual Studio Team Services

*Questo articolo si basa su [CI/CD completo della pipeline toodeploy un'applicazione multi-contenitore nel servizio di Azure contenitore con Docker Swarm con Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentazione*

Oggi, uno di hello maggiori sfide durante lo sviluppo di applicazioni moderne per cloud hello toodeliver in grado di queste applicazioni in modo continuo. In questo articolo è illustrato come tooimplement un'integrazione completa continua e distribuzione (CI/CD) di pipeline utilizzando: 
* Motore del servizio contenitore di Azure con la modalità Docker Swarm
* Registro di sistema del contenitore di Azure
* Visual Studio Team Services

Questo articolo si basa su una semplice applicazione, disponibile in [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux) e sviluppata con ASP.NET Core. un'applicazione Hello è composta da quattro diversi servizi: tre web API e un solo web front-end:

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

obiettivo di Hello è toodeliver questa applicazione in modo continuo in un cluster di Docker Swarm modalità, tramite Visual Studio Team Services. Hello figura riportata di seguito i dettagli questa pipeline il recapito continuo:

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Di seguito è riportata una breve spiegazione dei passaggi di hello:

1. Le modifiche al codice sono repository di codice sorgente toohello commit (in questo esempio GitHub) 
2. GitHub attiva una compilazione in Visual Studio Team Services 
3. Visual Studio Team Services Ottiene hello la versione più recente di origini di hello e compila tutte le immagini di hello che compongono un'applicazione hello 
4. Visual Studio Team Services inserisce ogni immagine tooa Docker del Registro di sistema creato con il servizio di Azure del Registro di sistema contenitore hello 
5. Visual Studio Team Services attiva un nuovo rilascio 
6. versione di Hello esegue alcuni comandi tramite SSH nel nodo principale di hello Azure contenitore del servizio cluster 
7. Docker Swarm modalità cluster hello estrae hello versione immagini hello 
8. nuova versione di Hello di un'applicazione hello viene distribuito con Stack di Docker 

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, è necessario hello toocomplete seguenti attività:

- [Creare un cluster in modalità Swarm nel servizio contenitore di Azure con il motore del servizio contenitore di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Connettersi con cluster sciame hello contenitore nel servizio di Azure](../container-service-connect.md)
- [Creare un Registro di sistema del contenitore di Azure](../../container-registry/container-registry-get-started-portal.md)
- [Disporre di un account Visual Studio Team Services e aver creato un progetto di team](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Fork hello GitHub repository tooyour account GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> orchestrator Docker Swarm Hello contenitore nel servizio di Azure Usa autonomo legacy sciame. Attualmente, hello integrato [modalità sciame](https://docs.docker.com/engine/swarm/) (in Docker 1.12 e versione successiva) non è un agente di orchestrazione supportati nel servizio contenitore di Azure. Per questo motivo, si sta usando [motore ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), contributo della community [modello delle Guide rapide](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), o una soluzione di Docker in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Passaggio 1: Configurare l'account di Visual Studio Team Services 

In questa sezione viene configurato l'account di Visual Studio Team Services. gli endpoint di servizi di VSTS tooconfigure, nel progetto di Visual Studio Team Services, fare clic su hello **impostazioni** icona nella barra degli strumenti hello e selezionare **servizi**.

![Aprire l'endpoint dei servizi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Connettere Visual Studio Team Services e l'account Azure

Impostare una connessione tra il progetto VSTS e l'account Azure.

1. A sinistra di hello, fare clic su **nuovo Endpoint del servizio** > **Azure Resource Manager**.
2. tooauthorize VSTS toowork con un account Azure, selezionare il **sottoscrizione** e fare clic su **OK**.

    ![Visual Studio Team Services - Autorizzazione di Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Connettere Visual Studio Team Services e GitHub

Impostare una connessione tra il progetto VSTS e l'account GitHub.

1. A sinistra di hello, fare clic su **nuovo Endpoint del servizio** > **GitHub**.
2. Fare clic su tooauthorize VSTS toowork con l'account GitHub, **Authorize** e seguire la procedura di hello nella finestra di hello visualizzata.

    ![Visual Studio Team Services - Autorizzazione GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>Connettere VSTS tooyour Azure contenitore Servizio cluster

ultimi passaggi di Hello prima di ottenere nella pipeline CI/CD hello sono tooconfigure cluster di Docker Swarm connessioni esterne tooyour in Azure. 

1. Per cluster di Docker Swarm hello, aggiungere un endpoint di tipo **SSH**. Immettere le informazioni di connessione SSH hello del cluster sciame (nodo principale).

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

Le configurazioni di hello vengono effettuate a questo punto. Nei passaggi successivi hello creare pipeline di CI/CD hello che crea e distribuisce hello applicazione toohello Docker Swarm cluster. 

## <a name="step-2-create-hello-build-definition"></a>Passaggio 2: Creare una definizione di compilazione hello

In questo passaggio, si imposta una definizione di compilazione per il progetto di Visual Studio Team Services e definisce il flusso di lavoro di hello compilazione per le immagini contenitore

### <a name="initial-definition-setup"></a>Configurazione iniziale della definizione

1. toocreate una definizione di compilazione, collegare tooyour progetto di Visual Studio Team Services e fare clic su **compilazione & versione**. In hello **le definizioni di compilazione** fare clic su **+ nuovo**. 

    ![Visual Studio Team Services - Nuova definizione di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Seleziona hello **processo vuoto**.

    ![Visual Studio Team Services - Nuova definizione di compilazione vuota](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. Quindi, fare clic su hello **variabili** scheda e creare due nuove variabili: **RegistryURL** e **AgentURL**. Incollare i valori hello del Registro di sistema e DNS di agenti di Cluster.

    ![Visual Studio Team Services - Configurazione variabili di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. In hello **le definizioni di compilazione** pagina, aprire hello **trigger** scheda e configurare l'integrazione continua di hello compilazione toouse con biforcazione hello del progetto MyShop hello creato nei prerequisiti hello. Selezionare quindi **Modifiche batch**. Assicurarsi di selezionare *docker linux* come hello **ramo specifica**.

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Infine, fare clic su hello **opzioni** scheda e configurare coda dell'agente di hello predefinito troppo**ospitato anteprima Linux**.

    ![Visual Studio Team Services - Configurazione agente host](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Definire il flusso di lavoro di hello compilazione
passaggi successivi Hello definiscono il flusso di lavoro di hello compilazione. In primo luogo, è necessario origine hello tooconfigure di codice hello. toodo esso, selezionare **GitHub** e **repository** e **ramo** (docker linux).

![Visual Studio Team Services - Configurazione origine del codice](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Esistono cinque toobuild di immagini contenitore per hello *MyShop* dell'applicazione. Ogni immagine viene creata con Dockerfile si trova in cartelle di progetto hello hello:

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

Sono necessari due passaggi di Docker per ogni immagine, un'immagine di hello toobuild e un'immagine di hello toopush nel Registro di sistema di hello contenitore di Azure. 

1. Fare clic su un passaggio nel flusso di lavoro compilazione hello tooadd **+ Aggiungi istruzione di compilazione** e selezionare **Docker**.

    ![Visual Studio Team Services - Aggiunta passaggi di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Per ogni immagine, configurare un unico passaggio che utilizza hello `docker build` comando.

    ![Visual Studio Team Services - Compilazione Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Operazione di compilazione hello, selezionare il Registro di sistema di contenitore di Azure, hello **compilare un'immagine** azione e hello Dockerfile che definisce ogni immagine. Set hello **la Directory di lavoro** come directory radice di hello Dockerfile, definire hello **nome immagine**e selezionare **includere Tag più recente**.
    
    Nome dell'immagine di Hello è toobe nel formato: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Sostituire **[nome]** con nome immagine hello:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Per ogni immagine, configurare un secondo passaggio che utilizza hello `docker push` comando.

    ![Visual Studio Team Services - Push Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Per l'operazione di push hello, selezionare il Registro di sistema di contenitore di Azure, hello **Push un'immagine** azione, immettere hello **nome immagine** che viene compilato nel passaggio precedente hello e scegliere **includere Tag più recente** .

4. Dopo aver configurato la compilazione hello e push passaggi per ognuna delle cinque immagini hello, aggiungere che tre ulteriori passaggi hello del flusso di lavoro di compilazione.

   ![Visual Studio Team Services - Aggiunta di attività della riga di comando](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Un'attività da riga di comando che utilizza un hello tooreplace di script bash *RegistryURL* occorrenza nel file di docker compose.yml hello con variabile RegistryURL hello. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - Aggiornamento file Compose con URL del registro](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Un'attività da riga di comando che utilizza un hello tooreplace di script bash *AgentURL* occorrenza nel file di docker compose.yml hello con variabile AgentURL hello.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Un'attività che elimina hello aggiornato Scrivi file come un elemento di compilazione, pertanto può essere utilizzato in versione di hello. Hello seguente schermata per informazioni dettagliate, vedere.

         ![Visual Studio Team Services - Pubblicazione elemento](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Pubblicazione file Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Fare clic su **Salva e coda** tootest la definizione di compilazione.

   ![Visual Studio Team Services - Salva e accoda](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - Nuova coda](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Se hello **compilare** sia corretto, si dispone di toosee questa schermata:

  ![Visual Studio Team Services - Compilazione completata](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>Passaggio 3: Creare una definizione di versione di hello

Visual Studio Team Services consente troppo[gestire i rilasci in ambienti](https://www.visualstudio.com/team-services/release-management/). È possibile abilitare la distribuzione continua toomake assicurarsi che l'applicazione viene distribuita in diversi ambienti (ad esempio sviluppo, test, pre-produzione e produzione) in modo uniforme. È possibile creare un ambiente che rappresenti il cluster della modalità Docker Swarm del servizio contenitore di Azure.

![Visual Studio Team Services - versione tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configurazione iniziale del rilascio

1. Fare clic su una definizione di versione, toocreate **versioni** > **+ versione**

2. origine dell'artefatto hello tooconfigure, fare clic su **elementi** > **collega un'origine artefatto**. In questo caso, collegare il nuovo toohello build di rilascio definizione definito nel passaggio precedente hello. Successivamente, è disponibile nel processo di rilascio hello file docker compose.yml hello.

    ![Visual Studio Team Services - Rilascio elementi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. trigger di rilascio hello tooconfigure, fare clic su **trigger** e selezionare **distribuzione continua**. Imposta il trigger hello sull'hello stessa origine artefatto. Questa impostazione assicura che una nuova versione viene avviata quando hello compilazione viene completata correttamente.

    ![Visual Studio Team Services - Rilascio trigger](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. Fare clic su variabili di versione di hello tooconfigure, **variabili** e selezionare **+ variabile** toocreate tre nuove variabili con informazioni hello del Registro di sistema hello: **docker.username**, **docker.password**, e **docker.registry**. Incollare i valori hello del Registro di sistema e DNS di agenti di Cluster.

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Come illustrato nella schermata precedente hello, fare clic su hello **blocco** docker.password casella di controllo. Questa impostazione è la password di hello toorestrict importanti.
    >

### <a name="define-hello-release-workflow"></a>Definizione del flusso di lavoro di hello versione

flusso di lavoro versione Hello è composta da due attività da aggiungere.

1. Configurare un hello di copia toosecurely attività comporre file tooa *distribuire* cartella hello Docker Swarm nodo principale, utilizzando una connessione SSH hello configurate in precedenza. Hello seguente schermata per informazioni dettagliate, vedere.
    
    Cartella di origine: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services - Rilascio SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. Configurare un secondo tooexecute attività un toorun comando bash `docker` e `docker stack deploy` comandi sul nodo principale hello. Hello seguente schermata per informazioni dettagliate, vedere.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - Rilascio bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    comando Hello eseguito sul master hello utilizza hello Docker CLI e hello toodo di Docker Compose CLI hello seguenti attività:

    - Accedi al Registro di sistema toohello contenitore di Azure (Usa tre variabili di compilazione che sono definite nel hello **variabili** scheda)
    - Definire hello **DOCKER_HOST** toowork variabile con endpoint sciame hello (: 2375)
    - Passare toohello *distribuire* cartella che è stato creato da hello precedenti attività di copia sicuro e che contiene i file di docker compose.yml hello 
    - Eseguire `docker stack deploy` comandi pull nuove immagini hello e creare contenitori hello.

    >[!IMPORTANT]
    > Come illustrato nella schermata precedente hello, lasciare hello **esito negativo in STDERR** casella di controllo deselezionata. Questa impostazione consente toocomplete del processo di rilascio hello scadenza troppo`docker-compose` stampa i messaggi di diagnostica diversi, ad esempio i contenitori sono arresto o eliminato, nell'output di errore standard hello. Se si seleziona la casella di controllo di hello, Visual Studio Team Services indica che si sono verificati errori durante il rilascio di hello, anche se tutto va bene.
    >
3. Salvare la nuova definizione di rilascio.

## <a name="step-4-test-hello-cicd-pipeline"></a>Passaggio 4: Testare pipeline CI/CD hello

Dopo avere con configurazione hello, è ora tootest questa nuova pipeline CI/CD-ROM. tootest modo più semplice Hello è tooupdate hello origine codice e il commit hello modifiche nel repository GitHub. Pochi secondi dopo che si esegue il push codice hello, si noterà una nuova compilazione in esecuzione in Visual Studio Team Services. Una volta completata, una nuova versione viene attivata e distribuito una nuova versione di hello di un'applicazione hello in cluster del servizio di contenitore di Azure hello.

## <a name="next-steps"></a>Passaggi successivi

* Per ulteriori informazioni sull'elemento di configurazione/CD con Visual Studio Team Services, vedere hello [Panoramica di compilazione VSTS](https://www.visualstudio.com/docs/build/overview).
* Per ulteriori informazioni sul motore di ACS, vedere hello [repository GitHub motore ACS](https://github.com/Azure/acs-engine).
* Per ulteriori informazioni sulla modalità di Docker Swarm, vedere hello [Panoramica sulla modalità di Docker Swarm](https://docs.docker.com/engine/swarm/).
