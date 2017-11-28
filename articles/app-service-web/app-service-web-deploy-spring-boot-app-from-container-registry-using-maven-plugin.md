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
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="430a4-103">Come toouse hello plug-in Maven per le app Web di Azure toodeploy un'applicazione di avvio Spring in tooAzure del Registro di sistema di Azure contenitore servizio App</span><span class="sxs-lookup"><span data-stu-id="430a4-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="430a4-104">Hello  **[Spring Framework]**  è un framework open source più diffuso che consente agli sviluppatori Java di creare applicazioni API web e dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="430a4-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="430a4-105">Questa esercitazione viene utilizzato una app di esempio creata con [avvio Spring], un approccio basato su convenzione per l'utilizzo di tooget Spring in tempi brevi.</span><span class="sxs-lookup"><span data-stu-id="430a4-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="430a4-106">In questo articolo viene illustrato come toodeploy un tooAzure di applicazione di esempio Spring avvio contenitore del Registro di sistema e quindi utilizzare hello plug-in Maven per le app Web di Azure toodeploy il tooAzure di applicazione del servizio App.</span><span class="sxs-lookup"><span data-stu-id="430a4-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="430a4-107">Hello plug-in Maven per le app Web di Azure è attualmente disponibile come anteprima.</span><span class="sxs-lookup"><span data-stu-id="430a4-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="430a4-108">Per il momento, è supportata solo la pubblicazione FTP, anche se le funzionalità aggiuntive sono pianificate per hello future.</span><span class="sxs-lookup"><span data-stu-id="430a4-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="430a4-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="430a4-109">Prerequisites</span></span>

