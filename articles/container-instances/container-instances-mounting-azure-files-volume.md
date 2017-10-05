---
title: Montare un volume di File di Azure in Istanze di contenitore di Azure
description: Informazioni su come montare un volume di File di Azure per rendere persistente lo stato con Istanze di contenitore di Azure
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 4248a3769ba8a0fb067b3904d55d487fe67e5778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="55e0a-103">Montare una condivisione file di Azure con Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="55e0a-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="55e0a-104">Per impostazione predefinita, Istanze di contenitore di Azure è senza stato.</span><span class="sxs-lookup"><span data-stu-id="55e0a-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="55e0a-105">Se il contenitore si blocca o si arresta, lo stato viene perso.</span><span class="sxs-lookup"><span data-stu-id="55e0a-105">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="55e0a-106">Per rendere persistente lo stato oltre la durata del contenitore, è necessario montare un volume da un archivio esterno.</span><span class="sxs-lookup"><span data-stu-id="55e0a-106">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span> <span data-ttu-id="55e0a-107">Questo articolo illustra come montare una condivisione file di Azure per l'uso con Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="55e0a-107">This article shows how to mount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="55e0a-108">Creare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="55e0a-108">Create an Azure file share</span></span>

<span data-ttu-id="55e0a-109">Prima di usare una condivisione file di Azure con Istanze di contenitore di Azure è necessario creare la condivisione.</span><span class="sxs-lookup"><span data-stu-id="55e0a-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="55e0a-110">Eseguire questo script per creare un account di archiviazione per ospitare la condivisione file e la condivisione in sé.</span><span class="sxs-lookup"><span data-stu-id="55e0a-110">Run the following script to create a storage account to host the file share and the share itself.</span></span> <span data-ttu-id="55e0a-111">Si noti che il nome dell'account di archiviazione deve essere globalmente univoco, quindi lo script aggiunge un valore casuale alla stringa di base.</span><span class="sxs-lookup"><span data-stu-id="55e0a-111">Note that the storage account name must be globally unique, so the script adds a random value to the base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create the storage account with the parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="55e0a-112">Acquisire i dettagli di accesso dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="55e0a-112">Acquire storage account access details</span></span>

<span data-ttu-id="55e0a-113">Per montare una condivisione file di Azure come volume in Istanze di contenitore di Azure sono necessari tre valori: il nome dell'account di archiviazione, il nome della condivisione e la chiave di accesso alle risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="55e0a-113">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage access key.</span></span> 

<span data-ttu-id="55e0a-114">Se si usa lo script precedente, il nome dell'account di archiviazione viene creato con un valore casuale alla fine.</span><span class="sxs-lookup"><span data-stu-id="55e0a-114">If you used the script above, the storage account name was created with a random value at the end.</span></span> <span data-ttu-id="55e0a-115">Per eseguire una query sulla stringa finale (inclusa la parte casuale), usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="55e0a-115">To query the final string (including the random portion), use the following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="55e0a-116">Il nome della condivisione è già noto (*acishare* nello script precedente), quindi resta da trovare solo la chiave dell'account di archiviazione, che può essere recuperata tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="55e0a-116">The share name is already known (it is *acishare* in the script above), so all that remains is the storage account key, which can be found using the following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="55e0a-117">Archiviare i dettagli di accesso dell'account di archiviazione con Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="55e0a-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="55e0a-118">Le chiavi dell'account di archiviazione proteggono l'accesso ai dati, quindi è consigliabile archiviarle in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="55e0a-118">Storage account keys protect access to your data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="55e0a-119">Creare un insieme di credenziali delle chiavi con l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="55e0a-119">Create a key vault with the Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="55e0a-120">L'opzione `enabled-for-template-deployment` consente ad Azure Resource Manager di eseguire il pull dei segreti dall'insieme di credenziali delle chiavi al momento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="55e0a-120">The `enabled-for-template-deployment` switch allows Azure Resource Manager to pull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="55e0a-121">Archiviare la chiave dell'account di archiviazione come nuovo segreto nell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="55e0a-121">Store the storage account key as a new secret in the key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-the-volume"></a><span data-ttu-id="55e0a-122">Montare il volume</span><span class="sxs-lookup"><span data-stu-id="55e0a-122">Mount the volume</span></span>

