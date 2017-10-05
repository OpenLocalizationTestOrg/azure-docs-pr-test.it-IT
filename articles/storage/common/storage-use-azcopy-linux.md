---
title: Copiare o spostare dati in Archiviazione di Microsoft Azure con AzCopy in Linux | Microsoft Docs
description: "Usare l'utilità AzCopy in Linux per spostare o copiare dati da o verso BLOB e contenuto del file. Copiare i dati in archiviazione di Azure da file locali o copiare i dati all'interno o tra account di archiviazione. Migrare facilmente i dati in archiviazione di Azure."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: 441227d84b9c1ec721ae36fdc423ba797654f128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="69472-105">Trasferire dati con AzCopy in Linux</span><span class="sxs-lookup"><span data-stu-id="69472-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="69472-106">AzCopy in Linux è un'utilità della riga di comando progettata la copia dei dati da e verso l'archiviazione BLOB e file di Microsoft Azure usando semplici comandi con prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="69472-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="69472-107">È possibile copiare dati da un oggetto a un altro all'interno dell'account di archiviazione o tra account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="69472-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="69472-108">Esistono due versioni di AzCopy che è possibile scaricare.</span><span class="sxs-lookup"><span data-stu-id="69472-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="69472-109">AzCopy in Linux viene compilato con .NET Core Framework per le piattaforme Linux e offre opzioni della riga di comando in stile POSIX.</span><span class="sxs-lookup"><span data-stu-id="69472-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="69472-110">[AzCopy in Windows](../storage-use-azcopy.md) viene compilato con .NET Framework e offre opzioni della riga di comando in stile Windows.</span><span class="sxs-lookup"><span data-stu-id="69472-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="69472-111">Questo articolo descrive AzCopy in Linux.</span><span class="sxs-lookup"><span data-stu-id="69472-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="69472-112">Scaricare e installare AzCopy</span><span class="sxs-lookup"><span data-stu-id="69472-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="69472-113">Installazione in Linux</span><span class="sxs-lookup"><span data-stu-id="69472-113">Installation on Linux</span></span>

