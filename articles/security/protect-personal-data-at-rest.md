---
title: Proteggere i dati personali inattivi con crittografia aaaAzure | Documenti Microsoft
description: Questo articolo fa parte di una serie consentono di utilizzare i dati personali tooprotect Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="70fa8-103">Tecnologie di crittografia di Azure: proteggere i dati personali inattivi con la crittografia</span><span class="sxs-lookup"><span data-stu-id="70fa8-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="70fa8-104">In questo articolo consente di comprendere e utilizzare dati toosecure tecnologie di crittografia Azure inattivi.</span><span class="sxs-lookup"><span data-stu-id="70fa8-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="70fa8-105">Crittografia dei dati inattivi è essenziale come best practice tooprotect riservate o personali dati e conformità toomeet e requisiti sulla privacy dei dati.</span><span class="sxs-lookup"><span data-stu-id="70fa8-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="70fa8-106">Crittografia inattivi è l'autore dell'attacco hello tooprevent progettato l'accesso ai dati di non crittografato hello garantendo hello dati vengono crittografati quando nel disco.</span><span class="sxs-lookup"><span data-stu-id="70fa8-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="70fa8-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="70fa8-107">Scenario</span></span> 

<span data-ttu-id="70fa8-108">Una società crociera di grandi dimensioni, sede hello negli Stati Uniti, all'espansione relativo itinerari toooffer operazioni Mediterraneo, hello e mare Baltico, nonché hello isole britannico.</span><span class="sxs-lookup"><span data-stu-id="70fa8-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="70fa8-109">toosupport tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito</span><span class="sxs-lookup"><span data-stu-id="70fa8-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="70fa8-110">la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="70fa8-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="70fa8-111">Può trattarsi di dipendente e/o informazioni sul cliente, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="70fa8-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="70fa8-112">Indirizzi</span><span class="sxs-lookup"><span data-stu-id="70fa8-112">addresses</span></span>
- <span data-ttu-id="70fa8-113">Numeri di telefono</span><span class="sxs-lookup"><span data-stu-id="70fa8-113">phone numbers</span></span>
- <span data-ttu-id="70fa8-114">Codici fiscali</span><span class="sxs-lookup"><span data-stu-id="70fa8-114">tax identification numbers</span></span>
- <span data-ttu-id="70fa8-115">informazioni mediche</span><span class="sxs-lookup"><span data-stu-id="70fa8-115">medical information</span></span>
- <span data-ttu-id="70fa8-116">Dati delle carte di credito</span><span class="sxs-lookup"><span data-stu-id="70fa8-116">credit card information</span></span>

<span data-ttu-id="70fa8-117">società Hello necessario proteggere la privacy hello di dati dipendenti e clienti durante la creazione di servizi accessibili toothose dati che ne hanno necessità.</span><span class="sxs-lookup"><span data-stu-id="70fa8-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="70fa8-118">ad esempio quelli che si occupano di retribuzioni e prenotazioni.</span><span class="sxs-lookup"><span data-stu-id="70fa8-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="70fa8-119">riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma che include informazioni personali tootrack relazioni con i clienti correnti e precedenti.</span><span class="sxs-lookup"><span data-stu-id="70fa8-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="70fa8-120">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="70fa8-120">Problem statement</span></span>

<span data-ttu-id="70fa8-121">società Hello necessario proteggere la privacy hello dei dati personali dei dipendenti e clienti durante la creazione di reparti toothose accessibile dati che ne hanno necessità (ad esempio, retribuzioni e le prenotazioni reparti).</span><span class="sxs-lookup"><span data-stu-id="70fa8-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="70fa8-122">Questi dati personali viene archiviati all'esterno di centro dati aziendale controllati hello e non sono incluso nel controllo fisico dell'azienda hello.</span><span class="sxs-lookup"><span data-stu-id="70fa8-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="70fa8-123">Obiettivo dell'azienda</span><span class="sxs-lookup"><span data-stu-id="70fa8-123">Company goal</span></span>

<span data-ttu-id="70fa8-124">Come parte di una strategia di sicurezza a più livelli di difesa in profondità, è un tooensure obiettivo aziendale che tutte le origini dati che contengono dati personali vengono crittografate, inclusi quelli che risiedono nell'archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="70fa8-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="70fa8-125">Se non è autorizzato toohello persone guadagno accedere ai dati personali, deve essere in un formato che verrà eseguito il rendering illeggibile.</span><span class="sxs-lookup"><span data-stu-id="70fa8-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="70fa8-126">L'applicazione della crittografia deve essere facile, o trasparente, per utenti e amministratori.</span><span class="sxs-lookup"><span data-stu-id="70fa8-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="70fa8-127">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="70fa8-127">Solutions</span></span>

