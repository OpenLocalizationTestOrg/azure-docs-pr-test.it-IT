---
title: aaaDeploy un'App Web di avvio molla su Linux nel servizio contenitore di Azure | Documenti Microsoft
description: In questa esercitazione viene tuttavia hello passaggi toodeploy un'applicazione di avvio molla come un'app web di Linux in Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Distribuire un'applicazione di avvio molla su Linux in hello servizio contenitore di Azure

Hello  **[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale. Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.

**[Docker]**  è soluzioni open source che consente agli sviluppatori di automatizzare la distribuzione di hello, scalabilità e gestione delle applicazioni in esecuzione nei contenitori.

In questa esercitazione illustra tramite Docker toodevelop e distribuire un host di Linux Spring avvio applicazione tooa in hello [servizio contenitore di Azure (ACS)].

## <a name="prerequisites"></a>Prerequisiti

In ordine toocomplete hello passaggi di questa esercitazione, è necessario hello toohave seguenti prerequisiti:

* Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].
* Hello [Azure interfaccia della riga di comando (CLI)].
* Un [Java Developer Kit (JDK)] aggiornato.
* Lo strumento di compilazione [Maven] di Apache (versione 3).
* Un client [Git].
* Un client [Docker].

> [!NOTE]
>
> A causa di requisiti della virtualizzazione toohello di questa esercitazione, non è possibile seguire i passaggi di hello in questo articolo in una macchina virtuale; è necessario utilizzare un computer fisico con le funzionalità di virtualizzazione abilitate.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Creare hello avvio molla nell'applicazione web di Guida introduttiva di Docker

Hello passaggi seguenti consentono di eseguire passaggi di hello che sono necessari toocreate una semplice applicazione web di avvio molla ed eseguirne il test in locale.

1. Aprire un prompt dei comandi e creare toohold una directory locale dell'applicazione e spostarsi nella directory toothat; Per esempio:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - o-
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Hello clone [avvio molla su Docker Introduzione] progetto di esempio nella directory hello è stato creato; ad esempio:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Cambiare il progetto completato toohello directory; Per esempio:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Compilare i file JAR hello utilizzando Maven; Per esempio:
   ```
   mvn package
   ```

1. Una volta hello web app è stata creata, cambiare directory toohello `target` directory in cui si trova il file JAR hello e avvia l'app web hello; ad esempio:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Testare l'app web hello esplorando tooit localmente tramite un web browser. Ad esempio, se dispone di curl disponibile e configurato hello Tomcat server toorun sulla porta 80:
   ```
   curl http://localhost
   ```

