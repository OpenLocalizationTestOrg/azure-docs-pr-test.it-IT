---
title: aaaUse Docker Compose in una VM Linux di Azure | Documenti Microsoft
description: Come toouse Docker e composizione nelle macchine virtuali Linux con hello CLI di Azure
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="c3f95-103">Ottenere avviato con toodefine Docker e di scrittura e l'esecuzione di un'applicazione multi-contenitore in Azure</span><span class="sxs-lookup"><span data-stu-id="c3f95-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="c3f95-104">Con [comporre](http://github.com/docker/compose), utilizzare un toodefine di file di testo semplice un'applicazione composta da più contenitori di Docker.</span><span class="sxs-lookup"><span data-stu-id="c3f95-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="c3f95-105">Quindi di creare rapidamente l'applicazione in un unico comando che esegue tutti gli elementi toodeploy l'ambiente definito.</span><span class="sxs-lookup"><span data-stu-id="c3f95-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="c3f95-106">Ad esempio, questo articolo illustra come tooquickly impostare un blog di WordPress con un back-end del database SQL MariaDB in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c3f95-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="c3f95-107">È anche possibile utilizzare tooset comporre le applicazioni più complesse.</span><span class="sxs-lookup"><span data-stu-id="c3f95-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="c3f95-108">Configurare una macchina virtuale Linux come host Docker</span><span class="sxs-lookup"><span data-stu-id="c3f95-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="c3f95-109">È possibile utilizzare varie procedure di Azure e le immagini disponibili o modelli di gestione risorse in hello Azure Marketplace toocreate una VM Linux e configurarlo come host Docker.</span><span class="sxs-lookup"><span data-stu-id="c3f95-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="c3f95-110">Ad esempio, vedere [utilizzando l'ambiente di hello estensione della macchina virtuale Docker toodeploy](dockerextension.md) tooquickly creare una VM Ubuntu con hello estensione della macchina virtuale Docker di Azure utilizzando un [modello delle Guide rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c3f95-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="c3f95-111">Quando si utilizza l'estensione della macchina virtuale Docker hello, la macchina virtuale viene impostata automaticamente come un host Docker e comporre è già installato.</span><span class="sxs-lookup"><span data-stu-id="c3f95-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="c3f95-112">Creare un host Docker con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c3f95-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="c3f95-113">Hello installazione più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c3f95-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c3f95-114">Innanzitutto, creare un gruppo di risorse per l'ambiente di Docker con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c3f95-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c3f95-115">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westus* percorso:</span><span class="sxs-lookup"><span data-stu-id="c3f95-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="c3f95-116">Successivamente, distribuire una macchina virtuale con [distribuzione gruppo az creare](/cli/azure/group/deployment#create) che include l'estensione della macchina virtuale Docker di Azure hello da [questo modello di gestione risorse di Azure su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c3f95-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="c3f95-117">Specificare i propri valori per *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="c3f95-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="c3f95-118">Sono necessari alcuni minuti per hello toofinish di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c3f95-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="c3f95-119">Una volta terminata la distribuzione di hello, [Sposta passaggio toonext](#verify-that-compose-is-installed) tooSSH tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3f95-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="c3f95-120">Facoltativamente, prompt dei comandi di tooinstead controllo restituito toohello e distribuzione hello let continuano in background hello, aggiungere hello `--no-wait` flag toohello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="c3f95-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="c3f95-121">Questo processo consente tooperform altre operazioni in hello CLI mentre hello distribuzione continua per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c3f95-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="c3f95-122">È quindi possibile visualizzare i dettagli sullo stato dell'host Docker hello con [Mostra vm az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="c3f95-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="c3f95-123">esempio Hello Controlla stato hello della macchina virtuale denominata hello *myDockerVM* (nome predefinito dal modello hello hello, non modificare questo nome) nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c3f95-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="c3f95-124">Quando questo comando restituisce *Succeeded*, distribuzione hello è terminata ed è possibile SSH toohello VM in hello riportata dopo il passaggio.</span><span class="sxs-lookup"><span data-stu-id="c3f95-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="c3f95-125">Verificare che Compose sia installato</span><span class="sxs-lookup"><span data-stu-id="c3f95-125">Verify that Compose is installed</span></span>
<span data-ttu-id="c3f95-126">Una volta terminata la distribuzione di hello, SSH tooyour nuovo host Docker con il nome DNS hello fornite durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c3f95-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="c3f95-127">È possibile utilizzare `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview dettagli della macchina virtuale, incluso il nome DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c3f95-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="c3f95-128">toocheck che compongono è installato nel hello macchina virtuale, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c3f95-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="c3f95-129">Viene visualizzato un output simile*docker-comporre 1.6.2, compilazione 4D 72027*.</span><span class="sxs-lookup"><span data-stu-id="c3f95-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="c3f95-130">Se è stato utilizzato un altro metodo toocreate un host Docker e necessario tooinstall comporre manualmente, vedere hello [comporre documentazione](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="c3f95-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="c3f95-131">Creare un file di configurazione docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="c3f95-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="c3f95-132">Successivamente è possibile creare un `docker-compose.yml` file, è sufficiente un file di testo, toodefine hello Docker contenitori toorun su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3f95-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="c3f95-133">file Hello specifica hello immagine toorun su ciascun contenitore oppure può trattarsi di una compilazione di un Dockerfile, variabili di ambiente necessarie e le dipendenze, porte e collegamenti hello tra contenitori.</span><span class="sxs-lookup"><span data-stu-id="c3f95-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="c3f95-134">Per informazioni dettagliate sulla sintassi dei file YML, vedere [Compose file reference](https://docs.docker.com/compose/compose-file/)(Informazioni di riferimento sui file di Compose).</span><span class="sxs-lookup"><span data-stu-id="c3f95-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="c3f95-135">Creare hello *docker compose.yml* file come segue:</span><span class="sxs-lookup"><span data-stu-id="c3f95-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="c3f95-136">Utilizzare il tooadd editor di testo preferito alcuni file di dati toohello.</span><span class="sxs-lookup"><span data-stu-id="c3f95-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="c3f95-137">esempio Hello utilizza hello *vi* editor:</span><span class="sxs-lookup"><span data-stu-id="c3f95-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="c3f95-138">Incollare l'esempio seguente nel file di testo hello.</span><span class="sxs-lookup"><span data-stu-id="c3f95-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="c3f95-139">Questa configurazione usa le immagini hello [Registro di sistema DockerHub](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello Apri origine blog e contenuto management system) e un back-end collegato MariaDB SQL database.</span><span class="sxs-lookup"><span data-stu-id="c3f95-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="c3f95-140">Immettere il proprio valore *MYSQL_ROOT_PASSWORD* come segue:</span><span class="sxs-lookup"><span data-stu-id="c3f95-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="c3f95-141">Inizio hello contenitori con composizione</span><span class="sxs-lookup"><span data-stu-id="c3f95-141">Start hello containers with Compose</span></span>
<span data-ttu-id="c3f95-142">In hello stessa directory come la *docker compose.yml* file, eseguire hello comando seguente (a seconda dell'ambiente, potrebbe essere necessario toorun `docker-compose` utilizzando `sudo`):</span><span class="sxs-lookup"><span data-stu-id="c3f95-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="c3f95-143">Questo comando Avvia contenitori Docker hello specificati nella *docker compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="c3f95-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="c3f95-144">Accetta un o due minuti per toocomplete questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="c3f95-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="c3f95-145">Vedrai toohello simili di output esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c3f95-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="c3f95-146">Essere certi hello toouse **-d** opzione all'avvio in modo che hello contenitori vengono eseguiti in background hello in modo continuo.</span><span class="sxs-lookup"><span data-stu-id="c3f95-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="c3f95-147">tooverify che sono contenitori di hello, tipo `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="c3f95-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="c3f95-148">Dovrebbe essere visualizzata una schermata analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="c3f95-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="c3f95-149">È ora possibile connettersi tooWordPress direttamente nella macchina virtuale sulla porta 80 hello.</span><span class="sxs-lookup"><span data-stu-id="c3f95-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="c3f95-150">Aprire un web browser e immettere il nome DNS hello della macchina virtuale (ad esempio `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="c3f95-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="c3f95-151">Dovrebbe essere hello che WordPress avviare schermo, in cui è possibile completare l'installazione di hello e iniziare con un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c3f95-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![Schermata iniziale di WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="c3f95-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3f95-153">Next steps</span></span>
* <span data-ttu-id="c3f95-154">Passare toohello [Guida dell'utente dell'estensione VM Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) per altre opzioni tooconfigure Docker e nella macchina virtuale Docker Compose.</span><span class="sxs-lookup"><span data-stu-id="c3f95-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="c3f95-155">Ad esempio, un'opzione è tooput hello comporre yml file (convertito tooJSON) direttamente nella configurazione di hello di hello estensione della macchina virtuale Docker.</span><span class="sxs-lookup"><span data-stu-id="c3f95-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="c3f95-156">Estrarre hello [comporre riferimento della riga di comando](http://docs.docker.com/compose/reference/) e [manuale dell'utente](http://docs.docker.com/compose/) per ulteriori esempi di compilazione e distribuzione di applicazioni multi-contenitore.</span><span class="sxs-lookup"><span data-stu-id="c3f95-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="c3f95-157">Utilizzare un modello di gestione risorse di Azure, ovvero il proprio o uno provengono da hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy una macchina virtuale di Azure con Docker e un'applicazione è configurato con la composizione.</span><span class="sxs-lookup"><span data-stu-id="c3f95-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="c3f95-158">Ad esempio, hello [distribuire un blog di WordPress con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) modello Usa Docker e comporre tooquickly distribuire WordPress con un back-end di MySQL in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c3f95-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="c3f95-159">Provare a integrare Docker Compose con un cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c3f95-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="c3f95-160">Per gli scenari, vedere [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) (Uso di Swarm con Compose).</span><span class="sxs-lookup"><span data-stu-id="c3f95-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
