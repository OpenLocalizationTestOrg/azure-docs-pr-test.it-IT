---
title: aaaAzure Service Fabric plug-in per Eclipse | Documenti Microsoft
description: Introduzione a hello Service Fabric plug-in per Eclipse.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Plug-in Service Fabric per lo sviluppo di applicazioni Java in Eclipse
Eclipse è uno dei più diffuse hello integrato (IDE) di ambienti di sviluppo per gli sviluppatori Java. In questo articolo viene descritto come tooset backup il toowork ambiente di sviluppo Eclipse con Azure Service Fabric. Scopri hello tooinstall Service Fabric plug-in, creare un'applicazione di Service Fabric e distribuire il Service Fabric applicazione tooa locale o remoto dell'infrastruttura del servizio cluster in Eclipse Neon.

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>Installare o aggiornare hello plug-in Eclipse Neon di Service Fabric
È possibile installare un plug-in Service Fabric in Eclipse. Hello plug-in consente di semplificare il processo di hello della compilazione e distribuzione di servizi di linguaggio.

1.  Verificare di disporre di più recente di Eclipse Neon hello e hello versione Buildship (1.0.17 o una versione successiva) installato:
    -   versioni di hello toocheck dei componenti installati, in Eclipse Neon, andare troppo**Guida** > **i dettagli di installazione**.
    -   vedere tooupdate Buildship, [Buildship Eclipse: Plug-in Eclipse per Gradle][buildship-update].
    -   toocheck per e installa gli aggiornamenti per Neon Eclipse, andare troppo**Guida** > **Controlla aggiornamenti**.

2.  hello tooinstall Service Fabric plug-in, in Eclipse Neon, andare troppo**Guida** > **installa nuovo Software**.
  1.    In hello **utilizzano** immettere **http://dl.microsoft.com/eclipse**.
  2.    Fare clic su **Aggiungi**.

         ![Plug-in Service Fabric per Eclipse Neon][sf-eclipse-plugin-install]
  3.    Selezionare i plug-in Service Fabric hello e quindi fare clic su **Avanti**.
  4.    Completare i passaggi di installazione hello e quindi accettare condizioni di licenza Software Microsoft hello.

Se si dispone già di hello Service Fabric di plug-in installato, accertarsi di avere la versione più recente di hello. toocheck per gli aggiornamenti disponibili, andare troppo**Guida** > **i dettagli di installazione**. Nell'elenco di hello del plug-in installati, selezionare Service Fabric e quindi fare clic su **aggiornamento**. Verranno installati gli aggiornamenti disponibili.

