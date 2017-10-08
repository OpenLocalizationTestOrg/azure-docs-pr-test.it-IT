---
title: Archiviazione Premium di Azure con SQL Server aaaUse | Documenti Microsoft
description: In questo articolo usa le risorse create con il modello di distribuzione classica hello e vengono fornite istruzioni sull'uso di archiviazione Premium di Azure con SQL Server in esecuzione in macchine virtuali di Azure.
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="70a8a-103">Utilizzare Archiviazione Premium di Azure con SQL Server in macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="70a8a-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="70a8a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="70a8a-104">Overview</span></span>
<span data-ttu-id="70a8a-105">[Archiviazione Premium di Azure](../../../storage/common/storage-premium-storage.md) è hello prossima generazione di archiviazione che fornisce bassa latenza e ad alta velocità effettiva dei / o.</span><span class="sxs-lookup"><span data-stu-id="70a8a-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="70a8a-106">Funziona al meglio per i carichi di lavoro con numerose operazioni di I/O, ad esempio SQL Server in [macchine virtuali](https://azure.microsoft.com/services/virtual-machines/)IaaS.</span><span class="sxs-lookup"><span data-stu-id="70a8a-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70a8a-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="70a8a-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="70a8a-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="70a8a-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="70a8a-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="70a8a-110">In questo articolo fornisce la pianificazione e indicazioni per la migrazione di una macchina virtuale in esecuzione SQL Server toouse archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="70a8a-111">Sono inclusi i passaggi relativi all'infrastruttura di Azure (rete, archiviazione) e alle macchine virtuali guest di Windows.</span><span class="sxs-lookup"><span data-stu-id="70a8a-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="70a8a-112">esempio Hello in hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) Mostra una migrazione tooend end completo completa di come toomove maggiore macchine virtuali tootake sfruttare un locale archiviazione sull'unità SSD con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70a8a-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="70a8a-113">Si tratta toounderstand importante hello end-to-end processo che utilizzano Premium di archiviazione di Azure con SQL Server in macchine virtuali IAAS.</span><span class="sxs-lookup"><span data-stu-id="70a8a-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="70a8a-114">Sono inclusi:</span><span class="sxs-lookup"><span data-stu-id="70a8a-114">This includes:</span></span>

