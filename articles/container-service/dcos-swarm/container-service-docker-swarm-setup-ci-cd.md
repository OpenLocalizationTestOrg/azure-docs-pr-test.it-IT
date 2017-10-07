---
title: aaaCI/CD con il servizio contenitore di Azure e sciame | Documenti Microsoft
description: Utilizzare il servizio contenitore di Azure con Docker Swarm un registro di sistema contenitore di Azure e Visual Studio Team Services toodeliver continuamente un'applicazione .NET Core multi-contenitore
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, contenitori, microservizi, Swarm, Azure, Visual Studio Team Services, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>CI/CD completo della pipeline toodeploy un'applicazione multi-contenitore nel servizio di Azure contenitore con Docker Swarm con Visual Studio Team Services

Uno dei hello maggiori sfide durante lo sviluppo di applicazioni moderne per cloud hello toodeliver in grado di queste applicazioni in modo continuo. In questo articolo informazioni su come creare un'integrazione completa continua tooimplement e pipeline di distribuzione (CI/CD) utilizzando il servizio contenitore di Azure con Visual Studio Team Services, Azure del Registro di sistema contenitore e Docker Swarm e gestione del rilascio.

Questo articolo si basa su una semplice applicazione, disponibile in [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs) e sviluppata con ASP.NET Core. un'applicazione Hello è composta da quattro diversi servizi: tre web API e un solo web front-end:

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

obiettivo di Hello è toodeliver questa applicazione in modo continuo in un cluster di Docker Swarm, tramite Visual Studio Team Services. Hello figura riportata di seguito i dettagli questa pipeline il recapito continuo:

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Di seguito è riportata una breve spiegazione dei passaggi di hello:

1. Le modifiche al codice sono repository di codice sorgente toohello commit (in questo esempio GitHub) 
2. GitHub attiva una compilazione in Visual Studio Team Services 
3. Visual Studio Team Services Ottiene hello la versione più recente di origini di hello e compila tutte le immagini di hello che compongono un'applicazione hello 
4. Visual Studio Team Services inserisce ogni immagine tooa Docker del Registro di sistema creato con il servizio di Azure del Registro di sistema contenitore hello 
5. Visual Studio Team Services attiva un nuovo rilascio 
6. versione di Hello esegue alcuni comandi tramite SSH nel nodo principale di hello Azure contenitore del servizio cluster 
7. Docker sciame hello cluster esegue il pull hello versione più recente di immagini hello 
8. nuova versione di Hello di un'applicazione hello viene distribuito tramite Docker Compose 

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, è necessario hello toocomplete seguenti attività:

- [Creare un cluster Swarm nel servizio contenitore di Azure](container-service-deployment.md)
- [Connettersi con cluster sciame hello contenitore nel servizio di Azure](../container-service-connect.md)
- [Creare un Registro di sistema del contenitore di Azure](../../container-registry/container-registry-get-started-portal.md)
- [Disporre di un account Visual Studio Team Services e aver creato un progetto di team](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Fork hello GitHub repository tooyour account GitHub](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

È inoltre necessario disporre di un computer Ubuntu (14.04 o 16.04) con Docker. Il computer è usato da Visual Studio Team Services hello durante la compilazione e versione processi. Un modo toocreate questo computer è un immagine hello toouse disponibile in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/). 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Passaggio 1: Configurare l'account di Visual Studio Team Services 

In questa sezione viene configurato l'account di Visual Studio Team Services.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Configurare un agente di compilazione Linux di Visual Studio Team Services

immagini Docker toocreate e push che compilare queste immagini in un registro di sistema di contenitore di Azure da Visual Studio Team Services, è necessario un agente Linux tooregister. Sono disponibili queste opzioni di installazione:

* [Distribuire un agente in Linux](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Usare l'agente di VSTS hello toorun Docker](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Installare l'estensione Docker integrazione VSTS hello

Microsoft fornisce un toowork estensione di Visual Studio Team Services con Docker in compilazione e i processi di rilascio. Questa estensione è disponibile in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker). Fare clic su **installare** tooadd questo account VSTS tooyour estensione:

![Installare hello integrazione di Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

Verrà chiesto di account VSTS tooyour tooconnect utilizzando le credenziali. 

### <a name="connect-visual-studio-team-services-and-github"></a>Connettere Visual Studio Team Services e GitHub

Impostare una connessione tra il progetto VSTS e l'account GitHub.

1. Nel progetto di Visual Studio Team Services, fare clic su hello **impostazioni** icona nella barra degli strumenti hello e selezionare **servizi**.

    ![Visual Studio Team Services - Connessione esterna](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. A sinistra di hello, fare clic su **nuovo Endpoint del servizio** > **GitHub**.

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. Fare clic su tooauthorize VSTS toowork con l'account GitHub, **Authorize** e seguire la procedura di hello nella finestra di hello visualizzata.

    ![Visual Studio Team Services - Autorizzazione GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>Connettersi al Registro di sistema VSTS tooyour contenitore di Azure e i cluster del servizio di contenitore di Azure

ultimi passaggi di Hello prima di ottenere nella pipeline CI/CD hello sono del Registro di sistema di tooconfigure connessioni esterne tooyour contenitore e il cluster Docker Swarm in Azure. 

1. In hello **servizi** impostazioni del progetto di Visual Studio Team Services, aggiungere un endpoint del servizio di tipo **Registro di sistema Docker**. 

2. Nella finestra popup di hello che viene visualizzata, immettere hello URL e le credenziali di hello Azure contenitore del Registro di sistema.

    ![Visual Studio Team Services - Docker Registry](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Per cluster di Docker Swarm hello, aggiungere un endpoint di tipo **SSH**. Immettere le informazioni sulla connessione del cluster sciame hello SSH.

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

Le configurazioni di hello vengono effettuate a questo punto. Nei passaggi successivi hello creare pipeline di CI/CD hello che crea e distribuisce hello applicazione toohello Docker Swarm cluster. 

## <a name="step-2-create-hello-build-definition"></a>Passaggio 2: Creare una definizione di compilazione hello

In questo passaggio, si imposta definitionfor una compilazione del progetto di Visual Studio Team Services e definisce il flusso di lavoro di hello compilazione per le immagini contenitore

### <a name="initial-definition-setup"></a>Configurazione iniziale della definizione

1. toocreate una definizione di compilazione, collegare tooyour progetto di Visual Studio Team Services e fare clic su **compilazione & versione**. 

2. In hello **le definizioni di compilazione** fare clic su **+ nuovo**. Seleziona hello **vuoto** modello.

    ![Visual Studio Team Services - Nuova definizione di compilazione](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. Configurare una nuova compilazione hello con un'origine di repository GitHub, controllo **integrazione continua**e coda dell'agente selezionare hello in cui è stato registrato l'agente Linux. Fare clic su **crea** toocreate hello definizione di compilazione.

    ![Visual Studio Team Services - Creazione definizione di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. In hello **le definizioni di compilazione** pagina, aprire innanzitutto hello **Repository** scheda e configurare hello compilazione toouse hello la biforcazione del progetto MyShop hello creato nei prerequisiti hello. Assicurarsi di selezionare *acs docs* come hello **ramo predefinito**.

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. In hello **trigger** , configurare hello compilazione toobe attivata dopo ciascun commit. Selezionare **Integrazione continua** e **Modifiche bacth**.

    ![Visual Studio Team Services - Configurazione trigger di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Definire il flusso di lavoro di hello compilazione
passaggi successivi Hello definiscono il flusso di lavoro di hello compilazione. Esistono cinque toobuild di immagini contenitore per hello *MyShop* dell'applicazione. Ogni immagine viene creata con Dockerfile si trova in cartelle di progetto hello hello:

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

Sono necessari due passaggi Docker tooadd per ogni immagine, un'immagine di hello toobuild e un'immagine di hello toopush nel Registro di sistema di hello contenitore di Azure. 

1. Fare clic su un passaggio nel flusso di lavoro compilazione hello tooadd **+ Aggiungi istruzione di compilazione** e selezionare **Docker**.

    ![Visual Studio Team Services - Aggiunta passaggi di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. Per ogni immagine, configurare un unico passaggio che utilizza hello `docker build` comando.

    ![Visual Studio Team Services - Compilazione Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Operazione di compilazione hello, selezionare il Registro di sistema di contenitore di Azure, hello **compilare un'immagine** azione e hello Dockerfile che definisce ogni immagine. Set hello **contesto di compilazione** come hello Dockerfile directory radice e definire hello **nome immagine**. 
    
    Come mostrato nella precedente schermata hello, il nome di immagine hello deve iniziare con hello URI Azure contenitore del Registro di sistema. (È anche possibile utilizzare un tag di hello tooparameterize variabili di compilazione dell'immagine di hello, ad esempio ID build hello in questo esempio.)

3. Per ogni immagine, configurare un secondo passaggio che utilizza hello `docker push` comando.

    ![Visual Studio Team Services - Push Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Per l'operazione di push hello, selezionare il Registro di sistema di contenitore di Azure, hello **Push un'immagine** action e immettere hello **nome immagine** che viene compilato nel passaggio precedente hello.

4. Dopo aver configurato la compilazione hello e push passaggi per ognuna delle cinque immagini hello, aggiungere che altri due passaggi hello del flusso di lavoro di compilazione.

    a. Un'attività da riga di comando che utilizza un hello tooreplace di script bash *BuildNumber* occorrenza nel file di docker compose.yml hello con hello corrente compilare ID. Hello seguente schermata per informazioni dettagliate, vedere.

    ![Visual Studio Team Services - Aggiornamento file Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Un'attività che elimina hello aggiornato Scrivi file come un elemento di compilazione, pertanto può essere utilizzato in versione di hello. Hello seguente schermata per informazioni dettagliate, vedere.

    ![Visual Studio Team Services - Pubblicazione file Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. Fare clic su **Salva** e assegnare un nome alla definizione di compilazione.

## <a name="step-3-create-hello-release-definition"></a>Passaggio 3: Creare una definizione di versione di hello

Visual Studio Team Services consente troppo[gestire i rilasci in ambienti](https://www.visualstudio.com/team-services/release-management/). È possibile abilitare la distribuzione continua toomake assicurarsi che l'applicazione viene distribuita in diversi ambienti (ad esempio sviluppo, test, pre-produzione e produzione) in modo uniforme. È possibile creare un nuovo ambiente che rappresenti il cluster Docker Swarm del servizio contenitore di Azure.

![Visual Studio Team Services - versione tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configurazione iniziale del rilascio

1. Fare clic su una definizione di versione, toocreate **versioni** > **+ versione**

2. origine dell'artefatto hello tooconfigure, fare clic su **elementi** > **collega un'origine artefatto**. In questo caso, collegare il nuovo toohello build di rilascio definizione definito nel passaggio precedente hello. In questo modo, i file di docker compose.yml hello è disponibili nel processo di rilascio hello.

    ![Visual Studio Team Services - Rilascio elementi](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. trigger di rilascio hello tooconfigure, fare clic su **trigger** e selezionare **distribuzione continua**. Imposta il trigger hello sull'hello stessa origine artefatto. Questa impostazione assicura che una nuova versione viene avviata non appena hello compilazione viene completata correttamente.

    ![Visual Studio Team Services - Rilascio trigger](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Definizione del flusso di lavoro di hello versione

flusso di lavoro versione Hello è composta da due attività da aggiungere.

1. Configurare un hello di copia toosecurely attività comporre file tooa *distribuire* cartella hello Docker Swarm nodo principale, utilizzando una connessione SSH hello configurate in precedenza. Hello seguente schermata per informazioni dettagliate, vedere.

    ![Visual Studio Team Services - Rilascio SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. Configurare un secondo tooexecute attività un toorun comando bash `docker` e `docker-compose` comandi sul nodo principale hello. Hello seguente schermata per informazioni dettagliate, vedere.

    ![Visual Studio Team Services - Rilascio bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    comando Hello eseguito hello utilizzare master hello Docker CLI e hello toodo di Docker Compose CLI hello seguenti attività:

    - Registro di sistema di account di accesso toohello contenitore di Azure (Usa tre variab'les di compilazione che sono definiti nel hello **variabili** scheda)
    - Definire hello **DOCKER_HOST** toowork variabile con endpoint sciame hello (: 2375)
    - Passare toohello *distribuire* cartella che è stato creato da hello precedenti attività di copia sicuro e che contiene i file di docker compose.yml hello 
    - Eseguire `docker-compose` comandi che recuperano nuove immagini hello, arrestare i servizi di hello, rimuovere servizi hello e creare contenitori hello.

    >[!IMPORTANT]
    > Come mostrato nella precedente schermata hello, lasciare hello **esito negativo in STDERR** casella di controllo deselezionata. Questa è un'impostazione importante, perché `docker-compose` stampa i messaggi di diagnostica diversi, ad esempio i contenitori sono arresto o eliminato, nell'output di errore standard hello. Se si seleziona la casella di controllo di hello, Visual Studio Team Services indica che si sono verificati errori durante il rilascio di hello, anche se tutto va bene.
    >
3. Salvare la nuova definizione di rilascio.


>[!NOTE]
>Questa distribuzione include i tempi di inattività Poiché stiamo l'arresto dei servizi precedente hello e in esecuzione hello uno nuovo. Si tratta tooavoid possibili effettuando una distribuzione verde-blu.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>Passaggio 4. Testare hello CI/CD pipeline

Dopo avere con configurazione hello, è ora tootest questa nuova pipeline CI/CD-ROM. tootest modo più semplice Hello è tooupdate hello origine codice e il commit hello modifiche nel repository GitHub. Pochi secondi dopo che si esegue il push codice hello, si noterà una nuova compilazione in esecuzione in Visual Studio Team Services. Una volta completata, una nuova versione verrà attivata e verrà distribuita hello nuova versione dell'applicazione hello in cluster del servizio di contenitore di Azure hello.

## <a name="next-steps"></a>Passaggi successivi

* Per ulteriori informazioni sull'elemento di configurazione/CD con Visual Studio Team Services, vedere hello [Panoramica di compilazione VSTS](https://www.visualstudio.com/docs/build/overview).