<span data-ttu-id="70fa8-128">Servizi di Azure forniscono più toohelp strumenti e tecnologie proteggere i dati personali rest crittografandola.</span><span class="sxs-lookup"><span data-stu-id="70fa8-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="70fa8-129">Insieme di credenziali chiave Azure</span><span class="sxs-lookup"><span data-stu-id="70fa8-129">Azure Key Vault</span></span>

<span data-ttu-id="70fa8-130">[Insieme di credenziali chiave di Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) fornisce l'archiviazione sicura per le chiavi di hello utilizzate tooencrypt dati inattivi nei servizi di Azure e hello consigliata principali soluzioni di archiviazione e la gestione.</span><span class="sxs-lookup"><span data-stu-id="70fa8-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="70fa8-131">Gestire la chiave di crittografia è essenziale toosecuring archiviati dati.</span><span class="sxs-lookup"><span data-stu-id="70fa8-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="70fa8-132">Utilizzo di chiavi di tooprotect Azure insieme di credenziali chiave di crittografia dati personali</span><span class="sxs-lookup"><span data-stu-id="70fa8-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="70fa8-133">toouse insieme di credenziali chiave di Azure, è necessario un account di Azure di tooan sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="70fa8-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="70fa8-134">Deve essere installato anche Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70fa8-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="70fa8-135">Con PowerShell cmdlet toodo hello seguenti passaggi:</span><span class="sxs-lookup"><span data-stu-id="70fa8-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="70fa8-136">Connettersi tooyour sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="70fa8-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="70fa8-137">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="70fa8-137">Create a key vault</span></span>

