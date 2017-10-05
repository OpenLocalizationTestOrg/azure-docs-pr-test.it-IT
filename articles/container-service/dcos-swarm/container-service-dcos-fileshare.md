---
title: Condivisione dei file per cluster DC/OS di Azure | Microsoft Docs
description: Creare e montare una condivisione di file per un cluster DC/OS nel servizio contenitore di Azure
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
ms.openlocfilehash: 549b52bfb0a0268f754da26c6a374b267861f6d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-mount-a-file-share-to-a-dcos-cluster"></a><span data-ttu-id="72b66-104">Creare e montare una condivisione di file per un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="72b66-104">Create and mount a file share to a DC/OS cluster</span></span>
<span data-ttu-id="72b66-105">Questa esercitazione illustra nei dettagli come creare una condivisione file in Azure e come montarla in ogni agente e nel master del cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="72b66-105">This tutorial details how to create a file share in Azure and mount it on each agent and master of the DC/OS cluster.</span></span> <span data-ttu-id="72b66-106">La configurazione della condivisione file semplifica la condivisione di file tra i cluster ad esempio configurazione, accesso, log e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="72b66-106">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="72b66-107">Nell'esercitazione verranno eseguite le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b66-107">The following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72b66-108">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="72b66-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="72b66-109">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="72b66-109">Create a file share</span></span>
> * <span data-ttu-id="72b66-110">Montare la condivisione nel cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="72b66-110">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="72b66-111">È necessario un cluster DC/OS del servizio contenitore di Azure per completare i passaggi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="72b66-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="72b66-112">Se necessario, questo [script di esempio](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) può crearne uno appositamente.</span><span class="sxs-lookup"><span data-stu-id="72b66-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="72b66-113">Questa esercitazione richiede l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="72b66-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="72b66-114">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="72b66-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="72b66-115">Se è necessario eseguire l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="72b66-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="72b66-116">Creare una condivisione file in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="72b66-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="72b66-117">Prima di usare una condivisione file di Azure con un cluster DC/OS del servizio contenitore di Azure, è necessario creare l'account di archiviazione e la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="72b66-117">Before using an Azure file share with an ACS DC/OS cluster, the storage account and file share must be created.</span></span> <span data-ttu-id="72b66-118">Eseguire lo script seguente per creare l'account di archiviazione e la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="72b66-118">Run the following script to create the storage and file share.</span></span> <span data-ttu-id="72b66-119">Aggiornare i parametri con valori appropriati dall'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="72b66-119">Update the parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create the storage account with the parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-the-share-in-your-cluster"></a><span data-ttu-id="72b66-120">Montare la condivisione nel cluster</span><span class="sxs-lookup"><span data-stu-id="72b66-120">Mount the share in your cluster</span></span>

<span data-ttu-id="72b66-121">La condivisione file deve poi essere montata in ogni macchina virtuale all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="72b66-121">Next, the file share needs to be mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="72b66-122">Questa attività viene eseguita tramite lo strumento/protocollo CIFS.</span><span class="sxs-lookup"><span data-stu-id="72b66-122">This task is completed using the cifs tool/protocol.</span></span> <span data-ttu-id="72b66-123">È possibile eseguire manualmente l'operazione di montaggio su ogni nodo del cluster o eseguendo uno script su ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="72b66-123">The mount operation can be completed manually on each node of the cluster, or by running a script against each node in the cluster.</span></span>

<span data-ttu-id="72b66-124">In questo esempio, vengono eseguiti due script, uno per montare la condivisione file di Azure e il secondo per eseguire questo script in ogni nodo del cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="72b66-124">In this example, two scripts are run, one to mount the Azure file share, and a second to run this script on each node of the DC/OS cluster.</span></span>

