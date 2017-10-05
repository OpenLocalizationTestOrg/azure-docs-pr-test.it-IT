---
title: Calcolo di Azure - Estensione Diagnostica per Linux | Microsoft Docs
description: Come configurare l'estensione Diagnostica di Azure per Linux (LAD) per raccogliere le metriche e gli eventi dei registri dalle macchine virtuali Linux in esecuzione in Azure.
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 525d706bd709ae72f2dca1c21e06db533ccf32b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-linux-diagnostic-extension-to-monitor-metrics-and-logs"></a><span data-ttu-id="dd071-103">Usare l'estensione Diagnostica per Linux per monitorare le metriche e i registri</span><span class="sxs-lookup"><span data-stu-id="dd071-103">Use Linux Diagnostic Extension to monitor metrics and logs</span></span>

<span data-ttu-id="dd071-104">Questo documento descrive la versione 3.0 e successive dell'estensione Diagnostica per Linux.</span><span class="sxs-lookup"><span data-stu-id="dd071-104">This document describes version 3.0 and newer of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd071-105">Per informazioni sulla versione 2.3 e precedenti, vedere [questo documento](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="dd071-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="dd071-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="dd071-106">Introduction</span></span>

<span data-ttu-id="dd071-107">L'estensione Diagnostica per Linux consente all'utente di monitorare l'integrità delle macchine virtuali Linux eseguite in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-107">The Linux Diagnostic Extension helps a user monitor the health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="dd071-108">Questo servizio offre le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd071-108">It has the following capabilities:</span></span>

* <span data-ttu-id="dd071-109">Raccoglie le metriche delle prestazioni di sistema dalla macchina virtuale e le inserisce in una tabella specifica in un account di archiviazione designato.</span><span class="sxs-lookup"><span data-stu-id="dd071-109">Collects system performance metrics from the VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="dd071-110">Recupera gli eventi di registrazione da SysLog e li inserisce in una tabella specifica nell'account di archiviazione designato.</span><span class="sxs-lookup"><span data-stu-id="dd071-110">Retrieves log events from syslog and stores them in a specific table in the designated storage account.</span></span>
* <span data-ttu-id="dd071-111">Consente agli utenti di personalizzare le metriche dei dati che verranno raccolte e caricate.</span><span class="sxs-lookup"><span data-stu-id="dd071-111">Enables users to customize the data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="dd071-112">Consente agli utenti di personalizzare i servizi di SysLog e i livelli di gravità degli eventi che vengono raccolti e caricati.</span><span class="sxs-lookup"><span data-stu-id="dd071-112">Enables users to customize the syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="dd071-113">Consente agli utenti di caricare in una tabella di archiviazione designata i file di log specificati.</span><span class="sxs-lookup"><span data-stu-id="dd071-113">Enables users to upload specified log files to a designated storage table.</span></span>
* <span data-ttu-id="dd071-114">Supporta l'invio delle metriche e del registro agli endpoint EventHub arbitrari e ai BLOB in formato JSON nell'account di archiviazione designato.</span><span class="sxs-lookup"><span data-stu-id="dd071-114">Supports sending metrics and log events to arbitrary EventHub endpoints and JSON-formatted blobs in the designated storage account.</span></span>

<span data-ttu-id="dd071-115">Questa estensione funziona con entrambi i modelli di distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-the-extension-in-your-vm"></a><span data-ttu-id="dd071-116">Installazione dell'estensione nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="dd071-116">Installing the extension in your VM</span></span>

<span data-ttu-id="dd071-117">È possibile abilitare questa estensione usando i cmdlet di Azure PowerShell, gli script dell'interfaccia della riga di comando di Azure o i modelli di distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-117">You can enable this extension by using the Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="dd071-118">Per altre informazioni, vedere [Funzionalità delle estensioni](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="dd071-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="dd071-119">Il portale di Azure non può essere usato per abilitare o configurare LAD 3.0,</span><span class="sxs-lookup"><span data-stu-id="dd071-119">The Azure portal cannot be used to enable or configure LAD 3.0.</span></span> <span data-ttu-id="dd071-120">ma esso stesso installa e configura la versione 2.3.</span><span class="sxs-lookup"><span data-stu-id="dd071-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="dd071-121">Gli avvisi e i grafici del portale di Azure funzionano con i dati di entrambe le versioni dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="dd071-121">Azure portal graphs and alerts work with data from both versions of the extension.</span></span>

