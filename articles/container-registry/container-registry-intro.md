---
title: i registri di contenitore Docker aaaPrivate in Azure | Documenti Microsoft
description: Introduzione toohello del Registro di sistema di Azure contenitore servizio basato su cloud gestiti, registri privati di Docker.
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Registri di sistema contenitore Docker tooprivate introduzione


Registro di sistema di contenitore di Azure è di tipo gestito [Registro di sistema Docker](https://docs.docker.com/registry/) servizio basato su hello open source Docker del Registro di sistema 2.0. Creare e gestire toostore registri contenitore di Azure e gestire il privato [contenitore Docker](https://www.docker.com/what-docker) immagini. Utilizzare i registri di contenitore in Azure con le pipeline di distribuzione e sviluppo contenitore esistente e disegnare sul corpo hello di esperienza della community di Docker.

Per informazioni su Docker e sui contenitori, vedere:

* [Guida dell'utente di Docker](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Casi d'uso
Effettuare il pull immagini da un contenitore di Azure le destinazioni di distribuzione toovarious del Registro di sistema:

* **Sistemi di orchestrazione scalabili** che gestiscono applicazioni in contenitori in cluster di host, quali [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) e [Kubernetes](http://kubernetes.io/docs/).
* **Servizi di Azure** che supportano la creazione e l'esecuzione di applicazioni su vasta scala, come [Servizio contenitore](../container-service/index.yml), [Servizio app](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) e altri.

Gli sviluppatori possono anche push tooa del Registro di sistema contenitore come parte di un flusso di lavoro di sviluppo di contenitore. ad esempio specificando come destinazione un Registro di sistema del contenitore da uno strumento di distribuzione e integrazione continua, quali [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) o [Jenkins](https://jenkins.io/).





## <a name="key-concepts"></a>Concetti chiave
* **Registro**. Creare uno o più registri contenitori nella sottoscrizione di Azure. Ogni registro di sistema è supportato da Azure un standard [account di archiviazione](../storage/common/storage-introduction.md) in hello nello stesso percorso. Sfruttare i vantaggi di archiviazione locale, rete e di chiusura delle immagini contenitore tramite la creazione di un registro di sistema in hello stesso percorso di Azure come le distribuzioni. Un nome completo del Registro di sistema ha il formato di hello `myregistry.azurecr.io`.

  Si [controllare l'accesso](container-registry-authentication.md) Registro di sistema di contenitore tooa mediante una Azure Active Directory di backup [dell'entità servizio](../active-directory/active-directory-application-objects.md) o un account amministratore specificato. Esecuzione hello standard `docker login` tooauthenticate comando con un registro di sistema.

* **Registro gestito**: livello che offre funzionalità aggiuntive per i registri in tre SKU, ovvero Basic, Standard e Premium. negli account di archiviazione gestiti dal servizio di registri di contenitore di Azure, che migliora l'affidabilità e offre funzionalità hello sono archiviate le immagini di Hello in queste SKU. Le nuove funzionalità includono l'integrazione webhook, l'autenticazione nel repository con Azure Active Directory e il supporto della funzionalità di eliminazione. Gli utenti hanno hello opzione toochoose tra registri gestiti o toocreate un registro di sistema supportato dai propri account di archiviazione durante la creazione di registri di sistema.

* **Repository**. Un registro contiene uno o più repository, costituiti da gruppi di immagini contenitore. Registro contenitori di Azure supporta spazi dei nomi dei repository multilivello. Questa funzionalità consente di toogroup raccolte di app specifica tooa correlati di immagini, o una raccolta di sviluppo di App toospecific o i team operativi. ad esempio:

  * `myregistry.azurecr.io/aspnetcore:1.0.1` rappresenta un'immagine a livello aziendale
  * `myregistry.azurecr.io/warrantydept/dotnet-build`rappresenta un'immagine usata app .NET toobuild, condivise tra il reparto di garanzia hello
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`rappresenta un'immagine di web app invii di hello cliente, reparto garanzia hello di proprietà di raggruppamento

* **Immagine**. Ogni immagine archiviata in un repository è uno snapshot di sola lettura di un contenitore Docker. I registri contenitori di Azure possono includere immagini sia Windows che Linux. L'utente controlla i nomi delle immagini per tutte le distribuzioni di contenitori. Standard di utilizzo [i comandi di Docker](https://docs.docker.com/engine/reference/commandline/) toopush immagini in un repository o un'immagine da un repository di pull.

* **Contenitore**. Un contenitore definisce e racchiude un'applicazione software e le relative dipendenze in un file system completo, con codice, runtime, strumenti di sistema e librerie. I contenitori Docker vengono eseguiti in base alle immagini Windows o Linux di cui si effettua il pull da un registro contenitori. Contenitori in esecuzione in un unico computer condividono kernel del sistema operativo hello. Contenitori di docker sono completamente portabili tooall principali distribuzioni di Linux, Mac e Windows.




## <a name="next-steps"></a>Passaggi successivi
* [Creare un registro di sistema di contenitore utilizzando hello portale di Azure](container-registry-get-started-portal.md)
* [Creare un registro di sistema di contenitore utilizzando hello CLI di Azure](container-registry-get-started-azure-cli.md)
* [La prima immagine usando Docker CLI hello push](container-registry-get-started-docker-cli.md)
* toobuild un'integrazione continua e flusso di lavoro di distribuzione utilizzando Visual Studio Team Services, servizio di contenitore di Azure e Azure contenitore Registro di sistema, vedere [questa esercitazione](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Se si desidera tooset proprio Docker privato del Registro di sistema in Azure (senza un endpoint pubblico), vedere [la distribuzione del proprio privata Docker Registro di sistema in Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
