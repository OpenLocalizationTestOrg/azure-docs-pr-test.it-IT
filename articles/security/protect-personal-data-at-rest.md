---
title: Azure proteggere i dati personali inattivi con crittografia | Documenti Microsoft
description: Questo articolo fa parte di una serie consentono di usare Azure per proteggere i dati personali
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
ms.openlocfilehash: d0ef3ca8d48f5ba11a89c787ff59df39eeaf673b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="b7991-103">Tecnologie di crittografia di Azure: proteggere i dati personali inattivi con la crittografia</span><span class="sxs-lookup"><span data-stu-id="b7991-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="b7991-104">Questo articolo aiuta a comprendere e usare le tecnologie di crittografia di Azure per proteggere i dati inattivi.</span><span class="sxs-lookup"><span data-stu-id="b7991-104">This article helps you understand and use Azure encryption technologies to secure data at rest.</span></span>

<span data-ttu-id="b7991-105">La crittografia dei dati inattivi è una procedura consigliata essenziale per proteggere dati sensibili o personali e per soddisfare la conformità e i requisiti di privacy dei dati.</span><span class="sxs-lookup"><span data-stu-id="b7991-105">Encryption of data at rest is essential as a best practice to protect sensitive or personal data and to meet compliance and data privacy requirements.</span></span>
<span data-ttu-id="b7991-106">La crittografia dei dati inattivi è progettata per impedire a un utente malintenzionato di accedere ai dati non crittografati, garantendo che i dati siano crittografati quando sono su disco.</span><span class="sxs-lookup"><span data-stu-id="b7991-106">Encryption at rest is designed to prevent the attacker from accessing the unencrypted data by ensuring the data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="b7991-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="b7991-107">Scenario</span></span> 

<span data-ttu-id="b7991-108">Un'importante compagnia di viaggi in crociera, con sede negli Stati Uniti, sta espandendo le proprie operazioni per offrire itinerari nel Mar Mediterraneo e nel Mar Baltico, nonché nelle isole britanniche.</span><span class="sxs-lookup"><span data-stu-id="b7991-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="b7991-109">Per supportare questo progetto, ha acquistato diverse linee minori con sede in Italia, Germania, Danimarca e Regno Unito.</span><span class="sxs-lookup"><span data-stu-id="b7991-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="b7991-110">La società usa Microsoft Azure per archiviare i dati aziendali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="b7991-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="b7991-111">Può trattarsi di dipendente e/o informazioni sul cliente, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b7991-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="b7991-112">Indirizzi</span><span class="sxs-lookup"><span data-stu-id="b7991-112">addresses</span></span>
- <span data-ttu-id="b7991-113">Numeri di telefono</span><span class="sxs-lookup"><span data-stu-id="b7991-113">phone numbers</span></span>
- <span data-ttu-id="b7991-114">Codici fiscali</span><span class="sxs-lookup"><span data-stu-id="b7991-114">tax identification numbers</span></span>
- <span data-ttu-id="b7991-115">informazioni mediche</span><span class="sxs-lookup"><span data-stu-id="b7991-115">medical information</span></span>
- <span data-ttu-id="b7991-116">Dati delle carte di credito</span><span class="sxs-lookup"><span data-stu-id="b7991-116">credit card information</span></span>

<span data-ttu-id="b7991-117">La società è necessario proteggere la privacy dei dati dipendenti e clienti durante la creazione di dati accessibili per i reparti che ne hanno necessità.</span><span class="sxs-lookup"><span data-stu-id="b7991-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="b7991-118">ad esempio quelli che si occupano di retribuzioni e prenotazioni.</span><span class="sxs-lookup"><span data-stu-id="b7991-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="b7991-119">La linea di crociere gestisce anche un database di grandi dimensioni dei membri dei programmi fedeltà e premi, che include informazioni personali per tenere traccia delle relazioni con i clienti attuali e del passato.</span><span class="sxs-lookup"><span data-stu-id="b7991-119">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="b7991-120">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="b7991-120">Problem statement</span></span>

<span data-ttu-id="b7991-121">La società è necessario proteggere la privacy dei dati personali dei dipendenti e clienti durante la creazione di dati accessibili per i reparti che ne hanno necessità (ad esempio, retribuzioni e le prenotazioni reparti).</span><span class="sxs-lookup"><span data-stu-id="b7991-121">The company must protect the privacy of employees’ and customers’ personal data while making data accessible to those departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="b7991-122">Questi dati personali vengono archiviati esternamente al data center controllato dall'azienda e non vengono controllati fisicamente dalla società.</span><span class="sxs-lookup"><span data-stu-id="b7991-122">This personal data is stored outside of the corporate-controlled data center and is not under the company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="b7991-123">Obiettivo dell'azienda</span><span class="sxs-lookup"><span data-stu-id="b7991-123">Company goal</span></span>

