---
title: Come usare il plug-in Maven per App Web di Azure per distribuire un'app Spring Boot in Azure
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
ms.openlocfilehash: dceb7edf788bd87b1de04aa435a12cd5853755b9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-to-azure"></a><span data-ttu-id="b37a4-103">Come usare il plug-in Maven per App Web di Azure per distribuire un'app Spring Boot in Azure</span><span class="sxs-lookup"><span data-stu-id="b37a4-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure</span></span>

<span data-ttu-id="b37a4-104">Il [plug-in Maven per App Web di Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) disponibile per [Apache Maven](http://maven.apache.org/) consente una facile integrazione del servizio app di Azure nei progetti Maven e semplifica il processo con cui gli sviluppatori distribuiscono app Web nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a4-104">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="b37a4-105">Questo articolo illustra l'uso del plug-in Maven per App Web di Azure per distribuire un'applicazione Spring Boot di esempio in Servizi app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a4-105">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b37a4-106">Il plug-in Maven per App Web di Azure è attualmente disponibile in anteprima.</span><span class="sxs-lookup"><span data-stu-id="b37a4-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="b37a4-107">Per il momento è supportata solo la pubblicazione FTP, ma sono previste in futuro funzionalità aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="b37a4-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="b37a4-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b37a4-108">Prerequisites</span></span>

<span data-ttu-id="b37a4-109">Per completare la procedura di questa esercitazione, sono necessari i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b37a4-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="b37a4-110">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="b37a4-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b37a4-111">[Interfaccia della riga di comando di Azure].</span><span class="sxs-lookup"><span data-stu-id="b37a4-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="b37a4-112">Java Development Kit (JDK) aggiornato, versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b37a4-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="b37a4-113">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="b37a4-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="b37a4-114">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="b37a4-114">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="b37a4-115">Clonare l'app Web Spring Boot di esempio</span><span class="sxs-lookup"><span data-stu-id="b37a4-115">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="b37a4-116">In questa sezione si clona e si testa in locale un'applicazione Spring Boot completata.</span><span class="sxs-lookup"><span data-stu-id="b37a4-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="b37a4-117">Aprire un prompt dei comandi o una finestra del terminale e creare una directory locale in cui salvare l'applicazione Spring Boot, quindi passare a tale directory. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b37a4-117">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="b37a4-118">- o-</span><span class="sxs-lookup"><span data-stu-id="b37a4-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="b37a4-119">Clonare il progetto di esempio di [introduzione a Spring Boot] nella directory creata, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b37a4-119">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="b37a4-120">Passare alla directory del progetto completato. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b37a4-120">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="b37a4-121">Compilare il file JAR usando Maven. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b37a4-121">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="b37a4-122">Dopo che è stata creata, avviare l'app Web con Maven, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b37a4-122">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="b37a4-123">Testare l'app Web esplorandola localmente tramite un Web browser.</span><span class="sxs-lookup"><span data-stu-id="b37a4-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="b37a4-124">Se è disponibile curl, ad esempio, è possibile usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b37a4-124">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="b37a4-125">Si dovrebbe visualizzare il messaggio seguente: **Greetings from Spring Boot!** (Benvenuti in Spring Boot!)</span><span class="sxs-lookup"><span data-stu-id="b37a4-125">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="b37a4-126">Creare un'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="b37a4-126">Create an Azure service principal</span></span>

<span data-ttu-id="b37a4-127">In questa sezione si crea un'entità servizio di Azure che verrà usata dal plug-in Maven durante la distribuzione dell'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a4-127">In this section, you create an Azure service principal that the Maven plugin uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="b37a4-128">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b37a4-128">Open a command prompt.</span></span>

1. <span data-ttu-id="b37a4-129">Accedere all'account Azure con l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="b37a4-129">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="b37a4-130">Seguire le istruzioni per completare il processo di accesso.</span><span class="sxs-lookup"><span data-stu-id="b37a4-130">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="b37a4-131">Creare un'entità servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="b37a4-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="b37a4-132">`uuuuuuuu` è il nome utente e `pppppppp` è la password dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b37a4-132">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="b37a4-133">Azure restituisce una risposta JSON simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b37a4-133">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="b37a4-134">I valori di questa risposta JSON verranno usati durante la configurazione del plug-in Maven per la distribuzione dell'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a4-134">You will use the values from this JSON response when you configure the Maven plugin to deploy your web app to Azure.</span></span> <span data-ttu-id="b37a4-135">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` e `tttttttt` sono segnaposto che vengono usati in questo esempio per facilitare il mapping di questi valori ai rispettivi elementi durante la configurazione del file `settings.xml` di Maven nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="b37a4-135">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="b37a4-136">Configurare Maven per l'uso dell'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="b37a4-136">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="b37a4-137">In questa sezione si usano i valori dell'entità servizio di Azure per configurare l'autenticazione che verrà usata da Maven durante la distribuzione dell'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a4-137">In this section, you use the values from your Azure service principal to configure the authentication that Maven uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="b37a4-138">Aprire il file `settings.xml` di Maven in un editor di testo. Il file potrebbe trovarsi in un percorso come quelli riportati negli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b37a4-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="b37a4-139">Aggiungere le impostazioni dell'entità servizio di Azure della sezione precedente di questa esercitazione alla raccolta `<servers>` nel file *settings.xml*. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b37a4-139">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="b37a4-140">Dove:</span><span class="sxs-lookup"><span data-stu-id="b37a4-140">Where:</span></span>
   <span data-ttu-id="b37a4-141">Elemento</span><span class="sxs-lookup"><span data-stu-id="b37a4-141">Element</span></span> | <span data-ttu-id="b37a4-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b37a4-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="b37a4-143">Specifica un nome univoco che viene usato da Maven per cercare le impostazioni di sicurezza quando si distribuisce l'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a4-143">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="b37a4-144">Contiene il valore `appId` dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b37a4-144">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="b37a4-145">Contiene il valore `tenant` dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b37a4-145">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="b37a4-146">Contiene il valore `password` dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b37a4-146">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="b37a4-147">Definisce l'ambiente cloud di Azure di destinazione, che in questo esempio è `AZURE`.</span><span class="sxs-lookup"><span data-stu-id="b37a4-147">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="b37a4-148">Un elenco completo degli ambienti è disponibile nella documentazione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="b37a4-148">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="b37a4-149">Salvare e chiudere il file *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="b37a4-149">Save and close the *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a><span data-ttu-id="b37a4-150">FACOLTATIVO: personalizzare pom.xml prima della distribuzione dell'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="b37a4-150">OPTIONAL: Customize your pom.xml before deploying your web app to Azure</span></span>

<span data-ttu-id="b37a4-151">Aprire il file `pom.xml` per l'applicazione Spring Boot in un editor di testo e quindi individuare l'elemento `<plugin>` per `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="b37a4-151">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="b37a4-152">L'elemento dovrebbe essere simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b37a4-152">This element should resemble the following example:</span></span>

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

<span data-ttu-id="b37a4-153">È possibile modificare diversi valori per il plug-in Maven. Una descrizione dettagliata di ognuno di questi elementi è disponibile nella documentazione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="b37a4-153">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="b37a4-154">Dopo questa premessa, in questo articolo è opportuno evidenziare diversi valori:</span><span class="sxs-lookup"><span data-stu-id="b37a4-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="b37a4-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="b37a4-155">Element</span></span> | <span data-ttu-id="b37a4-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b37a4-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="b37a4-157">Specifica la versione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="b37a4-157">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="b37a4-158">È consigliabile controllare la versione riportata nel [repository centrale Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) per assicurarsi di usare l'ultima versione.</span><span class="sxs-lookup"><span data-stu-id="b37a4-158">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="b37a4-159">Specifica le informazioni di autenticazione per Azure, che in questo esempio includono un elemento `<serverId>` contenente `azure-auth`. Maven usa questo valore per cercare i valori dell'entità servizio di Azure nel file *settings.xml* di Maven, in base a quanto definito in una sezione precedente di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b37a4-159">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="b37a4-160">Specifica il gruppo di risorse di destinazione, che in questo esempio è `maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="b37a4-160">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="b37a4-161">Se non esiste già, questo gruppo di risorse viene creato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b37a4-161">The resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="b37a4-162">Specifica il nome di destinazione dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="b37a4-162">Specifies the target name for your web app.</span></span> <span data-ttu-id="b37a4-163">In questo esempio, il nome di destinazione è `maven-web-app-${maven.build.timestamp}` e il suffisso `${maven.build.timestamp}` viene accodato per evitare conflitti.</span><span class="sxs-lookup"><span data-stu-id="b37a4-163">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="b37a4-164">Il timestamp è facoltativo. Come nome dell'app è possibile specificare qualsiasi stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="b37a4-164">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="b37a4-165">Specifica l'area di destinazione, che in questo esempio è `westus`.</span><span class="sxs-lookup"><span data-stu-id="b37a4-165">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="b37a4-166">Un elenco completo è disponibile nella documentazione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="b37a4-166">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="b37a4-167">Specifica la versione del runtime Java per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="b37a4-167">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="b37a4-168">Un elenco completo è disponibile nella documentazione del [plug-in Maven per App Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="b37a4-168">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="b37a4-169">Specifica il tipo di distribuzione per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="b37a4-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="b37a4-170">Per il momento è supportato solo `ftp`, ma è in fase di sviluppo il supporto di altri tipi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b37a4-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="b37a4-171">Specifica le risorse e le destinazioni che verranno usate da Maven durante la distribuzione dell'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a4-171">Specifies resources and target destinations which Maven uses when deploying your web app to Azure.</span></span> <span data-ttu-id="b37a4-172">In questo esempio, due elementi `<resource>` specificano che Maven distribuirà il file JAR per l'app Web e il file *web.config* del progetto Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="b37a4-172">In this example, two `<resource>` elements specify that Maven will deploy the JAR file for your web app and the *web.config* file from the Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="b37a4-173">Compilare e distribuire l'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="b37a4-173">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="b37a4-174">Dopo aver configurato tutte le impostazioni nelle sezioni precedenti di questo articolo, è possibile distribuire l'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="b37a4-174">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="b37a4-175">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b37a4-175">To do so, use the following steps:</span></span>

1. <span data-ttu-id="b37a4-176">Se sono state apportate modifiche al file *pom.xml*, dalla finestra del terminale o al prompt dei comandi usato in precedenza ricompilare il file JAR usando Maven. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b37a4-176">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="b37a4-177">Distribuire l'app Web in Azure usando Maven. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b37a4-177">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="b37a4-178">Maven distribuirà l'app Web in Azure. Se l'app Web non esiste già, verrà creata.</span><span class="sxs-lookup"><span data-stu-id="b37a4-178">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="b37a4-179">Dopo che è stata distribuita, l'app Web potrà essere gestita usando il [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="b37a4-179">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="b37a4-180">L'app Web sarà elencata in **Servizi app**:</span><span class="sxs-lookup"><span data-stu-id="b37a4-180">Your web app will be listed in **App Services**:</span></span>

   ![App Web elencata in Servizi app nel portale di Azure][AP01]

* <span data-ttu-id="b37a4-182">L'URL dell'app Web sarà riportato nella **panoramica** dell'app Web:</span><span class="sxs-lookup"><span data-stu-id="b37a4-182">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b37a4-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b37a4-184">Next steps</span></span>

<span data-ttu-id="b37a4-185">Per altre informazioni sulle varie tecnologie illustrate in questo articolo, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="b37a4-185">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="b37a4-186">[plug-in Maven per App Web di Azure]</span><span class="sxs-lookup"><span data-stu-id="b37a4-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="b37a4-187">Accedere ad Azure dall'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b37a4-187">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="b37a4-188">Come usare il plug-in Maven per App Web di Azure per distribuire un'app Spring Boot in contenitore in Azure</span><span class="sxs-lookup"><span data-stu-id="b37a4-188">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="b37a4-189">Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b37a4-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="b37a4-190">Informazioni di riferimento sulle impostazioni di Maven</span><span class="sxs-lookup"><span data-stu-id="b37a4-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

<span data-ttu-id="b37a4-191">[Interfaccia della riga di comando di Azure]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="b37a4-191">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="b37a4-192">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b37a4-192">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="b37a4-193">[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="b37a4-193">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="b37a4-194">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="b37a4-194">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="b37a4-195">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="b37a4-195">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="b37a4-196">[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="b37a4-196">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
[Spring Boot]: http://projects.spring.io/spring-boot/
<span data-ttu-id="b37a4-197">[introduzione a Spring Boot]: https://github.com/microsoft/gs-spring-boot</span><span class="sxs-lookup"><span data-stu-id="b37a4-197">[Spring Boot Getting Started]: https://github.com/microsoft/gs-spring-boot</span></span>
[Spring Framework]: https://spring.io/
<span data-ttu-id="b37a4-198">[plug-in Maven per App Web di Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="b37a4-198">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
