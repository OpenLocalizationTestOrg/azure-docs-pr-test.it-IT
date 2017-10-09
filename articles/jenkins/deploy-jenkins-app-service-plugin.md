---
title: aaaDeploy tooAzure servizio App con Jenkins Plugin | Documenti Microsoft
description: Informazioni su come toodeploy di plug-in Azure App Service Jenkins toouse un Java web app tooAzure in Jenkins
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="855fd-103">Distribuire tooAzure servizio App con plug-in di Jenkins</span><span class="sxs-lookup"><span data-stu-id="855fd-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="855fd-104">toodeploy un tooAzure di app web Java, è possibile utilizzare l'interfaccia CLI di Azure in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) alternativa, è possibile utilizzare di hello [plug-in Azure App Service Jenkins](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="855fd-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="855fd-105">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="855fd-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="855fd-106">Configurare Jenkins toodeploy tooAzure servizio App tramite FTP</span><span class="sxs-lookup"><span data-stu-id="855fd-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="855fd-107">Configurare Jenkins toodeploy tooAzure servizio App in Linux con Docker</span><span class="sxs-lookup"><span data-stu-id="855fd-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="855fd-108">Creare e configurare un'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="855fd-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="855fd-109">Se si dispone già di un master Jenkins, iniziare con hello [modello di soluzione](install-jenkins-solution-template.md), che include JDK8 e hello seguendo i plug-in obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="855fd-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="855fd-110">[Plug-in Git client Jenkins](https://plugins.jenkins.io/git-client) 2.4.6</span><span class="sxs-lookup"><span data-stu-id="855fd-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="855fd-111">[Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) 1.4.0</span><span class="sxs-lookup"><span data-stu-id="855fd-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="855fd-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) 1.2</span><span class="sxs-lookup"><span data-stu-id="855fd-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="855fd-113">[Servizio app di Azure](https://plugins.jenkins.io/azure-app-server) versione 0.1</span><span class="sxs-lookup"><span data-stu-id="855fd-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="855fd-114">È possibile utilizzare hello toodeploy plug-in servizio App App Web in tutti i linguaggi (ad esempio, c#, PHP, Java e node.js e così via) supportato dal servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="855fd-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="855fd-115">In questa esercitazione, si sta usando app Java di esempio hello, [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="855fd-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="855fd-116">toofork hello repository tooyour proprietari di account GitHub, fare clic su hello **Fork** pulsante nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="855fd-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="855fd-117">Sono necessari per la compilazione progetto Java hello Java JDK e Maven.</span><span class="sxs-lookup"><span data-stu-id="855fd-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="855fd-118">Assicurarsi di che installare i componenti di hello nel database master di Jenkins hello o agente VM hello se si utilizza uno per l'integrazione continua.</span><span class="sxs-lookup"><span data-stu-id="855fd-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="855fd-119">tooinstall, di log nell'istanza di Jenkins toohello tramite SSH ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="855fd-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="855fd-120">Per la distribuzione tooApp servizio su Linux, è necessario anche tooinstall Docker nello schema di Jenkins hello o agente VM hello utilizzato per la compilazione.</span><span class="sxs-lookup"><span data-stu-id="855fd-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="855fd-121">Vedere l'articolo di toothis tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="855fd-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="855fd-122">Aggiungere credenziali tooJenkins dell'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="855fd-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="855fd-123">Un'entità servizio di Azure è tooAzure toodeploy necessari.</span><span class="sxs-lookup"><span data-stu-id="855fd-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="855fd-124">Utilizzare [CLI di Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) o [portale di Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate un'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="855fd-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="855fd-125">Nel dashboard di Jenkins hello, fare clic su **credenziali -> sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="855fd-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="855fd-126">Fare clic su **Global credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="855fd-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="855fd-127">Fare clic su **Aggiungi credenziali** tooadd un'entità servizio di Microsoft Azure compilando hello ID sottoscrizione, l'ID Client, segreto Client ed Endpoint Token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="855fd-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="855fd-128">Indicare un ID, **mySp**, per l'uso nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="855fd-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="855fd-129">Plug-in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="855fd-129">Azure App Service plugin</span></span>

<span data-ttu-id="855fd-130">Versione 1.0 di plug-in Azure App Service supporta la distribuzione continua tooAzure App Web tramite:</span><span class="sxs-lookup"><span data-stu-id="855fd-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="855fd-131">GIT e FTP</span><span class="sxs-lookup"><span data-stu-id="855fd-131">Git and FTP</span></span>
* <span data-ttu-id="855fd-132">Docker per App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="855fd-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="855fd-133">Configurare Jenkins toodeploy App Web tramite FTP tramite il dashboard di Jenkins hello</span><span class="sxs-lookup"><span data-stu-id="855fd-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="855fd-134">toodeploy il tooAzure di project Web App, è possibile caricare gli artefatti di compilazione (ad esempio, file .war in Java) utilizzando Git o FTP.</span><span class="sxs-lookup"><span data-stu-id="855fd-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="855fd-135">Prima di configurare il processo di hello in Jenkins, è necessario un piano di servizio App di Azure e un'App Web per app Java di hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="855fd-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="855fd-136">Creare un piano di servizio App di Azure con hello **libero** tariffario utilizzando hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando CLI.</span><span class="sxs-lookup"><span data-stu-id="855fd-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="855fd-137">piano di servizio App Hello definisce hello risorse fisiche utilizzate toohost app.</span><span class="sxs-lookup"><span data-stu-id="855fd-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="855fd-138">Tutte le applicazioni assegnate piano di servizio App tooan condividono tali risorse, consentendo di costo toosave quando si ospitano più applicazioni.</span><span class="sxs-lookup"><span data-stu-id="855fd-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="855fd-139">Creare un'app Web.</span><span class="sxs-lookup"><span data-stu-id="855fd-139">Create a Web App.</span></span> <span data-ttu-id="855fd-140">È possibile l'uso hello [portale di Azure](/azure/app-service-web/web-sites-configure) o utilizzare hello successivo comando CLI Az:</span><span class="sxs-lookup"><span data-stu-id="855fd-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="855fd-141">Assicurarsi di impostare la configurazione di runtime Java hello necessari all'app.</span><span class="sxs-lookup"><span data-stu-id="855fd-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="855fd-142">Hello comando CLI di Azure seguente configura hello web app toorun in una versione recente di Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="855fd-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="855fd-143">Consente di impostare il processo di Jenkins hello</span><span class="sxs-lookup"><span data-stu-id="855fd-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="855fd-144">Creare un nuovo progetto **freestyle** nel dashboard di Jenkins</span><span class="sxs-lookup"><span data-stu-id="855fd-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="855fd-145">Configurare **gestione del codice sorgente** toouse nel fork locale di [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample) fornendo hello **URL del Repository**.</span><span class="sxs-lookup"><span data-stu-id="855fd-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="855fd-146">Ad esempio: http://github.com/&lt;yourID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="855fd-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="855fd-147">Aggiungere un progetto di hello toobuild passaggio di compilazione Maven utilizzando.</span><span class="sxs-lookup"><span data-stu-id="855fd-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="855fd-148">A tale scopo aggiungere un **Execute shell**.</span><span class="sxs-lookup"><span data-stu-id="855fd-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="855fd-149">Per questo esempio, è necessario un file di *.war passaggio aggiuntivo toorename hello in tooROOT.war cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="855fd-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="855fd-150">Aggiungere un'azione post-compilazione selezionando **Publish an Azure Web App** (Pubblica un'App Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="855fd-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="855fd-151">Alimentatore, "mySp" hello Azure SPN archiviati al passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="855fd-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="855fd-152">In **configurazione delle App** , scegliere l'app web e il gruppo di risorse hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="855fd-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="855fd-153">plug-in Hello rileva automaticamente se hello App Web è Windows o basata su Linux.</span><span class="sxs-lookup"><span data-stu-id="855fd-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="855fd-154">Per un'App Web basati su Windows, viene visualizzata l'opzione hello "Pubblica file".</span><span class="sxs-lookup"><span data-stu-id="855fd-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="855fd-155">Inserire nel file hello desiderato toodeploy (ad esempio, un war pacchetto se si usa Java.) La directory di origine e quella di destinazione sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="855fd-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="855fd-156">i parametri di Hello consentono di cartelle di origine e destinazione toospecify durante il caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="855fd-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="855fd-157">L'app Web Java in Azure viene eseguita in un server Tomcat.</span><span class="sxs-lookup"><span data-stu-id="855fd-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="855fd-158">Si carica il pacchetto war nella cartella webapps.</span><span class="sxs-lookup"><span data-stu-id="855fd-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="855fd-159">Per questo esempio, impostare **Directory di origine** troppo "target" e specificare "webapps" **Directory di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="855fd-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="855fd-160">Se si desidera toodeploy tooa slot diverso da produzione, è inoltre possibile impostare **Slot** nome.</span><span class="sxs-lookup"><span data-stu-id="855fd-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="855fd-161">Salvare il progetto hello e compilarlo.</span><span class="sxs-lookup"><span data-stu-id="855fd-161">Save hello project and build it.</span></span> <span data-ttu-id="855fd-162">L'app web è distribuito tooAzure al completamento.</span><span class="sxs-lookup"><span data-stu-id="855fd-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="855fd-163">Distribuire l'app Web tramite FTP usando la pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="855fd-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="855fd-164">plug-in di Hello è pronto per pipeline.</span><span class="sxs-lookup"><span data-stu-id="855fd-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="855fd-165">È possibile fare riferimento a esempio tooa nel repository GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="855fd-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="855fd-166">Nell'interfaccia utente Web di GitHub aprire il file **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="855fd-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="855fd-167">Fare clic su hello matita icona tooedit il gruppo di risorse di file tooupdate hello e il nome dell'app web sulla riga 11 e 12 rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="855fd-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="855fd-168">Modificare l'ID di riga tooupdate 14 credenziale nell'istanza di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="855fd-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="855fd-169">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="855fd-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="855fd-170">Aprire Jenkins in un Web browser, fare clic su **New Item**.</span><span class="sxs-lookup"><span data-stu-id="855fd-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="855fd-171">Specificare un nome per il processo di hello e selezionare **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="855fd-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="855fd-172">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="855fd-172">Click **OK**.</span></span>
3. <span data-ttu-id="855fd-173">Fare clic su hello **Pipeline** scheda accanto.</span><span class="sxs-lookup"><span data-stu-id="855fd-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="855fd-174">Per **Definition** selezionare **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="855fd-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="855fd-175">Per **SCM** selezionare **Git**.</span><span class="sxs-lookup"><span data-stu-id="855fd-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="855fd-176">Immettere hello GitHub URL per il repository con fork: https:&lt;repository di scenari > GIT</span><span class="sxs-lookup"><span data-stu-id="855fd-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="855fd-177">Aggiornamento **percorso dello Script** troppo "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="855fd-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="855fd-178">Fare clic su **salvare** e il processo di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="855fd-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="855fd-179">Configurare Jenkins toodeploy App Web in Linux con Docker</span><span class="sxs-lookup"><span data-stu-id="855fd-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="855fd-180">Oltre a Git o FTP, l'app Web in Linux supporta la distribuzione tramite Docker.</span><span class="sxs-lookup"><span data-stu-id="855fd-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="855fd-181">toodeploy usando Docker, è necessario tooprovide un Dockerfile utilizzate dai pacchetti di app web con runtime del servizio in un'immagine di docker.</span><span class="sxs-lookup"><span data-stu-id="855fd-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="855fd-182">Quindi plug-in hello Crea immagine hello, inserisce del Registro di sistema di tooa docker e distribuisce hello immagine tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="855fd-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="855fd-183">Web App in Linux supporta anche modalità tradizionali come Git e FTP, ma solo per i linguaggi predefiniti come .NET Core, Node.js, PHP e Ruby.</span><span class="sxs-lookup"><span data-stu-id="855fd-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="855fd-184">Per altre lingue, è necessario toopackage del runtime dell'applicazione di servizio e del codice insieme in un'immagine docker e usare docker toodeploy.</span><span class="sxs-lookup"><span data-stu-id="855fd-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="855fd-185">Prima di configurare il processo di hello in Jenkins, è necessario un servizio app di Azure in Linux.</span><span class="sxs-lookup"><span data-stu-id="855fd-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="855fd-186">Un registro di sistema del contenitore è anche necessario toostore e gestire le immagini contenitore Docker private.</span><span class="sxs-lookup"><span data-stu-id="855fd-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="855fd-187">È possibile usare DockerHub; per questo esempio viene usato Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="855fd-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="855fd-188">È possibile seguire i passaggi di hello [qui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate un'App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="855fd-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="855fd-189">Registro di sistema di contenitore di Azure è un gestito [Docker Registro di sistema] (https://docs.docker.com/registry/) servizio basato su hello open source Docker del Registro di sistema 2.0.</span><span class="sxs-lookup"><span data-stu-id="855fd-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="855fd-190">Procedura [qui] hello (/ azure/container-registry/container-registry-get-started-azure-cli) per maggiori informazioni su come toodo in modo.</span><span class="sxs-lookup"><span data-stu-id="855fd-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="855fd-191">È anche possibile usare DockerHub.</span><span class="sxs-lookup"><span data-stu-id="855fd-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="855fd-192">toodeploy usando docker:</span><span class="sxs-lookup"><span data-stu-id="855fd-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="855fd-193">Creare un nuovo progetto freestyle nel dashboard di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="855fd-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="855fd-194">Configurare **gestione del codice sorgente** toouse nel fork locale di [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample) fornendo hello **URL del Repository**.</span><span class="sxs-lookup"><span data-stu-id="855fd-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="855fd-195">Ad esempio: http://github.com/&lt;yourID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="855fd-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="855fd-196">Aggiungere un progetto di hello toobuild passaggio di compilazione Maven utilizzando.</span><span class="sxs-lookup"><span data-stu-id="855fd-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="855fd-197">A tale scopo, aggiungere un **eseguire shell** e aggiungere hello seguente riga **comando**:</span><span class="sxs-lookup"><span data-stu-id="855fd-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="855fd-198">Aggiungere un'azione post-compilazione selezionando **Publish an Azure Web App** (Pubblica un'App Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="855fd-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="855fd-199">Fornire, **mySp**, entità servizio di Azure hello archiviati al passaggio precedente come credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="855fd-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="855fd-200">In **configurazione delle App** , scegliere il gruppo di risorse di hello e un'app web di Linux nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="855fd-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="855fd-201">Scegliere Publish via Docker (Pubblica tramite Docker).</span><span class="sxs-lookup"><span data-stu-id="855fd-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="855fd-202">Compilare il percorso **Dockerfile**.</span><span class="sxs-lookup"><span data-stu-id="855fd-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="855fd-203">È possibile mantenere predefinite hello "/ Dockerfile" per **Docker del Registro di sistema URL**, specificare il formato di hello https://&lt;myRegistry >. azurecr.io se si utilizza Azure contenitore Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="855fd-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="855fd-204">Non specificare un valore se si usa DockerHub.</span><span class="sxs-lookup"><span data-stu-id="855fd-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="855fd-205">Per **le credenziali del Registro di sistema**, aggiungere la credenziale hello per hello del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="855fd-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="855fd-206">È possibile ottenere hello userid e password eseguendo hello seguenti comandi CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="855fd-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="855fd-207">Hello primo comando Abilita account amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="855fd-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="855fd-208">Hello nome immagine docker e tag in **avanzate** scheda sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="855fd-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="855fd-209">Per impostazione predefinita, il nome di immagine viene ottenuto dall'immagine hello nome configurato nel tag Azure hello portale (nel contenitore Docker impostazione.) viene generato da $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="855fd-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="855fd-210">Assicurarsi di specificare il nome di immagine hello in un portale di Azure o fornire un valore per **immagine Docker** in **avanzate** scheda. Per questo esempio, specificare "&lt;yourRegistry >.azurecr.io/calculator" per **immagine Docker** e lasciare vuoto il valore del **tag immagine Docker**.</span><span class="sxs-lookup"><span data-stu-id="855fd-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="855fd-211">Si noti che la distribuzione avrà esito negativo se si usa l'impostazione dell'immagine Docker predefinita.</span><span class="sxs-lookup"><span data-stu-id="855fd-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="855fd-212">Assicurarsi di cambiare immagine personalizzata toouse configurazione di docker in base alle impostazioni contenitore Docker nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="855fd-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="855fd-213">Per immagine incorporata, utilizzare toodeploy approccio di caricamento file.</span><span class="sxs-lookup"><span data-stu-id="855fd-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="855fd-214">Approccio di caricamento toofile simile, è possibile scegliere un altro slot diverso da produzione.</span><span class="sxs-lookup"><span data-stu-id="855fd-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="855fd-215">Salvare e compilare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="855fd-215">Save and build hello project.</span></span> <span data-ttu-id="855fd-216">Viene visualizzata l'immagine del contenitore viene inserito tooyour del Registro di sistema e app web viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="855fd-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="855fd-217">Distribuire App in Linux tramite Docker tramite la pipeline di Jenkins tooWeb</span><span class="sxs-lookup"><span data-stu-id="855fd-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="855fd-218">Nell'interfaccia utente Web di GitHub aprire il file **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="855fd-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="855fd-219">Fare clic su hello matita icona tooedit il gruppo di risorse di file tooupdate hello e il nome dell'app web sulla riga 11 e 12 rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="855fd-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="855fd-220">Modifica riga 13 tooyour contenitore del Registro di sistema server</span><span class="sxs-lookup"><span data-stu-id="855fd-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="855fd-221">Modificare l'ID di riga tooupdate 16 credenziale nell'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="855fd-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="855fd-222">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="855fd-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="855fd-223">Aprire Jenkins in un Web browser, fare clic su **New Item**.</span><span class="sxs-lookup"><span data-stu-id="855fd-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="855fd-224">Specificare un nome per il processo di hello e selezionare **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="855fd-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="855fd-225">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="855fd-225">Click **OK**.</span></span>
3. <span data-ttu-id="855fd-226">Fare clic su hello **Pipeline** scheda accanto.</span><span class="sxs-lookup"><span data-stu-id="855fd-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="855fd-227">Per **Definition** selezionare **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="855fd-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="855fd-228">Per **SCM** selezionare **Git**.</span><span class="sxs-lookup"><span data-stu-id="855fd-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="855fd-229">Immettere hello GitHub URL per il repository con fork: https:&lt;repository di scenari > GIT</span><span class="sxs-lookup"><span data-stu-id="855fd-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="855fd-230">Aggiornamento 7, **percorso dello Script** troppo "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="855fd-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="855fd-231">Fare clic su **salvare** e il processo di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="855fd-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="855fd-232">Verificare l'app Web</span><span class="sxs-lookup"><span data-stu-id="855fd-232">Verify your web app</span></span>

1. <span data-ttu-id="855fd-233">file WAR di hello tooverify venga distribuito correttamente tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="855fd-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="855fd-234">Aprire un Web browser.</span><span class="sxs-lookup"><span data-stu-id="855fd-234">Open a web browser.</span></span>
2. <span data-ttu-id="855fd-235">Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/ping visualizzati:</span><span class="sxs-lookup"><span data-stu-id="855fd-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="855fd-236">Benvenuto tooJava App Web.</span><span class="sxs-lookup"><span data-stu-id="855fd-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="855fd-237">indicante che l'aggiornamento è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="855fd-237">This is updated!</span></span>
   <span data-ttu-id="855fd-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="855fd-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="855fd-239">Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sostituire &lt;x > e &lt;y > con tutti i numeri) somma hello tooget di x e y</span><span class="sxs-lookup"><span data-stu-id="855fd-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![Calcolatrice: aggiungi](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="855fd-241">Per il servizio app in Linux</span><span class="sxs-lookup"><span data-stu-id="855fd-241">For App service on Linux</span></span>

* <span data-ttu-id="855fd-242">tooverify CLI di Azure, eseguire:</span><span class="sxs-lookup"><span data-stu-id="855fd-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="855fd-243">Si otterrà hello seguente risultato:</span><span class="sxs-lookup"><span data-stu-id="855fd-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="855fd-244">Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="855fd-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="855fd-245">Viene visualizzato il messaggio hello:</span><span class="sxs-lookup"><span data-stu-id="855fd-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="855fd-246">Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sostituire &lt;x > e &lt;y > con tutti i numeri) somma hello tooget di x e y</span><span class="sxs-lookup"><span data-stu-id="855fd-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="855fd-247">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="855fd-247">Next steps</span></span>

<span data-ttu-id="855fd-248">In questa esercitazione, si utilizza tooAzure toodeploy plug-in di hello Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="855fd-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="855fd-249">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="855fd-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="855fd-250">Configurare Jenkins toodeploy servizio App di Azure tramite FTP</span><span class="sxs-lookup"><span data-stu-id="855fd-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="855fd-251">Configurare Jenkins toodeploy tooAzure servizio App in Linux con Docker</span><span class="sxs-lookup"><span data-stu-id="855fd-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
