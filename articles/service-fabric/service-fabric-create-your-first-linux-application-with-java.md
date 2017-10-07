---
title: un'applicazione Java di Azure Service Fabric attori affidabile in Linux aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate e distribuire un'applicazione di attori affidabile Java Service Fabric in cinque minuti.
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Creare la prima applicazione Java Reliable Actors di Service Fabric in Linux
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Questa guida introduttiva consente di creare in pochi minuti la prima applicazione Java di Azure Service Fabric in un ambiente di sviluppo Linux.  Al termine, sarà necessario una semplice applicazione di servizio singolo Java in esecuzione nel cluster di sviluppo locale hello.  

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, installare Service Fabric SDK hello, hello servizio infrastruttura CLI e del programma di installazione in un cluster di sviluppo del [ambiente di sviluppo di Linux](service-fabric-get-started-linux.md). Se si usa Mac OS X, è possibile [configurare un ambiente di sviluppo Linux in una macchina virtuale usando Vagrant](service-fabric-get-started-mac.md).

È anche possibile hello tooinstall [servizio infrastruttura CLI](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Installare e configurare i generatori di hello per Java
Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione Java di Service Fabric dal terminale tramite il generatore di modelli Yeoman. Eseguire procedure hello sotto tooensure che aver generatore di modello yeoman hello Service Fabric per Java utilizzo nel computer.
1. Installare nodejs e NPM nella macchina virtuale

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM

  ```bash
  sudo npm install -g yo
  ```
3. Installare generatore di applicazione di servizio Fabric Yeo Java hello da NPM

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Creare un'applicazione hello
Un'applicazione di Service Fabric contiene uno o più servizi, ognuno con un ruolo specifico nell'offerta di funzionalità dell'applicazione hello. Generatore di Hello è installato nell'ultima sezione hello, rende facile toocreate il primo servizio e tooadd più avanti.  È anche possibile creare, compilare e distribuire applicazioni Java di Service Fabric usando un plug-in per Eclipse. Vedere [Creare e distribuire la prima applicazione Java usando Eclipse](service-fabric-get-started-eclipse.md). Per questa Guida introduttiva usare Yeoman toocreate un'applicazione con un unico servizio che consente di archiviare e ottiene un valore del contatore.

1. In un terminale digitare ``yo azuresfjava``.
2. Assegnare un nome all'applicazione.
3. Scegliere il tipo di hello del primo servizio e il nome. Per questa esercitazione, scegliere un servizio Reliable Actor. Per ulteriori informazioni su hello altri tipi di servizi, vedere [Cenni preliminari sul modello di programmazione di Service Fabric](service-fabric-choose-framework.md).
   ![Generatore Yeoman di Service Fabric per Java][sf-yeoman]

## <a name="build-hello-application"></a>Compilare un'applicazione hello
modelli di servizio dell'infrastruttura Yeoman Hello includono uno script di compilazione per [Gradle](https://gradle.org/), che è possibile utilizzare un'applicazione hello toobuild da hello terminal.
Le dipendenze Java di Service Fabric vengono recuperate da Maven. toobuild e attività per le applicazioni Java di infrastruttura servizio hello, è necessario tooensure che si disponga di JDK e Gradle installato. Se non è ancora installato, è possibile eseguire hello seguito tooinstall JDK(openjdk-8-jdk) e Gradle -

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild e pacchetto applicazione hello, eseguire hello seguente:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Distribuire un'applicazione hello
Una volta creata l'applicazione hello, è possibile distribuire cluster locale toohello.

1. Connettere il cluster di Service Fabric locale toohello.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Eseguire script di installazione di hello fornito in hello modello toocopy applicazione hello pacchetto archivio immagini toohello del cluster, registrare il tipo di applicazione hello e creare un'istanza di un'applicazione hello.

    ```bash
    ./install.sh
    ```

Distribuire un'applicazione hello compilato è hello stesso come qualsiasi altra applicazione di Service Fabric. Vedere la documentazione di hello su [la gestione di un'applicazione di Service Fabric con hello servizio infrastruttura CLI](service-fabric-application-lifecycle-sfctl.md) per istruzioni dettagliate.

I parametri toothese comandi sono disponibili nei manifesti hello generato all'interno del pacchetto di applicazione hello.

