---
title: CI/CD di Jenkins con Kubernetes nel servizio contenitore di Azure | Microsoft Docs
description: Come automatizzare un processo CI/CD con Jenkins per distribuire e aggiornare un'app dei contenitori in Kubernetes nel servizio contenitore di Azure
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: Docker, contenitori, Kubernetes, Azure, Jenkins
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: 2078d0694fc4dd6e83ecd2792588b4254980cd78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="25403-104">Integrazione di Jenkins con il servizio contenitore di Azure e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="25403-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="25403-105">Questa esercitazione illustra il processo per impostare l'integrazione continuata di un'applicazione multi-contenitore nel servizio contenitore di Azure Kubernetes usando la piattaforma Jenkins.</span><span class="sxs-lookup"><span data-stu-id="25403-105">In this tutorial, we walk through the process to set up continuous integration of a multi-container application into Azure Container Service Kubernetes using the Jenkins platform.</span></span> <span data-ttu-id="25403-106">Il flusso di lavoro aggiorna l'immagine del contenitore in Docker Hub e i podcast Kubernetes implementando la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="25403-106">The workflow updates the container image in Docker Hub and upgrades the Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="25403-107">Processo principale</span><span class="sxs-lookup"><span data-stu-id="25403-107">High level process</span></span>
<span data-ttu-id="25403-108">I passaggi di base descritti in questo articolo sono:</span><span class="sxs-lookup"><span data-stu-id="25403-108">The basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="25403-109">Installare un cluster Kubernetes nel servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="25403-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="25403-110">Impostare Jenkins e configurare l'accesso al servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="25403-110">Set up Jenkins and configure access to Container Service</span></span>
- <span data-ttu-id="25403-111">Creare un flusso di lavoro Jenkins</span><span class="sxs-lookup"><span data-stu-id="25403-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="25403-112">Testare il processo CI/CD end-to-end</span><span class="sxs-lookup"><span data-stu-id="25403-112">Test the CI/CD process end to end</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="25403-113">Installare un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="25403-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="25403-114">Distribuire il cluster Kubernetes nel servizio contenitore di Azure seguendo questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="25403-114">Deploy the Kubernetes cluster in Azure Container Service using the following steps.</span></span> <span data-ttu-id="25403-115">La documentazione completa è disponibile [qui](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="25403-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="25403-116">Passaggio 1: Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="25403-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-the-cluster"></a><span data-ttu-id="25403-117">Passaggio 2: Distribuire il cluster</span><span class="sxs-lookup"><span data-stu-id="25403-117">Step 2: Deploy the cluster</span></span>
> [!NOTE]
> <span data-ttu-id="25403-118">Le operazioni seguenti richiedono una chiave pubblica SSH locale archiviata nella cartella ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="25403-118">The following steps require a local SSH public key stored in the ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-to-container-service"></a><span data-ttu-id="25403-119">Impostare Jenkins e configurare l'accesso al servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="25403-119">Set up Jenkins and configure access to Container Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="25403-120">Passaggio 1: Installare Jenkins</span><span class="sxs-lookup"><span data-stu-id="25403-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="25403-121">Creare una macchina virtuale di Azure con Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="25403-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="25403-122">Poiché in seguito in questa procedura sarà necessario connettersi a questa VM mediante bash nel computer locale, impostare "Tipo di autenticazione" su "Chiave pubblica SSH" e incollare la chiave pubblica SSH archiviata localmente nella cartella ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="25403-122">Since later in the steps you will need to connect to this VM using bash on your local machine, set the 'Authentication type' to 'SSH public key' and paste the SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="25403-123">Inoltre, prendere nota del "Nome utente" che si specifica poiché sarà necessario per visualizzare il dashboard Jenkins e per la connessione alla VM Jenkins nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="25403-123">Also, take note of the 'User name' that you specify since this user name will be needed to view the Jenkins dashboard and for connecting to the Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="25403-124">Installare Jenkins tramite queste [istruzioni](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="25403-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="25403-125">Un'esercitazione più dettagliata è disponibile all'indirizzo [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="25403-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="25403-126">Per visualizzare il dashboard Jenkins sul computer locale, aggiornare il gruppo di sicurezza di rete di Azure per consentire la porta 8080 mediante l'aggiunta di una regola in ingresso che consente l'accesso alla porta 8080.</span><span class="sxs-lookup"><span data-stu-id="25403-126">To view the Jenkins dashboard on your local machine, update the Azure network security group to allow port 8080 by adding an inbound rule that allows access to port 8080.</span></span>  <span data-ttu-id="25403-127">In alternativa è possibile impostare il port forwarding eseguendo questo comando: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="25403-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="25403-128">Connettersi al server Jenkins mediante il browser accedendo all'indirizzo IP pubblico (http://<your_jenkins_public_ip>:8080) e sbloccare il dashboard Jenkins per la prima volta con la password di amministrazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="25403-128">Connect to your Jenkins server using the browser by navigating to the public IP (http://<your_jenkins_public_ip>:8080) and unlock the Jenkins dashboard for the first time with the initial admin password.</span></span>  <span data-ttu-id="25403-129">La password di amministrazione iniziale è archiviata in /var/lib/jenkins/secrets/initialAdminPassword nella VM Jenkins.</span><span class="sxs-lookup"><span data-stu-id="25403-129">The admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on the Jenkins VM.</span></span>  <span data-ttu-id="25403-130">Un modo semplice per ottenere la password è stabilire una connessione SSH alla VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="25403-130">An easy way to get this password is to SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="25403-131">Quindi eseguire: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="25403-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="25403-132">Installare Docker nel computer Jenkins tramite queste [istruzioni](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="25403-132">Install Docker on the Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="25403-133">In questo modo è possibile eseguire comandi Docker nei processi Jenkins.</span><span class="sxs-lookup"><span data-stu-id="25403-133">This allows for Docker commands to be run in Jenkins jobs.</span></span>
6. <span data-ttu-id="25403-134">Configurare le autorizzazioni di Docker per consentire a Jenkins di accedere all'endpoint Docker.</span><span class="sxs-lookup"><span data-stu-id="25403-134">Configure Docker permissions to allow Jenkins to access the Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="25403-135">Installare l'interfaccia della riga di comando `kubectl` in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="25403-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="25403-136">Altre informazioni sono disponibili leggendo l'articolo sull'[installazione e la configurazione di kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="25403-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="25403-137">I processi di Jenkins useranno "kubectl" per gestire e distribuire il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="25403-137">Jenkins jobs will use 'kubectl' to manage and deploy to the Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-to-the-kubernetes-cluster"></a><span data-ttu-id="25403-138">Passaggio 2: Impostare l'accesso al cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="25403-138">Step 2: Set up access to the Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="25403-139">Esistono diversi approcci per eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="25403-139">There are multiple approaches to accomplishing the following steps.</span></span> <span data-ttu-id="25403-140">Usare l'approccio che si ritiene più semplice.</span><span class="sxs-lookup"><span data-stu-id="25403-140">Use the approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="25403-141">Copiare il file di configurazione `kubectl` nel computer Jenkins, in modo che i processi Jenkins abbiano accesso al cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="25403-141">Copy the `kubectl` config file to the Jenkins machine so that Jenkins jobs have access to the Kubernetes cluster.</span></span> <span data-ttu-id="25403-142">Queste istruzioni presuppongono che si usi bash da un computer diverso rispetto alla VM Jenkins e che una chiave pubblica SSH locale sia archiviata nella cartella ~/.ssh del computer.</span><span class="sxs-lookup"><span data-stu-id="25403-142">These instructions assume that you are using bash from a different machine than the Jenkins VM and that a local SSH public key is stored in the machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="25403-143">Da Jenkins, verificare che il cluster Kubernetes sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="25403-143">Validate from Jenkins that the Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="25403-144">A tale scopo, eseguire una connessione SSH alla VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="25403-144">To do this, SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="25403-145">Quindi verificare che Jenkins possa connettersi al cluster: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="25403-145">Next, verify Jenkins can successfully connect to your cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="25403-146">Creare un flusso di lavoro Jenkins</span><span class="sxs-lookup"><span data-stu-id="25403-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="25403-147">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="25403-147">Prerequisites</span></span>

- <span data-ttu-id="25403-148">Account GitHub per il repository di codice.</span><span class="sxs-lookup"><span data-stu-id="25403-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="25403-149">Account Docker Hub per archiviare e aggiornare le immagini.</span><span class="sxs-lookup"><span data-stu-id="25403-149">Docker Hub account to store and update images.</span></span>
- <span data-ttu-id="25403-150">Applicazione in contenitore, ricompilabile e aggiornabile.</span><span class="sxs-lookup"><span data-stu-id="25403-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="25403-151">È possibile usare questa applicazione contenitore di esempio scritta in Golang: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="25403-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="25403-152">Eseguire i passaggi seguenti nel proprio account GitHub.</span><span class="sxs-lookup"><span data-stu-id="25403-152">The following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="25403-153">È possibile clonare il repository precedente, ma è necessario usare il proprio account per configurare i webhook e l'accesso a Jenkins.</span><span class="sxs-lookup"><span data-stu-id="25403-153">Feel free to clone the above repo, but you must use your own account to configure the webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="25403-154">Passaggio 1: Distribuire la versione 1 iniziale dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="25403-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="25403-155">Compilare l'applicazione dal computer per lo sviluppo con i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="25403-155">Build the app from the developer machine with the following commands.</span></span> <span data-ttu-id="25403-156">Sostituire `myrepo` con la propria.</span><span class="sxs-lookup"><span data-stu-id="25403-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="25403-157">Inviare l'immagine a Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="25403-157">Push image to Docker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="25403-158">Distribuire nel cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="25403-158">Deploy to the Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="25403-159">Modificare il file `go-web.yaml` per aggiornare l'immagine del contenitore e il repository.</span><span class="sxs-lookup"><span data-stu-id="25403-159">Edit the `go-web.yaml` file to update your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="25403-160">Passaggio 2: Configurare il sistema Jenkins</span><span class="sxs-lookup"><span data-stu-id="25403-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="25403-161">Fare clic su **Manage Jenkins (Gestisci Jenkins)** > **Configure System (Configura sistema)**.</span><span class="sxs-lookup"><span data-stu-id="25403-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="25403-162">In **GitHub**selezionare **Add GitHub Server** (Aggiungi server GitHub).</span><span class="sxs-lookup"><span data-stu-id="25403-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="25403-163">Lasciare il campo **API URL** come predefinito.</span><span class="sxs-lookup"><span data-stu-id="25403-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="25403-164">In **Credenziali**, aggiungere una credenziale Jenkins usando **Secret text** (Testo segreto).</span><span class="sxs-lookup"><span data-stu-id="25403-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="25403-165">Si consiglia di usare i token di accesso a GitHub personali, configurati nelle impostazioni dell'account utente GitHub.</span><span class="sxs-lookup"><span data-stu-id="25403-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="25403-166">Altre informazioni a riguardo sono disponibili [qui.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="25403-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="25403-167">Fare clic su **Connessione di test** per assicurarsi che la configurazione sia stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="25403-167">Click **Test connection** to ensure this is configured correctly.</span></span>
6. <span data-ttu-id="25403-168">In **Proprietà globali** aggiungere una variabile di ambiente `DOCKER_HUB` e indicare la password di Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="25403-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="25403-169">Questa operazione è utile per questa demo, ma uno scenario di produzione richiederà un approccio più sicuro.</span><span class="sxs-lookup"><span data-stu-id="25403-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="25403-170">Salvare.</span><span class="sxs-lookup"><span data-stu-id="25403-170">Save.</span></span>

![Accesso GitHub a Jenkins](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-the-jenkins-workflow"></a><span data-ttu-id="25403-172">Passaggio 3: Creare il flusso di lavoro Jenkins</span><span class="sxs-lookup"><span data-stu-id="25403-172">Step 3: Create the Jenkins workflow</span></span>
1. <span data-ttu-id="25403-173">Creare un elemento Jenkins.</span><span class="sxs-lookup"><span data-stu-id="25403-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="25403-174">Specificare un nome (ad esempio, "go-web") e selezionare **Freestyle Project** (Progetto Freestyle).</span><span class="sxs-lookup"><span data-stu-id="25403-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="25403-175">Controllare **GitHub project** (Progetto GitHub) e indicare l'URL del repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="25403-175">Check **GitHub project** and provide the URL to your GitHub repo.</span></span>
4. <span data-ttu-id="25403-176">In **Source Code Management** (Gestione codice sorgente) fornire l'URL e le credenziali del repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="25403-176">In **Source Code Management**, provide the GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="25403-177">Aggiungere un'**istruzione di compilazione** di tipo **Esegui shell** e usare il seguente testo:</span><span class="sxs-lookup"><span data-stu-id="25403-177">Add a **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="25403-178">Aggiungere un'altra **istruzione di compilazione** di tipo **Esegui shell** e usare il seguente testo:</span><span class="sxs-lookup"><span data-stu-id="25403-178">Add another **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Passaggi di compilazione in Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="25403-180">Salvare l'elemento Jenkins e testarlo con **Build Now** (Compila ora).</span><span class="sxs-lookup"><span data-stu-id="25403-180">Save the Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="25403-181">Passaggio 4: Connettere il webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="25403-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="25403-182">Nell'elemento di Jenkins creato fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="25403-182">In the Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="25403-183">In **Build Triggers** (Trigger di compilazione), selezionare l'opzione **GitHub hook trigger for GITScm polling** (Trigger di hook GitHub per polling GITScm) e **salvare**.</span><span class="sxs-lookup"><span data-stu-id="25403-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="25403-184">Verrà automaticamente configurato il webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="25403-184">This automatically configures the GitHub webhook.</span></span>
3. <span data-ttu-id="25403-185">Nel repository di GitHub per go-web, fare clic su **Impostazioni > Webhook**.</span><span class="sxs-lookup"><span data-stu-id="25403-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="25403-186">Verificare che l'URL del webhook Jenkins sia stato aggiunto correttamente.</span><span class="sxs-lookup"><span data-stu-id="25403-186">Verify that the Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="25403-187">L'URL deve terminare con "github-webhook".</span><span class="sxs-lookup"><span data-stu-id="25403-187">The URL should end in "github-webhook".</span></span>

![Configurazione del webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-the-cicd-process-end-to-end"></a><span data-ttu-id="25403-189">Testare il processo CI/CD end-to-end</span><span class="sxs-lookup"><span data-stu-id="25403-189">Test the CI/CD process end to end</span></span>

1. <span data-ttu-id="25403-190">Aggiornare il codice per il repository ed eseguire il push/sincronizzazione con il repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="25403-190">Update code for the repo and push/synch with the GitHub repository.</span></span>
2. <span data-ttu-id="25403-191">Dalla console Jenkins, controllare la **Build History** (Cronologia compilazione) e verificare l'esecuzione corretta del processo.</span><span class="sxs-lookup"><span data-stu-id="25403-191">From the Jenkins console, check the **Build History** and validate that the job has run.</span></span> <span data-ttu-id="25403-192">Visualizzazione l'output della console per i dettagli.</span><span class="sxs-lookup"><span data-stu-id="25403-192">View console output to see details.</span></span>
3. <span data-ttu-id="25403-193">Da Kubernetes, visualizzare i dettagli della distribuzione aggiornata:</span><span class="sxs-lookup"><span data-stu-id="25403-193">From Kubernetes, view details of the upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="25403-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25403-194">Next steps</span></span>

- <span data-ttu-id="25403-195">Distribuire un Registro di sistema del contenitore di Azure e archiviare le immagini in un repository sicuro.</span><span class="sxs-lookup"><span data-stu-id="25403-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="25403-196">Vedere la [documentazione sul Registro di sistema del contenitore di Azure](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="25403-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="25403-197">Creare un flusso di lavoro più complesso che includa la distribuzione affiancata e i test automatizzati in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="25403-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="25403-198">Per ulteriori informazioni su CI/CD con Jenkins e Kubernetes, vedere il [blog su Jenkins](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="25403-198">For more information about CI/CD with Jenkins and Kubernetes, see the [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
