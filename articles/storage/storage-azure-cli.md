---
title: Uso dell'interfaccia della riga di comando di Azure 2.0 con Archiviazione di Azure | Documentazione Microsoft
description: "Informazioni su come usare l'interfaccia della riga di comando di Azure 2.0 con Archiviazione di Azure per creare e gestire gli account di archiviazione e usare file e BLOB di Azure. L'interfaccia della riga di comando di Azure 2.0 è uno strumento multipiattaforma compilato in Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 6098216f7dd901ea48fb3ab969c7934cc288b247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="534d5-104">Uso dell'interfaccia della riga di comando di Azure 2.0 con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="534d5-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="534d5-105">L'interfaccia della riga di comando di Azure 2.0, open-source e multipiattaforma, offre un insieme di comandi per usare la piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="534d5-106">Fornisce gran parte delle funzionalità disponibili nel [portale di Azure](https://portal.azure.com) incluso l'accesso ai dati complessi.</span><span class="sxs-lookup"><span data-stu-id="534d5-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="534d5-107">Questa guida illustra come usare l'[interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) per eseguire diverse attività con le risorse nell'account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="534d5-108">Prima di usare questa guida, si consiglia di scaricare e installare oppure di aggiornare il sistema alla versione più recente dell'interfaccia della riga di comando 2.0.</span><span class="sxs-lookup"><span data-stu-id="534d5-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="534d5-109">Gli esempi di questa guida presuppongono l'uso della shell Bash in Ubuntu, ma la procedura dovrebbe funzionare in modo simile anche nelle altre piattaforme.</span><span class="sxs-lookup"><span data-stu-id="534d5-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="534d5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="534d5-110">Prerequisites</span></span>
<span data-ttu-id="534d5-111">Questa guida si presuppone che si conoscano i concetti di base dell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="534d5-112">e possa soddisfare i requisiti di creazione dell'account specificati di seguito per Azure e per il servizio Archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="534d5-113">Account</span><span class="sxs-lookup"><span data-stu-id="534d5-113">Accounts</span></span>
* <span data-ttu-id="534d5-114">**Account Azure**: se non si ha già una sottoscrizione di Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="534d5-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="534d5-115">**Account di archiviazione**: vedere [Creare un account di archiviazione](../storage/storage-create-storage-account.md#create-a-storage-account) in [Informazioni sugli account di archiviazione di Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="534d5-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="534d5-116">Installare l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="534d5-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="534d5-117">Scaricare e installare l'interfaccia della riga di comando di Azure 2.0 seguendo le istruzioni riportate in [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="534d5-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="534d5-118">Se si riscontrano problemi con l'installazione, consultare la sezione [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) (Risoluzione dei problemi di installazione) dell'articolo e la guida [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) (Risoluzione dei problemi di installazione) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="534d5-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="534d5-119">Uso dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="534d5-119">Working with the CLI</span></span>

