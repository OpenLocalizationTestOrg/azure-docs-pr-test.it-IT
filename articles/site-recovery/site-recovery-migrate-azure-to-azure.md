---
title: aaaMigrate le macchine virtuali IaaS di Azure tra le aree di Azure | Documenti Microsoft
description: Utilizzare macchine virtuali di Azure Site Recovery toomigrate IaaS di Azure da un'area di Azure tooanother.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Eseguire la migrazione delle macchine virtuali IaaS di Azure tra aree di Azure con Azure Site Recovery
## <a name="overview"></a>Panoramica
Benvenuti tooAzure Site Recovery. Se si desidera toomigrate macchine virtuali di Azure tra le aree di Azure, usare questo articolo. Prima di iniziare, tenere presente quanto segue:

* Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Azure Resource Manager e la distribuzione classica. Azure offre inoltre due portali: hello portale di Azure classico che supporta il modello di distribuzione classica hello e hello portale di Azure con il supporto per entrambi i modelli di distribuzione. passaggi di base Hello per la migrazione sono hello stesso se si sta configurando il ripristino del sito di gestione risorse o classica. Tuttavia hello istruzioni dell'interfaccia utente e le schermate contenute in questo articolo sono rilevanti per hello portale di Azure.
* **Attualmente è possibile migrare solo da un'area tooanother. È possibile eseguire il failover le macchine virtuali da un'area di Azure tooanother, ma non è possibile eseguire tali torna nuovamente.**

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Prerequisiti
Per la distribuzione è necessario quanto segue:

* **Macchine virtuali IaaS**: hello macchine virtuali che si desidera toomigrate. Nella migrazione queste VM vengono considerate macchine fisiche.

## <a name="deployment-steps"></a>Passaggi di distribuzione
Questa sezione descrive i passaggi di distribuzione hello nel nuovo portale di Azure hello.

1. [Creare un insieme di credenziali](site-recovery-vmware-to-azure.md).
2. [Abilitare la replica](site-recovery-vmware-to-azure.md). Abilitare la replica per le macchine virtuali toomigrate desiderato e scegliere Azure come origine hello. 
3. [ Eseguire un failover non pianificato](site-recovery-failover.md). Una volta completata la replica iniziale, è possibile eseguire un failover non pianificato da tooanother di una regione di Azure. Facoltativamente, è possibile creare un piano di ripristino ed eseguire un failover non pianificato, toomigrate più macchine virtuali tra aree. [Ulteriori informazioni](site-recovery-create-recovery-plans.md) sui piani di ripristino.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sui vari scenari di replica, vedere [Che cos'è Site Recovery?](site-recovery-overview.md)
