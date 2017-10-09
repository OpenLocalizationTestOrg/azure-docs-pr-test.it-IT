---
title: Preparazione di destinazione (tooAzure fisico) | Documenti Microsoft
description: Questo articolo viene descritto come tooprepare toostart l'ambiente Azure la replica di server fisici che eseguono tooAzure Windows o Linux.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Preparazione di destinazione (tooAzure VMware)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [TooAzure fisico](./site-recovery-prepare-target-physical-to-azure.md)

Questo articolo viene descritto come tooprepare toostart l'ambiente Azure la replica di server fisici (x64) in esecuzione Windows o Linux in Azure.

## <a name="prerequisites"></a>Prerequisiti

Hello presume seguente hello:
- È stato creato un archivio di servizi di ripristino di tooprotect i server fisici. È possibile creare un insieme di credenziali di servizi di ripristino da hello [portale di Azure](http://portal.azure.com "portale di Azure").
- Hai [configurare l'ambiente locale](./site-recovery-set-up-physical-to-azure.md) tooreplicate tooAzure di server fisici.

## <a name="prepare-target"></a>Preparare la destinazione

Dopo aver completato hello **obiettivi della protezione dati passaggio 1: selezionare** e **passaggio 2: preparare origine**, si passa troppo**passaggio 3: destinazione**

![Preparare la destinazione](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. **Sottoscrizione:** da hello menu a discesa, seleziona hello sottoscrizione che si desidera tooreplicate i server fisici.
2. **Modello di distribuzione:** modello di distribuzione selezionare hello (versione classica o Gestione risorse)

In base al modello di distribuzione scelto hello, una convalida viene eseguita tooensure che occorre almeno un account di archiviazione compatibile e la rete virtuale in tooreplicate sottoscrizione di destinazione hello e il failover dei server fisici per.

Una volta completate le convalide hello, fare clic su OK toogo toohello successivo passaggio.

Se si non dispone di un account di archiviazione compatibile di gestione delle risorse o una rete virtuale o si desidera tooadd altre, è possibile farlo facendo hello **+ Account di archiviazione** o **+ rete** pulsanti nella parte superiore di hello di hello pannello.

## <a name="next-steps"></a>Passaggi successivi
[Configurare le impostazioni di replica](./site-recovery-setup-replication-settings-vmware.md).
