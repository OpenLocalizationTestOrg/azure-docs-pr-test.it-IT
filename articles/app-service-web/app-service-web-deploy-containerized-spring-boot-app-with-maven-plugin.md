---
title: aaaHow toouse hello plug-in Maven per le app Web di Azure toodeploy nei contenitori tooAzure app Spring avvio
description: Informazioni su come toouse hello plug-in Maven per le app Web di Azure toodeploy un tooAzure app Spring avvio.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a>Come toouse hello plug-in Maven per le app Web di Azure toodeploy nei contenitori tooAzure app Spring avvio

Hello [plug-in Maven per le app Web di Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) per [Apache Maven](http://maven.apache.org/) fornisce un'integrazione perfetta di servizio App di Azure in progetti Maven e semplifica il processo di hello per le app web di sviluppatori toodeploy tooAzure servizio App.

In questo articolo viene illustrato l'utilizzo hello plug-in Maven per le app Web di Azure toodeploy un'applicazione di esempio Spring avvio in un tooAzure contenitore Docker servizi App.

> [!NOTE]
>
> Hello plug-in Maven per le app Web di Azure è attualmente disponibile come anteprima. Per il momento, è supportata solo la pubblicazione FTP, anche se le funzionalità aggiuntive sono pianificate per hello future.
>

## <a name="prerequisites"></a>Prerequisiti

In ordine toocomplete hello passaggi di questa esercitazione, è necessario hello toohave seguenti prerequisiti:

* Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].
* Hello [Azure interfaccia della riga di comando (CLI)].
* Java Development Kit (JDK) aggiornato, versione 1.7 o successiva.
* Lo strumento di compilazione [Maven] di Apache (versione 3).
* Un client [Git].
* Un client [Docker].

> [!NOTE]
>
> A causa di requisiti della virtualizzazione toohello di questa esercitazione, non è possibile seguire i passaggi di hello in questo articolo in una macchina virtuale; è necessario utilizzare un computer fisico con le funzionalità di virtualizzazione abilitate.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Esempio di hello clone avvio molla nell'applicazione web di Docker

In questa sezione si clona e si testa in locale un'applicazione Spring Boot in contenitore.

1. Aprire un prompt dei comandi o una finestra terminale e creare toohold una directory locale dell'applicazione di avvio molla e spostarsi nella directory toothat; Per esempio:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - o-
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Hello clone [avvio molla su Docker Introduzione] progetto di esempio nella directory hello è stato creato; ad esempio:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. Cambiare il progetto completato toohello directory; Per esempio:
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. Compilare i file JAR hello utilizzando Maven; Per esempio:
   ```shell
   mvn clean package
   ```

1. Quando hello web app è stato creato, avviare l'app web hello utilizzando Maven; Per esempio:
   ```shell
   mvn spring-boot:run
   ```

1. Testare l'app web hello esplorando tooit localmente tramite un web browser. Ad esempio, è possibile utilizzare il comando seguente, se si dispone di curl disponibili hello:
   ```shell
   curl http://localhost:8080
   ```

1. Dovrebbe essere hello segue messaggio visualizzato: **Docker Hello World**

## <a name="create-an-azure-service-principal"></a>Creare un'entità servizio di Azure

In questa sezione si crea un Azure entità di servizio che hello utilizza plug-in di Maven quando si distribuisce il tooAzure contenitore.

1. Aprire un prompt dei comandi.

1. Accesso all'account Azure tramite hello CLI di Azure:
   ```shell
   az login
   ```
   Seguire hello istruzioni toocomplete hello processo di accesso.

1. Creare un'entità servizio di Azure:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Dove `uuuuuuuu` è il nome utente hello e `pppppppp` hello password per l'entità servizio hello.