<span data-ttu-id="dd071-122">Le istruzioni di installazione e la [configurazione di esempio scaricabile](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configurano LAD 3.0 per:</span><span class="sxs-lookup"><span data-stu-id="dd071-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="dd071-123">acquisire e archiviare le stesse metriche fornite da LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="dd071-123">capture and store the same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="dd071-124">acquisire un insieme utile di metriche di file system, novità della versione 3.0 di LAD;</span><span class="sxs-lookup"><span data-stu-id="dd071-124">capture a useful set of file system metrics, new to LAD 3.0;</span></span>
* <span data-ttu-id="dd071-125">acquisire la raccolta di SysLog predefinita abilitata da LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="dd071-125">capture the default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="dd071-126">abilitare l'esperienza del portale di Azure per la creazione di grafici e avvisi relativi alle metriche della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd071-126">enable the Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="dd071-127">La configurazione scaricabile è solo un esempio; modificarla per adattarla alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="dd071-127">The downloadable configuration is just an example; modify it to suit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dd071-128">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dd071-128">Prerequisites</span></span>

* <span data-ttu-id="dd071-129">**Agente Linux di Azure 2.2.0 o versione successiva**.</span><span class="sxs-lookup"><span data-stu-id="dd071-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="dd071-130">La maggior parte delle immagini della raccolta Linux di macchine virtuali di Azure include la versione 2.2.7 o successive.</span><span class="sxs-lookup"><span data-stu-id="dd071-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="dd071-131">Eseguire `/usr/sbin/waagent -version` per verificare la versione installata nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd071-131">Run `/usr/sbin/waagent -version` to confirm the version installed on the VM.</span></span> <span data-ttu-id="dd071-132">Se la macchina virtuale esegue una versione precedente dell'agente guest, seguire [queste istruzioni](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) per aggiornarla.</span><span class="sxs-lookup"><span data-stu-id="dd071-132">If the VM is running an older version of the guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to update it.</span></span>
* <span data-ttu-id="dd071-133">**Interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="dd071-133">**Azure CLI**.</span></span> <span data-ttu-id="dd071-134">[Configurare l'ambiente dell'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd071-134">[Set up the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="dd071-135">Il comando wget. Se non è già disponibile, eseguire `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="dd071-135">The wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="dd071-136">Una sottoscrizione di Azure esistente e un account di archiviazione al suo interno per l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="dd071-136">An existing Azure subscription and an existing storage account within it to store the data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="dd071-137">Installazione di esempio</span><span class="sxs-lookup"><span data-stu-id="dd071-137">Sample installation</span></span>

<span data-ttu-id="dd071-138">Compilare i parametri corretti nelle prime tre righe, quindi eseguire lo script come radice:</span><span class="sxs-lookup"><span data-stu-id="dd071-138">Fill in the correct parameters on the first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login to Azure first before anything else
az login

# Select the subscription containing the storage account
az account set --subscription <your_azure_subscription_id>

# Download the sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build the VM resource ID. Replace storage account name and resource ID in the public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build the protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure to install and enable the extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="dd071-139">L'URL per la configurazione di esempio e il relativo contenuto sono soggetti a modifiche.</span><span class="sxs-lookup"><span data-stu-id="dd071-139">The URL for the sample configuration, and its contents, are subject to change.</span></span> <span data-ttu-id="dd071-140">Scaricare una copia del file JSON delle impostazioni del portale e personalizzarla in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="dd071-140">Download a copy of the portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="dd071-141">Qualsiasi modello o automazione creato dall'utente deve usare la propria copia, invece di scaricare l'URL ogni volta.</span><span class="sxs-lookup"><span data-stu-id="dd071-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-the-extension-settings"></a><span data-ttu-id="dd071-142">Aggiornamento delle impostazioni di estensione</span><span class="sxs-lookup"><span data-stu-id="dd071-142">Updating the extension settings</span></span>

<span data-ttu-id="dd071-143">Dopo aver modificato le impostazioni pubbliche o protette, è necessario distribuirle alla macchina virtuale eseguendo lo stesso comando.</span><span class="sxs-lookup"><span data-stu-id="dd071-143">After you've changed your Protected or Public settings, deploy them to the VM by running the same command.</span></span> <span data-ttu-id="dd071-144">Se un'impostazione viene modificata, questo aggiornamento viene inviato all'estensione.</span><span class="sxs-lookup"><span data-stu-id="dd071-144">If anything changed in the settings, the updated settings are sent to the extension.</span></span> <span data-ttu-id="dd071-145">LAD ricarica la configurazione e si riavvia.</span><span class="sxs-lookup"><span data-stu-id="dd071-145">LAD reloads the configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-the-extension"></a><span data-ttu-id="dd071-146">Migrazione dalle versioni precedenti dell'estensione</span><span class="sxs-lookup"><span data-stu-id="dd071-146">Migration from previous versions of the extension</span></span>

<span data-ttu-id="dd071-147">La versione più recente dell'estensione è **3.0**.</span><span class="sxs-lookup"><span data-stu-id="dd071-147">The latest version of the extension is **3.0**.</span></span> <span data-ttu-id="dd071-148">**Le versioni precedenti (2.x) sono deprecate e la loro pubblicazione potrebbe essere annullata a partire dal 31 luglio 2018**.</span><span class="sxs-lookup"><span data-stu-id="dd071-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd071-149">Questa estensione introduce importanti modifiche alla configurazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="dd071-149">This extension introduces breaking changes to the configuration of the extension.</span></span> <span data-ttu-id="dd071-150">Tale modifica è stata apportata per migliorare la sicurezza dell'estensione. Di conseguenza, la compatibilità con versioni precedenti alla versione 2.x potrebbe non essere mantenuta.</span><span class="sxs-lookup"><span data-stu-id="dd071-150">One such change was made to improve the security of the extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="dd071-151">In aggiunta, il server di pubblicazione per questa estensione è diverso dal server di pubblicazione per le versioni 2.x.</span><span class="sxs-lookup"><span data-stu-id="dd071-151">Also, the Extension Publisher for this extension is different than the publisher for the 2.x versions.</span></span>
>
> <span data-ttu-id="dd071-152">Per eseguire la migrazione dalla versione 2.x a questa nuova versione dell'estensione, è necessario disinstallare l'estensione precedente, sotto il nome del server di pubblicazione precedente, e installare la versione 3 dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="dd071-152">To migrate from 2.x to this new version of the extension, you must uninstall the old extension (under the old publisher name), then install version 3 of the extension.</span></span>

<span data-ttu-id="dd071-153">Consigli:</span><span class="sxs-lookup"><span data-stu-id="dd071-153">Recommendations:</span></span>

* <span data-ttu-id="dd071-154">Installare l'estensione abilitando l'aggiornamento automatico della versione secondaria.</span><span class="sxs-lookup"><span data-stu-id="dd071-154">Install the extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="dd071-155">Nelle macchine virtuali con modello di distribuzione classico, specificare "3.*" come versione, se si installa l'estensione tramite Powershell o l'interfaccia della riga di comando XPLAT di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-155">On classic deployment model VMs, specify '3.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="dd071-156">Nelle macchine virtuali con il modello di distribuzione Azure Resource Manager, includere ""autoUpgradeMinorVersion": true" nel modello di distribuzione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd071-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span>
* <span data-ttu-id="dd071-157">Usare un account di archiviazione nuovo o diverso per LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="dd071-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="dd071-158">Esistono diverse piccole incompatibilità tra LAD 2.3 e LAD 3.0 che creano problemi nella condivisione di un account:</span><span class="sxs-lookup"><span data-stu-id="dd071-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="dd071-159">LAD 3.0 inserisce gli eventi SysLog in una tabella con un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="dd071-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="dd071-160">Le stringhe counterSpecifier per le metriche `builtin` differiscono in LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="dd071-160">The counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="dd071-161">Impostazioni protette</span><span class="sxs-lookup"><span data-stu-id="dd071-161">Protected settings</span></span>

<span data-ttu-id="dd071-162">Questo set di informazioni per la configurazione contiene informazioni riservate che devono essere protette dalla visualizzazione pubblica, ad esempio, le credenziali di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd071-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="dd071-163">Queste impostazioni vengono trasmesse e memorizzate dall'estensione in modo crittografato.</span><span class="sxs-lookup"><span data-stu-id="dd071-163">These settings are transmitted to and stored by the extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "the storage account to receive data",
    "storageAccountEndPoint": "the hostname suffix for the cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="dd071-164">Nome</span><span class="sxs-lookup"><span data-stu-id="dd071-164">Name</span></span> | <span data-ttu-id="dd071-165">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-165">Value</span></span>
---- | -----
<span data-ttu-id="dd071-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="dd071-166">storageAccountName</span></span> | <span data-ttu-id="dd071-167">Nome dell'account di archiviazione in cui l'estensione scrive i dati.</span><span class="sxs-lookup"><span data-stu-id="dd071-167">The name of the storage account in which data is written by the extension.</span></span>
<span data-ttu-id="dd071-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="dd071-168">storageAccountEndPoint</span></span> | <span data-ttu-id="dd071-169">(facoltativo) Endpoint che identifica il cloud in cui esiste l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd071-169">(optional) The endpoint identifying the cloud in which the storage account exists.</span></span> <span data-ttu-id="dd071-170">Se questa impostazione è assente, LAD per impostazione predefinita considera il cloud pubblico di Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="dd071-170">If this setting is absent, LAD defaults to the Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="dd071-171">Per usare un account di archiviazione in Azure Germania, Azure per enti pubblici o Azure Cina, impostare questo valore di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="dd071-171">To use a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="dd071-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="dd071-172">storageAccountSasToken</span></span> | <span data-ttu-id="dd071-173">Un [token SAS dell'account](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) per i servizi BLOB e tabella (`ss='bt'`), applicabile a contenitori e oggetti (`srt='co'`), che concede le autorizzazioni di aggiunta, creazione, creazione di elenchi, aggiornamenti e scrittura (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="dd071-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable to containers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="dd071-174">*Non* includere il punto interrogativo (?) principale.</span><span class="sxs-lookup"><span data-stu-id="dd071-174">Do *not* include the leading question-mark (?).</span></span>
<span data-ttu-id="dd071-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="dd071-175">mdsdHttpProxy</span></span> | <span data-ttu-id="dd071-176">(facoltativo) Informazioni sul proxy HTTP necessarie per abilitare l'estensione affinché si connetta all'account di archiviazione e all'endpoint specificati.</span><span class="sxs-lookup"><span data-stu-id="dd071-176">(optional) HTTP proxy information needed to enable the extension to connect to the specified storage account and endpoint.</span></span>
<span data-ttu-id="dd071-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="dd071-177">sinksConfig</span></span> | <span data-ttu-id="dd071-178">(facoltativo) Informazioni sulle destinazioni alternative a cui possono essere inviati le metriche e gli eventi.</span><span class="sxs-lookup"><span data-stu-id="dd071-178">(optional) Details of alternative destinations to which metrics and events can be delivered.</span></span> <span data-ttu-id="dd071-179">Nelle sezioni che seguono vengono illustrati i dettagli specifici di ogni sink di dati supportato dall'estensione.</span><span class="sxs-lookup"><span data-stu-id="dd071-179">The specific details of each data sink supported by the extension are covered in the sections that follow.</span></span>

<span data-ttu-id="dd071-180">È possibile costruire con facilità il token SAS richiesto tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-180">You can easily construct the required SAS token through the Azure portal.</span></span>

1. <span data-ttu-id="dd071-181">Selezionare l'account di archiviazione generico che in cui si desidera che l'estensione scriva</span><span class="sxs-lookup"><span data-stu-id="dd071-181">Select the general-purpose storage account to which you want the extension to write</span></span>
1. <span data-ttu-id="dd071-182">Selezionare "Firma di accesso condiviso" nella sezione delle impostazioni del menu a sinistra</span><span class="sxs-lookup"><span data-stu-id="dd071-182">Select "Shared access signature" from the Settings part of the left menu</span></span>
1. <span data-ttu-id="dd071-183">Creare le sezioni appropriate come descritto in precedenza</span><span class="sxs-lookup"><span data-stu-id="dd071-183">Make the appropriate sections as previously described</span></span>
1. <span data-ttu-id="dd071-184">Fare clic sul pulsante "Genera firma di accesso condiviso".</span><span class="sxs-lookup"><span data-stu-id="dd071-184">Click the "Generate SAS" button.</span></span>

![immagine](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="dd071-186">Copiare la firma di accesso condiviso generata nel campo storageAccountSasToken; rimuovere il punto interrogativo ("?") principale.</span><span class="sxs-lookup"><span data-stu-id="dd071-186">Copy the generated SAS into the storageAccountSasToken field; remove the leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="dd071-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="dd071-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="dd071-188">Questa sezione facoltativa definisce altre destinazioni a cui l'estensione invia le informazioni raccolte.</span><span class="sxs-lookup"><span data-stu-id="dd071-188">This optional section defines additional destinations to which the extension sends the information it collects.</span></span> <span data-ttu-id="dd071-189">La matrice "sink" contiene un oggetto per ogni sink di dati aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="dd071-189">The "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="dd071-190">L'attributo "type" determina gli altri attributi dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="dd071-190">The "type" attribute determines the other attributes in the object.</span></span>

<span data-ttu-id="dd071-191">Elemento</span><span class="sxs-lookup"><span data-stu-id="dd071-191">Element</span></span> | <span data-ttu-id="dd071-192">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-192">Value</span></span>
------- | -----
<span data-ttu-id="dd071-193">name</span><span class="sxs-lookup"><span data-stu-id="dd071-193">name</span></span> | <span data-ttu-id="dd071-194">Una stringa usata per fare riferimento a questo sink altrove nella configurazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="dd071-194">A string used to refer to this sink elsewhere in the extension configuration.</span></span>
<span data-ttu-id="dd071-195">type</span><span class="sxs-lookup"><span data-stu-id="dd071-195">type</span></span> | <span data-ttu-id="dd071-196">Il tipo di sink da definire.</span><span class="sxs-lookup"><span data-stu-id="dd071-196">The type of sink being defined.</span></span> <span data-ttu-id="dd071-197">Determina gli altri valori, se presenti, nelle istanze di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="dd071-197">Determines the other values (if any) in instances of this type.</span></span>

<span data-ttu-id="dd071-198">La versione 3.0 dell'estensione Diagnostica per Linux supporta due tipi di sink: EventHub e JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="dd071-198">Version 3.0 of the Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="the-eventhub-sink"></a><span data-ttu-id="dd071-199">Sink EventHub</span><span class="sxs-lookup"><span data-stu-id="dd071-199">The EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="dd071-200">La voce "sasURL" contiene l'URL completo, incluso il token della firma di accesso condiviso, per l'hub di eventi in cui devono essere pubblicati i dati.</span><span class="sxs-lookup"><span data-stu-id="dd071-200">The "sasURL" entry contains the full URL, including SAS token, for the Event Hub to which data should be published.</span></span> <span data-ttu-id="dd071-201">Per LAD è necessario che la firma di accesso condiviso dia un nome a un criterio che consente l'attestazione di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="dd071-201">LAD requires a SAS naming a policy that enables the Send claim.</span></span> <span data-ttu-id="dd071-202">Esempio:</span><span class="sxs-lookup"><span data-stu-id="dd071-202">An example:</span></span>

* <span data-ttu-id="dd071-203">Creare uno spazio dei nomi dell'hub eventi denominato `contosohub`</span><span class="sxs-lookup"><span data-stu-id="dd071-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="dd071-204">Creare un hub eventi nello spazio dei nomi denominato `syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="dd071-204">Create an Event Hub in the namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="dd071-205">Creare un criterio di accesso condiviso nell'hub eventi denominato `writer` che consenta l'attestazione di trasmissione</span><span class="sxs-lookup"><span data-stu-id="dd071-205">Create a Shared access policy on the Event Hub named `writer` that enables the Send claim</span></span>

<span data-ttu-id="dd071-206">Se è stata creata una firma di accesso condiviso valida fino alla mezzanotte UTC del 1 gennaio 2018, il valore sasURL potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="dd071-206">If you created a SAS good until midnight UTC on January 1, 2018, the sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="dd071-207">Per altre informazioni sulla generazione di token SAS per gli hub eventi, vedere [questa pagina Web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd071-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="the-jsonblob-sink"></a><span data-ttu-id="dd071-208">Sink JsonBlob</span><span class="sxs-lookup"><span data-stu-id="dd071-208">The JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="dd071-209">I dati indirizzati a un sink JsonBlob vengono memorizzati nei BLOB dell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-209">Data directed to a JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="dd071-210">Ogni istanza di LAD crea un BLOB all'ora per ogni nome di sink.</span><span class="sxs-lookup"><span data-stu-id="dd071-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="dd071-211">Ciascun BLOB contiene sempre una matrice JSON sintatticamente valida dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="dd071-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="dd071-212">Le nuove voci vengono aggiunte in modo atomico alla matrice.</span><span class="sxs-lookup"><span data-stu-id="dd071-212">New entries are atomically added to the array.</span></span> <span data-ttu-id="dd071-213">I BLOB vengono archiviati in un contenitore con lo stesso nome come sink.</span><span class="sxs-lookup"><span data-stu-id="dd071-213">Blobs are stored in a container with the same name as the sink.</span></span> <span data-ttu-id="dd071-214">Le regole di archiviazione di Azure per i nomi dei contenitori BLOB si applicano ai nomi dei sink JsonBlob: dai 3 ai 63 caratteri ASCII alfanumerici minuscoli o trattini.</span><span class="sxs-lookup"><span data-stu-id="dd071-214">The Azure storage rules for blob container names apply to the names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="dd071-215">Impostazioni pubbliche</span><span class="sxs-lookup"><span data-stu-id="dd071-215">Public settings</span></span>

<span data-ttu-id="dd071-216">Questa struttura contiene diversi blocchi di impostazioni che controllano le informazioni raccolte dall'estensione.</span><span class="sxs-lookup"><span data-stu-id="dd071-216">This structure contains various blocks of settings that control the information collected by the extension.</span></span> <span data-ttu-id="dd071-217">Tutte le impostazioni sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="dd071-217">Each setting is optional.</span></span> <span data-ttu-id="dd071-218">Se si specifica `ladCfg`, è necessario specificare anche `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="dd071-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "the storage account to receive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="dd071-219">Elemento</span><span class="sxs-lookup"><span data-stu-id="dd071-219">Element</span></span> | <span data-ttu-id="dd071-220">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-220">Value</span></span>
------- | -----
<span data-ttu-id="dd071-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="dd071-221">StorageAccount</span></span> | <span data-ttu-id="dd071-222">Nome dell'account di archiviazione in cui l'estensione scrive i dati.</span><span class="sxs-lookup"><span data-stu-id="dd071-222">The name of the storage account in which data is written by the extension.</span></span> <span data-ttu-id="dd071-223">Deve essere lo stesso nome specificato nelle [Impostazioni protette](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="dd071-223">Must be the same name as is specified in the [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="dd071-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="dd071-224">mdsdHttpProxy</span></span> | <span data-ttu-id="dd071-225">(facoltativo) Uguale al valore indicato in [Impostazioni protette](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="dd071-225">(optional) Same as in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="dd071-226">Il valore pubblico viene sostituito dal valore privato, se impostato.</span><span class="sxs-lookup"><span data-stu-id="dd071-226">The public value is overridden by the private value, if set.</span></span> <span data-ttu-id="dd071-227">Inserire le impostazioni proxy che contengono un segreto, ad esempio una password, nelle [Impostazioni protette](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="dd071-227">Place proxy settings that contain a secret, such as a password, in the [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="dd071-228">Gli elementi rimanenti vengono descritti in dettaglio nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="dd071-228">The remaining elements are described in detail in the following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="dd071-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="dd071-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="dd071-230">Questa struttura facoltativa controlla la raccolta di metriche e registri per l'invio al servizio Metriche di Azure e ad altri dati sink.</span><span class="sxs-lookup"><span data-stu-id="dd071-230">This optional structure controls the gathering of metrics and logs for delivery to the Azure Metrics service and to other data sinks.</span></span> <span data-ttu-id="dd071-231">È necessario specificare `performanceCounters` o `syslogEvents` oppure entrambi.</span><span class="sxs-lookup"><span data-stu-id="dd071-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="dd071-232">È necessario specificare la struttura `metrics`.</span><span class="sxs-lookup"><span data-stu-id="dd071-232">You must specify the `metrics` structure.</span></span>

<span data-ttu-id="dd071-233">Elemento</span><span class="sxs-lookup"><span data-stu-id="dd071-233">Element</span></span> | <span data-ttu-id="dd071-234">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-234">Value</span></span>
------- | -----
<span data-ttu-id="dd071-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="dd071-235">eventVolume</span></span> | <span data-ttu-id="dd071-236">(facoltativo) Controlla il numero di partizioni create all'interno della tabella di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd071-236">(optional) Controls the number of partitions created within the storage table.</span></span> <span data-ttu-id="dd071-237">Può essere uno tra `"Large"`, `"Medium"` o `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="dd071-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="dd071-238">Se non è specificato, il valore predefinito è `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="dd071-238">If not specified, the default value is `"Medium"`.</span></span>
<span data-ttu-id="dd071-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="dd071-239">sampleRateInSeconds</span></span> | <span data-ttu-id="dd071-240">(facoltativo) L'intervallo predefinito tra la raccolta di metriche non elaborate, ovvero non aggregate.</span><span class="sxs-lookup"><span data-stu-id="dd071-240">(optional) The default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="dd071-241">La frequenza di esempio più piccola supportata è 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="dd071-241">The smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="dd071-242">Se non è specificato, il valore predefinito è `15`.</span><span class="sxs-lookup"><span data-stu-id="dd071-242">If not specified, the default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="dd071-243">Metriche</span><span class="sxs-lookup"><span data-stu-id="dd071-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="dd071-244">Elemento</span><span class="sxs-lookup"><span data-stu-id="dd071-244">Element</span></span> | <span data-ttu-id="dd071-245">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-245">Value</span></span>
------- | -----
<span data-ttu-id="dd071-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="dd071-246">resourceId</span></span> | <span data-ttu-id="dd071-247">L'ID della risorsa di Azure Resource Manager della macchina virtuale o del set di scalabilità di macchine a cui appartiene la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd071-247">The Azure Resource Manager resource ID of the VM or of the virtual machine scale set to which the VM belongs.</span></span> <span data-ttu-id="dd071-248">Questa impostazione deve essere specificata anche se nella configurazione viene usato un sink JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="dd071-248">This setting must be also specified if any JsonBlob sink is used in the configuration.</span></span>
<span data-ttu-id="dd071-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="dd071-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="dd071-250">La frequenza con cui le metriche aggregate devono essere calcolate e trasferite a Metriche di Azure, espressa come un intervallo di tempo IS 8601.</span><span class="sxs-lookup"><span data-stu-id="dd071-250">The frequency at which aggregate metrics are to be computed and transferred to Azure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="dd071-251">Il periodo di trasferimento più piccolo è 60 secondi, ovvero PT1M.</span><span class="sxs-lookup"><span data-stu-id="dd071-251">The smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="dd071-252">È necessario specificare almeno un scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="dd071-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="dd071-253">Gli esempi delle metriche specificate nella sezione performanceCounters vengono raccolti ogni 15 secondi o alla frequenza di esempio definita in modo esplicito per il contatore.</span><span class="sxs-lookup"><span data-stu-id="dd071-253">Samples of the metrics specified in the performanceCounters section are collected every 15 seconds or at the sample rate explicitly defined for the counter.</span></span> <span data-ttu-id="dd071-254">Se vengono visualizzate più frequenze scheduledTransferPeriod, come illustrato nell'esempio, ogni aggregazione viene calcolata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="dd071-254">If multiple scheduledTransferPeriod frequencies appear (as in the example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="dd071-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="dd071-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="dd071-256">Questa sezione facoltativa consente di controllare la raccolta delle metriche.</span><span class="sxs-lookup"><span data-stu-id="dd071-256">This optional section controls the collection of metrics.</span></span> <span data-ttu-id="dd071-257">Gli esempi non elaborati vengono aggregati per ogni [scheduledTransferPeriod](#metrics) al fine di produrre questi valori:</span><span class="sxs-lookup"><span data-stu-id="dd071-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) to produce these values:</span></span>

* <span data-ttu-id="dd071-258">mean</span><span class="sxs-lookup"><span data-stu-id="dd071-258">mean</span></span>
* <span data-ttu-id="dd071-259">minimum</span><span class="sxs-lookup"><span data-stu-id="dd071-259">minimum</span></span>
* <span data-ttu-id="dd071-260">maximum</span><span class="sxs-lookup"><span data-stu-id="dd071-260">maximum</span></span>
* <span data-ttu-id="dd071-261">ultimo valore raccolto</span><span class="sxs-lookup"><span data-stu-id="dd071-261">last-collected value</span></span>
* <span data-ttu-id="dd071-262">numero di esempi non elaborati usati per calcolare l'aggregazione</span><span class="sxs-lookup"><span data-stu-id="dd071-262">count of raw samples used to compute the aggregate</span></span>

<span data-ttu-id="dd071-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="dd071-263">Element</span></span> | <span data-ttu-id="dd071-264">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-264">Value</span></span>
------- | -----
<span data-ttu-id="dd071-265">sinks</span><span class="sxs-lookup"><span data-stu-id="dd071-265">sinks</span></span> | <span data-ttu-id="dd071-266">(facoltativo) Un elenco di nomi delimitato da virgole di sink a cui LAD invia i risultati di metrica aggregati.</span><span class="sxs-lookup"><span data-stu-id="dd071-266">(optional) A comma-separated list of names of sinks to which LAD sends aggregated metric results.</span></span> <span data-ttu-id="dd071-267">Tutte le metriche aggregate vengono pubblicate in ogni sink elencato.</span><span class="sxs-lookup"><span data-stu-id="dd071-267">All aggregated metrics are published to each listed sink.</span></span> <span data-ttu-id="dd071-268">Vedere [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="dd071-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="dd071-269">Esempio: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="dd071-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="dd071-270">type</span><span class="sxs-lookup"><span data-stu-id="dd071-270">type</span></span> | <span data-ttu-id="dd071-271">Identifica il provider effettivo della metrica.</span><span class="sxs-lookup"><span data-stu-id="dd071-271">Identifies the actual provider of the metric.</span></span>
<span data-ttu-id="dd071-272">class</span><span class="sxs-lookup"><span data-stu-id="dd071-272">class</span></span> | <span data-ttu-id="dd071-273">Con "counter" identifica la metrica specifica all'interno dello spazio dei nomi del provider.</span><span class="sxs-lookup"><span data-stu-id="dd071-273">Together with "counter", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="dd071-274">counter</span><span class="sxs-lookup"><span data-stu-id="dd071-274">counter</span></span> | <span data-ttu-id="dd071-275">Con "class" identifica la metrica specifica all'interno dello spazio dei nomi del provider.</span><span class="sxs-lookup"><span data-stu-id="dd071-275">Together with "class", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="dd071-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="dd071-276">counterSpecifier</span></span> | <span data-ttu-id="dd071-277">Identifica la metrica specifica all'interno dello spazio dei nomi di Metriche di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-277">Identifies the specific metric within the Azure Metrics namespace.</span></span>
<span data-ttu-id="dd071-278">condition</span><span class="sxs-lookup"><span data-stu-id="dd071-278">condition</span></span> | <span data-ttu-id="dd071-279">(facoltativo) Seleziona un'istanza specifica dell'oggetto a cui si applica la metrica oppure seleziona l'aggregazione in tutte le istanze di tale oggetto.</span><span class="sxs-lookup"><span data-stu-id="dd071-279">(optional) Selects a specific instance of the object to which the metric applies or selects the aggregation across all instances of that object.</span></span> <span data-ttu-id="dd071-280">Per ulteriori informazioni, vedere le [`builtin`definizioni delle metriche](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="dd071-280">For more information, see the [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="dd071-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="dd071-281">sampleRate</span></span> | <span data-ttu-id="dd071-282">Intervallo IS 8601 che imposta la frequenza con cui vengono raccolti gli esempi non elaborati per questa metrica.</span><span class="sxs-lookup"><span data-stu-id="dd071-282">IS 8601 interval that sets the rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="dd071-283">Se non viene impostata, l'intervallo di raccolta viene impostato dal valore di [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="dd071-283">If not set, the collection interval is set by the value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="dd071-284">La frequenza di esempio più piccola supportata è 15 secondi (PT15S).</span><span class="sxs-lookup"><span data-stu-id="dd071-284">The shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="dd071-285">unit</span><span class="sxs-lookup"><span data-stu-id="dd071-285">unit</span></span> | <span data-ttu-id="dd071-286">Deve essere una delle seguenti stringhe: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span><span class="sxs-lookup"><span data-stu-id="dd071-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="dd071-287">Definisce l'unità per la metrica.</span><span class="sxs-lookup"><span data-stu-id="dd071-287">Defines the unit for the metric.</span></span> <span data-ttu-id="dd071-288">Gli utenti dei dati raccolti prevedono che i valori dei dati raccolti corrispondano a questa unità.</span><span class="sxs-lookup"><span data-stu-id="dd071-288">Consumers of the collected data expect the collected data values to match this unit.</span></span> <span data-ttu-id="dd071-289">LAD ignora questo campo.</span><span class="sxs-lookup"><span data-stu-id="dd071-289">LAD ignores this field.</span></span>
<span data-ttu-id="dd071-290">displayName</span><span class="sxs-lookup"><span data-stu-id="dd071-290">displayName</span></span> | <span data-ttu-id="dd071-291">L'etichetta, nella lingua specificata dall'impostazione locale associata, da allegare a questi dati in Metriche di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-291">The label (in the language specified by the associated locale setting) to be attached to this data in Azure Metrics.</span></span> <span data-ttu-id="dd071-292">LAD ignora questo campo.</span><span class="sxs-lookup"><span data-stu-id="dd071-292">LAD ignores this field.</span></span>

<span data-ttu-id="dd071-293">counterSpecifier è un identificatore arbitrario.</span><span class="sxs-lookup"><span data-stu-id="dd071-293">The counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="dd071-294">Gli utenti di metriche, quali le funzionalità dei grafici del portale di Azure e gli avvisi, usano counterSpecifier come la "chiave" che identifica una metrica o un'istanza di una metrica.</span><span class="sxs-lookup"><span data-stu-id="dd071-294">Consumers of metrics, like the Azure portal charting and alerting feature, use counterSpecifier as the "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="dd071-295">Per le metriche `builtin`, è consigliabile usare i valori di counterSpecifier che iniziano con `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="dd071-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="dd071-296">Se si raccoglie un'istanza specifica di una metrica, è consigliabile allegare l'identificatore dell'istanza del valore counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="dd071-296">If you are collecting a specific instance of a metric, we recommend you attach the identifier of the instance to the counterSpecifier value.</span></span> <span data-ttu-id="dd071-297">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="dd071-297">Some examples:</span></span>

* <span data-ttu-id="dd071-298">`/builtin/Processor/PercentIdleTime` - Tempo di inattività medio calcolato per tutti i core</span><span class="sxs-lookup"><span data-stu-id="dd071-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="dd071-299">`/builtin/Disk/FreeSpace(/mnt)` - Spazio libero per il file system /mnt</span><span class="sxs-lookup"><span data-stu-id="dd071-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for the /mnt filesystem</span></span>
* <span data-ttu-id="dd071-300">`/builtin/Disk/FreeSpace` - Spazio libero medio calcolato per tutti i file system montati</span><span class="sxs-lookup"><span data-stu-id="dd071-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="dd071-301">Né per LAD né per il portale di Azure si prevede che il valore di counterSpecifier corrisponda a un modello.</span><span class="sxs-lookup"><span data-stu-id="dd071-301">Neither LAD nor the Azure portal expects the counterSpecifier value to match any pattern.</span></span> <span data-ttu-id="dd071-302">È consigliabile essere coerenti durante la creazione dei valori di counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="dd071-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="dd071-303">Quando si specifica `performanceCounters`, LAD scrive sempre i dati in una tabella nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-303">When you specify `performanceCounters`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="dd071-304">È possibile che gli stessi dati vengano scritti nel BLOB JSON e/o negli hub eventi, ma non è possibile disabilitare l'inserimento dei dati in una tabella.</span><span class="sxs-lookup"><span data-stu-id="dd071-304">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="dd071-305">Tutte le istanze dell'estensione di diagnostica configurate per l'uso dello stesso nome per l'account di archiviazione e dello stesso endpoint aggiungono le metriche e i registri alla stessa tabella.</span><span class="sxs-lookup"><span data-stu-id="dd071-305">All instances of the diagnostic extension configured to use the same storage account name and endpoint add their metrics and logs to the same table.</span></span> <span data-ttu-id="dd071-306">Se troppe macchine virtuali scrivono nella stessa partizione di tabella, Azure può limitare le scritture per tale partizione.</span><span class="sxs-lookup"><span data-stu-id="dd071-306">If too many VMs are writing to the same table partition, Azure can throttle writes to that partition.</span></span> <span data-ttu-id="dd071-307">L'impostazione eventVolume fa in modo che le voci si diffondano tra 1 (Piccolo), 10 (Medio) o 100 (Grande) partizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="dd071-307">The eventVolume setting causes entries to be spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="dd071-308">In genere, "Medio" è sufficiente a garantire che il traffico non venga limitato.</span><span class="sxs-lookup"><span data-stu-id="dd071-308">Usually, "Medium" is sufficient to ensure traffic is not throttled.</span></span> <span data-ttu-id="dd071-309">La funzionalità Metriche di Azure del portale di Azure usa i dati in questa tabella per creare grafici o per attivare gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="dd071-309">The Azure Metrics feature of the Azure portal uses the data in this table to produce graphs or to trigger alerts.</span></span> <span data-ttu-id="dd071-310">Il nome della tabella è la concatenazione delle stringhe seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd071-310">The table name is the concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="dd071-311">"scheduledTransferPeriod" per i valori aggregati inseriti nella tabella</span><span class="sxs-lookup"><span data-stu-id="dd071-311">The "scheduledTransferPeriod" for the aggregated values stored in the table</span></span>
* `P10DV2S`
* <span data-ttu-id="dd071-312">Una data nel formato "AAAAMMGG", che cambia ogni 10 giorni</span><span class="sxs-lookup"><span data-stu-id="dd071-312">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="dd071-313">Gli esempi includono `WADMetricsPT1HP10DV2S20170410` e `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="dd071-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="dd071-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="dd071-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="dd071-315">Questa sezione facoltativa consente di controllare la raccolta degli eventi del registro di SysLog.</span><span class="sxs-lookup"><span data-stu-id="dd071-315">This optional section controls the collection of log events from syslog.</span></span> <span data-ttu-id="dd071-316">Se viene omessa, gli eventi di SysLog non vengono acquisiti.</span><span class="sxs-lookup"><span data-stu-id="dd071-316">If the section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="dd071-317">La raccolta syslogEventConfiguration ha una voce per ogni impianto di interesse di SysLog.</span><span class="sxs-lookup"><span data-stu-id="dd071-317">The syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="dd071-318">Se minSeverity è "NONE" per un particolare impianto o se tale impianto non viene visualizzato nell'elemento, non viene acquisito alcun evento da tale impianto.</span><span class="sxs-lookup"><span data-stu-id="dd071-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in the element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="dd071-319">Elemento</span><span class="sxs-lookup"><span data-stu-id="dd071-319">Element</span></span> | <span data-ttu-id="dd071-320">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-320">Value</span></span>
------- | -----
<span data-ttu-id="dd071-321">sinks</span><span class="sxs-lookup"><span data-stu-id="dd071-321">sinks</span></span> | <span data-ttu-id="dd071-322">Un elenco delimitato da virgole di nomi di sink in cui vengono pubblicati i singoli eventi del registro.</span><span class="sxs-lookup"><span data-stu-id="dd071-322">A comma-separated list of names of sinks to which individual log events are published.</span></span> <span data-ttu-id="dd071-323">Tutti gli eventi del registro corrispondenti alle restrizioni in syslogEventConfiguration vengono pubblicati in tutti i sink elencati.</span><span class="sxs-lookup"><span data-stu-id="dd071-323">All log events matching the restrictions in syslogEventConfiguration are published to each listed sink.</span></span> <span data-ttu-id="dd071-324">Esempio: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="dd071-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="dd071-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="dd071-325">facilityName</span></span> | <span data-ttu-id="dd071-326">Un nome dell'impianto SysLog, ad esempio "LOG\_USER" o "LOG\_LOCAL0".</span><span class="sxs-lookup"><span data-stu-id="dd071-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="dd071-327">Per un elenco completo vedere la sezione "impianto" della [pagina di manuale SysLog](http://man7.org/linux/man-pages/man3/syslog.3.html).</span><span class="sxs-lookup"><span data-stu-id="dd071-327">See the "facility" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span>
<span data-ttu-id="dd071-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="dd071-328">minSeverity</span></span> | <span data-ttu-id="dd071-329">Un livello di gravità SysLog, ad esempio "LOG\_ERR" o "LOG\_INFO".</span><span class="sxs-lookup"><span data-stu-id="dd071-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="dd071-330">Per un elenco completo vedere la sezione "livello" della [pagina di manuale SysLog](http://man7.org/linux/man-pages/man3/syslog.3.html).</span><span class="sxs-lookup"><span data-stu-id="dd071-330">See the "level" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span> <span data-ttu-id="dd071-331">L'estensione acquisisce gli eventi inviati all'impianto con livello superiore o uguale a quello specificato.</span><span class="sxs-lookup"><span data-stu-id="dd071-331">The extension captures events sent to the facility at or above the specified level.</span></span>

<span data-ttu-id="dd071-332">Quando si specifica `syslogEvents`, LAD scrive sempre i dati in una tabella nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-332">When you specify `syslogEvents`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="dd071-333">È possibile che gli stessi dati vengano scritti nel BLOB JSON e/o negli hub eventi, ma non è possibile disabilitare l'inserimento dei dati in una tabella.</span><span class="sxs-lookup"><span data-stu-id="dd071-333">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="dd071-334">Il comportamento del partizionamento per questa tabella è identico a quello descritto per `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="dd071-334">The partitioning behavior for this table is the same as described for `performanceCounters`.</span></span> <span data-ttu-id="dd071-335">Il nome della tabella è la concatenazione delle stringhe seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd071-335">The table name is the concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="dd071-336">Una data nel formato "AAAAMMGG", che cambia ogni 10 giorni</span><span class="sxs-lookup"><span data-stu-id="dd071-336">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="dd071-337">Gli esempi includono `LinuxSyslog20170410` e `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="dd071-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="dd071-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="dd071-338">perfCfg</span></span>

<span data-ttu-id="dd071-339">Questa sezione facoltativa consente di controllare l'esecuzione delle query arbitrarie [OMI](https://github.com/Microsoft/omi).</span><span class="sxs-lookup"><span data-stu-id="dd071-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="dd071-340">Elemento</span><span class="sxs-lookup"><span data-stu-id="dd071-340">Element</span></span> | <span data-ttu-id="dd071-341">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-341">Value</span></span>
------- | -----
<span data-ttu-id="dd071-342">namespace</span><span class="sxs-lookup"><span data-stu-id="dd071-342">namespace</span></span> | <span data-ttu-id="dd071-343">(facoltativo) Lo spazio dei nomi OMI entro il quale deve essere eseguita la query.</span><span class="sxs-lookup"><span data-stu-id="dd071-343">(optional) The OMI namespace within which the query should be executed.</span></span> <span data-ttu-id="dd071-344">Se non viene specificato, il valore predefinito è "root/scx", implementato dai [provider multipiattaforma dei System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="dd071-344">If unspecified, the default value is "root/scx", implemented by the [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="dd071-345">query</span><span class="sxs-lookup"><span data-stu-id="dd071-345">query</span></span> | <span data-ttu-id="dd071-346">La query OMI da eseguire.</span><span class="sxs-lookup"><span data-stu-id="dd071-346">The OMI query to be executed.</span></span>
<span data-ttu-id="dd071-347">tabella</span><span class="sxs-lookup"><span data-stu-id="dd071-347">table</span></span> | <span data-ttu-id="dd071-348">(facoltativo) La tabella di archiviazione di Azure, nell'account di archiviazione designato. Vedere [Impostazioni protette](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="dd071-348">(optional) The Azure storage table, in the designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="dd071-349">frequency</span><span class="sxs-lookup"><span data-stu-id="dd071-349">frequency</span></span> | <span data-ttu-id="dd071-350">(facoltativo) Il numero di secondi tra le esecuzioni della query.</span><span class="sxs-lookup"><span data-stu-id="dd071-350">(optional) The number of seconds between execution of the query.</span></span> <span data-ttu-id="dd071-351">Il valore predefinito è 300, ovvero 5 minuti; il valore minimo è 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="dd071-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="dd071-352">sinks</span><span class="sxs-lookup"><span data-stu-id="dd071-352">sinks</span></span> | <span data-ttu-id="dd071-353">(facoltativo) Un elenco di nomi delimitato da virgole di sink aggiuntivi in cui pubblicare i risultati di metrica di esempio non elaborati.</span><span class="sxs-lookup"><span data-stu-id="dd071-353">(optional) A comma-separated list of names of additional sinks to which raw sample metric results should be published.</span></span> <span data-ttu-id="dd071-354">Nessuna aggregazione di questi esempi non elaborati viene calcolata dall'estensione o da Metriche di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-354">No aggregation of these raw samples is computed by the extension or by Azure Metrics.</span></span>

<span data-ttu-id="dd071-355">È necessario specificare "table" o "sink" o entrambi.</span><span class="sxs-lookup"><span data-stu-id="dd071-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="dd071-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="dd071-356">fileLogs</span></span>

<span data-ttu-id="dd071-357">Consente di controllare l'acquisizione dei file di registro.</span><span class="sxs-lookup"><span data-stu-id="dd071-357">Controls the capture of log files.</span></span> <span data-ttu-id="dd071-358">LAD acquisisce le nuove righe di testo quando vengono scritte nel file e le scrive nelle righe della tabella e/o nei sink specificati, JsonBlob o EventHub.</span><span class="sxs-lookup"><span data-stu-id="dd071-358">LAD captures new text lines as they are written to the file and writes them to table rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="dd071-359">Elemento</span><span class="sxs-lookup"><span data-stu-id="dd071-359">Element</span></span> | <span data-ttu-id="dd071-360">Valore</span><span class="sxs-lookup"><span data-stu-id="dd071-360">Value</span></span>
------- | -----
<span data-ttu-id="dd071-361">file</span><span class="sxs-lookup"><span data-stu-id="dd071-361">file</span></span> | <span data-ttu-id="dd071-362">Il percorso completo del file di registro da esaminate e acquisire.</span><span class="sxs-lookup"><span data-stu-id="dd071-362">The full pathname of the log file to be watched and captured.</span></span> <span data-ttu-id="dd071-363">Il percorso deve indicare solo un file. Non è possibile indicare una directory o i caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="dd071-363">The pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="dd071-364">tabella</span><span class="sxs-lookup"><span data-stu-id="dd071-364">table</span></span> | <span data-ttu-id="dd071-365">(facoltativo) La tabella di archiviazione di Azure, nell'account di archiviazione designato, come specificato nella configurazione protetta, in cui vengono scritte nuove righe dalla "coda" del file.</span><span class="sxs-lookup"><span data-stu-id="dd071-365">(optional) The Azure storage table, in the designated storage account (as specified in the protected configuration), into which new lines from the "tail" of the file are written.</span></span>
<span data-ttu-id="dd071-366">sinks</span><span class="sxs-lookup"><span data-stu-id="dd071-366">sinks</span></span> | <span data-ttu-id="dd071-367">(facoltativo) Un elenco di nomi delimitato da virgole di sink aggiuntivi a cui vengono inviate le righe del registro.</span><span class="sxs-lookup"><span data-stu-id="dd071-367">(optional) A comma-separated list of names of additional sinks to which log lines sent.</span></span>

<span data-ttu-id="dd071-368">È necessario specificare "table" o "sink" o entrambi.</span><span class="sxs-lookup"><span data-stu-id="dd071-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-the-builtin-provider"></a><span data-ttu-id="dd071-369">Metriche supportate dal provider Builtin</span><span class="sxs-lookup"><span data-stu-id="dd071-369">Metrics supported by the builtin provider</span></span>

<span data-ttu-id="dd071-370">Il provider di metriche Builtin è un'origine metriche più interessante per molti utenti.</span><span class="sxs-lookup"><span data-stu-id="dd071-370">The builtin metric provider is a source of metrics most interesting to a broad set of users.</span></span> <span data-ttu-id="dd071-371">Queste metriche sono suddivise in cinque grandi categorie:</span><span class="sxs-lookup"><span data-stu-id="dd071-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="dd071-372">Processore</span><span class="sxs-lookup"><span data-stu-id="dd071-372">Processor</span></span>
* <span data-ttu-id="dd071-373">Memoria</span><span class="sxs-lookup"><span data-stu-id="dd071-373">Memory</span></span>
* <span data-ttu-id="dd071-374">Rete</span><span class="sxs-lookup"><span data-stu-id="dd071-374">Network</span></span>
* <span data-ttu-id="dd071-375">File system</span><span class="sxs-lookup"><span data-stu-id="dd071-375">Filesystem</span></span>
* <span data-ttu-id="dd071-376">Disco</span><span class="sxs-lookup"><span data-stu-id="dd071-376">Disk</span></span>

### <a name="builtin-metrics-for-the-processor-class"></a><span data-ttu-id="dd071-377">Metriche Builtin per la classe Processore</span><span class="sxs-lookup"><span data-stu-id="dd071-377">builtin metrics for the Processor class</span></span>

<span data-ttu-id="dd071-378">La classe di metriche Processore offre informazioni sull'uso del processore nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd071-378">The Processor class of metrics provides information about processor usage in the VM.</span></span> <span data-ttu-id="dd071-379">Quando si aggregano le percentuali, il risultato è la media di tutte le CPU.</span><span class="sxs-lookup"><span data-stu-id="dd071-379">When aggregating percentages, the result is the average across all CPUs.</span></span> <span data-ttu-id="dd071-380">In una macchina virtuale a due core, se un core è completamente occupato, ma l'altro è completamente inattivo, il valore di PercentIdleTime restituito sarà 50.</span><span class="sxs-lookup"><span data-stu-id="dd071-380">In a two core VM, if one core was 100% busy and the other was 100% idle, the reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="dd071-381">Se ciascun core è occupato al 50% per lo stesso periodo, il risultato restituito sarà ugualmente 50.</span><span class="sxs-lookup"><span data-stu-id="dd071-381">If each core was 50% busy for the same period, the reported result would also be 50.</span></span> <span data-ttu-id="dd071-382">In una macchina virtuale a due core, se un core è completamente occupato, ma gli altri sono inattivo, il valore di PercentIdleTime restituito sarà 75.</span><span class="sxs-lookup"><span data-stu-id="dd071-382">In a four core VM, with one core 100% busy and the others idle, the reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="dd071-383">counter</span><span class="sxs-lookup"><span data-stu-id="dd071-383">counter</span></span> | <span data-ttu-id="dd071-384">Significato</span><span class="sxs-lookup"><span data-stu-id="dd071-384">Meaning</span></span>
------- | -------
<span data-ttu-id="dd071-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="dd071-385">PercentIdleTime</span></span> | <span data-ttu-id="dd071-386">Percentuale di tempo nella finestra di aggregazione durante la quale i processori hanno eseguito il ciclo inattivo del kernel</span><span class="sxs-lookup"><span data-stu-id="dd071-386">Percentage of time during the aggregation window that processors were executing the kernel idle loop</span></span>
<span data-ttu-id="dd071-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="dd071-387">PercentProcessorTime</span></span> | <span data-ttu-id="dd071-388">Percentuale di tempo di esecuzione di un thread non inattivo</span><span class="sxs-lookup"><span data-stu-id="dd071-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="dd071-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="dd071-389">PercentIOWaitTime</span></span> | <span data-ttu-id="dd071-390">Percentuale di tempo di attesa per il completamento delle operazioni di input/output</span><span class="sxs-lookup"><span data-stu-id="dd071-390">Percentage of time waiting for IO operations to complete</span></span>
<span data-ttu-id="dd071-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="dd071-391">PercentInterruptTime</span></span> | <span data-ttu-id="dd071-392">Percentuale di tempo per l'esecuzione di DPC, ovvero chiamate di procedura differite, e interruzioni di hardware o software</span><span class="sxs-lookup"><span data-stu-id="dd071-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="dd071-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="dd071-393">PercentUserTime</span></span> | <span data-ttu-id="dd071-394">Relativamente al tempo di inattività nella finestra di aggregazione, la percentuale di tempo impiegato dall'utente con priorità normale</span><span class="sxs-lookup"><span data-stu-id="dd071-394">Of non-idle time during the aggregation window, the percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="dd071-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="dd071-395">PercentNiceTime</span></span> | <span data-ttu-id="dd071-396">Relativamente al tempo di inattività, la percentuale di tempo impiegata a bassa priorità (interessante)</span><span class="sxs-lookup"><span data-stu-id="dd071-396">Of non-idle time, the percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="dd071-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="dd071-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="dd071-398">La percentuale di tempo di inattività impiegata in modalità privilegiata (kernel)</span><span class="sxs-lookup"><span data-stu-id="dd071-398">Of non-idle time, the percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="dd071-399">La somma dei primi quattro contatori deve essere 100%.</span><span class="sxs-lookup"><span data-stu-id="dd071-399">The first four counters should sum to 100%.</span></span> <span data-ttu-id="dd071-400">Anche la somma degli ultimi tre contatori deve essere 100%: vengono sommati i valori di PercentProcessorTime, PercentIOWaitTime e PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="dd071-400">The last three counters also sum to 100%; they subdivide the sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="dd071-401">Per ottenere un'unica metrica aggregata per tutti i processori, impostare `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="dd071-401">To obtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="dd071-402">Per ottenere una metrica per un processore specifico, ad esempio per il secondo processore logico di una macchina virtuale a quattro core, impostare `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="dd071-402">To obtain a metric for a specific processor, such as the second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="dd071-403">I valori del processore logico sono compresi nell'intervallo `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="dd071-403">Logical processor numbers are in the range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-the-memory-class"></a><span data-ttu-id="dd071-404">Metriche Builtin per la classe Memoria</span><span class="sxs-lookup"><span data-stu-id="dd071-404">builtin metrics for the Memory class</span></span>

<span data-ttu-id="dd071-405">La classe di memoria delle metriche contiene informazioni sull'uso della memoria, il paging e lo scambio.</span><span class="sxs-lookup"><span data-stu-id="dd071-405">The Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="dd071-406">counter</span><span class="sxs-lookup"><span data-stu-id="dd071-406">counter</span></span> | <span data-ttu-id="dd071-407">Significato</span><span class="sxs-lookup"><span data-stu-id="dd071-407">Meaning</span></span>
------- | -------
<span data-ttu-id="dd071-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="dd071-408">AvailableMemory</span></span> | <span data-ttu-id="dd071-409">Memoria fisica disponibile in MiB</span><span class="sxs-lookup"><span data-stu-id="dd071-409">Available physical memory in MiB</span></span>
<span data-ttu-id="dd071-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="dd071-410">PercentAvailableMemory</span></span> | <span data-ttu-id="dd071-411">Percentuale della memoria totale che indica la memoria fisica disponibile</span><span class="sxs-lookup"><span data-stu-id="dd071-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="dd071-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="dd071-412">UsedMemory</span></span> | <span data-ttu-id="dd071-413">Memoria fisica in uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="dd071-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="dd071-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="dd071-414">PercentUsedMemory</span></span> | <span data-ttu-id="dd071-415">Percentuale della memoria totale che indica la memoria fisica in uso</span><span class="sxs-lookup"><span data-stu-id="dd071-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="dd071-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="dd071-416">PagesPerSec</span></span> | <span data-ttu-id="dd071-417">Paging totale (lettura/scrittura)</span><span class="sxs-lookup"><span data-stu-id="dd071-417">Total paging (read/write)</span></span>
<span data-ttu-id="dd071-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="dd071-418">PagesReadPerSec</span></span> | <span data-ttu-id="dd071-419">Pagine lette dall'archivio di backup, ad esempio file di scambio, file di programma, file mappato e così via.</span><span class="sxs-lookup"><span data-stu-id="dd071-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="dd071-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="dd071-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="dd071-421">Pagine scritte nell'archivio di backup, ad esempio file di scambio, file mappato e così via.</span><span class="sxs-lookup"><span data-stu-id="dd071-421">Pages written to backing store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="dd071-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="dd071-422">AvailableSwap</span></span> | <span data-ttu-id="dd071-423">Spazio di swapping inutilizzato (MiB)</span><span class="sxs-lookup"><span data-stu-id="dd071-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="dd071-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="dd071-424">PercentAvailableSwap</span></span> | <span data-ttu-id="dd071-425">Percentuale dello swapping totale che indica lo spazio di swapping inutilizzato</span><span class="sxs-lookup"><span data-stu-id="dd071-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="dd071-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="dd071-426">UsedSwap</span></span> | <span data-ttu-id="dd071-427">Spazio di swapping in uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="dd071-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="dd071-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="dd071-428">PercentUsedSwap</span></span> | <span data-ttu-id="dd071-429">Percentuale dello swapping totale che indica lo spazio di swapping in uso</span><span class="sxs-lookup"><span data-stu-id="dd071-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="dd071-430">Questa classe di metriche presenta una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="dd071-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="dd071-431">L'attributo "condition" non presenta impostazioni utili e deve essere omesso.</span><span class="sxs-lookup"><span data-stu-id="dd071-431">The "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-the-network-class"></a><span data-ttu-id="dd071-432">Metriche Builtin per la classe Rete</span><span class="sxs-lookup"><span data-stu-id="dd071-432">builtin metrics for the Network class</span></span>

<span data-ttu-id="dd071-433">La classe di metriche Rete contiene informazioni sulle attività di rete su un interfacce di rete singole sin dall'avvio.</span><span class="sxs-lookup"><span data-stu-id="dd071-433">The Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="dd071-434">LAD non espone le metriche relative alla larghezza di banda, che possono essere recuperate dalle metriche dell'host.</span><span class="sxs-lookup"><span data-stu-id="dd071-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="dd071-435">counter</span><span class="sxs-lookup"><span data-stu-id="dd071-435">counter</span></span> | <span data-ttu-id="dd071-436">Significato</span><span class="sxs-lookup"><span data-stu-id="dd071-436">Meaning</span></span>
------- | -------
<span data-ttu-id="dd071-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="dd071-437">BytesTransmitted</span></span> | <span data-ttu-id="dd071-438">Byte totali inviati sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="dd071-438">Total bytes sent since boot</span></span>
<span data-ttu-id="dd071-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="dd071-439">BytesReceived</span></span> | <span data-ttu-id="dd071-440">Byte totali ricevuti sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="dd071-440">Total bytes received since boot</span></span>
<span data-ttu-id="dd071-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="dd071-441">BytesTotal</span></span> | <span data-ttu-id="dd071-442">Byte totali inviati o ricevuti sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="dd071-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="dd071-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="dd071-443">PacketsTransmitted</span></span> | <span data-ttu-id="dd071-444">Pacchetti totali inviati sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="dd071-444">Total packets sent since boot</span></span>
<span data-ttu-id="dd071-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="dd071-445">PacketsReceived</span></span> | <span data-ttu-id="dd071-446">Pacchetti totali ricevuti sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="dd071-446">Total packets received since boot</span></span>
<span data-ttu-id="dd071-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="dd071-447">TotalRxErrors</span></span> | <span data-ttu-id="dd071-448">Numero di errori di ricezione sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="dd071-448">Number of receive errors since boot</span></span>
<span data-ttu-id="dd071-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="dd071-449">TotalTxErrors</span></span> | <span data-ttu-id="dd071-450">Numero di errori di trasmissione sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="dd071-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="dd071-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="dd071-451">TotalCollisions</span></span> | <span data-ttu-id="dd071-452">Numero di conflitti segnalati tramite le porte di rete sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="dd071-452">Number of collisions reported by the network ports since boot</span></span>

 <span data-ttu-id="dd071-453">Anche se questa classe presenta un'istanza, LAD non supporta l'acquisizione delle metriche di rete aggregate per tutti i dispositivi di rete.</span><span class="sxs-lookup"><span data-stu-id="dd071-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="dd071-454">Per ottenere le metriche per un'interfaccia specifica, ad esempio eth0, impostare `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="dd071-454">To obtain the metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-the-filesystem-class"></a><span data-ttu-id="dd071-455">Metriche Builtin per la classe File system</span><span class="sxs-lookup"><span data-stu-id="dd071-455">builtin metrics for the Filesystem class</span></span>

<span data-ttu-id="dd071-456">La classe di metriche File system contiene informazioni sull'uso del file system.</span><span class="sxs-lookup"><span data-stu-id="dd071-456">The Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="dd071-457">I valori assoluti e in percentuale vengono segnalati come fossero visualizzati da utenti normali, non radice.</span><span class="sxs-lookup"><span data-stu-id="dd071-457">Absolute and percentage values are reported as they'd be displayed to an ordinary user (not root).</span></span>

<span data-ttu-id="dd071-458">counter</span><span class="sxs-lookup"><span data-stu-id="dd071-458">counter</span></span> | <span data-ttu-id="dd071-459">Significato</span><span class="sxs-lookup"><span data-stu-id="dd071-459">Meaning</span></span>
------- | -------
<span data-ttu-id="dd071-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="dd071-460">FreeSpace</span></span> | <span data-ttu-id="dd071-461">Spazio disponibile su disco in byte</span><span class="sxs-lookup"><span data-stu-id="dd071-461">Available disk space in bytes</span></span>
<span data-ttu-id="dd071-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="dd071-462">UsedSpace</span></span> | <span data-ttu-id="dd071-463">Spazio su disco usato in byte</span><span class="sxs-lookup"><span data-stu-id="dd071-463">Used disk space in bytes</span></span>
<span data-ttu-id="dd071-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="dd071-464">PercentFreeSpace</span></span> | <span data-ttu-id="dd071-465">Percentuale di spazio libero</span><span class="sxs-lookup"><span data-stu-id="dd071-465">Percentage free space</span></span>
<span data-ttu-id="dd071-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="dd071-466">PercentUsedSpace</span></span> | <span data-ttu-id="dd071-467">Percentuale di spazio usato</span><span class="sxs-lookup"><span data-stu-id="dd071-467">Percentage used space</span></span>
<span data-ttu-id="dd071-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="dd071-468">PercentFreeInodes</span></span> | <span data-ttu-id="dd071-469">Percentuale di inode non usati</span><span class="sxs-lookup"><span data-stu-id="dd071-469">Percentage of unused inodes</span></span>
<span data-ttu-id="dd071-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="dd071-470">PercentUsedInodes</span></span> | <span data-ttu-id="dd071-471">Percentuale di inode allocati, ovvero in uso, sommati tra tutti i file System</span><span class="sxs-lookup"><span data-stu-id="dd071-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="dd071-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-472">BytesReadPerSecond</span></span> | <span data-ttu-id="dd071-473">Byte letti per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-473">Bytes read per second</span></span>
<span data-ttu-id="dd071-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="dd071-475">Byte scritti per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-475">Bytes written per second</span></span>
<span data-ttu-id="dd071-476">Byte al secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-476">BytesPerSecond</span></span> | <span data-ttu-id="dd071-477">Byte letti o scritti per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-477">Bytes read or written per second</span></span>
<span data-ttu-id="dd071-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-478">ReadsPerSecond</span></span> | <span data-ttu-id="dd071-479">Operazioni di lettura per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-479">Read operations per second</span></span>
<span data-ttu-id="dd071-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-480">WritesPerSecond</span></span> | <span data-ttu-id="dd071-481">Operazioni di scrittura per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-481">Write operations per second</span></span>
<span data-ttu-id="dd071-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-482">TransfersPerSecond</span></span> | <span data-ttu-id="dd071-483">Operazioni di lettura o scrittura per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-483">Read or write operations per second</span></span>

<span data-ttu-id="dd071-484">È possibile ottenere i valori aggregati in tutti i file System impostando `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="dd071-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="dd071-485">È possibile ottenere i valori per un determinato file system montato, ad esempio "/mnt", può essere ottenuto impostando `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="dd071-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-the-disk-class"></a><span data-ttu-id="dd071-486">Metriche Builtin per la classe Disco</span><span class="sxs-lookup"><span data-stu-id="dd071-486">builtin metrics for the Disk class</span></span>

<span data-ttu-id="dd071-487">La classe di metriche Disco contiene informazioni sull'uso del dispositivo del disco.</span><span class="sxs-lookup"><span data-stu-id="dd071-487">The Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="dd071-488">Queste statistiche si applicano all'intera unità.</span><span class="sxs-lookup"><span data-stu-id="dd071-488">These statistics apply to the entire drive.</span></span> <span data-ttu-id="dd071-489">Se sono presenti più file System su un dispositivo, i contatori per il dispositivo sono aggregati in modo efficace per tutti loro.</span><span class="sxs-lookup"><span data-stu-id="dd071-489">If there are multiple file systems on a device, the counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="dd071-490">counter</span><span class="sxs-lookup"><span data-stu-id="dd071-490">counter</span></span> | <span data-ttu-id="dd071-491">Significato</span><span class="sxs-lookup"><span data-stu-id="dd071-491">Meaning</span></span>
------- | -------
<span data-ttu-id="dd071-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-492">ReadsPerSecond</span></span> | <span data-ttu-id="dd071-493">Operazioni di lettura per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-493">Read operations per second</span></span>
<span data-ttu-id="dd071-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-494">WritesPerSecond</span></span> | <span data-ttu-id="dd071-495">Operazioni di scrittura per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-495">Write operations per second</span></span>
<span data-ttu-id="dd071-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-496">TransfersPerSecond</span></span> | <span data-ttu-id="dd071-497">Operazioni totali per secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-497">Total operations per second</span></span>
<span data-ttu-id="dd071-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="dd071-498">AverageReadTime</span></span> | <span data-ttu-id="dd071-499">Media di secondi per operazione di lettura</span><span class="sxs-lookup"><span data-stu-id="dd071-499">Average seconds per read operation</span></span>
<span data-ttu-id="dd071-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="dd071-500">AverageWriteTime</span></span> | <span data-ttu-id="dd071-501">Media di secondi per operazione di scrittura</span><span class="sxs-lookup"><span data-stu-id="dd071-501">Average seconds per write operation</span></span>
<span data-ttu-id="dd071-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="dd071-502">AverageTransferTime</span></span> | <span data-ttu-id="dd071-503">Media di secondi per operazione</span><span class="sxs-lookup"><span data-stu-id="dd071-503">Average seconds per operation</span></span>
<span data-ttu-id="dd071-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="dd071-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="dd071-505">Media delle operazioni del disco in coda</span><span class="sxs-lookup"><span data-stu-id="dd071-505">Average number of queued disk operations</span></span>
<span data-ttu-id="dd071-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="dd071-507">Numero di byte letti al secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-507">Number of bytes read per second</span></span>
<span data-ttu-id="dd071-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="dd071-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="dd071-509">Numero di byte scritti al secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-509">Number of bytes written per second</span></span>
<span data-ttu-id="dd071-510">Byte al secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-510">BytesPerSecond</span></span> | <span data-ttu-id="dd071-511">Numero di byte letti o scritti al secondo</span><span class="sxs-lookup"><span data-stu-id="dd071-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="dd071-512">È possibile ottenere i valori aggregati per tutti i dischi impostando `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="dd071-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="dd071-513">Per ottenere le informazioni per un dispositivo specifico, ad esempio dev/sdf1, impostare `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="dd071-513">To get information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="dd071-514">Installazione e configurazione di LAD 3.0 tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="dd071-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="dd071-515">Supponendo che le impostazioni protette si trovino nel file PrivateConfig.json e che le informazioni di configurazione pubbliche si trovino in PublicConfig.json, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="dd071-515">Assuming your protected settings are in the file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="dd071-516">Il comando presuppone che si stia usando la modalità di Gestione risorse di Azure (arm) dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-516">The command assumes you are using the Azure Resource Management mode (arm) of the Azure CLI.</span></span> <span data-ttu-id="dd071-517">Per configurare LAD per le macchine virtuali che usano il modello di distribuzione classico (ASM), passare alla modalità "asm" (`azure config mode asm`) e omettere il nome del gruppo di risorse nel comando.</span><span class="sxs-lookup"><span data-stu-id="dd071-517">To configure LAD for classic deployment model (ASM) VMs, switch to "asm" mode (`azure config mode asm`) and omit the resource group name in the command.</span></span> <span data-ttu-id="dd071-518">Per altre informazioni, vedere la [documentazione sull'interfaccia della riga di comando multipiattaforma](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="dd071-518">For more information, see the [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="dd071-519">Una configurazione di LAD 3.0 di esempio</span><span class="sxs-lookup"><span data-stu-id="dd071-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="dd071-520">In base alle definizioni precedenti, ecco una configurazione dell'estensione 3.0 LAD di esempio con alcune spiegazioni.</span><span class="sxs-lookup"><span data-stu-id="dd071-520">Based on the preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="dd071-521">Per applicare questo esempio al caso in questione, è necessario usare il nome dell'account di archiviazione, il token SAS dell'account e i token SAS di EventHubs.</span><span class="sxs-lookup"><span data-stu-id="dd071-521">To apply this sample to your case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="dd071-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="dd071-522">PrivateConfig.json</span></span>

<span data-ttu-id="dd071-523">Queste impostazioni private consentono di configurare:</span><span class="sxs-lookup"><span data-stu-id="dd071-523">These private settings configure:</span></span>

* <span data-ttu-id="dd071-524">un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="dd071-524">a storage account</span></span>
* <span data-ttu-id="dd071-525">un token SAS dell'account corrispondente</span><span class="sxs-lookup"><span data-stu-id="dd071-525">a matching account SAS token</span></span>
* <span data-ttu-id="dd071-526">diversi sink, ad esempio JsonBlob o EventHubs con i token SAS</span><span class="sxs-lookup"><span data-stu-id="dd071-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="dd071-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="dd071-527">PublicConfig.json</span></span>

<span data-ttu-id="dd071-528">Con queste impostazioni pubbliche il LAD:</span><span class="sxs-lookup"><span data-stu-id="dd071-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="dd071-529">carica le metriche della percentuale di tempo del processore e dello spazio sul disco usato nella tabella `WADMetrics*`</span><span class="sxs-lookup"><span data-stu-id="dd071-529">Upload percent-processor-time and used-disk-space metrics to the `WADMetrics*` table</span></span>
* <span data-ttu-id="dd071-530">carica i messaggi delle "informazioni" sull'"utente" e sulla gravità dell'impianto SysLog nella tabella `LinuxSyslog*`</span><span class="sxs-lookup"><span data-stu-id="dd071-530">Upload messages from syslog facility "user" and severity "info" to the `LinuxSyslog*` table</span></span>
* <span data-ttu-id="dd071-531">carica i risultati delle query OMI non elaborati, ovvero PercentProcessorTime e PercentIdleTime, nella tabella denominata `LinuxCPU`</span><span class="sxs-lookup"><span data-stu-id="dd071-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) to the named `LinuxCPU` table</span></span>
* <span data-ttu-id="dd071-532">carica le righe aggiunte nel file `/var/log/myladtestlog` nella tabella `MyLadTestLog`</span><span class="sxs-lookup"><span data-stu-id="dd071-532">Upload appended lines in file `/var/log/myladtestlog` to the `MyLadTestLog` table</span></span>

<span data-ttu-id="dd071-533">In ogni caso, i dati vengono anche caricati:</span><span class="sxs-lookup"><span data-stu-id="dd071-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="dd071-534">nell'archivio BLOB di Azure, il nome del contenitore è definito nel sink JsonBlob</span><span class="sxs-lookup"><span data-stu-id="dd071-534">Azure Blob storage (container name is as defined in the JsonBlob sink)</span></span>
* <span data-ttu-id="dd071-535">nell'endopint EventHubs, come specificato nel sink EventHubs</span><span class="sxs-lookup"><span data-stu-id="dd071-535">EventHubs endpoint (as specified in the EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="dd071-536">Nella configurazione `resourceId` deve corrispondere al valore della macchina virtuale o al valore del set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd071-536">The `resourceId` in the configuration must match that of the VM or the virtual machine scale set.</span></span>

* <span data-ttu-id="dd071-537">I valori di resourceId della macchina virtuale in funzione sono noti a grafici e avvisi relativi alle metriche della piattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-537">Azure platform metrics charting and alerting knows the resourceId of the VM you're working on.</span></span> <span data-ttu-id="dd071-538">Si prevede di trovare i dati della macchina virtuale tramite la chiave di ricerca resourceId.</span><span class="sxs-lookup"><span data-stu-id="dd071-538">It expects to find the data for your VM using the resourceId the lookup key.</span></span>
* <span data-ttu-id="dd071-539">Se si usa la scalabilità automatica di Azure, il valore di resourceId nella configurazione di scalabilità automatica deve corrispondere a quello di resourceId usato da LAD.</span><span class="sxs-lookup"><span data-stu-id="dd071-539">If you use Azure autoscale, the resourceId in the autoscale configuration must match the resourceId used by LAD.</span></span>
* <span data-ttu-id="dd071-540">Il valore di resourceId viene creato nei nomi di JsonBlobs scritto da LAD.</span><span class="sxs-lookup"><span data-stu-id="dd071-540">The resourceId is built into the names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="dd071-541">Visualizzare i dati</span><span class="sxs-lookup"><span data-stu-id="dd071-541">View your data</span></span>

<span data-ttu-id="dd071-542">Usare il portale di Azure per visualizzare i dati sulle prestazioni o impostare gli avvisi:</span><span class="sxs-lookup"><span data-stu-id="dd071-542">Use the Azure portal to view performance data or set alerts:</span></span>

![immagine](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="dd071-544">I dati `performanceCounters` sono sempre archiviati in una tabella di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-544">The `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="dd071-545">Le API di Archiviazione di Azure sono disponibili per più linguaggi e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="dd071-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="dd071-546">I dati inviati ai sink JsonBlob sono archiviati nei BLOB nell'account di archiviazione indicato in [Impostazioni protette](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="dd071-546">Data sent to JsonBlob sinks is stored in blobs in the storage account named in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="dd071-547">È possibile usare i dati BLOB usando qualsiasi API di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd071-547">You can consume the blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="dd071-548">È anche possibile usare questi strumenti dell'interfaccia utente per accedere ai dati nell'archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="dd071-548">In addition, you can use these UI tools to access the data in Azure Storage:</span></span>

* <span data-ttu-id="dd071-549">Esplora server di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd071-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="dd071-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Microsoft Azure Storage Explorer").</span><span class="sxs-lookup"><span data-stu-id="dd071-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="dd071-551">Questo snapshot di una sessione di Microsoft Azure Storage Explorer mostra le tabelle di archiviazione di Azure e i contenitori generati da un'estensione LAD 3.0 correttamente configurata su una macchina virtuale di test.</span><span class="sxs-lookup"><span data-stu-id="dd071-551">This snapshot of a Microsoft Azure Storage Explorer session shows the generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="dd071-552">L'immagine non corrisponde esattamente alla [configurazione LAD 3.0 di esempio](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="dd071-552">The image doesn't match exactly with the [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![immagine](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="dd071-554">Vedere la relativa [documentazione di EventHubs](../../event-hubs/event-hubs-what-is-event-hubs.md) per avere informazioni su come usare i messaggi pubblicati in un endpoint EventHubs.</span><span class="sxs-lookup"><span data-stu-id="dd071-554">See the relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) to learn how to consume messages published to an EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd071-555">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd071-555">Next steps</span></span>

* <span data-ttu-id="dd071-556">Creare avvisi sulle metriche in [Monitoraggio di Azure](../../monitoring-and-diagnostics/insights-alerts-portal.md) per le metriche raccolte.</span><span class="sxs-lookup"><span data-stu-id="dd071-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for the metrics you collect.</span></span>
* <span data-ttu-id="dd071-557">Creare [grafici di monitoraggio](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) per le metriche.</span><span class="sxs-lookup"><span data-stu-id="dd071-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="dd071-558">Informazioni su come [creare un set di scalabilità di macchine virtuali](/azure/virtual-machines/linux/tutorial-create-vmss) con le metriche per controllare la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="dd071-558">Learn how to [create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics to control autoscaling.</span></span>
