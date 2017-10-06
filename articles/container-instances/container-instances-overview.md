---
title: Panoramica di istanze di contenitore aaaAzure | Documenti di Azure
description: Informazioni su Istanze di contenitore di Azure
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
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a>Istanze di contenitore di Azure

Contenitori stanno diventando toopackage modo hello preferito, distribuire e gestire le applicazioni cloud. Istanze di contenitore di Azure offre hello più veloce e più semplice modo toorun un contenitore in Azure, senza dovere tooprovision tutte le macchine virtuali e senza doverlo tooadopt un servizio di livello superiore. 

Istanze di contenitore di Azure è un'ottima soluzione per qualsiasi scenario e funziona anche in contenitori isolati, inclusi i processi di compilazione, l'automazione di attività e le applicazioni semplici. Per gli scenari in cui è necessario disporre di tutte orchestrazione contenitore, incluso l'individuazione del servizio tra più contenitori di scalabilità automatica e gli aggiornamenti dell'applicazione coordinato, si consiglia di hello [servizio contenitore di Azure](https://docs.microsoft.com/azure/container-service/).

## <a name="fast-startup-times"></a>Tempi di avvio rapidi

I contenitori offrono notevoli vantaggi in termini di avvio rispetto alle macchine virtuali. Con le istanze di contenitore di Azure, è possibile avviare un contenitore in Azure in pochi secondi senza tooprovision necessità hello e gestire macchine virtuali.

## <a name="hypervisor-level-security"></a>Sicurezza a livello di hypervisor

In passato i contenitori offrivano l'isolamento di dipendenze delle applicazioni e la governance delle risorse, ma non erano considerati sufficientemente protetti per l'uso di multi-tenant ostili. Con Istanze di contenitore di Azure, l'applicazione è altrettanto isolata nel contenitore che in una macchina virtuale.

## <a name="custom-sizes"></a>Dimensioni personalizzate

I contenitori sono in genere ottimizzato toorun solo una singola applicazione, ma esigenze hello di tali applicazioni possono variare notevolmente. Con Istanze di contenitore di Azure è possibile specificare esattamente la richiesta in termini di memoria e di core CPU. Verranno addebitati i costi in base alle quali richiesta fatturato da hello in secondo luogo, in modo da ottimizzare più preciso la spesa in base alle proprie esigenze.

## <a name="public-ip-connectivity"></a>Connettività tramite indirizzo IP pubblico

Con le istanze di contenitore di Azure, è possibile esporre ai contenitori direttamente toohello internet con un indirizzo IP pubblico. In hello future, si verrà espandere la rete integrazione tooinclude di funzionalità con le reti virtuali, caricare bilanciamento del carico e altre parti principali di hello infrastruttura di rete di Azure.

## <a name="persistent-storage"></a>Archiviazione permanente

tooretrieve e rendere persistente lo stato con istanze di contenitori di Azure, offriamo condivisioni di file montaggio diretto di Azure.

## <a name="linux-and-windows-containers"></a>Contenitori Linux e Windows

Con istanze di contenitori di Azure, è possibile pianificare entrambe le finestre e i contenitori di Linux con hello stessa API. È sufficiente indicare il tipo di sistema operativo base hello e tutto il resto è identico.

## <a name="co-scheduled-groups"></a>Gruppi con pianificazione condivisa

Istanze di contenitore di Azure supporta la pianificazione di gruppi multi-contenitore che condividono un computer host, una rete locale, un'archiviazione e un ciclo di vita. In questo modo si toocombine dell'applicazione principale con altri utenti che svolge un ruolo di supporto, ad esempio la registrazione.

## <a name="next-steps"></a>Passaggi successivi

Provare a distribuire tooAzure un contenitore con un singolo comando con il nostro [Guida rapida](container-instances-quickstart.md).
