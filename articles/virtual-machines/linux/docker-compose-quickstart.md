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
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Ottenere avviato con toodefine Docker e di scrittura e l'esecuzione di un'applicazione multi-contenitore in Azure
Con [comporre](http://github.com/docker/compose), utilizzare un toodefine di file di testo semplice un'applicazione composta da più contenitori di Docker. Quindi di creare rapidamente l'applicazione in un unico comando che esegue tutti gli elementi toodeploy l'ambiente definito. Ad esempio, questo articolo illustra come tooquickly impostare un blog di WordPress con un back-end del database SQL MariaDB in una VM Ubuntu. È anche possibile utilizzare tooset comporre le applicazioni più complesse.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Configurare una macchina virtuale Linux come host Docker
È possibile utilizzare varie procedure di Azure e le immagini disponibili o modelli di gestione risorse in hello Azure Marketplace toocreate una VM Linux e configurarlo come host Docker. Ad esempio, vedere [utilizzando l'ambiente di hello estensione della macchina virtuale Docker toodeploy](dockerextension.md) tooquickly creare una VM Ubuntu con hello estensione della macchina virtuale Docker di Azure utilizzando un [modello delle Guide rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Quando si utilizza l'estensione della macchina virtuale Docker hello, la macchina virtuale viene impostata automaticamente come un host Docker e comporre è già installato.


### <a name="create-docker-host-with-azure-cli-20"></a>Creare un host Docker con l'interfaccia della riga di comando di Azure 2.0
Hello installazione più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).

Innanzitutto, creare un gruppo di risorse per l'ambiente di Docker con il comando [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westus* percorso:

```azurecli
az group create --name myResourceGroup --location westus
```

Successivamente, distribuire una macchina virtuale con [distribuzione gruppo az creare](/cli/azure/group/deployment#create) che include l'estensione della macchina virtuale Docker di Azure hello da [questo modello di gestione risorse di Azure su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Specificare i propri valori per *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Sono necessari alcuni minuti per hello toofinish di distribuzione. Una volta terminata la distribuzione di hello, [Sposta passaggio toonext](#verify-that-compose-is-installed) tooSSH tooyour macchina virtuale. 

Facoltativamente, prompt dei comandi di tooinstead controllo restituito toohello e distribuzione hello let continuano in background hello, aggiungere hello `--no-wait` flag toohello precedente comando. Questo processo consente tooperform altre operazioni in hello CLI mentre hello distribuzione continua per alcuni minuti. È quindi possibile visualizzare i dettagli sullo stato dell'host Docker hello con [Mostra vm az](/cli/azure/vm#show). esempio Hello Controlla stato hello della macchina virtuale denominata hello *myDockerVM* (nome predefinito dal modello hello hello, non modificare questo nome) nel gruppo di risorse hello denominato *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Quando questo comando restituisce *Succeeded*, distribuzione hello è terminata ed è possibile SSH toohello VM in hello riportata dopo il passaggio.


## <a name="verify-that-compose-is-installed"></a>Verificare che Compose sia installato
Una volta terminata la distribuzione di hello, SSH tooyour nuovo host Docker con il nome DNS hello fornite durante la distribuzione. È possibile utilizzare `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview dettagli della macchina virtuale, incluso il nome DNS hello.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

toocheck che compongono è installato nel hello macchina virtuale, eseguire hello comando seguente:

```bash
docker-compose --version
```

Viene visualizzato un output simile*docker-comporre 1.6.2, compilazione 4D 72027*.

> [!TIP]
> Se è stato utilizzato un altro metodo toocreate un host Docker e necessario tooinstall comporre manualmente, vedere hello [comporre documentazione](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Creare un file di configurazione docker-compose.yml
Successivamente è possibile creare un `docker-compose.yml` file, è sufficiente un file di testo, toodefine hello Docker contenitori toorun su hello macchina virtuale. file Hello specifica hello immagine toorun su ciascun contenitore oppure può trattarsi di una compilazione di un Dockerfile, variabili di ambiente necessarie e le dipendenze, porte e collegamenti hello tra contenitori. Per informazioni dettagliate sulla sintassi dei file YML, vedere [Compose file reference](https://docs.docker.com/compose/compose-file/)(Informazioni di riferimento sui file di Compose).

Creare hello *docker compose.yml* file come segue:

```bash
touch docker-compose.yml
```

Utilizzare il tooadd editor di testo preferito alcuni file di dati toohello. esempio Hello utilizza hello *vi* editor:

```bash
vi docker-compose.yml
```

Incollare l'esempio seguente nel file di testo hello. Questa configurazione usa le immagini hello [Registro di sistema DockerHub](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello Apri origine blog e contenuto management system) e un back-end collegato MariaDB SQL database. Immettere il proprio valore *MYSQL_ROOT_PASSWORD* come segue:

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

## <a name="start-hello-containers-with-compose"></a>Inizio hello contenitori con composizione
In hello stessa directory come la *docker compose.yml* file, eseguire hello comando seguente (a seconda dell'ambiente, potrebbe essere necessario toorun `docker-compose` utilizzando `sudo`):

```bash
docker-compose up -d
```

Questo comando Avvia contenitori Docker hello specificati nella *docker compose.yml*. Accetta un o due minuti per toocomplete questo passaggio. Vedrai toohello simili di output esempio seguente:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Essere certi hello toouse **-d** opzione all'avvio in modo che hello contenitori vengono eseguiti in background hello in modo continuo.


tooverify che sono contenitori di hello, tipo `docker-compose ps`. Dovrebbe essere visualizzata una schermata analoga alla seguente:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

È ora possibile connettersi tooWordPress direttamente nella macchina virtuale sulla porta 80 hello. Aprire un web browser e immettere il nome DNS hello della macchina virtuale (ad esempio `http://mypublicdns.westus.cloudapp.azure.com`). Dovrebbe essere hello che WordPress avviare schermo, in cui è possibile completare l'installazione di hello e iniziare con un'applicazione hello.

![Schermata iniziale di WordPress][wordpress_start]

## <a name="next-steps"></a>Passaggi successivi
* Passare toohello [Guida dell'utente dell'estensione VM Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) per altre opzioni tooconfigure Docker e nella macchina virtuale Docker Compose. Ad esempio, un'opzione è tooput hello comporre yml file (convertito tooJSON) direttamente nella configurazione di hello di hello estensione della macchina virtuale Docker.
* Estrarre hello [comporre riferimento della riga di comando](http://docs.docker.com/compose/reference/) e [manuale dell'utente](http://docs.docker.com/compose/) per ulteriori esempi di compilazione e distribuzione di applicazioni multi-contenitore.
* Utilizzare un modello di gestione risorse di Azure, ovvero il proprio o uno provengono da hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy una macchina virtuale di Azure con Docker e un'applicazione è configurato con la composizione. Ad esempio, hello [distribuire un blog di WordPress con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) modello Usa Docker e comporre tooquickly distribuire WordPress con un back-end di MySQL in una VM Ubuntu.
* Provare a integrare Docker Compose con un cluster Docker Swarm. Per gli scenari, vedere [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) (Uso di Swarm con Compose).

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
