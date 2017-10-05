---
title: Eseguire l'interfaccia della riga di comando di Azure con Jenkins | Microsoft Docs
description: Informazioni su come usare l'interfaccia della riga di comando di Azure per distribuire un'app web di Java in Azure in Jenkins Pipeline
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 5ca8338d4bf343f08fe70081cff755fa76a126a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-and-the-azure-cli"></a><span data-ttu-id="07698-103">Distribuire nel servizio app di Azure con Jenkins e l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="07698-103">Deploy to Azure App Service with Jenkins and the Azure CLI</span></span>
<span data-ttu-id="07698-104">Per distribuire un'app Web di Java in Azure, è possibile usare l'interfaccia della riga di comando di Azure in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="07698-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="07698-105">In questa esercitazione viene creata una pipeline CI/CD in una macchina virtuale di Azure e viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="07698-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07698-106">Creare una macchina virtuale Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="07698-107">Configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-107">Configure Jenkins</span></span>
> * <span data-ttu-id="07698-108">Creare un'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="07698-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="07698-109">Preparare un repository GitHub</span><span class="sxs-lookup"><span data-stu-id="07698-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="07698-110">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="07698-111">Eseguire la pipeline e verificare l'app Web</span><span class="sxs-lookup"><span data-stu-id="07698-111">Run the pipeline and verify the web app</span></span>

<span data-ttu-id="07698-112">Questa esercitazione richiede l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="07698-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="07698-113">Per trovare la versione, eseguire `az --version`.</span><span class="sxs-lookup"><span data-stu-id="07698-113">To find the version, run `az --version`.</span></span> <span data-ttu-id="07698-114">Se è necessario eseguire l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="07698-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="07698-115">Creare e configurare un'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="07698-116">Se si dispone già di un master di Jenkins, iniziare con il [modello di soluzione](install-jenkins-solution-template.md) che include il plug-in delle [credenziali di Azure](https://plugins.jenkins.io/azure-credentials) richiesto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="07698-116">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="07698-117">Il plug-in delle credenziali di Azure consente di archiviare le credenziali dell'entità servizio di Microsoft Azure in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="07698-117">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="07698-118">Nella versione 1.2 è stato aggiunto il supporto affinché Jenkins Pipeline possa ottenere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="07698-118">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span></span> 

<span data-ttu-id="07698-119">Assicurarsi di disporre della versione 1.2 o versioni successive:</span><span class="sxs-lookup"><span data-stu-id="07698-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="07698-120">Nel dashboard di Jenkins, fare clic su **Manage Jenkins -> Plugin Manager ->** e cercare **Azure Credential**.</span><span class="sxs-lookup"><span data-stu-id="07698-120">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="07698-121">Se la versione è precedente alla 1.2, aggiornare il plug-in.</span><span class="sxs-lookup"><span data-stu-id="07698-121">Update the plugin if the version is earlier than 1.2.</span></span>

<span data-ttu-id="07698-122">Anche Java JDK e Maven sono necessari nel master di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="07698-122">Java JDK and Maven are also required in the Jenkins master.</span></span> <span data-ttu-id="07698-123">Per l'installazione, accedere al master di Jenkins usando SSH ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="07698-123">To install, log in to Jenkins master using SSH and run the following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="07698-124">Aggiungere l'entità servizio di Azure alla credenziale di Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-124">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="07698-125">Per eseguire l'interfaccia della riga di comando di Azure è necessaria una credenziale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07698-125">An Azure credential is needed to execute Azure CLI.</span></span>

* <span data-ttu-id="07698-126">Nel dashboard di Jenkins fare clic su **Credentials -> System ->**.</span><span class="sxs-lookup"><span data-stu-id="07698-126">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="07698-127">Fare clic su **Global credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="07698-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="07698-128">Fare clic su **Add Credentials** per aggiungere un'[entità servizio di Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json), immettendo: Subscription ID (ID sottoscrizione), Client ID (ID client), Client Secret (Segreto client) e OAuth 2.0 Token Endpoint (Endpoint di token OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="07698-128">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="07698-129">Indicare un ID per l'uso nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="07698-129">Provide an ID for use in subsequent step.</span></span>

