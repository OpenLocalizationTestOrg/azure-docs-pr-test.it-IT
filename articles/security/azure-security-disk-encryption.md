---
title: Crittografia dischi di Azure per le macchine virtuali IaaS Windows e Linux | Documentazione Microsoft
description: Questo articolo offre una panoramica di Crittografia dischi di Microsoft Azure per le VM IaaS Windows e Linux.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: a4f20fc19ae40561d042d5cff744a030014f75c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="219c7-103">Azure Disk Encryption per le macchine virtuali IaaS Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="219c7-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="219c7-104">Microsoft Azure è caratterizzato dal massimo impegno volto ad assicurare la privacy e la sovranità dei dati e a consentire il controllo dei dati ospitati in Azure con una gamma di tecnologie avanzate per crittografare, controllare e gestire le chiavi di crittografia e controllare e verificare l'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="219c7-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="219c7-105">I clienti di Azure hanno quindi la possibilità di scegliere la soluzione che meglio soddisfa le proprie esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="219c7-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span></span> <span data-ttu-id="219c7-106">In questo documento viene introdotta una nuova soluzione tecnologica, "Azure Disk Encryption per le macchine virtuali IaaS Windows e Linux", che facilita la protezione e la salvaguardia dei dati per rispettare gli impegni in termini di sicurezza e conformità dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="219c7-107">Il documento include informazioni dettagliate sull'uso delle funzionalità di crittografia del disco di Azure, compresi gli scenari supportati e le esperienze utente.</span><span class="sxs-lookup"><span data-stu-id="219c7-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-108">Alcune indicazioni possono comportare un maggior utilizzo delle risorse di calcolo, rete o dati con un conseguente aumento dei costi di licenza o sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="219c7-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="219c7-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="219c7-109">Overview</span></span>
<span data-ttu-id="219c7-110">Crittografia dischi di Azure è una nuova funzionalità che consente di crittografare i dischi delle macchine virtuali IaaS Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="219c7-111">Crittografia dischi di Azure si basa sulla funzionalità [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) standard di settore disponibile in Windows e sulla funzionalità [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) di Linux per offrire la crittografia del volume per i dischi dei dati e del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="219c7-112">La soluzione è integrata con [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) per consentire di controllare e gestire le chiavi di crittografia dei dischi e i segreti nella sottoscrizione di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="219c7-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="219c7-113">Questa soluzione assicura anche che tutti i dati nei dischi delle macchine virtuali vengano crittografati quando inattivi in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="219c7-114">Crittografia dischi di Azure per macchine virtuali IaaS Windows e Linux ha ora **disponibilità generale** in tutte le aree pubbliche e AzureGov di Azure per macchine virtuali standard e macchine virtuali con archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="219c7-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="219c7-115">Scenari di crittografia</span><span class="sxs-lookup"><span data-stu-id="219c7-115">Encryption scenarios</span></span>
<span data-ttu-id="219c7-116">La soluzione Crittografia dischi di Azure supporta i tre scenari dei clienti descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="219c7-116">The Azure Disk Encryption solution supports the following customer scenarios:</span></span>