<span data-ttu-id="b7991-124">Come parte di una strategia di sicurezza con difesa avanzata a più livelli, l'obiettivo della società è garantire che tutte le origini dati che contengono dati personali siano crittografate, incluse quelle che si trovano nello spazio di archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="b7991-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal to ensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="b7991-125">Se utenti non autorizzati ottengono l'accesso a dati personali, questi devono essere in forma illeggibile.</span><span class="sxs-lookup"><span data-stu-id="b7991-125">If unauthorized persons gain access to the personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="b7991-126">L'applicazione della crittografia deve essere facile, o trasparente, per utenti e amministratori.</span><span class="sxs-lookup"><span data-stu-id="b7991-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="b7991-127">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="b7991-127">Solutions</span></span>

<span data-ttu-id="b7991-128">I servizi di Azure offrono più strumenti e tecnologie per semplificare la protezione dei dati personali inattivi tramite la crittografia.</span><span class="sxs-lookup"><span data-stu-id="b7991-128">Azure services provide multiple tools and technologies to help you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="b7991-129">Insieme di credenziali chiave Azure</span><span class="sxs-lookup"><span data-stu-id="b7991-129">Azure Key Vault</span></span>

<span data-ttu-id="b7991-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) offre archiviazione sicura per le chiavi usate per crittografare dati inattivi nei servizi di Azure ed è la soluzione di gestione e archiviazione delle chiavi consigliata.</span><span class="sxs-lookup"><span data-stu-id="b7991-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for the keys used to encrypt data at rest in Azure services and is the recommended key storage and management solution.</span></span> <span data-ttu-id="b7991-131">La gestione delle chiavi di crittografia è essenziale per proteggere i dati archiviati.</span><span class="sxs-lookup"><span data-stu-id="b7991-131">Encryption key management is essential to securing stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-to-protect-keys-that-encrypt-personal-data"></a><span data-ttu-id="b7991-132">Come si usa Azure Key Vault per proteggere le chiavi che crittografano i dati personali?</span><span class="sxs-lookup"><span data-stu-id="b7991-132">How do I use Azure Key Vault to protect keys that encrypt personal data?</span></span>

<span data-ttu-id="b7991-133">Per usare Azure Key Vault, è necessaria la sottoscrizione di un account Azure.</span><span class="sxs-lookup"><span data-stu-id="b7991-133">To use Azure Key Vault, you need a subscription to an Azure account.</span></span> <span data-ttu-id="b7991-134">Deve essere installato anche Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7991-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="b7991-135">I passaggi includono l'uso dei cmdlet di PowerShell per eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7991-135">Steps include using PowerShell cmdlets to do the following:</span></span>

1. <span data-ttu-id="b7991-136">Connettersi alle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="b7991-136">Connect to your subscriptions</span></span>

2. <span data-ttu-id="b7991-137">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="b7991-137">Create a key vault</span></span>

3. <span data-ttu-id="b7991-138">Aggiungere una chiave o un segreto all'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="b7991-138">Add a key or secret to the key vault</span></span>

4. <span data-ttu-id="b7991-139">Registrare le applicazioni che useranno l'insieme di credenziali delle chiavi con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7991-139">Register applications that will use the key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="b7991-140">Autorizzare le applicazioni a usare la chiave o il segreto</span><span class="sxs-lookup"><span data-stu-id="b7991-140">Authorize the applications to use the key or secret</span></span>

<span data-ttu-id="b7991-141">Per creare un insieme di credenziali, usare il cmdlet di PowerShell New-AzureRmKeyVault.</span><span class="sxs-lookup"><span data-stu-id="b7991-141">To create a key vault, use the New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="b7991-142">È necessario assegnare un nome dell'insieme di credenziali, un nome del gruppo di risorse e una posizione geografica.</span><span class="sxs-lookup"><span data-stu-id="b7991-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="b7991-143">Il nome dell'insieme di credenziali verrà usato per la gestione delle chiavi con altri cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b7991-143">You’ll use the vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="b7991-144">Le applicazioni che usano l'insieme di credenziali tramite l'API REST devono usare questo URI.</span><span class="sxs-lookup"><span data-stu-id="b7991-144">Applications that use the vault through the REST API will use the vault URI.</span></span>

