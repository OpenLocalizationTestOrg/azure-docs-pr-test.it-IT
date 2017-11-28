---
title: aaaHow toouse hello plug-in Maven per le app Web di Azure toodeploy un tooAzure app Spring avvio
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
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="f6bdf-103">Come toouse hello plug-in Maven per le app Web di Azure toodeploy un tooAzure app Spring avvio</span><span class="sxs-lookup"><span data-stu-id="f6bdf-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="f6bdf-104">Hello [plug-in Maven per le app Web di Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) per [Apache Maven](http://maven.apache.org/) fornisce un'integrazione perfetta di servizio App di Azure in progetti Maven e semplifica il processo di hello per le app web di sviluppatori toodeploy tooAzure servizio App.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="f6bdf-105">In questo articolo viene illustrato l'utilizzo hello plug-in Maven per le app Web di Azure toodeploy un tooAzure di applicazione di esempio Spring avvio servizi App.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="f6bdf-106">Hello plug-in Maven per le app Web di Azure è attualmente disponibile come anteprima.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="f6bdf-107">Per il momento, è supportata solo la pubblicazione FTP, anche se le funzionalità aggiuntive sono pianificate per hello future.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="f6bdf-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f6bdf-108">Prerequisites</span></span>

<span data-ttu-id="f6bdf-109">In ordine toocomplete hello passaggi di questa esercitazione, è necessario hello toohave seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="f6bdf-110">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="f6bdf-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="f6bdf-111">Hello [Azure interfaccia della riga di comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="f6bdf-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="f6bdf-112">Java Development Kit (JDK) aggiornato, versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="f6bdf-113">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="f6bdf-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="f6bdf-114">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="f6bdf-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="f6bdf-115">Clone hello esempio Spring avvio web app</span><span class="sxs-lookup"><span data-stu-id="f6bdf-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="f6bdf-116">In questa sezione si clona e si testa in locale un'applicazione Spring Boot completata.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="f6bdf-117">Aprire un prompt dei comandi o una finestra terminale e creare toohold una directory locale dell'applicazione di avvio molla e spostarsi nella directory toothat; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="f6bdf-118">- o-</span><span class="sxs-lookup"><span data-stu-id="f6bdf-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="f6bdf-119">Hello clone [Spring avvio Introduzione] progetto di esempio nella directory hello è stato creato; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="f6bdf-120">Cambiare il progetto completato toohello directory; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="f6bdf-121">Compilare i file JAR hello utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="f6bdf-122">Quando hello web app è stato creato, avviare l'app web hello utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="f6bdf-123">Testare l'app web hello esplorando tooit localmente tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="f6bdf-124">Ad esempio, è possibile utilizzare il comando seguente, se si dispone di curl disponibili hello:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="f6bdf-125">Dovrebbe essere hello segue messaggio visualizzato: **Greetings da avvio Spring!**</span><span class="sxs-lookup"><span data-stu-id="f6bdf-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="f6bdf-126">Creare un'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="f6bdf-126">Create an Azure service principal</span></span>

<span data-ttu-id="f6bdf-127">In questa sezione si crea un Azure entità di servizio che hello utilizza plug-in di Maven quando si distribuisce il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="f6bdf-128">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-128">Open a command prompt.</span></span>