* <span data-ttu-id="219c7-117">Abilitare la crittografia nelle nuove VM IaaS create da chiavi di crittografia e VHD pre-crittografati</span><span class="sxs-lookup"><span data-stu-id="219c7-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="219c7-118">Abilitare la crittografia in nuove VM IaaS create da immagini della raccolta di Azure supportate</span><span class="sxs-lookup"><span data-stu-id="219c7-118">Enable encryption on new IaaS VMs created from the supported Azure Gallery images</span></span>
* <span data-ttu-id="219c7-119">Abilitare la crittografia in VM IaaS esistenti in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="219c7-120">Disabilitare la crittografia nelle VM IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="219c7-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="219c7-121">Disabilitare la crittografia nelle unità dati per le VM IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="219c7-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="219c7-122">Abilitare la crittografia delle macchine virtuali con disco gestito</span><span class="sxs-lookup"><span data-stu-id="219c7-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="219c7-123">Aggiornare le impostazioni di crittografia di una macchina virtuale non dotata di archiviazione Premium crittografata esistente</span><span class="sxs-lookup"><span data-stu-id="219c7-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="219c7-124">Backup e ripristino di macchine virtuali crittografate con chiave di crittografia della chiave</span><span class="sxs-lookup"><span data-stu-id="219c7-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="219c7-125">La soluzione supporta gli scenari seguenti per le macchine virtuali IaaS, se abilitati in Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="219c7-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="219c7-126">Integrazione dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="219c7-127">Macchine virtuali di livello Standard: [serie A, D, DS, G, GS, F e così via per VM IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="219c7-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="219c7-128">Abilitare la crittografia nelle macchine virtuali IaaS Windows e Linux e nelle macchine virtuali con disco gestito dalle immagini della raccolta di Azure supportate</span><span class="sxs-lookup"><span data-stu-id="219c7-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from the supported Azure Gallery images</span></span>
* <span data-ttu-id="219c7-129">Disabilitare la crittografia nel sistema operativo e nelle unità dati per le macchine virtuali IaaS Windows e per le macchine virtuali con disco gestito</span><span class="sxs-lookup"><span data-stu-id="219c7-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="219c7-130">Disabilitare la crittografia nelle unità dati per le macchine virtuali IaaS Linux e per le macchine virtuali con disco gestito</span><span class="sxs-lookup"><span data-stu-id="219c7-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="219c7-131">Abilitare la crittografia in VM IaaS eseguite nel sistema operativo client Windows</span><span class="sxs-lookup"><span data-stu-id="219c7-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="219c7-132">Abilitare la crittografia su volumi con percorsi di montaggio</span><span class="sxs-lookup"><span data-stu-id="219c7-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="219c7-133">Abilitare la crittografia nelle macchine virtuali Linux configurate con striping del disco (RAID) tramite mdadm</span><span class="sxs-lookup"><span data-stu-id="219c7-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="219c7-134">Abilitare la crittografia nelle macchine virtuali Linux usando LVM per i dischi dati</span><span class="sxs-lookup"><span data-stu-id="219c7-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="219c7-135">Abilitare la crittografia nelle VM Windows configurate con spazi di archiviazione</span><span class="sxs-lookup"><span data-stu-id="219c7-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="219c7-136">Aggiornare le impostazioni di crittografia di una macchina virtuale non dotata di archiviazione Premium crittografata esistente</span><span class="sxs-lookup"><span data-stu-id="219c7-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="219c7-137">Sono supportate tutte le aree di Azure pubbliche e AzureGov</span><span class="sxs-lookup"><span data-stu-id="219c7-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="219c7-138">La soluzione non supporta gli scenari, le funzionalità e la tecnologia seguenti:</span><span class="sxs-lookup"><span data-stu-id="219c7-138">The solution does not support the following scenarios, features, and technology:</span></span>

* <span data-ttu-id="219c7-139">VM IaaS del piano Basic</span><span class="sxs-lookup"><span data-stu-id="219c7-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="219c7-140">Disabilitazione della crittografia in un'unità del sistema operativo per le VM IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="219c7-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="219c7-141">Disabilitazione della crittografia in un'unità di dati se l'unità del sistema operativo è crittografata per le macchine virtuali Iaas di Linux</span><span class="sxs-lookup"><span data-stu-id="219c7-141">Disabling encryption on a data drive if the OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="219c7-142">Macchine virtuali IaaS create usando il metodo di creazione classico per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="219c7-142">IaaS VMs that are created by using the classic VM creation method</span></span>
* <span data-ttu-id="219c7-143">La crittografia per le immagini personalizzate nelle macchine virtuali Windows e Linux IaaS NON è supportata.</span><span class="sxs-lookup"><span data-stu-id="219c7-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="219c7-144">La crittografia in disco del sistema operativo di Linux LVM non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="219c7-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="219c7-145">Questa compatibilità è di prossima integrazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-145">This support will come soon.</span></span>
* <span data-ttu-id="219c7-146">Integrazione con il servizio di gestione delle chiavi locale.</span><span class="sxs-lookup"><span data-stu-id="219c7-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="219c7-147">File di Azure (file system condiviso), file system di rete (NFS, Network File System), volumi dinamici e macchine virtuali Windows configurate con sistemi RAID basati su software</span><span class="sxs-lookup"><span data-stu-id="219c7-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="219c7-148">Backup e ripristino di macchine virtuali crittografate senza chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="219c7-149">Aggiornare le impostazioni di crittografia di una macchina virtuale con archiviazione Premium crittografata esistente.</span><span class="sxs-lookup"><span data-stu-id="219c7-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-150">Il backup e il ripristino delle macchine virtuali crittografate sono supportati solo per le VM crittografate con la configurazione della chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="219c7-151">Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="219c7-152">La chiave di crittografia della chiave è un parametro facoltativo che abilita la crittografia delle VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="219c7-153">Questo supporto sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="219c7-153">This support is coming soon.</span></span>
> <span data-ttu-id="219c7-154">L'aggiornamento delle impostazioni di crittografia di una macchina virtuale con archiviazione Premium crittografata esistente non è supportato.</span><span class="sxs-lookup"><span data-stu-id="219c7-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="219c7-155">Questo supporto sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="219c7-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="219c7-156">Funzionalità di crittografia</span><span class="sxs-lookup"><span data-stu-id="219c7-156">Encryption features</span></span>
<span data-ttu-id="219c7-157">Quando si abilita e si distribuisce la Crittografia dischi di Azure per le VM IaaS di Azure, sono abilitate le funzionalità seguenti, a seconda della configurazione fornita:</span><span class="sxs-lookup"><span data-stu-id="219c7-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span></span>

* <span data-ttu-id="219c7-158">Crittografia del volume del sistema operativo per proteggere il volume di avvio inattivo nella risorsa di archiviazione dell'utente</span><span class="sxs-lookup"><span data-stu-id="219c7-158">Encryption of the OS volume to protect the boot volume at rest in your storage</span></span>
* <span data-ttu-id="219c7-159">Crittografia dei volumi dati per proteggere i volumi dati inattivi nella risorsa di archiviazione dell'utente</span><span class="sxs-lookup"><span data-stu-id="219c7-159">Encryption of data volumes to protect the data volumes at rest in your storage</span></span>
* <span data-ttu-id="219c7-160">Disabilitazione della crittografia nel sistema operativo e nelle unità dati per le VM IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="219c7-160">Disabling encryption on the OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="219c7-161">Disabilitazione della crittografia nelle unità dati per le macchine virtuali IaaS Linux (solo se l'unità del sistema operativo NON È crittografata)</span><span class="sxs-lookup"><span data-stu-id="219c7-161">Disabling encryption on the data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="219c7-162">Protezione delle chiavi di crittografia e dei segreti nella sottoscrizione di Key Vault</span><span class="sxs-lookup"><span data-stu-id="219c7-162">Safeguarding the encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="219c7-163">Segnalazione dello stato di crittografia della macchina virtuale IaaS crittografata</span><span class="sxs-lookup"><span data-stu-id="219c7-163">Reporting the encryption status of the encrypted IaaS VM</span></span>
* <span data-ttu-id="219c7-164">Rimozione delle impostazioni di configurazione della crittografia del disco dalla macchina virtuale IaaS</span><span class="sxs-lookup"><span data-stu-id="219c7-164">Removal of disk-encryption configuration settings from the IaaS virtual machine</span></span>
* <span data-ttu-id="219c7-165">Backup e ripristino delle macchine virtuali crittografate usando il servizio Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-165">Backup and restore of encrypted VMs by using the Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-166">Il backup e il ripristino delle macchine virtuali crittografate sono supportati solo per le VM crittografate con la configurazione della chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="219c7-167">Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="219c7-168">La chiave di crittografia della chiave è un parametro facoltativo che abilita la crittografia delle VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="219c7-169">Crittografia dischi di Azure per macchine virtuali IaaS per soluzioni Windows e Linux include:</span><span class="sxs-lookup"><span data-stu-id="219c7-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="219c7-170">Estensione di crittografia del disco per Windows.</span><span class="sxs-lookup"><span data-stu-id="219c7-170">The disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="219c7-171">Estensione di crittografia del disco per Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-171">The disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="219c7-172">Cmdlet di PowerShell per la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="219c7-172">The disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="219c7-173">Cmdlet dell'interfaccia della riga di comando di Azure per la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="219c7-173">The disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="219c7-174">Modelli di Azure Resource Manager per la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="219c7-174">The disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="219c7-175">La soluzione Crittografia dischi di Azure è supportata nelle macchine virtuali IaaS in esecuzione in sistemi operativi Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-175">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="219c7-176">Per altre informazioni sui sistemi operativi supportati, vedere la sezione "Prerequisiti".</span><span class="sxs-lookup"><span data-stu-id="219c7-176">For more information about the supported operating systems, see the "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-177">Non è previsto alcun addebito aggiuntivo per la crittografia dei dischi delle macchine virtuali con Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="219c7-178">Proposta di valore</span><span class="sxs-lookup"><span data-stu-id="219c7-178">Value proposition</span></span>
<span data-ttu-id="219c7-179">Quando si applica la soluzione di gestione Crittografia dischi di Azure, è possibile soddisfare le esigenze aziendali seguenti:</span><span class="sxs-lookup"><span data-stu-id="219c7-179">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span></span>

* <span data-ttu-id="219c7-180">Le VM IaaS inattive sono protette perché è possibile usare la tecnologia di crittografia standard per soddisfare i requisiti di sicurezza e conformità dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span></span>
* <span data-ttu-id="219c7-181">Le macchine virtuali IaaS vengono avviate con chiavi e criteri controllati dai clienti ed è possibile controllarne l'utilizzo nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="219c7-182">Flusso di lavoro della crittografia</span><span class="sxs-lookup"><span data-stu-id="219c7-182">Encryption workflow</span></span>
<span data-ttu-id="219c7-183">Per abilitare la crittografia dei dischi per macchine virtuali Windows e Linux, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-183">To enable disk encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="219c7-184">Scegliere uno scenario di crittografia tra gli scenari di crittografia precedenti.</span><span class="sxs-lookup"><span data-stu-id="219c7-184">Choose an encryption scenario from among the preceding encryption scenarios.</span></span>
2. <span data-ttu-id="219c7-185">Acconsentire esplicitamente per abilitare la crittografia dei dischi tramite il modello di Resource Manager di Crittografia dischi di Azure, i cmdlet di PowerShell o un comando dell'interfaccia della riga di comando e specificare la configurazione della crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-185">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span></span>

   * <span data-ttu-id="219c7-186">Per lo scenario di disco rigido virtuale con crittografia del cliente, caricare il disco rigido virtuale crittografato nell'account di archiviazione e il materiale della chiave di crittografia nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-186">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span></span> <span data-ttu-id="219c7-187">Specificare quindi la configurazione della crittografia per abilitare la crittografia in una nuova macchina virtuale IaaS.</span><span class="sxs-lookup"><span data-stu-id="219c7-187">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="219c7-188">Per le nuove macchine virtuali create dal Marketplace e per le macchine virtuali esistenti già in esecuzione in Azure, specificare la configurazione della crittografia per abilitare la crittografia nella VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="219c7-188">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span></span>

3. <span data-ttu-id="219c7-189">Concedere l'accesso alla piattaforma Azure per la lettura del materiale della chiave di crittografia, ovvero le chiavi di crittografia BitLocker per i sistemi Windows e Passphrase per Linux, dall'insieme di credenziali delle chiavi locale per abilitare la crittografia nella VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="219c7-189">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span></span>

4. <span data-ttu-id="219c7-190">Specificare l'identità dell'applicazione di Azure Active Directory (Azure AD) per scrivere il materiale della chiave di crittografia nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-190">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span></span> <span data-ttu-id="219c7-191">Questa operazione abilita la crittografia nella macchina virtuale IaaS per gli scenari indicati nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="219c7-191">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="219c7-192">Azure aggiorna il modello del servizio della macchina virtuale con la crittografia e la configurazione dell'insieme di credenziali delle chiavi e quindi configura la VM crittografata.</span><span class="sxs-lookup"><span data-stu-id="219c7-192">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="219c7-194">Flusso di lavoro della decrittografia</span><span class="sxs-lookup"><span data-stu-id="219c7-194">Decryption workflow</span></span>
<span data-ttu-id="219c7-195">Per disabilitare la crittografia dei dischi per le macchine virtuali IaaS, seguire questa procedura generale:</span><span class="sxs-lookup"><span data-stu-id="219c7-195">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span></span>

1. <span data-ttu-id="219c7-196">Scegliere di disabilitare la crittografia (decrittografia) in una macchina virtuale IaaS in esecuzione in Azure tramite il modello di Resource Manager per Crittografia dischi di Azure o i cmdlet di PowerShell, quindi specificare la configurazione della crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-196">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span></span>

 <span data-ttu-id="219c7-197">Questo passaggio agisce sul volume dati o sul volume del sistema operativo o entrambi nella VM IaaS Windows in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="219c7-197">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="219c7-198">Come indicato nella sezione precedente, tuttavia, la disabilitazione della crittografia del disco del sistema operativo per Linux non è supportata.</span><span class="sxs-lookup"><span data-stu-id="219c7-198">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="219c7-199">Il passaggio di decrittografia è consentito solo per le unità dati nelle macchine virtuali Linux, purché l'unità del sistema operativo non sia crittografata.</span><span class="sxs-lookup"><span data-stu-id="219c7-199">The decryption step is allowed only for data drives on Linux VMs as long as the OS disk is not encrypted.</span></span>
2. <span data-ttu-id="219c7-200">Azure aggiorna il modello di servizi della macchina virtuale e la VM IaaS viene contrassegnata come decrittografata.</span><span class="sxs-lookup"><span data-stu-id="219c7-200">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span></span> <span data-ttu-id="219c7-201">Il contenuto inattivo della VM non viene più crittografato.</span><span class="sxs-lookup"><span data-stu-id="219c7-201">The contents of the VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-202">L'operazione di disabilitazione della crittografia non elimina l'insieme di credenziali delle chiavi e il materiale della chiave di crittografia, ovvero le chiavi di crittografia BitLocker per sistemi Windows o Passphrase per Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-202">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="219c7-203">La disabilitazione della crittografica del disco del sistema operativo per Linux non è supportata.</span><span class="sxs-lookup"><span data-stu-id="219c7-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="219c7-204">Il passaggio di decrittografia è consentito solo per le unità dati nelle macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-204">The decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="219c7-205">La disabilitazione della crittografia del disco dati per Linux non è supportata se l'unità del sistema operativo è crittografata.</span><span class="sxs-lookup"><span data-stu-id="219c7-205">Disabling data disk encryption for Linux is not supported if the OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="219c7-206">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="219c7-206">Prerequisites</span></span>
<span data-ttu-id="219c7-207">Prima di abilitare Crittografia dischi di Azure nelle macchine virtuali IaaS di Azure per gli scenari supportati illustrati nella sezione "Panoramica", vedere i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="219c7-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span></span>

* <span data-ttu-id="219c7-208">Per creare le risorse in Azure nella aree geografiche supportate, è necessario avere una sottoscrizione di Azure attiva e valida.</span><span class="sxs-lookup"><span data-stu-id="219c7-208">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span></span>
* <span data-ttu-id="219c7-209">Crittografia dischi di Azure è supportata nelle versioni di Windows Server seguenti: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="219c7-209">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="219c7-210">Crittografia dischi di Azure è supportato nelle versioni client di Windows seguenti: client Windows 8 e client Windows 10.</span><span class="sxs-lookup"><span data-stu-id="219c7-210">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-211">Per Windows Server 2008 R2 è necessario che .NET Framework 4.5 sia installato prima dell'abilitazione della crittografia in Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="219c7-212">È possibile installarlo da Windows Update tramite l'aggiornamento facoltativo Microsoft .NET Framework 4.5.2 per i sistemi Windows Server 2008 R2 basati su x64 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="219c7-212">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="219c7-213">Crittografia dischi di Azure è supportato nelle seguenti distribuzioni e versioni della raccolta di Azure basata sul server Linux:</span><span class="sxs-lookup"><span data-stu-id="219c7-213">Azure Disk Encryption is supported on the following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="219c7-214">Distribuzione Linux</span><span class="sxs-lookup"><span data-stu-id="219c7-214">Linux Distribution</span></span> | <span data-ttu-id="219c7-215">Versione</span><span class="sxs-lookup"><span data-stu-id="219c7-215">Version</span></span> | <span data-ttu-id="219c7-216">Tipo di volume supportato per la crittografia</span><span class="sxs-lookup"><span data-stu-id="219c7-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="219c7-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="219c7-217">Ubuntu</span></span> | <span data-ttu-id="219c7-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="219c7-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="219c7-219">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="219c7-219">OS and Data disk</span></span> |
| <span data-ttu-id="219c7-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="219c7-220">Ubuntu</span></span> | <span data-ttu-id="219c7-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="219c7-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="219c7-222">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="219c7-222">OS and Data disk</span></span> |
| <span data-ttu-id="219c7-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="219c7-223">Ubuntu</span></span> | <span data-ttu-id="219c7-224">12.10</span><span class="sxs-lookup"><span data-stu-id="219c7-224">12.10</span></span> | <span data-ttu-id="219c7-225">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-225">Data disk</span></span> |
| <span data-ttu-id="219c7-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="219c7-226">Ubuntu</span></span> | <span data-ttu-id="219c7-227">12.04</span><span class="sxs-lookup"><span data-stu-id="219c7-227">12.04</span></span> | <span data-ttu-id="219c7-228">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-228">Data disk</span></span> |
| <span data-ttu-id="219c7-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="219c7-229">RHEL</span></span> | <span data-ttu-id="219c7-230">7.3</span><span class="sxs-lookup"><span data-stu-id="219c7-230">7.3</span></span> | <span data-ttu-id="219c7-231">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="219c7-231">OS and Data disk</span></span> |
| <span data-ttu-id="219c7-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="219c7-232">RHEL</span></span> | <span data-ttu-id="219c7-233">7,2</span><span class="sxs-lookup"><span data-stu-id="219c7-233">7.2</span></span> | <span data-ttu-id="219c7-234">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="219c7-234">OS and Data disk</span></span> |
| <span data-ttu-id="219c7-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="219c7-235">RHEL</span></span> | <span data-ttu-id="219c7-236">6.8</span><span class="sxs-lookup"><span data-stu-id="219c7-236">6.8</span></span> | <span data-ttu-id="219c7-237">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="219c7-237">OS and Data disk</span></span> |
| <span data-ttu-id="219c7-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="219c7-238">RHEL</span></span> | <span data-ttu-id="219c7-239">6.7</span><span class="sxs-lookup"><span data-stu-id="219c7-239">6.7</span></span> | <span data-ttu-id="219c7-240">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-240">Data disk</span></span> |
| <span data-ttu-id="219c7-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="219c7-241">CentOS</span></span> | <span data-ttu-id="219c7-242">7.3</span><span class="sxs-lookup"><span data-stu-id="219c7-242">7.3</span></span> | <span data-ttu-id="219c7-243">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="219c7-243">OS and Data disk</span></span> |
| <span data-ttu-id="219c7-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="219c7-244">CentOS</span></span> | <span data-ttu-id="219c7-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="219c7-245">7.2n</span></span> | <span data-ttu-id="219c7-246">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="219c7-246">OS and Data disk</span></span> |
| <span data-ttu-id="219c7-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="219c7-247">CentOS</span></span> | <span data-ttu-id="219c7-248">6.8</span><span class="sxs-lookup"><span data-stu-id="219c7-248">6.8</span></span> | <span data-ttu-id="219c7-249">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="219c7-249">OS and Data disk</span></span> |
| <span data-ttu-id="219c7-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="219c7-250">CentOS</span></span> | <span data-ttu-id="219c7-251">7.1</span><span class="sxs-lookup"><span data-stu-id="219c7-251">7.1</span></span> | <span data-ttu-id="219c7-252">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-252">Data disk</span></span> |
| <span data-ttu-id="219c7-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="219c7-253">CentOS</span></span> | <span data-ttu-id="219c7-254">7.0</span><span class="sxs-lookup"><span data-stu-id="219c7-254">7.0</span></span> | <span data-ttu-id="219c7-255">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-255">Data disk</span></span> |
| <span data-ttu-id="219c7-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="219c7-256">CentOS</span></span> | <span data-ttu-id="219c7-257">6.7</span><span class="sxs-lookup"><span data-stu-id="219c7-257">6.7</span></span> | <span data-ttu-id="219c7-258">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-258">Data disk</span></span> |
| <span data-ttu-id="219c7-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="219c7-259">CentOS</span></span> | <span data-ttu-id="219c7-260">6.6</span><span class="sxs-lookup"><span data-stu-id="219c7-260">6.6</span></span> | <span data-ttu-id="219c7-261">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-261">Data disk</span></span> |
| <span data-ttu-id="219c7-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="219c7-262">CentOS</span></span> | <span data-ttu-id="219c7-263">6,5</span><span class="sxs-lookup"><span data-stu-id="219c7-263">6.5</span></span> | <span data-ttu-id="219c7-264">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-264">Data disk</span></span> |
| <span data-ttu-id="219c7-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="219c7-265">openSUSE</span></span> | <span data-ttu-id="219c7-266">13.2</span><span class="sxs-lookup"><span data-stu-id="219c7-266">13.2</span></span> | <span data-ttu-id="219c7-267">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-267">Data disk</span></span> |
| <span data-ttu-id="219c7-268">SLES</span><span class="sxs-lookup"><span data-stu-id="219c7-268">SLES</span></span> | <span data-ttu-id="219c7-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="219c7-269">12 SP1</span></span> | <span data-ttu-id="219c7-270">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-270">Data disk</span></span> |
| <span data-ttu-id="219c7-271">SLES</span><span class="sxs-lookup"><span data-stu-id="219c7-271">SLES</span></span> | <span data-ttu-id="219c7-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="219c7-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="219c7-273">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-273">Data disk</span></span> |
| <span data-ttu-id="219c7-274">SLES</span><span class="sxs-lookup"><span data-stu-id="219c7-274">SLES</span></span> | <span data-ttu-id="219c7-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="219c7-275">HPC 12</span></span> | <span data-ttu-id="219c7-276">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-276">Data disk</span></span> |
| <span data-ttu-id="219c7-277">SLES</span><span class="sxs-lookup"><span data-stu-id="219c7-277">SLES</span></span> | <span data-ttu-id="219c7-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="219c7-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="219c7-279">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-279">Data disk</span></span> |
| <span data-ttu-id="219c7-280">SLES</span><span class="sxs-lookup"><span data-stu-id="219c7-280">SLES</span></span> | <span data-ttu-id="219c7-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="219c7-281">11 SP4</span></span> | <span data-ttu-id="219c7-282">Disco dati</span><span class="sxs-lookup"><span data-stu-id="219c7-282">Data disk</span></span> |

* <span data-ttu-id="219c7-283">Crittografia dischi di Azure richiede che l'insieme di credenziali delle chiavi e le macchine virtuali si trovino nella stessa area e sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-283">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-284">La configurazione delle risorse in aree separate causa un errore nell'attivazione della funzionalità Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-284">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="219c7-285">Per installare e configurare l'insieme di credenziali delle chiavi per Crittografia dischi di Azure, vedere la sezione **Installare e configurare l'insieme di credenziali delle chiavi per Crittografia dischi di Azure** nella sezione *Prerequisiti* di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="219c7-285">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="219c7-286">Per impostare e configurare l'applicazione Azure AD in Azure Active Directory per Crittografia dischi di Azure, vedere la sezione **Installare l'applicazione Azure AD in Azure Active Directory** nella sezione *Prerequisiti* di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="219c7-286">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="219c7-287">Per impostare e configurare i criteri di accesso dell'insieme di credenziali delle chiavi per l'applicazione Azure AD, vedere la sezione **Configurare i criteri di accesso per l'insieme di credenziali delle chiavi per l'applicazione Azure AD** nella sezione *Prerequisiti* di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="219c7-287">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="219c7-288">Per preparare un disco rigido virtuale Windows pre-crittografato, vedere la sezione **Preparare un disco rigido virtuale Windows pre-crittografato** nell'*Appendice*.</span><span class="sxs-lookup"><span data-stu-id="219c7-288">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="219c7-289">Per preparare un disco rigido virtuale Linux pre-crittografato, vedere la sezione **Preparare un disco rigido virtuale Linux pre-crittografato** nell'*Appendice*.</span><span class="sxs-lookup"><span data-stu-id="219c7-289">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="219c7-290">La piattaforma Azure deve avere accesso alle chiavi di crittografia o ai segreti nell'insieme di credenziali delle chiavi per renderli disponibili alla macchina virtuale in fase di avvio e di decrittografia del volume del sistema operativo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-290">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span></span> <span data-ttu-id="219c7-291">Per concedere autorizzazioni alla piattaforma Azure, impostare la proprietà **EnabledForDiskEncryption** nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-291">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span></span> <span data-ttu-id="219c7-292">Per altre informazioni, vedere **Installare e configurare l'insieme di credenziali delle chiavi per Crittografia dischi di Azure** nell'Appendice.</span><span class="sxs-lookup"><span data-stu-id="219c7-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span></span>
* <span data-ttu-id="219c7-293">È necessario applicare il controllo delle versioni agli URL del segreto dell'insieme di credenziali delle chiavi e della chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="219c7-294">Azure applica questa restrizione relativa al controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="219c7-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="219c7-295">Per informazioni sugli URL del segreto e della chiave di crittografia della chiave validi, vedere gli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="219c7-295">For valid secret and KEK URLs, see the following examples:</span></span>

  * <span data-ttu-id="219c7-296">Esempio di URL segreto valido: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="219c7-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="219c7-297">Esempio di URL della chiave di crittografia della chiave valido: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="219c7-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="219c7-298">Crittografia dischi di Azure non supporta la possibilità di specificare i numeri di porta come parte dei segreti dell'insieme di credenziali delle chiavi e degli URL della chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="219c7-299">Ecco alcuni esempi di URL di insiemi di credenziali delle chiavi non supportati e supportati:</span><span class="sxs-lookup"><span data-stu-id="219c7-299">For examples of non-supported and supported key vault URLs, see the following:</span></span>

  * <span data-ttu-id="219c7-300">URL dell'insieme di credenziali delle chiavi non accettabile: *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="219c7-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="219c7-301">URL dell'insieme di credenziali delle chiavi accettabile: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="219c7-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="219c7-302">Per abilitare la funzionalità Crittografia dischi di Azure, le VM IaaS devono soddisfare i requisiti di configurazione degli endpoint di rete seguenti:</span><span class="sxs-lookup"><span data-stu-id="219c7-302">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="219c7-303">Per ottenere un token per la connessione all'insieme di credenziali delle chiavi, è necessario che la macchina virtuale IaaS possa connettersi a un endpoint di Azure Active Directory, \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="219c7-303">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="219c7-304">Per scrivere le chiavi di crittografia nell'insieme di credenziali delle chiavi, è necessario che la macchina virtuale IaaS possa connettersi all'endpoint dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-304">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span></span>
  * <span data-ttu-id="219c7-305">La VM IaaS deve potersi connettere a un endpoint di archiviazione di Azure che ospita il repository delle estensioni di Azure e a un account di archiviazione di Azure che ospita i file del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-305">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="219c7-306">Se i criteri di sicurezza limitano l'accesso dalle macchine virtuali di Azure a Internet, è possibile risolvere l'URI precedente e configurare una regola specifica per consentire la connettività in uscita agli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="219c7-306">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span></span>
  >
  ><span data-ttu-id="219c7-307">Per configurare e accedere ad Azure Key Vault dietro un firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="219c7-307">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="219c7-308">Usare la versione più recente della versione di Azure PowerShell SDK per configurare Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-308">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span></span> <span data-ttu-id="219c7-309">Scaricare la versione più recente di [Azure PowerShell](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="219c7-309">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="219c7-310">Crittografia dischi di Azure non è supportata in [Azure PowerShell SDK versione 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="219c7-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="219c7-311">Se viene visualizzato un errore relativo all'uso di Azure PowerShell 1.1.0, vedere [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx) (Errore di Crittografia dischi di Azure correlato ad Azure PowerShell 1.1.0).</span><span class="sxs-lookup"><span data-stu-id="219c7-311">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="219c7-312">Per eseguire uno dei comandi dell'interfaccia della riga di comando di Azure e associarla alla sottoscrizione di Azure, è necessario installare prima di tutto l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="219c7-312">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="219c7-313">Per installare l'interfaccia della riga di comando di Azure e associarla alla sottoscrizione di Azure, vedere [Come installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="219c7-313">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="219c7-314">Per usare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows con Azure Resource Manager, vedere [Comandi dell'interfaccia della riga di comando Azure in modalità Resource Manager](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="219c7-314">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="219c7-315">Per la crittografia di un disco gestito, è un prerequisito obbligatorio eseguire uno snapshot del disco gestito o un backup del disco all'esterno di Crittografia dischi di Azure prima di abilitare la crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-315">When encrypting a managed disk, it is mandatory prerequisite to take a snapshot of the managed disk or a backup of the disk outside of Azure Disk Encryption prior to enabling encryption.</span></span>  <span data-ttu-id="219c7-316">In mancanza di un backup, qualsiasi errore imprevisto durante la crittografia potrebbe rendere il disco e la macchina virtuale inaccessibili senza possibilità di ripristino.</span><span class="sxs-lookup"><span data-stu-id="219c7-316">Without a backup in place, any unexpected failure during encryption may render the disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="219c7-317">Set-AzureRmVMDiskEncryptionExtension attualmente non esegue il backup dei dischi gestiti e genera un errore se viene usato su un disco gestito, a meno che non sia stato specificato il parametro -skipVmBackup.</span><span class="sxs-lookup"><span data-stu-id="219c7-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless the -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="219c7-318">Questo parametro non è sicuro da usare, a meno che non sia già stato eseguito un backup all'esterno di Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-318">This parameter is unsafe to use unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="219c7-319">Quando si specifica il parametro -skipVmBackup, il cmdlet non effettua una copia di backup del disco gestito prima della crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-319">When the -skipVmBackup parameter is specified, the cmdlet will not make a backup of the managed disk prior to encryption.</span></span>  <span data-ttu-id="219c7-320">Per questo motivo, viene considerato un prerequisito obbligatorio assicurarsi di aver eseguito un backup della macchina virtuale con il disco gestito prima di abilitare Crittografia dischi di Azure, nel caso sia necessario il ripristino in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="219c7-320">For this reason, it is considered a mandatory prerequisite to make sure a backup of the managed disk VM is in place prior to enabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="219c7-321">Il parametro -skipVmBackup non deve mai essere usato, a meno che non sia già stato eseguito uno snapshot o un backup all'esterno di Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-321">The -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="219c7-322">La soluzione Crittografia dischi di Azure usa la protezione con chiave esterna BitLocker per macchine virtuali IaaS Windows.</span><span class="sxs-lookup"><span data-stu-id="219c7-322">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="219c7-323">Per le macchine virtuali sono aggiunte a un dominio, NON eseguire il push di criteri di gruppo che applichino protezioni TPM.</span><span class="sxs-lookup"><span data-stu-id="219c7-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="219c7-324">Per informazioni sui Criteri di gruppo per consentire BitLocker senza un TPM compatibile, vedere [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521) (Informazioni di riferimento sui Criteri di gruppo BitLocker).</span><span class="sxs-lookup"><span data-stu-id="219c7-324">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="219c7-325">I criteri di BitLocker nelle macchine virtuali aggiunte a un dominio con criteri di gruppo personalizzati devono includere l'impostazione seguente: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Crittografia dischi di Azure avrà esito negativo quando le impostazioni dei criteri di gruppo personalizzati per BitLocker sono incompatibili.</span><span class="sxs-lookup"><span data-stu-id="219c7-325">Bitlocker policy on domain joined virtual machines with custom group policy must include the following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="219c7-326">Nei computer che non dispongono dell'impostazione dei criteri corretta potrebbe essere necessario applicare i nuovi criteri, forzare l'aggiornamento dei nuovi criteri (gpupdate.exe /force) e quindi eseguire il riavvio.</span><span class="sxs-lookup"><span data-stu-id="219c7-326">On machines that did not have the correct policy setting, applying the new policy, forcing the new policy to update (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="219c7-327">Per creare un'applicazione Azure AD, creare un insieme di credenziali delle chiavi o configurare un insieme di credenziali delle chiavi esistente e abilitare la crittografia, vedere lo [script di PowerShell prerequisito per Crittografia dischi di Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="219c7-327">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="219c7-328">Per configurare i prerequisiti della crittografia dei dischi usando l'interfaccia della riga di comando, vedere [questo script Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="219c7-328">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="219c7-329">Per usare il servizio Backup di Azure per eseguire il backup e ripristinare le macchine virtuali crittografate, quando la crittografia è abilitata con Crittografia dischi di Azure, crittografare le VM usando la configurazione delle chiavi di Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-329">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="219c7-330">Il servizio Backup supporta le macchine virtuali crittografate usando solo la configurazione della chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-330">The Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="219c7-331">Vedere [Come eseguire il backup e il ripristino delle macchine virtuali crittografate con il Backup di Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="219c7-331">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="219c7-332">Per la crittografia di un volume del sistema operativo Linux, è attualmente necessario un riavvio della macchina virtuale al termine del processo.</span><span class="sxs-lookup"><span data-stu-id="219c7-332">When encrypting a Linux OS volume, note that a VM restart is currently required at the end of the process.</span></span> <span data-ttu-id="219c7-333">Questa operazione può essere eseguita tramite il portale, PowerShell o l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="219c7-333">This can be done via the portal, powershell, or CLI.</span></span>   <span data-ttu-id="219c7-334">Per monitorare l'avanzamento della crittografia, eseguire periodicamente il polling del messaggio di stato restituito da Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span><span class="sxs-lookup"><span data-stu-id="219c7-334">To track the progress of encryption, periodically poll the status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="219c7-335">Al termine della crittografia, il messaggio di stato restituito da questo comando indicherà che l'operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="219c7-335">Once encryption is complete, the the status message returned by this command will indicate this.</span></span>  <span data-ttu-id="219c7-336">Ad esempio, "ProgressMessage: OS disk successfully encrypted, please reboot the VM" (ProgressMessage: disco del sistema operativo crittografato, riavviare la macchina virtuale). A questo punto, la macchina virtuale può essere riavviata e usata.</span><span class="sxs-lookup"><span data-stu-id="219c7-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot the VM"  At this point the VM can be restarted and used.</span></span>  

* <span data-ttu-id="219c7-337">Crittografia dischi di Azure per Linux richiede che i dischi dati abbiano un file system montato in Linux prima della crittografia</span><span class="sxs-lookup"><span data-stu-id="219c7-337">Azure Disk Encryption for Linux requires data disks to have a mounted file system in Linux prior to encryption</span></span>

* <span data-ttu-id="219c7-338">I dischi dati montati in modo ricorsivo non sono supportati da Crittografia dischi di Azure per Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-338">Recursively mounted data disks are not supported by the Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="219c7-339">Se ad esempio nel sistema di destinazione è stato eseguito il montaggio di un disco in /foo/bar e quindi di un altro disco in /foo/bar/baz, la crittografia di /foo/bar/baz verrà eseguita, mentre quella di /foo/bar avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-339">For example, if the target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, the encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="219c7-340">Crittografia dischi di Azure è supportata solo nelle immagini supportate della raccolta di Azure che soddisfano i prerequisiti menzionati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="219c7-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet the aforementioned prerequisites.</span></span> <span data-ttu-id="219c7-341">Le immagini personalizzate non sono supportate a causa degli schemi di partizione e dei comportamenti dei processi personalizzati che possono essere presenti in queste immagini.</span><span class="sxs-lookup"><span data-stu-id="219c7-341">Customer custom images are not supported due to custom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="219c7-342">Inoltre, potrebbero risultare incompatibili anche le macchine virtuali basate su immagini della raccolta che inizialmente soddisfacevano i prerequisiti ma che sono state modificate dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="219c7-343">Per tale motivo, la procedura consigliata per la crittografia di una macchina virtuale Linux prevede di partire da un'immagine della raccolta pulita, crittografare la macchina virtuale e quindi aggiungere alla macchina virtuale il software o i dati personalizzati in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="219c7-343">For that reason, the suggested procedure for encrypting a Linux VM is to start from a clean gallery image, encrypt the VM, and then add custom software or data to the VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="219c7-344">Il backup e il ripristino delle macchine virtuali crittografate sono supportati solo per le VM crittografate con la configurazione della chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="219c7-345">Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="219c7-346">La chiave di crittografia della chiave è un parametro facoltativo che abilita la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-the-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="219c7-347">Configurare l'applicazione Azure AD in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="219c7-347">Set up the Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="219c7-348">Quando è necessario abilitare la crittografia in una macchina virtuale in esecuzione in Azure, Crittografia dischi di Azure genera e scrive le chiavi di crittografia nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-348">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span></span> <span data-ttu-id="219c7-349">La gestione delle chiavi di crittografia nell'insieme di credenziali delle chiavi richiede l'autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="219c7-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="219c7-350">Creare quindi un'applicazione Azure AD per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="219c7-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="219c7-351">Per informazioni dettagliate sulla procedura di registrazione di un'applicazione, vedere la sezione relativa al recupero di un'identità per l'applicazione del post di blog [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx) (Procedura dettagliata per Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="219c7-351">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="219c7-352">Questo post include anche alcuni esempi utili per l'installazione e la configurazione dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="219c7-353">Ai fini dell'autenticazione, è possibile usare l'autenticazione basata sul segreto client o l'autenticazione di Azure AD basata sul certificato client.</span><span class="sxs-lookup"><span data-stu-id="219c7-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="219c7-354">Autenticazione basata su segreto client per Azure AD</span><span class="sxs-lookup"><span data-stu-id="219c7-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="219c7-355">Le sezioni seguenti sono utili per configurare l'autenticazione basata sul segreto client per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="219c7-355">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="219c7-356">Creare un'applicazione Azure AD usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="219c7-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="219c7-357">Usare il cmdlet di PowerShell seguenti per creare un'applicazione Azure AD:</span><span class="sxs-lookup"><span data-stu-id="219c7-357">Use the following PowerShell cmdlet to create an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="219c7-358">$azureAdApplication.ApplicationId è l'ID client di Azure AD e $aadClientSecret è il segreto client da usare in seguito per abilitare Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-358">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span></span> <span data-ttu-id="219c7-359">Proteggere correttamente il segreto client di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="219c7-359">Safeguard the Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-the-azure-ad-client-id-and-secret-from-the-azure-classic-portal"></a><span data-ttu-id="219c7-360">Configurazione dell'ID client e del segreto client di Azure AD dal portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="219c7-360">Setting up the Azure AD client ID and secret from the Azure classic portal</span></span>
<span data-ttu-id="219c7-361">È anche possibile configurare l'ID e il segreto del client di Azure AD usando il [portale di Azure classico]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="219c7-361">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="219c7-362">Per eseguire questa operazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-362">To perform this task, do the following:</span></span>

1. <span data-ttu-id="219c7-363">Fare clic sulla scheda **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="219c7-363">Click the **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="219c7-365">Fare clic su **Aggiungi applicazione**, quindi immettere il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-365">Click **Add Application**, and then type the application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="219c7-367">Fare clic sul pulsante con la freccia, quindi configurare le proprietà dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-367">Click the arrow button, and then configure the application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="219c7-369">Fare clic sul segno di spunta nell'angolo in basso a sinistra per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-369">Click the check mark in the lower left corner to finish.</span></span> <span data-ttu-id="219c7-370">Viene visualizzata la pagina di configurazione dell'applicazione e l'ID client di Azure AD è disponibile nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="219c7-370">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="219c7-372">Per salvare il segreto client di Azure AD usare il pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="219c7-372">Save the Azure AD client secret by clicking the **Save** button.</span></span> <span data-ttu-id="219c7-373">Si noti che il segreto client di Azure AD nella casella di testo delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-373">Note the Azure AD client secret in the keys text box.</span></span> <span data-ttu-id="219c7-374">Proteggerlo correttamente.</span><span class="sxs-lookup"><span data-stu-id="219c7-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="219c7-376">Il flusso precedente non è supportato nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="219c7-376">The preceding flow is not supported on the Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="219c7-377">Usare un'applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="219c7-377">Use an existing application</span></span>
<span data-ttu-id="219c7-378">Per eseguire i comandi seguenti, ottenere e usare il [modulo Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="219c7-378">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-379">I comandi seguenti devono essere eseguiti da una nuova finestra di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="219c7-379">The following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="219c7-380">Non usare Azure PowerShell o la finestra di Azure Resource Manager per eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="219c7-380">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span></span> <span data-ttu-id="219c7-381">È consigliabile usare questo approccio perché questi cmdlet sono disponibili nel modulo MSOnline o in Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="219c7-381">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="219c7-382">Autenticazione basata su certificato per Azure AD</span><span class="sxs-lookup"><span data-stu-id="219c7-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="219c7-383">L'autenticazione basata su certificato per Azure AD non è attualmente supportata nelle VM Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="219c7-384">Le sezioni seguenti illustrano come configurare l'autenticazione basata su certificato per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="219c7-384">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="219c7-385">Creare un'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="219c7-385">Create an Azure AD application</span></span>
<span data-ttu-id="219c7-386">Per creare un'applicazione Azure AD, eseguire i cmdlet di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="219c7-386">To create an Azure AD application, execute the following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-387">Sostituire la stringa `yourpassword` seguente con la password sicura e proteggere la password.</span><span class="sxs-lookup"><span data-stu-id="219c7-387">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="219c7-388">Dopo avere completato questo passaggio, caricare un file PFX nell'insieme di credenziali delle chiavi e abilitare i criteri di accesso necessari per distribuire il certificato a una VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-388">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="219c7-389">Usare un'applicazione Azure AD esistente</span><span class="sxs-lookup"><span data-stu-id="219c7-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="219c7-390">Se si configura l'autenticazione basata su certificato per un'applicazione esistente, usare i cmdlet di PowerShell seguenti.</span><span class="sxs-lookup"><span data-stu-id="219c7-390">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span></span> <span data-ttu-id="219c7-391">Assicurarsi di eseguirli in una nuova finestra di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="219c7-391">Be sure to execute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="219c7-392">Dopo avere completato questo passaggio, caricare un file PFX nell'insieme di credenziali delle chiavi e abilitare i criteri di accesso necessari per distribuire il certificato a una VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-392">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span></span>

##### <a name="upload-a-pfx-file-to-your-key-vault"></a><span data-ttu-id="219c7-393">Caricare un file PFX nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="219c7-393">Upload a PFX file to your key vault</span></span>
<span data-ttu-id="219c7-394">Per una spiegazione dettagliata di questo processo, vedere [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx) (Blog ufficiale del team di Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="219c7-394">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="219c7-395">I cmdlet di PowerShell seguenti sono comunque tutto ciò che serve per questa attività.</span><span class="sxs-lookup"><span data-stu-id="219c7-395">However, the following PowerShell cmdlets are all you need for the task.</span></span> <span data-ttu-id="219c7-396">Accertarsi di eseguirli dalla console di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="219c7-396">Be sure to execute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-397">Sostituire la stringa `yourpassword` seguente con la password sicura e proteggere la password.</span><span class="sxs-lookup"><span data-stu-id="219c7-397">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-to-an-existing-vm"></a><span data-ttu-id="219c7-398">Distribuire un certificato nell'insieme di credenziali delle chiavi in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="219c7-398">Deploy a certificate in your key vault to an existing VM</span></span>
<span data-ttu-id="219c7-399">Al termine del caricamento del file PFX, distribuire un certificato disponibile nell'insieme di credenziali delle chiavi in una VM esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-399">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-the-key-vault-access-policy-for-the-azure-ad-application"></a><span data-ttu-id="219c7-400">Configurare i criteri di accesso per l'insieme di credenziali delle chiavi per l'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="219c7-400">Set up the key vault access policy for the Azure AD application</span></span>
<span data-ttu-id="219c7-401">L'applicazione Azure AD deve avere i diritti di accesso alle chiavi o ai segreti nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="219c7-401">Your Azure AD application needs rights to access the keys or secrets in the vault.</span></span> <span data-ttu-id="219c7-402">Usare il cmdlet [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) per concedere le autorizzazioni all'applicazione con l'ID client, generato al momento della registrazione dell'applicazione, come valore del parametro _–ServicePrincipalName_.</span><span class="sxs-lookup"><span data-stu-id="219c7-402">Use the [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="219c7-403">Per altre informazioni, vedere il post di blog [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx) (Procedura dettagliata per Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="219c7-403">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="219c7-404">Ecco un esempio dell'esecuzione di questa attività tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="219c7-404">Here is an example of how to perform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="219c7-405">Crittografia dischi di Azure richiede la configurazione di criteri di accesso all'applicazione client di Azure AD, ovvero le autorizzazioni _WrapKey_ e _Set_.</span><span class="sxs-lookup"><span data-stu-id="219c7-405">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="219c7-406">Terminologia</span><span class="sxs-lookup"><span data-stu-id="219c7-406">Terminology</span></span>
<span data-ttu-id="219c7-407">Per informazioni su alcuni dei termini comuni usati da questa tecnologia, vedere la tabella terminologica seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-407">To understand some of the common terms used by this technology, use the following terminology table:</span></span>

| <span data-ttu-id="219c7-408">Terminologia</span><span class="sxs-lookup"><span data-stu-id="219c7-408">Terminology</span></span> | <span data-ttu-id="219c7-409">Definizione</span><span class="sxs-lookup"><span data-stu-id="219c7-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="219c7-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="219c7-410">Azure AD</span></span> | <span data-ttu-id="219c7-411">Azure AD è l'abbreviazione di [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="219c7-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="219c7-412">Un account Azure AD è un prerequisito per le operazioni di autenticazione, archiviazione e recupero dei segreti da un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="219c7-413">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="219c7-413">Azure Key Vault</span></span> | <span data-ttu-id="219c7-414">Key Vault è un servizio di crittografia e gestione delle chiavi basato su moduli di sicurezza hardware convalidati dagli standard FIPS (Federal Information Processing Standards), che consentono di proteggere le chiavi crittografiche e i segreti sensibili.</span><span class="sxs-lookup"><span data-stu-id="219c7-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="219c7-415">Per altre informazioni, vedere la documentazione di [Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="219c7-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="219c7-416">ARM</span><span class="sxs-lookup"><span data-stu-id="219c7-416">ARM</span></span> | <span data-ttu-id="219c7-417">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="219c7-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="219c7-418">BitLocker</span></span> |<span data-ttu-id="219c7-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) è una tecnologia di crittografia del volume di Windows riconosciuta nel settore, usata per abilitare la crittografia dei dischi nelle macchine virtuali IaaS di Windows.</span><span class="sxs-lookup"><span data-stu-id="219c7-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="219c7-420">BEK</span><span class="sxs-lookup"><span data-stu-id="219c7-420">BEK</span></span> | <span data-ttu-id="219c7-421">Le chiavi di crittografia BitLocker vengono usate per crittografare il volume di avvio del sistema operativo e i volumi dati.</span><span class="sxs-lookup"><span data-stu-id="219c7-421">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span></span> <span data-ttu-id="219c7-422">Le chiavi BitLocker sono protette nell'insieme di credenziali delle chiavi come segreti.</span><span class="sxs-lookup"><span data-stu-id="219c7-422">The BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="219c7-423">CLI</span><span class="sxs-lookup"><span data-stu-id="219c7-423">CLI</span></span> | <span data-ttu-id="219c7-424">Vedere [Interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="219c7-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="219c7-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="219c7-425">DM-Crypt</span></span> |<span data-ttu-id="219c7-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) è il sottosistema di crittografia del disco trasparente basato su Linux usato per abilitare la crittografia del disco nelle macchine virtuali IaaS Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="219c7-427">KEK</span><span class="sxs-lookup"><span data-stu-id="219c7-427">KEK</span></span> | <span data-ttu-id="219c7-428">La chiave di crittografia della chiave (KEK, Key Encryption Key) è la chiave asimmetrica (RSA 2048) che è possibile usare per proteggere o per eseguire il wrapping del segreto.</span><span class="sxs-lookup"><span data-stu-id="219c7-428">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span></span> <span data-ttu-id="219c7-429">È possibile fornire una chiave protetta tramite modulo di protezione hardware o una chiave protetta tramite software.</span><span class="sxs-lookup"><span data-stu-id="219c7-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="219c7-430">Per altre informazioni, vedere la documentazione di [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="219c7-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="219c7-431">Cmdlet PS</span><span class="sxs-lookup"><span data-stu-id="219c7-431">PS cmdlets</span></span> | <span data-ttu-id="219c7-432">Vedere [Azure PowerShell cmdlets](/powershell/azure/overview) (Cmdlet di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="219c7-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="219c7-433">Installare e configurare l'insieme di credenziali delle chiavi per Crittografia dischi di Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="219c7-434">Crittografia dischi di Azure consente di proteggere le chiavi di crittografia e i segreti dei dischi nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-434">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="219c7-435">Per configurare l'insieme di credenziali delle chiavi per Crittografia dischi di Azure, completare i passaggi in ogni sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="219c7-435">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="219c7-436">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="219c7-436">Create a key vault</span></span>
<span data-ttu-id="219c7-437">Per creare un insieme di credenziali delle chiavi, usare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="219c7-437">To create a key vault, use one of the following options:</span></span>

* [<span data-ttu-id="219c7-438">Modello di Resource Manager "101-Key-Vault-Create"</span><span class="sxs-lookup"><span data-stu-id="219c7-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* <span data-ttu-id="219c7-439">[Azure PowerShell key vault cmdlets](/powershell/module/azurerm.keyvault/#key_vault) (Cmdlet dell'insieme di credenziali delle chiavi di Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="219c7-439">[Azure PowerShell key vault cmdlets](/powershell/module/azurerm.keyvault/#key_vault)</span></span>
* <span data-ttu-id="219c7-440">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-440">Azure Resource Manager</span></span>
* <span data-ttu-id="219c7-441">Come [proteggere l'insieme di credenziali delle chiavi](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="219c7-441">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-442">Se è già stato configurato un insieme di credenziali delle chiavi per la sottoscrizione, passare alla sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="219c7-442">If you have already set up a key vault for your subscription, skip to the next section.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="219c7-444">Configurare una chiave di crittografia della chiave (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="219c7-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="219c7-445">Se si vuole usare una chiave di crittografia della chiave per un livello aggiuntivo di sicurezza per le chiavi di crittografia BitLocker aggiungere una chiave di crittografia della chiave all'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-445">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span></span> <span data-ttu-id="219c7-446">Usare il cmdlet [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) per creare una chiave di crittografia della chiave nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-446">Use the [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to create a key encryption key in the key vault.</span></span> <span data-ttu-id="219c7-447">È anche possibile importare una chiave di crittografia della chiave dal modulo di protezione hardware di gestione delle chiavi locale.</span><span class="sxs-lookup"><span data-stu-id="219c7-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="219c7-448">Per altre informazioni, vedere la [Documentazione su Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="219c7-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="219c7-449">È possibile aggiungere la chiave di crittografia della chiave passando ad Azure Resource Manager o usando l'interfaccia di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="219c7-449">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="219c7-451">Configurare le autorizzazioni dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="219c7-451">Set key vault permissions</span></span>
<span data-ttu-id="219c7-452">La piattaforma Azure deve avere accesso alle chiavi di crittografia o i segreti nell'insieme di credenziali delle chiavi per renderli disponibili alla macchina virtuale per l'avvio e la decrittografia dei volumi.</span><span class="sxs-lookup"><span data-stu-id="219c7-452">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="219c7-453">Per concedere autorizzazioni alla piattaforma Azure, configurare la proprietà **EnabledForDiskEncryption** nell'insieme di credenziali delle chiavi usando il cmdlet di PowerShell relativo all'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="219c7-453">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="219c7-454">È anche possibile configurare la proprietà **EnabledForDiskEncryption** in [Azure Resource Explorer](https://resources.azure.com) (Esplora risorse di Azure).</span><span class="sxs-lookup"><span data-stu-id="219c7-454">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="219c7-455">Come indicato in precedenza, è necessario configurare la proprietà **EnabledForDiskEncryption** nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-455">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="219c7-456">In caso contrario, la distribuzione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-456">Otherwise, the deployment will fail.</span></span>

<span data-ttu-id="219c7-457">È possibile configurare i criteri di accesso per l'applicazione Azure AD dall'interfaccia di Key Vault:</span><span class="sxs-lookup"><span data-stu-id="219c7-457">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="219c7-460">Nella scheda **Criteri di accesso avanzati** assicurarsi che l'insieme di credenziali delle chiavi sia abilitato per Crittografia dischi di Azure:</span><span class="sxs-lookup"><span data-stu-id="219c7-460">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="219c7-462">Scenari di distribuzione della crittografia dei dischi ed esperienze utente</span><span class="sxs-lookup"><span data-stu-id="219c7-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="219c7-463">È possibile abilitare molti scenari di crittografia dei dischi e la procedura può variare in base allo scenario.</span><span class="sxs-lookup"><span data-stu-id="219c7-463">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span></span> <span data-ttu-id="219c7-464">Le sezioni seguenti illustrano in modo più dettagliato gli scenari.</span><span class="sxs-lookup"><span data-stu-id="219c7-464">The following sections cover the scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-the-marketplace"></a><span data-ttu-id="219c7-465">Abilitare la crittografia nelle nuove macchine virtuali IaaS create dal Marketplace</span><span class="sxs-lookup"><span data-stu-id="219c7-465">Enable encryption on new IaaS VMs that are created from the Marketplace</span></span>
<span data-ttu-id="219c7-466">È possibile abilitare la crittografia dei dischi nella nuova macchina virtuale IaaS Windows dal Marketplace in Azure usando il modello di [Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="219c7-466">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="219c7-467">Nel modello di avvio rapido di Azure fare clic su **Distribuisci in Azure**, immettere la configurazione della crittografia nel pannello **Parametri**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="219c7-467">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="219c7-468">Selezionare la sottoscrizione, il gruppo di risorse, la posizione del gruppo di risorse, le note legali e il contratto, quindi fare clic su **Crea** per abilitare la crittografia in una nuova macchina virtuale IaaS.</span><span class="sxs-lookup"><span data-stu-id="219c7-468">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-469">Questo modello crea una nuova VM Windows crittografata che usa l'immagine della raccolta di Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="219c7-469">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="219c7-470">È possibile abilitare la crittografia dei dischi in una nuova macchina virtuale IaaS RedHat Linux 7.2 con una matrice RAID-0 da 200 GB usando questo modello di [Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="219c7-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="219c7-471">Dopo la distribuzione del modello, verificare lo stato della crittografia della macchina virtuale usando il cmdlet `Get-AzureRmVmDiskEncryptionStatus`, come descritto in [Crittografia dell'unità del sistema operativo in una VM Linux in esecuzione](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="219c7-471">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="219c7-472">Quando la macchina virtuale restituisce uno stato _VMRestartPending_, riavviarla.</span><span class="sxs-lookup"><span data-stu-id="219c7-472">When the machine returns a status of _VMRestartPending_, restart the VM.</span></span>

<span data-ttu-id="219c7-473">La tabella seguente elenca i parametri del modello di Resource Manager per lo scenario con nuove macchine virtuali dal Marketplace con ID client di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="219c7-473">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="219c7-474">Parametro</span><span class="sxs-lookup"><span data-stu-id="219c7-474">Parameter</span></span> | <span data-ttu-id="219c7-475">Descrizione</span><span class="sxs-lookup"><span data-stu-id="219c7-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="219c7-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="219c7-476">adminUserName</span></span> | <span data-ttu-id="219c7-477">Nome utente dell'amministratore per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-477">Admin user name for the virtual machine.</span></span> |
| <span data-ttu-id="219c7-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="219c7-478">adminPassword</span></span> | <span data-ttu-id="219c7-479">Password utente dell'amministratore per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-479">Admin user password for the virtual machine.</span></span> |
| <span data-ttu-id="219c7-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="219c7-480">newStorageAccountName</span></span> | <span data-ttu-id="219c7-481">Nome dell'account di archiviazione per archiviare i dischi rigidi virtuali di dati e del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-481">Name of the storage account to store OS and data VHDs.</span></span> |
| <span data-ttu-id="219c7-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="219c7-482">vmSize</span></span> | <span data-ttu-id="219c7-483">Dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-483">Size of the VM.</span></span> <span data-ttu-id="219c7-484">Attualmente sono supportate solo le serie A, D e G Standard.</span><span class="sxs-lookup"><span data-stu-id="219c7-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="219c7-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="219c7-485">virtualNetworkName</span></span> | <span data-ttu-id="219c7-486">Nome della rete virtuale a cui deve appartenere la scheda di interfaccia di rete della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-486">Name of the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="219c7-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="219c7-487">subnetName</span></span> | <span data-ttu-id="219c7-488">Nome della subnet nella rete virtuale a cui deve appartenere la scheda di interfaccia di rete della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-488">Name of the subnet in the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="219c7-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="219c7-489">AADClientID</span></span> | <span data-ttu-id="219c7-490">ID client dell'applicazione Azure AD con le autorizzazioni per la scrittura di segreti nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-490">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="219c7-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="219c7-491">AADClientSecret</span></span> | <span data-ttu-id="219c7-492">Segreto client dell'applicazione Azure AD con le autorizzazioni per la scrittura di segreti nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-492">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="219c7-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="219c7-493">keyVaultURL</span></span> | <span data-ttu-id="219c7-494">URL dell'insieme di credenziali delle chiavi in cui dovrà essere caricata la chiave BitLocker.</span><span class="sxs-lookup"><span data-stu-id="219c7-494">URL of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="219c7-495">È possibile ottenerlo usando il cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="219c7-495">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="219c7-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="219c7-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="219c7-497">URL della chiave di crittografia della chiave usata per crittografare la chiave BitLocker generata (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="219c7-497">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="219c7-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="219c7-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="219c7-499">Gruppo di risorse dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-499">Resource group of the key vault.</span></span> |
| <span data-ttu-id="219c7-500">vmName</span><span class="sxs-lookup"><span data-stu-id="219c7-500">vmName</span></span> | <span data-ttu-id="219c7-501">Nome della VM in cui deve essere eseguita l'operazione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-501">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="219c7-502">_KeyEncryptionKeyURL_ è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="219c7-503">È possibile specificare la chiave di crittografia della chiave (KEK) personalizzata per la protezione aggiuntiva della chiave DEK (segreto passphrase) nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-503">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="219c7-504">Abilitare la crittografia delle nuove VM IaaS create da chiavi di crittografia e dischi rigidi virtuali crittografati dei clienti</span><span class="sxs-lookup"><span data-stu-id="219c7-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="219c7-505">In questo scenario è possibile abilitare la crittografia usando il modello di Resource Manager, i cmdlet di PowerShell o i comandi dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="219c7-505">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="219c7-506">Le sezioni seguenti descrivono in modo più dettagliato il modello di Resource Manager e i comandi dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="219c7-506">The following sections explain in greater detail the Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="219c7-507">Seguire le istruzioni di una di queste sezioni per la preparazione di immagini pre-crittografate che possono essere usate in Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-507">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="219c7-508">Dopo aver creato l'immagine, è possibile usare i passaggi della sezione successiva per creare una VM di Azure crittografata.</span><span class="sxs-lookup"><span data-stu-id="219c7-508">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span></span>

* [<span data-ttu-id="219c7-509">Preparare un disco rigido virtuale Windows pre-crittografato</span><span class="sxs-lookup"><span data-stu-id="219c7-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="219c7-510">Preparare un disco rigido virtuale Linux pre-crittografato</span><span class="sxs-lookup"><span data-stu-id="219c7-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="219c7-511">Uso del modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="219c7-511">Using the Resource Manager template</span></span>
<span data-ttu-id="219c7-512">È possibile abilitare la crittografia dei dischi nel disco rigido virtuale crittografato usando il modello di [Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="219c7-512">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="219c7-513">Nel modello di avvio rapido di Azure fare clic su **Distribuisci in Azure**, immettere la configurazione della crittografia nel pannello **Parametri**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="219c7-513">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="219c7-514">Selezionare la sottoscrizione, il gruppo di risorse, la posizione del gruppo di risorse, le note legali e il contratto, quindi fare clic su **Crea** per abilitare la crittografia nella nuova macchina virtuale IaaS.</span><span class="sxs-lookup"><span data-stu-id="219c7-514">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span></span>

<span data-ttu-id="219c7-515">La tabella seguente elenca i parametri del modello di Resource Manager per il disco rigido virtuale crittografato:</span><span class="sxs-lookup"><span data-stu-id="219c7-515">The following table lists the Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="219c7-516">Parametro</span><span class="sxs-lookup"><span data-stu-id="219c7-516">Parameter</span></span> | <span data-ttu-id="219c7-517">Descrizione</span><span class="sxs-lookup"><span data-stu-id="219c7-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="219c7-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="219c7-518">newStorageAccountName</span></span> | <span data-ttu-id="219c7-519">Nome dell'account di archiviazione per archiviare il disco rigido virtuale del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-519">Name of the storage account to store the encrypted OS VHD.</span></span> <span data-ttu-id="219c7-520">È necessario che questo account di archiviazione sia già stato creato nello stesso gruppo di risorse e nello stesso percorso della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-520">This storage account should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="219c7-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="219c7-521">osVhdUri</span></span> | <span data-ttu-id="219c7-522">URI del disco rigido virtuale del sistema operativo dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-522">URI of the OS VHD from the storage account.</span></span> |
| <span data-ttu-id="219c7-523">osType</span><span class="sxs-lookup"><span data-stu-id="219c7-523">osType</span></span> | <span data-ttu-id="219c7-524">Tipo di prodotto del sistema operativo (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="219c7-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="219c7-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="219c7-525">virtualNetworkName</span></span> | <span data-ttu-id="219c7-526">Nome della rete virtuale a cui deve appartenere la scheda di interfaccia di rete della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-526">Name of the VNet that the VM NIC should belong to.</span></span> <span data-ttu-id="219c7-527">È necessario che il nome sia già stato creato nello stesso gruppo di risorse e nello stesso percorso della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-527">The name should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="219c7-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="219c7-528">subnetName</span></span> | <span data-ttu-id="219c7-529">Nome della subnet nella rete virtuale a cui deve appartenere la scheda di interfaccia di rete della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-529">Name of the subnet on the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="219c7-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="219c7-530">vmSize</span></span> | <span data-ttu-id="219c7-531">Dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-531">Size of the VM.</span></span> <span data-ttu-id="219c7-532">Attualmente sono supportate solo le serie A, D e G Standard.</span><span class="sxs-lookup"><span data-stu-id="219c7-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="219c7-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="219c7-533">keyVaultResourceID</span></span> | <span data-ttu-id="219c7-534">ResourceID che identifica la risorsa dell'insieme di credenziali delle chiavi in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="219c7-534">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="219c7-535">È possibile ottenerlo usando il cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId` di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="219c7-535">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="219c7-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="219c7-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="219c7-537">URL della chiave di crittografia dei dischi configurato nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-537">URL of the disk-encryption key that's set up in the key vault.</span></span> |
| <span data-ttu-id="219c7-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="219c7-538">keyVaultKekUrl</span></span> | <span data-ttu-id="219c7-539">URL della chiave di crittografia della chiave per crittografare la chiave di crittografia dei dischi generata.</span><span class="sxs-lookup"><span data-stu-id="219c7-539">URL of the key encryption key for encrypting the generated disk-encryption key.</span></span> |
| <span data-ttu-id="219c7-540">vmName</span><span class="sxs-lookup"><span data-stu-id="219c7-540">vmName</span></span> | <span data-ttu-id="219c7-541">Nome della VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="219c7-541">Name of the IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="219c7-542">Usare i cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="219c7-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="219c7-543">È possibile abilitare la crittografia dei dischi nel disco rigido virtuale crittografato usando il cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk) di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="219c7-543">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="219c7-544">Uso dei comandi dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="219c7-544">Using CLI commands</span></span>
<span data-ttu-id="219c7-545">Eseguire queste operazioni per abilitare la crittografia dei dischi per questo scenario con i comandi dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="219c7-545">To enable disk encryption for this scenario by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="219c7-546">Impostare criteri di accesso per l'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="219c7-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="219c7-547">Impostare il flag **EnabledForDiskEncryption**:</span><span class="sxs-lookup"><span data-stu-id="219c7-547">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="219c7-548">Configurare le autorizzazioni per l'applicazione Azure AD per scrivere segreti nell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="219c7-548">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="219c7-549">Per abilitare la crittografia in una VM esistente o in esecuzione, digitare:</span><span class="sxs-lookup"><span data-stu-id="219c7-549">To enable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="219c7-550">Ottenere lo stato della crittografia:</span><span class="sxs-lookup"><span data-stu-id="219c7-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="219c7-551">Per abilitare la crittografia in una nuova macchina virtuale dal disco rigido virtuale crittografato, usare i parametri seguenti con il comando `azure vm create`:</span><span class="sxs-lookup"><span data-stu-id="219c7-551">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="219c7-552">Abilitare la crittografia in una VM IaaS Windows esistente o in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="219c7-553">In questo scenario è possibile abilitare la crittografia usando il modello di Resource Manager, i cmdlet di PowerShell o i comandi dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="219c7-553">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="219c7-554">Le sezioni seguenti descrivono in modo più dettagliato come abilitarla usando il modello di Resource Manager e i comandi dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="219c7-554">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span></span>

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="219c7-555">Uso del modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="219c7-555">Using the Resource Manager template</span></span>
<span data-ttu-id="219c7-556">È possibile abilitare la crittografia dei dischi nelle macchine virtuali IaaS Windows esistenti o in esecuzione usando il modello di [Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="219c7-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="219c7-557">Nel modello di avvio rapido di Azure fare clic su **Distribuisci in Azure**, immettere la configurazione della crittografia nel pannello **Parametri**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="219c7-557">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="219c7-558">Selezionare la sottoscrizione, il gruppo di risorse, la posizione del gruppo di risorse, le note legali e il contratto, quindi fare clic su **Crea** per abilitare la crittografia nella macchina virtuale IaaS esistente o in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="219c7-558">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="219c7-559">La tabella seguente elenca i parametri del modello di Resource Manager per macchine virtuali esistenti o in esecuzione che usano un ID client di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="219c7-559">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="219c7-560">Parametro</span><span class="sxs-lookup"><span data-stu-id="219c7-560">Parameter</span></span> | <span data-ttu-id="219c7-561">Descrizione</span><span class="sxs-lookup"><span data-stu-id="219c7-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="219c7-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="219c7-562">AADClientID</span></span> | <span data-ttu-id="219c7-563">ID client dell'applicazione Azure AD con le autorizzazioni per la scrittura di segreti nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-563">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="219c7-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="219c7-564">AADClientSecret</span></span> | <span data-ttu-id="219c7-565">Segreto client dell'applicazione Azure AD con le autorizzazioni per la scrittura di segreti nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-565">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="219c7-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="219c7-566">keyVaultName</span></span> | <span data-ttu-id="219c7-567">Nome dell'insieme di credenziali delle chiavi in cui dovrà essere caricata la chiave BitLocker.</span><span class="sxs-lookup"><span data-stu-id="219c7-567">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="219c7-568">È possibile ottenerlo usando il cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="219c7-568">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="219c7-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="219c7-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="219c7-570">URL della chiave di crittografia della chiave usata per crittografare la chiave BitLocker generata.</span><span class="sxs-lookup"><span data-stu-id="219c7-570">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="219c7-571">Questo parametro è facoltativo se si seleziona **nokek** dall'elenco a discesa UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="219c7-571">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="219c7-572">Se si seleziona **kek** dall'elenco a discesa UseExistingKek, è necessario immettere il valore _keyEncryptionKeyURL_.</span><span class="sxs-lookup"><span data-stu-id="219c7-572">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="219c7-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="219c7-573">volumeType</span></span> | <span data-ttu-id="219c7-574">Tipo del volume in cui viene eseguita l'operazione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-574">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="219c7-575">I valori validi sono _OS_, _Data_ e _All_.</span><span class="sxs-lookup"><span data-stu-id="219c7-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="219c7-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="219c7-576">sequenceVersion</span></span> | <span data-ttu-id="219c7-577">Versione della sequenza dell'operazione BitLocker.</span><span class="sxs-lookup"><span data-stu-id="219c7-577">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="219c7-578">Incrementare questo numero di versione ogni volta che viene eseguita un'operazione di crittografia dei dischi nella stessa VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-578">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="219c7-579">vmName</span><span class="sxs-lookup"><span data-stu-id="219c7-579">vmName</span></span> | <span data-ttu-id="219c7-580">Nome della VM in cui deve essere eseguita l'operazione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-580">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="219c7-581">_KeyEncryptionKeyURL_ è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="219c7-582">È possibile specificare la chiave di crittografia della chiave (KEK) personalizzata per l'ulteriore protezione della chiave DEK (segreto di crittografia di BitLocker) nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-582">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="219c7-583">Usare i cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="219c7-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="219c7-584">Per informazioni sull'abilitazione della crittografia con Crittografia dischi di Azure tramite cmdlet di PowerShell, vedere i post di blog [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) (Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 1) ed [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx) (Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 2).</span><span class="sxs-lookup"><span data-stu-id="219c7-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="219c7-585">Uso dei comandi dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="219c7-585">Using CLI commands</span></span>
<span data-ttu-id="219c7-586">Per abilitare la crittografia in macchine virtuali IaaS Windows esistenti o in esecuzione in Azure usando i comandi dell'interfaccia della riga di comando, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-586">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span></span>

1. <span data-ttu-id="219c7-587">Per configurare i criteri di accesso nell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="219c7-587">To set access policies in the key vault:</span></span>
   * <span data-ttu-id="219c7-588">Impostare il flag **EnabledForDiskEncryption**:</span><span class="sxs-lookup"><span data-stu-id="219c7-588">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="219c7-589">Configurare le autorizzazioni per l'applicazione Azure AD per scrivere segreti nell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="219c7-589">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="219c7-590">Per abilitare la crittografia in una VM esistente o in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="219c7-590">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="219c7-591">Per ottenere lo stato della crittografia:</span><span class="sxs-lookup"><span data-stu-id="219c7-591">To get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="219c7-592">Per abilitare la crittografia in una nuova macchina virtuale dal disco rigido virtuale crittografato, usare i parametri seguenti con il comando `azure vm create`:</span><span class="sxs-lookup"><span data-stu-id="219c7-592">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="219c7-593">Abilitare la crittografia in una VM IaaS Linux esistente o in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="219c7-594">È possibile abilitare la crittografia dei dischi nelle macchine virtuali IaaS Linux esistenti o in esecuzione usando il modello di [Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="219c7-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="219c7-595">Nel modello di avvio rapido di Azure fare clic su **Distribuisci in Azure**, immettere la configurazione della crittografia nel pannello **Parametri**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="219c7-595">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="219c7-596">Selezionare la sottoscrizione, il gruppo di risorse, la posizione del gruppo di risorse, le note legali e il contratto, quindi fare clic su **Crea** per abilitare la crittografia nella macchina virtuale IaaS esistente o in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="219c7-596">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="219c7-597">La tabella seguente elenca i parametri del modello di Resource Manager per macchine virtuali esistenti o in esecuzione che usano un ID client di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="219c7-597">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="219c7-598">Parametro</span><span class="sxs-lookup"><span data-stu-id="219c7-598">Parameter</span></span> | <span data-ttu-id="219c7-599">Descrizione</span><span class="sxs-lookup"><span data-stu-id="219c7-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="219c7-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="219c7-600">AADClientID</span></span> | <span data-ttu-id="219c7-601">ID client dell'applicazione Azure AD con le autorizzazioni per la scrittura di segreti nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-601">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="219c7-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="219c7-602">AADClientSecret</span></span> | <span data-ttu-id="219c7-603">Segreto client dell'applicazione Azure AD con le autorizzazioni per la scrittura di segreti nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-603">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="219c7-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="219c7-604">keyVaultName</span></span> | <span data-ttu-id="219c7-605">Nome dell'insieme di credenziali delle chiavi in cui dovrà essere caricata la chiave BitLocker.</span><span class="sxs-lookup"><span data-stu-id="219c7-605">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="219c7-606">È possibile ottenerlo usando il cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="219c7-606">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="219c7-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="219c7-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="219c7-608">URL della chiave di crittografia della chiave usata per crittografare la chiave BitLocker generata.</span><span class="sxs-lookup"><span data-stu-id="219c7-608">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="219c7-609">Questo parametro è facoltativo se si seleziona **nokek** dall'elenco a discesa UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="219c7-609">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="219c7-610">Se si seleziona **kek** dall'elenco a discesa UseExistingKek, è necessario immettere il valore _keyEncryptionKeyURL_.</span><span class="sxs-lookup"><span data-stu-id="219c7-610">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="219c7-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="219c7-611">volumeType</span></span> | <span data-ttu-id="219c7-612">Tipo del volume in cui viene eseguita l'operazione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-612">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="219c7-613">I valori supportati validi sono _OS_ o _All_ (per RHEL 7.2, CentOS 7.2 e Ubuntu 16.04) e _Data_ (per tutte le altre distribuzioni).</span><span class="sxs-lookup"><span data-stu-id="219c7-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="219c7-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="219c7-614">sequenceVersion</span></span> | <span data-ttu-id="219c7-615">Versione della sequenza dell'operazione BitLocker.</span><span class="sxs-lookup"><span data-stu-id="219c7-615">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="219c7-616">Incrementare questo numero di versione ogni volta che viene eseguita un'operazione di crittografia dei dischi nella stessa VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-616">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="219c7-617">vmName</span><span class="sxs-lookup"><span data-stu-id="219c7-617">vmName</span></span> | <span data-ttu-id="219c7-618">Nome della VM in cui deve essere eseguita l'operazione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-618">Name of the VM that the encryption operation is to be performed on.</span></span> |
| <span data-ttu-id="219c7-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="219c7-619">passPhrase</span></span> | <span data-ttu-id="219c7-620">Immettere una passphrase complessa come chiave di crittografia dei dati.</span><span class="sxs-lookup"><span data-stu-id="219c7-620">Type a strong passphrase as the data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="219c7-621">_KeyEncryptionKeyURL_ è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="219c7-622">È possibile specificare la chiave di crittografia della chiave (KEK) personalizzata per la protezione aggiuntiva della chiave DEK (segreto passphrase) nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-622">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="219c7-623">Comandi dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="219c7-623">CLI commands</span></span>
<span data-ttu-id="219c7-624">È possibile abilitare la crittografia dei dischi nel disco rigido virtuale crittografato installando e usando il [comando dell'interfaccia della riga di comando](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="219c7-624">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="219c7-625">Per abilitare la crittografia in macchine virtuali IaaS Linux esistenti o in esecuzione in Azure usando i comandi dell'interfaccia della riga di comando, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-625">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="219c7-626">Configurare i criteri di accesso nell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="219c7-626">Set access policies in the key vault:</span></span>

 * <span data-ttu-id="219c7-627">Impostare il flag **EnabledForDiskEncryption**:</span><span class="sxs-lookup"><span data-stu-id="219c7-627">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="219c7-628">Configurare le autorizzazioni per l'applicazione Azure AD per scrivere segreti nell'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="219c7-628">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="219c7-629">Per abilitare la crittografia in una VM esistente o in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="219c7-629">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="219c7-630">Ottenere lo stato della crittografia:</span><span class="sxs-lookup"><span data-stu-id="219c7-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="219c7-631">Per abilitare la crittografia in una nuova macchina virtuale dal disco rigido virtuale crittografato, usare i parametri seguenti con il comando `azure vm create`:</span><span class="sxs-lookup"><span data-stu-id="219c7-631">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-the-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="219c7-632">Ottenere lo stato della crittografia di una VM IaaS crittografata</span><span class="sxs-lookup"><span data-stu-id="219c7-632">Get the encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="219c7-633">È possibile ottenere lo stato della crittografia usando Azure Resource Manager, i [cmdlet di PowerShell](/powershell/azure/overview) o i comandi dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="219c7-633">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="219c7-634">Le sezioni seguenti illustrano come usare il portale di Azure classico e i comandi dell'interfaccia della riga di comando per ottenere lo stato della crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-634">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="219c7-635">Ottenere lo stato della crittografia di una VM Windows crittografata usando Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="219c7-635">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="219c7-636">È possibile ottenere lo stato di crittografia della macchina virtuale IaaS da Azure Resource Manager seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-636">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span></span>

1. <span data-ttu-id="219c7-637">Accedere al [portale di Azure classico](https://portal.azure.com/), quindi fare clic su **Macchine virtuali** nel riquadro a sinistra per visualizzare un riepilogo delle macchine virtuali nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="219c7-637">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span></span> <span data-ttu-id="219c7-638">È possibile filtrare la visualizzazione Macchine virtuali selezionando il nome della sottoscrizione dall'elenco a discesa **Sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="219c7-638">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="219c7-639">Nella pagina superiore della pagina **Macchine virtuali** fare clic su **Colonne**.</span><span class="sxs-lookup"><span data-stu-id="219c7-639">At the top of the **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="219c7-640">Nel pannello  **Scegli colonna** selezionare **Crittografia del disco**, quindi fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="219c7-640">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="219c7-641">Verrà visualizzata la colonna relativa alla crittografia dei dischi, che mostra lo stato della crittografia, ovvero _Abilitato_ o _Non abilitato_, per ogni macchina virtuale, come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-641">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span></span>

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-the-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-the-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="219c7-643">Ottenere lo stato della crittografia di una VM Iaas crittografata (Windows/Linux) usando il cmdlet di PowerShell per la crittografia dei dischi</span><span class="sxs-lookup"><span data-stu-id="219c7-643">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="219c7-644">È possibile ottenere lo stato della crittografia della macchina virtuale IaaS cmdlet `Get-AzureRmVMDiskEncryptionStatus` di PowerShell per la crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="219c7-644">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="219c7-645">Per ottenere le impostazioni di crittografia per la macchina virtuale, immettere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="219c7-645">To get the encryption settings for your VM, enter the following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="219c7-646">È possibile esaminare l'output di _Get-AzureRmVMDiskEncryptionStatus_ per ottenere gli URL della chiave di crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-646">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="219c7-647">I valori delle impostazioni OSVolumeEncrypted e DataVolumesEncrypted sono impostati su _Encrypted_, che mostra che entrambi i volumi sono crittografati tramite Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-647">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="219c7-648">Per informazioni sull'abilitazione della crittografia con Crittografia dischi di Azure tramite cmdlet di PowerShell, vedere i post di blog [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) (Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 1) ed [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx) (Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 2).</span><span class="sxs-lookup"><span data-stu-id="219c7-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-649">Nelle macchine virtuali Linux sono necessari tre o quattro minuti per la visualizzazione dello stato della crittografia da parte del cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="219c7-649">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-the-iaas-vm-from-the-disk-encryption-cli-command"></a><span data-ttu-id="219c7-650">Ottenere lo stato della crittografia della VM IaaS usando il comando dell'interfaccia della riga di comando per la crittografia dei dischi</span><span class="sxs-lookup"><span data-stu-id="219c7-650">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span></span>
<span data-ttu-id="219c7-651">È possibile ottenere lo stato della crittografia della macchina virtuale IaaS usando il comando `azure vm show-disk-encryption-status` dell'interfaccia della riga di comando per la crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="219c7-651">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="219c7-652">Per ottenere le impostazioni delle crittografia per la VM, nella sessione dell'interfaccia della riga di comando digitare:</span><span class="sxs-lookup"><span data-stu-id="219c7-652">To get the encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="219c7-653">Disabilitare la crittografia nelle VM IaaS Windows in esecuzione</span><span class="sxs-lookup"><span data-stu-id="219c7-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="219c7-654">È possibile disabilitare la crittografia in una VM IaaS Windows o Linux in esecuzione tramite il modello di Resource Manager per Crittografia dischi di Azure o i cmdlet di PowerShell e specificare la configurazione della decrittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-654">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="219c7-655">Macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="219c7-655">Windows VM</span></span>
<span data-ttu-id="219c7-656">Il passaggio per disabilitare la crittografia agisce sul volume dati o sul volume del sistema operativo o entrambi nella VM IaaS Windows in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="219c7-656">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="219c7-657">Non è possibile disabilitare il volume del sistema operativo e lasciare il volume dati crittografato.</span><span class="sxs-lookup"><span data-stu-id="219c7-657">You cannot disable the OS volume and leave the data volume encrypted.</span></span> <span data-ttu-id="219c7-658">Dopo aver completato il passaggio per disabilitare la crittografia, il modello di distribuzione classica di Azure aggiorna il modello di servizi della VM e la VM IaaS Windows viene contrassegnata come decrittografata.</span><span class="sxs-lookup"><span data-stu-id="219c7-658">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="219c7-659">Il contenuto inattivo della VM non viene più crittografato.</span><span class="sxs-lookup"><span data-stu-id="219c7-659">The contents of the VM are no longer encrypted at rest.</span></span> <span data-ttu-id="219c7-660">La decrittografia non elimina l'insieme di credenziali delle chiavi e il materiale della chiave di crittografia, ovvero le chiavi di crittografia BitLocker per Windows o Passphrase per Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-660">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="219c7-661">VM Linux</span><span class="sxs-lookup"><span data-stu-id="219c7-661">Linux VM</span></span>
<span data-ttu-id="219c7-662">Il passaggio per disabilitare la crittografia agisce sul volume dati nella VM IaaS Linux in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="219c7-662">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span></span> <span data-ttu-id="219c7-663">Questo passaggio funziona soltanto se il disco del sistema operativo non è crittografato.</span><span class="sxs-lookup"><span data-stu-id="219c7-663">This step only works if the OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-664">La disabilitazione della crittografia del disco del sistema operativo non è consentita nelle macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-664">Disabling encryption on the OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="219c7-665">Disabilitare la crittografia in una macchina virtuale IaaS esistente o in esecuzione</span><span class="sxs-lookup"><span data-stu-id="219c7-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="219c7-666">È possibile disabilitare la crittografia dei dischi in macchine virtuali IaaS Windows usando il modello di [Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="219c7-666">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="219c7-667">Nel modello di avvio rapido di Azure fare clic su **Distribuisci in Azure**, immettere la configurazione della decrittografia nel pannello **Parametri**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="219c7-667">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="219c7-668">Selezionare la sottoscrizione, il gruppo di risorse, la posizione del gruppo di risorse, le note legali e il contratto, quindi fare clic su **Crea** per abilitare la crittografia in una nuova macchina virtuale IaaS.</span><span class="sxs-lookup"><span data-stu-id="219c7-668">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="219c7-669">Per le macchine virtuali Linux è possibile disabilitare la crittografia usando il modello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) (Disabilitare la crittografia in una VM Linux in esecuzione).</span><span class="sxs-lookup"><span data-stu-id="219c7-669">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="219c7-670">La tabella seguente elenca i parametri del modello di Resource Manager per la disabilitazione della crittografia in una VM IaaS in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="219c7-670">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="219c7-671">Parametro</span><span class="sxs-lookup"><span data-stu-id="219c7-671">Parameter</span></span> | <span data-ttu-id="219c7-672">Descrizione</span><span class="sxs-lookup"><span data-stu-id="219c7-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="219c7-673">vmName</span><span class="sxs-lookup"><span data-stu-id="219c7-673">vmName</span></span> | <span data-ttu-id="219c7-674">Nome della VM in cui deve essere eseguita l'operazione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-674">Name of the VM that the encryption operation is to be performed on.</span></span>
| <span data-ttu-id="219c7-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="219c7-675">volumeType</span></span> | <span data-ttu-id="219c7-676">Tipo del volume in cui viene eseguita l'operazione di decrittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="219c7-677">I valori validi sono _OS_, _Data_ e _All_.</span><span class="sxs-lookup"><span data-stu-id="219c7-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="219c7-678">Non è possibile disabilitare la crittografia sul volume del sistema operativo o di avvio di una macchina virtuale IaaS Windows in esecuzione senza disabilitare la crittografia sul volume _Data_.</span><span class="sxs-lookup"><span data-stu-id="219c7-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span></span> <span data-ttu-id="219c7-679">Si noti anche che la disabilitazione della crittografia del disco del sistema operativo non è consentita nelle macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-679">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="219c7-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="219c7-680">sequenceVersion</span></span> | <span data-ttu-id="219c7-681">Versione della sequenza dell'operazione BitLocker.</span><span class="sxs-lookup"><span data-stu-id="219c7-681">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="219c7-682">Incrementare questo numero di versione ogni volta che viene eseguita un'operazione di decrittografia dei dischi nella stessa VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-682">Increment this version number every time a disk decryption operation is performed on the same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="219c7-683">Disabilitare la crittografia in una macchina virtuale IaaS esistente o in esecuzione</span><span class="sxs-lookup"><span data-stu-id="219c7-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="219c7-684">Per disabilitare la crittografia in una VM IaaS esistente o in esecuzione usando il cmdlet di PowerShell, vedere [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="219c7-684">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="219c7-685">Questo cmdlet supporta sia le VM Windows che le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="219c7-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="219c7-686">Per disabilitare la crittografia, installa un'estensione nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-686">To disable encryption, it installs an extension on the virtual machine.</span></span> <span data-ttu-id="219c7-687">Se il parametro _Name_ non viene specificato, viene creata un'estensione con nome predefinito _AzureDiskEncryption for Windows VMs_.</span><span class="sxs-lookup"><span data-stu-id="219c7-687">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="219c7-688">Nelle VM Linux viene usata l'estensione AzureDiskEncryptionForLinux.</span><span class="sxs-lookup"><span data-stu-id="219c7-688">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="219c7-689">Questo cmdlet riavvia la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-689">This cmdlet reboots the virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="219c7-690">Abilitare la crittografia su macchina virtuale IaaS pre-crittografata con disco gestito Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="219c7-691">Per creare una macchina virtuale crittografata da un disco rigido virtuale pre-crittografato usare il modello ARM di disco gestito Azure, disponibile in</span><span class="sxs-lookup"><span data-stu-id="219c7-691">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span></span>   
<span data-ttu-id="219c7-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="219c7-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="219c7-693">Abilitare la crittografia su una nuova macchina virtuale IaaS Linux con disco gestito Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="219c7-694">Per creare una nuova macchina virtuale IaaS Linux crittografata usare il modello ARM di disco gestito Azure, disponibile in</span><span class="sxs-lookup"><span data-stu-id="219c7-694">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
<span data-ttu-id="219c7-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="219c7-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="219c7-696">Abilitare la crittografia su una nuova macchina virtuale IaaS Windows con disco gestito Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="219c7-697">Per creare una nuova macchina virtuale IaaS Linux crittografata usare il modello ARM di disco gestito Azure, disponibile in</span><span class="sxs-lookup"><span data-stu-id="219c7-697">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
 <span data-ttu-id="219c7-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="219c7-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="219c7-699">È obbligatorio eseguire uno snapshot e/o un backup di un'istanza di macchina virtuale basata su un disco gestito all'esterno di Crittografia dischi di Azure e prima di abilitarla.</span><span class="sxs-lookup"><span data-stu-id="219c7-699">It is mandatory to snapshot and/or backup a managed disk based VM instance outside of and prior to enabling Azure Disk Encryption.</span></span>  <span data-ttu-id="219c7-700">È possibile eseguire uno snapshot del disco gestito dal portale o tramite Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-700">A snapshot of the managed disk can be taken from the portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="219c7-701">I backup garantiscono la disponibilità di un'opzione di ripristino nel caso si verifichi un errore imprevisto durante la crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-701">Backups ensure that a recovery option is possible in the case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="219c7-702">Dopo aver eseguito un backup, è possibile usare il cmdlet Set-AzureRmVMDiskEncryptionExtension per crittografare i dischi gestiti specificando il parametro -skipVmBackup.</span><span class="sxs-lookup"><span data-stu-id="219c7-702">Once a backup is made, the Set-AzureRmVMDiskEncryptionExtension cmdlet can be used to encrypt managed disks by specifying the -skipVmBackup parameter.</span></span>  <span data-ttu-id="219c7-703">Questo comando ha esito negativo su una macchina virtuale basata su un disco gestito finché non viene eseguito un backup e non viene specificato il parametro.</span><span class="sxs-lookup"><span data-stu-id="219c7-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="219c7-704">Aggiornare le impostazioni di crittografia di una macchina virtuale non Premium crittografata esistente</span><span class="sxs-lookup"><span data-stu-id="219c7-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="219c7-705">Usare le interfacce supportate di Crittografia dischi di Azure esistenti per le macchine virtuali in esecuzione [cmdlet PS, CLI o modelli ARM] per aggiornare impostazioni di crittografia quali ID/segreto del client AAD, chiave di crittografia della chiave [KEK], chiave di crittografia BitLocker per macchina virtuale Windows o Passphrase per macchina virtuale Linux e così via. L'impostazione della crittografia di aggiornamento è supportata solo per le macchine virtuali non dotate di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="219c7-705">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="219c7-706">NON è supportata per le macchine virtuali dotate di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="219c7-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="219c7-707">Appendice</span><span class="sxs-lookup"><span data-stu-id="219c7-707">Appendix</span></span>
### <a name="connect-to-your-subscription"></a><span data-ttu-id="219c7-708">Eseguire la connessione alla sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="219c7-708">Connect to your subscription</span></span>
<span data-ttu-id="219c7-709">Prima di continuare, vedere la sezione *Prerequisiti* di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="219c7-709">Before you proceed, review the *Prerequisites* section in this article.</span></span> <span data-ttu-id="219c7-710">Dopo essersi assicurati che siano stati rispettati tutti i prerequisiti, connettersi alla sottoscrizione seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-710">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span></span>

1. <span data-ttu-id="219c7-711">Avviare una sessione di Azure PowerShell e accedere all'account Azure con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-711">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="219c7-712">Se sono disponibili più sottoscrizioni e se ne vuole specificare una da usare, digitare quanto segue per visualizzare le sottoscrizioni per il proprio account:</span><span class="sxs-lookup"><span data-stu-id="219c7-712">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="219c7-713">Per specificare la sottoscrizione che si vuole usare, digitare:</span><span class="sxs-lookup"><span data-stu-id="219c7-713">To specify the subscription you want to use, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="219c7-714">Per verificare che la sottoscrizione configurata sia corretta, digitare:</span><span class="sxs-lookup"><span data-stu-id="219c7-714">To verify that the subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="219c7-715">Per verificare che i cmdlet di Crittografia dischi di Azure siano installati, digitare:</span><span class="sxs-lookup"><span data-stu-id="219c7-715">To confirm the Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="219c7-716">L'output seguente conferma l'installazione di PowerShell per Crittografia dischi di Azure:</span><span class="sxs-lookup"><span data-stu-id="219c7-716">The following output confirms the Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="219c7-717">Preparare un disco rigido virtuale Windows pre-crittografato</span><span class="sxs-lookup"><span data-stu-id="219c7-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="219c7-718">Le sezioni seguenti sono necessarie per preparare un disco rigido virtuale Windows pre-crittografato per la distribuzione come disco rigido virtuale crittografato in Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="219c7-718">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="219c7-719">Usare le informazioni per preparare e avviare una nuova macchina virtuale Windows VM (disco rigido virtuale) in Azure Site Recovery o Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-719">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-to-allow-non-tpm-for-os-protection"></a><span data-ttu-id="219c7-720">Aggiornare i criteri di gruppo per consentire la protezione non TPM del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="219c7-720">Update group policy to allow non-TPM for OS protection</span></span>
<span data-ttu-id="219c7-721">Configurare l'impostazione **Crittografia unità BitLocker** di Criteri di gruppo per BitLocker, disponibile in **Criteri del computer locale** > **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows**.</span><span class="sxs-lookup"><span data-stu-id="219c7-721">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="219c7-722">Cambiare questa impostazione in **Unità del sistema operativo** > **Richiedi autenticazione aggiuntiva all'avvio** > **Consenti BitLocker senza un TPM compatibile**, come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-722">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span></span>

![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="219c7-724">Installare i componenti della funzionalità BitLocker</span><span class="sxs-lookup"><span data-stu-id="219c7-724">Install BitLocker feature components</span></span>
<span data-ttu-id="219c7-725">Per Windows Server 2012 e versioni successive, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-725">For Windows Server 2012 and later, use the following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="219c7-726">Per Windows Server 2008 R2, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-726">For Windows Server 2008 R2, use the following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-the-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="219c7-727">Preparare il volume del sistema operativo per BitLocker tramite `bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="219c7-727">Prepare the OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="219c7-728">Per comprimere la partizione del sistema operativo e preparare il computer per BitLocker, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-728">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-the-os-volume-by-using-bitlocker"></a><span data-ttu-id="219c7-729">Proteggere il volume del sistema operativo usando BitLocker</span><span class="sxs-lookup"><span data-stu-id="219c7-729">Protect the OS volume by using BitLocker</span></span>
<span data-ttu-id="219c7-730">Usare il comando [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) per abilitare la crittografia sul volume di avvio usando una protezione con chiave esterna.</span><span class="sxs-lookup"><span data-stu-id="219c7-730">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span></span> <span data-ttu-id="219c7-731">Salvare anche la chiave esterna (file con estensione bek) nell'unità o nel volume esterno.</span><span class="sxs-lookup"><span data-stu-id="219c7-731">Also place the external key (.bek file) on the external drive or volume.</span></span> <span data-ttu-id="219c7-732">La crittografia viene abilitata nel volume di sistema/di avvio al riavvio successivo.</span><span class="sxs-lookup"><span data-stu-id="219c7-732">Encryption is enabled on the system/boot volume after the next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="219c7-733">Preparare la macchina virtuale con un disco rigido virtuale dati/di risorse separato per recuperare la chiave esterna usando BitLocker.</span><span class="sxs-lookup"><span data-stu-id="219c7-733">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="219c7-734">Crittografia di un'unità del sistema operativo in una VM Linux in esecuzione</span><span class="sxs-lookup"><span data-stu-id="219c7-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="219c7-735">La crittografia di un'unità del sistema operativo in una VM Linux in esecuzione è supportata nelle distribuzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="219c7-735">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span></span>

* <span data-ttu-id="219c7-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="219c7-736">RHEL 7.2</span></span>
* <span data-ttu-id="219c7-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="219c7-737">CentOS 7.2</span></span>
* <span data-ttu-id="219c7-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="219c7-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="219c7-739">Prerequisiti per la crittografia del disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="219c7-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="219c7-740">La macchina virtuale deve essere creata dall'immagine del Marketplace in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="219c7-740">The VM must be created from the Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="219c7-741">VM di Azure con almeno 4 GB di RAM (7 GB consigliati).</span><span class="sxs-lookup"><span data-stu-id="219c7-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="219c7-742">(Per RHEL e CentOS) Disabilitare SELinux.</span><span class="sxs-lookup"><span data-stu-id="219c7-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="219c7-743">Per disabilitare SELinux, vedere "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="219c7-743">To disable SELinux, see "4.4.2.</span></span> <span data-ttu-id="219c7-744">Disabling SELinux" (4.4.2. Disabilitazione di SELinux) in [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) (Manuale dell'utente e dell'amministratore di SELinux) nella VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-744">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span></span>
* <span data-ttu-id="219c7-745">Dopo la disabilitazione di SELinux, riavviare la VM almeno una volta.</span><span class="sxs-lookup"><span data-stu-id="219c7-745">After you disable SELinux, reboot the VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="219c7-746">Passi</span><span class="sxs-lookup"><span data-stu-id="219c7-746">Steps</span></span>
1. <span data-ttu-id="219c7-747">Creare una macchina virtuale usando una delle distribuzioni specificate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="219c7-747">Create a VM by using one of the distributions specified previously.</span></span>

 <span data-ttu-id="219c7-748">Per CentOS 7.2, la crittografia del disco del sistema operativo è supportata tramite un'immagine speciale.</span><span class="sxs-lookup"><span data-stu-id="219c7-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="219c7-749">Per usare questa immagine, specificare "7.2n" come SKU durante la creazione della VM:</span><span class="sxs-lookup"><span data-stu-id="219c7-749">To use this image, specify "7.2n" as the SKU when you create the VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="219c7-750">Configurare la VM in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="219c7-750">Configure the VM according to your needs.</span></span> <span data-ttu-id="219c7-751">Se si intende crittografare tutte le unità (sistema operativo e dati), le unità dati dovranno essere specificate e montabili da /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="219c7-751">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="219c7-752">Usare UUID=... per specificare le unità di dati in /etc/fstab anziché specificare il nome del dispositivo a blocchi, ad esempio /dev/sdb1.</span><span class="sxs-lookup"><span data-stu-id="219c7-752">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="219c7-753">L'ordine delle unità viene modificato nella macchina virtuale durante la crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-753">During encryption, the order of drives changes on the VM.</span></span> <span data-ttu-id="219c7-754">Se la VM si basa su un ordine specifico di dispositivi a blocchi, questi dispositivi non potranno essere montati dopo la crittografia.</span><span class="sxs-lookup"><span data-stu-id="219c7-754">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span></span>

3. <span data-ttu-id="219c7-755">Disconnettersi dalle sessioni SSH.</span><span class="sxs-lookup"><span data-stu-id="219c7-755">Sign out of the SSH sessions.</span></span>

4. <span data-ttu-id="219c7-756">Per crittografare il sistema operativo, specificare volumeType come **All** oppure **OS** quando si [abilita la crittografia](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="219c7-756">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="219c7-757">Tutti i processi dello spazio dell'utente non in esecuzione come servizi `systemd` devono essere terminati con `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="219c7-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="219c7-758">Riavviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-758">Reboot the VM.</span></span> <span data-ttu-id="219c7-759">Quando si abilita la crittografia del disco del sistema operativo in una macchina virtuale in esecuzione, pianificare i tempi di inattività della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="219c7-760">Monitorare periodicamente lo stato della crittografia tramite le istruzioni indicate nella [sezione successiva](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="219c7-760">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="219c7-761">Quando Get-AzureRmVmDiskEncryptionStatus indica "VMRestartPending," riavviare la macchina virtuale accedendo alla VM o usando il portale, PowerShell oppure l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="219c7-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot the VM
    ```
<span data-ttu-id="219c7-762">Prima di riavviare, è consigliabile salvare i dati di [diagnostica di avvio](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="219c7-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="219c7-763">Monitoraggio dello stato della crittografia del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="219c7-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="219c7-764">Esistono tre modi per monitorare lo stato della crittografia del sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="219c7-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="219c7-765">Usare il cmdlet `Get-AzureRmVmDiskEncryptionStatus` ed esaminare il campo ProgressMessage:</span><span class="sxs-lookup"><span data-stu-id="219c7-765">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="219c7-766">Quando la VM raggiunge lo stato "OS disk encryption started", sono necessari circa 40 o 50 minuti in una VM con archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="219c7-766">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="219c7-767">A causa dell'[errore #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` e `DataVolumesEncrypted`vengono visualizzati come `Unknown` in alcune distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="219c7-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="219c7-768">Con WALinuxAgent 2.1.5 e versioni successive questo errore viene risolto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="219c7-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="219c7-769">Se viene visualizzato `Unknown` nell'output, è possibile verificare lo stato della crittografia del disco usando Esplora risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-769">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span></span>

 <span data-ttu-id="219c7-770">Passare a [Esplora risorse di Azure](https://resources.azure.com/), quindi espandere questa gerarchia nel pannello di selezione a sinistra:</span><span class="sxs-lookup"><span data-stu-id="219c7-770">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="219c7-771">In InstanceView scorrere verso il basso per visualizzare lo stato della crittografia delle unità.</span><span class="sxs-lookup"><span data-stu-id="219c7-771">In the InstanceView, scroll down to see the encryption status of your drives.</span></span>

 ![Visualizzazione dell'istanza della VM](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="219c7-773">Esaminare la [diagnostica di avvio](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="219c7-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="219c7-774">I messaggi provenienti dall'estensione ADE hanno il prefisso `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="219c7-774">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="219c7-775">Accedere alla VM tramite SSH e ottenere il log di estensione da:</span><span class="sxs-lookup"><span data-stu-id="219c7-775">Sign in to the VM via SSH, and get the extension log from:</span></span>

    <span data-ttu-id="219c7-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="219c7-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="219c7-777">È consigliabile non accedere alla VM mentre è in corso la crittografia del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="219c7-777">We recommend that you do not sign in to the VM while OS encryption is in progress.</span></span> <span data-ttu-id="219c7-778">Copiare i log solo in caso di errore degli altri due metodi.</span><span class="sxs-lookup"><span data-stu-id="219c7-778">Copy the logs only when the other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="219c7-779">Preparare un disco rigido virtuale Linux pre-crittografato</span><span class="sxs-lookup"><span data-stu-id="219c7-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="219c7-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="219c7-780">Ubuntu 16</span></span>
<span data-ttu-id="219c7-781">Configurare la crittografia durante l'installazione della distribuzione seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-781">Configure encryption during the distribution installation by doing the following:</span></span>

1. <span data-ttu-id="219c7-782">Selezionare **Configure encrypted volumes** (Configura volumi crittografati) durante il partizionamento dei dischi.</span><span class="sxs-lookup"><span data-stu-id="219c7-782">Select **Configure encrypted volumes** when you partition the disks.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="219c7-784">Creare un'unità di avvio separata che non deve essere crittografata.</span><span class="sxs-lookup"><span data-stu-id="219c7-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="219c7-785">Crittografare l'unità radice.</span><span class="sxs-lookup"><span data-stu-id="219c7-785">Encrypt your root drive.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="219c7-787">Specificare una passphrase.</span><span class="sxs-lookup"><span data-stu-id="219c7-787">Provide a passphrase.</span></span> <span data-ttu-id="219c7-788">Si tratta della passphrase che viene caricata nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-788">This is the passphrase that you upload to the key vault.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="219c7-790">Terminare il partizionamento.</span><span class="sxs-lookup"><span data-stu-id="219c7-790">Finish partitioning.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="219c7-792">Quando si avvia la macchina virtuale e viene richiesta una passphrase, usare la passphrase specificata nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="219c7-792">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="219c7-794">Preparare la macchina virtuale per il caricamento in Azure seguendo [queste istruzioni](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="219c7-794">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="219c7-795">Non eseguire ancora l'ultimo passaggio, ovvero il deprovisioning della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-795">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="219c7-796">Configurare la crittografia per l'uso in Azure seguendo queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="219c7-796">Configure encryption to work with Azure by doing the following:</span></span>

1. <span data-ttu-id="219c7-797">Creare un file in /usr/local/sbin/azure_crypt_key.sh, con il contenuto dello script seguente.</span><span class="sxs-lookup"><span data-stu-id="219c7-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span></span> <span data-ttu-id="219c7-798">Prestare attenzione a KeyFileName, perché è il nome file della passphrase usato da Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-798">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED to find suitable passphrase file ..." >&2
        echo -n "Try to enter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="219c7-799">Modificare la configurazione di crittografia in */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="219c7-799">Change the crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="219c7-800">L'aspetto dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="219c7-801">Se si modifica *azure_crypt_key.sh* in Windows e questo valore è stato copiato in Linux, eseguire `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="219c7-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="219c7-802">Aggiungere autorizzazioni di esecuzione allo script:</span><span class="sxs-lookup"><span data-stu-id="219c7-802">Add executable permissions to the script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="219c7-803">Modificare */etc/initramfs-tools/modules* accodando le righe:</span><span class="sxs-lookup"><span data-stu-id="219c7-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="219c7-804">Eseguire `update-initramfs -u -k all` per aggiornare initramfs e rendere operativo il `keyscript`.</span><span class="sxs-lookup"><span data-stu-id="219c7-804">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span></span>

7. <span data-ttu-id="219c7-805">È ora possibile effettuare il deprovisioning della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-805">Now you can deprovision the VM.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="219c7-807">Continuare con il passaggio successivo e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-807">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="219c7-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="219c7-808">openSUSE 13.2</span></span>
<span data-ttu-id="219c7-809">Per configurare la crittografia durante l'installazione della distribuzione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-809">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="219c7-810">Durante il partizionamento dei dischi, selezionare **Encrypt Volume Group** (Crittografa gruppo di volumi), quindi immettere una password.</span><span class="sxs-lookup"><span data-stu-id="219c7-810">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="219c7-811">Questa è la password che verrà caricata nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-811">This is the password that you will upload to your key vault.</span></span>

 ![Configurazione di openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="219c7-813">Avviare la VM usando la password.</span><span class="sxs-lookup"><span data-stu-id="219c7-813">Boot the VM using your password.</span></span>

 ![Configurazione di openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="219c7-815">Preparare la macchina virtuale per il caricamento in Azure seguendo le istruzioni disponibili in [Preparare una macchina virtuale SLES oppure openSUSE per Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="219c7-815">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="219c7-816">Non eseguire ancora l'ultimo passaggio, ovvero il deprovisioning della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-816">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="219c7-817">Per configurare la crittografia per l'uso in Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-817">To configure encryption to work with Azure, do the following:</span></span>
1. <span data-ttu-id="219c7-818">Modificare il file /etc/dracut.conf e aggiungere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-818">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="219c7-819">Impostare come commento queste righe verso la fine del file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="219c7-819">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="219c7-820">Aggiungere la riga seguente all'inizio del file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="219c7-820">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="219c7-821">Modificare quindi tutte le occorrenze di:</span><span class="sxs-lookup"><span data-stu-id="219c7-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="219c7-822">in:</span><span class="sxs-lookup"><span data-stu-id="219c7-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="219c7-823">Modificare /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e aggiungere questo codice dopo "# Open LUKS device":</span><span class="sxs-lookup"><span data-stu-id="219c7-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="219c7-824">Eseguire `/usr/sbin/dracut -f -v` per aggiornare initrd.</span><span class="sxs-lookup"><span data-stu-id="219c7-824">Run `/usr/sbin/dracut -f -v` to update the initrd.</span></span>

6. <span data-ttu-id="219c7-825">È ora possibile effettuare il deprovisioning della macchina virtuale e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-825">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="219c7-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="219c7-826">CentOS 7</span></span>
<span data-ttu-id="219c7-827">Per configurare la crittografia durante l'installazione della distribuzione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-827">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="219c7-828">Selezionare **Encrypt my data** (Crittografa dati personali) durante il partizionamento dei dischi.</span><span class="sxs-lookup"><span data-stu-id="219c7-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="219c7-830">Assicurarsi **Encrypt** (Crittografa) sia selezionato per la partizione radice.</span><span class="sxs-lookup"><span data-stu-id="219c7-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="219c7-832">Specificare una passphrase.</span><span class="sxs-lookup"><span data-stu-id="219c7-832">Provide a passphrase.</span></span> <span data-ttu-id="219c7-833">Questa è la passphrase che verrà caricata nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-833">This is the passphrase that you will upload to your key vault.</span></span>

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="219c7-835">Quando si avvia la macchina virtuale e viene richiesta una passphrase, usare la passphrase specificata nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="219c7-835">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="219c7-837">Preparare la macchina virtuale per il caricamento in Azure usando le istruzioni relative a "CentOS 7.0+" disponibili in [Preparare una macchina virtuale basata su CentOS per Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="219c7-837">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="219c7-838">Non eseguire ancora l'ultimo passaggio, ovvero il deprovisioning della VM.</span><span class="sxs-lookup"><span data-stu-id="219c7-838">Do not run the last step (deprovisioning the VM) yet.</span></span>

6. <span data-ttu-id="219c7-839">È ora possibile effettuare il deprovisioning della macchina virtuale e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="219c7-839">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="219c7-840">Per configurare la crittografia per l'uso in Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="219c7-840">To configure encryption to work with Azure, do the following:</span></span>

1. <span data-ttu-id="219c7-841">Modificare il file /etc/dracut.conf e aggiungere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="219c7-841">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="219c7-842">Impostare come commento queste righe verso la fine del file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="219c7-842">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="219c7-843">Aggiungere la riga seguente all'inizio del file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="219c7-843">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="219c7-844">Modificare quindi tutte le occorrenze di:</span><span class="sxs-lookup"><span data-stu-id="219c7-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="219c7-845">to</span><span class="sxs-lookup"><span data-stu-id="219c7-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="219c7-846">Modificare /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e aggiungere questo codice dopo "# Open LUKS device":</span><span class="sxs-lookup"><span data-stu-id="219c7-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="219c7-847">Eseguire "/usr/sbin/dracut -f -v" per aggiornare initrd.</span><span class="sxs-lookup"><span data-stu-id="219c7-847">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span></span>

![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-to-an-azure-storage-account"></a><span data-ttu-id="219c7-849">Caricare il VHD crittografato in un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="219c7-849">Upload encrypted VHD to an Azure storage account</span></span>
<span data-ttu-id="219c7-850">Dopo aver abilitato la crittografia BitLocker o la crittografia DM-Crypt, il disco rigido virtuale crittografato locale dovrà essere caricato nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="219c7-850">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-the-disk-encryption-secret-for-the-pre-encrypted-vm-to-your-key-vault"></a><span data-ttu-id="219c7-851">Caricare il segreto di crittografia del disco per la VM pre-crittografata nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="219c7-851">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span></span>
<span data-ttu-id="219c7-852">Il segreto di crittografia del disco ottenuto in precedenza deve essere caricato come segreto nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-852">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="219c7-853">L'insieme di credenziali delle chiavi deve avere la crittografia dei dischi e le autorizzazioni abilitate per il client di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="219c7-853">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="219c7-854">Segreto di crittografia del disco non crittografato con una chiave di crittografia della chiave</span><span class="sxs-lookup"><span data-stu-id="219c7-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="219c7-855">Per configurare il segreto nell'insieme di credenziali delle chiavi, usare [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="219c7-855">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="219c7-856">Se si ha una macchina virtuale Windows, il file con estensione bek viene codificato come stringa base64, quindi viene caricato nell'insieme di credenziali delle chiavi usando il cmdlet `Set-AzureKeyVaultSecret`.</span><span class="sxs-lookup"><span data-stu-id="219c7-856">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="219c7-857">Per Linux la passphrase viene codificata come stringa Base 64 e quindi caricata nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-857">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span></span> <span data-ttu-id="219c7-858">Assicurarsi anche che i tag seguenti siano impostati quando si crea il segreto nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="219c7-858">In addition, make sure that the following tags are set when you create the secret in the key vault.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="219c7-859">Usare `$secretUrl` nel passaggio successivo per [collegare il disco del sistema operativo senza usare una chiave di crittografia della chiave](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="219c7-859">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="219c7-860">Segreto di crittografia del disco crittografato con una chiave di crittografia della chiave</span><span class="sxs-lookup"><span data-stu-id="219c7-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="219c7-861">Prima di caricare il segreto nell'insieme di credenziali delle chiavi, è possibile crittografarlo usando una chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-861">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="219c7-862">Usare l'[API](https://msdn.microsoft.com/library/azure/dn878066.aspx) WRAP per crittografare prima di tutto il segreto con la chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="219c7-862">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span></span> <span data-ttu-id="219c7-863">L'output di questa operazione WRAP si basa su una stringa con codifica Base 64 dell'URL che può essere quindi caricata come segreto con il cmdlet [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="219c7-863">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="219c7-864">Usare `$KeyEncryptionKey` e `$secretUrl` nel passaggio successivo per [collegare il disco del sistema operativo usando una chiave di crittografia della chiave](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="219c7-864">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="219c7-865">Specificare un URL del segreto quando si collega un disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="219c7-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="219c7-866">Senza l'uso di una chiave di crittografia della chiave (KEK)</span><span class="sxs-lookup"><span data-stu-id="219c7-866">Without using a KEK</span></span>
<span data-ttu-id="219c7-867">Durante il collegamento del disco del sistema operativo è necessario passare `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="219c7-867">While you are attaching the OS disk, you need to pass `$secretUrl`.</span></span> <span data-ttu-id="219c7-868">L'URL è stato generato nella sezione "Segreto di crittografia del disco non crittografato con una chiave di crittografia della chiave".</span><span class="sxs-lookup"><span data-stu-id="219c7-868">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="219c7-869">Uso di una chiave di crittografia della chiave (KEK)</span><span class="sxs-lookup"><span data-stu-id="219c7-869">Using a KEK</span></span>
<span data-ttu-id="219c7-870">Quando si collega il disco del sistema operativo, vedere `$KeyEncryptionKey` e `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="219c7-870">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="219c7-871">L'URL è stato generato nella sezione "Segreto di crittografia del disco non crittografato con una chiave di crittografia della chiave".</span><span class="sxs-lookup"><span data-stu-id="219c7-871">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="219c7-872">Scaricare questa guida</span><span class="sxs-lookup"><span data-stu-id="219c7-872">Download this guide</span></span>
<span data-ttu-id="219c7-873">È possibile scaricare in questa guida dalla [Raccolta TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="219c7-873">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="219c7-874">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="219c7-874">For more information</span></span>
[<span data-ttu-id="219c7-875">Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 1</span><span class="sxs-lookup"><span data-stu-id="219c7-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="219c7-876">Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 2</span><span class="sxs-lookup"><span data-stu-id="219c7-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
