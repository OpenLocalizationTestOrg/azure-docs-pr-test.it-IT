---
title: aaaManage Azure controller di dominio o sistema operativo del cluster con l'API REST maratona | Documenti Microsoft
description: Distribuire i cluster di Azure contenitore del servizio controller di dominio o del sistema operativo di contenitori tooan tramite l'API REST maratona hello.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>Gestione dei contenitori di controller di dominio o del sistema operativo tramite l'API REST maratona hello
Controller di dominio/OS offre un ambiente per la distribuzione e scalabilità i carichi di lavoro cluster eliminando l'hardware sottostante hello. In DC/OS è disponibile anche un framework che gestisce la pianificazione e l'esecuzione dei carichi di lavoro di calcolo. Sebbene i Framework sono disponibili per molti carichi di lavoro comune, in questo documento consente di iniziare la creazione e scalabilità le distribuzioni di contenitori tramite l'API REST maratona hello. 

## <a name="prerequisites"></a>Prerequisiti

Prima di eseguire questi esempi, è necessario avere un cluster DC/OS configurato nel servizio contenitore di Azure. È inoltre necessario cluster toothis di toohave connettività remota. Per ulteriori informazioni su questi elementi, vedere hello seguenti articoli:

* [Distribuire un cluster del servizio contenitore di Azure](container-service-deployment.md)
* [Connessione tooan cluster del servizio di contenitore di Azure](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>Hello accesso API di controller di dominio o del sistema operativo
Dopo avere toohello connesso cluster del servizio di contenitore di Azure, è possibile accedere hello controller di dominio o del sistema operativo e le API REST correlate tramite http://localhost:local porta. Negli esempi di Hello in questo documento si presuppone che sono tunneling sulla porta 80. Ad esempio, gli endpoint maratona hello possono essere raggiunto all'URI a partire da `http://localhost/marathon/v2/`. 

Per ulteriori informazioni su hello diverse API, vedere documentazione Mesosphere hello hello [API maratona](https://mesosphere.github.io/marathon/docs/rest-api.html) e [Chronos API](https://mesos.github.io/chronos/docs/api.html)e la documentazione di Apache per hello [API dell'utilità di pianificazione Mesos ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Raccogliere informazioni da DC/OS e Marathon
Prima di distribuire cluster di controller di dominio/OS toohello contenitori, raccogliere informazioni sui cluster di controller di dominio/OS hello, ad esempio nomi di hello e lo stato degli agenti di controller di dominio/OS hello. toodo in tal caso, eseguire una query hello `master/slaves` endpoint dell'API REST di controller di dominio/OS hello. Se tutto va bene, query hello restituisce un elenco di agenti di controller di dominio/OS e diverse proprietà per ogni.

```bash
curl http://localhost/mesos/master/slaves
```

A questo punto, usare hello maratona `/apps` toocheck endpoint per cluster di toohello controller di dominio o del sistema operativo per le distribuzioni dell'applicazione corrente. Se si tratta di un nuovo cluster, viene visualizzata una matrice vuota di app.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Distribuire un contenitore Docker formattato
Distribuire contenitori Docker formattati tramite l'API REST maratona hello utilizzando un file JSON che descrive la distribuzione di hello previsto. Hello esempio seguente consente di distribuire un Nginx contenitore tooa privata dell'agente nel cluster hello. 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy un contenitore Docker in formato, archiviare file JSON hello in un percorso accessibile. Successivamente, toodeploy hello contenitore, eseguire hello comando seguente. Specificare il nome di hello del file JSON hello (`marathon.json` in questo esempio).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

output di Hello è simile toohello seguenti:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

A questo punto, se si esegue una query per le applicazioni maratona, questa nuova applicazione viene visualizzata nell'output di hello.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>Raggiungere hello contenitore

È possibile verificare tale hello che nginx viene eseguita in un contenitore in uno degli agenti di privata hello cluster hello. host hello toofind e la porta in cui è in esecuzione il contenitore di hello, eseguire una query maratona per hello attività in esecuzione: 

```bash
curl localhost/marathon/v2/tasks
```

Trovare il valore di hello `host` nell'output di hello (un indirizzo IP simile troppo`10.32.0.x`) e il valore di hello di `ports`.


Creare una gestione SSH terminal connessione (non un tunnel) toohello FQDN del cluster di hello. Una volta connessi, rendere hello richiesta seguente, sostituendo i valori corretti di hello di `host` e `ports`:

```bash
curl http://host:ports
```

Hello output server Nginx è simile toohello seguenti:

![Nginx dal contenitore](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Ridimensionare i contenitori
È possibile utilizzare hello maratona API tooscale out o la scala in distribuzioni di applicazioni. Nell'esempio precedente hello, si è distribuito un'istanza di un'applicazione. Possibile modificare le proporzioni toothree istanze di un'applicazione. toodo in tal caso, creare un file JSON utilizzando hello dopo il testo JSON e archiviarlo in un percorso accessibile.

```json
{ "instances": 3 }
```

Eseguire la connessione di tunneling, hello successivo comando tooscale out applicazione hello.

> [!NOTE]
> Hello URI è seguito dall'ID hello di hello applicazione tooscale http://localhost/marathon/v2/apps/. Se si utilizza hello Nginx esempio fornito in questo caso, hello URI sarebbe http://localhost/marathon/v2/apps/nginx.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Infine, eseguire una query endpoint maratona hello per le applicazioni. Ora sono presenti tre contenitori Nginx.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Comandi di PowerShell equivalenti
È possibile eseguire queste stesse azioni usando i comandi di PowerShell in un sistema Windows.

toogather informazioni sui cluster di controller di dominio/OS hello, ad esempio i nomi agente e lo stato dell'agente, eseguire hello comando seguente:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

Distribuire contenitori di Docker in formato tramite maratona utilizzando un file JSON che descrive la distribuzione di hello destinato. Hello esempio seguente consente di distribuire contenitore Nginx hello, porta 80 dell'agente per controller di dominio/OS hello tooport 80 del contenitore hello di associazione.

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy un contenitore Docker in formato, archiviare file JSON hello in un percorso accessibile. Successivamente, toodeploy hello contenitore, eseguire hello comando seguente. Specificare i file JSON di hello percorso toohello (`marathon.json` in questo esempio).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

È possibile utilizzare anche hello maratona API tooscale out o la scala in distribuzioni di applicazioni. Nell'esempio precedente hello, si è distribuito un'istanza di un'applicazione. Possibile modificare le proporzioni toothree istanze di un'applicazione. toodo in tal caso, creare un file JSON utilizzando hello dopo il testo JSON e archiviarlo in un percorso accessibile.

```json
{ "instances": 3 }
```

Eseguire hello tooscale comando out applicazione hello seguenti:

> [!NOTE]
> Hello URI è seguito dall'ID hello di hello applicazione tooscale http://localhost/marathon/v2/apps/. Se si utilizza esempio Nginx hello fornito di seguito, hello URI sarebbe http://localhost/marathon/v2/apps/nginx.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Passaggi successivi
* [Per ulteriori informazioni su endpoint HTTP Mesos hello](http://mesos.apache.org/documentation/latest/endpoints/)
* [Per ulteriori informazioni su hello maratona REST API](https://mesosphere.github.io/marathon/docs/rest-api.html)