<span data-ttu-id="b7991-145">Azure Key Vault può fornire una chiave protetta tramite software oppure è possibile importare una chiave esistente in un file PFX.</span><span class="sxs-lookup"><span data-stu-id="b7991-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="b7991-146">È anche possibile archiviare segreti (password) nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b7991-146">You can also store secrets (passwords) in the vault.</span></span>

<span data-ttu-id="b7991-147">È infine possibile generare una chiave nel modulo HSM locale e trasferirla nei moduli HSM nel servizio Azure Key Vault, senza che la chiave oltrepassi i confini del modulo HSM.</span><span class="sxs-lookup"><span data-stu-id="b7991-147">You can also generate a key in your local HSM and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary.</span></span>

<span data-ttu-id="b7991-148">Per istruzioni dettagliate sull'uso di Azure Key Vault, seguire i passaggi inclusi in [Introduzione ad Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="b7991-148">For detailed instructions on using Azure Key Vault, follow the steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="b7991-149">Per un elenco dei cmdlet di PowerShell usati con Azure Key Vault, vedere [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="b7991-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="b7991-150">Crittografia dischi di Azure per Windows</span><span class="sxs-lookup"><span data-stu-id="b7991-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="b7991-151">[Crittografia dischi di Azure per macchine virtuali IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protegge i dati personali inattivi nelle macchine virtuali di Azure e si integra con Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b7991-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="b7991-152">Crittografia dischi di Azure usa [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows e [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux per crittografare i dischi del sistema operativo e dei dati.</span><span class="sxs-lookup"><span data-stu-id="b7991-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux to encrypt both the OS and the data disks.</span></span> <span data-ttu-id="b7991-153">Crittografia dischi di Azure è supportata in Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 e nei client Windows 8 e Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b7991-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-to-protect-personal-data"></a><span data-ttu-id="b7991-154">Come si usa Crittografia dischi di Azure per proteggere i dati personali?</span><span class="sxs-lookup"><span data-stu-id="b7991-154">How do I use Azure Disk Encryption to protect personal data?</span></span>

<span data-ttu-id="b7991-155">Per usare Crittografia dischi di Azure, è necessaria la sottoscrizione di un account Azure.</span><span class="sxs-lookup"><span data-stu-id="b7991-155">To use Azure Disk Encryption, you need a subscription to an Azure account.</span></span> <span data-ttu-id="b7991-156">Per abilitare Crittografia dischi di Azure per macchine virtuali Windows e Linux, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7991-156">To enable Azure Disk Encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="b7991-157">Usare il modello di Resource Manager per Crittografia dischi di Azure, PowerShell o l'interfaccia della riga di comando per abilitare la crittografia dei dischi e specificare la configurazione della crittografia.</span><span class="sxs-lookup"><span data-stu-id="b7991-157">Use the Azure Disk Encryption Resource Manager template, PowerShell, or the command line interface (CLI) to enable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="b7991-158">Concedere l'accesso alla piattaforma Azure per leggere il materiale di crittografia dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="b7991-158">Grant access to the Azure platform to read the encryption material from your key vault.</span></span>

3. <span data-ttu-id="b7991-159">Specificare l'identità di un'applicazione di Azure Active Directory (AAD) per scrivere il materiale della chiave di crittografia nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="b7991-159">Provide an Azure Active Directory (AAD) application identity to write the encryption key material to your key vault.</span></span>

