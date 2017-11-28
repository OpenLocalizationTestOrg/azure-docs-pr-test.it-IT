---
title: aaaUsing hello Azure CLI 2.0 con l'archiviazione di Azure | Documenti Microsoft
description: "Informazioni su come toouse hello interfaccia della riga di comando di Azure (Azure CLI) 2.0 con toocreate di archiviazione di Azure e gestire gli account di archiviazione e utilizzo di BLOB di Azure e i file. Hello Azure CLI 2.0 è uno strumento di multipiattaforma scritto in Python."
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
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="4c1d7-104">Utilizzo di hello Azure CLI 2.0 con archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4c1d7-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="4c1d7-105">Hello open source, multipiattaforma Azure CLI versione 2.0 fornisce un set di comandi per l'utilizzo di hello piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="4c1d7-106">Fornisce gran parte delle stesse funzionalità, vedere hello hello [portale di Azure](https://portal.azure.com), incluso l'accesso a dati complessi.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="4c1d7-107">In questa Guida, verrà illustrato come hello toouse [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform diverse attività di utilizzo delle risorse nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="4c1d7-108">È consigliabile scaricare e installare o aggiornare toohello la versione più recente di hello CLI 2.0 prima di utilizzare questa Guida.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="4c1d7-109">esempi di Hello in hello Guida prevedono l'uso di hello di hello shell Bash in Ubuntu, ma altre piattaforme devono eseguire in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="4c1d7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4c1d7-110">Prerequisites</span></span>
<span data-ttu-id="4c1d7-111">Questa guida presuppone la conoscenza dei concetti di base hello dell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="4c1d7-112">Si presuppone inoltre che si è in grado di toosatisfy hello creazione requisiti dell'account specificate di seguito per Azure e hello servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="4c1d7-113">Account</span><span class="sxs-lookup"><span data-stu-id="4c1d7-113">Accounts</span></span>
* <span data-ttu-id="4c1d7-114">**Account Azure**: se non si ha già una sottoscrizione di Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="4c1d7-115">**Account di archiviazione**: vedere [Creare un account di archiviazione](../storage/storage-create-storage-account.md#create-a-storage-account) in [Informazioni sugli account di archiviazione di Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="4c1d7-116">Installare hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4c1d7-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="4c1d7-117">Scaricare e installare hello Azure CLI 2.0 seguendo le istruzioni di hello fornite in [installare Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="4c1d7-118">Se si verificano problemi con l'installazione di hello, estrarre hello [la risoluzione dei problemi di installazione](/cli/azure/install-az-cli2#installation-troubleshooting) sezione dell'articolo hello e hello [la risoluzione dei problemi di installazione](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) Guida su GitHub.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="4c1d7-119">Utilizzo di hello CLI</span><span class="sxs-lookup"><span data-stu-id="4c1d7-119">Working with hello CLI</span></span>

<span data-ttu-id="4c1d7-120">Dopo aver installato hello CLI, è possibile utilizzare hello `az` comando nei comandi CLI di Azure hello tooaccess interfaccia della riga di comando (Bash, Terminal, il prompt dei comandi).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="4c1d7-121">Hello tipo `az` comando toosee un elenco completo dei comandi di base hello (hello output di esempio seguente è stata troncata):</span><span class="sxs-lookup"><span data-stu-id="4c1d7-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="4c1d7-122">Nell'interfaccia della riga di comando, eseguire il comando hello `az storage --help` hello toolist `storage` comando sottogruppi.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="4c1d7-123">le descrizioni di Hello dei sottogruppi di hello viene fornita una panoramica di hello funzionalità hello che CLI di Azure fornisce per lavorare con le risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

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
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="4c1d7-124">Connettersi hello CLI tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="4c1d7-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="4c1d7-125">toowork con risorse hello nella sottoscrizione di Azure, è necessario innanzitutto accedere tooyour account Azure con `az login`.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="4c1d7-126">È possibile eseguire l'accesso in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="4c1d7-127">**Accesso interattivo**: `az login`</span><span class="sxs-lookup"><span data-stu-id="4c1d7-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="4c1d7-128">**Accesso con nome utente e password**: `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="4c1d7-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="4c1d7-129">Questo non funziona con gli account Microsoft o gli account che usano Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="4c1d7-130">**Accesso con un'entità servizio**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="4c1d7-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="4c1d7-131">Script di esempio dell'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4c1d7-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="4c1d7-132">Successivamente, è necessario utilizzare uno script della shell di piccole dimensioni che emette qualche toointeract di comandi CLI di Azure 2.0 base con le risorse di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="4c1d7-133">script Hello prima crea un nuovo contenitore nell'account di archiviazione, quindi carica un contenitore di toothat file (come un blob) esistente.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="4c1d7-134">Vengono quindi elencati tutti i BLOB nel contenitore hello e infine Scarica la destinazione nel computer locale che specificano tooa file hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="4c1d7-135">**Configurare ed eseguire script hello**</span><span class="sxs-lookup"><span data-stu-id="4c1d7-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="4c1d7-136">Aprire un editor di testo, quindi copiare e incollare hello precedente script nell'editor di hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="4c1d7-137">Aggiornare quindi tooreflect variabili dello script hello le impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="4c1d7-138">Sostituire hello valori, come specificato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="4c1d7-139">**\<storage_account_name\>**  nome hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="4c1d7-140">**\<storage_account_key\>**  chiave di accesso primaria o secondaria hello per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="4c1d7-141">**\<container_name\>**  un nome hello toocreate di nuovo contenitore, ad esempio "azure-cli-esempio-container".</span><span class="sxs-lookup"><span data-stu-id="4c1d7-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="4c1d7-142">**\<blob_name\>**  un nome per il blob di destinazione hello nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="4c1d7-143">**\<file_to_upload\>**  hello percorso toosmall file nel computer locale, ad esempio "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="4c1d7-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="4c1d7-144">**\<destination_file\>**  hello percorso file di destinazione, ad esempio "~ / downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="4c1d7-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="4c1d7-145">Dopo aver aggiornato le variabili necessarie hello, salvare script hello e chiudere l'editor.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="4c1d7-146">passaggi successivi Hello si supponga che è stato denominato script **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="4c1d7-147">Contrassegna script hello come eseguibile, se necessario:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="4c1d7-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="4c1d7-148">Eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-148">Execute hello script.</span></span> <span data-ttu-id="4c1d7-149">Ad esempio, in Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="4c1d7-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="4c1d7-150">Dovrebbe vedere seguenti toohello simili di output e hello  **\<destination_file\>**  specificato nel hello script devono essere visualizzate sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="4c1d7-151">Hello precedente l'output è in **tabella** formato.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="4c1d7-152">È possibile specificare quale output formato toouse specificando hello `--output` argomento nei comandi CLI, o impostare il valore a livello globale tramite `az configure`.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="4c1d7-153">Gestire gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4c1d7-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="4c1d7-154">Creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-154">Create a new storage account</span></span>
<span data-ttu-id="4c1d7-155">toouse archiviazione di Azure, è necessario un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="4c1d7-156">È possibile creare un nuovo account di archiviazione di Azure dopo aver configurato il computer troppo[connettere sottoscrizione tooyour](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="4c1d7-157">`--location` [Richiesto]: posizione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="4c1d7-158">Ad esempio "Stati Uniti occidentali".</span><span class="sxs-lookup"><span data-stu-id="4c1d7-158">For example, "West US".</span></span>
* <span data-ttu-id="4c1d7-159">`--name`[Obbligatorio]: nome account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="4c1d7-160">nome Hello deve essere di lunghezza 3 caratteri too24 e utilizzare solo caratteri alfanumerici minuscoli.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="4c1d7-161">`--resource-group`[Richiesto]: il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="4c1d7-162">`--sku`[Obbligatorio]: hello SKU di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="4c1d7-163">Valori consentiti:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="4c1d7-164">Impostare le variabili di ambiente predefinite dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4c1d7-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="4c1d7-165">È possibile avere più account di archiviazione nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="4c1d7-166">tooselect uno di questi comandi toouse per tutti gli archivi successive, è possibile impostare queste variabili di ambiente:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="4c1d7-167">Un altro modo tooset un account di archiviazione predefinito consiste nell'utilizzare una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="4c1d7-168">Innanzitutto, ottenere la stringa di connessione hello con hello `show-connection-string` comando:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="4c1d7-169">Quindi hello copia stringa di connessione di output e impostare hello `AZURE_STORAGE_CONNECTION_STRING` variabile di ambiente (potrebbe essere necessario tooenclose stringa di connessione hello racchiuso tra virgolette):</span><span class="sxs-lookup"><span data-stu-id="4c1d7-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="4c1d7-170">Tutti gli esempi di hello le sezioni seguenti di questo articolo si presuppongono di aver impostato hello `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY` le variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="4c1d7-171">Creare e gestire gli account di accesso</span><span class="sxs-lookup"><span data-stu-id="4c1d7-171">Create and manage blobs</span></span>
<span data-ttu-id="4c1d7-172">Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="4c1d7-173">Questa sezione presuppone la conoscenza dei concetti relativi al servizio di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="4c1d7-174">Per informazioni dettagliate, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md) e [Concetti relativi al servizio BLOB](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="4c1d7-175">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="4c1d7-175">Create a container</span></span>
<span data-ttu-id="4c1d7-176">Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="4c1d7-177">È possibile creare un contenitore utilizzando hello `az storage container create` comando:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="4c1d7-178">È possibile impostare uno dei tre livelli di accesso in lettura per un nuovo contenitore specificando hello facoltativo `--public-access` argomento:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="4c1d7-179">`off`(impostazione predefinita): dati del contenitore sono privato toohello proprietario dell'account.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="4c1d7-180">`blob`: Accesso in lettura pubblico per i BLOB.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="4c1d7-181">`container`: Lettura ed elenco accesso toohello intero contenitore pubblico.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="4c1d7-182">Per ulteriori informazioni, vedere [gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-182">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="4c1d7-183">Caricare un contenitore di blob tooa</span><span class="sxs-lookup"><span data-stu-id="4c1d7-183">Upload a blob tooa container</span></span>
<span data-ttu-id="4c1d7-184">Archiviazione BLOB di Azure supporta BLOB in blocchi, BLOB di accodamento e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="4c1d7-185">Caricamento BLOB tooa contenitore usando hello `blob upload` comando:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="4c1d7-186">Per impostazione predefinita, hello `blob upload` comando Carica BLOB toopage di file VHD o BLOB in blocchi in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="4c1d7-187">toospecify un altro tipo quando si carica un blob, è possibile usare hello `--type` argomento, ovvero i valori consentito sono `append`, `block`, e `page`.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="4c1d7-188">Per ulteriori informazioni sui tipi di blob diversi hello, vedere [informazioni sui BLOB in blocchi, BLOB di accodamento e BLOB di pagine](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="4c1d7-189">Scaricare un BLOB da un contenitore</span><span class="sxs-lookup"><span data-stu-id="4c1d7-189">Download a blob from a container</span></span>
<span data-ttu-id="4c1d7-190">Questo esempio viene illustrato come toodownload un blob da un contenitore:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="4c1d7-191">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="4c1d7-191">List hello blobs in a container</span></span>

<span data-ttu-id="4c1d7-192">Elencare i BLOB hello in un contenitore con hello [elenco blob di archiviazione az](/cli/azure/storage/blob#list) comando.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="4c1d7-193">Copiare i BLOB</span><span class="sxs-lookup"><span data-stu-id="4c1d7-193">Copy blobs</span></span>
<span data-ttu-id="4c1d7-194">È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="4c1d7-195">Hello esempio seguente viene illustrato come toocopy BLOB da un archivio account tooanother.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="4c1d7-196">È necessario creare un contenitore nell'account di archiviazione di origine hello, specificando l'accesso in lettura pubblico per il BLOB.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="4c1d7-197">Successivamente, si carica un contenitore toohello file e infine copia hello blob dal contenitore in un contenitore nell'account di archiviazione di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="4c1d7-198">In hello esempio precedente, il contenitore di destinazione hello deve esistere già nell'account di archiviazione di destinazione hello per toosucceed operazione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="4c1d7-199">Inoltre, i blob origine hello specificato in hello `--source-uri` argomento deve includere un token di firma di accesso condiviso oppure essere accessibile pubblicamente, come nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="4c1d7-200">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="4c1d7-200">Delete a blob</span></span>
<span data-ttu-id="4c1d7-201">toodelete un blob, utilizzare hello `blob delete` comando:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="4c1d7-202">Creare e gestire condivisioni di file</span><span class="sxs-lookup"><span data-stu-id="4c1d7-202">Create and manage file shares</span></span>
<span data-ttu-id="4c1d7-203">Archiviazione di File di Azure offre archiviazione condivisa per le applicazioni mediante protocollo Server Message Block (SMB) hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="4c1d7-204">Macchine virtuali di Microsoft Azure e servizi cloud, nonché applicazioni locali, possono condividere i dati di file tra condivisioni montate.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="4c1d7-205">È possibile gestire condivisioni file e dati di file tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="4c1d7-206">Per ulteriori informazioni sull'archiviazione di File di Azure, vedere [Introduzione all'archiviazione di File di Azure in Windows](storage-dotnet-how-to-use-files.md) o [come archiviazione di File di Azure con Linux toouse](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4c1d7-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="4c1d7-207">Creare una condivisione file</span><span class="sxs-lookup"><span data-stu-id="4c1d7-207">Create a file share</span></span>
<span data-ttu-id="4c1d7-208">Una condivisione di archiviazione file è una condivisione file SMB di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="4c1d7-209">Tutte le directory e i file devono essere creati in una condivisione padre.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="4c1d7-210">Un account può contenere un numero illimitato di condivisioni e una condivisione può archiviare un numero illimitato di file, i limiti di capacità toohello hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="4c1d7-211">esempio Hello crea una condivisione file denominata **myshare**.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="4c1d7-212">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="4c1d7-212">Create a directory</span></span>
<span data-ttu-id="4c1d7-213">Una directory fornisce una struttura gerarchica in una condivisione di file di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="4c1d7-214">esempio Hello crea una directory denominata **myDir** nella condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="4c1d7-215">Un percorso di directory può includere più livelli, ad esempio **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="4c1d7-216">Tuttavia, prima di creare una sottodirectory, è necessario assicurarsi che tutte le directory padre esistano.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="4c1d7-217">Ad esempio, per il percorso **dir1/dir2**, è necessario creare prima la directory **dir1** e poi la directory **dir2**.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="4c1d7-218">Caricare una condivisione di file locale tooa</span><span class="sxs-lookup"><span data-stu-id="4c1d7-218">Upload a local file tooa share</span></span>
<span data-ttu-id="4c1d7-219">esempio Hello carica un file da **~/temp/samplefile.txt** tooroot di hello **myshare** condivisione file.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="4c1d7-220">Hello `--source` argomento specifica tooupload file locale esistente hello.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="4c1d7-221">Come per la creazione della directory, è possibile specificare un percorso di directory all'interno di hello condivisione tooupload hello tooan esistente directory del file nella condivisione di hello:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="4c1d7-222">Un file nella condivisione di hello può essere backup too1 TB nella dimensione.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="4c1d7-223">Elencare i file hello in una condivisione</span><span class="sxs-lookup"><span data-stu-id="4c1d7-223">List hello files in a share</span></span>
<span data-ttu-id="4c1d7-224">È possibile elencare i file e directory in una condivisione con hello `az storage file list` comando:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="4c1d7-225">Copiare i file</span><span class="sxs-lookup"><span data-stu-id="4c1d7-225">Copy files</span></span>      
<span data-ttu-id="4c1d7-226">È possibile copiare un file con estensione tooanother, un blob tooa file o un file di blob tooa.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="4c1d7-227">Ad esempio, una directory tooa del file in una condivisione diversa toocopy:</span><span class="sxs-lookup"><span data-stu-id="4c1d7-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="4c1d7-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c1d7-228">Next steps</span></span>
<span data-ttu-id="4c1d7-229">Ecco alcune risorse aggiuntive per ottenere ulteriori informazioni sull'utilizzo di hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="4c1d7-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="4c1d7-230">Introduzione all'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4c1d7-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="4c1d7-231">Riferimento ai comandi dell'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4c1d7-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="4c1d7-232">Interfaccia della riga di comando di Azure 2.0 su GitHub</span><span class="sxs-lookup"><span data-stu-id="4c1d7-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
