---
title: Eliminare un insieme di credenziali di Site Recovery
description: Informazioni su come eliminare un insieme di credenziali di Azure Site Recovery, in base allo scenario di Site Recovery.
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
ms.openlocfilehash: b95b9defa0a037f7d7d3ef36b99bc7c53c751050
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="ba0b3-103">Eliminare un insieme di credenziali di Site Recovery</span><span class="sxs-lookup"><span data-stu-id="ba0b3-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="ba0b3-104">Le dipendenze possono impedire l'eliminazione di un insieme di credenziali di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="ba0b3-105">Le azioni da eseguire variano in base allo scenario di Site Recovery: VMware in Azure, Hyper-V (con e senza System Center Virtual Machine Manager) in Azure e Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-105">The actions you need to take vary based on the Site Recovery scenario: VMware to Azure, Hyper-V (with and without System Center Virtual Machine Manager) to Azure, and Azure Backup.</span></span> <span data-ttu-id="ba0b3-106">Per eliminare un insieme di credenziali usato in Backup di Azure, vedere [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md) (Eliminare un insieme di credenziali di Backup in Azure).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-106">To delete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="ba0b3-107">Se si esegue il test del prodotto e non si hanno problemi di perdita di dati, usare il metodo di eliminazione forzata per rimuovere rapidamente l'insieme di credenziali e tutte le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-107">If you're testing the product and aren't concerned about data loss, use the force delete method to rapidly remove the vault and all its dependencies.</span></span>

> <span data-ttu-id="ba0b3-108">Il comando di PowerShell elimina tutti i contenuti dell'insieme di credenziali e non è reversibile.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-108">The PowerShell command deletes all the contents of the vault and is not reversible.</span></span>

## <a name="use-powershell-to-force-delete-the-vault"></a><span data-ttu-id="ba0b3-109">Usare PowerShell per forzare l'eliminazione dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="ba0b3-109">Use PowerShell to force delete the vault</span></span> 

<span data-ttu-id="ba0b3-110">Per eliminare l'insieme di credenziali di Site Recovery anche se sono presenti elementi protetti, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba0b3-110">To delete the Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="ba0b3-111">Eliminare un insieme di credenziali di Site Recovery</span><span class="sxs-lookup"><span data-stu-id="ba0b3-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="ba0b3-112">Per eliminare l'insieme di credenziali, seguire la procedura consigliata per lo scenario.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-112">To delete the vault, follow the recommended steps for your scenario.</span></span>

### <a name="vmware-vms-to-azure"></a><span data-ttu-id="ba0b3-113">Da VM VMware ad Azure</span><span class="sxs-lookup"><span data-stu-id="ba0b3-113">VMware VMs to Azure</span></span>

1. <span data-ttu-id="ba0b3-114">Eliminare tutte le macchine virtuali protette seguendo la procedura descritta in [Disabilitare la protezione per una VM VMware o un server fisico](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-114">Delete all protected VMs by following the steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="ba0b3-115">Eliminare tutti i criteri di replica seguendo la procedura descritta in [Eliminare un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-115">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="ba0b3-116">Eliminare i riferimenti a vCenter seguendo la procedura descritta in [Eliminare un server vCenter in Azure Site Recovery](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-116">Delete references to vCenter by following the steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="ba0b3-117">Eliminare il server di configurazione seguendo la procedura descritta in [Rimozione delle autorizzazioni per un server di configurazione](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-117">Delete the configuration server by following the steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="ba0b3-118">Eliminare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-118">Delete the vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-to-azure"></a><span data-ttu-id="ba0b3-119">Macchine virtuali Hyper-V (con Virtual Machine Manager) in Azure</span><span class="sxs-lookup"><span data-stu-id="ba0b3-119">Hyper-V VMs (with Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="ba0b3-120">Eliminare tutte le macchine virtuali protette seguendo la procedura descritta in [Disabilitare la protezione per una VM VMware o un server fisico](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-120">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="ba0b3-121">Eliminare tutti i criteri di replica seguendo la procedura descritta in [Eliminare un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-121">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="ba0b3-122">Eliminare i riferimenti ai server Virtual Machine Manager seguendo la procedura descritta in [Annullare la registrazione di un server VMM connesso](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-122">Delete references to Virtual Machine Manager servers by following the steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="ba0b3-123">Eliminare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-123">Delete the vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-to-azure"></a><span data-ttu-id="ba0b3-124">Macchine virtuali Hyper-V (senza Virtual Machine Manager) in Azure</span><span class="sxs-lookup"><span data-stu-id="ba0b3-124">Hyper-V VMs (without Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="ba0b3-125">Eliminare tutte le macchine virtuali protette seguendo la procedura descritta in [Disabilitare la protezione per una VM VMware o un server fisico](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-125">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="ba0b3-126">Eliminare tutti i criteri di replica seguendo la procedura descritta in [Eliminare un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-126">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="ba0b3-127">Eliminare i riferimenti ai server Hyper-V seguendo la procedura descritta in [Annullare la registrazione di un host Hyper-V in un sito di Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="ba0b3-127">Delete references to Hyper-V servers by following the steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="ba0b3-128">Eliminare il sito Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-128">Delete the Hyper-V site.</span></span>

5. <span data-ttu-id="ba0b3-129">Eliminare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ba0b3-129">Delete the vault.</span></span>
