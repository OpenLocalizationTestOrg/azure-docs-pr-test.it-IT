---
title: aaaCreate privata Docker Registro di sistema - portale di Azure | Documenti Microsoft
description: Iniziare a creare e gestire i registri contenitore Docker privati con hello portale di Azure
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Creare un registro di sistema di contenitore gestito mediante hello portale di Azure

Registro contenitori di Azure è un servizio gestito di registri contenitori Docker usato per l'archiviazione di immagini di un contenitore Docker privato. Questa guida descrive la creazione di un'istanza gestita di Azure del Registro di sistema contenitore utilizzando hello portale di Azure.

I registri contenitori di Azure gestiti sono in anteprima e non disponibili in tutte le aree di Azure.

## <a name="log-in-tooazure"></a>Accedi tooAzure

Accedi toohello portale di Azure all'indirizzo http://portal.azure.com.

## <a name="create-a-container-registry"></a>Creare un registro di contenitori

1. Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.

2. Marketplace hello ricerca per **Registro di sistema di contenitore di Azure** e selezionarlo.

3. Fare clic su **crea** aprire Pannello di creazione ACR hello.

    ![Impostazioni di Registro contenitori](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. In hello **Registro di sistema di Azure contenitore** pannello, immettere le seguenti informazioni hello. Al termine dell'operazione fare clic su **Crea**.

    a. **Registry name** (Nome registro): nome di dominio di primo livello univoco globale per il registro. In questo esempio, nome del Registro di sistema hello è *myAzureContainerRegistry1*, ma sostituire un nome univoco del proprio. Hello nome può contenere solo lettere e numeri.

    b. **Gruppo di risorse**: selezionare un oggetto esistente [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) o nome di tipo hello uno nuovo.

    c. **Percorso**: selezionare un Data Center di Azure posizione servizio hello [disponibile](https://azure.microsoft.com/regions/services/), ad esempio **centro-meridionali**.

    d. **L'utente amministratore**: se si desidera, attivare del Registro di sistema hello tooaccess utente amministratore. È possibile modificare questa impostazione dopo la creazione del Registro di sistema di hello.

    e. **Registro di sistema gestito utilizzare**: selezionare Sì toohave ACR automaticamente gestire l'archiviazione del Registro di sistema hello, utilizzare webhook e utilizzare l'autenticazione AAD.

    f. **Piano tariffario**: selezionare un piano tariffario. Vedere le informazioni sui prezzi di Registro contenitori di Azure per altre informazioni.

## <a name="log-in-tooacr-instance"></a>Accedi tooACR istanza

Prima di push e pull immagini contenitore, è necessario accedere nell'istanza di record toohello. 

toodo, utilizzare hello CLI di Azure 2.0. Innanzitutto, se necessario, accedere utilizzando hello Azure [accesso az](/cli/azure/#login) comando. 

```azurecli
az login
```

Successivamente, utilizzare hello [accesso acr az](/cli/azure/acr#login) comando toolog in toohello del Registro di sistema contenitore di Azure.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a>Usare Registro contenitori di Azure

### <a name="list-container-images"></a>Elencare le immagini del contenitore

Hello utilizzare `az acr` contiene i comandi CLI immagini hello tooquery e tag in un repository.

> [!NOTE]
> Registro di sistema di contenitore non supporta attualmente hello `docker search` comando tooquery per immagini e i tag.

### <a name="list-repositories"></a>Elencare repository

Hello esempio seguente vengono elencati i repository hello nel Registro di sistema, in formato JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Elencare tag

Hello esempio seguente vengono elencati i tag hello in hello **esempi/nginx** repository, in formato JSON:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Passaggi successivi

In questa Guida introduttiva è stata creata un'istanza gestita di Azure del Registro di sistema contenitore utilizzando hello portale di Azure.

> [!div class="nextstepaction"]
> [La prima immagine usando Docker CLI hello push](container-registry-get-started-docker-cli.md)
