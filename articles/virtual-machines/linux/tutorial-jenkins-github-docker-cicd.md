---
title: Creare una pipeline di sviluppo in Azure con Jenkins | Microsoft Docs
description: Informazioni su come creare una macchina virtuale di Jenkins in Azure che esegue il pull da GitHub in ogni commit di codice e compila un nuovo contenitore Docker per l'esecuzione dell'app
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d9849b5e061dd7f2ae0744a3522dc2eb1fb37035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="316a9-103">Come creare un'infrastruttura di sviluppo in una macchina virtuale Linux in Azure con Jenkins, GitHub e Docker</span><span class="sxs-lookup"><span data-stu-id="316a9-103">How to create a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="316a9-104">Per automatizzare le fasi di compilazione e test dello sviluppo di un'applicazione, è possibile usare una pipeline per l'integrazione e la distribuzione continue (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="316a9-104">To automate the build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="316a9-105">In questa esercitazione viene creata una pipeline CI/CD in una macchina virtuale di Azure e viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="316a9-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="316a9-106">Creare una macchina virtuale Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="316a9-107">Installare e configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="316a9-108">Creare un'integrazione webhook tra GitHub e Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="316a9-109">Creare e attivare processi di compilazione Jenkins da commit GitHub</span><span class="sxs-lookup"><span data-stu-id="316a9-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="316a9-110">Creare un'immagine Docker per l'app</span><span class="sxs-lookup"><span data-stu-id="316a9-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="316a9-111">Verificare che i commit GitHub compilino una nuova immagine Docker e gli aggiornamenti che eseguono l'app</span><span class="sxs-lookup"><span data-stu-id="316a9-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="316a9-112">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="316a9-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="316a9-113">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="316a9-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="316a9-114">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="316a9-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="316a9-115">Creare l'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-115">Create Jenkins instance</span></span>
<span data-ttu-id="316a9-116">In un'esercitazione precedente, [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) (Come personalizzare una macchina virtuale Linux al primo avvio), è stato descritto come personalizzare una macchina virtuale al primo avvio con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="316a9-116">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="316a9-117">Questa esercitazione usa un file cloud-init per installare Jenkins e Docker in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="316a9-117">This tutorial uses a cloud-init file to install Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="316a9-118">Nella shell corrente creare un file denominato *cloud-init.txt* e incollare la configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="316a9-118">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="316a9-119">Ad esempio, creare il file in Cloud Shell anziché nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="316a9-119">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="316a9-120">Immettere `sensible-editor cloud-init-jenkins.txt` per creare il file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="316a9-120">Enter `sensible-editor cloud-init-jenkins.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="316a9-121">Assicurarsi che l'intero file cloud-init venga copiato correttamente, in particolare la prima riga:</span><span class="sxs-lookup"><span data-stu-id="316a9-121">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

<span data-ttu-id="316a9-122">Per poter creare una macchina virtuale è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="316a9-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="316a9-123">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroupJenkins* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="316a9-123">The following example creates a resource group named *myResourceGroupJenkins* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="316a9-124">Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="316a9-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="316a9-125">Usare il parametro `--custom-data` per specificare il file di configurazione di cloud-init.</span><span class="sxs-lookup"><span data-stu-id="316a9-125">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="316a9-126">Se il file è stato salvato all'esterno della directory di lavoro corrente, specificare il percorso completo di *cloud-init-jenkins.txt*.</span><span class="sxs-lookup"><span data-stu-id="316a9-126">Provide the full path to *cloud-init-jenkins.txt* if you saved the file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="316a9-127">Per creare e configurare la macchina virtuale sono necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="316a9-127">It takes a few minutes for the VM to be created and configured.</span></span>

