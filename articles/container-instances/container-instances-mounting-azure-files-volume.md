---
title: aaaMounting un volume di file di Azure in istanze di contenitori di Azure
description: Informazioni su come toomount un Azure file stato toopersist del volume con istanze di contenitori di Azure
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
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="2aff7-103">Montare una condivisione file di Azure con Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="2aff7-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="2aff7-104">Per impostazione predefinita, Istanze di contenitore di Azure è senza stato.</span><span class="sxs-lookup"><span data-stu-id="2aff7-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="2aff7-105">Se il contenitore di hello si blocca o si arresta, il relativo stato viene perso.</span><span class="sxs-lookup"><span data-stu-id="2aff7-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="2aff7-106">toopersist stato oltre la durata hello del contenitore di hello, è necessario montare un volume da un archivio esterno.</span><span class="sxs-lookup"><span data-stu-id="2aff7-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="2aff7-107">Questo articolo illustra come toomount condividere un file di Azure per l'uso con istanze di contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aff7-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="2aff7-108">Creare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="2aff7-108">Create an Azure file share</span></span>

<span data-ttu-id="2aff7-109">Prima di usare una condivisione file di Azure con Istanze di contenitore di Azure è necessario creare la condivisione.</span><span class="sxs-lookup"><span data-stu-id="2aff7-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="2aff7-110">Eseguire i seguenti script toocreate hello una condivisione di file di archiviazione account toohost hello e hello condividono stesso.</span><span class="sxs-lookup"><span data-stu-id="2aff7-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="2aff7-111">Si noti che il nome di account di archiviazione hello deve essere globalmente univoco, in modo script hello aggiunge una stringa in base toohello valore casuale.</span><span class="sxs-lookup"><span data-stu-id="2aff7-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="2aff7-112">Acquisire i dettagli di accesso dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2aff7-112">Acquire storage account access details</span></span>

<span data-ttu-id="2aff7-113">toomount condivisione di un file di Azure come un volume in istanze di contenitori di Azure, sono necessari tre valori: hello Nome account di archiviazione, il nome di condivisione hello e chiave di accesso di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="2aff7-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="2aff7-114">Se è stato utilizzato lo script hello precedente, nome account di archiviazione hello è stato creato con un valore casuale alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="2aff7-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="2aff7-115">stringa finale tooquery hello (tra cui hello casuale parte), utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2aff7-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="2aff7-116">Hello nome di condivisione è già nota (è *acishare* nello script hello precedente), pertanto tutto ciò che resta da una chiave account archiviazione hello, che può essere recuperata tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2aff7-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="2aff7-117">Archiviare i dettagli di accesso dell'account di archiviazione con Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="2aff7-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="2aff7-118">Chiavi dell'account di archiviazione proteggere tooyour di accedere ai dati, pertanto è consigliabile archiviarli in un insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aff7-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="2aff7-119">Creare un insieme di credenziali chiave con hello CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="2aff7-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="2aff7-120">Hello `enabled-for-template-deployment` switch consente Azure Resource Manager toopull segreti dall'insieme di credenziali delle chiavi in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2aff7-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="2aff7-121">Archivio hello chiave account di archiviazione come un nuovo segreto nell'insieme di credenziali chiave hello:</span><span class="sxs-lookup"><span data-stu-id="2aff7-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="2aff7-122">Montare il volume di hello</span><span class="sxs-lookup"><span data-stu-id="2aff7-122">Mount hello volume</span></span>

<span data-ttu-id="2aff7-123">Il montaggio di una condivisione file di Azure come volume in un contenitore prevede due fasi.</span><span class="sxs-lookup"><span data-stu-id="2aff7-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="2aff7-124">Prima di tutto, fornire i dettagli di hello della condivisione hello come parte della definizione di gruppo di contenitori di hello, è necessario specificare la modalità di volume hello montato all'interno di uno o più contenitori di hello nel gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="2aff7-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="2aff7-125">volumi di hello toodefine desiderato toomake disponibili per l'installazione, aggiungere un `volumes` toohello definizione del gruppo contenitore nel modello di gestione risorse di Azure hello della matrice, quindi farvi riferimento nella definizione di hello di singoli contenitori hello.</span><span class="sxs-lookup"><span data-stu-id="2aff7-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

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

<span data-ttu-id="2aff7-126">modello di Hello include nome account di archiviazione hello e la chiave come parametri, che possono essere forniti in un file di parametri separati.</span><span class="sxs-lookup"><span data-stu-id="2aff7-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="2aff7-127">file dei parametri hello toopopulate, sono necessari tre valori: hello Nome account di archiviazione, hello ID risorsa di credenziali delle chiavi di Azure e nome del segreto dell'insieme di credenziali chiave di avere utilizzato la chiave di archiviazione hello toostore hello.</span><span class="sxs-lookup"><span data-stu-id="2aff7-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="2aff7-128">Se è stata seguita la procedura precedente, è possibile ottenere questi valori con hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="2aff7-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="2aff7-129">Inserire i valori hello nel file dei parametri hello:</span><span class="sxs-lookup"><span data-stu-id="2aff7-129">Insert hello values into hello parameters file:</span></span>

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

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="2aff7-130">Distribuire il contenitore di hello e gestire i file</span><span class="sxs-lookup"><span data-stu-id="2aff7-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="2aff7-131">Con il modello di hello definito, è possibile creare il contenitore di hello e montare il volume utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aff7-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="2aff7-132">Supponendo che hello file modello è denominato *azuredeploy.json* e il file di parametri hello è denominato *azuredeploy.parameters.json*, quindi la riga di comando hello è:</span><span class="sxs-lookup"><span data-stu-id="2aff7-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="2aff7-133">Una volta contenitore hello viene avviata, è possibile utilizzare app web semplici hello distribuite tramite hello **aci/seanmckenna-hellofiles** immagine toohello gestire i file nella condivisione di file di Azure hello nel percorso di montaggio hello specificato.</span><span class="sxs-lookup"><span data-stu-id="2aff7-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="2aff7-134">Ottenere l'indirizzo ip hello hello di applicazione web tramite il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="2aff7-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="2aff7-135">È possibile utilizzare uno strumento quale hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve e controllare la condivisione file hello file scritti toohello.</span><span class="sxs-lookup"><span data-stu-id="2aff7-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="2aff7-136">toolearn ulteriori informazioni su utilizzo di modelli di gestione risorse di Azure, i file dei parametri e la distribuzione con hello CLI di Azure, vedere [distribuire le risorse con i modelli di gestione risorse e CLI di Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2aff7-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aff7-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2aff7-137">Next steps</span></span>

- <span data-ttu-id="2aff7-138">La distribuzione per il primo contenitore utilizzando istanze di contenitori di hello Azure [avvio rapido](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="2aff7-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="2aff7-139">Informazioni su hello [relazione tra le istanze di contenitore di Azure e orchestrators contenitore](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="2aff7-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