<span data-ttu-id="72b66-125">Servono innanzitutto il nome dell'account di archiviazione di Azure e la chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="72b66-125">First, the Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="72b66-126">Eseguire i comandi seguenti per ottenere queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="72b66-126">Run the following commands to get this information.</span></span> <span data-ttu-id="72b66-127">Prendere nota di tutti i valori perché vengono usati in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="72b66-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="72b66-128">Nome account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="72b66-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="72b66-129">Chiave di accesso dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="72b66-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="72b66-130">Ottenere poi il nome di dominio completo del master DC/OS e archiviarlo in una variabile.</span><span class="sxs-lookup"><span data-stu-id="72b66-130">Next, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="72b66-131">Copiare la chiave privata nel nodo master.</span><span class="sxs-lookup"><span data-stu-id="72b66-131">Copy your private key to the master node.</span></span> <span data-ttu-id="72b66-132">Questa chiave è necessaria per creare una connessione SSH con tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="72b66-132">This key is needed to create an ssh connection with all nodes in the cluster.</span></span> <span data-ttu-id="72b66-133">Aggiornare il nome utente se è stato usato un valore non predefinito al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="72b66-133">Update the user name if a non-default value was used when creating the cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="72b66-134">Creare una connessione SSH con il master (o il primo master) del cluster basato su DC/OS.</span><span class="sxs-lookup"><span data-stu-id="72b66-134">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="72b66-135">Aggiornare il nome utente se è stato usato un valore non predefinito al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="72b66-135">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="72b66-136">Creare un file denominato **cifsMount.sh** e copiare il contenuto seguente nel file.</span><span class="sxs-lookup"><span data-stu-id="72b66-136">Create a file named **cifsMount.sh**, and copy the following contents into it.</span></span> 

<span data-ttu-id="72b66-137">Questo script viene usato per montare la condivisione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="72b66-137">This script is used to mount the Azure file share.</span></span> <span data-ttu-id="72b66-138">Aggiornare le variabili `STORAGE_ACCT_NAME` e `ACCESS_KEY` con le informazioni raccolte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="72b66-138">Update the `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with the information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install the cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create the local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount the share under the previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="72b66-139">Creare un secondo file denominato **getNodesRunScript.sh** e copiare il contenuto seguente nel file.</span><span class="sxs-lookup"><span data-stu-id="72b66-139">Create a second file named **getNodesRunScript.sh** and copy the following contents into the file.</span></span> 

<span data-ttu-id="72b66-140">Questo script individua tutti i nodi del cluster e quindi esegue lo script **cifsMount.sh** per montare la condivisione file in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="72b66-140">This script discovers all cluster nodes, and then runs the **cifsMount.sh** script to mount the file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for the next command
sudo apt-get install jq -y

# Get the IP address of each node using the mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From the previous file created, run our script to mount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="72b66-141">Eseguire lo script per montare la condivisione file di Azure in tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="72b66-141">Run the script to mount the Azure file share on all nodes of the cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="72b66-142">La condivisione file è ora accessibile dal percorso `/mnt/share/dcosshare` in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="72b66-142">The file share is now accessible at `/mnt/share/dcosshare` on each node of the cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72b66-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72b66-143">Next steps</span></span>

<span data-ttu-id="72b66-144">In questa esercitazione è stata resa disponibile una condivisione file di Azure per un cluster DC/OS tramite questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="72b66-144">In this tutorial an Azure file share was made available to a DC/OS cluster using the steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72b66-145">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="72b66-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="72b66-146">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="72b66-146">Create a file share</span></span>
> * <span data-ttu-id="72b66-147">Montare la condivisione nel cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="72b66-147">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="72b66-148">Passare alla prossima esercitazione per informazioni sull'integrazione di Registro contenitori di Azure. con DC/OS in Azure.</span><span class="sxs-lookup"><span data-stu-id="72b66-148">Advance to the next tutorial to learn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="72b66-149">Bilanciare il carico delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="72b66-149">Load balance applications</span></span>](container-service-dcos-acr.md)