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
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="17c99-103">Come toouse hello plug-in Maven per le app Web di Azure toodeploy nei contenitori tooAzure app Spring avvio</span><span class="sxs-lookup"><span data-stu-id="17c99-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="17c99-104">Hello [plug-in Maven per le app Web di Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) per [Apache Maven](http://maven.apache.org/) fornisce un'integrazione perfetta di servizio App di Azure in progetti Maven e semplifica il processo di hello per le app web di sviluppatori toodeploy tooAzure servizio App.</span><span class="sxs-lookup"><span data-stu-id="17c99-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="17c99-105">In questo articolo viene illustrato l'utilizzo hello plug-in Maven per le app Web di Azure toodeploy un'applicazione di esempio Spring avvio in un tooAzure contenitore Docker servizi App.</span><span class="sxs-lookup"><span data-stu-id="17c99-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="17c99-106">Hello plug-in Maven per le app Web di Azure è attualmente disponibile come anteprima.</span><span class="sxs-lookup"><span data-stu-id="17c99-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="17c99-107">Per il momento, è supportata solo la pubblicazione FTP, anche se le funzionalità aggiuntive sono pianificate per hello future.</span><span class="sxs-lookup"><span data-stu-id="17c99-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="17c99-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="17c99-108">Prerequisites</span></span>

