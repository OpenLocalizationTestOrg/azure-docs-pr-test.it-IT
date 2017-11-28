---
title: Come usare il plug-in Maven per App Web di Azure per distribuire un'app Spring Boot in contenitore in Azure
description: Informazioni su come usare il plug-in Maven per App Web di Azure per distribuire un'app Spring Boot in Azure.
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
ms.openlocfilehash: 883040590291cee94daa227fbc6715ad4be0b393
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="dce1f-103">Come usare il plug-in Maven per App Web di Azure per distribuire un'app Spring Boot in contenitore in Azure</span><span class="sxs-lookup"><span data-stu-id="dce1f-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="dce1f-104">Il [plug-in Maven per App Web di Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) disponibile per [Apache Maven](http://maven.apache.org/) consente una facile integrazione del servizio app di Azure nei progetti Maven e semplifica il processo con cui gli sviluppatori distribuiscono app Web nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="dce1f-104">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service .</span></span>

<span data-ttu-id="dce1f-105">Questo articolo illustra l'uso del plug-in Maven per App Web di Azure per distribuire in Servizi app di Azure un'applicazione Spring Boot di esempio in un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="dce1f-105">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="dce1f-106">Il plug-in Maven per App Web di Azure è attualmente disponibile in anteprima.</span><span class="sxs-lookup"><span data-stu-id="dce1f-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="dce1f-107">Per il momento è supportata solo la pubblicazione FTP, ma sono previste in futuro funzionalità aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="dce1f-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="dce1f-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dce1f-108">Prerequisites</span></span>

<span data-ttu-id="dce1f-109">Per completare la procedura di questa esercitazione, sono necessari i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dce1f-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="dce1f-110">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="dce1f-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="dce1f-111">[Interfaccia della riga di comando di Azure].</span><span class="sxs-lookup"><span data-stu-id="dce1f-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="dce1f-112">Java Development Kit (JDK) aggiornato, versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="dce1f-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="dce1f-113">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="dce1f-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="dce1f-114">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="dce1f-114">A [Git] client.</span></span>
* <span data-ttu-id="dce1f-115">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="dce1f-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="dce1f-116">A causa dei requisiti di virtualizzazione di questa esercitazione, non è possibile seguire la procedura illustrata in questo articolo in una macchina virtuale. È necessario usare un computer fisico in cui sono abilitate le funzionalità di virtualizzazione.</span><span class="sxs-lookup"><span data-stu-id="dce1f-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="dce1f-117">Clonare l'app Web Spring Boot in Docker di esempio</span><span class="sxs-lookup"><span data-stu-id="dce1f-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="dce1f-118">In questa sezione si clona e si testa in locale un'applicazione Spring Boot in contenitore.</span><span class="sxs-lookup"><span data-stu-id="dce1f-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="dce1f-119">Aprire un prompt dei comandi o una finestra del terminale e creare una directory locale in cui salvare l'applicazione Spring Boot, quindi passare a tale directory. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dce1f-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="dce1f-120">- o-</span><span class="sxs-lookup"><span data-stu-id="dce1f-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="dce1f-121">Clonare il progetto di esempio [Spring Boot on Docker Getting Started] (Introduzione a Spring Boot in Docker) nella directory appena creata, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dce1f-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="dce1f-122">Passare alla directory del progetto completato. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dce1f-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="dce1f-123">Compilare il file JAR usando Maven. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dce1f-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="dce1f-124">Dopo che è stata creata, avviare l'app Web con Maven, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dce1f-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="dce1f-125">Testare l'app Web esplorandola localmente tramite un Web browser.</span><span class="sxs-lookup"><span data-stu-id="dce1f-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="dce1f-126">Se è disponibile curl, ad esempio, è possibile usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dce1f-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="dce1f-127">Dovrebbe essere visualizzato il messaggio seguente: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="dce1f-127">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="dce1f-128">Creare un'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="dce1f-128">Create an Azure service principal</span></span>