1. <span data-ttu-id="f6bdf-129">Accesso all'account Azure tramite hello CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="f6bdf-130">Seguire hello istruzioni toocomplete hello processo di accesso.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="f6bdf-131">Creare un'entità servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="f6bdf-132">Dove `uuuuuuuu` è il nome utente hello e `pppppppp` hello password per l'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="f6bdf-133">Azure risponde con il formato JSON che è simile a hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="f6bdf-134">Quando si configura toodeploy plug-in di Maven hello il tooAzure app web, si utilizzerà i valori hello questa risposta JSON.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="f6bdf-135">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` sono valori segnaposto, ovvero utilizzata in questo esempio toomake toomap più facilmente questi valori tootheir rispettivi elementi quando si configura il Maven `settings.xml` file hello accanto sezione.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="f6bdf-136">Configurare Maven toouse l'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="f6bdf-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="f6bdf-137">In questa sezione, utilizzare i valori hello dall'autenticazione hello tooconfigure dell'entità servizio di Azure Maven usato quando si distribuisce il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="f6bdf-138">Aprire il Maven `settings.xml` file in un editor di testo; questo file potrebbe essere in un percorso come hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="f6bdf-139">Aggiungere le impostazioni dell'entità servizio di Azure dalla sezione precedente di hello di questa esercitazione toohello `<servers>` insieme in hello *Settings* file; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="f6bdf-140">Dove:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-140">Where:</span></span>
   <span data-ttu-id="f6bdf-141">Elemento</span><span class="sxs-lookup"><span data-stu-id="f6bdf-141">Element</span></span> | <span data-ttu-id="f6bdf-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f6bdf-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="f6bdf-143">Specifica un nome univoco utilizzato Maven toolook backup delle impostazioni di sicurezza quando si distribuisce il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="f6bdf-144">Contiene hello `appId` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="f6bdf-145">Contiene hello `tenant` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="f6bdf-146">Contiene hello `password` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="f6bdf-147">Definisce l'ambiente cloud di Azure di destinazione di hello ovvero `AZURE` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="f6bdf-148">(Un elenco completo degli ambienti è disponibile in hello [plug-in Maven per le app Web di Azure] documentazione)</span><span class="sxs-lookup"><span data-stu-id="f6bdf-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="f6bdf-149">Salvare e chiudere hello *Settings* file.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="f6bdf-150">Facoltativo: Personalizzare il pom.xml prima di distribuire il tooAzure app web</span><span class="sxs-lookup"><span data-stu-id="f6bdf-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="f6bdf-151">Aprire hello `pom.xml` file per l'applicazione di avvio Spring in un editor di testo e quindi individuare hello `<plugin>` elemento per `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="f6bdf-152">Questo elemento dovrebbe essere simile a hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-152">This element should resemble hello following example:</span></span>

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="f6bdf-153">Esistono diversi valori che è possibile modificare per plug-in di Maven hello e una descrizione dettagliata per ognuno di questi elementi è disponibile in hello [plug-in Maven per le app Web di Azure] documentazione.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="f6bdf-154">Dopo questa premessa, in questo articolo è opportuno evidenziare diversi valori:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="f6bdf-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="f6bdf-155">Element</span></span> | <span data-ttu-id="f6bdf-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f6bdf-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="f6bdf-157">Specifica la versione di hello di hello [plug-in Maven per le app Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="f6bdf-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="f6bdf-158">Controllare versione hello elencata in hello [repository centrale Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure che si sta utilizzando hello versione più recente.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="f6bdf-159">Specifica le informazioni di autenticazione hello per Azure, che in questo esempio contiene un `<serverId>` elemento contenente `azure-auth`; Maven utilizza tale toolook valore i valori dell'entità servizio di Azure di hello nel Maven *Settings* file, che è definito in una sezione precedente di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="f6bdf-160">Specifica il gruppo risorse destinazione hello, ovvero `maven-plugin` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="f6bdf-161">gruppo di risorse Hello viene creato durante la distribuzione se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="f6bdf-162">Specifica il nome di destinazione hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="f6bdf-163">In questo esempio, è il nome di destinazione hello `maven-web-app-${maven.build.timestamp}`, dove hello `${maven.build.timestamp}` suffisso viene aggiunto in questo conflitto tooavoid di esempio.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="f6bdf-164">(timestamp hello è facoltativo, è possibile specificare qualsiasi stringa univoca per il nome dell'app hello).</span><span class="sxs-lookup"><span data-stu-id="f6bdf-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="f6bdf-165">Specifica l'area di destinazione hello, che in questo esempio è `westus`.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="f6bdf-166">(Un elenco completo è in hello [plug-in Maven per le app Web di Azure] documentazione.)</span><span class="sxs-lookup"><span data-stu-id="f6bdf-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="f6bdf-167">Specifica di versione di runtime Java hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="f6bdf-168">(Un elenco completo è in hello [plug-in Maven per le app Web di Azure] documentazione.)</span><span class="sxs-lookup"><span data-stu-id="f6bdf-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="f6bdf-169">Specifica il tipo di distribuzione per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="f6bdf-170">Per il momento è supportato solo `ftp`, ma è in fase di sviluppo il supporto di altri tipi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="f6bdf-171">Specifica le risorse e destinazioni Maven utilizzata quando si distribuisce il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="f6bdf-172">In questo esempio, due `<resource>` elementi specificano che Maven verrà distribuito il file JAR hello per l'applicazione web e hello *Web. config* file dal progetto di avvio Spring hello.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="f6bdf-173">Compilare e distribuire il tooAzure app web</span><span class="sxs-lookup"><span data-stu-id="f6bdf-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="f6bdf-174">Dopo aver configurato le impostazioni di hello in hello precedenti sezioni di questo articolo, si è pronti toodeploy il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="f6bdf-175">toodo in tal caso, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="f6bdf-176">Dal prompt dei comandi di hello o finestra terminale che si utilizzava in precedenza, ricompilare il file JAR hello utilizzando Maven se toohello eventuali modifiche apportate *pom.xml* file; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="f6bdf-177">Distribuire il tooAzure app web utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="f6bdf-178">Maven distribuirà tooAzure l'app web; Se l'applicazione web hello non esiste già, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="f6bdf-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="f6bdf-179">Quando è stato distribuito il web, sarà in grado di toomanage usando hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="f6bdf-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="f6bdf-180">L'app Web sarà elencata in **Servizi app**:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-180">Your web app will be listed in **App Services**:</span></span>

   ![App Web elencata in Servizi app nel portale di Azure][AP01]

* <span data-ttu-id="f6bdf-182">E hello URL per l'app web sarà elencato nel hello **Panoramica** per l'app web:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f6bdf-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6bdf-184">Next steps</span></span>

<span data-ttu-id="f6bdf-185">Per ulteriori informazioni su hello diverse tecnologie descritte in questo articolo, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="f6bdf-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="f6bdf-186">[plug-in Maven per le app Web di Azure]</span><span class="sxs-lookup"><span data-stu-id="f6bdf-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="f6bdf-187">Accedi tooAzure da hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="f6bdf-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="f6bdf-188">Come toouse hello plug-in Maven per le app Web di Azure toodeploy nei contenitori tooAzure app Spring avvio</span><span class="sxs-lookup"><span data-stu-id="f6bdf-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="f6bdf-189">Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f6bdf-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="f6bdf-190">Informazioni di riferimento sulle impostazioni di Maven</span><span class="sxs-lookup"><span data-stu-id="f6bdf-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure interfaccia della riga di comando (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portale di Azure]: https://portal.azure.com/
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring avvio Introduzione]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[plug-in Maven per le app Web di Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
