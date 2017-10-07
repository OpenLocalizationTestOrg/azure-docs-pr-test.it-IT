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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Montare una condivisione file di Azure con Istanze di contenitore di Azure

Per impostazione predefinita, Istanze di contenitore di Azure è senza stato. Se il contenitore di hello si blocca o si arresta, il relativo stato viene perso. toopersist stato oltre la durata hello del contenitore di hello, è necessario montare un volume da un archivio esterno. Questo articolo illustra come toomount condividere un file di Azure per l'uso con istanze di contenitori di Azure.

## <a name="create-an-azure-file-share"></a>Creare una condivisione file di Azure

Prima di usare una condivisione file di Azure con Istanze di contenitore di Azure è necessario creare la condivisione. Eseguire i seguenti script toocreate hello una condivisione di file di archiviazione account toohost hello e hello condividono stesso. Si noti che il nome di account di archiviazione hello deve essere globalmente univoco, in modo script hello aggiunge una stringa in base toohello valore casuale.

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

## <a name="acquire-storage-account-access-details"></a>Acquisire i dettagli di accesso dell'account di archiviazione

toomount condivisione di un file di Azure come un volume in istanze di contenitori di Azure, sono necessari tre valori: hello Nome account di archiviazione, il nome di condivisione hello e chiave di accesso di archiviazione hello. 

Se è stato utilizzato lo script hello precedente, nome account di archiviazione hello è stato creato con un valore casuale alla fine di hello. stringa finale tooquery hello (tra cui hello casuale parte), utilizzare hello seguenti comandi:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Hello nome di condivisione è già nota (è *acishare* nello script hello precedente), pertanto tutto ciò che resta da una chiave account archiviazione hello, che può essere recuperata tramite hello comando seguente:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Archiviare i dettagli di accesso dell'account di archiviazione con Azure Key Vault

Chiavi dell'account di archiviazione proteggere tooyour di accedere ai dati, pertanto è consigliabile archiviarli in un insieme di credenziali chiave di Azure. 

Creare un insieme di credenziali chiave con hello CLI di Azure:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Hello `enabled-for-template-deployment` switch consente Azure Resource Manager toopull segreti dall'insieme di credenziali delle chiavi in fase di distribuzione.

Archivio hello chiave account di archiviazione come un nuovo segreto nell'insieme di credenziali chiave hello:

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Montare il volume di hello

Il montaggio di una condivisione file di Azure come volume in un contenitore prevede due fasi. Prima di tutto, fornire i dettagli di hello della condivisione hello come parte della definizione di gruppo di contenitori di hello, è necessario specificare la modalità di volume hello montato all'interno di uno o più contenitori di hello nel gruppo di hello.

volumi di hello toodefine desiderato toomake disponibili per l'installazione, aggiungere un `volumes` toohello definizione del gruppo contenitore nel modello di gestione risorse di Azure hello della matrice, quindi farvi riferimento nella definizione di hello di singoli contenitori hello.

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

modello di Hello include nome account di archiviazione hello e la chiave come parametri, che possono essere forniti in un file di parametri separati. file dei parametri hello toopopulate, sono necessari tre valori: hello Nome account di archiviazione, hello ID risorsa di credenziali delle chiavi di Azure e nome del segreto dell'insieme di credenziali chiave di avere utilizzato la chiave di archiviazione hello toostore hello. Se è stata seguita la procedura precedente, è possibile ottenere questi valori con hello lo script seguente:

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Inserire i valori hello nel file dei parametri hello:

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

## <a name="deploy-hello-container-and-manage-files"></a>Distribuire il contenitore di hello e gestire i file

Con il modello di hello definito, è possibile creare il contenitore di hello e montare il volume utilizzando hello CLI di Azure. Supponendo che hello file modello è denominato *azuredeploy.json* e il file di parametri hello è denominato *azuredeploy.parameters.json*, quindi la riga di comando hello è:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Una volta contenitore hello viene avviata, è possibile utilizzare app web semplici hello distribuite tramite hello **aci/seanmckenna-hellofiles** immagine toohello gestire i file nella condivisione di file di Azure hello nel percorso di montaggio hello specificato. Ottenere l'indirizzo ip hello hello di applicazione web tramite il seguente hello:

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

È possibile utilizzare uno strumento quale hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve e controllare la condivisione file hello file scritti toohello.

>[!NOTE]
> toolearn ulteriori informazioni su utilizzo di modelli di gestione risorse di Azure, i file dei parametri e la distribuzione con hello CLI di Azure, vedere [distribuire le risorse con i modelli di gestione risorse e CLI di Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Passaggi successivi

- La distribuzione per il primo contenitore utilizzando istanze di contenitori di hello Azure [avvio rapido](container-instances-quickstart.md)
- Informazioni su hello [relazione tra le istanze di contenitore di Azure e orchestrators contenitore](container-instances-orchestrator-relationship.md)
