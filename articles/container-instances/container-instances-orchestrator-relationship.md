---
title: Istanze di contenitori aaaAzure e orchestrazione contenitore
description: Informazioni sull'interazione tra Istanze di contenitore di Azure e gli agenti di orchestrazione dei contenitori
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Istanze di contenitore di Azure e agenti di orchestrazione dei contenitori

Grazie alle dimensioni ridotte e all'orientamento alle applicazioni, i contenitori sono particolarmente adatti per ambienti di recapito flessibili e architetture basate su microservizi. Hello attività di automazione e gestione di un numero elevato di contenitori e l'interazione è detta *orchestrazione*. Orchestrators contenitore più diffusi includono Kubernetes, controller di dominio/OS e Docker Swarm, ognuno dei quali sono disponibili in hello [servizio contenitore di Azure](https://docs.microsoft.com/azure/container-service/).

Istanze di contenitore di Azure fornisce alcune funzionalità delle piattaforme di orchestrazione di programmazione base hello, ma non copre servizi di valore più alto di hello forniscano tali piattaforme e possono infatti essere complementare con essi. Questo articolo descrive l'ambito di hello di ciò che gestisce le istanze di contenitore di Azure e il livello di riempimento orchestrators contenitore potrebbe interagire con esso.

## <a name="traditional-orchestration"></a>Orchestrazione tradizionale

definizione di standard Hello dell'orchestrazione include hello seguenti attività:

- **Pianificazione**: data una richiesta di risorse e di un'immagine contenitore, trovare una macchina adatta per il contenitore di hello toorun.
- **Affinità/Antiaffinità**: specificare che i contenitori di un set devono essere eseguiti vicini tra loro (per le prestazioni) o sufficientemente distanti tra loro (disponibilità).
- **Monitoraggio dell'integrità**: monitorare gli errori dei contenitori e modificare automaticamente la pianificazione.
- **Failover**: tenere traccia dei quali è in esecuzione in ogni computer e riprogrammare i contenitori da nodi toohealthy macchine non riuscita.
- **Scalabilità**: aggiungere o rimuovere richiesta toomatch istanze di contenitore, automaticamente o manualmente.
- **Rete**: fornire una rete di sovrapposizione per il coordinamento di contenitori toocommunicate tra più computer host.
- **Individuazione del servizio**: abilitare contenitori toolocate loro automaticamente anche come che si spostano tra computer host e modificare gli indirizzi IP.
- **Coordinare gli aggiornamenti dell'applicazione**: gestire l'applicazione contenitore di tooavoid aggiornamenti tempi di inattività e abilitare il rollback in caso di errore.

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>Orchestrazione con Istanze di contenitore di Azure: un approccio a più livelli

Istanze di contenitore di Azure fornisce tooorchestration un approccio a più livelli, tutta la programmazione hello e funzionalità di gestione richiesti toorun un singolo contenitore, consentendo allo stesso orchestrator attività di contenitore a più piattaforme toomanage su di esso.

Poiché tutti hello sottostante l'infrastruttura per le istanze del contenitore è gestito da Azure, una piattaforma di orchestrator non è necessario tooconcern stessa con la ricerca di una macchina host appropriato nel quale toorun un singolo contenitore. l'elasticità del cloud hello Hello garantisce che uno è sempre disponibile. Al contrario, orchestrator hello può concentrarsi sulle attività hello che semplificano lo sviluppo di hello di architetture multi-contenitore, tra cui l'adattamento e coordinare gli aggiornamenti.



## <a name="potential-scenarios"></a>Potenziali scenari

Anche se l'integrazione degli agenti di orchestrazione con Istanze di contenitore di Azure è ancora agli inizi, si prevede che possano emergere alcuni ambienti diversi:

### <a name="orchestration-of-container-instances-exclusively"></a>Orchestrazione di Istanze di contenitore in modo esclusivo

Poiché l'avvio rapido e fatturare da hello in secondo luogo, un ambiente basato esclusivamente su istanze di contenitori di Azure offre avviato tooget modo più rapido hello e toodeal con carichi di lavoro estremamente variabile.

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>Combinazione di Istanze di contenitore e contenitori in macchine virtuali

Per l'esecuzione prolungata, carichi di lavoro stabile, l'orchestrazione di contenitori in un cluster di macchine virtuali dedicate corrisponderà in genere più economiche rispetto all'esecuzione hello stessi contenitori con istanze di contenitori. Tuttavia, istanze di contenitori offrono un'ottima soluzione per rapidamente espansione e la toodeal capacità globale con imprevisti o di breve durati picchi di utilizzo. Invece di scalabilità orizzontale numero hello di macchine virtuali del cluster, quindi la distribuzione di altri contenitori in tali computer, orchestrator hello può semplicemente pianificare altri contenitori hello utilizzando istanze di contenitori ed eliminarli quando non è più necessario.

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>Implementazione di esempio: connettore di Istanze di contenitore di Azure per Kubernetes

toodemonstrate come piattaforme di orchestrazione contenitore è possono integrare con istanze di contenitori di Azure, abbiamo iniziato compilazione un [connettore di esempio per Kubernetes][aci-connector-k8s]. 

Hello connettore per Kubernetes riproduce hello [kubelet] [ kubelet-doc] registrando come nodo con capacità di un numero illimitata e invio di creazione di hello di [POD] [ pod-doc] come gruppi contenitore in istanze di contenitori di Azure. 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

I connettori per altri orchestrators può essere implementati in modo analogo è integrato con piattaforma primitive toocombine hello potenza orchestrator hello API con velocità hello e semplicità di gestione dei contenitori di istanze di contenitori di Azure.

> [!WARNING]
> Hello connettore ACI per Kubernetes è *sperimentale* e non deve essere utilizzato nell'ambiente di produzione.

## <a name="next-steps"></a>Passaggi successivi

Creare il primo contenitore con le istanze di contenitore di Azure utilizzando hello [Guida introduttiva](container-instances-quickstart.md).

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/