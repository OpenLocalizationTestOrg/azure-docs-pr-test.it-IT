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
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a><span data-ttu-id="3f598-104">Creare e montare un cluster di controller di dominio/OS tooa condivisione file</span><span class="sxs-lookup"><span data-stu-id="3f598-104">Create and mount a file share tooa DC/OS cluster</span></span>
<span data-ttu-id="3f598-105">In questa esercitazione illustra in dettaglio come toocreate condividere in Azure e montarlo in ogni agente e il master di un file hello cluster controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3f598-105">This tutorial details how toocreate a file share in Azure and mount it on each agent and master of hello DC/OS cluster.</span></span> <span data-ttu-id="3f598-106">Impostazione di una condivisione file rende più semplice tooshare file tra il cluster, ad esempio di configurazione, l'accesso, i registri e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="3f598-106">Setting up a file share makes it easier tooshare files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="3f598-107">Hello seguenti attività viene eseguita in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="3f598-107">hello following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f598-108">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3f598-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="3f598-109">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="3f598-109">Create a file share</span></span>
> * <span data-ttu-id="3f598-110">Montare hello condivisione nel cluster di controller di dominio/OS hello</span><span class="sxs-lookup"><span data-stu-id="3f598-110">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="3f598-111">È necessario un ACS controller di dominio o sistema operativo hello toocomplete cluster i passaggi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3f598-111">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="3f598-112">Se necessario, questo [script di esempio](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) può crearne uno appositamente.</span><span class="sxs-lookup"><span data-stu-id="3f598-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="3f598-113">Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3f598-113">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3f598-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="3f598-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3f598-115">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3f598-115">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="3f598-116">Creare una condivisione file in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3f598-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="3f598-117">Prima di utilizzare una condivisione di file di Azure con un cluster ACS controller di dominio o del sistema operativo, è necessario creare hello storage account e la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="3f598-117">Before using an Azure file share with an ACS DC/OS cluster, hello storage account and file share must be created.</span></span> <span data-ttu-id="3f598-118">Eseguire i seguenti script toocreate hello archiviazione e la condivisione file hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-118">Run hello following script toocreate hello storage and file share.</span></span> <span data-ttu-id="3f598-119">Aggiornare i parametri di hello con thoes dall'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="3f598-119">Update hello parameters with thoes from your environment.</span></span>

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

## <a name="mount-hello-share-in-your-cluster"></a><span data-ttu-id="3f598-120">Montare hello condivisione nel cluster</span><span class="sxs-lookup"><span data-stu-id="3f598-120">Mount hello share in your cluster</span></span>

<span data-ttu-id="3f598-121">Successivamente, hello toobe esigenze di condivisione di file montati in ogni macchina virtuale all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="3f598-121">Next, hello file share needs toobe mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="3f598-122">Questa attività viene completata utilizzando lo strumento/protocollo cifs hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-122">This task is completed using hello cifs tool/protocol.</span></span> <span data-ttu-id="3f598-123">possibile completare l'operazione di montaggio Hello manualmente su ciascun nodo del cluster hello o tramite l'esecuzione di uno script in ogni nodo nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-123">hello mount operation can be completed manually on each node of hello cluster, or by running a script against each node in hello cluster.</span></span>

<span data-ttu-id="3f598-124">In questo esempio, vengono eseguiti due script, uno toomount hello Azure file condivisione e un secondo toorun questo script in ogni nodo del cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-124">In this example, two scripts are run, one toomount hello Azure file share, and a second toorun this script on each node of hello DC/OS cluster.</span></span>