<span data-ttu-id="55e0a-123">Il montaggio di una condivisione file di Azure come volume in un contenitore prevede due fasi.</span><span class="sxs-lookup"><span data-stu-id="55e0a-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="55e0a-124">Si forniscono prima i dettagli della condivisione nell'ambito della definizione del gruppo di contenitori, quindi si specifica come montare il volume in uno o più contenitori del gruppo.</span><span class="sxs-lookup"><span data-stu-id="55e0a-124">First, you provide the details of the share as part of defining the container group, then you specify how you want the volume mounted within one or more of the containers in the group.</span></span>

<span data-ttu-id="55e0a-125">Per definire i volumi da rendere disponibili per il montaggio, aggiungere una matrice `volumes` alla definizione del gruppo di contenitori nel modello di Azure Resource Manager, quindi farvi riferimento nella definizione dei singoli contenitori.</span><span class="sxs-lookup"><span data-stu-id="55e0a-125">To define the volumes you want to make available for mounting, add a `volumes` array to the container group definition in the Azure Resource Manager template, then reference them in the definition of the individual containers.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

<span data-ttu-id="55e0a-126">Il modello include il nome dell'account di archiviazione e la chiave come parametri che possono essere forniti in un file di parametri separati.</span><span class="sxs-lookup"><span data-stu-id="55e0a-126">The template includes the storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="55e0a-127">Per popolare il file dei parametri sono necessari tre valori: nome dell'account di archiviazione, ID risorsa di Azure Key Vault e nome del segreto dell'insieme di credenziali delle chiavi usato per archiviare la chiave di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="55e0a-127">To populate the parameters file, you will need three values: the storage account name, the resource ID of your Azure key vault, and the key vault secret name that you used to store the storage key.</span></span> <span data-ttu-id="55e0a-128">Se è stata seguita la procedura precedente, è possibile ottenere questi valori con questo script:</span><span class="sxs-lookup"><span data-stu-id="55e0a-128">If you have followed previous steps, you can get these values with the following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="55e0a-129">Inserire i valori nel file dei parametri:</span><span class="sxs-lookup"><span data-stu-id="55e0a-129">Insert the values into the parameters file:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-the-container-and-manage-files"></a><span data-ttu-id="55e0a-130">Distribuire il contenitore e gestire i file</span><span class="sxs-lookup"><span data-stu-id="55e0a-130">Deploy the container and manage files</span></span>

<span data-ttu-id="55e0a-131">Con il modello definito, è possibile creare il contenitore e montarne il volume usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="55e0a-131">With the template defined, you can create the container and mount its volume using the Azure CLI.</span></span> <span data-ttu-id="55e0a-132">Supponendo che il file del modello sia denominato *azuredeploy.json* e che il file dei parametri sia denominato *azuredeploy.parameters.json*, la riga di comando sarà:</span><span class="sxs-lookup"><span data-stu-id="55e0a-132">Assuming that the template file is named *azuredeploy.json* and that the parameters file is named *azuredeploy.parameters.json*, then the command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="55e0a-133">Dopo l'avvio del contenitore, è possibile usare la semplice app Web distribuita tramite l'immagine **seanmckenna/aci-hellofiles** per gestire i file nella condivisione file di Azure nel percorso di montaggio specificato.</span><span class="sxs-lookup"><span data-stu-id="55e0a-133">Once the container starts up, you can use the simple web app deployed via the **seanmckenna/aci-hellofiles** image, to the manage files in the Azure file share at the mount path that you specified.</span></span> <span data-ttu-id="55e0a-134">Ottenere l'indirizzo IP dell'app Web con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="55e0a-134">Obtain the ip address for the web app via the following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="55e0a-135">È possibile usare uno strumento come [Microsoft Azure Storage Explorer](http://storageexplorer.com) per recuperare e ispezionare il file scritto nella condivisione file.</span><span class="sxs-lookup"><span data-stu-id="55e0a-135">You can use a tool like the [Microsoft Azure Storage Explorer](http://storageexplorer.com) to retrieve and inspect the file writen to the file share.</span></span>

>[!NOTE]
> <span data-ttu-id="55e0a-136">Per altre informazioni sull'uso dei modelli di Azure Resource Manager e dei file dei parametri e sulla distribuzione con l'interfaccia della riga di comando di Azure, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="55e0a-136">To learn more about using Azure Resource Manager templates, parameter files, and deploying with the Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="55e0a-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55e0a-137">Next steps</span></span>

- <span data-ttu-id="55e0a-138">Distribuire il primo contenitore usando la [guida introduttiva](container-instances-quickstart.md) di Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="55e0a-138">Deploy for your first container using the Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="55e0a-139">Informazioni sulla [relazione tra Istanze di contenitore di Azure e gli agenti di orchestrazione di contenitori](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="55e0a-139">Learn about the [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
