---
title: aaaCreate registro contenitore privato Docker - CLI di Azure | Documenti Microsoft
description: Iniziare a creare e gestire i registri contenitore Docker privati con hello Azure CLI 2.0
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Creare un registro di sistema contenitore Docker privata mediante hello Azure CLI 2.0
Utilizzare i comandi in hello [CLI di Azure 2.0](https://github.com/Azure/azure-cli) toocreate del Registro di sistema un contenitore e gestire le impostazioni dal computer Linux, Mac e Windows. È anche possibile creare e gestire i registri di contenitore usando hello [portale di Azure](container-registry-get-started-portal.md) o a livello di codice con hello contenitore del Registro di sistema [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Per lo sfondo e i concetti, vedere [hello Panoramica](container-registry-intro.md)
* Per informazioni sui comandi CLI di contenitore del Registro di sistema (`az acr` comandi), passare hello `-h` comando tooany di parametro.


## <a name="prerequisites"></a>Prerequisiti
* **Azure CLI 2.0**: tooinstall e iniziare a utilizzare hello CLI 2.0, vedere hello [le istruzioni di installazione](/cli/azure/install-azure-cli). Accedi tooyour sottoscrizione di Azure eseguendo `az login`. Per ulteriori informazioni, vedere [introduzione hello CLI 2.0](/cli/azure/get-started-with-azure-cli).
* **Gruppo di risorse**: creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) prima di creare un registro di contenitori o usare un gruppo di risorse esistente. Verificare che il gruppo di risorse hello è in una posizione in cui è hello servizio Registro di sistema contenitore [disponibile](https://azure.microsoft.com/regions/services/). un gruppo di risorse utilizzando toocreate hello 2.0 CLI, vedere [hello riferimento CLI 2.0](/cli/azure/group).
* **Account di archiviazione** (facoltativo): creare un Azure standard [account di archiviazione](../storage/common/storage-introduction.md) tooback hello contenitore nel Registro di sistema hello nello stesso percorso. Se non si specifica un account di archiviazione durante la creazione di un registro di sistema `az acr create`, comando hello viene creata una automaticamente. un archivio account tramite toocreate hello CLI 2.0, vedere [hello riferimento CLI 2.0](/cli/azure/storage/account). Archiviazione Premium non è attualmente supportata.
* **Entità servizio** (facoltativo): quando si crea un registro di sistema con hello CLI, per impostazione predefinita non è configurato per l'accesso. A seconda delle esigenze, è possibile assegnare un registro tooa principale di servizio Azure Active Directory esistente o creare e assegnare uno nuovo, o abilitare l'account amministratore del Registro di sistema di hello. Vedere hello sezioni più avanti in questo articolo. Per ulteriori informazioni sull'accesso del Registro di sistema, vedere [autentica con del Registro di sistema di hello contenitore](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Creare un registro di contenitori
Eseguire hello `az acr create` toocreate comando del Registro di sistema un contenitore.

> [!TIP]
> Quando si crea un registro, specificare un nome di dominio univoco globale di primo livello, contenente solo lettere e numeri. nome del Registro di sistema Hello negli esempi di hello è `myRegistry1`, ma sostituire un nome univoco del proprio.
>
>

Hello comando utilizza hello del Registro di sistema di numero minimo di parametri toocreate contenitore seguente `myRegistry1` nel gruppo di risorse hello `myResourceGroup`e l'utilizzo di hello *base* sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` è facoltativo. Se non viene specificato, viene creato un account di archiviazione con un nome composto dal nome del Registro di sistema hello e un timestamp in hello specificato gruppo di risorse.

Quando viene creato il registro hello, l'output di hello è simile toohello seguenti:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Considerare con attenzione le seguenti voci:

* `id`-Identificatore del Registro di sistema hello nella sottoscrizione, è necessario se si desidera tooassign un'entità servizio.
* `loginServer`-nome completo di hello specificato troppo[log nel Registro di sistema toohello](container-registry-authentication.md). In questo esempio, è il nome di hello `myregistry1.exp.azurecr.io` (tutti in lettere minuscole).

## <a name="assign-a-service-principal"></a>Assegnare un'entità servizio
Utilizzare i comandi di CLI 2.0 tooassign un registro tooa dell'entità servizio di Azure Active Directory. Hello dell'entità servizio in questi esempi viene assegnato il ruolo di proprietario hello, ma è possibile assegnare [altri ruoli](../active-directory/role-based-access-control-configure.md) se si desidera.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>Creare un'entità servizio e assegnare del Registro di sistema di accesso toohello
In hello comando seguente, una nuova entità servizio viene assegnata l'ID proprietario ruolo accesso toohello del Registro di sistema superato con hello `--scopes` parametro. Specificare una password complessa con hello `--password` parametro.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Assegnare un'entità servizio esistente
Se si dispone di un'entità servizio già e desidera tooassign è proprietario ruolo accesso toohello Registro di sistema, eseguire una toohello simile comando riportato di seguito. Si passa hello ID app dell'entità del servizio utilizzando hello `--assignee` parametro:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Gestire le credenziali di amministratore
Per ogni registro di contenitori viene creato automaticamente un account amministratore che è disabilitato per impostazione predefinita. Hello seguente mostra esempi `az acr` CLI comandi credenziali di amministratore hello toomanage per il Registro di sistema del contenitore.

### <a name="obtain-admin-user-credentials"></a>Ottenere le credenziali di utente amministratore
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Abilitare l'utente amministratore per un registro esistente
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Disabilitare l'utente amministratore per un registro esistente
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Elencare immagini e tag
Hello utilizzare `az acr` contiene i comandi CLI immagini hello tooquery e tag in un repository.

> [!NOTE]
> Registro di sistema di contenitore non supporta attualmente hello `docker search` comando tooquery per immagini e i tag.


### <a name="list-repositories"></a>Elencare repository
Hello esempio seguente vengono elencati i repository hello nel Registro di sistema, in formato JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Elencare tag
Hello esempio seguente vengono elencati i tag hello in hello **esempi/nginx** repository, in formato JSON:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Passaggi successivi
* [La prima immagine usando Docker CLI hello push](container-registry-get-started-docker-cli.md)