<span data-ttu-id="dce1f-129">In questa sezione si crea un'entità servizio di Azure che verrà usata dal plug-in Maven durante la distribuzione del contenitore in Azure.</span><span class="sxs-lookup"><span data-stu-id="dce1f-129">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="dce1f-130">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="dce1f-130">Open a command prompt.</span></span>

1. <span data-ttu-id="dce1f-131">Accedere all'account Azure con l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="dce1f-131">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="dce1f-132">Seguire le istruzioni per completare il processo di accesso.</span><span class="sxs-lookup"><span data-stu-id="dce1f-132">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="dce1f-133">Creare un'entità servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="dce1f-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="dce1f-134">`uuuuuuuu` è il nome utente e `pppppppp` è la password dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="dce1f-134">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="dce1f-135">Azure restituisce una risposta JSON simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="dce1f-135">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="dce1f-136">I valori di questa risposta JSON verranno usati durante la configurazione del plug-in Maven per la distribuzione del contenitore in Azure.</span><span class="sxs-lookup"><span data-stu-id="dce1f-136">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="dce1f-137">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` e `tttttttt` sono segnaposto che vengono usati in questo esempio per facilitare il mapping di questi valori ai rispettivi elementi durante la configurazione del file `settings.xml` di Maven nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="dce1f-137">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="dce1f-138">Configurare Maven per l'uso dell'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="dce1f-138">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="dce1f-139">In questa sezione si usano i valori dell'entità servizio di Azure per configurare l'autenticazione che verrà usata da Maven durante la distribuzione del contenitore in Azure.</span><span class="sxs-lookup"><span data-stu-id="dce1f-139">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="dce1f-140">Aprire il file `settings.xml` di Maven in un editor di testo. Il file potrebbe trovarsi in un percorso come quelli riportati negli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dce1f-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="dce1f-141">Aggiungere le impostazioni dell'entità servizio di Azure della sezione precedente di questa esercitazione alla raccolta `<servers>` nel file *settings.xml*. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dce1f-141">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="dce1f-142">Dove:</span><span class="sxs-lookup"><span data-stu-id="dce1f-142">Where:</span></span>
   <span data-ttu-id="dce1f-143">Elemento</span><span class="sxs-lookup"><span data-stu-id="dce1f-143">Element</span></span> | <span data-ttu-id="dce1f-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dce1f-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="dce1f-145">Specifica un nome univoco che viene usato da Maven per cercare le impostazioni di sicurezza quando si distribuisce l'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="dce1f-145">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="dce1f-146">Contiene il valore `appId` dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="dce1f-146">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="dce1f-147">Contiene il valore `tenant` dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="dce1f-147">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="dce1f-148">Contiene il valore `password` dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="dce1f-148">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="dce1f-149">Definisce l'ambiente cloud di Azure di destinazione, che in questo esempio è `AZURE`.</span><span class="sxs-lookup"><span data-stu-id="dce1f-149">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="dce1f-150">Un elenco completo degli ambienti è disponibile nella documentazione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="dce1f-150">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="dce1f-151">Salvare e chiudere il file *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="dce1f-151">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="dce1f-152">FACOLTATIVO: distribuire il file Docker locale nell'hub Docker</span><span class="sxs-lookup"><span data-stu-id="dce1f-152">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="dce1f-153">Se si ha un account Docker, è possibile compilare l'immagine del contenitore Docker in locale ed eseguirne il push nell'hub Docker.</span><span class="sxs-lookup"><span data-stu-id="dce1f-153">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="dce1f-154">A tale scopo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="dce1f-154">To do so, use the following steps.</span></span>

