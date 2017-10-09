---
title: aaaAzure campioni CLI - servizio App | Documenti Microsoft
description: Esempi dell'Interfaccia della riga di comando di Azure - Servizio app
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Esempi dell'interfaccia della riga di comando di Azure

Hello nella tabella seguente include gli script toobash collegamenti compilati utilizzando hello CLI di Azure.

| | |
|-|-|
|**Creare un'app**||
| [Creare un'app Web e distribuire il codice da GitHub](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un'App Web di Azure e distribuisce il codice da un repository GitHub pubblico. |
| [Creare un'App Web con distribuzione continua da GitHub](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un'App Web con la pubblicazione continua da un archivio GitHub di cui si è proprietari. |
| [Creare un'App Web e distribuire il codice da un archivio Git locale](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un'App Web di Azure e configura il push del codice da un archivio Git locale. |
| [Creare un'app web e distribuire codice tooa ambiente di gestione temporanea](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un'App Web di Azure con uno slot di distribuzione per le modifiche al codice di gestione temporanea. |
| [Creare un'app Web ASP.NET Core in un contenitore Docker](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un'App Web di Azure in Linux e carica un'immagine Docker da Docker Hub. |
|**Configurare l'applicazione**||
| [Eseguire il mapping di un'app web tooa di dominio personalizzato](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un'app web di Azure e associa un tooit nome di dominio personalizzato. |
| [Associare un'app web tooa di certificati SSL personalizzata](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un'app web di Azure e associa il certificato SSL hello di un tooit nome di dominio personalizzato. |
|**Ridimensionare un'app**||
| [Ridimensionare un'App Web manualmente](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un'App Web di Azure e la ridimensiona su 2 istanze. |
| [Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | Crea due App Web di Azure in due aree geografiche diverse e le rende disponibili tramite un solo endpoint usando Gestione traffico di Azure. |
|**Connettersi tooresources app**||
| [Connettersi a un tooa app web SQL Database](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un'app web di Azure e un database SQL, quindi aggiunge hello stringa toohello app le impostazioni di connessione. |
| [Connettersi a un account di archiviazione tooa app web](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un'applicazione web di Azure e un account di archiviazione, quindi aggiunge hello archiviazione connessione toohello app le impostazioni della stringa. |
| [Connettersi a una cache di redis tooa app web](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un'applicazione web di Azure e una cache redis, quindi aggiunge le impostazioni di app toohello Dettagli connessione redis hello.) |
| [Connettersi a un tooCosmos app web DB](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un'applicazione web di Azure e un database Cosmos, quindi aggiunge le impostazioni di app toohello Dettagli connessione DB Cosmos hello. |
|**Monitorare un'app**||
| [Monitorare un'App Web con i log del server Web](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un'app web di Azure e consente la registrazione per il computer locale di hello registri tooyour Scarica. |
| | |