![Add Credentials](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-the-java-web-app"></a><span data-ttu-id="07698-131">Creare un servizio app di Azure per la distribuzione dell'app Web di Java</span><span class="sxs-lookup"><span data-stu-id="07698-131">Create an Azure App Service for deploying the Java web app</span></span>

<span data-ttu-id="07698-132">Creare un piano di servizio app di Azure con il piano tariffario **GRATUITO** usando il comando dell'interfaccia della riga di comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="07698-132">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="07698-133">Il piano di servizio app definisce le risorse fisiche usate per ospitare le app.</span><span class="sxs-lookup"><span data-stu-id="07698-133">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="07698-134">Tutte le applicazioni assegnate a un piano di servizio app condividono queste risorse, per poter consentire un risparmio sui costi quando si ospitano più app.</span><span class="sxs-lookup"><span data-stu-id="07698-134">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="07698-135">Quando il piano è pronto, l'output dell'interfaccia della riga di comando di Azure è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="07698-135">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="07698-136">Creare un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="07698-136">Create an Azure Web app</span></span>

 <span data-ttu-id="07698-137">Usare il comando dell'interfaccia della riga di comando [az webapp create](/cli/azure/appservice/web#create) per creare la definizione di un'app Web nel piano di servizio app `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="07698-137">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="07698-138">La definizione dell'app Web fornisce un URL con cui accedere all'applicazione e configura diverse opzioni per distribuire il codice in Azure.</span><span class="sxs-lookup"><span data-stu-id="07698-138">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="07698-139">Sostituire il segnaposto `<app_name>` con il nome univoco dell'app.</span><span class="sxs-lookup"><span data-stu-id="07698-139">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="07698-140">Questo nome univoco fa parte del nome di dominio predefinito per l'app Web, quindi è necessario che sia univoco rispetto a tutte le app presenti in Azure.</span><span class="sxs-lookup"><span data-stu-id="07698-140">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="07698-141">È possibile eseguire il mapping di una voce di nome di dominio personalizzata all'app Web prima di esporla agli utenti.</span><span class="sxs-lookup"><span data-stu-id="07698-141">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="07698-142">Quando la definizione dell'app Web è pronta, l'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="07698-142">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="07698-143">Configurare Java</span><span class="sxs-lookup"><span data-stu-id="07698-143">Configure Java</span></span> 

<span data-ttu-id="07698-144">Impostare la configurazione del runtime Java necessaria per l'app con il comando [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="07698-144">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="07698-145">Il comando seguente configura l'app Web per l'esecuzione in un'istanza recente di Java 8 JDK e in [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="07698-145">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="07698-146">Preparare un repository GitHub</span><span class="sxs-lookup"><span data-stu-id="07698-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="07698-147">Aprire il repository [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="07698-147">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="07698-148">Per creare il fork del repository nel proprio account GitHub, fare clic sul pulsante **Fork** nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="07698-148">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

* <span data-ttu-id="07698-149">Nell'interfaccia utente Web di GitHub, aprire il file **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="07698-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="07698-150">Fare clic sull'icona della matita per modificare il file per aggiornare il gruppo di risorse e il nome dell'app Web nella riga 20 e 21 rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="07698-150">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="07698-151">Modificare la riga 23 per aggiornare l'ID delle credenziali nell'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-151">Change line 23 to update credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="07698-152">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="07698-153">Aprire Jenkins in un Web browser, fare clic su **New Item**.</span><span class="sxs-lookup"><span data-stu-id="07698-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="07698-154">Specificare un nome per il processo e selezionare **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="07698-154">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="07698-155">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="07698-155">Click **OK**.</span></span>
* <span data-ttu-id="07698-156">Quindi fare clic sulla scheda **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="07698-156">Click the **Pipeline** tab next.</span></span> 
* <span data-ttu-id="07698-157">Per **Definition** selezionare **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="07698-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="07698-158">Per **SCM** selezionare **Git**.</span><span class="sxs-lookup"><span data-stu-id="07698-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="07698-159">Immettere l'URL di GitHub per il repository con fork: https:\<your forked repo\>.git</span><span class="sxs-lookup"><span data-stu-id="07698-159">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="07698-160">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="07698-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="07698-161">Testare la pipeline</span><span class="sxs-lookup"><span data-stu-id="07698-161">Test your pipeline</span></span>
* <span data-ttu-id="07698-162">Passare alla pipeline creata e fare clic su **Build now**</span><span class="sxs-lookup"><span data-stu-id="07698-162">Go to the pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="07698-163">Una build dovrebbe avere esito positivo in pochi secondi ed è possibile passare alla build e fare clic su **Console Output** per visualizzare i dettagli</span><span class="sxs-lookup"><span data-stu-id="07698-163">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="07698-164">Verificare l'app Web</span><span class="sxs-lookup"><span data-stu-id="07698-164">Verify your web app</span></span>
<span data-ttu-id="07698-165">Per verificare che il file WAR sia stato distribuito correttamente nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="07698-165">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="07698-166">Aprire un Web browser:</span><span class="sxs-lookup"><span data-stu-id="07698-166">Open a web browser:</span></span>

* <span data-ttu-id="07698-167">Passare a http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="07698-167">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="07698-168">Verranno visualizzati:</span><span class="sxs-lookup"><span data-stu-id="07698-168">You see:</span></span>

        Welcome to Java Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="07698-169">Passare a http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (sostituire &lt;x> e &lt;y> con numeri qualsiasi) per ottenere la somma di x e y</span><span class="sxs-lookup"><span data-stu-id="07698-169">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>

![Calcolatrice: aggiungi](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-to-azure-web-app-on-linux"></a><span data-ttu-id="07698-171">Distribuire un'app Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="07698-171">Deploy to Azure Web App on Linux</span></span>
<span data-ttu-id="07698-172">Ora che si è appreso come usare l'interfaccia della riga di comando di Azure nella pipeline di Jenkins, è possibile modificare lo script per la distribuzione di un'app Web di Azure in Linux.</span><span class="sxs-lookup"><span data-stu-id="07698-172">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span></span>

<span data-ttu-id="07698-173">L'app Web in Linux supporta un modo diverso di esecuzione della distribuzione, che consiste nell'usare Docker.</span><span class="sxs-lookup"><span data-stu-id="07698-173">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span></span> <span data-ttu-id="07698-174">Per la distribuzione è necessario fornire un Dockerfile che include l'app Web in runtime di servizio in un'immagine Docker.</span><span class="sxs-lookup"><span data-stu-id="07698-174">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="07698-175">Il plug-in compilerà l'immagine, la inserirà in un registro Docker e la distribuirà nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="07698-175">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span></span>

* <span data-ttu-id="07698-176">Seguire i passaggi indicati [qui](/azure/app-service-web/app-service-linux-how-to-create-web-app) per creare un'app Web di Azure in esecuzione in Linux.</span><span class="sxs-lookup"><span data-stu-id="07698-176">Follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="07698-177">Installare Docker nell'istanza Jenkins seguendo le istruzioni riportate in questo [articolo](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="07698-177">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="07698-178">Creare un registro contenitori nel portale di Azure seguendo i passaggi indicati [qui](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="07698-178">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="07698-179">Nello stesso repository [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) con fork modificare il file **Jenkinsfile2**:</span><span class="sxs-lookup"><span data-stu-id="07698-179">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="07698-180">Riga 18-21, aggiornare rispettivamente i nomi del gruppo di risorse, l'app Web e il record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="07698-180">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="07698-181">Riga 24, aggiornare \<azsrvprincipal\> all'ID delle credenziali</span><span class="sxs-lookup"><span data-stu-id="07698-181">Line 24, update \<azsrvprincipal\> to your credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="07698-182">Creare una nuova pipeline Jenkins come per la distribuzione dell'app Web di Azure in Windows; solo questa volta usare invece **Jenkinsfile2**.</span><span class="sxs-lookup"><span data-stu-id="07698-182">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="07698-183">Eseguire il nuovo processo.</span><span class="sxs-lookup"><span data-stu-id="07698-183">Run your new job.</span></span>
* <span data-ttu-id="07698-184">Per verificare, nell'interfaccia della riga di comando di Azure eseguire:</span><span class="sxs-lookup"><span data-stu-id="07698-184">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="07698-185">Si ottiene il risultato seguente:</span><span class="sxs-lookup"><span data-stu-id="07698-185">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="07698-186">Passare a http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="07698-186">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="07698-187">Viene visualizzato il messaggio:</span><span class="sxs-lookup"><span data-stu-id="07698-187">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="07698-188">Passare a http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (sostituire &lt;x> e &lt;y> con numeri qualsiasi) per ottenere la somma di x e y</span><span class="sxs-lookup"><span data-stu-id="07698-188">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="07698-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07698-189">Next steps</span></span>
<span data-ttu-id="07698-190">In questa esercitazione è stata configurata la pipeline Jenkins che estrae il codice sorgente nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="07698-190">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span></span> <span data-ttu-id="07698-191">Esegue Maven per compilare un file WAR e quindi usa l'interfaccia della riga di comando di Azure per distribuire nel servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="07698-191">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span></span> <span data-ttu-id="07698-192">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="07698-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07698-193">Creare una macchina virtuale Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="07698-194">Configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-194">Configure Jenkins</span></span>
> * <span data-ttu-id="07698-195">Creare un'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="07698-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="07698-196">Preparare un repository GitHub</span><span class="sxs-lookup"><span data-stu-id="07698-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="07698-197">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="07698-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="07698-198">Eseguire la pipeline e verificare l'app Web</span><span class="sxs-lookup"><span data-stu-id="07698-198">Run the pipeline and verify the web app</span></span>