<span data-ttu-id="316a9-128">Per consentire al traffico Web di raggiungere la macchina virtuale, usare [az vm open-port](/cli/azure/vm#open-port) per aprire la porta *8080* per il traffico Jenkins e la porta *1337* per l'app Node.js che viene usata per eseguire un'app di esempio:</span><span class="sxs-lookup"><span data-stu-id="316a9-128">To allow web traffic to reach your VM, use [az vm open-port](/cli/azure/vm#open-port) to open port *8080* for Jenkins traffic and port *1337* for the Node.js app that is used to run a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="316a9-129">Configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-129">Configure Jenkins</span></span>
<span data-ttu-id="316a9-130">Per accedere all'istanza di Jenkins, ottenere l'indirizzo IP pubblico della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="316a9-130">To access your Jenkins instance, obtain the public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="316a9-131">Per motivi di sicurezza, è necessario immettere la password amministratore iniziale che viene archiviata in un file di testo nella macchina virtuale per avviare l'installazione di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="316a9-131">For security purposes, you need to enter the initial admin password that is stored in a text file on your VM to start the Jenkins install.</span></span> <span data-ttu-id="316a9-132">Usare l'indirizzo IP pubblico ottenuto nel passaggio precedente per la connessione SSH alla macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="316a9-132">Use the public IP address obtained in the previous step to SSH to your VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="316a9-133">Visualizzare la password `initialAdminPassword` per l'installazione di Jenkins e copiarla:</span><span class="sxs-lookup"><span data-stu-id="316a9-133">View the `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="316a9-134">Se il file non è ancora disponibile, attendere ancora qualche minuto che cloud-init completi l'installazione di Jenkins e Docker.</span><span class="sxs-lookup"><span data-stu-id="316a9-134">If the file isn't available yet, wait a couple more minutes for cloud-init to complete the Jenkins and Docker install.</span></span>

<span data-ttu-id="316a9-135">Aprire un Web browser e passare a `http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="316a9-135">Now open a web browser and go to `http://<publicIps>:8080`.</span></span> <span data-ttu-id="316a9-136">Completare la configurazione iniziale di Jenkins come segue:</span><span class="sxs-lookup"><span data-stu-id="316a9-136">Complete the initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="316a9-137">Immettere la password *initialAdminPassword* ottenuta dalla macchina virtuale nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="316a9-137">Enter the *initialAdminPassword* obtained from the VM in the previous step.</span></span>
- <span data-ttu-id="316a9-138">Fare clic su **Select plugins to install** (Seleziona plug-in da installare).</span><span class="sxs-lookup"><span data-stu-id="316a9-138">Click **Select plugins to install**</span></span>
- <span data-ttu-id="316a9-139">Cercare *GitHub* nella casella di testo nella parte superiore, selezionare il *plug-in GitHub* e quindi fare clic su **Install** (Installa).</span><span class="sxs-lookup"><span data-stu-id="316a9-139">Search for *GitHub* in the text box across the top, select the *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="316a9-140">Per creare un account utente di Jenkins, compilare il modulo secondo le esigenze.</span><span class="sxs-lookup"><span data-stu-id="316a9-140">To create a Jenkins user account, fill out the form as desired.</span></span> <span data-ttu-id="316a9-141">Dal punto di vista della sicurezza, è consigliabile creare questo primo utente Jenkins anziché continuare con l'account amministratore predefinito.</span><span class="sxs-lookup"><span data-stu-id="316a9-141">From a security perspective, you should create this first Jenkins user rather than continuing as the default admin account.</span></span>
- <span data-ttu-id="316a9-142">Al termine, fare clic su **Start using Jenkins** (Inizia a usare Jenkins).</span><span class="sxs-lookup"><span data-stu-id="316a9-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="316a9-143">Creare webhook di GitHub</span><span class="sxs-lookup"><span data-stu-id="316a9-143">Create GitHub webhook</span></span>
<span data-ttu-id="316a9-144">Per configurare l'integrazione con GitHub, aprire l'[app di esempio Node.js Hello World](https://github.com/Azure-Samples/nodejs-docs-hello-world) dal repository di esempi di Azure.</span><span class="sxs-lookup"><span data-stu-id="316a9-144">To configure the integration with GitHub, open the [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from the Azure samples repo.</span></span> <span data-ttu-id="316a9-145">Per creare il fork del repository nel proprio account GitHub, fare clic sul pulsante **Fork** nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="316a9-145">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

<span data-ttu-id="316a9-146">Creare un webhook all'interno del fork creato:</span><span class="sxs-lookup"><span data-stu-id="316a9-146">Create a webhook inside the fork you created:</span></span>

- <span data-ttu-id="316a9-147">Fare clic su **Settings** (Impostazioni) e quindi selezionare **Integrations & services** (Integrazioni e servizi) sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="316a9-147">Click **Settings**, then select **Integrations & services** on the left-hand side.</span></span>
- <span data-ttu-id="316a9-148">Fare clic su **Add service** (Aggiungi servizio) e quindi immettere *Jenkins* nella casella del filtro.</span><span class="sxs-lookup"><span data-stu-id="316a9-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="316a9-149">Selezionare *Jenkins (GitHub plugin)* (Jenkins (plug-in GitHub)).</span><span class="sxs-lookup"><span data-stu-id="316a9-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="316a9-150">In **Jenkins hook URL** (URL hook Jenkins) immettere `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="316a9-150">For the **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="316a9-151">Assicurarsi di includere la barra finale (/).</span><span class="sxs-lookup"><span data-stu-id="316a9-151">Make sure you include the trailing /</span></span>
- <span data-ttu-id="316a9-152">Fare clic su **Add service** (Aggiungi servizio).</span><span class="sxs-lookup"><span data-stu-id="316a9-152">Click **Add service**</span></span>

![Aggiunta del webhook di GitHub al repository con fork](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="316a9-154">Creare un processo di Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-154">Create Jenkins job</span></span>
<span data-ttu-id="316a9-155">Per fare in modo che Jenkins risponda a un evento in GitHub, ad esempio l'esecuzione del commit di codice, creare un processo di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="316a9-155">To have Jenkins respond to an event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="316a9-156">Nel sito Web di Jenkins fare clic su **Create new jobs** (Crea nuovi processi) dalla home page:</span><span class="sxs-lookup"><span data-stu-id="316a9-156">In your Jenkins website, click **Create new jobs** from the home page:</span></span>

- <span data-ttu-id="316a9-157">Immettere *HelloWorld* come nome del processo.</span><span class="sxs-lookup"><span data-stu-id="316a9-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="316a9-158">Scegliere **Freestyle project** (Progetto Freestyle) e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="316a9-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="316a9-159">Nella sezione **General** (Generale) selezionare il progetto **GitHub** e immettere l'URL del repository con fork, ad esempio *https://github.com/iainfoulds/nodejs-docs-hello-world*.</span><span class="sxs-lookup"><span data-stu-id="316a9-159">Under the **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="316a9-160">Nella sezione **Source code management** (Gestione del codice sorgente) selezionare **Git** e immettere l'URL *.git* del repository con fork, ad esempio *https://github.com/iainfoulds/nodejs-docs-hello-world.git*.</span><span class="sxs-lookup"><span data-stu-id="316a9-160">Under the **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="316a9-161">Nella sezione **Build Triggers** (Trigger di compilazione) selezionare **GitHub hook trigger for GITScm polling** (Trigger di hook GitHub per polling GITScm).</span><span class="sxs-lookup"><span data-stu-id="316a9-161">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="316a9-162">Nella sezione **Build** (Compilazione) scegliere **Add build step** (Aggiungi istruzione di compilazione).</span><span class="sxs-lookup"><span data-stu-id="316a9-162">Under the **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="316a9-163">Selezionare **Execute shell** (Esegui shell) e quindi immettere `echo "Testing"` nella finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="316a9-163">Select **Execute shell**, then enter `echo "Testing"` in to command window.</span></span>
- <span data-ttu-id="316a9-164">Fare clic su **Save** (Salva) nella parte inferiore della finestra dei processi.</span><span class="sxs-lookup"><span data-stu-id="316a9-164">Click **Save** at the bottom of the jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="316a9-165">Testare l'integrazione di GitHub</span><span class="sxs-lookup"><span data-stu-id="316a9-165">Test GitHub integration</span></span>
<span data-ttu-id="316a9-166">Per testare l'integrazione di GitHub con Jenkins, eseguire il commit di una modifica nel fork.</span><span class="sxs-lookup"><span data-stu-id="316a9-166">To test the GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="316a9-167">Nell'interfaccia utente Web di GitHub selezionare il repository con fork e quindi fare clic sul file **index.js**.</span><span class="sxs-lookup"><span data-stu-id="316a9-167">Back in GitHub web UI, select your forked repo, and then click the **index.js** file.</span></span> <span data-ttu-id="316a9-168">Fare clic sull'icona a forma di matita per modificare il file in modo che la riga 6 corrisponda a:</span><span class="sxs-lookup"><span data-stu-id="316a9-168">Click the pencil icon to edit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="316a9-169">Per eseguire il commit delle modifiche, fare clic sul pulsante **Commit changes** (Esegui il commit delle modifiche) nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="316a9-169">To commit your changes, click the **Commit changes** button at the bottom.</span></span>

<span data-ttu-id="316a9-170">In Jenkins viene avviata una nuova compilazione nella sezione **Build history** (Cronologia compilazione) nell'angolo inferiore sinistro della pagina del processo.</span><span class="sxs-lookup"><span data-stu-id="316a9-170">In Jenkins, a new build starts under the **Build history** section of the bottom left-hand corner of your job page.</span></span> <span data-ttu-id="316a9-171">Fare clic sul collegamento del numero di build e selezionare **Console output** (Output console) sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="316a9-171">Click the build number link and select **Console output** on the left-hand size.</span></span> <span data-ttu-id="316a9-172">È possibile visualizzare i passaggi eseguiti in Jenkins mentre viene eseguito il pull del codice da GitHub e l'azione di compilazione genera il messaggio `Testing` nella console.</span><span class="sxs-lookup"><span data-stu-id="316a9-172">You can view the steps Jenkins takes as your code is pulled from GitHub and the build action outputs the message `Testing` to the console.</span></span> <span data-ttu-id="316a9-173">Ogni volta che si esegue un'operazione di commit in GitHub, il webhook contatta Jenkins e attiva una nuova compilazione in questo modo.</span><span class="sxs-lookup"><span data-stu-id="316a9-173">Each time a commit is made in GitHub, the webhook reaches out to Jenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="316a9-174">Definire l'immagine di compilazione di Docker</span><span class="sxs-lookup"><span data-stu-id="316a9-174">Define Docker build image</span></span>
<span data-ttu-id="316a9-175">Per visualizzare l'app Node.js in esecuzione sulla base dei commit GitHub, è necessario creare un'immagine Docker per l'esecuzione dell'app.</span><span class="sxs-lookup"><span data-stu-id="316a9-175">To see the Node.js app running based on your GitHub commits, lets build a Docker image to run the app.</span></span> <span data-ttu-id="316a9-176">L'immagine viene creata da un file Dockerfile che definisce come configurare il contenitore che esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="316a9-176">The image is built from a Dockerfile that defines how to configure the container that runs the app.</span></span> 

<span data-ttu-id="316a9-177">Dalla connessione SSH alla macchina virtuale, passare alla directory dell'area di lavoro di Jenkins denominata sulla base del processo creato in un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="316a9-177">From the SSH connection to your VM, change to the Jenkins workspace directory named after the job you created in a previous step.</span></span> <span data-ttu-id="316a9-178">In questo esempio è stata denominata *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="316a9-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="316a9-179">Creare un file con `sudo sensible-editor Dockerfile` in questa directory dell'area di lavoro e incollare il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="316a9-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste the following contents.</span></span> <span data-ttu-id="316a9-180">Assicurarsi che l'intero file Docker venga copiato correttamente, in particolare la prima riga:</span><span class="sxs-lookup"><span data-stu-id="316a9-180">Make sure that the whole Dockerfile is copied correctly, especially the first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="316a9-181">Questo file Dockerfile usa l'immagine di base Node.js con Alpine Linux, espone la porta 1337 in cui viene eseguita l'app Hello World, quindi copia i file dell'app e la inizializza.</span><span class="sxs-lookup"><span data-stu-id="316a9-181">This Dockerfile uses the base Node.js image using Alpine Linux, exposes port 1337 that the Hello World app runs on, then copies the app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="316a9-182">Creare regole di compilazione di Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-182">Create Jenkins build rules</span></span>
<span data-ttu-id="316a9-183">In un passaggio precedente è stata creata una regola di compilazione di base di Jenkins che genera un messaggio nella console.</span><span class="sxs-lookup"><span data-stu-id="316a9-183">In a previous step, you created a basic Jenkins build rule that output a message to the console.</span></span> <span data-ttu-id="316a9-184">Ora è necessario creare l'istruzione di compilazione per usare il file Dockerfile ed eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="316a9-184">Lets create the build step to use our Dockerfile and run the app.</span></span>

<span data-ttu-id="316a9-185">Nell'istanza di Jenkins selezionare il processo creato in un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="316a9-185">Back in your Jenkins instance, select the job you created in a previous step.</span></span> <span data-ttu-id="316a9-186">Fare clic su **Configure** (Configura) sul lato sinistro e scorrere fino alla sezione **Build** (Compilazione):</span><span class="sxs-lookup"><span data-stu-id="316a9-186">Click **Configure** on the left-hand side and scroll down to the **Build** section:</span></span>

- <span data-ttu-id="316a9-187">Rimuovere l'istruzione di compilazione `echo "Test"` esistente.</span><span class="sxs-lookup"><span data-stu-id="316a9-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="316a9-188">Fare clic sulla croce rossa nell'angolo superiore destro della casella dell'istruzione di compilazione esistente.</span><span class="sxs-lookup"><span data-stu-id="316a9-188">Click the red cross on the top right-hand corner of the existing build step box.</span></span>
- <span data-ttu-id="316a9-189">Fare clic su **Add build step** (Aggiungi istruzione di compilazione) e quindi selezionare **Execute shell** (Esegui shell).</span><span class="sxs-lookup"><span data-stu-id="316a9-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="316a9-190">Nella casella **Command** (Comando) immettere i comandi Docker seguenti, quindi selezionare **Save** (Salva):</span><span class="sxs-lookup"><span data-stu-id="316a9-190">In the **Command** box, enter the following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="316a9-191">Le istruzioni di compilazione Docker creano un'immagine contrassegnata con il numero di build Jenkins, in modo da mantenere una cronologia delle immagini.</span><span class="sxs-lookup"><span data-stu-id="316a9-191">The Docker build steps create an image and tag it with the Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="316a9-192">Gli eventuali contenitori esistenti che eseguono l'app vengono arrestati e quindi rimossi.</span><span class="sxs-lookup"><span data-stu-id="316a9-192">Any existing containers running the app are stopped and then removed.</span></span> <span data-ttu-id="316a9-193">Si avvia quindi un nuovo contenitore usando l'immagine e si esegue l'app Node.js in base agli ultimi commit in GitHub.</span><span class="sxs-lookup"><span data-stu-id="316a9-193">A new container is then started using the image and runs your Node.js app based on the latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="316a9-194">Testare la pipeline</span><span class="sxs-lookup"><span data-stu-id="316a9-194">Test your pipeline</span></span>
<span data-ttu-id="316a9-195">Per visualizzare l'intera pipeline in azione, modificare nuovamente il file *index.js* nel repository GitHub con fork e fare clic su **Commit change** (Esegui il commit della modifica).</span><span class="sxs-lookup"><span data-stu-id="316a9-195">To see the whole pipeline in action, edit the *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="316a9-196">Viene avviato un nuovo processo in Jenkins in base al webhook per GitHub.</span><span class="sxs-lookup"><span data-stu-id="316a9-196">A new job starts in Jenkins based on the webhook for GitHub.</span></span> <span data-ttu-id="316a9-197">Potrebbero essere necessari alcuni secondi per creare l'immagine Docker e avviare l'app in un nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="316a9-197">It takes a few seconds to create the Docker image and start your app in a new container.</span></span>

<span data-ttu-id="316a9-198">Se necessario, ottenere nuovamente l'indirizzo IP pubblico della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="316a9-198">If needed, obtain the public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="316a9-199">Aprire un Web browser e immettere `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="316a9-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="316a9-200">Viene visualizzata l'app Node.js che rispecchia gli ultimi commit nel fork GitHub come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="316a9-200">Your Node.js app is displayed and reflects the latest commits in your GitHub fork as follows:</span></span>

![Esecuzione dell'app Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="316a9-202">Apportare un'altra modifica al file *index.js* in GitHub ed eseguire il commit della modifica.</span><span class="sxs-lookup"><span data-stu-id="316a9-202">Now make another edit to the *index.js* file in GitHub and commit the change.</span></span> <span data-ttu-id="316a9-203">Attendere alcuni secondi per il completamento del processo in Jenkins, quindi aggiornare il Web browser per visualizzare la versione aggiornata dell'app in esecuzione in un nuovo contenitore come segue:</span><span class="sxs-lookup"><span data-stu-id="316a9-203">Wait a few seconds for the job to complete in Jenkins, then refresh your web browser to see the updated version of your app running in a new container as follows:</span></span>

![Esecuzione dell'app Node.js dopo un altro commit GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="316a9-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="316a9-205">Next steps</span></span>
<span data-ttu-id="316a9-206">In questa esercitazione è stato configurato GitHub per eseguire un processo di compilazione Jenkins in ogni commit di codice e quindi distribuire un contenitore Docker per testare l'app.</span><span class="sxs-lookup"><span data-stu-id="316a9-206">In this tutorial, you configured GitHub to run a Jenkins build job on each code commit and then deploy a Docker container to test your app.</span></span> <span data-ttu-id="316a9-207">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="316a9-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="316a9-208">Creare una macchina virtuale Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="316a9-209">Installare e configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="316a9-210">Creare un'integrazione webhook tra GitHub e Jenkins</span><span class="sxs-lookup"><span data-stu-id="316a9-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="316a9-211">Creare e attivare processi di compilazione Jenkins da commit GitHub</span><span class="sxs-lookup"><span data-stu-id="316a9-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="316a9-212">Creare un'immagine Docker per l'app</span><span class="sxs-lookup"><span data-stu-id="316a9-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="316a9-213">Verificare che i commit GitHub compilino una nuova immagine Docker e gli aggiornamenti che eseguono l'app</span><span class="sxs-lookup"><span data-stu-id="316a9-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="316a9-214">Passare all'esercitazione successiva per ottenere altre informazioni su come integrare Jenkins con Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="316a9-214">Advance to the next tutorial to learn more about how to integrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="316a9-215">Deploy apps with Jenkins and Team Services (Distribuire app con Jenkins e Team Services)</span><span class="sxs-lookup"><span data-stu-id="316a9-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)