3. <span data-ttu-id="70fa8-138">Aggiungere una chiave o un insieme di credenziali chiave segreta toohello</span><span class="sxs-lookup"><span data-stu-id="70fa8-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="70fa8-139">Registrare le applicazioni che verranno utilizzato l'insieme di credenziali chiave hello con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70fa8-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="70fa8-140">Autorizzare hello applicazioni toouse hello chiave o il segreto</span><span class="sxs-lookup"><span data-stu-id="70fa8-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="70fa8-141">toocreate un insieme di credenziali chiave, utilizzare i cmdlet di PowerShell New-AzureRmKeyVault hello.</span><span class="sxs-lookup"><span data-stu-id="70fa8-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="70fa8-142">È necessario assegnare un nome dell'insieme di credenziali, un nome del gruppo di risorse e una posizione geografica.</span><span class="sxs-lookup"><span data-stu-id="70fa8-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="70fa8-143">Si utilizzerà il nome di archivio hello quando la gestione delle chiavi tramite altri cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70fa8-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="70fa8-144">Le applicazioni che utilizzano l'insieme di credenziali di hello tramite API REST hello utilizzerà l'URI dell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="70fa8-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="70fa8-145">Azure Key Vault può fornire una chiave protetta tramite software oppure è possibile importare una chiave esistente in un file PFX.</span><span class="sxs-lookup"><span data-stu-id="70fa8-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="70fa8-146">È anche possibile archiviare i segreti (password) nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="70fa8-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="70fa8-147">È anche possibile generare una chiave nel modulo di protezione hardware locale e trasferirlo nel servizio insieme di credenziali chiave, hello tooHSMs senza chiave hello lasciando limite HSM hello.</span><span class="sxs-lookup"><span data-stu-id="70fa8-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="70fa8-148">Per istruzioni dettagliate sull'utilizzo di credenziali chiave di Azure, seguire i passaggi hello [introduzione insieme credenziali chiavi Azure.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="70fa8-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="70fa8-149">Per un elenco dei cmdlet di PowerShell usati con Azure Key Vault, vedere [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="70fa8-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="70fa8-150">Crittografia dischi di Azure per Windows</span><span class="sxs-lookup"><span data-stu-id="70fa8-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="70fa8-151">[Crittografia dischi di Azure per macchine virtuali IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protegge i dati personali inattivi nelle macchine virtuali di Azure e si integra con Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="70fa8-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="70fa8-152">La crittografia del disco di Azure Usa [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows e [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt entrambi hello del sistema operativo e hello dischi dati.</span><span class="sxs-lookup"><span data-stu-id="70fa8-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="70fa8-153">Crittografia dischi di Azure è supportata in Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 e nei client Windows 8 e Windows 10.</span><span class="sxs-lookup"><span data-stu-id="70fa8-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="70fa8-154">Utilizzo di dati personali tooprotect di crittografia del disco di Azure</span><span class="sxs-lookup"><span data-stu-id="70fa8-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="70fa8-155">toouse crittografia del disco di Azure, è necessario un account di Azure di tooan sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="70fa8-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="70fa8-156">tooenable Azure disco crittografia per Windows e le macchine virtuali Linux, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="70fa8-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="70fa8-157">Utilizzare il modello di gestione risorse di Azure disco crittografia hello, PowerShell o crittografia del disco tooenable hello interfaccia della riga di comando (CLI) e specificare la configurazione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="70fa8-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="70fa8-158">Concedere accesso toohello materiale della piattaforma Azure tooread hello crittografia di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="70fa8-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="70fa8-159">Fornire un Azure Active Directory (AAD) applicazione identità toowrite hello crittografia chiave tooyour materiale chiave insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="70fa8-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="70fa8-160">Azure Aggiorna hello macchina virtuale e la configurazione dell'insieme di credenziali chiave hello e impostare la macchina virtuale crittografata.</span><span class="sxs-lookup"><span data-stu-id="70fa8-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="70fa8-161">Quando si configura il toosupport insieme di credenziali chiave crittografia del disco di Azure, è possibile aggiungere una chiave di crittografia della chiave (KEK) per maggiore sicurezza e toosupport backup di macchine virtuali crittografati.</span><span class="sxs-lookup"><span data-stu-id="70fa8-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="70fa8-162">Le istruzioni dettagliate per esperienze utente e scenari di distribuzione specifici sono disponibili in [Crittografia dischi di Azure per le macchine virtuali IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="70fa8-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="70fa8-163">Crittografia del servizio di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="70fa8-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="70fa8-164">[Azure Storage Service crittografia (SSE) per i dati inattivi](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) consente di proteggere e salvaguardare i propri impegni di sicurezza e conformità organizzativi toomeet i dati.</span><span class="sxs-lookup"><span data-stu-id="70fa8-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="70fa8-165">Archiviazione di Azure crittografa i dati utilizzando toostorage di toopersisting precedente la crittografia AES a 256 bit automaticamente e lo decrittografa tooretrieval precedente.</span><span class="sxs-lookup"><span data-stu-id="70fa8-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="70fa8-166">Questo servizio è disponibile per BLOB di Azure e File di Azure.</span><span class="sxs-lookup"><span data-stu-id="70fa8-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="70fa8-167">Utilizzo di dati personali di tooprotect la crittografia del servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="70fa8-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="70fa8-168">la crittografia del servizio di archiviazione, tooenable hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="70fa8-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="70fa8-169">Accedere hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="70fa8-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="70fa8-170">Selezionare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="70fa8-170">Select a storage account.</span></span>

3. <span data-ttu-id="70fa8-171">In impostazioni, nella sezione del servizio Blob hello, selezionare la crittografia.</span><span class="sxs-lookup"><span data-stu-id="70fa8-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="70fa8-172">In hello sezione servizio File, selezionare la crittografia.</span><span class="sxs-lookup"><span data-stu-id="70fa8-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="70fa8-173">Dopo aver selezionato l'impostazione di crittografia hello, è possibile abilitare o disabilitare la crittografia del servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="70fa8-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="70fa8-174">I nuovi dati verranno crittografati.</span><span class="sxs-lookup"><span data-stu-id="70fa8-174">New data will be encrypted.</span></span> <span data-ttu-id="70fa8-175">I dati presenti nei file esistenti in questo account di archiviazione resteranno non crittografati.</span><span class="sxs-lookup"><span data-stu-id="70fa8-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="70fa8-176">Dopo l'abilitazione della crittografia, copiare account di archiviazione dati toohello utilizzando uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="70fa8-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="70fa8-177">Copiare BLOB o i file con hello [utilità della riga di comando AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="70fa8-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="70fa8-178">[Montare una condivisione file SMB tramite](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) pertanto è possibile utilizzare un'utilità, ad esempio file toocopy Robocopy.</span><span class="sxs-lookup"><span data-stu-id="70fa8-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="70fa8-179">Copiare blob o file di dati tooand dall'archiviazione blob o tra gli account di archiviazione tramite [le librerie Client di archiviazione, ad esempio .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="70fa8-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="70fa8-180">Utilizzare un [Esplora archivi](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload tooyour account di archiviazione di BLOB con la crittografia attivata.</span><span class="sxs-lookup"><span data-stu-id="70fa8-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="70fa8-181">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="70fa8-181">Transparent Data Encryption</span></span>

<span data-ttu-id="70fa8-182">Transparent Data Encryption (TDE) è una funzionalità di SQL Azure mediante il quale è possibile crittografare i dati in entrambi i livelli di hello database e server.</span><span class="sxs-lookup"><span data-stu-id="70fa8-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="70fa8-183">La tecnologia TDE è ora abilitata per impostazione predefinita in tutti i nuovi database creati.</span><span class="sxs-lookup"><span data-stu-id="70fa8-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="70fa8-184">TDE consente di eseguire la crittografia dei / o e la decrittografia dei file di dati e log hello in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="70fa8-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="70fa8-185">Utilizzo di dati personali tooprotect di Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="70fa8-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="70fa8-186">È possibile configurare Transparent Data Encryption tramite il portale di Azure, hello utilizzando hello API REST o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70fa8-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="70fa8-187">tooenable TDE in un database esistente tramite il portale di Azure, hello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="70fa8-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="70fa8-188">Visitare hello Azure portale in <https://portal.azure.com> e Accedi con l'account amministratore di Azure o collaboratore.</span><span class="sxs-lookup"><span data-stu-id="70fa8-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="70fa8-189">Nel banner sinistro hello, fare clic su tooBROWSE e quindi fare clic su database SQL.</span><span class="sxs-lookup"><span data-stu-id="70fa8-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="70fa8-190">Con il database SQL selezionati nel riquadro di sinistra hello, fare clic sul proprio database utente.</span><span class="sxs-lookup"><span data-stu-id="70fa8-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="70fa8-191">Nel pannello database hello, fare clic su tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="70fa8-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="70fa8-192">Nel pannello impostazioni hello, fare clic su Pannello di Transparent data encryption parte tooopen hello Transparent data encryption.</span><span class="sxs-lookup"><span data-stu-id="70fa8-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="70fa8-193">Nel Pannello di crittografia dati hello, spostare hello dati crittografia pulsante tooOn e quindi fare clic su Salva (in alto hello pagina hello) impostazione hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="70fa8-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="70fa8-194">lo stato di crittografia Hello indicherà approssimativamente lo stato di avanzamento hello di hello transparent data encryption.</span><span class="sxs-lookup"><span data-stu-id="70fa8-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![Abilitazione della crittografia dei dati](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="70fa8-196">Istruzioni su come tooenable Transparent Data Encryption e informazioni su come decrittografare i database protetti da Transparent Data Encryption e altro ancora sono disponibili nell'articolo hello [Transparent Data Encryption con il Database SQL di Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="70fa8-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="70fa8-197">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="70fa8-197">Summary</span></span>

<span data-ttu-id="70fa8-198">Per eseguire l'obiettivo di crittografare i dati personali archiviati nel cloud di Azure hello società Hello.</span><span class="sxs-lookup"><span data-stu-id="70fa8-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="70fa8-199">È possibile farlo mediante la crittografia del disco di Azure troppo proteggere volumi completi.</span><span class="sxs-lookup"><span data-stu-id="70fa8-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="70fa8-200">Questo può includere i file del sistema operativo hello e file di dati che contengono informazioni personali e altri dati sensibili.</span><span class="sxs-lookup"><span data-stu-id="70fa8-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="70fa8-201">È possibile tooprotect utilizzati i dati personali che viene archiviati in file di BLOB e crittografia del servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="70fa8-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="70fa8-202">Per i dati archiviati in database SQL di Azure, Transparent Data Encryption offre protezione dall'esposizione non autorizzata delle informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="70fa8-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="70fa8-203">tooprotect hello chiavi di dati tooencrypt usato in Azure, è possibile utilizzare insieme credenziali chiavi Azure aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="70fa8-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="70fa8-204">Questo semplifica il processo di gestione delle chiavi hello e Abilita hello controllo toomaintain aziendale delle chiavi per l'accesso e crittografare i dati personali.</span><span class="sxs-lookup"><span data-stu-id="70fa8-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70fa8-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70fa8-205">Next steps</span></span>

- [<span data-ttu-id="70fa8-206">Guida alla risoluzione dei problemi di Crittografia dischi di Azure</span><span class="sxs-lookup"><span data-stu-id="70fa8-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="70fa8-207">Crittografare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="70fa8-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="70fa8-208">Crittografia dei dati in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="70fa8-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="70fa8-209">Crittografia di dati inattivi del database in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="70fa8-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
