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
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Integrazione di Jenkins con il servizio contenitore di Azure e Kubernetes 
In questa esercitazione vengono illustrate le hello tooset di processo di integrazione continua di un'applicazione multi-contenitore in Kubernetes servizio contenitore di Azure usando hello Jenkins piattaforma. flusso di lavoro Hello immagine contenitore hello nell'Hub Docker e POD Kubernetes hello tramite un'implementazione della distribuzione di aggiornamenti. 

## <a name="high-level-process"></a>Processo principale
i passaggi di base Hello descritti in dettaglio in questo articolo sono: 
- Installare un cluster Kubernetes nel servizio contenitore
- Impostare Jenkins e configurare accesso tooContainer servizio
- Creare un flusso di lavoro Jenkins
- Test hello CI/CD processo end tooend

## <a name="install-a-kubernetes-cluster"></a>Installare un cluster Kubernetes
    
Distribuire cluster Kubernetes hello nel servizio di contenitore di Azure tramite hello alla procedura seguente. La documentazione completa è disponibile [qui](container-service-kubernetes-walkthrough.md).

### <a name="step-1-create-a-resource-group"></a>Passaggio 1: Creare un gruppo di risorse
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>Passaggio 2: Distribuire cluster hello
> [!NOTE]
> Hello i passaggi seguenti richiedono una locale memorizzata nella cartella ~/.ssh hello a chiave pubblica SSH.
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

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Impostare Jenkins e configurare accesso tooContainer servizio

### <a name="step-1-install-jenkins"></a>Passaggio 1: Installare Jenkins
1. Creare una macchina virtuale di Azure con Ubuntu 16.04 LTS.  Poiché i passaggi più avanti in hello è sarà necessario tooconnect toothis macchina virtuale con bash nel computer locale, chiave pubblica too'SSH set hello 'Tipo di autenticazione' ' e Incolla hello la chiave pubblica SSH archiviati localmente nella cartella ~/.ssh.  Inoltre, prendere nota di hello 'Nome utente' specificato poiché il nome utente sarà dashboard di Jenkins hello tooview necessarie e per la connessione toohello Jenkins VM nei passaggi successivi.
2. Installare Jenkins tramite queste [istruzioni](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu). Un'esercitazione più dettagliata è disponibile all'indirizzo [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).
3. tooview hello Jenkins dashboard sul computer locale, aggiornare hello Azure rete sicurezza gruppo tooallow porta 8080 mediante l'aggiunta di una regola in ingresso che consente accesso tooport 8080.  In alternativa è possibile impostare il port forwarding eseguendo questo comando: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`
4. Connessione server Jenkins tooyour tramite browser hello passando l'indirizzo IP pubblico toohello (http:// < your_jenkins_public_ip >: 8080) e sbloccare dashboard Jenkins hello per hello prima volta con password di amministratore iniziale hello.  password amministratore Hello viene archiviata in /var/lib/jenkins/secrets/initialAdminPassword su hello Jenkins VM.  Un modo semplice di tooget questa password è tooSSH in hello VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Quindi eseguire: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
5. Installare Docker nella macchina di Jenkins hello tramite questi [istruzioni](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts). In questo modo toobe i comandi di Docker eseguiti in processi di Jenkins.
6. Configurare Docker autorizzazioni tooallow Jenkins tooaccess hello Docker endpoint.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Installare l'interfaccia della riga di comando `kubectl` in Jenkins. Altre informazioni sono disponibili leggendo l'articolo sull'[installazione e la configurazione di kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).  I processi di Jenkins verranno utilizzata toomanage 'kubectl' e distribuire toohello Kubernetes cluster.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>Passaggio 2: Configurazione di cluster Kubernetes toohello di accesso

> [!NOTE]
> Esistono più hello tooaccomplishing di approcci alla procedura seguente. Utilizzare l'approccio hello è più semplice per l'utente.
>

1. Hello copia `kubectl` toohello di file di configurazione Jenkins macchina in modo che i processi di Jenkins cluster Kubernetes toohello di accesso. Queste istruzioni presuppongono che si sta utilizzando bash da un computer diverso rispetto a hello Jenkins VM e che una chiave pubblica SSH locale viene archiviata nella cartella ~/.ssh della macchina hello.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. Convalidare da Jenkins che hello Kubernetes cluster sia accessibile.  toodo, SSH in hello VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Successivamente, verificare Jenkins può connettersi cluster tooyour: `kubectl cluster-info`.
    

