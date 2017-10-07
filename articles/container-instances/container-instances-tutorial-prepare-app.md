---
title: esercitazione per istanze di contenitori - aaaAzure preparazione dell'app | Documenti di Azure
description: Preparare un'applicazione per la distribuzione tooAzure istanze di contenitori
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Creare il contenitore per la distribuzione tooAzure istanze di contenitori

Istanze di contenitore di Azure consente la distribuzione di contenitori Docker nell'infrastruttura di Azure senza effettuare il provisioning di macchine virtuali o adottare servizi di livello superiore. In questa esercitazione si compilerà una semplice applicazione Web in Node.js e si creerà un pacchetto in un contenitore che può essere eseguito usando Istanze di contenitore di Azure. Verranno illustrati gli argomenti seguenti:

> [!div class="checklist"]
> * Clonazione dell'origine applicazione da GitHub  
> * Creazione di immagini del contenitore dall'origine applicazione
> * Test delle immagini di hello in un ambiente locale in Docker

Nelle esercitazioni successive, è caricare il tooan immagine del Registro di sistema di Azure contenitore e quindi distribuirli tooAzure istanze di contenitori.

## <a name="before-you-begin"></a>Prima di iniziare

Questa esercitazione presuppone una conoscenza di base dei concetti principali di Docker, come contenitori, immagini dei contenitore e comandi essenziali. Se necessario, vedere [Introduzione a Docker]( https://docs.docker.com/get-started/) per una panoramica sui concetti fondamentali relativi al contenitore. 

toocomplete questa esercitazione, è necessario un ambiente di sviluppo di Docker. Docker offre pacchetti che consentono di configurare facilmente Docker in qualsiasi sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) o [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Ottenere il codice dell'applicazione

esempio Hello in questa esercitazione include una semplice applicazione web incorporata [Node.js](http://nodejs.org). applicazione Hello serve di una pagina HTML statica e simile al seguente:

![App dell'esercitazione visualizzata in un browser][aci-tutorial-app]

Usare git toodownload hello-esempio:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Crea immagine del contenitore hello

Hello Dockerfile fornito nel repository di esempio hello viene illustrata la modalità di compilazione contenitore hello. Viene avviato da un [ufficiale immagine Node.js] [ dockerhub-nodeimage] in base a [Linux Alpine](https://alpinelinux.org/), una distribuzione di piccole dimensioni che è adatto toouse con i contenitori. Viene quindi copia i file dell'applicazione hello in un contenitore di hello, installa le dipendenze tramite Gestione pacchetti di nodi hello e infine viene avviata un'applicazione hello.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Hello utilizzare `docker build` comando toocreate hello immagine contenitore come tag *aci-esercitazione-app*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Hello utilizzare `docker images` immagine hello compilato toosee:

```bash
docker images
```

Output:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Eseguire il contenitore di hello in locale

Prima di tentare la distribuzione di hello contenitore tooAzure istanze di contenitori, eseguirla localmente tooconfirm del corretto funzionamento. Hello `-d` switch consente contenitore hello eseguito in background hello, mentre `-p` consente toomap una porta arbitraria del tooport calcolo 80 nel contenitore hello.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Aprire hello browser toohttp://localhost:8080 tooconfirm che hello contenitore è in esecuzione.

![App di hello in esecuzione in locale nel browser hello][aci-tutorial-app-local]

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, è stato creato un'immagine contenitore che può essere distribuito tooAzure istanze di contenitori. sono stata completata Hello alla procedura seguente:

> [!div class="checklist"]
> * La clonazione di origine dell'applicazione hello da GitHub  
> * Creazione di immagini del contenitore dall'origine applicazione
> * Contenitore di hello di test in locale

Spostare toohello Avanti toolearn esercitazione sull'archiviazione di immagini contenitore in un registro di sistema di contenitore di Azure.

> [!div class="nextstepaction"]
> [Push tooAzure immagini contenitore del Registro di sistema](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png