* <span data-ttu-id="70a8a-115">Identificazione dei prerequisiti di hello toouse archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="70a8a-116">Esempi di distribuzione di SQL Server su IaaS tooPremium archiviazione per nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="70a8a-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="70a8a-117">Esempi di migrazione delle distribuzioni esistenti, sia di server autonomi che distribuzioni tramite gruppi di disponibilità di SQL AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="70a8a-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="70a8a-118">Approcci di migrazione possibili.</span><span class="sxs-lookup"><span data-stu-id="70a8a-118">Possible migration approaches.</span></span>
* <span data-ttu-id="70a8a-119">Esempio completo end-to-end che mostra i passaggi di Azure, Windows e SQL Server per la migrazione di hello di un'implementazione di Always On esistente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="70a8a-120">Per ottenere le informazioni più esaustive sull'uso di SQL Server in Macchine virtuali di Azure, vedere [SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70a8a-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="70a8a-121">**Autore:** Daniel Sol **Revisori tecnici:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="70a8a-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="70a8a-122">Prerequisiti per Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="70a8a-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="70a8a-123">Esistono diversi prerequisiti per l'utilizzo di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="70a8a-124">Dimensioni della macchina</span><span class="sxs-lookup"><span data-stu-id="70a8a-124">Machine size</span></span>
<span data-ttu-id="70a8a-125">Per l'utilizzo di archiviazione Premium è necessario serie DS toouse macchine virtuali (VM).</span><span class="sxs-lookup"><span data-stu-id="70a8a-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="70a8a-126">Se si utilizzano macchine serie DS nel servizio cloud prima di, è necessario eliminare hello macchina virtuale esistente, mantenere i dischi collegato hello e quindi creare un nuovo servizio cloud prima di ricreare hello macchina virtuale come dimensioni del ruolo DS *.</span><span class="sxs-lookup"><span data-stu-id="70a8a-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="70a8a-127">Per ulteriori informazioni sulle dimensioni della macchine virtuali, vedere [Dimensioni delle macchine virtuali e dei servizi cloud per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70a8a-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="70a8a-128">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="70a8a-128">Cloud services</span></span>
<span data-ttu-id="70a8a-129">È possibile utilizzare le macchine virtuali DS* con Archiviazione Premium solo quando vengono create in un nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="70a8a-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="70a8a-130">Se si utilizza SQL Server Always On in Azure, hello sempre sul Listener farà riferimento toohello indirizzo interno di Azure o indirizzo IP di bilanciamento del carico esterno che è associata a un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="70a8a-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="70a8a-131">Questo articolo è incentrato sulla toomigrate, mantenendo la disponibilità in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="70a8a-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="70a8a-132">Una serie DS * deve essere hello prima macchina virtuale che viene distribuito toohello nuovo servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="70a8a-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="70a8a-133">Reti virtuali regionali</span><span class="sxs-lookup"><span data-stu-id="70a8a-133">Regional VNETS</span></span>
<span data-ttu-id="70a8a-134">Per le macchine virtuali DS * è necessario configurare una rete virtuale (VNET) che ospita la macchine virtuali toobe internazionali hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="70a8a-135">Questo hello "viene ampliato" rete virtuale è tooallow hello toobe macchine virtuali più grandi il provisioning in altri cluster e consentire la comunicazione tra di essi.</span><span class="sxs-lookup"><span data-stu-id="70a8a-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="70a8a-136">Nella seguente schermata di hello, hello evidenziato percorso Mostra regione, mentre il primo risultato hello Mostra una rete virtuale "narrow".</span><span class="sxs-lookup"><span data-stu-id="70a8a-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="70a8a-138">È possibile generare un tooa di toomigrate ticket di supporto Microsoft rete virtuale di regione, Microsoft apportata una modifica, quindi toocomplete hello migrazione tooregional reti virtuali, modificare la proprietà hello AffinityGroup hello configurazione della rete.</span><span class="sxs-lookup"><span data-stu-id="70a8a-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="70a8a-139">Prima di tutto esportare hello configurazione di rete in PowerShell e quindi sostituire hello **AffinityGroup** proprietà hello **VirtualNetworkSite** elemento con un **percorso** proprietà.</span><span class="sxs-lookup"><span data-stu-id="70a8a-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="70a8a-140">Specificare `Location = XXXX` dove `XXXX` è un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="70a8a-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="70a8a-141">Quindi importare nuova configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-141">Then import hello new configuration.</span></span>

<span data-ttu-id="70a8a-142">Ad esempio, considerare hello seguente configurazione di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="70a8a-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="70a8a-143">toomove questo tooa internazionali tra reti VIRTUALI in Europa occidentale, modificare hello toohello di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="70a8a-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="70a8a-144">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="70a8a-144">Storage accounts</span></span>
<span data-ttu-id="70a8a-145">Sarà necessario toocreate un nuovo account di archiviazione è configurato per l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="70a8a-146">Si noti che utilizzo hello di archiviazione Premium è impostata in account di archiviazione di hello, non su singoli dischi rigidi virtuali, tuttavia quando si utilizza una macchina virtuale serie DS * è possibile collegare i file VHD dall'account di archiviazione Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="70a8a-147">Se non si desidera tooplace hello disco rigido virtuale del sistema operativo su toohello account di archiviazione Premium, è possibile considerare questo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="70a8a-148">esempio Hello **New AzureStorageAccountPowerShell** comando con "Premium_LRS" hello **tipo** crea un Account di archiviazione Premium:</span><span class="sxs-lookup"><span data-stu-id="70a8a-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="70a8a-149">Impostazioni della cache di dischi rigidi virtuali</span><span class="sxs-lookup"><span data-stu-id="70a8a-149">VHDs Cache Settings</span></span>
<span data-ttu-id="70a8a-150">Hello differenza principale tra la creazione di dischi che fanno parte di un account di archiviazione Premium è impostazione della cache di hello disco.</span><span class="sxs-lookup"><span data-stu-id="70a8a-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="70a8a-151">Per i dischi del volume di dati di SQL Server, è consigliabile usare "**Read Caching**".</span><span class="sxs-lookup"><span data-stu-id="70a8a-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="70a8a-152">Per i volumi di log delle transazioni, impostazione della cache di hello disco deve essere impostato troppo '**Nessuno**'.</span><span class="sxs-lookup"><span data-stu-id="70a8a-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="70a8a-153">Questa è diversa da quelle consigliate hello per gli account di archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="70a8a-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="70a8a-154">Dopo aver allegati hello i dischi rigidi virtuali, non è possibile modificare l'impostazione della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="70a8a-155">Si sarebbe necessario toodetach e si ricollega hello disco rigido virtuale con un'impostazione della cache aggiornata.</span><span class="sxs-lookup"><span data-stu-id="70a8a-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="70a8a-156">Spazi di archiviazione di Windows</span><span class="sxs-lookup"><span data-stu-id="70a8a-156">Windows storage spaces</span></span>
<span data-ttu-id="70a8a-157">È possibile utilizzare [spazi di archiviazione di Windows](https://technet.microsoft.com/library/hh831739.aspx) in modo analogo al precedente archiviazione Standard, in questo modo si toomigrate una macchina virtuale che è già utilizzano spazi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="70a8a-158">esempio Hello in [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (passaggio 9 in poi) illustra hello tooextract codice Powershell e importare una macchina virtuale con più dischi rigidi virtuali collegati.</span><span class="sxs-lookup"><span data-stu-id="70a8a-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="70a8a-159">Pool di archiviazione utilizzati con velocità effettiva tooenhance di account di archiviazione di Azure Standard e ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="70a8a-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="70a8a-160">Può essere utile testare i pool di archiviazione con Archiviazione Premium per le nuove distribuzioni, ma l’impostazione dell’archiviazione aggiunge ulteriore complessità.</span><span class="sxs-lookup"><span data-stu-id="70a8a-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="70a8a-161">Come toofind toostorage pool di mappare i dischi virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="70a8a-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="70a8a-162">Vi sono indicazioni di impostazione della cache diverse per i dischi rigidi virtuali collegati, è possibile decidere toocopy hello dischi rigidi virtuali tooa account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="70a8a-163">Tuttavia, quando si ricollegarli toohello serie DS nuova macchina virtuale, potrebbe essere necessario tooalter le impostazioni della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="70a8a-164">È più semplice hello tooapply che archiviazione Premium consigliata le impostazioni della cache quando si dispone di dischi rigidi virtuali separati per hello SQL dati file e log file (anziché un singolo disco rigido virtuale che contiene entrambi).</span><span class="sxs-lookup"><span data-stu-id="70a8a-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="70a8a-165">Se si dispone di file di dati e log di SQL Server su hello stesso volume, opzione che si sceglie di memorizzazione nella cache di hello dipende da modelli di accesso i/o hello per i carichi di lavoro del database.</span><span class="sxs-lookup"><span data-stu-id="70a8a-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="70a8a-166">Solo i test possono dimostrare quale opzione di memorizzazione nella cache è più adatta a questo scenario.</span><span class="sxs-lookup"><span data-stu-id="70a8a-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="70a8a-167">Tuttavia, se si utilizza spazi di archiviazione di Windows che sono costituite da più dischi rigidi virtuali è necessario toolook nel tooidentify script originale cui collegata a dischi rigidi virtuali sono in quale pool specifico, pertanto, è quindi possibile impostare le impostazioni della cache di hello conseguenza per ogni disco.</span><span class="sxs-lookup"><span data-stu-id="70a8a-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="70a8a-168">Se non si dispone originale tooshow disponibili di script di cui eseguire il mapping di dischi rigidi virtuali toohello pool di archiviazione, è possibile utilizzare hello dopo il mapping del pool passaggi toodetermine hello/archiviazione su disco.</span><span class="sxs-lookup"><span data-stu-id="70a8a-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="70a8a-169">Per ogni disco, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70a8a-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="70a8a-170">Ottenere un elenco di dischi collegati tooVM con hello **Get-AzureVM** comando:</span><span class="sxs-lookup"><span data-stu-id="70a8a-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="70a8a-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="70a8a-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="70a8a-172">Si noti hello Diskname e al LUN.</span><span class="sxs-lookup"><span data-stu-id="70a8a-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="70a8a-174">Desktop remoto in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="70a8a-175">Quindi andare troppo**Gestione Computer** | **Gestione dispositivi** | **unità disco**.</span><span class="sxs-lookup"><span data-stu-id="70a8a-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="70a8a-176">Esaminare la proprietà hello di ogni hello 'Microsoft dischi virtuali'</span><span class="sxs-lookup"><span data-stu-id="70a8a-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="70a8a-178">numero LUN Hello qui è un numero LUN toohello riferimento specificato durante il collegamento hello VHD toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="70a8a-179">Per "Disco virtuale di Microsoft" hello, visitare toohello **dettagli** scheda, quindi hello **proprietà** elenco, andare troppo**chiave Driver**.</span><span class="sxs-lookup"><span data-stu-id="70a8a-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="70a8a-180">In hello **valore**, hello nota **Offset**, ovvero 0002 nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="70a8a-181">Hello 0002 indica hello PhysicalDisk2 che hello riferimenti di pool di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="70a8a-183">Per ogni pool di archiviazione, dump out hello associati dischi:</span><span class="sxs-lookup"><span data-stu-id="70a8a-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="70a8a-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="70a8a-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="70a8a-186">È ora possibile usare questo tooassociate informazioni collegati dischi rigidi virtuali tooPhysical dischi nel pool di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="70a8a-187">Dopo aver mappato i dischi rigidi virtuali tooPhysical dischi nel pool di archiviazione è quindi possibile scollegare e copiarli su tooa account di archiviazione Premium, quindi collegarli con cache di hello corretta impostazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="70a8a-188">Vedere l'esempio hello in hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), i passaggi da 8 a 12.</span><span class="sxs-lookup"><span data-stu-id="70a8a-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="70a8a-189">Questi passaggi mostrano come tooextract un VHD associato alla macchina virtuale su disco tooa CSV file di configurazione copiare i dischi rigidi virtuali hello, modificare le impostazioni della cache di hello disco configurazione e infine ridistribuire hello macchina virtuale come macchina virtuale della serie DS con hello tutti i dischi collegati.</span><span class="sxs-lookup"><span data-stu-id="70a8a-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="70a8a-190">Larghezza di banda di archiviazione della VM e velocità effettiva di archiviazione del VHD</span><span class="sxs-lookup"><span data-stu-id="70a8a-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="70a8a-191">Hello le prestazioni di archiviazione dipende hello dimensioni DS * VM specificata e hello dimensioni disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="70a8a-192">macchine virtuali Hello hanno quote diverse per il numero di dischi rigidi virtuali che possono essere collegati e larghezza di banda massima (MB/s) supporteranno hello hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="70a8a-193">Per i numeri di hello specifica larghezza di banda, vedere [macchina virtuale e alle dimensioni dei servizi Cloud per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70a8a-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="70a8a-194">Input/output al secondo maggiori si ottengono con dimensioni del disco maggiori.</span><span class="sxs-lookup"><span data-stu-id="70a8a-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="70a8a-195">Tenere conto di questa considerazione quando si decide il percorso di migrazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="70a8a-196">Per informazioni dettagliate, [per IOPS e tipi di disco, vedere la tabella hello](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="70a8a-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="70a8a-197">Infine, tenere presente che le macchine virtuali supporteranno larghezza di banda massime diverse per tutti i dischi collegati.</span><span class="sxs-lookup"><span data-stu-id="70a8a-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="70a8a-198">Un carico elevato, è Impossibile saturare hello su disco massimo della larghezza di banda disponibile per la dimensione di ruolo macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="70a8a-199">Ad esempio un Standard_DS14 supporteranno backup too512MB/s. Pertanto, con tre dischi P30 è Impossibile saturare hello disco larghezza di banda di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="70a8a-200">Ma in questo esempio, può essere superato il limite di velocità effettiva di hello a seconda della combinazione di hello di lettura e scrittura IOs.</span><span class="sxs-lookup"><span data-stu-id="70a8a-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="70a8a-201">Nuove distribuzioni</span><span class="sxs-lookup"><span data-stu-id="70a8a-201">New deployments</span></span>
<span data-ttu-id="70a8a-202">Hello nelle due sezioni successive viene illustrato come è possibile distribuire le macchine virtuali di SQL Server tooPremium archiviazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="70a8a-203">Come accennato in precedenza, non è necessariamente necessario disco del sistema operativo di hello tooplace in archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="70a8a-204">Si potrebbe scegliere toodo questa opzione se si sta prendendo in considerazione tooplace i carichi di lavoro con utilizzo intensivo dei / o su disco rigido virtuale del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="70a8a-205">Hello primo esempio viene illustrato l'utilizzo di immagini della raccolta Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="70a8a-206">Hello secondo esempio viene mostrato come una macchina virtuale personalizzata toouse immagine che si dispone di un account di archiviazione Standard esistente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="70a8a-207">Questi esempi presuppongono che sia già stata creata una rete virtuale regionale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="70a8a-208">Creare una nuova macchina virtuale con Archiviazione Premium con immagine della raccolta</span><span class="sxs-lookup"><span data-stu-id="70a8a-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="70a8a-209">esempio Hello riportato di seguito viene illustrato come tooplace hello disco rigido virtuale del sistema operativo in archiviazione premium e collegare i dischi rigidi virtuali di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="70a8a-210">Tuttavia, è possibile inoltre inserire disco del sistema operativo hello in un account di archiviazione Standard e quindi collegare i dischi rigidi virtuali che risiedono in un account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="70a8a-211">Vengono illustrati entrambi gli scenari.</span><span class="sxs-lookup"><span data-stu-id="70a8a-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="70a8a-212">Passaggio 1: Creare un account di Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="70a8a-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="70a8a-213">Passaggio 2: Creare un nuovo servizio cloud</span><span class="sxs-lookup"><span data-stu-id="70a8a-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="70a8a-214">Passaggio 3: Riservare un VIP di servizio cloud (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="70a8a-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="70a8a-215">Passaggio 4: Creare un contenitore di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="70a8a-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="70a8a-216">Passaggio 5: Collocazione del disco rigido virtuale su Archiviazione Standard o Premium </span><span class="sxs-lookup"><span data-stu-id="70a8a-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="70a8a-217">Passaggio 6: Creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="70a8a-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="70a8a-218">Creare un nuovo toouse VM archiviazione Premium con un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="70a8a-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="70a8a-219">Questo scenario mostra la posizione delle immagini personalizzate esistenti che risiedono in un account di Archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="70a8a-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="70a8a-220">Come accennato in se si desidera tooplace hello disco rigido virtuale del sistema operativo in archiviazione Premium, sarà necessario toocopy hello immagine che esiste in account di archiviazione Standard hello e li trasferisce tooa archiviazione Premium prima che possa essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="70a8a-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="70a8a-221">Se dispone di un'immagine locale, è possibile inoltre utilizzare questo metodo toocopy che direttamente toohello account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="70a8a-222">Passaggio 1: Creare l’account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="70a8a-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="70a8a-223">Passaggio 2: Creare il servizio cloud</span><span class="sxs-lookup"><span data-stu-id="70a8a-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="70a8a-224">Passaggio 3: Usare l'immagine esistente</span><span class="sxs-lookup"><span data-stu-id="70a8a-224">Step 3: Use existing image</span></span>
<span data-ttu-id="70a8a-225">È possibile utilizzare un'immagine esistente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-225">You can use an existing image.</span></span> <span data-ttu-id="70a8a-226">In alternativa è possibile [acquisire un'immagine di una macchina esistente](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70a8a-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="70a8a-227">Macchina hello nota che creare l'immagine non dispone di toobe DS * macchina.</span><span class="sxs-lookup"><span data-stu-id="70a8a-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="70a8a-228">Dopo aver creato immagine hello, hello seguente procedura mostra come toocopy, account di archiviazione Premium con hello toohello **inizio AzureStorageBlobCopy** cmdlet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70a8a-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="70a8a-229">Passaggio 4: Copiare BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="70a8a-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="70a8a-230">Passaggio 5: Verificare regolarmente lo stato della copia:</span><span class="sxs-lookup"><span data-stu-id="70a8a-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="70a8a-231">Passaggio 6: Aggiungere immagini disco tooAzure disco Repository nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="70a8a-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="70a8a-232">È possibile che anche se i rapporti di stato di hello come esito positivo, è comunque possibile ottenere un errore di lease del disco.</span><span class="sxs-lookup"><span data-stu-id="70a8a-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="70a8a-233">In questo caso, attendere circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="70a8a-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="70a8a-234">Passaggio 7: Compilazione hello VM</span><span class="sxs-lookup"><span data-stu-id="70a8a-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="70a8a-235">Qui si sta compilando hello macchina virtuale da un'immagine e collegamento di due dischi rigidi virtuali archiviazione Premium:</span><span class="sxs-lookup"><span data-stu-id="70a8a-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="70a8a-236">Distribuzioni esistenti che non usano i gruppi di disponibilità AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="70a8a-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="70a8a-237">Per le distribuzioni esistenti, vedere prima hello [prerequisiti](#prerequisites-for-premium-storage) sezione di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="70a8a-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="70a8a-238">Esistono diverse considerazioni per le distribuzioni di SQL Server che non usano i gruppi di disponibilità AlwaysOn e per quelle che li usano.</span><span class="sxs-lookup"><span data-stu-id="70a8a-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="70a8a-239">Se non si usa Always On e un Server SQL autonomo esistente, è possibile aggiornare tooPremium archiviazione utilizzando un nuovo account di servizio e l'archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="70a8a-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="70a8a-240">prendere in considerazione hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="70a8a-240">Consider hello following options:</span></span>

* <span data-ttu-id="70a8a-241">**Creare una nuova macchina virtuale di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="70a8a-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="70a8a-242">È possibile creare una nuova macchina virtuale di SQL Server che utilizza un account di Archiviazione Premium, come documentato in Nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="70a8a-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="70a8a-243">Eseguire quindi il backup e ripristino della configurazione di SQL Server e dei database utente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="70a8a-244">Hello applicazione sarà necessario aggiornare toobe tooreference hello nuovo SQL Server se si accede a internamente o esternamente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="70a8a-245">È necessario toocopy tutti gli oggetti 'fuori db' come se si verificasse una migrazione Side-by-Side (SxS) SQL Server.</span><span class="sxs-lookup"><span data-stu-id="70a8a-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="70a8a-246">Sono inclusi oggetti come account di accesso, certificati e server collegati.</span><span class="sxs-lookup"><span data-stu-id="70a8a-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="70a8a-247">**Eseguire la migrazione di una macchina virtuale di Server SQL esistente**.</span><span class="sxs-lookup"><span data-stu-id="70a8a-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="70a8a-248">Sarà necessario portare offline hello macchina virtuale SQL Server, quindi trasferirli tooa nuovo servizio cloud, che include la copia di tutti i relativi toohello dischi rigidi virtuali collegato, account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="70a8a-249">Quando si hello VM viene portata online, un'applicazione hello farà riferimento hello nome host del server come prima.</span><span class="sxs-lookup"><span data-stu-id="70a8a-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="70a8a-250">Tenere presente che dimensioni hello del disco esistente hello influirà sulle prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="70a8a-251">Ad esempio, un disco di 400 GB Ottiene arrotondato per eccesso tooa P20.</span><span class="sxs-lookup"><span data-stu-id="70a8a-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="70a8a-252">Se si sa che non richiedono che le prestazioni del disco, quindi è possibile ricreare hello macchina virtuale come macchina virtuale serie DS e collegare i dischi rigidi virtuali archiviazione Premium della specifica di dimensione/prestazioni hello desiderate.</span><span class="sxs-lookup"><span data-stu-id="70a8a-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="70a8a-253">È quindi possibile scollegare e ricollegare i file di database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="70a8a-254">Quando la copia dei dischi VHD hello è necessario essere consapevoli delle dimensioni di hello, a seconda delle dimensioni di hello implica il tipo di disco di archiviazione Premium che rientrano in, determina specifica delle prestazioni del disco.</span><span class="sxs-lookup"><span data-stu-id="70a8a-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="70a8a-255">Azure arrotonderà backup toohello più vicino al disco di dimensioni, se si dispone di un disco di 400 GB, questo verrà arrotondato tooa P20.</span><span class="sxs-lookup"><span data-stu-id="70a8a-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="70a8a-256">A seconda dei requisiti dei / o esistenti di hello disco rigido virtuale del sistema operativo, potrebbe non essere necessario toomigrate questo tooa account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="70a8a-257">Se SQL Server è accessibile dall'esterno, hello VIP di servizio cloud verrà modificato.</span><span class="sxs-lookup"><span data-stu-id="70a8a-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="70a8a-258">Sarà inoltre necessario tooupdate punti di fine, gli ACL e DNS impostazioni.</span><span class="sxs-lookup"><span data-stu-id="70a8a-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="70a8a-259">Distribuzioni esistenti che usano i gruppi di disponibilità AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="70a8a-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="70a8a-260">Per le distribuzioni esistenti, vedere prima hello [prerequisiti](#prerequisites-for-premium-storage) sezione di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="70a8a-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="70a8a-261">In questa sezione si osserverà prima di tutto in che modo AlwaysOn interagisce con una rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="70a8a-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="70a8a-262">Si verrà quindi scomporre le migrazioni in scenari tootwo: le migrazioni in cui è necessario ottenere tempi di inattività minimi e le migrazioni in cui è possibile tollerare i tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="70a8a-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="70a8a-263">I gruppi di disponibilità di SQL Server AlwaysOn locali usano un listener locale che registra un nome DNS virtuale con un indirizzo IP condiviso tra uno o più server SQL.</span><span class="sxs-lookup"><span data-stu-id="70a8a-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="70a8a-264">Quando si connettono i client vengono indirizzate tramite hello listener IP toohello primaria di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="70a8a-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="70a8a-265">Questo è il server hello proprietario hello risorsa sempre su IP in quel momento.</span><span class="sxs-lookup"><span data-stu-id="70a8a-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="70a8a-267">In Microsoft Azure è possibile avere un solo IP indirizzo assegnato tooa NIC nella macchina virtuale, hello in ordine tooachieve hello stesso livello di astrazione come locale, Azure Usa indirizzo IP hello assegnato bilanciamenti del carico interno/esterno di toohello (bilanciamento del carico interno/ELB).</span><span class="sxs-lookup"><span data-stu-id="70a8a-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="70a8a-268">risorsa IP Hello condivisi tra i server hello impostata toohello stesso IP come hello/ELB di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="70a8a-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="70a8a-269">Questo viene pubblicato in DNS hello e il traffico dei client verrà passato tramite replica di SQL Server primario toohello ILB/ELB hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="70a8a-270">bilanciamento del carico interno/ELB Hello sa che SQL Server è primario, poiché Usa risorse di probe tooprobe hello sempre su IP.</span><span class="sxs-lookup"><span data-stu-id="70a8a-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="70a8a-271">Nell'esempio precedente hello, analizza ogni nodo che dispone di un endpoint a cui fa riferimento hello ELB/ILB, a seconda del valore di risposta è hello primaria di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="70a8a-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="70a8a-272">Hello ILB ELB entrambi assegnati e tooa specifico servizio cloud Azure, pertanto, qualsiasi migrazione cloud in Azure verranno probabilmente che hello che IP di bilanciamento del carico verrà modificato.</span><span class="sxs-lookup"><span data-stu-id="70a8a-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="70a8a-273">Migrazione delle distribuzioni di AlwaysOn che tollerano tempi di inattività</span><span class="sxs-lookup"><span data-stu-id="70a8a-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="70a8a-274">Sono disponibili due strategie toomigrate Always On le distribuzioni che consentono di tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="70a8a-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="70a8a-275">**Aggiungere ulteriori tooan repliche secondarie esistenti sempre in Cluster**</span><span class="sxs-lookup"><span data-stu-id="70a8a-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="70a8a-276">**Eseguire la migrazione tooa nuovo sempre in Cluster**</span><span class="sxs-lookup"><span data-stu-id="70a8a-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="70a8a-277">1. Aggiungere ulteriori repliche secondarie tooan sempre nel Cluster esistente</span><span class="sxs-lookup"><span data-stu-id="70a8a-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="70a8a-278">Una strategia è tooadd più database secondari toohello gruppo di disponibilità AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="70a8a-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="70a8a-279">È necessario tooadd in un nuovo servizio cloud e aggiornare listener hello con hello nuovo indirizzo IP del servizio di bilanciamento di carico.</span><span class="sxs-lookup"><span data-stu-id="70a8a-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="70a8a-280">Punti dei tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="70a8a-280">Points of downtime:</span></span>
* <span data-ttu-id="70a8a-281">Convalida del cluster.</span><span class="sxs-lookup"><span data-stu-id="70a8a-281">Cluster Validation.</span></span>
* <span data-ttu-id="70a8a-282">Test di failover AlwaysOn per nuovi database secondari.</span><span class="sxs-lookup"><span data-stu-id="70a8a-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="70a8a-283">Se si utilizza il pool di archiviazione di Windows all'interno di hello macchina virtuale per una velocità effettiva dei / o, queste verranno portate offline durante una convalida completa di Cluster.</span><span class="sxs-lookup"><span data-stu-id="70a8a-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="70a8a-284">test di convalida Hello è obbligatorio quando si aggiunge nodi toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="70a8a-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="70a8a-285">Hello tempo test hello toorun può variare, quindi è opportuno verificare questo nel tooget ambiente di test rappresentativo un tempo approssimativo di questo tempo richiesto.</span><span class="sxs-lookup"><span data-stu-id="70a8a-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="70a8a-286">È necessario eseguire il provisioning di tempo in cui è possibile eseguire il failover manuale e chaos test hello appena aggiunto le funzioni di disponibilità elevata Always On tooensure nodi come previsto.</span><span class="sxs-lookup"><span data-stu-id="70a8a-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="70a8a-288">È necessario arrestare tutte le istanze di SQL Server in cui vengono utilizzati i pool di archiviazione hello prima hello la convalida viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="70a8a-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="70a8a-289">Procedure generali</span><span class="sxs-lookup"><span data-stu-id="70a8a-289">High-level steps</span></span>
>

1. <span data-ttu-id="70a8a-290">Creare due nuovi server SQL Server nel nuovo servizio cloud con Archiviazione Premium collegata.</span><span class="sxs-lookup"><span data-stu-id="70a8a-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="70a8a-291">Copiare i backup completi e ripristinare con **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="70a8a-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="70a8a-292">Copiare gli oggetti dipendenti esterni al database utente, ad esempio nomi di accesso e così via.</span><span class="sxs-lookup"><span data-stu-id="70a8a-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="70a8a-293">Crea un nuovo servizio di carico bilanciamento interno (ILB) oppure utilizzare un servizio di bilanciamento del carico esterno (ELB) e quindi impostare gli endpoint con bilanciamento del carico in entrambi i nodi nuovi.</span><span class="sxs-lookup"><span data-stu-id="70a8a-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="70a8a-294">Controllare che tutti i nodi dispongono di configurazione dell'Endpoint corretto hello prima di continuare</span><span class="sxs-lookup"><span data-stu-id="70a8a-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="70a8a-295">Arrestare l'accesso utente/applicazione toohello SQL Server (se si Usa pool di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="70a8a-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="70a8a-296">Arrestare i servizi motore di SQL Server in tutti i nodi (se si utilizzano il pool di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="70a8a-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="70a8a-297">Aggiungere nuovi nodi toocluster ed eseguire la convalida completa.</span><span class="sxs-lookup"><span data-stu-id="70a8a-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="70a8a-298">Quando la convalida ha esito positivo, avviare tutti i servizi di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="70a8a-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="70a8a-299">Eseguire il backup dei log delle transazioni e ripristinare i database utente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="70a8a-300">Aggiungere nuovi nodi nel gruppo di disponibilità AlwaysOn hello e inserire la replica in **sincrono**.</span><span class="sxs-lookup"><span data-stu-id="70a8a-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="70a8a-301">Aggiungi IP hello risorsa indirizzo di hello nuovo Cloud servizio di bilanciamento del carico interno/ELB tramite PowerShell per Always On in base a esempio multisito hello in hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="70a8a-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="70a8a-302">Nel clustering di Windows, impostare hello **proprietari possibili** di hello **indirizzo IP** toohello nuovi nodi di risorsa precedenti.</span><span class="sxs-lookup"><span data-stu-id="70a8a-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="70a8a-303">Nella sezione hello 'Aggiunta di risorse di indirizzo IP nella stessa Subnet' di hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="70a8a-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="70a8a-304">Failover tooone di nuovi nodi hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="70a8a-305">Assicurarsi di hello nuovi nodi partner di Failover automatico e i failover di test.</span><span class="sxs-lookup"><span data-stu-id="70a8a-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="70a8a-306">Rimuovere i nodi originali dal gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="70a8a-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="70a8a-307">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="70a8a-307">Advantages</span></span>
* <span data-ttu-id="70a8a-308">Nuovo SQL Server possono essere testati (SQL Server e dell'applicazione) prima che vengano aggiunti tooAlways in.</span><span class="sxs-lookup"><span data-stu-id="70a8a-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="70a8a-309">È possibile cambiare dimensioni della VM hello e personalizzare i requisiti di hello archiviazione tooyour esatto.</span><span class="sxs-lookup"><span data-stu-id="70a8a-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="70a8a-310">Tuttavia, sarebbe utile tookeep tutti i percorsi di file SQL hello hello stesso.</span><span class="sxs-lookup"><span data-stu-id="70a8a-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="70a8a-311">È possibile controllare quando vengono avviati i trasferimento hello di hello DB backup toohello repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="70a8a-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="70a8a-312">Questo comportamento è diverso dall'utilizzo di Azure **inizio AzureStorageBlobCopy** toocopy cmdlet dischi rigidi virtuali, in quanto si tratta di una copia asincrona.</span><span class="sxs-lookup"><span data-stu-id="70a8a-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="70a8a-313">Svantaggi:</span><span class="sxs-lookup"><span data-stu-id="70a8a-313">Disadvantages</span></span>
* <span data-ttu-id="70a8a-314">Quando si utilizza il pool di archiviazione di Windows, si è il tempo di inattività del Cluster durante hello convalida completa del Cluster per i nuovi nodi aggiuntivi di hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="70a8a-315">A seconda della versione di SQL Server di hello e numero di repliche secondarie esistenti hello, potrebbe non essere in grado di tooadd più repliche secondarie senza rimuovere i database secondari esistenti.</span><span class="sxs-lookup"><span data-stu-id="70a8a-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="70a8a-316">Possono essere molto tempo di trasferimento di dati SQL durante l'impostazione delle repliche secondarie hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="70a8a-317">Esiste un costo aggiuntivo durante la migrazione mentre le nuove macchine vengono eseguite in parallelo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="70a8a-318">2. Eseguire la migrazione tooa nuovo sempre in Cluster</span><span class="sxs-lookup"><span data-stu-id="70a8a-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="70a8a-319">Un'altra strategia consiste di un nuovo sempre in Cluster con nodi nuovi toocreate nel nuovo servizio cloud e quindi reindirizzamento hello client toouse è.</span><span class="sxs-lookup"><span data-stu-id="70a8a-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="70a8a-320">Punti dei tempi di inattività</span><span class="sxs-lookup"><span data-stu-id="70a8a-320">Points of downtime</span></span>
<span data-ttu-id="70a8a-321">Quando si trasferisce utenti e applicazioni toohello nuovo Always On listener, è tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="70a8a-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="70a8a-322">dipende dal tempo di inattività Hello:</span><span class="sxs-lookup"><span data-stu-id="70a8a-322">hello downtime depends on:</span></span>

* <span data-ttu-id="70a8a-323">Hello scattato toodatabases di backup del log delle transazioni finale toorestore nei nuovi server.</span><span class="sxs-lookup"><span data-stu-id="70a8a-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="70a8a-324">Hello scattato tooupdate applicazioni toouse nuovo Always On listener del client.</span><span class="sxs-lookup"><span data-stu-id="70a8a-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="70a8a-325">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="70a8a-325">Advantages</span></span>
* <span data-ttu-id="70a8a-326">È possibile testare l'ambiente di produzione reale hello, SQL Server, e sistema operativo compilazione (modifiche).</span><span class="sxs-lookup"><span data-stu-id="70a8a-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="70a8a-327">È necessario hello opzione toocustomize hello archivio e toopotentially ridurre le dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="70a8a-328">Ciò potrebbe causare determinare una riduzione dei costi.</span><span class="sxs-lookup"><span data-stu-id="70a8a-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="70a8a-329">Durante questo processo, è possibile aggiornare il build o la versione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="70a8a-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="70a8a-330">È inoltre possibile aggiornare hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="70a8a-331">Hello che sempre nel Cluster precedente può fungere da destinazione di rollback a tinta unita.</span><span class="sxs-lookup"><span data-stu-id="70a8a-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="70a8a-332">Svantaggi:</span><span class="sxs-lookup"><span data-stu-id="70a8a-332">Disadvantages</span></span>
* <span data-ttu-id="70a8a-333">Nome DNS di hello toochange del listener hello è necessario se si desidera che sia sempre in cluster che eseguono contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="70a8a-334">Amministrazione overhead durante la migrazione di hello verrà aggiunto come le stringhe dell'applicazione client devono riflettere hello nuovo nome del Listener.</span><span class="sxs-lookup"><span data-stu-id="70a8a-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="70a8a-335">È necessario implementare un meccanismo di sincronizzazione tra hello due ambienti tookeep come chiudere toominimize possibili i requisiti di sincronizzazione finale hello prima della migrazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="70a8a-336">Esiste aggiunta costo durante la migrazione mentre il nuovo ambiente hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="70a8a-337">Migrazione delle distribuzioni AlwaysOn per un tempo di inattività minimo</span><span class="sxs-lookup"><span data-stu-id="70a8a-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="70a8a-338">Sono disponibili due strategie per la migrazione delle distribuzioni di AlwaysOn per un tempo di inattività minimo:</span><span class="sxs-lookup"><span data-stu-id="70a8a-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="70a8a-339">**Utilizzare una replica secondaria esistente: singolo sito**</span><span class="sxs-lookup"><span data-stu-id="70a8a-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="70a8a-340">**Utilizzare repliche secondarie esistenti: multisito**</span><span class="sxs-lookup"><span data-stu-id="70a8a-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="70a8a-341">1. Usare una replica secondaria esistente: sito singolo</span><span class="sxs-lookup"><span data-stu-id="70a8a-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="70a8a-342">Una strategia per tempo di inattività minimo è un cloud esistente secondario tootake e rimuoverlo dal servizio cloud corrente hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="70a8a-343">Copiare quindi hello toohello di dischi rigidi virtuali nuovo account di archiviazione Premium e hello macchina virtuale nel nuovo servizio cloud di hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="70a8a-344">Aggiornare quindi il listener hello in clustering e il failover.</span><span class="sxs-lookup"><span data-stu-id="70a8a-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="70a8a-345">Punti dei tempi di inattività</span><span class="sxs-lookup"><span data-stu-id="70a8a-345">Points of downtime</span></span>
* <span data-ttu-id="70a8a-346">Quando si aggiorna il nodo finale di hello con endpoint con carico bilanciato hello è tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="70a8a-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="70a8a-347">La riconnessione del client potrebbe essere rimandata a seconda della configurazione client/DNS.</span><span class="sxs-lookup"><span data-stu-id="70a8a-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="70a8a-348">Se si sceglie tootake hello sempre il Cluster nel gruppo non in linea tooswap gli indirizzi IP hello è tempo di inattività aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="70a8a-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="70a8a-349">È possibile evitare questo problema utilizzando una dipendenza OR e proprietari possibili per hello aggiunto la risorsa indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="70a8a-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="70a8a-350">Nella sezione hello 'Aggiunta di risorse di indirizzo IP nella stessa Subnet' di hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="70a8a-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="70a8a-351">Quando si desidera hello toopartake nodo aggiunto in come un sempre nel Partner di Failover, è necessario tooadd un Endpoint di Azure con carico bilanciato impostato un toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="70a8a-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="70a8a-352">Quando si esegue hello **Add-AzureEndpoint** comando toodo, tooremain connessioni corrente aperto, ma nuovo listener toohello di connessioni non saranno in grado di toobe stabilita solo servizio di bilanciamento del carico hello è aggiornato.</span><span class="sxs-lookup"><span data-stu-id="70a8a-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="70a8a-353">Nei test questo era 90-120seconds toolast rilevato, questa deve essere testata.</span><span class="sxs-lookup"><span data-stu-id="70a8a-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="70a8a-354">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="70a8a-354">Advantages</span></span>
* <span data-ttu-id="70a8a-355">Nessun costo aggiuntivo durante la migrazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="70a8a-356">Una migrazione uno a uno.</span><span class="sxs-lookup"><span data-stu-id="70a8a-356">A one-to-one migration.</span></span>
* <span data-ttu-id="70a8a-357">Minore complessità.</span><span class="sxs-lookup"><span data-stu-id="70a8a-357">Reduced complexity.</span></span>
* <span data-ttu-id="70a8a-358">Consente un maggiore IOPS dalle SKU di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="70a8a-359">Quando parti un 3rd hello dischi vengono scollegata dalla macchina virtuale hello e copiati toohello del nuovo servizio cloud, può essere tooincrease utilizzate dimensioni di disco rigido virtuale hello, che offre una maggiore produttività.</span><span class="sxs-lookup"><span data-stu-id="70a8a-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="70a8a-360">Per aumentare le dimensioni del disco rigido virtuale, vedere questo [forum di discussione](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="70a8a-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="70a8a-361">Svantaggi:</span><span class="sxs-lookup"><span data-stu-id="70a8a-361">Disadvantages</span></span>
* <span data-ttu-id="70a8a-362">Perdita temporanea di disponibilità elevata e ripristino di emergenza durante la migrazione.</span><span class="sxs-lookup"><span data-stu-id="70a8a-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="70a8a-363">Poiché si tratta di una migrazione 1:1, sarà necessario toouse una dimensione minima di macchina virtuale in grado di supportare il numero di dischi rigidi virtuali, pertanto potrebbe non essere in grado di toodownsize le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="70a8a-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="70a8a-364">Questo scenario utilizza hello Azure **inizio AzureStorageBlobCopy** cmdlet, che è asincrono.</span><span class="sxs-lookup"><span data-stu-id="70a8a-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="70a8a-365">Non esiste alcun contratto di servizio al completamento della copia.</span><span class="sxs-lookup"><span data-stu-id="70a8a-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="70a8a-366">tempo di Hello di copie di hello varia, mentre questo dipende dal tempo di attesa in coda che variano inoltre quantità hello di tootransfer di dati.</span><span class="sxs-lookup"><span data-stu-id="70a8a-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="70a8a-367">tempo di copia Hello aumenta se il trasferimento di hello verrà tooanother data center di Azure che supporta l'archiviazione Premium in un'altra area.</span><span class="sxs-lookup"><span data-stu-id="70a8a-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="70a8a-368">Se si dispone solo di 2 nodi, prendere in considerazione una mitigazione possibili in caso di copia hello richiede più tempo durante i test.</span><span class="sxs-lookup"><span data-stu-id="70a8a-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="70a8a-369">Ad esempio hello seguenti idee.</span><span class="sxs-lookup"><span data-stu-id="70a8a-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="70a8a-370">Aggiungere un nodo di SQL Server 3 temporaneo per la disponibilità elevata prima della migrazione hello concordata tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="70a8a-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="70a8a-371">Eseguire la migrazione di hello di fuori di manutenzione pianificata di Azure.</span><span class="sxs-lookup"><span data-stu-id="70a8a-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="70a8a-372">Assicurarsi di che avere configurato correttamente il quorum del cluster.</span><span class="sxs-lookup"><span data-stu-id="70a8a-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="70a8a-373">Procedure generali</span><span class="sxs-lookup"><span data-stu-id="70a8a-373">High-level steps</span></span>
<span data-ttu-id="70a8a-374">Questo documento viene illustrato un esempio di tooend end completa, tuttavia hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) fornisce informazioni dettagliate che possono essere sfruttate tooperform questo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="70a8a-376">Configurazione del disco sequenziale e Rimuovi nodo hello (non eliminare i dischi rigidi virtuali collegati).</span><span class="sxs-lookup"><span data-stu-id="70a8a-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="70a8a-377">Creare un account di archiviazione Premium e copiare i dischi rigidi virtuali da hello account di archiviazione Standard</span><span class="sxs-lookup"><span data-stu-id="70a8a-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="70a8a-378">Crea nuovo servizio cloud e ridistribuire hello VM SQL2 nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="70a8a-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="70a8a-379">Creare VM hello utilizzando hello copiati i file VHD originale del sistema operativo e collegamento hello dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="70a8a-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="70a8a-380">Configurare ILB/ELB e aggiungere gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="70a8a-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="70a8a-381">Aggiornare il listener in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="70a8a-381">Update Listener by either:</span></span>
  * <span data-ttu-id="70a8a-382">Tenendo hello gruppo Always On non in linea e l'aggiornamento hello sempre sul Listener con bilanciamento del carico interno nuovo / indirizzo IP ELB.</span><span class="sxs-lookup"><span data-stu-id="70a8a-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="70a8a-383">O l'aggiunta di hello la risorsa indirizzo IP del nuovo Cloud servizio di bilanciamento del carico interno/ELB tramite PowerShell in Windows clustering.</span><span class="sxs-lookup"><span data-stu-id="70a8a-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="70a8a-384">Quindi set hello possibili proprietari del toohello risorsa indirizzo IP di hello eseguita la migrazione di nodo, SQL2 e impostare la dipendenza OR hello nome di rete.</span><span class="sxs-lookup"><span data-stu-id="70a8a-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="70a8a-385">Nella sezione hello 'Aggiunta di risorse di indirizzo IP nella stessa Subnet' di hello [appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="70a8a-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="70a8a-386">Controllare i client toohello configurazione/propagazione DNS.</span><span class="sxs-lookup"><span data-stu-id="70a8a-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="70a8a-387">Eseguire la migrazione della macchina virtuale SQL1 ed effettuare i passaggi da 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="70a8a-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="70a8a-388">Se si utilizza 5ii passaggi, quindi aggiungere SQL1 come possibile proprietario di hello aggiunto la risorsa indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="70a8a-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="70a8a-389">Testare i failover.</span><span class="sxs-lookup"><span data-stu-id="70a8a-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="70a8a-390">2. Usare una o più repliche secondarie esistenti: multisito</span><span class="sxs-lookup"><span data-stu-id="70a8a-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="70a8a-391">Se si dispongono di nodi in più Data Center Azure (DC) o se si dispone di un ambiente ibrido, è possibile utilizzare una configurazione di Always On in questo periodo di inattività toominimize ambiente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="70a8a-392">approccio Hello è toochange hello Always On sincronizzazione tooSynchronous per hello in locale o controller di dominio secondario di Azure e il failover su toothat SQL Server.</span><span class="sxs-lookup"><span data-stu-id="70a8a-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="70a8a-393">Quindi copiare i dischi rigidi virtuali di hello tooa account di archiviazione Premium, quindi ridistribuire macchina hello in un nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="70a8a-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="70a8a-394">Aggiornare listener hello e quindi eseguire il failback.</span><span class="sxs-lookup"><span data-stu-id="70a8a-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="70a8a-395">Punti dei tempi di inattività</span><span class="sxs-lookup"><span data-stu-id="70a8a-395">Points of downtime</span></span>
<span data-ttu-id="70a8a-396">tempo di inattività Hello è costituito da toofailover toohello alternativa controller di dominio di hello tempo e viceversa.</span><span class="sxs-lookup"><span data-stu-id="70a8a-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="70a8a-397">Dipende anche dalla configurazione del client/DNS e potrebbe determinare un ritardo della riconnessione del client.</span><span class="sxs-lookup"><span data-stu-id="70a8a-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="70a8a-398">Prendere in considerazione hello seguente esempio di una configurazione ibrida Always On:</span><span class="sxs-lookup"><span data-stu-id="70a8a-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="70a8a-400">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="70a8a-400">Advantages</span></span>
* <span data-ttu-id="70a8a-401">È possibile utilizzare l'infrastruttura esistente.</span><span class="sxs-lookup"><span data-stu-id="70a8a-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="70a8a-402">È necessario innanzitutto hello toopre-aggiornamento di hello opzione di archiviazione di Azure nel controller di dominio di ripristino di emergenza Azure hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="70a8a-403">è possibile riconfigurare Hello archiviazione di ripristino di emergenza Azure controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="70a8a-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="70a8a-404">Esiste un minimo di due failover durante la migrazione, esclusi i failover di test.</span><span class="sxs-lookup"><span data-stu-id="70a8a-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="70a8a-405">Non è necessario toomove dati di SQL Server con backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="70a8a-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="70a8a-406">Svantaggi:</span><span class="sxs-lookup"><span data-stu-id="70a8a-406">Disadvantages</span></span>
* <span data-ttu-id="70a8a-407">A seconda di tooSQL di accesso client Server, potrebbe esserci un aumento della latenza durante l'esecuzione di SQL Server in un'applicazione di toohello controller di dominio alternativa.</span><span class="sxs-lookup"><span data-stu-id="70a8a-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="70a8a-408">Hello copia di dischi rigidi virtuali tooPremium archiviazione potrebbe richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="70a8a-409">Ciò potrebbe influenzare la decisione su se tookeep hello nodo hello gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="70a8a-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="70a8a-410">Considerare questo aspetto quando durante la migrazione di hello eseguono carichi di lavoro a elevato utilizzo log è obbligatorio, poiché il nodo primario hello avrà tookeep hello transazioni non replicate nel log delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="70a8a-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="70a8a-411">aumentando così in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="70a8a-412">Questo scenario utilizza hello Azure **inizio AzureStorageBlobCopy** cmdlet, che è asincrono.</span><span class="sxs-lookup"><span data-stu-id="70a8a-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="70a8a-413">Non esiste alcun contratto di servizio al completamento.</span><span class="sxs-lookup"><span data-stu-id="70a8a-413">There is no SLA on completion.</span></span> <span data-ttu-id="70a8a-414">Hello orario di copie di hello cambia, anche se ciò dipende dal tempo di attesa in coda, verrà inoltre dipendono quantità hello di tootransfer di dati.</span><span class="sxs-lookup"><span data-stu-id="70a8a-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="70a8a-415">Pertanto, è sufficiente un nodo nel centro dati 2, eseguire passaggi di attenuazione nel caso in cui la copia hello richiede più tempo durante i test.</span><span class="sxs-lookup"><span data-stu-id="70a8a-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="70a8a-416">Ad esempio hello seguenti idee.</span><span class="sxs-lookup"><span data-stu-id="70a8a-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="70a8a-417">Aggiungere un nodo SQL 2nd temporaneo per la disponibilità elevata prima della migrazione hello concordata tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="70a8a-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="70a8a-418">Eseguire la migrazione di hello di fuori di manutenzione pianificata di Azure.</span><span class="sxs-lookup"><span data-stu-id="70a8a-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="70a8a-419">Assicurarsi di che avere configurato correttamente il quorum del cluster.</span><span class="sxs-lookup"><span data-stu-id="70a8a-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="70a8a-420">Questo scenario si presuppone di aver documentato l'installazione e conoscere la modalità di mapping di archiviazione hello modifiche toomake ordine per le impostazioni della cache del disco ottimali.</span><span class="sxs-lookup"><span data-stu-id="70a8a-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="70a8a-421">Procedure generali</span><span class="sxs-lookup"><span data-stu-id="70a8a-421">High-level steps</span></span>
![MultiSite2][10]

* <span data-ttu-id="70a8a-423">Rendere hello locale / alternativo hello Azure controller di dominio primario di SQL Server e renderlo hello altri Partner di Failover automatico (AFP).</span><span class="sxs-lookup"><span data-stu-id="70a8a-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="70a8a-424">Raccogliere informazioni di configurazione disco SQL2 e Rimuovi nodo hello (non eliminare i dischi rigidi virtuali collegati).</span><span class="sxs-lookup"><span data-stu-id="70a8a-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="70a8a-425">Creare un account di archiviazione Premium e copiare i dischi rigidi virtuali da hello account di archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="70a8a-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="70a8a-426">Creare un nuovo servizio cloud e creare hello SQL2 VM con i dischi di archiviazione premi associati.</span><span class="sxs-lookup"><span data-stu-id="70a8a-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="70a8a-427">Configurare ILB/ELB e aggiungere gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="70a8a-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="70a8a-428">Hello aggiornamento sempre sul Listener con nuovo bilanciamento del carico interno / ELB IP indirizzo e il failover.</span><span class="sxs-lookup"><span data-stu-id="70a8a-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="70a8a-429">Controllare la configurazione DNS hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="70a8a-430">Modificare hello AFP tooSQL2, eseguire la migrazione di SQL1 ed eseguire i passaggi 2-5.</span><span class="sxs-lookup"><span data-stu-id="70a8a-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="70a8a-431">Testare i failover.</span><span class="sxs-lookup"><span data-stu-id="70a8a-431">Test failovers.</span></span>
* <span data-ttu-id="70a8a-432">Passare tooSQL1 indietro hello AFP e SQL2</span><span class="sxs-lookup"><span data-stu-id="70a8a-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="70a8a-433">Appendice: La migrazione di un tooPremium sempre sul Cluster multisito archiviazione</span><span class="sxs-lookup"><span data-stu-id="70a8a-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="70a8a-434">resto Hello di questo argomento fornisce un esempio dettagliato di conversione di un archivio per multisito AlwaysOn cluster tooPremium.</span><span class="sxs-lookup"><span data-stu-id="70a8a-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="70a8a-435">Converte inoltre hello Listener dall'utilizzo di bilanciamento del carico interno un carico esterno (ELB) del servizio di bilanciamento tooan (ILB).</span><span class="sxs-lookup"><span data-stu-id="70a8a-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="70a8a-436">Environment</span><span class="sxs-lookup"><span data-stu-id="70a8a-436">Environment</span></span>
* <span data-ttu-id="70a8a-437">Windows 2K12 /SQL 2K12</span><span class="sxs-lookup"><span data-stu-id="70a8a-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="70a8a-438">1 File DB su SP</span><span class="sxs-lookup"><span data-stu-id="70a8a-438">1 DB Files on SP</span></span>
* <span data-ttu-id="70a8a-439">2 pool di archiviazione per ogni nodo</span><span class="sxs-lookup"><span data-stu-id="70a8a-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="70a8a-441">VM:</span><span class="sxs-lookup"><span data-stu-id="70a8a-441">VM:</span></span>
<span data-ttu-id="70a8a-442">In questo esempio verrà toodemonstrate lo spostamento da un tooILB ELB.</span><span class="sxs-lookup"><span data-stu-id="70a8a-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="70a8a-443">Viene illustrato come toothis tooswitch durante hello migrazione ELB era disponibile prima di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="70a8a-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="70a8a-445">I passaggi precedenti: Connettersi tooSubscription</span><span class="sxs-lookup"><span data-stu-id="70a8a-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="70a8a-446">Passaggio 1: Creare un nuovo account di archiviazione e servizio cloud</span><span class="sxs-lookup"><span data-stu-id="70a8a-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="70a8a-447">Passaggio 2: Hello aumento consentito errori sulle risorse<Optional></span><span class="sxs-lookup"><span data-stu-id="70a8a-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="70a8a-448">In alcune risorse appartenenti al gruppo di disponibilità AlwaysOn tooyour esistono limiti il numero di errori che può verificarsi in un periodo, in cui il servizio cluster hello tenterà gruppo di risorse toorestart hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="70a8a-449">È consigliabile che aumentare questo al contempo scorrere tramite questa procedura, poiché in caso contrario manualmente failover failover e trigger arrestando macchine si può ottenere il limite di toothis Chiudi.</span><span class="sxs-lookup"><span data-stu-id="70a8a-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="70a8a-450">Potrebbe essere consentito di errore hello prudente toodouble, toodo in Gestione Cluster di Failover, vedere toohello proprietà hello sempre nel gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="70a8a-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="70a8a-452">Modificare hello too6 numero massimo di errori.</span><span class="sxs-lookup"><span data-stu-id="70a8a-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="70a8a-453">Passaggio 3: Aggiungere la risorsa indirizzo IP per il gruppo di cluster <Optional></span><span class="sxs-lookup"><span data-stu-id="70a8a-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="70a8a-454">Se si dispone di un solo indirizzo IP per il gruppo di Cluster hello e la subnet cloud toohello allineato, tenere presente, se si accidentalmente portare offline tutti i nodi del cluster nel cloud hello che rete quindi risorsa indirizzo IP del Cluster hello e nome di rete Cluster non saranno in grado di toocome in linea.</span><span class="sxs-lookup"><span data-stu-id="70a8a-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="70a8a-455">In hello evento di questo che eviterà Aggiorna tooother risorse del cluster.</span><span class="sxs-lookup"><span data-stu-id="70a8a-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="70a8a-456">Passaggio 4: Eseguire la configurazione di DNS</span><span class="sxs-lookup"><span data-stu-id="70a8a-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="70a8a-457">tooimplement una transizione uniforme dipende dalla modalità DNS viene usato e aggiornato.</span><span class="sxs-lookup"><span data-stu-id="70a8a-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="70a8a-458">Quando viene installato Always On, viene creato un gruppo di risorse Cluster di Windows, se si apre Gestione Cluster di Failover, si noterà che almeno avrà tre risorse, hello due che hello documento fa riferimento tooare:</span><span class="sxs-lookup"><span data-stu-id="70a8a-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="70a8a-459">Nome di rete virtuale (VNN) – si tratta hello DNS nome client connettersi toowhen che desiderano tooconnect tooSQL server tramite Always On.</span><span class="sxs-lookup"><span data-stu-id="70a8a-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="70a8a-460">Risorsa indirizzo IP: si tratta di indirizzi IP associato alla hello VNN hello, è possibile avere più e sarà necessario un indirizzo IP per ogni sito e subnet in una configurazione multisito.</span><span class="sxs-lookup"><span data-stu-id="70a8a-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="70a8a-461">Quando si recupera i record DNS hello associato listener hello, provare tooconnect tooeach tooSQL connessione Server, il driver di SQL Server Client hello Always On associato l'indirizzo IP, seguito prende in esame alcuni fattori che possono influenzare questo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="70a8a-462">Hello numero di record DNS simultanee associati con il nome del listener hello dipende non solo il numero di hello di indirizzi IP associati, ma hello ' RegisterAllIpProviders'setting nel Clustering di Failover per la risorsa nome di rete virtuale ON sempre hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="70a8a-463">Quando si distribuisce Always On in Azure sono disponibili diversi passaggi toocreate hello Listener e gli indirizzi IP, si dispone di toomanually configurare too1 'RegisterAllIpProviders' hello, si tratta di diversi tooan distribuzione sempre in locale in cui è già impostato too1.</span><span class="sxs-lookup"><span data-stu-id="70a8a-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="70a8a-464">Se 'RegisterAllIpProviders' è 0, viene visualizzata solo un record DNS nel DNS associato hello Listener:</span><span class="sxs-lookup"><span data-stu-id="70a8a-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="70a8a-466">Se 'RegisterAllIpProviders' è 1:</span><span class="sxs-lookup"><span data-stu-id="70a8a-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="70a8a-468">codice Hello riportato di seguito verrà eseguire il dump di hello le impostazioni di nome di rete virtuale e impostarlo per l'utente, si noti che per hello tootake effetto occorrerà tootake hello VNN offline e attivare di nuovo online, questa acquisire hello offline che causa interruzioni di connettività client Listener.</span><span class="sxs-lookup"><span data-stu-id="70a8a-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="70a8a-469">In un passaggio successivo di migrazione sarà necessario tooupdate hello Always On listener con un indirizzo IP aggiornato che fa riferimento un servizio di bilanciamento del carico, questo comporta un rimozione della risorsa indirizzo IP e l'aggiunta.</span><span class="sxs-lookup"><span data-stu-id="70a8a-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="70a8a-470">Dopo l'aggiornamento IP hello, è necessario tooensure hello nuovo indirizzo IP è stato aggiornato nella zona DNS e che i client hello Aggiorna cache DNS locale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="70a8a-471">Se i client si trovano in un segmento di rete diversa e fanno riferimento a un altro server DNS, è necessario tooconsider conseguenze sui trasferimenti di zona DNS durante la migrazione di hello, hello applicazione si riconnettono ora sarà vincolato dal hello almeno il tempo di trasferimento zona di eventuali nuovi indirizzi IP per il listener hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="70a8a-472">Se si è nel vincolo di tempo in questo caso, è consigliabile discutere e testare l'utilizzo forzato di un trasferimento di zona incrementale con i team di Windows, e anche inserire hello DNS tooa record host tooLive TTL (Time), ridurre in modo da aggiornano i client hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="70a8a-473">Per ulteriori informazioni, vedere [Trasferimenti di zona incrementali](https://technet.microsoft.com/library/cc958973.aspx) e [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="70a8a-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="70a8a-474">Impostazione hello predefinito durata (TTL) per i Record DNS associato hello Listener Always On in Azure è 1200 secondi.</span><span class="sxs-lookup"><span data-stu-id="70a8a-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="70a8a-475">È possibile tooreduce in questo caso nel vincolo di tempo durante l'aggiornamento client di migrazione tooensure hello relativi nomi con IP hello aggiornato l'indirizzo per il listener hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="70a8a-476">È possibile visualizzare e modificare la configurazione di hello eseguendo il dump out configurazione hello di hello VNN:</span><span class="sxs-lookup"><span data-stu-id="70a8a-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="70a8a-477">Si noti, hello inferiore hello 'HostRecordTTL', si verificherà una maggiore quantità di traffico DNS.</span><span class="sxs-lookup"><span data-stu-id="70a8a-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="70a8a-478">Impostazioni applicazione client</span><span class="sxs-lookup"><span data-stu-id="70a8a-478">Client application settings</span></span>
<span data-ttu-id="70a8a-479">Se supportate dall'applicazione client SQL hello .net 4.5 SQLClient, sarà possibile usare ' MULTISUBNETFAILOVER = TRUE' (parola chiave), questa opzione è consigliata toobe applicato, che consente di tooSQL connessione più veloce gruppo di disponibilità AlwaysOn durante il failover.</span><span class="sxs-lookup"><span data-stu-id="70a8a-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="70a8a-480">Enumera tutti gli indirizzi IP associati hello Always On listener in parallelo ed esegue una velocità di tentativi di connessione TCP più aggressiva durante un failover.</span><span class="sxs-lookup"><span data-stu-id="70a8a-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="70a8a-481">Per ulteriori informazioni sulla hello impostazioni indicate sopra, vedere [parola chiave MultiSubnetFailover e funzionalità associate](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="70a8a-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="70a8a-482">Vedere anche [Supporto SqlClient per disponibilità elevata, ripristino di emergenza](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="70a8a-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="70a8a-483">Passaggio 5: Impostare il quorum del cluster</span><span class="sxs-lookup"><span data-stu-id="70a8a-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="70a8a-484">Come si intende toobe richiede almeno un server SQL verso il basso alla volta, è necessario modificare impostazione del quorum del cluster hello, con 2 nodi di controllo di condivisione File (FSW), è necessario impostare maggioranza dei nodi di hello quorum tooallow e utilizzare il voto dinamico, se si tratta di tooallow per condizione tooremain un singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="70a8a-485">Per ulteriori informazioni sulla gestione e la configurazione quorum del cluster hello, vedere [configurare e gestire il Quorum in un Cluster di Failover di Windows Server 2012 di hello](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="70a8a-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="70a8a-486">Passaggio 6: Estrarre endpoint e ACL esistenti</span><span class="sxs-lookup"><span data-stu-id="70a8a-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="70a8a-487">Salvare questi file di testo tooa.</span><span class="sxs-lookup"><span data-stu-id="70a8a-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="70a8a-488">Passaggio 7: Modificare i partner di failover e le modalità di replica</span><span class="sxs-lookup"><span data-stu-id="70a8a-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="70a8a-489">Se si dispone di più di 2 istanze di SQL Server, è necessario impostare failover hello di un'altra replica secondaria in un altro controller di dominio o 'too'Synchronous on-premise e renderlo un Partner di Failover automatico (AFP), in modo da mantenere a disponibilità elevata, mentre si apportano modifiche.</span><span class="sxs-lookup"><span data-stu-id="70a8a-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="70a8a-490">A tale scopo, è possibile utilizzare TSQL o SSMS:</span><span class="sxs-lookup"><span data-stu-id="70a8a-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="70a8a-492">Passaggio 8: Rimuovere la VM secondaria dal servizio cloud</span><span class="sxs-lookup"><span data-stu-id="70a8a-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="70a8a-493">Si consiglia di pianificare toomigrate un nodo secondario del cloud in primo luogo, se si tratta attualmente primario, si deve avviare un failover manuale.</span><span class="sxs-lookup"><span data-stu-id="70a8a-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="70a8a-494">Passaggio 9: Modificare le impostazioni di caching del disco nel file CSV e salvare</span><span class="sxs-lookup"><span data-stu-id="70a8a-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="70a8a-495">Per i volumi di dati questi deve essere impostati tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="70a8a-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="70a8a-496">Per i volumi TLOG questi deve essere impostati tooNONE.</span><span class="sxs-lookup"><span data-stu-id="70a8a-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="70a8a-498">Passaggio 10: Copiare i dischi rigidi virtuali</span><span class="sxs-lookup"><span data-stu-id="70a8a-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="70a8a-499">È possibile controllare lo stato di copia hello di hello dischi rigidi virtuali toohello account di archiviazione Premium:</span><span class="sxs-lookup"><span data-stu-id="70a8a-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="70a8a-501">Attendere che tutto venga registrato come esito positivo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="70a8a-502">Per informazioni per i singoli BLOB:</span><span class="sxs-lookup"><span data-stu-id="70a8a-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="70a8a-503">Passaggio 11: Registrare un disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="70a8a-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="70a8a-504">Passaggio 12: Importare la replica secondaria nel nuovo servizio cloud</span><span class="sxs-lookup"><span data-stu-id="70a8a-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="70a8a-505">codice Hello seguito anche aggiunto di hello utilizza opzione qui è possibile importare la macchina hello e utilizzare hello retainable VIP.</span><span class="sxs-lookup"><span data-stu-id="70a8a-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="70a8a-506">Passaggio 13: Creare il servizio ILB sul nuovo Svc cloud, aggiungere endpoint a carico bilanciato e ACL</span><span class="sxs-lookup"><span data-stu-id="70a8a-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="70a8a-507">Passaggio 14: Aggiornare AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="70a8a-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="70a8a-509">Rimuovere il servizio di cloud precedente hello indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="70a8a-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="70a8a-511">Passaggio 15: Eseguire il controllo dell'aggiornamento DNS</span><span class="sxs-lookup"><span data-stu-id="70a8a-511">Step 15: DNS update check</span></span>
<span data-ttu-id="70a8a-512">È ora necessario controllare i server DNS di una rete di client di SQL Server e assicurarsi che il servizio cluster sia aggiunto hello record host aggiuntivi per hello aggiunta indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="70a8a-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="70a8a-513">Se i server DNS non sono aggiornate, è possibile forzare un trasferimento di zona DNS e verificare che i client nella subnet sono hello sono in grado di tooresolve tooboth sempre su indirizzi IP, in tal caso non è necessario toowait per la replica automatica DNS.</span><span class="sxs-lookup"><span data-stu-id="70a8a-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="70a8a-514">Passaggio 16: Riconfigurare Always On</span><span class="sxs-lookup"><span data-stu-id="70a8a-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="70a8a-515">A questo punto è attendere hello secondario tale nodo che è stato migrato toofully risincronizzare con nodo locale hello e passa il nodo di replica toosynchronous e renderlo AFP hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="70a8a-516">Passaggio 17: Eseguire la migrazione del secondo nodo</span><span class="sxs-lookup"><span data-stu-id="70a8a-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="70a8a-517">Passaggio 18: Modificare le impostazioni di caching del disco nel file CSV e salvare</span><span class="sxs-lookup"><span data-stu-id="70a8a-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="70a8a-518">Per i volumi di dati questi deve essere impostati tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="70a8a-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="70a8a-519">Per i volumi TLOG questi deve essere impostati tooNONE.</span><span class="sxs-lookup"><span data-stu-id="70a8a-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="70a8a-521">Passaggio 19: Creare nuovi account di archiviazione indipendente per il nodo secondario</span><span class="sxs-lookup"><span data-stu-id="70a8a-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="70a8a-522">Passaggio 20: Copiare i dischi rigidi virtuali</span><span class="sxs-lookup"><span data-stu-id="70a8a-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="70a8a-523">È possibile controllare lo stato di copia di hello disco rigido virtuale per tutti i dischi rigidi virtuali: ForEach ($disk in $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. EtichettaDisco $diskName = $disk. DiskName</span><span class="sxs-lookup"><span data-stu-id="70a8a-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="70a8a-525">Attendere che tutto venga registrato come esito positivo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="70a8a-526">Per informazioni per i singoli BLOB:</span><span class="sxs-lookup"><span data-stu-id="70a8a-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="70a8a-527">Passaggio 21: Registrare il disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="70a8a-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="70a8a-528">Passaggio 22: Aggiungere endpoint con carico bilanciato e ACL</span><span class="sxs-lookup"><span data-stu-id="70a8a-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="70a8a-529">Passaggio 23: Eseguire il failover di test</span><span class="sxs-lookup"><span data-stu-id="70a8a-529">Step 23: Test failover</span></span>
<span data-ttu-id="70a8a-530">A questo punto, è consigliabile consentire nodo migrati hello sincronizzare con hello on-premise sempre nel nodo, posizionare il report in modalità di replica toosynchronous e attendere fino a quando viene sincronizzata.</span><span class="sxs-lookup"><span data-stu-id="70a8a-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="70a8a-531">Quindi il failover da locale toohello primo nodo migrato, ovvero AFP hello.</span><span class="sxs-lookup"><span data-stu-id="70a8a-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="70a8a-532">Una volta che ha funzionato, hello modifica ultima migrazione AFP toohello nodo.</span><span class="sxs-lookup"><span data-stu-id="70a8a-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="70a8a-533">È consigliabile i failover tra tutti i nodi di test ed eseguire se test chaos failover tooensure funziona come previsto e in un tempo indicato.</span><span class="sxs-lookup"><span data-stu-id="70a8a-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="70a8a-534">Passaggio 24: Ripristinare le impostazioni quorum del cluster / TTL DNS / Failover Pntrs / impostazioni di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="70a8a-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="70a8a-535">Aggiunta della risorsa indirizzo IP nella stessa Subnet</span><span class="sxs-lookup"><span data-stu-id="70a8a-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="70a8a-536">Se si dispone solo 2 istanze di SQL Server e che si desidera toomigrate li tooa nuovo servizio cloud, ma si desidera tookeep su hello stessa subnet, è possibile evitare di creare listener hello originale di hello toodelete offline sempre l'indirizzo IP e aggiungere hello nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="70a8a-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="70a8a-537">Se si esegue la migrazione di subnet di tooanother hello macchine virtuali non è necessario toodo questo come sarà presente una rete di cluster aggiuntivo che farà riferimento a subnet.</span><span class="sxs-lookup"><span data-stu-id="70a8a-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="70a8a-538">Dopo aver spostato hello eseguita la migrazione di database secondario e aggiunto nella nuova risorsa indirizzo IP hello per nuovo servizio cloud di hello prima failover hello primario esistente, è necessario eseguire la procedura all'interno di hello gestione Cluster di Failover:</span><span class="sxs-lookup"><span data-stu-id="70a8a-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="70a8a-539">tooadd nell'indirizzo IP, vedere hello [appendice](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), passaggio 14.</span><span class="sxs-lookup"><span data-stu-id="70a8a-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="70a8a-540">Per la risorsa indirizzo IP corrente di hello, modificare hello possibile proprietario too'Existing Server SQL primario ', nell'esempio riportato di seguito, 'dansqlams4' hello:</span><span class="sxs-lookup"><span data-stu-id="70a8a-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="70a8a-542">Per la nuova risorsa indirizzo IP di hello, modificare hello possibile proprietario too'Migrated secondaria SQL Server ", nell'esempio riportato di seguito, 'dansqlams5' hello:</span><span class="sxs-lookup"><span data-stu-id="70a8a-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="70a8a-544">Dopo aver impostato questo è possibile eseguire il failover, e quando viene eseguita la migrazione dell'ultimo nodo hello hello possibili proprietari possono essere modificati in modo tale nodo viene aggiunto come possibile proprietario:</span><span class="sxs-lookup"><span data-stu-id="70a8a-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="70a8a-546">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="70a8a-546">Additional resources</span></span>
* [<span data-ttu-id="70a8a-547">Archiviazione Premium di Azure</span><span class="sxs-lookup"><span data-stu-id="70a8a-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="70a8a-548">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="70a8a-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="70a8a-549">SQL Server in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="70a8a-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
