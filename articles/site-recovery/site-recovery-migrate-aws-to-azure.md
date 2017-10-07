---
title: aaaMigrate macchine virtuali da AWS tooAzure | Documenti Microsoft
description: In questo articolo viene descritto come toomigrate virtuale dei computer in esecuzione in tooAzure Amazon Web Services (AWS) usando Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Eseguire la migrazione di macchine virtuali in tooAzure Amazon Web Services (AWS) con Azure Site Recovery

In questo articolo viene descritto come toomigrate Windows AWS istanze tooAzure le macchine virtuali con hello [Azure Site Recovery](site-recovery-overview.md) servizio.

La migrazione è in realtà un failover da AWS tooAzure. Non è possibile eseguire il failback macchine tooAWS e non vi è alcuna replica in corso. In questo articolo vengono descritti i passaggi hello per la migrazione in hello portale di Azure e sono basati su istruzioni hello per [la replica di un computer fisico di tooAzure](site-recovery-vmware-to-azure.md).

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Sistemi operativi supportati

Il ripristino del sito può essere utilizzato toomigrate EC2 istanze in esecuzione uno dei seguenti sistemi operativi hello:

- Windows (solo versione a 64 bit)
    - Windows Server 2008 R2 SP1+ (solo driver Citrix PV o driver AWS PV: **le istanze con driver RedHat PV non sono supportate**) Windows Server 2012 Windows Server 2012 R2
- Linux (solo versione a 64 bit)
    - Red Hat Enterprise Linux 6.7 (solo per istanze HVM virtualizzate)

## <a name="prerequisites"></a>Prerequisiti

Per la distribuzione è necessario quanto segue:

* **Server di configurazione**: una macchina virtuale di EC2 Amazon che esegue Windows Server 2012 R2 viene distribuito come server di configurazione hello. Per impostazione predefinita, hello altri componenti di Azure Site Recovery (server di elaborazione e il server di destinazione master) vengono installati quando si distribuisce il server di configurazione hello. In questo articolo vengono descritti i passaggi hello per la migrazione in hello portale di Azure e sono basati su istruzioni hello per [maggiori informazioni](site-recovery-components.md)

* **Le istanze di EC2**: hello Amazon EC2 le istanze di macchine virtuali che si desidera toomigrate.

## <a name="deployment-steps"></a>Passaggi di distribuzione

1. Creare un insieme di credenziali dei servizi di ripristino.
2. Gruppo di sicurezza delle istanze EC2 Hello deve disporre di regole configurate tooallow comunicazione tra l'istanza di EC2 hello che si desidera toomigrate e hello istanza su cui si prevede di toodeploy hello del Server di configurazione.

3. In hello stesso Amazon di Cloud privato virtuale come le istanze di EC2, distribuire un server di configurazione di ripristino automatico di sistema. Fare riferimento hello VMware / fisici tooAzure prerequisiti per i requisiti di distribuzione server di configurazione.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Dopo che il server di configurazione è distribuito in AWS e registrato con l'insieme di credenziali di servizi di ripristino, verrà visualizzato il server di configurazione di hello e server di elaborazione in dell'infrastruttura di Site Recovery come illustrato di seguito:

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Dopo aver distribuito il server di configurazione di hello (operazione può richiedere per tale too15 minustes tooappear), convalidare in grado di comunicare con le macchine virtuali hello che si desidera toomigrate.

6. [Configurare le impostazioni di replica](site-recovery-setup-replication-settings-vmware.md).

7. Abilitare la replica: abilitare la replica per le macchine virtuali desiderate toomigrate hello. È possibile individuare le istanze di EC2 hello utilizzando indirizzi IP privati hello, che è possibile ottenere dalla console EC2 hello.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Dopo che sono stati protetti istanze hello EC2 e hello tooAzure di replica è stata completata, [eseguire un Failover di Test](site-recovery-test-failover-to-azure.md) toovalidate le prestazioni dell'applicazione in Azure.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Eseguire un Failover da AWS tooAzure per ogni macchina virtuale. Facoltativamente, è possibile creare un piano di ripristino ed eseguire un Failover, toomigrate più macchine virtuali da AWS tooAzure. [Ulteriori informazioni](site-recovery-create-recovery-plans.md) sui piani di ripristino.

10. Per la migrazione, non è necessario toocommit un failover. Invece si seleziona l'opzione di completare la migrazione di hello per ogni computer si desidera toomigrate. Hello azione di completare la migrazione termina il processo di migrazione hello, rimuove la replica per macchina hello e interrompe il ripristino del sito per la macchina hello di fatturazione.

    ![Migrazione](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Passaggi successivi

- [Preparare la migrazione di macchine tooenable replica](site-recovery-azure-to-azure-after-migration.md) tooanother area per esigenze di ripristino di emergenza.
- Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md).
