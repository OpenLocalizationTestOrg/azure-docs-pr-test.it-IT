---
title: aaaCopy o lo spostamento dati tooAzure archiviazione con AzCopy in Linux | Documenti Microsoft
description: "Usare AzCopy hello in Linux utilità toomove o copia dati tooor dal contenuto di blob e file. Copiare i dati tooAzure archiviazione da file locali, o copiare dati in o tra gli account di archiviazione. Migrare facilmente l'archiviazione di tooAzure di dati."
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
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="24871-105">Trasferire dati con AzCopy in Linux</span><span class="sxs-lookup"><span data-stu-id="24871-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="24871-106">AzCopy in Linux è un'utilità della riga di comando progettata per la copia di dati tooand dall'archiviazione Blob di Microsoft Azure e i File utilizzando i comandi semplici con prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="24871-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="24871-107">È possibile copiare dati da un oggetto tooanother all'interno dell'account di archiviazione o tra gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="24871-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="24871-108">Esistono due versioni di AzCopy che è possibile scaricare.</span><span class="sxs-lookup"><span data-stu-id="24871-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="24871-109">AzCopy in Linux viene compilato con .NET Core Framework per le piattaforme Linux e offre opzioni della riga di comando in stile POSIX.</span><span class="sxs-lookup"><span data-stu-id="24871-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="24871-110">[AzCopy in Windows](../storage-use-azcopy.md) viene compilato con .NET Framework e offre opzioni della riga di comando in stile Windows.</span><span class="sxs-lookup"><span data-stu-id="24871-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="24871-111">Questo articolo descrive AzCopy in Linux.</span><span class="sxs-lookup"><span data-stu-id="24871-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="24871-112">Scaricare e installare AzCopy</span><span class="sxs-lookup"><span data-stu-id="24871-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="24871-113">Installazione in Linux</span><span class="sxs-lookup"><span data-stu-id="24871-113">Installation on Linux</span></span>

