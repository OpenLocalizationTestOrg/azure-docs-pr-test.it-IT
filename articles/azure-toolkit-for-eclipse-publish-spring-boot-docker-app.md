---
title: un'app Spring avvio come un contenitore Docker utilizzando aaaPublish hello Azure Toolkit per Eclipse | Documenti Microsoft
description: Informazioni su come toopublish un tooMicrosoft app web Azure come un contenitore Docker usando hello Azure Toolkit per Eclipse.
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
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Pubblicare un'app Spring avvio come un contenitore Docker usando hello Azure Toolkit per Eclipse

Hello [Spring Framework] è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale. Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonomo.

[Docker] è una soluzione open source che consente agli sviluppatori di automatizzare la distribuzione di hello, scalabilità e gestione delle applicazioni in esecuzione nei contenitori.

In questa esercitazione illustra hello passaggi toodeploy un'applicazione di avvio molla come un tooMicrosoft contenitore Docker Azure tramite hello Azure Toolkit per Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Clonare il repository di Docker avvio Spring hello predefinito

### <a name="import-hello-public-repository"></a>Archivio pubblico hello di importazione

Hello passaggi seguenti consentono di eseguire la clonazione di computer locale tooyour hello Spring avvio Docker repository utilizzando IntelliJ. Se si desidera toouse una riga di comando, vedere [distribuire un'applicazione di avvio molla su Linux nel servizio contenitore di Azure][Deploy Spring Boot on Linux in ACS].

1. Aprire Eclipse.

1. Fare clic su **File** > **Import** (Importa).

   ![Opzione Import (Importa) del menu File][CL01]

1. Quando hello **importazione** verrà visualizzata la finestra di dialogo:

   a. Espandere **Git**.

   b. Selezionare **Projects from Git** (Progetti da Git).
   
   c. Fare clic su **Avanti**.

   ![Finestra di dialogo Import (Importa)][CL02]

1. In hello **selezionare l'origine del Repository** pagina:

   a. Selezionare **Clone URI** (Clona URI).
   
   b. Fare clic su **Avanti**.

   ![Selezionare la pagina origine del repository][CL03]

1. In hello **Git Repository di origine** pagina:

   a. Per **URI**, immettere `https://github.com/spring-guides/gs-spring-boot-docker.git`. Questo passaggio deve popolare automaticamente hello **Host** e **il percorso del Repository** i campi con hello correggere i valori.
   
   b. repository di avvio Spring Hello è pubblica, pertanto non è necessario tooenter nome Git utente e password.
   
   c. Fare clic su **Avanti**.

   ![Pagina del repository Git di origine][CL04]

1. In hello **selezione ramo** pagina, fare clic su **Avanti**.

   ![Pagina Branch Selection (Selezione ramo)][CL05]

1. In hello **destinazione locale** pagina:

   a. Specificare hello cartella locale in cui si desidera il repository locale.
   
   b. Fare clic su **Avanti**.

   ![Pagina Local Destination (Destinazione locale)][CL06]

1. In hello **toouse una procedura guidata per l'importazione di progetti selezionare** pagina:

   a. Selezionare **Import as a general project** (Importa come progetto generale).
   
   b. Fare clic su **Avanti**.

   !["Seleziona toouse una procedura guidata per l'importazione di progetti"][CL07]

1. In hello **importazione progetti** pagina:

   a. Specificare il nome del progetto.
   
   b. Fare clic su **Finish**.

   ![Pagina Import Projects (Importa progetti)][CL08]

1. Quando è clonare il repository di hello, vengono visualizzati tutti i file hello elencati in Eclipse.

   ![Repository locale][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Creare un progetto Maven dal repository locale

repository di Docker avvio Spring Hello contiene un progetto di Maven completato, che verrà utilizzato per questa esercitazione. 

1. Fare clic su **File** > **Import** (Importa).

   ![Importare i comandi nel menu File hello][CL01]

1. Quando hello **importazione** verrà visualizzata la finestra di dialogo:

   a. Espandere **Maven**.
   
   b. Selezionare **Existing Maven Projects** (Progetti Maven esistenti).
   
   c. Fare clic su **Avanti**.

   ![Finestra di dialogo Import (Importa)][MV01]

1. In hello **progetti Maven** pagina:

   a. Per **Directory radice**, specificare hello **completo** cartella nel repository locale.
   
   b. Espandere hello **avanzate** sezione e immettere un nome personalizzato per **modello nome**.
   
   c. Casella di selezione hello hello **pom.xml** file nel progetto hello.
   
   d. Fare clic su **Finish**.

   ![Pagina Maven Projects (Progetti Maven)][MV02]

1. Quando il progetto di Maven hello viene aperto correttamente, viene visualizzato un secondo progetto elencato in Eclipse.

   ![Progetto Maven locale][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Compilazione dell'app Spring Boot mediante Maven

1. In Project Explorer di Eclipse hello, selezionare il progetto di Maven hello.

1. Fare clic su **Run** > **Run As** > **Maven build** (Esegui > Esegui come > Compilazione Maven)

   ![Comandi toorun come compilazione Maven][BU01]

1. Quando l'applicazione viene compilata correttamente, finestra di console hello Mostra stato hello.

   ![Completamento della compilazione Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Pubblicare il tooAzure app web con un contenitore Docker

1. In Project Explorer di Eclipse hello, selezionare il progetto di Maven hello.

1. Fare clic su hello Azure **pubblica** menu e quindi fare clic su **pubblica come contenitore Docker**.

   ![Comando Publish as Docker Container (Pubblica come contenitore Docker)][PU01]

1. Quando hello **distribuzione contenitore Docker in Azure** viene visualizzata la finestra di dialogo:

   a. Immettere il nome di un'immagine Docker personalizzata.
   
   b. Per **artefatto toodeploy**, specificare hello percorso toohello **gs-spring-avvio-docker-0.1.0.jar** file appena compilato.

   ![Specificare le opzioni per Docker][PU02]

   Verranno visualizzati tutti gli host Docker esistenti. 

1. Se si sceglie toodeploy tooan esistente host, è possibile ignorare toostep 5. In caso contrario, utilizzare hello seguendo i passaggi toocreate un host:

   a. Fare clic su **Aggiungi**.

      ![Aggiungere un nuovo host Docker][PU03]

   b. Quando hello **creare Host Docker** viene visualizzata la finestra di dialogo, è possibile scegliere le impostazioni predefinite hello tooaccept o è possibile specificare le impostazioni personalizzate per il nuovo host Docker. (Per una descrizione dettagliata di hello diverse impostazioni, vedere [pubblicare un'app web come un contenitore Docker usando hello Azure Toolkit per IntelliJ][Publish Container with Azure Toolkit].) Fare clic su **Avanti** una volta specificate le impostazioni toouse.

      ![Specificare le opzioni per l'host Docker][PU04]

   c. È possibile scegliere le credenziali di accesso esistente toouse da un insieme di credenziali chiave di Azure, oppure è possibile scegliere tooenter nuove credenziali di accesso di Docker. Dopo aver specificato le opzioni, fare clic su **Finish** (Fine).

      ![Specificare le credenziali per l'host Docker][PU05]

1. Selezionare l'host Docker e quindi fare clic su **Next** (Avanti).

   ![Selezionare toouse host Docker][PU06]

1. Hello ultima pagina di hello **distribuzione contenitore Docker in Azure** finestra di dialogo specificare hello le opzioni seguenti:

   a. È possibile scegliere un nome personalizzato per il contenitore hello che ospiterà il contenitore Docker toospecify oppure è possibile accettare l'impostazione predefinita di hello.

   b. Immettere le porte TCP hello per l'host docker usando hello la seguente sintassi: *[porta esterna]*:*[porta interna]*. Ad esempio, **80:8080** specifica una porta esterna dell'80 e la porta interna Spring avvio hello predefinita del 8080.
   
      Se è stato personalizzato la porta interna (ad esempio, modificando il file di application.yml hello), è necessario il numero di porta hello toospecify per hello toooccur routing corretto in Azure.

   c. Dopo aver configurato queste opzioni, fare clic su **Finish** (Fine).

   ![Distribuire un contenitore Docker in Azure][PU07]

1. Al termine hello Azure Toolkit pubblicazione, hello Visualizza Log attività Azure **pubblicato** per lo stato di hello.

   ![Distribuzione dell'host Docker completata][PU08]

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[avvio Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