<span data-ttu-id="69472-114">AzCopy in Linux richiede .NET Core Framework sulla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="69472-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="69472-115">Vedere le istruzioni per l'installazione nella pagina di [.NET Core](https://www.microsoft.com/net/core#linuxubuntu).</span><span class="sxs-lookup"><span data-stu-id="69472-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="69472-116">Ecco un esempio di installazione di .NET Core in Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="69472-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="69472-117">Per le istruzioni di installazione più recenti, vedere la pagina di installazione di [.NET Core in Linux](https://www.microsoft.com/net/core#linuxubuntu).</span><span class="sxs-lookup"><span data-stu-id="69472-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="69472-118">Dopo aver installato .NET Core, scaricare e installare AzCopy.</span><span class="sxs-lookup"><span data-stu-id="69472-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="69472-119">Dopo aver installato AzCopy in Linux, è possibile rimuovere i file estratti.</span><span class="sxs-lookup"><span data-stu-id="69472-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="69472-120">In alternativa, se non si hanno autorizzazioni come superuser, è possibile eseguire AzCopy usando lo script della shell 'azcopy' nella cartella estratta.</span><span class="sxs-lookup"><span data-stu-id="69472-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="69472-121">Installazione alternativa in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="69472-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="69472-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="69472-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="69472-123">Aggiungere un'origine apt per .Net Core:</span><span class="sxs-lookup"><span data-stu-id="69472-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="69472-124">Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:</span><span class="sxs-lookup"><span data-stu-id="69472-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="69472-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="69472-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="69472-126">Aggiungere un'origine apt per .Net Core:</span><span class="sxs-lookup"><span data-stu-id="69472-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="69472-127">Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:</span><span class="sxs-lookup"><span data-stu-id="69472-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="69472-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="69472-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="69472-129">Aggiungere un'origine apt per .Net Core:</span><span class="sxs-lookup"><span data-stu-id="69472-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="69472-130">Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:</span><span class="sxs-lookup"><span data-stu-id="69472-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="69472-131">Scrittura del primo comando AzCopy </span><span class="sxs-lookup"><span data-stu-id="69472-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="69472-132">La sintassi di base per i comandi di AzCopy è la seguente:</span><span class="sxs-lookup"><span data-stu-id="69472-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="69472-133">Gli esempi seguenti illustrano vari scenari per la copia dei dati da e in BLOB e file di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="69472-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="69472-134">Per una spiegazione dettagliata dei parametri usati in ogni esempio, fare riferimento al menu `azcopy --help`.</span><span class="sxs-lookup"><span data-stu-id="69472-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="69472-135">BLOB: scaricare</span><span class="sxs-lookup"><span data-stu-id="69472-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="69472-136">Scaricare un singolo BLOB</span><span class="sxs-lookup"><span data-stu-id="69472-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="69472-137">Se la cartella `/mnt/myfiles` non esiste ancora, AzCopy la crea e scarica `abc.txt ` nella nuova cartella.</span><span class="sxs-lookup"><span data-stu-id="69472-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="69472-138">Scaricare un singolo BLOB da un'area secondaria</span><span class="sxs-lookup"><span data-stu-id="69472-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="69472-139">È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="69472-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="69472-140">Scaricare tutti BLOB</span><span class="sxs-lookup"><span data-stu-id="69472-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="69472-141">Si supponga che i BLOB seguenti risiedano nel contenitore specificato:</span><span class="sxs-lookup"><span data-stu-id="69472-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="69472-142">Dopo l'operazione di download, la directory `/mnt/myfiles` include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="69472-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="69472-143">Se non si specifica l'opzione `--recursive`, non verrà scaricato alcun BLOB.</span><span class="sxs-lookup"><span data-stu-id="69472-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="69472-144">Scaricare i BLOB con il prefisso specificato</span><span class="sxs-lookup"><span data-stu-id="69472-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="69472-145">Si supponga che i BLOB seguenti risiedano nel contenitore specificato.</span><span class="sxs-lookup"><span data-stu-id="69472-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="69472-146">Vengono scaricati tutti i BLOB che iniziano con il prefisso `a`.</span><span class="sxs-lookup"><span data-stu-id="69472-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="69472-147">Dopo l'operazione di download, la cartella `/mnt/myfiles` include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="69472-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="69472-148">Il prefisso si applica alla directory virtuale che forma la prima parte del nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="69472-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="69472-149">Nell'esempio precedente, la directory virtuale non corrisponde al prefisso specificato, quindi non viene scaricato alcun BLOB.</span><span class="sxs-lookup"><span data-stu-id="69472-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="69472-150">Se inoltre l'opzione `--recursive` non è specificata, AzCopy non scarica alcun BLOB.</span><span class="sxs-lookup"><span data-stu-id="69472-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="69472-151">Impostare l'ora dell'ultima modifica dei file esportati sulla stessa ora dei BLOB di origine</span><span class="sxs-lookup"><span data-stu-id="69472-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="69472-152">È anche possibile escludere BLOB dall'operazione di download in base all'ora dell'ultima modifica.</span><span class="sxs-lookup"><span data-stu-id="69472-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="69472-153">Se ad esempio si vogliono escludere i BLOB in cui l'ora dell'ultima modifica è uguale o successiva a quella del file di destinazione, aggiungere l'opzione `--exclude-newer` .</span><span class="sxs-lookup"><span data-stu-id="69472-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="69472-154">In alternativa, se si vogliono escludere i BLOB in cui l'ora dell'ultima modifica è uguale o precedente a quella del file di destinazione, aggiungere l'opzione `--exclude-older` .</span><span class="sxs-lookup"><span data-stu-id="69472-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="69472-155">BLOB: caricare</span><span class="sxs-lookup"><span data-stu-id="69472-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="69472-156">Caricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="69472-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="69472-157">Se il contenitore di destinazione specificato non esiste, AzCopy ne crea uno e vi carica il file.</span><span class="sxs-lookup"><span data-stu-id="69472-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="69472-158">Caricare un singolo file nella directory virtuale</span><span class="sxs-lookup"><span data-stu-id="69472-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="69472-159">Se la directory virtuale specificata non esiste, AzCopy carica il file in modo da includere la directory virtuale nel nome del BLOB, *ovvero* `vd/abc.txt` nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="69472-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="69472-160">Caricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="69472-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="69472-161">Se si specifica l'opzione `--recursive`, il contenuto della directory specificata viene caricato nell'archiviazione BLOB in modo ricorsivo, ovvero vengono caricati anche tutte le sottocartelle e i relativi file.</span><span class="sxs-lookup"><span data-stu-id="69472-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="69472-162">Si supponga ad esempio che i file seguenti risiedano nella cartella `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="69472-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="69472-163">Dopo l'operazione di caricamento, il contenitore include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="69472-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="69472-164">Quando l'opzione `--recursive` non viene specificata, vengono caricati solo i tre file seguenti:</span><span class="sxs-lookup"><span data-stu-id="69472-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="69472-165">Caricare i file corrispondenti ai criteri specificati</span><span class="sxs-lookup"><span data-stu-id="69472-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="69472-166">Si supponga che i file seguenti risiedano nella cartella `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="69472-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="69472-167">Dopo l'operazione di caricamento, il contenitore include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="69472-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="69472-168">Quando l'opzione `--recursive` non viene specificata, AzCopy ignora file presenti nelle sottodirectory:</span><span class="sxs-lookup"><span data-stu-id="69472-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="69472-169">Specificare il tipo di contenuto MIME di un BLOB di destinazione</span><span class="sxs-lookup"><span data-stu-id="69472-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="69472-170">Per impostazione predefinita, AzCopy imposta il tipo di contenuto di un BLOB di destinazione su `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="69472-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="69472-171">È tuttavia possibile specificare il tipo di contenuto in modo esplicito tramite l'opzione `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="69472-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="69472-172">Questa sintassi imposta il tipo di contenuto per tutti i BLOB in un'operazione di caricamento.</span><span class="sxs-lookup"><span data-stu-id="69472-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="69472-173">Se si specifica l'opzione `--set-content-type` senza fornire un valore, AzCopy imposta il tipo di contenuto di ogni BLOB o file in base all'estensione di ciascuno di questi elementi.</span><span class="sxs-lookup"><span data-stu-id="69472-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="69472-174">BLOB: copiare</span><span class="sxs-lookup"><span data-stu-id="69472-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="69472-175">Copiare un BLOB all'interno di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="69472-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="69472-176">Quando si copia un BLOB senza l'opzione --sync-copy, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="69472-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="69472-177">Copiare un singolo BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="69472-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="69472-178">Quando si copia un BLOB senza l'opzione --sync-copy, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="69472-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="69472-179">Copiare in BLOB singolo da un'area secondaria all'area primaria</span><span class="sxs-lookup"><span data-stu-id="69472-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="69472-180">È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="69472-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="69472-181">Copiare un singolo BLOB e i relativi snapshot tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="69472-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="69472-182">Dopo l'operazione di copia, il contenitore di destinazione include il BLOB e i relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="69472-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="69472-183">Il contenitore include i BLOB seguenti e i relativi snapshot:</span><span class="sxs-lookup"><span data-stu-id="69472-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="69472-184">Copiare in modo sincrono i BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="69472-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="69472-185">Per impostazione predefinita, AzCopy copia i dati tra due endpoint di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="69472-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="69472-186">L'operazione di copia viene pertanto eseguita in background sfruttando la capacità di larghezza di banda disponibile non limitata da alcun contratto di servizio relativo alla velocità di copia di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="69472-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="69472-187">L'opzione `--sync-copy` garantisce che l'operazione di copia avvenga a velocità costante.</span><span class="sxs-lookup"><span data-stu-id="69472-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="69472-188">AzCopy esegue la copia sincrona scaricando i BLOB da copiare dall'origine specificata nella memoria locale, per poi caricarli nella destinazione dell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="69472-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="69472-189">`--sync-copy`, tuttavia, può generare costi aggiuntivi in uscita rispetto alla copia asincrona.</span><span class="sxs-lookup"><span data-stu-id="69472-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="69472-190">Per evitare costi in uscita, si consiglia quindi di usare questa opzione in una macchina virtuale di Azure che si trova nella stessa area dell'account di archiviazione di origine.</span><span class="sxs-lookup"><span data-stu-id="69472-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="69472-191">File: scaricare</span><span class="sxs-lookup"><span data-stu-id="69472-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="69472-192">Scaricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="69472-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="69472-193">Se l'origine specificata è una condivisione file di Azure, è necessario specificare il nome file esatto, *ad esempio* `abc.txt`, per copiare un solo file oppure specificare l'opzione `--recursive` per copiare tutti i file nella condivisione in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="69472-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="69472-194">Se si specificano sia il criterio del file che l'opzione `--recursive` contemporaneamente, verrà generato un errore.</span><span class="sxs-lookup"><span data-stu-id="69472-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="69472-195">Scaricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="69472-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="69472-196">Le cartelle vuote non vengono scaricate.</span><span class="sxs-lookup"><span data-stu-id="69472-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="69472-197">File: caricare</span><span class="sxs-lookup"><span data-stu-id="69472-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="69472-198">Caricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="69472-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="69472-199">Caricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="69472-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="69472-200">Le cartelle vuote non vengono caricate.</span><span class="sxs-lookup"><span data-stu-id="69472-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="69472-201">Caricare i file corrispondenti ai criteri specificati</span><span class="sxs-lookup"><span data-stu-id="69472-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="69472-202">File: copia</span><span class="sxs-lookup"><span data-stu-id="69472-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="69472-203">Copiare tra condivisioni file</span><span class="sxs-lookup"><span data-stu-id="69472-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="69472-204">Quando si copia un file tra condivisioni file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="69472-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="69472-205">Copiare dalla condivisione file al BLOB</span><span class="sxs-lookup"><span data-stu-id="69472-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="69472-206">Quando si copia un file dalla condivisione file al BLOB, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="69472-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="69472-207">Copy dal BLOB alla condivisione file</span><span class="sxs-lookup"><span data-stu-id="69472-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="69472-208">Quando si copia un file dal BLOB alla condivisione file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="69472-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="69472-209">Copiare file in modo sincrono</span><span class="sxs-lookup"><span data-stu-id="69472-209">Synchronously copy files</span></span>
<span data-ttu-id="69472-210">È possibile specificare l'opzione `--sync-copy` per copiare i dati da archiviazione file ad archiviazione file, da archiviazione file ad archiviazione BLOB e da archiviazione BLOB ad archiviazione file in modo sincrono.</span><span class="sxs-lookup"><span data-stu-id="69472-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="69472-211">AzCopy esegue questa operazione scaricando i dati di origine nella memoria locale e caricandoli di nuovo nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="69472-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="69472-212">In questo caso, vengono applicati i costi in uscita standard.</span><span class="sxs-lookup"><span data-stu-id="69472-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="69472-213">Durante la copia da Archiviazione file ad Archiviazione BLOB, il tipo di BLOB predefinito è il BLOB in blocchi. Per modificare il tipo di BLOB di destinazione, è possibile specificare l'opzione `/BlobType:page`.</span><span class="sxs-lookup"><span data-stu-id="69472-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="69472-214">`--sync-copy` può generare costi aggiuntivi in uscita rispetto alla copia asincrona.</span><span class="sxs-lookup"><span data-stu-id="69472-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="69472-215">Per evitare costi in uscita, si consiglia quindi di usare questa opzione in una macchina virtuale di Azure che si trova nella stessa area dell'account di archiviazione di origine.</span><span class="sxs-lookup"><span data-stu-id="69472-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="69472-216">Altre funzionalità di AzCopy</span><span class="sxs-lookup"><span data-stu-id="69472-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="69472-217">Copiare solo i dati che non esistono nella destinazione</span><span class="sxs-lookup"><span data-stu-id="69472-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="69472-218">I parametri `--exclude-older` e `--exclude-newer` consentono di escludere dalla copia, rispettivamente, le risorse di origine precedenti o più recenti.</span><span class="sxs-lookup"><span data-stu-id="69472-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="69472-219">Per copiare solo e risorse di origine che non esistono nella destinazione, è possibile specificare entrambi i parametri nel comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="69472-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="69472-220">Usare un file di configurazione per specificare i parametri della riga di comando</span><span class="sxs-lookup"><span data-stu-id="69472-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="69472-221">È possibile includere i parametri della riga di comando di AzCopy in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="69472-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="69472-222">AzCopy elabora i parametri nel file come se fossero stati specificati nella riga di comando, eseguendo una sostituzione diretta con i contenuti del file.</span><span class="sxs-lookup"><span data-stu-id="69472-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="69472-223">Si supponga che sia presente un file di configurazione denominato `copyoperation`, che contiene le righe seguenti.</span><span class="sxs-lookup"><span data-stu-id="69472-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="69472-224">Ogni parametro di AzCopy può essere specificato su una singola riga</span><span class="sxs-lookup"><span data-stu-id="69472-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="69472-225">o su righe separate:</span><span class="sxs-lookup"><span data-stu-id="69472-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="69472-226">Se il parametro viene suddiviso su due righe, l'operazione di AzCopy ha esito negativo, come mostrato di seguito per il parametro `--source-key`:</span><span class="sxs-lookup"><span data-stu-id="69472-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="69472-227">Specificare una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="69472-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="69472-228">È anche possibile specificare una firma di accesso condiviso per il contenitore URI:</span><span class="sxs-lookup"><span data-stu-id="69472-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="69472-229">AzCopy attualmente supporta solo la [firma di accesso condiviso dell'account](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="69472-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="69472-230">Cartella del file journal</span><span class="sxs-lookup"><span data-stu-id="69472-230">Journal file folder</span></span>
<span data-ttu-id="69472-231">Ogni volta che si invia un comando ad AzCopy, l'utilità verifica se il file journal è presente nella cartella predefinita o in una cartella specificata dall'utente tramite questa opzione.</span><span class="sxs-lookup"><span data-stu-id="69472-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="69472-232">Se il file journal non viene trovato in tali percorsi, AzCopy considera l'operazione come nuova e quindi crea un nuovo file journal.</span><span class="sxs-lookup"><span data-stu-id="69472-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="69472-233">Se il file journal esiste, AzCopy verifica se la riga di comando di input corrisponde alla riga di comando nel file journal.</span><span class="sxs-lookup"><span data-stu-id="69472-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="69472-234">Se le righe di comando corrispondono, AzCopy avvia la ripresa dell'operazione incompleta.</span><span class="sxs-lookup"><span data-stu-id="69472-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="69472-235">Se non corrispondono, viene richiesto se si vuole sovrascrivere il file journal per avviare una nuova operazione o annullare l'operazione corrente.</span><span class="sxs-lookup"><span data-stu-id="69472-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="69472-236">Se si vuole usare il percorso predefinito per il file journal:</span><span class="sxs-lookup"><span data-stu-id="69472-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="69472-237">Se si omette l'opzione`--resume` o si specifica l'opzione `--resume` senza il percorso della cartella, come illustrato sopra, AzCopy creerà il file journal nel percorso predefinito, ovvero `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="69472-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="69472-238">Se il file journal esiste già, AzCopy riprenderà l'operazione in base al file journal.</span><span class="sxs-lookup"><span data-stu-id="69472-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="69472-239">Se si vuole specificare un percorso personalizzato per il file journal:</span><span class="sxs-lookup"><span data-stu-id="69472-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="69472-240">In questo esempio viene creato il file journal, nel caso in cui non esista già:</span><span class="sxs-lookup"><span data-stu-id="69472-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="69472-241">Se esiste, AzCopy riprenderà l'operazione in base al file journal.</span><span class="sxs-lookup"><span data-stu-id="69472-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="69472-242">Se si vuole riprendere un'operazione di AzCopy, ripetere lo stesso comando.</span><span class="sxs-lookup"><span data-stu-id="69472-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="69472-243">AzCopy in Linux richiederà la conferma:</span><span class="sxs-lookup"><span data-stu-id="69472-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="69472-244">Output di log dettagliati</span><span class="sxs-lookup"><span data-stu-id="69472-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="69472-245">Specificare il numero di operazioni simultanee da avviare</span><span class="sxs-lookup"><span data-stu-id="69472-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="69472-246">L'opzione `--parallel-level` specifica il numero di operazioni di copia simultanee.</span><span class="sxs-lookup"><span data-stu-id="69472-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="69472-247">Per impostazione predefinita, AzCopy avvia un determinato numero di operazioni simultanee per aumentare la velocità effettiva di trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="69472-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="69472-248">Il numero di operazioni simultanee è uguale a 8 volte il numero di processori disponibili.</span><span class="sxs-lookup"><span data-stu-id="69472-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="69472-249">Se AzCopy è in esecuzione in una rete con larghezza di banda ridotta, è possibile specificare un numero inferiore per --parallel-level in modo da evitare errori generati dalla competizione tra le risorse.</span><span class="sxs-lookup"><span data-stu-id="69472-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="69472-250">Per visualizzare l'elenco completo dei parametri di AzCopy, vedere il menu 'azcopy - help'.</span><span class="sxs-lookup"><span data-stu-id="69472-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="69472-251">Problemi noti e procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="69472-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="69472-252">Errore: impossibile trovare .NET Core nel sistema.</span><span class="sxs-lookup"><span data-stu-id="69472-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="69472-253">Se viene visualizzato un errore che indica che .NET Core non è installato nel sistema, è possibile che manchi il percorso per il file binario di .NET Core `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="69472-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="69472-254">Per risolvere il problema, trovare il file binario di .NET Core nel sistema:</span><span class="sxs-lookup"><span data-stu-id="69472-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="69472-255">Viene restituito il percorso del file binario dotnet.</span><span class="sxs-lookup"><span data-stu-id="69472-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="69472-256">Aggiungere questo percorso alla variabile PATH.</span><span class="sxs-lookup"><span data-stu-id="69472-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="69472-257">Per sudo, modificare secure_path in modo da includere il percorso del file binario dotnet:</span><span class="sxs-lookup"><span data-stu-id="69472-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="69472-258">In questo esempio, la variabile secure_path è:</span><span class="sxs-lookup"><span data-stu-id="69472-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="69472-259">Per l'utente corrente, modificare .bash_profile/.profile in modo da includere il percorso del file binario dotnet nella variabile PATH</span><span class="sxs-lookup"><span data-stu-id="69472-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="69472-260">Verificare che .NET Core sia ora presente in PATH:</span><span class="sxs-lookup"><span data-stu-id="69472-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="69472-261">Errore durante l'installazione di AzCopy</span><span class="sxs-lookup"><span data-stu-id="69472-261">Error Installing AzCopy</span></span>
<span data-ttu-id="69472-262">Se si verificano problemi con l'installazione di AzCopy, si può provare a eseguire AzCopy usando lo script bash nella cartella `azcopy` estratta.</span><span class="sxs-lookup"><span data-stu-id="69472-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="69472-263">Limitare le scritture simultanee durante la copia dei dati</span><span class="sxs-lookup"><span data-stu-id="69472-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="69472-264">Durante la copia di BLOB o file con AzCopy, tenere presente che altre applicazioni potrebbero modificare i dati mentre è in corso la copia.</span><span class="sxs-lookup"><span data-stu-id="69472-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="69472-265">Se possibile, assicurarsi che i dati copiati non vengano modificati durante l'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="69472-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="69472-266">Ad esempio, se si copia un file VHD associato a una macchina virtuale di Azure, verificare che altre applicazioni non stiano scrivendo nel file VHD durante la copia.</span><span class="sxs-lookup"><span data-stu-id="69472-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="69472-267">Un buon metodo per eseguire questa operazione è tramite leasing della risorsa da copiare.</span><span class="sxs-lookup"><span data-stu-id="69472-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="69472-268">In alternativa, è prima possibile creare uno snapshot del file VHD e quindi copiare lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="69472-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="69472-269">Se non è possibile evitare che altre applicazioni scrivano nei BLOB o nei file durante l'operazione di copia, tenere presente che al termine del processo la parità delle risorse copiate con le risorse di origine potrebbe non essere completa.</span><span class="sxs-lookup"><span data-stu-id="69472-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="69472-270">Eseguire un'istanza di AzCopy su un computer.</span><span class="sxs-lookup"><span data-stu-id="69472-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="69472-271">AzCopy è progettato per massimizzare l'utilizzo della risorsa del computer per accelerare il trasferimento dei dati, è consigliabile eseguire solo un'istanza di AzCopy in un computer e specificare l'opzione `--parallel-level` se sono necessarie più operazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="69472-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="69472-272">Per ulteriori dettagli, digitare `AzCopy --help parallel-level` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="69472-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69472-273">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69472-273">Next steps</span></span>
<span data-ttu-id="69472-274">Per altre informazioni su Archiviazione di Azure e AzCopy, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="69472-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="69472-275">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="69472-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="69472-276">Introduzione ad Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="69472-276">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="69472-277">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="69472-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="69472-278">Gestire BLOB con Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="69472-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="69472-279">Uso dell'interfaccia della riga di comando di Azure 2.0 con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="69472-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="69472-280">Come usare l'archiviazione BLOB da C++</span><span class="sxs-lookup"><span data-stu-id="69472-280">How to use Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="69472-281">Come usare l'archiviazione BLOB da Java</span><span class="sxs-lookup"><span data-stu-id="69472-281">How to use Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="69472-282">Come usare l'archiviazione BLOB da Node.js</span><span class="sxs-lookup"><span data-stu-id="69472-282">How to use Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="69472-283">Come usare l'archiviazione BLOB da Python</span><span class="sxs-lookup"><span data-stu-id="69472-283">How to use Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="69472-284">Post del blog di Archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="69472-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="69472-285">Annuncio della versione di anteprima di AzCopy in Linux</span><span class="sxs-lookup"><span data-stu-id="69472-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="69472-286">Introduzione alla versione di anteprima della libreria per lo spostamento dei dati di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="69472-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="69472-287">AzCopy: introduzione alla copia sincrona e al tipo di contenuto personalizzato</span><span class="sxs-lookup"><span data-stu-id="69472-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="69472-288">AzCopy: annuncio della disponibilità per tutti di AzCopy 3.0 oltre alla versione di anteprima di AzCopy 4.0 con il supporto di tabelle e file</span><span class="sxs-lookup"><span data-stu-id="69472-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="69472-289">AzCopy: ottimizzazione per gli scenari di copia su larga scala</span><span class="sxs-lookup"><span data-stu-id="69472-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="69472-290">AzCopy:supporto per l'archiviazione con ridondanza geografica e accesso in lettura</span><span class="sxs-lookup"><span data-stu-id="69472-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="69472-291">AzCopy:trasferimento di dati con modalità riavviabile e token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="69472-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="69472-292">AzCopy: uso del comando di copia dei BLOB tra account</span><span class="sxs-lookup"><span data-stu-id="69472-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="69472-293">AzCopy: Caricamento e download di file per BLOB di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="69472-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

