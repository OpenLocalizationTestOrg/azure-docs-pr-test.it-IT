---
title: aaaPush Docker immagine tooprivate del Registro di sistema Azure | Documenti Microsoft
description: Push e pull immagini tooa contenitore privato del Registro di sistema in Azure utilizzando hello Docker CLI di Docker
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>La prima immagine tooa privata Docker contenitore del Registro di sistema utilizzando hello Docker CLI push
Un registro di sistema di contenitore di Azure archivia e gestisce privata [Docker](http://hub.docker.com) immagini contenitore, simile toohello modo [Hub Docker](https://hub.docker.com/) archivia le immagini Docker pubbliche. Utilizzare hello [interfaccia della riga di comando di Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) per [accesso](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/)e altre operazioni sul contenitore Registro di sistema.

Per altre sfondo e i concetti, vedere [hello Panoramica](container-registry-intro.md)



## <a name="prerequisites"></a>Prerequisiti
* **Registro di contenitori di Azure**: creare un registro di contenitori nella sottoscrizione di Azure. Ad esempio, utilizzare hello [portale di Azure](container-registry-get-started-portal.md) o hello [CLI di Azure 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset del computer locale come un host e accesso hello Docker CLI i comandi di Docker, installare [motore Docker](https://docs.docker.com/engine/installation/).

## <a name="log-in-tooa-registry"></a>Accedi al Registro di sistema tooa
Eseguire `docker login` toolog nel Registro di sistema tooyour contenitore con il [le credenziali del Registro di sistema](container-registry-authentication.md).

Hello seguente esempio passa hello ID e la password di Azure Active Directory [dell'entità servizio](../active-directory/active-directory-application-objects.md). Ad esempio, è stato assegnato un registro di sistema tooyour dell'entità servizio per uno scenario di automazione.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> Verificare nome completo del Registro di sistema di hello che toospecify (tutti in lettere minuscole). In questo esempio si tratta di `myregistry.azurecr.io`.

## <a name="steps-toopull-and-push-an-image"></a>Passaggi toopull e inserire un'immagine
Hello seguire l'esempio download hello immagine Nginx da hello pubblica Hub Docker del Registro di sistema, i tag per il Registro di sistema contenitore privato di Azure, inserisce tooyour del Registro di sistema, quindi grado di estrarre nuovamente.

**1. Pull immagine ufficiale di hello Docker per Nginx**

Primo pull hello pubblica Nginx immagine tooyour computer locale.

```
docker pull nginx
```
**2. Avviare il contenitore Nginx hello**

Hello comando seguente avvia hello locale Nginx contenitore in modo interattivo sulla porta 8080, consentendo di output toosee Nginx. Rimuove hello in esecuzione una volta arrestato contenitore.

```
docker run -it --rm -p 8080:80 nginx
```

Sfoglia troppo[http://localhost:8080](http://localhost:8080) tooview hello in esecuzione contenitore. Viene visualizzato un toohello simile schermata segue quello.

![Nginx sul computer locale](./media/container-registry-get-started-docker-cli/nginx.png)

toostop hello contenitore in esecuzione, premere [CTRL] + [C].

**3. Creare un alias dell'immagine di hello nel Registro di sistema**

Hello seguente comando crea un alias dell'immagine di hello, con un registro di sistema tooyour il percorso completo. In questo esempio specifica hello `samples` disordine tooavoid dello spazio dei nomi nella directory radice del Registro di sistema hello hello.

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4. Eseguire il push del Registro di sistema di hello immagine tooyour**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5. Immagine di hello pull dal Registro di sistema**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6. Avviare il contenitore di Nginx hello dal Registro di sistema**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

Sfoglia troppo[http://localhost:8080](http://localhost:8080) tooview hello in esecuzione contenitore.

toostop hello contenitore in esecuzione, premere [CTRL] + [C].

**7. (Facoltativo) Rimuovere un'immagine di hello**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>Limiti delle chiamate simultanee
In alcuni scenari, l'esecuzione di chiamate simultanee può provocare errori. Hello nella tabella seguente contiene i limiti di hello di chiamate simultanee con operazioni "Push" e "Pull" del Registro di sistema di contenitore di Azure:

| Operazione  | Limite                                  |
| ---------- | -------------------------------------- |
| PULL       | Backup too10 simultanee estrae al Registro di sistema |
| PUSH       | Backup too5 simultanee inserisce al Registro di sistema |

## <a name="next-steps"></a>Passaggi successivi
Ora che si conoscono i concetti di base hello, si è pronti toostart mediante il Registro di sistema. Ad esempio, iniziare la distribuzione di contenitore immagini tooan [servizio contenitore di Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.
