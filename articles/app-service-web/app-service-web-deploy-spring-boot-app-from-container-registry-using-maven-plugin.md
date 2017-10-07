---
title: aaaHow toouse hello plug-in Maven per le app Web di Azure toodeploy un'applicazione di avvio Spring in tooAzure del Registro di sistema di Azure contenitore servizio App
description: In questa esercitazione assiste l'utente tuttavia hello passaggi toodeploy un'applicazione di avvio molla nel Registro di sistema di Azure contenitore tooAzure tooAzure servizio App usando un plug-in di Maven.
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Come toouse hello plug-in Maven per le app Web di Azure toodeploy un'applicazione di avvio Spring in tooAzure del Registro di sistema di Azure contenitore servizio App

Hello  **[Spring Framework]**  è un framework open source più diffuso che consente agli sviluppatori Java di creare applicazioni API web e dispositivi mobili. Questa esercitazione viene utilizzato una app di esempio creata con [avvio Spring], un approccio basato su convenzione per l'utilizzo di tooget Spring in tempi brevi.

In questo articolo viene illustrato come toodeploy un tooAzure di applicazione di esempio Spring avvio contenitore del Registro di sistema e quindi utilizzare hello plug-in Maven per le app Web di Azure toodeploy il tooAzure di applicazione del servizio App.

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
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
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

   ![Esplorare l'app di esempio in locale][SB01]

## <a name="create-an-azure-service-principal"></a>Creare un'entità servizio di Azure

In questa sezione si crea un Azure entità di servizio che hello utilizza plug-in di Maven quando si distribuisce il tooAzure contenitore.

1. Aprire un prompt dei comandi.

1. Accesso all'account Azure tramite hello CLI di Azure:
   ```azurecli
   az login
   ```
   Seguire hello istruzioni toocomplete hello processo di accesso.

1. Creare un'entità servizio di Azure:
   ```azurecli
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

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Creare un Azure contenitore del Registro di sistema utilizzando hello CLI di Azure

1. Aprire un prompt dei comandi.

1. Accedi tooyour account di Azure:
   ```azurecli
   az login
   ```

1. Creare un gruppo di risorse per hello risorse di Azure che verrà utilizzato in questo articolo:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Sostituire il valore `wingtiptoysresources` di questo esempio con un nome univoco per il gruppo di risorse.

1. Creare un registro di sistema contenitore privato di Azure nel gruppo di risorse hello per l'app avvio molla: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Sostituire il valore `wingtiptoysregistry` di questo esempio con un nome univoco per il registro contenitori.

1. Recuperare la password di hello per il Registro di sistema del contenitore:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure restituirà la password, ad esempio:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Aggiungere impostazioni di Maven tooyour principale di servizi di Azure e del Registro di sistema di contenitore di Azure

1. Aprire il Maven `settings.xml` file in un editor di testo; questo file potrebbe essere in un percorso come hello seguono esempi:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Aggiungere le impostazioni di accesso del Registro di sistema di Azure contenitore dalla sezione precedente di hello di questo articolo di toohello `<servers>` insieme in hello *Settings* file; ad esempio:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Dove:
   Elemento | Descrizione
   ---|---|---
   `<id>` | Contiene il nome di hello contenitore privato di Azure del Registro di sistema.
   `<username>` | Contiene il nome di hello contenitore privato di Azure del Registro di sistema.
   `<password>` | Contiene la password di hello recuperato nella sezione precedente di hello di questo articolo.

1. Aggiungere le impostazioni dell'entità servizio di Azure da una sezione precedente di questo articolo di toohello `<servers>` insieme in hello *Settings* file; ad esempio:

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

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Compilare il Docker immagine contenitore e inviare tooyour del Registro di sistema contenitore di Azure

1. Passare directory del progetto toohello completato per l'applicazione di avvio Spring (ad esempio "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e aprire hello *pom.xml* file con un editor di testo.

1. Hello aggiornamento `<properties>` insieme in hello *pom.xml* file con valore hello di server di accesso per il Registro di sistema contenitore di Azure dalla sezione precedente di hello di questa esercitazione; ad esempio:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Dove:
   Elemento | Descrizione
   ---|---|---
   `<azure.containerRegistry>` | Specifica il nome di hello contenitore privato di Azure del Registro di sistema.
   `<docker.image.prefix>` | Specifica l'URL di hello contenitore privato di Azure del Registro di sistema, che è derivato aggiungendo ". azurecr.io" toohello nome contenitore privato del Registro di sistema.

1. Verificare che `<plugin>` per plug-in Docker hello nel *pom.xml* file contiene le proprietà corrette di hello hello nome di accesso server indirizzo e del Registro di sistema dal passaggio precedente hello in questa esercitazione. ad esempio:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Dove:
   Elemento | Descrizione
   ---|---|---
   `<serverId>` | Specifica la proprietà hello che contiene il nome contenitore privato di Azure del Registro di sistema.
   `<registryUrl>` | Specifica la proprietà hello che contiene l'URL di hello contenitore privato di Azure del Registro di sistema.

1. Directory del progetto toohello completato per l'applicazione di avvio Spring passare ed eseguire seguito comando toorebuild hello applicazione hello e push hello contenitore tooyour del Registro di sistema di contenitore di Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

1. Facoltativo: Sfoglia toohello [portale di Azure] e verificare che sia presente l'immagine contenitore Docker denominata **docker gs-spring-avvio** nel Registro di sistema contenitore.

   ![Verificare il contenitore nel portale di Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Personalizzare il pom.xml, quindi compilare e distribuire tooAzure il contenitore

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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
`<resourceGroup>` | Specifica il gruppo risorse destinazione hello, ovvero `wingtiptoysresources` in questo esempio. verrà creato il gruppo di risorse Hello durante la distribuzione se non esiste già.
`<appName>` | Specifica il nome di destinazione hello per le app web. In questo esempio, è il nome di destinazione hello `maven-linux-app-${maven.build.timestamp}`, dove hello `${maven.build.timestamp}` suffisso viene aggiunto in questo conflitto tooavoid di esempio. (timestamp hello è facoltativo, è possibile specificare qualsiasi stringa univoca per il nome dell'app hello).
`<region>` | Specifica l'area di destinazione hello, che in questo esempio è `westus`. (Un elenco completo è in hello [plug-in Maven per le app Web di Azure] documentazione.)
`<containerSettings>` | Specifica le proprietà di hello contenenti hello nome e l'URL del contenitore.
`<appSettings>` | Specifica eventuali impostazioni univoche per Maven toouse quando si distribuisce il tooAzure app web. In questo esempio, un `<property>` elemento contiene una coppia nome/valore di elementi figlio che specificano la porta hello per l'app.

> [!NOTE]
>
> Hello impostazioni toochange hello numero di porta in questo esempio sono necessari solo quando si modifica la porta hello da predefinito hello.
>

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

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello diverse tecnologie descritte in questo articolo, vedere hello seguenti articoli:

* [plug-in Maven per le app Web di Azure]

* [Accedi tooAzure da hello CLI di Azure](/azure/xplat-cli-connect)

* [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Informazioni di riferimento sulle impostazioni di Maven](https://maven.apache.org/settings.html)

* [Plug-in Docker per Maven]

<!-- URL List -->

[Azure interfaccia della riga di comando (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portale di Azure]: https://portal.azure.com/
[plug-in Maven per le app Web di Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Plug-in Docker per Maven]: https://github.com/spotify/docker-maven-plugin
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[avvio Spring]: http://projects.spring.io/spring-boot/
[avvio molla su Docker Introduzione]: https://github.com/spring-guides/gs-spring-boot-docker (Introduzione a Spring Boot in Docker)
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
