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
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>Come toocreate un'infrastruttura di sviluppo in una VM Linux in Azure con Jenkins, GitHub e Docker
tooautomate hello compilazione e test fase dello sviluppo di applicazioni, è possibile utilizzare un'integrazione continua e la pipeline di distribuzione (CI/CD). In questa esercitazione viene creata una pipeline CI/CD in una macchina virtuale di Azure e viene illustrato come:

> [!div class="checklist"]
> * Creare una macchina virtuale Jenkins
> * Installare e configurare Jenkins
> * Creare un'integrazione webhook tra GitHub e Jenkins
> * Creare e attivare processi di compilazione Jenkins da commit GitHub
> * Creare un'immagine Docker per l'app
> * Verificare che i commit GitHub compilino una nuova immagine Docker e gli aggiornamenti che eseguono l'app


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Creare l'istanza di Jenkins
Nell'esercitazione precedente su [come toocustomize una macchina virtuale Linux al primo avvio](tutorial-automate-vm-deployment.md), si è appreso tooautomate personalizzazione con cloud init. Questa esercitazione viene utilizzato un cloud init file tooinstall Jenkins e Docker in una macchina virtuale. 

Nella shell corrente, creare un file denominato *cloud init.txt* e Incolla hello seguente configurazione. Ad esempio, creare file hello in hello Shell Cloud non presenti nel computer locale. Immettere `sensible-editor cloud-init-jenkins.txt` toocreate hello file e visualizzare un elenco degli editor disponibili. Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:

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

Per poter creare una macchina virtuale è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroupJenkins* in hello *eastus* percorso:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create). Hello utilizzare `--custom-data` toopass parametro nel file di configurazione cloud init. Fornire il percorso completo di hello troppo*cloud-init-jenkins.txt* se è stato salvato il file hello all'esterno delle directory di lavoro attuale.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Sono necessari alcuni minuti per hello VM toobe creato e configurato.

