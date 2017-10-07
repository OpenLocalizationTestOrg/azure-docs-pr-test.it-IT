---
title: aaaIntroduction tooAzure servizio contenitore per Kubernetes | Documenti Microsoft
description: Servizio di contenitore di Azure per Kubernetes rende semplice toodeploy e gestire applicazioni basate sul contenitore in Azure.
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, Docker, contenitori, microservizi, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Introduzione tooAzure servizio contenitore per Kubernetes
Servizio di contenitore di Azure per Kubernetes rende semplice toocreate, configurare e gestire un cluster di macchine virtuali che sono preconfigurati toorun contenitore applicazioni. Questo consente di toouse le competenze esistenti, o disegnare su un corpo di grandi dimensioni e in continua crescito di esperienza della community, toodeploy e gestire le applicazioni basate sul contenitore in Microsoft Azure.

Tramite il servizio contenitore di Azure, è possibile sfruttare i vantaggi di hello funzionalità aziendale di Azure, mantenendo al tempo stesso la portabilità dell'applicazione tramite Kubernetes e hello formato immagine Docker.

## <a name="using-azure-container-service-for-kubernetes"></a>Uso del servizio contenitore di Azure per Kubernetes
L'obiettivo di Microsoft con il servizio contenitore di Azure è tooprovide un ambiente host del contenitore tramite strumenti open source e tecnologie che sono comuni tra i clienti oggi. toothis fine, è necessario esporre gli endpoint dell'API di Kubernetes standard hello. Tramite questi endpoint standard, è possibile utilizzare qualsiasi software che è in grado di comunicare tooa Kubernetes cluster. È ad esempio possibile scegliere [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) o [draft](https://github.com/Azure/draft).

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Creazione di un cluster Kubernetes con il servizio contenitore di Azure
toobegin utilizzando servizio contenitore di Azure, distribuire un cluster il servizio contenitore di Azure con hello [CLI di Azure 2.0](container-service-kubernetes-walkthrough.md) o tramite il portale di hello (hello ricerca Marketplace per **servizio contenitore di Azure**). Nel caso di un utente avanzato che necessita di maggiore controllo sui modelli di hello Azure Resource Manager, è possibile utilizzare open source di hello [acs motore](https://github.com/Azure/acs-engine) toobuild di progetto personalizzati Kubernetes personalizzato del cluster e distribuirlo tramite hello `az` CLI.

### <a name="using-kubernetes"></a>Uso di Kubernetes
Kubernetes automatizza la distribuzione, il ridimensionamento e la gestione delle applicazioni nei contenitori. Dispone di un set completo di funzionalità tra cui:
* Bin packing automatico
* Riparazione automatica
* Scalabilità orizzontale
* Bilanciamento del carico e rilevamento del servizio
* Implementazioni e ripristini dello stato precedente automatizzati
* Gestione della configurazione e dei segreti
* Orchestrazione dell'archiviazione
* Esecuzione batch

Diagramma dell'architettura di Kubernetes distribuito tramite il servizio contenitore di Azure:

![Il servizio contenitore di Azure configurato toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Video

Il supporto per Kubernetes nei servizi contenitore di Azure (Azure Friday, gennaio 2017):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Strumenti per lo sviluppo e la distribuzione di applicazioni in Kubernetes (Azure OpenDev, giugno 2017):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Passaggi successivi

Esplorare hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin esplorazione oggi servizio contenitore di Azure.
