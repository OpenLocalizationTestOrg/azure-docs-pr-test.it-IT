---
title: condivisione aaaFile per cluster di controller di dominio o sistema operativo di Azure | Documenti Microsoft
description: Creare e montare un cluster di controller di dominio/OS tooa condivisione file nel servizio contenitore di Azure
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, micro-servizi, Mesos, Azure, FileShare, CIFS
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>Creare e montare un cluster di controller di dominio/OS tooa condivisione file
In questa esercitazione illustra in dettaglio come toocreate condividere in Azure e montarlo in ogni agente e il master di un file hello cluster controller di dominio o del sistema operativo. Impostazione di una condivisione file rende più semplice tooshare file tra il cluster, ad esempio di configurazione, l'accesso, i registri e altro ancora. Hello seguenti attività viene eseguita in questa esercitazione:

> [!div class="checklist"]
> * Creare un account di archiviazione di Azure
> * Creare una condivisione file
> * Montare hello condivisione nel cluster di controller di dominio/OS hello

È necessario un ACS controller di dominio o sistema operativo hello toocomplete cluster i passaggi in questa esercitazione. Se necessario, questo [script di esempio](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) può crearne uno appositamente.

Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Creare una condivisione file in Microsoft Azure

Prima di utilizzare una condivisione di file di Azure con un cluster ACS controller di dominio o del sistema operativo, è necessario creare hello storage account e la condivisione file. Eseguire i seguenti script toocreate hello archiviazione e la condivisione file hello. Aggiornare i parametri di hello con thoes dall'ambiente in uso.

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a>Montare hello condivisione nel cluster

Successivamente, hello toobe esigenze di condivisione di file montati in ogni macchina virtuale all'interno del cluster. Questa attività viene completata utilizzando lo strumento/protocollo cifs hello. possibile completare l'operazione di montaggio Hello manualmente su ciascun nodo del cluster hello o tramite l'esecuzione di uno script in ogni nodo nel cluster hello.

In questo esempio, vengono eseguiti due script, uno toomount hello Azure file condivisione e un secondo toorun questo script in ogni nodo del cluster di controller di dominio/OS hello.

In primo luogo, sono necessari nome account di archiviazione di Azure hello e chiave di accesso. Eseguire hello tooget i comandi seguenti di queste informazioni. Prendere nota di tutti i valori perché vengono usati in un passaggio successivo.

Nome account di archiviazione:

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

Chiave di accesso dell'account di archiviazione:

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

Quindi, ottenere hello FQDN di hello DC/OS master e archiviarlo in una variabile.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Copia il nodo principale toohello chiave privata. Questa chiave è necessaria toocreate un ssh connessione con tutti i nodi cluster hello. Aggiornare il nome utente hello se è stato utilizzato un valore non predefinito durante la creazione di cluster hello. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

Creare una connessione SSH con hello master (o master prima di hello) del cluster basato su controller di dominio/OS. Aggiornare il nome utente hello se è stato utilizzato un valore non predefinito durante la creazione di cluster hello.

```azurecli-interactive
ssh azureuser@$FQDN
```

Creare un file denominato **cifsMount.sh**, e hello copia seguendo contenuto al suo interno. 

Questo script viene utilizzato toomount hello Azure in una condivisione. Hello aggiornamento `STORAGE_ACCT_NAME` e `ACCESS_KEY` variabili con le informazioni di hello raccolte in precedenza.

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
Creare un secondo file denominato **getNodesRunScript.sh** e hello copia seguente contenuto nel file hello. 

Questo script individua tutti i nodi del cluster e quindi esegue hello **cifsMount.sh** condivisione file di script toomount hello in ognuno.

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

Eseguire la condivisione file di Azure hello script toomount hello in tutti i nodi del cluster di hello.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

Hello condivisione file è ora possibile accedere al `/mnt/share/dcosshare` in ogni nodo del cluster di hello.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione di Azure condivisione file è stata effettuata tooa disponibili cluster di controller di dominio/OS attenendosi alla procedura hello:

> [!div class="checklist"]
> * Creare un account di archiviazione di Azure
> * Creare una condivisione file
> * Montare hello condivisione nel cluster di controller di dominio/OS hello

Spostare toohello Avanti toolearn esercitazione sull'integrazione di un registro di sistema di contenitore di Azure con controller di dominio o del sistema operativo in Azure.  

> [!div class="nextstepaction"]
> [Bilanciare il carico delle applicazioni](container-service-dcos-acr.md)