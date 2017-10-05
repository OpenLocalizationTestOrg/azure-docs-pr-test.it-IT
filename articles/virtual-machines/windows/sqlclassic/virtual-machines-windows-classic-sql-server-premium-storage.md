---
title: Usare Archiviazione Premium di Azure con SQL Server | Microsoft Docs
description: Questo articolo sfrutta le risorse create con il modello di distribuzione classica e fornisce istruzioni su come utilizzare Archiviazione Premium di Azure con SQL Server in esecuzione su Macchine virtuali di Azure.
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
ms.openlocfilehash: 6790db207fc7ec8a4b1546ef07c97ef30abe9513
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="ecc6b-103">Utilizzare Archiviazione Premium di Azure con SQL Server in macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="ecc6b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ecc6b-104">Overview</span></span>
<span data-ttu-id="ecc6b-105">[Archiviazione Premium di Azure](../../../storage/common/storage-premium-storage.md) è la risorsa di archiviazione di nuova generazione che fornisce bassa latenza e I/O ad alta velocità.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="ecc6b-106">Funziona al meglio per i carichi di lavoro con numerose operazioni di I/O, ad esempio SQL Server in [macchine virtuali](https://azure.microsoft.com/services/virtual-machines/)IaaS.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecc6b-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ecc6b-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ecc6b-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="ecc6b-110">In questo articolo sono fornite indicazioni per la migrazione di una macchina virtuale che esegue SQL Server per l’uso di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span></span> <span data-ttu-id="ecc6b-111">Sono inclusi i passaggi relativi all'infrastruttura di Azure (rete, archiviazione) e alle macchine virtuali guest di Windows.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="ecc6b-112">Nell'esempio incluso nell' [Appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) viene mostrata una migrazione end-to-end completa in cui le VM più grandi vengono spostate per sfruttare i vantaggi dell'archiviazione SSD locale migliorata con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-112">The example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="ecc6b-113">È importante comprendere il processo end-to-end di utilizzo di Archiviazione Premium di Azure con SQL Server in macchine virtuali IAAS.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="ecc6b-114">Sono inclusi:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-114">This includes:</span></span>

* <span data-ttu-id="ecc6b-115">Identificazione dei prerequisiti per l'utilizzo di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-115">Identification of the prerequisites to use Premium Storage.</span></span>
* <span data-ttu-id="ecc6b-116">Esempi di distribuzione di SQL Server su IaaS in Archiviazione Premium per nuove distribuzioni</span><span class="sxs-lookup"><span data-stu-id="ecc6b-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span></span>
* <span data-ttu-id="ecc6b-117">Esempi di migrazione delle distribuzioni esistenti, sia di server autonomi che distribuzioni tramite gruppi di disponibilità di SQL AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="ecc6b-118">Approcci di migrazione possibili.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-118">Possible migration approaches.</span></span>
* <span data-ttu-id="ecc6b-119">Esempio end-to-end completo che mostra i passaggi di Azure, Windows e SQL Server per la migrazione di un'implementazione di AlwaysOn esistente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span></span>

<span data-ttu-id="ecc6b-120">Per ottenere le informazioni più esaustive sull'uso di SQL Server in Macchine virtuali di Azure, vedere [SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="ecc6b-121">**Autore:** Daniel Sol **Revisori tecnici:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="ecc6b-122">Prerequisiti per Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="ecc6b-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="ecc6b-123">Esistono diversi prerequisiti per l'utilizzo di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="ecc6b-124">Dimensioni della macchina</span><span class="sxs-lookup"><span data-stu-id="ecc6b-124">Machine size</span></span>
<span data-ttu-id="ecc6b-125">Per utilizzare Archiviazione Premium occorre usare macchine virtuali (VM) serie DS.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-125">For using Premium Storage you will need to use DS series Virtual Machines (VM).</span></span> <span data-ttu-id="ecc6b-126">Se in precedenza non sono state utilizzate macchine serie DS nel servizio cloud, è necessario eliminare la macchina virtuale esistente, mantenere i dischi collegati e creare quindi un nuovo servizio cloud prima di ricreare la macchina virtuale con dimensioni del ruolo DS*.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS* role size.</span></span> <span data-ttu-id="ecc6b-127">Per ulteriori informazioni sulle dimensioni della macchine virtuali, vedere [Dimensioni delle macchine virtuali e dei servizi cloud per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="ecc6b-128">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="ecc6b-128">Cloud services</span></span>
<span data-ttu-id="ecc6b-129">È possibile utilizzare le macchine virtuali DS* con Archiviazione Premium solo quando vengono create in un nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="ecc6b-130">Se si usa SQL Server AlwaysOn in Azure, il listener AlwaysOn farà riferimento all'indirizzo IP del servizio di bilanciamento del carico interno o esterno di Azure associato a un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-130">If you are using SQL Server Always On in Azure, the Always On Listener will refer to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="ecc6b-131">In questo articolo viene illustrato come eseguire la migrazione mantenendo la disponibilità in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-131">This article focuses on how to migrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc6b-132">Una macchina virtuale serie DS* deve essere la prima macchina virtuale distribuita nel nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-132">A DS* Series must be the first VM that is deployed to the new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="ecc6b-133">Reti virtuali regionali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-133">Regional VNETS</span></span>
<span data-ttu-id="ecc6b-134">Per le macchine virtuali DS* è necessario configurare la rete virtuale (VNET) che ospita le macchine virtuali regionali.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-134">For DS* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span></span> <span data-ttu-id="ecc6b-135">In tal modo si "amplia" la rete virtuale per consentire il provisioning delle macchine virtuali più grandi in altri cluster e permettere la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="ecc6b-136">Nella schermata seguente, la posizione evidenziata mostra le VNET regionali, mentre il primo risultato mostra una rete virtuale limitata.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="ecc6b-138">È possibile generare un ticket di supporto Microsoft per eseguire la migrazione a una rete virtuale regionale.  Microsoft apporterà una modifica, quindi per completare la migrazione alle reti virtuali regionali sarà necessario modificare la proprietà AffinityGroup nella configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-138">You can raise a Microsoft support ticket to migrate to a regional VNET, Microsoft will make a change, then to complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span></span> <span data-ttu-id="ecc6b-139">Esportare innanzitutto la configurazione di rete in PowerShell, quindi sostituire la proprietà **AffinityGroup** nell’elemento **VirtualNetworkSite** con una proprietà **Location**.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-139">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="ecc6b-140">Specificare `Location = XXXX` dove `XXXX` è un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="ecc6b-141">Importare quindi la nuova configurazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-141">Then import the new configuration.</span></span>

<span data-ttu-id="ecc6b-142">Ad esempio, prendere in considerazione la seguente configurazione di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-142">For example, considering the following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="ecc6b-143">Per spostarla in una rete virtuale regionale in Europa occidentale, modificare la configurazione come segue:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-143">To move this to a regional VNET in West Europe, change the configuration to the following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="ecc6b-144">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ecc6b-144">Storage accounts</span></span>
<span data-ttu-id="ecc6b-145">Occorre creare un nuovo account di archiviazione configurato per Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-145">You will need to create a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="ecc6b-146">Si noti che l'utilizzo di Archiviazione Premium è impostato sull’account di archiviazione, non sui singoli dischi rigidi virtuali. Tuttavia, quando si utilizza una macchina virtuale serie DS* è possibile collegare i dischi rigidi virtuali dagli account di archiviazione Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-146">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="ecc6b-147">Se non si desidera collocare il disco rigido virtuale del sistema operativo sull'account di Archiviazione Premium, è possibile valutare questa possibilità.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-147">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span></span>

<span data-ttu-id="ecc6b-148">Il seguente comando **New-AzureStorageAccountPowerShell** con **Type** "Premium_LRS" consente di creare un account di Archiviazione Premium:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-148">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="ecc6b-149">Impostazioni della cache di dischi rigidi virtuali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-149">VHDs Cache Settings</span></span>
<span data-ttu-id="ecc6b-150">La differenza principale con la creazione di dischi che fanno parte di un account di Archiviazione Premium è l'impostazione della cache su disco.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-150">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span></span> <span data-ttu-id="ecc6b-151">Per i dischi del volume di dati di SQL Server, è consigliabile usare "**Read Caching**".</span><span class="sxs-lookup"><span data-stu-id="ecc6b-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="ecc6b-152">Per i volumi del log delle transazioni, l'impostazione della cache su disco deve essere "**None**".</span><span class="sxs-lookup"><span data-stu-id="ecc6b-152">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span></span> <span data-ttu-id="ecc6b-153">Questa impostazione differisce da quelle consigliate per gli account di archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-153">This is different from the recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="ecc6b-154">Dopo aver collegato i dischi rigidi virtuali, l'impostazione della cache non può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-154">Once the VHDs have been attached, the cache setting cannot be altered.</span></span> <span data-ttu-id="ecc6b-155">È necessario scollegare e ricollegare il disco rigido virtuale con un'impostazione di cache aggiornata.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-155">You would need to detach and reattach the VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="ecc6b-156">Spazi di archiviazione di Windows</span><span class="sxs-lookup"><span data-stu-id="ecc6b-156">Windows storage spaces</span></span>
<span data-ttu-id="ecc6b-157">È possibile utilizzare [Spazi di archiviazione Windows](https://technet.microsoft.com/library/hh831739.aspx) come è avvenuto con la precedente Archiviazione Standard; questo consentirà di eseguire la migrazione di una macchina virtuale che già utilizza Spazi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you to migrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="ecc6b-158">Nell'esempio riportato in [Appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (passaggio 9 e successivi) viene illustrato il codice di Powershell per estrarre e importare una macchina virtuale con più dischi rigidi virtuali collegati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-158">The example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="ecc6b-159">Sono stati utilizzati pool di archiviazione con account di archiviazione Azure Standard per migliorare la velocità effettiva e ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-159">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span></span> <span data-ttu-id="ecc6b-160">Può essere utile testare i pool di archiviazione con Archiviazione Premium per le nuove distribuzioni, ma l’impostazione dell’archiviazione aggiunge ulteriore complessità.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-to-find-which-azure-virtual-disks-map-to-storage-pools"></a><span data-ttu-id="ecc6b-161">Come individuare quali dischi virtuali di Azure sono mappati ai pool di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ecc6b-161">How to find which Azure Virtual Disks map to storage pools</span></span>
<span data-ttu-id="ecc6b-162">Poiché esistono diverse indicazioni di impostazione della cache per i dischi rigidi virtuali collegati, è possibile copiare i dischi rigidi virtuali in un account di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-162">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span></span> <span data-ttu-id="ecc6b-163">Tuttavia, quando vengono ricollegati alla nuova macchina virtuale serie DS, è necessario modificare le impostazioni della cache.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-163">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span></span> <span data-ttu-id="ecc6b-164">È più semplice applicare le impostazioni della cache di Archiviazione Premium consigliate quando si dispone di dischi rigidi virtuali separati per i file di dati SQL e file di log (anziché di un singolo disco rigido virtuale che contiene entrambi).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-164">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="ecc6b-165">Se si dispone di file di log e dati di SQL Server nello stesso volume, l'opzione di memorizzazione nella cache da scegliere dipende dai modelli di accesso I/O per i carichi di lavoro del database.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-165">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span></span> <span data-ttu-id="ecc6b-166">Solo i test possono dimostrare quale opzione di memorizzazione nella cache è più adatta a questo scenario.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="ecc6b-167">Tuttavia, se si usano spazi di archiviazione di Windows costituiti da più VHD, è necessario esaminare gli script originali per identificare quali VHD collegati si trovano in un pool specifico in modo da poter impostare adeguatamente la cache per ogni disco.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span></span>

<span data-ttu-id="ecc6b-168">Se non è disponibile lo script originale che mostra quali dischi rigidi virtuali sono mappati al pool di archiviazione, è possibile utilizzare la procedura seguente per determinare il mapping tra disco e pool di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-168">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span></span>

<span data-ttu-id="ecc6b-169">Per ogni disco, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-169">For each disk, use the following steps:</span></span>

1. <span data-ttu-id="ecc6b-170">Ottenere l’elenco di dischi collegati alla macchina virtuale con il comando **Get-AzureVM** :</span><span class="sxs-lookup"><span data-stu-id="ecc6b-170">Get list of disks attached to VM with the **Get-AzureVM** command:</span></span>

    <span data-ttu-id="ecc6b-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="ecc6b-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="ecc6b-172">Prendere nota del nome del disco e del LUN.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-172">Note the Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="ecc6b-174">Desktop remoto nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-174">Remote desktop into the VM.</span></span> <span data-ttu-id="ecc6b-175">Passare quindi a **Gestione computer** | **Gestione dispositivi** | **Unità disco**.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-175">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="ecc6b-176">Esaminare le proprietà di ciascun ’Disco virtuale Microsoft’</span><span class="sxs-lookup"><span data-stu-id="ecc6b-176">Look at the properties of each of the ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="ecc6b-178">Il numero LUN è un riferimento al numero LUN specificato al momento del collegamento del disco rigido virtuale alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-178">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span></span>
5. <span data-ttu-id="ecc6b-179">Per il "Disco virtuale Microsoft" andare alla scheda **Dettagli**, quindi nell’elenco **Proprietà** andare a **Chiave driver**.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-179">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span></span> <span data-ttu-id="ecc6b-180">In **Valore**, notare l'**Offset**, ovvero 0002 nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-180">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span></span> <span data-ttu-id="ecc6b-181">Il valore 0002 denota PhysicalDisk2 a cui fa riferimento il pool di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-181">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="ecc6b-183">Per ogni del pool di archiviazione eseguire il dump dei dischi associati:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-183">For each storage pool, dump out the associated disks:</span></span>

    <span data-ttu-id="ecc6b-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="ecc6b-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="ecc6b-186">Ora è possibile utilizzare queste informazioni per collegare i dischi rigidi virtuali collegati ai dischi fisici nei pool di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-186">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span></span>

<span data-ttu-id="ecc6b-187">Una volta eseguito il mapping dei dischi rigidi virtuali ai dischi fisici nei pool di archiviazione è possibile scollegarli e copiarli su un account di Archiviazione Premium e quindi collegarli con l'impostazione corretta della cache.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-187">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span></span> <span data-ttu-id="ecc6b-188">Vedere l'esempio fornito in [Appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), passaggi da 8 a 12.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-188">Please see the example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="ecc6b-189">Questi passaggi illustrano come estrarre una configurazione di disco rigido virtuale collegato alla macchina virtuale in un file CSV, copiare i dischi rigidi virtuali, modificare le impostazioni della cache di configurazione disco e infine ridistribuire la macchina virtuale come macchina virtuale serie DS con tutti i dischi collegati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-189">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="ecc6b-190">Larghezza di banda di archiviazione della VM e velocità effettiva di archiviazione del VHD</span><span class="sxs-lookup"><span data-stu-id="ecc6b-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="ecc6b-191">Le prestazioni dell’archiviazione dipendono dalle dimensioni della macchina virtuale DS* specificate e della dimensioni del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-191">The amount of storage performance depends on the DS* VM size specified and the VHD sizes.</span></span> <span data-ttu-id="ecc6b-192">Le macchine virtuali hanno quote diverse per il numero di dischi rigidi virtuali che possono essere collegati e la larghezza di banda massima che supporteranno (MB/s).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-192">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="ecc6b-193">Per i numeri di larghezza di banda specifici, vedere [Dimensioni delle macchine virtuali e dei servizi cloud per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-193">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ecc6b-194">Input/output al secondo maggiori si ottengono con dimensioni del disco maggiori.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="ecc6b-195">Tenere conto di questa considerazione quando si decide il percorso di migrazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="ecc6b-196">Per i dettagliate [vedere la tabella per i tipi di disco e input/output al secondo](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-196">For details, [see the table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="ecc6b-197">Infine, tenere presente che le macchine virtuali supporteranno larghezza di banda massime diverse per tutti i dischi collegati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="ecc6b-198">Con un carico elevato si potrebbe saturare la larghezza di banda su disco massima disponibile per le dimensioni del ruolo di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-198">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="ecc6b-199">Ad esempio, Standard_DS14 supporterà fino a 512 MB/s. Pertanto, con tre dischi P30 si potrebbe saturare la larghezza di banda del disco della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-199">For example a Standard_DS14 will support up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span></span> <span data-ttu-id="ecc6b-200">In questo esempio, tuttavia, il limite di velocità effettiva potrebbe essere superato a seconda della combinazione di I/O di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-200">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="ecc6b-201">Nuove distribuzioni</span><span class="sxs-lookup"><span data-stu-id="ecc6b-201">New deployments</span></span>
<span data-ttu-id="ecc6b-202">Nelle due sezioni successive viene illustrato come distribuire le macchine virtuali di SQL Server in Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-202">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span></span> <span data-ttu-id="ecc6b-203">Come affermato in precedenza, non occorre necessariamente collocare il disco del sistema operativo su Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-203">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span></span> <span data-ttu-id="ecc6b-204">È possibile eseguire questa operazione se si intende posizionare i carichi di lavoro con numerose operazioni di I/O sul disco rigido virtuale del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-204">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span></span>

<span data-ttu-id="ecc6b-205">Nel primo esempio viene illustrato l'utilizzo di immagini della raccolta Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-205">The first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="ecc6b-206">Nel secondo esempio viene illustrato come utilizzare un'immagine di macchina virtuale personalizzata disponibile in un account di archiviazione Standard esistente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-206">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc6b-207">Questi esempi presuppongono che sia già stata creata una rete virtuale regionale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="ecc6b-208">Creare una nuova macchina virtuale con Archiviazione Premium con immagine della raccolta</span><span class="sxs-lookup"><span data-stu-id="ecc6b-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="ecc6b-209">Nell'esempio seguente viene illustrato come collocare il disco rigido virtuale di sistema operativo su Archiviazione Premium e collegare dischi rigidi virtuali di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-209">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="ecc6b-210">Tuttavia, è anche possibile collocare il disco del sistema operativo in un account di archiviazione Standard e quindi collegare dischi rigidi virtuali che risiedono in un account di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-210">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="ecc6b-211">Vengono illustrati entrambi gli scenari.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="ecc6b-212">Passaggio 1: Creare un account di Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="ecc6b-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="ecc6b-213">Passaggio 2: Creare un nuovo servizio cloud</span><span class="sxs-lookup"><span data-stu-id="ecc6b-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="ecc6b-214">Passaggio 3: Riservare un VIP di servizio cloud (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="ecc6b-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="ecc6b-215">Passaggio 4: Creare un contenitore di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="ecc6b-216">Passaggio 5: Collocazione del disco rigido virtuale su Archiviazione Standard o Premium </span><span class="sxs-lookup"><span data-stu-id="ecc6b-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used to place the OS VHD in

    #If you want to place the OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted to place the OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="ecc6b-217">Passaggio 6: Creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ecc6b-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from the Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember to change to DS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks to VM Config
    #Note the size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising the Premium Storage enabled Storage account

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


### <a name="create-a-new-vm-to-use-premium-storage-with-a-custom-image"></a><span data-ttu-id="ecc6b-218">Creare una nuova VM per usare Archiviazione Premium con un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="ecc6b-218">Create a new VM to use Premium Storage with a custom image</span></span>
<span data-ttu-id="ecc6b-219">Questo scenario mostra la posizione delle immagini personalizzate esistenti che risiedono in un account di Archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="ecc6b-220">Come accennato, se si desidera collocare il disco rigido virtuale del sistema operativo su Archiviazione Premium, è necessario copiare l'immagine esistente nell'account di Archiviazione Standard e trasferirlo a una Archiviazione Premium prima che possa essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-220">As mentioned if you want to place the OS VHD on Premium Storage you will need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span></span> <span data-ttu-id="ecc6b-221">Se si dispone di un'immagine locale, è possibile usare questo metodo per copiarla direttamente nell'account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-221">If you have an image on-premises, you can also use this method to copy that directly to the Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="ecc6b-222">Passaggio 1: Creare l’account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ecc6b-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="ecc6b-223">Passaggio 2: Creare il servizio cloud</span><span class="sxs-lookup"><span data-stu-id="ecc6b-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="ecc6b-224">Passaggio 3: Usare l'immagine esistente</span><span class="sxs-lookup"><span data-stu-id="ecc6b-224">Step 3: Use existing image</span></span>
<span data-ttu-id="ecc6b-225">È possibile utilizzare un'immagine esistente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-225">You can use an existing image.</span></span> <span data-ttu-id="ecc6b-226">In alternativa è possibile [acquisire un'immagine di una macchina esistente](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="ecc6b-227">Si noti che la macchina non deve essere DS\*.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-227">Note the machine you image does not have to be DS* machine.</span></span> <span data-ttu-id="ecc6b-228">Dopo aver creato l'immagine, la procedura seguente illustra come copiarla nell'account di archiviazione Premium con il cmdlet **Start-AzureStorageBlobCopy** di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-228">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for the storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="ecc6b-229">Passaggio 4: Copiare BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ecc6b-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="ecc6b-230">Passaggio 5: Verificare regolarmente lo stato della copia:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-to-azure-disk-repository-in-subscription"></a><span data-ttu-id="ecc6b-231">Passaggio 6: Aggiungere il disco immagine al repository dischi di Azure in Sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ecc6b-231">Step 6: Add Image disk to Azure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="ecc6b-232">È possibile che si verifichino errori di lease del disco anche se i report di stato indicano un esisto positivo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-232">You may find that even though the status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="ecc6b-233">In questo caso, attendere circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-the-vm"></a><span data-ttu-id="ecc6b-234">Passaggio 7: Compilare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ecc6b-234">Step 7:  Build the VM</span></span>
<span data-ttu-id="ecc6b-235">Si compila la macchina virtuale da un'immagine e si collegano due dischi rigidi virtuali di Archiviazione Premium:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-235">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need to be a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use to DS Series VM
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

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="ecc6b-236">Distribuzioni esistenti che non usano i gruppi di disponibilità AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="ecc6b-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="ecc6b-237">Per le distribuzioni esistenti, vedere prima la sezione [Prerequisiti](#prerequisites-for-premium-storage) di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-237">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="ecc6b-238">Esistono diverse considerazioni per le distribuzioni di SQL Server che non usano i gruppi di disponibilità AlwaysOn e per quelle che li usano.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="ecc6b-239">Se non si usa AlwaysOn ed è disponibile un SQL Server autonomo esistente, si può eseguire l'aggiornamento ad Archiviazione Premium con un nuovo servizio cloud e un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="ecc6b-240">Valutare le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-240">Consider the following options:</span></span>

* <span data-ttu-id="ecc6b-241">**Creare una nuova macchina virtuale di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="ecc6b-242">È possibile creare una nuova macchina virtuale di SQL Server che utilizza un account di Archiviazione Premium, come documentato in Nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="ecc6b-243">Eseguire quindi il backup e ripristino della configurazione di SQL Server e dei database utente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="ecc6b-244">L'applicazione dovrà essere aggiornata per fare riferimento al nuovo SQL Server se si accede internamente o esternamente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-244">The application will need to be updated to reference the new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="ecc6b-245">È necessario copiare tutti gli oggetti esterni al db, come se si eseguisse una migrazione di SQL Server SxS (Side by Side).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-245">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="ecc6b-246">Sono inclusi oggetti come account di accesso, certificati e server collegati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="ecc6b-247">**Eseguire la migrazione di una macchina virtuale di Server SQL esistente**.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="ecc6b-248">Sarà necessario disconnettere la macchina virtuale di SQL Server e trasferirla in un nuovo servizio cloud, operazione che implica la copia di tutti i relativi dischi rigidi virtuali collegati all'account di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-248">This will require taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span></span> <span data-ttu-id="ecc6b-249">Quando la macchina virtuale torna online, l'applicazione farà riferimento al nome host del server come prima.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-249">When the VM comes online, the application will reference the server host name as before.</span></span> <span data-ttu-id="ecc6b-250">Tenere presente che le dimensioni del disco esistente influiranno sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-250">Be aware that the size of the existing disk will affect the performance characteristics.</span></span> <span data-ttu-id="ecc6b-251">Ad esempio, un disco di 400 GB viene arrotondato per eccesso a un P20.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-251">For example, a 400 GB disk gets rounded up to a P20.</span></span> <span data-ttu-id="ecc6b-252">Se si sa che tali prestazioni del disco non sono necessarie, è possibile ricreare la macchina virtuale come macchina virtuale serie DS e collegare dischi rigidi di archiviazione virtuale di Archiviazione Premium con le prestazioni/dimensioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-252">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span></span> <span data-ttu-id="ecc6b-253">È quindi possibile scollegare e ricollegare i file di database SQL.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-253">Then you could detach and reattach the SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc6b-254">Quando si copiano i dischi rigidi virtuali è necessario fare attenzione alle dimensioni in quanto indicano in quale tipo di disco di archiviazione Premium rientrano, determinando la specifica delle prestazioni del disco.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-254">When copying the VHD disks you should be aware of the size, depending on the size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="ecc6b-255">Azure arrotonderà alla dimensione del disco più vicina, per cui se si dispone di un disco di 400 GB, questo verrà arrotondato a un P20.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-255">Azure will round up to the nearest disk size, so if you have a 400GB disk, this will be rounded up to a P20.</span></span> <span data-ttu-id="ecc6b-256">A seconda dei requisiti di I/O esistenti del disco rigido virtuale del sistema operativo, potrebbe essere necessario eseguirne la migrazione a un account di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-256">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span></span>
>
>

<span data-ttu-id="ecc6b-257">Se si accede esternamente a SQL Server, verrà modificato il VIP del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-257">If your SQL Server is accessed externally, then the cloud service VIP will change.</span></span> <span data-ttu-id="ecc6b-258">Sarà necessario, inoltre, aggiornare le impostazioni di endpoint, ACL e DNS.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-258">You will also have to update end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="ecc6b-259">Distribuzioni esistenti che usano i gruppi di disponibilità AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="ecc6b-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="ecc6b-260">Per le distribuzioni esistenti, vedere prima la sezione [Prerequisiti](#prerequisites-for-premium-storage) di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-260">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="ecc6b-261">In questa sezione si osserverà prima di tutto in che modo AlwaysOn interagisce con una rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="ecc6b-262">Verranno quindi descritte le migrazioni in due scenari: migrazioni in cui viene considerato tollerabile un certo tempo di inattività e migrazioni in cui è necessario che i tempi di inattività siano minimi.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-262">We will then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="ecc6b-263">I gruppi di disponibilità di SQL Server AlwaysOn locali usano un listener locale che registra un nome DNS virtuale con un indirizzo IP condiviso tra uno o più server SQL.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="ecc6b-264">Quando si connettono i client vengono indirizzati attraverso l’IP del listener a SQL Server primario.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-264">When clients connect they are routed through the listener IP to the Primary SQL Server.</span></span> <span data-ttu-id="ecc6b-265">Si tratta del server a cui appartiene la risorsa IP AlwaysOn in quel momento.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-265">This is the server that owns the Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="ecc6b-267">In Microsoft Azure è consentito un solo indirizzo IP assegnato a una scheda di rete nella macchina virtuale, pertanto per conseguire lo stesso livello di astrazione possibile in locale, Azure utilizza l'indirizzo IP assegnato ai servizi di bilanciamento del carico interno ed esterno (ILB/ELB).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-267">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="ecc6b-268">La risorsa IP condivisa tra i server viene impostata sullo stesso IP del servizio ILB/ELB,  che viene pubblicato nel DNS, e il traffico del client viene passato attraverso il servizio ILB/ELB alla replica di SQL Server primario.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-268">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span></span> <span data-ttu-id="ecc6b-269">Il servizio ILB/ELB riconosce l'istanza di SQL Server primaria, perché usa i probe per verificare la presenza della risorsa IP AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-269">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span></span> <span data-ttu-id="ecc6b-270">Nell'esempio precedente, verifica ogni nodo che dispone di un endpoint a cui fa riferimento il servizio ELB/ILB.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-270">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span></span> <span data-ttu-id="ecc6b-271">Quello che risponde è il Server SQL primario.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-271">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc6b-272">Il servizio ILB e il servizio ELB vengono assegnati a un servizio cloud di Azure specifico, pertanto qualsiasi migrazione cloud in Azure comporterà probabilmente la modifica dell'IP del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-272">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that the Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="ecc6b-273">Migrazione delle distribuzioni di AlwaysOn che tollerano tempi di inattività</span><span class="sxs-lookup"><span data-stu-id="ecc6b-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="ecc6b-274">Sono disponibili due strategie per eseguire la migrazione delle distribuzioni di AlwaysOn che consentono periodi di inattività:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-274">There are two strategies to migrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="ecc6b-275">**Aggiungere più repliche secondarie a un cluster AlwaysOn esistente**</span><span class="sxs-lookup"><span data-stu-id="ecc6b-275">**Add more secondary replicas to an existing Always On Cluster**</span></span>
2. <span data-ttu-id="ecc6b-276">**Eseguire la migrazione a un nuovo cluster AlwaysOn**</span><span class="sxs-lookup"><span data-stu-id="ecc6b-276">**Migrate to a new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-to-an-existing-always-on-cluster"></a><span data-ttu-id="ecc6b-277">1. Aggiungere più repliche secondarie a un cluster AlwaysOn esistente</span><span class="sxs-lookup"><span data-stu-id="ecc6b-277">1. Add more Secondary Replicas to an Existing Always On Cluster</span></span>
<span data-ttu-id="ecc6b-278">Una strategia consiste nell'aggiungere più repliche secondarie al gruppo di disponibilità AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-278">One strategy is to add more secondaries to the Always On Availability Group.</span></span> <span data-ttu-id="ecc6b-279">È necessario aggiungere questi elementi in un nuovo servizio cloud e aggiornare il listener con il nuovo IP del servizio di bilanciamento carico.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-279">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="ecc6b-280">Punti dei tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-280">Points of downtime:</span></span>
* <span data-ttu-id="ecc6b-281">Convalida del cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-281">Cluster Validation.</span></span>
* <span data-ttu-id="ecc6b-282">Test di failover AlwaysOn per nuovi database secondari.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="ecc6b-283">Se si utilizzano pool di archiviazione di Windows nella macchina virtuale per una velocità effettiva I/O superiore, questi saranno portati offline durante una convalida completa del cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-283">If you are using Windows Storage Pools within the VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="ecc6b-284">Il test di convalida è necessario quando si aggiungono nodi al cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-284">The validation test is required when you add nodes to the cluster.</span></span> <span data-ttu-id="ecc6b-285">Il tempo necessario per eseguire il test può variare, pertanto verificarlo nell'ambiente di test rappresentativo per ottenere una stima approssimativa della durata.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-285">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this will take.</span></span>

<span data-ttu-id="ecc6b-286">È necessario prevedere tempo per eseguire il failover manuale e test CHAOS sui nodi appena aggiunti per assicurarsi che la disponibilità elevata AlwaysOn funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-286">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="ecc6b-288">Prima che venga eseguita la convalida è necessario arrestare tutte le istanze di SQL Server in cui vengono usati i pool di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-288">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="ecc6b-289">Procedure generali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-289">High-level steps</span></span>
>

1. <span data-ttu-id="ecc6b-290">Creare due nuovi server SQL Server nel nuovo servizio cloud con Archiviazione Premium collegata.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="ecc6b-291">Copiare i backup completi e ripristinare con **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="ecc6b-292">Copiare gli oggetti dipendenti esterni al database utente, ad esempio nomi di accesso e così via.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="ecc6b-293">Crea un nuovo servizio di carico bilanciamento interno (ILB) oppure utilizzare un servizio di bilanciamento del carico esterno (ELB) e quindi impostare gli endpoint con bilanciamento del carico in entrambi i nodi nuovi.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ecc6b-294">Prima di continuare, verificare che tutti i nodi abbiano la configurazione dell'endpoint corretta</span><span class="sxs-lookup"><span data-stu-id="ecc6b-294">Check all Nodes have the correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="ecc6b-295">Impedire all'utente/applicazione l’accesso a SQL Server (se si utilizzano pool di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-295">Stop User/Application Access to the SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="ecc6b-296">Arrestare i servizi motore di SQL Server in tutti i nodi (se si utilizzano il pool di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="ecc6b-297">Aggiungere nuovi nodi al cluster ed eseguire la convalida completa.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-297">Add new Nodes to cluster and run full validation.</span></span>
8. <span data-ttu-id="ecc6b-298">Quando la convalida ha esito positivo, avviare tutti i servizi di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="ecc6b-299">Eseguire il backup dei log delle transazioni e ripristinare i database utente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="ecc6b-300">Aggiungere nuovi nodi nel gruppo di disponibilità AlwaysOn e impostare la replica come **sincrona**.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-300">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="ecc6b-301">Aggiungere la risorsa indirizzo IP del nuovo ILB/ELB del servizio cloud tramite PowerShell per AlwaysOn in base all'esempio multisito riportato nell' [Appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-301">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="ecc6b-302">Nel clustering di Windows impostare i **Proprietari possibili** della risorsa **Indirizzo IP** sui nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-302">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span></span> <span data-ttu-id="ecc6b-303">Vedere la sezione 'Aggiunta della risorsa indirizzo IP nella stessa subnet' in [Appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-303">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="ecc6b-304">Failover su uno dei nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-304">Failover to one of the new nodes.</span></span>
13. <span data-ttu-id="ecc6b-305">Impostare i nuovi nodi come Partner di failover automatico e testare i failover.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-305">Make the new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="ecc6b-306">Rimuovere i nodi originali dal gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="ecc6b-307">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="ecc6b-307">Advantages</span></span>
* <span data-ttu-id="ecc6b-308">Nuovi SQL Server possono essere testati (SQL Server e applicazione) prima di essere aggiunti a AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-308">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span></span>
* <span data-ttu-id="ecc6b-309">È possibile modificare le dimensioni della macchina virtuale e personalizzare la risorsa di archiviazione per i requisiti specifici.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-309">You can change the VM size and customize the storage to your exact requirements.</span></span> <span data-ttu-id="ecc6b-310">Tuttavia, sarebbe opportuno mantenere tutti i percorsi di file SQL inalterati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-310">However, it would be beneficial to keep all the SQL file paths the same.</span></span>
* <span data-ttu-id="ecc6b-311">È possibile controllare quando viene avviato il trasferimento dei backup del database per le repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-311">You can control when the transfer of the DB backups to the Secondary Replicas are started.</span></span> <span data-ttu-id="ecc6b-312">Questo comportamento è diverso dal quello del commandlet di Azure **Start-AzureStorageBlobCopy** per copiare i dischi rigidi virtuali perché in quest’ultimo caso la copia è asincrona.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="ecc6b-313">Svantaggi:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-313">Disadvantages</span></span>
* <span data-ttu-id="ecc6b-314">Quando si utilizzano pool di archiviazione di Windows, durante la convalida del cluster completo si verifica un tempo di inattività del cluster per i nuovi nodi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-314">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span></span>
* <span data-ttu-id="ecc6b-315">A seconda della versione di SQL Server e del numero di repliche secondarie esistenti, potrebbe non essere possibile aggiungere ulteriori repliche secondarie senza rimuovere i le repliche secondarie esistenti.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-315">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="ecc6b-316">Il tempo di trasferimento dei dati SQL potrebbe essere molto lungo durante la configurazione di repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-316">There could be long SQL data transfer time while setting up the secondaries.</span></span>
* <span data-ttu-id="ecc6b-317">Esiste un costo aggiuntivo durante la migrazione mentre le nuove macchine vengono eseguite in parallelo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-to-a-new-always-on-cluster"></a><span data-ttu-id="ecc6b-318">2. Eseguire la migrazione a un nuovo cluster AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="ecc6b-318">2. Migrate to a new Always On Cluster</span></span>
<span data-ttu-id="ecc6b-319">Un'altra strategia consiste nel creare un nuovo cluster AlwaysOn con nuovi nodi nel nuovo servizio cloud e quindi reindirizzare i client in modo che lo usino.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-319">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="ecc6b-320">Punti dei tempi di inattività</span><span class="sxs-lookup"><span data-stu-id="ecc6b-320">Points of downtime</span></span>
<span data-ttu-id="ecc6b-321">Quando si trasferiscono utenti e applicazioni al nuovo listener AlwaysOn, si verifica un tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-321">There is downtime when you transfer applications and users to the new Always On listener.</span></span> <span data-ttu-id="ecc6b-322">Il tempo di inattività dipende da:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-322">The downtime depends on:</span></span>

* <span data-ttu-id="ecc6b-323">Il tempo necessario per ripristinare i backup dei log delle transazioni finali nei database in nuovi server.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-323">The time taken to restore final transaction log backups to databases on new servers.</span></span>
* <span data-ttu-id="ecc6b-324">Il tempo impiegato per aggiornare le applicazioni client in modo che usino il nuovo listener AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-324">The time taken to update client applications to use new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="ecc6b-325">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="ecc6b-325">Advantages</span></span>
* <span data-ttu-id="ecc6b-326">È possibile testare l'ambiente di produzione reale, SQL Server e le modifiche del build del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-326">You can test the actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="ecc6b-327">È possibile personalizzare l'archiviazione e ridurre le dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-327">You have the option to customize the storage and to potentially reduce size of VM.</span></span> <span data-ttu-id="ecc6b-328">Ciò potrebbe causare determinare una riduzione dei costi.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="ecc6b-329">Durante questo processo, è possibile aggiornare il build o la versione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="ecc6b-330">È inoltre possibile aggiornare il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-330">You can also upgrade the Operating System.</span></span>
* <span data-ttu-id="ecc6b-331">Il cluster AlwaysOn precedente può fungere da destinazione di rollback.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-331">The previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="ecc6b-332">Svantaggi:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-332">Disadvantages</span></span>
* <span data-ttu-id="ecc6b-333">È necessario modificare il nome DNS del listener, se si vuole che entrambi i cluster AlwaysOn vengano eseguiti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-333">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="ecc6b-334">Ciò comporta un sovraccarico di amministrazione durante la migrazione perché le stringhe dell’applicazione client devono riflettere il nuovo nome del listener.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-334">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span></span>
* <span data-ttu-id="ecc6b-335">È necessario implementare un meccanismo di sincronizzazione tra i due ambienti per mantenerli quanto più vicini è possibile al fine di ridurre al minimo i requisiti di sincronizzazione finale prima della migrazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-335">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span></span>
* <span data-ttu-id="ecc6b-336">Esiste un costo aggiunto durante la migrazione mentre il nuovo ambiente è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-336">There is added cost during migration while you have the new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="ecc6b-337">Migrazione delle distribuzioni AlwaysOn per un tempo di inattività minimo</span><span class="sxs-lookup"><span data-stu-id="ecc6b-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="ecc6b-338">Sono disponibili due strategie per la migrazione delle distribuzioni di AlwaysOn per un tempo di inattività minimo:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="ecc6b-339">**Utilizzare una replica secondaria esistente: singolo sito**</span><span class="sxs-lookup"><span data-stu-id="ecc6b-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="ecc6b-340">**Utilizzare repliche secondarie esistenti: multisito**</span><span class="sxs-lookup"><span data-stu-id="ecc6b-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="ecc6b-341">1. Usare una replica secondaria esistente: sito singolo</span><span class="sxs-lookup"><span data-stu-id="ecc6b-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="ecc6b-342">Una strategia per il tempo di inattività minimo consiste nel rimuovere una replica secondaria del cloud esistente dal servizio cloud corrente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-342">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span></span> <span data-ttu-id="ecc6b-343">Successivamente si copiano i dischi rigidi virtuali nel nuovo account di Archiviazione Premium e si crea la macchina virtuale nel nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-343">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span></span> <span data-ttu-id="ecc6b-344">A questo punto, si aggiorna il listener in clustering e failover.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-344">Then update the listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="ecc6b-345">Punti dei tempi di inattività</span><span class="sxs-lookup"><span data-stu-id="ecc6b-345">Points of downtime</span></span>
* <span data-ttu-id="ecc6b-346">Quando si aggiorna il nodo finale con l'endpoint di bilanciamento del carico, si verifica un tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-346">There is downtime when you update the final node with the Load Balanced endpoint.</span></span>
* <span data-ttu-id="ecc6b-347">La riconnessione del client potrebbe essere rimandata a seconda della configurazione client/DNS.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="ecc6b-348">Un tempo di inattività aggiuntivo si verifica se si sceglie di portare offline il gruppo di cluster AlwaysOn per sostituire gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-348">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span></span> <span data-ttu-id="ecc6b-349">È possibile evitare questa situazione usando una dipendenza OR e possibili proprietari per la risorsa indirizzo IP aggiunto.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-349">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span></span> <span data-ttu-id="ecc6b-350">Vedere la sezione 'Aggiunta della risorsa indirizzo IP nella stessa subnet' in [Appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-350">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="ecc6b-351">Quando si vuole che il nodo aggiunto partecipi come partner di failover AlwaysOn, è necessario aggiungere un endpoint di Azure con un riferimento al set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-351">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span></span> <span data-ttu-id="ecc6b-352">Quando si esegue il comando **Add-AzureEndpoint** per eseguire questa operazione, le connessioni correnti restano aperte, ma non sarà possibile stabilire nuove connessioni fino a quando non viene aggiornato il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-352">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener will not be able to be established until the load balancer has updated.</span></span> <span data-ttu-id="ecc6b-353">Nel test questo processo è durato 90-120 secondi; è opportuno verificare questa durata.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-353">In testing this was seen to last 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="ecc6b-354">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="ecc6b-354">Advantages</span></span>
* <span data-ttu-id="ecc6b-355">Nessun costo aggiuntivo durante la migrazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="ecc6b-356">Una migrazione uno a uno.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-356">A one-to-one migration.</span></span>
* <span data-ttu-id="ecc6b-357">Minore complessità.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-357">Reduced complexity.</span></span>
* <span data-ttu-id="ecc6b-358">Consente un maggiore IOPS dalle SKU di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="ecc6b-359">Quando i dischi sono disconnessi dalla macchina virtuale e copiati nel nuovo servizio cloud, è possibile utilizzare uno strumento di terze parti per aumentare le dimensioni del disco rigido virtuale, fornendo una maggiore velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-359">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="ecc6b-360">Per aumentare le dimensioni del disco rigido virtuale, vedere questo [forum di discussione](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="ecc6b-361">Svantaggi:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-361">Disadvantages</span></span>
* <span data-ttu-id="ecc6b-362">Perdita temporanea di disponibilità elevata e ripristino di emergenza durante la migrazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="ecc6b-363">Poiché si tratta di una migrazione 1:1, è necessario utilizzare una dimensione minima di macchina virtuale che supporti il numero di dischi rigidi virtuali presenti, pertanto potrebbe non essere possibile ridurre le dimensioni delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-363">As this is a 1:1 migration, you will have to use a minimum VM size that will support your number of VHDs, so you might not be able to downsize your VMs.</span></span>
* <span data-ttu-id="ecc6b-364">Questo scenario prevede l’uso del commandlet **Start-AzureStorageBlobCopy** di Azure, che è asincrono.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-364">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="ecc6b-365">Non esiste alcun contratto di servizio al completamento della copia.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="ecc6b-366">Il tempo delle copie varia perché dipende dal tempo di attesa in coda e dalla quantità di dati da trasferire.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-366">The time of the copies varies, while this depends on wait in queue it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="ecc6b-367">Il tempo di copia aumenta se la destinazione del trasferimento è un altro centro dati di Azure che supporta Archiviazione Premium in un'altra area.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-367">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="ecc6b-368">Se si dispone solo di due nodi, valutare la possibilità di un’attenuazione per l’eventualità che la copia richieda più tempo durante i test.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-368">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span></span> <span data-ttu-id="ecc6b-369">Valutare, ad esempio, le possibilità seguenti.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-369">This could include the following ideas.</span></span>
  * <span data-ttu-id="ecc6b-370">Aggiungere un terzo nodo di SQL Server temporaneo per la disponibilità elevata prima della migrazione con tempi di inattività concordati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-370">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="ecc6b-371">Eseguire la migrazione all'esterno della manutenzione pianificata di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-371">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="ecc6b-372">Assicurarsi di che avere configurato correttamente il quorum del cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="ecc6b-373">Procedure generali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-373">High-level steps</span></span>
<span data-ttu-id="ecc6b-374">In questo documento non viene illustrato un esempio end-to-end completo. Nella sezione [Appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), tuttavia, sono forniti dettagli che possono essere usati per eseguire questo tipo di migrazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-374">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="ecc6b-376">Raccogliere la configurazione del disco e rimuovere il nodo (non eliminare i dischi rigidi virtuali collegati).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-376">Gather disk configuration, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="ecc6b-377">Creare un account di Archiviazione Premium e copiare i dischi rigidi virtuali dall'account di Archiviazione Standard</span><span class="sxs-lookup"><span data-stu-id="ecc6b-377">Create a Premium Storage account and copy VHDs from the Standard Storage account</span></span>
* <span data-ttu-id="ecc6b-378">Creare il nuovo servizio cloud e ridistribuire la macchina virtuale SQL2 in tale servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-378">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span></span> <span data-ttu-id="ecc6b-379">Creare la macchina virtuale utilizzando la copia del disco rigido virtuale del sistema operativo originale e collegare i dischi rigidi virtuali copiati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-379">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span></span>
* <span data-ttu-id="ecc6b-380">Configurare ILB/ELB e aggiungere gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="ecc6b-381">Aggiornare il listener in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-381">Update Listener by either:</span></span>
  * <span data-ttu-id="ecc6b-382">Portare offline il gruppo AlwaysOn e aggiornare il listener di AlwaysOn con il nuovo indirizzo IP ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-382">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="ecc6b-383">Aggiungere la risorsa indirizzo IP del servizio ILB/ELB del nuovo servizio cloud tramite PowerShell nel clustering di Windows.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-383">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="ecc6b-384">Quindi impostare i possibili proprietari della risorsa indirizzo IP sul nodo migrato, SQL2, e impostare tale nodo come dipendenza OR nel nome di rete.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-384">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span></span> <span data-ttu-id="ecc6b-385">Vedere la sezione 'Aggiunta della risorsa indirizzo IP nella stessa subnet' in [Appendice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-385">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="ecc6b-386">Controllare la configurazione DNS/propagazione ai client.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-386">Check DNS configuration/propogation to the clients.</span></span>
* <span data-ttu-id="ecc6b-387">Eseguire la migrazione della macchina virtuale SQL1 ed effettuare i passaggi da 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="ecc6b-388">Se si utilizzano i passaggi 5ii, aggiungere SQL1 come possibile proprietario per la risorsa indirizzo IP aggiunto</span><span class="sxs-lookup"><span data-stu-id="ecc6b-388">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span></span>
* <span data-ttu-id="ecc6b-389">Testare i failover.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="ecc6b-390">2. Usare una o più repliche secondarie esistenti: multisito</span><span class="sxs-lookup"><span data-stu-id="ecc6b-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="ecc6b-391">Se sono disponibili nodi in più data center di Azure o se è disponibile un ambiente ibrido, si può usare una configurazione AlwaysOn in questo ambiente per ridurre al minimo i tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span></span>

<span data-ttu-id="ecc6b-392">L'approccio consiste nel cambiare in sincrona la sincronizzazione di AlwaysOn per il data center di Azure locale o secondario e quindi eseguire il failover in tale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-392">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span></span> <span data-ttu-id="ecc6b-393">Copiare quindi i dischi rigidi virtuali in un account di Archiviazione Premium e ridistribuire la macchina in un nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-393">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span></span> <span data-ttu-id="ecc6b-394">Aggiornare il listener ed eseguire il failback.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-394">Update the listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="ecc6b-395">Punti dei tempi di inattività</span><span class="sxs-lookup"><span data-stu-id="ecc6b-395">Points of downtime</span></span>
<span data-ttu-id="ecc6b-396">Il tempo di inattività corrisponde al tempo necessario per il failover al centro dati alternativo e ritorno.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-396">The downtime consists of the time to failover to the alternative DC and back.</span></span> <span data-ttu-id="ecc6b-397">Dipende anche dalla configurazione del client/DNS e potrebbe determinare un ritardo della riconnessione del client.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="ecc6b-398">Si consideri l'esempio seguente di una configurazione di AlwaysOn ibrida:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-398">Consider the following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="ecc6b-400">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="ecc6b-400">Advantages</span></span>
* <span data-ttu-id="ecc6b-401">È possibile utilizzare l'infrastruttura esistente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="ecc6b-402">È possibile pre-aggiornare Archiviazione di Azure nel centro dati di Azure di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-402">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span></span>
* <span data-ttu-id="ecc6b-403">È possibile riconfigurare l'archiviazione del centro dati di Azure di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-403">The DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="ecc6b-404">Esiste un minimo di due failover durante la migrazione, esclusi i failover di test.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="ecc6b-405">Non è necessario spostare i dati di SQL Server con backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-405">You do not need to move SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="ecc6b-406">Svantaggi:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-406">Disadvantages</span></span>
* <span data-ttu-id="ecc6b-407">A seconda dell’accesso client a SQL Server, potrebbe esserci un aumento della latenza durante l'esecuzione di SQL Server in un centro dati alternativo per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-407">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span></span>
* <span data-ttu-id="ecc6b-408">Il tempo di copia dei dischi rigidi virtuali in Archiviazione Premium potrebbe essere lungo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-408">The copy time of VHDs to Premium storage could be long.</span></span> <span data-ttu-id="ecc6b-409">Ciò potrebbe influire sulla decisione relativa al mantenimento del nodo nel gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-409">This might affect your decision on whether to keep the node in the Availability Group.</span></span> <span data-ttu-id="ecc6b-410">Considerare questo aspetto quando carichi di lavoro a uso intensivo di log vengono eseguiti durante le migrazioni richieste dal momento che il nodo primario dovrà mantenere le transazioni non replicate nel proprio log delle transazioni,</span><span class="sxs-lookup"><span data-stu-id="ecc6b-410">Consider this for when log intensive work loads are running during the migration is required, since the Primary node will have to keep the unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="ecc6b-411">aumentando così in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="ecc6b-412">Questo scenario prevede l’uso del commandlet **Start-AzureStorageBlobCopy** di Azure, che è asincrono.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-412">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="ecc6b-413">Non esiste alcun contratto di servizio al completamento.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-413">There is no SLA on completion.</span></span> <span data-ttu-id="ecc6b-414">Il tempo delle copie varia perché dipende dal tempo di attesa in coda e dalla quantità di dati da trasferire.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-414">The time of the copies varies, while this depends on wait in queue, it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="ecc6b-415">Di conseguenza, dal momento che si dispone di un solo nodo nel secondo centro dati, è opportuno prevedere operazioni di attenuazione per l’eventualità che la copia richieda più tempo durante i test.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span></span> <span data-ttu-id="ecc6b-416">Valutare, ad esempio, le possibilità seguenti.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-416">This could include the following ideas.</span></span>
  * <span data-ttu-id="ecc6b-417">Aggiungere un secondo nodo di SQL Server temporaneo per la disponibilità elevata prima della migrazione con tempi di inattività concordati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-417">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="ecc6b-418">Eseguire la migrazione all'esterno della manutenzione pianificata di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-418">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="ecc6b-419">Assicurarsi di che avere configurato correttamente il quorum del cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="ecc6b-420">Questo scenario presuppone di aver documentato l'installazione e che si sappia come viene eseguito il mapping dell’archiviazione in modo da poter apportare le modifiche necessarie a definire impostazioni della cache su disco ottimali.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-420">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="ecc6b-421">Procedure generali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-421">High-level steps</span></span>
![MultiSite2][10]

* <span data-ttu-id="ecc6b-423">Rendere il centro dati di Azure locale/alternativo l'SQL Server primario e l’altro partner di failover automatico.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-423">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="ecc6b-424">Raccogliere la configurazione del disco da SQL2 e rimuovere il nodo (non eliminare i dischi rigidi virtuali collegati).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-424">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="ecc6b-425">Creare un account di Archiviazione Premium e copiare i dischi rigidi virtuali dall'account di Archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-425">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span></span>
* <span data-ttu-id="ecc6b-426">Creare un nuovo servizio cloud e la macchina virtuale SQL2 con relativi dischi di archiviazione Premium collegati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-426">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="ecc6b-427">Configurare ILB/ELB e aggiungere gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="ecc6b-428">Aggiornare il listener di AlwaysOn con nuovo il indirizzo IP ILB/ELB e testare il failover.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-428">Update the Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="ecc6b-429">Controllare la configurazione DNS.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-429">Check the DNS configuration.</span></span>
* <span data-ttu-id="ecc6b-430">Modificare l'AFP in SQL2, quindi eseguire la migrazione di SQL1 ed eseguire i passaggi da 2 a 5.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-430">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="ecc6b-431">Testare i failover.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-431">Test failovers.</span></span>
* <span data-ttu-id="ecc6b-432">Riportare l'AFP a SQL1 e SQL2</span><span class="sxs-lookup"><span data-stu-id="ecc6b-432">Switch the AFP back to SQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-to-premium-storage"></a><span data-ttu-id="ecc6b-433">Appendice: Migrazione di un cluster AlwaysOn multisito all'Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="ecc6b-433">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span></span>
<span data-ttu-id="ecc6b-434">La parte restante di questo argomento fornisce un esempio dettagliato della conversione di un cluster AlwaysOn multisito all'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-434">The remainder of this topic provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span></span> <span data-ttu-id="ecc6b-435">Il listener, inoltre, viene passato dall’uso di un servizio di bilanciamento del carico esterno (ELB) all’uso di un servizio di bilanciamento del carico interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-435">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="ecc6b-436">Environment</span><span class="sxs-lookup"><span data-stu-id="ecc6b-436">Environment</span></span>
* <span data-ttu-id="ecc6b-437">Windows 2K12 /SQL 2K12</span><span class="sxs-lookup"><span data-stu-id="ecc6b-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="ecc6b-438">1 File DB su SP</span><span class="sxs-lookup"><span data-stu-id="ecc6b-438">1 DB Files on SP</span></span>
* <span data-ttu-id="ecc6b-439">2 pool di archiviazione per ogni nodo</span><span class="sxs-lookup"><span data-stu-id="ecc6b-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="ecc6b-441">VM:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-441">VM:</span></span>
<span data-ttu-id="ecc6b-442">In questo esempio sarà illustrato lo spostamento da un ELB a un ILB.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-442">In this example we are going to demonstrate moving from an ELB to ILB.</span></span> <span data-ttu-id="ecc6b-443">ELB era disponibile prima di ILB, pertanto viene illustrato come eseguire questo passaggio durante la migrazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-443">ELB was available before ILB, so this shows how to switch to this during the migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-to-subscription"></a><span data-ttu-id="ecc6b-445">Passaggi precedenti: Connettersi alla sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ecc6b-445">Pre Steps: Connect to Subscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="ecc6b-446">Passaggio 1: Creare un nuovo account di archiviazione e servizio cloud</span><span class="sxs-lookup"><span data-stu-id="ecc6b-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where the vm to migrate resides
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

#### <a name="step-2-increase-the-permitted-failures-on-resources-optional"></a><span data-ttu-id="ecc6b-447">Passaggio 2: Aumentare il numero di errori consentiti nelle risorse <Optional></span><span class="sxs-lookup"><span data-stu-id="ecc6b-447">Step 2: Increase the permitted failures on resources <Optional></span></span>
<span data-ttu-id="ecc6b-448">In alcune risorse che appartengono al gruppo di disponibilità AlwaysOn sono previsti limiti al numero di errori che possono verificarsi in un intervallo di tempo durante il quale il servizio cluster prova a riavviare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-448">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service will attempt to restart the resource group.</span></span> <span data-ttu-id="ecc6b-449">Si consiglia di aumentare questo numero durante l’esecuzione di questa procedura poiché se non si esegue il failover manuale e non si attivano i failover arrestando le macchine si potrebbe raggiungere il limite.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span></span>

<span data-ttu-id="ecc6b-450">Sarebbe prudente raddoppiare la quantità di errori consentita. A questo scopo, in Gestione cluster di failover passare alle proprietà del gruppo di risorse AlwaysOn:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-450">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="ecc6b-452">Modificare il numero massimo di errori in 6.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-452">Change the Maximum Failures to 6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="ecc6b-453">Passaggio 3: Aggiungere la risorsa indirizzo IP per il gruppo di cluster <Optional></span><span class="sxs-lookup"><span data-stu-id="ecc6b-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="ecc6b-454">Se si dispone di un solo indirizzo IP per il gruppo cluster e questo viene allineato alla subnet cloud, tenere presente che se di portano accidentalmente offline tutti i nodi del cluster nel cloud nella rete, la risorsa IP del cluster e il nome di rete del cluster non potranno essere portati online.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-454">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name will not be able to come online.</span></span> <span data-ttu-id="ecc6b-455">In tal caso, gli aggiornamenti per altre risorse cluster non saranno consentiti.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-455">In the event of this it will prevent updates to other cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="ecc6b-456">Passaggio 4: Eseguire la configurazione di DNS</span><span class="sxs-lookup"><span data-stu-id="ecc6b-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="ecc6b-457">L'implementazione di una transizione senza intoppi dipende dalla modalità di uso e aggiornamento del DNS.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-457">To implement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="ecc6b-458">Quando viene installato AlwaysOn, crea un gruppo di risorse cluster di Windows. Se si apre Gestione cluster di failover, si noterà la presenza di almeno tre risorse. Le due a cui fa riferimento il documento sono:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, the two that the document refers to are:</span></span>

* <span data-ttu-id="ecc6b-459">Nome di rete virtuale (VNN): questo è il nome DNS a cui si connette il client quando si sceglie di stabilire la connessione a SQL Server tramite AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-459">Virtual Network Name (VNN) – This is the DNS name that client connect to when wanting to connect to SQL Servers via Always On.</span></span>
* <span data-ttu-id="ecc6b-460">Risorsa indirizzo IP: questo è l'indirizzo IP associato al nome di rete virtuale; possono essere più di uno e in una configurazione multisito sarà presente un indirizzo IP per sito/subnet.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-460">IP Address Resource – This is the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="ecc6b-461">Quando ci si connette a SQL Sevrer, il driver del client SQL Server recupera i record DNS associati al listener e prova a connettersi a ogni indirizzo IP associato a AlwaysOn. Di seguito sono illustrati alcuni fattori che possono influenzare questa situazione.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-461">When connecting to SQL Server, the SQL Server Client driver will retrieve the DNS records associated with the listener and try to connect to each Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="ecc6b-462">Il numero di record DNS simultanei associati al nome del listener dipende non solo dal numero di indirizzi IP associati, ma anche dall'impostazione 'RegisterAllIpProviders' in Clustering di failover per la risorsa nome di rete virtuale di AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-462">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span></span>

<span data-ttu-id="ecc6b-463">Quando si distribuisce AlwaysOn in Azure, sono disponibili diversi passaggi per creare il listener e gli indirizzi IP. È necessario configurare manualmente su 1 l'impostazione "RegisterAllIpProviders", diversamente dalla distribuzione di AlwaysOn locale, dove è già impostata su 1.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-463">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on-premises Always On deployment where it is already set to 1.</span></span>

<span data-ttu-id="ecc6b-464">Se 'RegisterAllIpProviders' è 0, verrà visualizzato solo un record DNS nel DNS associato il listener:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with the Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="ecc6b-466">Se 'RegisterAllIpProviders' è 1:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="ecc6b-468">Il codice riportato di seguito esegue dump delle impostazioni del nome di rete virtuale e lo imposta automaticamente. Tenere presente che per rendere effettiva la modifica è necessario portare il nome di rete virtuale offline e poi di nuovo online, operazione che causa l'interruzione della connettività client.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-468">The code below will dump out the VNN settings and set it for you, please note, for the change to take effect you will need to take the VNN offline and turn it back online, this taking the Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="ecc6b-469">In un passaggio di migrazione successivo si dovrà aggiornare il listener AlwaysOn con un indirizzo IP aggiornato che farà riferimento a un servizio di bilanciamento del carico. Ciò comporterà la rimozione e l'aggiunta di una risorsa indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-469">In a later migration step you will need to update the Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="ecc6b-470">Dopo l’aggiornamento IP, è necessario assicurarsi che il nuovo indirizzo IP sia stato aggiornato nella zona DNS e che i client aggiornino la relativa cache DNS locale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-470">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span></span>

<span data-ttu-id="ecc6b-471">Se i client si trovano in segmenti di rete diversi e fanno riferimento a un server DNS diverso, è necessario considerare ciò che accade sul trasferimento di zona DNS durante la migrazione dal momento che il tempo di riconnessione dell'applicazione sarà limitato almeno del tempo di trasferimento di zona di ogni nuovo indirizzo IP per il listener.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-471">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time will be constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span></span> <span data-ttu-id="ecc6b-472">In caso di vincolo di tempo, è necessario discutere e verificare imponendo un trasferimento di zona incrementale con i team di Windows e, inoltre, impostare il record host DNS su una durata (TTL) inferiore, così i client si aggiornano.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span></span> <span data-ttu-id="ecc6b-473">Per ulteriori informazioni, vedere [Trasferimenti di zona incrementali](https://technet.microsoft.com/library/cc958973.aspx) e [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="ecc6b-474">Per impostazione predefinita, il valore TTL per il Record DNS associato al Listener in AlwaysOn in Azure è 1200 secondi.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-474">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="ecc6b-475">È possibile ridurre questo valore in caso di vincolo di tempo durante la migrazione per assicurarsi che i client aggiornino il proprio DNS con l'indirizzo IP aggiornato per il listener.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-475">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span></span> <span data-ttu-id="ecc6b-476">È possibile visualizzare e modificare la configurazione eseguendo il dump della configurazione del nome di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-476">You can see and modify the configuration by dumping out the configuration of the VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="ecc6b-477">Si noti che più basso è 'HostRecordTTL' più alto sarà il traffico DNS.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-477">Please note, the lower the ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="ecc6b-478">Impostazioni applicazione client</span><span class="sxs-lookup"><span data-stu-id="ecc6b-478">Client application settings</span></span>
<span data-ttu-id="ecc6b-479">Se l'applicazione client SQL supporta .Net 4.5 SQLClient, è possibile usare la parola chiave "MULTISUBNETFAILOVER=TRUE", che è consigliabile applicare perché consente una connessione più veloce al gruppo di disponibilità SQL AlwaysOn durante il failover.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-479">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended to be applied as it allows for faster connection to SQL Always On Availability Group during failover.</span></span> <span data-ttu-id="ecc6b-480">Enumera tutti gli indirizzi IP associati al listener AlwaysOn in parallelo e consente una velocità di tentativi di connessione TCP maggiore durante un failover.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-480">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="ecc6b-481">Per ulteriori informazioni riguardanti le impostazioni precedenti, vedere [Parola chiave MultiSubnetFailover e funzionalità associate](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-481">For more information regarding the settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="ecc6b-482">Vedere anche [Supporto SqlClient per disponibilità elevata, ripristino di emergenza](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="ecc6b-483">Passaggio 5: Impostare il quorum del cluster</span><span class="sxs-lookup"><span data-stu-id="ecc6b-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="ecc6b-484">Poiché sarà portato offline almeno un SQL Server alla volta, è necessario modificare l'impostazione del quorum cluster, se si usa FSW (File Share Witness) con due nodi. Il quorum deve essere impostato in modo da consentire la maggioranza del nodo e usare la votazione dinamica al fine di permettere a un singolo nodo di rimanere permanente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-484">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set the quorum to allow node majority and utilize dynamic voting, and this is to allow for a single node to remain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="ecc6b-485">Per ulteriori informazioni sulla gestione e configurazione del quorum del cluster, vedere [Configurare e gestire il quorum in un cluster di failover di Windows Server 2012](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecc6b-485">For more information on managing and configuring the cluster quorum, please see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="ecc6b-486">Passaggio 6: Estrarre endpoint e ACL esistenti</span><span class="sxs-lookup"><span data-stu-id="ecc6b-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for the Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="ecc6b-487">Salvarli in un file di testo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-487">Save these to a text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="ecc6b-488">Passaggio 7: Modificare i partner di failover e le modalità di replica</span><span class="sxs-lookup"><span data-stu-id="ecc6b-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="ecc6b-489">Se si dispone di più di 2 SQL Server, è necessario impostare su "Sincrono" il failover di un'altra replica secondaria in un altro centro dati o locale e renderlo Partner di failover automatico (AFP) in modo da mantenere la disponibilità elevata mentre si apportano modifiche.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-489">If you have more than 2 SQL Servers, you should change the failover of another secondary in another DC or on-premises to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="ecc6b-490">A tale scopo, è possibile utilizzare TSQL o SSMS:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="ecc6b-492">Passaggio 8: Rimuovere la VM secondaria dal servizio cloud</span><span class="sxs-lookup"><span data-stu-id="ecc6b-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="ecc6b-493">È consigliabile pianificare prima la migrazione di un nodo secondario del cloud, se è attualmente primario, è necessario avviare un failover manuale.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-493">You should be planning to migrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

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

    #Check disk config, make sure below returns the disks associated with the VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="ecc6b-494">Passaggio 9: Modificare le impostazioni di caching del disco nel file CSV e salvare</span><span class="sxs-lookup"><span data-stu-id="ecc6b-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="ecc6b-495">Per i volumi di dati, devono essere impostate su READONLY.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-495">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="ecc6b-496">Per i volumi di TLOG, devono essere impostate su NONE.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-496">For TLOG volumes these should be set to NONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="ecc6b-498">Passaggio 10: Copiare i dischi rigidi virtuali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
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



<span data-ttu-id="ecc6b-499">È possibile controllare lo stato della copia dei dischi rigidi virtuali per l'account di Archiviazione Premium:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-499">You can check the copy status of the VHDs to the Premium Storage account:</span></span>

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

<span data-ttu-id="ecc6b-501">Attendere che tutto venga registrato come esito positivo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="ecc6b-502">Per informazioni per i singoli BLOB:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="ecc6b-503">Passaggio 11: Registrare un disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="ecc6b-503">Step 11: Register OS disk</span></span>
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

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="ecc6b-504">Passaggio 12: Importare la replica secondaria nel nuovo servizio cloud</span><span class="sxs-lookup"><span data-stu-id="ecc6b-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="ecc6b-505">Il codice riportato di seguito utilizza anche l'opzione aggiunta qui, è possibile importare la macchina e utilizzare l'indirizzo VIP da conservare.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-505">The code below also uses the added option here you can import the machine and use the retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember to change to XIO
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

    ###Attaching disks to a VM during a deploy to a new cloud service and new storage account is different from just attaching VHDs to just a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="ecc6b-506">Passaggio 13: Creare il servizio ILB sul nuovo Svc cloud, aggiungere endpoint a carico bilanciato e ACL</span><span class="sxs-lookup"><span data-stu-id="ecc6b-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
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

#### <a name="step-14-update-always-on"></a><span data-ttu-id="ecc6b-507">Passaggio 14: Aggiornare AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="ecc6b-507">Step 14: Update Always On</span></span>
    #Code to be executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # the azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency to Listener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="ecc6b-509">Ora, rimuovere l’indirizzo IP del servizio cloud precedente.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-509">Now remove the old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="ecc6b-511">Passaggio 15: Eseguire il controllo dell'aggiornamento DNS</span><span class="sxs-lookup"><span data-stu-id="ecc6b-511">Step 15: DNS update check</span></span>
<span data-ttu-id="ecc6b-512">È ora necessario controllare i server DNS nelle reti client SQL Server e assicurarsi che il servizio cluster abbia aggiunto il record host aggiuntivo per l'indirizzo IP aggiunto.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span></span> <span data-ttu-id="ecc6b-513">Se tali server DNS non sono stati aggiornati, forzare un trasferimento di zona DNS e assicurarsi che i client presenti nella subnet riescano a risolversi in entrambi gli indirizzi IP di AlwaysOn, in modo che non sia necessario attendere la replica DNS automatica.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="ecc6b-514">Passaggio 16: Riconfigurare Always On</span><span class="sxs-lookup"><span data-stu-id="ecc6b-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="ecc6b-515">A questo punto è necessario attendere che il database secondario su cui è stato migrato il nodo venga risincronizzato completamente e passare al nodo di replica sincrona e renderlo AFP.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-515">At this point you wait for the secondary that node that was migrated to fully resynchronize with the on-premises node and switch to synchronous replication node and make it the AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="ecc6b-516">Passaggio 17: Eseguire la migrazione del secondo nodo</span><span class="sxs-lookup"><span data-stu-id="ecc6b-516">Step 17: Migrate second node</span></span>
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

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="ecc6b-517">Passaggio 18: Modificare le impostazioni di caching del disco nel file CSV e salvare</span><span class="sxs-lookup"><span data-stu-id="ecc6b-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="ecc6b-518">Per i volumi di dati, devono essere impostate su READONLY.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-518">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="ecc6b-519">Per i volumi di TLOG, devono essere impostate su NONE.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-519">For TLOG volumes these should be set to NONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="ecc6b-521">Passaggio 19: Creare nuovi account di archiviazione indipendente per il nodo secondario</span><span class="sxs-lookup"><span data-stu-id="ecc6b-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset the storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="ecc6b-522">Passaggio 20: Copiare i dischi rigidi virtuali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
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


<span data-ttu-id="ecc6b-523">È possibile controllare lo stato di copia del disco rigido virtuale per tutti i dischi rigidi virtuali: ForEach ($disk in $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. EtichettaDisco $diskName = $disk.DiskName</span><span class="sxs-lookup"><span data-stu-id="ecc6b-523">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="ecc6b-525">Attendere che tutto venga registrato come esito positivo.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="ecc6b-526">Per informazioni per i singoli BLOB:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="ecc6b-527">Passaggio 21: Registrare il disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="ecc6b-527">Step 21: Register OS disk</span></span>
    #change storage account to the new XIO storage account
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

    #Join to existing Avaiability Set

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

    ###This is different to just a straight cloud service change
    #note if you do not have a disk label the command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="ecc6b-528">Passaggio 22: Aggiungere endpoint con carico bilanciato e ACL</span><span class="sxs-lookup"><span data-stu-id="ecc6b-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in the Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="ecc6b-529">Passaggio 23: Eseguire il failover di test</span><span class="sxs-lookup"><span data-stu-id="ecc6b-529">Step 23: Test failover</span></span>
<span data-ttu-id="ecc6b-530">A questo punto, è consigliabile consentire al nodo migrato di sincronizzarsi con il nodo AlwaysOn locale, impostarlo in modalità di replica sincrona e attendere che sia sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-530">You should now let the migrated node synchronize with the on-premises Always On node, place it in to synchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="ecc6b-531">Quindi eseguire il failover da locale sul primo nodo migrato, ossia AFP.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-531">Then failover from on-prem to the first node migrated, which is the AFP.</span></span> <span data-ttu-id="ecc6b-532">Successivamente, modificare l’ultimo nodo migrato in AFP.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-532">Once that has worked, change the last migrated node to the AFP.</span></span>

<span data-ttu-id="ecc6b-533">È consigliabile testare i failover tra tutti i nodi ed eseguire i caos test per assicurarsi che i failover funzionino nel modo previsto e nei tempi indicati.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-533">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="ecc6b-534">Passaggio 24: Ripristinare le impostazioni quorum del cluster / TTL DNS / Failover Pntrs / impostazioni di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="ecc6b-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="ecc6b-535">Aggiunta della risorsa indirizzo IP nella stessa Subnet</span><span class="sxs-lookup"><span data-stu-id="ecc6b-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="ecc6b-536">Se sono presenti solo due server SQL e si vuole eseguirne la migrazione a un nuovo servizio cloud ma mantenerli nella stessa subnet, è possibile evitare di portare offline il listener per eliminare l'indirizzo IP di AlwaysOn originale e aggiungere il nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-536">If you have only 2 SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span></span> <span data-ttu-id="ecc6b-537">Se si esegue la migrazione delle macchine virtuali in un'altra subnet non sarà necessario eseguire questa operazione perché una rete di cluster aggiuntiva farà riferimento a tale subnet.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-537">If you are migrating the VMs to another subnet you will not need to do this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="ecc6b-538">Dopo aver attivato la replica secondaria migrata e aggiunto la nuova risorsa indirizzo IP per il nuovo servizio cloud prima del failover della replica primaria esistente, è necessario eseguire questi passaggi in Gestione failover cluster:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-538">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span></span>

<span data-ttu-id="ecc6b-539">Per aggiungere l'indirizzo IP, vedere l’ [Appendice](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), passaggio 14.</span><span class="sxs-lookup"><span data-stu-id="ecc6b-539">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="ecc6b-540">Per la risorsa indirizzo IP corrente, modificare il proprietario possibile in 'SQL Server primario esistente', nell'esempio seguente 'dansqlams4':</span><span class="sxs-lookup"><span data-stu-id="ecc6b-540">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="ecc6b-542">Per la nuova risorsa indirizzo IP, modificare il proprietario possibile in 'SQL Server secondario migrato', nell'esempio seguente 'dansqlams5':</span><span class="sxs-lookup"><span data-stu-id="ecc6b-542">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="ecc6b-544">Dopo queste impostazioni, è possibile eseguire il failover e quando l'ultimo viene migrato, i possibili proprietari devono essere modificati in modo che tale nodo venga aggiunto come possibile proprietario:</span><span class="sxs-lookup"><span data-stu-id="ecc6b-544">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="ecc6b-546">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ecc6b-546">Additional resources</span></span>
* [<span data-ttu-id="ecc6b-547">Archiviazione Premium di Azure</span><span class="sxs-lookup"><span data-stu-id="ecc6b-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="ecc6b-548">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ecc6b-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="ecc6b-549">SQL Server in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="ecc6b-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

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