1. <span data-ttu-id="dce1f-155">Aprire il file `pom.xml` per l'applicazione Spring Boot in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="dce1f-155">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="dce1f-156">Individuare l'elemento figlio `<imageName>` nell'elemento `<containerSettings>`.</span><span class="sxs-lookup"><span data-stu-id="dce1f-156">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="dce1f-157">Aggiornare il valore `${docker.image.prefix}` con il nome dell'account Docker:</span><span class="sxs-lookup"><span data-stu-id="dce1f-157">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="dce1f-158">Scegliere uno dei metodi di distribuzione seguenti.</span><span class="sxs-lookup"><span data-stu-id="dce1f-158">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="dce1f-159">Compilare l'immagine del contenitore in locale con Maven e quindi usare Docker per eseguire il push del contenitore nell'hub Docker:</span><span class="sxs-lookup"><span data-stu-id="dce1f-159">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="dce1f-160">Se è installato il [plug-in Docker per Maven], è possibile compilare automaticamente l'immagine del contenitore nell'hub Docker usando il parametro `-DpushImage`:</span><span class="sxs-lookup"><span data-stu-id="dce1f-160">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="dce1f-161">FACOLTATIVO: personalizzare pom.xml prima della distribuzione del contenitore in Azure</span><span class="sxs-lookup"><span data-stu-id="dce1f-161">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="dce1f-162">Aprire il file `pom.xml` per l'applicazione Spring Boot in un editor di testo e quindi individuare l'elemento `<plugin>` per `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="dce1f-162">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="dce1f-163">L'elemento dovrebbe essere simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="dce1f-163">This element should resemble the following example:</span></span>

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

<span data-ttu-id="dce1f-164">È possibile modificare diversi valori per il plug-in Maven. Una descrizione dettagliata di ognuno di questi elementi è disponibile nella documentazione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="dce1f-164">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="dce1f-165">Dopo questa premessa, in questo articolo è opportuno evidenziare diversi valori:</span><span class="sxs-lookup"><span data-stu-id="dce1f-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="dce1f-166">Elemento</span><span class="sxs-lookup"><span data-stu-id="dce1f-166">Element</span></span> | <span data-ttu-id="dce1f-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dce1f-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="dce1f-168">Specifica la versione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="dce1f-168">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="dce1f-169">È consigliabile controllare la versione riportata nel [repository centrale Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) per assicurarsi di usare l'ultima versione.</span><span class="sxs-lookup"><span data-stu-id="dce1f-169">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="dce1f-170">Specifica le informazioni di autenticazione per Azure, che in questo esempio includono un elemento `<serverId>` contenente `azure-auth`. Maven usa questo valore per cercare i valori dell'entità servizio di Azure nel file *settings.xml* di Maven, in base a quanto definito in una sezione precedente di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="dce1f-170">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="dce1f-171">Specifica il gruppo di risorse di destinazione, che in questo esempio è `maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="dce1f-171">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="dce1f-172">Se non esiste già, questo gruppo di risorse verrà creato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dce1f-172">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="dce1f-173">Specifica il nome di destinazione dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="dce1f-173">Specifies the target name for your web app.</span></span> <span data-ttu-id="dce1f-174">In questo esempio, il nome di destinazione è `maven-linux-app-${maven.build.timestamp}` e il suffisso `${maven.build.timestamp}` viene accodato per evitare conflitti.</span><span class="sxs-lookup"><span data-stu-id="dce1f-174">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="dce1f-175">Il timestamp è facoltativo. Come nome dell'app è possibile specificare qualsiasi stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="dce1f-175">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="dce1f-176">Specifica l'area di destinazione, che in questo esempio è `westus`.</span><span class="sxs-lookup"><span data-stu-id="dce1f-176">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="dce1f-177">Un elenco completo è disponibile nella documentazione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="dce1f-177">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="dce1f-178">Specifica qualsiasi impostazione univoca che dovrà essere usata da Maven durante la distribuzione dell'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="dce1f-178">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="dce1f-179">In questo esempio, un elemento `<property>` contiene una coppia nome-valore di elementi figlio che specificano la porta dell'app.</span><span class="sxs-lookup"><span data-stu-id="dce1f-179">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="dce1f-180">Le impostazioni per modificare il numero di porta in questo esempio sono necessarie solo in caso di modifica della porta rispetto all'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dce1f-180">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="dce1f-181">Compilare e distribuire il contenitore in Azure</span><span class="sxs-lookup"><span data-stu-id="dce1f-181">Build and deploy your container to Azure</span></span>

