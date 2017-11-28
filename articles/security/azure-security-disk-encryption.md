---
title: Crittografia del disco per Windows e le macchine virtuali IaaS Linux aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="76716-103">Azure Disk Encryption per le macchine virtuali IaaS Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="76716-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="76716-104">Microsoft Azure è attivamente impegnata tooensuring la privacy dei dati, sovranità dati e consente di Azure ospitati toocontrol dati attraverso una serie di tecnologie avanzate tooencrypt, controllare e gestire chiavi di crittografia, access control e controllo dei dati.</span><span class="sxs-lookup"><span data-stu-id="76716-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="76716-105">In questo modo i clienti di Azure la soluzione hello flessibilità toochoose hello che meglio soddisfa le proprie esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="76716-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="76716-106">In questo articolo, si introdurrà tooa nuova soluzione "Crittografia del disco di Azure per Windows e di Linux IaaS VM" toohelp proteggere e salvaguardare i propri impegni di sicurezza e conformità organizzativi toomeet i dati.</span><span class="sxs-lookup"><span data-stu-id="76716-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="76716-107">carta Hello fornisce indicazioni dettagliate su come toouse hello disco di Azure le funzionalità di crittografia inclusi hello supportato scenari e l'esperienza utente hello.</span><span class="sxs-lookup"><span data-stu-id="76716-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-108">Alcune indicazioni possono comportare un maggior utilizzo delle risorse di calcolo, rete o dati con un conseguente aumento dei costi di licenza o sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="76716-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="76716-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="76716-109">Overview</span></span>
<span data-ttu-id="76716-110">Crittografia dischi di Azure è una nuova funzionalità che consente di crittografare i dischi delle macchine virtuali IaaS Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="76716-111">Crittografia disco Azure sfrutta standard di settore hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funzionalità di Windows e hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funzionalità di crittografia del volume tooprovide Linux per hello del sistema operativo e i dischi dati hello.</span><span class="sxs-lookup"><span data-stu-id="76716-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="76716-112">soluzione hello è integrato con [insieme credenziali chiavi Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp è controllare e gestire i segreti e tutte le chiavi di crittografia del disco hello nella sottoscrizione dell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="76716-113">soluzione Hello assicura anche che tutti i dati nei dischi di macchina virtuale hello vengono crittografati a riposo nell'archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="76716-114">Crittografia dischi di Azure per macchine virtuali IaaS Windows e Linux ha ora **disponibilità generale** in tutte le aree pubbliche e AzureGov di Azure per macchine virtuali standard e macchine virtuali con archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="76716-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="76716-115">Scenari di crittografia</span><span class="sxs-lookup"><span data-stu-id="76716-115">Encryption scenarios</span></span>
<span data-ttu-id="76716-116">Hello soluzioni di crittografia del disco di Azure supporta hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="76716-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="76716-117">Abilitare la crittografia nelle nuove VM IaaS create da chiavi di crittografia e VHD pre-crittografati</span><span class="sxs-lookup"><span data-stu-id="76716-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="76716-118">Abilitare la crittografia in nuove macchine virtuali IaaS create da immagini della raccolta di Azure hello è supportato</span><span class="sxs-lookup"><span data-stu-id="76716-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="76716-119">Abilitare la crittografia in VM IaaS esistenti in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="76716-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="76716-120">Disabilitare la crittografia nelle VM IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="76716-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="76716-121">Disabilitare la crittografia nelle unità dati per le VM IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="76716-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="76716-122">Abilitare la crittografia delle macchine virtuali con disco gestito</span><span class="sxs-lookup"><span data-stu-id="76716-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="76716-123">Aggiornare le impostazioni di crittografia di una macchina virtuale non dotata di archiviazione Premium crittografata esistente</span><span class="sxs-lookup"><span data-stu-id="76716-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="76716-124">Backup e ripristino di macchine virtuali crittografate con chiave di crittografia della chiave</span><span class="sxs-lookup"><span data-stu-id="76716-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="76716-125">soluzione Hello supporta hello seguenti scenari per le macchine virtuali IaaS quando sono abilitati in Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="76716-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="76716-126">Integrazione dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="76716-127">Macchine virtuali di livello Standard: [serie A, D, DS, G, GS, F e così via per VM IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="76716-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="76716-128">Abilitare la crittografia in Windows e le macchine virtuali IaaS di Linux e le macchine virtuali di disco gestito da hello supportate immagini della raccolta di Azure</span><span class="sxs-lookup"><span data-stu-id="76716-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="76716-129">Disabilitare la crittografia nel sistema operativo e nelle unità dati per le macchine virtuali IaaS Windows e per le macchine virtuali con disco gestito</span><span class="sxs-lookup"><span data-stu-id="76716-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="76716-130">Disabilitare la crittografia nelle unità dati per le macchine virtuali IaaS Linux e per le macchine virtuali con disco gestito</span><span class="sxs-lookup"><span data-stu-id="76716-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="76716-131">Abilitare la crittografia in VM IaaS eseguite nel sistema operativo client Windows</span><span class="sxs-lookup"><span data-stu-id="76716-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="76716-132">Abilitare la crittografia su volumi con percorsi di montaggio</span><span class="sxs-lookup"><span data-stu-id="76716-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="76716-133">Abilitare la crittografia nelle macchine virtuali Linux configurate con striping del disco (RAID) tramite mdadm</span><span class="sxs-lookup"><span data-stu-id="76716-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="76716-134">Abilitare la crittografia nelle macchine virtuali Linux usando LVM per i dischi dati</span><span class="sxs-lookup"><span data-stu-id="76716-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="76716-135">Abilitare la crittografia nelle VM Windows configurate con spazi di archiviazione</span><span class="sxs-lookup"><span data-stu-id="76716-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="76716-136">Aggiornare le impostazioni di crittografia di una macchina virtuale non dotata di archiviazione Premium crittografata esistente</span><span class="sxs-lookup"><span data-stu-id="76716-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="76716-137">Sono supportate tutte le aree di Azure pubbliche e AzureGov</span><span class="sxs-lookup"><span data-stu-id="76716-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="76716-138">soluzione Hello non supporta hello seguenti scenari, le funzionalità e tecnologie:</span><span class="sxs-lookup"><span data-stu-id="76716-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="76716-139">VM IaaS del piano Basic</span><span class="sxs-lookup"><span data-stu-id="76716-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="76716-140">Disabilitazione della crittografia in un'unità del sistema operativo per le VM IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="76716-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="76716-141">La disabilitazione della crittografia in un'unità di dati se è crittografato hello unità del sistema operativo per le macchine virtuali Iaas di Linux</span><span class="sxs-lookup"><span data-stu-id="76716-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="76716-142">Macchine virtuali IaaS che vengono creati utilizzando il metodo di creazione hello classico di VM</span><span class="sxs-lookup"><span data-stu-id="76716-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="76716-143">La crittografia per le immagini personalizzate nelle macchine virtuali Windows e Linux IaaS NON è supportata.</span><span class="sxs-lookup"><span data-stu-id="76716-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="76716-144">La crittografia in disco del sistema operativo di Linux LVM non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="76716-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="76716-145">Questa compatibilità è di prossima integrazione.</span><span class="sxs-lookup"><span data-stu-id="76716-145">This support will come soon.</span></span>
* <span data-ttu-id="76716-146">Integrazione con il servizio di gestione delle chiavi locale.</span><span class="sxs-lookup"><span data-stu-id="76716-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="76716-147">File di Azure (file system condiviso), file system di rete (NFS, Network File System), volumi dinamici e macchine virtuali Windows configurate con sistemi RAID basati su software</span><span class="sxs-lookup"><span data-stu-id="76716-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="76716-148">Backup e ripristino di macchine virtuali crittografate senza chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="76716-149">Aggiornare le impostazioni di crittografia di una macchina virtuale con archiviazione Premium crittografata esistente.</span><span class="sxs-lookup"><span data-stu-id="76716-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-150">Backup e ripristino di macchine virtuali crittografate è supportata solo per le macchine virtuali che vengono crittografate con la configurazione KEK hello.</span><span class="sxs-lookup"><span data-stu-id="76716-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="76716-151">Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="76716-152">La chiave di crittografia della chiave è un parametro facoltativo che abilita la crittografia delle VM.</span><span class="sxs-lookup"><span data-stu-id="76716-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="76716-153">Questo supporto sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="76716-153">This support is coming soon.</span></span>
> <span data-ttu-id="76716-154">L'aggiornamento delle impostazioni di crittografia di una macchina virtuale con archiviazione Premium crittografata esistente non è supportato.</span><span class="sxs-lookup"><span data-stu-id="76716-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="76716-155">Questo supporto sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="76716-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="76716-156">Funzionalità di crittografia</span><span class="sxs-lookup"><span data-stu-id="76716-156">Encryption features</span></span>
<span data-ttu-id="76716-157">Quando si abilita e distribuire la crittografia del disco di Azure per le macchine virtuali IaaS di Azure, hello seguenti funzionalità sono abilitate, a seconda della configurazione di hello fornita:</span><span class="sxs-lookup"><span data-stu-id="76716-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="76716-158">Crittografia del volume del sistema operativo hello volume tooprotect hello avvio inattivi nell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="76716-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="76716-159">Crittografia dei dati volumi tooprotect hello volumi di dati inattivi nell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="76716-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="76716-160">La disabilitazione della crittografia in hello del sistema operativo e dati unità per le macchine virtuali IaaS di Windows</span><span class="sxs-lookup"><span data-stu-id="76716-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="76716-161">La disabilitazione della crittografia dati hello unità per le macchine virtuali IaaS Linux (solo se OS unità non crittografata)</span><span class="sxs-lookup"><span data-stu-id="76716-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="76716-162">Protezione delle chiavi di crittografia hello e segreti nella sottoscrizione dell'insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="76716-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="76716-163">La segnalazione dello stato di crittografia hello di hello crittografati VM IaaS</span><span class="sxs-lookup"><span data-stu-id="76716-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="76716-164">Rimozione delle impostazioni di configurazione di crittografia del disco dalla macchina virtuale IaaS di hello</span><span class="sxs-lookup"><span data-stu-id="76716-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="76716-165">Backup e ripristino di macchine virtuali crittografati utilizzando il servizio di Backup di Azure hello</span><span class="sxs-lookup"><span data-stu-id="76716-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="76716-166">Backup e ripristino di macchine virtuali crittografate è supportata solo per le macchine virtuali che vengono crittografate con la configurazione KEK hello.</span><span class="sxs-lookup"><span data-stu-id="76716-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="76716-167">Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="76716-168">La chiave di crittografia della chiave è un parametro facoltativo che abilita la crittografia delle VM.</span><span class="sxs-lookup"><span data-stu-id="76716-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="76716-169">Crittografia dischi di Azure per macchine virtuali IaaS per soluzioni Windows e Linux include:</span><span class="sxs-lookup"><span data-stu-id="76716-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="76716-170">estensione di crittografia del disco Hello per Windows.</span><span class="sxs-lookup"><span data-stu-id="76716-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="76716-171">estensione di crittografia del disco Hello per Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="76716-172">cmdlet di PowerShell Hello crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="76716-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="76716-173">Hello la crittografia del cmdlet di Azure interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="76716-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="76716-174">modelli di Azure Resource Manager Hello crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="76716-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="76716-175">Hello soluzioni di crittografia del disco di Azure è supportata nelle macchine virtuali IaaS che eseguono Windows o del sistema operativo Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="76716-176">Per ulteriori informazioni sui sistemi operativi hello supportato, vedere hello "Prerequisiti" sezione.</span><span class="sxs-lookup"><span data-stu-id="76716-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-177">Non è previsto alcun addebito aggiuntivo per la crittografia dei dischi delle macchine virtuali con Crittografia dischi di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="76716-178">Proposta di valore</span><span class="sxs-lookup"><span data-stu-id="76716-178">Value proposition</span></span>
<span data-ttu-id="76716-179">Quando si applica la soluzione hello crittografia-Gestione disco di Azure, è possibile soddisfare hello esigenze aziendali seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="76716-180">Le macchine virtuali IaaS sono protette a rest, poiché è possibile utilizzare la crittografia standard del settore tecnologia tooaddress sicurezza e conformità i requisiti organizzativi.</span><span class="sxs-lookup"><span data-stu-id="76716-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="76716-181">Le macchine virtuali IaaS vengono avviate con chiavi e criteri controllati dai clienti ed è possibile controllarne l'utilizzo nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="76716-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="76716-182">Flusso di lavoro della crittografia</span><span class="sxs-lookup"><span data-stu-id="76716-182">Encryption workflow</span></span>
<span data-ttu-id="76716-183">crittografia disco tooenable per Windows e le macchine virtuali Linux, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="76716-184">Scegliere uno scenario di crittografia tra hello precedente gli scenari di crittografia.</span><span class="sxs-lookup"><span data-stu-id="76716-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="76716-185">Crittografia disco tooenabling tramite il modello di gestione risorse di Azure disco crittografia hello, i cmdlet di PowerShell o il comando CLI di partecipare e specificare la configurazione di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="76716-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="76716-186">Per uno scenario VHD cliente crittografato hello, caricare l'account di archiviazione tooyour VHD crittografato hello e hello crittografia chiave tooyour materiale chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="76716-187">Quindi, è possibile fornire hello crittografia configurazione tooenable crittografia in una nuova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="76716-188">Per nuove macchine virtuali create da hello Marketplace e le macchine virtuali esistenti che sono già in esecuzione in Azure, fornire la crittografia tooenable configurazione di crittografia hello in hello VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="76716-189">Concedere accesso toohello piattaforma Azure tooread hello chiave di crittografia materiale (chiavi di crittografia di BitLocker per i sistemi Windows) e la Passphrase per Linux dalla crittografia di tooenable insieme di credenziali delle chiavi in hello VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="76716-190">Fornire hello Azure Active Directory (Azure AD) dell'applicazione identità toowrite hello crittografia chiave tooyour materiale chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="76716-191">In questo modo viene abilitata la crittografia su hello VM IaaS per gli scenari di hello descritti nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="76716-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="76716-192">Azure Aggiorna modello del servizio VM hello con la crittografia e la configurazione dell'insieme di credenziali chiave hello e imposta le VM crittografate.</span><span class="sxs-lookup"><span data-stu-id="76716-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="76716-194">Flusso di lavoro della decrittografia</span><span class="sxs-lookup"><span data-stu-id="76716-194">Decryption workflow</span></span>
<span data-ttu-id="76716-195">crittografia del disco toodisable per le macchine virtuali IaaS, hello completo seguendo i passaggi generali:</span><span class="sxs-lookup"><span data-stu-id="76716-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="76716-196">Scegliere crittografia toodisable (decrittografia) in una VM IaaS in esecuzione in Azure tramite il modello di gestione risorse di Azure disco crittografia hello o i cmdlet di PowerShell e specificare la configurazione di decrittografia hello.</span><span class="sxs-lookup"><span data-stu-id="76716-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="76716-197">Questo passaggio consente di disattivare la crittografia del volume di dati del sistema operativo o hello hello o entrambi in esecuzione la macchina virtuale IaaS Windows hello.</span><span class="sxs-lookup"><span data-stu-id="76716-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="76716-198">Tuttavia, come indicato nella sezione precedente di hello, la disabilitazione della crittografia del disco del sistema operativo per Linux non è supportata.</span><span class="sxs-lookup"><span data-stu-id="76716-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="76716-199">passaggio di decrittografia Hello è consentito solo per le unità dati le macchine virtuali Linux come disco del sistema operativo hello non è crittografato.</span><span class="sxs-lookup"><span data-stu-id="76716-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="76716-200">Gli aggiornamenti di Azure hello modello di macchina virtuale del servizio e VM IaaS hello è contrassegnato decrittografata.</span><span class="sxs-lookup"><span data-stu-id="76716-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="76716-201">contenuto Hello di hello VM non venga crittografati a riposo.</span><span class="sxs-lookup"><span data-stu-id="76716-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-202">operazione di disabilitazione crittografia Hello non elimina il materiale della chiave dell'insieme di credenziali e hello crittografia chiave (chiavi di crittografia di BitLocker per i sistemi Windows) o la Passphrase per Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="76716-203">La disabilitazione della crittografica del disco del sistema operativo per Linux non è supportata.</span><span class="sxs-lookup"><span data-stu-id="76716-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="76716-204">passaggio di decrittografia Hello è consentito solo per le unità dati le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="76716-205">La disabilitazione della crittografia del disco dati per Linux non è supportata se è crittografato hello unità del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="76716-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76716-206">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="76716-206">Prerequisites</span></span>
<span data-ttu-id="76716-207">Prima di abilitare la crittografia del disco di Azure nelle macchine virtuali IaaS di Azure per gli scenari supportato hello illustrati nella sezione "Overview" hello, vedere hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="76716-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="76716-208">È necessario disporre le risorse toocreate una sottoscrizione Azure attiva valida in Azure in aree hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="76716-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="76716-209">Crittografia disco Azure è supportata in hello seguenti versioni di Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="76716-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="76716-210">Crittografia di disco di Azure è supportata nelle seguenti versioni di client Windows hello: il client di Windows 10 e Windows 8.</span><span class="sxs-lookup"><span data-stu-id="76716-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-211">Per Windows Server 2008 R2 è necessario che .NET Framework 4.5 sia installato prima dell'abilitazione della crittografia in Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="76716-212">È possibile installare da Windows Update per l'installazione dell'aggiornamento facoltativo hello Microsoft .NET Framework 4.5.2 per sistemi basati su x64 di Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="76716-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="76716-213">Crittografia disco Azure è supportata in hello seguente raccolta di Azure basato su distribuzioni di server Linux e le versioni:</span><span class="sxs-lookup"><span data-stu-id="76716-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="76716-214">Distribuzione Linux</span><span class="sxs-lookup"><span data-stu-id="76716-214">Linux Distribution</span></span> | <span data-ttu-id="76716-215">Versione</span><span class="sxs-lookup"><span data-stu-id="76716-215">Version</span></span> | <span data-ttu-id="76716-216">Tipo di volume supportato per la crittografia</span><span class="sxs-lookup"><span data-stu-id="76716-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="76716-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="76716-217">Ubuntu</span></span> | <span data-ttu-id="76716-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="76716-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="76716-219">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="76716-219">OS and Data disk</span></span> |
| <span data-ttu-id="76716-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="76716-220">Ubuntu</span></span> | <span data-ttu-id="76716-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="76716-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="76716-222">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="76716-222">OS and Data disk</span></span> |
| <span data-ttu-id="76716-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="76716-223">Ubuntu</span></span> | <span data-ttu-id="76716-224">12.10</span><span class="sxs-lookup"><span data-stu-id="76716-224">12.10</span></span> | <span data-ttu-id="76716-225">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-225">Data disk</span></span> |
| <span data-ttu-id="76716-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="76716-226">Ubuntu</span></span> | <span data-ttu-id="76716-227">12.04</span><span class="sxs-lookup"><span data-stu-id="76716-227">12.04</span></span> | <span data-ttu-id="76716-228">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-228">Data disk</span></span> |
| <span data-ttu-id="76716-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="76716-229">RHEL</span></span> | <span data-ttu-id="76716-230">7.3</span><span class="sxs-lookup"><span data-stu-id="76716-230">7.3</span></span> | <span data-ttu-id="76716-231">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="76716-231">OS and Data disk</span></span> |
| <span data-ttu-id="76716-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="76716-232">RHEL</span></span> | <span data-ttu-id="76716-233">7,2</span><span class="sxs-lookup"><span data-stu-id="76716-233">7.2</span></span> | <span data-ttu-id="76716-234">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="76716-234">OS and Data disk</span></span> |
| <span data-ttu-id="76716-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="76716-235">RHEL</span></span> | <span data-ttu-id="76716-236">6.8</span><span class="sxs-lookup"><span data-stu-id="76716-236">6.8</span></span> | <span data-ttu-id="76716-237">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="76716-237">OS and Data disk</span></span> |
| <span data-ttu-id="76716-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="76716-238">RHEL</span></span> | <span data-ttu-id="76716-239">6.7</span><span class="sxs-lookup"><span data-stu-id="76716-239">6.7</span></span> | <span data-ttu-id="76716-240">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-240">Data disk</span></span> |
| <span data-ttu-id="76716-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="76716-241">CentOS</span></span> | <span data-ttu-id="76716-242">7.3</span><span class="sxs-lookup"><span data-stu-id="76716-242">7.3</span></span> | <span data-ttu-id="76716-243">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="76716-243">OS and Data disk</span></span> |
| <span data-ttu-id="76716-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="76716-244">CentOS</span></span> | <span data-ttu-id="76716-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="76716-245">7.2n</span></span> | <span data-ttu-id="76716-246">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="76716-246">OS and Data disk</span></span> |
| <span data-ttu-id="76716-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="76716-247">CentOS</span></span> | <span data-ttu-id="76716-248">6.8</span><span class="sxs-lookup"><span data-stu-id="76716-248">6.8</span></span> | <span data-ttu-id="76716-249">Disco del sistema operativo e dati</span><span class="sxs-lookup"><span data-stu-id="76716-249">OS and Data disk</span></span> |
| <span data-ttu-id="76716-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="76716-250">CentOS</span></span> | <span data-ttu-id="76716-251">7.1</span><span class="sxs-lookup"><span data-stu-id="76716-251">7.1</span></span> | <span data-ttu-id="76716-252">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-252">Data disk</span></span> |
| <span data-ttu-id="76716-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="76716-253">CentOS</span></span> | <span data-ttu-id="76716-254">7.0</span><span class="sxs-lookup"><span data-stu-id="76716-254">7.0</span></span> | <span data-ttu-id="76716-255">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-255">Data disk</span></span> |
| <span data-ttu-id="76716-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="76716-256">CentOS</span></span> | <span data-ttu-id="76716-257">6.7</span><span class="sxs-lookup"><span data-stu-id="76716-257">6.7</span></span> | <span data-ttu-id="76716-258">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-258">Data disk</span></span> |
| <span data-ttu-id="76716-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="76716-259">CentOS</span></span> | <span data-ttu-id="76716-260">6.6</span><span class="sxs-lookup"><span data-stu-id="76716-260">6.6</span></span> | <span data-ttu-id="76716-261">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-261">Data disk</span></span> |
| <span data-ttu-id="76716-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="76716-262">CentOS</span></span> | <span data-ttu-id="76716-263">6,5</span><span class="sxs-lookup"><span data-stu-id="76716-263">6.5</span></span> | <span data-ttu-id="76716-264">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-264">Data disk</span></span> |
| <span data-ttu-id="76716-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="76716-265">openSUSE</span></span> | <span data-ttu-id="76716-266">13.2</span><span class="sxs-lookup"><span data-stu-id="76716-266">13.2</span></span> | <span data-ttu-id="76716-267">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-267">Data disk</span></span> |
| <span data-ttu-id="76716-268">SLES</span><span class="sxs-lookup"><span data-stu-id="76716-268">SLES</span></span> | <span data-ttu-id="76716-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="76716-269">12 SP1</span></span> | <span data-ttu-id="76716-270">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-270">Data disk</span></span> |
| <span data-ttu-id="76716-271">SLES</span><span class="sxs-lookup"><span data-stu-id="76716-271">SLES</span></span> | <span data-ttu-id="76716-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="76716-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="76716-273">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-273">Data disk</span></span> |
| <span data-ttu-id="76716-274">SLES</span><span class="sxs-lookup"><span data-stu-id="76716-274">SLES</span></span> | <span data-ttu-id="76716-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="76716-275">HPC 12</span></span> | <span data-ttu-id="76716-276">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-276">Data disk</span></span> |
| <span data-ttu-id="76716-277">SLES</span><span class="sxs-lookup"><span data-stu-id="76716-277">SLES</span></span> | <span data-ttu-id="76716-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="76716-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="76716-279">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-279">Data disk</span></span> |
| <span data-ttu-id="76716-280">SLES</span><span class="sxs-lookup"><span data-stu-id="76716-280">SLES</span></span> | <span data-ttu-id="76716-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="76716-281">11 SP4</span></span> | <span data-ttu-id="76716-282">Disco dati</span><span class="sxs-lookup"><span data-stu-id="76716-282">Data disk</span></span> |

* <span data-ttu-id="76716-283">Crittografia disco Azure richiede che l'insieme di credenziali chiave e le macchine virtuali si trovino in hello stessa regione di Azure e di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="76716-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-284">Configurazione delle risorse hello in aree separate provoca un errore nell'attivazione di funzionalità di crittografia del disco Azure hello.</span><span class="sxs-lookup"><span data-stu-id="76716-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="76716-285">tooset configurato e configurare l'insieme di credenziali chiave di crittografia del disco di Azure, vedere sezione **impostare e configurare l'insieme di credenziali chiave di crittografia del disco Azure** in hello *prerequisiti* sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="76716-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="76716-286">tooset configurato e configurare l'applicazione Azure AD in Azure Active directory per la crittografia del disco di Azure, vedere sezione **configurare un'applicazione hello Azure AD in Azure Active Directory** in hello *prerequisiti* sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="76716-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="76716-287">tooset configurato e configurare criteri di accesso hello chiave dell'insieme di credenziali per un'applicazione hello Azure AD, nella sezione **impostare i criteri di accesso hello chiave dell'insieme di credenziali per un'applicazione hello Azure AD** in hello *prerequisiti* sezione In questo articolo.</span><span class="sxs-lookup"><span data-stu-id="76716-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="76716-288">Nella sezione tooprepare un VHD di Windows pre-crittografato, **preparare un disco rigido virtuale di Windows pre-crittografato** in hello *appendice*.</span><span class="sxs-lookup"><span data-stu-id="76716-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="76716-289">Nella sezione tooprepare un VHD Linux pre-crittografato, **preparare un VHD Linux pre-crittografato** in hello *appendice*.</span><span class="sxs-lookup"><span data-stu-id="76716-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="76716-290">Hello piattaforma Azure necessita di chiavi di crittografia toohello di accesso o i segreti nel toomake insieme di credenziali chiave li macchina virtuale di toohello disponibili quando viene avviato e decrittografa il volume di macchina virtuale del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="76716-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="76716-291">piattaforma tooAzure toogrant autorizzazioni set hello **EnabledForDiskEncryption** proprietà nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="76716-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="76716-292">Per ulteriori informazioni, vedere **impostare e configurare l'insieme di credenziali chiave di crittografia del disco Azure** in hello appendice.</span><span class="sxs-lookup"><span data-stu-id="76716-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="76716-293">È necessario applicare il controllo delle versioni agli URL del segreto dell'insieme di credenziali delle chiavi e della chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="76716-294">Azure applica questa restrizione relativa al controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="76716-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="76716-295">Per privata valida e KEK URL, vedere hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="76716-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="76716-296">Esempio di URL segreto valido: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="76716-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="76716-297">Esempio di URL della chiave di crittografia della chiave valido: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="76716-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="76716-298">Crittografia dischi di Azure non supporta la possibilità di specificare i numeri di porta come parte dei segreti dell'insieme di credenziali delle chiavi e degli URL della chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="76716-299">Per esempi di URL di credenziali di chiave supportati e non supportati, vedere esempio hello:</span><span class="sxs-lookup"><span data-stu-id="76716-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="76716-300">URL dell'insieme di credenziali delle chiavi non accettabile: *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="76716-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="76716-301">URL dell'insieme di credenziali delle chiavi accettabile: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="76716-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="76716-302">funzionalità di crittografia del disco Azure hello tooenable, hello le macchine virtuali IaaS deve soddisfare hello seguendo i requisiti di configurazione di endpoint di rete:</span><span class="sxs-lookup"><span data-stu-id="76716-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="76716-303">un token tooconnect tooyour chiave insieme di credenziali, hello VM IaaS tooget deve essere in grado di tooconnect endpoint di Azure Active Directory tooan, \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="76716-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="76716-304">toowrite hello crittografia chiavi tooyour chiave dell'insieme di credenziali, hello VM IaaS, deve essere in grado di tooconnect toohello chiave dell'insieme di credenziali endpoint.</span><span class="sxs-lookup"><span data-stu-id="76716-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="76716-305">Hello VM IaaS, deve essere in grado di tooconnect tooan archiviazione di Azure endpoint che ospita hello repository estensioni di Azure e un account di archiviazione di Azure che ospita hello file VHD.</span><span class="sxs-lookup"><span data-stu-id="76716-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="76716-306">Se i criteri di protezione limitano l'accesso da macchine virtuali di Azure toohello Internet, è possibile risolvere l'URI precedente hello e configurare un toohello di connettività in uscita tooallow regola specifica gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="76716-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="76716-307">tooconfigure e accesso insieme credenziali chiavi Azure dietro un firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="76716-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="76716-308">Utilizzare hello la versione più recente di Azure PowerShell SDK versione tooconfigure crittografia del disco di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="76716-309">Scaricare una versione più recente di hello di [versione di Azure PowerShell](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="76716-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="76716-310">Crittografia dischi di Azure non è supportata in [Azure PowerShell SDK versione 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="76716-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="76716-311">Se si riceve un errore correlato toousing Azure PowerShell 1.1.0, vedere [tooAzure errore correlate di Azure disco crittografia PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="76716-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="76716-312">toorun qualsiasi comando CLI di Azure e associarlo a una sottoscrizione di Azure, è necessario installare prima CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="76716-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="76716-313">tooinstall CLI di Azure e associarlo a una sottoscrizione di Azure, vedere [come tooinstall e configurare Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="76716-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="76716-314">toouse CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure, vedere [i comandi CLI di Azure in modalità di gestione risorse](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="76716-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="76716-315">Quando la crittografia di un disco gestito, è obbligatorio tootake prerequisiti uno snapshot del disco hello gestito o un backup del disco hello di fuori di crittografia precedente tooenabling di crittografia del disco di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="76716-316">Senza un backup sul posto, qualsiasi errore imprevisto durante la crittografia potrebbe rendere impossibile disco hello e VM accessibili senza un'opzione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="76716-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="76716-317">Set-AzureRmVMDiskEncryptionExtension attualmente non eseguire il backup di dischi gestiti e genereranno un errore in cui viene eseguito un disco gestito, a meno che non è stato specificato il parametro - skipVmBackup hello.</span><span class="sxs-lookup"><span data-stu-id="76716-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="76716-318">Questo parametro è unsafe toouse a meno che non è di fuori di crittografia del disco di Azure è già stata effettuata una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="76716-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="76716-319">Quando viene specificato il parametro - skipVmBackup hello, hello cmdlet verrà non eseguire il backup di hello gestito disco precedente tooencryption.</span><span class="sxs-lookup"><span data-stu-id="76716-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="76716-320">Per questo motivo, viene considerato un toomake prerequisito obbligatorio che un backup del disco di hello gestito che macchina virtuale sia in posizione precedente tooenabling Azure crittografia del disco nel caso in cui è successivo ripristino necessari.</span><span class="sxs-lookup"><span data-stu-id="76716-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="76716-321">parametro - skipVmBackup Hello non deve mai essere utilizzata a meno che un backup o dello snapshot è già stato effettuato di fuori di crittografia del disco di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="76716-322">Hello soluzioni di crittografia del disco di Azure Usa protezione con chiave esterna di hello BitLocker per le macchine virtuali IaaS di Windows.</span><span class="sxs-lookup"><span data-stu-id="76716-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="76716-323">Per le macchine virtuali sono aggiunte a un dominio, NON eseguire il push di criteri di gruppo che applichino protezioni TPM.</span><span class="sxs-lookup"><span data-stu-id="76716-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="76716-324">Per informazioni sui criteri di gruppo hello "Consenti BitLocker senza un TPM compatibile", vedere [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="76716-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="76716-325">Criteri di BitLocker nelle macchine virtuali appartenenti a un dominio con criteri di gruppo personalizzato devono includere hello seguente impostazione: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` crittografia del disco di Azure avrà esito negativo quando le impostazioni di criteri di gruppo personalizzato per Bitlocker sono incompatibili.</span><span class="sxs-lookup"><span data-stu-id="76716-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="76716-326">Nei computer che non disponevano di hello corretta impostazione di criteri di applicare i nuovi criteri hello, imponendo hello nuovi criteri tooupdate (gpupdate.exe /force) e il riavvio potrebbe essere necessario.</span><span class="sxs-lookup"><span data-stu-id="76716-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="76716-327">toocreate un'applicazione Azure AD, creare un insieme di credenziali chiave, o configurare un insieme di credenziali chiave esistente e attivare la crittografia, vedere hello [script di PowerShell dei prerequisiti di crittografia del disco di Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="76716-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="76716-328">prerequisiti di crittografia del disco tooconfigure utilizzando hello CLI di Azure, vedere [questo script Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="76716-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="76716-329">toouse hello Azure Backup service tooback backup e ripristino crittografato le macchine virtuali, quando è abilitata la crittografia con la crittografia del disco di Azure, crittografano le macchine virtuali tramite la configurazione della chiave di crittografia del disco Azure hello.</span><span class="sxs-lookup"><span data-stu-id="76716-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="76716-330">Hello servizio di Backup supporta le macchine virtuali che vengono crittografate utilizzando solo la configurazione KEK.</span><span class="sxs-lookup"><span data-stu-id="76716-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="76716-331">Vedere [la modalità di crittografia delle macchine virtuali con la crittografia di Backup di Azure tooback backup e ripristino](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="76716-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="76716-332">Per la crittografia di un volume del sistema operativo Linux, riavviare una macchina virtuale è attualmente necessaria alla fine di hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="76716-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="76716-333">Questa operazione può essere eseguita tramite il portale di hello, powershell o CLI.</span><span class="sxs-lookup"><span data-stu-id="76716-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="76716-334">stato di hello tootrack della crittografia, eseguire periodicamente il polling il messaggio di stato hello restituito da Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span><span class="sxs-lookup"><span data-stu-id="76716-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="76716-335">Una volta completata la crittografia, messaggio di stato hello hello restituito da questo comando indicherà questo.</span><span class="sxs-lookup"><span data-stu-id="76716-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="76716-336">Ad esempio, "ProgressMessage: disco del sistema operativo sono state crittografate, riavviare hello VM" in questo punto di hello VM può essere riavviato e utilizzato.</span><span class="sxs-lookup"><span data-stu-id="76716-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="76716-337">Crittografia disco Azure per Linux richiede dati dischi toohave un file system montato in Linux precedenti tooencryption</span><span class="sxs-lookup"><span data-stu-id="76716-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="76716-338">In modo ricorsivo i dischi montati dati non supportati da hello crittografia del disco di Azure per Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="76716-339">Ad esempio, se hello sistema di destinazione è montato un disco in /foo/bar e quindi un'altra in /foo/bar/baz, crittografia hello di /foo/bar/baz avrà esito positivo, ma la crittografia di foo/barra avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="76716-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="76716-340">Crittografia disco Azure è supportata solo su immagini della raccolta di Azure supportata che soddisfano i prerequisiti di hello menzionati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="76716-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="76716-341">Immagini personalizzate di clienti non sono supportate a causa di toocustom gli schemi di partizione e i comportamenti di processo che potrebbero esistere in queste immagini.</span><span class="sxs-lookup"><span data-stu-id="76716-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="76716-342">Inoltre, potrebbero risultare incompatibili anche le macchine virtuali basate su immagini della raccolta che inizialmente soddisfacevano i prerequisiti ma che sono state modificate dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="76716-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="76716-343">Per che motivo, hello suggerito procedure per la crittografia di una VM Linux toostart da un'immagine della raccolta pulita, crittografare hello VM e aggiungere software personalizzato o dati toohello macchina virtuale in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="76716-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="76716-344">Backup e ripristino di macchine virtuali crittografate è supportata solo per le macchine virtuali che vengono crittografate con la configurazione KEK hello.</span><span class="sxs-lookup"><span data-stu-id="76716-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="76716-345">Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="76716-346">La chiave di crittografia della chiave è un parametro facoltativo che abilita la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="76716-347">Impostare hello applicazione Azure AD in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76716-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="76716-348">Quando è necessario toobe crittografia abilitata in una macchina virtuale in esecuzione in Azure, la crittografia del disco di Azure genera e scrive hello crittografia chiavi tooyour chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="76716-349">La gestione delle chiavi di crittografia nell'insieme di credenziali delle chiavi richiede l'autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76716-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="76716-350">Creare quindi un'applicazione Azure AD per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="76716-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="76716-351">È possibile trovare i passaggi dettagliati per la registrazione di un'applicazione nella sezione "Ottenere un'identità per hello applicazione" hello del post di blog hello [insieme credenziali chiavi Azure - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="76716-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="76716-352">Questo post include anche alcuni esempi utili per l'installazione e la configurazione dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="76716-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="76716-353">Ai fini dell'autenticazione, è possibile usare l'autenticazione basata sul segreto client o l'autenticazione di Azure AD basata sul certificato client.</span><span class="sxs-lookup"><span data-stu-id="76716-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="76716-354">Autenticazione basata su segreto client per Azure AD</span><span class="sxs-lookup"><span data-stu-id="76716-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="76716-355">Nelle sezioni Hello che seguono consentono di configurare un'autenticazione client basata su chiave privata per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76716-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="76716-356">Creare un'applicazione Azure AD usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="76716-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="76716-357">Utilizzare hello seguente cmdlet di PowerShell toocreate un'applicazione Azure AD:</span><span class="sxs-lookup"><span data-stu-id="76716-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="76716-358">$azureAdApplication.ApplicationId è hello AD ClientID Azure e $aadClientSecret è privata hello del client che è necessario utilizzare tooenable successiva crittografia del disco di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="76716-359">Proteggere la chiave privata client hello Azure AD in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="76716-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="76716-360">Configurare Azure AD hello client ID e il segreto dal portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="76716-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="76716-361">È possibile anche impostare l'ID client di Azure AD e il segreto tramite hello [portale di Azure classico]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="76716-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="76716-362">tooperform questa attività, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="76716-363">Fare clic su hello **Active Directory** scheda.</span><span class="sxs-lookup"><span data-stu-id="76716-363">Click hello **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="76716-365">Fare clic su **Aggiungi applicazione**e quindi nome dell'applicazione hello tipo.</span><span class="sxs-lookup"><span data-stu-id="76716-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="76716-367">Fare clic sul pulsante freccia hello e quindi configurare le proprietà dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="76716-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="76716-369">Fare clic su hello segno di spunta in hello inferiore sinistro toofinish.</span><span class="sxs-lookup"><span data-stu-id="76716-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="76716-370">verrà visualizzata la pagina di configurazione dell'applicazione Hello e ID client di Azure AD hello viene visualizzato nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="76716-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="76716-372">Salvare la chiave privata client hello Azure AD, scegliendo hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="76716-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="76716-373">Si noti segreto client hello Azure AD nella casella di testo hello chiavi.</span><span class="sxs-lookup"><span data-stu-id="76716-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="76716-374">Proteggerlo correttamente.</span><span class="sxs-lookup"><span data-stu-id="76716-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="76716-376">Hello che precedono il flusso non è supportata nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="76716-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="76716-377">Usare un'applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="76716-377">Use an existing application</span></span>
<span data-ttu-id="76716-378">tooexecute hello i comandi seguenti, ottenere e usare hello [modulo Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="76716-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="76716-379">Hello comandi seguenti devono essere eseguiti da una nuova finestra di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76716-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="76716-380">Non usare Azure PowerShell o comandi di hello Azure Resource Manager finestra tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="76716-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="76716-381">Questo approccio è consigliato poiché questi cmdlet nel modulo di MSOnline hello o Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76716-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="76716-382">Autenticazione basata su certificato per Azure AD</span><span class="sxs-lookup"><span data-stu-id="76716-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="76716-383">L'autenticazione basata su certificato per Azure AD non è attualmente supportata nelle VM Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="76716-384">Hello nelle sezioni che seguono Mostra come tooconfigure un'autenticazione basata su certificati per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76716-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="76716-385">Creare un'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="76716-385">Create an Azure AD application</span></span>
<span data-ttu-id="76716-386">toocreate un'applicazione Azure AD, eseguire hello i cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="76716-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="76716-387">Sostituire segue hello `yourpassword` stringa con la password sicura e la password di hello misura di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="76716-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="76716-388">Dopo aver completato questo passaggio, caricare un file PFX file tooyour chiave dell'insieme di credenziali e abilitare hello accesso criteri necessari toodeploy che tooa certificato macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="76716-389">Usare un'applicazione Azure AD esistente</span><span class="sxs-lookup"><span data-stu-id="76716-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="76716-390">Se si configura l'autenticazione basata su certificati per un'applicazione esistente, utilizzare i cmdlet di PowerShell hello illustrati di seguito.</span><span class="sxs-lookup"><span data-stu-id="76716-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="76716-391">Essere tooexecute che di una nuova finestra di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76716-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="76716-392">Dopo aver completato questo passaggio, caricare un file PFX file tooyour chiave dell'insieme di credenziali e abilitare i criteri di accesso hello sono sufficiente toodeploy hello certificato tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="76716-393">Caricare un file PFX file tooyour chiave dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="76716-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="76716-394">Per una spiegazione dettagliata di questo processo, vedere [hello Blog del Team dell'insieme di credenziali chiave di Azure ufficiale](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="76716-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="76716-395">Hello seguendo i cmdlet di PowerShell è, tuttavia, è sufficiente per l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="76716-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="76716-396">Essere tooexecute che essi dalla console di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76716-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-397">Sostituire segue hello `yourpassword` stringa con la password sicura e la password di hello misura di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="76716-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

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

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="76716-398">Distribuire un certificato di tooan l'insieme di credenziali chiave macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="76716-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="76716-399">Dopo aver completato il caricamento di hello PFX, è possibile distribuire un certificato in hello insieme di credenziali chiave tooan esistente VM con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="76716-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
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

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="76716-400">Impostare i criteri di accesso hello chiave dell'insieme di credenziali per un'applicazione hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="76716-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="76716-401">L'applicazione Azure AD richiede le chiavi di hello tooaccess diritti o i segreti nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="76716-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="76716-402">Hello utilizzare [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant autorizzazioni toohello dell'applicazione, utilizzando l'ID client hello (che è stato generato quando è stata registrata un'applicazione hello) come hello _– ServicePrincipalName_ valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="76716-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="76716-403">toolearn informazioni, vedere hello post di blog [insieme credenziali chiavi Azure - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="76716-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="76716-404">Di seguito è riportato un esempio di come tooperform questa attività tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="76716-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="76716-405">Crittografia disco Azure richiede hello tooconfigure dopo l'applicazione client tooyour AD Azure i criteri di accesso: _WrapKey_ e _impostare_ autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="76716-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="76716-406">Terminologia</span><span class="sxs-lookup"><span data-stu-id="76716-406">Terminology</span></span>
<span data-ttu-id="76716-407">toounderstand alcuni dei termini comuni hello utilizzati da questa tecnologia, utilizzare hello terminologia nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="76716-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="76716-408">Terminologia</span><span class="sxs-lookup"><span data-stu-id="76716-408">Terminology</span></span> | <span data-ttu-id="76716-409">Definizione</span><span class="sxs-lookup"><span data-stu-id="76716-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="76716-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="76716-410">Azure AD</span></span> | <span data-ttu-id="76716-411">Azure AD è l'abbreviazione di [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="76716-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="76716-412">Un account Azure AD è un prerequisito per le operazioni di autenticazione, archiviazione e recupero dei segreti da un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="76716-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="76716-413">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="76716-413">Azure Key Vault</span></span> | <span data-ttu-id="76716-414">Key Vault è un servizio di crittografia e gestione delle chiavi basato su moduli di sicurezza hardware convalidati dagli standard FIPS (Federal Information Processing Standards), che consentono di proteggere le chiavi crittografiche e i segreti sensibili.</span><span class="sxs-lookup"><span data-stu-id="76716-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="76716-415">Per altre informazioni, vedere la documentazione di [Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="76716-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="76716-416">ARM</span><span class="sxs-lookup"><span data-stu-id="76716-416">ARM</span></span> | <span data-ttu-id="76716-417">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="76716-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="76716-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="76716-418">BitLocker</span></span> |<span data-ttu-id="76716-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) è una riconosciuto dal settore Windows volume tecnologia di crittografia utilizzato tooenable crittografia del disco nelle macchine virtuali IaaS di Windows.</span><span class="sxs-lookup"><span data-stu-id="76716-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="76716-420">BEK</span><span class="sxs-lookup"><span data-stu-id="76716-420">BEK</span></span> | <span data-ttu-id="76716-421">Le chiavi di crittografia di BitLocker sono volumi di dati e il volume di avvio utilizzati tooencrypt hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="76716-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="76716-422">le chiavi BitLocker Hello siano protette in un insieme di credenziali chiave come segreti.</span><span class="sxs-lookup"><span data-stu-id="76716-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="76716-423">CLI</span><span class="sxs-lookup"><span data-stu-id="76716-423">CLI</span></span> | <span data-ttu-id="76716-424">Vedere [Interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="76716-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="76716-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="76716-425">DM-Crypt</span></span> |<span data-ttu-id="76716-426">[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) è il sottosistema di crittografia del disco basati su Linux, trasparente hello utilizzati di crittografia del disco tooenable nelle macchine virtuali IaaS di Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="76716-427">KEK</span><span class="sxs-lookup"><span data-stu-id="76716-427">KEK</span></span> | <span data-ttu-id="76716-428">Chiave di crittografia è hello chiave asimmetrica (RSA 2048) che è possibile utilizzare tooprotect o eseguire il wrapping segreto hello.</span><span class="sxs-lookup"><span data-stu-id="76716-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="76716-429">È possibile fornire una chiave protetta tramite modulo di protezione hardware o una chiave protetta tramite software.</span><span class="sxs-lookup"><span data-stu-id="76716-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="76716-430">Per altre informazioni, vedere la documentazione di [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="76716-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="76716-431">Cmdlet PS</span><span class="sxs-lookup"><span data-stu-id="76716-431">PS cmdlets</span></span> | <span data-ttu-id="76716-432">Vedere [Azure PowerShell cmdlets](/powershell/azure/overview) (Cmdlet di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="76716-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="76716-433">Installare e configurare l'insieme di credenziali delle chiavi per Crittografia dischi di Azure</span><span class="sxs-lookup"><span data-stu-id="76716-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="76716-434">Crittografia disco Azure consente di salvaguardare hello disco crittografia chiavi e segreti nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="76716-435">tooset di credenziali delle chiavi di crittografia del disco di Azure, hello completato i passaggi in ognuna delle seguenti sezioni hello.</span><span class="sxs-lookup"><span data-stu-id="76716-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="76716-436">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="76716-436">Create a key vault</span></span>
<span data-ttu-id="76716-437">toocreate un insieme di credenziali chiave, utilizzare uno dei hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="76716-438">Modello di Resource Manager "101-Key-Vault-Create"</span><span class="sxs-lookup"><span data-stu-id="76716-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* <span data-ttu-id="76716-439">[Azure PowerShell key vault cmdlets](/powershell/module/azurerm.keyvault/#key_vault) (Cmdlet dell'insieme di credenziali delle chiavi di Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="76716-439">[Azure PowerShell key vault cmdlets](/powershell/module/azurerm.keyvault/#key_vault)</span></span>
* <span data-ttu-id="76716-440">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="76716-440">Azure Resource Manager</span></span>
* <span data-ttu-id="76716-441">Come troppo[proteggere credenziali delle chiavi](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="76716-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="76716-442">Se un insieme di credenziali chiave è già configurato per la sottoscrizione, è possibile ignorare toohello nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="76716-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Insieme di credenziali chiave Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="76716-444">Configurare una chiave di crittografia della chiave (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="76716-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="76716-445">Se si desidera toouse una chiave di scambio delle CHIAVI per un ulteriore livello di protezione per le chiavi di crittografia BitLocker hello, aggiungere un insieme di credenziali chiave di KEK tooyour.</span><span class="sxs-lookup"><span data-stu-id="76716-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="76716-446">Hello utilizzare [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate cmdlet una chiave di crittografia della chiave nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="76716-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="76716-447">È anche possibile importare una chiave di crittografia della chiave dal modulo di protezione hardware di gestione delle chiavi locale.</span><span class="sxs-lookup"><span data-stu-id="76716-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="76716-448">Per altre informazioni, vedere la [Documentazione su Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="76716-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="76716-449">È possibile aggiungere hello KEK passando tooAzure Resource Manager o tramite l'interfaccia dell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Insieme di credenziali chiave Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="76716-451">Configurare le autorizzazioni dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="76716-451">Set key vault permissions</span></span>
<span data-ttu-id="76716-452">Hello piattaforma Azure necessita di chiavi di crittografia toohello di accesso o i segreti nel toomake insieme di credenziali chiave li toohello disponibile macchina virtuale per l'avvio e la decrittografia dei volumi hello.</span><span class="sxs-lookup"><span data-stu-id="76716-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="76716-453">toogrant autorizzazioni toohello piattaforma Azure, hello set **EnabledForDiskEncryption** insieme di credenziali delle proprietà nella chiave hello tramite cmdlet di PowerShell hello insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="76716-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="76716-454">È inoltre possibile impostare hello **EnabledForDiskEncryption** proprietà visitando hello [Esplora inventario risorse di Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="76716-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="76716-455">Come accennato in precedenza, è necessario impostare hello **EnabledForDiskEncryption** proprietà credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="76716-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="76716-456">In caso contrario, la distribuzione di hello non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="76716-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="76716-457">È possibile impostare i criteri di accesso per l'applicazione Azure AD dall'interfaccia di insieme di credenziali chiave hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="76716-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Insieme di credenziali chiave Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Insieme di credenziali chiave Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="76716-460">In hello **criteri di accesso avanzato** scheda, assicurarsi che l'insieme di credenziali chiave è abilitata per la crittografia del disco di Azure:</span><span class="sxs-lookup"><span data-stu-id="76716-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="76716-462">Scenari di distribuzione della crittografia dei dischi ed esperienze utente</span><span class="sxs-lookup"><span data-stu-id="76716-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="76716-463">È possibile abilitare molti scenari di crittografia del disco e passaggi hello possono variare in base uno scenario toohello.</span><span class="sxs-lookup"><span data-stu-id="76716-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="76716-464">Hello nelle sezioni seguenti riguardano scenari hello in maggiore dettaglio.</span><span class="sxs-lookup"><span data-stu-id="76716-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="76716-465">Abilitare la crittografia in nuove macchine virtuali IaaS creati da hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="76716-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="76716-466">È possibile abilitare la crittografia del disco nella nuova macchina virtuale Windows IaaS da hello Marketplace in Azure utilizzando hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="76716-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="76716-467">Nel modello hello avvio rapido di Azure, fare clic su **distribuire tooAzure**, immettere la configurazione di crittografia hello hello **parametri** blade e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76716-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="76716-468">Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** tooenable crittografia in una nuova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-469">Questo modello consente di creare un nuovo crittografati macchina virtuale di Windows che usa l'immagine della raccolta hello Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="76716-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="76716-470">È possibile abilitare la crittografia dei dischi in una nuova macchina virtuale IaaS RedHat Linux 7.2 con una matrice RAID-0 da 200 GB usando questo modello di [Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="76716-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="76716-471">Dopo aver distribuito il modello di hello, verificare lo stato di crittografia di hello VM utilizzando hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, come descritto in [unità la crittografia del sistema operativo in una VM Linux in esecuzione](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="76716-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="76716-472">Quando viene restituito lo stato della macchina hello _VMRestartPending_, riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="76716-473">Hello nella tabella seguente sono elencati i parametri del modello di gestione risorse hello per nuove macchine virtuali da uno scenario di Marketplace hello usando un ID client di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="76716-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="76716-474">.</span><span class="sxs-lookup"><span data-stu-id="76716-474">Parameter</span></span> | <span data-ttu-id="76716-475">Descrizione</span><span class="sxs-lookup"><span data-stu-id="76716-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="76716-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="76716-476">adminUserName</span></span> | <span data-ttu-id="76716-477">Nome utente di amministratore per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="76716-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="76716-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="76716-478">adminPassword</span></span> | <span data-ttu-id="76716-479">Password dell'utente amministratore per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="76716-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="76716-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="76716-480">newStorageAccountName</span></span> | <span data-ttu-id="76716-481">Nome del toostore di account di archiviazione hello del sistema operativo e dischi rigidi virtuali dati.</span><span class="sxs-lookup"><span data-stu-id="76716-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="76716-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="76716-482">vmSize</span></span> | <span data-ttu-id="76716-483">Dimensioni della VM hello.</span><span class="sxs-lookup"><span data-stu-id="76716-483">Size of hello VM.</span></span> <span data-ttu-id="76716-484">Attualmente sono supportate solo le serie A, D e G Standard.</span><span class="sxs-lookup"><span data-stu-id="76716-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="76716-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="76716-485">virtualNetworkName</span></span> | <span data-ttu-id="76716-486">Nome della rete virtuale che hello NIC VM hello deve appartenere allo.</span><span class="sxs-lookup"><span data-stu-id="76716-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="76716-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="76716-487">subnetName</span></span> | <span data-ttu-id="76716-488">Nome della subnet hello nella rete virtuale che hello NIC VM hello deve appartenere allo.</span><span class="sxs-lookup"><span data-stu-id="76716-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="76716-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="76716-489">AADClientID</span></span> | <span data-ttu-id="76716-490">ID client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti tooyour chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="76716-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="76716-491">AADClientSecret</span></span> | <span data-ttu-id="76716-492">Segreto client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti tooyour chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="76716-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="76716-493">keyVaultURL</span></span> | <span data-ttu-id="76716-494">URL della chiave hello insieme di credenziali di tale chiave deve essere caricata a BitLocker hello.</span><span class="sxs-lookup"><span data-stu-id="76716-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="76716-495">È possibile ottenerlo utilizzando cmdlet hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="76716-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="76716-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="76716-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="76716-497">URL della chiave di crittografia della chiave hello che è usato tooencrypt hello generato chiave BitLocker (facoltativa).</span><span class="sxs-lookup"><span data-stu-id="76716-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="76716-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="76716-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="76716-499">Gruppo di risorse dell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="76716-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="76716-500">vmName</span><span class="sxs-lookup"><span data-stu-id="76716-500">vmName</span></span> | <span data-ttu-id="76716-501">Nome della macchina virtuale che hello l'operazione di crittografia hello è toobe eseguiti.</span><span class="sxs-lookup"><span data-stu-id="76716-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="76716-502">_KeyEncryptionKeyURL_ è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="76716-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="76716-503">È possibile portare la propria KEK toofurther salvaguardia hello dati chiave di crittografia (Passphrase segreto) nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="76716-504">Abilitare la crittografia delle nuove VM IaaS create da chiavi di crittografia e dischi rigidi virtuali crittografati dei clienti</span><span class="sxs-lookup"><span data-stu-id="76716-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="76716-505">In questo scenario, è possibile abilitare la crittografia utilizzando il modello di gestione risorse di hello, i cmdlet di PowerShell o i comandi CLI.</span><span class="sxs-lookup"><span data-stu-id="76716-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="76716-506">Hello nelle sezioni seguenti illustrano nel modello di gestione risorse di maggiore dettaglio hello e i comandi CLI.</span><span class="sxs-lookup"><span data-stu-id="76716-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="76716-507">Seguire le istruzioni di hello da una di queste sezioni per preparare immagini pre-crittografate che possono essere usate in Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="76716-508">Dopo aver creato l'immagine di hello, è possibile utilizzare i passaggi di hello in hello successiva sezione toocreate una macchina virtuale Azure crittografati.</span><span class="sxs-lookup"><span data-stu-id="76716-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="76716-509">Preparare un disco rigido virtuale Windows pre-crittografato</span><span class="sxs-lookup"><span data-stu-id="76716-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="76716-510">Preparare un disco rigido virtuale Linux pre-crittografato</span><span class="sxs-lookup"><span data-stu-id="76716-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="76716-511">Utilizzando il modello di gestione risorse di hello</span><span class="sxs-lookup"><span data-stu-id="76716-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="76716-512">È possibile abilitare crittografia del disco in disco rigido virtuale crittografato utilizzando hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="76716-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="76716-513">Nel modello hello avvio rapido di Azure, fare clic su **distribuire tooAzure**, immettere la configurazione di crittografia hello hello **parametri** blade e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76716-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="76716-514">Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** crittografia tooenable in hello nuova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="76716-515">Hello nella tabella seguente elenca i parametri del modello di gestione risorse hello per il disco rigido virtuale crittografato:</span><span class="sxs-lookup"><span data-stu-id="76716-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="76716-516">.</span><span class="sxs-lookup"><span data-stu-id="76716-516">Parameter</span></span> | <span data-ttu-id="76716-517">Descrizione</span><span class="sxs-lookup"><span data-stu-id="76716-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="76716-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="76716-518">newStorageAccountName</span></span> | <span data-ttu-id="76716-519">Nome di hello toostore di hello storage account crittografati disco rigido virtuale del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="76716-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="76716-520">Questo account di archiviazione deve già stato creato in hello stesso gruppo di risorse e la stessa posizione come hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="76716-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="76716-521">osVhdUri</span></span> | <span data-ttu-id="76716-522">URI del disco rigido virtuale del sistema operativo di hello dall'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="76716-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="76716-523">osType</span><span class="sxs-lookup"><span data-stu-id="76716-523">osType</span></span> | <span data-ttu-id="76716-524">Tipo di prodotto del sistema operativo (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="76716-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="76716-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="76716-525">virtualNetworkName</span></span> | <span data-ttu-id="76716-526">Nome della rete virtuale che hello NIC VM hello deve appartenere allo.</span><span class="sxs-lookup"><span data-stu-id="76716-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="76716-527">Hello nome debba sono già stato creato in hello stesso gruppo di risorse e la stessa posizione come hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="76716-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="76716-528">subnetName</span></span> | <span data-ttu-id="76716-529">Nome della subnet hello nella rete virtuale che hello NIC VM hello deve appartenere allo.</span><span class="sxs-lookup"><span data-stu-id="76716-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="76716-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="76716-530">vmSize</span></span> | <span data-ttu-id="76716-531">Dimensioni della VM hello.</span><span class="sxs-lookup"><span data-stu-id="76716-531">Size of hello VM.</span></span> <span data-ttu-id="76716-532">Attualmente sono supportate solo le serie A, D e G Standard.</span><span class="sxs-lookup"><span data-stu-id="76716-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="76716-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="76716-533">keyVaultResourceID</span></span> | <span data-ttu-id="76716-534">Hello ResourceID che identifica una risorsa dell'insieme di credenziali chiave hello in Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="76716-535">È possibile ottenere tramite i cmdlet di PowerShell hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="76716-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="76716-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="76716-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="76716-537">URL della chiave di crittografia del disco hello impostato nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="76716-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="76716-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="76716-538">keyVaultKekUrl</span></span> | <span data-ttu-id="76716-539">URL della chiave di crittografia della chiave hello per crittografare una chiave di crittografia del disco hello generato.</span><span class="sxs-lookup"><span data-stu-id="76716-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="76716-540">vmName</span><span class="sxs-lookup"><span data-stu-id="76716-540">vmName</span></span> | <span data-ttu-id="76716-541">Nome di hello VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="76716-542">Usare i cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="76716-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="76716-543">È possibile abilitare crittografia del disco in disco rigido virtuale crittografato tramite i cmdlet di PowerShell hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="76716-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="76716-544">Uso dei comandi dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="76716-544">Using CLI commands</span></span>
<span data-ttu-id="76716-545">crittografia disco tooenable per questo scenario utilizzando i comandi CLI, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="76716-546">Impostare criteri di accesso per l'insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="76716-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="76716-547">Set hello **EnabledForDiskEncryption** flag:</span><span class="sxs-lookup"><span data-stu-id="76716-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="76716-548">Impostare le autorizzazioni tooAzure AD applicazione toowrite segreti tooyour chiave dell'insieme di credenziali:</span><span class="sxs-lookup"><span data-stu-id="76716-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="76716-549">crittografia tooenable in una macchina virtuale esistente o in esecuzione, tipo:</span><span class="sxs-lookup"><span data-stu-id="76716-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="76716-550">Ottenere lo stato della crittografia:</span><span class="sxs-lookup"><span data-stu-id="76716-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="76716-551">crittografia tooenable in una nuova macchina virtuale dal disco rigido virtuale crittografato, utilizzare hello seguenti parametri con hello `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="76716-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="76716-552">Abilitare la crittografia in una VM IaaS Windows esistente o in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="76716-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="76716-553">In questo scenario, è possibile abilitare la crittografia utilizzando il modello di gestione risorse di hello, i cmdlet di PowerShell o i comandi CLI.</span><span class="sxs-lookup"><span data-stu-id="76716-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="76716-554">Hello nelle sezioni seguenti illustrano in dettaglio come tooenable usando hello modello di gestione risorse e i comandi CLI.</span><span class="sxs-lookup"><span data-stu-id="76716-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="76716-555">Utilizzando il modello di gestione risorse di hello</span><span class="sxs-lookup"><span data-stu-id="76716-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="76716-556">È possibile abilitare la crittografia del disco esistente o IaaS macchine virtuali di Windows in esecuzione in Azure utilizzando hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="76716-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="76716-557">Nel modello hello avvio rapido di Azure, fare clic su **distribuire tooAzure**, immettere la configurazione di crittografia hello hello **parametri** blade e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76716-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="76716-558">Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** crittografia tooenable in hello esistente o in esecuzione VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="76716-559">Hello nella tabella seguente vengono elencati parametri di modello di gestione risorse di hello per esistente o l'esecuzione di macchine virtuali che utilizzano un ID client di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="76716-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="76716-560">.</span><span class="sxs-lookup"><span data-stu-id="76716-560">Parameter</span></span> | <span data-ttu-id="76716-561">Descrizione</span><span class="sxs-lookup"><span data-stu-id="76716-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="76716-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="76716-562">AADClientID</span></span> | <span data-ttu-id="76716-563">ID client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti toohello chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="76716-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="76716-564">AADClientSecret</span></span> | <span data-ttu-id="76716-565">Segreto client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti toohello chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="76716-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="76716-566">keyVaultName</span></span> | <span data-ttu-id="76716-567">Nome della chiave hello insieme di credenziali di tale chiave deve essere caricata a BitLocker hello.</span><span class="sxs-lookup"><span data-stu-id="76716-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="76716-568">È possibile ottenerlo utilizzando cmdlet hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="76716-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="76716-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="76716-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="76716-570">URL della chiave di crittografia della chiave hello che è usato tooencrypt hello generato chiave BitLocker.</span><span class="sxs-lookup"><span data-stu-id="76716-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="76716-571">Questo parametro è facoltativo se si seleziona **nokek** nell'elenco a discesa UseExistingKek hello.</span><span class="sxs-lookup"><span data-stu-id="76716-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="76716-572">Se si seleziona **kek** nell'elenco a discesa UseExistingKek hello, è necessario immettere hello _keyEncryptionKeyURL_ valore.</span><span class="sxs-lookup"><span data-stu-id="76716-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="76716-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="76716-573">volumeType</span></span> | <span data-ttu-id="76716-574">Tipo di volume viene eseguita l'operazione di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="76716-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="76716-575">I valori validi sono _OS_, _Data_ e _All_.</span><span class="sxs-lookup"><span data-stu-id="76716-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="76716-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="76716-576">sequenceVersion</span></span> | <span data-ttu-id="76716-577">Versione di sequenza di hello operazione BitLocker.</span><span class="sxs-lookup"><span data-stu-id="76716-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="76716-578">Questo numero di versione incrementato ogni volta che viene eseguita un'operazione di crittografia del disco su hello stessa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="76716-579">vmName</span><span class="sxs-lookup"><span data-stu-id="76716-579">vmName</span></span> | <span data-ttu-id="76716-580">Nome della macchina virtuale che hello l'operazione di crittografia hello è toobe eseguiti.</span><span class="sxs-lookup"><span data-stu-id="76716-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="76716-581">_KeyEncryptionKeyURL_ è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="76716-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="76716-582">È possibile portare la propria KEK toofurther salvaguardia hello dati chiave di crittografia (segreti di crittografia di BitLocker) nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="76716-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="76716-583">Usare i cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="76716-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="76716-584">Per informazioni sull'abilitazione della crittografia con la crittografia del disco di Azure tramite i cmdlet di PowerShell, vedere il post di blog di hello [esplorare di crittografia del disco di Azure con Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [esplorare crittografia del disco di Azure con Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="76716-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="76716-585">Uso dei comandi dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="76716-585">Using CLI commands</span></span>
<span data-ttu-id="76716-586">crittografia tooenable in esistente o in esecuzione Windows IaaS con macchina virtuale in Azure mediante i comandi CLI, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="76716-587">criteri di accesso tooset nell'insieme di credenziali chiave hello:</span><span class="sxs-lookup"><span data-stu-id="76716-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="76716-588">Set hello **EnabledForDiskEncryption** flag:</span><span class="sxs-lookup"><span data-stu-id="76716-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="76716-589">Impostare le autorizzazioni tooAzure AD applicazione toowrite segreti tooyour chiave dell'insieme di credenziali:</span><span class="sxs-lookup"><span data-stu-id="76716-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="76716-590">crittografia tooenable in una macchina virtuale esistente o in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="76716-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="76716-591">stato di crittografia tooget:</span><span class="sxs-lookup"><span data-stu-id="76716-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="76716-592">crittografia tooenable in una nuova macchina virtuale dal disco rigido virtuale crittografato, utilizzare hello seguenti parametri con hello `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="76716-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="76716-593">Abilitare la crittografia in una VM IaaS Linux esistente o in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="76716-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="76716-594">È possibile abilitare la crittografia del disco in una VM Linux IaaS esistenti o è in esecuzione in Azure utilizzando hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="76716-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="76716-595">Fare clic su **distribuire tooAzure** sul modello hello avvio rapido di Azure, immettere la configurazione di crittografia hello hello **parametri** blade e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76716-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="76716-596">Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** crittografia tooenable in hello esistente o in esecuzione VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="76716-597">Hello nella tabella seguente elenca i parametri di modello di gestione risorse per esistente o in esecuzione macchine virtuali che utilizzano un ID client di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="76716-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="76716-598">.</span><span class="sxs-lookup"><span data-stu-id="76716-598">Parameter</span></span> | <span data-ttu-id="76716-599">Descrizione</span><span class="sxs-lookup"><span data-stu-id="76716-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="76716-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="76716-600">AADClientID</span></span> | <span data-ttu-id="76716-601">ID client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti toohello chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="76716-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="76716-602">AADClientSecret</span></span> | <span data-ttu-id="76716-603">Segreto client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti tooyour chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="76716-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="76716-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="76716-604">keyVaultName</span></span> | <span data-ttu-id="76716-605">Nome della chiave hello insieme di credenziali di tale chiave deve essere caricata a BitLocker hello.</span><span class="sxs-lookup"><span data-stu-id="76716-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="76716-606">È possibile ottenerlo utilizzando cmdlet hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="76716-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="76716-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="76716-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="76716-608">URL della chiave di crittografia della chiave hello che è usato tooencrypt hello generato chiave BitLocker.</span><span class="sxs-lookup"><span data-stu-id="76716-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="76716-609">Questo parametro è facoltativo se si seleziona **nokek** nell'elenco a discesa UseExistingKek hello.</span><span class="sxs-lookup"><span data-stu-id="76716-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="76716-610">Se si seleziona **kek** nell'elenco a discesa UseExistingKek hello, è necessario immettere hello _keyEncryptionKeyURL_ valore.</span><span class="sxs-lookup"><span data-stu-id="76716-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="76716-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="76716-611">volumeType</span></span> | <span data-ttu-id="76716-612">Tipo di volume viene eseguita l'operazione di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="76716-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="76716-613">I valori supportati validi sono _OS_ o _All_ (per RHEL 7.2, CentOS 7.2 e Ubuntu 16.04) e _Data_ (per tutte le altre distribuzioni).</span><span class="sxs-lookup"><span data-stu-id="76716-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="76716-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="76716-614">sequenceVersion</span></span> | <span data-ttu-id="76716-615">Versione di sequenza di hello operazione BitLocker.</span><span class="sxs-lookup"><span data-stu-id="76716-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="76716-616">Questo numero di versione incrementato ogni volta che viene eseguita un'operazione di crittografia del disco su hello stessa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="76716-617">vmName</span><span class="sxs-lookup"><span data-stu-id="76716-617">vmName</span></span> | <span data-ttu-id="76716-618">Nome della macchina virtuale che hello l'operazione di crittografia hello è toobe eseguiti.</span><span class="sxs-lookup"><span data-stu-id="76716-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="76716-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="76716-619">passPhrase</span></span> | <span data-ttu-id="76716-620">Digitare una passphrase sicura come chiave di crittografia dati hello.</span><span class="sxs-lookup"><span data-stu-id="76716-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="76716-621">_KeyEncryptionKeyURL_ è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="76716-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="76716-622">È possibile portare la propria KEK toofurther salvaguardia hello dati chiave di crittografia (passphrase segreto) nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="76716-623">Comandi dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="76716-623">CLI commands</span></span>
<span data-ttu-id="76716-624">È possibile abilitare crittografia del disco in disco rigido virtuale crittografato mediante installazione e utilizzo hello [comando CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="76716-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="76716-625">crittografia tooenable in esistente o macchine virtuali Linux IaaS in esecuzione in Azure utilizzando i comandi CLI, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="76716-626">Impostare i criteri di accesso nell'insieme di credenziali chiave hello:</span><span class="sxs-lookup"><span data-stu-id="76716-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="76716-627">Set hello **EnabledForDiskEncryption** flag:</span><span class="sxs-lookup"><span data-stu-id="76716-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="76716-628">Impostare le autorizzazioni tooAzure AD applicazione toowrite segreti tooyour chiave dell'insieme di credenziali:</span><span class="sxs-lookup"><span data-stu-id="76716-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="76716-629">crittografia tooenable in una macchina virtuale esistente o in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="76716-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="76716-630">Ottenere lo stato della crittografia:</span><span class="sxs-lookup"><span data-stu-id="76716-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="76716-631">crittografia tooenable in una nuova macchina virtuale dal disco rigido virtuale crittografato, utilizzare hello seguenti parametri con hello `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="76716-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="76716-632">Ottenere lo stato di crittografia hello di una VM IaaS crittografati</span><span class="sxs-lookup"><span data-stu-id="76716-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="76716-633">È possibile ottenere lo stato di crittografia hello usando Gestione risorse di Azure, [i cmdlet di PowerShell](/powershell/azure/overview), o i comandi CLI.</span><span class="sxs-lookup"><span data-stu-id="76716-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="76716-634">Hello le sezioni seguenti illustrano come toouse hello portale di Azure classico e tooget comandi CLI hello lo stato di crittografia.</span><span class="sxs-lookup"><span data-stu-id="76716-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="76716-635">Ottenere lo stato di crittografia hello di una macchina virtuale di Windows crittografato tramite Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="76716-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="76716-636">È possibile ottenere lo stato di crittografia hello di hello VM IaaS da Gestione risorse di Azure eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="76716-637">Accedi toohello [portale di Azure classico](https://portal.azure.com/), quindi fare clic su **macchine virtuali** nel riquadro sinistro di hello toosee una visualizzazione di riepilogo delle macchine virtuali hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="76716-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="76716-638">È possibile filtrare una visualizzazione di macchine virtuali hello selezionando il nome della sottoscrizione hello in hello **sottoscrizione** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="76716-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="76716-639">Nella parte superiore di hello di hello **macchine virtuali** pagina, fare clic su **colonne**.</span><span class="sxs-lookup"><span data-stu-id="76716-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="76716-640">In hello **scegliere colonna** pannello seleziona **crittografia del disco**e quindi fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="76716-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="76716-641">Verrà visualizzato lo stato di crittografia hello che mostra colonna crittografia disco hello _abilitato_ o _non abilitato_ per ogni macchina virtuale, come illustrato nella seguente illustrazione hello:</span><span class="sxs-lookup"><span data-stu-id="76716-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="76716-643">Ottenere lo stato di crittografia hello di una VM di IaaS (Windows/Linux) crittografata tramite cmdlet di PowerShell hello crittografia disco</span><span class="sxs-lookup"><span data-stu-id="76716-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="76716-644">È possibile ottenere lo stato di crittografia hello di hello VM IaaS dal cmdlet PowerShell di crittografia del disco hello `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="76716-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="76716-645">le impostazioni di crittografia hello tooget per la macchina virtuale, immettere il seguente di hello:</span><span class="sxs-lookup"><span data-stu-id="76716-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="76716-646">È possibile esaminare l'output di hello di _Get AzureRmVMDiskEncryptionStatus_ per la crittografia della chiave URL.</span><span class="sxs-lookup"><span data-stu-id="76716-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

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

<span data-ttu-id="76716-647">Hello OSVolumeEncrypted e i valori delle impostazioni DataVolumesEncrypted vengono impostati too_Encrypted_, indicante che entrambi i volumi sono crittografati tramite crittografia di disco di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="76716-648">Per informazioni sull'abilitazione della crittografia con la crittografia del disco di Azure tramite i cmdlet di PowerShell, vedere il post di blog di hello [esplorare di crittografia del disco di Azure con Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [esplorare crittografia del disco di Azure con Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="76716-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="76716-649">Nelle macchine virtuali Linux, sono necessari tre minuti di toofour per hello `Get-AzureRmVMDiskEncryptionStatus` lo stato di crittografia di cmdlet tooreport hello.</span><span class="sxs-lookup"><span data-stu-id="76716-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="76716-650">Ottenere lo stato di crittografia hello di hello VM IaaS dal comando CLI di hello crittografia disco</span><span class="sxs-lookup"><span data-stu-id="76716-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="76716-651">È possibile ottenere lo stato di crittografia hello di hello VM IaaS tramite comando CLI di crittografia del disco hello `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="76716-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="76716-652">le impostazioni di crittografia hello tooget per la macchina virtuale, immettere la sessione CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="76716-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="76716-653">Disabilitare la crittografia nelle VM IaaS Windows in esecuzione</span><span class="sxs-lookup"><span data-stu-id="76716-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="76716-654">È possibile disabilitare la crittografia in un'esecuzione di Windows o Linux IaaS con macchina virtuale tramite il modello di gestione risorse di Azure disco crittografia hello o i cmdlet di PowerShell e specificare la configurazione di decrittografia hello.</span><span class="sxs-lookup"><span data-stu-id="76716-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="76716-655">Macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="76716-655">Windows VM</span></span>
<span data-ttu-id="76716-656">passaggio di disabilitare la crittografia Hello disabilita la crittografia di hello del sistema operativo, il volume di dati hello o entrambi in esecuzione la macchina virtuale IaaS Windows hello.</span><span class="sxs-lookup"><span data-stu-id="76716-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="76716-657">Non è possibile disabilitare il volume del sistema operativo hello e lasciare il volume di dati hello crittografato.</span><span class="sxs-lookup"><span data-stu-id="76716-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="76716-658">Quando viene eseguito il passaggio di disabilitare la crittografia hello, modello di distribuzione classica Azure hello Aggiorna modello del servizio VM hello e hello Windows IaaS con macchina virtuale è contrassegnato decrittografata.</span><span class="sxs-lookup"><span data-stu-id="76716-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="76716-659">contenuto Hello di hello VM non venga crittografati a riposo.</span><span class="sxs-lookup"><span data-stu-id="76716-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="76716-660">la decrittografia di Hello non elimina il materiale della chiave dell'insieme di credenziali e hello crittografia chiave (chiavi di crittografia di BitLocker per Windows e la Passphrase per Linux).</span><span class="sxs-lookup"><span data-stu-id="76716-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="76716-661">VM Linux</span><span class="sxs-lookup"><span data-stu-id="76716-661">Linux VM</span></span>
<span data-ttu-id="76716-662">passaggio di disabilitare la crittografia Hello disabilita la crittografia dei volumi di dati hello hello in esecuzione Linux IaaS con macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="76716-663">Questo passaggio funziona solo se il disco del sistema operativo hello non è crittografato.</span><span class="sxs-lookup"><span data-stu-id="76716-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-664">La disabilitazione della crittografia nel disco del sistema operativo hello non è consentita nelle macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="76716-665">Disabilitare la crittografia in una macchina virtuale IaaS esistente o in esecuzione</span><span class="sxs-lookup"><span data-stu-id="76716-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="76716-666">È possibile disabilitare la crittografia del disco durante l'esecuzione di macchine virtuali IaaS di Windows tramite hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="76716-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="76716-667">Nel modello hello avvio rapido di Azure, fare clic su **distribuire tooAzure**, immettere configurazione decrittografia hello hello **parametri** blade e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76716-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="76716-668">Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** tooenable crittografia in una nuova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="76716-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="76716-669">Per le macchine virtuali Linux, è possibile disabilitare la crittografia tramite hello [disabilitare la crittografia in una VM Linux in esecuzione](https://aka.ms/decrypt-linuxvm) modello.</span><span class="sxs-lookup"><span data-stu-id="76716-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="76716-670">Hello nella tabella seguente sono elencati i parametri di modello di gestione delle risorse per la disabilitazione della crittografia in una VM IaaS in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="76716-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="76716-671">.</span><span class="sxs-lookup"><span data-stu-id="76716-671">Parameter</span></span> | <span data-ttu-id="76716-672">Descrizione</span><span class="sxs-lookup"><span data-stu-id="76716-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="76716-673">vmName</span><span class="sxs-lookup"><span data-stu-id="76716-673">vmName</span></span> | <span data-ttu-id="76716-674">Nome della macchina virtuale che hello l'operazione di crittografia hello è toobe eseguiti.</span><span class="sxs-lookup"><span data-stu-id="76716-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="76716-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="76716-675">volumeType</span></span> | <span data-ttu-id="76716-676">Tipo del volume in cui viene eseguita l'operazione di decrittografia.</span><span class="sxs-lookup"><span data-stu-id="76716-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="76716-677">I valori validi sono _OS_, _Data_ e _All_.</span><span class="sxs-lookup"><span data-stu-id="76716-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="76716-678">Non è possibile disabilitare la crittografia durante l'esecuzione di volume di avvio o del sistema operativo Windows IaaS con macchina virtuale senza la disabilitazione della crittografia in hello _dati_ volume.</span><span class="sxs-lookup"><span data-stu-id="76716-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="76716-679">Si noti inoltre che la disabilitazione della crittografia nel disco del sistema operativo hello non è consentita nelle macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="76716-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="76716-680">sequenceVersion</span></span> | <span data-ttu-id="76716-681">Versione di sequenza di hello operazione BitLocker.</span><span class="sxs-lookup"><span data-stu-id="76716-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="76716-682">Questo numero di versione incrementato ogni volta che viene eseguita un'operazione di decrittografia del disco su hello stessa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="76716-683">Disabilitare la crittografia in una macchina virtuale IaaS esistente o in esecuzione</span><span class="sxs-lookup"><span data-stu-id="76716-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="76716-684">crittografia toodisable in una VM IaaS esistenti o è in esecuzione tramite i cmdlet di PowerShell hello, vedere [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="76716-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="76716-685">Questo cmdlet supporta sia le VM Windows che le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="76716-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="76716-686">crittografia toodisable, installa un'estensione nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="76716-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="76716-687">Se hello _nome_ parametro non viene specificato, un'estensione con il nome predefinito hello _AzureDiskEncryption per le macchine virtuali Windows_ viene creato.</span><span class="sxs-lookup"><span data-stu-id="76716-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="76716-688">Nelle macchine virtuali Linux, hello AzureDiskEncryptionForLinux estensione viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="76716-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="76716-689">Questo cmdlet riavvia una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="76716-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="76716-690">Abilitare la crittografia su macchina virtuale IaaS pre-crittografata con disco gestito Azure</span><span class="sxs-lookup"><span data-stu-id="76716-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="76716-691">Utilizzare hello Azure gestito disco ARM modello toocreate una macchina virtuale crittografata da un disco rigido virtuale pre-crittografato utilizzando hello ARM modello si trova in</span><span class="sxs-lookup"><span data-stu-id="76716-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="76716-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="76716-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="76716-693">Abilitare la crittografia su una nuova macchina virtuale IaaS Linux con disco gestito Azure</span><span class="sxs-lookup"><span data-stu-id="76716-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="76716-694">Utilizzare hello Azure gestito disco ARM modello toocreate in che un nuovo crittografato Linux IaaS con macchina virtuale utilizzando il modello ARM hello</span><span class="sxs-lookup"><span data-stu-id="76716-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="76716-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="76716-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="76716-696">Abilitare la crittografia su una nuova macchina virtuale IaaS Windows con disco gestito Azure</span><span class="sxs-lookup"><span data-stu-id="76716-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="76716-697">Utilizzare hello Azure gestito disco ARM modello toocreate in che un nuovo crittografato Linux IaaS con macchina virtuale utilizzando il modello ARM hello</span><span class="sxs-lookup"><span data-stu-id="76716-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="76716-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="76716-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="76716-699">È obbligatorio toosnapshot e/o di backup un disco gestito basato all'esterno dell'istanza della macchina virtuale e precedenti tooenabling crittografia del disco di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="76716-700">Uno snapshot del disco gestito hello può essere prelevato portale hello o Backup di Azure può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="76716-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="76716-701">Backup di verificare che un'opzione di ripristino è possibile nel caso di hello di qualsiasi errore imprevisto durante la crittografia.</span><span class="sxs-lookup"><span data-stu-id="76716-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="76716-702">Una volta che viene eseguito un backup, il cmdlet Set-AzureRmVMDiskEncryptionExtension hello può essere utilizzato tooencrypt gestiti dischi specificando il parametro - skipVmBackup hello.</span><span class="sxs-lookup"><span data-stu-id="76716-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="76716-703">Questo comando ha esito negativo su una macchina virtuale basata su un disco gestito finché non viene eseguito un backup e non viene specificato il parametro.</span><span class="sxs-lookup"><span data-stu-id="76716-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="76716-704">Aggiornare le impostazioni di crittografia di una macchina virtuale non Premium crittografata esistente</span><span class="sxs-lookup"><span data-stu-id="76716-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="76716-705">Utilizzare hello Azure disco crittografia supportata interfacce esistenti per l'esecuzione di macchine Virtuali [cmdlet di Powershell, i modelli di CLI o ARM] tooupdate le impostazioni di crittografia hello come client AAD ID/chiave privata, chiave di crittografia [KEK], chiave di crittografia di BitLocker per la macchina virtuale di Windows o la Passphrase per Impostazione di crittografia ECC VM Linux hello aggiornamento è supportato solo per le macchine virtuali supportate dall'archiviazione non premium.</span><span class="sxs-lookup"><span data-stu-id="76716-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="76716-706">NON è supportata per le macchine virtuali dotate di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="76716-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="76716-707">Appendice</span><span class="sxs-lookup"><span data-stu-id="76716-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="76716-708">Connettere tooyour sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="76716-708">Connect tooyour subscription</span></span>
<span data-ttu-id="76716-709">Prima di procedere, rivedere hello *prerequisiti* sezione in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="76716-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="76716-710">Dopo avere verificato che tutti i prerequisiti siano stati soddisfatti, connettere tooyour sottoscrizione effettuando hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="76716-711">Avviare una sessione di Azure PowerShell e accedere con il comando seguente hello tooyour account Azure:</span><span class="sxs-lookup"><span data-stu-id="76716-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="76716-712">Se si dispone di più sottoscrizioni e si desidera uno toouse toospecify, digitare hello sottoscrizioni hello toosee per l'account di seguito:</span><span class="sxs-lookup"><span data-stu-id="76716-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="76716-713">sottoscrizione di hello toospecify da toouse, tipo:</span><span class="sxs-lookup"><span data-stu-id="76716-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="76716-714">tooverify che sottoscrizione hello configurata sia corretto, digitare:</span><span class="sxs-lookup"><span data-stu-id="76716-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="76716-715">tooconfirm hello Azure crittografia del disco sono installati i cmdlet, tipo:</span><span class="sxs-lookup"><span data-stu-id="76716-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="76716-716">Dopo l'output di Hello conferma installazione crittografia disco di Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="76716-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="76716-717">Preparare un disco rigido virtuale Windows pre-crittografato</span><span class="sxs-lookup"><span data-stu-id="76716-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="76716-718">Nelle sezioni Hello che seguono sono tooprepare necessario un disco rigido virtuale di Windows pre-crittografato per la distribuzione come un disco rigido virtuale crittografata in IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="76716-719">Utilizzare tooprepare informazioni hello e avviare un nuovo Windows macchina virtuale (VHD) in Azure Site Recovery o Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="76716-720">Aggiornamento gruppo criteri tooallow senza TPM per la protezione del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="76716-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="76716-721">Configurare l'impostazione di criteri di gruppo per BitLocker hello **crittografia unità BitLocker**, che si trova in **criteri del Computer locale** > **configurazione Computer**  >  **Modelli amministrativi** > **componenti di Windows**.</span><span class="sxs-lookup"><span data-stu-id="76716-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="76716-722">Modificare questa impostazione troppo**unità del sistema operativo** > **Richiedi autenticazione aggiuntiva all'avvio** > **Consenti BitLocker senza un TPM compatibile**, come illustrato nella seguente illustrazione hello:</span><span class="sxs-lookup"><span data-stu-id="76716-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="76716-724">Installare i componenti della funzionalità BitLocker</span><span class="sxs-lookup"><span data-stu-id="76716-724">Install BitLocker feature components</span></span>
<span data-ttu-id="76716-725">Per Windows Server 2012 e versioni successive, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="76716-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="76716-726">Per Windows Server 2008 R2, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="76716-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="76716-727">Preparare il volume del sistema operativo hello per BitLocker utilizzando`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="76716-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="76716-728">toocompress hello partizione del sistema operativo e preparare hello macchina per BitLocker, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="76716-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="76716-729">Proteggere il volume di sistema operativo hello mediante BitLocker</span><span class="sxs-lookup"><span data-stu-id="76716-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="76716-730">Hello utilizzare [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) crittografia tooenable comando nel volume di avvio hello utilizzando una protezione con chiave esterna.</span><span class="sxs-lookup"><span data-stu-id="76716-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="76716-731">Nel volume o unità esterne hello inoltre inserire la chiave esterna hello (.bek file).</span><span class="sxs-lookup"><span data-stu-id="76716-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="76716-732">La crittografia è abilitata nel volume di sistema/avvio hello dopo il riavvio di hello.</span><span class="sxs-lookup"><span data-stu-id="76716-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="76716-733">Preparare hello macchina virtuale con una data/risorsa distinta disco rigido virtuale per ottenere la chiave esterna di hello mediante BitLocker.</span><span class="sxs-lookup"><span data-stu-id="76716-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="76716-734">Crittografia di un'unità del sistema operativo in una VM Linux in esecuzione</span><span class="sxs-lookup"><span data-stu-id="76716-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="76716-735">Crittografia di un'unità del sistema operativo in una VM Linux in esecuzione è supportata in hello seguenti distribuzioni:</span><span class="sxs-lookup"><span data-stu-id="76716-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="76716-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="76716-736">RHEL 7.2</span></span>
* <span data-ttu-id="76716-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="76716-737">CentOS 7.2</span></span>
* <span data-ttu-id="76716-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="76716-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="76716-739">Prerequisiti per la crittografia del disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="76716-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="76716-740">dall'immagine del Marketplace hello in Gestione risorse di Azure, è necessario creare Hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="76716-741">VM di Azure con almeno 4 GB di RAM (7 GB consigliati).</span><span class="sxs-lookup"><span data-stu-id="76716-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="76716-742">(Per RHEL e CentOS) Disabilitare SELinux.</span><span class="sxs-lookup"><span data-stu-id="76716-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="76716-743">toodisable SELinux, vedere "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="76716-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="76716-744">La disabilitazione di SELinux"in hello [Guida dell'amministratore e dell'utente di SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="76716-745">Dopo aver disabilitato SELinux, riavviare almeno una volta hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="76716-746">Passi</span><span class="sxs-lookup"><span data-stu-id="76716-746">Steps</span></span>
1. <span data-ttu-id="76716-747">Creare una macchina virtuale utilizzando una delle distribuzioni di hello specificate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="76716-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="76716-748">Per CentOS 7.2, la crittografia del disco del sistema operativo è supportata tramite un'immagine speciale.</span><span class="sxs-lookup"><span data-stu-id="76716-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="76716-749">toouse questa immagine, specificare "7.2n" come hello SKU quando si crea hello VM:</span><span class="sxs-lookup"><span data-stu-id="76716-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="76716-750">Configurare secondo tooyour esigenze di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="76716-751">Se si intende tooencrypt tutte le unità hello (sistema operativo + dati), unità dati hello necessario toobe montabile da /etc/fstab. e specificati.</span><span class="sxs-lookup"><span data-stu-id="76716-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="76716-752">Utilizzare UUID =... toospecify unità di dati in fstab/e così via, anziché specificare nome del dispositivo hello blocco (ad esempio, /dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="76716-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="76716-753">Durante la crittografia, hello ordine delle modifiche di unità nel hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="76716-754">Se la macchina virtuale si basa su un ordine specifico di bloccare i dispositivi, ne verrà eseguito toomount dopo averle crittografia.</span><span class="sxs-lookup"><span data-stu-id="76716-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="76716-755">Disconnessione da sessioni SSH hello.</span><span class="sxs-lookup"><span data-stu-id="76716-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="76716-756">tooencrypt hello del sistema operativo, specificare volumeType come **tutti** o **OS** quando si [abilitare la crittografia](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="76716-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="76716-757">Tutti i processi dello spazio dell'utente non in esecuzione come servizi `systemd` devono essere terminati con `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="76716-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="76716-758">Riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-758">Reboot hello VM.</span></span> <span data-ttu-id="76716-759">Quando si abilita la crittografia del disco del sistema operativo in una macchina virtuale in esecuzione, pianificare i tempi di inattività della VM.</span><span class="sxs-lookup"><span data-stu-id="76716-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="76716-760">Monitorare periodicamente lo stato di avanzamento hello di crittografia utilizzando istruzioni hello in hello [nella sezione successiva](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="76716-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="76716-761">Dopo Get AzureRmVmDiskEncryptionStatus mostrato "VMRestartPending", riavviare la macchina virtuale tramite l'accesso tooit o tramite il portale di hello, PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="76716-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="76716-762">Prima di riavviare, si consiglia di salvare [diagnostica di avvio](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="76716-763">Monitoraggio dello stato della crittografia del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="76716-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="76716-764">Esistono tre modi per monitorare lo stato della crittografia del sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="76716-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="76716-765">Hello utilizzare `Get-AzureRmVmDiskEncryptionStatus` cmdlet ed esaminare il campo di ProgressMessage hello:</span><span class="sxs-lookup"><span data-stu-id="76716-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="76716-766">Raggiunge hello VM "Crittografia avviata del disco del sistema operativo", accetta di circa 40 minuti too50 su un'archiviazione Premium sottoposti a macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="76716-767">A causa dell'[errore #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` e `DataVolumesEncrypted`vengono visualizzati come `Unknown` in alcune distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="76716-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="76716-768">Con WALinuxAgent 2.1.5 e versioni successive questo errore viene risolto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="76716-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="76716-769">Se viene visualizzato `Unknown` nell'output di hello, è possibile verificare lo stato di crittografia del disco tramite hello Esplora inventario risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="76716-770">Andare troppo[Esplora inventario risorse di Azure](https://resources.azure.com/), quindi espandere questa gerarchia nel Pannello di selezione hello a sinistra:</span><span class="sxs-lookup"><span data-stu-id="76716-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

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

 <span data-ttu-id="76716-771">In hello InstanceView, scorrere verso il basso lo stato di crittografia hello toosee delle unità.</span><span class="sxs-lookup"><span data-stu-id="76716-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![Visualizzazione dell'istanza della VM](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="76716-773">Esaminare la [diagnostica di avvio](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="76716-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="76716-774">I messaggi da hello estensione ADE devono essere preceduti dalla `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="76716-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="76716-775">Accedi toohello VM tramite SSH e ottenere log di estensione hello da:</span><span class="sxs-lookup"><span data-stu-id="76716-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="76716-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="76716-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="76716-777">Si consiglia di non accedere toohello VM mentre la crittografia del sistema operativo è in corso.</span><span class="sxs-lookup"><span data-stu-id="76716-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="76716-778">Copiare i registri di hello solo quando hello altri due metodi hanno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="76716-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="76716-779">Preparare un disco rigido virtuale Linux pre-crittografato</span><span class="sxs-lookup"><span data-stu-id="76716-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="76716-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="76716-780">Ubuntu 16</span></span>
<span data-ttu-id="76716-781">Configurare la crittografia durante l'installazione di distribuzione hello eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="76716-782">Selezionare **configurare volumi crittografati** quando si creano partizioni dischi hello.</span><span class="sxs-lookup"><span data-stu-id="76716-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="76716-784">Creare un'unità di avvio separata che non deve essere crittografata.</span><span class="sxs-lookup"><span data-stu-id="76716-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="76716-785">Crittografare l'unità radice.</span><span class="sxs-lookup"><span data-stu-id="76716-785">Encrypt your root drive.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="76716-787">Specificare una passphrase.</span><span class="sxs-lookup"><span data-stu-id="76716-787">Provide a passphrase.</span></span> <span data-ttu-id="76716-788">Si tratta di passphrase hello caricare toohello insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="76716-790">Terminare il partizionamento.</span><span class="sxs-lookup"><span data-stu-id="76716-790">Finish partitioning.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="76716-792">Quando si avvia VM hello e una passphrase viene richiesto, utilizzare hello passphrase fornita nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="76716-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="76716-794">Preparare hello VM per il caricamento in Azure utilizzando [queste istruzioni](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="76716-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="76716-795">Non eseguire ancora ultimo passaggio di hello (Buongiorno deprovisioning VM).</span><span class="sxs-lookup"><span data-stu-id="76716-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="76716-796">Configurare crittografia toowork con Azure eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="76716-797">Creare un file in /usr/local/sbin/azure_crypt_key.sh, con contenuto hello in hello lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="76716-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="76716-798">Prestare attenzione toohello KeyFileName, perché è un nome di file passphrase hello usato da Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="76716-799">Modifica configurazione crypt hello in */e così via/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="76716-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="76716-800">L'aspetto dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="76716-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="76716-801">Se si sta modificando *azure_crypt_key.sh* in Windows ed è stato copiato tooLinux, eseguire `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="76716-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="76716-802">Aggiungere script toohello delle autorizzazioni di esecuzione:</span><span class="sxs-lookup"><span data-stu-id="76716-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="76716-803">Modificare */etc/initramfs-tools/modules* accodando le righe:</span><span class="sxs-lookup"><span data-stu-id="76716-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="76716-804">Eseguire `update-initramfs -u -k all` tooupdate prova initramfs toomake prova `keyscript` effettive.</span><span class="sxs-lookup"><span data-stu-id="76716-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="76716-805">È ora possibile eseguire il deprovisioning hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-805">Now you can deprovision hello VM.</span></span>

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="76716-807">Passaggio successivo toohello continuare e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="76716-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="76716-808">openSUSE 13.2</span></span>
<span data-ttu-id="76716-809">crittografia tooconfigure durante l'installazione di distribuzione hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="76716-810">Quando si partiziona dischi hello, selezionare **gruppo di volumi crittografare**e quindi immettere una password.</span><span class="sxs-lookup"><span data-stu-id="76716-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="76716-811">Si tratta hello password che verrà caricato tooyour insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![Configurazione di openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="76716-813">Avvio hello VM utilizzando la password.</span><span class="sxs-lookup"><span data-stu-id="76716-813">Boot hello VM using your password.</span></span>

 ![Configurazione di openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="76716-815">Preparazione hello VM per il caricamento tooAzure seguendo le istruzioni hello [preparare una macchina virtuale SLES o openSUSE per Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="76716-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="76716-816">Non eseguire ancora ultimo passaggio di hello (Buongiorno deprovisioning VM).</span><span class="sxs-lookup"><span data-stu-id="76716-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="76716-817">tooconfigure crittografia toowork con Azure, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="76716-818">Modificare /etc/dracut.conf hello e aggiungere hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="76716-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="76716-819">Impostare come commento le righe dall'entità finale hello hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="76716-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="76716-820">Aggiungere hello seguente riga all'inizio di hello di /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh file hello:</span><span class="sxs-lookup"><span data-stu-id="76716-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="76716-821">Modificare quindi tutte le occorrenze di:</span><span class="sxs-lookup"><span data-stu-id="76716-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="76716-822">in:</span><span class="sxs-lookup"><span data-stu-id="76716-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="76716-823">Modifica /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e aggiungerlo troppo "dispositivo aprire LUKS #":</span><span class="sxs-lookup"><span data-stu-id="76716-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="76716-824">Eseguire `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="76716-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="76716-825">Ora è possibile eseguire il deprovisioning hello VM e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="76716-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="76716-826">CentOS 7</span></span>
<span data-ttu-id="76716-827">crittografia tooconfigure durante l'installazione di distribuzione hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="76716-828">Selezionare **Encrypt my data** (Crittografa dati personali) durante il partizionamento dei dischi.</span><span class="sxs-lookup"><span data-stu-id="76716-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="76716-830">Assicurarsi **Encrypt** (Crittografa) sia selezionato per la partizione radice.</span><span class="sxs-lookup"><span data-stu-id="76716-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="76716-832">Specificare una passphrase.</span><span class="sxs-lookup"><span data-stu-id="76716-832">Provide a passphrase.</span></span> <span data-ttu-id="76716-833">Si tratta di hello passphrase che verrà caricato tooyour insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="76716-835">Quando si avvia VM hello e una passphrase viene richiesto, utilizzare hello passphrase fornita nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="76716-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="76716-837">Hello preparare la macchina virtuale per il caricamento in Azure utilizzando istruzioni "CentOS 7.0 +" hello [preparare una macchina virtuale basata su CentOS per Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="76716-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="76716-838">Non eseguire ancora ultimo passaggio di hello (Buongiorno deprovisioning VM).</span><span class="sxs-lookup"><span data-stu-id="76716-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="76716-839">Ora è possibile eseguire il deprovisioning hello VM e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="76716-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="76716-840">tooconfigure crittografia toowork con Azure, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76716-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="76716-841">Modificare /etc/dracut.conf hello e aggiungere hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="76716-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="76716-842">Impostare come commento le righe dall'entità finale hello hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="76716-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="76716-843">Aggiungere hello seguente riga all'inizio di hello di /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh file hello:</span><span class="sxs-lookup"><span data-stu-id="76716-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="76716-844">Modificare quindi tutte le occorrenze di:</span><span class="sxs-lookup"><span data-stu-id="76716-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="76716-845">to</span><span class="sxs-lookup"><span data-stu-id="76716-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="76716-846">Modificare /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e aggiungere questo dopo hello "dispositivo aprire LUKS #":</span><span class="sxs-lookup"><span data-stu-id="76716-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="76716-847">Eseguire hello "usr/servizio/dracut / -f - v" tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="76716-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="76716-849">Caricare crittografati VHD tooan account di archiviazione Azure</span><span class="sxs-lookup"><span data-stu-id="76716-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="76716-850">Dopo aver abilitato la crittografia BitLocker o DM Crypt, hello locale crittografato account di archiviazione tooyour toobe caricato esigenze disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="76716-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="76716-851">Carica una chiave privata di crittografia del disco hello per hello pre-crittografato VM tooyour chiave dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="76716-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="76716-852">chiave privata di crittografia del disco Hello ottenuto in precedenza deve essere caricato come un segreto nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="76716-853">insieme di credenziali chiave Hello necessita di crittografia del disco toohave e autorizzazioni abilitate per il client di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76716-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="76716-854">Segreto di crittografia del disco non crittografato con una chiave di crittografia della chiave</span><span class="sxs-lookup"><span data-stu-id="76716-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="76716-855">tooset backup segreto hello nell'insieme di credenziali chiave, utilizzare [Set AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="76716-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="76716-856">Se si dispone di una macchina virtuale di Windows, file bek hello viene codificato come stringa base64 e quindi caricato tooyour insieme di credenziali chiave usando hello `Set-AzureKeyVaultSecret` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76716-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="76716-857">Per Linux, hello passphrase viene codificata come stringa base64 e quindi caricato toohello insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="76716-858">Inoltre, assicurarsi che tale hello tag seguenti vengono impostate quando si crea il segreto hello nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="76716-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="76716-859">Hello utilizzare `$secretUrl` nel passaggio successivo di hello per [collegamento del disco del sistema operativo hello senza utilizzare KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="76716-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="76716-860">Segreto di crittografia del disco crittografato con una chiave di crittografia della chiave</span><span class="sxs-lookup"><span data-stu-id="76716-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="76716-861">Prima di caricare l'insieme di credenziali chiave segreta toohello hello, è possibile crittografare facoltativamente, usando una chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="76716-862">Incapsulamento hello utilizzare [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst crittografare segreto hello utilizzando hello chiave di crittografia della chiave.</span><span class="sxs-lookup"><span data-stu-id="76716-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="76716-863">output di questa operazione wrap Hello è una stringa di URL con codificata base64, che è quindi possibile caricare come segreto tramite hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76716-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
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

<span data-ttu-id="76716-864">Utilizzare `$KeyEncryptionKey` e `$secretUrl` nel passaggio successivo di hello per [collegamento del disco del sistema operativo hello utilizzando KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="76716-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="76716-865">Specificare un URL del segreto quando si collega un disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="76716-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="76716-866">Senza l'uso di una chiave di crittografia della chiave (KEK)</span><span class="sxs-lookup"><span data-stu-id="76716-866">Without using a KEK</span></span>
<span data-ttu-id="76716-867">Mentre si collega disco hello del sistema operativo, è necessario toopass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="76716-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="76716-868">URL di Hello è stato generato nella sezione "segreto di crittografia del disco non crittografata con una chiave di scambio delle CHIAVI" hello.</span><span class="sxs-lookup"><span data-stu-id="76716-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="76716-869">Uso di una chiave di crittografia della chiave (KEK)</span><span class="sxs-lookup"><span data-stu-id="76716-869">Using a KEK</span></span>
<span data-ttu-id="76716-870">Quando si collega il disco del sistema operativo hello, passare `$KeyEncryptionKey` e `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="76716-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="76716-871">URL di Hello è stato generato nella sezione "segreto di crittografia del disco non crittografata con una chiave di scambio delle CHIAVI" hello.</span><span class="sxs-lookup"><span data-stu-id="76716-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

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

## <a name="download-this-guide"></a><span data-ttu-id="76716-872">Scaricare questa guida</span><span class="sxs-lookup"><span data-stu-id="76716-872">Download this guide</span></span>
<span data-ttu-id="76716-873">È possibile scaricare questa Guida da hello [Raccolta TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="76716-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="76716-874">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="76716-874">For more information</span></span>
[<span data-ttu-id="76716-875">Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 1</span><span class="sxs-lookup"><span data-stu-id="76716-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="76716-876">Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 2</span><span class="sxs-lookup"><span data-stu-id="76716-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
