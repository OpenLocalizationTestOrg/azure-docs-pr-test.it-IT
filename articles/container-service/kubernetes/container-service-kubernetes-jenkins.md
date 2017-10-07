---
title: aaaJenkins CI/CD con Kubernetes contenitore nel servizio di Azure | Documenti Microsoft
description: Come un elemento di configurazione/CD tooautomate elaborare con Jenkins toodeploy e aggiornare un'app nei contenitori su Kubernetes nel servizio contenitore di Azure
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
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="ed4ae-104">Integrazione di Jenkins con il servizio contenitore di Azure e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ed4ae-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="ed4ae-105">In questa esercitazione vengono illustrate le hello tooset di processo di integrazione continua di un'applicazione multi-contenitore in Kubernetes servizio contenitore di Azure usando hello Jenkins piattaforma.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="ed4ae-106">flusso di lavoro Hello immagine contenitore hello nell'Hub Docker e POD Kubernetes hello tramite un'implementazione della distribuzione di aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="ed4ae-107">Processo principale</span><span class="sxs-lookup"><span data-stu-id="ed4ae-107">High level process</span></span>
<span data-ttu-id="ed4ae-108">i passaggi di base Hello descritti in dettaglio in questo articolo sono:</span><span class="sxs-lookup"><span data-stu-id="ed4ae-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="ed4ae-109">Installare un cluster Kubernetes nel servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="ed4ae-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="ed4ae-110">Impostare Jenkins e configurare accesso tooContainer servizio</span><span class="sxs-lookup"><span data-stu-id="ed4ae-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="ed4ae-111">Creare un flusso di lavoro Jenkins</span><span class="sxs-lookup"><span data-stu-id="ed4ae-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="ed4ae-112">Test hello CI/CD processo end tooend</span><span class="sxs-lookup"><span data-stu-id="ed4ae-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="ed4ae-113">Installare un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ed4ae-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="ed4ae-114">Distribuire cluster Kubernetes hello nel servizio di contenitore di Azure tramite hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="ed4ae-115">La documentazione completa è disponibile [qui](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="ed4ae-116">Passaggio 1: Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ed4ae-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="ed4ae-117">Passaggio 2: Distribuire cluster hello</span><span class="sxs-lookup"><span data-stu-id="ed4ae-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="ed4ae-118">Hello i passaggi seguenti richiedono una locale memorizzata nella cartella ~/.ssh hello a chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
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

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="ed4ae-119">Impostare Jenkins e configurare accesso tooContainer servizio</span><span class="sxs-lookup"><span data-stu-id="ed4ae-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="ed4ae-120">Passaggio 1: Installare Jenkins</span><span class="sxs-lookup"><span data-stu-id="ed4ae-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="ed4ae-121">Creare una macchina virtuale di Azure con Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="ed4ae-122">Poiché i passaggi più avanti in hello è sarà necessario tooconnect toothis macchina virtuale con bash nel computer locale, chiave pubblica too'SSH set hello 'Tipo di autenticazione' ' e Incolla hello la chiave pubblica SSH archiviati localmente nella cartella ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="ed4ae-123">Inoltre, prendere nota di hello 'Nome utente' specificato poiché il nome utente sarà dashboard di Jenkins hello tooview necessarie e per la connessione toohello Jenkins VM nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="ed4ae-124">Installare Jenkins tramite queste [istruzioni](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="ed4ae-125">Un'esercitazione più dettagliata è disponibile all'indirizzo [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="ed4ae-126">tooview hello Jenkins dashboard sul computer locale, aggiornare hello Azure rete sicurezza gruppo tooallow porta 8080 mediante l'aggiunta di una regola in ingresso che consente accesso tooport 8080.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="ed4ae-127">In alternativa è possibile impostare il port forwarding eseguendo questo comando: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="ed4ae-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="ed4ae-128">Connessione server Jenkins tooyour tramite browser hello passando l'indirizzo IP pubblico toohello (http:// < your_jenkins_public_ip >: 8080) e sbloccare dashboard Jenkins hello per hello prima volta con password di amministratore iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="ed4ae-129">password amministratore Hello viene archiviata in /var/lib/jenkins/secrets/initialAdminPassword su hello Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="ed4ae-130">Un modo semplice di tooget questa password è tooSSH in hello VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="ed4ae-131">Quindi eseguire: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="ed4ae-132">Installare Docker nella macchina di Jenkins hello tramite questi [istruzioni](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="ed4ae-133">In questo modo toobe i comandi di Docker eseguiti in processi di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="ed4ae-134">Configurare Docker autorizzazioni tooallow Jenkins tooaccess hello Docker endpoint.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="ed4ae-135">Installare l'interfaccia della riga di comando `kubectl` in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="ed4ae-136">Altre informazioni sono disponibili leggendo l'articolo sull'[installazione e la configurazione di kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="ed4ae-137">I processi di Jenkins verranno utilizzata toomanage 'kubectl' e distribuire toohello Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="ed4ae-138">Passaggio 2: Configurazione di cluster Kubernetes toohello di accesso</span><span class="sxs-lookup"><span data-stu-id="ed4ae-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="ed4ae-139">Esistono più hello tooaccomplishing di approcci alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="ed4ae-140">Utilizzare l'approccio hello è più semplice per l'utente.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="ed4ae-141">Hello copia `kubectl` toohello di file di configurazione Jenkins macchina in modo che i processi di Jenkins cluster Kubernetes toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="ed4ae-142">Queste istruzioni presuppongono che si sta utilizzando bash da un computer diverso rispetto a hello Jenkins VM e che una chiave pubblica SSH locale viene archiviata nella cartella ~/.ssh della macchina hello.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="ed4ae-143">Convalidare da Jenkins che hello Kubernetes cluster sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="ed4ae-144">toodo, SSH in hello VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="ed4ae-145">Successivamente, verificare Jenkins può connettersi cluster tooyour: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="ed4ae-146">Creare un flusso di lavoro Jenkins</span><span class="sxs-lookup"><span data-stu-id="ed4ae-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ed4ae-147">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ed4ae-147">Prerequisites</span></span>

- <span data-ttu-id="ed4ae-148">Account GitHub per il repository di codice.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="ed4ae-149">Docker Hub account toostore e aggiornare le immagini.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="ed4ae-150">Applicazione in contenitore, ricompilabile e aggiornabile.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="ed4ae-151">È possibile usare questa applicazione contenitore di esempio scritta in Golang: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="ed4ae-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="ed4ae-152">Hello seguenti passaggi devono essere eseguiti nell'account GitHub.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="ed4ae-153">Possibile hello tooclone disponibile di sopra di repository, ma è necessario utilizzare il propria webhook hello tooconfigure di account e accedere a Jenkins.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="ed4ae-154">Passaggio 1: Distribuire la versione 1 iniziale dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ed4ae-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="ed4ae-155">Compilazione dell'applicazione hello computer dello sviluppatore hello con hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="ed4ae-156">Sostituire `myrepo` con la propria.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="ed4ae-157">Push immagine tooDocker Hub.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="ed4ae-158">Distribuire toohello Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ed4ae-159">Modifica hello `go-web.yaml` file tooupdate l'immagine contenitore e il repository.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="ed4ae-160">Passaggio 2: Configurare il sistema Jenkins</span><span class="sxs-lookup"><span data-stu-id="ed4ae-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="ed4ae-161">Fare clic su **Manage Jenkins (Gestisci Jenkins)** > **Configure System (Configura sistema)**.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="ed4ae-162">In **GitHub**selezionare **Add GitHub Server** (Aggiungi server GitHub).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="ed4ae-163">Lasciare il campo **API URL** come predefinito.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="ed4ae-164">In **Credenziali**, aggiungere una credenziale Jenkins usando **Secret text** (Testo segreto).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="ed4ae-165">Si consiglia di usare i token di accesso a GitHub personali, configurati nelle impostazioni dell'account utente GitHub.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="ed4ae-166">Altre informazioni a riguardo sono disponibili [qui.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="ed4ae-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="ed4ae-167">Fare clic su **Test della connessione** tooensure questo sia configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="ed4ae-168">In **Proprietà globali** aggiungere una variabile di ambiente `DOCKER_HUB` e indicare la password di Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="ed4ae-169">Questa operazione è utile per questa demo, ma uno scenario di produzione richiederà un approccio più sicuro.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="ed4ae-170">Salvare.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-170">Save.</span></span>

![Accesso GitHub a Jenkins](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="ed4ae-172">Passaggio 3: Creazione del flusso di lavoro di hello Jenkins</span><span class="sxs-lookup"><span data-stu-id="ed4ae-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="ed4ae-173">Creare un elemento Jenkins.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="ed4ae-174">Specificare un nome (ad esempio, "go-web") e selezionare **Freestyle Project** (Progetto Freestyle).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="ed4ae-175">Controllare **GitHub progetto** e fornire repository di GitHub tooyour URL hello.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="ed4ae-176">In **gestione del codice sorgente**, fornire l'URL di repository GitHub hello e le credenziali.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="ed4ae-177">Aggiungere un **istruzione di compilazione** di tipo **eseguire shell** e utilizzare hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="ed4ae-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="ed4ae-178">Aggiungere un altro **istruzione di compilazione** di tipo **eseguire shell** e utilizzare hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="ed4ae-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Passaggi di compilazione in Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="ed4ae-180">Salvare l'elemento Jenkins hello e verificare con **compilare ora**.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="ed4ae-181">Passaggio 4: Connettere il webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="ed4ae-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="ed4ae-182">Nell'elemento Jenkins hello creato, fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="ed4ae-183">In **Build Triggers** (Trigger di compilazione), selezionare l'opzione **GitHub hook trigger for GITScm polling** (Trigger di hook GitHub per polling GITScm) e **salvare**.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="ed4ae-184">Verrà automaticamente configurato hello GitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="ed4ae-185">Nel repository di GitHub per go-web, fare clic su **Impostazioni > Webhook**.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="ed4ae-186">Verificare che hello webhook Jenkins URL è stato aggiunto correttamente.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="ed4ae-187">URL di Hello deve terminare in "github webhook".</span><span class="sxs-lookup"><span data-stu-id="ed4ae-187">hello URL should end in "github-webhook".</span></span>

![Configurazione del webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="ed4ae-189">Test hello CI/CD processo end tooend</span><span class="sxs-lookup"><span data-stu-id="ed4ae-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="ed4ae-190">Aggiornare il codice per il repository di hello e push/sincronizzazione con il repository di GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="ed4ae-191">Dalla console di Jenkins hello, controllare hello **cronologia compilare** e convalidare tale hello esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="ed4ae-192">Visualizzare i dettagli toosee output console.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-192">View console output toosee details.</span></span>
3. <span data-ttu-id="ed4ae-193">Da Kubernetes, visualizzare i dettagli di hello aggiornamento distribuzione:</span><span class="sxs-lookup"><span data-stu-id="ed4ae-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="ed4ae-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed4ae-194">Next steps</span></span>

- <span data-ttu-id="ed4ae-195">Distribuire un Registro di sistema del contenitore di Azure e archiviare le immagini in un repository sicuro.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="ed4ae-196">Vedere la [documentazione sul Registro di sistema del contenitore di Azure](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="ed4ae-197">Creare un flusso di lavoro più complesso che includa la distribuzione affiancata e i test automatizzati in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="ed4ae-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="ed4ae-198">Per ulteriori informazioni sull'elemento di configurazione/CD con Jenkins e Kubernetes, vedere hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="ed4ae-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
