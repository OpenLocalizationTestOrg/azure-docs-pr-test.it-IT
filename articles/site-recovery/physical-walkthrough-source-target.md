---
title: aaaSet backup hello origine e di destinazione per i server fisici replica tooAzure con Azure Site Recovery | Documenti Microsoft
description: Riepiloga hello passaggi tooset le impostazioni di origine e di destinazione per la replica di archiviazione di server fisici tooAzure con hello servizio Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>Passaggio 7: Configurare hello origine e di destinazione per tooAzure replica server fisico

In questo articolo viene descritto come le impostazioni di tooconfigure origine e di destinazione durante la replica locale tooAzure server fisici, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Configurare il server di configurazione di hello, registrarla nell'insieme di credenziali hello e individuare i computer.

1. Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Origine**.
2. Se non è disponibile un server di configurazione, fare clic su **+Server di configurazione**.
3. In **Aggiungi server** verificare che **Tipo di server** contenga **Server di configurazione**.
4. Scaricare i file di installazione di hello installazione unificata di Site Recovery.
5. Scaricare la chiave di registrazione dell'insieme di credenziali di hello. che sarà necessaria quando si esegue l'Installazione unificata. chiave di Hello è valida per cinque giorni dopo la generazione è.

   ![Impostare l'origine](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Registrare il server di configurazione di hello nell'insieme di credenziali hello

Seguito hello prima di avviare, quindi eseguire il programma di installazione unificata tooinstall hello configurazione server, il server di elaborazione hello e il server di destinazione master hello. Hello video viene illustrata l'impostazione per i componenti per la replica VMware VM tooAzure hello. Tuttavia, hello stesso processo è valido per la replica tooAzure server fisico.

- Nel server di configurazione hello VM, verificare che l'orologio di sistema hello è sincronizzato con un [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deve corrispondere. Se è avanti o indietro di 15 minuti, l'installazione potrebbe avere esito negativo.
- Eseguire l'installazione come amministratore locale nel computer server di configurazione hello.
- Assicurarsi che sia abilitato TLS 1.0 su hello macchina virtuale.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> può anche essere installato il server di configurazione di Hello [dalla riga di comando hello](http://aka.ms/installconfigsrv).




## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello

Prima configurare un ambiente di destinazione hello, verificare di che disporre di un account di archiviazione di Azure e una configurazione di rete virtuale.

1. Fare clic su **Prepare infrastruttura** > **destinazione**, e selezionare hello sottoscrizione di Azure da toouse.
2. Specificare se per la destinazione deve essere usato il modello di distribuzione classica o Resource Manager.
3. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.

   ![Destinazione](./media/physical-walkthrough-source-target/gs-target.png)

4. Se è stata creata una rete o un account di archiviazione, fare clic su **+ account di archiviazione** o **+ rete**, toocreate un inline di account o rete di gestione risorse.

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 8: impostare un criterio di replica](physical-walkthrough-replication.md)
