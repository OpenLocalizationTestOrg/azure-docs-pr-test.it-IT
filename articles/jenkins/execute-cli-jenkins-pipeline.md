---
title: hello aaaExecute CLI di Azure con Jenkins | Documenti Microsoft
description: Informazioni su come toouse CLI di Azure toodeploy un Java web app tooAzure nella Pipeline di Jenkins
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
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="d9ac5-103">Distribuire il servizio App con Jenkins tooAzure e hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="d9ac5-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="d9ac5-104">toodeploy un tooAzure di app web Java, è possibile utilizzare l'interfaccia CLI di Azure in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="d9ac5-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="d9ac5-105">In questa esercitazione viene creata una pipeline CI/CD in una macchina virtuale di Azure e viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9ac5-106">Creare una macchina virtuale Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="d9ac5-107">Configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-107">Configure Jenkins</span></span>
> * <span data-ttu-id="d9ac5-108">Creare un'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="d9ac5-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="d9ac5-109">Preparare un repository GitHub</span><span class="sxs-lookup"><span data-stu-id="d9ac5-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="d9ac5-110">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="d9ac5-111">Eseguire la pipeline hello e verificare hello web app</span><span class="sxs-lookup"><span data-stu-id="d9ac5-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="d9ac5-112">Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d9ac5-113">versione di hello toofind, eseguire `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="d9ac5-114">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d9ac5-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="d9ac5-115">Creare e configurare un'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="d9ac5-116">Se si dispone già di un master Jenkins, iniziare con hello [modello di soluzione](install-jenkins-solution-template.md), che include hello necessario [le credenziali di Azure](https://plugins.jenkins.io/azure-credentials) plug-in per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="d9ac5-117">plug-in credenziali di Azure Hello consente credenziali dell'entità servizio di Microsoft Azure toostore Jenkins.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="d9ac5-118">Nella versione 1.2, viene aggiunto il supporto di hello pertanto Jenkins Pipeline ottenere hello le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="d9ac5-119">Assicurarsi di disporre della versione 1.2 o versioni successive:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="d9ac5-120">Nel dashboard di Jenkins hello, fare clic su **Jenkins Gestisci -> Gestione plug-in ->** e cercare **credenziali di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="d9ac5-121">Aggiornare i plug-in hello se hello versione è precedente a 1.2.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="d9ac5-122">Java JDK e Maven sono inoltre necessari nel database master di Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="d9ac5-123">tooinstall, di log nel database master tooJenkins tramite SSH ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="d9ac5-124">Aggiungere credenziali tooJenkins dell'entità servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="d9ac5-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="d9ac5-125">Una credenziale di Azure è necessario tooexecute CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="d9ac5-126">Nel dashboard di Jenkins hello, fare clic su **credenziali -> sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="d9ac5-127">Fare clic su **Global credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="d9ac5-128">Fare clic su **Aggiungi credenziali** tooadd un [dell'entità servizio di Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) compilando hello ID sottoscrizione, l'ID Client, segreto Client ed Endpoint Token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="d9ac5-129">Indicare un ID per l'uso nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-129">Provide an ID for use in subsequent step.</span></span>

![Add Credentials](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="d9ac5-131">Creare un servizio App di Azure per la distribuzione di app web Java di hello</span><span class="sxs-lookup"><span data-stu-id="d9ac5-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="d9ac5-132">Creare un piano di servizio App di Azure con hello **libero** tariffario utilizzando hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando CLI.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="d9ac5-133">piano di servizio App Hello definisce hello risorse fisiche utilizzate toohost app.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="d9ac5-134">Tutte le applicazioni assegnate piano di servizio App tooan condividono tali risorse, consentendo di costo toosave quando si ospitano più applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="d9ac5-135">Quando il piano di hello è pronto, hello che CLI di Azure viene illustrato simile output toohello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="d9ac5-136">Creare un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="d9ac5-136">Create an Azure Web app</span></span>

 <span data-ttu-id="d9ac5-137">Hello utilizzare [az webapp creare](/cli/azure/appservice/web#create) toocreate comando CLI una definizione di applicazione web in hello `myAppServicePlan` piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="d9ac5-138">definizione dell'app web Hello fornisce un tooaccess URL all'applicazione e consente di configurare diverse opzioni toodeploy tooAzure il codice.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="d9ac5-139">Hello Substitute `<app_name>` segnaposto con il proprio nome applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="d9ac5-140">Questo nome univoco fa parte del nome di dominio hello predefinito per l'app web hello, quindi nome hello deve toobe univoco tra tutte le App in Azure.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="d9ac5-141">È possibile eseguire il mapping di un'app web di toohello voce di nome di dominio personalizzato prima di esporre tooyour utenti.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="d9ac5-142">Quando la definizione di applicazione web hello è pronta, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="d9ac5-143">Configurare Java</span><span class="sxs-lookup"><span data-stu-id="d9ac5-143">Configure Java</span></span> 

<span data-ttu-id="d9ac5-144">Impostare la configurazione di runtime Java hello necessari all'app con hello [aggiornamento configurazione web di az appservice](/cli/azure/appservice/web/config#update) comando.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="d9ac5-145">Hello comando seguente consente di configurare hello web app toorun in una versione recente di Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="d9ac5-146">Preparare un repository GitHub</span><span class="sxs-lookup"><span data-stu-id="d9ac5-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="d9ac5-147">Aprire hello [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample) repository.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="d9ac5-148">toofork hello repository tooyour proprietari di account GitHub, fare clic su hello **Fork** pulsante nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="d9ac5-149">Nell'interfaccia utente Web di GitHub, aprire il file **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="d9ac5-150">Fare clic su hello matita icona tooedit il gruppo di risorse di file tooupdate hello e il nome dell'app web nella riga 20 e 21 rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="d9ac5-151">Modificare l'ID di riga tooupdate 23 credenziale nell'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="d9ac5-152">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="d9ac5-153">Aprire Jenkins in un Web browser, fare clic su **New Item**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="d9ac5-154">Specificare un nome per il processo di hello e selezionare **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="d9ac5-155">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-155">Click **OK**.</span></span>
* <span data-ttu-id="d9ac5-156">Fare clic su hello **Pipeline** scheda accanto.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="d9ac5-157">Per **Definition** selezionare **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="d9ac5-158">Per **SCM** selezionare **Git**.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="d9ac5-159">Immettere hello GitHub URL per il repository con fork: https:\<repository di scenari\>GIT</span><span class="sxs-lookup"><span data-stu-id="d9ac5-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="d9ac5-160">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="d9ac5-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="d9ac5-161">Testare la pipeline</span><span class="sxs-lookup"><span data-stu-id="d9ac5-161">Test your pipeline</span></span>
* <span data-ttu-id="d9ac5-162">Pipeline toohello è stato creato, quindi scegliere **compilare ora**</span><span class="sxs-lookup"><span data-stu-id="d9ac5-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="d9ac5-163">Una build dovrebbe avere esito positivo in pochi secondi, ed è possibile passare toohello compilazione e fare clic su **Output di Console** dettagli hello toosee</span><span class="sxs-lookup"><span data-stu-id="d9ac5-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="d9ac5-164">Verificare l'app Web</span><span class="sxs-lookup"><span data-stu-id="d9ac5-164">Verify your web app</span></span>
<span data-ttu-id="d9ac5-165">file WAR di hello tooverify venga distribuito correttamente tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="d9ac5-166">Aprire un Web browser:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-166">Open a web browser:</span></span>

* <span data-ttu-id="d9ac5-167">Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="d9ac5-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="d9ac5-168">Verranno visualizzati:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="d9ac5-169">Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sostituire &lt;x > e &lt;y > con tutti i numeri) somma hello tooget di x e y</span><span class="sxs-lookup"><span data-stu-id="d9ac5-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Calcolatrice: aggiungi](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="d9ac5-171">Distribuire tooAzure App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="d9ac5-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="d9ac5-172">Ora che si conosce la modalità di pipeline toouse CLI di Azure nel Jenkins, è possibile modificare hello script toodeploy tooan App Web di Azure in Linux.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="d9ac5-173">Web App in Linux supporta una distribuzione di hello toodo modo diverso, ovvero toouse Docker.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="d9ac5-174">toodeploy, è necessario tooprovide un Dockerfile utilizzate dai pacchetti di app web con runtime del servizio in un'immagine di Docker.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="d9ac5-175">plug-in Hello verrà quindi compilato immagine hello, spingerla del Registro di sistema di tooa Docker e distribuito hello immagine tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="d9ac5-176">Seguire i passaggi di hello [qui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate un'App Web di Azure in esecuzione in Linux.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="d9ac5-177">Installare Docker sull'istanza Jenkins seguendo le istruzioni di hello in questo [articolo](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="d9ac5-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="d9ac5-178">Creare un contenitore del Registro di sistema nel portale di Azure hello attenendosi alla procedura hello [qui](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d9ac5-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="d9ac5-179">In hello stesso [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample) repository è duplicato, modificare hello **Jenkinsfile2** file:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="d9ac5-180">Riga 18-21, aggiornare i nomi di toohello del gruppo di risorse e app web, ACR rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="d9ac5-181">Riga 24, aggiornamento \<azsrvprincipal\> ID delle credenziali tooyour</span><span class="sxs-lookup"><span data-stu-id="d9ac5-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="d9ac5-182">Creare una nuova pipeline di Jenkins seguendo durante la distribuzione in Windows, solo questa volta, utilizzare l'app web tooAzure **Jenkinsfile2** invece.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="d9ac5-183">Eseguire il nuovo processo.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-183">Run your new job.</span></span>
* <span data-ttu-id="d9ac5-184">tooverify CLI di Azure, eseguire:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="d9ac5-185">Si otterrà hello seguente risultato:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="d9ac5-186">Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="d9ac5-187">Viene visualizzato il messaggio hello:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="d9ac5-188">Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sostituire &lt;x > e &lt;y > con tutti i numeri) somma hello tooget di x e y</span><span class="sxs-lookup"><span data-stu-id="d9ac5-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="d9ac5-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d9ac5-189">Next steps</span></span>
<span data-ttu-id="d9ac5-190">In questa esercitazione, è configurata una pipeline di Jenkins che consente di estrarre il codice sorgente hello nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="d9ac5-191">Esecuzione di un file war toobuild Maven e quindi utilizza tooAzure toodeploy CLI di Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d9ac5-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="d9ac5-192">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="d9ac5-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9ac5-193">Creare una macchina virtuale Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="d9ac5-194">Configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-194">Configure Jenkins</span></span>
> * <span data-ttu-id="d9ac5-195">Creare un'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="d9ac5-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="d9ac5-196">Preparare un repository GitHub</span><span class="sxs-lookup"><span data-stu-id="d9ac5-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="d9ac5-197">Creare una pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="d9ac5-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="d9ac5-198">Eseguire la pipeline hello e verificare hello web app</span><span class="sxs-lookup"><span data-stu-id="d9ac5-198">Run hello pipeline and verify hello web app</span></span>