> [!NOTE]
> Se l'installazione o aggiornamento hello plug-in Service Fabric è lenta, potrebbe essere dovuto impostazione Eclipse tooan. Eclipse raccoglie i metadati in tutti i siti tooupdate modifiche che sono registrati con l'istanza di Eclipse. toospeed backup processo hello di rilevamento e installazione di un aggiornamento di Service Fabric plug-in, andare troppo**siti Software disponibili**. Deselezionare le caselle di controllo hello per tutti i siti, ad eccezione di hello quello che punta toohello percorso plug-in Service Fabric (http://dl.microsoft.com/eclipse/azure/servicefabric).

## <a name="create-a-service-fabric-application-in-eclipse"></a>Creare un'applicazione di Service Fabric in Eclipse

1.  In Eclipse Neon, andare troppo**File** > **New** > **altri**. Selezionare **Service Fabric Project**, quindi fare clic su **Next** (Avanti).

    ![Pagina 1 del nuovo progetto di Service Fabric][create-application/p1]

2.  Immettere un nome per il progetto e quindi fare clic su **Next** (Avanti).

    ![Pagina 2 del nuovo progetto di Service Fabric][create-application/p2]

3.  Nell'elenco dei modelli di hello selezionare **modello di servizio**. Selezionare il tipo di modello di servizio (Actor, Stateless, Container, or Guest Binary) e quindi fare clic su **Next** (Avanti).

    ![Pagina 3 del nuovo progetto di Service Fabric][create-application/p3]

4.  Immettere il nome di servizio hello e dettagli del servizio e quindi fare clic su **fine**.

    ![Pagina 4 del nuovo progetto di Service Fabric][create-application/p4]

5. Quando si crea il primo progetto, Service Fabric in hello **Open Perspective associata** la finestra di dialogo, fare clic su **Sì**.

    ![Pagina 5 del nuovo progetto di Service Fabric][create-application/p5]

6.  L'aspetto del nuovo progetto sarà simile al seguente:

    ![Pagina 6 del nuovo progetto di Service Fabric][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Creare e distribuire un'applicazione di Service Fabric in Eclipse

1.  Fare clic con il pulsante destro del mouse sulla nuova applicazione di Service Fabric, quindi scegliere **Service Fabric**.

    ![Menu di scelta rapida di Service Fabric][publish/RightClick]

2. Nel sottomenu hello, selezionare l'opzione hello desiderata:
    -   Fare clic su un'applicazione hello toobuild senza la pulizia, **applicazione compilazione**.
    -   Fare clic su una compilazione pulita dell'applicazione hello, toodo **ricompilare applicazione**.
    -   Fare clic su un'applicazione hello tooclean di artefatti compilati, **applicazione pulita**.

3.  Da questo menu è anche possibile distribuire, annullare la distribuzione e pubblicare l'applicazione:
    -   cluster locale tooyour toodeploy, fare clic su **distribuire applicazione**.
    -   In hello **pubblica l'applicazione** finestra di dialogo, selezionare un profilo di pubblicazione:
        -  **Local.json**
        -  **Cloud.json**

     Questi file JavaScript Object Notation (JSON) le informazioni (ad esempio endpoint della connessione e informazioni di sicurezza) che sono necessario tooconnect tooyour locale o cloud (Azure).

  ![Menu di pubblicazione di Service Fabric][publish/Publish]

Un modo alternativo di toodeploy l'applicazione di Service Fabric è usando Eclipse configurazioni di esecuzione.

  1.    Andare troppo**eseguire** > **eseguire configurazioni**.
  2.    In **Gradle progetto**selezionare hello **ServiceFabricDeployer** configurazione di esecuzione.
  3.    Nel riquadro di destra hello, su hello **argomenti** scheda per **publishProfile**selezionare **locale** o **cloud**.  valore predefinito di Hello è **locale**. tooa toodeploy remoto o un cloud di cluster **cloud**.
  4.    che informazioni corrette hello viene popolate in hello tooensure profili di pubblicazione, modificare **Local.json** o **Cloud.json** in base alle esigenze. È possibile aggiungere o aggiornare i dettagli degli endpoint e delle credenziali di sicurezza.
  5.    Verificare che **la Directory di lavoro** punta applicazione toohello da toodeploy. toochange hello applicazione, fare clic su hello **dell'area di lavoro** e quindi selezionare un'applicazione hello desiderato.
  6.    Fare clic su **Apply** (Applica) e quindi su **Run** (Esegui).

L'applicazione verrà compilata e distribuita dopo alcuni istanti. È possibile monitorare lo stato di distribuzione hello in Service Fabric Explorer.  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>Aggiungere un tooyour di servizio dell'applicazione di Service Fabric di Service Fabric

un'infrastruttura a servizio tooan esistente Service Fabric applicazione di servizio, tooadd hello i passaggi seguenti:

1.  Progetto di hello pulsante destro del mouse si desidera che un servizio tooadd e quindi fare clic su **Service Fabric**.

    ![Pagina 1 dell'aggiunta di un servizio di Service Fabric][add-service/p1]

2.  Fare clic su **Aggiungi servizio Service Fabric**, e hello completo di set di passaggi tooadd un progetto di servizio toohello.
3.  Modello di servizio selezionare hello desidera tooadd tooyour progetto e quindi fare clic su **Avanti**.

    ![Pagina 2 dell'aggiunta di un servizio di Service Fabric][add-service/p2]

4.  Immettere il nome di servizio hello (e altri dettagli, in base alle esigenze) e quindi fare clic su hello **Aggiungi servizio** pulsante.  

    ![Pagina 3 dell'aggiunta di un servizio di Service Fabric][add-service/p3]

5.  Dopo aver aggiunto il servizio di hello, la struttura del progetto complessivo è simile toohello progetto seguente:

    ![Pagina 4 dell'aggiunta di un servizio di Service Fabric][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>Modifica versioni del manifesto dell'applicazione Java di Service Fabric

versioni di manifesto tooedit, fare clic con il pulsante destro sul progetto hello, andare troppo**Service Fabric** e selezionare **modifica manifesto versioni...**  da hello menu a discesa. Nella procedura guidata hello, è possibile aggiornare le versioni di manifesto hello manifesto dell'applicazione, manifesto del servizio e hello per **codice**, **Config** e **dati** pacchetti.

Se si seleziona l'opzione hello **aggiornare automaticamente versioni dell'applicazione e servizio** e quindi di aggiornare una versione, le versioni di manifesto hello quindi verranno aggiornate automaticamente. toogive un esempio, innanzitutto selezionare hello casella di controllo, quindi hello aggiornamento versione **codice** versione da visualizzata sarà 0.0.0 too0.0.1 e fare clic su **fine**, quindi service versione del manifesto e manifesto dell'applicazione versione sarà too0.0.1 aggiornate automaticamente.

## <a name="upgrade-your-service-fabric-java-application"></a>Aggiornare l'applicazione Java di Service Fabric

Per uno scenario di aggiornamento, ad esempio creato hello **App1** progetto tramite hello Service Fabric plug-in Eclipse. È distribuito usando hello toocreate di plug-in un'applicazione denominata **fabric: / App1Application**. tipo di applicazione Hello è **App1AppicationType**, e versione dell'applicazione hello è 1.0. A questo punto, si desidera tooupgrade dell'applicazione senza interrompere la disponibilità.

In primo luogo, apportare le modifiche dell'applicazione tooyour e quindi ricompilare il servizio di hello modificato. Hello aggiornamento modifica il file manifesto del servizio (ServiceManifest.xml) con versioni aggiornata di hello per servizio hello (e codice, configurazione o dati, se pertinente). Inoltre, modificare il manifesto dell'applicazione hello (ApplicationManifest.xml) con numero di versione di hello aggiornato per un'applicazione hello e hello servizio modificato.  

tooupgrade l'applicazione mediante Neon Eclipse, è possibile creare un profilo di configurazione di esecuzione duplicati. Utilizzare quindi tooupgrade l'applicazione in base alle esigenze.

1.  Andare troppo**eseguire** > **eseguire configurazioni**. Nel riquadro di sinistra hello, fare clic su hello piccola freccia toohello sinistro **Gradle progetto**.
2.  Fare clic con il pulsante destro del mouse su **ServiceFabricDeployer** e quindi scegliere **Duplicate** (Duplica). Specificare un nuovo nome per questa configurazione, ad esempio **ServiceFabricUpgrader**.
3.  Nel riquadro di destra hello, su hello **argomenti** modificare **- ipconfig = 'Distribuisci'** troppo**- ipconfig = 'Aggiorna'**, quindi fare clic su **applica**.

Questo processo crea e salva un profilo di configurazione di esecuzione è possibile utilizzare qualsiasi tooupgrade ora l'applicazione. Ottiene anche hello applicazione aggiornata tipo più recente dal file manifesto dell'applicazione hello.

aggiornamento dell'applicazione Hello richiede alcuni minuti. È possibile monitorare l'aggiornamento dell'applicazione hello in Service Fabric Explorer.

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>La migrazione precedente toobe di applicazioni Java di infrastruttura del servizio utilizzato con Maven
È stato spostato nella librerie di Service Fabric Java recente dal repository tooMaven Service Fabric Java SDK. Mentre le nuove applicazioni hello generati usando Eclipse, genererà progetti aggiornati più recente (che saranno in grado di toowork con Maven), è possibile aggiornare l'infrastruttura esistente di servizio senza stato o applicazioni Java attore che usavano hello Service Fabric SDK per Java versioni precedenti, toouse hello Service Fabric Java dipendenze Maven. Seguire i passaggi di hello indicati [qui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure precedente applicazione funziona con Maven.

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