tooallow web tooreach traffico la macchina virtuale, utilizzare [az vm aprire porte](/cli/azure/vm#open-port) tooopen porta *8080* per il traffico di Jenkins e porta *1337* per hello app Node.js toorun usato un'app di esempio:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Configurare Jenkins
tooaccess il Jenkins dell'istanza, ottenere l'indirizzo IP pubblico hello della macchina virtuale:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Per motivi di sicurezza, è necessario tooenter hello iniziale amministratore la password viene archiviata in un file di testo nel hello toostart VM che installare Jenkins. Utilizzare l'indirizzo IP pubblico hello ottenuto nel hello precedente passaggio tooSSH tooyour VM:

```bash
ssh azureuser@<publicIps>
```

Hello vista `initialAdminPassword` per il Jenkins installare e copiarlo:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Se il file hello non è ancora disponibile, attendere alcuni minuti per cloud init toocomplete hello Jenkins e installazione di Docker.

Aprire un web browser e andare troppo`http://<publicIps>:8080`. Completare l'installazione di Jenkins iniziale hello come segue:

- Immettere hello *initialAdminPassword* ottenuto da hello VM nel passaggio precedente hello.
- Fare clic su **selezionare tooinstall plug-in**
- Cercare *GitHub* nella casella di testo hello in alto di hello, selezionare hello *plug-in GitHub*, quindi fare clic su **installare**
- un account utente di Jenkins, toocreate compilare hello in base alle esigenze. Da una prospettiva di sicurezza, è necessario creare il primo utente di Jenkins anziché continuare come account di amministrazione di hello predefinito.
- Al termine, fare clic su **Start using Jenkins** (Inizia a usare Jenkins).


## <a name="create-github-webhook"></a>Creare webhook di GitHub
integrazione di hello tooconfigure con GitHub, aprire hello [app di esempio HelloWorld Node.js](https://github.com/Azure-Samples/nodejs-docs-hello-world) dal repository di esempi di Azure hello. toofork hello repository tooyour proprietari di account GitHub, fare clic su hello **Fork** pulsante nell'angolo superiore destro di hello.

Creare un webhook all'interno di divisione hello è stato creato:

- Fare clic su **impostazioni**, quindi selezionare **servizi e integrazioni** sul lato sinistro di hello.
- Fare clic su **Add service** (Aggiungi servizio) e quindi immettere *Jenkins* nella casella del filtro.
- Selezionare *Jenkins (GitHub plugin)* (Jenkins (plug-in GitHub)).
- Per hello **Jenkins hook URL**, immettere `http://<publicIps>:8080/github-webhook/`. Assicurarsi di includere hello finali /
- Fare clic su **Add service** (Aggiungi servizio).

![Aggiungi repository di GitHub webhook tooyour duplicata](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Creare un processo di Jenkins
toohave Jenkins tooan evento respond in GitHub, ad esempio l'esecuzione del commit di codice, creare un processo di Jenkins. 

Nel sito Web Jenkins, fare clic su **creare nuovi processi** dalla home page di hello:

- Immettere *HelloWorld* come nome del processo. Scegliere **Freestyle project** (Progetto Freestyle) e quindi selezionare **OK**.
- In hello **generale** selezionare **GitHub** del progetto e immettere l'URL di repository con fork, ad esempio *https://github.com/iainfoulds/nodejs-docs-hello-world*
- In hello **gestione del codice sorgente** selezionare **Git**, immettere il repository con fork *GIT* URL, ad esempio *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- In hello **trigger di compilazione** selezionare **trigger hook GitHub per il polling GITscm**.
- In hello **compilare** , scegliere **istruzione di compilazione Aggiungi**. Selezionare **eseguire shell**, quindi immettere `echo "Testing"` nella finestra toocommand.
- Fare clic su **salvare** nella parte inferiore di hello della finestra processi hello.


## <a name="test-github-integration"></a>Testare l'integrazione di GitHub
hello tootest integrazione GitHub con Jenkins, eseguire il commit di una modifica nel fork. 

In GitHub interfaccia utente web, selezionare il repository con fork e quindi fare clic su hello **index.js** file. Fare clic su hello matita icona tooedit questo file in modo che sia di riga 6:

```nodejs
response.end("Hello World!");
```

toocommit le modifiche, fare clic su hello **Commit delle modifiche** pulsante nella parte inferiore di hello.

In Jenkins, viene avviata una nuova compilazione hello **compilare cronologia** sezione dell'angolo hello inferiore sinistro della pagina di processo. Fare clic su collegamento numero di build hello e selezionare **output di Console** sulle dimensioni di hello a sinistra. È possibile visualizzare i passaggi di hello Jenkins accetta come il codice viene effettuato il pull da GitHub e hello compilazione azione output messaggio hello `Testing` toohello console. Ogni volta che viene eseguita un'operazione di commit in GitHub, hello webhook raggiunge tooJenkins e attivare una nuova compilazione in questo modo.


## <a name="define-docker-build-image"></a>Definire l'immagine di compilazione di Docker
app Node.js di hello toosee in base al commit di GitHub, consente di compilare una Docker immagine toorun hello app. immagine di Hello viene creato da un Dockerfile che definisce la modalità tooconfigure hello contenitore che esegue l'applicazione hello. 

Dalla connessione SSH hello tooyour macchina virtuale, spostarsi toohello Jenkins dell'area di lavoro denominato dopo il processo di hello creato nel passaggio precedente. In questo esempio è stata denominata *HelloWorld*.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Crea un file in questa directory dell'area di lavoro con `sudo sensible-editor Dockerfile` e Incolla hello seguendo contenuto. Verificare che hello che dockerfile intero viene copiato correttamente, soprattutto hello prima riga:

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Questo Dockerfile utilizza hello Node.js immagine di base con Linux Alpine porta espone 1337 hello World Hello app viene eseguita, quindi copia i file di applicazione hello e la inizializza.


## <a name="create-jenkins-build-rules"></a>Creare regole di compilazione di Jenkins
In un passaggio precedente, è creata una regola di compilazione Jenkins base che una console toohello messaggio di output. Consente di creare i Dockerfile di hello compilazione passaggio toouse ed eseguire app hello.

Indietro nell'istanza di Jenkins, selezionare il processo di hello creato nel passaggio precedente. Fare clic su **configura** sul lato sinistro di hello e scorrere verso il basso toohello **compilare** sezione:

- Rimuovere l'istruzione di compilazione `echo "Test"` esistente. Fare clic su rosso incrociato in hello angolo superiore destro della casella passaggio di compilazione esistente hello hello.
- Fare clic su **Add build step** (Aggiungi istruzione di compilazione) e quindi selezionare **Execute shell** (Esegui shell).
- In hello **comando** casella, immettere i seguenti comandi di Docker hello, quindi selezionare **salvare**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

istruzioni di compilazione Docker Hello creare un'immagine e un tag con hello Jenkins numero di build di conservare una cronologia delle immagini. Qualsiasi contenitore esistente in esecuzione app hello vengono arrestate e quindi rimosso. Un nuovo contenitore è stata avviata tramite immagine hello e viene eseguita l'app Node.js in base a commit più recente di hello in GitHub.


## <a name="test-your-pipeline"></a>Testare la pipeline
pipeline di intero hello toosee in azione, modificare hello *index.js* nuovamente il file nel repository di GitHub con fork e fare clic su **il Commit delle modifiche**. Un nuovo processo viene avviato in Jenkins basati su hello webhook per GitHub. Accetta alcuni secondi immagine di Docker toocreate hello e avviare l'app in un nuovo contenitore.

Se necessario, è possibile ottenere nuovo indirizzo IP pubblico hello della macchina virtuale:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Aprire un Web browser e immettere `http://<publicIps>:1337`. App Node.js viene visualizzato e riflette commit più recente hello nel fork GitHub come indicato di seguito:

![Esecuzione dell'app Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Creare un'altra modifica toohello *index.js* file modifica hello GitHub e il commit. Attendere alcuni secondi per toocomplete processo hello in Jenkins, quindi aggiornare la versione del web browser toosee hello aggiornata dell'app in esecuzione in un nuovo contenitore, come indicato di seguito:

![Esecuzione dell'app Node.js dopo un altro commit GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato GitHub toorun un processo di compilazione Jenkins in ogni caso di commit di codice e quindi distribuire un tootest contenitore Docker dell'app. Si è appreso come:

> [!div class="checklist"]
> * Creare una macchina virtuale Jenkins
> * Installare e configurare Jenkins
> * Creare un'integrazione webhook tra GitHub e Jenkins
> * Creare e attivare processi di compilazione Jenkins da commit GitHub
> * Creare un'immagine Docker per l'app
> * Verificare che i commit GitHub compilino una nuova immagine Docker e gli aggiornamenti che eseguono l'app

Spostare toolearn esercitazione successiva toohello ulteriori informazioni su toointegrate Jenkins con Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Deploy apps with Jenkins and Team Services (Distribuire app con Jenkins e Team Services)](tutorial-build-deploy-jenkins.md)