---
title: ospita aaaUse macchina Docker toocreate Linux in Azure | Documenti Microsoft
description: Viene descritto come toouse macchina Docker toocreate Docker ospitata in Azure.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a>Come toouse Docker macchina toocreate ospitata in Azure
Questo articolo come dettagli toouse [Docker macchina](https://docs.docker.com/machine/) host toocreate in Azure. Hello `docker-machine` comando crea una macchina virtuale Linux (VM) in Azure, quindi installa Docker. È quindi possibile gestire gli host Docker in Azure tramite hello stessi strumenti locali e i flussi di lavoro.

## <a name="create-vms-with-docker-machine"></a>Creare VM con Docker Machine
Ottenere prima di tutto l'ID sottoscrizione di Azure con [az account show](/cli/azure/account#show) nel modo seguente:

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Creare le macchine virtuali host Docker in Azure con `docker-machine create` specificando *azure* come driver hello. Per ulteriori informazioni, vedere hello [documentazione del Driver di Azure di Docker](https://docs.docker.com/machine/drivers/azure/)

esempio Hello crea una macchina virtuale denominata *myVM*, crea un account utente denominato *azureuser*e l'apertura della porta *80* in hello host macchina virtuale. Seguire toolog qualsiasi richiesta in tooyour account Azure e concedere toocreate autorizzazioni macchina Docker e gestire le risorse.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

output di Hello è simile toohello esempio seguente:

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>Configurare la shell di Docker
host di tooconnect tooyour Docker in Azure, definire le impostazioni di connessione appropriata hello. Come indicato alla fine di hello dell'output di hello, visualizzare informazioni di connessione hello per l'host Docker come segue: 

```bash
docker-machine env myvmdocker
```

Hello l'output è simile toohello seguente esempio:

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

è possibile l'esecuzione hello le impostazioni di connessione di toodefine hello consigliate comando di configurazione (`eval $(docker-machine env myvmdocker)`), oppure è possibile impostare le variabili di ambiente hello manualmente. 

## <a name="run-a-container"></a>Eseguire un contenitore
toosee un contenitore in azione, consente l'esecuzione di un server Web NGINX di base. Creare un contenitore con `docker run` ed esporre la porta 80 al traffico Web nel modo seguente:

```bash
docker run -d -p 80:80 --restart=always nginx
```

Hello l'output è simile toohello seguente esempio:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Visualizzare i contenitori in esecuzione con `docker ps`. Hello output di esempio seguente viene illustrato hello NGINX contenitore in esecuzione con la porta 80 esposti:

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a>Contenitore di test hello
Ottenere hello indirizzo IP dell'host Docker come indicato di seguito:


```bash
docker-machine ip myvmdocker
```

contenitore hello toosee in azione, aprire un web browser e immettere l'indirizzo IP pubblico hello indicato nell'output di hello di hello precedente comando:

![Esecuzione di un contenitore ngnix](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Passaggi successivi
È inoltre possibile creare l'host con hello [estensione della macchina virtuale Docker](dockerextension.md). Per esempi sull'uso di Docker Compose, vedere [Introduzione a Docker e Compose in Azure](docker-compose-quickstart.md).
