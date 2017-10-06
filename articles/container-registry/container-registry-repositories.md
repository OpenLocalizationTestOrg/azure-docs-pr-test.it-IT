---
title: repository del Registro di sistema di contenitore aaaAzure | Documenti Microsoft
description: Il repository del Registro di sistema di Azure contenitore toouse per le immagini Docker
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Archivi di registri contenitori di Azure

Registro di sistema di contenitore di Azure consente di immagini contenitore toostore nel repository. Archiviando le immagini nei repository, è possibile avere gruppi di immagini (o versioni delle immagini) in ambienti isolati. Quando si esegue il push del Registro di sistema tooyour immagini, è possibile specificare questi archivi.


## <a name="prerequisites"></a>Prerequisiti
* **Registro di contenitori di Azure**: creare un registro di contenitori nella sottoscrizione di Azure. Ad esempio, utilizzare hello [portale di Azure](container-registry-get-started-portal.md) o hello [CLI di Azure 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset del computer locale come un host e accesso hello Docker CLI i comandi di Docker, installare [motore Docker](https://docs.docker.com/engine/installation/).
* **Estrarre un'immagine** - Pull un'immagine dal Registro di sistema di hello pubblico Hub Docker, tag e spingerla tooyour del Registro di sistema. Per indicazioni su come eseguire il push e pull immagini, vedere [Registro di sistema privata Push Docker immagine tooAzure](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-hello-portal"></a>Visualizzazione di repository in hello portale

Dopo avere eseguito il push del Registro di sistema di immagini tooyour contenitore, è possibile visualizzare un elenco dei repository hello hosting immagini hello in hello portale di Azure.

Se è stata seguita la procedura hello in hello [registro privata di Push di Docker immagini tooAzure](container-registry-get-started-docker-cli.md) articolo, è stata acquisita un'immagine di Nginx nel Registro di sistema contenitore. Come parte delle istruzioni di hello, si deve specificare uno spazio dei nomi per l'immagine di hello. Nell'esempio hello seguente comando hello inserisce i repository di hello NGinx immagini toohello "esempi":

```
docker push myregistry.azurecr.io/samples/nginx
```
 Registro contenitori di Azure supporta spazi dei nomi dei repository multilivello. Questa funzionalità consente di toogroup raccolte di app specifica tooa correlati di immagini, o una raccolta di sviluppo di App toospecific o i team operativi. tooread ulteriori informazioni su repository nei registri di sistema di contenitore, vedere [registri contenitore privato Docker in Azure](container-registry-intro.md).

repository del Registro di sistema di tooview hello contenitore:

1. Accedi toohello portale di Azure
2. In hello **Registro di sistema di Azure contenitore** blade, Registro di sistema selezionare hello desiderato tooinspect
3. Nel Pannello di hello del Registro di sistema, fare clic su **repository** toosee un elenco di tutti i repository hello e proprie immagini
4. (Facoltativo) Selezionare un tag di immagine specifico toosee

![Repository nel portale di hello](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Passaggi successivi
Ora che si conoscono i concetti di base hello, si è pronti toostart mediante il Registro di sistema. Ad esempio, iniziare la distribuzione di contenitore immagini tooan [servizio contenitore di Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.
