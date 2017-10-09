---
title: aaaDeploy tooAzure istanze di contenitori da hello del Registro di sistema di Azure contenitore | Documenti di Azure
description: Distribuire istanze di contenitori tooAzure da hello del Registro di sistema contenitore di Azure
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>Distribuire istanze di contenitori tooAzure da hello del Registro di sistema contenitore di Azure

Hello del Registro di sistema di Azure contenitore è un registro basato su Azure e privato, per le immagini contenitore Docker. Questo articolo descrive come le immagini contenitore toodeploy archiviati in hello del Registro di sistema di Azure contenitore tooAzure istanze di contenitori.

## <a name="using-hello-azure-cli"></a>Utilizzo di hello CLI di Azure

Hello CLI di Azure include i comandi per la creazione e gestione dei contenitori di istanze di contenitori di Azure. Se si specifica un'immagine privata in hello `create` comando, è inoltre possibile specificare hello immagine del Registro di sistema di password tooauthenticate con del Registro di sistema di hello contenitore.

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

Hello `create` comando inoltre supporta la definizione di hello `registry-login-server` e `registry-username`. Tuttavia, il server di accesso hello per hello del Registro di sistema di Azure contenitore è sempre *registryname*. nome utente predefinito azurecr.io e hello *registryname*, pertanto questi valori vengono dedotti dal nome dell'immagine hello se non specificato in modo esplicito.

## <a name="using-an-azure-resource-manager-template"></a>Uso di un modello di Azure Resource Manager

È possibile specificare proprietà hello Azure contenitore del Registro di sistema in un modello di gestione risorse di Azure includendo hello `imageRegistryCredentials` proprietà nella definizione del gruppo contenitore hello:

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

tooavoid archiviare la password del Registro di sistema contenitore direttamente nel modello di hello, è consigliabile memorizzarlo come segreto in [insieme credenziali chiavi Azure](../key-vault/key-vault-manage-with-cli2.md) e farvi riferimento nel modello di hello utilizzando hello [integrazione nativa tra Hello Azure Resource Manager e l'insieme di credenziali chiave](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="using-hello-azure-portal"></a>Utilizzo di hello portale di Azure

Se si mantengono le immagini contenitore in hello del Registro di sistema contenitore di Azure, è possibile creare facilmente un contenitore in istanze di contenitori di Azure utilizzando hello portale di Azure.

1. Nel portale di Azure hello, passare tooyour del Registro di sistema contenitore.

2. Scegliere Repository.

    ![dal menu del Registro di sistema di Azure contenitore Hello hello portale di Azure][acr-menu]

3. Scegliere il repository hello che si desidera toodeploy da.

4. Fare doppio clic su tag hello per immagine contenitore hello desiderato toodeploy.

    ![Menu di scelta rapida per avviare il contenitore con Istanze di contenitore di Azure][acr-runinstance-contextmenu]

5. Immettere un nome per il contenitore di hello e un nome per il gruppo di risorse hello. Se si desidera, è possibile modificare anche i valori predefiniti di hello.

    ![Menu di creazione per Istanze di contenitore di Azure][acr-create-deeplink]

6. Una volta completata la distribuzione di hello, è possibile passare il gruppo di contenitori toohello da hello notifiche riquadro toofind l'indirizzo IP e altre proprietà.

    ![Visualizzazione dei dettagli del gruppo di contenitori in Istanze di contenitore di Azure][aci-detailsview]

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come effettuare il push del Registro di sistema di tooa contenitore privato, contenitori toobuild e distribuirli istanze di contenitori tooAzure da [completato hello esercitazione](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
