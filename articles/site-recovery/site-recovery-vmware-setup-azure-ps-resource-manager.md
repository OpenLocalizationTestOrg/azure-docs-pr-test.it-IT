---
title: " Gestire un server di elaborazione in esecuzione in Azure (Resource Manager) | Microsoft Docs"
description: Questo articolo descrive come tooset backup un failback processo server (gestione delle risorse) In Azure.
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Gestire un server di elaborazione in esecuzione in Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Gestione risorse](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Classica](./site-recovery-vmware-setup-azure-ps-classic.md)

Durante il failback, server process toodeploy in Azure è consigliabile se è presente una latenza elevata tra hello rete virtuale di Azure e la rete locale. Questo articolo descrive come è possibile impostare, configurare e gestire i server di elaborazione hello in esecuzione in Azure.

> [!NOTE]
> Questo articolo è toobe se è utilizzata **Gestione risorse** come modello di distribuzione hello per le macchine virtuali hello durante il failover. Se è stato utilizzato **classico** come modello di distribuzione hello, seguire i passaggi di hello in [come tooset a & configurare un server di elaborazione di Failback (versione classica)](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>Prerequisiti

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Distribuire un server di elaborazione in Azure
1. Nell'insieme di credenziali hello > **infrastruttura di Site Recovery** (sotto l'intestazione "Manage" hello) > **server di configurazione** (sotto l'intestazione "Per VMware e computer fisici"), selezionare il server di configurazione di hello.
2. Nella pagina di dettagli di configurazione Server hello visualizzata fare clic su "+ processo server"

  ![Raccolta per l'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  In hello **Aggiungi server di elaborazione** pagina, seleziona hello seguenti valori

  ![Elemento della raccolta per l'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**Nome campo**|**Valore**|
|-|-|
|Scegliere dove si vuole toodeploy il server di elaborazione|Selezionare il valore di hello **distribuire un server di elaborazione di failback in Azure** |
|Sottoscrizione|Selezionare la sottoscrizione di Azure in cui è stato eseguito il failover delle macchine virtuali hello hello|
|Gruppo di risorse|È possibile creare un gruppo di risorse di toodeploy questo server di elaborazione o scegliere i server di elaborazione toodeploy hello in un gruppo di risorse esistente|
|Percorso|Selezionare hello Azure Data Center in cui hello di macchine virtuali in cui è stato eseguito il failover in|
|Azure Network|Seleziona hello Network(VNet) virtuale di Azure che hello macchine virtuali in cui è stato eseguito il failover in. Se è stato eseguito il failover delle macchine virtuali in più reti virtuali di Azure, è necessario distribuire un server di elaborazione per ogni rete virtuale|

4. Compilare il resto di hello delle proprietà di hello del server di elaborazione hello

  ![Riepilogo dell'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**Nome campo**|**Valore**|
|-|-|
|Server Name|Nome visualizzato/nome host per la macchina virtuale del server di elaborazione|
| User Name|Un nome utente che diventa amministratore sulla macchina virtuale|
|Account di archiviazione|Nome dell'Account di archiviazione in cui viene inserito del disco virtuale della macchina virtuale hello hello|
|Subnet|subnet Hello della macchina virtuale di hello rete virtuale di Azure toowhich hello è connesso|
| Indirizzo IP|Indirizzo IP che si desidera hello processo server tooassume dopo l'avvio|
5. Fare clic su toostart pulsante OK hello hello processo macchina virtuale del server di distribuzione.

> [!NOTE]
> toouse in grado di toobe questo server di elaborazione per il failback, è necessario tooregister con server di configurazione di on-premise hello.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Registrazione hello processo server (in esecuzione in Azure) tooa Server di configurazione (in esecuzione in locale)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>L'aggiornamento di versione di toolatest hello processo server.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>L'annullamento della registrazione di server di elaborazione hello (in esecuzione in Azure) da un Server di configurazione (in esecuzione in locale)

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
