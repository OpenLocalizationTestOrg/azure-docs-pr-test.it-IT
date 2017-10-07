---
title: aaaCreate Docker ospitata in Azure con Docker macchina | Documenti Microsoft
description: Viene descritto l'utilizzo di host di macchina Docker toocreate docker in Azure.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Creare host Docker in Azure con Docker Machine
Esecuzione [Docker](https://www.docker.com/) contenitori richiede un host macchina virtuale in esecuzione hello daemondocker.
Questo argomento viene descritto come hello toouse [macchina docker](https://docs.docker.com/machine/) comando toocreate nuove macchine virtuali Linux, configurato con hello daemon Docker, in esecuzione in Azure. 

**Nota:** 

* *Questo articolo si basa sulla versione di Docker Machine 0.9.0-rc2 o versione successiva*
* *Contenitori di Windows saranno supportati tramite docker-macchina in hello prossimo futuro*

## <a name="create-vms-with-docker-machine"></a>Creare VM con Docker Machine
Creare le macchine virtuali host docker in Azure con hello `docker-machine create` comando utilizzando hello `azure` driver. 

Hello driver Azure richiede l'ID sottoscrizione. È possibile utilizzare hello [CLI di Azure](cli-install-nodejs.md) o hello [portale Azure](https://portal.azure.com) tooretrieve la sottoscrizione di Azure. 

**Utilizzo di hello portale di Azure**

* Selezionare **sottoscrizioni** da hello spostamento a sinistra pagina e copia hello id sottoscrizione.

**Utilizzo di hello CLI di Azure**

* Tipo ```azure account list``` e l'id sottoscrizione hello di copia.

Tipo `docker-machine create --driver azure` toosee hello opzioni e i relativi valori predefiniti.
È inoltre possibile visualizzare hello [documentazione del Driver Azure Docker](https://docs.docker.com/machine/drivers/azure/) per altre informazioni. 

Hello esempio seguente si basa su hello [i valori predefiniti](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ma se lo si desidera impostare questi valori: 

* dns di Azure per il nome di hello associato a indirizzo IP pubblico hello e i certificati generati. Questo è il nome DNS hello della macchina virtuale. Hello VM può quindi in modo sicuro arrestare, rilasciare l'indirizzo IP dinamico hello e fornire hello possibilità tooreconnect dopo hello vm inizia nuovamente con un nuovo indirizzo IP. prefisso del nome Hello deve essere univoco per tale area UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* Aprire la porta 80 in hello macchina virtuale per l'accesso a internet in uscita
* dimensioni di archiviazione premium più veloce di VM tooutilize hello
* archiviazione Premium utilizzato per il disco di macchina virtuale hello

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Scegliere un host di Docker con Docker Machine
Dopo aver creato una voce nella macchina di docker per l'host, è possibile impostare l'host predefinito hello durante l'esecuzione di comandi di docker.

## <a name="using-powershell"></a>Tramite PowerShell
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Tramite Bash
```bash
eval $(docker-machine env MyDockerHost)
```

È ora possibile eseguire i comandi di docker per gli host specificati hello

```
docker ps
docker info
```

## <a name="run-a-container"></a>Eseguire un contenitore
Con un host è configurato, è ora possibile eseguire un tootest di server web semplice se l'host è stato configurato correttamente.
Qui è usare un'immagine standard nginx, specificare che deve restare in attesa sulla porta 80 e se si riavvia, macchina virtuale host hello contenitore hello verrà riavviato anche (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

output di Hello dovrebbe essere simile alla seguente hello:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Contenitore di test hello
Esaminare i contenitori in esecuzione usando `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

E, hello toosee contenitore, tipo di esecuzione `docker-machine ip <VM name>` toofind tooenter indirizzo IP di hello nel browser hello:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Esecuzione di un contenitore ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Riepilogo
Docker Machine consente di eseguire facilmente il provisioning di host Docker in Azure per le convalide di host Docker singoli.
Per la produzione di hosting di contenitori, vedere hello [servizio contenitore di Azure](http://aka.ms/AzureContainerService)

toodevelop .NET Core applicazioni con Visual Studio, vedere [Docker Tools per Visual Studio](http://aka.ms/DockerToolsForVS)

