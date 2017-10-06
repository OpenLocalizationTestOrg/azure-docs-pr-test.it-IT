---
title: aaaReplicate fisico locale tooAzure server con Azure Site Recovery | Documenti Microsoft
description: Viene fornita una panoramica dei passaggi di hello per la replica dei carichi di lavoro in esecuzione in locale Windows/Linux server fisici tooAzure con hello servizio Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Replicare tooAzure server fisici con il ripristino del sito

In questo articolo viene fornita una panoramica di hello passaggi necessari tooreplicate locale Windows/Linux server fisici tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.


## <a name="step-1-review-architecture-and-prerequisites"></a>Passaggio 1: Esaminare l'architettura e i prerequisiti

Prima di iniziare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di che aver compreso tutti i componenti di hello necessari tooset distribuzione hello.

Andare troppo[passaggio 1: esaminare l'architettura di hello](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Passaggio 2: Esaminare i prerequisiti

Assicurarsi di avere i prerequisiti di hello sul posto per ogni componente di distribuzione:

- **Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.
- **Componenti locali di Site Recovery**: è necessario un computer che esegue i componenti locali di Site Recovery.
- **Le macchine replicate**: server da tooreplicate necessario toocomply con requisiti di Azure e locali.

Andare troppo[passaggio 2: esaminare i prerequisiti e limitazioni](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Passaggio 3: Pianificare la capacità

Se si sta eseguendo una distribuzione completa, è necessario toofigure risorse quali la replica è necessario. Se si sta eseguendo una rapida Configura tootest hello ambiente, è possibile ignorare questo passaggio.

Andare troppo[passaggio 3: pianificare la capacità](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Passaggio 4: Pianificare la rete

È necessario toodo alcuni pianificazione tooensure che macchine virtuali di Azure siano connessi toonetworks dopo che si verifica il failover e che dispongano di hello destra indirizzi IP della rete.

Andare troppo[passaggio 4: pianificare la rete](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Passaggio 5: Preparare le risorse di Azure

Configurare le reti e le risorse di archiviazione di Azure prima di iniziare. 

Andare troppo[passaggio 5: preparare Azure](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>Passaggio 6: Configurare un insieme di credenziali

Per impostare un tooorchestrate insieme di credenziali di servizi di ripristino e gestire la replica. Quando si imposta l'insieme di credenziali hello, specificare gli elementi da tooreplicate, e in cui si desidera tooreplicate a.

Andare troppo[passaggio 6: configurare un insieme di credenziali](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>Passaggio 7: Configurare le impostazioni di origine e di destinazione

Configurare le impostazioni per l'origine hello e di destinazione del sito (Azure). Le impostazioni dell'origine include l'esecuzione del programma di installazione unificata tooinstall componenti Site Recovery di hello locali.

Andare troppo[passaggio 7: configurare hello origine e di destinazione](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>Passaggio 8: Configurare un criterio di replica

Impostare un criterio toospecify fisico come i server devono essere replicati.

Andare troppo[passaggio 8: impostare un criterio di replica](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>Passaggio 9: Installare il servizio di mobilità hello

servizio di mobilità Hello deve essere installato in ogni server desiderate tooreplicate. Esistono alcuni modi tooset servizio hello, con l'installazione push o pull.

Andare troppo[passaggio 9: installare il servizio Mobility hello](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>Passaggio 10: Abilitare la replica

Dopo che il servizio di mobilità hello è in esecuzione in un server, è possibile abilitare la replica. Dopo aver abilitato, viene eseguita la replica iniziale di VM hello.

Andare troppo[passaggio 10: abilitare la replica](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Passaggio 11: Eseguire un failover di test

Al termine della replica iniziale e la replica differenziale è in esecuzione, è possibile eseguire un toomake di failover di test che tutto funziona come previsto.

Andare troppo[passaggio 11: eseguire un failover di test](physical-walkthrough-test-failover.md)

