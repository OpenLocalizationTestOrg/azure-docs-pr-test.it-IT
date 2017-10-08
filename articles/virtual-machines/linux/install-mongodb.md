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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>Come tooinstall e configurare MongoDB in una VM Linux
[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate. In questo articolo illustra come tooinstall e configurare MongoDB in una VM Linux con hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](install-mongodb-nodejs.md). Alcuni esempi illustrano in dettaglio come fare a:

* [Installare e configurare manualmente un'istanza di MongoDB di base](#manually-install-and-configure-mongodb-on-a-vm)
* [Creare un'istanza di MongoDB di base usando un modello di Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Creare un cluster complesso di MongoDB partizionato con set di repliche usando un modello di Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Installare e configurare manualmente MongoDB su una VM
MongoDB [fornisce le istruzioni di installazione](https://docs.mongodb.com/manual/administration/install-on-linux/) per i sistemi operativi Linux Red Hat/CentOS, SUSE, Ubuntu e Debian. Hello esempio seguente viene creato un *CentOS* macchina virtuale. toocreate questo ambiente, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroup --location eastus
```

Creare una VM con il comando [az vm create](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata *myVM* con un utente denominato *azureuser* utilizzando l'autenticazione con chiave pubblica SSH

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello VM usando il proprio nome utente e hello `publicIpAddress` elencati nell'output di hello dal passaggio precedente hello:

```bash
ssh azureuser@<publicIpAddress>
```

origine dell'installazione di hello tooadd per MongoDB, creare un **yum** file del repository come indicato di seguito:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Aprire il file di repository hello MongoDB per la modifica. Aggiungere hello seguenti righe:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

Installare MongoDB usando **yum** come illustrato di seguito:

```bash
sudo yum install -y mongodb-org
```

Per impostazione predefinita, alle immagini CentOS è applicato SELinux, che impedisce di accedere a MongoDB. Installare strumenti di gestione di criteri e configurare SELinux tooallow MongoDB toooperate sulla porta TCP predefinita 27017 come segue:

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Avviare il servizio di MongoDB hello come indicato di seguito:

```bash
sudo service mongod start
```

Verificare l'installazione di MongoDB hello connettendosi usando hello locale `mongo` client:

```bash
mongo
```

Ora è possibile testare istanza MongoDB hello aggiungendo alcuni dati e quindi la ricerca:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

Se si desidera, configurare MongoDB toostart automaticamente durante un riavvio del sistema:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Creare un'istanza di MongoDB di base su CentOS usando un modello
È possibile creare un'istanza di MongoDB base in una singola macchina virtuale CentOS usando hello segue il modello di avvio rapido di Azure da GitHub. Questo modello Usa l'estensione Custom Script hello per Linux tooadd un **yum** tooyour repository creata la macchina virtuale CentOS e quindi installare MongoDB.

* [Istanza di MongoDB di base su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate questo ambiente, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login). Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroup --location eastus
```

Successivamente, distribuire il modello di MongoDB hello con [distribuzione gruppo az creare](/cli/azure/group/deployment#create). Definire i nomi e le dimensioni delle risorse desiderati dove necessario per *newStorageAccountName*, *virtualNetworkName* e *vmSize*:

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

Accedere toohello VM utilizzando l'indirizzo DNS pubblico hello della macchina virtuale. È possibile visualizzare l'indirizzo DNS pubblico hello con [Mostra vm az](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour VM usando il proprio nome utente e l'indirizzo DNS pubblico:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Verificare l'installazione di MongoDB hello connettendosi usando hello locale `mongo` client come indicato di seguito:

```bash
mongo
```

Ora hello istanza test aggiungendo alcuni dati e la ricerca come segue:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Creare un cluster complesso di MongoDB partizionato in CentOS usando un modello
È possibile creare un cluster di partizionati MongoDB complesso utilizzando hello segue il modello di avvio rapido di Azure da GitHub. Questo modello segue hello [procedure consigliate di MongoDB cluster partizionati](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide disponibilità elevata e ridondanza. Hello modello consente di creare due partizioni, con tre nodi in ogni set di repliche. Una replica di server di configurazione impostata con tre nodi viene creata anche, più due **mongos** router di server di tooprovide di coerenza tooapplications da tra partizioni hello.

* [Cluster di partizionamento di MongoDB su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Distribuzione di cluster partizionati MongoDB complesso richiede più di 20 core, che è in genere hello numero di core predefinita per ogni area per una sottoscrizione. Aprire un tooincrease di richiesta di supporto tecnico di Azure il numero di core.

toocreate questo ambiente, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login). Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroup --location eastus
```

Successivamente, distribuire il modello di MongoDB hello con [distribuzione gruppo az creare](/cli/azure/group/deployment#create). Definire i nomi e le dimensioni delle risorse desiderati dove necessario per *mongoAdminUsername*, *sizeOfDataDiskInGB* e *configNodeVmSize*:

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

Questa distribuzione può assumere un toodeploy ora e configurare tutte le istanze VM hello. Hello `--no-wait` flag viene utilizzato alla fine hello hello precedente prompt dei comandi di comando tooreturn controllo toohello dopo la distribuzione dei modelli di hello è stato accettato dalla piattaforma Azure hello. È quindi possibile visualizzare lo stato di distribuzione hello con [Mostra la distribuzione di gruppo az](/cli/azure/group/deployment#show). viste di esempio seguenti Hello hello stato per hello *myMongoDBCluster* distribuzione in hello *myResourceGroup* gruppo di risorse:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Passaggi successivi
In questi esempi, è connettersi toohello MongoDB istanza localmente da hello macchina virtuale. Se si desidera tooconnect toohello MongoDB istanza da un'altra macchina virtuale o una rete, assicurarsi di hello appropriato [vengono create regole Network Security Group](nsg-quickstart.md).

Questi esempi distribuirlo hello core MongoDB per scopi di sviluppo. Applicare opzioni di configurazione di sicurezza hello necessario per l'ambiente. Per ulteriori informazioni, vedere hello [documenti sicurezza MongoDB](https://docs.mongodb.com/manual/security/).

Per ulteriori informazioni sulla creazione di modelli, vedere hello [Panoramica di gestione risorse di Azure](../../azure-resource-manager/resource-group-overview.md).

modelli di Azure Resource Manager Hello utilizzano toodownload estensione Script personalizzata hello ed eseguire script in macchine virtuali. Per ulteriori informazioni, vedere [Using hello estensione Script personalizzata di Azure con le macchine virtuali Linux](extensions-customscript.md).

