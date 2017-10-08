---
title: aaaTroubleshooting istanze di contenitori di Azure
description: Informazioni su come tootroubleshoot problemi con le istanze di contenitore di Azure
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
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Risolvere i problemi di distribuzione in Istanze di contenitore di Azure

Questo articolo illustra come tootroubleshoot problemi durante la distribuzione di contenitori tooAzure istanze di contenitori. Vengono inoltre descritti alcuni dei problemi comuni di hello che si verifichino.

## <a name="getting-diagnostic-events"></a>Recupero degli eventi di diagnostica

log tooview dal codice dell'applicazione in un contenitore, è possibile utilizzare hello [az contenitore registri](/cli/azure/container#logs) comando. Ma se il contenitore non viene distribuito correttamente, è necessario informazioni di diagnostica hello tooreview fornite dal provider di risorse hello istanze di contenitori di Azure. eventi di hello tooview per il contenitore, eseguire hello comando seguente:

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

output di Hello include proprietà principali hello del contenitore, insieme agli eventi di distribuzione:

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a>Problemi di distribuzione comuni

La maggior parte degli errori riscontrati durante la distribuzione è dovuta ad alcuni problemi comuni.

### <a name="unable-toopull-image"></a>Non è possibile toopull immagine

Se le istanze di contenitore di Azure è Impossibile toopull immagine inizialmente, eseguire un nuovo tentativo per un certo periodo prima che alla fine. Se non è possibile effettuare il pull di immagine hello, vengono visualizzati gli eventi hello seguente:

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

tooresolve, eliminare il contenitore di hello e ripetere la distribuzione, che sia stato digitato correttamente il nome di immagine hello pagante attenzione.

### <a name="container-continually-exits-and-restarts"></a>Il contenitore viene continuamente chiuso e riavviato

Istanze di contenitore di Azure supporta attualmente solo servizi a esecuzione prolungata. Se il contenitore esegue toocompletion e viene chiusa, viene automaticamente riavviata e viene eseguito di nuovo. In questo caso, vengono visualizzati eventi simili ai seguenti. Nota che il contenitore hello si avvia, viene riavviato rapidamente. Hello contenitore istanze API include un `retryCount` proprietà che indica quante volte un determinato contenitore è stato riavviato.

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> La maggior parte delle immagini contenitore per le distribuzioni di Linux impostare una shell, come bash, come comando predefinito hello. Poiché una shell non è di per sé un servizio a esecuzione prolungata, questi contenitori vengono chiusi immediatamente e sono soggetti a un riavvio ciclico.

### <a name="container-takes-a-long-time-toostart"></a>Contenitore accetta un toostart molto tempo

Se il contenitore richiede un toostart molto tempo, ma andrà a buon fine, iniziare esaminando dimensioni hello dell'immagine contenitore. Poiché le istanze di contenitore di Azure effettua il pull dell'immagine del contenitore su richiesta, si verificano tempi di avvio di hello sono tooits direttamente correlate, dimensioni.

È possibile visualizzare dimensioni hello dell'immagine contenitore con Docker CLI hello:

```bash
docker images
```

Output:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

dimensioni dell'immagine di Hello tookeeping chiave piccole consiste nel garantire che l'immagine finale non può contenere dati che non è necessaria in fase di esecuzione. Un modo toodo con [compilazioni a più fasi](https://docs.docker.com/engine/userguide/eng-image/multistage-build/). Le compilazioni a più fasi rendono tooensure semplice che immagine finale hello contenga solo elementi hello è necessario per l'applicazione e non hello aggiuntivo di contenuto che è stato richiesto al momento della compilazione.

altri effetti di hello tooreduce modo di hello immagine pull ora di avvio del contenitore Hello sono toohost hello contenitore immagine utilizzando Ciao del Registro di sistema di Azure contenitore hello stessa area in cui si intende toouse istanze di contenitori di Azure. Questo riduce percorso di rete hello hello tootravel di esigenze immagine contenitore, ridurre notevolmente i tempi di download hello.