Dopo la distribuzione di un'applicazione hello, aprire un browser e passare a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) in [http://localhost:19080/Esplora](http://localhost:19080/Explorer).
Espandere quindi hello **applicazioni** nodo e notare che è ora disponibile una voce per il tipo di applicazione e un altro per hello prima istanza di quel tipo.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Avviare il client di prova hello ed eseguire un failover
Gli attori non eseguire alcuna operazione in modo autonomo, richiedono un altro servizio o client di toosend tali messaggi. modello attore Hello include uno script di test semplice che è possibile utilizzare toointeract con servizio actor hello.

1. Eseguire script hello utilizzando hello espressioni di controllo utilità toosee hello output del servizio actor hello.  script di test hello chiama hello `setCountAsync()` metodo hello attore tooincrement un contatore, chiama hello `getCountAsync()` metodo hello attore tooget hello nuovo valore del contatore e consente di visualizzare tale valore toohello console.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. In Service Fabric Explorer, individuare hello nodo hosting hello replica primaria per il servizio actor hello. Nella schermata di hello riportata di seguito, è il nodo 3. Hello servizio primario replica gestisce operazioni lettura e scrittura.  Modifiche di stato del servizio vengono quindi replicate out toohello repliche secondarie, in esecuzione su 0 e 1 nella schermata di hello sotto i nodi.

    ![Trovare la replica primaria hello in Service Fabric Explorer][sfx-primary]

3. In **nodi**, fare clic sul nodo hello è stata individuata nel passaggio precedente hello, scegliere **Deactivate (riavvio)** dal menu Azioni hello. Questa azione riavvia il nodo hello esegue hello servizio primario replica e forza un tooone failover delle repliche secondarie di hello in esecuzione in un altro nodo.  Replica secondaria è tooprimary innalzate di livello, viene creata un'altra replica secondaria su un nodo diverso e la replica primaria hello inizia le operazioni di lettura/scrittura tootake. Come hello riavvii di nodo, espressioni di controllo di output di hello dalla hello client di prova e prendere nota di tale contatore hello continua tooincrement nonostante hello failover.

## <a name="remove-hello-application"></a>Rimuovere un'applicazione hello
Utilizzare script di disinstallazione hello fornito nell'istanza di applicazione hello toodelete modello hello, annullare la registrazione del pacchetto dell'applicazione hello e rimuovere il pacchetto di applicazione hello dall'archivio di immagini del cluster hello.

```bash
./uninstall.sh
```

In Esplora Service Fabric è visualizzato che un'applicazione hello e tipo di applicazione non è più in hello **applicazioni** nodo.

## <a name="service-fabric-java-libraries-on-maven"></a>Librerie Java di Service Fabric in Maven
Le librerie Java di Service Fabric sono ospitate in Maven. È possibile aggiungere le dipendenze di hello in hello ``pom.xml`` o ``build.gradle`` di raccolte di Service Fabric Java toouse di progetti da **mavenCentral**.

### <a name="actors"></a>Actor

Supporto di Service Fabric Reliable Actors per l'applicazione.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Services

Supporto di servizi senza stato di Service Fabric per l'applicazione.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Altro
#### <a name="transport"></a>Trasporto

Supporto del livello trasporto per l'applicazione Java di Service Fabric. Non è necessario tooexplicitly aggiungere questa dipendenza tooyour Reliable Actor o applicazioni di servizio, a meno che la programmazione a livello di trasporto hello.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Supporto di Fabric

Supporto di livello di sistema per l'infrastruttura del servizio, che comunica toonative runtime di Service Fabric. Non è necessario tooexplicitly aggiungere questa dipendenza tooyour Reliable Actor o applicazioni di servizio. Si ottiene recuperato automaticamente da Maven, quando si includono hello altre dipendenze precedente.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>La migrazione precedente toobe di applicazioni Java di infrastruttura del servizio utilizzato con Maven
È stato spostato nella librerie di Service Fabric Java recente dal repository tooMaven Service Fabric Java SDK. Mentre le nuove applicazioni hello generati usando Yeoman o Eclipse, genererà progetti aggiornati più recente (che saranno in grado di toowork con Maven), è possibile aggiornare l'infrastruttura esistente di servizio senza stato o applicazioni Java attore che usavano hello servizio Fabric SDK per Java in precedenza, le dipendenze di Service Fabric Java hello toouse Maven. Seguire i passaggi di hello indicati [qui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure precedente applicazione funziona con Maven.

## <a name="next-steps"></a>Passaggi successivi

* [Creare la prima applicazione Java di Service Fabric in Linux usando Eclipse](service-fabric-get-started-eclipse.md)
* [Altre informazioni su Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interagire con i cluster di Service Fabric usando hello servizio infrastruttura CLI](service-fabric-cli.md)
* Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)
* [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
