---
title: aaaDelete un insieme di credenziali di Site Recovery
description: Informazioni su come toodelete un insieme di credenziali di Azure Site Recovery, basate su scenario di ripristino del sito hello.
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a>Eliminare un insieme di credenziali di Site Recovery
Le dipendenze possono impedire l'eliminazione di un insieme di credenziali di Azure Site Recovery. Hello azioni è necessario tootake variano in base uno scenario di ripristino del sito hello: tooAzure VMware, tooAzure Hyper-V (con e senza System Center Virtual Machine Manager) e Backup di Azure. toodelete un insieme di credenziali usato nel Backup di Azure, vedere [eliminare un insieme di credenziali di Backup in Azure](../backup/backup-azure-delete-vault.md).

>[!Important]
>Se si sta testando prodotto hello e non sono interessati alla perdita di dati, utilizzare hello forza eliminazione metodo toorapidly rimuovere insieme di credenziali hello e tutte le relative dipendenze.

> comando di PowerShell Hello Elimina tutto il contenuto dell'insieme di credenziali hello hello e non è reversibile.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>Utilizzare PowerShell tooforce Elimina insieme di credenziali hello 

hello toodelete insieme di credenziali di Site Recovery anche se sono presenti elementi protetti, utilizzare i seguenti comandi:

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Eliminare un insieme di credenziali di Site Recovery 
insieme di credenziali hello toodelete hello seguire i passaggi per lo scenario consigliato.

### <a name="vmware-vms-tooazure"></a>Le macchine virtuali VMware tooAzure

1. Elimina tutti protetti macchine virtuali seguendo procedure hello [disabilitare la protezione per un VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Eliminare tutti i criteri di replica seguendo procedure hello [Elimina un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Eliminare i riferimenti toovCenter da hello seguente passaggi [eliminare vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Eliminare il server di configurazione hello seguendo procedure hello [rimuovere le autorizzazioni di un server di configurazione](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Eliminare l'insieme di credenziali hello.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>Macchine virtuali Hyper-V (con Virtual Machine Manager) tooAzure
1. Elimina tutti protetti macchine virtuali seguendo procedure hello [disabilitare la protezione per un server fisico o di VMware VM](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Eliminare tutti i criteri di replica seguendo procedure hello [Elimina un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  Delete fa riferimento a tooVirtual Machine Manager server seguendo i passaggi di hello in [annullare la registrazione di un server VMM connesso](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Eliminare l'insieme di credenziali hello.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>Macchine virtuali Hyper-V (senza Virtual Machine Manager) tooAzure
1. Elimina tutti protetti macchine virtuali seguendo procedure hello [disabilitare la protezione per un server fisico o di VMware VM](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Eliminare tutti i criteri di replica seguendo procedure hello [Elimina un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Delete fa riferimento a server-V tooHyper seguendo procedure hello [annullare la registrazione di un host Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Eliminare il sito hello Hyper-V.

5. Eliminare l'insieme di credenziali hello.
