---
title: Installare MongoDB in una VM Linux usando l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come installare e configurare MongoDB su una macchina virtuale Linux in Azure usando il modello di distribuzione di Resource Manager.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: c97ade0a3d95824f723aad55776de861fe49441f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="b2373-103">Come installare e configurare MongoDB in una VM Linux usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b2373-103">How to install and configure MongoDB on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="b2373-104">[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="b2373-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="b2373-105">Questo articolo illustra come installare e configurare MongoDB su una VM Linux in Azure usando il modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b2373-105">This article shows you how to install and configure MongoDB on a Linux VM in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="b2373-106">Alcuni esempi illustrano in dettaglio come fare a:</span><span class="sxs-lookup"><span data-stu-id="b2373-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="b2373-107">Installare e configurare manualmente un'istanza di MongoDB di base</span><span class="sxs-lookup"><span data-stu-id="b2373-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="b2373-108">Creare un'istanza di MongoDB di base usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2373-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="b2373-109">Creare un cluster complesso di MongoDB partizionato con set di repliche usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2373-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="b2373-110">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="b2373-110">CLI versions to complete the task</span></span>
<span data-ttu-id="b2373-111">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="b2373-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="b2373-112">Interfaccia della riga di comando di Azure 1.0: interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="b2373-112">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b2373-113">[Interfaccia della riga di comando di Azure 2.0](create-cli-complete-nodejs.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="b2373-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="b2373-114">Installare e configurare manualmente MongoDB su una VM</span><span class="sxs-lookup"><span data-stu-id="b2373-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="b2373-115">MongoDB [fornisce le istruzioni di installazione](https://docs.mongodb.com/manual/administration/install-on-linux/) per i sistemi operativi Linux Red Hat/CentOS, SUSE, Ubuntu e Debian.</span><span class="sxs-lookup"><span data-stu-id="b2373-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="b2373-116">L'esempio seguente crea una macchina virtuale *CentOS* usando una chiave SSH archiviata in *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="b2373-116">The following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="b2373-117">Rispondere ai messaggi per l'inserimento delle informazioni su nome dell'account di archiviazione, nome DNS e credenziali di amministratore:</span><span class="sxs-lookup"><span data-stu-id="b2373-117">Answer the prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="b2373-118">Accedere alla VM usando l'indirizzo IP pubblico visualizzato alla fine del precedente passaggio per la creazione della VM:</span><span class="sxs-lookup"><span data-stu-id="b2373-118">Log on to the VM using the public IP address displayed at the end of the preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="b2373-119">Per aggiungere le origini di installazione di MongoDB, creare un file di archivio **yum** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b2373-119">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="b2373-120">Aprire il file di archivio di MongoDB da modificare.</span><span class="sxs-lookup"><span data-stu-id="b2373-120">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="b2373-121">Aggiungere le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2373-121">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="b2373-122">Installare MongoDB usando **yum** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b2373-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="b2373-123">Per impostazione predefinita, alle immagini CentOS è applicato SELinux, che impedisce di accedere a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b2373-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="b2373-124">Con il codice illustrato di seguito, installare gli strumenti per la gestione dei criteri e configurare SELinux in modo tale da consentire a MongoDB di operare sulla porta TCP 27017 predefinita.</span><span class="sxs-lookup"><span data-stu-id="b2373-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="b2373-125">Avviare il servizio MongoDB come di seguito:</span><span class="sxs-lookup"><span data-stu-id="b2373-125">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="b2373-126">Verificare l'installazione di MongoDB connettendosi tramite il client `mongo` locale:</span><span class="sxs-lookup"><span data-stu-id="b2373-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="b2373-127">A questo punto, testare l'istanza di MongoDB aggiungendo alcuni dati ed eseguendo la ricerca:</span><span class="sxs-lookup"><span data-stu-id="b2373-127">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="b2373-128">Se lo si desidera, configurare MongoDB per l'avvio automatico durante il riavvio del sistema:</span><span class="sxs-lookup"><span data-stu-id="b2373-128">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="b2373-129">Creare un'istanza di MongoDB di base su CentOS usando un modello</span><span class="sxs-lookup"><span data-stu-id="b2373-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="b2373-130">Per creare un'istanza di MongoDB di base in una singola VM CentOS, è possibile usare il seguente modello di avvio rapido di Azure in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2373-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="b2373-131">Usando l'estensione dello script personalizzata, questo modello consente a Linux di aggiungere un repository `yum` alla VM CentOS appena creata, per poi installare MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b2373-131">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="b2373-132">[Istanza di MongoDB di base su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b2373-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="b2373-133">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nell'area `eastus`.</span><span class="sxs-lookup"><span data-stu-id="b2373-133">The following example creates a resource group with the name `myResourceGroup` in the `eastus` region.</span></span> <span data-ttu-id="b2373-134">Immettere valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="b2373-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="b2373-135">L'interfaccia della riga di comando di Azure restituisce un avviso a pochi secondi dalla creazione della distribuzione, ma per completare l'installazione e la configurazione serve qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="b2373-135">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration takes a few minutes to complete.</span></span> <span data-ttu-id="b2373-136">Controllare lo stato della distribuzione con `azure group deployment show myResourceGroup`, immettendo il nome del gruppo di risorse appropriato.</span><span class="sxs-lookup"><span data-stu-id="b2373-136">Check the status of the deployment with `azure group deployment show myResourceGroup`, entering the name of your resource group accordingly.</span></span> <span data-ttu-id="b2373-137">Attendere che **ProvisioningState** indichi *Succeeded* prima di provare la connessione SSH alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b2373-137">Wait until the **ProvisioningState** shows *Succeeded* before trying to SSH to the VM.</span></span>

<span data-ttu-id="b2373-138">Al termine della distribuzione, effettuare la connessione SSH alla VM.</span><span class="sxs-lookup"><span data-stu-id="b2373-138">Once the deployment is complete, SSH to the VM.</span></span> <span data-ttu-id="b2373-139">Ottenere l'indirizzo IP della VM usando il comando `azure vm show` come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b2373-139">Obtain the IP address of your VM using the `azure vm show` command as in the following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="b2373-140">Verso la fine dell'output, viene visualizzato l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="b2373-140">Near the end of the output, the public IP address is displayed.</span></span> <span data-ttu-id="b2373-141">Effettuare la connessione SSH alla VM con l'indirizzo IP di quest'ultima:</span><span class="sxs-lookup"><span data-stu-id="b2373-141">SSH to your VM with the IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="b2373-142">Verificare l'installazione di MongoDB connettendosi tramite il client `mongo` locale, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="b2373-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="b2373-143">A questo punto, testare l'istanza aggiungendo alcuni dati ed eseguendo la ricerca seguente:</span><span class="sxs-lookup"><span data-stu-id="b2373-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="b2373-144">Creare un cluster complesso di MongoDB partizionato in CentOS usando un modello</span><span class="sxs-lookup"><span data-stu-id="b2373-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="b2373-145">Per creare un cluster complesso di MongoDB partizionato, è possibile usare il seguente modello di avvio rapido in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2373-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="b2373-146">Questo modello segue le [procedure consigliate per cluster MongoDB partizionati](https://docs.mongodb.com/manual/core/sharded-cluster-components/) per garantire ridondanza e disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="b2373-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="b2373-147">Il modello crea due partizioni, con tre nodi in ogni set di repliche.</span><span class="sxs-lookup"><span data-stu-id="b2373-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="b2373-148">Inoltre, nel server di configurazione viene creato un set di repliche con tre nodi, più due server router **mongos** per garantire coerenza tra le applicazioni delle varie partizioni.</span><span class="sxs-lookup"><span data-stu-id="b2373-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="b2373-149">[Cluster di partizionamento di MongoDB su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b2373-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="b2373-150">La distribuzione di questo cluster complesso di MongoDB partizionato richiede più di 20 core, che in genere è il numero di core predefinito per ogni area di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b2373-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="b2373-151">Per aumentare il numero di core, aprire una richiesta di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2373-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="b2373-152">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*.</span><span class="sxs-lookup"><span data-stu-id="b2373-152">The following example creates a resource group with the name *myResourceGroup* in the *eastus* region.</span></span> <span data-ttu-id="b2373-153">Immettere valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="b2373-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="b2373-154">L'interfaccia della riga di comando di Azure restituisce un avviso a pochi secondi dalla creazione della distribuzione, ma per completare l'installazione e la configurazione può servire più di un'ora.</span><span class="sxs-lookup"><span data-stu-id="b2373-154">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration can take over an hour to complete.</span></span> <span data-ttu-id="b2373-155">Controllare lo stato della distribuzione con `azure group deployment show myResourceGroup`, adeguando il nome del gruppo di risorse di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="b2373-155">Check the status of the deployment with `azure group deployment show myResourceGroup`, adjusting the name of your resource group accordingly.</span></span> <span data-ttu-id="b2373-156">Attendere che **ProvisioningState** indichi *Succeeded* prima di eseguire la connessione alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b2373-156">Wait until the **ProvisioningState** shows *Succeeded* before connecting to the VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b2373-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2373-157">Next steps</span></span>
<span data-ttu-id="b2373-158">In questi esempi si effettua la connessione all'istanza di MongoDB locale dalla VM.</span><span class="sxs-lookup"><span data-stu-id="b2373-158">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="b2373-159">Se si desidera connettersi all'istanza di MongoDB da un'altra VM o un'altra rete, accertarsi di [creare le regole del gruppo di sicurezza di rete](nsg-quickstart.md) appropriate.</span><span class="sxs-lookup"><span data-stu-id="b2373-159">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="b2373-160">Per altre informazioni sulla creazione tramite modelli, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2373-160">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b2373-161">I modelli di Azure Resource Manager usano l'estensione dello script personalizzata per scaricare ed eseguire script nelle VM.</span><span class="sxs-lookup"><span data-stu-id="b2373-161">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="b2373-162">Per altre informazioni, vedere [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md) (Usare l'estensione dello script personalizzata di Azure con macchine virtuali Linux).</span><span class="sxs-lookup"><span data-stu-id="b2373-162">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

