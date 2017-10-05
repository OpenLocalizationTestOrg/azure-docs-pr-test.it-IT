---
title: Integrare il Key Vault con SQL Server in VM Windows in Azure (Resource Manager) | Documentazione Microsoft
description: Informazioni su come automatizzare la configurazione della crittografia di SQL Server per l'uso con l'insieme di credenziali delle chiavi di Azure. Questo argomento illustra come usare l'integrazione dell'insieme di credenziali delle chiavi di Azure con le macchine virtuali di SQL Server create con Gestione risorse.
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
ms.openlocfilehash: 32b9564fa5c9ca6864ade343fda309b2c3edf123
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="31013-104">Configurare l'integrazione di Azure Key Vault per SQL Server in macchine virtuali di Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="31013-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31013-105">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="31013-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="31013-106">Classico</span><span class="sxs-lookup"><span data-stu-id="31013-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="31013-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="31013-107">Overview</span></span>
<span data-ttu-id="31013-108">Esistono più funzionalità di crittografia di SQL Server, ad esempio [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [crittografia a livello di colonna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) e [crittografia di backup](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="31013-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="31013-109">Queste modalità di crittografia richiedono la gestione e l'archiviazione delle chiavi usate per la crittografia.</span><span class="sxs-lookup"><span data-stu-id="31013-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span></span> <span data-ttu-id="31013-110">Il servizio dell'insieme di credenziali delle chiavi di Azure (AKV) è progettato per migliorare la sicurezza e la gestione di queste chiavi in una posizione sicura e a elevata disponibilità.</span><span class="sxs-lookup"><span data-stu-id="31013-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="31013-111">Il [connettore di SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) consente a SQL Server di usare queste chiavi dall'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="31013-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span></span>

<span data-ttu-id="31013-112">Se si esegue SQL Server con computer locali, sono disponibili [passaggi per accedere all'insieme di credenziali delle chiavi di Azure dal computer locale con SQL Server](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="31013-112">If you running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="31013-113">Se si esegue SQL Server in macchine virtuali di Azure, è possibile risparmiare tempo usando la funzionalità di *Integrazione dell'insieme di credenziali delle chiavi di Azure* .</span><span class="sxs-lookup"><span data-stu-id="31013-113">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="31013-114">Quando questa funzionalità è abilitata, installa automaticamente il connettore di SQL Server, configura il provider EKM per accedere all'insieme di credenziali delle chiavi di Azure e crea le credenziali per consentire l'accesso all'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="31013-114">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span></span> <span data-ttu-id="31013-115">Se sono stati esaminati i passaggi nella documentazione locale menzionati in precedenza, si noterà che questa funzionalità consente di automatizzare i passaggi 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="31013-115">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="31013-116">L'unica attività che è comunque necessario eseguire manualmente è la creazione delle chiavi e dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="31013-116">The only thing you would still need to do manually is to create the key vault and keys.</span></span> <span data-ttu-id="31013-117">Una volta completata questa operazione, l'intera installazione della macchina virtuale di SQL è automatizzata.</span><span class="sxs-lookup"><span data-stu-id="31013-117">From there, the entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="31013-118">Quando la funzionalità ha completato l'installazione, è possibile eseguire istruzioni T-SQL per iniziare la crittografia dei database o del backup regolarmente.</span><span class="sxs-lookup"><span data-stu-id="31013-118">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="31013-119">Abilitazione e configurazione dell'integrazione di AKV</span><span class="sxs-lookup"><span data-stu-id="31013-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="31013-120">È possibile abilitare l'integrazione di AKV durante il provisioning oppure configurarlo per VM esistenti.</span><span class="sxs-lookup"><span data-stu-id="31013-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="31013-121">Nuove VM</span><span class="sxs-lookup"><span data-stu-id="31013-121">New VMs</span></span>
<span data-ttu-id="31013-122">Se si esegue il provisioning di una nuova macchina virtuale SQL Server con Resource Manager, il portale di Azure offre una procedura per abilitare l'integrazione dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="31013-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, the Azure portal provides a step to enable Azure Key Vault integration.</span></span> <span data-ttu-id="31013-123">La funzionalità dell'insieme di credenziali delle chiavi di Azure è disponibile solo per la Enterprise, la Developer Edition e la copia di valutazione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="31013-123">The Azure Key Vault feature is available only for the Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Integrazione dell'insieme di credenziali delle chiavi di Azure per SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="31013-125">Per una procedura dettagliata del provisioning, vedere [Effettuare il provisioning di una macchina virtuale di SQL Server nel portale di Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="31013-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="31013-126">VM esistenti</span><span class="sxs-lookup"><span data-stu-id="31013-126">Existing VMs</span></span>
<span data-ttu-id="31013-127">Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="31013-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="31013-128">Dopodiché, selezionare la sezione **Configurazione di SQL Server** del pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="31013-128">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Integrazione di AKV SQL per le VM esistenti](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="31013-130">Nel pannello **Configurazione di SQL Server** fare clic sul pulsante **Modifica** nella sezione sull'integrazione automatica dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="31013-130">In the **SQL Server configuration** blade, click the **Edit** button in the Automated Key Vault integration section.</span></span>

![Configurare l'integrazione di AKV SQL per le VM esistenti](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="31013-132">Al termine, fare clic sul pulsante **OK** in fondo al pannello **Configurazione di SQL Server** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="31013-132">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="31013-133">È inoltre possibile configurare l'integrazione di AKV mediante un modello.</span><span class="sxs-lookup"><span data-stu-id="31013-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="31013-134">Per altre informazioni, vedere l'articolo relativo al [modello di avvio rapido di Azure per l'integrazione dell'insieme di credenziali delle chiavi di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="31013-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