<span data-ttu-id="3f598-125">In primo luogo, sono necessari nome account di archiviazione di Azure hello e chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="3f598-125">First, hello Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="3f598-126">Eseguire hello tooget i comandi seguenti di queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="3f598-126">Run hello following commands tooget this information.</span></span> <span data-ttu-id="3f598-127">Prendere nota di tutti i valori perché vengono usati in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="3f598-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="3f598-128">Nome account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="3f598-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="3f598-129">Chiave di accesso dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="3f598-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="3f598-130">Quindi, ottenere hello FQDN di hello DC/OS master e archiviarlo in una variabile.</span><span class="sxs-lookup"><span data-stu-id="3f598-130">Next, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="3f598-131">Copia il nodo principale toohello chiave privata.</span><span class="sxs-lookup"><span data-stu-id="3f598-131">Copy your private key toohello master node.</span></span> <span data-ttu-id="3f598-132">Questa chiave è necessaria toocreate un ssh connessione con tutti i nodi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-132">This key is needed toocreate an ssh connection with all nodes in hello cluster.</span></span> <span data-ttu-id="3f598-133">Aggiornare il nome utente hello se è stato utilizzato un valore non predefinito durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-133">Update hello user name if a non-default value was used when creating hello cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="3f598-134">Creare una connessione SSH con hello master (o master prima di hello) del cluster basato su controller di dominio/OS.</span><span class="sxs-lookup"><span data-stu-id="3f598-134">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="3f598-135">Aggiornare il nome utente hello se è stato utilizzato un valore non predefinito durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-135">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="3f598-136">Creare un file denominato **cifsMount.sh**, e hello copia seguendo contenuto al suo interno.</span><span class="sxs-lookup"><span data-stu-id="3f598-136">Create a file named **cifsMount.sh**, and copy hello following contents into it.</span></span> 

<span data-ttu-id="3f598-137">Questo script viene utilizzato toomount hello Azure in una condivisione.</span><span class="sxs-lookup"><span data-stu-id="3f598-137">This script is used toomount hello Azure file share.</span></span> <span data-ttu-id="3f598-138">Hello aggiornamento `STORAGE_ACCT_NAME` e `ACCESS_KEY` variabili con le informazioni di hello raccolte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3f598-138">Update hello `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with hello information collected earlier.</span></span>

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
<span data-ttu-id="3f598-139">Creare un secondo file denominato **getNodesRunScript.sh** e hello copia seguente contenuto nel file hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-139">Create a second file named **getNodesRunScript.sh** and copy hello following contents into hello file.</span></span> 

<span data-ttu-id="3f598-140">Questo script individua tutti i nodi del cluster e quindi esegue hello **cifsMount.sh** condivisione file di script toomount hello in ognuno.</span><span class="sxs-lookup"><span data-stu-id="3f598-140">This script discovers all cluster nodes, and then runs hello **cifsMount.sh** script toomount hello file share on each.</span></span>

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

<span data-ttu-id="3f598-141">Eseguire la condivisione file di Azure hello script toomount hello in tutti i nodi del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-141">Run hello script toomount hello Azure file share on all nodes of hello cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="3f598-142">Hello condivisione file è ora possibile accedere al `/mnt/share/dcosshare` in ogni nodo del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="3f598-142">hello file share is now accessible at `/mnt/share/dcosshare` on each node of hello cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f598-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f598-143">Next steps</span></span>

<span data-ttu-id="3f598-144">In questa esercitazione di Azure condivisione file è stata effettuata tooa disponibili cluster di controller di dominio/OS attenendosi alla procedura hello:</span><span class="sxs-lookup"><span data-stu-id="3f598-144">In this tutorial an Azure file share was made available tooa DC/OS cluster using hello steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f598-145">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3f598-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="3f598-146">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="3f598-146">Create a file share</span></span>
> * <span data-ttu-id="3f598-147">Montare hello condivisione nel cluster di controller di dominio/OS hello</span><span class="sxs-lookup"><span data-stu-id="3f598-147">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="3f598-148">Spostare toohello Avanti toolearn esercitazione sull'integrazione di un registro di sistema di contenitore di Azure con controller di dominio o del sistema operativo in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f598-148">Advance toohello next tutorial toolearn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f598-149">Bilanciare il carico delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="3f598-149">Load balance applications</span></span>](container-service-dcos-acr.md)