<span data-ttu-id="24871-114">AzCopy in Linux richiede il framework .NET Core su piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="24871-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="24871-115">Vedere le istruzioni di installazione di hello sulla hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) pagina.</span><span class="sxs-lookup"><span data-stu-id="24871-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="24871-116">Ecco un esempio di installazione di .NET Core in Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="24871-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="24871-117">Hello più recente della Guida all'installazione, visitare [.NET Core su Linux](https://www.microsoft.com/net/core#linuxubuntu) pagina di installazione.</span><span class="sxs-lookup"><span data-stu-id="24871-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="24871-118">Dopo aver installato .NET Core, scaricare e installare AzCopy.</span><span class="sxs-lookup"><span data-stu-id="24871-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="24871-119">Dopo aver installato AzCopy in Linux, è possibile rimuovere file hello estratto.</span><span class="sxs-lookup"><span data-stu-id="24871-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="24871-120">In alternativa se non si dispone di privilegi avanzati, è possibile anche eseguire tramite script della shell hello AzCopy 'azcopy' nella cartella di estrazione hello.</span><span class="sxs-lookup"><span data-stu-id="24871-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="24871-121">Installazione alternativa in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="24871-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="24871-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="24871-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="24871-123">Aggiungere un'origine apt per .Net Core:</span><span class="sxs-lookup"><span data-stu-id="24871-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="24871-124">Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:</span><span class="sxs-lookup"><span data-stu-id="24871-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="24871-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="24871-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="24871-126">Aggiungere un'origine apt per .Net Core:</span><span class="sxs-lookup"><span data-stu-id="24871-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="24871-127">Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:</span><span class="sxs-lookup"><span data-stu-id="24871-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="24871-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="24871-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="24871-129">Aggiungere un'origine apt per .Net Core:</span><span class="sxs-lookup"><span data-stu-id="24871-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="24871-130">Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:</span><span class="sxs-lookup"><span data-stu-id="24871-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="24871-131">Scrittura del primo comando AzCopy </span><span class="sxs-lookup"><span data-stu-id="24871-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="24871-132">sintassi di base per i comandi AzCopy Hello è:</span><span class="sxs-lookup"><span data-stu-id="24871-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="24871-133">Hello seguenti esempi illustrano vari scenari per la copia dei dati tooand da file e i BLOB di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="24871-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="24871-134">Fare riferimento toohello `azcopy --help` menu per una spiegazione dettagliata dei parametri di hello utilizzata in ogni esempio.</span><span class="sxs-lookup"><span data-stu-id="24871-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="24871-135">BLOB: scaricare</span><span class="sxs-lookup"><span data-stu-id="24871-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="24871-136">Scaricare un singolo BLOB</span><span class="sxs-lookup"><span data-stu-id="24871-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="24871-137">Se la cartella hello `/mnt/myfiles` non esiste, AzCopy crea e ne scarica `abc.txt ` nella nuova cartella hello.</span><span class="sxs-lookup"><span data-stu-id="24871-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="24871-138">Scaricare un singolo BLOB da un'area secondaria</span><span class="sxs-lookup"><span data-stu-id="24871-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="24871-139">È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="24871-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="24871-140">Scaricare tutti BLOB</span><span class="sxs-lookup"><span data-stu-id="24871-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="24871-141">Si supponga che segue hello BLOB si trovano nel contenitore specificato hello:</span><span class="sxs-lookup"><span data-stu-id="24871-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="24871-142">Dopo un'operazione di download hello hello directory `/mnt/myfiles` include hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="24871-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="24871-143">Se non si specifica l'opzione `--recursive`, non verrà scaricato alcun BLOB.</span><span class="sxs-lookup"><span data-stu-id="24871-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="24871-144">Scaricare i BLOB con il prefisso specificato</span><span class="sxs-lookup"><span data-stu-id="24871-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="24871-145">Si supponga che segue hello BLOB si trovano nel contenitore specificato hello.</span><span class="sxs-lookup"><span data-stu-id="24871-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="24871-146">Tutti i blob che iniziano con il prefisso hello `a` vengono scaricati.</span><span class="sxs-lookup"><span data-stu-id="24871-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="24871-147">Dopo un'operazione di download hello hello cartella `/mnt/myfiles` include hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="24871-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="24871-148">prefisso Hello applica toohello directory virtuale, che costituisce hello prima parte del nome blob hello.</span><span class="sxs-lookup"><span data-stu-id="24871-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="24871-149">Nell'esempio hello illustrato in precedenza, la directory virtuale hello non corrisponde prefisso specificato hello, non viene scaricato alcun blob.</span><span class="sxs-lookup"><span data-stu-id="24871-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="24871-150">Inoltre, se hello opzione `--recursive` non viene specificato, AzCopy non scarica tutti i BLOB.</span><span class="sxs-lookup"><span data-stu-id="24871-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="24871-151">Impostare l'ora dell'ultima modifica hello dei file esportati toobe stesso hello BLOB di origine</span><span class="sxs-lookup"><span data-stu-id="24871-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="24871-152">È anche possibile escludere i BLOB da un'operazione di download hello in base all'ora ultima modifica.</span><span class="sxs-lookup"><span data-stu-id="24871-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="24871-153">Ad esempio, se si desidera tooexclude BLOB la cui ultima modifica è hello uguale o più file di destinazione hello recente, aggiungere hello `--exclude-newer` opzione:</span><span class="sxs-lookup"><span data-stu-id="24871-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="24871-154">O se si desidera tooexclude BLOB la cui ultima modifica è hello stesso o meno i file di destinazione hello, aggiungere hello `--exclude-older` opzione:</span><span class="sxs-lookup"><span data-stu-id="24871-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="24871-155">BLOB: caricare</span><span class="sxs-lookup"><span data-stu-id="24871-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="24871-156">Caricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="24871-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="24871-157">Se il contenitore di destinazione specificato hello non esiste, AzCopy crea e ne caricamenti hello file al suo interno.</span><span class="sxs-lookup"><span data-stu-id="24871-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="24871-158">Caricare file singoli toovirtual directory</span><span class="sxs-lookup"><span data-stu-id="24871-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="24871-159">Se hello specificato una directory virtuale non esiste, AzCopy carica hello file tooinclude hello directory virtuale nel nome di blob hello (*ad esempio*, `vd/abc.txt` nell'esempio hello sopra).</span><span class="sxs-lookup"><span data-stu-id="24871-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="24871-160">Caricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="24871-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="24871-161">Specifica l'opzione `--recursive` contenuto hello caricamenti di hello specificato directory tooBlob archiviazione in modo ricorsivo, vale a dire che tutte le sottocartelle e i file vengono caricati anche.</span><span class="sxs-lookup"><span data-stu-id="24871-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="24871-162">Ad esempio, si supponga che segue hello file si trovano nella cartella `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="24871-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="24871-163">Dopo un'operazione di caricamento hello contenitore hello include hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="24871-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="24871-164">Hello quando l'opzione `--recursive` non viene specificato, solo hello tre vengono caricati file seguenti:</span><span class="sxs-lookup"><span data-stu-id="24871-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="24871-165">Caricare i file corrispondenti ai criteri specificati</span><span class="sxs-lookup"><span data-stu-id="24871-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="24871-166">Si supponga che segue hello file si trovano nella cartella `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="24871-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="24871-167">Dopo un'operazione di caricamento hello contenitore hello include hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="24871-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="24871-168">Hello quando l'opzione `--recursive` non viene specificato, AzCopy Ignora file presenti nella sottodirectory:</span><span class="sxs-lookup"><span data-stu-id="24871-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="24871-169">Specificare hello tipo di contenuto MIME di un blob di destinazione</span><span class="sxs-lookup"><span data-stu-id="24871-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="24871-170">Per impostazione predefinita, AzCopy Imposta tipo di contenuto di un blob di destinazione hello troppo`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="24871-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="24871-171">Tuttavia, è possibile specificare in modo esplicito tipo di contenuto tramite l'opzione hello hello `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="24871-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="24871-172">Questa sintassi Imposta tipo di contenuto hello per tutti i BLOB in un'operazione di caricamento.</span><span class="sxs-lookup"><span data-stu-id="24871-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="24871-173">Se hello opzione `--set-content-type` viene specificata senza un valore, quindi AzCopy imposta ogni blob o il file del tipo di contenuto in base tooits estensione di file.</span><span class="sxs-lookup"><span data-stu-id="24871-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="24871-174">BLOB: copiare</span><span class="sxs-lookup"><span data-stu-id="24871-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="24871-175">Copiare un BLOB all'interno di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="24871-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="24871-176">Quando si copia un BLOB senza l'opzione --sync-copy, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="24871-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="24871-177">Copiare un singolo BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="24871-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="24871-178">Quando si copia un BLOB senza l'opzione --sync-copy, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="24871-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="24871-179">Copiare blob singolo dall'area tooprimary area secondaria</span><span class="sxs-lookup"><span data-stu-id="24871-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="24871-180">È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="24871-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="24871-181">Copiare un singolo BLOB e i relativi snapshot tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="24871-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="24871-182">Dopo un'operazione di copia hello contenitore di destinazione hello include blob hello e i relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="24871-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="24871-183">contenitore Hello include hello segue blob e i relativi snapshot:</span><span class="sxs-lookup"><span data-stu-id="24871-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="24871-184">Copiare in modo sincrono i BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="24871-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="24871-185">Per impostazione predefinita, AzCopy copia i dati tra due endpoint di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="24871-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="24871-186">Pertanto, hello copia operazione viene eseguita in background hello usando la capacità della larghezza di banda di riserva che non dispone di alcun contratto di servizio in termini di velocità con cui un blob viene copiato.</span><span class="sxs-lookup"><span data-stu-id="24871-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="24871-187">Hello `--sync-copy` opzione assicura che l'operazione di copia hello Ottiene velocità coerente.</span><span class="sxs-lookup"><span data-stu-id="24871-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="24871-188">AzCopy esegue copia sincrono hello scaricando BLOB hello toocopy da hello specificato memoria toolocal di origine e quindi caricarli toohello destinazione di archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="24871-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="24871-189">`--sync-copy`potrebbe generare uscita ulteriori costi rispetto tooasynchronous copia.</span><span class="sxs-lookup"><span data-stu-id="24871-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="24871-190">Hello approccio consigliato è toouse questa opzione in una macchina virtuale di Azure, che è in hello stessa area del costo di uscita origine tooavoid account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="24871-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="24871-191">File: scaricare</span><span class="sxs-lookup"><span data-stu-id="24871-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="24871-192">Scaricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="24871-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="24871-193">Se è specificato l'origine è una condivisione di file di Azure, quindi è necessario specificare il nome di file esatto hello, hello (*ad esempio* `abc.txt`) toodownload un singolo file, oppure specificare l'opzione `--recursive` toodownload tutti i file nella condivisione di hello in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="24871-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="24871-194">Il tentativo di toospecify un modello di file e l'opzione `--recursive` contemporaneamente provoca un errore.</span><span class="sxs-lookup"><span data-stu-id="24871-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="24871-195">Scaricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="24871-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="24871-196">Le cartelle vuote non vengono scaricate.</span><span class="sxs-lookup"><span data-stu-id="24871-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="24871-197">File: caricare</span><span class="sxs-lookup"><span data-stu-id="24871-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="24871-198">Caricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="24871-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="24871-199">Caricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="24871-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="24871-200">Le cartelle vuote non vengono caricate.</span><span class="sxs-lookup"><span data-stu-id="24871-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="24871-201">Caricare i file corrispondenti ai criteri specificati</span><span class="sxs-lookup"><span data-stu-id="24871-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="24871-202">File: copia</span><span class="sxs-lookup"><span data-stu-id="24871-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="24871-203">Copiare tra condivisioni file</span><span class="sxs-lookup"><span data-stu-id="24871-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="24871-204">Quando si copia un file tra condivisioni file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="24871-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="24871-205">Copiare da tooblob condivisione file</span><span class="sxs-lookup"><span data-stu-id="24871-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="24871-206">Quando si copia un file da tooblob di condivisione file, un [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) viene eseguita l'operazione.</span><span class="sxs-lookup"><span data-stu-id="24871-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="24871-207">Copiare da blob toofile condivisione</span><span class="sxs-lookup"><span data-stu-id="24871-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="24871-208">Quando si copia un file dalla condivisione toofile blob, un [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) viene eseguita l'operazione.</span><span class="sxs-lookup"><span data-stu-id="24871-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="24871-209">Copiare file in modo sincrono</span><span class="sxs-lookup"><span data-stu-id="24871-209">Synchronously copy files</span></span>
<span data-ttu-id="24871-210">È possibile specificare hello `--sync-copy` opzione toocopy dati da archiviazione di File tooFile archiviazione da archiviazione di File tooBlob, archiviazione e, dall'archiviazione Blob tooFile archiviazione in modo sincrono.</span><span class="sxs-lookup"><span data-stu-id="24871-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="24871-211">AzCopy viene eseguita questa operazione per il download di memoria di toolocal hello origine dati e quindi caricarli toodestination.</span><span class="sxs-lookup"><span data-stu-id="24871-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="24871-212">In questo caso, vengono applicati i costi in uscita standard.</span><span class="sxs-lookup"><span data-stu-id="24871-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="24871-213">Durante la copia da archiviazione di File tooBlob archiviazione, è di tipo di blob predefinito hello blob in blocchi, l'utente può specificare l'opzione `/BlobType:page` toochange hello tipo di blob di destinazione.</span><span class="sxs-lookup"><span data-stu-id="24871-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="24871-214">Si noti che `--sync-copy` potrebbe generare uscita ulteriore costi Copia tooasynchronous il confronto.</span><span class="sxs-lookup"><span data-stu-id="24871-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="24871-215">Hello approccio consigliato è toouse questa opzione in una macchina virtuale di Azure, che è in hello stessa area del costo di uscita origine tooavoid account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="24871-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="24871-216">Altre funzionalità di AzCopy</span><span class="sxs-lookup"><span data-stu-id="24871-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="24871-217">Copia solo i dati che non esistono nella destinazione hello</span><span class="sxs-lookup"><span data-stu-id="24871-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="24871-218">Hello `--exclude-older` e `--exclude-newer` parametri consentono tooexclude le risorse dell'origine o meno recente viene copiato, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="24871-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="24871-219">Se si desidera solo le risorse dell'origine toocopy che non sono presenti nella destinazione hello, è possibile specificare entrambi i parametri nel comando AzCopy hello:</span><span class="sxs-lookup"><span data-stu-id="24871-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="24871-220">Utilizzare i parametri della riga di comando toospecify file configurazione</span><span class="sxs-lookup"><span data-stu-id="24871-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="24871-221">È possibile includere i parametri della riga di comando di AzCopy in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="24871-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="24871-222">I processi di AzCopy hello parametri nel file hello come se fossero stati specificati nella riga di comando hello, eseguire una sostituzione diretta con contenuto hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="24871-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="24871-223">Si supponga che un file di configurazione denominato `copyoperation`, che contiene hello seguenti righe.</span><span class="sxs-lookup"><span data-stu-id="24871-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="24871-224">Ogni parametro di AzCopy può essere specificato su una singola riga</span><span class="sxs-lookup"><span data-stu-id="24871-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="24871-225">o su righe separate:</span><span class="sxs-lookup"><span data-stu-id="24871-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="24871-226">AzCopy ha esito negativo se il parametro hello si divide in due righe, come illustrato di seguito per hello `--source-key` parametro:</span><span class="sxs-lookup"><span data-stu-id="24871-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="24871-227">Specificare una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="24871-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="24871-228">È inoltre possibile specificare una firma di accesso condiviso nel contenitore hello URI:</span><span class="sxs-lookup"><span data-stu-id="24871-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="24871-229">Si noti che AzCopy supporta attualmente solo hello [SAS Account](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="24871-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="24871-230">Cartella del file journal</span><span class="sxs-lookup"><span data-stu-id="24871-230">Journal file folder</span></span>
<span data-ttu-id="24871-231">Ogni volta che si esegue un comando tooAzCopy, controlla se è presente un file journal nella cartella predefinita hello o se esiste in una cartella specificata tramite questa opzione.</span><span class="sxs-lookup"><span data-stu-id="24871-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="24871-232">Se non esiste alcun file journal hello in entrambe le posizioni, AzCopy considera nuova operazione hello e genera un nuovo file journal.</span><span class="sxs-lookup"><span data-stu-id="24871-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="24871-233">Se esistono file journal hello, AzCopy controlla se hello riga di comando che l'input corrisponde hello riga di comando nel file journal hello.</span><span class="sxs-lookup"><span data-stu-id="24871-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="24871-234">Se due righe di comando hello corrispondono, AzCopy riprende hello incompleti.</span><span class="sxs-lookup"><span data-stu-id="24871-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="24871-235">Se non corrispondono, AzCopy richiede all'utente tooeither sovrascrittura hello journal file toostart una nuova operazione o l'operazione corrente di toocancel hello.</span><span class="sxs-lookup"><span data-stu-id="24871-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="24871-236">Se si desidera toouse hello percorso predefinito file journal hello:</span><span class="sxs-lookup"><span data-stu-id="24871-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="24871-237">Se si omette l'opzione `--resume`, oppure specificare l'opzione `--resume` senza percorso della cartella hello, come illustrato in precedenza, AzCopy crea file journal hello nel percorso predefinito di hello, ovvero `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="24871-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="24871-238">Se il file journal di hello esiste già, quindi AzCopy riprende l'operazione di hello basato su file journal hello.</span><span class="sxs-lookup"><span data-stu-id="24871-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="24871-239">Se si desidera toospecify un percorso personalizzato per il file journal hello:</span><span class="sxs-lookup"><span data-stu-id="24871-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="24871-240">Questo esempio crea file journal hello se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="24871-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="24871-241">Se esiste, quindi AzCopy riprende l'operazione di hello basato su file journal hello.</span><span class="sxs-lookup"><span data-stu-id="24871-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="24871-242">Se si desidera tooresume un'operazione AzCopy, ripetere hello stesso comando.</span><span class="sxs-lookup"><span data-stu-id="24871-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="24871-243">AzCopy in Linux richiederà la conferma:</span><span class="sxs-lookup"><span data-stu-id="24871-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="24871-244">Output di log dettagliati</span><span class="sxs-lookup"><span data-stu-id="24871-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="24871-245">Specificare il numero di hello di operazioni simultanee toostart</span><span class="sxs-lookup"><span data-stu-id="24871-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="24871-246">Opzione `--parallel-level` specifica hello numero di operazioni di copia simultanea.</span><span class="sxs-lookup"><span data-stu-id="24871-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="24871-247">Per impostazione predefinita, AzCopy inizia un certo numero di velocità effettiva di trasferimento dei dati di operazioni simultanee tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="24871-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="24871-248">numero di Hello di operazioni simultanee è uguale otto volte hello numero di processori disponibili.</span><span class="sxs-lookup"><span data-stu-id="24871-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="24871-249">Se si esegue AzCopy attraverso una rete con larghezza di banda ridotta, è possibile specificare un numero inferiore per - parallelo livello tooavoid errore di concorrenza di risorse.</span><span class="sxs-lookup"><span data-stu-id="24871-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="24871-250">elenco completo di hello tooview dei parametri di AzCopy, estrarre "azcopy - help" dal menu.</span><span class="sxs-lookup"><span data-stu-id="24871-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="24871-251">Problemi noti e procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="24871-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="24871-252">Errore: .NET Core non è stato trovato nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="24871-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="24871-253">Se si verifica un errore che informa che .NET Core non è installato nel sistema hello, hello binario di .NET Core toohello percorso `dotnet` potrebbe essere mancante.</span><span class="sxs-lookup"><span data-stu-id="24871-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="24871-254">In ordine tooaddress questo problema, trovare il file binario di .NET Core hello nel sistema hello:</span><span class="sxs-lookup"><span data-stu-id="24871-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="24871-255">Vengono restituite hello percorso toohello dotnet binario.</span><span class="sxs-lookup"><span data-stu-id="24871-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="24871-256">Aggiungere quindi questa variabile di percorso toohello percorso.</span><span class="sxs-lookup"><span data-stu-id="24871-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="24871-257">Per sudo, modifica secure_path toocontain hello percorso toohello dotnet binario:</span><span class="sxs-lookup"><span data-stu-id="24871-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="24871-258">In questo esempio, la variabile secure_path è:</span><span class="sxs-lookup"><span data-stu-id="24871-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="24871-259">Per l'utente corrente di hello, modificare.bash_profile/.profile tooinclude hello percorso toohello dotnet binario nella variabile PATH</span><span class="sxs-lookup"><span data-stu-id="24871-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="24871-260">Verificare che .NET Core sia ora presente in PATH:</span><span class="sxs-lookup"><span data-stu-id="24871-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="24871-261">Errore durante l'installazione di AzCopy</span><span class="sxs-lookup"><span data-stu-id="24871-261">Error Installing AzCopy</span></span>
<span data-ttu-id="24871-262">Se si verificano problemi con l'installazione di AzCopy, è possibile provare toorun AzCopy utilizzando script bash hello in hello estratti `azcopy` cartella.</span><span class="sxs-lookup"><span data-stu-id="24871-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="24871-263">Limitare le scritture simultanee durante la copia dei dati</span><span class="sxs-lookup"><span data-stu-id="24871-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="24871-264">Quando si copiano BLOB o i file con AzCopy, tenere presente che un'altra applicazione può modificare dati hello mentre si copiano.</span><span class="sxs-lookup"><span data-stu-id="24871-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="24871-265">Se possibile, verificare che i dati di hello che si copia non viene modificati durante l'operazione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="24871-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="24871-266">Ad esempio, quando si copia un disco rigido virtuale associato a una macchina virtuale di Azure, assicurarsi che altre applicazioni non sono attualmente scrivendo toohello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="24871-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="24871-267">Toodo un modo efficace questa caratteristica è leasing hello risorsa toobe copiati.</span><span class="sxs-lookup"><span data-stu-id="24871-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="24871-268">In alternativa, è possibile creare uno snapshot del disco rigido virtuale hello prima e quindi copiare hello snapshot.</span><span class="sxs-lookup"><span data-stu-id="24871-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="24871-269">Se non è possibile impedire o la scrittura tooblobs file mentre vengono copiate, quindi tenere presente che, dal processo di hello hello tempo al termine di altre applicazioni, hello copiate risorse possono non avere completa parità con le risorse dell'origine hello.</span><span class="sxs-lookup"><span data-stu-id="24871-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="24871-270">Eseguire un'istanza di AzCopy su un computer.</span><span class="sxs-lookup"><span data-stu-id="24871-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="24871-271">AzCopy è progettato toomaximize hello utilizzo del computer risorse tooaccelerate hello di trasferimento dei dati, è consigliabile eseguire solo un'istanza di AzCopy in un computer e specificare l'opzione hello `--parallel-level` se è necessario simultanea di più operazioni.</span><span class="sxs-lookup"><span data-stu-id="24871-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="24871-272">Per ulteriori informazioni, digitare `AzCopy --help parallel-level` nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="24871-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24871-273">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="24871-273">Next steps</span></span>
<span data-ttu-id="24871-274">Per ulteriori informazioni sull'archiviazione di Azure e AzCopy, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="24871-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="24871-275">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="24871-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="24871-276">Introduzione tooAzure archiviazione</span><span class="sxs-lookup"><span data-stu-id="24871-276">Introduction tooAzure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="24871-277">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="24871-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="24871-278">Gestire BLOB con Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="24871-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="24871-279">Utilizzo di hello Azure CLI 2.0 con archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="24871-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="24871-280">Come toouse archiviazione Blob da C++</span><span class="sxs-lookup"><span data-stu-id="24871-280">How toouse Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="24871-281">Come toouse archiviazione Blob da Java</span><span class="sxs-lookup"><span data-stu-id="24871-281">How toouse Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="24871-282">Come toouse archiviazione Blob da Node.js</span><span class="sxs-lookup"><span data-stu-id="24871-282">How toouse Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="24871-283">Come toouse archiviazione Blob da Python</span><span class="sxs-lookup"><span data-stu-id="24871-283">How toouse Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="24871-284">Post del blog di Archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="24871-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="24871-285">Annuncio della versione di anteprima di AzCopy in Linux</span><span class="sxs-lookup"><span data-stu-id="24871-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="24871-286">Introduzione alla versione di anteprima della libreria per lo spostamento dei dati di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="24871-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="24871-287">AzCopy: introduzione alla copia sincrona e al tipo di contenuto personalizzato</span><span class="sxs-lookup"><span data-stu-id="24871-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="24871-288">AzCopy: annuncio della disponibilità per tutti di AzCopy 3.0 oltre alla versione di anteprima di AzCopy 4.0 con il supporto di tabelle e file</span><span class="sxs-lookup"><span data-stu-id="24871-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="24871-289">AzCopy: ottimizzazione per gli scenari di copia su larga scala</span><span class="sxs-lookup"><span data-stu-id="24871-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="24871-290">AzCopy:supporto per l'archiviazione con ridondanza geografica e accesso in lettura</span><span class="sxs-lookup"><span data-stu-id="24871-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="24871-291">AzCopy:trasferimento di dati con modalità riavviabile e token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="24871-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="24871-292">AzCopy: uso del comando di copia dei BLOB tra account</span><span class="sxs-lookup"><span data-stu-id="24871-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="24871-293">AzCopy: Caricamento e download di file per BLOB di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="24871-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