## <a name="create-a-jenkins-workflow"></a>Creare un flusso di lavoro Jenkins

### <a name="prerequisites"></a>Prerequisiti

- Account GitHub per il repository di codice.
- Docker Hub account toostore e aggiornare le immagini.
- Applicazione in contenitore, ricompilabile e aggiornabile. È possibile usare questa applicazione contenitore di esempio scritta in Golang: https://github.com/chzbrgr71/go-web 

> [!NOTE]
> Hello seguenti passaggi devono essere eseguiti nell'account GitHub. Possibile hello tooclone disponibile di sopra di repository, ma è necessario utilizzare il propria webhook hello tooconfigure di account e accedere a Jenkins.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>Passaggio 1: Distribuire la versione 1 iniziale dell'applicazione
1. Compilazione dell'applicazione hello computer dello sviluppatore hello con hello i comandi seguenti. Sostituire `myrepo` con la propria.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. Push immagine tooDocker Hub.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Distribuire toohello Kubernetes cluster.
    
    > [!NOTE] 
    > Modifica hello `go-web.yaml` file tooupdate l'immagine contenitore e il repository.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>Passaggio 2: Configurare il sistema Jenkins
1. Fare clic su **Manage Jenkins (Gestisci Jenkins)** > **Configure System (Configura sistema)**.
2. In **GitHub**selezionare **Add GitHub Server** (Aggiungi server GitHub).
3. Lasciare il campo **API URL** come predefinito.
4. In **Credenziali**, aggiungere una credenziale Jenkins usando **Secret text** (Testo segreto). Si consiglia di usare i token di accesso a GitHub personali, configurati nelle impostazioni dell'account utente GitHub. Altre informazioni a riguardo sono disponibili [qui.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
5. Fare clic su **Test della connessione** tooensure questo sia configurato correttamente.
6. In **Proprietà globali** aggiungere una variabile di ambiente `DOCKER_HUB` e indicare la password di Docker Hub. Questa operazione è utile per questa demo, ma uno scenario di produzione richiederà un approccio più sicuro.
7. Salvare.

![Accesso GitHub a Jenkins](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>Passaggio 3: Creazione del flusso di lavoro di hello Jenkins
1. Creare un elemento Jenkins.
2. Specificare un nome (ad esempio, "go-web") e selezionare **Freestyle Project** (Progetto Freestyle). 
3. Controllare **GitHub progetto** e fornire repository di GitHub tooyour URL hello.
4. In **gestione del codice sorgente**, fornire l'URL di repository GitHub hello e le credenziali. 
5. Aggiungere un **istruzione di compilazione** di tipo **eseguire shell** e utilizzare hello seguente testo:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. Aggiungere un altro **istruzione di compilazione** di tipo **eseguire shell** e utilizzare hello seguente testo:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Passaggi di compilazione in Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Salvare l'elemento Jenkins hello e verificare con **compilare ora**.

### <a name="step-4-connect-github-webhook"></a>Passaggio 4: Connettere il webhook GitHub
1. Nell'elemento Jenkins hello creato, fare clic su **configura**.
2. In **Build Triggers** (Trigger di compilazione), selezionare l'opzione **GitHub hook trigger for GITScm polling** (Trigger di hook GitHub per polling GITScm) e **salvare**. Verrà automaticamente configurato hello GitHub webhook.
3. Nel repository di GitHub per go-web, fare clic su **Impostazioni > Webhook**.
4. Verificare che hello webhook Jenkins URL è stato aggiunto correttamente. URL di Hello deve terminare in "github webhook".

![Configurazione del webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Test hello CI/CD processo end tooend

1. Aggiornare il codice per il repository di hello e push/sincronizzazione con il repository di GitHub hello.
2. Dalla console di Jenkins hello, controllare hello **cronologia compilare** e convalidare tale hello esecuzione del processo. Visualizzare i dettagli toosee output console.
3. Da Kubernetes, visualizzare i dettagli di hello aggiornamento distribuzione:

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>Passaggi successivi

- Distribuire un Registro di sistema del contenitore di Azure e archiviare le immagini in un repository sicuro. Vedere la [documentazione sul Registro di sistema del contenitore di Azure](https://docs.microsoft.com/azure/container-registry).
- Creare un flusso di lavoro più complesso che includa la distribuzione affiancata e i test automatizzati in Jenkins.
- Per ulteriori informazioni sull'elemento di configurazione/CD con Jenkins e Kubernetes, vedere hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).
