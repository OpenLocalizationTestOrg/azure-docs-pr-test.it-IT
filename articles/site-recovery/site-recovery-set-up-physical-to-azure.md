---
title: Configurare un ambiente di origine hello (tooAzure server fisici) | Documenti Microsoft
description: Questo articolo viene descritto come tooset backup il toostart ambiente locale la replica di server fisici che eseguono Windows o Linux in Azure.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Configurare un ambiente di origine hello (server fisico tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure fisico](./site-recovery-set-up-physical-to-azure.md)

Questo articolo viene descritto come tooset backup il toostart ambiente locale la replica di server fisici che eseguono Windows o Linux in Azure.

## <a name="prerequisites"></a>Prerequisiti

articolo Hello si presuppone che esista già:
1. Un insieme di credenziali di servizi di ripristino in hello [portale di Azure](http://portal.azure.com "portale di Azure").
3. Un computer fisico nel quale server di configurazione tooinstall hello.

### <a name="configuration-server-minimum-requirements"></a>Requisiti minimi per il server di configurazione
Hello nella tabella seguente sono elencati i requisiti hardware minimi hello, software e requisiti di rete per un server di configurazione.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Server proxy basato su HTTPS non sono supportati dal server di configurazione hello.

## <a name="choose-your-protection-goals"></a>Scegliere gli obiettivi della protezione

1. Nel portale di Azure hello, passare toohello **servizi di ripristino** insiemi di credenziali di blade e selezionare l'insieme di credenziali.
2. In hello **risorse** menu dell'insieme di credenziali di hello, fare clic su **Introduzione** > **Site Recovery** > **passaggio 1: preparare Infrastruttura** > **obiettivi della protezione dati**.

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. In **obiettivi della protezione dati**selezionare **tooAzure** e **non virtualizzato/altri**, quindi fare clic su **OK**.

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

1. In **origine Prepare**, se non è un server di configurazione, fare clic su **+ server di configurazione** tooadd uno.

  ![Impostare l'origine](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. In hello **Aggiungi Server** pannello, verificare che **Server di configurazione** viene visualizzato **tipo Server**.
4. Scaricare i file di installazione di hello installazione unificata di Site Recovery.
5. Scaricare la chiave di registrazione dell'insieme di credenziali di hello. Chiave di registrazione hello è necessario quando si esegue il programma di installazione unificata. chiave di Hello è valida per cinque giorni dopo la generazione è.

    ![Impostare l'origine](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. Nel computer in uso come server di configurazione hello hello eseguire **installazione unificata di Azure Site Recovery** tooinstall hello configurazione server, server process hello e master hello server di destinazione.

#### <a name="run-azure-site-recovery-unified-setup"></a>Eseguire l'Installazione unificata di Azure Site Recovery

> [!TIP]
> Registrazione del server di configurazione non riesce se il tempo di hello clock di sistema del computer più di cinque minuti dall'ora locale. Sincronizzare l'orologio di sistema con un [server ora](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) prima di avviare l'installazione di hello.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> il server di configurazione di Hello può essere installato tramite una riga di comando. Per altre informazioni, vedere l'argomento relativo all'[installazione del server di configurazione con gli strumenti da riga di comando](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Problemi comuni

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Passaggi successivi

Nel prossimo passaggio viene eseguita la [configurazione dell'ambiente di destinazione](./site-recovery-prepare-target-physical-to-azure.md) in Azure.
