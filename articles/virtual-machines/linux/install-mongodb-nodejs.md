---
title: aaaInstall MongoDB in una VM Linux utilizzando hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come tooinstall e configurare MongoDB in una macchina virtuale di Linux in Azure tramite il modello di distribuzione di gestione risorse di hello.
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
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="8298b-103">Come tooinstall e configurare MongoDB in una VM Linux utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8298b-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="8298b-104">[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="8298b-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="8298b-105">In questo articolo illustra come tooinstall e configurare MongoDB in una VM Linux di Azure tramite il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="8298b-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="8298b-106">Alcuni esempi illustrano in dettaglio come fare a:</span><span class="sxs-lookup"><span data-stu-id="8298b-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="8298b-107">Installare e configurare manualmente un'istanza di MongoDB di base</span><span class="sxs-lookup"><span data-stu-id="8298b-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="8298b-108">Creare un'istanza di MongoDB di base usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8298b-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="8298b-109">Creare un cluster complesso di MongoDB partizionato con set di repliche usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8298b-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8298b-110">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="8298b-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="8298b-111">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="8298b-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="8298b-112">CLI di Azure 1.0-nostri CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="8298b-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8298b-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="8298b-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="8298b-114">Installare e configurare manualmente MongoDB su una VM</span><span class="sxs-lookup"><span data-stu-id="8298b-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="8298b-115">MongoDB [fornisce le istruzioni di installazione](https://docs.mongodb.com/manual/administration/install-on-linux/) per i sistemi operativi Linux Red Hat/CentOS, SUSE, Ubuntu e Debian.</span><span class="sxs-lookup"><span data-stu-id="8298b-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="8298b-116">Hello esempio seguente viene creato un *CentOS* macchina virtuale usando una chiave SSH è archiviata in *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="8298b-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="8298b-117">Hello risposta richiede il nome account di archiviazione, nome DNS e credenziali di amministratore:</span><span class="sxs-lookup"><span data-stu-id="8298b-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="8298b-118">Accedere toohello VM utilizzando l'indirizzo IP pubblico hello visualizzato alla fine hello hello precedente passaggio di creazione della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="8298b-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="8298b-119">origine dell'installazione di hello tooadd per MongoDB, creare un **yum** file del repository come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8298b-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="8298b-120">Aprire il file di repository hello MongoDB per la modifica.</span><span class="sxs-lookup"><span data-stu-id="8298b-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="8298b-121">Aggiungere hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="8298b-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="8298b-122">Installare MongoDB usando **yum** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8298b-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="8298b-123">Per impostazione predefinita, alle immagini CentOS è applicato SELinux, che impedisce di accedere a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8298b-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="8298b-124">Installare gli strumenti di gestione di criteri e configurare SELinux tooallow MongoDB toooperate sulla porta TCP predefinita 27017 come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8298b-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="8298b-125">Avviare il servizio di MongoDB hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8298b-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="8298b-126">Verificare l'installazione di MongoDB hello connettendosi usando hello locale `mongo` client:</span><span class="sxs-lookup"><span data-stu-id="8298b-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="8298b-127">Ora è possibile testare istanza MongoDB hello aggiungendo alcuni dati e quindi la ricerca:</span><span class="sxs-lookup"><span data-stu-id="8298b-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="8298b-128">Se si desidera, configurare MongoDB toostart automaticamente durante un riavvio del sistema:</span><span class="sxs-lookup"><span data-stu-id="8298b-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="8298b-129">Creare un'istanza di MongoDB di base su CentOS usando un modello</span><span class="sxs-lookup"><span data-stu-id="8298b-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="8298b-130">È possibile creare un'istanza di MongoDB base in una singola macchina virtuale CentOS usando hello segue il modello di avvio rapido di Azure da GitHub.</span><span class="sxs-lookup"><span data-stu-id="8298b-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="8298b-131">Questo modello Usa l'estensione Custom Script hello per Linux tooadd un `yum` tooyour repository creata la macchina virtuale CentOS e quindi installare MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8298b-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="8298b-132">[Istanza di MongoDB di base su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="8298b-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="8298b-133">Hello seguente viene creato un gruppo di risorse con nome hello `myResourceGroup` in hello `eastus` area.</span><span class="sxs-lookup"><span data-stu-id="8298b-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="8298b-134">Immettere valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="8298b-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="8298b-135">Hello CLI di Azure restituisce tooa richiesta entro pochi secondi di creazione di distribuzione di hello, ma l'installazione di hello e configurazione accetta toocomplete di pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="8298b-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="8298b-136">Controllare lo stato di hello della distribuzione hello con `azure group deployment show myResourceGroup`, di conseguenza l'immissione di nome hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8298b-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="8298b-137">Attendere hello **ProvisioningState** Mostra *Succeeded* prima durante il tentativo tooSSH toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8298b-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="8298b-138">Dopo la distribuzione di hello è completata, SSH toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8298b-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="8298b-139">Ottenere l'indirizzo IP hello della macchina virtuale utilizzando hello `azure vm show` comando come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8298b-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="8298b-140">In prossimità di fine hello dell'output di hello, viene visualizzato l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="8298b-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="8298b-141">SSH tooyour macchina virtuale con indirizzo IP hello la macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="8298b-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="8298b-142">Verificare l'installazione di MongoDB hello connettendosi usando hello locale `mongo` client come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8298b-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="8298b-143">Ora hello istanza test aggiungendo alcuni dati e la ricerca come segue:</span><span class="sxs-lookup"><span data-stu-id="8298b-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="8298b-144">Creare un cluster complesso di MongoDB partizionato in CentOS usando un modello</span><span class="sxs-lookup"><span data-stu-id="8298b-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="8298b-145">È possibile creare un cluster di partizionati MongoDB complesso utilizzando hello segue il modello di avvio rapido di Azure da GitHub.</span><span class="sxs-lookup"><span data-stu-id="8298b-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="8298b-146">Questo modello segue hello [procedure consigliate di MongoDB cluster partizionati](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide disponibilità elevata e ridondanza.</span><span class="sxs-lookup"><span data-stu-id="8298b-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="8298b-147">Hello modello consente di creare due partizioni, con tre nodi in ogni set di repliche.</span><span class="sxs-lookup"><span data-stu-id="8298b-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="8298b-148">Una replica di server di configurazione impostata con tre nodi viene creata anche, più due **mongos** router di server di tooprovide di coerenza tooapplications da tra partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="8298b-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="8298b-149">[Cluster di partizionamento di MongoDB su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="8298b-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="8298b-150">Distribuzione di cluster partizionati MongoDB complesso richiede più di 20 core, che è in genere hello numero di core predefinita per ogni area per una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8298b-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="8298b-151">Aprire un tooincrease di richiesta di supporto tecnico di Azure il numero di core.</span><span class="sxs-lookup"><span data-stu-id="8298b-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="8298b-152">Hello seguente viene creato un gruppo di risorse con nome hello *myResourceGroup* in hello *eastus* area.</span><span class="sxs-lookup"><span data-stu-id="8298b-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="8298b-153">Immettere valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="8298b-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="8298b-154">Hello CLI di Azure restituisce tooa richiesta entro pochi secondi di creazione di distribuzione di hello, ma hello installazione e la configurazione può richiedere più di un toocomplete ora.</span><span class="sxs-lookup"><span data-stu-id="8298b-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="8298b-155">Controllare lo stato di hello della distribuzione hello con `azure group deployment show myResourceGroup`, regolando il nome di hello del gruppo di risorse di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="8298b-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="8298b-156">Attendere hello **ProvisioningState** Mostra *Succeeded* prima di connettere le macchine virtuali toohello.</span><span class="sxs-lookup"><span data-stu-id="8298b-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8298b-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8298b-157">Next steps</span></span>
<span data-ttu-id="8298b-158">In questi esempi, è connettersi toohello MongoDB istanza localmente da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8298b-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="8298b-159">Se si desidera tooconnect toohello MongoDB istanza da un'altra macchina virtuale o una rete, assicurarsi di hello appropriato [vengono create regole Network Security Group](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="8298b-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="8298b-160">Per ulteriori informazioni sulla creazione di modelli, vedere hello [Panoramica di gestione risorse di Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8298b-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="8298b-161">modelli di Azure Resource Manager Hello utilizzano toodownload estensione Script personalizzata hello ed eseguire script in macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8298b-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="8298b-162">Per ulteriori informazioni, vedere [Using hello estensione Script personalizzata di Azure con le macchine virtuali Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="8298b-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

