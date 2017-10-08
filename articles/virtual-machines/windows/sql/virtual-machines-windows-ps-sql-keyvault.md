---
title: aaaIntegrate insieme di credenziali di chiave con SQL Server in macchine virtuali di Windows in Azure (gestione delle risorse) | Documenti Microsoft
description: Informazioni su come tooautomate hello configurazione di crittografia di SQL Server per l'utilizzo con l'insieme di credenziali chiave di Azure. In questo argomento viene illustrato come toouse integrazione dell'insieme di credenziali chiave di Azure con le macchine virtuali di SQL Server creato con Gestione risorse.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="d4e24-104">Configurare l'integrazione di Azure Key Vault per SQL Server in macchine virtuali di Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="d4e24-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4e24-105">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="d4e24-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="d4e24-106">Classico</span><span class="sxs-lookup"><span data-stu-id="d4e24-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d4e24-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d4e24-107">Overview</span></span>
<span data-ttu-id="d4e24-108">Esistono più funzionalità di crittografia di SQL Server, ad esempio [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [crittografia a livello di colonna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) e [crittografia di backup](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4e24-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="d4e24-109">I moduli di crittografia occorre toomanage e archiviano le chiavi di crittografia hello che è utilizzare per la crittografia.</span><span class="sxs-lookup"><span data-stu-id="d4e24-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="d4e24-110">Hello servizio insieme di credenziali chiave di Azure (insieme) è progettata tooimprove hello sicurezza e la gestione di queste chiavi in una posizione sicura e altamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="d4e24-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="d4e24-111">Hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) consente di SQL Server toouse queste chiavi dall'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4e24-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="d4e24-112">Se si esegue SQL Server locale dei computer, vi sono [è possibile attenersi alla procedura tooaccess insieme credenziali chiavi Azure dal computer di SQL Server on-premise](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4e24-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="d4e24-113">Ma per SQL Server in macchine virtuali di Azure, è possibile risparmiare tempo utilizzando hello *integrazione dell'insieme di credenziali chiave di Azure* funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d4e24-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="d4e24-114">Quando questa funzionalità è abilitata, automaticamente installa hello connettore SQL Server, configura hello EKM provider tooaccess insieme credenziali chiavi Azure e crea hello credenziali tooallow si tooaccess l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d4e24-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="d4e24-115">Se è stato esaminato passaggi hello hello indicato in precedenza documentazione locale, è possibile vedere che questa funzionalità consente di automatizzare i passaggi 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="d4e24-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="d4e24-116">Hello è comunque necessario toodo manualmente è chiavi e l'insieme di credenziali chiave hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d4e24-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="d4e24-117">Da qui, hello intero il programma di installazione della VM SQL è automatizzato.</span><span class="sxs-lookup"><span data-stu-id="d4e24-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="d4e24-118">Quando questa funzionalità viene completato il programma di installazione, è possibile eseguire toobegin istruzioni T-SQL la crittografia del database o backup in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="d4e24-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="d4e24-119">Abilitazione e configurazione dell'integrazione di AKV</span><span class="sxs-lookup"><span data-stu-id="d4e24-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="d4e24-120">È possibile abilitare l'integrazione di AKV durante il provisioning oppure configurarlo per VM esistenti.</span><span class="sxs-lookup"><span data-stu-id="d4e24-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="d4e24-121">Nuove VM</span><span class="sxs-lookup"><span data-stu-id="d4e24-121">New VMs</span></span>
<span data-ttu-id="d4e24-122">Se si esegue il provisioning di una nuova macchina virtuale con Gestione risorse di SQL Server, hello portale di Azure fornisce un tooenable passaggio integrazione insieme credenziali chiavi Azure.</span><span class="sxs-lookup"><span data-stu-id="d4e24-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="d4e24-123">Hello insieme credenziali chiavi Azure funzionalità è disponibile solo per hello Enterprise, Developer ed Evaluation Edition di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4e24-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Integrazione dell'insieme di credenziali delle chiavi di Azure per SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="d4e24-125">Per una procedura dettagliata di provisioning, vedere [il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="d4e24-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="d4e24-126">VM esistenti</span><span class="sxs-lookup"><span data-stu-id="d4e24-126">Existing VMs</span></span>
<span data-ttu-id="d4e24-127">Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4e24-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="d4e24-128">Selezionare quindi hello **configurazione di SQL Server** sezione di hello **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="d4e24-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Integrazione di AKV SQL per le VM esistenti](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="d4e24-130">In hello **configurazione di SQL Server** pannello, fare clic su hello **modifica** pulsante hello sezione integrazione automatizzata insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="d4e24-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![Configurare l'integrazione di AKV SQL per le VM esistenti](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="d4e24-132">Al termine, fare clic su hello **OK** pulsante nella parte inferiore di hello di hello **configurazione di SQL Server** pannello toosave le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d4e24-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="d4e24-133">È inoltre possibile configurare l'integrazione di AKV mediante un modello.</span><span class="sxs-lookup"><span data-stu-id="d4e24-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="d4e24-134">Per altre informazioni, vedere l'articolo relativo al [modello di avvio rapido di Azure per l'integrazione dell'insieme di credenziali delle chiavi di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="d4e24-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

