---
title: aaaInstall MongoDB in una VM Linux con hello CLI di Azure | Documenti Microsoft
description: Informazioni su come tooinstall e configurare MongoDB su hello di iusing una macchina virtuale Linux Azure CLI 2.0
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
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="e3a6b-103">Come tooinstall e configurare MongoDB in una VM Linux</span><span class="sxs-lookup"><span data-stu-id="e3a6b-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="e3a6b-104">[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="e3a6b-105">In questo articolo illustra come tooinstall e configurare MongoDB in una VM Linux con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="e3a6b-106">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="e3a6b-107">Alcuni esempi illustrano in dettaglio come fare a:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="e3a6b-108">Installare e configurare manualmente un'istanza di MongoDB di base</span><span class="sxs-lookup"><span data-stu-id="e3a6b-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="e3a6b-109">Creare un'istanza di MongoDB di base usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3a6b-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="e3a6b-110">Creare un cluster complesso di MongoDB partizionato con set di repliche usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3a6b-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="e3a6b-111">Installare e configurare manualmente MongoDB su una VM</span><span class="sxs-lookup"><span data-stu-id="e3a6b-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="e3a6b-112">MongoDB [fornisce le istruzioni di installazione](https://docs.mongodb.com/manual/administration/install-on-linux/) per i sistemi operativi Linux Red Hat/CentOS, SUSE, Ubuntu e Debian.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="e3a6b-113">Hello esempio seguente viene creato un *CentOS* macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="e3a6b-114">toocreate questo ambiente, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e3a6b-115">Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e3a6b-116">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e3a6b-117">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e3a6b-118">esempio Hello crea una macchina virtuale denominata *myVM* con un utente denominato *azureuser* utilizzando l'autenticazione con chiave pubblica SSH</span><span class="sxs-lookup"><span data-stu-id="e3a6b-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="e3a6b-119">SSH toohello VM usando il proprio nome utente e hello `publicIpAddress` elencati nell'output di hello dal passaggio precedente hello:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="e3a6b-120">origine dell'installazione di hello tooadd per MongoDB, creare un **yum** file del repository come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="e3a6b-121">Aprire il file di repository hello MongoDB per la modifica.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="e3a6b-122">Aggiungere hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="e3a6b-123">Installare MongoDB usando **yum** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="e3a6b-124">Per impostazione predefinita, alle immagini CentOS è applicato SELinux, che impedisce di accedere a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="e3a6b-125">Installare strumenti di gestione di criteri e configurare SELinux tooallow MongoDB toooperate sulla porta TCP predefinita 27017 come segue:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="e3a6b-126">Avviare il servizio di MongoDB hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="e3a6b-127">Verificare l'installazione di MongoDB hello connettendosi usando hello locale `mongo` client:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="e3a6b-128">Ora è possibile testare istanza MongoDB hello aggiungendo alcuni dati e quindi la ricerca:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="e3a6b-129">Se si desidera, configurare MongoDB toostart automaticamente durante un riavvio del sistema:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="e3a6b-130">Creare un'istanza di MongoDB di base su CentOS usando un modello</span><span class="sxs-lookup"><span data-stu-id="e3a6b-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="e3a6b-131">È possibile creare un'istanza di MongoDB base in una singola macchina virtuale CentOS usando hello segue il modello di avvio rapido di Azure da GitHub.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="e3a6b-132">Questo modello Usa l'estensione Custom Script hello per Linux tooadd un **yum** tooyour repository creata la macchina virtuale CentOS e quindi installare MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="e3a6b-133">[Istanza di MongoDB di base su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="e3a6b-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="e3a6b-134">toocreate questo ambiente, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="e3a6b-135">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e3a6b-136">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e3a6b-137">Successivamente, distribuire il modello di MongoDB hello con [distribuzione gruppo az creare](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="e3a6b-138">Definire i nomi e le dimensioni delle risorse desiderati dove necessario per *newStorageAccountName*, *virtualNetworkName* e *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

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

<span data-ttu-id="e3a6b-139">Accedere toohello VM utilizzando l'indirizzo DNS pubblico hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="e3a6b-140">È possibile visualizzare l'indirizzo DNS pubblico hello con [Mostra vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="e3a6b-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="e3a6b-141">SSH tooyour VM usando il proprio nome utente e l'indirizzo DNS pubblico:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="e3a6b-142">Verificare l'installazione di MongoDB hello connettendosi usando hello locale `mongo` client come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="e3a6b-143">Ora hello istanza test aggiungendo alcuni dati e la ricerca come segue:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="e3a6b-144">Creare un cluster complesso di MongoDB partizionato in CentOS usando un modello</span><span class="sxs-lookup"><span data-stu-id="e3a6b-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="e3a6b-145">È possibile creare un cluster di partizionati MongoDB complesso utilizzando hello segue il modello di avvio rapido di Azure da GitHub.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="e3a6b-146">Questo modello segue hello [procedure consigliate di MongoDB cluster partizionati](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide disponibilità elevata e ridondanza.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="e3a6b-147">Hello modello consente di creare due partizioni, con tre nodi in ogni set di repliche.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="e3a6b-148">Una replica di server di configurazione impostata con tre nodi viene creata anche, più due **mongos** router di server di tooprovide di coerenza tooapplications da tra partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="e3a6b-149">[Cluster di partizionamento di MongoDB su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="e3a6b-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="e3a6b-150">Distribuzione di cluster partizionati MongoDB complesso richiede più di 20 core, che è in genere hello numero di core predefinita per ogni area per una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="e3a6b-151">Aprire un tooincrease di richiesta di supporto tecnico di Azure il numero di core.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="e3a6b-152">toocreate questo ambiente, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="e3a6b-153">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e3a6b-154">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e3a6b-155">Successivamente, distribuire il modello di MongoDB hello con [distribuzione gruppo az creare](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="e3a6b-156">Definire i nomi e le dimensioni delle risorse desiderati dove necessario per *mongoAdminUsername*, *sizeOfDataDiskInGB* e *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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

<span data-ttu-id="e3a6b-157">Questa distribuzione può assumere un toodeploy ora e configurare tutte le istanze VM hello.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="e3a6b-158">Hello `--no-wait` flag viene utilizzato alla fine hello hello precedente prompt dei comandi di comando tooreturn controllo toohello dopo la distribuzione dei modelli di hello è stato accettato dalla piattaforma Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="e3a6b-159">È quindi possibile visualizzare lo stato di distribuzione hello con [Mostra la distribuzione di gruppo az](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="e3a6b-160">viste di esempio seguenti Hello hello stato per hello *myMongoDBCluster* distribuzione in hello *myResourceGroup* gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="e3a6b-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="e3a6b-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3a6b-161">Next steps</span></span>
<span data-ttu-id="e3a6b-162">In questi esempi, è connettersi toohello MongoDB istanza localmente da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="e3a6b-163">Se si desidera tooconnect toohello MongoDB istanza da un'altra macchina virtuale o una rete, assicurarsi di hello appropriato [vengono create regole Network Security Group](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="e3a6b-164">Questi esempi distribuirlo hello core MongoDB per scopi di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="e3a6b-165">Applicare opzioni di configurazione di sicurezza hello necessario per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="e3a6b-166">Per ulteriori informazioni, vedere hello [documenti sicurezza MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="e3a6b-167">Per ulteriori informazioni sulla creazione di modelli, vedere hello [Panoramica di gestione risorse di Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="e3a6b-168">modelli di Azure Resource Manager Hello utilizzano toodownload estensione Script personalizzata hello ed eseguire script in macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e3a6b-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="e3a6b-169">Per ulteriori informazioni, vedere [Using hello estensione Script personalizzata di Azure con le macchine virtuali Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e3a6b-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

