---
title: Eseguire la distribuzione nel Servizio app di Azure con il plug-in Jenkins| Microsoft Docs
description: Informazioni su come usare il Servizio app di Azure per distribuire un'app Web Java in Azure con Jenkins
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
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a><span data-ttu-id="0d704-103">Eseguire la distribuzione nel Servizio app di Azure con il plug-in Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-103">Deploy to Azure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="0d704-104">Per distribuire un'app Web Java in Azure, è possibile usare l'interfaccia della riga di comando di Azure in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) oppure il [plug-in Jenkins Servizio app di Azure](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="0d704-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="0d704-105">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="0d704-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0d704-106">Configurare Jenkins per eseguire la distribuzione nel Servizio app di Azure tramite FTP</span><span class="sxs-lookup"><span data-stu-id="0d704-106">Configure Jenkins to deploy to Azure App Service through FTP</span></span> 
> * <span data-ttu-id="0d704-107">Configurare Jenkins per eseguire la distribuzione nel Servizio app di Azure su Linux tramite Docker</span><span class="sxs-lookup"><span data-stu-id="0d704-107">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="0d704-108">Creare e configurare un'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="0d704-109">Se non è già disponibile un master Jenkins, iniziare con il [modello di soluzione](install-jenkins-solution-template.md) che include JDK8 e i seguenti plug-in necessari:</span><span class="sxs-lookup"><span data-stu-id="0d704-109">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and the following required plugins:</span></span>