1. Azure risponde con il formato JSON che è simile a hello di esempio seguente:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Quando si configura toodeploy plug-in di Maven hello tooAzure il contenitore, si utilizzerà i valori hello questa risposta JSON. Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` sono valori segnaposto, ovvero utilizzata in questo esempio toomake toomap più facilmente questi valori tootheir rispettivi elementi quando si configura il Maven `settings.xml` file hello accanto sezione.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Configurare Maven toouse l'entità servizio di Azure

In questa sezione, utilizzare i valori hello dall'autenticazione di hello tooconfigure dell'entità servizio di Azure che usa Maven durante la distribuzione tooAzure il contenitore.

1. Aprire il Maven `settings.xml` file in un editor di testo; questo file potrebbe essere in un percorso come hello seguono esempi:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Aggiungere le impostazioni dell'entità servizio di Azure dalla sezione precedente di hello di questa esercitazione toohello `<servers>` insieme in hello *Settings* file; ad esempio:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Dove:
   Elemento | Descrizione
   ---|---|---
   `<id>` | Specifica un nome univoco utilizzato Maven toolook backup delle impostazioni di sicurezza quando si distribuisce il tooAzure app web.
   `<client>` | Contiene hello `appId` compreso l'entità servizio.
   `<tenant>` | Contiene hello `tenant` compreso l'entità servizio.
   `<key>` | Contiene hello `password` compreso l'entità servizio.
   `<environment>` | Definisce l'ambiente cloud di Azure di destinazione di hello ovvero `AZURE` in questo esempio. (Un elenco completo degli ambienti è disponibile in hello [plug-in Maven per le app Web di Azure] documentazione)

1. Salvare e chiudere hello *Settings* file.

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a>Facoltativo: Distribuire il tooDocker di file locale Docker Hub

Se si dispone di un account di Docker, è possibile compilare il Docker in locale l'immagine contenitore e spingerla tooDocker Hub. toodo, utilizzare hello alla procedura seguente.

1. Aprire hello `pom.xml` file per l'applicazione di avvio Spring in un editor di testo.

1. Individuare hello `<imageName>` elemento figlio di hello `<containerSettings>` elemento.

1. Hello aggiornamento `${docker.image.prefix}` valore con il nome dell'account Docker:
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. Scegliere uno dei seguenti metodi di distribuzione hello:

   * Genera l'immagine del contenitore in locale con Maven e quindi utilizzare il tooDocker contenitore Hub Docker toopush:
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * Se si dispone di hello [plug-in di Docker per Maven] installato, è possibile compilare automaticamente e tooDocker di immagine del contenitore Hub utilizzando hello `-DpushImage` parametro:
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a>Facoltativo: Personalizzare il pom.xml prima di distribuire il contenitore tooAzure

Aprire hello `pom.xml` file per l'applicazione di avvio Spring in un editor di testo e quindi individuare hello `<plugin>` elemento per `azure-webapp-maven-plugin`. Questo elemento dovrebbe essere simile a hello di esempio seguente:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Esistono diversi valori che è possibile modificare per plug-in di Maven hello e una descrizione dettagliata per ognuno di questi elementi è disponibile in hello [plug-in Maven per le app Web di Azure] documentazione. Dopo questa premessa, in questo articolo è opportuno evidenziare diversi valori:

Elemento | Descrizione
---|---|---
`<version>` | Specifica la versione di hello di hello [plug-in Maven per le app Web di Azure]. Controllare versione hello elencata in hello [repository centrale Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure che si sta utilizzando hello versione più recente.
`<authentication>` | Specifica le informazioni di autenticazione hello per Azure, che in questo esempio contiene un `<serverId>` elemento contenente `azure-auth`; Maven utilizza tale toolook valore i valori dell'entità servizio di Azure di hello nel Maven *Settings* file, che è definito in una sezione precedente di questo articolo.
`<resourceGroup>` | Specifica il gruppo risorse destinazione hello, ovvero `maven-plugin` in questo esempio. verrà creato il gruppo di risorse Hello durante la distribuzione se non esiste già.
`<appName>` | Specifica il nome di destinazione hello per le app web. In questo esempio, è il nome di destinazione hello `maven-linux-app-${maven.build.timestamp}`, dove hello `${maven.build.timestamp}` suffisso viene aggiunto in questo conflitto tooavoid di esempio. (timestamp hello è facoltativo, è possibile specificare qualsiasi stringa univoca per il nome dell'app hello).
`<region>` | Specifica l'area di destinazione hello, che in questo esempio è `westus`. (Un elenco completo è in hello [plug-in Maven per le app Web di Azure] documentazione.)
`<appSettings>` | Specifica eventuali impostazioni univoche per Maven toouse quando si distribuisce il tooAzure app web. In questo esempio, un `<property>` elemento contiene una coppia nome/valore di elementi figlio che specificano la porta hello per l'app.

> [!NOTE]
>
> Hello impostazioni toochange hello numero di porta in questo esempio sono necessari solo quando si modifica la porta hello da predefinito hello.
>

## <a name="build-and-deploy-your-container-tooazure"></a>Compilare e distribuire il contenitore tooAzure

Dopo aver configurato le impostazioni di hello in hello precedenti sezioni di questo articolo, si è pronti toodeploy tooAzure il contenitore. toodo in tal caso, utilizzare hello alla procedura seguente:

1. Dal prompt dei comandi di hello o finestra terminale che si utilizzava in precedenza, ricompilare il file JAR hello utilizzando Maven se toohello eventuali modifiche apportate *pom.xml* file; ad esempio:
   ```shell
   mvn clean package
   ```

1. Distribuire il tooAzure app web utilizzando Maven; Per esempio:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven distribuirà tooAzure l'app web; Se l'applicazione web hello non esiste già, verrà creato.

> [!NOTE]
>
> Se area hello specificati nel hello `<region>` elemento il *pom.xml* file non è sufficiente server disponibili quando si avvia la distribuzione, è possibile visualizzare un toohello simile di errore riportato di seguito:
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> In questo caso, è possibile specificare che un'altra area ed eseguire di nuovo hello Maven comando toodeploy l'applicazione.
>
>

Quando è stato distribuito il web, sarà in grado di toomanage usando hello [portale di Azure].

* L'app Web sarà elencata in **Servizi app**:

   ![App Web elencata in Servizi app nel portale di Azure][AP01]

* E hello URL per l'app web sarà elencato nel hello **Panoramica** per l'app web:

   ![Determinare l'URL di hello per le app web][AP02]

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

Per ulteriori informazioni su hello diverse tecnologie descritte in questo articolo, vedere hello seguenti articoli:

* [plug-in Maven per le app Web di Azure]

* [Accedi tooAzure da hello CLI di Azure](/azure/xplat-cli-connect)

* [Come toouse hello plug-in Maven per le app Web di Azure toodeploy un tooAzure app Spring avvio servizio App](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Informazioni di riferimento sulle impostazioni di Maven](https://maven.apache.org/settings.html)

* [plug-in di Docker per Maven]

<!-- URL List -->

[Azure interfaccia della riga di comando (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portale di Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[plug-in di Docker per Maven]: https://github.com/spotify/docker-maven-plugin
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[avvio molla su Docker Introduzione]: https://github.com/spring-guides/gs-spring-boot-docker (Introduzione a Spring Boot in Docker)
[Spring Framework]: https://spring.io/
[plug-in Maven per le app Web di Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