<span data-ttu-id="17c99-109">In ordine toocomplete hello passaggi di questa esercitazione, è necessario hello toohave seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="17c99-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="17c99-110">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="17c99-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="17c99-111">Hello [Azure interfaccia della riga di comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="17c99-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="17c99-112">Java Development Kit (JDK) aggiornato, versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="17c99-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="17c99-113">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="17c99-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="17c99-114">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="17c99-114">A [Git] client.</span></span>
* <span data-ttu-id="17c99-115">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="17c99-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="17c99-116">A causa di requisiti della virtualizzazione toohello di questa esercitazione, non è possibile seguire i passaggi di hello in questo articolo in una macchina virtuale; è necessario utilizzare un computer fisico con le funzionalità di virtualizzazione abilitate.</span><span class="sxs-lookup"><span data-stu-id="17c99-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="17c99-117">Esempio di hello clone avvio molla nell'applicazione web di Docker</span><span class="sxs-lookup"><span data-stu-id="17c99-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="17c99-118">In questa sezione si clona e si testa in locale un'applicazione Spring Boot in contenitore.</span><span class="sxs-lookup"><span data-stu-id="17c99-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="17c99-119">Aprire un prompt dei comandi o una finestra terminale e creare toohold una directory locale dell'applicazione di avvio molla e spostarsi nella directory toothat; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="17c99-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="17c99-120">- o-</span><span class="sxs-lookup"><span data-stu-id="17c99-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="17c99-121">Hello clone [avvio molla su Docker Introduzione] progetto di esempio nella directory hello è stato creato; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="17c99-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="17c99-122">Cambiare il progetto completato toohello directory; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="17c99-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="17c99-123">Compilare i file JAR hello utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="17c99-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="17c99-124">Quando hello web app è stato creato, avviare l'app web hello utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="17c99-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="17c99-125">Testare l'app web hello esplorando tooit localmente tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="17c99-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="17c99-126">Ad esempio, è possibile utilizzare il comando seguente, se si dispone di curl disponibili hello:</span><span class="sxs-lookup"><span data-stu-id="17c99-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="17c99-127">Dovrebbe essere hello segue messaggio visualizzato: **Docker Hello World**</span><span class="sxs-lookup"><span data-stu-id="17c99-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="17c99-128">Creare un'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="17c99-128">Create an Azure service principal</span></span>

<span data-ttu-id="17c99-129">In questa sezione si crea un Azure entità di servizio che hello utilizza plug-in di Maven quando si distribuisce il tooAzure contenitore.</span><span class="sxs-lookup"><span data-stu-id="17c99-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="17c99-130">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="17c99-130">Open a command prompt.</span></span>

1. <span data-ttu-id="17c99-131">Accesso all'account Azure tramite hello CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="17c99-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="17c99-132">Seguire hello istruzioni toocomplete hello processo di accesso.</span><span class="sxs-lookup"><span data-stu-id="17c99-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="17c99-133">Creare un'entità servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="17c99-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="17c99-134">Dove `uuuuuuuu` è il nome utente hello e `pppppppp` hello password per l'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="17c99-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="17c99-135">Azure risponde con il formato JSON che è simile a hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="17c99-135">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="17c99-136">Quando si configura toodeploy plug-in di Maven hello tooAzure il contenitore, si utilizzerà i valori hello questa risposta JSON.</span><span class="sxs-lookup"><span data-stu-id="17c99-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="17c99-137">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` sono valori segnaposto, ovvero utilizzata in questo esempio toomake toomap più facilmente questi valori tootheir rispettivi elementi quando si configura il Maven `settings.xml` file hello accanto sezione.</span><span class="sxs-lookup"><span data-stu-id="17c99-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="17c99-138">Configurare Maven toouse l'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="17c99-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="17c99-139">In questa sezione, utilizzare i valori hello dall'autenticazione di hello tooconfigure dell'entità servizio di Azure che usa Maven durante la distribuzione tooAzure il contenitore.</span><span class="sxs-lookup"><span data-stu-id="17c99-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="17c99-140">Aprire il Maven `settings.xml` file in un editor di testo; questo file potrebbe essere in un percorso come hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="17c99-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="17c99-141">Aggiungere le impostazioni dell'entità servizio di Azure dalla sezione precedente di hello di questa esercitazione toohello `<servers>` insieme in hello *Settings* file; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="17c99-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="17c99-142">Dove:</span><span class="sxs-lookup"><span data-stu-id="17c99-142">Where:</span></span>
   <span data-ttu-id="17c99-143">Elemento</span><span class="sxs-lookup"><span data-stu-id="17c99-143">Element</span></span> | <span data-ttu-id="17c99-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="17c99-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="17c99-145">Specifica un nome univoco utilizzato Maven toolook backup delle impostazioni di sicurezza quando si distribuisce il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="17c99-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="17c99-146">Contiene hello `appId` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="17c99-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="17c99-147">Contiene hello `tenant` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="17c99-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="17c99-148">Contiene hello `password` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="17c99-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="17c99-149">Definisce l'ambiente cloud di Azure di destinazione di hello ovvero `AZURE` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="17c99-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="17c99-150">(Un elenco completo degli ambienti è disponibile in hello [plug-in Maven per le app Web di Azure] documentazione)</span><span class="sxs-lookup"><span data-stu-id="17c99-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="17c99-151">Salvare e chiudere hello *Settings* file.</span><span class="sxs-lookup"><span data-stu-id="17c99-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="17c99-152">Facoltativo: Distribuire il tooDocker di file locale Docker Hub</span><span class="sxs-lookup"><span data-stu-id="17c99-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="17c99-153">Se si dispone di un account di Docker, è possibile compilare il Docker in locale l'immagine contenitore e spingerla tooDocker Hub.</span><span class="sxs-lookup"><span data-stu-id="17c99-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="17c99-154">toodo, utilizzare hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="17c99-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="17c99-155">Aprire hello `pom.xml` file per l'applicazione di avvio Spring in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="17c99-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="17c99-156">Individuare hello `<imageName>` elemento figlio di hello `<containerSettings>` elemento.</span><span class="sxs-lookup"><span data-stu-id="17c99-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="17c99-157">Hello aggiornamento `${docker.image.prefix}` valore con il nome dell'account Docker:</span><span class="sxs-lookup"><span data-stu-id="17c99-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="17c99-158">Scegliere uno dei seguenti metodi di distribuzione hello:</span><span class="sxs-lookup"><span data-stu-id="17c99-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="17c99-159">Genera l'immagine del contenitore in locale con Maven e quindi utilizzare il tooDocker contenitore Hub Docker toopush:</span><span class="sxs-lookup"><span data-stu-id="17c99-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="17c99-160">Se si dispone di hello [plug-in di Docker per Maven] installato, è possibile compilare automaticamente e tooDocker di immagine del contenitore Hub utilizzando hello `-DpushImage` parametro:</span><span class="sxs-lookup"><span data-stu-id="17c99-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="17c99-161">Facoltativo: Personalizzare il pom.xml prima di distribuire il contenitore tooAzure</span><span class="sxs-lookup"><span data-stu-id="17c99-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="17c99-162">Aprire hello `pom.xml` file per l'applicazione di avvio Spring in un editor di testo e quindi individuare hello `<plugin>` elemento per `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="17c99-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="17c99-163">Questo elemento dovrebbe essere simile a hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="17c99-163">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="17c99-164">Esistono diversi valori che è possibile modificare per plug-in di Maven hello e una descrizione dettagliata per ognuno di questi elementi è disponibile in hello [plug-in Maven per le app Web di Azure] documentazione.</span><span class="sxs-lookup"><span data-stu-id="17c99-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="17c99-165">Dopo questa premessa, in questo articolo è opportuno evidenziare diversi valori:</span><span class="sxs-lookup"><span data-stu-id="17c99-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="17c99-166">Elemento</span><span class="sxs-lookup"><span data-stu-id="17c99-166">Element</span></span> | <span data-ttu-id="17c99-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="17c99-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="17c99-168">Specifica la versione di hello di hello [plug-in Maven per le app Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="17c99-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="17c99-169">Controllare versione hello elencata in hello [repository centrale Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure che si sta utilizzando hello versione più recente.</span><span class="sxs-lookup"><span data-stu-id="17c99-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="17c99-170">Specifica le informazioni di autenticazione hello per Azure, che in questo esempio contiene un `<serverId>` elemento contenente `azure-auth`; Maven utilizza tale toolook valore i valori dell'entità servizio di Azure di hello nel Maven *Settings* file, che è definito in una sezione precedente di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="17c99-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="17c99-171">Specifica il gruppo risorse destinazione hello, ovvero `maven-plugin` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="17c99-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="17c99-172">verrà creato il gruppo di risorse Hello durante la distribuzione se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="17c99-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="17c99-173">Specifica il nome di destinazione hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="17c99-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="17c99-174">In questo esempio, è il nome di destinazione hello `maven-linux-app-${maven.build.timestamp}`, dove hello `${maven.build.timestamp}` suffisso viene aggiunto in questo conflitto tooavoid di esempio.</span><span class="sxs-lookup"><span data-stu-id="17c99-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="17c99-175">(timestamp hello è facoltativo, è possibile specificare qualsiasi stringa univoca per il nome dell'app hello).</span><span class="sxs-lookup"><span data-stu-id="17c99-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="17c99-176">Specifica l'area di destinazione hello, che in questo esempio è `westus`.</span><span class="sxs-lookup"><span data-stu-id="17c99-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="17c99-177">(Un elenco completo è in hello [plug-in Maven per le app Web di Azure] documentazione.)</span><span class="sxs-lookup"><span data-stu-id="17c99-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="17c99-178">Specifica eventuali impostazioni univoche per Maven toouse quando si distribuisce il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="17c99-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="17c99-179">In questo esempio, un `<property>` elemento contiene una coppia nome/valore di elementi figlio che specificano la porta hello per l'app.</span><span class="sxs-lookup"><span data-stu-id="17c99-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="17c99-180">Hello impostazioni toochange hello numero di porta in questo esempio sono necessari solo quando si modifica la porta hello da predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="17c99-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="17c99-181">Compilare e distribuire il contenitore tooAzure</span><span class="sxs-lookup"><span data-stu-id="17c99-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="17c99-182">Dopo aver configurato le impostazioni di hello in hello precedenti sezioni di questo articolo, si è pronti toodeploy tooAzure il contenitore.</span><span class="sxs-lookup"><span data-stu-id="17c99-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="17c99-183">toodo in tal caso, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="17c99-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="17c99-184">Dal prompt dei comandi di hello o finestra terminale che si utilizzava in precedenza, ricompilare il file JAR hello utilizzando Maven se toohello eventuali modifiche apportate *pom.xml* file; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="17c99-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="17c99-185">Distribuire il tooAzure app web utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="17c99-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="17c99-186">Maven distribuirà tooAzure l'app web; Se l'applicazione web hello non esiste già, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="17c99-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="17c99-187">Se area hello specificati nel hello `<region>` elemento il *pom.xml* file non è sufficiente server disponibili quando si avvia la distribuzione, è possibile visualizzare un toohello simile di errore riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="17c99-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="17c99-188">In questo caso, è possibile specificare che un'altra area ed eseguire di nuovo hello Maven comando toodeploy l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17c99-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="17c99-189">Quando è stato distribuito il web, sarà in grado di toomanage usando hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="17c99-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="17c99-190">L'app Web sarà elencata in **Servizi app**:</span><span class="sxs-lookup"><span data-stu-id="17c99-190">Your web app will be listed in **App Services**:</span></span>

   ![App Web elencata in Servizi app nel portale di Azure][AP01]

* <span data-ttu-id="17c99-192">E hello URL per l'app web sarà elencato nel hello **Panoramica** per l'app web:</span><span class="sxs-lookup"><span data-stu-id="17c99-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="17c99-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17c99-194">Next steps</span></span>

<span data-ttu-id="17c99-195">Per ulteriori informazioni su hello diverse tecnologie descritte in questo articolo, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="17c99-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="17c99-196">[plug-in Maven per le app Web di Azure]</span><span class="sxs-lookup"><span data-stu-id="17c99-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="17c99-197">Accedi tooAzure da hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="17c99-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="17c99-198">Come toouse hello plug-in Maven per le app Web di Azure toodeploy un tooAzure app Spring avvio servizio App</span><span class="sxs-lookup"><span data-stu-id="17c99-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="17c99-199">Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="17c99-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="17c99-200">Informazioni di riferimento sulle impostazioni di Maven</span><span class="sxs-lookup"><span data-stu-id="17c99-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="17c99-201">[plug-in di Docker per Maven]</span><span class="sxs-lookup"><span data-stu-id="17c99-201">[Docker plugin for Maven]</span></span>

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