* <span data-ttu-id="0d704-110">[Plug-in Git client Jenkins](https://plugins.jenkins.io/git-client) 2.4.6</span><span class="sxs-lookup"><span data-stu-id="0d704-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="0d704-111">[Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) 1.4.0</span><span class="sxs-lookup"><span data-stu-id="0d704-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="0d704-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) 1.2</span><span class="sxs-lookup"><span data-stu-id="0d704-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="0d704-113">[Servizio app di Azure](https://plugins.jenkins.io/azure-app-server) versione 0.1</span><span class="sxs-lookup"><span data-stu-id="0d704-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="0d704-114">È possibile usare il plug-in del servizio app per distribuire l'app Web in tutti i linguaggi, ad esempio C#, PHP, Java e node.js, supportati dal servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d704-114">You can use the App Service plugin to deploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="0d704-115">In questa esercitazione viene usata l'app Java di esempio, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="0d704-115">In this tutorial, we are using the sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="0d704-116">Per creare il fork del repository nel proprio account GitHub, fare clic sul pulsante **Fork** nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="0d704-116">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>  

<span data-ttu-id="0d704-117">Per compilare il progetto Java sono necessari Java JDK e Maven.</span><span class="sxs-lookup"><span data-stu-id="0d704-117">Java JDK and Maven are required for building the Java project.</span></span> <span data-ttu-id="0d704-118">Assicurarsi di installare i componenti nel master Jenkins o l'agente VM, se in uso per l'integrazione continua.</span><span class="sxs-lookup"><span data-stu-id="0d704-118">Make sure you install the components in the Jenkins master or the VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="0d704-119">Per l'installazione, accedere all'istanza di Jenkins usando SSH ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d704-119">To install, log in to the Jenkins instance using SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="0d704-120">Per la distribuzione del servizio app in Linux, è necessario anche installare Docker sul master Jenkins o sull'agente VM usato per la compilazione.</span><span class="sxs-lookup"><span data-stu-id="0d704-120">For deploying to App Service on Linux, you also need to install Docker on the Jenkins master or the VM agent used for build.</span></span> <span data-ttu-id="0d704-121">Leggere questo articolo per installare Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="0d704-121">Refer to this article to install Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="0d704-122">Aggiungere l'entità servizio di Azure alla credenziale di Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-122">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="0d704-123">Per la distribuzione in Azure è necessaria un'entità servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d704-123">An Azure service principal is needed to deploy to Azure.</span></span> 

<ol>
<li><span data-ttu-id="0d704-124">Usare l'[interfaccia della riga di comando di Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) o il [portale di Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) per creare un'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="0d704-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) to create an Azure service principal</span></span></li>
<li><span data-ttu-id="0d704-125">Nel dashboard di Jenkins fare clic su **Credentials -> System ->**.</span><span class="sxs-lookup"><span data-stu-id="0d704-125">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="0d704-126">Fare clic su **Global credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="0d704-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="0d704-127">Fare clic su **Add Credentials** (Aggiungi credenziali) per aggiungere un'entità servizio di Microsoft Azure immettendo: Subscription ID (ID sottoscrizione), Client ID (ID client), Client Secret (Segreto client) e OAuth 2.0 Token Endpoint (Endpoint di token OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="0d704-127">Click **Add Credentials** to add a Microsoft Azure service principal by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="0d704-128">Indicare un ID, **mySp**, per l'uso nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="0d704-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="0d704-129">Plug-in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="0d704-129">Azure App Service plugin</span></span>

<span data-ttu-id="0d704-130">Il plug-in Servizio app di Azure v1.0 supporta la distribuzione continua in App Web di Azure tramite:</span><span class="sxs-lookup"><span data-stu-id="0d704-130">Azure App Service plugin v1.0 supports continuous deployment to Azure Web App through:</span></span>

* <span data-ttu-id="0d704-131">GIT e FTP</span><span class="sxs-lookup"><span data-stu-id="0d704-131">Git and FTP</span></span>
* <span data-ttu-id="0d704-132">Docker per App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="0d704-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a><span data-ttu-id="0d704-133">Configurare Jenkins per distribuire l'app Web tramite FTP usando il dashboard di Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-133">Configure Jenkins to deploy Web App through FTP using the Jenkins dashboard</span></span>

<span data-ttu-id="0d704-134">Per distribuire il progetto in App Web di Azure, è possibile caricare gli artefatti di compilazione, ad esempio i file .war in Java, usando Git o FTP.</span><span class="sxs-lookup"><span data-stu-id="0d704-134">To deploy your project to Azure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="0d704-135">Prima di configurare il processo in Jenkins, è necessario un piano di servizio app di Azure e un'app Web per l'esecuzione dell'app Java.</span><span class="sxs-lookup"><span data-stu-id="0d704-135">Before setting up the job in Jenkins, you need an Azure App Service plan and a Web App for running the Java app.</span></span>


1. <span data-ttu-id="0d704-136">Creare un piano di servizio app di Azure con il piano tariffario **GRATUITO** usando il comando dell'interfaccia della riga di comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="0d704-136">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="0d704-137">Il piano di servizio app definisce le risorse fisiche usate per ospitare le app.</span><span class="sxs-lookup"><span data-stu-id="0d704-137">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="0d704-138">Tutte le applicazioni assegnate a un piano di servizio app condividono queste risorse, per poter consentire un risparmio sui costi quando si ospitano più app.</span><span class="sxs-lookup"><span data-stu-id="0d704-138">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="0d704-139">Creare un'app Web.</span><span class="sxs-lookup"><span data-stu-id="0d704-139">Create a Web App.</span></span> <span data-ttu-id="0d704-140">È possibile usare il [portale di Azure](/azure/app-service-web/web-sites-configure) o il seguente comando Az dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="0d704-140">You can either use the [Azure portal](/azure/app-service-web/web-sites-configure) or use the following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="0d704-141">Assicurarsi di impostare la configurazione del runtime Java di cui l'app necessita.</span><span class="sxs-lookup"><span data-stu-id="0d704-141">Make sure you set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="0d704-142">Il comando dell'interfaccia della riga di comando di Azure seguente configura l'app Web per l'esecuzione in un'istanza recente di Java 8 JDK e in [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="0d704-142">The following Azure CLI command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="0d704-143">Impostare il processo Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-143">Set up the Jenkins job</span></span>


1. <span data-ttu-id="0d704-144">Creare un nuovo progetto **freestyle** nel dashboard di Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="0d704-145">Configurare la **gestione del codice sorgente** da usare nel fork locale di [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) fornendo l'**URL del repository**.</span><span class="sxs-lookup"><span data-stu-id="0d704-145">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="0d704-146">Ad esempio: http://github.com/&lt;yourID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="0d704-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="0d704-147">Aggiungere un'istruzione di compilazione per compilare il progetto usando Maven.</span><span class="sxs-lookup"><span data-stu-id="0d704-147">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="0d704-148">A tale scopo aggiungere un **Execute shell**.</span><span class="sxs-lookup"><span data-stu-id="0d704-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="0d704-149">Per questo esempio, è necessario un passaggio aggiuntivo per rinominare il file *.war nella cartella di destinazione in ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="0d704-149">For this example, we need an additional step to rename the *.war file in target folder to ROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="0d704-150">Aggiungere un'azione post-compilazione selezionando **Publish an Azure Web App** (Pubblica un'App Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="0d704-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="0d704-151">Fornire "mySp", l'entità servizio di Azure archiviata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="0d704-151">Supply, "mySp", the Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="0d704-152">Nella sezione **Configurazione app** scegliere l'app Web e il gruppo di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0d704-152">In **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="0d704-153">Il plug-in rileva automaticamente se l'app Web è basata su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="0d704-153">The plugin automatically detects whether the Web App is Windows or Linux-based.</span></span> <span data-ttu-id="0d704-154">Per un'app Web basata su Windows, viene visualizzata l'opzione "Publish Files" (Pubblica file).</span><span class="sxs-lookup"><span data-stu-id="0d704-154">For a Windows-based Web App, the option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="0d704-155">Compilare i file da distribuire, ad esempio un pacchetto war se si usa Java. La directory di origine e quella di destinazione sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="0d704-155">Fill in the files you want to deploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="0d704-156">I parametri consentono di specificare le cartelle di origine e di destinazione durante il caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="0d704-156">The parameters allow you to specify source and target folders when uploading files.</span></span> <span data-ttu-id="0d704-157">L'app Web Java in Azure viene eseguita in un server Tomcat.</span><span class="sxs-lookup"><span data-stu-id="0d704-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="0d704-158">Si carica il pacchetto war nella cartella webapps.</span><span class="sxs-lookup"><span data-stu-id="0d704-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="0d704-159">Per questo esempio, impostare **Source Directory** (Directory di origine) su "target" e specificare "webapps" per **Target Directory** (Directory di destinazione).</span><span class="sxs-lookup"><span data-stu-id="0d704-159">For this example, set **Source Directory** to "target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="0d704-160">Se si vuole eseguire la distribuzione in uno slot di diverso dalla produzione, è possibile anche impostare il nome **Slot**.</span><span class="sxs-lookup"><span data-stu-id="0d704-160">If you want to deploy to a slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="0d704-161">Salvare e compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="0d704-161">Save the project and build it.</span></span> <span data-ttu-id="0d704-162">L'app web viene distribuita in Azure al termine della compilazione.</span><span class="sxs-lookup"><span data-stu-id="0d704-162">Your web app is deployed to Azure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="0d704-163">Distribuire l'app Web tramite FTP usando la pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="0d704-164">Il plug-in è pronto per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="0d704-164">The plugin is pipeline-ready.</span></span> <span data-ttu-id="0d704-165">È possibile fare riferimento a un esempio nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="0d704-165">You can refer to a sample in the GitHub repo.</span></span>

1. <span data-ttu-id="0d704-166">Nell'interfaccia utente Web di GitHub aprire il file **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="0d704-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="0d704-167">Fare clic sull'icona della matita per modificare il file aggiornando il gruppo di risorse e il nome dell'app Web rispettivamente nella riga 11 e 12.</span><span class="sxs-lookup"><span data-stu-id="0d704-167">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="0d704-168">Modificare la riga 14 per aggiornare l'ID delle credenziali nell'istanza di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="0d704-168">Change line 14 to update credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="0d704-169">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="0d704-170">Aprire Jenkins in un Web browser, fare clic su **New Item**.</span><span class="sxs-lookup"><span data-stu-id="0d704-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="0d704-171">Specificare un nome per il processo e selezionare **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="0d704-171">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="0d704-172">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d704-172">Click **OK**.</span></span>
3. <span data-ttu-id="0d704-173">Quindi fare clic sulla scheda **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="0d704-173">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="0d704-174">Per **Definition** selezionare **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="0d704-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="0d704-175">Per **SCM** selezionare **Git**.</span><span class="sxs-lookup"><span data-stu-id="0d704-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="0d704-176">Immettere l'URL di GitHub per il repository con fork: https:&lt;your forked repo>.git</span><span class="sxs-lookup"><span data-stu-id="0d704-176">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="0d704-177">Aggiornare **Script Path** in "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="0d704-177">Update **Script Path** to "Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="0d704-178">Fare clic su **Salva** ed eseguire il processo.</span><span class="sxs-lookup"><span data-stu-id="0d704-178">Click **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a><span data-ttu-id="0d704-179">Configurare Jenkins per distribuire l'app Web in Linux tramite Docker</span><span class="sxs-lookup"><span data-stu-id="0d704-179">Configure Jenkins to deploy Web App on Linux through Docker</span></span>

<span data-ttu-id="0d704-180">Oltre a Git o FTP, l'app Web in Linux supporta la distribuzione tramite Docker.</span><span class="sxs-lookup"><span data-stu-id="0d704-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="0d704-181">Per la distribuzione usando Docker, è necessario fornire un Dockerfile che includa l'app Web in runtime di servizio in un'immagine Docker.</span><span class="sxs-lookup"><span data-stu-id="0d704-181">To deploy using Docker, you need to provide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="0d704-182">Il plug-in compila l'immagine, la inserisce in un registro Docker e la distribuisce nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="0d704-182">Then the plugin builds the image, pushes it to a docker registry and deploys the image to your web app.</span></span>

<span data-ttu-id="0d704-183">Web App in Linux supporta anche modalità tradizionali come Git e FTP, ma solo per i linguaggi predefiniti come .NET Core, Node.js, PHP e Ruby.</span><span class="sxs-lookup"><span data-stu-id="0d704-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="0d704-184">Per altri linguaggi, è necessario creare un pacchetto del runtime di servizio e del codice dell'applicazione in un'immagine docker e usare docker per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0d704-184">For other languages, you need to package your application code and service runtime together into a docker image and use docker to deploy.</span></span>

<span data-ttu-id="0d704-185">Prima di configurare il processo in Jenkins, è necessario un servizio app di Azure su Linux.</span><span class="sxs-lookup"><span data-stu-id="0d704-185">Before setting up the job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="0d704-186">Per archiviare e gestire immagini del contenitore Docker private è necessario anche un registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="0d704-186">A container registry is also needed to store and manage your private Docker container images.</span></span> <span data-ttu-id="0d704-187">È possibile usare DockerHub; per questo esempio viene usato Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d704-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="0d704-188">Seguire la procedura indicata [qui](/azure/app-service-web/app-service-linux-how-to-create-web-app) per creare un'app Web in Linux.</span><span class="sxs-lookup"><span data-stu-id="0d704-188">You can follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create a Web App on Linux</span></span> 
* <span data-ttu-id="0d704-189">Registro contenitori di Azure è un servizio gestito di [registri Docker] (https://docs.docker.com/registry/) basato sull'applicazione open source Docker Registry versione 2.0.</span><span class="sxs-lookup"><span data-stu-id="0d704-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="0d704-190">Seguire la procedura [qui] (/azure/container-registry/container-registry-get-started-azure-cli) per altro materiale sussidiario utile per eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="0d704-190">Follow the steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how to do so.</span></span> <span data-ttu-id="0d704-191">È anche possibile usare DockerHub.</span><span class="sxs-lookup"><span data-stu-id="0d704-191">You can also use DockerHub.</span></span>

### <a name="to-deploy-using-docker"></a><span data-ttu-id="0d704-192">Per eseguire la distribuzione usando Docker:</span><span class="sxs-lookup"><span data-stu-id="0d704-192">To deploy using docker:</span></span>

1. <span data-ttu-id="0d704-193">Creare un nuovo progetto freestyle nel dashboard di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="0d704-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="0d704-194">Configurare la **gestione del codice sorgente** da usare nel fork locale di [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) fornendo l'**URL del repository**.</span><span class="sxs-lookup"><span data-stu-id="0d704-194">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="0d704-195">Ad esempio: http://github.com/&lt;yourID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="0d704-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="0d704-196">Aggiungere un'istruzione di compilazione per compilare il progetto usando Maven.</span><span class="sxs-lookup"><span data-stu-id="0d704-196">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="0d704-197">A tale scopo aggiungere **Execute shell** e aggiungere la riga seguente in **Command**:</span><span class="sxs-lookup"><span data-stu-id="0d704-197">Do so by adding an **Execute shell** and add the following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="0d704-198">Aggiungere un'azione post-compilazione selezionando **Publish an Azure Web App** (Pubblica un'App Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="0d704-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="0d704-199">Fornire **mySp**, l'entità servizio di Azure archiviata nel passaggio precedente come Azure Credentials.</span><span class="sxs-lookup"><span data-stu-id="0d704-199">Supply, **mySp**, the Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="0d704-200">Nella sezione **App Configuration** (Configurazione app) scegliere il gruppo di risorse e un'app Web di Linux nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0d704-200">In **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="0d704-201">Scegliere Publish via Docker (Pubblica tramite Docker).</span><span class="sxs-lookup"><span data-stu-id="0d704-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="0d704-202">Compilare il percorso **Dockerfile**.</span><span class="sxs-lookup"><span data-stu-id="0d704-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="0d704-203">È possibile mantenere il valore predefinito "/Dockerfile" per l'**URL del registro Docker**, specificare il formato https://&lt;myRegistry >.azurecr.io se si usa il Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d704-203">You can keep the default "/Dockerfile" For **Docker registry URL**, supply in the format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="0d704-204">Non specificare un valore se si usa DockerHub.</span><span class="sxs-lookup"><span data-stu-id="0d704-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="0d704-205">Per **Registry credentials** (Credenziali registro) aggiungere le credenziali per il Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d704-205">For **Registry credentials**, add the credential for the Azure Container Registry.</span></span> <span data-ttu-id="0d704-206">Eseguire i comandi seguenti nell'interfaccia della riga di comando di Azure per ottenere l'ID utente e la password.</span><span class="sxs-lookup"><span data-stu-id="0d704-206">You can get the userid and password by running the following commands in Azure CLI.</span></span> <span data-ttu-id="0d704-207">Il primo comando abilita l'account Administrator.</span><span class="sxs-lookup"><span data-stu-id="0d704-207">The first command enables the administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="0d704-208">Il nome e il tag dell'immagine docker nella scheda **Avanzata** sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="0d704-208">The docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="0d704-209">Per impostazione predefinita, il nome dell'immagine viene ottenuto dal nome dell'immagine configurata nel portale di Azure, nell'impostazione del contenitore Docker. Il tag viene generato da $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="0d704-209">By default, image name is obtained from the image name you configured in Azure portal (in Docker Container setting.) The tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="0d704-210">Assicurarsi di specificare il nome dell'immagine nel portale di Azure o fornire un valore per l'**immagine Docker** nella scheda **Avanzata**. Per questo esempio, specificare "&lt;yourRegistry >.azurecr.io/calculator" per **immagine Docker** e lasciare vuoto il valore del **tag immagine Docker**.</span><span class="sxs-lookup"><span data-stu-id="0d704-210">Make sure you specify the image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="0d704-211">Si noti che la distribuzione avrà esito negativo se si usa l'impostazione dell'immagine Docker predefinita.</span><span class="sxs-lookup"><span data-stu-id="0d704-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="0d704-212">Assicurarsi di modificare la configurazione di Docker in modo da usare l'immagine personalizzata nell'impostazione del contenitore Docker nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d704-212">Make sure you change docker config to use custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="0d704-213">Per l'immagine predefinita, usare il metodo di caricamento file per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0d704-213">For built-in image, use file upload approach to deploy.</span></span>
11. <span data-ttu-id="0d704-214">Analogamente all'approccio di caricamento di file, è possibile scegliere un slot diverso da quello di produzione.</span><span class="sxs-lookup"><span data-stu-id="0d704-214">Similar to file upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="0d704-215">Salvare e compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="0d704-215">Save and build the project.</span></span> <span data-ttu-id="0d704-216">Viene eseguito il push dell'immagine del contenitore nel registro e l'app Web viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="0d704-216">You see your container image is pushed to your registry and web app is deployed.</span></span>

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="0d704-217">Eseguire la distribuzione nell'app Web in Linux tramite Docker usando la pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-217">Deploy to Web App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="0d704-218">Nell'interfaccia utente Web di GitHub aprire il file **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="0d704-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="0d704-219">Fare clic sull'icona della matita per modificare il file aggiornando il gruppo di risorse e il nome dell'app Web rispettivamente nella riga 11 e 12.</span><span class="sxs-lookup"><span data-stu-id="0d704-219">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="0d704-220">Modificare la riga 13 sul server del registro contenitori</span><span class="sxs-lookup"><span data-stu-id="0d704-220">Change line 13 to your container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="0d704-221">Modificare la riga 16 per aggiornare l'ID delle credenziali nell'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-221">Change line 16 to update credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="0d704-222">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="0d704-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="0d704-223">Aprire Jenkins in un Web browser, fare clic su **New Item**.</span><span class="sxs-lookup"><span data-stu-id="0d704-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="0d704-224">Specificare un nome per il processo e selezionare **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="0d704-224">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="0d704-225">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d704-225">Click **OK**.</span></span>
3. <span data-ttu-id="0d704-226">Quindi fare clic sulla scheda **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="0d704-226">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="0d704-227">Per **Definition** selezionare **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="0d704-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="0d704-228">Per **SCM** selezionare **Git**.</span><span class="sxs-lookup"><span data-stu-id="0d704-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="0d704-229">Immettere l'URL di GitHub per il repository con fork: https:&lt;your forked repo>.git</span><span class="sxs-lookup"><span data-stu-id="0d704-229">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="0d704-230">7, Aggiornare **Script Path** in "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="0d704-230">7, Update **Script Path** to "Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="0d704-231">Fare clic su **Salva** ed eseguire il processo.</span><span class="sxs-lookup"><span data-stu-id="0d704-231">Click **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="0d704-232">Verificare l'app Web</span><span class="sxs-lookup"><span data-stu-id="0d704-232">Verify your web app</span></span>

1. <span data-ttu-id="0d704-233">Per verificare che il file WAR sia stato distribuito correttamente nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="0d704-233">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="0d704-234">Aprire un Web browser.</span><span class="sxs-lookup"><span data-stu-id="0d704-234">Open a web browser.</span></span>
2. <span data-ttu-id="0d704-235">Passare a http://&lt;app_name>.azurewebsites.net/api/calculator/ping. Verrà visualizzato</span><span class="sxs-lookup"><span data-stu-id="0d704-235">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="0d704-236">un messaggio di benvenuto nell'app Web Java</span><span class="sxs-lookup"><span data-stu-id="0d704-236">Welcome to Java Web App!!!</span></span> <span data-ttu-id="0d704-237">indicante che l'aggiornamento è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="0d704-237">This is updated!</span></span>
   <span data-ttu-id="0d704-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="0d704-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="0d704-239">Passare a http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (sostituire &lt;x> e &lt;y> con numeri qualsiasi) per ottenere la somma di x e y</span><span class="sxs-lookup"><span data-stu-id="0d704-239">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>        
    ![Calcolatrice: aggiungi](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="0d704-241">Per il servizio app in Linux</span><span class="sxs-lookup"><span data-stu-id="0d704-241">For App service on Linux</span></span>

* <span data-ttu-id="0d704-242">Per verificare, nell'interfaccia della riga di comando di Azure eseguire:</span><span class="sxs-lookup"><span data-stu-id="0d704-242">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="0d704-243">Si ottiene il risultato seguente:</span><span class="sxs-lookup"><span data-stu-id="0d704-243">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="0d704-244">Passare a http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="0d704-244">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="0d704-245">Viene visualizzato il messaggio:</span><span class="sxs-lookup"><span data-stu-id="0d704-245">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="0d704-246">Passare a http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (sostituire &lt;x> e &lt;y> con numeri qualsiasi) per ottenere la somma di x e y</span><span class="sxs-lookup"><span data-stu-id="0d704-246">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="0d704-247">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d704-247">Next steps</span></span>

<span data-ttu-id="0d704-248">In questa esercitazione usare il plug-in Servizio app di Azure per eseguire la distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d704-248">In this tutorial, you use the Azure App Service plugin to deploy to Azure.</span></span>

<span data-ttu-id="0d704-249">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="0d704-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0d704-250">Configurare Jenkins per distribuire il Servizio app di Azure tramite FTP</span><span class="sxs-lookup"><span data-stu-id="0d704-250">Configure Jenkins to deploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="0d704-251">Configurare Jenkins per eseguire la distribuzione nel Servizio app di Azure su Linux tramite Docker</span><span class="sxs-lookup"><span data-stu-id="0d704-251">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 