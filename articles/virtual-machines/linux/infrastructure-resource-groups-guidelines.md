---
title: gruppi aaaResource per le macchine virtuali Linux in Azure | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la distribuzione di gruppi di risorse in servizi di infrastruttura di Azure.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8809cb5eeb9a166d2bcf1946cd26b0ee748f8cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Linee guida sui gruppi di risorse di Azure per macchine virtuali Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

In questo articolo si incentra sulla comprensione come toologically orizzontale dell'ambiente di compilazione e raggruppare tutti i componenti di hello in gruppi di risorse.

## <a name="implementation-guidelines-for-resource-groups"></a>Linee guida sui gruppi di risorse
Decisioni:

* Verranno toobuild i gruppi di risorse dai componenti di infrastruttura core hello o dalla distribuzione di applicazione completa?
* È necessario toorestrict accesso tooResource gruppi tramite i controlli di accesso basato sui ruoli?

Attività:

* Definire i componenti dell'infrastruttura di base e i gruppi di risorse dedicati necessari.
* Revisione come tooimplement i modelli di gestione risorse per le distribuzioni coerente e riproducibile.
* Definire i ruoli di accesso utente è necessario per controllare l'accesso tooResource gruppi.
* Creare set di hello di gruppi di risorse utilizzando la convenzione di denominazione. È possibile utilizzare hello CLI di Azure o il portale.

## <a name="resource-groups"></a>Gruppi di risorse
In Azure, logicamente risorse correlate, ad esempio gli account di archiviazione, reti virtuali e macchine virtuali (VM) toodeploy, gestire e li gestisce come una singola entità. Questo approccio rende un più semplice applicazioni toodeploy mentre mantenendo hello tutte risorse correlate insieme da una prospettiva di gestione o toogrant altri gruppo toothat di accesso di risorse. I nomi dei gruppi di risorse non possono contenere più di 90 caratteri. Per una comprensione più completa dei gruppi di risorse, è possibile leggere hello [Panoramica di gestione risorse di Azure](../../azure-resource-manager/resource-group-overview.md).

Una funzionalità chiave tooResource gruppi hello possibilità toobuild ambiente mediante un file JSON che dichiara hello reti di archiviazione, e le risorse di calcolo. È inoltre possibile definire qualsiasi script personalizzato correlati o tooapply configurazioni. Tramite i modelli JSON è possibile creare distribuzioni coerenti e riproducibili delle applicazioni. Questo approccio consente di creare un ambiente di sviluppo e quindi utilizzare tale toocreate modello stesso, una distribuzione di produzione, o viceversa. Per una migliore comprensione sull'utilizzo dei modelli, leggere [hello procedura dettagliata modello](../../azure-resource-manager/resource-manager-template-walkthrough.md) che illustra ogni passaggio della creazione di un modello JSON.

Esistono due diversi approcci alla progettazione dell'ambiente con gruppi di risorse:

* Gruppi di risorse per ogni distribuzione dell'applicazione che combina hello account di archiviazione, reti virtuali e subnet, le macchine virtuali, caricare il bilanciamento del carico e così via.
* Gruppi di risorse centralizzate che contengono la rete virtuale di base e le subnet oppure gli account di archiviazione. Le applicazioni si trovano quindi nei propri gruppi di risorse che contengono solo macchine virtuali, servizi di bilanciamento del carico, interfacce di rete e così via.

La scalabilità orizzontale, la creazione di gruppi di risorse centralizzata per la rete virtuale e subnet rende più semplice toobuild cross-premise le connessioni per le opzioni di connettività ibrida di rete. approccio alternativo Hello è per ogni applicazione toohave la propria rete virtuale che richiede una configurazione e manutenzione. [I controlli di accesso basato sui ruoli](../../active-directory/role-based-access-control-what-is.md) forniscono un accesso toocontrol modo granulare tooResource gruppi. Per le applicazioni di produzione, è possibile controllare gli utenti di hello che possono accedere alle risorse, o per le risorse di infrastruttura di hello core è possibile limitare solo tecnici dell'infrastruttura toowork con essi. I proprietari delle applicazioni hanno solo accesso toohello componenti dell'applicazione nei propri non hello componenti di base dell'ambiente di infrastruttura di Azure e nel gruppo di risorse. Quando si progetta l'ambiente, considerare gli utenti di hello che richiedono l'accesso alle risorse di toohello e progettare di conseguenza i gruppi di risorse. 

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

