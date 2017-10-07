---
title: un'app Spring avvio come un contenitore Docker utilizzando aaaPublish hello Azure Toolkit per IntelliJ | Documenti Microsoft
description: Informazioni su come toopublish un tooMicrosoft app web Azure come un contenitore Docker usando hello Azure Toolkit per IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Pubblicare un'app Spring avvio come un contenitore Docker usando hello Azure Toolkit per IntelliJ

Hello [Spring Framework] è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale. Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonomo.

[Docker] è una soluzione open source che consente agli sviluppatori di automatizzare la distribuzione di hello, scalabilità e gestione delle applicazioni in esecuzione nei contenitori.

In questa esercitazione illustra hello passaggi toodeploy un'applicazione di avvio molla come un tooMicrosoft contenitore Docker Azure tramite hello Azure Toolkit per IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a>Clonare hello predefinito Spring avvio Docker repository

Hello passaggi seguenti consentono di eseguire la clonazione di repository di Docker avvio Spring hello utilizzando IntelliJ. Se si desidera toouse una riga di comando, vedere [distribuire un'applicazione di avvio molla su Linux nel servizio contenitore di Azure][Deploy Spring Boot on Linux in ACS].

1. Aprire IntelliJ.

1. Nella schermata iniziale hello selezionare hello **GitHub** opzione hello **estrarre dal controllo della versione** elenco.

   ![Opzione GitHub per il controllo della versione][CL01]

1. Immettere le credenziali in caso di richiesta toolog in.

   * Se si utilizza un nome utente e password toolog in tooGitHub:

      ![Finestra di dialogo per l'immissione del nome utente e password GitHub][CL02a]

   * Se si utilizza un token toolog in tooGitHub:

      ![Finestra di dialogo per l'immissione di un token GitHub][CL02b]

1. Immettere **https://github.com/spring-guides/gs-spring-boot-docker.git** per l'URL del repository hello, specificare il percorso locale e informazioni sulla cartella e quindi fare clic su **Clone**.

   ![Finestra di dialogo per la clonazione del repository][CL03]

1. Quando viene richiesto un progetto IntelliJ toocreate **n**.

   ![Rifiuto di un progetto IntelliJ toocreate][CL04]

1. Nella pagina di benvenuto hello, fare clic su **importazione progetto**.

   ![Selezione del progetto da importare][CL05]

1. Individuare il percorso di hello in cui è stato clonato il repository di avvio Spring hello, selezionare hello **completo** cartella radice hello e quindi fare clic su **OK**.

   ![Selezionare una cartella per l'importazione][CL06]

1. Quando richiesto, scegliere **Create project from existing sources** (Crea progetto da origini esistenti).

   ![Opzione toocreate un progetto da origini esistenti][CL07]

1. Specificare il nome del progetto o accettare l'impostazione predefinita di hello, verificare hello percorso corretto toohello **completo** cartella e quindi fare clic su **Avanti**.

   ![Specificare il nome di progetto hello][CL08]

1. Personalizzare le directory per l'importazione e quindi fare clic su **Next** (Avanti).

   ![Scegliere le directory][CL09]

1. Esaminare tooimport librerie hello e quindi fare clic su **Avanti**.

   ![Esaminare le librerie del progetto][CL10]

1. Struttura del modulo hello di esaminare e quindi fare clic su **Avanti**.

   ![Esaminare la struttura del modulo][CL11]

1. Specificare il JDK e quindi fare clic su **Next** (Avanti).

   ![Specificare un JDK][CL12]

1. Fare clic su **Finish**.

   ![Pulsante Fine][CL13]

IntelliJ Importa hello Spring avvio app come un progetto e Visualizza struttura hello quando terminata l'importazione di hello.

![App Spring Boot in IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Compilare l'app Spring Boot

### <a name="build-hello-app-by-using-hello-maven-pom"></a>Compilare l'applicazione hello utilizzando hello POM di Maven

1. Se non è già aperto, aprire finestra degli strumenti di Maven hello. Fare clic su **Visualizza** > **Finestre degli strumenti** > **Maven Projects** (Progetti Maven).

   ![Comandi Finestre degli strumenti e Maven Projects (Progetti Maven)][BU01]

1. Nella finestra strumento di Maven hello, fare doppio clic su **pacchetto** e selezionare **Esegui compilazione Maven**. (Se il progetto di Maven non vengono visualizzate automaticamente, fare clic su hello **reimportare** icona sulla barra degli strumenti Maven hello.)

   ![Comando Run Maven Build (Esegui compilazione Maven)][BU02]

1. Una volta creata correttamente l'app Spring Boot, IntelliJ visualizzerà un messaggio **BUILD SUCCESS** (COMPILAZIONE COMPLETATA).

   ![Messaggio BUILD SUCCESS (COMPILAZIONE COMPLETATA)][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Creare un elemento pronto per la distribuzione

toopublish app Spring avvio, è necessario toocreate un elemento pronto per la distribuzione. Utilizzare hello alla procedura seguente:

1. Aprire il progetto dell'app Web in IntelliJ.

1. Fare clic su **File** e quindi fare clic su **Project Structure** (Struttura del progetto).

   ![Comando Project Structure (Struttura del progetto)][ART01]

1. Fare clic su hello verde plus (**+**) di simboli tooadd un elemento, fare clic su **JAR**e quindi fare clic su **vuoto**.

   ![Aggiungere un elemento][ART02]

1. Denominare l'elemento assicurandosi che non tooadd hello "JAR" estensione e quindi specificare la cartella di destinazione hello per hello Maven output.

   ![Specificare le proprietà dell'elemento][ART03]

1. Creare un manifesto per l'elemento (facoltativo):

   a. Fare clic su **Create Manifest** (Crea manifesto).

      ![Fare clic sul pulsante Crea manifesto hello][ART04a]

   b. Scegliere il percorso predefinito hello per artefatto hello e quindi fare clic su **OK**.

      ![Specificare il percorso dell'elemento][ART04b]

   c. Fare clic sui puntini di sospensione hello (**... **) toolocate classe principale di hello.

      ![Individuare la classe principale][ART04c]

   d. Scegliere la classe principale e quindi fare clic su **OK**.

      ![Specificare la classe principale][ART04d]

1. Fare clic su **OK**.

   ![Chiudere la finestra di dialogo di hello struttura del progetto][ART05]

> [!NOTE]
> Per ulteriori informazioni sulla creazione di elementi in IntelliJ, vedere [gli elementi di configurazione] nel sito Web JetBrains hello.
>

### <a name="build-hello-artifact-for-deployment"></a>Hello artefatto per la distribuzione di compilazione

1. Fare clic su **Build** (Compila) e quindi su **Artifacts** (Elementi).

   ![Comando Build Artifacts (Compila elementi)][BU04]

1. Quando hello **artefatto di compilazione** menu di scelta rapida viene visualizzato, fare clic su **compilare**.

   ![Menu di scelta rapida Build Artifact (Compila elemento)][BU05]

IntelliJ deve essere visualizzato artefatto hello completato per l'app avvio Spring nella finestra strumento di hello progetto.

   ![Elemento creato][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Pubblicare il tooAzure app web con un contenitore Docker

1. Se non è stato firmato in tooyour account Azure, seguire hello [accesso le istruzioni per hello Azure Toolkit per IntelliJ][Azure Sign In for IntelliJ].

1. Nella finestra degli strumenti di Esplora progetti hello, fare clic sul progetto hello e quindi selezionare **Azure** > **pubblica come contenitore Docker**.

   ![Comando Publish as Docker Container (Pubblica come contenitore Docker)][PU01]

1. Quando hello **distribuire contenitore Docker in Azure** viene visualizzata la finestra di dialogo, vengono visualizzati gli host Docker esistenti. Se si sceglie toodeploy tooan esistente host, è possibile ignorare toostep 4. In caso contrario, utilizzare hello seguendo i passaggi toocreate un host:

   a. Fare clic su hello verde plus (**+**) simbolo.

      ![Aggiungere un nuovo host Docker][PU02]

   b. Quando hello **creare Host Docker** viene visualizzata la finestra di dialogo, è possibile scegliere le impostazioni predefinite hello tooaccept o è possibile specificare le impostazioni personalizzate per il nuovo host Docker. (Per una descrizione dettagliata di hello diverse impostazioni, vedere [pubblicare un'app web come un contenitore Docker usando hello Azure Toolkit per IntelliJ][Publish Container with Azure Toolkit].) Fare clic su **Avanti** una volta specificate le impostazioni toouse.

      ![Specificare le opzioni per l'host Docker][PU03a]

   c. È possibile scegliere le credenziali di accesso esistente toouse da un insieme di credenziali chiave di Azure, oppure è possibile scegliere tooenter nuove credenziali di accesso di Docker. Dopo aver specificato le opzioni, fare clic su **Finish** (Fine).

      ![Specificare le credenziali per l'host Docker][PU03b]

1. Selezionare l'host Docker e quindi fare clic su **Next** (Avanti).

   ![Selezionare hello Docker host toouse][PU04]

1. Hello ultima pagina di hello **distribuire contenitore Docker in Azure** finestra di dialogo specificare hello le opzioni seguenti:

   a. È possibile scegliere un nome personalizzato per il contenitore hello che ospiterà il contenitore Docker toospecify oppure è possibile accettare l'impostazione predefinita di hello.

   b. Immettere le porte TCP hello per l'host docker usando hello la seguente sintassi: *[porta esterna]*:*[porta interna]*. Ad esempio, **80:8080** specifica una porta esterna dell'80 e la porta interna Spring avvio hello predefinita del 8080.
   
      Se è stato personalizzato la porta interna (ad esempio, modificando il file di application.yml hello), è necessario il numero di porta hello toospecify per hello toooccur routing corretto in Azure.

   c. Dopo aver configurato queste opzioni, fare clic su **Finish** (Fine).

   ![Distribuire un contenitore Docker in Azure][PU05]

1. Al termine hello Azure Toolkit pubblicazione, hello Visualizza Log attività Azure **pubblicato** per lo stato di hello.

   ![Distribuzione dell'host Docker completata][PU06]

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

vedere toolearn sui metodi aggiuntivi per la creazione di applicazioni di avvio Spring utilizzando IntelliJ, [creazione di progetti di avvio Spring](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) nel sito Web JetBrains hello.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configurazione di elementi)
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
