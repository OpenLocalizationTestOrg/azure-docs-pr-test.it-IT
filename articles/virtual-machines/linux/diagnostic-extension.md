---
title: Calcolo aaaAzure - estensione diagnostica per Linux | Documenti Microsoft
description: "La modalità tooconfigure hello metriche toocollect Azure Linux diagnostica estensione (LAD) e registrare eventi da macchine virtuali Linux in esecuzione in Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="a66f3-103">Utilizzare i registri e le metriche toomonitor estensione diagnostica per Linux</span><span class="sxs-lookup"><span data-stu-id="a66f3-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="a66f3-104">Questo documento descrive versione 3.0 e successive di hello estensione diagnostica per Linux.</span><span class="sxs-lookup"><span data-stu-id="a66f3-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a66f3-105">Per informazioni sulla versione 2.3 e precedenti, vedere [questo documento](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="a66f3-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="a66f3-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="a66f3-106">Introduction</span></span>

<span data-ttu-id="a66f3-107">Estensione diagnostica per Linux Hello consente un utente monitoraggio hello integrità di una VM Linux in esecuzione in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="a66f3-108">Dispone di hello seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="a66f3-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="a66f3-109">Raccoglie le metriche delle prestazioni del sistema da hello VM e li archivia in una tabella specifica in un account di archiviazione designate.</span><span class="sxs-lookup"><span data-stu-id="a66f3-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="a66f3-110">Recupera la registrazione degli eventi dal Registro di sistema e li archivia in una tabella specifica in hello designato account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a66f3-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="a66f3-111">Consente la metrica utenti toocustomize hello dati venga raccolti e caricata.</span><span class="sxs-lookup"><span data-stu-id="a66f3-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="a66f3-112">Abilita funzioni syslog hello toocustomize di utenti e i livelli di gravità degli eventi che vengono raccolti e caricati.</span><span class="sxs-lookup"><span data-stu-id="a66f3-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="a66f3-113">Consente agli utenti tooupload log specificato file tooa designato archiviazione tabella.</span><span class="sxs-lookup"><span data-stu-id="a66f3-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="a66f3-114">Supporta l'invio delle metriche e log eventi tooarbitrary EventHub gli endpoint e i BLOB in formato JSON in hello definito account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a66f3-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="a66f3-115">Questa estensione funziona con entrambi i modelli di distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="a66f3-116">L'installazione dell'estensione hello nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a66f3-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="a66f3-117">È possibile abilitare questa estensione tramite il cmdlet di Azure PowerShell hello, script CLI di Azure o i modelli di distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="a66f3-118">Per altre informazioni, vedere [Funzionalità delle estensioni](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="a66f3-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="a66f3-119">Hello portale di Azure non può essere tooenable utilizzati oppure configurare LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="a66f3-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="a66f3-120">ma esso stesso installa e configura la versione 2.3.</span><span class="sxs-lookup"><span data-stu-id="a66f3-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="a66f3-121">Avvisi e i grafici del portale di azure funzionano con i dati di entrambe le versioni dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="a66f3-122">Le istruzioni di installazione e la [configurazione di esempio scaricabile](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configurano LAD 3.0 per:</span><span class="sxs-lookup"><span data-stu-id="a66f3-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="a66f3-123">acquisire e archiviare hello stesse metriche come sono stati forniti da 2.3 LAD;</span><span class="sxs-lookup"><span data-stu-id="a66f3-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="a66f3-124">acquisire un set di metriche di sistema di file, nuovo tooLAD 3.0; utile</span><span class="sxs-lookup"><span data-stu-id="a66f3-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="a66f3-125">acquisire l'insieme di syslog predefinito hello abilitata da 2.3 LAD;</span><span class="sxs-lookup"><span data-stu-id="a66f3-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="a66f3-126">abilitare hello esperienza del portale di Azure per la creazione di grafici e avvisi sulle metriche di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a66f3-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="a66f3-127">configurazione scaricabile Hello è solo un esempio; modificarlo toosuit le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="a66f3-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a66f3-128">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a66f3-128">Prerequisites</span></span>

* <span data-ttu-id="a66f3-129">**Agente Linux di Azure 2.2.0 o versione successiva**.</span><span class="sxs-lookup"><span data-stu-id="a66f3-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="a66f3-130">La maggior parte delle immagini della raccolta Linux di macchine virtuali di Azure include la versione 2.2.7 o successive.</span><span class="sxs-lookup"><span data-stu-id="a66f3-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="a66f3-131">Eseguire `/usr/sbin/waagent -version` tooconfirm hello versione hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a66f3-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="a66f3-132">Se hello macchina virtuale è in esecuzione una versione precedente dell'agente guest hello, seguire [queste istruzioni](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate è.</span><span class="sxs-lookup"><span data-stu-id="a66f3-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="a66f3-133">**Interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="a66f3-133">**Azure CLI**.</span></span> <span data-ttu-id="a66f3-134">[Impostare hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) ambiente nel computer.</span><span class="sxs-lookup"><span data-stu-id="a66f3-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="a66f3-135">Hello wget comando, se si dispone già: eseguire `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="a66f3-136">Una sottoscrizione di Azure esistente e una risorsa di archiviazione esistente all'interno dell'account dati hello toostore.</span><span class="sxs-lookup"><span data-stu-id="a66f3-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="a66f3-137">Installazione di esempio</span><span class="sxs-lookup"><span data-stu-id="a66f3-137">Sample installation</span></span>

<span data-ttu-id="a66f3-138">Compilare i parametri corretti hello in hello prime tre righe, quindi eseguire lo script come radice:</span><span class="sxs-lookup"><span data-stu-id="a66f3-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="a66f3-139">Hello URL per la configurazione di esempio hello e il relativo contenuto è toochange soggetto.</span><span class="sxs-lookup"><span data-stu-id="a66f3-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="a66f3-140">Scaricare una copia del file JSON di impostazioni del portale hello e personalizzarlo per le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="a66f3-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="a66f3-141">Qualsiasi modello o automazione creato dall'utente deve usare la propria copia, invece di scaricare l'URL ogni volta.</span><span class="sxs-lookup"><span data-stu-id="a66f3-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="a66f3-142">L'aggiornamento delle impostazioni di estensione hello</span><span class="sxs-lookup"><span data-stu-id="a66f3-142">Updating hello extension settings</span></span>

<span data-ttu-id="a66f3-143">Dopo aver modificato il protetti o le impostazioni pubbliche, distribuire le VM toohello eseguendo hello stesso comando.</span><span class="sxs-lookup"><span data-stu-id="a66f3-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="a66f3-144">Se qualsiasi elemento modificata nelle impostazioni di hello, impostazioni hello aggiornato vengono inviate toohello estensione.</span><span class="sxs-lookup"><span data-stu-id="a66f3-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="a66f3-145">LAD ricaricamenti configurazione hello e riavviato.</span><span class="sxs-lookup"><span data-stu-id="a66f3-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="a66f3-146">Migrazione da versioni precedenti di estensione hello</span><span class="sxs-lookup"><span data-stu-id="a66f3-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="a66f3-147">Hello la versione più recente dell'estensione hello è **3.0**.</span><span class="sxs-lookup"><span data-stu-id="a66f3-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="a66f3-148">**Le versioni precedenti (2.x) sono deprecate e la loro pubblicazione potrebbe essere annullata a partire dal 31 luglio 2018**.</span><span class="sxs-lookup"><span data-stu-id="a66f3-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a66f3-149">Questa estensione è stata introdotta configurazione toohello modifiche di rilievo dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="a66f3-150">Una di queste modifiche è stata effettuata sicurezza hello tooimprove di estensione hello. di conseguenza, la compatibilità con 2. x potrebbe non essere mantenuta.</span><span class="sxs-lookup"><span data-stu-id="a66f3-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="a66f3-151">Inoltre, hello estensione server di pubblicazione per questa estensione è diverso dal server di pubblicazione hello per le versioni 2. x hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="a66f3-152">toomigrate da 2. x toothis nuova versione dell'estensione di hello, è necessario disinstallare l'estensione precedente di hello (nel nome di server di pubblicazione hello precedente), quindi installare la versione 3 di estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="a66f3-153">Consigli:</span><span class="sxs-lookup"><span data-stu-id="a66f3-153">Recommendations:</span></span>

* <span data-ttu-id="a66f3-154">Installare l'estensione di hello con l'aggiornamento di versione secondaria automatico abilitato.</span><span class="sxs-lookup"><span data-stu-id="a66f3-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="a66f3-155">Nel modello di distribuzione classica le macchine virtuali, specificare '3.*' come versione di hello se si sta installando l'estensione hello tramite Azure XPLAT CLI o Powershell.</span><span class="sxs-lookup"><span data-stu-id="a66f3-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="a66f3-156">Distribuzione di gestione risorse di Azure le macchine virtuali del modello, includere ' "autoUpgradeMinorVersion": true' nel modello di distribuzione VM hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="a66f3-157">Usare un account di archiviazione nuovo o diverso per LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="a66f3-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="a66f3-158">Esistono diverse piccole incompatibilità tra LAD 2.3 e LAD 3.0 che creano problemi nella condivisione di un account:</span><span class="sxs-lookup"><span data-stu-id="a66f3-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="a66f3-159">LAD 3.0 inserisce gli eventi SysLog in una tabella con un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="a66f3-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="a66f3-160">le stringhe per counterSpecifier Hello `builtin` metriche differiscono LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="a66f3-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="a66f3-161">Impostazioni protette</span><span class="sxs-lookup"><span data-stu-id="a66f3-161">Protected settings</span></span>

<span data-ttu-id="a66f3-162">Questo set di informazioni per la configurazione contiene informazioni riservate che devono essere protette dalla visualizzazione pubblica, ad esempio, le credenziali di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a66f3-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="a66f3-163">Queste impostazioni sono trasmessi tooand archiviati dall'estensione hello in forma crittografata.</span><span class="sxs-lookup"><span data-stu-id="a66f3-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="a66f3-164">Nome</span><span class="sxs-lookup"><span data-stu-id="a66f3-164">Name</span></span> | <span data-ttu-id="a66f3-165">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-165">Value</span></span>
---- | -----
<span data-ttu-id="a66f3-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="a66f3-166">storageAccountName</span></span> | <span data-ttu-id="a66f3-167">nome Hello hello dell'account di archiviazione in cui i dati vengono scritti dall'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="a66f3-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="a66f3-168">storageAccountEndPoint</span></span> | <span data-ttu-id="a66f3-169">endpoint (facoltativo) hello identificazione cloud hello in cui hello esiste l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a66f3-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="a66f3-170">Se questa impostazione è assente, LAD predefinito toohello cloud pubblico di Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="a66f3-171">toouse un account di archiviazione in Azure in Germania, Azure per enti pubblici o Azure China, imposta questo valore di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="a66f3-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="a66f3-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="a66f3-172">storageAccountSasToken</span></span> | <span data-ttu-id="a66f3-173">Un [token SAS Account](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) per i servizi Blob e tabella (`ss='bt'`), applicabile toocontainers e oggetti (`srt='co'`), che aggiungono, creare, elencare, aggiornare e le autorizzazioni di scrittura (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="a66f3-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="a66f3-174">Eseguire *non* includono hello iniziali punto interrogativo (?).</span><span class="sxs-lookup"><span data-stu-id="a66f3-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="a66f3-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="a66f3-175">mdsdHttpProxy</span></span> | <span data-ttu-id="a66f3-176">(facoltativo) HTTP proxy informazioni necessarie tooenable hello estensione tooconnect toohello specificato l'account di archiviazione e l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="a66f3-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="a66f3-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="a66f3-177">sinksConfig</span></span> | <span data-ttu-id="a66f3-178">(facoltativo) I dettagli di metriche toowhich destinazioni alternative e gli eventi possono essere recapitati.</span><span class="sxs-lookup"><span data-stu-id="a66f3-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="a66f3-179">dettagli specifici di Hello di ogni sink dati supportata dall'estensione hello vengono trattati nelle sezioni hello che seguono.</span><span class="sxs-lookup"><span data-stu-id="a66f3-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="a66f3-180">È possibile creare facilmente token SAS hello necessarie tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="a66f3-181">Selezionare toowhich account di archiviazione generico hello desiderato hello estensione toowrite</span><span class="sxs-lookup"><span data-stu-id="a66f3-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="a66f3-182">Selezionare "Firma di accesso condiviso" da parte di impostazioni hello del menu a sinistra di hello</span><span class="sxs-lookup"><span data-stu-id="a66f3-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="a66f3-183">Assicurarsi di sezioni di hello appropriate come descritte in precedenza</span><span class="sxs-lookup"><span data-stu-id="a66f3-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="a66f3-184">Fare clic su hello "Generare SAS".</span><span class="sxs-lookup"><span data-stu-id="a66f3-184">Click hello "Generate SAS" button.</span></span>

![immagine](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="a66f3-186">Hello di copia generato SAS nel campo storageAccountSasToken hello; rimuovere hello iniziali punto interrogativo ("?").</span><span class="sxs-lookup"><span data-stu-id="a66f3-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="a66f3-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="a66f3-187">sinksConfig</span></span>

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

<span data-ttu-id="a66f3-188">Questa sezione facoltativa definisce le destinazioni aggiuntive estensione hello toowhich invia informazioni hello che raccoglie.</span><span class="sxs-lookup"><span data-stu-id="a66f3-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="a66f3-189">Matrice di Hello "sink" contiene un oggetto per ogni sink dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="a66f3-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="a66f3-190">attributo "tipo" determina Hello hello altri attributi nell'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="a66f3-191">Elemento</span><span class="sxs-lookup"><span data-stu-id="a66f3-191">Element</span></span> | <span data-ttu-id="a66f3-192">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-192">Value</span></span>
------- | -----
<span data-ttu-id="a66f3-193">name</span><span class="sxs-lookup"><span data-stu-id="a66f3-193">name</span></span> | <span data-ttu-id="a66f3-194">Sink di toothis toorefer altrove nella configurazione dell'estensione hello è utilizzata una stringa.</span><span class="sxs-lookup"><span data-stu-id="a66f3-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="a66f3-195">type</span><span class="sxs-lookup"><span data-stu-id="a66f3-195">type</span></span> | <span data-ttu-id="a66f3-196">tipo di Hello del sink da definire.</span><span class="sxs-lookup"><span data-stu-id="a66f3-196">hello type of sink being defined.</span></span> <span data-ttu-id="a66f3-197">Determina hello altri valori (se presente) in istanze di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="a66f3-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="a66f3-198">La versione 3.0 di hello estensione diagnostica per Linux supporta due tipi di sink: EventHub e JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="a66f3-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="a66f3-199">sink di EventHub Hello</span><span class="sxs-lookup"><span data-stu-id="a66f3-199">hello EventHub sink</span></span>

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

<span data-ttu-id="a66f3-200">voce "sasURL" Hello contiene hello URL completo, incluso il token di firma di accesso condiviso, per hello dati toowhich Hub eventi deve essere pubblicata.</span><span class="sxs-lookup"><span data-stu-id="a66f3-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="a66f3-201">LAD richiede una firma di accesso condiviso denominazione di un criterio che consente l'attestazione di trasmissione hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="a66f3-202">Esempio:</span><span class="sxs-lookup"><span data-stu-id="a66f3-202">An example:</span></span>

* <span data-ttu-id="a66f3-203">Creare uno spazio dei nomi dell'hub eventi denominato `contosohub`</span><span class="sxs-lookup"><span data-stu-id="a66f3-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="a66f3-204">Creare un Hub eventi nello spazio dei nomi hello chiamato`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="a66f3-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="a66f3-205">Creare un criterio di accesso condiviso in Hub eventi denominato hello `writer` che abilita hello attestazione di trasmissione</span><span class="sxs-lookup"><span data-stu-id="a66f3-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="a66f3-206">Se è stata creata una firma di accesso condiviso valida fino a mezzanotte UTC del 1 ° gennaio 2018, potrebbe essere il valore di sasURL hello:</span><span class="sxs-lookup"><span data-stu-id="a66f3-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="a66f3-207">Per altre informazioni sulla generazione di token SAS per gli hub eventi, vedere [questa pagina Web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a66f3-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="a66f3-208">sink JsonBlob Hello</span><span class="sxs-lookup"><span data-stu-id="a66f3-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="a66f3-209">Dati indirizzati tooa JsonBlob sink vengono archiviati in BLOB in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="a66f3-210">Ogni istanza di LAD crea un BLOB all'ora per ogni nome di sink.</span><span class="sxs-lookup"><span data-stu-id="a66f3-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="a66f3-211">Ciascun BLOB contiene sempre una matrice JSON sintatticamente valida dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="a66f3-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="a66f3-212">Le nuove voci vengono aggiunti in modo atomico toohello matrice.</span><span class="sxs-lookup"><span data-stu-id="a66f3-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="a66f3-213">BLOB vengono archiviati in un contenitore con stesso nome come sink hello hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="a66f3-214">Hello regole di archiviazione di Azure per i nomi dei contenitori blob applicare toohello nomi di sink JsonBlob: tra 3 e 63 caratteri ASCII alfanumerici minuscoli o trattini.</span><span class="sxs-lookup"><span data-stu-id="a66f3-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="a66f3-215">Impostazioni pubbliche</span><span class="sxs-lookup"><span data-stu-id="a66f3-215">Public settings</span></span>

<span data-ttu-id="a66f3-216">Questa struttura contiene diversi blocchi di impostazioni che controllano i dati raccolti dall'estensione hello hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="a66f3-217">Tutte le impostazioni sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="a66f3-217">Each setting is optional.</span></span> <span data-ttu-id="a66f3-218">Se si specifica `ladCfg`, è necessario specificare anche `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="a66f3-219">Elemento</span><span class="sxs-lookup"><span data-stu-id="a66f3-219">Element</span></span> | <span data-ttu-id="a66f3-220">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-220">Value</span></span>
------- | -----
<span data-ttu-id="a66f3-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="a66f3-221">StorageAccount</span></span> | <span data-ttu-id="a66f3-222">nome Hello hello dell'account di archiviazione in cui i dati vengono scritti dall'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="a66f3-223">Deve essere hello stesso nome specificato nella hello [protetto impostazioni](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="a66f3-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="a66f3-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="a66f3-224">mdsdHttpProxy</span></span> | <span data-ttu-id="a66f3-225">(facoltativo) Stessa descrizione disponibile hello [protetto impostazioni](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="a66f3-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="a66f3-226">valore pubblica Hello viene sottoposto a override dal valore private hello, se impostata.</span><span class="sxs-lookup"><span data-stu-id="a66f3-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="a66f3-227">Inserire le impostazioni proxy che contengono un segreto, ad esempio una password, in hello [protetto impostazioni](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="a66f3-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="a66f3-228">gli elementi rimanenti Hello sono descritti in dettaglio nelle sezioni che seguono hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="a66f3-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="a66f3-229">ladCfg</span></span>

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

<span data-ttu-id="a66f3-230">Sink di questa raccolta di hello controlli struttura facoltativo di metriche e i registri per toohello di recapito dei dati di servizio e tooother le metriche di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="a66f3-231">È necessario specificare `performanceCounters` o `syslogEvents` oppure entrambi.</span><span class="sxs-lookup"><span data-stu-id="a66f3-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="a66f3-232">È necessario specificare hello `metrics` struttura.</span><span class="sxs-lookup"><span data-stu-id="a66f3-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="a66f3-233">Elemento</span><span class="sxs-lookup"><span data-stu-id="a66f3-233">Element</span></span> | <span data-ttu-id="a66f3-234">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-234">Value</span></span>
------- | -----
<span data-ttu-id="a66f3-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="a66f3-235">eventVolume</span></span> | <span data-ttu-id="a66f3-236">(facoltativo) Controlli hello numero di partizioni create all'interno di tabella di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="a66f3-237">Può essere uno tra `"Large"`, `"Medium"` o `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="a66f3-238">Se non specificato, il valore di predefinito hello è `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="a66f3-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="a66f3-239">sampleRateInSeconds</span></span> | <span data-ttu-id="a66f3-240">intervallo predefinito di hello (facoltativo) tra raccolta della metrica (non aggregata) non elaborata.</span><span class="sxs-lookup"><span data-stu-id="a66f3-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="a66f3-241">frequenza di campionamento Hello più piccola supportata è 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="a66f3-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="a66f3-242">Se non specificato, il valore di predefinito hello è `15`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="a66f3-243">Metriche</span><span class="sxs-lookup"><span data-stu-id="a66f3-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="a66f3-244">Elemento</span><span class="sxs-lookup"><span data-stu-id="a66f3-244">Element</span></span> | <span data-ttu-id="a66f3-245">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-245">Value</span></span>
------- | -----
<span data-ttu-id="a66f3-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="a66f3-246">resourceId</span></span> | <span data-ttu-id="a66f3-247">ID di risorsa di gestione risorse di Azure di Hello di hello macchina virtuale o di scalabilità della macchina virtuale hello impostare hello toowhich che VM appartiene.</span><span class="sxs-lookup"><span data-stu-id="a66f3-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="a66f3-248">Questa impostazione deve essere specificato anche se qualsiasi sink JsonBlob viene utilizzata nella configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="a66f3-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="a66f3-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="a66f3-250">frequenza di Hello in cui le metriche di aggregazione sono toobe calcolata e trasferiti tooAzure metriche, espresso come un intervallo di tempo è 8601.</span><span class="sxs-lookup"><span data-stu-id="a66f3-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="a66f3-251">periodo di trasferimento più piccolo Hello è 60 secondi, ovvero PT1M.</span><span class="sxs-lookup"><span data-stu-id="a66f3-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="a66f3-252">È necessario specificare almeno un scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="a66f3-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="a66f3-253">Esempi di hello metriche specificate nella sezione performanceCounters hello vengono raccolti ogni 15 secondi o frequenza di campionamento hello definito in modo esplicito per il contatore hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="a66f3-254">Se più frequenze scheduledTransferPeriod visualizzato (come esempio hello), ogni aggregazione viene calcolato in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="a66f3-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="a66f3-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="a66f3-255">performanceCounters</span></span>

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

<span data-ttu-id="a66f3-256">Questa sezione facoltativa controlla raccolta hello della metrica.</span><span class="sxs-lookup"><span data-stu-id="a66f3-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="a66f3-257">Gli esempi non elaborati vengono aggregati per ogni [scheduledTransferPeriod](#metrics) tooproduce questi valori:</span><span class="sxs-lookup"><span data-stu-id="a66f3-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="a66f3-258">mean</span><span class="sxs-lookup"><span data-stu-id="a66f3-258">mean</span></span>
* <span data-ttu-id="a66f3-259">minimum</span><span class="sxs-lookup"><span data-stu-id="a66f3-259">minimum</span></span>
* <span data-ttu-id="a66f3-260">maximum</span><span class="sxs-lookup"><span data-stu-id="a66f3-260">maximum</span></span>
* <span data-ttu-id="a66f3-261">ultimo valore raccolto</span><span class="sxs-lookup"><span data-stu-id="a66f3-261">last-collected value</span></span>
* <span data-ttu-id="a66f3-262">numero di campioni non elaborati usato aggregazione hello toocompute</span><span class="sxs-lookup"><span data-stu-id="a66f3-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="a66f3-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="a66f3-263">Element</span></span> | <span data-ttu-id="a66f3-264">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-264">Value</span></span>
------- | -----
<span data-ttu-id="a66f3-265">sinks</span><span class="sxs-lookup"><span data-stu-id="a66f3-265">sinks</span></span> | <span data-ttu-id="a66f3-266">(facoltativo) Un elenco delimitato da virgole di nomi di sink toowhich che LAD invia i risultati di metrica aggregati.</span><span class="sxs-lookup"><span data-stu-id="a66f3-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="a66f3-267">Tutte le metriche aggregate sono pubblicati tooeach elencati sink.</span><span class="sxs-lookup"><span data-stu-id="a66f3-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="a66f3-268">Vedere [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="a66f3-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="a66f3-269">Esempio: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="a66f3-270">type</span><span class="sxs-lookup"><span data-stu-id="a66f3-270">type</span></span> | <span data-ttu-id="a66f3-271">Identifica hello provider effettivo della metrica hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="a66f3-272">class</span><span class="sxs-lookup"><span data-stu-id="a66f3-272">class</span></span> | <span data-ttu-id="a66f3-273">Insieme a "counter", identifica metrica specifica di hello nello spazio dei nomi del provider di hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="a66f3-274">counter</span><span class="sxs-lookup"><span data-stu-id="a66f3-274">counter</span></span> | <span data-ttu-id="a66f3-275">Insieme a "class", identifica metrica specifica di hello nello spazio dei nomi del provider di hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="a66f3-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="a66f3-276">counterSpecifier</span></span> | <span data-ttu-id="a66f3-277">Identifica una metrica specifica di hello nello spazio dei nomi Azure metriche hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="a66f3-278">condition</span><span class="sxs-lookup"><span data-stu-id="a66f3-278">condition</span></span> | <span data-ttu-id="a66f3-279">(facoltativo) Consente di selezionare un'istanza specifica di metrica di hello toowhich oggetto hello applica o seleziona hello aggregazione in tutte le istanze di tale oggetto.</span><span class="sxs-lookup"><span data-stu-id="a66f3-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="a66f3-280">Per ulteriori informazioni, vedere hello [ `builtin` le definizioni delle metriche](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="a66f3-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="a66f3-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="a66f3-281">sampleRate</span></span> | <span data-ttu-id="a66f3-282">È l'intervallo 8601 che imposta la frequenza di hello in cui vengono raccolti degli esempi non elaborati per la metrica.</span><span class="sxs-lookup"><span data-stu-id="a66f3-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="a66f3-283">Se non è impostata, l'intervallo di raccolta hello è impostata dal valore hello di [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="a66f3-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="a66f3-284">frequenza di campionamento supportata più breve Hello è 15 secondi (PT15S).</span><span class="sxs-lookup"><span data-stu-id="a66f3-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="a66f3-285">unit</span><span class="sxs-lookup"><span data-stu-id="a66f3-285">unit</span></span> | <span data-ttu-id="a66f3-286">Deve essere una delle seguenti stringhe: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span><span class="sxs-lookup"><span data-stu-id="a66f3-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="a66f3-287">Definisce l'unità di hello metrica hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="a66f3-288">Consumer di dati raccolti hello prevedere hello raccolti dati valori toomatch questa unità.</span><span class="sxs-lookup"><span data-stu-id="a66f3-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="a66f3-289">LAD ignora questo campo.</span><span class="sxs-lookup"><span data-stu-id="a66f3-289">LAD ignores this field.</span></span>
<span data-ttu-id="a66f3-290">displayName</span><span class="sxs-lookup"><span data-stu-id="a66f3-290">displayName</span></span> | <span data-ttu-id="a66f3-291">Hello etichetta (in lingua hello specificata dalle impostazioni locali associato di hello impostazione) toobe collegato toothis dati di metrica di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="a66f3-292">LAD ignora questo campo.</span><span class="sxs-lookup"><span data-stu-id="a66f3-292">LAD ignores this field.</span></span>

<span data-ttu-id="a66f3-293">counterSpecifier Hello è un identificatore arbitrario.</span><span class="sxs-lookup"><span data-stu-id="a66f3-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="a66f3-294">I consumer di dati di metrica, ad esempio hello grafici portale Azure e avviso di funzionalità, utilizzano counterSpecifier come hello "key" che identifica una metrica o un'istanza di una metrica.</span><span class="sxs-lookup"><span data-stu-id="a66f3-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="a66f3-295">Per le metriche `builtin`, è consigliabile usare i valori di counterSpecifier che iniziano con `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="a66f3-296">Se si raccolgono un'istanza di una metrica specifica, è consigliabile che allegare identificatore hello del valore di counterSpecifier toohello istanza hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="a66f3-297">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="a66f3-297">Some examples:</span></span>

* <span data-ttu-id="a66f3-298">`/builtin/Processor/PercentIdleTime` - Tempo di inattività medio calcolato per tutti i core</span><span class="sxs-lookup"><span data-stu-id="a66f3-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="a66f3-299">`/builtin/Disk/FreeSpace(/mnt)`-Spazio per hello /mnt filesystem</span><span class="sxs-lookup"><span data-stu-id="a66f3-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="a66f3-300">`/builtin/Disk/FreeSpace` - Spazio libero medio calcolato per tutti i file system montati</span><span class="sxs-lookup"><span data-stu-id="a66f3-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="a66f3-301">LAD né hello portale di Azure prevede hello counterSpecifier valore toomatch qualsiasi criterio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="a66f3-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="a66f3-302">È consigliabile essere coerenti durante la creazione dei valori di counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="a66f3-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="a66f3-303">Quando si specifica `performanceCounters`, LAD scrive sempre tabella tooa dati nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="a66f3-304">È possibile avere hello stesso dati scritti tooJSON BLOB e/o hub eventi, ma non è possibile disabilitare l'archiviazione tabella tooa di dati.</span><span class="sxs-lookup"><span data-stu-id="a66f3-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="a66f3-305">Tutte le istanze di hello estensione diagnostica configurato toouse hello stesso account di archiviazione con nome e l'endpoint aggiungere toohello i registri e le metriche stessa tabella.</span><span class="sxs-lookup"><span data-stu-id="a66f3-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="a66f3-306">Se la scrittura di un numero eccessivo di macchine virtuali toohello stessa partizione della tabella, Azure può limitare scrive toothat partizione.</span><span class="sxs-lookup"><span data-stu-id="a66f3-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="a66f3-307">Hello eventVolume impostazione cause voci toobe distribuite su 1 (piccola), 10 (Media) o 100 partizioni diverse (grande).</span><span class="sxs-lookup"><span data-stu-id="a66f3-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="a66f3-308">In genere, "Medium" è sufficiente tooensure traffico non è limitato.</span><span class="sxs-lookup"><span data-stu-id="a66f3-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="a66f3-309">funzionalità di Azure metriche Hello di hello portale di Azure utilizza i dati di hello grafici tooproduce tabella o tootrigger avvisi.</span><span class="sxs-lookup"><span data-stu-id="a66f3-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="a66f3-310">nome della tabella Hello è la concatenazione di hello di queste stringhe:</span><span class="sxs-lookup"><span data-stu-id="a66f3-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="a66f3-311">Hello "scheduledTransferPeriod" per hello aggregati i valori archiviati nella tabella hello</span><span class="sxs-lookup"><span data-stu-id="a66f3-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="a66f3-312">Una data nel formato hello "Aaaammgg", che modifica ogni 10 giorni</span><span class="sxs-lookup"><span data-stu-id="a66f3-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="a66f3-313">Gli esempi includono `WADMetricsPT1HP10DV2S20170410` e `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="a66f3-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="a66f3-314">syslogEvents</span></span>

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

<span data-ttu-id="a66f3-315">Questa sezione facoltativa controlla raccolta hello di eventi dal Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="a66f3-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="a66f3-316">Se la sezione hello viene omesso, è possibile che gli eventi syslog non vengono acquisiti affatto.</span><span class="sxs-lookup"><span data-stu-id="a66f3-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="a66f3-317">raccolta syslogEventConfiguration Hello ha una voce per ogni funzione syslog di interesse.</span><span class="sxs-lookup"><span data-stu-id="a66f3-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="a66f3-318">Se minSeverity è "NONE" per una particolare caratteristica o se tale funzionalità è presente nell'elemento hello, non viene acquisito nessun evento da tale struttura.</span><span class="sxs-lookup"><span data-stu-id="a66f3-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="a66f3-319">Elemento</span><span class="sxs-lookup"><span data-stu-id="a66f3-319">Element</span></span> | <span data-ttu-id="a66f3-320">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-320">Value</span></span>
------- | -----
<span data-ttu-id="a66f3-321">sinks</span><span class="sxs-lookup"><span data-stu-id="a66f3-321">sinks</span></span> | <span data-ttu-id="a66f3-322">Un elenco delimitato da virgole di nomi di sink toowhich singolo registro eventi vengono pubblicati.</span><span class="sxs-lookup"><span data-stu-id="a66f3-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="a66f3-323">Tutti gli eventi di registro corrispondenti restrizioni hello in syslogEventConfiguration sono pubblicati tooeach elencati sink.</span><span class="sxs-lookup"><span data-stu-id="a66f3-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="a66f3-324">Esempio: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="a66f3-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="a66f3-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="a66f3-325">facilityName</span></span> | <span data-ttu-id="a66f3-326">Un nome dell'impianto SysLog, ad esempio "LOG\_USER" o "LOG\_LOCAL0".</span><span class="sxs-lookup"><span data-stu-id="a66f3-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="a66f3-327">Sezione "funzionalità" hello di hello [pagina man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) per l'elenco completo di hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="a66f3-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="a66f3-328">minSeverity</span></span> | <span data-ttu-id="a66f3-329">Un livello di gravità SysLog, ad esempio "LOG\_ERR" o "LOG\_INFO".</span><span class="sxs-lookup"><span data-stu-id="a66f3-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="a66f3-330">Sezione "livello" hello di hello [pagina man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) per l'elenco completo di hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="a66f3-331">estensione Hello acquisisce gli eventi inviati toohello funzionalità in o sopra hello specificato livello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="a66f3-332">Quando si specifica `syslogEvents`, LAD scrive sempre tabella tooa dati nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="a66f3-333">È possibile avere hello stesso dati scritti tooJSON BLOB e/o hub eventi, ma non è possibile disabilitare l'archiviazione tabella tooa di dati.</span><span class="sxs-lookup"><span data-stu-id="a66f3-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="a66f3-334">Hello partizionamento per questa tabella è hello uguali a quelli descritti per `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="a66f3-335">nome della tabella Hello è la concatenazione di hello di queste stringhe:</span><span class="sxs-lookup"><span data-stu-id="a66f3-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="a66f3-336">Una data nel formato hello "Aaaammgg", che modifica ogni 10 giorni</span><span class="sxs-lookup"><span data-stu-id="a66f3-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="a66f3-337">Gli esempi includono `LinuxSyslog20170410` e `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="a66f3-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="a66f3-338">perfCfg</span></span>

<span data-ttu-id="a66f3-339">Questa sezione facoltativa consente di controllare l'esecuzione delle query arbitrarie [OMI](https://github.com/Microsoft/omi).</span><span class="sxs-lookup"><span data-stu-id="a66f3-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

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

<span data-ttu-id="a66f3-340">Elemento</span><span class="sxs-lookup"><span data-stu-id="a66f3-340">Element</span></span> | <span data-ttu-id="a66f3-341">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-341">Value</span></span>
------- | -----
<span data-ttu-id="a66f3-342">namespace</span><span class="sxs-lookup"><span data-stu-id="a66f3-342">namespace</span></span> | <span data-ttu-id="a66f3-343">(facoltativo) hello OMI dello spazio dei nomi all'interno delle quali hello query deve essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="a66f3-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="a66f3-344">Se non viene specificato, hello predefinita è "root/scx", implementata da hello [provider multipiattaforma di System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="a66f3-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="a66f3-345">query</span><span class="sxs-lookup"><span data-stu-id="a66f3-345">query</span></span> | <span data-ttu-id="a66f3-346">Hello OMI query toobe eseguita.</span><span class="sxs-lookup"><span data-stu-id="a66f3-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="a66f3-347">tabella</span><span class="sxs-lookup"><span data-stu-id="a66f3-347">table</span></span> | <span data-ttu-id="a66f3-348">tabella di archiviazione di Azure, hello (facoltativo) hello designato account di archiviazione (vedere [protetto impostazioni](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="a66f3-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="a66f3-349">frequency</span><span class="sxs-lookup"><span data-stu-id="a66f3-349">frequency</span></span> | <span data-ttu-id="a66f3-350">numero di hello (facoltativo) di secondi tra l'esecuzione di query hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="a66f3-351">Il valore predefinito è 300, ovvero 5 minuti; il valore minimo è 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="a66f3-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="a66f3-352">sinks</span><span class="sxs-lookup"><span data-stu-id="a66f3-352">sinks</span></span> | <span data-ttu-id="a66f3-353">(facoltativo) Pubblicare un elenco delimitato da virgole di nomi di risultati di metrica del sink aggiuntive toowhich campione non elaborato.</span><span class="sxs-lookup"><span data-stu-id="a66f3-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="a66f3-354">Nessuna aggregazione di questi esempi non elaborati viene calcolata per estensione hello o per le metriche di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="a66f3-355">È necessario specificare "table" o "sink" o entrambi.</span><span class="sxs-lookup"><span data-stu-id="a66f3-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="a66f3-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="a66f3-356">fileLogs</span></span>

<span data-ttu-id="a66f3-357">Hello controlli acquisizione di file di log.</span><span class="sxs-lookup"><span data-stu-id="a66f3-357">Controls hello capture of log files.</span></span> <span data-ttu-id="a66f3-358">LAD acquisisce di nuove righe di testo quando vengono scritti i file toohello e li scrive tootable righe e/o qualsiasi sink specificato (JsonBlob o EventHub).</span><span class="sxs-lookup"><span data-stu-id="a66f3-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="a66f3-359">Elemento</span><span class="sxs-lookup"><span data-stu-id="a66f3-359">Element</span></span> | <span data-ttu-id="a66f3-360">Valore</span><span class="sxs-lookup"><span data-stu-id="a66f3-360">Value</span></span>
------- | -----
<span data-ttu-id="a66f3-361">file</span><span class="sxs-lookup"><span data-stu-id="a66f3-361">file</span></span> | <span data-ttu-id="a66f3-362">percorso completo di Hello di hello log file toobe controllata e acquisiti.</span><span class="sxs-lookup"><span data-stu-id="a66f3-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="a66f3-363">Hello pathname deve essere un singolo file, il nome Impossibile denominare una directory o i caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="a66f3-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="a66f3-364">tabella</span><span class="sxs-lookup"><span data-stu-id="a66f3-364">table</span></span> | <span data-ttu-id="a66f3-365">tabella di archiviazione di Azure hello (facoltativo), nel servizio di archiviazione hello designato account (come specificato nella configurazione hello protetto), in cui le nuove righe da hello "tail" del file hello vengono scritte.</span><span class="sxs-lookup"><span data-stu-id="a66f3-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="a66f3-366">sinks</span><span class="sxs-lookup"><span data-stu-id="a66f3-366">sinks</span></span> | <span data-ttu-id="a66f3-367">(facoltativo) Un elenco delimitato da virgole di nomi delle righe di log aggiuntivi sink toowhich inviato.</span><span class="sxs-lookup"><span data-stu-id="a66f3-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="a66f3-368">È necessario specificare "table" o "sink" o entrambi.</span><span class="sxs-lookup"><span data-stu-id="a66f3-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="a66f3-369">Metriche supportate dal provider builtin hello</span><span class="sxs-lookup"><span data-stu-id="a66f3-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="a66f3-370">provider di metrica builtin Hello è un'origine di metriche più interessanti tooa ampio gruppo di utenti.</span><span class="sxs-lookup"><span data-stu-id="a66f3-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="a66f3-371">Queste metriche sono suddivise in cinque grandi categorie:</span><span class="sxs-lookup"><span data-stu-id="a66f3-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="a66f3-372">Processore</span><span class="sxs-lookup"><span data-stu-id="a66f3-372">Processor</span></span>
* <span data-ttu-id="a66f3-373">Memoria</span><span class="sxs-lookup"><span data-stu-id="a66f3-373">Memory</span></span>
* <span data-ttu-id="a66f3-374">Rete</span><span class="sxs-lookup"><span data-stu-id="a66f3-374">Network</span></span>
* <span data-ttu-id="a66f3-375">File system</span><span class="sxs-lookup"><span data-stu-id="a66f3-375">Filesystem</span></span>
* <span data-ttu-id="a66f3-376">Disco</span><span class="sxs-lookup"><span data-stu-id="a66f3-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="a66f3-377">metriche Builtin per hello classe del processore</span><span class="sxs-lookup"><span data-stu-id="a66f3-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="a66f3-378">classe del processore delle metriche Hello fornisce informazioni sull'utilizzo del processore in hello VM.</span><span class="sxs-lookup"><span data-stu-id="a66f3-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="a66f3-379">Quando si aggregano le percentuali, il risultato di hello è Media hello per tutte le CPU.</span><span class="sxs-lookup"><span data-stu-id="a66f3-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="a66f3-380">In una macchina virtuale di core due, se un core è stato occupato al 100% e altri hello è inattiva, al 100% hello segnalati che percentidletime sarà 50.</span><span class="sxs-lookup"><span data-stu-id="a66f3-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="a66f3-381">Se il 50% di disponibilità per ogni core hello stesso periodo, hello segnalati risultato sarebbe inoltre 50.</span><span class="sxs-lookup"><span data-stu-id="a66f3-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="a66f3-382">In una macchina virtuale, a quattro core con uno dei core occupato al 100% e hello altri inattivo, hello segnalato che percentidletime sarebbe 75.</span><span class="sxs-lookup"><span data-stu-id="a66f3-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="a66f3-383">counter</span><span class="sxs-lookup"><span data-stu-id="a66f3-383">counter</span></span> | <span data-ttu-id="a66f3-384">Significato</span><span class="sxs-lookup"><span data-stu-id="a66f3-384">Meaning</span></span>
------- | -------
<span data-ttu-id="a66f3-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-385">PercentIdleTime</span></span> | <span data-ttu-id="a66f3-386">Percentuale di tempo durante la finestra di aggregazione hello processori erano in esecuzione il ciclo inattivo di hello kernel</span><span class="sxs-lookup"><span data-stu-id="a66f3-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="a66f3-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-387">PercentProcessorTime</span></span> | <span data-ttu-id="a66f3-388">Percentuale di tempo di esecuzione di un thread non inattivo</span><span class="sxs-lookup"><span data-stu-id="a66f3-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="a66f3-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-389">PercentIOWaitTime</span></span> | <span data-ttu-id="a66f3-390">Percentuale di tempo di attesa per toocomplete di operazioni dei / o</span><span class="sxs-lookup"><span data-stu-id="a66f3-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="a66f3-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-391">PercentInterruptTime</span></span> | <span data-ttu-id="a66f3-392">Percentuale di tempo per l'esecuzione di DPC, ovvero chiamate di procedura differite, e interruzioni di hardware o software</span><span class="sxs-lookup"><span data-stu-id="a66f3-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="a66f3-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-393">PercentUserTime</span></span> | <span data-ttu-id="a66f3-394">Tempo di inattività durante la finestra di aggregazione hello, hello percentuale di tempo impiegato per l'utente più con priorità normale</span><span class="sxs-lookup"><span data-stu-id="a66f3-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="a66f3-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-395">PercentNiceTime</span></span> | <span data-ttu-id="a66f3-396">Tempo di inattività, hello percentuale impiegato per una priorità (nice)</span><span class="sxs-lookup"><span data-stu-id="a66f3-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="a66f3-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="a66f3-398">Tempo di inattività, hello percentuale impiegato in modalità privilegiata (kernel)</span><span class="sxs-lookup"><span data-stu-id="a66f3-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="a66f3-399">Hello primi quattro contatori devono sommare too100%.</span><span class="sxs-lookup"><span data-stu-id="a66f3-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="a66f3-400">Hello ultima tre contatori anche somma too100%. essi suddividere somma hello PercentProcessorTime PercentIOWaitTime e PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="a66f3-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="a66f3-401">impostare una singola misura aggregata su tutti i processori, tooobtain `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="a66f3-402">tooobtain una metrica per un processore specifico, ad esempio hello secondo processore di un tipo di quattro core VM, impostare `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="a66f3-403">I numeri dei processori logici sono nell'intervallo di hello `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="a66f3-404">metriche Builtin per hello classe memoria</span><span class="sxs-lookup"><span data-stu-id="a66f3-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="a66f3-405">classe di memoria delle metriche Hello fornisce informazioni sull'utilizzo della memoria, spostamento e lo scambio.</span><span class="sxs-lookup"><span data-stu-id="a66f3-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="a66f3-406">counter</span><span class="sxs-lookup"><span data-stu-id="a66f3-406">counter</span></span> | <span data-ttu-id="a66f3-407">Significato</span><span class="sxs-lookup"><span data-stu-id="a66f3-407">Meaning</span></span>
------- | -------
<span data-ttu-id="a66f3-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="a66f3-408">AvailableMemory</span></span> | <span data-ttu-id="a66f3-409">Memoria fisica disponibile in MiB</span><span class="sxs-lookup"><span data-stu-id="a66f3-409">Available physical memory in MiB</span></span>
<span data-ttu-id="a66f3-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="a66f3-410">PercentAvailableMemory</span></span> | <span data-ttu-id="a66f3-411">Percentuale della memoria totale che indica la memoria fisica disponibile</span><span class="sxs-lookup"><span data-stu-id="a66f3-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="a66f3-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="a66f3-412">UsedMemory</span></span> | <span data-ttu-id="a66f3-413">Memoria fisica in uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="a66f3-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="a66f3-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="a66f3-414">PercentUsedMemory</span></span> | <span data-ttu-id="a66f3-415">Percentuale della memoria totale che indica la memoria fisica in uso</span><span class="sxs-lookup"><span data-stu-id="a66f3-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="a66f3-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="a66f3-416">PagesPerSec</span></span> | <span data-ttu-id="a66f3-417">Paging totale (lettura/scrittura)</span><span class="sxs-lookup"><span data-stu-id="a66f3-417">Total paging (read/write)</span></span>
<span data-ttu-id="a66f3-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="a66f3-418">PagesReadPerSec</span></span> | <span data-ttu-id="a66f3-419">Pagine lette dall'archivio di backup, ad esempio file di scambio, file di programma, file mappato e così via.</span><span class="sxs-lookup"><span data-stu-id="a66f3-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="a66f3-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="a66f3-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="a66f3-421">Pagine scritte toobacking archiviano (file di scambio, il file mappato e così via)</span><span class="sxs-lookup"><span data-stu-id="a66f3-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="a66f3-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="a66f3-422">AvailableSwap</span></span> | <span data-ttu-id="a66f3-423">Spazio di swapping inutilizzato (MiB)</span><span class="sxs-lookup"><span data-stu-id="a66f3-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="a66f3-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="a66f3-424">PercentAvailableSwap</span></span> | <span data-ttu-id="a66f3-425">Percentuale dello swapping totale che indica lo spazio di swapping inutilizzato</span><span class="sxs-lookup"><span data-stu-id="a66f3-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="a66f3-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="a66f3-426">UsedSwap</span></span> | <span data-ttu-id="a66f3-427">Spazio di swapping in uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="a66f3-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="a66f3-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="a66f3-428">PercentUsedSwap</span></span> | <span data-ttu-id="a66f3-429">Percentuale dello swapping totale che indica lo spazio di swapping in uso</span><span class="sxs-lookup"><span data-stu-id="a66f3-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="a66f3-430">Questa classe di metriche presenta una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="a66f3-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="a66f3-431">attributo "condizione" Hello non è disponibili impostazioni utili e deve essere omessa.</span><span class="sxs-lookup"><span data-stu-id="a66f3-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="a66f3-432">metriche Builtin per hello classe rete</span><span class="sxs-lookup"><span data-stu-id="a66f3-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="a66f3-433">Hello classe delle metriche di rete fornisce informazioni sulle attività di rete su un interfacce di rete singoli dall'avvio.</span><span class="sxs-lookup"><span data-stu-id="a66f3-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="a66f3-434">LAD non espone le metriche relative alla larghezza di banda, che possono essere recuperate dalle metriche dell'host.</span><span class="sxs-lookup"><span data-stu-id="a66f3-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="a66f3-435">counter</span><span class="sxs-lookup"><span data-stu-id="a66f3-435">counter</span></span> | <span data-ttu-id="a66f3-436">Significato</span><span class="sxs-lookup"><span data-stu-id="a66f3-436">Meaning</span></span>
------- | -------
<span data-ttu-id="a66f3-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="a66f3-437">BytesTransmitted</span></span> | <span data-ttu-id="a66f3-438">Byte totali inviati sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="a66f3-438">Total bytes sent since boot</span></span>
<span data-ttu-id="a66f3-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="a66f3-439">BytesReceived</span></span> | <span data-ttu-id="a66f3-440">Byte totali ricevuti sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="a66f3-440">Total bytes received since boot</span></span>
<span data-ttu-id="a66f3-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="a66f3-441">BytesTotal</span></span> | <span data-ttu-id="a66f3-442">Byte totali inviati o ricevuti sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="a66f3-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="a66f3-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="a66f3-443">PacketsTransmitted</span></span> | <span data-ttu-id="a66f3-444">Pacchetti totali inviati sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="a66f3-444">Total packets sent since boot</span></span>
<span data-ttu-id="a66f3-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="a66f3-445">PacketsReceived</span></span> | <span data-ttu-id="a66f3-446">Pacchetti totali ricevuti sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="a66f3-446">Total packets received since boot</span></span>
<span data-ttu-id="a66f3-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="a66f3-447">TotalRxErrors</span></span> | <span data-ttu-id="a66f3-448">Numero di errori di ricezione sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="a66f3-448">Number of receive errors since boot</span></span>
<span data-ttu-id="a66f3-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="a66f3-449">TotalTxErrors</span></span> | <span data-ttu-id="a66f3-450">Numero di errori di trasmissione sin dall'avvio</span><span class="sxs-lookup"><span data-stu-id="a66f3-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="a66f3-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="a66f3-451">TotalCollisions</span></span> | <span data-ttu-id="a66f3-452">Numero di conflitti segnalati dalle porte di rete hello dall'avvio</span><span class="sxs-lookup"><span data-stu-id="a66f3-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="a66f3-453">Anche se questa classe presenta un'istanza, LAD non supporta l'acquisizione delle metriche di rete aggregate per tutti i dispositivi di rete.</span><span class="sxs-lookup"><span data-stu-id="a66f3-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="a66f3-454">impostare le metriche di hello tooobtain per un'interfaccia specifica, ad esempio eth0, `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="a66f3-455">metriche Builtin per hello classe Filesystem</span><span class="sxs-lookup"><span data-stu-id="a66f3-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="a66f3-456">Hello classe Filesystem delle metriche vengono fornite informazioni sull'utilizzo del file System.</span><span class="sxs-lookup"><span data-stu-id="a66f3-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="a66f3-457">Valori assoluti e percentuale vengono segnalati come sono visualizzati tooan utente ordinario (non radice).</span><span class="sxs-lookup"><span data-stu-id="a66f3-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="a66f3-458">counter</span><span class="sxs-lookup"><span data-stu-id="a66f3-458">counter</span></span> | <span data-ttu-id="a66f3-459">Significato</span><span class="sxs-lookup"><span data-stu-id="a66f3-459">Meaning</span></span>
------- | -------
<span data-ttu-id="a66f3-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="a66f3-460">FreeSpace</span></span> | <span data-ttu-id="a66f3-461">Spazio disponibile su disco in byte</span><span class="sxs-lookup"><span data-stu-id="a66f3-461">Available disk space in bytes</span></span>
<span data-ttu-id="a66f3-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="a66f3-462">UsedSpace</span></span> | <span data-ttu-id="a66f3-463">Spazio su disco usato in byte</span><span class="sxs-lookup"><span data-stu-id="a66f3-463">Used disk space in bytes</span></span>
<span data-ttu-id="a66f3-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="a66f3-464">PercentFreeSpace</span></span> | <span data-ttu-id="a66f3-465">Percentuale di spazio libero</span><span class="sxs-lookup"><span data-stu-id="a66f3-465">Percentage free space</span></span>
<span data-ttu-id="a66f3-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="a66f3-466">PercentUsedSpace</span></span> | <span data-ttu-id="a66f3-467">Percentuale di spazio usato</span><span class="sxs-lookup"><span data-stu-id="a66f3-467">Percentage used space</span></span>
<span data-ttu-id="a66f3-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="a66f3-468">PercentFreeInodes</span></span> | <span data-ttu-id="a66f3-469">Percentuale di inode non usati</span><span class="sxs-lookup"><span data-stu-id="a66f3-469">Percentage of unused inodes</span></span>
<span data-ttu-id="a66f3-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="a66f3-470">PercentUsedInodes</span></span> | <span data-ttu-id="a66f3-471">Percentuale di inode allocati, ovvero in uso, sommati tra tutti i file System</span><span class="sxs-lookup"><span data-stu-id="a66f3-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="a66f3-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-472">BytesReadPerSecond</span></span> | <span data-ttu-id="a66f3-473">Byte letti per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-473">Bytes read per second</span></span>
<span data-ttu-id="a66f3-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="a66f3-475">Byte scritti per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-475">Bytes written per second</span></span>
<span data-ttu-id="a66f3-476">Byte al secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-476">BytesPerSecond</span></span> | <span data-ttu-id="a66f3-477">Byte letti o scritti per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-477">Bytes read or written per second</span></span>
<span data-ttu-id="a66f3-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-478">ReadsPerSecond</span></span> | <span data-ttu-id="a66f3-479">Operazioni di lettura per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-479">Read operations per second</span></span>
<span data-ttu-id="a66f3-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-480">WritesPerSecond</span></span> | <span data-ttu-id="a66f3-481">Operazioni di scrittura per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-481">Write operations per second</span></span>
<span data-ttu-id="a66f3-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-482">TransfersPerSecond</span></span> | <span data-ttu-id="a66f3-483">Operazioni di lettura o scrittura per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-483">Read or write operations per second</span></span>

<span data-ttu-id="a66f3-484">È possibile ottenere i valori aggregati in tutti i file System impostando `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="a66f3-485">È possibile ottenere i valori per un determinato file system montato, ad esempio "/mnt", può essere ottenuto impostando `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="a66f3-486">metriche Builtin per hello classe dei dischi</span><span class="sxs-lookup"><span data-stu-id="a66f3-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="a66f3-487">Hello classe dei dischi delle metriche vengono fornite informazioni sull'utilizzo di dispositivo disco.</span><span class="sxs-lookup"><span data-stu-id="a66f3-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="a66f3-488">Queste statistiche si applicano toohello intera unità.</span><span class="sxs-lookup"><span data-stu-id="a66f3-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="a66f3-489">Se sono presenti più file System in un dispositivo, hello contatori per il dispositivo sono, in modo efficiente, tutti gli aggregati.</span><span class="sxs-lookup"><span data-stu-id="a66f3-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="a66f3-490">counter</span><span class="sxs-lookup"><span data-stu-id="a66f3-490">counter</span></span> | <span data-ttu-id="a66f3-491">Significato</span><span class="sxs-lookup"><span data-stu-id="a66f3-491">Meaning</span></span>
------- | -------
<span data-ttu-id="a66f3-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-492">ReadsPerSecond</span></span> | <span data-ttu-id="a66f3-493">Operazioni di lettura per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-493">Read operations per second</span></span>
<span data-ttu-id="a66f3-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-494">WritesPerSecond</span></span> | <span data-ttu-id="a66f3-495">Operazioni di scrittura per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-495">Write operations per second</span></span>
<span data-ttu-id="a66f3-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-496">TransfersPerSecond</span></span> | <span data-ttu-id="a66f3-497">Operazioni totali per secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-497">Total operations per second</span></span>
<span data-ttu-id="a66f3-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-498">AverageReadTime</span></span> | <span data-ttu-id="a66f3-499">Media di secondi per operazione di lettura</span><span class="sxs-lookup"><span data-stu-id="a66f3-499">Average seconds per read operation</span></span>
<span data-ttu-id="a66f3-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-500">AverageWriteTime</span></span> | <span data-ttu-id="a66f3-501">Media di secondi per operazione di scrittura</span><span class="sxs-lookup"><span data-stu-id="a66f3-501">Average seconds per write operation</span></span>
<span data-ttu-id="a66f3-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="a66f3-502">AverageTransferTime</span></span> | <span data-ttu-id="a66f3-503">Media di secondi per operazione</span><span class="sxs-lookup"><span data-stu-id="a66f3-503">Average seconds per operation</span></span>
<span data-ttu-id="a66f3-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="a66f3-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="a66f3-505">Media delle operazioni del disco in coda</span><span class="sxs-lookup"><span data-stu-id="a66f3-505">Average number of queued disk operations</span></span>
<span data-ttu-id="a66f3-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="a66f3-507">Numero di byte letti al secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-507">Number of bytes read per second</span></span>
<span data-ttu-id="a66f3-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="a66f3-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="a66f3-509">Numero di byte scritti al secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-509">Number of bytes written per second</span></span>
<span data-ttu-id="a66f3-510">Byte al secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-510">BytesPerSecond</span></span> | <span data-ttu-id="a66f3-511">Numero di byte letti o scritti al secondo</span><span class="sxs-lookup"><span data-stu-id="a66f3-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="a66f3-512">È possibile ottenere i valori aggregati per tutti i dischi impostando `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="a66f3-513">tooget informazioni per un dispositivo specifico (ad esempio dev/sdf1), impostare `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="a66f3-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="a66f3-514">Installazione e configurazione di LAD 3.0 tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="a66f3-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="a66f3-515">Presupponendo che le impostazioni protette nel file hello Privateconfig e le informazioni di configurazione pubblico sono nella PublicConfig.json, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="a66f3-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="a66f3-516">comando Hello presuppone che si utilizza la modalità di gestione delle risorse Azure hello (arm) di hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="a66f3-517">tooconfigure LAD per distribuzione classica del modello di macchine virtuali (ASM), passare troppo "asm" modalità (`azure config mode asm`) e omettere nome gruppo di risorse hello nel comando hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="a66f3-518">Per ulteriori informazioni, vedere hello [documentazione CLI multipiattaforma](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="a66f3-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="a66f3-519">Una configurazione di LAD 3.0 di esempio</span><span class="sxs-lookup"><span data-stu-id="a66f3-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="a66f3-520">In base che precede le definizioni, una configurazione di estensione di esempio LAD 3.0 con alcune spiegazioni hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="a66f3-521">tooapply questo esempio tooyour case, è necessario usare il proprio nome di account di archiviazione, tenere conto di token di firma di accesso condiviso e i token SAS EventHubs.</span><span class="sxs-lookup"><span data-stu-id="a66f3-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="a66f3-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="a66f3-522">PrivateConfig.json</span></span>

<span data-ttu-id="a66f3-523">Queste impostazioni private consentono di configurare:</span><span class="sxs-lookup"><span data-stu-id="a66f3-523">These private settings configure:</span></span>

* <span data-ttu-id="a66f3-524">un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a66f3-524">a storage account</span></span>
* <span data-ttu-id="a66f3-525">un token SAS dell'account corrispondente</span><span class="sxs-lookup"><span data-stu-id="a66f3-525">a matching account SAS token</span></span>
* <span data-ttu-id="a66f3-526">diversi sink, ad esempio JsonBlob o EventHubs con i token SAS</span><span class="sxs-lookup"><span data-stu-id="a66f3-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

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

### <a name="publicconfigjson"></a><span data-ttu-id="a66f3-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="a66f3-527">PublicConfig.json</span></span>

<span data-ttu-id="a66f3-528">Con queste impostazioni pubbliche il LAD:</span><span class="sxs-lookup"><span data-stu-id="a66f3-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="a66f3-529">Caricare le metriche percentuale tempo processore e spazio su disco utilizzato toohello `WADMetrics*` tabella</span><span class="sxs-lookup"><span data-stu-id="a66f3-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="a66f3-530">Caricare i messaggi syslog funzionalità "user" e alla gravità "info" toohello `LinuxSyslog*` tabella</span><span class="sxs-lookup"><span data-stu-id="a66f3-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="a66f3-531">Caricare raw OMI query risultati (PercentProcessorTime e PercentIdleTime) toohello denominato `LinuxCPU` tabella</span><span class="sxs-lookup"><span data-stu-id="a66f3-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="a66f3-532">Caricare le righe aggiunte nel file `/var/log/myladtestlog` toohello `MyLadTestLog` tabella</span><span class="sxs-lookup"><span data-stu-id="a66f3-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="a66f3-533">In ogni caso, i dati vengono anche caricati:</span><span class="sxs-lookup"><span data-stu-id="a66f3-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="a66f3-534">Archiviazione Blob di Azure (nome del contenitore è definito in sink JsonBlob hello)</span><span class="sxs-lookup"><span data-stu-id="a66f3-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="a66f3-535">Endpoint EventHubs (come specificato nel sink EventHubs hello)</span><span class="sxs-lookup"><span data-stu-id="a66f3-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

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

<span data-ttu-id="a66f3-536">Hello `resourceId` hello configurazione deve corrispondere che di scalabilità di macchine virtuali di macchina virtuale o hello hello impostata.</span><span class="sxs-lookup"><span data-stu-id="a66f3-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="a66f3-537">Le metriche di piattaforma Azure per grafici e di avviso SA resourceId hello di hello macchina virtuale che si sta lavorando.</span><span class="sxs-lookup"><span data-stu-id="a66f3-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="a66f3-538">È previsto che i dati di hello toofind per la macchina virtuale usando una chiave di ricerca di hello resourceId hello.</span><span class="sxs-lookup"><span data-stu-id="a66f3-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="a66f3-539">Se si usano Azure scalabilità automatica, resourceId hello nella configurazione della scalabilità automatica hello devono corrispondere resourceId hello utilizzato da LAD.</span><span class="sxs-lookup"><span data-stu-id="a66f3-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="a66f3-540">resourceId Hello viene compilata in nomi di hello di JsonBlobs scritti da LAD.</span><span class="sxs-lookup"><span data-stu-id="a66f3-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="a66f3-541">Visualizzare i dati</span><span class="sxs-lookup"><span data-stu-id="a66f3-541">View your data</span></span>

<span data-ttu-id="a66f3-542">Utilizzare i dati sulle prestazioni tooview portale Azure hello o impostare gli avvisi:</span><span class="sxs-lookup"><span data-stu-id="a66f3-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![immagine](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="a66f3-544">Hello `performanceCounters` dati vengono sempre archiviati in una tabella di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="a66f3-545">Le API di Archiviazione di Azure sono disponibili per più linguaggi e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="a66f3-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="a66f3-546">Dati inviati tooJsonBlob sink vengono archiviati nel BLOB nell'account di archiviazione hello denominato in hello [protetto impostazioni](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="a66f3-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="a66f3-547">È possibile utilizzare i dati di blob hello tramite le API di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="a66f3-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="a66f3-548">Inoltre, è possibile utilizzare questi dati di hello tooaccess degli strumenti dell'interfaccia utente in archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="a66f3-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="a66f3-549">Esplora server di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a66f3-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="a66f3-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Microsoft Azure Storage Explorer").</span><span class="sxs-lookup"><span data-stu-id="a66f3-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="a66f3-551">Questo snapshot di una sessione di Microsoft Azure Storage Explorer Mostra hello generate tabelle di archiviazione di Azure e i contenitori da un'estensione LAD 3.0 configurata correttamente in una macchina virtuale di test.</span><span class="sxs-lookup"><span data-stu-id="a66f3-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="a66f3-552">immagine di Hello non corrisponde esattamente alla hello [configurazione di esempio 3.0 LAD](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="a66f3-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![immagine](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="a66f3-554">Vedere hello rilevante [EventHubs documentazione](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn come tooconsume messaggi pubblicati tooan EventHubs endpoint.</span><span class="sxs-lookup"><span data-stu-id="a66f3-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a66f3-555">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a66f3-555">Next steps</span></span>

* <span data-ttu-id="a66f3-556">Creare metrici avvisi in [Monitor Azure](../../monitoring-and-diagnostics/insights-alerts-portal.md) per le metriche di hello è raccogliere.</span><span class="sxs-lookup"><span data-stu-id="a66f3-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="a66f3-557">Creare [grafici di monitoraggio](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) per le metriche.</span><span class="sxs-lookup"><span data-stu-id="a66f3-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="a66f3-558">Informazioni su come troppo[creare un set di scalabilità della macchina virtuale](/azure/virtual-machines/linux/tutorial-create-vmss) tramite la scalabilità automatica toocontrol metriche.</span><span class="sxs-lookup"><span data-stu-id="a66f3-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