<span data-ttu-id="534d5-120">Dopo l'installazione dell'interfaccia della riga di comando, sarà possibile usare il comando `az` nell'interfaccia della riga di comando (Bash, terminale, prompt dei comandi) per accedere ai relativi comandi.</span><span class="sxs-lookup"><span data-stu-id="534d5-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="534d5-121">Digitare il comando `az` per visualizzare un elenco completo dei comandi di base (l'output di esempio seguente è stato troncato):</span><span class="sxs-lookup"><span data-stu-id="534d5-121">Type the `az` command to see a full list of the base commands (the following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="534d5-122">Nell'interfaccia della riga di comando eseguire il comando `az storage --help` per elencare i sottogruppi del comando `storage`.</span><span class="sxs-lookup"><span data-stu-id="534d5-122">In your command-line interface, execute the command `az storage --help` to list the `storage` command subgroups.</span></span> <span data-ttu-id="534d5-123">Le descrizioni dei sottogruppi forniscono una panoramica delle funzionalità che l'interfaccia della riga di comando offre per lavorare con le risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues to effectively scale applications according to traffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="534d5-124">Connettere l'interfaccia della riga di comando alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="534d5-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="534d5-125">Per lavorare con le risorse nella sottoscrizione di Azure è necessario innanzitutto accedere al proprio account Azure con `az login`.</span><span class="sxs-lookup"><span data-stu-id="534d5-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="534d5-126">È possibile eseguire l'accesso in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="534d5-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="534d5-127">**Accesso interattivo**: `az login`</span><span class="sxs-lookup"><span data-stu-id="534d5-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="534d5-128">**Accesso con nome utente e password**: `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="534d5-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="534d5-129">Questo non funziona con gli account Microsoft o gli account che usano Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="534d5-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="534d5-130">**Accesso con un'entità servizio**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="534d5-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="534d5-131">Script di esempio dell'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="534d5-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="534d5-132">Successivamente useremo un piccolo script della shell che attiva alcuni semplici comandi dell'interfaccia della riga di comando di Azure 2.0 per interagire con risorse di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="534d5-133">Innanzitutto lo script crea un nuovo contenitore nell'account di archiviazione e poi carica un file esistente (come un BLOB) in tale contenitore.</span><span class="sxs-lookup"><span data-stu-id="534d5-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="534d5-134">Quindi genera un elenco di tutti i BLOB nel contenitore e infine scarica il file in una destinazione specificata nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="534d5-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create --name $container_name

echo "Uploading the file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing the blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading the file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="534d5-135">**Configurare ed eseguire lo script**</span><span class="sxs-lookup"><span data-stu-id="534d5-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="534d5-136">Aprire un editor di testo quindi copiare e incollare lo script precedente nell'editor.</span><span class="sxs-lookup"><span data-stu-id="534d5-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="534d5-137">A questo punto aggiornare le variabili dello script in modo che riflettano le impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="534d5-138">Sostituire i seguenti valori come indicato:</span><span class="sxs-lookup"><span data-stu-id="534d5-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="534d5-139">**\<storage_account_name\>** Il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="534d5-140">**\<storage_account_key\>** La chiave di accesso primaria o secondaria per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="534d5-141">**\<container_name\>** Un nome per il nuovo contenitore da creare, come "azure-cli-sample-container".</span><span class="sxs-lookup"><span data-stu-id="534d5-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="534d5-142">**\<blob_name\>** Un nome per il BLOB di destinazione nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="534d5-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="534d5-143">**\<file_to_upload\>** Il percorso di un piccolo file nel computer locale, come "~/images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="534d5-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="534d5-144">**\<destination_file\>** Il percorso del file di destinazione, come "~/downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="534d5-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="534d5-145">Dopo aver aggiornato le variabili necessarie, salvare lo script e chiudere l'editor.</span><span class="sxs-lookup"><span data-stu-id="534d5-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="534d5-146">I passaggi successivi presuppongono che allo sript sia stato assegnato il nome **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="534d5-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="534d5-147">Contrassegnare lo script come eseguibile, se necessario:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="534d5-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="534d5-148">Eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="534d5-148">Execute the script.</span></span> <span data-ttu-id="534d5-149">Ad esempio, in Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="534d5-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="534d5-150">Verrà visualizzato un output simile al seguente e il **\<destination_file\>** specificato nello script dovrebbe essere visualizzato sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="534d5-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
{
  "created": true
}
Uploading the file...
Percent complete: %100.0
Listing the blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading the file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="534d5-151">L'output precedente è in formato **tabella**.</span><span class="sxs-lookup"><span data-stu-id="534d5-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="534d5-152">È possibile specificare il formato di output da usare specificando l'argomento `--output` nei comandi dell'interfaccia della riga di comando oppure impostarlo a livello globale tramite `az configure`.</span><span class="sxs-lookup"><span data-stu-id="534d5-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="534d5-153">Gestire gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="534d5-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="534d5-154">Creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-154">Create a new storage account</span></span>
<span data-ttu-id="534d5-155">Per usare Archiviazione di Azure, è necessario un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="534d5-156">Dopo aver configurato il computer per [connettersi alla sottoscrizione](#connect-to-your-azure-subscription), è possibile creare un nuovo account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="534d5-157">`--location` [Richiesto]: posizione.</span><span class="sxs-lookup"><span data-stu-id="534d5-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="534d5-158">Ad esempio "Stati Uniti occidentali".</span><span class="sxs-lookup"><span data-stu-id="534d5-158">For example, "West US".</span></span>
* <span data-ttu-id="534d5-159">`--name` [Richiesto]: il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-159">`--name` [Required]: The storage account name.</span></span> <span data-ttu-id="534d5-160">Il nome può contenere da 3 a 24 caratteri e usare solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="534d5-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="534d5-161">`--resource-group`[Richiesto]: il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="534d5-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="534d5-162">`--sku` [Richiesto]: lo SKU dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="534d5-163">Valori consentiti:</span><span class="sxs-lookup"><span data-stu-id="534d5-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="534d5-164">Impostare le variabili di ambiente predefinite dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="534d5-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="534d5-165">È possibile avere più account di archiviazione nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="534d5-166">Per selezionarne uno da usare per tutti i comandi di archiviazione successivi, è possibile impostare queste variabili di ambiente:</span><span class="sxs-lookup"><span data-stu-id="534d5-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="534d5-167">Un altro modo per impostare un account di archiviazione predefinito è mediante una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="534d5-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="534d5-168">In primo luogo ottenere la stringa di connessione con il comando `show-connection-string`:</span><span class="sxs-lookup"><span data-stu-id="534d5-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="534d5-169">Quindi copiare la stringa di connessione di output e impostare la variabile di ambiente `AZURE_STORAGE_CONNECTION_STRING` (potrebbe essere necessario racchiudere la stringa di connessione tra virgolette):</span><span class="sxs-lookup"><span data-stu-id="534d5-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="534d5-170">Tutti gli esempi nelle sezioni seguenti di questo articolo presuppongono che siano state impostate le variabili di ambiente `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY`.</span><span class="sxs-lookup"><span data-stu-id="534d5-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="534d5-171">Creare e gestire gli account di accesso</span><span class="sxs-lookup"><span data-stu-id="534d5-171">Create and manage blobs</span></span>
<span data-ttu-id="534d5-172">Archivio BLOB di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binari, a cui è possibile accedere da qualsiasi parte del mondo tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="534d5-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="534d5-173">Questa sezione presuppone la conoscenza dei concetti relativi al servizio di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="534d5-174">Per informazioni dettagliate, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md) e [Concetti relativi al servizio BLOB](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="534d5-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="534d5-175">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="534d5-175">Create a container</span></span>
<span data-ttu-id="534d5-176">Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="534d5-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="534d5-177">È possibile creare un contenitore usando il comando `az storage container create`:</span><span class="sxs-lookup"><span data-stu-id="534d5-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="534d5-178">È possibile impostare uno fra tre livelli di accesso in lettura per un nuovo contenitore specificando l'argomento opzionale `--public-access`:</span><span class="sxs-lookup"><span data-stu-id="534d5-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="534d5-179">`off`(impostazione predefinita): i dati del contenitore sono privati per il proprietario dell'account.</span><span class="sxs-lookup"><span data-stu-id="534d5-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="534d5-180">`blob`: Accesso in lettura pubblico per i BLOB.</span><span class="sxs-lookup"><span data-stu-id="534d5-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="534d5-181">`container`: Accesso in lettura e per elenchi pubblico all'intero contenitore.</span><span class="sxs-lookup"><span data-stu-id="534d5-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="534d5-182">Per altre informazioni, vedere [Gestire l'accesso in lettura anonimo a contenitori e BLOB](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="534d5-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="534d5-183">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="534d5-183">Upload a blob to a container</span></span>
<span data-ttu-id="534d5-184">Archiviazione BLOB di Azure supporta BLOB in blocchi, BLOB di accodamento e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="534d5-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="534d5-185">Caricare i BLOB in un contenitore utilizzando il comando `blob upload`:</span><span class="sxs-lookup"><span data-stu-id="534d5-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="534d5-186">Per impostazione predefinita il comando `blob upload` carica i file *.vhd in BLOB di pagine o altrimenti in BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="534d5-186">By default, the `blob upload` command uploads *.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="534d5-187">Per specificare un altro tipo quando si carica un BLOB, è possibile usare l'argomento `--type`: i valori consentiti sono `append`, `block` e `page`.</span><span class="sxs-lookup"><span data-stu-id="534d5-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="534d5-188">Per altre informazioni sui diversi tipi di BLOB, vedere [Informazioni sui BLOB in blocchi, sui BLOB di accodamento e sui BLOB di pagine](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="534d5-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="534d5-189">Scaricare un BLOB da un contenitore</span><span class="sxs-lookup"><span data-stu-id="534d5-189">Download a blob from a container</span></span>
<span data-ttu-id="534d5-190">Questo esempio dimostra come scaricare i BLOB da un contenitore:</span><span class="sxs-lookup"><span data-stu-id="534d5-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="534d5-191">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="534d5-191">List the blobs in a container</span></span>

<span data-ttu-id="534d5-192">Elencare i BLOB in un contenitore con il comando [az storage blob list](/cli/azure/storage/blob#list).</span><span class="sxs-lookup"><span data-stu-id="534d5-192">List the blobs in a container with the [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="534d5-193">Copiare i BLOB</span><span class="sxs-lookup"><span data-stu-id="534d5-193">Copy blobs</span></span>
<span data-ttu-id="534d5-194">È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="534d5-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="534d5-195">Nell'esempio seguente viene illustrato come copiare BLOB da un account di archiviazione a un altro.</span><span class="sxs-lookup"><span data-stu-id="534d5-195">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="534d5-196">Prima di tutto si crea un contenitore nell'account di archiviazione di origine, specificando l'accesso in lettura pubblico per i suoi BLOB.</span><span class="sxs-lookup"><span data-stu-id="534d5-196">We first create a container in the source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="534d5-197">Quindi si carica un file nel contenitore e infine si copia il BLOB dal contenitore in un contenitore nell'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-197">Next, we upload a file to the container, and finally, copy the blob from that container into a container in the destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob to container in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account to destination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="534d5-198">Nell'esempio precedente, perché l'operazione di copia riesca il contenitore di destinazione deve esistere già nell'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-198">In the above example, the destination container must already exist in the destination storage account for the copy operation to succeed.</span></span> <span data-ttu-id="534d5-199">Inoltre, il BLOB di origine specificato nell'argomento `--source-uri` deve includere un token di firma di accesso condiviso oppure essere accessibile pubblicamente, come in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="534d5-199">Additionally, the source blob specified in the `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="534d5-200">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="534d5-200">Delete a blob</span></span>
<span data-ttu-id="534d5-201">Per eliminare un BLOB, usare il comando `blob delete`:</span><span class="sxs-lookup"><span data-stu-id="534d5-201">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="534d5-202">Creare e gestire condivisioni di file</span><span class="sxs-lookup"><span data-stu-id="534d5-202">Create and manage file shares</span></span>
<span data-ttu-id="534d5-203">L'archiviazione file di Azure offre un'archiviazione condivisa per le applicazioni che usano il protocollo Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="534d5-203">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="534d5-204">Macchine virtuali di Microsoft Azure e servizi cloud, nonché applicazioni locali, possono condividere i dati di file tra condivisioni montate.</span><span class="sxs-lookup"><span data-stu-id="534d5-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="534d5-205">È possibile gestire condivisioni di file e dati di file tramite la CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-205">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="534d5-206">Per altre informazioni su Archiviazione file di Azure, vedere [Introduzione ad Archiviazione file di Azure in Windows](storage-dotnet-how-to-use-files.md) o [Come usare Archiviazione file di Azure con Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="534d5-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="534d5-207">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="534d5-207">Create a file share</span></span>
<span data-ttu-id="534d5-208">Una condivisione di archiviazione file è una condivisione file SMB di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="534d5-209">Tutte le directory e i file devono essere creati in una condivisione padre.</span><span class="sxs-lookup"><span data-stu-id="534d5-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="534d5-210">Un account può contenere un numero illimitato di condivisioni e una condivisione può archiviare un numero illimitato di file, fino ai limiti di capacità dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="534d5-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="534d5-211">Nell'esempio seguente viene creata una condivisione file denominata **myshare**.</span><span class="sxs-lookup"><span data-stu-id="534d5-211">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="534d5-212">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="534d5-212">Create a directory</span></span>
<span data-ttu-id="534d5-213">Una directory fornisce una struttura gerarchica in una condivisione di file di Azure.</span><span class="sxs-lookup"><span data-stu-id="534d5-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="534d5-214">Nell'esempio seguente viene creata una directory denominata **myDir** nella condivisione di file.</span><span class="sxs-lookup"><span data-stu-id="534d5-214">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="534d5-215">Un percorso di directory può includere più livelli, ad esempio **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="534d5-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="534d5-216">Tuttavia, prima di creare una sottodirectory, è necessario assicurarsi che tutte le directory padre esistano.</span><span class="sxs-lookup"><span data-stu-id="534d5-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="534d5-217">Ad esempio, per il percorso **dir1/dir2**, è necessario creare prima la directory **dir1** e poi la directory **dir2**.</span><span class="sxs-lookup"><span data-stu-id="534d5-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="534d5-218">Caricare un file locale da condividere</span><span class="sxs-lookup"><span data-stu-id="534d5-218">Upload a local file to a share</span></span>
<span data-ttu-id="534d5-219">Nell'esempio seguente viene caricato un file da **~/temp/samplefile.txt** nella radice della condivisione file **myshare**.</span><span class="sxs-lookup"><span data-stu-id="534d5-219">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="534d5-220">L'argomento `--source` specifica il file locale esistente da caricare.</span><span class="sxs-lookup"><span data-stu-id="534d5-220">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="534d5-221">Come con la creazione di directory, è possibile specificare un percorso di directory all'interno della condivisione per caricare il file in una directory esistente all'interno della condivisione:</span><span class="sxs-lookup"><span data-stu-id="534d5-221">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="534d5-222">Un file della condivisione può avere una dimensione massima di 1 TB.</span><span class="sxs-lookup"><span data-stu-id="534d5-222">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="534d5-223">Elencare i file di una condivisione</span><span class="sxs-lookup"><span data-stu-id="534d5-223">List the files in a share</span></span>
<span data-ttu-id="534d5-224">È possibile elencare i file e le directory di una condivisione tramite il comando `az storage file list`:</span><span class="sxs-lookup"><span data-stu-id="534d5-224">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list --share-name myshare --output table

# List the files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List the files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="534d5-225">Copiare i file</span><span class="sxs-lookup"><span data-stu-id="534d5-225">Copy files</span></span>      
<span data-ttu-id="534d5-226">È possibile copiare un file in un altro file, un file in un BLOB o un BLOB in un file.</span><span class="sxs-lookup"><span data-stu-id="534d5-226">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="534d5-227">Ad esempio, per copiare un file in una directory di un'altra condivisione:</span><span class="sxs-lookup"><span data-stu-id="534d5-227">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="534d5-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="534d5-228">Next steps</span></span>
<span data-ttu-id="534d5-229">Di seguito sono segnalate altre risorse relative all'utilizzo dell'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="534d5-229">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* [<span data-ttu-id="534d5-230">Introduzione all'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="534d5-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="534d5-231">Riferimento ai comandi dell'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="534d5-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="534d5-232">Interfaccia della riga di comando di Azure 2.0 su GitHub</span><span class="sxs-lookup"><span data-stu-id="534d5-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
