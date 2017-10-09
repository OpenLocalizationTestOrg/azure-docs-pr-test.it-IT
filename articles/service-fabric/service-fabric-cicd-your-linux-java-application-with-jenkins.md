---
title: aaaContinuous build e integrazione dell'applicazione Azure Service Fabric Linux Java utilizzando Jenkins | Documenti Microsoft
description: Compilazione continua e integrazione per un'applicazione Java Linux tramite Jenkins
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Utilizzare toobuild Jenkins e distribuire l'applicazione Java di Linux
Jenkins è uno strumento diffuso per l'integrazione e la distribuzione continue delle app. Ecco come toobuild e distribuire l'applicazione Azure Service Fabric con Jenkins.

## <a name="general-prerequisites"></a>Prerequisiti generali
- È necessario che Git sia installato in locale. È possibile installare una versione Git appropriata hello da [pagina di download hello Git](https://git-scm.com/downloads), in base al sistema operativo. Nel caso di nuova tooGit, altre informazioni, da hello [Git documentazione](https://git-scm.com/docs).
- Hello plug-in Service Fabric Jenkins sono utili. È possibile scaricarlo dalla pagina di [download di Service Fabric](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Configurare Jenkins all'interno di un cluster di Service Fabric

È possibile configurare Jenkins all'interno o all'esterno di un cluster di Service Fabric. esempio Hello sezioni Mostra come tooset, configurarlo all'interno di un cluster durante l'utilizzo di una risorsa di archiviazione Azure account stato hello toosave dell'istanza di contenitore hello.

### <a name="prerequisites"></a>Prerequisiti
1. Un cluster Linux Service Fabric pronto. Un cluster di Service Fabric già creato dal portale di Azure hello con Docker installato. Se si eseguono cluster hello in locale, verificare che sia installato tramite il comando hello Docker ``docker info``. Se non è installato, installarlo utilizzando conseguenza hello seguenti comandi:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Dispone di un'applicazione contenitore hello Service Fabric distribuita in cluster hello, mediante hello alla procedura seguente:

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. È necessario hello connettersi dettagli sulle opzioni di hello condivisione-file di archiviazione di Azure, in cui si desidera che toopersist hello stato dell'istanza di hello Jenkins contenitore. Se si utilizza il portale di Microsoft Azure hello per hello stesso, per seguire i passaggi di hello - creare un account di archiviazione di Azure, ad esempio ``sfjenkinsstorage1``. Creare una **condivisione file** con tale account di archiviazione, ad esempio ``sfjenkins``. Fare clic su **Connetti** per hello condivisione file e prendere nota di hello di valori, viene visualizzato in **connessione da Linux**, ad esempio questo avrà un aspetto analogo, come segue:
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Aggiornare i valori segnaposto hello hello ```setupentrypoint.sh``` script con i dettagli di archiviazione di azure corrispondenti.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
Sostituire ``[REMOTE_FILE_SHARE_LOCATION]`` con valore hello ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` dall'output di hello di hello connettersi al punto 3 sopra.
Sostituire ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` con valore hello ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` dal punto 3 descritto sopra.

5. Connettere il cluster toohello e installare un'applicazione contenitore hello.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
Questo consente di installare un contenitore di Jenkins nel cluster hello e può essere monitorato tramite hello Service Fabric Explorer.

### <a name="steps"></a>Passi
1. Dal browser, passare troppo``http://PublicIPorFQDN:8081``. Fornisce il percorso di hello di hello iniziale di amministrazione di password toosign in. È possibile continuare toouse Jenkins come un utente amministratore. Oppure è possibile creare e modificare utente hello, dopo l'accesso con account admin iniziale hello.

   > [!NOTE]
   > Verificare che la porta 8081 hello è specificata come porta dell'endpoint applicazione hello durante la creazione di cluster hello.
   >

2. Ottenere l'ID dell'istanza di hello contenitore usando ``docker ps -a``.
3. Secure Shell (SSH) Accedi toohello contenitore e incollare il percorso di hello che è stato visualizzato nel portale di Jenkins hello. Ad esempio, se nel portale di hello è indicato il percorso di hello `PATH_TO_INITIAL_ADMIN_PASSWORD`, eseguire hello seguente:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Impostare toowork GitHub con Jenkins, usando i passaggi di hello indicati in [generare una nuova chiave SSH e l'aggiunta dell'agente SSH toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * Utilizzare le istruzioni di hello fornite dalla chiave SSH hello toogenerate di GitHub e tooadd hello SSH chiave toohello account GitHub che ospita il repository.
    * Eseguire i comandi di hello citati in hello precedente collegamento hello shell Jenkins Docker (e non nell'host).
    * toosign in toohello shell Jenkins dall'host, utilizzare hello comando seguente:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Configurare Jenkins all'esterno di un cluster di Service Fabric

È possibile configurare Jenkins all'interno o all'esterno di un cluster di Service Fabric. Hello seguente mostra sezioni come tooset, configurarlo all'esterno di un cluster.

### <a name="prerequisites"></a>Prerequisiti
È necessario toohave Docker installato. Hello i comandi seguenti può essere utilizzati tooinstall Docker da hello terminal:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Quando si esegue ``docker info`` nella hello terminal, verrà visualizzato nell'output di hello che hello Docker servizio è in esecuzione.

### <a name="steps"></a>Passi
  1. Immagine di contenitore hello Jenkins dell'infrastruttura del servizio di pull:``docker pull raunakpandya/jenkins:v1``
  2. Eseguire l'immagine contenitore hello:``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Ottenere l'ID di hello dell'istanza di immagine contenitore hello. È possibile elencare tutti i contenitori di Docker hello con il comando hello``docker ps –a``
  4. Accedi toohello Jenkins portale tramite hello alla procedura seguente:

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Se l'ID contenitore è 2d24a73b5964, usare 2d24.
    * Questa password è obbligatoria per la firma nel dashboard di Jenkins toohello dal portale, ovvero``http://<HOST-IP>:8080``
    * Dopo l'accesso per hello prima volta, è possibile creare il proprio account utente e utilizzarlo per scopi futuri oppure è possibile continuare l'account di amministratore toouse hello. Dopo aver creato un utente, è necessario toocontinue con quello.
  5. Impostare toowork GitHub con Jenkins, usando i passaggi di hello indicati in [generare una nuova chiave SSH e l'aggiunta dell'agente SSH toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * Utilizzare istruzioni hello fornite dalla chiave SSH hello toogenerate di GitHub e tooadd hello SSH chiave toohello account GitHub che ospita il repository di hello.
        * Eseguire i comandi di hello citati in hello precedente collegamento hello shell Jenkins Docker (e non nell'host).
      * toosign in toohello shell Jenkins dall'host, hello di utilizzare i comandi seguenti:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Verificare che tale cluster hello o un computer in cui è ospitato l'immagine contenitore Jenkins hello ha un indirizzo IP pubblico. In questo modo hello Jenkins istanza tooreceive notifiche di GitHub.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>Installazione di plug-in Service Fabric Jenkins hello dal portale di hello

1. Andare troppo``http://PublicIPorFQDN:8081``
2. Dal dashboard Jenkins hello selezionare **gestire Jenkins** > **gestire plug-in** > **avanzate**.
In questa schermata è possibile caricare un plug-in. Selezionare **Choose file**, quindi selezionare hello **serviceFabric.hpi** file, che è stato scaricato in prerequisiti. Quando si seleziona **caricare**, Jenkins hello plug-in viene installato automaticamente. Se richiesto, consentire il riavvio.

## <a name="create-and-configure-a-jenkins-job"></a>Creare e configurare un processo Jenkins

1. Creare un **nuovo elemento** dal dashboard.
2. Immettere un nome per l'elemento, ad esempio **MyJob**. Selezionare **free-style project** (progetto libero) e fare clic su **OK**.
3. Vai a pagina processo hello e fare clic su **configura**.

   a. Nella sezione generale hello in **GitHub progetto**, specificare l'URL di project di GitHub. Questo URL host servizio Fabric Java un'applicazione hello che si desidera toointegrate con hello integrazione continuata Jenkins, la distribuzione continua (CI/CD) flusso (ad esempio, ``https://github.com/sayantancs/SFJenkins``).

   b. In hello **gestione del codice sorgente** selezionare **Git**. Specificare l'URL del repository hello che ospita un'applicazione hello Java dell'infrastruttura di servizio che si desidera toointegrate con hello Jenkins CI/CD flusso (ad esempio, ``https://github.com/sayantancs/SFJenkins.git``). Inoltre, è possibile specificare quali toobuild branch (ad esempio, **/master**).
4. Configurare il *GitHub* (che ospita il repository hello) in modo che sia in grado di tootalk tooJenkins. Utilizzare hello alla procedura seguente:

   a. Vai a pagina repository di GitHub tooyour. Andare troppo**impostazioni** > **servizi e integrazioni**.

   b. Selezionare **Aggiungi servizio**, tipo **Jenkins**e seleziona hello **plug-in GitHub di Jenkins**.

   c. Immettere l'URL webhook di Jenkins (per impostazione predefinita, ``http://<PublicIPorFQDN>:8081/github-webhook/``). Fare clic su **add/update service** (aggiungi/aggiorna il servizio).

   d. Istanza Jenkins tooyour viene inviato un evento di test. Verrà visualizzato un segno di spunta verde per il webhook hello in GitHub e il progetto verrà compilato.

   e. In hello **trigger di compilazione** , selezionare l'opzione da quale di compilazione. In questo esempio si desidera tootrigger una compilazione ogni volta che si verifica un repository toohello push. Selezionare quindi l'opzione **GitHub hook trigger for GITScm polling** (Trigger di hook GitHub per polling GITScm). (In precedenza, questa opzione è stata chiamata **di compilazione quando una modifica viene inserita tooGitHub**.)

   f. In hello **compilare sezione**, dall'elenco a discesa hello **istruzione di compilazione Aggiungi**, selezionare l'opzione hello **richiamare Gradle Script**. Nel widget hello fornito, specificare il percorso di hello troppo**radice compilazione script** per l'applicazione. Preleva gradle dal percorso hello specificato e di conseguenza funziona. Se si crea un progetto denominato ``MyActor`` (utilizzando Generatore di plug-in o Yeoman Eclipse hello), script di compilazione hello radice deve contenere ``${WORKSPACE}/MyActor``. Vedere hello seguente schermata per un esempio di questo aspetto:

    ![Azione di compilazione di Jenkins per Service Fabric][build-step]

   g. Da hello **azioni post-compilazione** elenco a discesa, selezionare **Distribuisci progetto di infrastruttura servizio**. In questo caso, è necessario cluster tooprovide distribuzione dettagli hello Jenkins compilati applicazione di Service Fabric. È anche possibile fornire dettagli aggiuntivi dell'applicazione utilizzata un'applicazione hello toodeploy. Vedere hello seguente schermata per un esempio di questo aspetto:

    ![Azione di compilazione di Jenkins per Service Fabric][post-build-step]

   > [!NOTE]
   > cluster Hello qui potrebbe corrispondere allo hello hosting uno hello Jenkins applicazione contenitore, nel caso in cui si usa l'immagine di contenitore di Service Fabric toodeploy hello Jenkins.
   >

## <a name="next-steps"></a>Passaggi successivi
GitHub e Jenkins sono ora configurati. Prendere in considerazione alcuni esempio modifica il ``MyActor`` progetto nell'esempio hello repository https://github.com/sayantancs/SFJenkins. Push del tooa modifiche remoto ``master`` branch (o qualsiasi ramo configurati toowork con). Questa operazione attiva il processo di Jenkins hello, ``MyJob``, che è stato configurato. Recupera le modifiche di hello da GitHub, li compila e distribuisce l'endpoint di hello applicazione toohello cluster specificato nelle azioni di post-compilazione.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
