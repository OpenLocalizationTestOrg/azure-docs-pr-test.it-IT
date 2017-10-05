---
title: Usare Docker Compose in una VM Linux in Azure | Documentazione Microsoft
description: Come usare Docker e Compose in macchine virtuali Linux con l'interfaccia della riga di comando di Azure
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
ms.openlocfilehash: 541722cb02dd991228726e62a2304b49cdd806f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="34f57-103">Introduzione a Docker e Compose per la definizione e l'esecuzione di un'applicazione multi-contenitore in Azure</span><span class="sxs-lookup"><span data-stu-id="34f57-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="34f57-104">Con [Compose](http://github.com/docker/compose) si usa un file di testo semplice per definire un'applicazione costituita da più contenitori Docker.</span><span class="sxs-lookup"><span data-stu-id="34f57-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="34f57-105">Si avvia quindi l'applicazione mediante un unico comando che effettua le operazioni necessarie per distribuire l'ambiente definito.</span><span class="sxs-lookup"><span data-stu-id="34f57-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="34f57-106">Come esempio, questo articolo illustra come configurare rapidamente un blog WordPress con un database SQL MariaDB back-end in una macchina virtuale di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="34f57-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="34f57-107">È possibile usare Compose anche per configurare applicazioni più complesse.</span><span class="sxs-lookup"><span data-stu-id="34f57-107">You can also use Compose to set up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="34f57-108">Configurare una macchina virtuale Linux come host Docker</span><span class="sxs-lookup"><span data-stu-id="34f57-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="34f57-109">È possibile usare diverse procedure di Azure e le immagini o i modelli di Resource Manager disponibili in Azure Markeplace per creare una macchina virtuale di Linux da configurare come host Docker.</span><span class="sxs-lookup"><span data-stu-id="34f57-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="34f57-110">Ad esempio, vedere [Using the Docker VM Extension to deploy your environment](dockerextension.md) (Uso dell'estensione di VM Docker per distribuire l'ambiente) per creare rapidamente una VM Ubuntu con l'estensione VM Docker di Azure tramite un [modello di avvio rapido](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="34f57-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="34f57-111">Quando si usa l'estensione di VM Docker, la macchina virtuale viene automaticamente configurata come host Docker e Compose è già installato.</span><span class="sxs-lookup"><span data-stu-id="34f57-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="34f57-112">Creare un host Docker con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="34f57-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="34f57-113">Installare la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="34f57-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="34f57-114">Innanzitutto, creare un gruppo di risorse per l'ambiente di Docker con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="34f57-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="34f57-115">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *westus*:</span><span class="sxs-lookup"><span data-stu-id="34f57-115">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="34f57-116">Successivamente, distribuire una macchina virtuale con il comando [az group deployment create](/cli/azure/group/deployment#create) che include l'estensione di VM Docker di Azure da [questo modello di Azure Resource Manager su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="34f57-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="34f57-117">Specificare i propri valori per *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="34f57-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="34f57-118">L'operazione di distribuzione richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="34f57-118">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="34f57-119">Al termine della distribuzione, [procedere al passaggio successivo](#verify-that-compose-is-installed) per configurare SSH sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="34f57-119">Once the deployment is finished, [move to next step](#verify-that-compose-is-installed) to SSH to your VM.</span></span> 

<span data-ttu-id="34f57-120">Facoltativamente, per restituire il controllo al prompt e per consentire la distribuzione continua in background, aggiungere il flag `--no-wait` al comando precedente.</span><span class="sxs-lookup"><span data-stu-id="34f57-120">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="34f57-121">Questo processo consente di eseguire altre operazioni nell'interfaccia della riga di comando mentre la distribuzione continua per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="34f57-121">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="34f57-122">È possibile visualizzare i dettagli sullo stato dell'host Docker con il comando [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="34f57-122">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="34f57-123">L'esempio seguente controlla lo stato della macchina virtuale denominata *myDockerVM* (il nome predefinito del modello, non modificare questo nome) che appartiene al gruppo di risorse *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="34f57-123">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="34f57-124">Quando questo comando restituisce *Succeeded*, la distribuzione è stata completata ed è possibile configurare SSH sulla macchina virtuale nel passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="34f57-124">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="34f57-125">Verificare che Compose sia installato</span><span class="sxs-lookup"><span data-stu-id="34f57-125">Verify that Compose is installed</span></span>
<span data-ttu-id="34f57-126">Al termine della distribuzione, stabilire una connessione SSH al nuovo host Docker con il nome DNS specificato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="34f57-126">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span></span> <span data-ttu-id="34f57-127">È possibile usare `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` per visualizzare i dettagli della VM, incluso il nome DNS.</span><span class="sxs-lookup"><span data-stu-id="34f57-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` to view details of your VM, including the DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="34f57-128">Per verificare l'installazione di Compose nella macchina virtuale, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="34f57-128">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="34f57-129">Si ottiene un output simile a *docker-compose 1.6.2, build 4d72027*.</span><span class="sxs-lookup"><span data-stu-id="34f57-129">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="34f57-130">Se è stato usato un altro metodo per creare un host Docker ed è necessario installare Compose manualmente, vedere la [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md)(Documentazione di Compose).</span><span class="sxs-lookup"><span data-stu-id="34f57-130">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="34f57-131">Creare un file di configurazione docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="34f57-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="34f57-132">In seguito viene creato un file `docker-compose.yml` , che è semplicemente un file di configurazione di testo, per definire i contenitori Docker ed eseguirli nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="34f57-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="34f57-133">Il file specifica l'immagine da eseguire su ciascun contenitore (o può essere una compilazione da un file Docker), le variabili d'ambiente, le dipendenze necessarie, le porte e i collegamenti tra i contenitori.</span><span class="sxs-lookup"><span data-stu-id="34f57-133">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="34f57-134">Per informazioni dettagliate sulla sintassi dei file YML, vedere [Compose file reference](https://docs.docker.com/compose/compose-file/)(Informazioni di riferimento sui file di Compose).</span><span class="sxs-lookup"><span data-stu-id="34f57-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="34f57-135">Creare il file *docker-compose.yml* come segue:</span><span class="sxs-lookup"><span data-stu-id="34f57-135">Create the *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="34f57-136">Usare un editor di testo per aggiungere dati al file.</span><span class="sxs-lookup"><span data-stu-id="34f57-136">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="34f57-137">L'esempio seguente usa l'editor *vi*:</span><span class="sxs-lookup"><span data-stu-id="34f57-137">The following example uses the *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="34f57-138">Incollare l'esempio seguente nel file di testo.</span><span class="sxs-lookup"><span data-stu-id="34f57-138">Paste the following example into your text file.</span></span> <span data-ttu-id="34f57-139">Questa configurazione utilizza le immagini del [Registro di sistema DockerHub](https://registry.hub.docker.com/_/wordpress/) per installare WordPress (il sistema di creazione blog e gestione del contenuto open source) e un database SQL MariaDB back-end collegato.</span><span class="sxs-lookup"><span data-stu-id="34f57-139">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="34f57-140">Immettere il proprio valore *MYSQL_ROOT_PASSWORD* come segue:</span><span class="sxs-lookup"><span data-stu-id="34f57-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

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

## <a name="start-the-containers-with-compose"></a><span data-ttu-id="34f57-141">Avviare i contenitori con Compose</span><span class="sxs-lookup"><span data-stu-id="34f57-141">Start the containers with Compose</span></span>
<span data-ttu-id="34f57-142">Nella stessa directory del file *docker-compose.yml* eseguire il comando seguente (a seconda dell'ambiente, può essere necessario eseguire `docker-compose` usando `sudo`):</span><span class="sxs-lookup"><span data-stu-id="34f57-142">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="34f57-143">Il comando avvia i contenitori Docker specificati in *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="34f57-143">This command starts the Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="34f57-144">L'esecuzione di questo passaggio richiede un paio di minuti.</span><span class="sxs-lookup"><span data-stu-id="34f57-144">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="34f57-145">L'output sarà simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="34f57-145">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="34f57-146">Assicurarsi di utilizzare l’opzione **-d** all'avvio in modo che i contenitori vengano eseguiti in background continuamente.</span><span class="sxs-lookup"><span data-stu-id="34f57-146">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="34f57-147">Per verificare che i contenitori siano attivi, digitare `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="34f57-147">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="34f57-148">Dovrebbe essere visualizzata una schermata analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="34f57-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="34f57-149">Ora è possibile connettersi a WordPress direttamente nella VM dalla porta 80.</span><span class="sxs-lookup"><span data-stu-id="34f57-149">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="34f57-150">Aprire un Web browser e immettere il nome DNS della VM (ad esempio `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="34f57-150">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="34f57-151">Viene visualizzata la schermata di avvio di WordPress, in cui è possibile completare l'installazione e iniziare a utilizzare l’applicazione.</span><span class="sxs-lookup"><span data-stu-id="34f57-151">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![Schermata iniziale di WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="34f57-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34f57-153">Next steps</span></span>
* <span data-ttu-id="34f57-154">Vedere la [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) (Guida dell'utente dell'estensione di VM Docker) per altre opzioni di configurazione di Docker e Compose nella VM Docker.</span><span class="sxs-lookup"><span data-stu-id="34f57-154">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="34f57-155">Ad esempio, un'opzione consiste nell'inserire il file YML di Compose (convertito in JSON) direttamente nella configurazione dell'estensione della VM Docker.</span><span class="sxs-lookup"><span data-stu-id="34f57-155">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="34f57-156">Per altri esempi di compilazione e distribuzione di app multi-contenitore, vedere [Compose command-line reference](http://docs.docker.com/compose/reference/) (Informazioni di riferimento sulla riga di comando di Compose) e la [guida dell'utente](http://docs.docker.com/compose/).</span><span class="sxs-lookup"><span data-stu-id="34f57-156">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="34f57-157">Utilizzare un modello di Gestione risorse di Azure, quello proprio o uno fornito dalla [community](https://azure.microsoft.com/documentation/templates/), per distribuire una macchina virtuale di Azure con Docker e un'applicazione configurata con Compose.</span><span class="sxs-lookup"><span data-stu-id="34f57-157">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="34f57-158">Ad esempio, il modello [Distribuire un blog WordPress con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) utilizza Docker e Compose per distribuire rapidamente WordPress con un back-end MySQL in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="34f57-158">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="34f57-159">Provare a integrare Docker Compose con un cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="34f57-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="34f57-160">Per gli scenari, vedere [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) (Uso di Swarm con Compose).</span><span class="sxs-lookup"><span data-stu-id="34f57-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
