---
title: Panoramica di Istanze di contenitore di Azure | Azure Docs
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
ms.openlocfilehash: 6e614f1120b3dc54871b393ac0a2703c21b30ae8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="azure-container-instances"></a>Istanze di contenitore di Azure

I contenitori si stanno rapidamente affermando come soluzione preferita per creare pacchetti, distribuire e gestire le applicazioni cloud. Istanze di contenitore di Azure rappresenta il modo più semplice e rapido per eseguire un contenitore in Azure, senza dover effettuare il provisioning di macchine virtuali o adottare un servizio di livello superiore.

Istanze di contenitore di Azure è un'ottima soluzione per qualsiasi scenario e funziona anche in contenitori isolati, inclusi i processi di compilazione, l'automazione di attività e le applicazioni semplici. Per gli scenari in cui si rende necessaria l'orchestrazione completa dei contenitori, quali il rilevamento dei servizi tra più contenitori, la scalabilità automatica e gli aggiornamenti coordinati delle applicazioni, è consigliabile usare il [Servizio contenitore di Azure](https://docs.microsoft.com/azure/container-service/).

## <a name="fast-startup-times"></a>Tempi di avvio rapidi

I contenitori offrono notevoli vantaggi in termini di avvio rispetto alle macchine virtuali. Istanze di contenitore di Azure permette di avviare un contenitore in Azure in pochi secondi, senza dover gestire macchine virtuali o effettuarne il provisioning.

## <a name="hypervisor-level-security"></a>Sicurezza a livello di hypervisor

In passato i contenitori offrivano l'isolamento di dipendenze delle applicazioni e la governance delle risorse, ma non erano considerati sufficientemente protetti per l'uso di multi-tenant ostili. Con Istanze di contenitore di Azure, l'applicazione è altrettanto isolata nel contenitore che in una macchina virtuale.

## <a name="custom-sizes"></a>Dimensioni personalizzate

I contenitori sono in genere ottimizzati per l'esecuzione di un'applicazione singola, ma le esigenze specifiche di tale applicazione possono variare notevolmente. Con Istanze di contenitore di Azure è possibile specificare esattamente la richiesta in termini di memoria e di core CPU. Si paga in base alla richiesta, fatturata al secondo. Questo permette di ottimizzare con precisione la spesa in base alle esigenze.

## <a name="public-ip-connectivity"></a>Connettività tramite indirizzo IP pubblico

Istanze di contenitore di Azure permette di esporre i contenitori direttamente a Internet con un indirizzo IP pubblico. In futuro, le funzionalità di rete verranno estese all'integrazione con reti virtuali, servizi di bilanciamento del carico e altre componenti essenziali dell'infrastruttura di rete di Azure.

## <a name="persistent-storage"></a>Archiviazione permanente

Per recuperare e rendere persistente lo stato con Istanze di contenitore di Azure, è disponibile il montaggio diretto di condivisioni file di Azure.

## <a name="linux-and-windows-containers"></a>Contenitori Linux e Windows

Istanze di contenitore di Azure permette di pianificare i contenitori Windows e Linux con la stessa API. È sufficiente indicare il tipo di sistema operativo di base. Tutti gli altri elementi sono identici.

## <a name="co-scheduled-groups"></a>Gruppi con pianificazione condivisa

Istanze di contenitore di Azure supporta la pianificazione di gruppi multi-contenitore che condividono un computer host, una rete locale, un'archiviazione e un ciclo di vita. Questo permette di combinare l'applicazione principale con altre che svolgono un ruolo di supporto, ad esempio la registrazione.

## <a name="next-steps"></a>Passaggi successivi

Provare a distribuire un contenitore in Azure con un comando singolo, seguendo le indicazioni della [guida introduttiva](container-instances-quickstart.md).