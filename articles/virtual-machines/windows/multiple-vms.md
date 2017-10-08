---
title: "aaaCreate più macchine virtuali | Documenti Microsoft"
description: "Opzioni per la creazione di più macchine virtuali in Windows"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Creazione di più macchine virtuali di Azure
Esistono molti scenari in cui è necessario toocreate un numero elevato di macchine virtuali simili (VM). Alcuni esempi comprendono scenari di high-performance computing (HPC), di analisi dei dati su larga scala, di server di livello intermedio o back-end scalabili e spesso senza stato (come i server Web) e di database distribuiti.

Questo articolo illustra hello opzioni disponibili toocreate più macchine virtuali in Azure. Queste opzioni andare oltre casi più semplici hello in cui si crea manualmente una serie di macchine virtuali. toocreate più macchine virtuali, i processi di hello utilizzato in genere non applicare la scalabilità anche se è necessario toocreate più di un numero limitato di macchine virtuali.

Unidirezionale toocreate più macchine virtuali simili è costrutto di gestione risorse di Azure hello toouse di *risorse cicli*.

## <a name="resource-loops"></a>cicli di risorse
I cicli di risorse sono una sintassi abbreviata nei modelli di Gestione risorse di Azure. I cicli di risorse possono creare un set di risorse configurate in modo simile in un ciclo. È possibile utilizzare risorse cicli toocreate più account di archiviazione, interfacce di rete o le macchine virtuali. Per ulteriori informazioni sui cicli di risorse, vedere troppo[creare macchine virtuali nel set di disponibilità utilizzando cicli risorsa](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Problemi di scalabilità
Anche se i cicli di risorsa rendono più semplice toobuild out un'infrastruttura cloud su scala e generare modelli più concisi, rimangono alcuni problemi. Ad esempio, se si utilizzano un ciclo toocreate 100 macchine virtuali di risorse, è necessario toocorrelate controller di interfaccia rete (NIC) con le macchine virtuali corrispondenti e gli account di archiviazione. Poiché il numero di hello di macchine virtuali è probabilmente toobe diverso dal numero di hello di account di archiviazione, toodeal con dimensioni di ciclo di risorse diverso, sarà necessario troppo. Si tratta subito i problemi, ma la complessità di hello aumenta notevolmente con scala.

Un altro problema si verifica quando è necessaria un'infrastruttura che viene ridimensionata in modo elastico. Ad esempio, è un'infrastruttura di scalabilità automatica che aumenta o riduce hello numero di macchine virtuali in tooworkload risposta automaticamente. Macchine virtuali non forniscono un meccanismo integrato di toovary in quanto a numero (scalabilità orizzontale e scalabilità in). Se scala in rimuovendo le macchine virtuali, è difficile tooguarantee la disponibilità elevata assicurandosi che le macchine virtuali vengono bilanciate tra i domini di aggiornamento e di errore.

Infine, quando si utilizza un ciclo di risorsa, le risorse di più chiamate toocreate andare infrastruttura sottostante toohello. Quando più chiamate creano risorse simili, Azure ha un tooimprove opportunità implicita durante la progettazione e ottimizzare le prestazioni e affidabilità di distribuzione. A questo punto entrano in gioco i *set di scalabilità di macchine virtuali* .

## <a name="virtual-machine-scale-sets"></a>set di scalabilità di macchine virtuali
Set di scalabilità di macchine virtuali sono un toodeploy risorse di calcolo di Azure e gestire un set di macchine virtuali identiche. Con tutte le macchine virtuali configurate hello stesso, il set di scalabilità di macchine Virtuali è tooscale semplice in e la scalabilità orizzontale. È sufficiente modificare il numero di hello di macchine virtuali nel set di hello. È inoltre possibile configurare tooautoscale di set di scalabilità macchina virtuale in base alle esigenze di hello del carico di lavoro hello.

Per applicazioni che richiedono risorse di calcolo tooscale in scala e le operazioni sono bilanciate in modo implicito tra i domini di errore e di aggiornamento.

Invece di correlare più risorse, ad esempio schede NIC e VM, un set di scalabilità della VM è dotato delle proprietà relative alla rete, all'archiviazione, alle macchine virtuali e all'estensione, che è possibile configurare in modo centralizzato.

Per il set di una scala tooVM introduzione, vedere toohello [scalabilità della macchina virtuale Imposta pagina prodotto](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Per ulteriori informazioni, visitare toohello [scalabilità di macchine virtuali imposta documentazione](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

