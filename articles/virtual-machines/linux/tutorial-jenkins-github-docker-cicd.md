---
title: una pipeline di sviluppo in Azure con Jenkins aaaCreate | Documenti Microsoft
description: Informazioni su come computer toocreate un Jenkins virtuale in Azure che esegue il pull da GitHub in ciascun codice eseguire il commit e compila una nuovo Docker toorun contenitore dell'app
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
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="dacdb-103">Come toocreate un'infrastruttura di sviluppo in una VM Linux in Azure con Jenkins, GitHub e Docker</span><span class="sxs-lookup"><span data-stu-id="dacdb-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="dacdb-104">tooautomate hello compilazione e test fase dello sviluppo di applicazioni, è possibile utilizzare un'integrazione continua e la pipeline di distribuzione (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="dacdb-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="dacdb-105">In questa esercitazione viene creata una pipeline CI/CD in una macchina virtuale di Azure e viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="dacdb-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dacdb-106">Creare una macchina virtuale Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="dacdb-107">Installare e configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="dacdb-108">Creare un'integrazione webhook tra GitHub e Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="dacdb-109">Creare e attivare processi di compilazione Jenkins da commit GitHub</span><span class="sxs-lookup"><span data-stu-id="dacdb-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="dacdb-110">Creare un'immagine Docker per l'app</span><span class="sxs-lookup"><span data-stu-id="dacdb-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="dacdb-111">Verificare che i commit GitHub compilino una nuova immagine Docker e gli aggiornamenti che eseguono l'app</span><span class="sxs-lookup"><span data-stu-id="dacdb-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dacdb-112">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="dacdb-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="dacdb-113">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="dacdb-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dacdb-114">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dacdb-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="dacdb-115">Creare l'istanza di Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-115">Create Jenkins instance</span></span>
<span data-ttu-id="dacdb-116">Nell'esercitazione precedente su [come toocustomize una macchina virtuale Linux al primo avvio](tutorial-automate-vm-deployment.md), si è appreso tooautomate personalizzazione con cloud init.</span><span class="sxs-lookup"><span data-stu-id="dacdb-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="dacdb-117">Questa esercitazione viene utilizzato un cloud init file tooinstall Jenkins e Docker in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dacdb-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="dacdb-118">Nella shell corrente, creare un file denominato *cloud init.txt* e Incolla hello seguente configurazione.</span><span class="sxs-lookup"><span data-stu-id="dacdb-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="dacdb-119">Ad esempio, creare file hello in hello Shell Cloud non presenti nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="dacdb-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="dacdb-120">Immettere `sensible-editor cloud-init-jenkins.txt` toocreate hello file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="dacdb-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="dacdb-121">Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:</span><span class="sxs-lookup"><span data-stu-id="dacdb-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="dacdb-122">Per poter creare una macchina virtuale è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="dacdb-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="dacdb-123">esempio Hello crea un gruppo di risorse denominato *myResourceGroupJenkins* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="dacdb-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="dacdb-124">Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="dacdb-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="dacdb-125">Hello utilizzare `--custom-data` toopass parametro nel file di configurazione cloud init.</span><span class="sxs-lookup"><span data-stu-id="dacdb-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="dacdb-126">Fornire il percorso completo di hello troppo*cloud-init-jenkins.txt* se è stato salvato il file hello all'esterno delle directory di lavoro attuale.</span><span class="sxs-lookup"><span data-stu-id="dacdb-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="dacdb-127">Sono necessari alcuni minuti per hello VM toobe creato e configurato.</span><span class="sxs-lookup"><span data-stu-id="dacdb-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="dacdb-128">tooallow web tooreach traffico la macchina virtuale, utilizzare [az vm aprire porte](/cli/azure/vm#open-port) tooopen porta *8080* per il traffico di Jenkins e porta *1337* per hello app Node.js toorun usato un'app di esempio:</span><span class="sxs-lookup"><span data-stu-id="dacdb-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="dacdb-129">Configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-129">Configure Jenkins</span></span>
<span data-ttu-id="dacdb-130">tooaccess il Jenkins dell'istanza, ottenere l'indirizzo IP pubblico hello della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="dacdb-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="dacdb-131">Per motivi di sicurezza, è necessario tooenter hello iniziale amministratore la password viene archiviata in un file di testo nel hello toostart VM che installare Jenkins.</span><span class="sxs-lookup"><span data-stu-id="dacdb-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="dacdb-132">Utilizzare l'indirizzo IP pubblico hello ottenuto nel hello precedente passaggio tooSSH tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="dacdb-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="dacdb-133">Hello vista `initialAdminPassword` per il Jenkins installare e copiarlo:</span><span class="sxs-lookup"><span data-stu-id="dacdb-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="dacdb-134">Se il file hello non è ancora disponibile, attendere alcuni minuti per cloud init toocomplete hello Jenkins e installazione di Docker.</span><span class="sxs-lookup"><span data-stu-id="dacdb-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="dacdb-135">Aprire un web browser e andare troppo`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="dacdb-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="dacdb-136">Completare l'installazione di Jenkins iniziale hello come segue:</span><span class="sxs-lookup"><span data-stu-id="dacdb-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="dacdb-137">Immettere hello *initialAdminPassword* ottenuto da hello VM nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="dacdb-138">Fare clic su **selezionare tooinstall plug-in**</span><span class="sxs-lookup"><span data-stu-id="dacdb-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="dacdb-139">Cercare *GitHub* nella casella di testo hello in alto di hello, selezionare hello *plug-in GitHub*, quindi fare clic su **installare**</span><span class="sxs-lookup"><span data-stu-id="dacdb-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="dacdb-140">un account utente di Jenkins, toocreate compilare hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="dacdb-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="dacdb-141">Da una prospettiva di sicurezza, è necessario creare il primo utente di Jenkins anziché continuare come account di amministrazione di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="dacdb-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="dacdb-142">Al termine, fare clic su **Start using Jenkins** (Inizia a usare Jenkins).</span><span class="sxs-lookup"><span data-stu-id="dacdb-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="dacdb-143">Creare webhook di GitHub</span><span class="sxs-lookup"><span data-stu-id="dacdb-143">Create GitHub webhook</span></span>
<span data-ttu-id="dacdb-144">integrazione di hello tooconfigure con GitHub, aprire hello [app di esempio HelloWorld Node.js](https://github.com/Azure-Samples/nodejs-docs-hello-world) dal repository di esempi di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="dacdb-145">toofork hello repository tooyour proprietari di account GitHub, fare clic su hello **Fork** pulsante nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="dacdb-146">Creare un webhook all'interno di divisione hello è stato creato:</span><span class="sxs-lookup"><span data-stu-id="dacdb-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="dacdb-147">Fare clic su **impostazioni**, quindi selezionare **servizi e integrazioni** sul lato sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="dacdb-148">Fare clic su **Add service** (Aggiungi servizio) e quindi immettere *Jenkins* nella casella del filtro.</span><span class="sxs-lookup"><span data-stu-id="dacdb-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="dacdb-149">Selezionare *Jenkins (GitHub plugin)* (Jenkins (plug-in GitHub)).</span><span class="sxs-lookup"><span data-stu-id="dacdb-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="dacdb-150">Per hello **Jenkins hook URL**, immettere `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="dacdb-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="dacdb-151">Assicurarsi di includere hello finali /</span><span class="sxs-lookup"><span data-stu-id="dacdb-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="dacdb-152">Fare clic su **Add service** (Aggiungi servizio).</span><span class="sxs-lookup"><span data-stu-id="dacdb-152">Click **Add service**</span></span>

![Aggiungi repository di GitHub webhook tooyour duplicata](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="dacdb-154">Creare un processo di Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-154">Create Jenkins job</span></span>
<span data-ttu-id="dacdb-155">toohave Jenkins tooan evento respond in GitHub, ad esempio l'esecuzione del commit di codice, creare un processo di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="dacdb-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="dacdb-156">Nel sito Web Jenkins, fare clic su **creare nuovi processi** dalla home page di hello:</span><span class="sxs-lookup"><span data-stu-id="dacdb-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="dacdb-157">Immettere *HelloWorld* come nome del processo.</span><span class="sxs-lookup"><span data-stu-id="dacdb-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="dacdb-158">Scegliere **Freestyle project** (Progetto Freestyle) e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="dacdb-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="dacdb-159">In hello **generale** selezionare **GitHub** del progetto e immettere l'URL di repository con fork, ad esempio *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="dacdb-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="dacdb-160">In hello **gestione del codice sorgente** selezionare **Git**, immettere il repository con fork *GIT* URL, ad esempio *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="dacdb-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="dacdb-161">In hello **trigger di compilazione** selezionare **trigger hook GitHub per il polling GITscm**.</span><span class="sxs-lookup"><span data-stu-id="dacdb-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="dacdb-162">In hello **compilare** , scegliere **istruzione di compilazione Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dacdb-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="dacdb-163">Selezionare **eseguire shell**, quindi immettere `echo "Testing"` nella finestra toocommand.</span><span class="sxs-lookup"><span data-stu-id="dacdb-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="dacdb-164">Fare clic su **salvare** nella parte inferiore di hello della finestra processi hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="dacdb-165">Testare l'integrazione di GitHub</span><span class="sxs-lookup"><span data-stu-id="dacdb-165">Test GitHub integration</span></span>
<span data-ttu-id="dacdb-166">hello tootest integrazione GitHub con Jenkins, eseguire il commit di una modifica nel fork.</span><span class="sxs-lookup"><span data-stu-id="dacdb-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="dacdb-167">In GitHub interfaccia utente web, selezionare il repository con fork e quindi fare clic su hello **index.js** file.</span><span class="sxs-lookup"><span data-stu-id="dacdb-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="dacdb-168">Fare clic su hello matita icona tooedit questo file in modo che sia di riga 6:</span><span class="sxs-lookup"><span data-stu-id="dacdb-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="dacdb-169">toocommit le modifiche, fare clic su hello **Commit delle modifiche** pulsante nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="dacdb-170">In Jenkins, viene avviata una nuova compilazione hello **compilare cronologia** sezione dell'angolo hello inferiore sinistro della pagina di processo.</span><span class="sxs-lookup"><span data-stu-id="dacdb-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="dacdb-171">Fare clic su collegamento numero di build hello e selezionare **output di Console** sulle dimensioni di hello a sinistra.</span><span class="sxs-lookup"><span data-stu-id="dacdb-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="dacdb-172">È possibile visualizzare i passaggi di hello Jenkins accetta come il codice viene effettuato il pull da GitHub e hello compilazione azione output messaggio hello `Testing` toohello console.</span><span class="sxs-lookup"><span data-stu-id="dacdb-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="dacdb-173">Ogni volta che viene eseguita un'operazione di commit in GitHub, hello webhook raggiunge tooJenkins e attivare una nuova compilazione in questo modo.</span><span class="sxs-lookup"><span data-stu-id="dacdb-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="dacdb-174">Definire l'immagine di compilazione di Docker</span><span class="sxs-lookup"><span data-stu-id="dacdb-174">Define Docker build image</span></span>
<span data-ttu-id="dacdb-175">app Node.js di hello toosee in base al commit di GitHub, consente di compilare una Docker immagine toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="dacdb-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="dacdb-176">immagine di Hello viene creato da un Dockerfile che definisce la modalità tooconfigure hello contenitore che esegue l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="dacdb-177">Dalla connessione SSH hello tooyour macchina virtuale, spostarsi toohello Jenkins dell'area di lavoro denominato dopo il processo di hello creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="dacdb-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="dacdb-178">In questo esempio è stata denominata *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="dacdb-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="dacdb-179">Crea un file in questa directory dell'area di lavoro con `sudo sensible-editor Dockerfile` e Incolla hello seguendo contenuto.</span><span class="sxs-lookup"><span data-stu-id="dacdb-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="dacdb-180">Verificare che hello che dockerfile intero viene copiato correttamente, soprattutto hello prima riga:</span><span class="sxs-lookup"><span data-stu-id="dacdb-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="dacdb-181">Questo Dockerfile utilizza hello Node.js immagine di base con Linux Alpine porta espone 1337 hello World Hello app viene eseguita, quindi copia i file di applicazione hello e la inizializza.</span><span class="sxs-lookup"><span data-stu-id="dacdb-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="dacdb-182">Creare regole di compilazione di Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-182">Create Jenkins build rules</span></span>
<span data-ttu-id="dacdb-183">In un passaggio precedente, è creata una regola di compilazione Jenkins base che una console toohello messaggio di output.</span><span class="sxs-lookup"><span data-stu-id="dacdb-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="dacdb-184">Consente di creare i Dockerfile di hello compilazione passaggio toouse ed eseguire app hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="dacdb-185">Indietro nell'istanza di Jenkins, selezionare il processo di hello creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="dacdb-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="dacdb-186">Fare clic su **configura** sul lato sinistro di hello e scorrere verso il basso toohello **compilare** sezione:</span><span class="sxs-lookup"><span data-stu-id="dacdb-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="dacdb-187">Rimuovere l'istruzione di compilazione `echo "Test"` esistente.</span><span class="sxs-lookup"><span data-stu-id="dacdb-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="dacdb-188">Fare clic su rosso incrociato in hello angolo superiore destro della casella passaggio di compilazione esistente hello hello.</span><span class="sxs-lookup"><span data-stu-id="dacdb-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="dacdb-189">Fare clic su **Add build step** (Aggiungi istruzione di compilazione) e quindi selezionare **Execute shell** (Esegui shell).</span><span class="sxs-lookup"><span data-stu-id="dacdb-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="dacdb-190">In hello **comando** casella, immettere i seguenti comandi di Docker hello, quindi selezionare **salvare**:</span><span class="sxs-lookup"><span data-stu-id="dacdb-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="dacdb-191">istruzioni di compilazione Docker Hello creare un'immagine e un tag con hello Jenkins numero di build di conservare una cronologia delle immagini.</span><span class="sxs-lookup"><span data-stu-id="dacdb-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="dacdb-192">Qualsiasi contenitore esistente in esecuzione app hello vengono arrestate e quindi rimosso.</span><span class="sxs-lookup"><span data-stu-id="dacdb-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="dacdb-193">Un nuovo contenitore è stata avviata tramite immagine hello e viene eseguita l'app Node.js in base a commit più recente di hello in GitHub.</span><span class="sxs-lookup"><span data-stu-id="dacdb-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="dacdb-194">Testare la pipeline</span><span class="sxs-lookup"><span data-stu-id="dacdb-194">Test your pipeline</span></span>
<span data-ttu-id="dacdb-195">pipeline di intero hello toosee in azione, modificare hello *index.js* nuovamente il file nel repository di GitHub con fork e fare clic su **il Commit delle modifiche**.</span><span class="sxs-lookup"><span data-stu-id="dacdb-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="dacdb-196">Un nuovo processo viene avviato in Jenkins basati su hello webhook per GitHub.</span><span class="sxs-lookup"><span data-stu-id="dacdb-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="dacdb-197">Accetta alcuni secondi immagine di Docker toocreate hello e avviare l'app in un nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="dacdb-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="dacdb-198">Se necessario, è possibile ottenere nuovo indirizzo IP pubblico hello della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="dacdb-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="dacdb-199">Aprire un Web browser e immettere `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="dacdb-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="dacdb-200">App Node.js viene visualizzato e riflette commit più recente hello nel fork GitHub come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="dacdb-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Esecuzione dell'app Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="dacdb-202">Creare un'altra modifica toohello *index.js* file modifica hello GitHub e il commit.</span><span class="sxs-lookup"><span data-stu-id="dacdb-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="dacdb-203">Attendere alcuni secondi per toocomplete processo hello in Jenkins, quindi aggiornare la versione del web browser toosee hello aggiornata dell'app in esecuzione in un nuovo contenitore, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="dacdb-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Esecuzione dell'app Node.js dopo un altro commit GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="dacdb-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dacdb-205">Next steps</span></span>
<span data-ttu-id="dacdb-206">In questa esercitazione, è configurato GitHub toorun un processo di compilazione Jenkins in ogni caso di commit di codice e quindi distribuire un tootest contenitore Docker dell'app.</span><span class="sxs-lookup"><span data-stu-id="dacdb-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="dacdb-207">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="dacdb-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dacdb-208">Creare una macchina virtuale Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="dacdb-209">Installare e configurare Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="dacdb-210">Creare un'integrazione webhook tra GitHub e Jenkins</span><span class="sxs-lookup"><span data-stu-id="dacdb-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="dacdb-211">Creare e attivare processi di compilazione Jenkins da commit GitHub</span><span class="sxs-lookup"><span data-stu-id="dacdb-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="dacdb-212">Creare un'immagine Docker per l'app</span><span class="sxs-lookup"><span data-stu-id="dacdb-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="dacdb-213">Verificare che i commit GitHub compilino una nuova immagine Docker e gli aggiornamenti che eseguono l'app</span><span class="sxs-lookup"><span data-stu-id="dacdb-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="dacdb-214">Spostare toolearn esercitazione successiva toohello ulteriori informazioni su toointegrate Jenkins con Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="dacdb-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dacdb-215">Deploy apps with Jenkins and Team Services (Distribuire app con Jenkins e Team Services)</span><span class="sxs-lookup"><span data-stu-id="dacdb-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)