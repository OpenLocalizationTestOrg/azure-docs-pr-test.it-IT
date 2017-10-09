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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>Come tooinstall e configurare MongoDB in una VM Linux utilizzando hello Azure CLI 1.0
[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate. In questo articolo illustra come tooinstall e configurare MongoDB in una VM Linux di Azure tramite il modello di distribuzione di gestione risorse di hello. Alcuni esempi illustrano in dettaglio come fare a:

* [Installare e configurare manualmente un'istanza di MongoDB di base](#manually-install-and-configure-mongodb-on-a-vm)
* [Creare un'istanza di MongoDB di base usando un modello di Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Creare un cluster complesso di MongoDB partizionato con set di repliche usando un modello di Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- CLI di Azure 1.0-nostri CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](create-cli-complete-nodejs.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Installare e configurare manualmente MongoDB su una VM
MongoDB [fornisce le istruzioni di installazione](https://docs.mongodb.com/manual/administration/install-on-linux/) per i sistemi operativi Linux Red Hat/CentOS, SUSE, Ubuntu e Debian. Hello esempio seguente viene creato un *CentOS* macchina virtuale usando una chiave SSH è archiviata in *~/.ssh/id_rsa.pub*. Hello risposta richiede il nome account di archiviazione, nome DNS e credenziali di amministratore:

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

Accedere toohello VM utilizzando l'indirizzo IP pubblico hello visualizzato alla fine hello hello precedente passaggio di creazione della macchina virtuale:

```bash
ssh azureuser@40.78.23.145
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

Per impostazione predefinita, alle immagini CentOS è applicato SELinux, che impedisce di accedere a MongoDB. Installare gli strumenti di gestione di criteri e configurare SELinux tooallow MongoDB toooperate sulla porta TCP predefinita 27017 come indicato di seguito. 

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
È possibile creare un'istanza di MongoDB base in una singola macchina virtuale CentOS usando hello segue il modello di avvio rapido di Azure da GitHub. Questo modello Usa l'estensione Custom Script hello per Linux tooadd un `yum` tooyour repository creata la macchina virtuale CentOS e quindi installare MongoDB.

* [Istanza di MongoDB di base su CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

Hello seguente viene creato un gruppo di risorse con nome hello `myResourceGroup` in hello `eastus` area. Immettere valori personalizzati come di seguito:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> Hello CLI di Azure restituisce tooa richiesta entro pochi secondi di creazione di distribuzione di hello, ma l'installazione di hello e configurazione accetta toocomplete di pochi minuti. Controllare lo stato di hello della distribuzione hello con `azure group deployment show myResourceGroup`, di conseguenza l'immissione di nome hello del gruppo di risorse. Attendere hello **ProvisioningState** Mostra *Succeeded* prima durante il tentativo tooSSH toohello macchina virtuale.

Dopo la distribuzione di hello è completata, SSH toohello macchina virtuale. Ottenere l'indirizzo IP hello della macchina virtuale utilizzando hello `azure vm show` comando come hello di esempio seguente:

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

In prossimità di fine hello dell'output di hello, viene visualizzato l'indirizzo IP pubblico hello. SSH tooyour macchina virtuale con indirizzo IP hello la macchina virtuale:

```bash
ssh azureuser@138.91.149.74
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

Hello seguente viene creato un gruppo di risorse con nome hello *myResourceGroup* in hello *eastus* area. Immettere valori personalizzati come di seguito:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> Hello CLI di Azure restituisce tooa richiesta entro pochi secondi di creazione di distribuzione di hello, ma hello installazione e la configurazione può richiedere più di un toocomplete ora. Controllare lo stato di hello della distribuzione hello con `azure group deployment show myResourceGroup`, regolando il nome di hello del gruppo di risorse di conseguenza. Attendere hello **ProvisioningState** Mostra *Succeeded* prima di connettere le macchine virtuali toohello.


## <a name="next-steps"></a>Passaggi successivi
In questi esempi, è connettersi toohello MongoDB istanza localmente da hello macchina virtuale. Se si desidera tooconnect toohello MongoDB istanza da un'altra macchina virtuale o una rete, assicurarsi di hello appropriato [vengono create regole Network Security Group](nsg-quickstart.md).

Per ulteriori informazioni sulla creazione di modelli, vedere hello [Panoramica di gestione risorse di Azure](../../azure-resource-manager/resource-group-overview.md).

modelli di Azure Resource Manager Hello utilizzano toodownload estensione Script personalizzata hello ed eseguire script in macchine virtuali. Per ulteriori informazioni, vedere [Using hello estensione Script personalizzata di Azure con le macchine virtuali Linux](extensions-customscript.md).

