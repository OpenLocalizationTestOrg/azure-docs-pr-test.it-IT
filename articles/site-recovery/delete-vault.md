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
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="a8859-103">Eliminare un insieme di credenziali di Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a8859-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="a8859-104">Le dipendenze possono impedire l'eliminazione di un insieme di credenziali di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a8859-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="a8859-105">Hello azioni è necessario tootake variano in base uno scenario di ripristino del sito hello: tooAzure VMware, tooAzure Hyper-V (con e senza System Center Virtual Machine Manager) e Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8859-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="a8859-106">toodelete un insieme di credenziali usato nel Backup di Azure, vedere [eliminare un insieme di credenziali di Backup in Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="a8859-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="a8859-107">Se si sta testando prodotto hello e non sono interessati alla perdita di dati, utilizzare hello forza eliminazione metodo toorapidly rimuovere insieme di credenziali hello e tutte le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a8859-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="a8859-108">comando di PowerShell Hello Elimina tutto il contenuto dell'insieme di credenziali hello hello e non è reversibile.</span><span class="sxs-lookup"><span data-stu-id="a8859-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="a8859-109">Utilizzare PowerShell tooforce Elimina insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="a8859-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="a8859-110">hello toodelete insieme di credenziali di Site Recovery anche se sono presenti elementi protetti, utilizzare i seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a8859-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="a8859-111">Eliminare un insieme di credenziali di Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a8859-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="a8859-112">insieme di credenziali hello toodelete hello seguire i passaggi per lo scenario consigliato.</span><span class="sxs-lookup"><span data-stu-id="a8859-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="a8859-113">Le macchine virtuali VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="a8859-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="a8859-114">Elimina tutti protetti macchine virtuali seguendo procedure hello [disabilitare la protezione per un VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="a8859-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="a8859-115">Eliminare tutti i criteri di replica seguendo procedure hello [Elimina un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="a8859-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="a8859-116">Eliminare i riferimenti toovCenter da hello seguente passaggi [eliminare vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="a8859-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="a8859-117">Eliminare il server di configurazione hello seguendo procedure hello [rimuovere le autorizzazioni di un server di configurazione](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="a8859-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="a8859-118">Eliminare l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="a8859-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="a8859-119">Macchine virtuali Hyper-V (con Virtual Machine Manager) tooAzure</span><span class="sxs-lookup"><span data-stu-id="a8859-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="a8859-120">Elimina tutti protetti macchine virtuali seguendo procedure hello [disabilitare la protezione per un server fisico o di VMware VM](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="a8859-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="a8859-121">Eliminare tutti i criteri di replica seguendo procedure hello [Elimina un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="a8859-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="a8859-122">Delete fa riferimento a tooVirtual Machine Manager server seguendo i passaggi di hello in [annullare la registrazione di un server VMM connesso](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="a8859-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="a8859-123">Eliminare l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="a8859-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="a8859-124">Macchine virtuali Hyper-V (senza Virtual Machine Manager) tooAzure</span><span class="sxs-lookup"><span data-stu-id="a8859-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="a8859-125">Elimina tutti protetti macchine virtuali seguendo procedure hello [disabilitare la protezione per un server fisico o di VMware VM](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="a8859-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="a8859-126">Eliminare tutti i criteri di replica seguendo procedure hello [Elimina un criterio di replica](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="a8859-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="a8859-127">Delete fa riferimento a server-V tooHyper seguendo procedure hello [annullare la registrazione di un host Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="a8859-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="a8859-128">Eliminare il sito hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a8859-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="a8859-129">Eliminare l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="a8859-129">Delete hello vault.</span></span>