<span data-ttu-id="b7991-160">Azure aggiorna la configurazione della macchina virtuale e dell'insieme di credenziali delle chiavi e configura la macchina virtuale crittografata.</span><span class="sxs-lookup"><span data-stu-id="b7991-160">Azure will update the VM and the key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="b7991-161">Quando si configura l'insieme di credenziali delle chiavi per supportare Crittografia dischi di Azure, è possibile aggiungere una chiave di crittografia della chiave per fornire ulteriore sicurezza e supportare il backup delle macchine virtuali crittografate.</span><span class="sxs-lookup"><span data-stu-id="b7991-161">When you set up your key vault to support Azure Disk Encryption, you can add a key encryption key (KEK) for added security and to support backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="b7991-162">Le istruzioni dettagliate per esperienze utente e scenari di distribuzione specifici sono disponibili in [Crittografia dischi di Azure per le macchine virtuali IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="b7991-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="b7991-163">Crittografia del servizio di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b7991-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="b7991-164">[Crittografia del servizio di archiviazione di Azure per dati inattivi](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) consente di proteggere e salvaguardare i dati, in modo da soddisfare i criteri di sicurezza e conformità dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b7991-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="b7991-165">Archiviazione di Azure crittografa automaticamente i dati usando crittografia AES a 256 bit prima della persistenza nella risorsa di archiviazione e li decrittografa prima del recupero.</span><span class="sxs-lookup"><span data-stu-id="b7991-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior to persisting to storage, and decrypts it prior to retrieval.</span></span> <span data-ttu-id="b7991-166">Questo servizio è disponibile per BLOB di Azure e File di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7991-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-to-protect-personal-data"></a><span data-ttu-id="b7991-167">Come si usa Crittografia del servizio di archiviazione per proteggere i dati personali?</span><span class="sxs-lookup"><span data-stu-id="b7991-167">How do I use Storage Service Encryption to protect personal data?</span></span>

<span data-ttu-id="b7991-168">Per abilitare Crittografia del servizio di archiviazione, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7991-168">To enable Storage Service Encryption, do the following:</span></span>

1. <span data-ttu-id="b7991-169">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7991-169">Log into the Azure portal.</span></span>

2. <span data-ttu-id="b7991-170">Selezionare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b7991-170">Select a storage account.</span></span>

3. <span data-ttu-id="b7991-171">Nella sezione Servizio BLOB in Impostazioni selezionare Crittografia.</span><span class="sxs-lookup"><span data-stu-id="b7991-171">In Settings, under the Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="b7991-172">Nella sezione Servizio file selezionare Crittografia.</span><span class="sxs-lookup"><span data-stu-id="b7991-172">Under the File Service section, select Encryption.</span></span>

<span data-ttu-id="b7991-173">Dopo avere selezionato l'impostazione Crittografia, è possibile abilitare o disabilitare Crittografia del servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b7991-173">After you click the Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="b7991-174">I nuovi dati verranno crittografati.</span><span class="sxs-lookup"><span data-stu-id="b7991-174">New data will be encrypted.</span></span> <span data-ttu-id="b7991-175">I dati presenti nei file esistenti in questo account di archiviazione resteranno non crittografati.</span><span class="sxs-lookup"><span data-stu-id="b7991-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="b7991-176">Dopo aver abilitato la crittografia, copiare i dati nell'account di archiviazione usando uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7991-176">After enabling encryption, copy data to the storage account using one of the following methods:</span></span>

1. <span data-ttu-id="b7991-177">Copiare i BLOB o i file con l'[utilità della riga di comando AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="b7991-177">Copy blobs or files with the [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="b7991-178">[Montare una condivisione di file con SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows), per poter usare un'utilità come Robocopy per copiare i file.</span><span class="sxs-lookup"><span data-stu-id="b7991-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy to copy files.</span></span>

3. <span data-ttu-id="b7991-179">Copiare dati di BLOB o file da e verso l'archiviazione BLOB o tra account di archiviazione usando [librerie client di archiviazione come .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="b7991-179">Copy blob or file data to and from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="b7991-180">Usare uno [strumento di esplorazione di archiviazione](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) per caricare BLOB nell'account di archiviazione con la crittografia abilitata.</span><span class="sxs-lookup"><span data-stu-id="b7991-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) to upload blobs to your storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="b7991-181">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="b7991-181">Transparent Data Encryption</span></span>

<span data-ttu-id="b7991-182">Transparent Data Encryption (TDE) è una funzionalità inclusa in SQL Azure che permette di crittografare i dati a livello di database e di server.</span><span class="sxs-lookup"><span data-stu-id="b7991-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both the database and server levels.</span></span> <span data-ttu-id="b7991-183">La tecnologia TDE è ora abilitata per impostazione predefinita in tutti i nuovi database creati.</span><span class="sxs-lookup"><span data-stu-id="b7991-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="b7991-184">TDE esegue la crittografia e la decrittografia delle operazioni di I/O di file di dati e log in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="b7991-184">TDE performs real-time I/O encryption and decryption of the data and log files.</span></span>

#### <a name="how-do-i-use-tde-to-protect-personal-data"></a><span data-ttu-id="b7991-185">Come si usa TDE per proteggere i dati personali?</span><span class="sxs-lookup"><span data-stu-id="b7991-185">How do I use TDE to protect personal data?</span></span>

<span data-ttu-id="b7991-186">È possibile configurare TDE tramite il portale di Azure, con l'API REST o con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7991-186">You can configure TDE through the Azure portal, by using the REST API, or by using PowerShell.</span></span> <span data-ttu-id="b7991-187">Per abilitare TDE in un database esistente usando il portale di Azure, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7991-187">To enable TDE on an existing database using the Azure Portal, do the following:</span></span>

1. <span data-ttu-id="b7991-188">Accedere al portale di Azure all'indirizzo <https://portal.azure.com> con l'account di amministratore o collaboratore di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7991-188">Visit the Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="b7991-189">Nel banner a sinistra fare clic su SFOGLIA e quindi su Database SQL.</span><span class="sxs-lookup"><span data-stu-id="b7991-189">On the left banner, click to BROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="b7991-190">Con Database SQL selezionato nel riquadro a sinistra, fare clic sul database utente.</span><span class="sxs-lookup"><span data-stu-id="b7991-190">With SQL databases selected in the left pane, click your user database.</span></span>

4. <span data-ttu-id="b7991-191">Nel pannello del database fare clic su Tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="b7991-191">In the database blade, click All settings.</span></span>

5. <span data-ttu-id="b7991-192">Nel riquadro Impostazioni fare clic sulla parte Transparent Data Encryption per aprire il riquadro Transparent Data Encryption.</span><span class="sxs-lookup"><span data-stu-id="b7991-192">In the Settings blade, click Transparent data encryption part to open the Transparent data encryption blade.</span></span>

6. <span data-ttu-id="b7991-193">Nel riquadro Crittografia dati spostare il pulsante Crittografia dati su Sì e quindi fare clic su Salva (nella parte superiore della pagina) per applicare l'impostazione.</span><span class="sxs-lookup"><span data-stu-id="b7991-193">In the Data encryption blade, move the Data encryption button to On, and then click Save (at the top of the page) to apply the setting.</span></span> <span data-ttu-id="b7991-194">Lo stato di crittografia indicherà approssimativamente lo stato di Transparent Data Encryption.</span><span class="sxs-lookup"><span data-stu-id="b7991-194">The Encryption status will approximate the progress of the transparent data encryption.</span></span>

![Abilitazione della crittografia dei dati](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="b7991-196">Le istruzioni su come abilitare TDE e le informazioni sulla decrittografia di database protetti con TDE sono disponibili nell'articolo [Transparent Data Encryption con il database SQL di Azure ](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).</span><span class="sxs-lookup"><span data-stu-id="b7991-196">Instructions on how to enable TDE and information on decrypting TDE-protected databases and more can be found in the article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="b7991-197">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b7991-197">Summary</span></span>

<span data-ttu-id="b7991-198">La società può realizzare il proprio obiettivo di crittografare i dati personali archiviati nel cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7991-198">The company can accomplish its goal of encrypting personal data stored in the Azure cloud.</span></span> <span data-ttu-id="b7991-199">A questo scopo, può usare Crittografia dischi di Azure per proteggere interi volumi.</span><span class="sxs-lookup"><span data-stu-id="b7991-199">They can do this by using Azure Disk Encryption to  protect entire volumes.</span></span> <span data-ttu-id="b7991-200">Possono essere inclusi i file del sistema operativo e i file di dati che contengono informazioni personali e altri dati sensibili.</span><span class="sxs-lookup"><span data-stu-id="b7991-200">This may include both the operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="b7991-201">È possibile usare Crittografia del servizio di archiviazione di Azure per proteggere dati personali archiviati in BLOB e file.</span><span class="sxs-lookup"><span data-stu-id="b7991-201">Azure Storage Service encryption can be used to protect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="b7991-202">Per i dati archiviati in database SQL di Azure, Transparent Data Encryption offre protezione dall'esposizione non autorizzata delle informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="b7991-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="b7991-203">Per proteggere le chiavi usate per crittografare dati in Azure, la società può usare Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b7991-203">To protect the keys that are used to encrypt data in Azure, the company can use Azure Key Vault.</span></span> <span data-ttu-id="b7991-204">Questo servizio semplifica il processo di gestione delle chiavi e permette alla società di mantenere il controllo delle chiavi che accedono ai dati personali e li crittografano.</span><span class="sxs-lookup"><span data-stu-id="b7991-204">This streamlines the key management process and enables the company to maintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7991-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7991-205">Next steps</span></span>

- [<span data-ttu-id="b7991-206">Guida alla risoluzione dei problemi di Crittografia dischi di Azure</span><span class="sxs-lookup"><span data-stu-id="b7991-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="b7991-207">Crittografare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="b7991-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="b7991-208">Crittografia dei dati in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b7991-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="b7991-209">Crittografia di dati inattivi del database in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b7991-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