1. Dovrebbe essere hello segue messaggio visualizzato: **Docker Hello World!**

   ![Esplorare l'app di esempio in locale][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Creare un toouse del Registro di sistema di Azure contenitore privato Docker Registro di sistema

Hello passaggi seguenti consentono l'utilizzo di hello toocreate portale Azure del Registro di sistema un contenitore di Azure.

> [!NOTE]
>
> Se si vuole toouse hello CLI di Azure anziché hello portale di Azure, seguire i passaggi di hello in [creare un registro di sistema contenitore Docker privata mediante hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).
>

1. Sfoglia toohello [portale di Azure] ed eseguire l'accesso.

   Dopo l'accesso account tooyour in hello portale di Azure, è possibile seguire i passaggi di hello in hello [creare un registro di sistema contenitore Docker privata tramite il portale di Azure hello] articolo, sono tratto in hello alla procedura seguente per hello efficienza di convenienza.

1. Fare clic sull'icona di menu hello per **+ nuovo**, quindi fare clic su **contenitori**, quindi fare clic su **Registro di sistema di Azure contenitore**.
   
   ![Creare un nuovo Registro contenitori di Azure][AR01]

1. Quando viene visualizzata la pagina informazioni hello per il modello del Registro di sistema di Azure contenitore hello, fare clic su **crea**. 

   ![Creare un nuovo Registro contenitori di Azure][AR02]

1. Quando hello **Registro di sistema contenitore crea** viene visualizzata la pagina, immettere il **del Registro di sistema** e **gruppo di risorse**, scegliere **abilitare** per Hello **utente Admin**, quindi fare clic su **crea**.

   ![Configurare le impostazioni del Registro contenitori di Azure][AR03]

1. Dopo aver creato il Registro di sistema del contenitore, passare tooyour contenitore del Registro di sistema hello portale di Azure e quindi fare clic su **chiavi di accesso**. Prendere nota del nome utente di hello e una password per i passaggi successivi hello.

   ![Chiavi di accesso al Registro contenitori di Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Configurare le chiavi di accesso del Registro di sistema di Azure contenitore di Maven toouse

1. Passare toohello directory di configurazione per l'installazione di Maven e aprire hello *Settings* file con un editor di testo.

1. Aggiungere le impostazioni di accesso del Registro di sistema di Azure contenitore dalla sezione precedente di hello di questa esercitazione toohello `<servers>` insieme in hello *Settings* file; ad esempio:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Passare a directory di progetto toohello completato per l'applicazione di avvio molla, (ad esempio: "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker / completamento*") e aprire hello *pom.xml* file con un editor di testo.

1. Hello aggiornamento `<properties>` insieme in hello *pom.xml* file con valore hello di server di accesso per il Registro di sistema contenitore di Azure dalla sezione precedente di hello di questa esercitazione; ad esempio:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Hello aggiornamento `<plugins>` insieme in hello *pom.xml* file in modo che hello `<plugin>` contiene hello server indirizzo e del Registro di sistema nome di accesso per il Registro di sistema contenitore di Azure dalla sezione precedente di hello di questa esercitazione. ad esempio:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Directory del progetto toohello completato per l'applicazione di avvio Spring passare ed eseguire seguito comando toorebuild hello applicazione hello e push hello contenitore tooyour del Registro di sistema di Azure contenitore:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Quando si effettua il push del tooAzure contenitore Docker, si potrebbe ricevere un messaggio di errore è simile tooone di hello seguente anche se è stato creato il contenitore Docker:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> In questo caso, potrebbe essere necessario toosign in tooyour account Azure dalla riga di comando di Docker hello; Per esempio:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> È quindi possibile distribuire il contenitore dalla riga di comando hello; Per esempio:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Creare un'app Web in Linux nel servizio app di Azure usando l'immagine del contenitore

1. Sfoglia toohello [portale di Azure] ed eseguire l'accesso.

1. Fare clic sull'icona di menu hello per **+ nuovo**, quindi fare clic su **Web e dispositivi mobili**, quindi fare clic su **App Web in Linux**.
   
   ![Creare una nuova app web nel portale di Azure hello][LX01]

1. Quando hello **App Web in Linux** viene visualizzata la pagina, immettere hello le seguenti informazioni:

   a. Immettere un nome univoco per hello **nome App**, ad esempio: "*wingtiptoyslinux*."

   b. Scegliere il **sottoscrizione** dall'elenco a discesa hello.

   c. Scegliere un oggetto esistente **gruppo di risorse**, oppure specificare un toocreate nome nuovo gruppo di risorse.

   d. Fare clic su **Configura contenitore** e immettere hello le seguenti informazioni:

      * Scegliere **Registro di sistema privato**.

      * **Immagine e tag facoltativo**: specificare il nome del contenitore dai passaggi precedenti, ad esempio: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"

      * **URL server**: specificare l'URL del registro dai passaggi precedenti, ad esempio: "*https://wingtiptoysregistry.azurecr.io*"

      * **Nome utente di accesso** e **Password**: specificare le credenziali di accesso dalle **Chiavi di accesso** usate nei passaggi precedenti.
   
   e. Dopo aver immesso tutte hello sopra informazioni, fare clic su **OK**.

   ![Configurare le impostazioni dell'app Web][LX02]

1. Fare clic su **Crea**.

> [!NOTE]
>
> Azure eseguirà automaticamente il mapping Internet richieste tooembedded Tomcat server in cui viene eseguito su porte standard di hello di 80 o 8080. Tuttavia, se è stato configurato l'incorporato toorun server Tomcat su una porta personalizzata, è necessario tooadd un'app web tooyour variabile di ambiente che definisce la porta hello del server Tomcat incorporato. toodo in tal caso, utilizzare hello alla procedura seguente:
>
> 1. Sfoglia toohello [portale di Azure] ed eseguire l'accesso.
> 
> 2. Fare clic sull'icona hello **servizi App**. (Vedere il #1 immagine hello riportata di seguito).
>
> 3. Selezionare l'app web dall'elenco di hello. (Voce #2 dell'immagine hello riportata di seguito).
>
> 4. Fare clic su **Impostazioni applicazione**. (Voce #3 dell'immagine di hello riportata di seguito).
>
> 5. In hello **impostazioni App** sezione, aggiungere una nuova variabile di ambiente denominata **porta** e immettere il numero di porta personalizzato per il valore di hello. (Voce #4 dell'immagine di hello riportata di seguito).
>
> 6. Fare clic su **Salva**. (Voce #5 dell'immagine di hello riportata di seguito).
>
> ![Salvataggio di un numero di porta personalizzato in hello portale di Azure][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'utilizzo di applicazioni di avvio Spring in Azure, vedere hello seguenti articoli:

* [Distribuire un servizio App di Azure di toohello Spring avvio applicazione](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Distribuire un'applicazione di avvio Spring in un Kubernetes Cluster in hello servizio contenitore di Azure](container-service-deploy-spring-boot-app-on-kubernetes.md)

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].

Per ulteriori dettagli sull'hello Spring avvio nel progetto di esempio Docker, vedere [avvio molla su Docker Introduzione].

Per informazioni sulla Guida introduttiva a applicazioni Spring avvio, vedere hello **Initializr Spring** in https://start.spring.io/.

Per ulteriori informazioni sulle attività iniziali con la creazione di una semplice applicazione di avvio molla, vedere hello Spring Initializr in https://start.spring.io/.

Per altri esempi per la modalità toouse immagini Docker personalizzato con Azure, vedere [utilizzando un'immagine Docker personalizzata per l'App Web di Azure in Linux].

<!-- URL List -->

[Azure interfaccia della riga di comando (CLI)]: /cli/azure/overview
[servizio contenitore di Azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[portale di Azure]: https://portal.azure.com/
[creare un registro di sistema contenitore Docker privata tramite il portale di Azure hello]: /azure/container-registry/container-registry-get-started-portal
[utilizzando un'immagine Docker personalizzata per l'App Web di Azure in Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[avvio Spring]: http://projects.spring.io/spring-boot/
[avvio molla su Docker Introduzione]: https://github.com/spring-guides/gs-spring-boot-docker (Introduzione a Spring Boot in Docker)
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
