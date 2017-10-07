---
title: Configurare un ambiente di origine hello (VMware tooAzure) | Documenti Microsoft
description: In questo articolo viene descritto come tooset backup il toostart ambiente locale la replica VMware virtual macchine tooAzure.
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Configurare un ambiente di origine hello (tooAzure VMware)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure fisico](./site-recovery-set-up-physical-to-azure.md)

In questo articolo viene descritto come tooset backup il toostart ambiente locale replica virtuale dei computer in esecuzione su VMware tooAzure.

## <a name="prerequisites"></a>Prerequisiti

Hello si presume che sia già stato creato:
- Un archivio di servizi di ripristino in hello [portale di Azure](http://portal.azure.com "portale di Azure").
- Account dedicato in VMware vCenter che può essere usato per l'[individuazione automatica](./site-recovery-vmware-to-azure.md).
- Una macchina virtuale nel server di configurazione che tooinstall hello.

## <a name="configuration-server-minimum-requirements"></a>Requisiti minimi per il server di configurazione
software server di configurazione Hello deve essere distribuiti in una macchina virtuale di VMware a disponibilità elevata. Hello nella tabella seguente sono elencati i requisiti hardware minimi hello, software e requisiti di rete per un server di configurazione.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Server proxy basato su HTTPS non sono supportati dal server di configurazione hello.

## <a name="choose-your-protection-goals"></a>Scegliere gli obiettivi della protezione

1. Nel portale di Azure hello, passare toohello **servizi di ripristino** pannello dell'insieme di credenziali e selezionare l'insieme di credenziali.
2. Menu hello risorsa dell'insieme di credenziali hello andare troppo**Introduzione** > **Site Recovery** > **passaggio 1: preparare l'infrastruttura**  >  **Obiettivi della protezione dati**.

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. In **obiettivi della protezione dati**selezionare **tooAzure**e scegliere **Sì, con VMware vSphere Hypervisor**. Fare quindi clic su **OK**.

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello
L'impostazione di ambiente di origine hello comporta due attività principali:

- Installare e registrare un server di configurazione con Site Recovery.
- Individuare le macchine virtuali in locale tramite la connessione a Site Recovery tooyour locale VMware vCenter o vSphere EXSi host.

### <a name="step-1-install-and-register-a-configuration-server"></a>Passaggio 1: Installare e registrare un server di configurazione

1. Fare clic su **Passaggio 1: Preparare l'infrastruttura** > **Origine**. In **origine Prepare**, se non è un server di configurazione, fare clic su **+ server di configurazione** tooadd uno.

    ![Impostare l'origine](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. In hello **Aggiungi Server** pannello, verificare che **Server di configurazione** viene visualizzato **tipo Server**.
4. Scaricare i file di installazione di hello installazione unificata di Site Recovery.
5. Scaricare la chiave di registrazione dell'insieme di credenziali di hello. Chiave di registrazione hello è necessario quando si esegue il programma di installazione unificata. chiave di Hello è valida per cinque giorni dopo la generazione è.

    ![Impostare l'origine](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. Nel computer in uso come server di configurazione hello hello eseguire **installazione unificata di Azure Site Recovery** tooinstall hello configurazione server, server process hello e master hello server di destinazione.

#### <a name="run-azure-site-recovery-unified-setup"></a>Eseguire l'Installazione unificata di Azure Site Recovery

> [!TIP]
> Registrazione del server di configurazione non riesce se il tempo di hello clock di sistema del computer è diverso dall'ora locale da più di cinque minuti. Sincronizzare l'orologio di sistema con un [Server ora](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) prima di avviare l'installazione di hello.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> il server di configurazione di Hello può essere installato tramite riga di comando. Per ulteriori informazioni, vedere [installare server di configurazione di hello utilizzando gli strumenti da riga di comando](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Aggiungere hello VMware account per l'individuazione automatica

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>Passaggio 2 - Aggiungere un vCenter
macchine virtuali toodiscover Azure Site Recovery tooallow in esecuzione nell'ambiente locale, è necessario tooconnect il Server VMware vCenter o l'host ESXi vSphere con il ripristino del sito.

Selezionare **+ vCenter** toostart la connessione a un server VMware vCenter o un host VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Problemi comuni
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Passaggi successivi
[Configurare l'ambiente di destinazione](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.
