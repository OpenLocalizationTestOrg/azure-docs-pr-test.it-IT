---
title: "hello aaaInstall servizio di mobilità per la replica VMware tooAzure | Documenti Microsoft"
description: "In questo articolo viene descritto come tooinstall hello agente del servizio di mobilità per la replica tooAzure VMware con il servizio di Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>Passaggio 10: Installare il servizio di mobilità hello


In questo articolo viene descritto come le impostazioni di tooconfigure origine e di destinazione durante la replica locale tooAzure di macchine virtuali VMware, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

servizio di mobilità Hello acquisisce scritture di dati in un computer e li inoltra toohello server di elaborazione. È necessario installarlo in ogni computer che si desidera tooreplicate tooAzure.

È possibile eseguire l'installazione manuale del servizio di mobilità hello, un'installazione push dal server di elaborazione di Site Recovery hello quando è abilitata la replica o utilizzare uno strumento di System Center Configuration Manager. Se si utilizza l'installazione push, servizio hello viene installato nella macchina virtuale hello quando è abilitata la replica.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Eseguire l'installazione manuale

1. Controllare hello [prerequisiti](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) per l'installazione manuale.
2. Seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) per l'installazione manuale tramite il portale di hello.
3. Se si preferisce tooinstall dalla riga di comando hello, seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Installare dal server di elaborazione hello

Se si desidera l'installazione del servizio Mobility hello toopush dal server di elaborazione hello quando si abilita la replica per una macchina virtuale, è necessario un account che può essere utilizzato da hello processo server tooaccess hello macchina virtuale. account di Hello viene utilizzato solo per l'installazione push hello.

1. È necessario aver [creato un account](vmware-walkthrough-prepare-vmware.md) che possa essere usato per l'installazione push. È quindi possibile specificare account hello da toouse quando si configurano le impostazioni di origine durante la distribuzione di Site Recovery.
2. Seguire quindi [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se si desidera servizio di mobilità toopush hello in macchine virtuali in esecuzione Windows o Linux.

## <a name="other-methods"></a>Altri metodi

Altre informazioni, vedere [installazione del servizio di mobilità hello utilizzando Gestione configurazione](site-recovery-install-mobility-service-using-sccm.md), o tramite [Automation DSC per Azure](site-recovery-automate-mobility-service-install.md).

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 11: abilitare la replica](vmware-walkthrough-enable-replication.md)
