---
title: Monitoraggio di una macchina virtuale Linux con un'estensione VM | Documentazione Microsoft
description: Informazioni su come usare l'estensione di diagnostica Linux per monitorare le prestazioni e i dati di diagnostica di una VM Linux in Azure.
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: b8c6e2e22d8478b6e92e7b7942f15d37a840fed3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-linux-diagnostic-extension-to-monitor-the-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="885b6-103">Uso dell'estensione di diagnostica Linux per monitorare le prestazioni e i dati di diagnostica di una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="885b6-103">Use the Linux Diagnostic Extension to monitor the performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="885b6-104">Questo documento descrive la versione 2.3 dell'estensione Diagnostica per Linux.</span><span class="sxs-lookup"><span data-stu-id="885b6-104">This document describes version 2.3 of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="885b6-105">Questa versione è deprecata e la sua pubblicazione potrebbe essere annullata a partire dal 30 giugno 2018.</span><span class="sxs-lookup"><span data-stu-id="885b6-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="885b6-106">È stata sostituita dalla versione 3.0.</span><span class="sxs-lookup"><span data-stu-id="885b6-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="885b6-107">Per altre informazioni, vedere la [documentazione per la versione 3.0 dell'estensione Diagnostica per Linux](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="885b6-107">For more information, see the [documentation for version 3.0 of the Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="885b6-108">Introduzione</span><span class="sxs-lookup"><span data-stu-id="885b6-108">Introduction</span></span>

<span data-ttu-id="885b6-109">**Nota**: l'estensione della diagnostica Linux è open source in [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic), dove vengono pubblicate per prime le informazioni più aggiornate sull'estensione.</span><span class="sxs-lookup"><span data-stu-id="885b6-109">(**Note**: The Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where the most current information on the extension is first published.</span></span> <span data-ttu-id="885b6-110">È possibile vedere la [pagina GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic).</span><span class="sxs-lookup"><span data-stu-id="885b6-110">You might want to check the [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="885b6-111">L'estensione di diagnostica Linux consente all'utente di monitorare le VM Linux eseguite in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="885b6-111">The Linux Diagnostic Extension helps a user monitor the Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="885b6-112">Questo servizio offre le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="885b6-112">It has the following capabilities:</span></span>

* <span data-ttu-id="885b6-113">Raccoglie e carica informazioni sulle prestazioni del sistema dalla VM Linux alla tabella di archiviazione dell'utente, incluse informazioni di diagnostica e di syslog.</span><span class="sxs-lookup"><span data-stu-id="885b6-113">Collects and uploads the system performance information from the Linux VM to the user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="885b6-114">Consente agli utenti di personalizzare la metrica dei dati che verrà raccolta e caricata.</span><span class="sxs-lookup"><span data-stu-id="885b6-114">Enables users to customize the data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="885b6-115">Consente agli utenti di caricare in una tabella di archiviazione designata i file di log specificati.</span><span class="sxs-lookup"><span data-stu-id="885b6-115">Enables users to upload specified log files to a designated storage table.</span></span>

<span data-ttu-id="885b6-116">Nella versione 2.3 i dati includono:</span><span class="sxs-lookup"><span data-stu-id="885b6-116">In the current version 2.3, the data includes:</span></span>

* <span data-ttu-id="885b6-117">Tutti i log Rsyslog Linux, inclusi i log di sistema, sicurezza e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="885b6-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="885b6-118">Tutti i dati di sistema specificati nel [sito System Center Cross Platform Solutions](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="885b6-118">All system data that's specified on [the System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="885b6-119">I file di log specificati dall'utente.</span><span class="sxs-lookup"><span data-stu-id="885b6-119">User-specified log files.</span></span>

<span data-ttu-id="885b6-120">Questa estensione funziona sia con i modelli classici che con i modelli di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="885b6-120">This extension works with both the classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-the-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="885b6-121">Versione corrente dell'estensione e versioni precedenti deprecate</span><span class="sxs-lookup"><span data-stu-id="885b6-121">Current version of the extension and deprecation of old versions</span></span>

<span data-ttu-id="885b6-122">La versione più recente dell'estensione è la **2.3**, mentre **tutte le versioni precedenti, ovvero le versioni 2.0, 2.1 e 2.2, verranno deprecate, annullandone la pubblicazione entro la fine di quest'anno (2017)**.</span><span class="sxs-lookup"><span data-stu-id="885b6-122">The latest version of the extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="885b6-123">Se è installata l'estensione di diagnostica Linux con disabilitato l'aggiornamento automatico della versione secondaria, è consigliabile disinstallare l'estensione e reinstallarla abilitando l'aggiornamento automatico della versione secondaria.</span><span class="sxs-lookup"><span data-stu-id="885b6-123">If you installed the Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall the extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="885b6-124">Nelle macchine virtuali classiche (ASM), è possibile ottenere questo risultato specificando '2.*' come versione, se si installa l'estensione tramite Powershell o l'interfaccia della riga di comando XPLAT di Azure.</span><span class="sxs-lookup"><span data-stu-id="885b6-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="885b6-125">Nelle macchine virtuali ARM, è possibile ottenere questo risultato includendo '"autoUpgradeMinorVersion": true' nel modello di distribuzione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="885b6-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span> <span data-ttu-id="885b6-126">Inoltre, in qualsiasi nuova installazione dell'estensione dovrebbe essere attivata l'opzione di aggiornamento automatico alla versione secondaria.</span><span class="sxs-lookup"><span data-stu-id="885b6-126">Also, any new installation of the extension should have the auto minor version upgrade option turned on.</span></span>

## <a name="enable-the-extension"></a><span data-ttu-id="885b6-127">Abilitare l'estensione</span><span class="sxs-lookup"><span data-stu-id="885b6-127">Enable the extension</span></span>

<span data-ttu-id="885b6-128">È possibile abilitare questa estensione usando il [portale di Azure](https://portal.azure.com/#), Azure PowerShell o gli script dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="885b6-128">You can enable this extension by using the [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="885b6-129">Per visualizzare e configurare i dati di sistema e le prestazioni direttamente dal portale di Azure, seguire questa [procedura nel blog di Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="885b6-129">To view and configure the system and performance data directly from the Azure portal, follow [these steps on the Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="885b6-130">Questo articolo illustra come abilitare e configurare l'estensione usando i comandi dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="885b6-130">This article focuses on how to enable and configure the extension by using Azure CLI commands.</span></span> <span data-ttu-id="885b6-131">In questo modo è possibile leggere e visualizzare i dati direttamente dalla tabella di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="885b6-131">This allows you to read and view the data directly from the storage table.</span></span>

<span data-ttu-id="885b6-132">Si noti che i metodi di configurazione descritti qui non funzioneranno per il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="885b6-132">Note that the configuration methods that are described here won't work for the Azure portal.</span></span> <span data-ttu-id="885b6-133">Per visualizzare e configurare i dati di sistema e prestazioni direttamente dal portale di Azure, l'estensione deve essere abilitata con il portale.</span><span class="sxs-lookup"><span data-stu-id="885b6-133">To view and configure the system and performance data directly from the Azure portal, the extension must be enabled through the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="885b6-134">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="885b6-134">Prerequisites</span></span>

* <span data-ttu-id="885b6-135">**Agente Linux di Azure 2.0.6 o versione successiva**.</span><span class="sxs-lookup"><span data-stu-id="885b6-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="885b6-136">Si noti che la maggior parte delle immagini della raccolta Linux di macchine virtuali di Azure include la versione 2.0.6 o successive.</span><span class="sxs-lookup"><span data-stu-id="885b6-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="885b6-137">È possibile eseguire **WAAgent -version** per verificare la versione installata nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="885b6-137">You can run **WAAgent -version** to confirm which version is installed on the VM.</span></span> <span data-ttu-id="885b6-138">Se la macchina virtuale esegue una versione precedente alla 2.0.6, è possibile seguire queste [istruzioni in GitHub](https://github.com/Azure/WALinuxAgent "istruzioni") per aggiornarla.</span><span class="sxs-lookup"><span data-stu-id="885b6-138">If the VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") to update it.</span></span>
* <span data-ttu-id="885b6-139">**Interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="885b6-139">**Azure CLI**.</span></span> <span data-ttu-id="885b6-140">Seguire le linee guida in [Installare l'interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md) per configurare l'ambiente dell'interfaccia della riga di comando di Azure nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="885b6-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) to set up the Azure CLI environment on your machine.</span></span> <span data-ttu-id="885b6-141">Dopo l'installazione dell'interfaccia della riga di comando di Azure, sarà possibile usare il comando **azure** nell'interfaccia della riga di comando (Bash, terminale o prompt dei comandi) per accedere ai relativi comandi.</span><span class="sxs-lookup"><span data-stu-id="885b6-141">After Azure CLI is installed, you can use the **azure** command from your command-line interface (Bash, Terminal, or command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="885b6-142">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="885b6-142">For example:</span></span>

  * <span data-ttu-id="885b6-143">Eseguire **azure vm extension set --help** per informazioni della Guida dettagliate.</span><span class="sxs-lookup"><span data-stu-id="885b6-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="885b6-144">Eseguire **azure login** per accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="885b6-144">Run **azure login** to sign in to Azure.</span></span>
  * <span data-ttu-id="885b6-145">Eseguire **azure vm list** per elencare tutte le macchine virtuali disponibili in Azure.</span><span class="sxs-lookup"><span data-stu-id="885b6-145">Run **azure vm list** to list all the virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="885b6-146">Un account di archiviazione per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="885b6-146">A storage account to store the data.</span></span> <span data-ttu-id="885b6-147">Saranno necessari un nome di account di archiviazione creato in precedenza e una chiave di accesso per caricare i dati nella risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="885b6-147">You will need a storage account name that was created previously and an access key to upload the data to your storage.</span></span>

## <a name="use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension"></a><span data-ttu-id="885b6-148">Usare l'interfaccia della riga di comando di Azure per abilitare l'estensione della diagnostica Linux</span><span class="sxs-lookup"><span data-stu-id="885b6-148">Use the Azure CLI command to enable the Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-the-extension-with-the-default-data-set"></a><span data-ttu-id="885b6-149">Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="885b6-149">Scenario 1.</span></span> <span data-ttu-id="885b6-150">Abilitare l'estensione con il set di dati predefinito</span><span class="sxs-lookup"><span data-stu-id="885b6-150">Enable the extension with the default data set</span></span>

<span data-ttu-id="885b6-151">Nella versione 2.3 e successive i dati predefiniti che verranno raccolti includono:</span><span class="sxs-lookup"><span data-stu-id="885b6-151">In version 2.3 or later, the default data that will be collected includes:</span></span>

* <span data-ttu-id="885b6-152">Tutte le informazioni Rsyslog (inclusi i log di sistema, sicurezza e applicazioni).</span><span class="sxs-lookup"><span data-stu-id="885b6-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="885b6-153">Un set principale di dati di sistema di base.</span><span class="sxs-lookup"><span data-stu-id="885b6-153">A core set of basis system data.</span></span> <span data-ttu-id="885b6-154">Si noti che il set di dati completo è descritto nel [sito System Center Cross Platform Solutions](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="885b6-154">Note that the full data set is described on the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="885b6-155">Per abilitare dati aggiuntivi, proseguire con i passaggi degli scenari 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="885b6-155">If you want to enable extra data, continue with the steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="885b6-156">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="885b6-156">Step 1.</span></span> <span data-ttu-id="885b6-157">Creare un file denominato PrivateConfig.json con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="885b6-157">Create a file named PrivateConfig.json with the following content:</span></span>

    {
        "storageAccountName" : "the storage account to receive data",
        "storageAccountKey" : "the key of the account"
    }

<span data-ttu-id="885b6-158">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="885b6-158">Step 2.</span></span> <span data-ttu-id="885b6-159">Eseguire **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="885b6-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-the-performance-monitor-metrics"></a><span data-ttu-id="885b6-160">Scenario 2.</span><span class="sxs-lookup"><span data-stu-id="885b6-160">Scenario 2.</span></span> <span data-ttu-id="885b6-161">Personalizzare le metriche di monitoraggio delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="885b6-161">Customize the performance monitor metrics</span></span>

<span data-ttu-id="885b6-162">In questa sezione viene descritto come personalizzare la tabella dati delle prestazioni e della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="885b6-162">This section describes how to customize the performance and diagnostic data table.</span></span>

<span data-ttu-id="885b6-163">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="885b6-163">Step 1.</span></span> <span data-ttu-id="885b6-164">Creare un file denominato PrivateConfig.json con il contenuto descritto nello scenario 1.</span><span class="sxs-lookup"><span data-stu-id="885b6-164">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="885b6-165">Creare anche un file denominato PublicConfig.json.</span><span class="sxs-lookup"><span data-stu-id="885b6-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="885b6-166">Specificare i dati specifici che si desidera raccogliere.</span><span class="sxs-lookup"><span data-stu-id="885b6-166">Specify the particular data you want to collect.</span></span>

<span data-ttu-id="885b6-167">Per tutti i provider e le variabili supportati, vedere il [sito System Center Cross Platform Solutions](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="885b6-167">For all supported providers and variables, reference the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="885b6-168">È possibile disporre di più query e archiviarle in più tabelle aggiungendo altre query nello script.</span><span class="sxs-lookup"><span data-stu-id="885b6-168">You can have multiple queries and store them in multiple tables by appending more queries to the script.</span></span>

<span data-ttu-id="885b6-169">Per impostazione predefinita i dati Rsyslog verranno sempre raccolti.</span><span class="sxs-lookup"><span data-stu-id="885b6-169">By default, the Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="885b6-170">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="885b6-170">Step 2.</span></span> <span data-ttu-id="885b6-171">Eseguire **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="885b6-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="885b6-172">Scenario 3.</span><span class="sxs-lookup"><span data-stu-id="885b6-172">Scenario 3.</span></span> <span data-ttu-id="885b6-173">Caricamento dei propri file di log</span><span class="sxs-lookup"><span data-stu-id="885b6-173">Upload your own log files</span></span>

<span data-ttu-id="885b6-174">Questa sezione descrive come raccogliere e caricare file di log specifici nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="885b6-174">This section describes how to collect and upload specific log files to your storage account.</span></span> <span data-ttu-id="885b6-175">È necessario specificare sia il percorso del file di log che il nome della tabella in cui si vuole archiviare il log.</span><span class="sxs-lookup"><span data-stu-id="885b6-175">You need to specify both the path to your log file and the name of the table where you want to store your log.</span></span> <span data-ttu-id="885b6-176">È possibile creare più file di log aggiungendo più voci di file/tabella nello script.</span><span class="sxs-lookup"><span data-stu-id="885b6-176">You can create multiple log files by adding multiple file/table entries to the script.</span></span>

<span data-ttu-id="885b6-177">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="885b6-177">Step 1.</span></span> <span data-ttu-id="885b6-178">Creare un file denominato PrivateConfig.json con il contenuto descritto nello scenario 1.</span><span class="sxs-lookup"><span data-stu-id="885b6-178">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="885b6-179">Creare quindi un altro file denominato PublicConfig.json con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="885b6-179">Then create another file named PublicConfig.json with the following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="885b6-180">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="885b6-180">Step 2.</span></span> <span data-ttu-id="885b6-181">Eseguire `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="885b6-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="885b6-182">Si noti che con questa impostazione nelle versioni dell'estensione precedenti la 2.3, tutti i log scritti in `/var/log/mysql.err` potrebbero essere duplicati anche in `/var/log/syslog` o `/var/log/messages` a seconda del distributore di Linux.</span><span class="sxs-lookup"><span data-stu-id="885b6-182">Note that with this setting on the extension versions prior to 2.3, all logs written to `/var/log/mysql.err` might be duplicated to `/var/log/syslog` (or `/var/log/messages` depending on the Linux distro) as well.</span></span> <span data-ttu-id="885b6-183">Se si vuole evitare la registrazione duplicata, è possibile escludere la registrazione dei log `local6` della struttura nella configurazione rsyslog.</span><span class="sxs-lookup"><span data-stu-id="885b6-183">If you'd like to avoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="885b6-184">Dipende dalla distribuzione di Linux, ma in un sistema di Ubuntu 14.04, il file da modificare è `/etc/rsyslog.d/50-default.conf` ed è possibile sostituire la riga `*.*;auth,authpriv.none -/var/log/syslog` con `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="885b6-184">It depends on the Linux distro, but on an Ubuntu 14.04 system, the file to modify is `/etc/rsyslog.d/50-default.conf` and you can replace the line `*.*;auth,authpriv.none -/var/log/syslog` to `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="885b6-185">Il problema viene risolto nell'ultimo aggiornamento rapido 2.3 (2.3.9007), pertanto se si dispone della versione dell'estensione 2.3 il problema non dovrebbe verificarsi.</span><span class="sxs-lookup"><span data-stu-id="885b6-185">This issue is fixed in the latest hotfix release of 2.3 (2.3.9007), so if you have the extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="885b6-186">Se invece il problema persiste anche dopo aver riavviato la VM, è possibile contattarci e aiutarci a rintracciare il motivo per cui l'ultima versione dell'aggiornamento rapido non viene installata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="885b6-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why the latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-the-extension-from-collecting-any-logs"></a><span data-ttu-id="885b6-187">Scenario 4.</span><span class="sxs-lookup"><span data-stu-id="885b6-187">Scenario 4.</span></span> <span data-ttu-id="885b6-188">Arrestare la raccolta di log dell'estensione</span><span class="sxs-lookup"><span data-stu-id="885b6-188">Stop the extension from collecting any logs</span></span>

<span data-ttu-id="885b6-189">Questa sezione descrive come arrestare la raccolta di log da parte dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="885b6-189">This section describes how to stop the extension from collecting logs.</span></span> <span data-ttu-id="885b6-190">Si noti che il processo dell'agente di monitoraggio sarà operativo anche con questa riconfigurazione.</span><span class="sxs-lookup"><span data-stu-id="885b6-190">Note that the monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="885b6-191">Per arrestare completamente il processo dell'agente di monitoraggio, è possibile disabilitare l'estensione.</span><span class="sxs-lookup"><span data-stu-id="885b6-191">If you'd like to stop the monitoring agent process completely, you can do so by disabling the extension.</span></span> <span data-ttu-id="885b6-192">Il comando per disabilitare l'estensione è `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="885b6-192">The command to disable the extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="885b6-193">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="885b6-193">Step 1.</span></span> <span data-ttu-id="885b6-194">Creare un file denominato PrivateConfig.json con il contenuto descritto nello scenario 1.</span><span class="sxs-lookup"><span data-stu-id="885b6-194">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="885b6-195">Creare un altro file denominato PublicConfig.json con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="885b6-195">Create another file named PublicConfig.json with the following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="885b6-196">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="885b6-196">Step 2.</span></span> <span data-ttu-id="885b6-197">Eseguire **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="885b6-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="885b6-198">Esaminare i dati</span><span class="sxs-lookup"><span data-stu-id="885b6-198">Review your data</span></span>

<span data-ttu-id="885b6-199">I dati delle prestazioni e della diagnostica vengono archiviati in una tabella di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="885b6-199">The performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="885b6-200">Per informazioni su come accedere ai dati nella tabella di archiviazione usando gli script dell'interfaccia della riga di comando di Azure, vedere [Come usare l'archivio tabelle di Azure da Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) .</span><span class="sxs-lookup"><span data-stu-id="885b6-200">Review [How to use Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) to learn how to access the data in the storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="885b6-201">È anche possibile usare gli strumenti dell'interfaccia utente seguenti per accedere ai dati:</span><span class="sxs-lookup"><span data-stu-id="885b6-201">In addition, you can use following UI tools to access the data:</span></span>

1. <span data-ttu-id="885b6-202">Esplora server di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="885b6-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="885b6-203">Passare all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="885b6-203">Go to your storage account.</span></span> <span data-ttu-id="885b6-204">Dopo circa cinque minuti dall'esecuzione della VM, verranno visualizzate le quattro tabelle predefinite: "LinuxCpu", "LinuxDisk", "LinuxMemory" e "Linuxsyslog".</span><span class="sxs-lookup"><span data-stu-id="885b6-204">After the VM runs for about five minutes, you'll see the four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="885b6-205">Fare doppio clic sui nomi delle tabelle per visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="885b6-205">Double-click the table names to view the data.</span></span>
1. <span data-ttu-id="885b6-206">[Esplora archivi di Azure](https://azurestorageexplorer.codeplex.com/ "Esplora archivi di Azure").</span><span class="sxs-lookup"><span data-stu-id="885b6-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![immagine](./media/diagnostic-extension/no1.png)

<span data-ttu-id="885b6-208">Se è stato abilitato fileCfg o perfCfg (come illustrato negli scenari 2 e 3), è possibile usare Esplora server di Visual Studio e Azure Storage Explorer per visualizzare i dati non predefiniti.</span><span class="sxs-lookup"><span data-stu-id="885b6-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer to view non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="885b6-209">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="885b6-209">Known issues</span></span>

* <span data-ttu-id="885b6-210">Le informazioni Rsyslog e il file di log specificato dal cliente sono accessibili solo tramite scripting.</span><span class="sxs-lookup"><span data-stu-id="885b6-210">The Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