<span data-ttu-id="dce1f-182">Dopo aver configurato tutte le impostazioni nelle sezioni precedenti di questo articolo, è possibile distribuire il contenitore in Azure.</span><span class="sxs-lookup"><span data-stu-id="dce1f-182">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="dce1f-183">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dce1f-183">To do so, use the following steps:</span></span>

1. <span data-ttu-id="dce1f-184">Se sono state apportate modifiche al file *pom.xml*, dalla finestra del terminale o al prompt dei comandi usato in precedenza ricompilare il file JAR usando Maven. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dce1f-184">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="dce1f-185">Distribuire l'app Web in Azure usando Maven. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dce1f-185">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="dce1f-186">Maven distribuirà l'app Web in Azure. Se l'app Web non esiste già, verrà creata.</span><span class="sxs-lookup"><span data-stu-id="dce1f-186">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="dce1f-187">Se nell'area specificata nell'elemento `<region>` del file *pom.xml* non sono disponibili server sufficienti quando si avvia la distribuzione, potrebbe essere visualizzato un errore simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="dce1f-187">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="dce1f-188">In questo caso, è possibile specificare un'altra area e rieseguire il comando Maven per distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dce1f-188">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="dce1f-189">Dopo che è stata distribuita, l'app Web potrà essere gestita usando il [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="dce1f-189">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="dce1f-190">L'app Web sarà elencata in **Servizi app**:</span><span class="sxs-lookup"><span data-stu-id="dce1f-190">Your web app will be listed in **App Services**:</span></span>

   ![App Web elencata in Servizi app nel portale di Azure][AP01]

* <span data-ttu-id="dce1f-192">L'URL dell'app Web sarà riportato nella **panoramica** dell'app Web:</span><span class="sxs-lookup"><span data-stu-id="dce1f-192">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Individuazione dell'URL dell'app Web][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="dce1f-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dce1f-194">Next steps</span></span>

<span data-ttu-id="dce1f-195">Per altre informazioni sulle varie tecnologie illustrate in questo articolo, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="dce1f-195">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="dce1f-196">[plug-in Maven per App Web di Azure]</span><span class="sxs-lookup"><span data-stu-id="dce1f-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="dce1f-197">Accedere ad Azure dall'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="dce1f-197">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="dce1f-198">Come usare il plug-in Maven per App Web di Azure per distribuire un'app Spring Boot nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="dce1f-198">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="dce1f-199">Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dce1f-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="dce1f-200">Informazioni di riferimento sulle impostazioni di Maven</span><span class="sxs-lookup"><span data-stu-id="dce1f-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="dce1f-201">[plug-in Docker per Maven]</span><span class="sxs-lookup"><span data-stu-id="dce1f-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

<span data-ttu-id="dce1f-202">[Interfaccia della riga di comando di Azure]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="dce1f-202">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="dce1f-203">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="dce1f-203">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="dce1f-204">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="dce1f-204">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="dce1f-205">[plug-in Docker per Maven]: https://github.com/spotify/docker-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="dce1f-205">[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin</span></span>
<span data-ttu-id="dce1f-206">[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="dce1f-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="dce1f-207">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="dce1f-207">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="dce1f-208">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="dce1f-208">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="dce1f-209">[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="dce1f-209">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
[Spring Boot]: http://projects.spring.io/spring-boot/
<span data-ttu-id="dce1f-210">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Introduzione a Spring Boot in Docker)</span><span class="sxs-lookup"><span data-stu-id="dce1f-210">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
[Spring Framework]: https://spring.io/
<span data-ttu-id="dce1f-211">[plug-in Maven per App Web di Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="dce1f-211">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
