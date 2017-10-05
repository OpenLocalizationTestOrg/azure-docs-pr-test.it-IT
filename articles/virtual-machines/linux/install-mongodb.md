---
title: Installare MongoDB in una macchina virtuale Linux con l'interfaccia della riga di comando di Azure | Documentazione Microsoft
description: Informazioni su come installare e configurare MongoDB in una macchina virtuale Linux usando l'interfaccia della riga di comando di Azure 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: e19c09558285497f29eb78b4f4ae5b15d7f1a191
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="09391-103">Come installare e configurare MongoDB in una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="09391-103">How to install and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="09391-104">[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="09391-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="09391-105">Questo articolo illustra come installare e configurare MongoDB in una VM Linux usando l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="09391-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="09391-106">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="09391-106">You can also perform these steps with the [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="09391-107">Alcuni esempi illustrano in dettaglio come fare a:</span><span class="sxs-lookup"><span data-stu-id="09391-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="09391-108">Installare e configurare manualmente un'istanza di MongoDB di base</span><span class="sxs-lookup"><span data-stu-id="09391-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="09391-109">Creare un'istanza di MongoDB di base usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="09391-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="09391-110">Creare un cluster complesso di MongoDB partizionato con set di repliche usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="09391-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="09391-111">Installare e configurare manualmente MongoDB su una VM</span><span class="sxs-lookup"><span data-stu-id="09391-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="09391-112">MongoDB [fornisce le istruzioni di installazione](https://docs.mongodb.com/manual/administration/install-on-linux/) per i sistemi operativi Linux Red Hat/CentOS, SUSE, Ubuntu e Debian.</span><span class="sxs-lookup"><span data-stu-id="09391-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="09391-113">L'esempio seguente crea una macchina virtuale *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="09391-113">The following example creates a *CentOS* VM.</span></span> <span data-ttu-id="09391-114">Per creare questo ambiente, è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure tramite [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="09391-114">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="09391-115">Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="09391-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="09391-116">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="09391-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="09391-117">Creare una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="09391-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="09391-118">L'esempio seguente crea una macchina virtuale denominata *myVM* con un utente chiamato *azureuser* usando l'autenticazione con chiave pubblica SSH</span><span class="sxs-lookup"><span data-stu-id="09391-118">The following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="09391-119">Eseguire SSH sulla macchina virtuale usando il proprio nome utente e l'indirizzo `publicIpAddress` elencato nell'output ottenuto nel passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="09391-119">SSH to the VM using your own username and the `publicIpAddress` listed in the output from the previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="09391-120">Per aggiungere le origini di installazione di MongoDB, creare un file di archivio **yum** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="09391-120">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="09391-121">Aprire il file di archivio di MongoDB da modificare.</span><span class="sxs-lookup"><span data-stu-id="09391-121">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="09391-122">Aggiungere le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="09391-122">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="09391-123">Installare MongoDB usando **yum** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="09391-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="09391-124">Per impostazione predefinita, alle immagini CentOS è applicato SELinux, che impedisce di accedere a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="09391-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="09391-125">Installare gli strumenti per la gestione dei criteri e configurare SELinux in modo tale da consentire a MongoDB di operare sulla porta TCP 27017 predefinita, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="09391-125">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="09391-126">Avviare il servizio MongoDB come di seguito:</span><span class="sxs-lookup"><span data-stu-id="09391-126">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="09391-127">Verificare l'installazione di MongoDB connettendosi tramite il client `mongo` locale:</span><span class="sxs-lookup"><span data-stu-id="09391-127">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="09391-128">A questo punto, testare l'istanza di MongoDB aggiungendo alcuni dati ed eseguendo la ricerca:</span><span class="sxs-lookup"><span data-stu-id="09391-128">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="09391-129">Se lo si desidera, configurare MongoDB per l'avvio automatico durante il riavvio del sistema:</span><span class="sxs-lookup"><span data-stu-id="09391-129">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="09391-130">Creare un'istanza di MongoDB di base su CentOS usando un modello</span><span class="sxs-lookup"><span data-stu-id="09391-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="09391-131">Per creare un'istanza di MongoDB di base in una singola VM CentOS, è possibile usare il seguente modello di avvio rapido di Azure in GitHub.</span><span class="sxs-lookup"><span data-stu-id="09391-131">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="09391-132">Usando l'estensione dello script personalizzata, questo modello consente a Linux di aggiungere un archivio **yum** alla macchina virtuale CentOS appena creata, per poi installare MongoDB.</span><span class="sxs-lookup"><span data-stu-id="09391-132">This template uses the Custom Script extension for Linux to add a **yum** repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="09391-133">[Istanza di MongoDB di base su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="09391-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="09391-134">Per creare questo ambiente, è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure tramite [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="09391-134">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="09391-135">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="09391-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="09391-136">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="09391-136">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="09391-137">Quindi distribuire il modello MongoDB con [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="09391-137">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="09391-138">Definire i nomi e le dimensioni delle risorse desiderati dove necessario per *newStorageAccountName*, *virtualNetworkName* e *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="09391-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

<span data-ttu-id="09391-139">Eseguire l'accesso alla VM usando l'indirizzo DNS pubblico della VM.</span><span class="sxs-lookup"><span data-stu-id="09391-139">Log on to the VM using the public DNS address of your VM.</span></span> <span data-ttu-id="09391-140">È possibile visualizzare l'indirizzo DNS pubblico con [az vm show](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="09391-140">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="09391-141">Eseguire SSH sulla VM usando il proprio nome utente e l'indirizzo DNS pubblico:</span><span class="sxs-lookup"><span data-stu-id="09391-141">SSH to your VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="09391-142">Verificare l'installazione di MongoDB connettendosi tramite il client `mongo` locale, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="09391-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="09391-143">A questo punto, testare l'istanza aggiungendo alcuni dati ed eseguendo la ricerca seguente:</span><span class="sxs-lookup"><span data-stu-id="09391-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="09391-144">Creare un cluster complesso di MongoDB partizionato in CentOS usando un modello</span><span class="sxs-lookup"><span data-stu-id="09391-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="09391-145">Per creare un cluster complesso di MongoDB partizionato, è possibile usare il seguente modello di avvio rapido in GitHub.</span><span class="sxs-lookup"><span data-stu-id="09391-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="09391-146">Questo modello segue le [procedure consigliate per cluster MongoDB partizionati](https://docs.mongodb.com/manual/core/sharded-cluster-components/) per garantire ridondanza e disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="09391-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="09391-147">Il modello crea due partizioni, con tre nodi in ogni set di repliche.</span><span class="sxs-lookup"><span data-stu-id="09391-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="09391-148">Inoltre, nel server di configurazione viene creato un set di repliche con tre nodi, più due server router **mongos** per garantire coerenza tra le applicazioni delle varie partizioni.</span><span class="sxs-lookup"><span data-stu-id="09391-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="09391-149">[Cluster di partizionamento di MongoDB su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="09391-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="09391-150">La distribuzione di questo cluster complesso di MongoDB partizionato richiede più di 20 core, che in genere è il numero di core predefinito per ogni area di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="09391-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="09391-151">Per aumentare il numero di core, aprire una richiesta di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="09391-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="09391-152">Per creare questo ambiente, è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure tramite [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="09391-152">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="09391-153">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="09391-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="09391-154">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="09391-154">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="09391-155">Quindi distribuire il modello MongoDB con [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="09391-155">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="09391-156">Definire i nomi e le dimensioni delle risorse desiderati dove necessario per *mongoAdminUsername*, *sizeOfDataDiskInGB* e *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="09391-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

<span data-ttu-id="09391-157">Questa distribuzione può impiegare più di un'ora per distribuire e configurare tutte le istanze di VM.</span><span class="sxs-lookup"><span data-stu-id="09391-157">This deployment can take over an hour to deploy and configure all the VM instances.</span></span> <span data-ttu-id="09391-158">Il flag `--no-wait` viene usato alla fine del comando precedente per restituire il controllo al prompt dei comandi dopo che la distribuzione del modello è stata accettata dalla piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="09391-158">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span></span> <span data-ttu-id="09391-159">È quindi possibile visualizzare lo stato della distribuzione con [az group deployment show](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="09391-159">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="09391-160">L'esempio seguente visualizza lo stato per la distribuzione *myMongoDBCluster* nel gruppo di risorse *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="09391-160">The following example views the status for the *myMongoDBCluster* deployment in the *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="09391-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09391-161">Next steps</span></span>
<span data-ttu-id="09391-162">In questi esempi si effettua la connessione all'istanza di MongoDB locale dalla VM.</span><span class="sxs-lookup"><span data-stu-id="09391-162">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="09391-163">Se si desidera connettersi all'istanza di MongoDB da un'altra VM o un'altra rete, accertarsi di [creare le regole del gruppo di sicurezza di rete](nsg-quickstart.md) appropriate.</span><span class="sxs-lookup"><span data-stu-id="09391-163">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="09391-164">Questi esempi consentono di distribuire l'ambiente MongoDB di base per scopi di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="09391-164">These examples deploy the core MongoDB environment for development purposes.</span></span> <span data-ttu-id="09391-165">Applicare le opzioni di configurazione della sicurezza necessarie per l'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="09391-165">Apply the required security configuration options for your environment.</span></span> <span data-ttu-id="09391-166">Per altre informazioni, vedere i [documenti sulla sicurezza di MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="09391-166">For more information, see the [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="09391-167">Per altre informazioni sulla creazione tramite modelli, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="09391-167">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="09391-168">I modelli di Azure Resource Manager usano l'estensione dello script personalizzata per scaricare ed eseguire script nelle VM.</span><span class="sxs-lookup"><span data-stu-id="09391-168">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="09391-169">Per altre informazioni, vedere [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md) (Usare l'estensione dello script personalizzata di Azure con macchine virtuali Linux).</span><span class="sxs-lookup"><span data-stu-id="09391-169">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

