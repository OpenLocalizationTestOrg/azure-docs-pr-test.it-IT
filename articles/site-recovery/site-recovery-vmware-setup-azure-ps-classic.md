---
title: " Gestire un server di elaborazione in esecuzione in Azure (versione classica) | Microsoft Docs"
description: Questo articolo viene descritto come tooset di un processo Server(Classic) In Azure il failback.
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>Gestire un server di elaborazione in esecuzione in Azure (versione classica)
> [!div class="op_single_selector"]
> * [Azure versione classica](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Gestione risorse](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

Durante il failback, è consigliabile toodeploy Server di elaborazione in Azure se è presente una latenza elevata tra hello rete virtuale di Azure e la rete locale. Questo articolo descrive come è possibile impostare, configurare e gestire i server di elaborazione hello in esecuzione in Azure.

> [!NOTE]
> Questo articolo è toobe se classica è utilizzata come modello di distribuzione hello per le macchine virtuali hello durante il failover. Se utilizzato Gestione risorse come passaggi di distribuzione modello seguire hello in hello [come tooset a & configurare un Server di elaborazione di Failback (gestione delle risorse)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Prerequisiti

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Distribuire un server di elaborazione in Azure

1. In Azure Marketplace, creare una macchina virtuale utilizzando hello **Microsoft Azure Site Recovery processo Server V2** </br>
    ![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. Assicurarsi di selezionare il modello di distribuzione hello come **classico** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. Nella procedura guidata di hello crea macchina virtuale > Impostazioni di base, assicurarsi di selezionare hello toowhere sottoscrizione e il percorso è stato eseguito il failover delle macchine virtuali hello.</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Verificare che la macchina virtuale hello sia connesso hello toowhich di rete virtuale di Azure toohello failover macchina virtuale è connessa.</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Una volta provisioning hello Server di elaborazione della macchina virtuale, è necessario toolog in e registrarlo con hello del Server di configurazione.

> [!NOTE]
> toouse in grado di toobe questo Server di elaborazione per il failback, è necessario tooregister con server di configurazione di on-premise hello.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Registrazione hello processo Server (in esecuzione in Azure) tooa Server di configurazione (in esecuzione in locale)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>L'aggiornamento di versione di toolatest hello Server di elaborazione.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Annullamento della registrazione hello processo Server (in esecuzione in Azure) da un Server di configurazione (in esecuzione in locale)

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