<span data-ttu-id="430a4-110">In ordine toocomplete hello passaggi di questa esercitazione, è necessario hello toohave seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="430a4-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="430a4-111">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="430a4-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="430a4-112">Hello [Azure interfaccia della riga di comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="430a4-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="430a4-113">Java Development Kit (JDK) aggiornato, versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="430a4-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="430a4-114">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="430a4-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="430a4-115">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="430a4-115">A [Git] client.</span></span>
* <span data-ttu-id="430a4-116">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="430a4-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="430a4-117">A causa di requisiti della virtualizzazione toohello di questa esercitazione, non è possibile seguire i passaggi di hello in questo articolo in una macchina virtuale; è necessario utilizzare un computer fisico con le funzionalità di virtualizzazione abilitate.</span><span class="sxs-lookup"><span data-stu-id="430a4-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="430a4-118">Esempio di hello clone avvio molla nell'applicazione web di Docker</span><span class="sxs-lookup"><span data-stu-id="430a4-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="430a4-119">In questa sezione si clona e si testa in locale un'applicazione Spring Boot in contenitore.</span><span class="sxs-lookup"><span data-stu-id="430a4-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="430a4-120">Aprire un prompt dei comandi o una finestra terminale e creare toohold una directory locale dell'applicazione di avvio molla e spostarsi nella directory toothat; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="430a4-121">- o-</span><span class="sxs-lookup"><span data-stu-id="430a4-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="430a4-122">Hello clone [avvio molla su Docker Introduzione] progetto di esempio nella directory hello è stato creato; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="430a4-123">Cambiare il progetto completato toohello directory; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="430a4-124">Compilare i file JAR hello utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="430a4-125">Quando hello web app è stato creato, avviare l'app web hello utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="430a4-126">Testare l'app web hello esplorando tooit localmente tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="430a4-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="430a4-127">Ad esempio, è possibile utilizzare il comando seguente, se si dispone di curl disponibili hello:</span><span class="sxs-lookup"><span data-stu-id="430a4-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="430a4-128">Dovrebbe essere hello segue messaggio visualizzato: **Docker Hello World**</span><span class="sxs-lookup"><span data-stu-id="430a4-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Esplorare l'app di esempio in locale][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="430a4-130">Creare un'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="430a4-130">Create an Azure service principal</span></span>

<span data-ttu-id="430a4-131">In questa sezione si crea un Azure entità di servizio che hello utilizza plug-in di Maven quando si distribuisce il tooAzure contenitore.</span><span class="sxs-lookup"><span data-stu-id="430a4-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="430a4-132">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="430a4-132">Open a command prompt.</span></span>

1. <span data-ttu-id="430a4-133">Accesso all'account Azure tramite hello CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="430a4-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="430a4-134">Seguire hello istruzioni toocomplete hello processo di accesso.</span><span class="sxs-lookup"><span data-stu-id="430a4-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="430a4-135">Creare un'entità servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="430a4-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="430a4-136">Dove `uuuuuuuu` è il nome utente hello e `pppppppp` hello password per l'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="430a4-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="430a4-137">Azure risponde con il formato JSON che è simile a hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="430a4-137">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="430a4-138">Quando si configura toodeploy plug-in di Maven hello tooAzure il contenitore, si utilizzerà i valori hello questa risposta JSON.</span><span class="sxs-lookup"><span data-stu-id="430a4-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="430a4-139">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` sono valori segnaposto, ovvero utilizzata in questo esempio toomake toomap più facilmente questi valori tootheir rispettivi elementi quando si configura il Maven `settings.xml` file hello accanto sezione.</span><span class="sxs-lookup"><span data-stu-id="430a4-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="430a4-140">Creare un Azure contenitore del Registro di sistema utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="430a4-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="430a4-141">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="430a4-141">Open a command prompt.</span></span>

1. <span data-ttu-id="430a4-142">Accedi tooyour account di Azure:</span><span class="sxs-lookup"><span data-stu-id="430a4-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="430a4-143">Creare un gruppo di risorse per hello risorse di Azure che verrà utilizzato in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="430a4-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="430a4-144">Sostituire il valore `wingtiptoysresources` di questo esempio con un nome univoco per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="430a4-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="430a4-145">Creare un registro di sistema contenitore privato di Azure nel gruppo di risorse hello per l'app avvio molla:</span><span class="sxs-lookup"><span data-stu-id="430a4-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="430a4-146">Sostituire il valore `wingtiptoysregistry` di questo esempio con un nome univoco per il registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="430a4-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="430a4-147">Recuperare la password di hello per il Registro di sistema del contenitore:</span><span class="sxs-lookup"><span data-stu-id="430a4-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="430a4-148">Azure restituirà la password, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="430a4-149">Aggiungere impostazioni di Maven tooyour principale di servizi di Azure e del Registro di sistema di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="430a4-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="430a4-150">Aprire il Maven `settings.xml` file in un editor di testo; questo file potrebbe essere in un percorso come hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="430a4-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="430a4-151">Aggiungere le impostazioni di accesso del Registro di sistema di Azure contenitore dalla sezione precedente di hello di questo articolo di toohello `<servers>` insieme in hello *Settings* file; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="430a4-152">Dove:</span><span class="sxs-lookup"><span data-stu-id="430a4-152">Where:</span></span>
   <span data-ttu-id="430a4-153">Elemento</span><span class="sxs-lookup"><span data-stu-id="430a4-153">Element</span></span> | <span data-ttu-id="430a4-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="430a4-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="430a4-155">Contiene il nome di hello contenitore privato di Azure del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="430a4-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="430a4-156">Contiene il nome di hello contenitore privato di Azure del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="430a4-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="430a4-157">Contiene la password di hello recuperato nella sezione precedente di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="430a4-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="430a4-158">Aggiungere le impostazioni dell'entità servizio di Azure da una sezione precedente di questo articolo di toohello `<servers>` insieme in hello *Settings* file; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="430a4-159">Dove:</span><span class="sxs-lookup"><span data-stu-id="430a4-159">Where:</span></span>
   <span data-ttu-id="430a4-160">Elemento</span><span class="sxs-lookup"><span data-stu-id="430a4-160">Element</span></span> | <span data-ttu-id="430a4-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="430a4-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="430a4-162">Specifica un nome univoco utilizzato Maven toolook backup delle impostazioni di sicurezza quando si distribuisce il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="430a4-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="430a4-163">Contiene hello `appId` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="430a4-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="430a4-164">Contiene hello `tenant` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="430a4-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="430a4-165">Contiene hello `password` compreso l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="430a4-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="430a4-166">Definisce l'ambiente cloud di Azure di destinazione di hello ovvero `AZURE` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="430a4-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="430a4-167">(Un elenco completo degli ambienti è disponibile in hello [plug-in Maven per le app Web di Azure] documentazione)</span><span class="sxs-lookup"><span data-stu-id="430a4-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="430a4-168">Salvare e chiudere hello *Settings* file.</span><span class="sxs-lookup"><span data-stu-id="430a4-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="430a4-169">Compilare il Docker immagine contenitore e inviare tooyour del Registro di sistema contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="430a4-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="430a4-170">Passare directory del progetto toohello completato per l'applicazione di avvio Spring (ad esempio "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e aprire hello *pom.xml* file con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="430a4-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="430a4-171">Hello aggiornamento `<properties>` insieme in hello *pom.xml* file con valore hello di server di accesso per il Registro di sistema contenitore di Azure dalla sezione precedente di hello di questa esercitazione; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="430a4-172">Dove:</span><span class="sxs-lookup"><span data-stu-id="430a4-172">Where:</span></span>
   <span data-ttu-id="430a4-173">Elemento</span><span class="sxs-lookup"><span data-stu-id="430a4-173">Element</span></span> | <span data-ttu-id="430a4-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="430a4-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="430a4-175">Specifica il nome di hello contenitore privato di Azure del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="430a4-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="430a4-176">Specifica l'URL di hello contenitore privato di Azure del Registro di sistema, che è derivato aggiungendo ". azurecr.io" toohello nome contenitore privato del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="430a4-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="430a4-177">Verificare che `<plugin>` per plug-in Docker hello nel *pom.xml* file contiene le proprietà corrette di hello hello nome di accesso server indirizzo e del Registro di sistema dal passaggio precedente hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="430a4-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="430a4-178">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-178">For example:</span></span>

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
   <span data-ttu-id="430a4-179">Dove:</span><span class="sxs-lookup"><span data-stu-id="430a4-179">Where:</span></span>
   <span data-ttu-id="430a4-180">Elemento</span><span class="sxs-lookup"><span data-stu-id="430a4-180">Element</span></span> | <span data-ttu-id="430a4-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="430a4-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="430a4-182">Specifica la proprietà hello che contiene il nome contenitore privato di Azure del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="430a4-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="430a4-183">Specifica la proprietà hello che contiene l'URL di hello contenitore privato di Azure del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="430a4-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="430a4-184">Directory del progetto toohello completato per l'applicazione di avvio Spring passare ed eseguire seguito comando toorebuild hello applicazione hello e push hello contenitore tooyour del Registro di sistema di contenitore di Azure:</span><span class="sxs-lookup"><span data-stu-id="430a4-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="430a4-185">Facoltativo: Sfoglia toohello [portale di Azure] e verificare che sia presente l'immagine contenitore Docker denominata **docker gs-spring-avvio** nel Registro di sistema contenitore.</span><span class="sxs-lookup"><span data-stu-id="430a4-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Verificare il contenitore nel portale di Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="430a4-187">Personalizzare il pom.xml, quindi compilare e distribuire tooAzure il contenitore</span><span class="sxs-lookup"><span data-stu-id="430a4-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="430a4-188">Aprire hello `pom.xml` file per l'applicazione di avvio Spring in un editor di testo e quindi individuare hello `<plugin>` elemento per `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="430a4-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="430a4-189">Questo elemento dovrebbe essere simile a hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="430a4-189">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="430a4-190">Esistono diversi valori che è possibile modificare per plug-in di Maven hello e una descrizione dettagliata per ognuno di questi elementi è disponibile in hello [plug-in Maven per le app Web di Azure] documentazione.</span><span class="sxs-lookup"><span data-stu-id="430a4-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="430a4-191">Dopo questa premessa, in questo articolo è opportuno evidenziare diversi valori:</span><span class="sxs-lookup"><span data-stu-id="430a4-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="430a4-192">Elemento</span><span class="sxs-lookup"><span data-stu-id="430a4-192">Element</span></span> | <span data-ttu-id="430a4-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="430a4-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="430a4-194">Specifica la versione di hello di hello [plug-in Maven per le app Web di Azure].</span><span class="sxs-lookup"><span data-stu-id="430a4-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="430a4-195">Controllare versione hello elencata in hello [repository centrale Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure che si sta utilizzando hello versione più recente.</span><span class="sxs-lookup"><span data-stu-id="430a4-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="430a4-196">Specifica le informazioni di autenticazione hello per Azure, che in questo esempio contiene un `<serverId>` elemento contenente `azure-auth`; Maven utilizza tale toolook valore i valori dell'entità servizio di Azure di hello nel Maven *Settings* file, che è definito in una sezione precedente di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="430a4-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="430a4-197">Specifica il gruppo risorse destinazione hello, ovvero `wingtiptoysresources` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="430a4-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="430a4-198">verrà creato il gruppo di risorse Hello durante la distribuzione se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="430a4-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="430a4-199">Specifica il nome di destinazione hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="430a4-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="430a4-200">In questo esempio, è il nome di destinazione hello `maven-linux-app-${maven.build.timestamp}`, dove hello `${maven.build.timestamp}` suffisso viene aggiunto in questo conflitto tooavoid di esempio.</span><span class="sxs-lookup"><span data-stu-id="430a4-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="430a4-201">(timestamp hello è facoltativo, è possibile specificare qualsiasi stringa univoca per il nome dell'app hello).</span><span class="sxs-lookup"><span data-stu-id="430a4-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="430a4-202">Specifica l'area di destinazione hello, che in questo esempio è `westus`.</span><span class="sxs-lookup"><span data-stu-id="430a4-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="430a4-203">(Un elenco completo è in hello [plug-in Maven per le app Web di Azure] documentazione.)</span><span class="sxs-lookup"><span data-stu-id="430a4-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="430a4-204">Specifica le proprietà di hello contenenti hello nome e l'URL del contenitore.</span><span class="sxs-lookup"><span data-stu-id="430a4-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="430a4-205">Specifica eventuali impostazioni univoche per Maven toouse quando si distribuisce il tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="430a4-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="430a4-206">In questo esempio, un `<property>` elemento contiene una coppia nome/valore di elementi figlio che specificano la porta hello per l'app.</span><span class="sxs-lookup"><span data-stu-id="430a4-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="430a4-207">Hello impostazioni toochange hello numero di porta in questo esempio sono necessari solo quando si modifica la porta hello da predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="430a4-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="430a4-208">Dal prompt dei comandi di hello o finestra terminale che si utilizzava in precedenza, ricompilare il file JAR hello utilizzando Maven se toohello eventuali modifiche apportate *pom.xml* file; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="430a4-209">Distribuire il tooAzure app web utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="430a4-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="430a4-210">Maven distribuirà tooAzure l'app web; Se l'applicazione web hello non esiste già, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="430a4-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="430a4-211">Se area hello specificati nel hello `<region>` elemento il *pom.xml* file non è sufficiente server disponibili quando si avvia la distribuzione, è possibile visualizzare un toohello simile di errore riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="430a4-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="430a4-212">In questo caso, è possibile specificare che un'altra area ed eseguire di nuovo hello Maven comando toodeploy l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="430a4-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="430a4-213">Quando è stato distribuito il web, sarà in grado di toomanage usando hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="430a4-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="430a4-214">L'app Web sarà elencata in **Servizi app**:</span><span class="sxs-lookup"><span data-stu-id="430a4-214">Your web app will be listed in **App Services**:</span></span>

   ![App Web elencata in Servizi app nel portale di Azure][AP01]

* <span data-ttu-id="430a4-216">E hello URL per l'app web sarà elencato nel hello **Panoramica** per l'app web:</span><span class="sxs-lookup"><span data-stu-id="430a4-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Determinare l'URL di hello per le app web][AP02]

## <a name="next-steps"></a><span data-ttu-id="430a4-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="430a4-218">Next steps</span></span>

<span data-ttu-id="430a4-219">Per ulteriori informazioni su hello diverse tecnologie descritte in questo articolo, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="430a4-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="430a4-220">[plug-in Maven per le app Web di Azure]</span><span class="sxs-lookup"><span data-stu-id="430a4-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="430a4-221">Accedi tooAzure da hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="430a4-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="430a4-222">Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="430a4-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="430a4-223">Informazioni di riferimento sulle impostazioni di Maven</span><span class="sxs-lookup"><span data-stu-id="430a4-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="430a4-224">[Plug-in Docker per Maven]</span><span class="sxs-lookup"><span data-stu-id="430a4-224">[Docker plugin for Maven]</span></span>

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
